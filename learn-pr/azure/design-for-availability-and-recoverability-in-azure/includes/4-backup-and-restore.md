Sicherungen sind die letzte und leistungsstärkste Verteidigung gegen dauerhaften Datenverlust. Eine effektive Sicherungsstrategie erfordert mehr als nur das Kopieren von Daten. Sie muss die Datenarchitektur und Infrastruktur Ihrer Anwendung berücksichtigen. Mit Ihrer App werden unter Umständen viele Arten von Daten unterschiedlicher Wichtigkeit verwaltet, die über Dateisysteme, Datenbanken und andere Speicherdienste verteilt sind – in der Cloud und lokal. Indem Sie die richtigen Dienste und Produkte für den Auftrag verwenden, wird Ihr Sicherungsprozess vereinfacht und die Wiederherstellungszeit erhöht, falls eine Sicherung wiederhergestellt werden muss.

## <a name="establish-backup-and-restoration-requirements"></a>Ermitteln der Sicherungs- und Wiederherstellungsanforderungen

Wie bei einer Strategie zur Notfallwiederherstellung auch, basieren die Sicherungsanforderungen auf einer Kosten-Nutzen-Analyse. Die Analyse der Daten Ihrer App sollte sich nach der relativen Wichtigkeit der unterschiedlichen Datenkategorien richten, die von der App verwaltet werden, sowie nach externen Anforderungen, z.B. Gesetzen zur Datenaufbewahrung.

Ermitteln Sie die Sicherungsanforderungen Ihrer App, indem Sie eine Bestandsaufnahme für die Daten Ihrer Anwendung und eine anschließende Analyse durchführen, um diese anhand der folgenden Anforderungen zu gruppieren:

* Anteil des zulässigen Verlustanteils für einen Datentyp (nach Dauer)
* Gewünschte maximale Dauer der Wiederherstellung dieses Datentyps
* Anforderungen zur Aufbewahrung von Sicherungen: Dauer und Häufigkeit der Verfügbarkeit von Sicherungen

Diese Konzepte passen gut zu den Konzepten Recovery Point Objective (RPO) und Recovery Time Objective (RTO). Die Dauer des zulässigen Verlusts kann normalerweise direkt in die erforderlichen Sicherungsintervalle und den RPO-Wert übersetzt werden. Die maximale Dauer einer Wiederherstellung entspricht dem RTO-Wert für die Datenkomponente Ihrer Anwendung. Beide Anforderungen sollten relativ zu den Kosten für deren Erfüllung entwickelt werden. Jede Organisation würde gerne die Aussage treffen, dass *keinerlei* Daten verloren gehen dürfen. Dies ist aber häufig nicht mehr der Fall, wenn die Kosten für die Erfüllung dieser Anforderung betrachtet werden.

Sicherungen spielen bei der Notfallwiederherstellung auf jeden Fall eine Rolle, aber Sicherungen, Wiederherstellungen und die damit verbundenen Szenarien gehen über den Umfang der Notfallwiederherstellung hinaus. Sicherungen müssen unter Umständen auch in anderen Situationen als Notfallsituationen wiederhergestellt werden, z.B. wenn der RTO- und RPO-Wert keine größere Bedeutung haben. Wenn eine kleinere Menge von Daten, die älter als Ihr Sicherungsintervall ist, beschädigt oder gelöscht wird, aber es für die Anwendung nicht zu Ausfallzeit kommt, gilt beispielsweise Folgendes: Für Ihre Anwendung besteht ggf. nicht die Gefahr, dass die SLA-Vorgaben nicht erreicht werden, und eine erfolgreiche Wiederherstellung führt nicht zu einem Verlust von Daten. Ihr Plan für die Notfallwiederherstellung kann auch eine Anleitung für die Durchführung von Wiederherstellungen in anderen Situationen als Notfallsituationen enthalten.

> [!TIP]
> Verwechseln Sie nicht die Begriffe *Archivierung*, *Replikation* und *Sicherung*. Archivierung ist die Speicherung von Daten für die langfristige Aufbewahrung und den Lesezugriff. Replikation ist das Kopieren von Daten zwischen Replikaten nahezu in Echtzeit, um Hochverfügbarkeit und bestimmte Szenarien der Notfallwiederherstellung zu unterstützen. Einige Anforderungen (z.B. Gesetze zur Datenaufbewahrung) können Ihre Strategien für alle drei Anliegen beeinflussen. Archivierung, Replikation und Sicherung erfordern jeweils eine separate Analyse und Implementierung.

## <a name="azure-backup-and-restore-capabilities"></a>Azure-Sicherungs- und -Wiederherstellungsfunktionen

Azure verfügt über mehrere sicherungsbezogene Dienste und Features für unterschiedliche Szenarien, z.B. Daten in Azure und lokale Daten. Die meisten Azure-Dienste umfassen eine Sicherungsfunktion. Hier sind einige der beliebtesten sicherungsbezogenen Azure-Angebote beschrieben.

### <a name="azure-backup"></a>Azure Backup

Bei Azure Backup handelt es sich um eine Familie von Sicherungsprodukten, mit denen Daten in Azure Recovery Services-Tresoren für die Speicherung und Wiederherstellung gesichert werden. Recovery Services-Tresore sind Speicherressourcen in Azure, die zum Speichern von Daten- und Konfigurationssicherungen für virtuelle Computer, Server und einzelne Arbeitsstationen und Workloads dienen.

> [!NOTE]
> Sowohl für Azure Backup als auch für Azure Site Recovery werden Azure Recovery Services-Tresore für die Speicherung verwendet. Azure Backup ist eine allgemeine Sicherungslösung. Mit Azure Site Recovery können Replikationen und Failover koordiniert und Notfallwiederherstellungsvorgänge mit niedrigen RPO- und RTO-Werten unterstützt werden.

Azure Backup dient als allgemeine Sicherungslösung für Workflows in der Cloud und lokal, die auf virtuellen Computern oder physischen Servern ausgeführt werden. Der Dienst ist als Ersatz für herkömmliche Sicherungslösungen konzipiert, und die Daten werden in Azure gespeichert, anstatt auf Archivierungsbändern oder anderen lokalen physischen Medien.

Für vier unterschiedliche Produkte und Dienste kann Azure Backup zum Erstellen von Sicherungen verwendet werden:

* **Azure Backup-Agent** ist eine kleine Windows-Anwendung, mit der Dateien, Ordner und der Systemstatus von dem virtuellen Windows-Computer oder -Server gesichert werden, auf dem die Anwendung installiert ist. Sie funktioniert ähnlich wie viele andere cloudbasierte Sicherungslösungen für Verbraucher, aber es muss ein Azure Recovery-Tresor konfiguriert werden. Nachdem Sie die Anwendung heruntergeladen und auf einem Windows-Server oder virtuellen Computer installiert haben, können Sie sie konfigurieren, um bis zu drei Sicherungen pro Tag zu erstellen.
* **System Center Data Protection Manager** ist ein robustes Sicherungs- und Wiederherstellungssystem mit vollem Funktionsumfang, das für Unternehmen geeignet ist. Data Protection Manager ist eine Windows Server-Anwendung, mit der Dateisysteme und virtuelle Computer (Windows und Linux) gesichert, Bare-Metal-Sicherungen von physischen Servern erstellt und anwendungsabhängige Sicherungen für viele Microsoft-Serverprodukte, z.B. SQL Server und Exchange, durchgeführt werden können. Data Protection Manager ist Teil der System Center-Produktfamilie und wird mit System Center lizenziert und verkauft. Das Produkt wird aber als Teil der Azure Backup-Familie angesehen, da damit Sicherungen in einem Azure Recovery-Tresor gespeichert werden können.
* **Azure Backup Server** ähnelt Data Protection Manager, wird aber im Rahmen eines Azure-Abonnements lizenziert und benötigt keine System Center-Lizenz. Azure Backup Server unterstützt die gleichen Funktionen wie Data Protection Manager, mit Ausnahme der lokalen Bandsicherung und Integration in andere System Center-Produkte.
* **Azure IaaS-VM-Sicherung** ist ein nutzungsbereites Sicherungs- und Wiederherstellungsfeature von Azure Virtual Machines. Für die VM-Sicherung werden Sicherungen für virtuelle Windows- und Linux-Computer ein Mal pro Tag unterstützt. Sie unterstützt die Wiederherstellung einzelner Dateien, vollständiger Datenträger und vollständiger virtueller Computer und kann auch anwendungskonsistente Sicherungen ausführen. Einzelne Anwendungen können für Sicherungsvorgänge aktiviert werden und ihre Dateisystemressourcen in einen konsistenten Zustand versetzen, bevor die Momentaufnahme erstellt wird.

![Azure Backup](../media-draft/azure-backup.png)

Azure Backup kann den Nutzen erhöhen und einen Beitrag zur Sicherungs- und Wiederherstellungsstrategie für IaaS- und lokale Anwendungen nahezu jeder Größe und Form leisten.

### <a name="azure-blob-storage"></a>Azure Blob Storage

Azure Storage enthält kein Feature für automatisierte Sicherungen, aber häufig werden Blobs verwendet, um alle möglichen Arten von Daten aus unterschiedlichen Quellen zu sichern. Für viele Dienste mit Sicherungsfunktionen werden Blobs genutzt, um die Daten zu speichern, und Blobs sind auch ein häufiges Ziel für Skripts und Tools bei allen Arten von Sicherungsszenarien.

Speicherkonten vom Typ „Allgemein v2“ unterstützen drei verschiedene Blobspeicherebenen mit unterschiedlichen Leistungs- und Kostenaspekten. Speicher vom Typ **Cool** (Kalt) bietet für die meisten Sicherungen das beste Preis-Leistungs-Verhältnis, während beim Speicher vom Typ **Hot** (Heiß) die Zugriffskosten niedriger und die Speicherkosten höher sind. Die Speicherebene **Archive** (Archiv) eignet sich ggf. gut für sekundäre Sicherungen oder Sicherungen von Daten mit geringeren Anforderungen in Bezug auf die Wiederherstellungszeit. Die Kosten sind niedrig, die Vorlaufzeit für den Zugriff kann aber bis zu 15 Stunden betragen.

Unveränderlicher Blobspeicher kann für ein vom Benutzer angegebenes Intervall als nicht löschbar und nicht änderbar konfiguriert werden. Unveränderlicher Blobspeicher soll in erster Linie strenge Anforderungen für bestimmte Arten von Daten erfüllen, z.B. für Finanzdaten. Er ist eine gute Option, um sicherzustellen, dass Sicherungen vor versehentlichem Löschen oder Ändern geschützt sind.

### <a name="azure-sql-database"></a>Azure SQL-Datenbank

Die Funktionalität für umfassende, automatische Sicherungen ist ohne weitere Kosten in Azure SQL-Datenbank enthalten. Wöchentlich werden vollständige Sicherungen erstellt, wobei alle zwölf Stunden differenzielle Sicherungen durchgeführt und alle fünf Minuten Protokollsicherungen erstellt werden. Vom Dienst erstellte Sicherungen können verwendet werden, um für eine Datenbank den Stand zu einem bestimmten Zeitpunkt wiederherzustellen. Dies gilt auch, wenn diese gelöscht wurde. Wiederherstellungen können mit dem Azure-Portal, PowerShell oder der REST-API durchgeführt werden. Sicherungen für Datenbanken, die per Transparent Data Encryption verschlüsselt werden, werden standardmäßig auch verschlüsselt.

SQL-Datenbanksicherungen sind für Unternehmen geeignet, produktionsbereit und standardmäßig aktiviert. Wenn Sie unterschiedliche Datenbankoptionen für eine App auswerten, sollte dies in die Kosten-Nutzen-Analyse einfließen, da es für den Dienst einen erheblichen Nutzen darstellt. Jede App, für die Azure SQL-Datenbank verwendet wird, sollte diese Option nutzen, indem sie in den Plan für die Notfallwiederherstellung und die Sicherungs- und Wiederherstellungsverfahren eingebunden wird.

### <a name="azure-app-service"></a>Azure App Service

Webanwendungen, die auf der Standard- und Premium-Ebene von Azure App Service gehostet werden, unterstützen geplante und manuelle Sicherungen, die bereit für die Nutzung sind. Die Sicherungen umfassen Konfigurations- und Dateiinhalte sowie Inhalte von Datenbanken, die von der App verwendet werden. Außerdem werden einfache Filter zum Ausschließen von Dateien unterstützt. Wiederherstellungsvorgänge können auf verschiedene App Service-Instanzen abzielen, sodass App Service-Sicherungen eine einfache Möglichkeit darstellen, um den Inhalt einer App in eine andere App zu verschieben.

App Service-Sicherungen sind auf insgesamt 10 GB beschränkt, einschließlich der App- und Datenbankinhalte. Sie stellen eine gute Lösung für neue Apps, die aktuell entwickelt werden, sowie für kleinere Apps dar. Für ausgereiftere Anwendungen werden im Allgemeinen keine App Service-Sicherungen verwendet. Stattdessen werden robuste Bereitstellungs- und Rollbackverfahren, Speicherstrategien ohne Anwendungsdatenträgerspeicher und dedizierte Sicherungsstrategien für Datenbanken und beständigen Speicher verwendet.

## <a name="verify-backups-and-test-restore-procedures"></a>Überprüfen von Sicherungen und Testen von Wiederherstellungsverfahren

Ein Sicherungssystem ist ohne eine Strategie zum Überprüfen von Sicherungen und Testen von Wiederherstellungsverfahren nicht vollständig. Auch wenn Sie einen dedizierten Sicherungsdienst oder ein entsprechendes Produkt verwenden, sollten Sie Wiederherstellungsverfahren trotzdem dokumentieren und üben. So wird sichergestellt, dass die Verfahren vollständig verinnerlicht werden und das System damit in den erwarteten Zustand zurückversetzt werden kann.

Die Strategien zum Überprüfen von Sicherungen variieren und richten sich nach der Art Ihrer Infrastruktur. Es kann ratsam sein, die Nutzung von bestimmten Verfahren zu erwägen, z.B. die Erstellung einer neuen Bereitstellung der Anwendung, die Wiederherstellung der zugehörigen Sicherung und der Vergleich des Zustands von zwei Instanzen. In vielen Fällen entspricht dieses Verfahren den tatsächlichen Verfahren für die Notfallwiederherstellung. Die einfache Durchführung eines Vergleichs einer Teilmenge der Sicherungsdaten mit den Livedaten direkt nach der Erstellung einer Sicherung ist hierfür ausreichend. Ein häufiger Bestandteil der Sicherungsüberprüfung ist der Versuch, alte Sicherungen wiederherzustellen. So können Sie sich vergewissern, dass diese noch verfügbar und funktionsfähig sind und sich das Sicherungssystem nicht so geändert hat, dass es zu Inkompatibilitäten kommt.

Jede Strategie ist besser als die Erkenntnis, dass Ihre Sicherungen beschädigt oder unvollständig sind, wenn Sie versuchen, nach einer Notfallsituation die Wiederherstellung durchzuführen.

Eine Sicherungs- und Wiederherstellungsstrategie ist wichtig, um sicherzustellen, dass Ihre Architektur nach dem Verlust oder der Beschädigung von Daten wiederhergestellt werden kann. Überprüfen Sie Ihre Architektur, um Ihre Anforderungen an die Sicherung und Wiederherstellung zu definieren. Azure enthält mehrere Dienste und Features, mit denen Sicherungs- und Wiederherstellungsfunktionen für jede Architektur bereitgestellt werden.
