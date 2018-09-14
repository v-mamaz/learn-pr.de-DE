Auswählen der richtigen speicherlösung kann eine bessere Leistung, Kosten zu sparen und verbesserte Verwaltbarkeit führen. Hier werden Sie anwenden, was Sie haben gelernt, über die Daten in Ihrem Szenario Onlinehandel, und finden die beste Azure-Dienst für jedes DataSet. 

## <a name="product-catalog-data"></a>Produktkatalogdaten

**Datenklassifizierung:** halbstrukturierten aufgrund müssen erweitern oder ändern das Schema für neue Produkte

**Vorgänge**:

- Kunden benötigen eine hohe Anzahl von Lesevorgängen, mit der Möglichkeit, Abfragen für viele Felder innerhalb der Datenbank.
- Das Unternehmen benötigt eine hohe Anzahl von Schreibvorgängen auf die ständig verändernden Inventur verfolgen.

**Latenz und Durchsatz**: Hoher Durchsatz bei niedriger Latenz

**Transaktionsunterstützung**: Erforderlich

### <a name="recommended-service-azure-cosmos-db"></a>Empfohlener Dienst: Azure Cosmos DB

Azure Cosmos DB unterstützt teilweise strukturierte Daten oder NoSQL-Daten. Unterstützung der neuen Felder, z. B. das Feld "Bluetooth-aktiviert" oder in der Zukunft Sie müssen neue Felder ist also ein mit Azure Cosmos DB erhalten.

Azure Cosmos DB unterstützt SQL für Abfragen, und jede Eigenschaft standardmäßig indiziert. Sie können Abfragen erstellen, sodass Ihre Kunden auf einer beliebigen Eigenschaft im Katalog filtern können.

Azure Cosmos DB ist auch mit ACID konform, sodass Sie sicher sein können, dass Ihre Transaktionen entsprechend dieser strikten Anforderungen durchgeführt werden.

Ein weiteres Plus: Mit Azure Cosmos DB können Sie Ihre Daten zudem mit einem einzigen Mausklick auf der ganzen Welt replizieren. Also wenn Ihre e-Commerce-Website auf Benutzer, die in den USA, Frankreich und England concentrated gibt, können Sie replizieren Ihre Daten in diesen Rechenzentren um Latenz zu verringern, wie Sie die Daten näher an Ihre Benutzer physisch verschoben haben. 

Auch bei Daten, die auf der ganzen Welt repliziert werden können Sie von einem der fünf konsistenzebenen auswählen. Wenn Sie die richtige Ebene auswählen, können Sie die Kompromisse zwischen Konsistenz, Verfügbarkeit, Latenz und Durchsatz bestimmen. Sie können zentral hochskalieren, um einer höheren Nachfrage der Kunden während der Spitzeneinkaufszeiten gerecht zu werden, oder während ruhigerer Zeiten herunterskalieren, um Kosten zu sparen.

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Azure SQL-Datenbank wäre eine hervorragende Wahl für dieses DataSet wäre da nicht die Notwendigkeit zum Erweitern des Schema-Ad-Hoc für neue Produkte. In Azure SQL-Datenbank werden alle Daten an ein Schema entsprechen muss. Azure SQL-Datenbank können viele der Vorteile von Azure Cosmos DB bereitstellen, aber es kann keine heterogenen Daten verarbeiten. 

Andere Azure-Dienste wie Azure Table Storage, Azure HBase als Teil von HDInsight und Azure Redis Cache können ebenfalls NoSQL-Daten speichern. In diesem Szenario werden Benutzer nach mehreren Feldern abfragen möchten damit Azure Cosmos DB besser geeignet ist. Azure Cosmos DB indiziert jedes Feld in der Standardeinstellung, während die anderen Dienste sind, beschränkt, in den Daten, die sie indizieren und Abfragen für nicht indizierte Felder-führt zu Leistungseinbußen.

## <a name="photos-and-videos"></a>Fotos und Videos

**Datenklassifizierung**: Unstrukturiert

**Vorgänge**:

- Nur nach ID abgerufen werden müssen
- Kunden benötigen eine hohe Anzahl der Lesevorgänge mit geringer Latenz.
- Erstellungs- und Aktualisierungsvorgänge kommen nur gelegentlich vor und weisen eventuell höhere Latenzen auf als Lesevorgänge.

**Latenz und Durchsatz**: Abrufe anhand der ID müssen niedrige Latenzen und einen hohen Durchsatz unterstützen. Erstellungs- und Aktualisierungsvorgänge weisen eventuell höhere Latenzen auf als Lesevorgänge.

**Transaktionsunterstützung**: Nicht erforderlich

### <a name="recommended-service-azure-blob-storage"></a>Empfohlener Dienst: Azure Blob Storage

Azure Blob Storage unterstützt das Speichern von Dateien, z.B. Fotos und Videos. Es funktioniert auch mit Azure Content Delivery Network (CDN) durch das Zwischenspeichern von des am häufigsten verwendeten Inhalts, und speichern es auf Edgeservern an. Azure CDN verringert die Latenz bei der Verarbeitung von diesen Abbildern an Ihre Benutzer.

Mit Azure Blob Storage, können Sie Images auch aus der Speicherebene "Hot" in der Speicherebene "kalt" oder "Archiv" verschieben, um Kosten und den Durchsatz der Fokus auf die am häufigsten zu reduzieren angezeigt werden soll, Bilder und Videos.

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Sie konnte Ihre Images in Azure App Service hochgeladen werden, damit der gleiche Server, der Ihre app ausgeführt wird, um Ihre Images eingesetzt wird. Diese Lösung funktioniert, wenn Sie nicht viele Dateien enthalten. Aber bei vielen Dateien und einer globalen Zielgruppe erzielen Sie bessere Ergebnisse mit Azure Blob Storage mit Azure Content Delivery Network.

## <a name="business-data"></a>Geschäftsdaten

**Datenklassifizierung**: Strukturiert

**Vorgänge**: Schreibgeschützte komplexe Analyseabfragen über verschiedene Datenbanken hinweg

**Latenz und Durchsatz**: Eine gewisse Latenz in den Ergebnissen ist aufgrund der komplexen Natur der Abfragen zu erwarten.

**Transaktionsunterstützung**: Erforderlich

### <a name="recommended-service-azure-sql-database"></a>Empfohlener Dienst: Azure SQL-Datenbank

Geschäftsdaten werden in den meisten Fällen von Wirtschaftsanalysten abgefragt, die aller Wahrscheinlichkeit nach eher mit SQL als anderen Abfragesprachen vertraut sind. Azure SQL-Datenbank selbst könnte als Lösung verwendet werden, aber in Verbindung mit Azure Analysis Services können Datenanalysten ein semantisches Modell der Daten in SQL-Datenbank erstellen. Die Datenanalysten können dann es Geschäftsbenutzern, freigeben, damit es genügt, eine Verbindung mit dem Modell jedes Business Intelligence (BI)-Tool sofort untersuchen Sie die Daten und gewinnen von Einblicken. 

### <a name="why-not-other-azure-services"></a>Warum keine anderen Azure-Dienste?

Azure SQL Data Warehouse unterstützt OLAP-Lösungen und SQL-Abfragen. Aber Ihre Wirtschaftsanalysten müssen datenbankübergreifende Abfragen ausführen, was SQL Data Warehouse nicht unterstützt.

Azure Analysis Services kann zusätzlich zu Azure SQL-Datenbank verwendet werden. Jedoch werden Ihre Unternehmensanalysten mehr Kenntnisse in SQL als bei der Arbeit mit Power BI. So möchten sie eine Datenbank, die SQL-Abfragen, unterstützt Azure Analysis Services nicht. Darüber hinaus sind die finanziellen Daten, die Sie in Ihrem Business-Dataset speichern, relationaler und mehrdimensionaler Natur. Azure Analysis Services unterstützt tabellarische Daten, die für den Dienst selbst gespeichert, aber keine mehrdimensionalen Daten. Zum Analysieren von mehrdimensionalen Daten mit Azure Analysis Services können Sie eine direkte Abfragen der SQL-Datenbank verwenden.

Azure Stream Analytics bietet eine hervorragende Möglichkeit, um Daten zu analysieren und in verwertbare Erkenntnisse umzuwandeln. Der Schwerpunkt liegt hier jedoch auf Echtzeitdaten, die gestreamt werden. In diesem Szenario werden nur Daten zur Versionsgeschichte der Wirtschaftsanalytiker untersucht.

## <a name="summary"></a>Zusammenfassung

Jeder Typ von Daten hat unterschiedliche Anforderungen, und es ist Ihre Aufgabe, um zu ermitteln, welche Lösung am besten geeignet ist. Denken Sie stets den Typ der Daten, die Vorgänge, die erforderlich sind, erwartet, Latenz und die Notwendigkeit der transaktionsunterstützung.