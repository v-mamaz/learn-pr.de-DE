Endbenutzer erwarten mehr von ihren Anwendungen. Sie erwarten eine besonders hohe Benutzerfreundlichkeit und möchten nicht durch Leistungsprobleme beeinträchtigt werden. Wie lässt sich die Erkennung von Leistungsengpässen in Ihre Architektur integrieren? In dieser Einheit betrachten wir Prozesse und Tools, mit deren Hilfe Sie eine optimale Leistung Ihrer Anwendung sicherstellen und bei Bedarf die Ursache einer Leistungsbeeinträchtigung ermitteln können.

## <a name="importance-of-requirements"></a>Die Bedeutung von Anforderungen

Bevor wir uns über die Leistung unterhalten, sollten wir über Anforderungen sprechen. Theoretisch könnten wir Skalierbarkeit und Leistung ohne Ende immer weiter verbessern. Ab einem bestimmten Punkt wird die Verbesserung jedoch unbezahlbar, schwierig und wirkt sich nicht mehr genügend auf den Geschäftsbetrieb aus. 

Unsere **nicht funktionsbezogenen Anforderungen** helfen uns dabei, diesen Punkt zu finden. Diese speziellen Anforderungen sagen nichts darüber aus, was unsere App *tun* muss. Vielmehr geben sie Aufschluss darüber, welche Qualitätsstufen unsere App erreichen muss. Diese nicht funktionsbezogenen Anforderungen können beispielsweise für folgende Angaben definiert werden:

- Geschwindigkeit, mit der eine Transaktion unter einer gegebenen Last Ergebnisse zurückgeben muss.
- Anzahl gleichzeitiger Verbindungen, die wir unterstützen müssen, bevor ein Fehler zurückgegeben wird.
- Maximale Zeitdauer, für die unsere Anwendung bei einem Serverfehler nicht verfügbar sein darf, bevor eine Sicherung online geschaltet wird.

Es ist wichtig, diese Anforderungen vor dem Erstellen einer Lösung zu definieren, um sicherzustellen, dass die Anwendung die Erwartungen erfüllt, jedoch keinen größeren Aufwand erfordert oder mehr Geld kostet als nötig. Wir können auch unsere Überwachungs- und Betriebsregeln unter Einbeziehung dieser nicht funktionsbezogenen Anforderungen planen. 

Besprechen Sie Anforderungen mit Ihren Projektbeteiligten oder Kunden, dokumentieren Sie sie, und machen Sie sie allgemein bekannt, um sicherzustellen, dass alle wissen, was mit „guter Leistung“ gemeint ist.

## <a name="devops-and-application-performance"></a>DevOps und Anwendungsleistung

Hinter DevOps verbirgt sich die Vorstellung, dass wir keine Entwicklungs- und Infrastruktursilos in unserer Organisation haben. Vielmehr findet eine Zusammenarbeit statt, um Apps in einem optimierten Prozess effektiv zu erstellen, bereitzustellen, zu überwachen und zu verwalten.

Planung, Entwicklung, Tests und Überwachung werden in einem iterativen Ansatz durchgeführt. Die Leistung und Qualität unserer Anwendung werden Teil unseres Softwareentwicklungs-Lebenszyklus und sind nicht mehr nur ein Nebenaspekt bei der Bereitstellung in einer Liveumgebung. In der folgenden Abbildung werden Gelegenheiten für die Zusammenarbeit im Softwareentwicklungs-Lebenszyklus dargestellt.

![Abbildung der als Schleife dargestellten Schritte eines Softwarelebenszyklus, um zu veranschaulichen, wie jede Phase in die jeweils nächste Phase übergreift.](../media/5-devops-cycle.png)

Dieser Ansatz entspricht dem DevOps-Konzept der sogenannten Linksverschiebung. Dieser besagt, dass die Qualitätslenkungsprüfungen früher im Bereitstellungs- und Freigabeprozess erfolgen müssen. Dadurch können Sie Probleme, die sich auf den Endbenutzer auswirken, früher im Prozess auffangen. Da wir in einem fortlaufenden Zyklus arbeiten, begrenzen wir die Anzahl manueller Eingriffe und automatisieren so viel wie möglich. 

Eine Möglichkeit, wie wir die Leistung zu einem Teil unseres DevOps-Prozesses machen können, besteht darin, vor der Bereitstellung in einer Produktionsumgebung Leistungs- oder Auslastungstests durchzuführen, um zu prüfen, ob die Anwendung den nicht funktionsbezogenen Anforderungen entspricht.

Im Idealfall können wir Leistungs- und Auslastungstests in einer Umgebung durchführen, die exakt der Produktionsumgebung entspricht, jedoch keine Auswirkungen auf die eigentlichen Produktionsserver hat. Wenn Sie die Cloud nutzen, haben Sie genau diese Möglichkeit. Sie können die Erstellung einer mit der Produktionsumgebung vergleichbaren Umgebung automatisieren, Tests durchführen und anschließend die Umgebung zerstören, um Kosten zu sparen. Mit diesem Automatisierungsansatz können Sie dafür sorgen, dass Ihre Anwendung nicht nur Ihren aktuellen Anforderungen gewachsen, sondern auch für zukünftiges Wachstum gerüstet ist.

Die Überwachung der Anwendungsleistung wird zum zentralen Teil dieses Ansatzes. Wenn wir Leistungs- und Auslastungstests für unsere Anwendung durchführen oder unsere Produktionsleistung unter Kontrolle halten möchten, müssen wir wissen, welche Teile unserer Anwendung möglicherweise nicht optimal funktionieren. Betrachten wir nun einige Möglichkeiten, die uns hierzu zur Verfügung stehen.

## <a name="performance-monitoring-options-in-azure"></a>Möglichkeiten für die Leistungsüberwachung in Azure

Überwachung ist das Erfassen und Analysieren von Daten, um die Leistung, Integrität und Verfügbarkeit Ihrer Geschäftsanwendung und der jeweiligen Ressourcen zu bestimmen.

Wir möchten darüber informiert werden, ob unsere Anwendung reibungslos ausgeführt wird. Proaktive Benachrichtigungen können verwendet werden, um über kritische Probleme zu informieren, die auftreten können. Es gibt viele Überwachungsebenen, die berücksichtigt werden müssen, in erster Linie die Infrastrukturebene und die Anwendungsebene.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor stellt einen zentralen Verwaltungspunkt für Protokolle auf Infrastrukturebene sowie für die Überwachung der meisten Ihrer Azure-Dienste bereit. Die Lösung erfasst Metriken, Aktivitäts- und Diagnoseprotokolle und vieles mehr. Azure Monitor bietet eine Reihe von Features. Dazu zählen unter anderem folgende:

- Azure-Warnungen, um proaktiv über Verstöße gegen Metriken oder Aktivitäten zu informieren oder entsprechende Maßnahmen zu ergreifen
- Verwendung von Azure-Dashboards, um verschiedene Überwachungsquellen in einer zentralen Ansicht der Anwendung zu vereinen

Azure Monitor ist der Ausgangspunkt für sämtliche Einblicke in Ressourcenmetriken nahezu in Echtzeit. Viele Azure-Ressourcen beginnen nach der Bereitstellung automatisch mit der Ausgabe von Metriken. Azure-Web-App-Instanzen geben beispielsweise Metriken für Compute- und Anwendungsanforderungen aus. Neben VM-Host-Diagnosemetriken werden hier auch Metriken aus Application Insights sortiert. Und auch VM-Gast-Diagnosemetriken werden angezeigt, nachdem Sie sich angemeldet haben.

### <a name="log-analytics"></a>Log Analytics

Mithilfe der zentralen Protokollierung können Sie versteckte Probleme aufdecken, die möglicherweise schwierig aufzuspüren sind. Mit Log Analytics können Sie Daten protokollübergreifend abfragen und aggregieren. Dank dieser quellenübergreifenden Korrelation können Sie Probleme oder Leistungsengpässe erkennen, die bei Betrachtung einzelner Protokolle oder Metriken möglicherweise nicht offensichtlich sind. In der folgenden Abbildung wird veranschaulicht, wie Log Analytics als zentraler Hub für die Datenüberwachung fungiert. Log Analytics empfängt Überwachungsdaten von Ihren Azure-Ressourcen und stellt sie Consumern zur Analyse oder Visualisierung zur Verfügung.

![Abbildung der Rolle von Log Analytics bei der Ressourcenüberwachung.](../media/5-log-analytics.png)

Sie können eine Vielzahl von Datenquellen, Sicherheitsprotokollen, Azure-Aktivitätsprotokollen, Servern, Netzwerken und Anwendungsprotokollen sortieren. Ferner können Sie in Hybridbereitstellungsszenarien lokale System Center Operations Manager-Daten an Log Analytics pushen und dafür sorgen, dass Azure SQL-Datenbank Diagnoseinformationen zur detaillierten Leistungsüberwachung direkt an Log Analytics sendet.

Die zentralisierte Protokollierung kann für die Problembehandlung bei allen Arten von Szenarios, auch bei Leistungsproblemen, extrem vorteilhaft sein. Sie ist ein wichtiger Bestandteil einer guten Überwachungsstrategie für jede Architektur.

## <a name="application-performance-management"></a>Steuerung der Anwendungsleistung

Tiefliegende Anwendungsprobleme sind oft schwierig aufzuspüren. Hier kann die Integration von Telemetrie in eine Anwendung mithilfe einer APM-Lösung (Application Performance Management, Steuerung der Anwendungsleistung) zum Aufspüren schlechter Anwendungsleistung und ungünstigem Anwendungsverhalten vorteilhaft sein. Diese Telemetriedaten können einzelne Seitenanforderungszeiten, Ausnahmen in Ihrer Anwendung und sogar benutzerdefinierte Metriken zur Überwachung von Geschäftslogiken enthalten. Ferner können diese Telemetriedaten eine Fülle von Einblicken in die Abläufe in Ihrer Anwendung bieten.

Bei Azure ist Application Insights ein Dienst, der diese ausführliche Steuerung der Anwendungsleistung ermöglicht. Sie installieren ein kleines Instrumentierungspaket in Ihrer Anwendung und richten eine Application Insights-Ressource im Microsoft Azure-Portal ein. Die Instrumentierung überwacht Ihre App und sendet Telemetriedaten an das Portal.

Telemetriedaten aus Hostumgebungen (etwa Leistungsindikatoren, Azure-Diagnosen und Docker-Protokolle) können erfasst werden. Sie können auch Webtests einrichten, die in regelmäßigen Abständen synthetische Anforderungen an den Webdienst senden. Sie können Ihre Anwendung sogar so konfigurieren, dass benutzerdefinierte Ereignisse und Metriken gesendet werden, die Sie selbst in den Client- oder Servercode schreiben. Beispielsweise anwendungsspezifische Ereignisse wie verkaufte Artikel oder gewonnene Spiele.

Application Insights speichert die eigenen Daten in einem gemeinsamen Repository, und Metriken werden für Azure Monitor freigegeben. Sie können gemeinsame Funktionen wie Warnungen, Dashboards und umfassende Analysen mit der Log Analytics-Abfragesprache nutzen.

Das Muster für die Überwachung der Integrität von Endpunkten ist eine gängige Lösung für die Ermittlung der Verfügbarkeit einer Webanwendung. Es wird zur Überwachung von Webanwendungen und entsprechenden Back-End-Diensten verwendet, um sicherzustellen, dass sie verfügbar sind und einwandfrei funktionieren. Das Muster wird durch Abfragen eines bestimmten URI implementiert. Der Endpunkt überprüft nicht nur die Verfügbarkeit des Front-Ends, sondern auch den Status zahlreicher Komponenten (einschließlich der Back-End-Dienste, von denen die App abhängig ist). Dies dient als Integritätsprüfung auf Dienstebene und gibt Aufschluss über die allgemeine Integrität des Diensts.

Verwenden Sie eine APM-Lösung wie Application Insights, um ausführliche Informationen zu Ihrer Anwendung zu erhalten und Aktivitäten in der gesamten Anwendung zu korrelieren. Diese Lösung kann dabei hilfreich sein, die Funktionsweise einer bestimmten Aktion im Clientbrowser, auf dem Server und in den Downstreamdiensten nachzuvollziehen. Darüber hinaus liefert sie Informationen zu Trends, stellt bei Problemen Benachrichtigungen bereit und hilft beim Aufspüren und Beheben des Problems, bevor Benutzer es bemerken.

## <a name="performance-monitoring-at-lamna-healthcare"></a>Leistungsüberwachung bei Lamna Healthcare

Bei Lamna Healthcare wurde ein webbasiertes Patientenbuchungssystem mit virtuellen Computern und einer Azure SQL-Datenbank in zwei Azure-Regionen implementiert. Es wurde entschieden, zur Überwachung der Leistung der zugrunde liegenden virtuellen Front-End-Computer den VM-Agent und Log Analytics zu verwenden.

Azure Monitor wird verwendet, um Informationen zur Leistung der Azure SQL-Datenbanken abzurufen und wichtige Leistungsmetriken wie prozentuale CPU-Auslastung und Deadlocks zu erfassen.

Application Insights wurde so konfiguriert, dass Informationen zur Verfügbarkeit und Telemetrie erfasst werden. Das Team hat die neue Buchungsfunktion so geändert, dass benutzerdefinierte Telemetriedaten an Application Insights gesendet werden. So verfügt das Team nun über ein Konzept zur Ermittlung von Informationen zum Umfang geschäftlicher Ereignisse und erhält damit bessere Einblicke in die Abläufe der eigenen Anwendung.

Wir haben einige Prozesse, Tools und bewährte Methoden zum Aufspüren von Leistungsproblemen sowie zum Sicherstellen einer optimalen Funktionsweise Ihrer Anwendung betrachtet.