Sicherungen sind die letzte und leistungsstärkste Verteidigung gegen dauerhaften Datenverlust. Eine effektive Sicherungsstrategie ist erforderlich, mehr als nur Kopien von Daten. Data-Architektur und die Infrastruktur der Anwendung berücksichtigt werden muss. Die Verwaltung Ihrer app kann viele Arten von Daten für unterschiedliche Bedeutung, häufig auf Dateisysteme, Datenbanken und anderen Speicherdiensten sowohl in der Cloud und lokal verteilt. Indem Sie die richtigen Dienste und Produkte für den Auftrag verwenden, wird Ihr Sicherungsprozess vereinfacht und die Wiederherstellungszeit erhöht, falls eine Sicherung wiederhergestellt werden muss.

## <a name="establish-backup-and-restoration-requirements"></a>Ermitteln der Sicherungs- und Wiederherstellungsanforderungen

Wie bei einer Strategie zur Notfallwiederherstellung auch, basieren die Sicherungsanforderungen auf einer Kosten-Nutzen-Analyse. Analyse von Ihrer app Daten sollten durch die relative Bedeutung der verschiedenen Kategorien von Daten von die app verwaltet wird, sowie externe Anforderungen, wie z. B. datenaufbewahrung Gesetze geführt.

Ermitteln Sie die Sicherungsanforderungen Ihrer App, indem Sie eine Bestandsaufnahme für die Daten Ihrer Anwendung und eine anschließende Analyse durchführen, um diese anhand der folgenden Anforderungen zu gruppieren:

* Anteil des zulässigen Verlustanteils für einen Datentyp (nach Dauer)
* Gewünschte maximale Dauer der Wiederherstellung dieses Datentyps
* Sichern Sie die Aufbewahrungsrichtlinie zu erfüllen: wie viel Zeit und wie häufig Sicherungen müssen zur Verfügung stehen

Diese Konzepte zuordnen sauber in die Konzepte der Recovery Point Objective und Recovery Time Objective (RPO und RTO-Wert). Die Dauer des zulässigen Verlusts kann normalerweise direkt in die erforderlichen Sicherungsintervalle und den RPO-Wert übersetzt werden. Die maximale Dauer einer Wiederherstellung entspricht dem RTO-Wert für die Datenkomponente Ihrer Anwendung. Beide Anforderungen sollten relativ zu die Kosten für das erreichen sie entwickelt werden. Jedes Unternehmen würde gerne sagen, dass sie wirklich leisten können nicht *alle* Daten, aber häufig, die nicht der Fall ist, wenn die Kosten für das erreichen diese Anforderung gilt.

Sicherungen spielen bei der Notfallwiederherstellung auf jeden Fall eine Rolle, aber Sicherungen, Wiederherstellungen und die damit verbundenen Szenarien gehen über den Umfang der Notfallwiederherstellung hinaus. Sicherungen müssen in nicht-Notfallsituationen, einschließlich der wiederhergestellt werden, in denen RTO und RPO von großer Wichtigkeit sind nicht. Beispielsweise wenn eine kleine Menge von Daten, die älter sind als Ihre Intervall für die Sicherung beschädigt oder gelöscht wird, aber die Anwendung nicht zu Ausfallzeiten kommen, wird Ihre Anwendung möglicherweise nie Gefahr, dass er fehlt der SLA und eine erfolgreiche Wiederherstellung führt keine Daten verloren gehen. Ihr Plan für die Notfallwiederherstellung kann auch eine Anleitung für die Durchführung von Wiederherstellungen in anderen Situationen als Notfallsituationen enthalten.

> [!TIP]
> Verwechseln Sie nicht die Begriffe *Archivierung*, *Replikation* und *Sicherung*. Archivierung ist die Speicherung von Daten für die langfristige Beibehaltung als auch Lesezugriff besteht. Die Replikation ist das nahezu in Echtzeit-Kopieren von Daten zwischen Replikaten auf hohe Verfügbarkeit zu unterstützen und bestimmte Szenarien für die notfallwiederherstellung. Einige Voraussetzungen, z. B. datenaufbewahrung Gesetze, können Ihre Strategien für alle drei dieser Aspekte beeinflussen. Archivierung, müssen Sie Replikation und Sicherung alle separate Analyse und Implementierung.

## <a name="azure-backup-and-restore-capabilities"></a>Azure-Sicherungs- und -Wiederherstellungsfunktionen

Azure verfügt über mehrere sicherungsbezogene Dienste und Features für unterschiedliche Szenarien, z.B. Daten in Azure und lokale Daten. Die meisten Azure-Dienste umfassen eine Sicherungsfunktion. Hier sind einige der beliebtesten sicherungsbezogenen Azure-Angebote beschrieben.

### <a name="azure-backup"></a>Azure Backup

Bei Azure Backup handelt es sich um eine Familie von Sicherungsprodukten, mit denen Daten in Azure Recovery Services-Tresoren für die Speicherung und Wiederherstellung gesichert werden. Recovery Services-Tresore sind Speicherressourcen in Azure, die zum Speichern von Daten- und Konfigurationssicherungen für virtuelle Computer, Server und einzelne Arbeitsstationen und Workloads dienen.

> [!NOTE]
> Sowohl für Azure Backup als auch für Azure Site Recovery werden Azure Recovery Services-Tresore für die Speicherung verwendet. Azure Backup ist eine allgemeine sicherungslösung. Azure Site Recovery kann koordiniert Replikation und Failover und Unterstützung niedrige RPO- und RTO-Disaster-Recovery-Vorgänge.

Azure Backup dient als allgemeine Sicherungslösung für Workflows in der Cloud und lokal, die auf VMs oder physischen Servern ausgeführt werden. Der Dienst ist als Ersatz für herkömmliche Sicherungslösungen konzipiert, und die Daten werden in Azure gespeichert, anstatt auf Archivierungsbändern oder anderen lokalen physischen Medien.

Für vier unterschiedliche Produkte und Dienste kann Azure Backup zum Erstellen von Sicherungen verwendet werden:

* **Azure Backup-Agent** ist eine kleine Windows-Anwendung, die Dateien, Ordnern und Systemstatus gesichert, aus der Windows virtuellen Computer oder Server, auf dem er installiert ist. Dies funktioniert auf eine Weise, die viele Consumer cloudbasierte sicherungslösungen ähnelt, aber erfordert die Konfiguration von einem Azure Recovery-Tresor. Nachdem Sie die Anwendung heruntergeladen und auf einem Windows-Server oder virtuellen Computer installiert haben, können Sie sie konfigurieren, um bis zu drei Sicherungen pro Tag zu erstellen.
* **System Center Data Protection Manager** ist ein robustes Sicherungs- und Wiederherstellungssystem mit vollem Funktionsumfang, das für Unternehmen geeignet ist. Data Protection Manager ist eine Windows Server-Anwendung, die Dateisysteme und virtuelle Computer (Windows und Linux) sichern, bare-Metal-Sicherungen von physischen Servern zu erstellen und anwendungsbezogene Sicherung von vielen Microsoft-Serverprodukten, z. B. SQL ausführen können Server und Exchange. Data Protection Manager ist Teil der System Center-Produktfamilie lizenziert und verkauft, die mit System Center allerdings gilt dies Teil der Azure Backup-Produktfamilie, da es Sicherungen in einem Azure Recovery-Tresor gespeichert werden kann.
* **Azure Backup Server** ähnlich Data Protection Manager, aber sie ist als Teil eines Azure-Abonnements lizenziert ist, und erfordert keine System Center-Lizenz. Azure Backup Server unterstützt die gleiche Funktionalität wie Data Protection Manager, mit Ausnahme von lokalen bandsicherung und Integration mit anderen System Center-Produkte.
* **Azure IaaS-VM-Sicherung** ist ein nutzungsbereites Sicherungs- und Wiederherstellungsfeature von Azure Virtual Machines. VM-Sicherung unterstützt einmal täglich Sicherungen für Windows und Linux-Computer. Es unterstützt die Wiederherstellung der einzelnen Dateien vollen Festplatten und gesamte VMs, und kann auch mit der anwendungskonsistente Sicherungen ausführen. Einzelne Anwendungen können Sicherungsvorgänge aufmerksam gemacht werden und die Dateisystem-Ressourcen in einem konsistenten Zustand zu erhalten, bevor die Momentaufnahme erstellt wird.

![Azure Backup](../media/azure-backup.png)

Azure Backup kann den Nutzen erhöhen und einen Beitrag zur Sicherungs- und Wiederherstellungsstrategie für IaaS- und lokale Anwendungen nahezu jeder Größe und Form leisten.

### <a name="azure-blob-storage"></a>Azure-Blobspeicher

Azure Storage eine automatische Sicherungsfunktion beinhaltet keine, aber die Blobs dienen meist so sichern Sie alle Arten von Daten aus verschiedenen Quellen. Für viele Dienste mit Sicherungsfunktionen werden Blobs genutzt, um die Daten zu speichern, und Blobs sind auch ein häufiges Ziel für Skripts und Tools bei allen Arten von Sicherungsszenarien.

Speicherkonten vom Typ „Allgemein, Version 2“ unterstützen drei verschiedene Blobspeicherebenen mit unterschiedlichen Leistungs- und Kostenaspekten. **"Cool"** Storage bietet die beste Kosten-Leistungs-Verhältnis für die meisten Sicherungen, im Gegensatz zu **"Hot"** -Speicherung, bietet geringerer Zugriff Kosten, aber höhere Speicherkosten. **Archiv**-Tarifs eignet sich möglicherweise dafür sekundäre oder Sicherungen von Daten mit niedriger Erwartungen für die Wiederherstellungszeit. Es ist in die Kosten niedrig, erfordert jedoch bis zu 15 Stunden Vorlaufzeit zugreifen.

Unveränderlicher Blobspeicher kann für ein vom Benutzer angegebenes Intervall als nicht löschbar und nicht änderbar konfiguriert werden. Unveränderlicher blobspeicher soll in erster Linie strenge Anforderungen für bestimmte Arten von Daten, z. B. finanzielle Daten zu erfüllen. Es ist eine hervorragende Möglichkeit, um sicherzustellen, dass Sicherungen vor versehentlichem Löschen oder Änderungen geschützt sind.

### <a name="azure-sql-database"></a>Azure SQL-Datenbank

Die Funktionalität für umfassende, automatische Sicherungen ist ohne weitere Kosten in Azure SQL-Datenbank enthalten. Wöchentlich werden vollständige Sicherungen erstellt, wobei alle zwölf Stunden differenzielle Sicherungen durchgeführt und alle fünf Minuten Protokollsicherungen erstellt werden. Vom Dienst erstellte Sicherungen können verwendet werden, um für eine Datenbank den Stand zu einem bestimmten Zeitpunkt wiederherzustellen. Dies gilt auch, wenn diese gelöscht wurde. Wiederherstellungen können mit dem Azure-Portal, PowerShell oder der REST-API durchgeführt werden. Sicherungen für Datenbanken, die per Transparent Data Encryption verschlüsselt werden, werden standardmäßig auch verschlüsselt.

SQL-Datenbank-Sicherungen sind für Unternehmen geeignet, produktionsbereit und standardmäßig aktiviert. Wenn Sie eine andere Datenbank-Optionen für eine app bewerten möchten, sollte es als Bestandteil von Kosten-Nutzen-Analyse, sein, da es sich um ein entscheidender Vorteil des Diensts ist. Jede App, für die Azure SQL-Datenbank verwendet wird, sollte diese Option nutzen, indem sie in den Plan für die Notfallwiederherstellung und die Sicherungs- und Wiederherstellungsverfahren eingebunden wird.

### <a name="azure-app-service"></a>Azure App Service

In der Azure App Service Standard und Premium-Tarif gehostete unterstützt sofort einsetzbare geplante und manuelle Sicherungen Webanwendungen. Die Sicherungen umfassen Konfigurations- und Dateiinhalte sowie Inhalte von Datenbanken, die von der App verwendet werden. Außerdem werden einfache Filter zum Ausschließen von Dateien unterstützt. Wiederherstellen diese Vorgänge können ausgeführt werden verschiedene App Service-Instanzen, sodass App Service sichern Sie eine einfache Möglichkeit, eine app-Inhalte in ein anderes zu verschieben.

App Service-Sicherungen sind auf insgesamt 10 GB beschränkt, einschließlich der App- und Datenbankinhalte. Sie stellen eine gute Lösung für neue Apps, die gerade entwickelt werden, sowie für kleinere Apps dar. Weiter entwickelte Anwendungen nicht in der Regel mit App Service-Sicherung verwendet. Sie werden stattdessen auf robuste Bereitstellung und die rollbackverfahren, Speicherstrategien, die keine Anwendung Datenträgerspeicher verwenden und dedizierten Sicherungsstrategien für Datenbanken und permanenten Speicher verlassen.

## <a name="verify-backups-and-test-restore-procedures"></a>Überprüfen von Sicherungen und Testen von Wiederherstellungsverfahren

Ein Sicherungssystem ist ohne eine Strategie zum Überprüfen von Sicherungen und Testen von Wiederherstellungsverfahren nicht vollständig. Auch wenn Sie eine dedizierte backup-Dienst oder Produkt verwenden, sollten Sie immer noch Dokument und Übungen Wiederherstellungsverfahren, um sicherzustellen, dass sie gut verstanden haben, und geben Sie das System in den erwarteten Status zurück.

Die Strategien zum Überprüfen von Sicherungen variieren und richten sich nach der Art Ihrer Infrastruktur. Möglicherweise möchten die Techniken, z. B. Erstellen einer neuen Bereitstellung der Anwendung, die Sicherung, Wiederherstellung und vergleichen den Status der beiden Instanzen zu berücksichtigen. In vielen Fällen wird diese Technik eng tatsächliche Notfallwiederherstellungsverfahren imitiert. Die einfache Durchführung eines Vergleichs einer Teilmenge der Sicherungsdaten mit den Livedaten direkt nach der Erstellung einer Sicherung ist hierfür ausreichend. Der sicherungsüberprüfung eine gemeinsame Komponente versucht, Wiederherstellen auf alte Sicherungen, um sicherzustellen, dass sie weiterhin verfügbar und betriebsbereit sind und dass das backup-System nicht auf eine Weise geändert hat, die sie nicht kompatible rendert.

Jede Strategie ist besser als das Ergebnis, dass Ihre Sicherungen beschädigt oder unvollständig sind, wenn Sie versuchen, nach einer Notfallsituation die Wiederherstellung durchzuführen.

Eine Sicherungs- und Wiederherstellungsstrategie ist wichtig, um sicherzustellen, dass Ihre Architektur nach dem Verlust oder der Beschädigung von Daten wiederhergestellt werden kann. Überprüfen Sie Ihre Architektur, um Ihre Anforderungen an die Sicherung und Wiederherstellung zu definieren. Azure enthält mehrere Dienste und Features, mit denen Sicherungs- und Wiederherstellungsfunktionen für jede Architektur bereitgestellt werden.
