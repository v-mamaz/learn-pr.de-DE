Stellen Sie sich vor, es wurde gerade ein Bericht über die bahnbrechende neue Krebstherapie Ihres Unternehmens veröffentlicht. Dies ist ein großartiger Meilenstein, der zweifellos einen großen Zustrom von Besuchern auf Ihre Website bringen wird. Wird die Website diesen Anstieg des Datenverkehrs bewältigen, oder wird die Last dazu führen, dass die Website langsam wird oder gar nicht mehr reagiert?

Hier betrachten wir einige der Grundprinzipien, um eine hervorragende Anwendungsleistung durch Skalierungs- und Optimierungsprinzipien zu gewährleisten.

## <a name="what-is-scaling-and-performance-optimization"></a>Was versteht man unter Skalierung und Leistungsoptimierung?

Bei der Skalierung und Leistungsoptimierung geht es darum, die für eine Anwendung verfügbaren Ressourcen mit dem Bedarf abzugleichen, den sie empfängt. Die Leistungsoptimierung umfasst die Skalierung von Ressourcen, das Identifizieren und Optimieren potenzieller Engpässe sowie die Optimierung Ihres Anwendungscodes für Spitzenleistung.

### <a name="scaling"></a>Skalierung

Computeressourcen können in zwei verschiedenen Richtungen skaliert werden:

* Zentrales *Hochskalieren* ist die Aktion, bei der einer einzelnen Instanz weitere Ressourcen hinzugefügt werden.
* Horizontales *Hochskalieren* bedeutet das Hinzufügen von Instanzen.

![Abbildung, in der das zentrale Hoch- und Herunterskalieren einer VM zum Steigern der Leistungsfähigkeit veranschaulicht wird.](../media/scale-up-scale-out.png)

Beim zentralen Hochskalieren geht es darum, einer einzelnen Instanz mehr Ressourcen (etwa CPU oder Arbeitsspeicher) hinzuzufügen. Bei dieser Instanz kann es sich um einen virtuellen Computer oder einen PaaS-Dienst handeln. Durch das Hinzufügen von mehr Kapazität zur Instanz werden die für Ihre Anwendung verfügbaren Ressourcen erhöht, aber es gibt eine Einschränkung. Virtuelle Computer sind auf die Kapazität des Hosts eingeschränkt, auf dem sie ausgeführt werden, und die Hosts selbst weisen physische Einschränkungen auf. Wenn Sie eine Instanz zentral hochskalieren, können Sie gelegentlich an diese Grenzen stoßen, was Ihre Möglichkeit einschränkt, der Instanz weitere Ressourcen hinzuzufügen.

Beim horizontalen Hochskalieren geht es darum, einem Dienst zusätzliche Instanzen hinzuzufügen. Dies können virtuelle Computer oder PaaS-Dienste sein, aber anstatt mehr Kapazität hinzuzufügen, indem eine einzelne Instanz leistungsfähiger wird, fügen wir Kapazität hinzu, indem wir die Gesamtzahl der Instanzen erhöhen. Der Vorteil der horizontalen Hochskalierung besteht darin, dass Sie unbegrenzt horizontal hochskalieren können, wenn Sie der Architektur weitere Computer hinzufügen müssen. Horizontales Hochskalieren erfordert eine Art der Lastverteilung. Dies könnte ein Load Balancer sein, der Anforderungen auf die verfügbaren Server verteilt, oder ein Dienstermittlungsmechanismus zum Identifizieren der aktiven Server, an die Anforderungen gesendet werden sollen.

In beiden Fällen können Ressourcen verringert und somit Kosten optimiert werden.

### <a name="performance-optimization"></a>Leistungsoptimierung

Bei der Optimierung der Leistung werden Sie sich mit Netzwerk und Speicher befassen, um sicherzustellen, dass die Leistung akzeptabel ist. Beides kann sich negativ auf die Reaktionszeit der Anwendung auswirken. Die Auswahl der richtigen Netzwerk- und Speichertechnologien für Ihre Architektur wird Ihnen helfen, sicherzustellen, dass Sie Ihren Kunden das beste Erlebnis bieten.

Für die Leistungsoptimierung müssen Sie auch verstehen, wie die Anwendungen selbst ausgeführt werden. Fehler, schlechter Code und Engpässe in abhängigen Systemen können durch ein Tool zur Steuerung der Anwendungsleistung aufgedeckt werden. Diese Probleme bleiben den Endbenutzern, Entwicklern und Administratoren häufig verborgen, können sich aber nachteilig auf die Gesamtleistung Ihrer Anwendung auswirken.

## <a name="scalability-and-performance-patterns-and-practices"></a>Muster und Verfahren für Skalierbarkeit und Leistung

Sehen wir uns einige Muster und Verfahren an, mit denen Sie die Skalierbarkeit und Leistung Ihrer Anwendung verbessern können.

### <a name="data-partitioning"></a>Datenpartitionierung

In vielen umfangreichen Lösungen werden Daten in separate Partitionen aufgeteilt, die getrennt verwaltet werden können und auf die separat zugegriffen werden kann. Die Partitionierungsstrategie muss sorgfältig ausgewählt werden, um die Vorteile zu maximieren und gleichzeitig nachteilige Auswirkungen zu minimieren. Partitionierung kann die Skalierbarkeit verbessern, Konflikte reduzieren und die Leistung optimieren.

### <a name="caching"></a>Caching

Die Verwendung von Caching in Ihrer Architektur kann die Leistung verbessern. Caching ist ein Mechanismus zum Speichern von häufig verwendeten Daten oder Objekten (Webseiten, Bilder), um diese schneller abrufen zu können. Caching kann auf verschiedenen Ebenen Ihrer Anwendung verwendet werden. Sie können Caching zwischen Ihren Anwendungsservern und einer Datenbank verwenden, um die für den Datenabruf benötigte Zeit zu verringern. Sie können auch Caching zwischen Ihren Endbenutzern und Ihren Webservern verwenden, indem Sie statische Inhalte näher am Benutzer platzieren und die Zeit verkürzen, die benötigt wird, um Webseiten an den Endbenutzer zurückzugeben. Darüber hinaus werden dadurch Anforderungen von Ihrer Datenbank oder Ihren Webservern ausgelagert, sodass sich die Leistung für andere Anforderungen erhöht.

### <a name="autoscaling"></a>Automatische Skalierung

Die automatische Skalierung ist der Prozess zum dynamischen Zuweisen von Ressourcen gemäß den jeweiligen Leistungsanforderungen. Wenn das Arbeitsvolumen zunimmt, sind für eine Anwendung ggf. zusätzliche Ressourcen erforderlich, um die gewünschten Leistungsebenen aufrechtzuerhalten und die Vereinbarungen zum Servicelevel (SLAs) einzuhalten. Wenn die Nachfrage abnimmt und die zusätzlichen Ressourcen nicht mehr benötigt werden, kann die Zuordnung aufgehoben werden, um Kosten zu sparen.

Die automatische Skalierung nutzt die Elastizität von Umgebungen, die in der Cloud gehostet werden, und reduziert gleichzeitig den Verwaltungsaufwand. Die Leistung des Systems muss nicht ständig von einem Bediener überwacht werden, um zu entscheiden, ob Ressourcen hinzugefügt oder entfernt werden müssen.

### <a name="decouple-resource-intensive-tasks-as-background-jobs"></a>Entkoppeln ressourcenintensiver Aufgaben als Hintergrundaufträge

Viele Arten von Anwendungen benötigen Hintergrundaufgaben, die unabhängig von der Benutzeroberfläche (UI) ausgeführt werden. Beispiele hierfür sind Batchaufträge, rechenintensive Aufgaben und langwierige Prozesse wie Workflows. Hintergrundaufträge können ohne Benutzerinteraktion ausgeführt werden. Die Anwendung kann den Auftrag starten und dann mit der Verarbeitung interaktiver Benutzeranforderungen fortfahren. Damit kann die Arbeitsauslastung der Anwendungsbenutzeroberfläche minimiert werden, was zu einer höheren Verfügbarkeit und zu kürzeren interaktiven Antwortzeiten beitragen kann.

### <a name="use-a-messaging-layer-between-services"></a>Verwenden einer Messagingebene zwischen Diensten

Das Hinzufügen einer Messagingebene zwischen Diensten kann sich positiv auf die Leistung und Skalierbarkeit auswirken. Beim Hinzufügen einer Messagingebene wird ein Puffer für Anforderungen zwischen den Diensten erstellt, damit Anforderungen weiterhin ohne Fehler eingehen können, auch wenn die Anwendung überlastet ist. Die Anforderungen werden von der Anwendung in der Reihenfolge beantwortet, in der sie empfangen wurden.

### <a name="implement-scale-units"></a>Implementieren von Skalierungseinheiten

Skalieren Sie ganze Einheiten. Bestimmen Sie für jede Ressource die Auswirkungen, die eine Skalierungsaktivität auf abhängige Systeme haben kann. Dies erleichtert die Anwendung horizontaler Skalierungsvorgänge und ist weniger anfällig für negative Auswirkungen auf die Anwendung. Zum Beispiel kann das Hinzufügen von x Web- und Workerrollen möglicherweise y zusätzliche Warteschlangen und z Speicherkonten erforderlich machen, um die durch die Rollen generierte Workload zu bewältigen. Eine Skalierungseinheit kann aus x Web- und Workerrollen, y Warteschlangen und z Speicherkonten bestehen. Fügen Sie Skalierungseinheiten hinzu, um eine problemlose Skalierung der Anwendung zu ermöglichen.

### <a name="performance-monitoring"></a>Leistungsüberwachung

Verteilte Anwendungen und Dienste in der Cloud sind naturgemäß komplexe Softwarekomponenten mit zahlreichen Variablen. In einer Produktionsumgebung sollten Sie unbedingt nachvollziehen können, auf welche Weise Benutzer Ihr System verwenden. Ferner müssen Sie in der Lage sein, die Ressourcennutzung nachzuverfolgen und allgemein die Integrität und Leistung des Systems zu überwachen. Diese Informationen dienen als Diagnosehilfe, um vorhandene Probleme zu erkennen und zu korrigieren und potenziellen Problemen vorzubeugen.

Überprüfen Sie alle Ebenen Ihrer Anwendung, und identifizieren und beheben Sie Leistungsengpässe in Ihrer Anwendung. Bei diesen Engpässen kann es sich beispielsweise um eine mangelhafte Arbeitsspeicherverwaltung in Ihrer Anwendung oder sogar um den Prozess zum Hinzufügen von Indizes zu Ihrer Datenbank handeln. Dabei kann es durchaus vorkommen, dass Sie nach der Beseitigung eines Engpasses einen weiteren entdecken, von dem Sie bislang gar nichts wussten.

Mit einem sorgfältig ausgearbeiteten Leistungsüberwachungskonzept können Sie ermitteln, welche Muster und Verfahren für Ihre Architektur von Vorteil sind.