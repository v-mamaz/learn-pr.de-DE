Die Wahl der richtigen Speicherlösung kann zu einer Leistungsverbesserung führen. In diesem Artikel wenden Sie das Wissen an, das Sie in Bezug auf die Daten im Szenario des Onlinehändlers erworben haben, und wählen den idealen Azure-Dienst für jedes Dataset aus. 

## <a name="product-catalog-data"></a>Produktkatalogdaten

Datenklassifizierung: Teilweise strukturiert

Vorgänge:

* Kunden müssen eine Vielzahl von Lesevorgängen ausführen und die Möglichkeit haben, auf viele Felder in der Datenbank zuzugreifen.
* Unternehmen müssen eine Vielzahl von Lesevorgängen ausführen, um den sich ständig ändernden Bestand nachzuvollziehen.

Latenz und Durchsatz: Hoher Durchsatz bei niedriger Latenz

Transaktionsunterstützung: Erforderlich

### <a name="recommended-service-azure-cosmos-db"></a>Empfohlener Dienst: Azure Cosmos DB

Azure Cosmos DB unterstützt teilweise strukturierte Daten oder NoSQL-Daten. Unterstützung für neue Felder wie das Feld „Bluetooth-fähig“ oder sonstige neue Felder, die Sie später womöglich benötigen, ist bei Azure Cosmos DB eine Selbstverständlichkeit.

In Bezug auf Vorgänge unterstützt Azure Cosmos DB SQL für Abfragen, und jede Eigenschaft wird standardmäßig indiziert, sodass die Erstellung von Abfragen entsprechend den Anforderungen Ihrer Kunden zum Filtern nach fast sämtlichen Inhalten unterstützt wird.

In Bezug auf Latenz und Durchsatz ermöglicht Ihnen Azure Cosmos DB die Konfiguration Ihres Durchsatzes, sodass Sie in Spitzenzeiten beim Einkauf Ressourcen zentral hochskalieren können, um die steigende Kundennachfrage bedienen zu können, und in Zeiten mit nachlassender Nachfrage Ressourcen zentral hochskalieren zentral herunterskalieren können, um Kosten zu sparen. Da Azure Cosmos DB alle Eigenschaften standardmäßig indiziert, können Sie es Kunden ermöglichen, beliebige Felder abzufragen.

Azure Cosmos DB ist auch mit ACID konform, sodass Sie sicher sein können, dass Ihre Transaktionen entsprechend dieser strikten Anforderungen durchgeführt werden.

Ein weiteres Plus: Mit Azure Cosmos DB können Sie Ihre Daten zudem mit einem einzigen Mausklick auf der ganzen Welt replizieren. Wenn Ihre E-Commerce-Website bisher z.B. auf Benutzer in den USA, in Frankreich und im Vereinigten Königreich ausgerichtet war, können Sie Ihre Daten in diesen Rechenzentren replizieren, um Latenzen zu verringern, da Sie die Daten physisch näher zu Ihren Benutzern migriert haben. Auch wenn Daten auf der ganzen Welt repliziert werden, können Sie aus einer der fünf Konsistenzebenen wählen, damit Sie den Trade-Off zwischen Konsistenz, Verfügbarkeit, Latenz und Durchsatz ermitteln können.

### <a name="why-not-other-azure-services"></a>Gründe für andere Azure-Dienste

Andere Azure-Dienste wie Azure Table Storage, Azure HBase als Teil von HDInsight und Azure Redis Cache können ebenfalls NoSQL-Daten speichern. In diesem Szenario ist Azure Cosmos DB besser geeignet als Azure Table Storage, Azure Redis Cache oder Azure HBase als Teil von HDInsight, da Benutzer mehrere Felder abfragen. Azure Cosmos DB indiziert standardmäßig jedes Feld, während die anderen Dienste eingeschränkt sind, was die Daten, die indiziert werden können, betrifft, und die Möglichkeiten zum Abfragen von Feldern in der Datenbank somit beschränkt sind.

## <a name="photos-and-videos"></a>Fotos und Videos

Datenklassifizierung: Unstrukturiert

Vorgänge:

* Fotos und Videos müssen nur anhand der ID abgerufen werden.
* Erstellungs- und Aktualisierungsvorgänge kommen nur gelegentlich vor und weisen eventuell höhere Latenzen auf als Lesevorgänge.

Latenz und Durchsatz: Abrufe anhand der ID müssen niedrige Latenzen und einen hohen Durchsatz unterstützen. Erstellungs- und Aktualisierungsvorgänge weisen eventuell höhere Latenzen auf als Lesevorgänge.

Transaktionsunterstützung: Nicht erforderlich

## <a name="recommended-service-azure-blob-storage"></a>Empfohlener Dienst: Azure Blob Storage

Azure Blob Storage unterstützt das Speichern von Dateien, z.B. Fotos und Videos. Da der Dienst mit Azure Content Delivery Network (CDN) konform ist, können die am häufigsten verwendeten Inhalte zwischengespeichert und auf Edgeservern gespeichert werden, wodurch Latenzen bei der Verarbeitung dieser Bilder zugunsten Ihrer Benutzer verkürzt werden.

Mithilfe von Azure Blob Storage können Sie Bilder auch von der heißen zur kalten Speicherebene oder Archivspeicherebene migrieren, um die Kosten zu reduzieren und den Durchsatz auf die am häufigsten angezeigten Bilder und Videos zu konzentrieren.

### <a name="why-not-other-azure-services"></a>Gründe für andere Azure-Dienste

Sie könnten Ihre Bilder in Azure App Services hochladen, damit der Server, auf dem Ihre App ausgeführt wird, Ihre Bilder verarbeiten kann. Dies würde funktionieren, wenn Sie nicht über viele Bilder, sondern über viele Dateien und eine globale Zielgruppe verfügen. Sie würden dann bessere Ergebnisse mit Azure Blob Storage als mit Azure Content Delivery Network erhalten.

## <a name="business-data"></a>Geschäftsdaten

Datenklassifizierung: Strukturiert

Vorgänge: Schreibgeschützte komplexe Analyseabfragen über verschiedene Datenbanken hinweg

Latenz und Durchsatz: Eine gewisse Latenz in den Ergebnissen ist aufgrund der komplexen Natur der Abfragen zu erwarten.

Transaktionsunterstützung: Erforderlich

### <a name="recommended-service-azure-sql-database"></a>Empfohlener Dienst: Azure SQL-Datenbank

Geschäftsdaten werden in den meisten Fällen von Business Analysten abgefragt, die aller Wahrscheinlichkeit eher mit SQL als mit anderen Abfragesprachen vertraut sind. Azure SQL-Datenbank könnte als eigenständige Lösung verwendet werden, jedoch auch mit Azure Analysis Services gekoppelt werden. Datenanalysten könnten dann ein semantisches Modell für die Daten in Azure SQL-Datenbank erstellen und diese dann für Geschäftskunden freigeben, indem sie lediglich eine Verbindung mit dem Modell über ein beliebiges BI-Tool herstellen. Die Daten können dann unmittelbar eingesehen und zur Gewinnung eines umfangreicheren Einblicks untersucht werden. 

### <a name="why-not-other-azure-services"></a>Gründe für andere Azure-Dienste

Azure SQL Data Warehouse unterstützt OLAP-Lösungen und SQL-Abfragen. Business Analysten müssen jedoch plattformübergreifende Datenbankabfragen ausführen, die Azure SQL Data Warehouse nicht unterstützt.

Azure Analysis Services könnte zusätzlich zu Azure SQL-Datenbank verwendet werden. Ihre Business Analysten werden jedoch weitaus versierter in der Arbeit mit SQL sein als mit Power BI, weshalb sie aller Wahrscheinlichkeit nach eine Datenbank benötigen werden, die SQL-Abfragen unterstützt. Diese werden nicht von Azure Analysis Services unterstützt. Darüber hinaus sind die Finanzdaten, die Sie in Ihrem Geschäftsdataset speichern, relational und mehrdimensional. Azure Analysis Services unterstützt zwar die im Dienst selbst gespeicherten Tabellendaten, allerdings keine mehrdimensionalen Daten. Zum Analysieren von mehrdimensionalen Daten mit Azure Analysis Services können Sie direkte Abfragen an Azure SQL-Datenbank verwenden.

Azure Stream Analytics bietet eine hervorragende Möglichkeit, um Daten zu analysieren und in verwertbare Erkenntnisse umzuwandeln. Der Schwerpunkt liegt hier jedoch auf Echtzeitdaten, die gestreamt werden, und in diesem Fall ziehen Business Analysten nur historische Daten heran.

## <a name="summary"></a>Zusammenfassung

Jede Datenkategorie stellt unterschiedliche Anforderungen. Ihre Aufgabe besteht darin, zu ermitteln, welche Lösung am besten geeignet ist. Folgendes sollten Sie immer in Betracht ziehen: die Kategorie der Daten, die erforderlichen Vorgänge, Latenzen und die Notwendigkeit für Transaktionsunterstützung.
