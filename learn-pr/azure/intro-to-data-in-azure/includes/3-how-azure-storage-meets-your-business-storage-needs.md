Wenn Sie sich die Vorteile der Azure-Datenspeicher ansehen, werden Sie schnell verstehen, dass sie die besten Optionen für die Speicherung Ihres Schulungsportals bietet. Erkunden Sie die Vorteile und Optionen im Einzelnen, um herauszufinden, wie sie Ihre Geschäftsanforderungen erfüllt.

## <a name="how-azure-data-storage-can-meet-your-business-storage-needs"></a>So erfüllen Azure-Datenspeicher Ihre Geschäftsanforderungen

Azure Storage bietet verschiedene Speicheroptionen für verschiedene Arten von Anforderungen an Datenspeicher. Werfen Sie einen kurzen Blick auf einige von ihnen.

:::row:::
  :::column:::
    ![Azure SQL-Datenbank](../media/3-azure-sql-db.png)
  :::column-end:::
    :::column span="3":::
**Azure SQL-Datenbank**

**Azure SQL-Datenbank** ist eine stabile, vollständig verwaltete relationale Clouddatenbank. Sie können dieses Feature verwenden, um Daten zu speichern, auf die Sie häufig zugreifen und die Sie häufig aktualisieren, z.B. Informationen zu Schulungen für Ihre Mitarbeiter. Sie können auch Ihre vorhandenen SQL Server-Datenbanken migrieren, ohne Ihre Anwendungen ändern zu müssen. In der folgenden Abbildung werden die Datentypen aus dem Szenario für ein Onlinelernportal veranschaulicht, die in einer SQL-Datenbank von Azure gespeichert werden würden.

![Eine Abbildung, die die Verwendung von Azure SQL zum Speichern von Informationen von Schülern und Studenten veranschaulicht, z.B. Transkripte, Zertifizierungen und Lernmaterialien.](../media/3-Azure_SQL.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure Cosmos DB](../media/3-cosmos-db.png)
  :::column-end:::
    :::column span="3":::
**Azure Cosmos DB**

Azure Cosmos DB ist ein global verteilter Datenbankdienst. Der Dienst unterstützt schemalose Daten, mit denen Sie extrem reaktionsschnelle **Always On**-Anwendungen erstellen können, um Daten zu unterstützen, die sich ständig ändern. Sie können dieses Feature verwenden, um Daten zu speichern, die von Benutzern auf der ganzen Welt aktualisiert und verwaltet werden. In der folgenden Abbildung wird eine Beispieldatenbank von Azure Cosmos DB gezeigt, die zum Speichern von Daten verwendet wird, auf die Personen aus der ganzen Welt zugreifen.

![Eine Abbildung, die die Verwendung von Azure Cosmos DB im Szenario für Onlinetraining zum Speichern des Kurskatalogs veranschaulicht. In diesem Szenario eignet sich Azure Cosmos DB gut, da der Katalog von Administratoren aktualisiert wird und Schüler bzw. Studenten aus aller Welt auf ihn zugreifen.](../media/3-Azure_cosmos_db.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure Blob Storage](../media/3-azure-blob-storage.png)
  :::column-end:::
    :::column span="3":::
**Azure Blob Storage**

Azure Blob Storage bietet Ihnen die Möglichkeit, große Video- und Audiodateien von jedem Standort der Welt aus direkt in Browser von Benutzern zu streamen. Blobspeicher wird auch zum Speichern von Daten für die Sicherung und Wiederherstellung, die Notfallwiederherstellung sowie die Archivierung verwendet. Er kann bis zu 8 TB Daten für virtuelle Computer speichern. In der folgenden Abbildung wird ein Beispiel zur Verwendung von Azure Blob Storage veranschaulicht.

![Eine Abbildung, die die Verwendung von Azure Blob Storage zum Speichern und Streamen von Video- und Audiodateien veranschaulicht.](../media/3-Azure_blob.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure Data Lake Storage Gen2](../media/3-azure-data-lake.png)
  :::column-end:::
    :::column span="3":::
**Azure Data Lake Storage Gen2**

Das Data Lake-Feature ermöglicht es Ihnen, Ihre Datennutzung zu analysieren und Berichte zu erstellen. Data Lake ist ein umfangreiches Repository, in dem sowohl strukturierte als auch unstrukturierte Daten gespeichert werden können.

**Azure Data Lake Storage Gen2** kombiniert die Skalierbarkeit und Kostenvorteile eines Objektspeichers mit der Zuverlässigkeit und Leistung eines Big Data-Dateisystems. In der folgenden Abbildung wird gezeigt, wie Azure Data Lake all Ihre Geschäftsdaten speichert und für die Analyse zur Verfügung stellt.

![Eine Abbildung, die die Rolle von Azure Data Lake beim Vorbereiten und Speichern Ihrer Daten zur Verwendung durch Analysetools veranschaulicht. Azure Data Lake kann eine Vielzahl von Eingabetypen verarbeiten, z.B. relationale, Video- oder Sensordaten.](../media/3-Data_lake_store_concept.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure Files](../media/3-azure-files.png)
  :::column-end:::
    :::column span="3":::
**Azure Files**

Azure Files bietet vollständig verwaltete Dateifreigaben in der Cloud. Anwendungen, die in Azure ausgeführt werden, können problemlos Dateien zwischen virtuellen Computern freigeben. Sie können Azure-Dateifreigaben gleichzeitig für Cloud- und lokale Bereitstellungen von Windows, Linux und macOS verwenden. In der folgenden Abbildung wird die Verwendung von Azure Files zum Freigeben von Daten für zwei geografische Standorte veranschaulicht. Azure Files verwendet das SMB-Protokoll (Server Message Block). Es stellt sicher, dass Daten im Ruhezustand und während der Übertragung verschlüsselt sind.

![Eine Abbildung, die die Azure Files-Funktionen zum Freigeben von Dateien veranschaulicht. ](../media/3-Azure_Files.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure Queue](../media/3-azure-queue.png)
  :::column-end:::
    :::column span="3":::
**Azure Queue**

Azure Queue ist ein Dienst zur Speicherung einer großen Anzahl von Nachrichten, auf die von überall auf der Welt aus zugegriffen werden kann. In Zahlen: Eine einzelne Warteschlangennachricht kann bis zu 64 KB groß sein, und eine Warteschlange kann Millionen von Nachrichten enthalten.

In der Regel gibt es mindestens eine Senderkomponente und mindestens eine Empfängerkomponente. Senderkomponenten fügen Nachrichten zur Warteschlange hinzu, während Empfängerkomponenten Nachrichten vom Anfang der Warteschlange zur Verarbeitung abrufen. Die folgende Abbildung zeigt mehrere Senderanwendungen beim Hinzufügen von Nachrichten zur Azure-Warteschlange und eine Empfängeranwendung beim Abrufen der Nachrichten.

![Abbildung der allgemeinen Architektur von Azure Queue Storage](../media/3-Azure_Queue.png)

Sie können Queue Storage für die folgenden Aufgaben verwenden:

- Erstellen eines Arbeitsbacklogs und Übermitteln von Nachrichten zwischen Azure-Webservern.
- Verteilen der Last auf verschiedene Webserver/Infrastrukturen und Verwalten von Traffic Bursts.
- Aufbauen eines robusten Schutzes vor Komponentenfehlern, wenn mehrere Benutzer gleichzeitig auf Ihre Daten zugreifen.

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Azure-Standardspeicher](../media/3-azure-standard-storage.png)
  :::column-end:::
    :::column span="3":::
**Azure Storage Standard**

Virtuelle Computer in Azure verwenden Datenträger zum Speichern von Betriebssystemen, Anwendungen und Daten. Azure-Standardspeicher bieten zuverlässige, kostengünstige Datenträgerunterstützung für virtuelle Computer mit nicht geschäftskritischen Workloads. Bei Verwendung von Storage Standard werden die Daten auf Festplattenlaufwerken (Hard Disk Drives, HDDs) gespeichert.

Wenn Sie mit virtuellen Computern arbeiten, können Sie standardmäßige SSD- und HDD-Datenträger für weniger kritische Workloads und Premium-SSD-Datenträger für unternehmenskritische Produktionsanwendungen verwenden. Azure-Datenträger stellen konsistent Dauerhaftigkeit auf Unternehmensniveau bereit, mit einer branchenweit führenden auf das Jahr umgerechneten Fehlerrate von NULL %. In der folgenden Abbildung wird gezeigt, wie ein virtueller Azure-Computer separate Datenträger nutzt, um unterschiedliche Daten zu speichern.

![Eine Abbildung, die zwei Datenträger innerhalb einer VM zeigt, auf einem wird das Betriebssystem gespeichert und auf dem anderen die Daten.](../media/3-Azure_disks.png)

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Speicherebenen](../media/3-storage-tiers.png)
  :::column-end:::
    :::column span="3":::
**Speicherebenen**

Azure bietet drei Speicherebenen für Blobobjektspeicher.

1. Die **heiße Speicherebene** ist für das Speichern von Daten optimiert, auf die häufig zugegriffen wird.

1. Die **kalte Speicherebene** ist für Daten optimiert, auf die selten zugegriffen wird, und die mindestens 30 Tage lang gespeichert werden.

1. Die **Archivspeicherebene** ist für Daten optimiert, auf die selten zugegriffen wird und die bei flexiblen Latenzanforderungen mindestens 180 Tage lang gespeichert werden.

:::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Verschlüsselung und Replikation](../media/3-azure-storage-encryption.png)
  :::column-end:::
    :::column span="3":::
**Verschlüsselung und Replikation**

Azure bietet Verschlüsselungs- und Replikationsfeatures, um für die Sicherheit und Hochverfügbarkeit Ihrer Daten zu sorgen.

#### <a name="encryption-for-storage-services"></a>Verschlüsselung für Speicherdienste

Ihnen stehen folgende Verschlüsselungstypen für Ihre Ressourcen zur Verfügung:

1. Die **Azure-Speicherdienstverschlüsselung (Azure Storage Service Encryption, SSE)** für ruhende Daten unterstützt Sie dabei, Ihre Daten zu sichern, um die Anforderungen Ihrer Organisation an die Sicherheit und Einhaltung von gesetzlichen Bestimmungen zu erfüllen. SSE verschlüsselt die Daten vor dem Speichern und entschlüsselt sie vor dem Abrufen. Verschlüsselung und Entschlüsselung sind für den Benutzer transparent.

1. Bei der **clientseitigen Verschlüsselung** werden die Daten bereits von den Clientbibliotheken verschlüsselt. Azure speichert die Daten verschlüsselt im Ruhezustand, und die Daten werden während des Abrufs entschlüsselt.

#### <a name="replication-for-storage-availability"></a>Replikation für Speicherverfügbarkeit

Wenn Sie ein Speicherkonto erstellen, wird ein Replikationstyp festgelegt. Das Replikationsfeature stellt sicher, dass Ihre Daten stabil und jederzeit verfügbar sind. Azure bietet regionale und geografische Replikationen, um Ihre Daten bei Naturkatastrophen und anderen lokalen Ereignissen wie Bränden oder Überflutungen zu schützen.

  :::column-end:::
:::row-end:::