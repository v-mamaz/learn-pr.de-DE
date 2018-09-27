Angenommen, Ihr Unternehmen möchte prüfen, ob Azure Load Balancer Ihre ERP-Anwendung (Enterprise Resource Planning) unterstützt. Die Anwendung verfügt über eine Weboberfläche für Benutzer und wird auf mehreren Webservern ausgeführt. Jeder Server verfügt über eine lokale Kopie der ERP-Datenbank, die mit allen Servern synchronisiert wird.

Im Folgenden erfahren Sie, wie ein Lastenausgleich zur Hochverfügbarkeit von Diensten beitragen kann. Sie lernen den Unterschied zwischen den Load Balancer-Optionen „Basic“ und „Standard“ kennen und erfahren, wie Sie einen Lastenausgleich für Azure Virtual Machines erstellen.

## <a name="what-is-load-balancing"></a>Was ist ein Lastenausgleich?

Unter _Lastenausgleich_ sind verschiedene Verfahren zur Verteilung von Workloads auf mehrere Geräte wie Compute-, Speicher- oder Netzwerkgeräte zu verstehen. Ziel des Lastenausgleichs ist die Optimierung der Nutzung mehrerer Ressourcen, eine möglichst effiziente Gestaltung dieser Nutzung, wenn eine Infrastruktur horizontal hochskaliert wird, und die Sicherstellung der Aufrechterhaltung von Diensten, wenn einzelne Komponenten nicht verfügbar sind.

Im Folgenden wird erläutert, wie Azure den Lastenausgleich für virtuelle Computer (VMs) unterstützt.

### <a name="what-is-high-availability"></a>Was ist Hochverfügbarkeit?

Als Hochverfügbarkeit gilt die Fähigkeit einer Anwendung oder eines Diensts, trotz eines Ausfalls einer Systemkomponente weiterhin den Zugriff zu ermöglichen. Im Idealfall ist dann keine Dienstunterbrechung spürbar.

Ein Lastenausgleich ist für die Bereitstellung von Hochverfügbarkeit unerlässlich, da mehrere VMs als ein Pool von Servern fungieren können. Der Pool kann weiterhin Dienstanforderungen entgegennehmen, auch wenn einige VMs abstürzen sollten oder zur Wartung offline geschaltet werden.

## <a name="what-is-azure-load-balancer"></a>Was ist Azure Load Balancer?

**Azure Load Balancer** ist ein Azure-Dienst, der eingehende Anforderungen auf mehrere virtuelle Computer in einem Pool verteilt. Der Dienst verteilt eingehenden Netzwerkdatenverkehr auf mehrere ordnungsgemäß funktionierende VMs und umgeht VMs, die nicht reagieren können.

 Azure Load Balancer arbeitet auf der 4. Schicht (TCP, UDP) des aus 7 Schichten bestehenden OSI-Modells. Der Dienst kann zur Unterstützung von TCP- und UDP-Anwendungsszenarios konfiguriert werden, bei denen der Datenverkehr an Azure-VMs gesendet wird. Er unterstützt auch Szenarios mit ausgehendem Datenverkehr, bei denen andere Azure-Dienste den TCP- und UDP-Datenverkehr über Azure-VMs an externe Endpunkte weiterleiten.

#### <a name="what-is-a-load-balancer"></a>Was ist ein Lastenausgleich mit Load Balancer?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yBWo]

## <a name="public-vs-internal-load-balancers"></a>Vergleich zwischen öffentlichen und internen Lastenausgleichsmodulen von Load Balancer

Azure Load Balancer kann je nach Quelle der eingehenden Anforderungen auf _öffentlicher_ oder _interner_ Ebene agieren.

Im Rahmen eines **öffentlichen Lastenausgleichs** mit Load Balancer werden Clientanforderungen verarbeitet, die von außerhalb der Azure-Infrastruktur eingehen. Die öffentliche IP-Adresse wird dem Lastenausgleichsmodul zugewiesen, und die eingehenden Anforderungen werden an verschiedene Ressourcen weitergeleitet, die sich in einem privaten Netzwerk befinden. Dieser Ansatz wird in der Regel verwendet, um Hochverfügbarkeit für Webserver bereitzustellen. Auf der folgenden Abbildung sehen Sie ein öffentliches Load Balancer-Modul.

![Abbildung: öffentliches Load Balancer-Modul, das Clientanforderungen aus dem Internet an drei VMs in einem virtuellen Netzwerk verteilt.](../media/2-public-load-balancer.png)

Im Rahmen eines **internen Lastenausgleichs** mit Load Balancer werden Anforderungen verarbeitet, die von innerhalb eines virtuellen Netzwerks (oder einem VPN) gesendet werden. Er verteilt Anforderungen an Ressourcen in diesem virtuellen Netzwerk. Auf Load Balancer, die Front-End-IP-Adressen und virtuelle Netzwerke kann nicht direkt über das Internet zugegriffen werden. Die folgende Abbildung zeigt eine Architektur mit einem öffentlichen und einem internen Load Balancer-Modul. Der öffentliche Load Balancer verarbeitet externe Anforderungen, während der interne Load Balancer die Anforderungen zur Verarbeitung an die internen virtuellen Computer und Datenbanken weiterleitet.

![Eine Abbildung mit einem öffentlichen Load Balancer, der Clientanforderungen an einen internen Load Balancer weiterleitet. Der interne Load Balancer verteilt dann Anforderungen basierend auf ihrem Typ an ein Subnetz auf Web- oder Datenschicht. Im Subnetz der Web- oder Datenbankschicht gibt es mehrere Server, die Anforderungen verarbeiten.](../media/2-internal-load-balancer.png)

## <a name="how-does-azure-load-balancer-work"></a>Wie funktioniert Azure Load Balancer?

Azure Load Balancer verwendet Informationen, die in _Regeln_ und _Integritätstests_ konfiguriert sind, um zu bestimmen, wie eingehender Datenverkehr, der vom _Front-End_ des Load Balancer-Moduls empfangen wird, auf VM-Instanzen in einem _Back-End-Adresspool_ verteilt wird. Nachfolgend werden die einzelnen Komponenten im Detail erläutert.

### <a name="what-is-the-load-balancer-front-end"></a>Was ist das Load Balancer-Front-End?

Das Load Balancer-Front-End ist eine IP-Konfiguration mit mindestens einer öffentlichen IP-Adresse, die den Zugriff auf Load Balancer und die zugehörigen Anwendungen über das Internet ermöglicht.

### <a name="what-is-the-backend-address-pool"></a>Was ist der Back-End-Adresspool?

Virtuelle Computer werden über die zugehörige virtuelle Netzwerkschnittstelle (vNIC) mit einem Load Balancer-Modul verbunden. Der Back-End-Adresspool enthält die IP-Adressen der vNICs, die mit dem Load Balancer-Modul verbunden sind. Wenn Sie alle Ihre VMs in einer Verfügbarkeitsgruppe platzieren, können Sie diese verwenden, um Ihre VMs bei der Konfiguration des Load Balancer-Moduls ganz einfach zu einem Back-End-Pool hinzuzufügen.

### <a name="what-is-a-health-probe"></a>Was ist ein Integritätstest?

Load Balancer-Module verwenden _Integritätstests_, um zu bestimmen, welche virtuellen Computer die Anforderungen erfüllen können. Der Load Balancer verteilt den Datenverkehr nur an VMs, die verfügbar und betriebsbereit sind.

Ein Integritätstest überwacht auf jedem virtuellen Computer bestimmte Ports. Sie können definieren, welche Art von Antwort „Integrität“ entspricht. Sie können z.B. eine Antwort `HTTP 200 Available` von einer Webanwendung anfordern. Standardmäßig wird eine VM nach zwei aufeinanderfolgenden Ausfällen in Abständen von 15 Sekunden als „nicht verfügbar“ gekennzeichnet.

### <a name="load-balancer-rules"></a>Lastenausgleichsregeln

_Lastenausgleichsregeln_ bestimmen, wie Datenverkehr auf virtuelle Computer im Back-End verteilt wird. Ziel ist es, Anforderungen gleichmäßig auf die fehlerfreien VMs im Back-End-Pool zu verteilen.

Azure Load Balancer verwendet einen hashbasierten Algorithmus, um die Header eingehender Pakete neu zu schreiben. Standardmäßig erstellt Load Balancer einen Hash aus folgenden Informationen:

- IP-Adresse der Quelle
- Quellport
- IP-Adresse des Ziels
- Zielport
- IP-Protokollnummer

Dieser Mechanismus stellt sicher, dass alle Pakete innerhalb der Paketübertragung eines Clients an dieselbe VM-Instanz im Back-End gesendet werden. Für jede Übertragung eines Clients wird ein anderer zufällig zugewiesener Quellport verwendet. Das bedeutet, dass sich der Hash ändert und das Load Balancer-Modul diese Daten an einen anderen Endpunkt im Back-End überträgt.

## <a name="basic-vs-standard-load-balancer-skus"></a>Gegenüberstellung von Load Balancer-SKUs in den Tarifen „Basic“ und „Standard“

Es gibt zwei Azure Load Balancer-Versionen: **Basic** und **Standard**. Sie unterscheiden sich im Hinblick auf Staffelung, Features und Preise. Beispiele:

- Der Tarif „Standard“ unterstützt die sichere Weiterleitung von Datenverkehr über HTTPS.
- Der Tarif „Standard“ unterstützt wesentlich größere Back-End-Pools (1000 im Gegensatz zu 100 im Tarif „Basic“).
- Datenverkehr kann an einen größeren Endpunktpool weitergeleitet werden, einschließlich einer Mischung aus Skalierungsgruppen, Verfügbarkeitsgruppen und VMs. Die SKU im Tarif „Basic“ ist auf eine Verfügbarkeitsgruppe, eine Skalierungsgruppe oder eine VM beschränkt.
- Unterstützung von Hochverfügbarkeitsports für den gleichzeitigen Lastenausgleich von TCP- und UDP-Datenflüssen auf allen Ports, wenn Sie ein internes Load Balancer-Modul verwenden.
- „Basic“ ist kostenlos, während „Standard“ basierend auf Regeln und Durchsatz in Rechnung gestellt wird.

„Standard“ ist eine Obermenge von „Basic“. Daher sollte jedes für „Basic“ geeignete Szenario auch für „Standard“ funktionieren. Die SKU im Tarif „Basic“ ist eher für die Erstellung von Prototypen und Tests vorgesehen, während sich die SKU im Tarif „Standard“ für Produktionsumgebungen eignet.

## <a name="start-the-deployment-of-a-basic-public-load-balancer"></a>Einleiten der Bereitstellung eines öffentlichen Load Balancer-Moduls im Tarif „Basic“

Zum Erstellen eines VM-Systems mit Lastenausgleich müssen Sie selbst das Load Balancer-Modul und ein virtuelles Netzwerk für Ihre virtuellen Computer erstellen und anschließend dem virtuellen Netzwerk VMs hinzufügen.

Zum Erstellen des Load Balancers im Azure-Portal müssen Sie Folgendes definieren:

- Name des Load Balancer-Moduls
- Typ: öffentlich oder intern
- SKU: „Basic“ oder „Standard“
- Öffentliche IP-Adresse: dynamisch oder statisch
- Ressourcengruppe und -standort

Ihre Back-End-VMs werden alle mit demselben virtuellen Netzwerk verbunden. Daher müssen Sie diese Ressource als Nächstes konfigurieren:

- Name des virtuellen Netzwerks
- Zu verwendender Adressraum, z.B. 172.20.0.0/16
- Ressourcengruppe
- Namen des zu verwendenden Subnetzes
- Adressraum des Subnetzes (muss sich innerhalb des Hauptbereichs befinden), z.B. 172.20.0.0/24

Da eingehender Datenverkehr zur erwarten ist, müssen Sie mithilfe einer Netzwerksicherheitsgruppe einige Regeln für die Netzwerksicherheit erstellen. Öffnen Sie für dieses Beispiel Port 80 für HTTP-Datenverkehr.

Anschließend müssen Sie virtuelle Computer erstellen, bereitstellen und für die Verwendung Ihres virtuellen Netzwerks konfigurieren. Erstellen Sie außerdem eine Verfügbarkeitsgruppe, in der diese virtuellen Computer zusammengefasst werden. Verfügbarkeitsgruppen definieren den Grad an Fehlertoleranz für eine Gruppe von VMs, doch beim Lastenausgleich helfen sie Ihnen auch, Ihre VMs Back-End-Pools zuzuweisen.

Sie haben soeben erfahren, wie Sie Azure Load Balancer als Teil einer Hochverfügbarkeitslösung einsetzen können. Führen Sie diese Schritte aus, um Ihr eigenes Load Balancer-Modul bereitzustellen.