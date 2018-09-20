Sie haben erfahren, wie Ihre Anwendung durch eine entsprechende Architektur für Hochverfügbarkeit, Notfallwiederherstellung und Sicherungen verfügbar und wiederherstellbar wird. Sehen Sie sich im Folgenden einige der wesentlichen Schlussfolgerungen an.

## <a name="high-availability"></a>Hochverfügbarkeit

- Bei der Hochverfügbarkeit geht es um die Fähigkeit, mit dem Verlust oder der schwerwiegenden Leistungsverschlechterung einer Komponente eines Systems umzugehen.
- Werten Sie Ihre Anwendung für die Hochverfügbarkeit anhand der drei folgenden Schwerpunkte aus:
  - Ihre festgelegte SLA.
  - Die Hochverfügbarkeitsfunktionen Ihrer Anwendung.
  - Die Hochverfügbarkeitsfunktionen von abhängigen Anwendungen.
- Verwenden Sie Verfügbarkeitsgruppen und Verfügbarkeitszonen in Azure, um Hochverfügbarkeit für VM-Workloads bereitzustellen.
- Verwenden Sie Lastenausgleichsdienste wie Azure Traffic Manager, Azure Application Gateway und Azure Load Balancer, um die Auslastung über verfügbare Systeme zu verteilen.
- PaaS-Dienste verfügen über integrierte Hochverfügbarkeit. Nutzen Sie diese Dienste also in Ihrer Architektur, wenn möglich.

## <a name="disaster-recovery"></a>Notfallwiederherstellung

- Bei der Notfallwiederherstellung geht es um *die Wiederherstellung nach schwerwiegenden Ereignissen*, die zu Ausfallzeiten und Datenverlust führen.
- Erstellen Sie einen Notfallwiederherstellungsplan, um die Prozeduren, Aufgaben und Aktivitäten für die Wiederherstellung nach einer Notsituation zu definieren.
- Definieren Sie die RPO (Recovery Point Objective) und die RTO (Recovery Time Objective), um die Notfallwiederherstellungsanforderungen für Ihre Anwendung zu definieren.
- Verwenden Sie Sicherung und Replikation, um Kopien Ihrer Systeme und Daten für die Wiederherstellung bereitzustellen.
- Verwenden Sie Azure Site Recovery für Notfallwiederherstellungsfunktionen für Ihre Anwendung.
- Testen Sie Ihren Notfallwiederherstellungsplan, um Lücken und die Wichtigkeit der Schritte zu ermitteln.

## <a name="backup-and-restore"></a>Sichern und Wiederherstellen

- Verwenden Sie Sicherungsdateien, um Ihre Daten als Teil Ihres Notfallwiederherstellungsplans oder für isolierte Datenverlustszenarios wiederherstellen zu können.
- Verwenden Sie Azure Backup für die vollständige Sicherung von VMs, Dateien, Ordnern und Systemen in einer lokalen Umgebung.
- PaaS-Dienste verfügen häufig über integrierte Sicherungsfunktionen, z.B. Azure SQL-Datenbank und Azure App Service. Nutzen Sie diese Sicherungsfunktionen nach Möglichkeit, und lernen Sie ihre Standardkonfiguration und allgemeinen Funktionen kennen.
- Testen Sie Ihre Wiederherstellungsprozesse und -Vorgänge regelmäßig, um sicherzustellen, dass sie gültig und ausreichend sind.
