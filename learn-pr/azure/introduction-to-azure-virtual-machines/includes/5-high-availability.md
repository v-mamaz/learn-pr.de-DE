Häufig steht der Erfolg eines Dienstleistungsunternehmens im unmittelbaren Zusammenhang mit den Vereinbarungen zum Servicelevel (SLAs), die das Unternehmen mit seinen Kunden schließt. Ihre Kunden erwarten, dass die von Ihnen bereitgestellten Dienste immer zur Verfügung stehen und ihre Daten sicher aufbewahrt werden. Dies nimmt Microsoft sehr ernst. Azure bietet Tools, mit denen Sie die Verfügbarkeit, Datensicherheit und Überwachung verwalten können, sodass Sie gewiss sein können, dass Ihre Dienste stets für Ihre Kunden verfügbar sind.

Die Verwaltung einer Azure-VM ist nicht auf die Verwaltung des Betriebssystems oder einer Software begrenzt, die auf der VM ausgeführt wird. Es ist hilfreich, zu wissen, welche Dienste Azure bietet, die Dienstverfügbarkeit sicherstellen und die Automatisierung unterstützen. Diese Dienste unterstützen Sie bei der Planung der Business Continuity & Disaster Recovery-Strategie (BCDR) Ihrer Organisationen.

In diesem Artikel wird der Azure-Dienst behandelt, mit dem Sie die VM-Verfügbarkeit verbessern, VM-Verwaltungsaufgaben optimieren und Ihre VM-Daten sichern und schützen können. Definieren wir zunächst einmal die Verfügbarkeit.

## <a name="what-is-availability"></a>Was ist Verfügbarkeit?

Verfügbarkeit ist der Anteil der Zeit, in dem ein Dienst für die Verwendung verfügbar ist.

Nehmen wir an, Sie betreiben eine Website, auf deren Informationen Ihre Kunden jederzeit zugreifen können sollen. Ihre Erwartung bezüglich der Verfügbarkeit des Websitezugriffs liegt somit bei 100 %.

### <a name="why-do-i-need-to-think-about-availability-when-using-azure"></a>Warum muss bei der Verwendung von Azure die Verfügbarkeit berücksichtigt werden?

Azure-VMs werden auf physischen Servern ausgeführt, die in Rechenzentren von Microsoft gehostet werden. Wie bei den meisten physischen Geräten besteht das Risiko eines Ausfalls. Wenn der physische Server ausfällt, fallen auch die auf diesem Server gehosteten virtuellen Computer aus. In diesem Fall migriert Azure die jeweilige VM automatisch zu einem fehlerfreien Hostserver. Diese Selbstreparaturmigration könnte allerdings einige Minuten dauern. In diesem Zeitraum sind die Anwendungen, die auf dieser VM gehostet werden, nicht verfügbar.

Für die VMs können zudem regelmäßige Updates durchgeführt werden, die von Azure selbst initiiert werden. Derartige Wartungsereignisse können sich von Softwareupdates auf Hardwareaufrüstungen erstrecken und sind notwendig, um die Zuverlässigkeit und die Leistung der Plattform zu verbessern. Diese Ereignisse erfolgen in der Regel ohne Beeinträchtigung von Gast-VMs, doch gelegentlich werden die virtuellen Computer zur Ausführung eines Updates oder eines Upgrades neu gestartet.

> [!NOTE]
> Microsoft aktualisiert nicht automatisch das Betriebssystem oder die Software Ihrer VMs. Die gesamte Kontrolle und Zuständigkeit obliegt Ihnen. Der zugrunde liegende Softwarehost und die Hardware werden jedoch in regelmäßigen Abständen gepatcht, um stets Zuverlässigkeit und eine hohe Leistung sicherzustellen.

Um sicherzustellen, dass Ihre Dienste nicht unterbrochen werden, und einen Single Point of Failure zu vermeiden, wird empfohlen, mindestens zwei Instanzen von jeder VM bereitzustellen. Dieses Feature wird als _Verfügbarkeitsgruppe_ bezeichnet.

### <a name="what-is-an-availability-set"></a>Was ist eine Verfügbarkeitsgruppe?

Eine **Verfügbarkeitsgruppe** ist ein logisches Feature, das sicherstellt, dass eine Gruppe von verwandten VMs bereitgestellt wird, damit sie nicht alle einem Single Point of Failure unterliegen und kein Hostbetriebssystemupgrade für alle VMs gleichzeitig im Rechenzentrum durchgeführt wird. VMs, die in einer Verfügbarkeitsgruppe platziert sind, sollten eine identische Gruppe von Funktionen ausführen, und die gleiche Software sollte installiert sein.

> [!TIP]
> Microsoft bietet für VMs mit mehreren Instanzen, die in einer Verfügbarkeitsgruppe bereitgestellt werden, eine Vereinbarung zum Servicelevel (SLA) mit einer Verfügbarkeit externer Konnektivität von 99,95 %. Das bedeutet, dass für die SLA mindestens zwei Instanzen der VM, die innerhalb einer Verfügbarkeitsgruppe bereitgestellt wird, vorhanden sein müssen. 

Sie können über das Azure-Portal im Abschnitt „Notfallwiederherstellung“ Verfügbarkeitsgruppen erstellen. Darüber hinaus können Sie sie mithilfe von Resource Manager-Vorlagen oder Skripterstellungs- oder API-Tools erstellen. Wenn Sie VMs in einer Verfügbarkeitsgruppe platzieren, garantiert Azure, dass diese auf **Fehlerdomänen** und **Updatedomänen** verteilt werden.

#### <a name="what-is-a-fault-domain"></a>Was ist eine Fehlerdomäne?

Eine Fehlerdomäne ist eine logische Gruppe von Hardware in Azure, die eine Stromquelle und einen Netzwerkswitch gemeinsam nutzen. Sie können sich diese als Rack in einem lokalen Rechenzentrum vorstellen. Die ersten beiden VMs in einer Verfügbarkeitsgruppe werden in zwei unterschiedlichen Racks bereitgestellt, um sicherzustellen, dass nur eine VM betroffen ist, wenn das Netzwerk oder die Stromversorgung in einem Rack ausfällt. Fehlerdomänen werden auch für verwaltete Datenträger, die an VMs angefügt sind, definiert.

![Fehlerdomänen](../media-draft/5-fault-domains.png)

#### <a name="what-is-an-update-domain"></a>Was ist eine Updatedomäne?

Eine Updatedomäne ist eine logische Gruppe von Hardware, die zur gleichen Zeit gewartet oder neu gestartet werden kann. Azure platziert automatisch Verfügbarkeitsgruppen in Updatedomänen, um die Auswirkungen zu minimieren, wenn die Azure-Plattform Änderungen am Hostbetriebssystem einführt. Azure verarbeitet anschließend jeweils eine Updatedomäne.

Verfügbarkeitsgruppen stellen ein leistungsstarkes Feature dar, mit dem sichergestellt werden kann, dass die auf Ihren VMs ausgeführten Dienste immer für Ihre Kunden zur Verfügung stehen. Diese sind jedoch nicht zu 100 % vor Ausfällen gefeit. Was geschieht, wenn ein Fehler bei den Daten oder der Software auf der VM selbst auftritt? Hierfür müssten wir auf andere Notfallwiederherstellungs- und Sicherungsmethoden zurückgreifen.

## <a name="failover-across-locations"></a>Failover zwischen Standorten

Sie können Ihre Infrastruktur auch zwischen Standorten replizieren, um regionale Failover durchzuführen. **Azure Site Recovery** (ASR) repliziert Workloads von einem primären Standort zu einem sekundären Standort. Bei einem Ausfall am primären Standort können Sie ein Failover zu einem sekundären Standort ausführen. Durch ein solches Failover können Benutzer ohne Unterbrechung auf Ihre Anwendungen zugreifen. Sie können dann ein Failback zum primären Standort ausführen, sobald dieser wieder betriebsbereit ist. Azure Site Recovery dient zur Replikation von virtuellen oder physischen Computern und sorgt dafür, dass Ihre Workloads bei einem Ausfall weiterhin verfügbar sind.

ASR weist eine Vielzahl von ausgefeilten technischen Features auf, darunter sind jedoch mindestens zwei bedeutende geschäftliche Vorteile zu beachten:

1. Bei ASR kann Azure als Ziel für die Wiederherstellung verwendet werden, wodurch die Kosten für die Verwaltung eines sekundären physischen Rechenzentrums und deren Komplexität wegfallen.

2. ASR macht es unglaublich einfach, Failover im Hinblick auf Wiederherstellungsroutinen zu testen, ohne Produktionsumgebungen zu beeinträchtigen. So können Sie mühelos geplante oder ungeplante Failover testen. Denn ohne diese Tests wäre Ihr Notfallwiederherstellungsplan nicht gut.

Mit ASR können entsprechend Ihres Szenarios einfache oder komplexe Wiederherstellungspläne erstellt werden. Diese können benutzerdefinierte PowerShell-Skripts, Azure Automation-Runbooks oder Schritte für manuelle Eingriffe enthalten. Anhand der Wiederherstellungspläne können Sie Workloads in Azure replizieren, um mühelos neue Möglichkeiten zur Migration zu erschließen, temporäre Bursts in Spitzenzeiten zu verarbeiten oder Entwicklungs- und Testaufgaben für neue Anwendungen durchzuführen.

Azure Site Recovery ist mit Azure-Ressourcen oder Hyper-V, VMware und physischen Server in Ihrer lokalen Infrastruktur kompatibel und kann einen wichtigen Bestandteil der BCDR-Strategie (Business Continuity & Disaster Recovery) Ihrer Organisation einnehmen, indem beim Ausfall des primären Standorts die Replikation, das Failover und die Wiederherstellung von Workloads und Anwendungen orchestriert werden.
