Manchmal müssen Anwendungen eine Reihe von Datenaktualisierungen gruppieren, da eine Änderung an einem Teil der Daten zu einer Änderung an einem anderen Teil der Daten führt. Mithilfe von Transaktionen können Sie diese Updates gruppieren, sodass bei einem Fehler in einem Ereignis in einer Serie von Aktualisierungen ein Rollback für die gesamte Serie ausgeführt oder diese rückgängig gemacht werden kann. 

Beispielsweise könnte ein Onlinehändler eine Transaktion zum Aufgeben einer Bestellung und Zahlungsbestätigung verwenden. Durch die Gruppierung der verwandten Ereignisse wird sichergestellt, dass Sie Ihre Lagerbestände erst reduzieren, wenn eine Zahlung auf eine zulässige Weise eingegangen ist.

Im Folgenden erfahren Sie mehr über Transaktionen und deren Notwendigkeit für Ihre Daten.

## <a name="what-is-a-transaction"></a>Was ist eine Transaktion?

Eine Transaktion ist eine logische Gruppe von Datenbankvorgängen, die gemeinsam ausgeführt werden.

In Bezug auf die Notwendigkeit von Transaktionen in Ihrer Datenbank müssen Sie sich folgende Frage stellen: Wirkt sich eine Änderung an einem Teil der Daten in Ihrem Dataset auf einen anderen Teil aus? Wenn Ihre Antwort darauf positiv ausfällt, ist die Unterstützung von Transaktionen in Ihrem Datenbankdienst erforderlich.

Transaktionen werden häufig durch vier Anforderungen definiert, die als ACID-Garantien bezeichnet werden. ACID steht für „Atomicity, Consistency, Isolation, Durability“ (Atomarität, Konsistenz, Isolation, Dauerhaftigkeit):

- Atomarität bedeutet, dass entweder alle Vorgänge in der Transaktion ausgeführt werden oder keine von ihnen.
- Konsistenz stellt sicher, dass kein Teil der Daten aus den Aktualisierungen ausgeschlossen wird, wenn etwas während der Transaktion geschieht. Die Transaktion wird im Allgemeinen entweder konsistent oder gar nicht angewendet.
- Isolation stellt sicher, dass eine Transaktion nicht durch eine andere Transaktion beeinträchtigt wird.
- Dauerhaftigkeit bedeutet, dass die aufgrund der Transaktion vorgenommenen Änderungen dauerhaft im System gespeichert werden. Daten, für die ein Commit ausgeführt wurde, werden vom System gespeichert, sodass die Daten selbst bei einem Fehler oder Systemneustart in einem ordnungsgemäßen Zustand verfügbar sind.

Wenn eine Datenbank ACID-Garantien bereitstellt, werden diese Prinzipien einheitlich auf alle Transaktionen angewendet.

## <a name="oltp-vs-olap"></a>OLTP im Vergleich zu OLAP

Transaktionsdatenbanken werden häufig als OLTP-Systeme (Online Transaction Processing) bezeichnet. OLTP-Systeme unterstützen häufig viele Benutzer, haben schnelle Antwortzeiten und verarbeiten große Datenmengen. Sie sind auch hoch verfügbar (d.h. sie haben nur eine äußerst minimale Ausfallzeit) und verarbeiten in der Regel kleine oder relativ einfache Transaktionen.

OLAP-Systeme (Online Analytical Processing) hingegen unterstützen allgemein weniger Benutzer, weisen längere Antwortzeiten und eine geringere Verfügbarkeit auf und verarbeiten in der Regel große und komplexe Transaktionen.

Die Begriffe OLTP und OLAP werden mittlerweile nicht mehr so häufig verwendet wie früher, jedoch ist es einfacher, die Anforderungen Ihrer Anwendung zu kategorisieren, wenn man die Systeme versteht. 

Nachdem Sie sich mit Transaktionen sowie OLTP- und OLAP-Systemen vertraut gemacht haben, sehen Sie sich die einzelnen Datasets in einem Onlinehändlerszenario an, und Sie ermitteln die Notwendigkeit von Transaktionen.

## <a name="product-catalog-data"></a>Produktkatalogdaten

Produktkatalogdaten sollten in einer Transaktionsdatenbank gespeichert werden. Wenn Benutzer eine Bestellung aufgeben und die Zahlung überprüft wird, sollte der Bestand für den Artikel aktualisiert werden. Gleichermaßen gilt: Wenn die Kreditkarte des Kunden abgelehnt wird, sollte für die Bestellung ein Rollback ausgeführt werden, und der Bestand sollte nicht aktualisiert werden. Für all diese Beziehungen sind Transaktionen erforderlich.

## <a name="photos-and-videos"></a>Fotos und Videos

Für Fotos und Videos in einem Produktkatalog ist keine Transaktionsunterstützung erforderlich. Diese Dateien werden nur geändert, wenn ein Update erfolgt oder neue Dateien hinzugefügt werden. Auch wenn eine Beziehung zwischen dem Bild und den tatsächlichen Produktdaten besteht, ist diese nicht von transaktionaler Beschaffenheit.

## <a name="business-data"></a>Geschäftsdaten

Da alle Daten bei Geschäftsdaten historisch und unveränderlich sind, ist keine Transaktionsunterstützung erforderlich. Die Business Analysts, die mit den Daten arbeiten, stellen ebenfalls spezielle Anforderungen, da sie häufig Aggregate in ihren Abfragen verwenden müssen, um mit den Gesamtsummen von anderen kleineren Datenpunkten arbeiten zu können.

## <a name="summary"></a>Zusammenfassung

Sicherzustellen, dass sich Ihre Daten im richtigen Zustand befinden, ist nicht immer eine einfache Aufgabe. Transaktionen können hier nützlich sein, da sie Datenintegritätsanforderungen für Ihre Daten erzwingen. Wählen Sie eine Speicherlösung aus, die Transaktionen unterstützt, wenn Ihre Daten von den ACID-Prinzipien profitieren.