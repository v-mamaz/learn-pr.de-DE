Wenn Sie sich die Vorteile von Azure Storage ansehen, werden Sie schnell verstehen, dass dieser Dienst die besten Optionen für die Speicherung Ihres Schulungsportals bietet. Erkunden Sie die Vorteile und Optionen im Einzelnen, um herauszufinden, wie Azure Storage Ihre Geschäftsanforderungen erfüllt.

## <a name="how-azure-storage-can-meet-your-business-storage-needs"></a>So erfüllt Azure Storage die Speicheranforderungen Ihres Unternehmens

Azure Storage bietet verschiedene Optionen für die verschiedenen Arten von Anforderungen an Datenspeicher.

### <a name="azure-sql-database"></a>Azure SQL-Datenbank

**Azure SQL-Datenbank** ist eine stabile, vollständig verwaltete relationale Clouddatenbank, in der Sie all Ihre Daten speichern können. Sie können dieses Feature verwenden, um Daten zu speichern, auf die Sie häufig zugreifen und die Sie häufig aktualisieren – wie z.B. Informationen zu Schulungen für Ihre Mitarbeiter. Sie können auch Ihre vorhandenen SQL Server-Datenbanken migrieren, ohne Ihre Anwendungen ändern zu müssen.

![Azure SQL](../images/Azure_SQL.png)

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

Azure Cosmos DB ist ein preisgekrönter, global verteilter Datenbankdienst. Der Dienst unterstützt schemalose Daten, mit denen sich extrem reaktionsschnelle *Always On*-Anwendungen erstellen lassen, um sich ständig ändernde Daten zu unterstützen. Sie können dieses Feature verwenden, um Daten zu speichern, die basierend auf Eingaben von Benutzern auf der ganzen Welt aktualisiert und verwaltet werden.

![Cosmos DB](../images/Azure_cosmos_db.png)

### <a name="azure-blob-storage"></a>Azure Blob Storage

Azure Blob Storage bietet die Möglichkeit, große Video- und Audiodateien von jedem Standort der Welt aus direkt in Browser von Benutzern zu streamen. Blob Storage wird auch zum Speichern von Daten für Sicherung und Wiederherstellung, Notfallwiederherstellung und Archivierung verwendet. Azure Blob Storage kann bis zu 8 TB Daten für Dateien auf virtuellen Computern speichern.

![Azure Blob](../images/Azure_blob.png)

### <a name="azure-data-lake-storage-gen2"></a>Azure Data Lake Storage Gen2

Das Data Lake-Feature von Azure Storage ermöglicht es Ihnen, Ihre Datennutzung zu analysieren und entsprechende Berichte zu erstellen. Ein Data Lake ist ein umfangreiches Repository, in dem sowohl strukturierte als auch unstrukturierte Daten gespeichert werden können.

**Azure Data Lake Storage Gen2** kombiniert die Skalierbarkeit und Kostenvorteile eines Objektspeichers mit der Zuverlässigkeit und Leistung eines Big Data-Dateisystems.

![Data_lake_Store_concept](../images/Data_lake_store_concept.png)

### <a name="azure-files"></a>Azure Files

Azure Files bietet vollständig verwaltete Dateifreigaben in der Cloud. Anwendungen, die in Azure ausgeführt werden, können problemlos Dateien zwischen virtuellen Computern freigeben. Sie können Azure-Dateifreigaben gleichzeitig für Cloud- und lokale Bereitstellungen von Windows, Linux und macOS verwenden.

![Azure_Files](../images/Azure_Files.png)

### <a name="azure-queue"></a>Azure Queue

Azure Queue ist ein Dienst zur Speicherung einer großen Anzahl von Nachrichten, auf die von überall auf der Welt aus zugegriffen werden kann. Eine einzelne Warteschlangennachricht kann bis zu 64 KB groß sein, und eine Warteschlange kann Millionen von Nachrichten enthalten.

Queue wird hauptsächlich zu folgenden Zwecken verwendet:

- Erstellen eines Arbeitsbacklogs und Übermitteln von Nachrichten zwischen Azure-Webservern.
- Lastenausgleich zwischen verschiedenen Webservern und Infrastrukturen und Verwalten von Bursts in der Datenverkehrsübertragung.
- Aufbauen eines robusten Schutzes vor Komponentenfehlern, wenn mehrere Benutzer gleichzeitig auf Ihre Daten zugreifen.

![Azure_Queue](../images/Azure_Queue.png)

### <a name="azure-standard-storage"></a>Azure Storage Standard

Virtuelle Computer in Azure verwenden Datenträger zum Speichern von Betriebssystem, Anwendungen und Daten. Azure Storage Standard bietet zuverlässige, kostengünstige Datenträgerunterstützung für virtuelle Computer mit nicht geschäftskritischen Workloads. Bei Verwendung von Storage Standard werden die Daten auf Festplattenlaufwerken (Hard Disk Drives, HDDs) gespeichert.

Wenn Sie mit virtuellen Computern arbeiten, können Sie standardmäßige SSD- und HDD-Datenträger für weniger kritische Workloads und Premium-SSD-Datenträger für unternehmenskritische Produktionsanwendungen verwenden. Azure-Datenträger stellen durchgängig eine Dauerhaftigkeit auf Unternehmensniveau bereit, mit einer branchenweit führenden auf das Jahr umgerechneten Fehlerrate von NULL%.

![Azure_Disk](../images/Azure_disks.png)

### <a name="storage-tiers"></a>Speicherebenen

Azure Storage bietet drei Speicherebenen für Blobspeicher:

1. **Speicherebene „Heiß“**: Diese Azure-Speicherebene ist für die Speicherung von Daten optimiert, auf die häufig zugegriffen wird. 
1. **Speicherebene „Kalt“**: Diese Azure-Speicherebene ist für die Speicherung von Daten optimiert, auf die weniger häufig zugegriffen wird und die mindestens 30 Tage lang gespeichert werden.
1. **Speicherebene „Archiv“**: Diese Azure-Speicherebene ist für die Speicherung von Daten optimiert, auf die selten zugegriffen wird und die bei flexiblen Latenzanforderungen mindestens 180 Tage lang gespeichert werden. Der Archivspeicher in Azure eignet sich ideal zum Speichern älterer Versionen Ihrer Daten, sodass Sie die Daten abrufen können, wenn diese für Prüfungen oder andere unregelmäßige Aktivitäten benötigt werden.

![Archive_Tier](../images/Archive_Storage_Tier.png)

### <a name="azure-storage-encryptionreplication"></a>Azure Storage-Verschlüsselung/-Replikation

Azure Storage bietet Verschlüsselungs- und Replikationsfeatures, um für die Sicherheit und Hochverfügbarkeit Ihrer Daten zu sorgen.

#### <a name="encryption-for-storage-services"></a>Verschlüsselung für Speicherdienste

Für Ihre Ressourcen stehen die folgenden Arten der Verschlüsselung zur Verfügung:

1. **Azure Storage Service Encryption (SSE)** für ruhende Daten unterstützt Sie dabei, Ihre Daten zu sichern, um die Anforderungen Ihrer Organisation an die Sicherheit und Einhaltung von gesetzlichen Bestimmungen zu erfüllen. Azure SSE verschlüsselt die Daten vor dem Speichern und entschlüsselt sie vor dem Abrufen wieder. Verschlüsselung und Entschlüsselung sind für den Benutzer transparent.
1. **Clientseitige Verschlüsselung**, bei der die Daten bereits durch die Clientbibliotheken verschlüsselt werden. Azure speichert die Daten verschlüsselt im Ruhezustand, und die Daten werden während des Abrufs entschlüsselt.

    Dieses Verschlüsselungsfeature stellt sicher, dass Ihre Daten die globalen Schutzstandards erfüllen. Es eignet sich zum Speichern vertraulicher Informationen wie beispielsweise persönlicher und finanzieller Daten.

#### <a name="replication-for-storage-availability"></a>Replikation für Speicherverfügbarkeit

Wenn Sie ein Speicherkonto erstellen, wird ein Replikationstyp festgelegt. Das Replikationsfeature stellt sicher, dass Ihre Daten stabil und jederzeit verfügbar sind. Azure Storage ermöglicht regionale und geografische Replikationen, um Ihre Daten bei Naturkatastrophen und anderen lokalen Ereignissen wie Bränden oder Überflutungen zu schützen.
