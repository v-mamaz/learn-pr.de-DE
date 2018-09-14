Betrachten die Vorteile der Azure-Datenspeicher, wissen Sie, dass sie mit die besten Optionen zum Speichern Ihrer Learning-Portals bietet. Jetzt sehen wir uns die Vorteile und die Optionen ausführlich, um festzustellen, wie es Ihren geschäftsanforderungen passt.

## <a name="how-azure-data-storage-can-meet-your-business-storage-needs"></a>Wie der Azure-Datenspeicher Storage unternehmensanforderungen erfüllen kann

Azure bietet verschiedene Speicheroptionen, die bestimmte Arten von Speicher zu berücksichtigen.

### <a name="azure-sql-database"></a>Azure SQL-Datenbank

**Azure SQL-Datenbank** ist eine stabile, vollständig verwalteter, relationaler Clouddatenbank. Sie können dieses Feature verwenden, um Daten zu speichern, auf die Sie häufig zugreifen und die Sie häufig aktualisieren, z.B. Informationen zu Schulungen für Ihre Mitarbeiter. Sie können auch Ihre vorhandenen SQL Server-Datenbanken migrieren, ohne Ihre Anwendungen ändern zu müssen. Die folgende Abbildung zeigt die Arten von Daten aus dem Portal online Learning-Szenario, das in einer Azure SQL-Datenbank gespeichert werden sollen.

![Eine Abbildung, die mit Azure SQL, die zum Speichern von Informationen für Schüler und Studenten, z. B. Aufzeichnungen Zertifizierungen, und die Materialien verwendet werden.](../media/3-Azure_SQL.png)

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

Azure Cosmos DB ist ein global verteilter Datenbankdienst. Er unterstützt schemalose Daten, die Sie extrem reaktionsschneller erstellen können und *Always On-* Anwendungen, die sich ständig verändernden Daten zu unterstützen. Sie können diese Funktion verwenden, zum Speichern von Daten, die aktualisiert wird und Beibehalten von Benutzern auf der ganzen Welt. Die folgende Abbildung zeigt eine Azure Cosmos DB-Beispieldatenbank verwendet zum Speichern von Daten, die durch mehrere Personen, die auf der ganzen Welt aus zugegriffen wird.

![Mit der Nutzung von Azure Cosmos DB im online-Schulung Szenario zum Speichern der Kurskatalog veranschaulicht. Azure Cosmos DB ist eine gute Wahl, da der Katalog, die von Administratoren aktualisiert und Schüler/Studenten, auf der ganzen Welt zugreifen.](../media/3-Azure_cosmos_db.png)

### <a name="azure-blob-storage"></a>Azure-Blobspeicher

Azure-BLOB-Speicher können Sie große Stream-Video oder audio-Dateien direkt an den Browser des Benutzers von jedem beliebigen Standort in der ganzen Welt. Blob-Speicher werden auch zum Speichern von Daten für die Sicherung und Wiederherstellung, die Notfallwiederherstellung sowie die Archivierung verwendet. Azure Blob Storage kann bis zu 8 TB Daten für Dateien auf virtuellen Computern speichern. Die folgende Abbildung zeigt eine Beispiel zur Verwendung von Azure Blob Storage.

![Eine Abbildung, zeigt Azure-Blob-Speicher verwendet, um den Speicher und Stream-Video oder audio-Dateien.](../media/3-Azure_blob.png)

### <a name="azure-data-lake-storage-gen2"></a>Azure Data Lake Storage Gen2

Die Data Lake-Funktion können Sie Analysen durchführen, auf die Verwendung Ihrer Daten und Berichte. Data Lake ist ein umfangreiches Repository, in dem sowohl strukturierte als auch unstrukturierte Daten gespeichert werden können.

**Azure Data Lake Storage Gen2** kombiniert die Skalierbarkeit und Kostenvorteile eines Objektspeichers mit der Zuverlässigkeit und Leistung eines Big Data-Dateisystems. Die folgende Abbildung zeigt, wie Azure Data Lake speichert Ihre gesamten Geschäftsdaten und macht sie für die Analyse verfügbar.

![Eine Abbildung, die die Rolle des Azure Data Lake in Vorbereitung und das Speichern Ihrer Daten für die Verwendung von Analysetools angezeigt. Azure Data Lake können verschiedene Eingabetypen wie z. B. relationale, Video, verarbeiten oder Sensordaten.](../media/3-Data_lake_store_concept.png)

### <a name="azure-files"></a>Azure Files

Azure Files bietet vollständig verwaltete Dateifreigaben in der Cloud. Anwendungen, die in Azure ausgeführt werden, können problemlos Dateien zwischen virtuellen Computern freigeben. Sie können Azure-Dateifreigaben gleichzeitig für Cloud- und lokale Bereitstellungen von Windows, Linux und macOS verwenden. Die folgende Abbildung zeigt die Azure-Dateien, die zum Freigeben von Daten zwischen den beiden geografischen Standorten verwendet wird. Azure Files verwendet das Server Message Block (SMB)-Protokoll, um sicherzustellen, dass die Daten im Ruhezustand und während der Übertragung verschlüsselt werden.

![Eine Abbildung, zeigt die Funktionen von Azure Files-Dateifreigabe. ](../media/3-Azure_Files.png)

### <a name="azure-queue"></a>Azure Queue

Azure Queue ist ein Dienst zur Speicherung einer großen Anzahl von Nachrichten, auf die von überall auf der Welt aus zugegriffen werden kann. Eine einzelne Warteschlangennachricht kann bis zu 64 KB groß sein, und eine Warteschlange kann Millionen von Nachrichten enthalten.

Es gibt in der Regel eine oder mehrere Sender-Komponenten und eine oder mehrere Empfänger-Komponenten. Senderkomponenten fügen der Warteschlange eine Nachricht hinzu. Empfängerkomponenten rufen Nachrichten am Anfang der Warteschlange zur Verarbeitung ab. Die folgende Abbildung zeigt mehrere Senderanwendungen beim Hinzufügen von Nachrichten zur Azure-Warteschlange und eine Empfängeranwendung beim Abrufen der Nachrichten.

![Abbildung der allgemeinen Architektur von Azure Queue Storage](../media/3-Azure_Queue.png)

Warteschlangenspeicher werden hauptsächlich für Folgendes verwendet:

- Erstellen eines Arbeitsbacklogs und Übermitteln von Nachrichten zwischen Azure-Webservern.
- Lastenausgleiche zwischen verschiedenen Webservern und Infrastrukturen und Verwalten von Bursts in der Datenverkehrsübertragung.
- Aufbauen eines robusten Schutzes vor Komponentenfehlern, wenn mehrere Benutzer gleichzeitig auf Ihre Daten zugreifen.

### <a name="azure-standard-storage"></a>Azure-Standardspeicher

Virtuelle Computer in Azure verwenden Datenträger zum Speichern von Betriebssystemen, Anwendungen und Daten. Azure-Standardspeicher bieten zuverlässige, kostengünstige Datenträgerunterstützung für virtuelle Computer mit nicht geschäftskritischen Workloads. Bei Verwendung von Standardspeicher werden die Daten auf Festplattenlaufwerken (Hard Disk Drives, HDDs) gespeichert.

Wenn Sie mit virtuellen Computern arbeiten, können Sie standardmäßige SSD- und HDD-Datenträger für weniger kritische Workloads und Premium-SSD-Datenträger für unternehmenskritische Produktionsanwendungen verwenden. Azure-Datenträger stellen durchgängig eine Dauerhaftigkeit auf Unternehmensniveau bereit, mit einer branchenweit führenden auf das Jahr umgerechneten Fehlerrate von NULL%. Die folgende Abbildung zeigt einen virtuellen Azure-Computer verwenden separate Datenträger zum Speichern von unterschiedliche Daten.

![Eine Abbildung mit zwei Datenträgern innerhalb eines virtuellen Computers, der das Betriebssystem speichert und eine, die Daten speichert.](../media/3-Azure_disks.png)

### <a name="storage-tiers"></a>Speicherebenen

Azure bietet drei Speicherebenen für blobobjektspeicher:

1. **Speicherebene "Hot"**: optimiert für das Speichern von Daten, die häufig zugegriffen werden. 

1. **Speicherebene "cool"**: optimiert für Daten, die selten zugegriffen wird und mindestens 30 Tage lang gespeichert.

1. **Speicherebene "Archiv"**: für Daten, die äußerst selten zugegriffen wird und mindestens 180 Tage lang mit flexiblen latenzanforderungen gespeichert.

### <a name="encryptionreplication"></a>Verschlüsselung/Replikation

Azure bietet Sicherheit und hochverfügbarkeit für Ihre Daten mithilfe der Funktionen für Verschlüsselung und die Replikation.

#### <a name="encryption-for-storage-services"></a>Verschlüsselung für Speicherdienste

Ihnen stehen folgende Verschlüsselungstypen für Ihre Ressourcen zur Verfügung:

1. Die **Azure-Speicherdienstverschlüsselung ( Storage Service Encryption, SSE)** für ruhende Daten unterstützt Sie dabei, Ihre Daten zu sichern, um die Anforderungen Ihrer Organisation an die Sicherheit und Einhaltung von gesetzlichen Bestimmungen zu erfüllen. Azure SSE verschlüsselt die Daten vor dem Speichern und entschlüsselt sie vor dem Abrufen wieder. Die Verschlüsselung und Entschlüsselung sind für den Benutzer transparent.

1. Bei der **clientseitigen Verschlüsselung** werden die Daten bereits von den Clientbibliotheken verschlüsselt. Azure speichert die Daten verschlüsselt im Ruhezustand, und die Daten werden während des Abrufs entschlüsselt.

#### <a name="replication-for-storage-availability"></a>Replikation für Speicherverfügbarkeit

Wenn Sie ein Speicherkonto erstellen, wird ein Replikationstyp festgelegt. Das Replikationsfeature stellt sicher, dass Ihre Daten stabil und jederzeit verfügbar sind. Azure bietet die regionale und geografische Replikationen zum Schutz Ihrer Daten vor Naturkatastrophen und anderen lokalen Naturkatastrophen wie Feuer oder Überflutung.