Ein Onlinehandelsunternehmen verwendet verschiedene Arten von Daten. Jede Art von Daten profitiert von einer anderen Speicherlösung. 

Anwendungsdaten können auf drei Arten klassifiziert werden: strukturiert, teilweise strukturiert und unstrukturiert. Im Folgenden erfahren Sie, wie Sie Ihre Daten klassifizieren, um die passende Speicherlösung auszuwählen.

#### <a name="approaches-to-storing-data-in-the-cloud"></a>Ansätze zum Speichern von Daten in der Cloud

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEuY]

## <a name="structured-data"></a>Strukturierte Daten

Strukturierte Daten sind Daten, die einem bestimmten Schema folgen, sodass alle Daten die gleichen Felder oder Eigenschaften aufweisen. Strukturierte Daten können in einer Datenbanktabelle mit Zeilen und Spalten gespeichert werden. Für strukturierte Daten werden Schlüssel verwendet, um den Zusammenhang zwischen einer Zeile in einer Tabelle und einer anderen Zeile in einer anderen Tabelle anzugeben. Strukturierte Daten werden auch als relationale Daten bezeichnet, da die Datentabelle, die Tabellenfelder und deren eindeutige Beziehung vom Schema der Daten definiert wird.

Strukturierte Daten sind einfach aufgebaut und können problemlos eingegeben, abgefragt und analysiert werden. Alle Daten weisen das gleiche Format auf.

Zu strukturierten Daten zählen beispielsweise Folgende:

- Sensordaten
- Finanzdaten

## <a name="semi-structured-data"></a>Teilweise strukturierte Daten

Teilweise strukturierte Daten sind in geringerem Umfang strukturiert als strukturierte Daten und werden nicht im relationalen Format gespeichert, da die Felder nicht ohne weiteres in Tabellen, Zeilen und Spalten eingefügt werden können. Teilweise strukturierte Daten enthalten Tags, die die Organisation und Hierarchie der Daten angeben. Sie werden auch als nicht relationale oder NoSQL-Daten bezeichnet.

#### <a name="what-is-nosql"></a>Was ist NoSQL?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvd]

Zu teilweise strukturierten Daten zählen beispielsweise Folgende:

- Schlüssel/Wert-Paare
- Diagrammdaten
- JSON-Dateien
- XML-Dateien

## <a name="unstructured-data"></a>Unstrukturierte Daten

Die Organisation von unstrukturierten Daten lässt sich nicht eindeutig bestimmen. Unstrukturierte Daten werden häufig in Dateien übermittelt, z.B. Fotos oder Videos. Die Videodatei selbst hat möglicherweise eine Gesamtstruktur und teilweise strukturierte Metadaten, aber die Daten, die das Video selbst darstellen, sind unstrukturiert. Aus diesem Grund werden Fotos, Videos und andere ähnliche Dateien als unstrukturierte Daten klassifiziert.

Zu unstrukturierten Daten zählen beispielsweise Folgende:

- Mediendateien (z.B. Fotos, Videos und Audiodateien)
- Office-Dateien (z.B. Word-Dokumente)
- Textdateien
- Protokolldateien

Nachdem Sie nun die Unterschiede zwischen den einzelnen Arten von Daten kennengelernt haben, werfen Sie einen Blick auf die Datasets, die in einem Onlinehandelsunternehmen verwendet werden, und klassifizieren Sie diese.

## <a name="product-catalog-data"></a>Produktkatalogdaten

Die Produktkatalogdaten eines Onlinehandelsunternehmens sind relativ strukturiert, da jedes Produkt eine Produkt-SKU, eine Beschreibung, eine Mengenangabe, einen Preis, Größen- und Farboptionen, ein Foto und möglicherweise ein Video umfasst. Diese Daten wirken auf den ersten Blick relational, da sie die gleiche Struktur aufweisen. Wenn Sie jedoch neue Produkte bzw. neue Arten von Produkten einführen, sollten Sie mit der Zeit verschiedene Felder hinzufügen. Stellen Sie sich beispielsweise vor, Sie nehmen neue Tennisschuhe in Ihr Sortiment auf, die über eine Bluetoothfunktion verfügen, mit der Sensordaten von den Schuhen an eine Fitness-App auf dem Smartphone des Benutzers übertragen werden. Dieser Trend scheint mittlerweile immer beliebter zu werden, sodass Sie Kunden in absehbarer Zukunft ermöglichen möchten, nach „bluetoothfähigen“ Schuhen zu filtern. Alle vorhandenen Daten zu Schuhen nun mit der Eigenschaft „Bluetoothfähig“ zu aktualisieren, wäre viel zu aufwändig. Unkomplizierter wäre es hingegen, neuen Schuhen diese Eigenschaft einfach hinzuzufügen.

Durch Hinzufügen der Eigenschaft „Bluetoothfähig“ wären die Daten Ihrer Schuhe nicht mehr homogen, da Sie Unterschiede in das Schema eingeführt hätten. Wenn dies die einzige zu erwartende Ausnahme ist, können Sie die vorhandenen Daten normalisieren, sodass alle Produkte über ein „Bluetoothfähig“-Feld verfügen, um eine strukturierte und relationale Ordnung aufrechtzuerhalten. Wenn dies jedoch nur eines von mehreren speziellen Feldern ist, die Sie in Zukunft unterstützen möchten, dann ist die Klassifizierung der Daten teilweise strukturiert. Die Daten werden durch Tags organisiert, wobei jedes Produkt im Katalog jedoch eindeutige Felder enthalten kann.

Datenklassifizierung: **Teilweise strukturiert**

## <a name="photos-and-videos"></a>Fotos und Videos

Bei den Fotos und Videos, die auf den Produktseiten angezeigt werden, handelt es sich um unstrukturierte Daten. Obwohl Mediendateien Metadaten enthalten können, ist der Text der Mediendatei unstrukturiert.

Datenklassifizierung: **Unstrukturiert**

## <a name="business-data"></a>Geschäftsdaten

Business Analysten möchten in der Regel Business Intelligence-Funktionen implementieren, um Bestandspipelines auszuwerten und Vertriebsdaten zu überprüfen. Um diese Vorgänge auszuführen, müssen Daten aus mehreren Monaten aggregiert und dann abgefragt werden. Aufgrund des Bedarfs, ähnliche Daten zu aggregieren, müssen diese Daten strukturiert werden, damit die Daten der einzelnen Monate miteinander verglichen werden können.

Datenklassifizierung: **Strukturiert**

## <a name="summary"></a>Zusammenfassung

Daten können auf drei Arten klassifiziert werden: strukturiert, teilweise strukturiert und unstrukturiert. Damit Sie Ihre eigenen Daten klassifizieren und die passende Speicherlösung auswählen können, ist ein grundlegendes Verständnis der Unterschiede unabdingbar. 

Zusammenfassend sind strukturierte Daten organisierte Daten, die ohne Weiteres in Zeilen und Spalten in Tabellen eingefügt werden können. Teilweise strukturierte Daten sind zwar ebenfalls organisiert und verfügen über eindeutige Eigenschaften und Werte, weisen jedoch Abweichungen in den Daten auf. Unstrukturierte Daten lassen sich nicht ohne Weiteres in Tabellen einfügen und weisen kein Schema auf.