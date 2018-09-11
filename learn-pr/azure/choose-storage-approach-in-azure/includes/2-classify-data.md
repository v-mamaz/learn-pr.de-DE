Ein Onlinehandelsunternehmen arbeitet eventuell mit verschiedenen Arten von Daten. Einige Daten wie die Kontaktinformationen von Kunden können strukturiert sein, während andere Daten möglicherweise unstrukturiert sind (z.B. ein Produktbild). Es gibt drei Kategorien von Daten: strukturiert, teilweise strukturiert und unstrukturiert. Für die einzelnen Kategorien von Daten können sich unterschiedliche Speicherlösungen anbieten.

Im Folgenden erfahren Sie, wie Sie Ihre Daten in die entsprechenden Kategorien klassifizieren, um die richtige Speicherlösung auszuwählen.

## <a name="structured-data"></a>Strukturierte Daten

Strukturierte Daten sind Daten, die einem bestimmten Schema folgen, sodass alle Daten die gleichen Felder oder Eigenschaften aufweisen. Strukturierte Daten können in einer Datenbanktabelle mit Zeilen und Spalten gespeichert werden. Mithilfe von Schlüsseln werden strukturierte Daten in einer Zeile einer Tabelle mit verwandten Daten in einer Zeile einer anderen Tabelle verknüpft. Strukturierte Daten werden auch als relationale Daten bezeichnet, da das Schema die Datentabellen, die Felder in den Tabellen und die eindeutige Beziehung zwischen den beiden definiert.

Strukturierte Daten sind einfach aufgebaut und können problemlos eingegeben, abgefragt und analysiert werden, da alle Daten das gleiche Format aufweisen.

Zu strukturierten Daten zählen beispielsweise Folgende:
* Sensordaten
* Finanzdaten

## <a name="semi-structured-data"></a>Teilweise strukturierte Daten

Teilweise strukturierte Daten sind in geringerem Umfang strukturiert als strukturierte Daten und werden nicht in relationalen Datenbanken gespeichert, da die Felder nicht ohne Weiteres in Tabellen, Zeilen und Spalten eingefügt werden können. Teilweise strukturierte Daten enthalten Tags, die die Organisation und Hierarchie der Daten innerhalb der Daten offenlegen.  

Sie werden auch als nicht relationale oder NoSQL-Daten bezeichnet.

Zu teilweise strukturierten Daten zählen beispielsweise Folgende:
* JSON-Dateien
* XML-Dateien

## <a name="unstructured-data"></a>Unstrukturierte Daten

Die Organisation von unstrukturierten Daten lässt sich allein schon, was ihre Form betrifft, in der Regel nicht eindeutig bestimmen. Unstrukturierte Daten werden oft als Dateien (z.B. Fotos oder Videos) bereitgestellt, wobei die Videodatei selbst eine allgemeine Struktur und teilweise strukturierte Metadaten aufweisen kann, die Daten, in denen das Video selbst eingebettet ist, sind jedoch unstrukturiert. Fotos, Videos und andere vergleichbare Dateien werden daher als unstrukturierte Daten klassifiziert.

Zu unstrukturierten Daten zählen beispielsweise Folgende:
* Mediendateien (z.B. Fotos, Videos und Audiodateien)
* Office-Dateien (z.B. Word-Dokumente)
* Textdateien
* Protokolldateien

Nachdem Sie nun die Unterschiede zwischen den einzelnen Arten von Daten kennengelernt haben, werfen wir einen Blick auf die Datasets, die in einer Onlinehandels-App verwendet werden, und klassifizieren diese.

### <a name="product-catalog-data"></a>Produktkatalogdaten

Die Produktkatalogdaten eines Onlinehändlers sind relativ strukturiert, da jedes Produkt eine Produkt-SKU, eine Beschreibung, eine Mengenangabe, einen Preis, Größen- und Farboptionen, ein Foto und möglicherweise ein Video umfasst. Diese Daten wirken auf den ersten Blick relational, da sie die gleiche Struktur aufweisen. Werden allerdings neue Produkte eingeführt, kann es vorkommen, dass Sie im Laufe der Zeit verschiedene Felder zu Ihren Produkten hinzufügen müssen. Stellen Sie sich beispielsweise vor, Sie nehmen neue Tennisschuhe in Ihr Sortiment auf, die über eine Bluetooth-Funktion verfügen, mit der zur Aufzeichnung der Geschwindigkeit Sensordaten von den Schuhen an eine Fitness-App auf dem Smartphone des Benutzers übertragen werden. Dieser Trend scheint mittlerweile immer mehr Zulauf zu erhalten, sodass Sie es Kunden in absehbarer Zukunft ermöglichen wollen, nach „Bluetooth-fähigen“ Schuhen zu filtern. Alle vorhandenen Daten zu Schuhen nun mit der Eigenschaft „Bluetooth-fähig“ zu aktualisieren, wäre viel zu aufwendig. Unkomplizierter wäre es hingegen, neuen Schuhen diese Eigenschaft einfach hinzuzufügen.

Durch Hinzufügen des Felds „Bluetooth-fähig“ wären die Daten Ihrer Schuhe nicht mehr heterogen, da Sie Unterschiede in das Schema eingeführt hätten. Wäre dies eine einmalige Änderung und die einzige Ausnahme, die Sie sich jemals vorstellen könnten, könnten Sie die vorhandenen Daten normalisieren, sodass alle Produkte ein Feld mit der Bezeichnung „Bluetooth-fähig“ enthalten. Dies ist jedoch nur eines von zahlreichen speziellen Feldern, die Sie in Zukunft eventuell unterstützen möchten. Die Klassifizierung dieser Daten ist deshalb als teilweise strukturiert zu betrachten. Die Daten werden durch Tags organisiert, wobei jedes Produkt im Katalog jedoch eindeutige Felder enthalten kann.

Datenklassifizierung: **Teilweise strukturiert**

### <a name="photos-and-videos"></a>Fotos und Videos

Bei den Fotos und Videos, die auf den Produktseiten angezeigt werden, handelt es sich um unstrukturierte Daten. Obwohl Mediendateien Metadaten enthalten können, ist der Text der Mediendatei unstrukturiert.

Datenklassifizierung: **Unstrukturiert**

### <a name="business-data"></a>Geschäftsdaten

Business Analysten möchten in der Regel Business Intelligence-Funktionen implementieren, um Bestandspipelines auszuwerten und Vertriebsdaten zu überprüfen. Um diese Vorgänge auszuführen, müssen Daten aus mehreren Monaten zusammen aggregiert und dann abgefragt werden. Aufgrund des großen Bedarfs für Aggregatdaten müssen diese Daten strukturiert werden, damit die Daten der einzelnen Monate miteinander verglichen werden können.

Datenklassifizierung: **Strukturiert**

## <a name="summary"></a>Zusammenfassung

Es gibt drei Kategorien von Daten: strukturiert, teilweise strukturiert und unstrukturiert. Für die Auswahl der richtigen Speicherlösung sind ein grundlegendes Verständnis zu den Unterschieden und die Ermittlung der Kategorie Ihrer Daten erforderlich. Strukturierte Daten sind organisierte Daten, die ohne Weiteres in Zeilen und Spalten in Tabellen eingefügt werden können. Teilweise strukturierte Daten sind zwar ebenfalls organisiert und verfügen über eindeutige Eigenschaften und Werte, weisen jedoch Abweichungen in den Daten auf. Unstrukturierte Daten lassen sich nicht ohne Weiteres in Tabellen einfügen und weisen kein Schema auf.
