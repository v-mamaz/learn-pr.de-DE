Häufig kann es vorkommen, dass Sie eine Serie von Datenaktualisierungen gruppieren müssen, da eine Änderung an einem Teil der Daten zu einer Änderung an einem anderen Teil der Daten führt. Mithilfe von Transaktionen können Sie diese Updates gruppieren, sodass bei einem Fehler in einem Ereignis in einer Serie von Aktualisierungen ein Rollback für die gesamte Serie ausgeführt oder diese rückgängig gemacht werden kann. Beispielsweise könnte ein Onlinehändler eine Transaktion für die Aufgabe einer Bestellung zusammen mit einer Zahlungsbestätigung verwenden. Durch die Gruppierung der relevanten Ereignisse wird sichergestellt, dass Sie Ihre Lagerbestände erst verringern, wenn eine Zahlung auf eine zulässige Weise eingegangen ist.

Im Folgenden erfahren Sie mehr über Transaktionen und deren Notwendigkeit für Ihre Daten.

## <a name="what-is-a-transaction"></a>Was ist eine Transaktion?

Eine Transaktion ist eine logische Einheit, die für Datenabrufe oder -aktualisierungen separat ausgeführt wird.

In Bezug auf die Notwendigkeit einer Transaktionsdatenbank müssen Sie sich folgende Frage stellen: Wirkt sich eine Änderung an einem Teil der Daten in Ihrem Dataset auf einen anderen Teil aus? Wenn Ihre Antwort darauf positiv ausfällt, benötigen Sie Transaktionsunterstützung in Ihrem Datenbankdienst.

Transaktionen werden häufig durch eine Gruppe von vier Anforderungen definiert, die als ACID-Garantien bezeichnet werden. ACID steht für „Atomicity, Consistency, Isolation, Durability“ (Unteilbarkeit, Konsistenz, Isolation, Dauerhaftigkeit):

- Unteilbarkeit bedeutet, dass alle Daten aktualisiert werden oder ein Rollback für alle Daten auf den ursprünglichen Zustand ausgeführt wird.
- Konsistenz stellt sicher, dass bei einem Ereignis während der Transaktion die Daten nicht teilweise aktualisiert werden. Die Transaktion wird also konsistent auf die Daten angewendet – oder eben nicht.
- Isolation stellt sicher, dass eine Transaktion nicht durch eine andere Transaktion beeinträchtigt wird.
- Dauerhaftigkeit bedeutet, dass die aufgrund der Transaktion vorgenommenen Änderungen dauerhaft im System gespeichert werden. Daten, für die ein Commit ausgeführt wurde, werden vom System gespeichert, sodass die Daten selbst bei einem Fehler oder Systemneustart in einem ordnungsgemäßen Zustand verfügbar sind.

Wenn eine Datenbank ACID-Garantien aufweist, werden diese Prinzipien auf die Transaktionen angewendet, und Sie können sicher sein, dass Ihre Transaktionen auf konsistente Weise angewendet werden.

## <a name="oltp-vs-olap"></a>OLTP im Vergleich zu OLAP

Transaktionsdatenbanken werden häufig als OLTP-Systeme (Online Transaction Processing) bezeichnet. OLTP-Systeme unterstützen häufig viele Benutzer, haben schnelle Antwortzeiten und verarbeiten große Datenmengen. Sie sind auch hoch verfügbar (d.h. sie haben nur eine äußerst minimale Ausfallzeit) und verarbeiten in der Regel kleine oder relativ einfache Transaktionen.

OLAP-Systeme (Online Analytical Processing) hingegen unterstützen allgemein weniger Benutzer, weisen längere Antwortzeiten und eine geringere Hochverfügbarkeit auf und verarbeiten in der Regel große und komplexe Transaktionen.

OLTP- und OLAP-Systeme werden nicht mehr so häufig verwendet wie in der Vergangenheit, durch den Vergleich können jedoch die Anforderungen Ihrer Anwendung einfacher kategorisiert werden. Dieses Konzept sollte daher auf jeden Fall in Betracht gezogen werden. 

Nachdem Sie sich mit Transaktionen sowie OLTP- und OLAP-Systemen vertraut gemacht haben, sehen Sie sich die einzelnen Datasets im Szenario des Onlinehändlers an, und stellen Sie die Anforderungen für Transaktionen fest.

### <a name="product-catalog-data"></a>Produktkatalogdaten

Produktkatalogdaten sollten in einer Transaktionsdatenbank gespeichert werden. Wenn Benutzer eine Bestellung aufgeben und die Zahlung überprüft wird, sollte der Bestand für den Artikel aktualisiert werden. Gleichermaßen gilt: Wenn die Kreditkarte des Kunden abgelehnt wird, sollte für die Bestellung ein Rollback ausgeführt werden, und der Bestand sollte nicht aktualisiert werden. Für all diese Beziehungen sind Transaktionen erforderlich.

### <a name="photos-and-videos"></a>Fotos und Videos

Für Fotos und Videos in einem Produktkatalog ist keine Transaktionsunterstützung erforderlich. Eine Änderung an einem Foto oder Video ist nur dann erforderlich, wenn eine Aktualisierung vorgenommen wurde oder neue Dateien hinzugefügt wurden. Auch wenn eine Beziehung zwischen dem Bild und den tatsächlichen Produktdaten besteht, ist diese nicht von transaktionaler Beschaffenheit.

### <a name="business-data"></a>Geschäftsdaten

Da alle Daten bei Geschäftsdaten historisch und unveränderlich sind, ist keine Transaktionsunterstützung erforderlich. Die Business Analysten, die mit den Daten arbeiten, stellen ebenfalls spezielle Anforderungen, da sie häufig Aggregate in ihren Abfragen verwenden müssen, um mit den Gesamtsummen von anderen kleineren Datenpunkten arbeiten zu können.

## <a name="summary"></a>Zusammenfassung

Sicherzustellen, dass sich Ihre Daten im richtigen Zustand befinden, ist nicht immer eine einfache Aufgabe. Transaktionen können dahingehend unterstützen, indem sie Datenintegritätsanforderungen für Ihre Daten erzwingen. Wenn die ACID-Prinzipien bei Ihren Daten von Vorteil sind, sollten Sie eine Speicherlösung wählen, die Transaktionen unterstützt.