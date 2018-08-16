## <a name="motivation"></a>Motivation

Der online-Händler, denen Sie sich für Pläne, in einen neuen geografischen Bereich und erweitern in der nahen Zukunft arbeiten. Diese Umstellung wird Ihr Kunde Basis- und Transaktion Volume erhöhen. Sie müssen sicherstellen, dass Ihre Datenbank ausgestattet ist, um Erweiterung nach Bedarf zu verarbeiten.

Eine Partitionsstrategie für die stellt sicher, dass Ihre Datenbank vergrößert werden muss, kann zu diesem einfach Zweck und weiterhin effiziente Abfragen und Transaktionen durchzuführen.

## <a name="what-is-a-partition-strategy"></a>Was ist eine Partitionsstrategie?

Wenn Sie einen einzelnen Server oder eine einzelne Partition neue Daten hinzufügen weiterhin, wird es schließlich kein Speicherplatz mehr ausgeführt. Um zur Vorbereitung eine Partitionierungsstrategie für benötigten **horizontal hochskalieren** anstelle von einrichten. Horizontales Skalieren wird auch die horizontale Skalierung bezeichnet, und es kann mehrere Partitionen mit Ihrer Datenbank, wenn Sie Ihre Anwendung benötigt hinzufügen.

Die Partition und den Scale out-Strategie für die in Azure Cosmos DB wird gesteuert, anhand des partitionsschlüssels, der ist ein Wert festgelegt, wenn Sie eine Sammlung erstellen. Sobald der Partitionsschlüssel festgelegt ist, kann es ohne die Auflistung neu zu erstellen, also Auswahl des richtigen partitionsschlüssels eine wichtige Entscheidung, stellen Sie frühzeitig im Entwicklungsprozess geändert werden.  

In dieser Einheit stellen Sie erfahren, wie Sie einen Schlüssel für die Partition auswählen, der für Ihr Szenario geeignet ist, und nutzt die automatische Skalierung, die Azure Cosmos DB für Sie ausführen können.

## <a name="partition-key-basics"></a>Partition Key-Grundlagen

Ein Partitionsschlüssel darstellen, einen Wert in der Datenbank, die häufig abgefragt wird. Daher ist in einem Szenario mit online-Einzelhandel, verwenden den Wert "UserID" oder "ProductID" als Partitionsschlüssel eine gute Wahl. Benutzer-ID ist eine gute Wahl, wie Ihre Anwendung muss häufig zum Abrufen der Einstellungen für ansichtspersonalisierung, Einkaufswagen, Bestellverlauf und Profilinformationen für den Benutzer aus, um nur einige zu nennen. ProductID ist auch eine gute Wahl, wie Ihre Anwendung benötigt werden, zum Abfragen der Lagerbestände, Versandkosten, Farboptionen, Warehouse Speicherorte und vieles mehr.

Partitionsschlüssel sollten versuchen, um Vorgänge auf die Datenbank zu verteilen. Möchten Sie die Verteilung von Anforderungen in dem Bestreben, die hot-Partitionen zu vermeiden. Eine hot Partition ist eine einzelne Partition, die viel mehr Anforderungen als die anderen empfängt und einen Durchsatz-Engpass erstellen. Für Ihre e-Commerce-Anwendung wäre die aktuelle Uhrzeit z. B. eine schlechte Wahl des partitionsschlüssels, da alle eingehenden Daten an einen einzelnen Partitionsschlüssel aufgenommen werden würden. "UserID" oder "ProductID" wäre besser als alle Benutzer auf Ihre Website würde wahrscheinlich hinzufügen und Aktualisieren von ihren Warenkorb oder Profilinformationen zu der gleichen Häufigkeit an, die verteilt die Lesevorgänge und Schreibvorgänge für alle Benutzerpartitionen auf. Ebenso würde Updates auf Produktdaten wahrscheinlich auch relativ gleichmäßig verteilt, "ProductID" eine gute Partition-Key-Auswahl treffen.

Jeder Partitionsschlüssel hat es sich um einen maximalen Speicherplatz von 10 GB, die die Größe einer physischen Partition in Azure Cosmos DB ist. Also, wenn Ihre einzelne Datensatz für "UserID" oder "ProductID" größer als 10 GB sein soll, überlegen Sie stattdessen die Verwendung eines zusammengesetzten Schlüssels, damit jeder Datensatz kleiner ist. Ein Beispiel für einen zusammengesetzten Schlüssel wäre "UserID"-Datum, die wie CustomerName-08072018 aussehen. Dieser Ansatz für zusammengesetzte Schlüssel können Sie eine neue Partition für jeden Tag erstellen Sie ein Benutzer die Site besucht haben.

## <a name="best-practices"></a>Bewährte Methoden

Wenn Sie versuchen, den richtigen Partitionsschlüssel zu bestimmen und die Lösung nicht offensichtlich ist, sind hier einige Tipps zu berücksichtigen.

* Keine Angst dass zu viele partitionsschlüsseln, die weitere Partitionsschlüssel haben die höhere Skalierbarkeit, was man.

* Um den besten Partitionsschlüssel für eine arbeitsauslastung mit vielen Lesevorgängen zu bestimmen, überprüfen Sie die oberen drei bis fünf Abfragen, die Sie planen. Der Wert, der am häufigsten in der WHERE-Klausel enthalten ist ein guter Kandidat für den Partitionsschlüssel.

* Für Workloads mit vielen Schreibvorgängen müssen Sie die transaktionalen Anforderungen Ihrer Workload verstehen, da es sich bei der Partitionsschlüssel des Bereichs der Transaktionen mit mehreren Dokumenten ist.
