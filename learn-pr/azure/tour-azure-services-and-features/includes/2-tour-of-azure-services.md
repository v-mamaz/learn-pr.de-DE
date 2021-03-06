Microsoft Azure ist ein Portfolio mit Clouddiensten, das kontinuierlich erweitert wird und Ihre Organisation dabei unterstützt, aktuelle und zukünftige geschäftliche Herausforderungen zu bewältigen. Mit Azure können Sie Anwendungen in einem umfassenden globalen Netzwerk mit Ihren bevorzugten Tools und Frameworks erstellen, verwalten und bereitstellen. Verschaffen wir uns nun einen Überblick über die allgemeinen Dienste, die Azure bereitstellt.

#### <a name="azure-the-big-picture"></a>Azure: Übersicht

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yuas]

## <a name="azure-services"></a>Azure-Dienste

Azure bietet eine große Bandbreite cloudbasierter Dienste, denen jeden Monat neue und erweiterte Features hinzugefügt werden. 

![Diagramm mit Übersicht der Azure-Dienste](../media/2-azure-services.png "Azure-Dienste")

Sehen wir uns einige häufig verwendete Features genauer an: 

- Compute
- Netzwerk
- Speicher
- Mobile
- Datenbanken
- Web

### <a name="compute"></a>Compute

Computedienste sind einer der Hauptgründe, aus denen Unternehmen auf die Azure-Plattform umsteigen. Azure bietet eine Vielzahl von Optionen zum Hosten von Anwendungen und Diensten:

![Eine Abbildung zeigt drei Arten von Azure-Computediensten: Infrastructure-as-a-Service, Platform-as-a-Service und Functions-as-a-Service. Sie zeigt auch die Komponenten, die Sie verwalten, und die von Azure verwalteten Komponenten unter dem jeweiligen Typdienst.](../media/2-iaas-paas-faas.png)

Hier sind einige Beispiele für IaaS, PaaS und FaaS in Azure.

|  Typ  |  Dienstname             | Funktion des Diensts                                                         |
|--------|---------------------------|--------------------------------------------------------------------------|
| IaaS   | Azure Virtual Machines    | In Azure gehostete Windows- oder Linux-VMs                  | 
| IaaS   | Azure Kubernetes Service  | Ermöglicht die Verwaltung eines Clusters aus VMs, die Dienste in Containern ausführen   |
| PaaS   | Azure Service Fabric      | Plattform für verteilte Systeme. Wird in Azure oder lokal ausgeführt.               |
| PaaS   | Azure Batch               | Verwalteter Dienst für parallele und hochleistungsfähige Computinganwendungen. |
| PaaS   | Azure Cloud Services      | Verwalteter Dienst zum Ausführen von Cloudanwendungen                           |
| FaaS   | Azure Container Instances | Stellt Container bereit, ohne VMs oder höherwertige Dienste zu erfordern    |
| FaaS   | Azure Functions           | Verwalteter FaaS-Dienst                                                     |

### <a name="networking"></a>Netzwerk

Das Verknüpfen von Computeressourcen und Ermöglichen des Zugriffs auf Anwendungen sind die Hauptfunktionen von Azure-Netzwerken. Die Netzwerkfunktionen in Azure umfassen eine Reihe von Optionen, um die Außenwelt mit Diensten und Features in den globalen Microsoft Azure-Rechenzentren zu verbinden.

Die Azure-Netzwerkfunktionen bieten folgende Features:

|  Dienstname             | Funktion des Diensts                                                                     |
| -------------             | -------------                                                                        |
| Azure Virtual Network     | Verknüpfen von VMs mit eingehenden VPN-Verbindungen (virtuelles privates Netzwerk)                   |
| Azure Load Balancer       | Gleichmäßige Verteilung ein- und ausgehender Verbindungen auf Anwendungen oder Dienstendpunkte       |
| Azure Application Gateway | Optimieren der Bereitstellung von App-Serverfarmen und gleichzeitiges Erhöhen der Anwendungssicherheit             |
| Azure VPN Gateway         | Zugriff auf Azure Virtual Networks über hochleistungsfähige VPN-Gateways                |
| Azure DNS                 | Bereitstellen von ultraschnellen DNS-Antworten und ultrahoher Domänenverfügbarkeit                 |
| Azure Content Delivery Network  | Inhaltsbereitstellung mit hoher Bandbreite für Kunden auf der ganzen Welt                          |
| Azure DDoS Protection     | Schützen von in Azure gehosteten Anwendungen vor DDoS-Angriffen (Distributed Denial of Service) |
| Azure Traffic Manager     | Verteilen des Netzwerkdatenverkehrs über Azure-Regionen weltweit                           |
| Azure ExpressRoute        | Dedizierte sichere Verbindungen mit Azure mit hoher Bandbreite                   |
| Azure Network Watcher     | Überwachen und Diagnostizieren von Netzwerkproblemen mithilfe von szenariobasierten Analysen                  |
| Azure Firewall            | Implementieren einer Firewall mit hoher Sicherheit und Verfügbarkeit sowie unbegrenzter Skalierbarkeit      |
| Azure Virtual WAN         | Erstellen eines einheitlichen WAN, über das lokale und Remotestandorte verbunden werden         |

### <a name="storage"></a>Speicher

Azure bietet vier wesentliche Arten von Speicherdiensten. Folgende Dienste stehen zur Verfügung:

- **Azure Blob Storage** bietet Speicher für sehr große Objekte wie Videodateien oder Bitmaps.
- **Azure File Storage** erstellt Dateifreigaben, deren Verwaltung und Zugriff genauso wie bei einem Dateiserver funktioniert.
- **Azure Queue Storage** implementiert einen Speicher für Warteschlangen und die zuverlässige Übermittlung von Nachrichten zwischen Anwendungen.
- **Azure Table Storage** besteht aus einem NoSQL-Speicher, der unstrukturierte Daten unabhängig von einem Schema hostet.

All diese Dienste weisen die folgenden gemeinsamen Merkmale auf:

- Dauerhaft und hochverfügbar durch Redundanz- und Replikationsfunktionen.
- Sicher dank automatischer Verschlüsselung und rollenbasierter Zugriffssteuerung.
- Skalierbar dank praktisch unbegrenzter Speichermenge.
- Verwaltung sowie und Behandlung aller kritischen Probleme werden für Sie übernommen.
- Zugriff von jedem Ort der Welt über HTTP oder HTTPS möglich.

### <a name="mobile"></a>Mobile

Azure ermöglicht Entwicklern, mit einer Vielzahl von Sprachen und in der Entwicklungsumgebung ihrer Wahl schnell und einfach ansprechende iOS-, Android- und Windows-Apps zu erstellen. Features, die bisher viel Zeit kosteten und das Projektrisiko erhöhten, z.B. das Hinzufügen von Unternehmensanmeldungen und Herstellen von Verbindungen mit lokalen Ressourcen wie SAP, Oracle, SQL Server und SharePoint, lassen sich jetzt ganz einfach integrieren.

Dieser Dienst bietet zudem folgende Features:

- Offlinedatensynchronisierung.
- Konnektivität zu lokalen Daten.
- Übertragen von Pushbenachrichtigungen.
- Automatische Skalierung zum Erfüllen sich verändernder Geschäftsanforderungen.

### <a name="databases"></a>Datenbanken

Azure bietet mehrere Datenbankdienste, um eine Vielzahl von Datentypen und Datenvolumen zu speichern. Und dank der globalen Konnektivität sind diese Daten für Benutzer sofort verfügbar.

|  Dienstname              | Funktion des Diensts                                                                                |
| -------------              | -------------                                                                                   |
| Azure Cosmos DB            | Global verteilte Datenbank, die NoSQL-Optionen unterstützt.                                       |
| Azure SQL-Datenbank         | Vollständig verwaltete relationale Datenbank mit automatischer Skalierung, integrierten intelligenten Funktionen und stabiler Sicherheit.    |
| Azure Database for MySQL   | Vollständig verwaltete und skalierbare relationale MySQL-Datenbank mit hoher Verfügbarkeit und Sicherheit        |
| Azure Database for PostgreSQL   | Vollständig verwaltete und skalierbare relationale PostgreSQL-Datenbank mit hoher Verfügbarkeit und Sicherheit   |
| SQL Server auf virtuellen Computern          | Hosten von SQL Server-Unternehmens-Apps in der Cloud                                                    |
| Azure SQL Data Warehouse   | Vollständig verwaltetes Data Warehouse mit integrierter Sicherheit in jeder Größenordnung ohne Zusatzkosten    |
| Azure Database Migration Service    | Migrieren Ihrer Datenbanken in die Cloud, ohne Änderungen am Anwendungscode vorzunehmen                  |
| Azure Redis Cache          | Zwischenspeichern von häufig verwendeten und statischen Daten, um die Latenz für Daten und Anwendungen zu reduzieren                   |
| Azure Database for MariaDB | Vollständig verwaltete und skalierbare relationale MySQL-Datenbank mit hoher Verfügbarkeit und Sicherheit        |

### <a name="web"></a>Web

Webdienste in Azure umfassen die folgenden Funktionen:

| Name des Diensts | Beschreibung |
|--------------|-------------|
| Azure App Service | Schnelle Erstellung von leistungsstarken Cloud-Apps für Web- und Mobilgeräte |
| Azure Notification Hubs |Senden von Pushbenachrichtigungen an jede Plattform und von jedem Back-End aus |
| Azure API Management | Sicheres Veröffentlichen von APIs für Entwickler, Partner und Mitarbeiter im erforderlichen Umfang |
| Azure Search | Vollständig verwaltete SaaS-Lösung (Search-as-a-Service) |
| Web-Apps-Funktion von Azure App Service | Erstellen und Bereitstellen von unternehmenskritischen Web-Apps nach Maß |
| Azure SignalR Service | Einfaches Hinzufügen von Echtzeit-Webfunktionen |

Nachdem wir einige Bereiche entdeckt haben, die für ein Unternehmen, das zu Azure wechseln möchte, von Interesse sein können, sehen wir uns an, welche Voraussetzungen zur Verwendung der Dienste und Funktionen erfüllt sein müssen.
