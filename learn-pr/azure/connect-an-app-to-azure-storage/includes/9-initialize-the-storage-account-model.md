Die Clientbibliothek von Azure Storage stellt ein Objektmodell bereit, das für die Interaktion mit Azure Storage-Konten verwendet wird. Es wird dazu verwendet, schnell eine Verbindung mit dem Azure Storage-Konto herzustellen und die Dienst-APIs von Azure Storage zu verwenden. 

## <a name="azure-storage-client-library-object-model"></a>Objektmodell der Azure Storage-Clientbibliothek

::: zone pivot="csharp"

Die Grundlage für das Objektmodell des Storage-Konto in der Clientbibliothek für .NET Core ist die Klasse `CloudStorageAccount`. Die einfachste Methode zum Initialisieren des Objektmodells ist die Verwendung von `CloudStorageAccount.Parse` oder `CloudStorageAccount.TryParse` zum Analysieren der Verbindungszeichenfolge.

> [!NOTE]
> Die Clientbibliothek versucht erst eine Verbindung herzustellen, wenn ein Vorgang aufgerufen wird, für den eine Verbindung erforderlich ist. `Parse()` und `TryParse()` stellen nur sicher, dass die Verbindungszeichenfolge korrekt formatiert ist, es wird nicht überprüft, ob das Konto existiert oder der Schlüssel richtig ist. 

Die resultierende `CloudStorageAccount` von zurückgegebene Instanz der `Parse()` oder `TryParse()` Methodenaufruf stellt Methoden zum Erstellen eines Clients Objekte, die Zugriff auf die Speicherdienste von Azure-Blob, Dateien, Warteschlangen- und Tabellenspeicherdienste. 

Der folgende Codeausschnitt veranschaulicht ein Beispiel zum Erstellen eines Clients zur Verwendung eines Blobspeichers:

```csharp
using Microsoft.WindowsAzure.Storage;

CloudStorageAccount storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");

CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient()
```

`CloudStorageAccount` und die Clientobjekte sind einfach, sie können bei Bedarf oder direkt für die Freigabe in der Anwendung erstellt werden. Die Verwendung von `CloudStorageAccount.TryParse()` in der Nähe des Einstiegspunkts Ihrer Anwendung ist ein standardisierter Ansatz, mit dem Sie eine Instanz erstellen und in Ihrer Anwendung zur Verfügung stellen können, um Clientinstanzen zu erstellen.

Nachdem Sie ein Clientobjekt zu einem bestimmten Speicher-Typ haben, können Sie Methoden verwenden, um die eigentliche Arbeit zu erledigen. Methoden, die Netzwerk-Aufrufe sind absichtlich asynchron – in .NET verwenden wir die `async` und `await` Stichworte, um effizient mit diesen Methoden arbeiten.

Als Beispiel verwenden wir die `CloudBlobClient` zum Erstellen einer _blobcontainer_ und Hochladen einer Datei in Blob Storage.

```csharp
// Create a local CloudBlobContainer object. No network call.
string containerName = "myblobcontainer";
CloudBlobContainer blobContainer = blobClient.GetContainerReference(containerName);

// This makes an actual service call to the Azure Storage service. 
// Unless this call fails, the container will have been created.
await blobContainer.CreateAsync();

// Create a local object to represent our blob. No network call.
string blobName = "myphoto";
CloudBlockBlob blob = blobContainer.GetBlockBlobReference(blobName);

// This transfers data in the file to the blob on the service.
string filename = "photo.png";
await blob.UploadFromFileAsync(fileName);
```

::: zone-end

::: zone pivot="javascript"

Die Grundlage für das Objektmodell des Storage-Konto in der **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** ist die `azurestorage` Objekt. Dies wird durch Hinzufügen, erstellt die **Azure Storage-** Modul, um Ihre app über eine `require` Anweisung.

```javascript
const storage = require('azure-storage');
```

Dieses Objekt enthält eine Reihe von _Factory_ Methoden, die bestimmten Objekte, die Arbeit mit jedes Facet von Azure-Speicher zu erstellen. Rufen Sie `createXXX` Methoden, um jedes Objekt zu erstellen.

| Typ | Methode | Rückgabe |
|--------|---------|-------------|
| **Blob** | `createBlobService` | `BlobService` |
| **Tabelle** | `createTableService` | `TableService` |
| **Warteschlange** | `createQueueService` | `QueueService` |
| **Datei** | `createFileService` | `FileService` |

> [!NOTE]
> Die Clientbibliothek versucht erst eine Verbindung herzustellen, wenn ein Vorgang aufgerufen wird, für den eine Verbindung erforderlich ist. Jede dieser `create` Methoden zurückgeben, ein einfaches Objekt, das Zugriff auf den Speichertyp darstellt&mdash;überprüft nicht die Verbindung oder die Zugriffstaste verwendet wird.

Nachdem Sie ein Dienstobjekt zu einem bestimmten Speicher-Typ haben, können Sie Methoden verwenden, um die eigentliche Arbeit zu erledigen. Methoden, mit denen Netzwerkaufrufe sind absichtlich asynchron. Derzeit unterstützt die Bibliothek _Rückrufe_ asynchrone Ergebnisse zurückgegeben. Hier ist z. B. Code, der einen Blob-Container erstellt.

```javascript
var azure = require('azure-storage');
var blobService = azure.createBlobService();

blobService.createContainerIfNotExists('myblobcontainer', function(err, result, response) {
  if (!err) {
    // if result.created = true, container was created.
    // if result.created = false, container already existed.
  }
});
```

Dieser Ansatz funktioniert gut, aber sie ist dazu führen, dass viel Code hinzugefügt wird, in die Rückrufe, die nicht handhabbaren abrufen können. Ein besserer Ansatz in JavaScript ist die Verwendung _verspricht_ mit diesen Methoden arbeiten. Stehen verschiedene hervorragende Bibliotheken, die Rückruf-Stil-Methoden in Zusagen konvertiert&mdash;Sie auswählen können, die Sie lieber ein.

Hier verwenden wir die `util.promisify` Funktion auf Knoten aus und Verwenden der `BlobService` zum Erstellen des Containers und Hochladen einer Datei in Blob Storage. Darüber hinaus verwenden wir die `async` und `await` Schlüsselwörter mit Zusagen etwas ausführlicher auf natürliche Weise zu arbeiten.

```javascript
const util = require('util');
const storage = require('azure-storage');

const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);
const uploadBlobAsync = util.promisify(blobService.createBlockBlobFromLocalFile).bind(blobService);

async function main() {
    try {
        // This makes an actual service call to the Azure Storage service. 
        // Unless this call fails, the container will have been created.
        await createContainerAsync(containerName);

        // This transfers data in the file to the blob on the service.
        var uploadResult = await uploadBlobAsync(containerName, "myphoto", "photo.png");
        if (uploadResult) {
            console.log("blob uploaded");
        }
    }
    catch (err) {
        console.log(err.message);
    }
}

main();
```
::: zone-end

Probieren Sie dies in unserer app.