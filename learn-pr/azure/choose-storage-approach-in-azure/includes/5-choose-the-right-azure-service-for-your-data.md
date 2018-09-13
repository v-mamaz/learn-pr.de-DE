Die Wahl der richtigen Speicherlösung kann zu einer Leistungsverbesserung führen. In diesem Artikel wenden Sie das Wissen an, das Sie in Bezug auf die Daten im Szenario des Onlinehändlers erworben haben, und wählen den idealen Azure-Dienst für jedes Dataset aus. 

## <a name="product-catalog-data"></a>Produktkatalogdaten

**Datenklassifizierung**: Teilweise strukturiert

**Vorgänge**:

- Kunden müssen eine Vielzahl von Lesevorgängen ausführen und die Möglichkeit haben, viele Felder in der Datenbank abzufragen.
- Unternehmen müssen eine Vielzahl von Lesevorgängen ausführen, um den sich ständig ändernden Bestand nachzuvollziehen.

**Latenz und Durchsatz**: Hoher Durchsatz bei niedriger Latenz

**Transaktionsunterstützung**: Erforderlich

### <a name="recommended-service-azure-cosmos-db"></a>Empfohlener Dienst: Azure Cosmos DB

Azure Cosmos DB unterstützt teilweise strukturierte Daten oder NoSQL-Daten. Unterstützung für neue Felder wie das Feld „Bluetooth-fähig“ oder sonstige neue Felder, die Sie später womöglich benötigen, ist bei Azure Cosmos DB eine Selbstverständlichkeit.

In Bezug auf Vorgänge unterstützt Azure Cosmos DB SQL für Abfragen, und jede Eigenschaft ist standardmäßig indiziert. Erstellen von Abfragen entsprechend den Anforderungen Ihrer Kunden zum Filtern nach fast allem wird unterstützt.

Für Latenz und Durchsatz gilt: Mit Azure Cosmos DB können Sie Ihren Durchsatz konfigurieren. Sie können zentral hochskalieren, um einer höheren Nachfrage der Kunden während der Spitzeneinkaufszeiten gerecht zu werden, oder während ruhigerer Zeiten herunterskalieren, um Kosten zu sparen. Da Azure Cosmos DB alle Eigenschaften standardmäßig indiziert, können Sie Kunden ermöglichen, beliebige Felder abzufragen.

Azure Cosmos DB ist auch mit ACID konform, sodass Sie sicher sein können, dass Ihre Transaktionen entsprechend dieser strikten Anforderungen durchgeführt werden.

Ein weiteres Plus: Mit Azure Cosmos DB können Sie Ihre Daten zudem mit einem einzigen Mausklick auf der ganzen Welt replizieren. Wenn Ihre E-Commerce-Website bisher z.B. auf Benutzer in den USA, in Frankreich und im Vereinigten Königreich ausgerichtet war, können Sie Ihre Daten in diesen Rechenzentren replizieren, um Latenzen zu verringern, da Sie die Daten physisch näher zu Ihren Benutzern migriert haben. Und auch bei Daten, die auf der ganzen Welt repliziert werden, können Sie eine von fünf Konsistenzebenen auswählen. Sie bestimmen die Kompromisse zwischen Konsistenz, Verfügbarkeit, Latenz und Durchsatz.

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Andere Azure-Dienste wie Azure Table Storage, Azure HBase als Teil von HDInsight und Azure Redis Cache können ebenfalls NoSQL-Daten speichern. Da Benutzer mehrere Felder abfragen möchten, ist Azure Cosmos DB in diesem Szenario besser geeignet. Der Grund ist, dass Azure Cosmos DB jedes Feld standardmäßig indiziert, während in den anderen Diensten die indizierten Daten eingeschränkt sind, sodass sie nur eingeschränkte Möglichkeiten bieten, ein beliebiges Feld in der Datenbank abzufragen.

## <a name="photos-and-videos"></a>Fotos und Videos

**Datenklassifizierung**: Unstrukturiert

**Vorgänge**:

- Fotos und Videos müssen nur anhand der ID abgerufen werden.
- Erstellungs- und Aktualisierungsvorgänge kommen nur gelegentlich vor und weisen eventuell höhere Latenzen auf als Lesevorgänge.

**Latenz und Durchsatz**: Abrufe anhand der ID müssen niedrige Latenzen und einen hohen Durchsatz unterstützen. Erstellungs- und Aktualisierungsvorgänge weisen eventuell höhere Latenzen auf als Lesevorgänge.

**Transaktionsunterstützung**: Nicht erforderlich

### <a name="recommended-service-azure-blob-storage"></a>Empfohlener Dienst: Azure Blob Storage

Azure Blob Storage unterstützt das Speichern von Dateien, z.B. Fotos und Videos. Da der Dienst mit Azure Content Delivery Network (CDN) konform ist, können die am häufigsten verwendeten Inhalte zwischengespeichert und auf Edgeservern gespeichert werden. Dies verringert die Latenz bei der Bereitstellung dieser Bilder für Ihre Benutzer.

Mithilfe von Azure Blob Storage können Sie Bilder auch von der heißen zur kalten Zugriffsebene oder Archivspeicherebene migrieren, um die Kosten zu reduzieren und den Durchsatz auf die am häufigsten angezeigten Bilder und Videos zu konzentrieren.

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Sie könnten Ihre Bilder in Azure App Service hochladen, damit der Server, auf dem Ihre App ausgeführt wird, Ihre Bilder bereitstellen kann. Bei wenigen Bildern würde das funktionieren. Aber bei vielen Dateien und einer globalen Zielgruppe erzielen Sie bessere Ergebnisse mit Azure Blob Storage mit Azure Content Delivery Network.

## <a name="business-data"></a>Geschäftsdaten

**Datenklassifizierung**: Strukturiert

**Vorgänge**: Schreibgeschützte komplexe Analyseabfragen über verschiedene Datenbanken hinweg

**Latenz und Durchsatz**: Eine gewisse Latenz in den Ergebnissen ist aufgrund der komplexen Natur der Abfragen zu erwarten.

**Transaktionsunterstützung**: Erforderlich

### <a name="recommended-service-azure-sql-database"></a>Empfohlener Dienst: Azure SQL-Datenbank

Geschäftsdaten werden in den meisten Fällen von Wirtschaftsanalysten abgefragt, die aller Wahrscheinlichkeit nach eher mit SQL als anderen Abfragesprachen vertraut sind. Azure SQL-Datenbank selbst könnte als Lösung verwendet werden, aber in Verbindung mit Azure Analysis Services können Datenanalysten ein semantisches Modell der Daten in SQL-Datenbank erstellen. Sie können es dann für Geschäftsbenutzer freigeben, sodass diese nur von einem beliebigen BI-Tool aus eine Verbindung mit dem Modell herstellen müssen und sofort die Daten untersuchen und Einblicke gewinnen können. 

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Azure SQL Data Warehouse unterstützt OLAP-Lösungen und SQL-Abfragen. Aber Ihre Wirtschaftsanalysten müssen datenbankübergreifende Abfragen ausführen, was SQL Data Warehouse nicht unterstützt.

Analysis Services könnte zusätzlich zu SQL-Datenbank verwendet werden. Aber Ihre Wirtschaftsanalysten sind in SQL mehr zu Hause als im Arbeiten mit Power BI. Sie wünschen sich darum eine Datenbank, die SQL-Abfragen unterstützt, was bei Analysis Services nicht der Fall ist. Darüber hinaus sind die finanziellen Daten, die Sie in Ihrem Business-Dataset speichern, relationaler und mehrdimensionaler Natur. Analysis Services unterstützt im Dienst selbst gespeicherte tabellarische Daten, aber keine mehrdimensionalen Daten. Zum Analysieren mehrdimensionaler Daten mit Analysis Services können Sie direkte Abfragen an SQL-Datenbank richten.

Azure Stream Analytics bietet eine hervorragende Möglichkeit, um Daten zu analysieren und in verwertbare Erkenntnisse umzuwandeln. Der Schwerpunkt liegt hier jedoch auf Echtzeitdaten, die gestreamt werden. In diesem Fall ziehen unsere Wirtschaftsanalysten nur Daten zur Versionsgeschichte heran.

## <a name="summary"></a>Zusammenfassung

Jede Datenkategorie stellt unterschiedliche Anforderungen. Ihre Aufgabe besteht darin, zu ermitteln, welche Lösung am besten geeignet ist. Folgendes sollten Sie immer in Betracht ziehen: die Kategorie der Daten, die erforderlichen Vorgänge, Latenzen und die Notwendigkeit für Transaktionsunterstützung.