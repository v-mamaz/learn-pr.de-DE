Wir habe beschrieben, wie Sie Ihre Anwendung verfügbar und wiederherstellbar machen, indem Sie die Architektur für hochverfügbarkeit, notfallwiederherstellung und Sicherungen. Werfen wir einen Blick auf einige der Hauptargumente.

## <a name="high-availability"></a>Hochverfügbarkeit

- Bei der Hochverfügbarkeit geht es um die Fähigkeit, mit dem Verlust oder der schwerwiegenden Leistungsverschlechterung einer Komponente eines Systems umzugehen.
- Bewerten Sie Ihre Anwendung für hohe Verfügbarkeit durch die Konzentration auf die drei wichtigen Bereichen:
  - Der festgelegten SLA.
  - Die HA-Funktionen der Anwendung.
  - Die Hochverfügbarkeitsfunktionen des abhängigen Anwendungen.
- Verwenden Sie Verfügbarkeitsgruppen und verfügbarkeitszonen in Azure, um hohe Verfügbarkeit für VM-Workloads bereitzustellen.
- Verwenden Sie Lastenausgleich für Dienste, wie z. B. das Laden von Azure Traffic Manager, Azure Application Gateway und Azure Load Balancer verteilen systemübergreifend verfügbar.
- PaaS-Dienste hohe Verfügbarkeit integriert haben, also diese Dienste in Ihrer Architektur nutzen, wenn möglich.

## <a name="disaster-recovery"></a>Notfallwiederherstellung

- Bei der Notfallwiederherstellung geht es um *die Wiederherstellung nach schwerwiegenden Ereignissen*, die zu Ausfallzeiten und Datenverlust führen.
- Erstellen eines Wiederherstellungsplans, um die Prozeduren, Aufgaben und Aktivitäten erforderlich, um die Wiederherstellung im Notfall zu definieren.
- Definieren Sie die RPO und RTO für Ihre Anwendung aus, um zu ermitteln, die Anforderungen bei der Notfallwiederherstellung für Ihre Anwendung.
- Verwenden Sie Sicherung und Replikation, um Kopien Ihrer Systeme und Daten zum Wiederherstellen an bereitzustellen.
- Verwenden Sie Azure Site Recovery für DR-Prozess-Wiederherstellungsfunktionen für Ihre Anwendung ein.
- Testen Sie Ihres Plans zur notfallwiederherstellung zum Identifizieren von Lücken und Relevanz von Schritten an.

## <a name="backup-and-restore"></a>Sichern und Wiederherstellen

- Verwenden Sie Sicherungen zum Wiederherstellen Ihrer Daten als Teil Ihrer Strategie für die Notfallwiederherstellung oder für Szenarien mit isolierter Daten verloren gehen.
- Verwenden Sie Azure Backup, für die vollständige VM-Sicherung, Datei- und ordnersicherung und Sicherung von Systemen in einer lokalen Umgebung.
- Backup-Funktionen sind häufig in PaaS-Dienste wie Azure SQL-Datenbank und Azure App Service integriert. Profitieren Sie von diesen Funktionen nach Möglichkeit, zu verstehen Sie, die Standardkonfiguration und die allgemeinen Funktionen.
- Testen Sie Ihre Wiederherstellung-Prozesse und Verfahren regelmäßig, stellen Sie sicher, dass sie gültig und ausreichend sind.
