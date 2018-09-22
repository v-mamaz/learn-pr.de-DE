Die Wahl der richtigen Speicherlösung kann zu Leistungsverbesserung, Kostenersparnis und verbesserter Verwaltbarkeit führen. In diesem Artikel wenden Sie das Wissen an, das Sie in Bezug auf die Daten im Szenario des Onlinehändlers erworben haben, und wählen den idealen Azure-Dienst für jedes Dataset aus. 

## <a name="product-catalog-data"></a>Produktkatalogdaten

**Datenklassifizierung:** Teilweise strukturiert, da das Erweitern oder Ändern des Schemas für neue Produkte erforderlich ist.

**Vorgänge:**

- Kunden müssen eine Vielzahl von Lesevorgängen ausführen und über die Möglichkeit verfügen, viele Felder in der Datenbank abzufragen.
- Das Unternehmen muss eine Vielzahl von Lesevorgängen ausführen, um den sich ständig ändernden Bestand nachzuverfolgen.

**Latenz und Durchsatz:** Hoher Durchsatz bei niedriger Latenz

**Transaktionsunterstützung**: Erforderlich

### <a name="recommended-service-azure-cosmos-db"></a>Empfohlener Dienst: Azure Cosmos DB

Azure Cosmos DB unterstützt teilweise strukturierte Daten oder NoSQL-Daten. Unterstützung für neue Felder wie das Feld „Bluetoothfähig“ oder sonstige neue Felder, die Sie später womöglich benötigen, ist bei Azure Cosmos DB eine Selbstverständlichkeit.

Azure Cosmos DB unterstützt SQL für Abfragen, und jede Eigenschaft wird standardmäßig indiziert. Sie können Abfragen erstellen, damit Ihre Kunden den Katalog nach jeder Eigenschaft filtern können.

Azure Cosmos DB ist auch mit ACID konform, sodass Sie sicher sein können, dass Ihre Transaktionen entsprechend dieser strikten Anforderungen durchgeführt werden.

Ein weiteres Plus: Mit Azure Cosmos DB können Sie Ihre Daten zudem mit einem einzigen Mausklick auf der ganzen Welt replizieren. Wenn sich die Benutzer Ihrer E-Commerce-Website überwiegend in den USA, in Frankreich und in England befinden, können Sie Ihre Daten in den entsprechenden Rechenzentren replizieren, um die Latenz zu reduzieren, da Sie die Daten so physisch näher zu Ihren Benutzern verschoben haben. 

Selbst bei Daten, die auf der ganzen Welt repliziert werden, können Sie eine von fünf Konsistenzebenen auswählen. Durch Auswählen der richtigen Konsistenzebene bestimmen Sie die Kompromisse zwischen Konsistenz, Verfügbarkeit, Latenz und Durchsatz. Sie können zentral hochskalieren, um einer höheren Nachfrage der Kunden während der Spitzeneinkaufszeiten gerecht zu werden, oder während ruhigerer Zeiten herunterskalieren, um Kosten zu sparen.

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Azure SQL-Datenbank wäre eine gute Wahl für dieses Dataset, wenn das unmittelbare Erweitern des Schemas für neue Produkte nicht erforderlich wäre. In Azure SQL-Datenbank müssen alle Daten einem Schema entsprechen. Azure SQL-Datenbank kann viele der Vorteile von Azure Cosmos DB bereitstellen, jedoch können heterogene Daten nicht verarbeitet werden. 

Andere Azure-Dienste wie Azure-Tabellenspeicher, Azure HBase als Teil von HDInsight und Azure Redis Cache können ebenfalls NoSQL-Daten speichern. Da Benutzer mehrere Felder abfragen möchten, ist Azure Cosmos DB in diesem Szenario besser geeignet. Azure Cosmos DB indiziert standardmäßig jedes Feld, während andere Dienste bei den von ihnen indizierten Daten beschränkt sind und Abfragen von nicht indizierten Feldern zu Leistungseinbußen führen.

## <a name="photos-and-videos"></a>Fotos und Videos

**Datenklassifizierung**: Unstrukturiert

**Vorgänge:**

- Sie müssen nur anhand der ID abgerufen werden.
- Kunden benötigen eine hohe Anzahl von Lesevorgängen mit geringer Latenz.
- Erstellungsvorgänge und Updates kommen nur gelegentlich vor und weisen eventuell höhere Latenzen auf als Lesevorgänge.

**Latenz und Durchsatz**: Abrufe anhand der ID müssen niedrige Latenzen und einen hohen Durchsatz unterstützen. Erstellungs- und Aktualisierungsvorgänge weisen eventuell höhere Latenzen auf als Lesevorgänge.

**Transaktionsunterstützung**: Nicht erforderlich

### <a name="recommended-service-azure-blob-storage"></a>Empfohlener Dienst: Azure Blob Storage

Azure Blob Storage unterstützt das Speichern von Dateien, z.B. Fotos und Videos. Da der Dienst mit Azure Content Delivery Network (CDN) kompatibel ist, können die am häufigsten verwendeten Inhalte zwischengespeichert und auf Edgeservern gespeichert werden. Azure CDN verringert die Latenz bei der Bereitstellung dieser Bilder für Ihre Benutzer.

Mithilfe von Azure Blob Storage können Sie Bilder auch von der heißen zur kalten Speicherebene oder Archivspeicherebene migrieren, um die Kosten zu reduzieren und den Durchsatz auf die am häufigsten angezeigten Bilder und Videos zu konzentrieren.

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Sie können Ihre Bilder in Azure App Service hochladen, damit der Server, auf dem Ihre App ausgeführt wird, Ihre Bilder bereitstellen kann. Diese Lösung würde funktionieren, wenn Sie nur wenige Dateien verwenden. Da Sie jedoch über viele Dateien und eine globale Zielgruppe verfügen, erzielen Sie mit Azure Blob Storage mit Azure CDN bessere Ergebnisse.

## <a name="business-data"></a>Geschäftsdaten

**Datenklassifizierung**: Strukturiert

**Vorgänge**: Schreibgeschützte komplexe Analyseabfragen über verschiedene Datenbanken hinweg

**Latenz und Durchsatz**: Eine gewisse Latenz in den Ergebnissen ist aufgrund der komplexen Natur der Abfragen zu erwarten.

**Transaktionsunterstützung**: Erforderlich

### <a name="recommended-service-azure-sql-database"></a>Empfohlener Dienst: Azure SQL-Datenbank

Geschäftsdaten werden in den meisten Fällen von Wirtschaftsanalysten abgefragt, die aller Wahrscheinlichkeit nach eher mit SQL als anderen Abfragesprachen vertraut sind. Azure SQL-Datenbank selbst könnte als Lösung verwendet werden, aber in Verbindung mit Azure Analysis Services können Datenanalysten ein semantisches Modell der Daten in SQL-Datenbank erstellen. Business Analysts können es dann für Geschäftsbenutzer freigeben, damit diese nur eine Verbindung mit dem Modell über ein beliebiges BI-Tool (Business Intelligence) herstellen müssen, um die Daten sofort untersuchen und sich Einblicke verschaffen zu können. 

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Azure SQL Data Warehouse unterstützt OLAP-Lösungen und SQL-Abfragen. Ihre Business Analysts müssen jedoch datenbankübergreifende Abfragen ausführen, was nicht von SQL Data Warehouse unterstützt wird.

Azure Analysis Services könnte zusätzlich zu Azure SQL-Datenbank verwendet werden. Aber Ihre Business Analysts sind eher mit SQL vertraut als mit Power BI. Sie wünschen sich darum eine Datenbank, die SQL-Abfragen unterstützt, was bei Azure Analysis Services nicht der Fall ist. Darüber hinaus sind die Finanzdaten, die Sie in Ihrem Unternehmensdataset speichern, relationaler und mehrdimensionaler Natur. Azure Analysis Services unterstützt im Dienst selbst gespeicherte tabellarische Daten, aber keine mehrdimensionalen Daten. Zum Analysieren von mehrdimensionalen Daten mit Azure Analysis Services können Sie eine direkte Abfrage der SQL-Datenbank verwenden.

Azure Stream Analytics bietet eine hervorragende Möglichkeit, um Daten zu analysieren und in verwertbare Erkenntnisse umzuwandeln. Der Schwerpunkt liegt hier jedoch auf Echtzeitdaten, die gestreamt werden. In diesem Szenario untersuchen Business Analysts nur historische Daten.

## <a name="summary"></a>Zusammenfassung

Jeder Typ von Daten weist unterschiedliche Anforderungen auf. Ihre Aufgabe besteht darin, zu ermitteln, welche Lösung am besten geeignet ist. Sie sollten immer Rücksicht auf den Typ der Daten, die erforderlichen Vorgänge, die erwartete Latenz und die Notwendigkeit für Transaktionsunterstützung nehmen.