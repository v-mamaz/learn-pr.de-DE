Angenommen, Ihr Unternehmen möchte feststellen, ob Azure Load Balancer Ihre ERP-Anwendung (Enterprise Resource Planning) unterstützt. Die Anwendung verfügt über eine Weboberfläche für Benutzer und wird auf mehreren Servern ausgeführt. Jeder Server verfügt über eine lokale Kopie der ERP-Datenbank, die auf allen Servern synchronisiert ist.

Hier erfahren Sie, wie ein Lastenausgleich zur hohen Verfügbarkeit von Diensten beitragen kann. Sie lernen den Unterschied zwischen den Load Balancer-Optionen „Basic“ und „Standard“ kennen und erfahren, wie Sie einen Lastenausgleich für Azure Virtual Machines erstellen.

## <a name="what-is-load-balancing"></a>Was ist Lastenausgleich?

Unter _Lastenausgleich_ sind verschiedene Verfahren zur Verteilung von Workloads auf mehrere Compute-, Speicher- und Netzwerkgeräte zu verstehen. Ziel des Lastenausgleichs ist die Optimierung der Nutzung mehrerer Ressourcen, die effizienteste Nutzung dieser Ressourcen, wenn eine Infrastruktur horizontal hochskaliert wird, und die Sicherstellung der Aufrechterhaltung von Diensten bei Ausfall einzelner Komponenten.

Im Folgenden wird erläutert, wie Azure den Lastenausgleich für virtuelle Computer (VMs) unterstützt.

### <a name="what-is-high-availability"></a>Was ist Hochverfügbarkeit?

Als Hochverfügbarkeit gilt die Fähigkeit einer Anwendung oder eines Diensts, trotz eines Ausfalls einer Systemkomponente weiterhin den Zugriff zu ermöglichen. Im Idealfall wird keine Dienstunterbrechung spürbar.

Ein Lastenausgleich ist für die Ermöglichung von Hochverfügbarkeit unerlässlich, da mehrere VMs als ein Pool von Servern fungieren können. Der Pool kann weiterhin Dienstanforderungen entgegennehmen, auch wenn einige VMs abstürzen sollten oder zur Wartung offline geschaltet werden.

## <a name="what-is-the-azure-load-balancer"></a>Was ist der Azure Load Balancer?

Der **Azure Load Balancer** ist ein Azure-Dienst, der eingehende Anforderungen auf mehrere virtuelle Computer in einem Pool verteilt. Der Dienst verteilt eingehenden Netzwerkdatenverkehr auf eine Gruppe ordnungsgemäß funktionierender VMs und vermeidet VMs, die nicht reagieren können.

Der Azure Load Balancer arbeitet auf der 4. Schicht (TCP, UDP) des aus 7 Schichten bestehenden OSI-Modells. Der Dienst kann zur Unterstützung von TCP- und UDP-Anwendungsszenarien konfiguriert werden, bei denen der Datenverkehr in Azure-VMs eingeht. Er unterstützt auch Szenarien mit ausgehendem Datenverkehr, bei denen andere Azure-Dienste den TCP- und UDP-Datenverkehr über Azure-VMs an externe Endpunkte weiterleiten.

## <a name="public-vs-internal-load-balancers"></a>Vergleich zwischen öffentlichen und internen Lastenausgleichsmodulen

Ein Azure Load Balancer kann je nach Quelle der eingehenden Anforderungen _öffentlich_ oder _intern_ sein.

Ein **öffentlichen Load Balancer** verarbeitet Clientanforderungen, die von außerhalb Ihrer Azure-Infrastruktur stammen. Die öffentliche IP-Adresse wird automatisch als Front-End des Load Balancers konfiguriert, wenn Sie die öffentliche IP-Adresse und die Lastenausgleichsressource erstellen. Die folgende Abbildung zeigt einen öffentlichen Load Balancer.

![Die Abbildung zeigt einen öffentlichen Load Balancer, der Clientanforderungen aus dem Internet an drei VMs in einem virtuellen Netzwerk verteilt.](../media-draft/2-public-load-balancer.png)

Ein **interner Load Balancer** verarbeitet Anforderungen, die von innerhalb eines virtuellen Netzwerks (oder einem VPN) stammen. Er verteilt Anforderungen an Ressourcen in diesem virtuellen Netzwerk. Auf den Load Balancer, die Front-End-IP-Adressen und virtuellen Netzwerke kann nicht direkt über das Internet zugegriffen werden. Die folgende Abbildung zeigt eine Architektur mit einem öffentlichen und einem internen Load Balancer. Der öffentliche Load Balancer verarbeitet externe Anforderungen, während der interne Load Balancer die Anforderungen zur Verarbeitung an die internen virtuellen Computer und Datenbanken weiterleitet.

![Eine Abbildung mit einem öffentlichen Load Balancer, der Clientanforderungen an einen internen Load Balancer weiterleitet. Der interne Load Balancer verteilt dann Anforderungen basierend auf ihrem Typ an ein Subnetz auf Web- oder Datenschicht. Im Subnetz auf Web- oder Datenschicht gibt es mehrere Server, die Anforderungen verarbeiten.](../media-draft/2-internal-load-balancer.png)

## <a name="how-does-the-azure-load-balancer-work"></a>Was funktioniert der Azure Load Balancer?

Der Azure Load Balancer nutzt Informationen, die in **Regeln** und **Integritätstests** konfiguriert sind, um zu bestimmen, wie neuer eingehender Datenverkehr, der vom **Front-End** des Load Balancers empfangen wird, auf VM-Instanzen in einem **Back-End-Pool** verteilt wird.

### <a name="frontend"></a>Front-End

Das Load Balancer-Front-End ist eine IP-Konfiguration mit einer oder mehreren öffentlichen IP-Adressen, die den Zugriff auf den Load Balancer und seine Anwendungen über das Internet ermöglicht.

### <a name="backend-address-pool"></a>Back-End-Adresspool

Virtuelle Computer werden über die zugehörige virtuelle Netzwerkschnittstelle (vNIC) mit einem Load Balancer verbunden. Der Back-End-Adresspool enthält die IP-Adressen der vNICs, die mit dem Load Balancer verbunden sind. Wenn Sie alle Ihre VMs in einer Verfügbarkeitsgruppe platzieren, können Sie diese verwenden, um Ihre VMs bei der Konfiguration des Load Balancers ganz einfach zu einem Back-End-Pool hinzuzufügen.

### <a name="health-probe"></a>Integritätstest

Load Balancer verwenden _Integritätstests_, um zu bestimmen, welche virtuellen Computer die Anforderungen erfüllen können. Der Load Balancer verteilt den Datenverkehr nur an VMs, die verfügbar und betriebsbereit sind. 

Ein Integritätstest überwacht auf jedem virtuellen Computer bestimmte Ports. Sie können definieren, welche Art von Antwort „Integrität“ entspricht. Sie können z.B. eine Antwort `HTTP 200 Available` von einer Webanwendung anfordern. Standardmäßig wird eine VM nach zwei aufeinanderfolgenden Ausfällen in Abständen von 15 Sekunden als „nicht verfügbar“ gekennzeichnet.

### <a name="load-balancer-rules"></a>Lastenausgleichsregeln

_Lastenausgleichsregeln_ bestimmen, wie Datenverkehr auf virtuelle Computer im Back-End verteilt wird. Ziel ist es, Anforderungen gleichmäßig auf die fehlerfreien VMs im Back-End-Pool zu verteilen.

Der Azure Load Balancer verwendet einen hashbasierten Algorithmus, um die Header eingehender Pakete neu zu schreiben. Standardmäßig erstellt der Load Balancer einen Hash aus folgenden Informationen:

- Quell-IP-Adresse
- Quellport
- Ziel-IP-Adresse
- Zielport
- IP-Protokollnummer

Dieser Mechanismus stellt sicher, dass alle Pakete innerhalb der Paketübertragung eines Clients an dieselbe VM-Instanz im Back-End gesendet werden. Eine neue Übertragung von einem Client verwendet einen anderen nach dem Zufallsprinzip zugewiesenen Quellport, sodass sich der Hash ändert, und der Load Balancer sendet diese Übertragung möglicherweise an einen anderen Back-End-Endpunkt.

## <a name="basic-vs-standard-load-balancer-skus"></a>Gegenüberstellung der  Load Balancer-SKUs „Basic“ und „Standard“

Es gibt zwei Azure Load Balancer-Typen: **Basic** und **Standard**. Sie unterscheiden sich hinsichtlich Staffelung, Features und Preisen. Beispiel:

- „Standard“ unterstützt HTTPS, „Basic“ jedoch nicht.
- „Standard“ unterstützt wesentlich größere Pools.
- „Basic“ ist kostenlos, während „Standard“ basierend auf Regeln und Durchsatz in Rechnung gestellt wird.

„Standard“ ist eine Obermenge von „Basic“. Daher sollte jedes für „Basic“ geeignete Szenario auch für „Standard“ funktionieren. Die SKU „Basic“ ist eher für die Erstellung von Prototypen und Tests vorgesehen, während sich „Standard“ für Produktionsumgebungen eignet.

## <a name="start-the-deployment-of-a-basic-public-load-balancer"></a>Einleiten der Bereitstellung eines öffentlichen Load Balancers des Typs „Basic“

Um ein VM-System mit Lastenausgleich einzurichten, müssen Sie den Load Balancer selbst erstellen, ein virtuelles Netzwerk für Ihre virtuellen Computer erstellen und dann dem virtuellen Netzwerk VMs hinzufügen.

Zum Erstellen des Load Balancers im Azure-Portal definieren Sie Folgendes:

- Name des Load Balancers
- Typ: Öffentlich oder Intern
- SKU: Basic oder Standard
- Öffentliche IP-Adresse: Dynamisch oder Statisch.
- Ressourcengruppe und Standort

Ihre Back-End-VMs werden alle mit demselben virtuellen Netzwerk (VNET) verbunden, weshalb Sie diese Ressource als Nächstes konfigurieren müssen:

- VNET-Name
- Zu verwendender Adressraum wie z.B. 172.20.0.0/16
- Ressourcengruppe
- Namen des zu verwendenden Subnetzes
- Adressraum des Subnetzes (muss sich innerhalb des Hauptbereichs befinden), z.B. 172.20.0.0/24

Anschließend müssen Sie Ihre Back-End-VMs erstellen und bereitstellen und sie für die Nutzung Ihres VNET konfigurieren. Sie sollten auch Ihre virtuellen Computer in derselben Verfügbarkeitsgruppe platzieren. Verfügbarkeitsgruppen definieren den Grad an Fehlertoleranz für eine Gruppe von VMs, doch beim Lastenausgleich helfen sie Ihnen auch, Ihre VMs Back-End-Pools zuzuweisen.

Sie haben soeben erfahren, wie Sie einen Azure Load Balancer als Teil einer Hochverfügbarkeitslösung einsetzen können. Als Nächstes befolgen Sie diese Schritte, um Ihren eigenen Load Balancer bereitzustellen.