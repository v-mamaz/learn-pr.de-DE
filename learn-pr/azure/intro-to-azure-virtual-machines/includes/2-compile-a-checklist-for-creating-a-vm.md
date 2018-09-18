Die Migration von lokalen Servern zu Azure erfordert Planung und Sorgfalt. Sie können diese alle gleichzeitig oder eher zutreffend in kleinen Batches oder sogar einzeln verschieben. Bevor Sie eine einzelne VM erstellen, sollten Sie Ihr aktuelles Infrastrukturmodell skizzieren und herausfinden, wie es sich in der Cloud abbilden lässt.

Werfen wir einen Blick auf eine Prüfliste der Punkte, die es zu bedenken gilt.

- [Einstieg mit dem Netzwerk](#Network)
- [Benennen der VM](#Name_VM)
- [Festlegen des Standorts für die VM](#VM_Location)
- [Bestimmen der Größe der VM](#VM_Size)
- [Grundlagen zum Preismodell](#VM_Cost)
- [Speicher für die VM](#VM_Storage)
- [Auswählen eines Betriebssystems](#VM_OS)

<a name="Network" />

## <a name="start-with-the-network"></a>Einstieg mit dem Netzwerk

Der erste Punkt, mit dem Sie beginnen sollten, ist nicht der virtuelle Computer, sondern das Netzwerk.

Virtuelle Netzwerke (VNETs) werden in Azure verwendet, um private Konnektivität zwischen virtuellen Azure-Computern und anderen Azure-Diensten bereitzustellen. VMs und Dienste, die Teil des gleichen virtuellen Netzwerks sind, können aufeinander zugreifen. Dienste außerhalb des virtuellen Netzwerks können standardmäßig keine Verbindung mit Diensten innerhalb des virtuellen Netzwerks herstellen. Sie können jedoch das Netzwerk für den Zugriff auf den externen Dienst, einschließlich Ihrer lokalen Server, konfigurieren.

Dieser letzte Punkt macht deutlich, warum Sie Ihre Netzwerkkonfiguration sorgfältig überdenken sollten. Netzwerkadressen und Subnetze lassen sich nicht ohne Weiteres ändern, sobald diese eingerichtet sind. Wenn Sie zudem eine Verbindung zwischen Ihrem privaten Unternehmensnetzwerk und den Azure-Diensten herstellen möchten, sollten Sie in jedem Fall die Topologie berücksichtigen, bevor Sie VMs platzieren.

Beim Einrichten eines virtuellen Netzwerks geben Sie die verfügbaren Adressräume, Subnetze und die Sicherheit an. Wenn das VNET mit anderen VNETs verbunden werden soll, müssen Sie Adressbereiche auswählen, die sich nicht überlappen. Dies ist der Bereich privater Adressen, die die VMs und Dienste in Ihrem Netzwerk verwenden können. Sie können IP-Adressen, die nicht weitergeleitet werden können (z.B. 10.0.0.0/8, 172.16.0.0/12 oder 192.168.0.0/16), verwenden oder Ihren eigenen Adressbereich definieren. Azure behandelt alle Adressbereiche als Teil des privaten VNET-IP-Adressraums, wenn sie nur innerhalb des VNET, innerhalb von miteinander verbundenen VNETs und von Ihrem lokalen Standort aus erreichbar sind. Wenn eine andere Person für die internen Netzwerke zuständig ist, sollte die Auswahl des Adressraums in Zusammenarbeit mit dieser Person erfolgen, um sicherzustellen, dass es keine Überlappung gibt. Zudem wird sie informiert, welchen Raum Sie verwenden möchten, und sichergestellt, dass sie nicht den gleichen IP-Adressbereich auswählt.

### <a name="segregate-your-network"></a>Trennen des Netzwerks

Nachdem Sie die Adressräume des virtuellen Netzwerks festgelegt haben, können Sie ein oder mehrere Subnetze für Ihr virtuelles Netzwerk erstellen. Hierdurch können Sie Ihr Netzwerk in besser verwaltbare Abschnitte aufteilen. Beispielsweise können Sie VMs 10.1.0.0, Back-End-Diensten 10.2.0.0 und SQL Server-VMs 10.3.0.0 zuweisen.

> [!NOTE]
> Azure reserviert die ersten vier Adressen sowie die letzte Adresse in jedem Subnetz für deren Verwendung.

### <a name="secure-the-network"></a>Schützen des Netzwerks

Standardmäßig besteht keine Sicherheitsgrenze zwischen Subnetzen, sodass Dienste in diesen Subnetzen miteinander kommunizieren können. Sie können aber Netzwerksicherheitsgruppen (NSGs) einrichten, mit denen Sie den Datenverkehrsfluss für Subnetze und VMs in eingehender und ausgehender Richtung steuern können. NSGs dienen als Softwarefirewalls, die benutzerdefinierte Regeln auf die einzelnen eingehenden oder ausgehenden Anforderungen auf der Ebene der Netzwerkschnittstelle und des Subnetzes anwenden. Dadurch können Sie jede auf der VM ein- oder ausgehende Netzwerkanforderung vollständig steuern.

## <a name="plan-each-vm-deployment"></a>Planen der VM-Bereitstellungen

Nachdem Sie Ihre Kommunikations- und Netzwerkanforderungen ausgearbeitet haben, können Sie sich nun mit der Auswahl der VMs auseinandersetzen, die Sie erstellen möchten. Ein guter Plan besteht darin, einen Server auszuwählen und eine Bestandsaufnahme durchzuführen:

- Mit welchen Komponenten kommuniziert der Server?
- Welche Ports sind geöffnet?
- Welches Betriebssystem wird verwendet?
- Wie viel Speicherplatz auf dem Datenträger wird verwendet?
- Welche Art von Daten beanspruchen diesen Speicherplatz? Gibt es (rechtliche oder andere) Einschränkungen, wenn der Server nicht lokal ausgeführt wird?
- Auf welche Höhe belaufen sich CPU-, Arbeitsspeicher- und E/A-Datenträgerlast des Servers? Muss Burstdatenverkehr berücksichtigt werden?

Anschließend können wir uns mit einigen Fragen befassen, die sich bei einem neuen virtuellen Computer mit Azure stellen.

<a name="Name_VM" />

### <a name="name-the-vm"></a>Benennen der VM

Eine Information, denen Benutzer oftmals wenig Bedeutung beimessen, ist der **Name** der VM. Der VM-Name wird als Computername verwendet, der als Teil des Betriebssystems konfiguriert ist. Sie können einen Namen mit bis zu 15 Zeichen auf einer Windows-VM und einen Namen mit 64 Zeichen auf einer Linux-VM angeben.

Dieser Name definiert auch eine verwaltbare **Azure-Ressource** und lässt sich später nicht ohne Weiteres ändern. Sie sollten daher sinnvolle und konsistente Namen auswählen, damit Sie mühelos erkennen können, welchem Zweck eine VM dient. Es hat sich bewährt, die folgenden Informationen im Namen anzugeben:

| Element | Beispiel | Hinweise |
| --- | --- | --- |
| Umgebung |dev, prod, QA |Identifiziert die Umgebung für die Ressource. |
| Standort |uw (USA, Westen), ue (USA, Osten) |Identifiziert die Region, in welcher die Ressource bereitgestellt wird. |
| Instanz |01, 02 |Für Ressourcen, die mehr als eine benannte Instanz aufweisen (Webserver usw.). |
| Produkt oder Dienst |service |Identifiziert das Element (Produkt, Anwendung oder Dienst), das von der Ressource unterstützt wird. |
| Rolle |sql, web, messaging |Identifiziert die Rolle der zugeordneten Ressource. | 

Beispielsweise kann `devusc-webvm01` den ersten Entwicklungswebserver darstellen, der in der Region „USA, Süden-Mitte“ gehostet wird. 

#### <a name="what-is-an-azure-resource"></a>Was ist eine Azure-Ressource?

Eine **Azure-Ressource** ist ein verwaltbares Element in Azure. Genau wie ein physischer Computer in Ihrem Rechenzentrum weisen VMs mehrere Elemente auf, die erforderlich sind, um die jeweilige Aufgabe auszuführen:

- Die VM selbst
- Speicherkonto für die Datenträger
- Virtuelles Netzwerk (gemeinsam mit anderen VMs und Diensten verwendet)
- Netzwerkschnittstelle für die Kommunikation mit dem Netzwerk
- Netzwerksicherheitsgruppe(n), um den Netzwerkdatenverkehr zu schützen
- Öffentliche IP-Adresse (optional)

Azure erstellt all diese Ressourcen bei Bedarf, oder Sie können vorhandene Ressourcen im Rahmen des Bereitstellungsprozesses angeben. Jede Ressource benötigt einen Namen, der zur Identifizierung verwendet wird. Wenn Azure die Ressource erstellt, wird der VM-Name zum Generieren eines Ressourcennamens verwendet – ein weiterer Grund, warum sich eine konsistente Benennung bei VM-Namen empfiehlt!

<a name="VM_Location" />

### <a name="decide-the-location-for-the-vm"></a>Festlegen des Standorts für die VM

Azure stellt Rechenzentren auf der ganzen Welt zur Verfügung, die mit Servern und Datenträgern ausgestattet sind. Diese Rechenzentren sind in geografische _Regionen_ unterteilt („USA, Westen“, „Europa, Norden“, „Asien, Südosten“ usw.), um Redundanz und Verfügbarkeit bereitzustellen.

Wenn Sie einen virtuellen Computer erstellen und bereitstellen, müssen Sie eine Region auswählen, in der die Ressourcen (CPU, Speicher usw.) zugeteilt werden sollen. So können Sie Ihre VMs möglichst in der Nähe Ihrer Benutzer platzieren, um die Leistung zu verbessern und gesetzliche, compliancebezogene oder steuerrechtliche Anforderungen zu erfüllen.

<a name="VM_Size" />

### <a name="determine-the-size-of-the-vm"></a>Bestimmen der Größe der VM

Nachdem Sie den Namen und den Standort festgelegt haben, müssen Sie die Größe Ihrer VM auswählen. Statt im Einzelnen Verarbeitungsgeschwindigkeit, Arbeitsspeicher und Speicherkapazitäten angeben zu müssen, stellt Azure verschiedene _VM-Größen_ zur Verfügung, die Varianten dieser Elemente in unterschiedlichen Größen bieten. Azure bietet eine große Bandbreite an VM-Größenoptionen, mit der Sie eine geeignete Kombination aus Compute-, Arbeitsspeicher- und Speicherkapazitäten für die von Ihnen gewünschte Aufgabe erfüllen können.

Um die geeignete VM-Größe zu bestimmen, empfiehlt es sich, die Art der Workload, die auf Ihrer VM ausgeführt werden muss, in Betracht zu ziehen. Basierend auf der Workload können Sie eine Teilmenge der verfügbaren VM-Größen auswählen. Workloadoptionen sind wie folgt in Azure klassifiziert:

| Option              | Beschreibung |
|---------------------|-------------|
| **Allgemeiner Zweck** | Universelle VM-Größen zeichnen sich durch ein ausgewogenes Verhältnis zwischen CPU und Arbeitsspeicher aus. Ideal für Tests und Entwicklung, kleine bis mittlere Datenbanken sowie Webserver mit geringer bis mittlerer Auslastung. |
| **Für Compute optimiert** | Für Compute optimierte VMs zeichnen sich durch ein hohes Verhältnis zwischen CPU und Arbeitsspeicher aus. Geeignet für Webserver, Netzwerkappliances, Batchprozesse und Anwendungsserver mit mittlerer Auslastung. |
| **Arbeitsspeicheroptimiert** | Arbeitsspeicheroptimierte VMs zeichnen sich durch ein hohes Verhältnis zwischen Arbeitsspeicher und CPU aus. Hervorragend geeignet für relationale Datenbankserver, mittlere bis große Caches und In-Memory-Analysen. |
| **Speicheroptimiert** | Datenspeicheroptimierte VMs zeichnen sich durch einen hohen Durchsatz und eine hohe E/A-Leistung aus. Ideal für VMs, auf denen Datenbanken ausgeführt werden. |
| **GPU** | GPU-VMs sind auf virtuelle Computer für intensives Grafikrendering und intensive Videobearbeitung spezialisiert. Diese VMs sind ideale Optionen für das Modelltraining und Rückschlüsse mit Deep Learning. |
| **High Performance Computing** | HPC-VMs (High Performance Computing) sind virtuelle Computer mit den schnellsten und leistungsstärksten CPUs, die optional über Netzwerkschnittstellen mit hohem Durchsatz verfügen. |

Sie können nach dem Workloadtyp filtern, wenn Sie die VM-Größe in Azure konfigurieren. Die von Ihnen gewählte Größe wirkt sich unmittelbar auf die Kosten für Ihren Dienst aus. Je mehr CPU-, Arbeitsspeicher- und GPU-Kapazitäten Sie benötigen, desto höher sind die Kosten.

<a name="VM_Cost" />

### <a name="understanding-the-pricing-model"></a>Grundlegendes zum Preismodell

Es gibt zwei separate Kosten, die im Rahmen des Abonnements für die einzelnen VMs in Rechnung gestellt werden: Compute- und Speicherressourcen.

**Computekosten**: Computeausgaben werden auf Stundenbasis abgerechnet, jedoch pro Minute abgerechnet. Wenn die VM beispielsweise 55 Minuten lang bereitgestellt wird, werden Ihnen nur 55 Minuten für die Nutzung berechnet. Die Computekapazität wird nicht berechnet, wenn Sie die VM anhalten und deren Zuordnung aufheben, da hierdurch die Hardware freigegeben wird. Der Preis pro Stunde variiert je nach VM-Größe und Betriebssystem, die Sie auswählen. Die Kosten für eine VM umfassen die Gebühren für das Windows-Betriebssystem. Linux-basierte Instanzen sind kostengünstiger, da keine Gebühren für Betriebssystemlizenzen anfallen.

> [!TIP]
> So können Sie eventuell Kosten einsparen, indem Sie mithilfe des **Azure-Hybridvorteils** vorhandene Lizenzen für Windows wiederverwenden.

**Speicherkosten**: Der Speicher, der von der VM verwendet wird, wird separat berechnet. Der Status der VM wird nicht bei den anfallenden Speichergebühren berücksichtig. Selbst wenn die VM angehalten bzw. deren Zuordnung aufgehoben wurde und Ihnen keine Kosten für die ausgeführte VM berechnet werden, wird Ihnen der von den Datenträgern beanspruchte Speicher in Rechnung gestellt.

Sie können aus zwei Zahlungsoptionen für die Computekosten wählen.

| Option | Beschreibung |
|--------|-------------|
| **Nutzungsbasierte Zahlung** | Bei der Option zur **nutzungsbasierten Zahlung** profitieren Sie von einer sekundengenauen Abrechnung von Computekapazitäten, ohne langfristige Verpflichtungen oder Vorauszahlungen. Sie können Computekapazität nach Bedarf erhöhen oder verringern und jederzeit starten oder anhalten. Diese Option empfiehlt sich, wenn Sie Anwendungen mit Workloads von kurzer Laufzeit oder unvorhersagbaren Workloads ausführen, die nicht unterbrochen werden dürfen. Dies wäre beispielsweise eine geeignete Option, wenn Sie einen schnellen Test ausführen oder eine App auf einer VM entwickeln. |
| **Reservierte VM-Instanzen** | Bei der Option für reservierte VM-Instanzen (RI) kann im Vorfeld ein virtueller Computer für eine Laufzeit von einem oder drei Jahren in einer bestimmten Region erworben werden. Die Zahlungsverpflichtung wird dabei im Voraus getätigt, wobei Sie im Gegenzug von Einsparungen in Höhe von bis zu 72 % im Vergleich zur nutzungsbasierten Zahlung profitieren. **RIs** sind flexibel und lassen sich mühelos austauschen oder gegen eine Gebühr bei vorzeitiger Beendigung zurückgeben. Diese Option empfiehlt sich, wenn die VM kontinuierlich ausgeführt werden muss oder Sie auf Vorhersagbarkeit in Bezug auf das Budget angewiesen sind **und** eine VM-Nutzung von mindestens einem Jahr vorhersehen können. |

<a name="VM_Storage" />

### <a name="storage-for-the-vm"></a>Speicher für die VM

Alle virtuellen Azure-Computer müssen mindestens zwei virtuelle Festplatten (Virtual Hard Disks, VHDs) aufweisen. Der erste Datenträger speichert das Betriebssystem, während der zweite Datenträger als temporärer Speicher dient. Sie können weitere Datenträger zum Speichern von Anwendungsdaten hinzufügen. Die maximale Anzahl richtet sich nach derWahl der VM-Größe (in der Regel zwei pro CPU). Üblicherweise werden ein oder mehrere Datenträger erstellt, insbesondere, da der Betriebssystemdatenträger meist recht klein ist. Zudem können Sie durch eine Auslagerung der Daten auf andere VHDs die Sicherheit, Zuverlässigkeit und Leistung des Datenträgers unabhängig voneinander verwalten.

Die Daten für die einzelnen VHDs werden in **Azure Storage** als Seitenblobs gespeichert, sodass Azure nur für den von Ihnen verwendeten Speicher Speicherplatz zuweisen kann. Auf diese Weise werden auch Ihre Speicherkosten berechnet: Sie zahlen nur für Speicherkapazitäten, die Sie tatsächlich in Anspruch nehmen.

#### <a name="what-is-azure-storage"></a>Was ist Azure Storage?

Azure Storage ist die cloudbasierte Datenspeicherlösung von Microsoft. Sie unterstützt nahezu jeden Datentyp und bietet Sicherheit, Redundanz sowie skalierbaren Zugriff auf die gespeicherten Daten. Ein Speicherkonto bietet Zugriff auf Objekte in Azure Storage für ein bestimmtes Abonnement. VMs beinhalten stets mindestens ein Speicherkonto, das angefügte virtuelle Datenträger umfasst.

Virtuelle Datenträger können entweder durch Storage **Standard**- oder **Premium**-Konten gesichert werden. Azure Storage Premium nutzt Solid State Drives (SSDs), um eine hohe Leistung und geringe Latenzen auf VMs sicherzustellen, auf denen E/A-intensive Workloads ausgeführt werden. Verwenden Sie Azure Storage Premium für Produktionsworkloads, insbesondere für solche, die empfindlich auf Leistungsschwankungen reagieren oder E/A-intensiv sind. Für Entwicklungs- oder Testzwecke ist Storage Standard völlig ausreichend.

Bei der Datenträgererstellung stehen Ihnen zwei Optionen zur Verfügung, um die Beziehung zwischen dem Speicherkonto und den einzelnen VHDs zu verwalten. Sie können entweder **nicht verwaltete Datenträger** oder **verwaltete Datenträger** verwenden.

| Option | Beschreibung |
|--------|-------------|
| **Nicht verwaltete Datenträger** | Mit nicht verwalteten Datenträgern sind Sie für die Speicherkonten verantwortlich, die verwendet werden, um die VHDs zu speichern, die den Datenträgern Ihrer VMs entsprechen. Sie zahlen die Speicherkontogebühren für die Menge an Speicherplatz, die Sie verwenden. Ein einzelnes Speicherkonto verfügt über ein festes Ratenlimit von 20.000 E/A-Vorgängen pro Sekunde. Das bedeutet, dass ein einzelnes Speicherkonto 40 virtuelle Standardfestplatten mit voller Auslastung unterstützen kann. Wenn Sie mithilfe weiterer Datenträger horizontal hochskalieren müssen, benötigen Sie weitere Speicherkonten. Dies kann kompliziert sein. |
| **Verwaltete Datenträger** | Die Verwendung von verwalteten Datenträgern stellet das **neuere Datenträgerspeichermodell dar und wird empfohlen**. Sie lösen dieses komplexe Problem elegant, indem Sie die Last der Verwaltung der Speicherkonten auf Azure übertragen. Geben Sie die Größe des Datenträgers (max. 4 TB) an. Dann erstellt und verwaltet Azure den Datenträger _und_ den Speicher. Sie müssen sich keine Gedanken um die Grenzwerte für Speicherkonten machen. Dies erleichtert die horizontale Hochskalierung von verwalteten Datenträgern. |

<a name="VM_OS" />

### <a name="select-an-operating-system"></a>Auswählen eines Betriebssystems

Azure bietet eine Vielzahl von Betriebssystemimages, die Sie auf der VM mit den verschiedenen Windows-Versionen und Linux-Konfigurationen installieren können. Wie bereits erwähnt, beeinflusst die Wahl des Betriebssystems die stundenbasierte Abrechnung Ihrer Computeressourcen, da Azure die Kosten für die Betriebssystemlizenz im Preis bündelt.

Wenn Sie mehr als nur Basisbetriebssystemimages suchen, können Sie im Azure Marketplace nach komplexeren Installationsimages suchen, die das Betriebssystem und beliebte Softwaretools für spezielle Szenarien umfassen. Wenn Sie z.B. eine neue Wordpress-Website benötigen, besteht der Standardtechnologiestapel aus einem Linux-Server, einem Apache-Webserver, einer MySQL-Datenbank und PHP. Statt die einzelnen Komponenten separat einrichten und konfigurieren zu müssen, können Sie mithilfe eines Marketplace-Image gleich den gesamten Stapel nutzen und installieren.

Wenn Sie zu guter Letzt kein geeignetes Betriebssystemimage finden sollten, können Sie ein Datenträgerimage mit den erforderlichen Komponenten erstellen, in Azure Storage hochladen und damit eine Azure-VM erstellen. Denken Sie jedoch daran, dass Azure nur 64-Bit-Betriebssysteme unterstützt.