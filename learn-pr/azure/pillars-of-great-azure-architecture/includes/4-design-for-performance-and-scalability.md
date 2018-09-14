Stellen Sie sich vor, es wurde gerade ein Bericht über die bahnbrechende neue Krebstherapie Ihres Unternehmens veröffentlicht. Dies ist ein großartiger Meilenstein, der zweifellos einen großen Zustrom von Besuchern auf Ihre Website bringen wird. Wird die Website diesen Anstieg des Datenverkehrs bewältigen, oder wird die Last dazu führen, dass die Website langsam wird oder gar nicht mehr reagiert?

Hier betrachten wir einige der Grundprinzipien, um eine hervorragende Anwendungsleistung durch Skalierungs- und Optimierungsprinzipien zu gewährleisten.

## <a name="what-is-scaling-and-performance-optimization"></a>Was versteht man unter Skalierung und Leistungsoptimierung?

Bei der Skalierung und Leistungsoptimierung geht es darum, die für eine Anwendung verfügbaren Ressourcen mit dem Bedarf abzugleichen, den sie empfängt. Die Leistungsoptimierung umfasst die Skalierung von Ressourcen, das Identifizieren und Optimieren potenzieller Engpässe sowie die Optimierung Ihres Anwendungscodes für Spitzenleistung.

### <a name="scaling"></a>Skalierung

Computeressourcen können in zwei verschiedenen Richtungen skaliert werden:

* Zentrales *Hochskalieren* ist die Aktion, bei der einer einzelnen Instanz weitere Ressourcen hinzugefügt werden.
* Horizontales *Hochskalieren* bedeutet das Hinzufügen von Instanzen.

![Zentrales Hochskalieren und horizontales Hochskalieren](../media-draft/scale-up-scale-out.png)

Beim zentralen Hochskalieren geht es darum, einer einzelnen Instanz mehr Ressourcen (etwa CPU oder Arbeitsspeicher) hinzuzufügen. Bei dieser Instanz kann es sich um einen virtuellen Computer oder einen PaaS-Dienst handeln. Durch das Hinzufügen von mehr Kapazität zur Instanz werden die für Ihre Anwendung verfügbaren Ressourcen erhöht, aber es gibt eine Einschränkung. Virtuelle Computer sind auf die Kapazität des Hosts eingeschränkt, auf dem sie ausgeführt werden, und die Hosts selbst weisen physische Einschränkungen auf. Wenn Sie eine Instanz zentral hochskalieren, können Sie gelegentlich an diese Grenzen stoßen, was Ihre Möglichkeit einschränkt, der Instanz weitere Ressourcen hinzuzufügen.

Beim horizontalen Hochskalieren geht es darum, einem Dienst zusätzliche Instanzen hinzuzufügen. Dies können virtuelle Computer oder PaaS-Dienste sein, aber anstatt mehr Kapazität hinzuzufügen, indem eine einzelne Instanz leistungsfähiger wird, fügen wir Kapazität hinzu, indem wir die Gesamtzahl der Instanzen erhöhen. Der Vorteil der horizontalen Hochskalierung besteht darin, dass Sie unbegrenzt horizontal hochskalieren können, wenn Sie der Architektur weitere Computer hinzufügen müssen. Horizontales Hochskalieren erfordert eine Art der Lastverteilung. Dies könnte ein Load Balancer sein, der Anforderungen auf die verfügbaren Server verteilt, oder ein Dienstermittlungsmechanismus zum Identifizieren der aktiven Server, an die Anforderungen gesendet werden sollen.

In beiden Fällen können Ressourcen verringert und somit Kosten optimiert werden.

### <a name="performance-optimization"></a>Leistungsoptimierung

Bei der Optimierung der Leistung werden Sie sich mit Netzwerk und Speicher befassen, um sicherzustellen, dass die Leistung akzeptabel ist. Beides kann sich negativ auf die Reaktionszeit der Anwendung auswirken. Die Auswahl der richtigen Netzwerk- und Speichertechnologien für Ihre Architektur wird Ihnen helfen, sicherzustellen, dass Sie Ihren Kunden das beste Erlebnis bieten.

Für die Leistungsoptimierung müssen Sie auch verstehen, wie die Anwendungen selbst ausgeführt werden. Fehler, schlechter Code und Engpässe in abhängigen Systeme können durch ein Tool zur Steuerung der Anwendungsleistung aufgedeckt werden. Häufig bleiben diese Probleme für Endbenutzer, Entwickler und Administratoren verborgen oder verschleiert, können sich aber nachteilig auf die Gesamtleistung Ihrer Anwendung auswirken.

## <a name="scalability-and-performance-best-practices"></a>Bewährte Methoden für Skalierbarkeit und Leistung

Überprüfen Sie alle Ebenen Ihrer Anwendung, und identifizieren und beheben Sie Leistungsengpässe in Ihrer Anwendung. Diese Engpässe können eine schlechte Speicherverwaltung in Ihrer Anwendung oder sogar das Hinzufügen von Indizes in Ihrer Datenbank sein. Es kann ein iterativer Prozess sein, da Sie einen Engpass beseitigen und dann einen anderen entdecken können, von dem Sie nichts wussten.

Die Verwendung von Caching in Ihrer Architektur kann die Leistung verbessern. Caching ist ein Mechanismus zum Speichern von häufig verwendeten Daten oder Objekten (Webseiten, Bilder), um diese schneller abrufen zu können. Caching kann auf verschiedenen Ebenen Ihrer Anwendung verwendet werden. Sie können Caching zwischen Ihren Anwendungsservern und einer Datenbank verwenden, um die für den Datenabruf benötigte Zeit zu verringern. Sie können auch Caching zwischen Ihren Endbenutzern und Ihren Webservern verwenden, indem Sie statische Inhalte näher am Benutzer platzieren und die Zeit verkürzen, die benötigt wird, um Webseiten an den Endbenutzer zurückzugeben. Dies hat auch einen sekundären Effekt, indem eine Entlastung Ihrer Datenbank oder Ihrer Webserver von Anforderungen stattfindet, was die Leistung für andere Anforderungen erhöht.

Es ist nicht ungewöhnlich, dass Legacyanwendungen als eine große Anwendung für mehrere Aufgaben erstellt wurden. Diese Architekturen sind häufig ausschließlich auf zentrales Hochskalieren eingeschränkt und können nicht horizontal hochskaliert werden. In solchen Architekturen sollten Sie darauf achten, Ihre Anwendung zu modernisieren und Dienste voneinander zu entkoppeln. Entkopplung ist der Vorgang, bei dem die wichtigsten Funktionen einer Anwendung in separate Anwendungen zerlegt werden. Nach der Trennung könnte jeder Dienst dann unabhängig voneinander nach Bedarf horizontal hoch- bzw. herunterskaliert werden.

Zusammen mit Entkopplung kann das Hinzufügen einer Messagingebene zwischen Diensten einen Vorteil für die Leistung bedeuten. Das Hinzufügen einer Messagingebene erstellt einen Puffer für Anforderungen zwischen den Diensten, damit Anforderungen ohne Fehler weiterhin eingehen können, wenn die Anwendung überlastet ist. Während die Anwendung die Anforderungen abarbeitet, werden sie in der Reihenfolge beantwortet, in der sie empfangen wurden.

Abhängig von der Architektur gibt es eine Vielzahl von Aspekten, die Sie untersuchen müssen, um die Leistung Ihrer Anwendung zu optimieren. Sie müssen die Leistung Ihrer Anwendung auswerten und nach Bereichen suchen, die möglicherweise nicht optimal funktionieren.
