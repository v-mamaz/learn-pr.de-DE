Cloud Computing-Ressourcen werden mithilfe drei verschiedener Modelle bereitgestellt.

- **Infrastructure-as-a-Service (IaaS)** bietet eine sofort nutzbare Computinginfrastruktur, die Sie über das Internet bereitstellen und verwalten können.
- **Platform-as-a-Service (PaaS)** bietet vordefinierte Entwicklungs- und Bereitstellungsumgebungen, die Sie verwenden können, um Ihre eigenen Clouddienste zu übermitteln.
- **Software-as-a-Service (SaaS)** stellt Anwendungen über das Internet als webbasierten Dienst bereit.

Berücksichtigen Sie bei der Auswahl eines Dienstmodells, welche Partei für die Computingressource verantwortlich sein soll. Auf der Basis Ihres Szenarios können Sie entscheiden, wie viel gemeinsame Verantwortung für die Verwaltung Sie wünschen.

![Modell der gemeinsamen Zuständigkeit](../media/3-shared-responsibility.png)

## <a name="iaas"></a>IaaS

Infrastructure-as-a-Service ist eine sofort nutzbare Computinginfrastruktur, die Sie über das Internet bereitstellen und verwalten können. Mit IaaS können Sie schnell Ressourcen skalieren, um der Nachfrage gerecht zu werden, und Sie bezahlen nur für das, was Sie nutzen. IaaS vermeidet Kosten und Komplexität von Kauf und Verwaltung eigener physischer Server und sonstiger Rechenzentrumsinfrastruktur. Jede Ressource wird als separate Dienstkomponente angeboten, und Sie *mieten* die Ressource so lange, wie Sie sie benötigen. IaaS ist daher sehr flexibel. Sie können allgemeine Infrastruktur wie z.B. VMs, Speicher, virtuelle Subnetze, Firewalls und VPNs zum Erstellen einer Lösung bereitstellen. Sie müssen keine physischen Server und Geräte verwalten. Allerdings sind Sie verantwortlich für das Konfigurieren der direkten Verwaltung und das Verwalten der Komponenten. Darunter fällt z.B. das Konfigurieren von Firewalls, Aktualisieren von VM-Betriebssystemen, Aktualisieren von DBMS und Runtimes.

### <a name="common-scenarios"></a>Häufige Szenarios 

Nehmen wir an, dass Ihr Unternehmen im Gesundheitswesen eine spezielle Version einer Desktopsoftware ausführen muss. Die Software wird nur von einer bestimmten Version eines Betriebssystems unterstützt, und nur ein Benutzer und eine Lizenz sind erforderlich. Sie können einen virtuellen Computer mit der erforderlichen Software erstellen. Der Benutzer kann mit Remotedesktop eine Verbindung mit dem virtuellen Computer herstellen, um die Software zu verwenden.

Nehmen wir ein weiteres Szenario an. Ihre Entwicklungsteams benötigen mehrere eindeutige Entwicklungsumgebungen. Im Laufe des Entwicklungszyklus müssen sie verschiedene Versionen des Produkts testen. Die Entwickler können bei Bedarf Umgebungen bereitstellen. Wenn eine Umgebung nicht mehr benötigt wird, kann sie problemlos gelöscht werden.

Andere häufige Szenarios sind:

**Websitehosting:** Wenn Sie mehr Kontrolle über das Hosting einer Website wünschen, ist das Ausführen von Websites mithilfe von IaaS möglicherweise eine bessere Option als das herkömmliche Webhosting.

**Web-Apps:** IaaS bietet die gesamte Infrastruktur zur Unterstützung von Web-Apps, einschließlich Speicher, Web- und Anwendungsservern sowie Netzwerkressourcen. Organisationen können mit IaaS schnell Web-Apps bereitstellen und mühelos Infrastruktur zentral hoch- und herunterskalieren, wenn die Nachfrage nach den Apps nicht vorhersagbar ist.

**Speicher, Sicherung und Wiederherstellung:** Speicherverwaltung kann komplex sein und eine umfangreiche Kapitalinvestition sowie erfahrene Mitarbeiter erfordern, um Daten zu verwalten und rechtliche und Complianceanforderungen zu erfüllen. IaaS kann vereinfachen, Planung, Verwaltung, unvorhersehbaren Bedarf und stetig steigende Speicheranforderungen zu erfüllen.

**High Performance Computing:** Wenn Ihre Workload High Performance Computing erfordert, können Sie die Workload in der Cloud ausführen und so die vorab entstehenden Hardwarekosten vermeiden, sodass Sie nur für die bedarfsorientierte Nutzung zahlen müssen. 

**Big Data-Analyse:** Wenn Sie große Datasets haben, die potenziell wertvolle Muster, Trends und Assoziationen enthalten, kann IaaS die Verarbeitungsleistung bereitstellen, um Datasets zu extrahieren, um Muster zu finden.

### <a name="advantages"></a>Vorteile

**Keinerlei Investitionskosten und niedrigere laufende Kosten:** Mit IaaS vermeiden Sie die im Vorfeld entstehenden Kosten für das Einrichten und Verwalten eines lokalen Rechenzentrums, und damit ist IaaS eine wirtschaftliche Option für Startups und Unternehmen, die neue Ideen testen möchten. Sobald Sie entschieden haben, ein neues Produkt oder eine neue Initiative zu starten, kann die erforderliche Computinginfrastruktur in Minuten oder Stunden bereit stehen statt in Tagen oder Wochen – manchmal sogar Monaten – die eine interne Einrichtung in Anspruch nehmen könnte.

**Verbesserte Geschäftskontinuität und Notfallwiederherstellung:** Hohe Verfügbarkeit, Geschäftskontinuität und Notfallwiederherstellung sind kostenintensiv, da ein entsprechendes Potenzial an Technologie und Mitarbeitern erforderlich ist. Doch mit der richtigen Vereinbarung zum Servicelevel (SLA, Service Level Agreement) kann IaaS diese Kosten senken und während einer Notfallsituation oder eines Ausfalls wie gewohnt auf Anwendungen und Daten zugreifen.

**Schnellere Reaktion auf sich ändernde Geschäftsbedingungen:** Mit IaaS können Sie schnell Ressourcen zentral hochskalieren, um Spitzen bei der Nachfrage bezüglich Ihrer Anwendung – z.B. während der Ferien – gerecht zu werden, und dann wieder Ressourcen herunterskalieren, wenn die Aktivität sinkt, um Geld zu sparen. Da Sie nicht zuerst die Infrastruktur einrichten müssen, bevor Sie Apps entwickeln und bereitstellen können, können Ihre Apps mit IaaS die Benutzer schneller erreichen.

**Mehr Stabilität, Zuverlässigkeit und Unterstützungsmöglichkeiten:** Mit IaaS müssen Sie weder Software und Hardware verwalten und aktualisieren noch Geräteprobleme behandeln. Mit der entsprechenden Vereinbarung stellt der Dienstanbieter sicher, dass Ihre Infrastruktur zuverlässig ist und die jeweiligen SLAs einhält.

## <a name="paas"></a>PaaS

Platform-as-a-Service ist eine vollständige Entwicklungs- und Bereitstellungsumgebung in der Cloud. Mit PaaS können Sie alles von einfachen cloudbasierten Apps bis hin zu ausgereiften, cloudfähigen Unternehmensanwendungen erstellen und bereitstellen. Sie erwerben die Ressourcen von einem Clouddienstanbieter auf nutzungsabhängiger Basis und greifen über eine sichere Internetverbindung darauf zu. Genau wie IaaS umfasst PaaS Infrastruktur wie Server, Speicher und Netzwerk. Darüber hinaus sind Middleware, Entwicklungstools und andere Dienste enthalten. PaaS unterstützt den vollständigen Lebenszyklus einer Webanwendung: Erstellen, Testen, Bereitstellen, Verwalten und Aktualisieren. PaaS macht das Verwalten von Softwarelizenzen, Middleware und Infrastruktur der Dienste überflüssig. Stattdessen verwalten Sie die von Ihnen entwickelten Anwendungen und Dienste, und der Clouddienstanbieter verwaltet normalerweise alles andere.

### <a name="common-scenarios"></a>Gängige Szenarios

Nehmen wir an, Ihr Unternehmen im Gesundheitswesen benötigt eine Website zur Beschreibung eines Produkts. Ihre Entwickler möchten PHP verwenden. Mit PaaS haben Ihre Entwickler die Möglichkeit, *eine Web-App zu erstellen*. Die Infrastrukturdetails wie z.B. das Erstellen eines virtuellen Computers, Installieren eines Webservers und Installieren von Middleware werden außer Acht gelassen. Sie müssen sich nicht darum kümmern, auf welchem Betriebssystem sie ausgeführt wird, oder welche physische Hardware erforderlich ist. Ihre Entwickler stellen die Websitedateien in der Cloud bereit, und Ihre Website ist im Internet verfügbar.

Nehmen wir ein weiteres Szenario an. Ihr Unternehmen benötigt eine SQL-Datenbank, um Datenanalysten bei einem bestimmten Projekt zu unterstützen. Sie haben keine geeignete Infrastruktur, um der Anforderung gerecht zu werden. Sie können schnell eine SQL Server-Instanz in der Cloud bereitstellen, die dem Bedarf des Projekts entspricht. Die Datenanalysten können eine Verbindung mit dem Server herstellen. Die SQL Server-Datenbank wird als Dienst bereitgestellt. Darum müssen Sie sich über Updates, Sicherheitspatches oder das Optimieren des physischen Speichers für Lese- und Schreibvorgänge keine Gedanken zu machen.

Andere häufige Szenarios sind:

**Entwicklungsframework:** PaaS bietet ein Framework, das Entwickler als Basis zum Entwickeln oder Anpassen cloudbasierter Anwendungen nutzen können. Ähnlich wie beim Erstellen eines Excel-Makros ermöglicht PaaS Entwicklern, Anwendungen mit integrierten Softwarekomponenten zu erstellen. Cloudfeatures wie Skalierbarkeit, hohe Verfügbarkeit und Mehrinstanzenfähigkeit sind enthalten und reduzieren den Programmieraufwand der Entwickler.

**Analyse oder Business Intelligence:** Mit als Dienst bereitgestellten Analysetools können Sie Daten analysieren und extrahieren. Organisationen können Einblicke und Muster finden, um Ergebnisse vorherzusagen und so Prognosen, Entscheidungen zu Produktentwürfen, Renditen und andere geschäftliche Entscheidungen zu verbessern.

### <a name="advantages"></a>Vorteile

Durch die Bereitstellung von Infrastruktur als Dienst bietet PaaS ähnliche Vorteile wie IaaS. Aber die zusätzlichen Features von PaaS einschließlich Middleware, Entwicklungstools und anderer Unternehmenstools bieten zusätzliche Vorteile:

**Geringere Entwicklungszeit:** PaaS-Entwicklungstools können die Entwicklungszeit für neue Anwendungen verkürzen. Entwickler können in die Plattform integrierte vorab programmierte Anwendungskomponenten wie Workflow, Verzeichnisdienste, Sicherheitsfeatures und Suche verwenden. „Platform-as-a-Service“-Komponenten können Ihrem Entwicklungsteam zu neuen Fähigkeiten verhelfen, sodass Sie keine zusätzlichen Mitarbeiter mit entsprechenden Qualifikationen einstellen müssen.

**Entwickeln für mehrere Plattformen:** Einige Dienstanbieter bieten Ihnen Entwicklungsoptionen für mehrere Plattformen wie Desktop, mobile Geräte und Browser, sodass plattformübergreifende Apps schneller und einfacher entwickelt werden können.

**Kostengünstige Nutzung ausgereifter Tools:** Ein nutzungsbasiertes Zahlungsmodell ermöglicht Einzelpersonen oder Organisationen, komplexe Entwicklungssoftware sowie Business Intelligence- und Analysetools zu verwenden, die sie sich absolut nicht leisten könnten.

**Unterstützung geografisch verteilter Entwicklungsteams:** Da der Zugriff auf die Entwicklungsumgebung über das Internet erfolgt, können Entwicklungsteams auch dann an Projekten arbeiten, wenn Teammitglieder sich an Remotestandorten befinden.

**Effiziente Verwaltung des Anwendungslebenszyklus:** PaaS bietet alle Funktionen, die Sie benötigen, um den gesamten Lebenszyklus der Webanwendung zu unterstützen: Erstellen, Testen, Bereitstellen, Verwalten und Aktualisieren innerhalb derselben integrierten Umgebung.

## <a name="saas"></a>SaaS

Software-as-a-Service ermöglicht Benutzern das Herstellen einer Verbindung mit cloudbasierten Apps über das Internet und deren Verwendung. Häufige Beispiele sind E-Mail-, Kalender- und Bürotools wie Microsoft Office 365. SaaS bietet eine umfassende Softwarelösung, die Sie gemäß eines nutzungsabhängigen Zahlungsmodells von einem Clouddienstanbieter erwerben. Sie *mieten* die Verwendung einer Anwendung für Ihre Organisation. Ihre Benutzer stellen über das Internet eine Verbindung mit dem Dienst her, in der Regel mit einem Webbrowser. Alle zugrunde liegenden Komponenten wie Infrastruktur, Middleware, App-Software und App-Daten befinden sich im Rechenzentrum des Dienstanbieters. Der Dienstanbieter verwaltet die Hardware und Software und stellt gemäß der entsprechenden Vereinbarung zum Servicelevel die Verfügbarkeit und Sicherheit sowohl Ihrer App als auch Ihrer Daten sicher. Mit SaaS kann Ihr Unternehmen eine App mit minimalen Investitionskosten schnell bereitstellen.

Wenn Sie einen webbasierten E-Mail-Dienst wie Outlook, Hotmail oder Yahoo! Mail verwendet haben, haben Sie bereits eine Art von SaaS verwendet. Bei diesen Diensten melden Sie sich über das Internet – häufig mittels eines Webbrowsers – bei Ihrem Konto an. Die E-Mail-Software befindet sich im Netzwerk des Dienstanbieters, und Ihre Nachrichten werden dort auch gespeichert. Sie können von einem beliebigen Computer oder dem Internet verbundenen Gerät aus über einen Webbrowser auf Ihre E-Mail und gespeicherten Nachrichten zugreifen.

### <a name="common-scenarios"></a>Gängige Szenarios

Nehmen wir an, Ihr Unternehmen im Gesundheitswesen benötige für sein Vertriebsteam eine Lösung für das Kundenbeziehungsmanagement (Customer Relationship Management, CRM). Das Team ist global. Sie können mittels eines SaaS-CRM-Anbieters schnell eine Lösung für das Vertriebsteam Ihres Unternehmens implementieren.

Für die Nutzung im Unternehmen können Sie Produktivitäts-Apps mieten, z.B. für E-Mail, Zusammenarbeit und Kalenderfunktionen; und anspruchsvolle Unternehmensanwendungen, z.B. für Kundenbeziehungsmanagement (CRM), Unternehmensressourcenplanung (ERP, Enterprise Resource Planning) und Dokumentenverwaltung. Sie bezahlen für die Verwendung dieser Apps gemäß dem Abonnement oder der Nutzungsebene.

### <a name="advantages"></a>Vorteile

**Zugang zu ausgereiften Anwendungen:** Um SaaS-Apps für Benutzer bereitzustellen, müssen Sie keine Hardware, Middleware oder Software erwerben, installieren oder aktualisieren. Mit SaaS sind sogar ausgereifte Unternehmensanwendungen wie ERP und CRM für Unternehmen erschwinglich, die nicht selbst über die Ressourcen zum Erwerben, Bereitstellen und Verwalten der erforderlichen Infrastruktur und Software verfügen.
Sie zahlen nur für wirklich genutzte Ressourcen. Außerdem sparen Sie Geld, da der SaaS-Dienst automatisch gemäß der Nutzungsebene nach oben oder unten skaliert wird.

**Nutzen Sie kostenlose Clientsoftware:** Benutzer können die meisten SaaS-Apps direkt über ihren Webbrowser ausführen, ohne Software herunterladen und installieren zu müssen. Sie müssen keine Clientsoftware für Ihre Benutzer kaufen oder bereitstellen.

**Problemlose Mobilisierung Ihrer Mitarbeiter:** Benutzer können von jedem mit dem Internet verbundenen Computer oder mobilen Gerät aus auf SaaS-Apps und Daten zugreifen. Der Dienstanbieter konzentriert sich auf die Bereitstellung des Diensts für Geräte.

**Zugriff auf App-Daten von beliebigem Ort aus:** Da die Daten in der Cloud gespeichert sind, können Benutzer von jedem mit dem Internet verbundenen Computer oder mobilen Gerät aus auf ihre Informationen zugreifen. Außerdem gehen beim Ausfall von Computer oder Gerät eines Benutzers keine Daten verloren, wenn App-Daten in der Cloud gespeichert werden.