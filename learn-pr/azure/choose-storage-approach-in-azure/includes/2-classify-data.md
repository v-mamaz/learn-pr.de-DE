Ein online-Einzelhandelsunternehmen hat es sich um unterschiedliche Arten von Daten. Jede Art von Daten kann von einer anderen speicherlösung profitieren. 

Daten können in drei verschiedene Arten klassifiziert werden: strukturierten, teilweise strukturierten und unstrukturierten. Hier erfahren Sie, wie Sie Ihre Daten zu klassifizieren, sodass Sie die passende speicherlösung auswählen können.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEuY]

## <a name="structured-data"></a>Strukturierte Daten

Strukturierte Daten sind Daten, die einem bestimmten Schema folgen, sodass alle Daten die gleichen Felder oder Eigenschaften aufweisen. Strukturierte Daten können in einer Datenbanktabelle mit Zeilen und Spalten gespeichert werden. Strukturierte Daten basieren auf Schlüssel an, wie eine Zeile in einer Tabelle beziehen sich auf Daten in einer anderen Zeile einer anderen Tabelle. Strukturierte Daten werden auch als relationale Daten bezeichnet, wie die Daten des Schemas der Tabelle mit Daten, die Felder in der Tabelle, und die klare Beziehung zwischen den beiden definiert.

Strukturierte Daten sind einfach aufgebaut und können problemlos eingegeben, abgefragt und analysiert werden. Alle Daten weisen das gleiche Format auf.

Zu strukturierten Daten zählen beispielsweise Folgende:

- Sensordaten
- Finanzdaten

## <a name="semi-structured-data"></a>Teilweise strukturierte Daten

Teilweise strukturierte Daten ist kleiner als an strukturierten Daten organisiert und werden nicht in einem relationalen Format gespeichert, wie die Felder nicht sauber in Tabellen, Zeilen und Spalten passen. Teilweise strukturierte Daten enthalten Tags, die die Organisation und die Hierarchie der Daten deutlich zu machen. Sie werden auch als nicht relationale oder NoSQL-Daten bezeichnet.

### <a name="what-is-nosql"></a>Was ist eine NoSQL?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvd]

Zu teilweise strukturierten Daten zählen beispielsweise Folgende:

- Schlüssel-Wert-Paare
- Diagrammdaten
- JSON-Dateien
- XML-Dateien

## <a name="unstructured-data"></a>Unstrukturierte Daten

Die Organisation von unstrukturierten Daten ist in der Regel nicht eindeutig. Unstrukturierte Daten werden häufig in Dateien, z. B. Fotos oder Videos übermittelt. Die Videodatei selbst hat möglicherweise eine Gesamtstruktur und teilweise strukturierte Metadaten, aber die Daten, die das Video selbst darstellen, sind unstrukturiert. Aus diesem Grund werden Fotos, Videos und andere ähnliche Dateien als unstrukturierte Daten klassifiziert.

Zu unstrukturierten Daten zählen beispielsweise Folgende:

- Mediendateien (z.B. Fotos, Videos und Audiodateien)
- Office-Dateien (z.B. Word-Dokumente)
- Textdateien
- Protokolldateien

Nun, dass Sie die Unterschiede zwischen jeder Art von Daten kennen, lassen Sie uns betrachten Sie die Datasets, die in einer online-Einzelhandelsunternehmen verwendet, und klassifizieren.

## <a name="product-catalog-data"></a>Produktkatalogdaten

Produktkatalogdaten für eine online-Einzelhandelsunternehmen ist ziemlich Natur, strukturiert, wie jedes Produkt eine Produkt-SKU, eine Beschreibung, eine Menge, einen Preis, Optionen für die Größe, Farboptionen, ein Foto, und möglicherweise ein Video hat. Diese Daten wirken auf den ersten Blick relational, da sie die gleiche Struktur aufweisen. Allerdings, wie Sie neue Produkte oder verschiedene Arten von Produkten einführen, können Sie verschiedene Felder hinzufügen möchten im Laufe der Zeit. Beispielsweise sind neue Tennis Schuhe, die Sie ausführen können Bluetooth-fähigen und Relay-Sensordaten von der Schuh für eine Fitness-app auf das Telefon des Benutzers. Dies scheint ein aufkommender Trend zu sein, und Sie Kunden nach Schuhe "Bluetooth-fähigen" Filtern in der Zukunft aktivieren möchten. Sie möchten nicht wechseln zurück und aktualisieren Ihre vorhandenen Schuh-Daten mit Bluetooth-fähigen-Eigenschaft, möchten Sie einfach sie neue Schuhe hinzuzufügen.

Durch das Hinzufügen der Bluetooth-fähigen-Eigenschaft ist Ihre Schuh Daten nicht mehr homogene, wie Sie die Unterschiede im Schema eingeführt haben. Wenn dies die einzige Ausnahme, die Sie erwarten ist, auftreten, können Sie zurückkehren und die vorhandenen Daten zu normalisieren, damit alle Produkte ein Feld "Bluetooth-fähigen", um eine strukturierte, relationale Organisation verwalten enthalten. Allerdings ist dies nur eine von vielen spezielle Felder, die Ihnen vorschweben in Zukunft unterstützt werden, erfolgt die Klassifizierung der Daten teilweise strukturierte. Die Daten sind nach Tags organisiert, aber jedes Produkt im Katalog kann eindeutige Felder enthalten.

Datenklassifizierung: **Teilweise strukturiert**

## <a name="photos-and-videos"></a>Fotos und Videos

Bei den Fotos und Videos, die auf den Produktseiten angezeigt werden, handelt es sich um unstrukturierte Daten. Obwohl Mediendateien Metadaten enthalten können, ist der Text der Mediendatei unstrukturiert.

Datenklassifizierung: **Unstrukturiert**

## <a name="business-data"></a>Geschäftsdaten

Business Analysten möchten in der Regel Business Intelligence-Funktionen implementieren, um Bestandspipelines auszuwerten und Vertriebsdaten zu überprüfen. Um diese Vorgänge auszuführen, müssen Daten aus mehreren Monaten aggregiert und dann abgefragt werden. Aufgrund der die Notwendigkeit zum Aggregieren von Daten ähnlich müssen diese Daten strukturiert werden, damit, einen Monat mit der nächsten verglichen werden können.

Datenklassifizierung: **Strukturiert**

## <a name="summary"></a>Zusammenfassung

Daten können in drei verschiedene Arten klassifiziert werden: strukturierten, teilweise strukturierten und unstrukturierten. Grundlegendes zu den unterschieden, sodass Sie Ihre eigenen Daten klassifizieren, können helfen Ihnen bei der Auswahl der richtigen speicherlösung. 

Zusammenfassend ist strukturierte Daten organisierte Daten, die ordentlich in Zeilen und Spalten in Tabellen geeignet ist. Teilweise strukturierte Daten sind zwar ebenfalls organisiert und verfügen über eindeutige Eigenschaften und Werte, weisen jedoch Abweichungen in den Daten auf. Unstrukturierte Daten lassen sich nicht ohne Weiteres in Tabellen einfügen und weisen kein Schema auf.