Der Onlinehändler, für den Sie arbeiten, möchte demnächst expandieren. Diese Umstellung wird Ihre Kundenbasis und das Transaktionsvolumen vergrößern. Sie müssen sicherstellen, dass Ihre Datenbank für die Erweiterung nach Bedarf vorbereitet ist.

Mit einer Partitionsstrategie stellen Sie sicher, dass Ihre Datenbank bei Bedarf mühelos wachsen und weiterhin effizient Abfragen und Transaktionen durchführen kann.

## <a name="what-is-a-partition-strategy"></a>Was ist eine Partitionsstrategie?

Wenn Sie fortfahren, einem einzelnen Server oder einer einzelne Partition neue Daten hinzuzufügen, wird dort schließlich kein Speicherplatz mehr zur Verfügung stehen. Zur Vorbereitung darauf benötigen Sie eine Partitionierungsstrategie, um statt zentral **horizontal hochzuskalieren**. Horizontales Hochskalieren ermöglicht Ihnen, Ihrer Datenbank weitere Partitionen hinzuzufügen, wenn Ihre Anwendung sie benötigt.

Die Partition und die Strategie zum horizontalen Hochskalieren in Azure Cosmos DB werden vom Partitionsschlüssel gesteuert, einem Wert, den Sie beim Erstellen einer Sammlung festlegen. Sobald der Partitionsschlüssel festgelegt ist, kann er nicht ohne Neuerstellen der Sammlung geändert werden; darum ist die Auswahl des richtigen Partitionsschlüssels eine wichtige Entscheidung, die Sie frühzeitig im Entwicklungsprozess treffen müssen.  

In dieser Einheit erfahren Sie, wie Sie einen Partitionsschlüssel auswählen, der für Ihr Szenario geeignet ist, und Sie nutzen die automatischen Skalierung, die Azure Cosmos DB für Sie erledigen kann.

## <a name="what-is-a-partition-key"></a>Was ist ein Partitionsschlüssel?

Ein Partitionsschlüssel ist der Wert, mit dem Azure Ihre Daten in logische Bereiche organisiert. In diesem Onlinehändlerszenario sind die Werte `userID` und `productId` eine gute Wahl für den Partitionsschlüssel, da dieser eindeutig ist und wahrscheinlich zum Suchen von Datensätzen verwendet wird. `userID` ist eine gute Wahl, da Ihre Anwendung beispielsweise häufig Personalisierungseinstellungen, den Einkaufswagen, den Bestellverlauf und Profilinformationen des Benutzers aufrufen muss. `productId` ist ebenfalls eine gute Wahl, da Ihre Anwendung Lagerbestände, Versandkosten, Farboptionen, Lagerhausstandorte usw. abfragen muss.

Mit einem Partitionsschlüssel sollte versucht werden, Vorgänge in der Datenbank zu verteilen. Durch die Verteilung von Anforderungen können Sie „heiße“ Partitionen vermeiden. Eine „heiße“ Partition ist eine einzelne Partition, die viel mehr Anforderungen als die anderen empfängt, sodass ein Durchsatzengpass auftreten kann. Für Ihre E-Commerce-Anwendung wäre die aktuelle Uhrzeit z.B. als Partitionsschlüssel eine schlechte Wahl, da alle eingehenden Daten an einen einzelnen Partitionsschlüssel gesendet würden. `userID` oder `productId` wäre besser, da alle Benutzer auf Ihrer Website ihre Warenkorb- oder Profilinformationen in etwa mit der gleichen Häufigkeit hinzufügen und aktualisieren würden, wodurch die Lese- und Schreibvorgänge auf alle Benutzer- und Produktpartitionen verteilt würden.

Der Speicherplatz für die Daten, die den einzelnen Partitionsschlüsseln zugeordnet wird, darf nicht 10 GB überschreiten, was der Größe einer physischen Partition in Azure Cosmos DB entspricht. Wenn also Ihr einzelner `userID`- oder `productId`-Datensatz größer als 10 GB sein wird, erwägen Sie stattdessen die Verwendung eines zusammengesetzten Schlüssels, damit die Größe aller Datensätze verringert wird. Ein Beispiel für einen zusammengesetzten Schlüssel wäre `userID-date`, der **Kundenname-08072018** ähneln würde. Mit diesem Ansatz des zusammengesetzten Schlüssels könnten Sie für jeden Tag, an dem ein Benutzer die Website besucht, eine neue Partition erstellen.

## <a name="best-practices"></a>Bewährte Methoden

Wenn Sie versuchen, den richtigen Partitionsschlüssel zu bestimmen und die Lösung nicht offensichtlich ist, helfen Ihnen die folgenden Tipps.

- Sie können einen Partitionsschlüssel auswählen, der eine große Anzahl von Werten aufweist. Je mehr Werte Ihr Partitionsschlüssel aufweist, desto mehr Skalierungsmöglichkeiten haben Sie.
- Um den besten Partitionsschlüssel für eine Workload mit vielen Lesevorgängen zu bestimmen, überprüfen Sie die wichtigsten drei bis fünf Abfragen, die Sie zu verwenden planen. Der am häufigsten in der WHERE-Klausel enthaltene Wert ist ein guter Kandidat für den Partitionsschlüssel.
- Für Workloads mit vielen Schreibvorgängen müssen Sie die Transaktionsanforderungen Ihrer Workload verstehen, da der Partitionsschlüssel der Bereich der Transaktionen mit mehreren Dokumenten ist.
