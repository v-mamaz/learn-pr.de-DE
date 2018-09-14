Glückwunsch, Sie haben das Modul zu Leistung und Skalierbarkeit abgeschlossen. Im Folgenden wird zusammengefasst, was Sie gelernt haben:

## <a name="scaling-up-and-scaling-out"></a>Zentrales und horizontales Hochskalieren

- Den Unterschied zwischen dem Hoch- und Herunterskalieren (die Ebene der Ressource, die in einer Instanz bereitgestellt wird) und dem horizontalen Hoch- und Herunterskalieren (die Anzahl der verfügbaren Instanzen erhöhen oder verringern) – hierfür wurden jeweils Beispiele in Azure angeführt.
- Die notwendigen Überlegungen, die angestellt werden müssen, wenn das horizontale Hoch-/Herunterskalieren bei der Zustandsverwaltung und den Startzeiten von Anwendungen eingesetzt wird
- Die automatische Skalierung und wie diese Sie bei der Skalierung der Anzahl von Instanzen nach einem Zeitplan oder dem Verbrauch einer Anwendung unterstützen kann
- Alternative Technologien wurden erläutert, die Sie bei der Skalierbarkeit unterstützen können (einschließlich serverlose Verfahren und Container).

## <a name="optimize-network-performance"></a>Optimieren der Netzwerkleistung

- Als Netzwerklatenz wird die Messung der Verzögerung beim Senden von Daten vom Sender zum Empfänger bezeichnet.
- In einer Cloudumgebung können Anwendungen, die viel kommunizieren, sich im Vergleich zu lokalen Anwendungen auf die Leistung auswirken, da die Ressourcen sich an unterschiedlichen Orten befinden.
- APIs in der Nähe von Endpunkten für Datenbankschreibvorgänge zu positionieren, kann sich positiv auf die Leistung auswirken, da die Netzwerklatenz zwischen den beiden Ressourcen verringert wird.
- Azure Traffic Manager kann verwendet werden, um Benutzer zu der bereitgestellten Instanz mit der niedrigsten Netzwerklatenz weiterzuleiten.
- Azure Content Delivery Network (CDN) kann verwendet werden, um Computevorgänge aus der Hauptanwendung auszulagern und die Ladezeiten der Anwendung zu beschleunigen, indem der Inhalt in einem CDN-Edgeknoten in der Nähe des Benutzers zwischengespeichert wird.

## <a name="optimize-storage-performance"></a>Optimieren der Speicherleistung

- Drei Hauptarten von Datenträgern sind für Infrastructure-as-a-Service-Bereitstellungen (IaaS) verfügbar. HDD SSD Standard-Datenträger (inkonsistente Latenz und geringer Durchsatz), SSD Standard-Datenträger (konsistente Latenz und geringer Durchsatz) und SSD Premium-Datenträger (konsistente Latenz und hoher Durchsatz).
- Das Zwischenspeichern kann in der Anwendungsschicht verwendet werden, um die Ladezeiten einer Anwendung zu verbessern. Häufig angeforderte Informationen können in einem Cache vor der Datenbank gespeichert werden, der die Ladezeiten der am häufigsten angeforderten Informationen dann optimieren kann.
- Sie sollten den entsprechenden Back-End-Datenspeicher für den Auftrag verwenden (mehrsprachige Persistenz), wenn Sie Ihre Lösung erstellen.

## <a name="identify-performance-bottlenecks"></a>Erkennen von Leistungsengpässen

- Setzen Sie sich mit den Anforderungen der Anwendung auseinander, bevor Sie Vorgänge entwerfen oder erstellen.
- Bedenken Sie, dass wirksame DevOps-Strategien Sie beim Erstellen von stabileren und leistungsfähigen Anwendungen unterstützen können.
- Eine Zusammenfassung der in Azure verfügbaren Überwachungsoptionen wurde bereitgestellt, einschließlich Azure Monitor (Bereich für die Überwachung in Azure), Azure Log Analytics (Protokollerfassung und IaaS-Überwachung) und Application Insights (Überwachung der Anwendungsleistung, einschließlich Verfügbarkeit, Leistung und Informationen zu Ausnahmen).
