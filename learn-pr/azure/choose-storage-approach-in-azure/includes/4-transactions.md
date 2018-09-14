Anwendungen müssen möglicherweise eine Reihe von Aktualisierungen an den Daten zu gruppieren, da eine Änderung an der ein Teil der Daten benötigt, um eine Änderung auf andere Daten zu erhalten. Mithilfe von Transaktionen können Sie diese Updates gruppieren, sodass bei einem Fehler in einem Ereignis in einer Serie von Aktualisierungen ein Rollback für die gesamte Serie ausgeführt oder diese rückgängig gemacht werden kann. 

Beispielsweise können Sie als ein Onlinehändler eine Transaktion für die Platzierung der eine Bestellung und Zahlung-Überprüfung verwenden. Durch die Gruppierung der relevanten Ereignisse wird sichergestellt, dass Sie Ihre Lagerbestände erst verringern, wenn eine Zahlung auf eine zulässige Weise eingegangen ist.

Hier erfahren Sie, zu Transaktionen und gibt an, ob sie für Ihre Daten erforderlich sind.

## <a name="what-is-a-transaction"></a>Was ist eine Transaktion?

Eine Transaktion ist eine logische Einheit, die für Datenabrufe oder -aktualisierungen separat ausgeführt wird.

Hier ist die Frage, Fragen Sie sich in Bezug auf Transaktionen in der Anwendung verwendet werden sollen: Änderungen an der ein Teil der Daten in Ihrem Dataset wirken sich eine andere? Wenn die Antwort "Ja" lautet, ist Sie Unterstützung für Transaktionen in Ihrem Datenbankdienst erforderlich.

Transaktionen werden häufig durch eine Gruppe von vier Anforderungen definiert, die als ACID-Garantien bezeichnet werden. ACID steht für „Atomicity, Consistency, Isolation, Durability“ (Unteilbarkeit, Konsistenz, Isolation, Dauerhaftigkeit):

- Unteilbarkeit bedeutet, dass entweder alle Daten aktualisiert werden, oder alle Daten auf den ursprünglichen Zustand zurückgesetzt wird.
- Konsistenz stellt sicher, dass ein Teil der Daten aus der Updates ist nicht, wenn etwas eines durch die Transaktion ausgeschlossen passiert. In allen Bereichen wird in die Transaktion konsistent oder gar nicht angewendet werden.
- Isolation stellt sicher, dass eine Transaktion nicht durch eine andere Transaktion beeinträchtigt wird.
- Dauerhaftigkeit bedeutet, dass die aufgrund der Transaktion vorgenommenen Änderungen dauerhaft im System gespeichert werden. Festgeschriebenen Daten werden vom System gespeichert, sodass auch bei Fehler "und" System neu gestartet werden, die Daten in einem ordnungsgemäßen Zustand verfügbar sind.

Wenn eine Datenbank ACID-Garantien bietet, gelten diese Prinzipien für alle Transaktionen auf einheitliche Weise.

## <a name="oltp-vs-olap"></a>OLTP im Vergleich zu OLAP

Transaktionsdatenbanken werden häufig als OLTP-Systeme (Online Transaction Processing) bezeichnet. OLTP-Systeme unterstützen häufig viele Benutzer, haben schnelle Antwortzeiten und verarbeiten große Datenmengen. Sie sind auch hoch verfügbar (d.h. sie haben nur eine äußerst minimale Ausfallzeit) und verarbeiten in der Regel kleine oder relativ einfache Transaktionen.

OLAP-Systeme (Online Analytical Processing) hingegen unterstützen allgemein weniger Benutzer, weisen längere Antwortzeiten und eine geringere Hochverfügbarkeit auf und verarbeiten in der Regel große und komplexe Transaktionen.

Die Begriffe OLTP- und OLAP-werden nicht verwendet, so oft wie sie verwendet werden, aber deren Verständnis es erleichtert, die Anforderungen Ihrer Anwendung zu kategorisieren. 

Nun, da Sie mit der Transaktionen, OLTP und OLAP-vertraut sind, sehen wir uns die einzelnen der Datasets im online-Einzelhandel-Szenario, und die Notwendigkeit, Transaktionen zu bestimmen.

## <a name="product-catalog-data"></a>Produktkatalogdaten

Produktkatalogdaten sollten in einer Transaktionsdatenbank gespeichert werden. Wenn Benutzer eine Bestellung aufgeben und die Zahlung überprüft wird, sollte der Bestand für den Artikel aktualisiert werden. Gleichermaßen gilt: Wenn die Kreditkarte des Kunden abgelehnt wird, sollte für die Bestellung ein Rollback ausgeführt werden, und der Bestand sollte nicht aktualisiert werden. Für all diese Beziehungen sind Transaktionen erforderlich.

## <a name="photos-and-videos"></a>Fotos und Videos

Fotos und Videos in einem Produktkatalog ist keine transaktionsunterstützung erforderlich. Diese Dateien werden geändert, nur, wenn ein Update erfolgt, oder neue Dateien hinzugefügt werden. Auch wenn eine Beziehung zwischen dem Bild und den tatsächlichen Produktdaten besteht, ist diese nicht von transaktionaler Beschaffenheit.

## <a name="business-data"></a>Geschäftsdaten

Für die Geschäftsdaten da alle Daten historische und unveränderlich ist transaktionsunterstützung nicht erforderlich. Die Business Analysten, die mit den Daten arbeiten, stellen ebenfalls spezielle Anforderungen, da sie häufig Aggregate in ihren Abfragen verwenden müssen, um mit den Gesamtsummen von anderen kleineren Datenpunkten arbeiten zu können.

## <a name="summary"></a>Zusammenfassung

Sicherzustellen, dass sich Ihre Daten im richtigen Zustand befinden, ist nicht immer eine einfache Aufgabe. Transaktionen können dahingehend unterstützen, indem sie Datenintegritätsanforderungen für Ihre Daten erzwingen. Wenn Ihre Daten von ACID-Prinzipien Vorteile bietet, wählen Sie eine speicherlösung dar, die Transaktionen unterstützt.