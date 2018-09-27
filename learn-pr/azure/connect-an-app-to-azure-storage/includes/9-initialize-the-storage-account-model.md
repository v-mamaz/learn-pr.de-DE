Die Azure Storage-Clientbibliothek stellt ein Objektmodell für die Interaktion mit Azure-Speicherkonten bereit. Es dient dazu, schnell eine Verbindung mit einem Azure-Speicherkonto herzustellen und die APIs des Azure Storage-Diensts zu verwenden. 

## <a name="azure-storage-client-library-object-model"></a>Objektmodell der Azure Storage-Clientbibliothek

::: zone pivot="csharp"

In der .NET Core-Clientbibliothek basiert das Speicherkonto-Objektmodell auf der Klasse `CloudStorageAccount`. Die einfachste Methode zum Initialisieren des Objektmodells ist die Analyse der Verbindungszeichenfolge mithilfe von `CloudStorageAccount.Parse` oder `CloudStorageAccount.TryParse`.

> [!NOTE]
> Die Clientbibliothek stellt erst eine Verbindung her, wenn ein Vorgang aufgerufen wird, für den eine Verbindung erforderlich ist. `Parse()` und `TryParse()` stellen nur sicher, dass die Verbindungszeichenfolge korrekt formatiert ist. Es wird nicht überprüft, ob das Konto vorhanden oder der Schlüssel korrekt ist. 

Die resultierende `CloudStorageAccount`-Instanz, die nach dem Aufruf der Methode `Parse()` oder `TryParse()` zurückgegeben wird, macht Methoden zum Erstellen eines Clientobjekts für den Zugriff auf die Speicherdienste Azure Blob, Azure Files, Azure Queue und Azure Table verfügbar. 

Der folgende Codeausschnitt zeigt ein Beispiel zum Erstellen eines Clients für Blobspeicher:

```csharp
using Microsoft.WindowsAzure.Storage;

CloudStorageAccount storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");

CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient()
```

`CloudStorageAccount` und die Clientobjekte sind einfache Elemente und können entweder bei Bedarf oder vorab erstellt und innerhalb Ihrer Anwendung freigegeben werden. Die Verwendung von `CloudStorageAccount.TryParse()` in der Nähe des Einstiegspunkts Ihrer Anwendung ist ein gängiger Ansatz, mit dem Sie eine Instanz erstellen und in Ihrer Anwendung verfügbar machen können, um Clientinstanzen zu erstellen.

Sobald Sie über ein Clientobjekt für einen bestimmten Speichertyp verfügen, können Sie mithilfe von Methoden Aufgaben erledigen. Methoden für Netzwerkaufrufe sind bewusst asynchron. In .NET verwenden wir die Schlüsselwörter `async` und `await`, um effizient mit diesen Methoden zu arbeiten.

So können wir beispielsweise `CloudBlobClient` verwenden, um einen _Blobcontainer_ zu erstellen und eine Datei in den Blobspeicher hochzuladen.

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

In der **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** basiert das Speicherkonto-Objektmodell auf dem Objekt `azurestorage`. Zur Erstellung wird Ihrer App über eine `require`-Anweisung das Modul **azure-storage** hinzugefügt.

```javascript
const storage = require('azure-storage');
```

Dieses Objekt bietet eine Reihe von _factory_-Methoden, die spezifische Objekte für die Verwendung sämtlicher Facetten von Azure-Speicher erstellen. Zur Erstellung der einzelnen Objekte muss jeweils eine Methode vom Typ `createXXX` aufgerufen werden.

| Typ | Methode | Rückgabe |
|--------|---------|-------------|
| **Blob** | `createBlobService` | `BlobService` |
| **Tabelle** | `createTableService` | `TableService` |
| **Warteschlange** | `createQueueService` | `QueueService` |
| **Datei** | `createFileService` | `FileService` |

> [!NOTE]
> Die Clientbibliothek stellt erst eine Verbindung her, wenn ein Vorgang aufgerufen wird, für den eine Verbindung erforderlich ist. Jede dieser `create`-Methoden gibt ein einfaches Objekt zurück, das den Zugriff auf den Speichertyp darstellt. Die Verbindung und der verwendete Zugriffsschlüssel werden dabei nicht überprüft.

Sobald Sie über ein Dienstobjekt für einen bestimmten Speichertyp verfügen, können Sie mithilfe von Methoden Aufgaben erledigen. Methoden für Netzwerkaufrufe sind absichtlich asynchron. Die Bibliothek unterstützt _Rückrufe_ derzeit für die Rückgabe asynchroner Ergebnisse. Hier sehen Sie beispielsweise Code zum Erstellen eines Blobcontainers.

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

Dieser Ansatz funktioniert, führt allerdings häufig dazu, dass dem Rückruf sehr viel Code hinzugefügt wird, was die Verwaltung erheblich erschweren kann. In JavaScript empfiehlt es sich daher, bei diesen Methoden mit _Zusagen_ zu arbeiten. Ihnen stehen mehrere gute Bibliotheken zur Verfügung, die Methoden mit Rückruf in Zusagen konvertieren. Wählen Sie die Bibliothek aus, die Sie bevorzugen.

Hier verwenden wir das Feature `util.promisify` von Node sowie `BlobService`, um den Container zu erstellen und eine Datei in den Blobspeicher hochzuladen. Darüber hinaus verwenden wir die Schlüsselwörter `async` und `await`, um die Arbeit mit Zusagen etwas natürlicher zu gestalten.

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

Probieren wir das doch einmal in unserer App aus.