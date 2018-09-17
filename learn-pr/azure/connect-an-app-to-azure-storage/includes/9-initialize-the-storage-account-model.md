<span data-ttu-id="a372b-101">Die Azure Storage-Clientbibliothek stellt ein Objektmodell für die Interaktion mit Azure-Speicherkonten bereit.</span><span class="sxs-lookup"><span data-stu-id="a372b-101">The Azure Storage client library provides an object model that is used to interact with Azure storage accounts.</span></span> <span data-ttu-id="a372b-102">Es dient dazu, schnell eine Verbindung mit einem Azure-Speicherkonto herzustellen und die APIs des Azure Storage-Diensts zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="a372b-102">It's used to quickly connect to an Azure storage account and use the Azure Storage service APIs.</span></span> 

## <a name="azure-storage-client-library-object-model"></a><span data-ttu-id="a372b-103">Objektmodell der Azure Storage-Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="a372b-103">Azure Storage client library object model</span></span>

<span data-ttu-id="a372b-104">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="a372b-104">::: zone pivot="csharp"</span></span>

<span data-ttu-id="a372b-105">In der .NET Core-Clientbibliothek basiert das Speicherkonto-Objektmodell auf der Klasse `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="a372b-105">The foundation of the storage account object model in the .NET Core client library is the class `CloudStorageAccount`.</span></span> <span data-ttu-id="a372b-106">Die einfachste Methode zum Initialisieren des Objektmodells ist die Analyse der Verbindungszeichenfolge mithilfe von `CloudStorageAccount.Parse` oder `CloudStorageAccount.TryParse`.</span><span class="sxs-lookup"><span data-stu-id="a372b-106">The simplest way to initialize the object model is to use `CloudStorageAccount.Parse` or `CloudStorageAccount.TryParse` to parse the connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="a372b-107">Die Clientbibliothek stellt erst eine Verbindung her, wenn ein Vorgang aufgerufen wird, für den eine Verbindung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="a372b-107">The client library will not attempt to connect until an operation is invoked that requires it.</span></span> <span data-ttu-id="a372b-108">`Parse()` und `TryParse()` stellen nur sicher, dass die Verbindungszeichenfolge korrekt formatiert ist. Es wird nicht überprüft, ob das Konto vorhanden oder der Schlüssel korrekt ist.</span><span class="sxs-lookup"><span data-stu-id="a372b-108">`Parse()` and `TryParse()` only guarantee that the connection string is well-formatted; they don't verify that the account exists or that the key is correct.</span></span> 

<span data-ttu-id="a372b-109">Die resultierende `CloudStorageAccount`-Instanz, die nach dem Aufruf der Methode `Parse()` oder `TryParse()` zurückgegeben wird, macht Methoden zum Erstellen eines Clientobjekts für den Zugriff auf die Speicherdienste Azure Blob, Azure Files, Azure Queue und Azure Table verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a372b-109">The resulting `CloudStorageAccount` instance returned from the `Parse()` or `TryParse()` method call exposes methods to create a client objects to access the Azure Blob, Files, Queue and Table storage services.</span></span> 

<span data-ttu-id="a372b-110">Der folgende Codeausschnitt zeigt ein Beispiel zum Erstellen eines Clients für Blobspeicher:</span><span class="sxs-lookup"><span data-stu-id="a372b-110">The code snippet below shows an example of creating a client to use for blob storage:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;

CloudStorageAccount storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");

CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient()
```

<span data-ttu-id="a372b-111">`CloudStorageAccount` und die Clientobjekte sind einfache Elemente und können entweder bei Bedarf oder vorab erstellt und innerhalb Ihrer Anwendung freigegeben werden.</span><span class="sxs-lookup"><span data-stu-id="a372b-111">`CloudStorageAccount` and the client objects are lightweight and can be created on demand or created up front to be shared within your application.</span></span> <span data-ttu-id="a372b-112">Die Verwendung von `CloudStorageAccount.TryParse()` in der Nähe des Einstiegspunkts Ihrer Anwendung ist ein gängiger Ansatz, mit dem Sie eine Instanz erstellen und in Ihrer Anwendung verfügbar machen können, um Clientinstanzen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a372b-112">A standard approach is to use `CloudStorageAccount.TryParse()` near the entry point of your application to create an instance, and make it available within your application for creating client instances.</span></span>

<span data-ttu-id="a372b-113">Sobald Sie über ein Clientobjekt für einen bestimmten Speichertyp verfügen, können Sie mithilfe von Methoden Aufgaben erledigen.</span><span class="sxs-lookup"><span data-stu-id="a372b-113">Once you have a client object to a specific storage type, you can use methods to perform actual work.</span></span> <span data-ttu-id="a372b-114">Methoden für Netzwerkaufrufe sind bewusst asynchron. In .NET verwenden wir die Schlüsselwörter `async` und `await`, um effizient mit diesen Methoden zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="a372b-114">Methods which make network calls are intentionally asynchronous - in .NET we use the `async` and `await` keywords to work with these methods efficiently.</span></span>

<span data-ttu-id="a372b-115">So können wir beispielsweise `CloudBlobClient` verwenden, um einen _Blobcontainer_ zu erstellen und eine Datei in den Blobspeicher hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="a372b-115">As an example, we can use the `CloudBlobClient` to create a _blob container_ and upload a file to blob storage.</span></span>

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

<span data-ttu-id="a372b-116">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="a372b-116">::: zone-end</span></span>

<span data-ttu-id="a372b-117">::: zone-pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="a372b-117">::: zone-pivot="javascript"</span></span>

<span data-ttu-id="a372b-118">In der **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** basiert das Speicherkonto-Objektmodell auf dem Objekt `azurestorage`.</span><span class="sxs-lookup"><span data-stu-id="a372b-118">The foundation of the storage account object model in the **Microsoft Azure Storage Client Library for Node.js and JavaScript** is the `azurestorage` object.</span></span> <span data-ttu-id="a372b-119">Zur Erstellung wird Ihrer App über eine `require`-Anweisung das Modul **azure-storage** hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="a372b-119">This is created by adding the **azure-storage** module to your app through a `require` statement.</span></span>

```javascript
const storage = require('azure-storage');
```

<span data-ttu-id="a372b-120">Dieses Objekt bietet eine Reihe von _factory_-Methoden, die spezifische Objekte für die Verwendung sämtlicher Facetten von Azure-Speicher erstellen.</span><span class="sxs-lookup"><span data-stu-id="a372b-120">This object provides a series of _factory_ methods that create specific objects to work with each facet of Azure storage.</span></span> <span data-ttu-id="a372b-121">Zur Erstellung der einzelnen Objekte muss jeweils eine Methode vom Typ `createXXX` aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="a372b-121">You call `createXXX` methods to create each object.</span></span>

| <span data-ttu-id="a372b-122">Typ</span><span class="sxs-lookup"><span data-stu-id="a372b-122">Type</span></span> | <span data-ttu-id="a372b-123">Methode</span><span class="sxs-lookup"><span data-stu-id="a372b-123">Method</span></span> | <span data-ttu-id="a372b-124">Rückgabe</span><span class="sxs-lookup"><span data-stu-id="a372b-124">Returns</span></span> |
|--------|---------|-------------|
| <span data-ttu-id="a372b-125">**Blob**</span><span class="sxs-lookup"><span data-stu-id="a372b-125">**Blob**</span></span> | `createBlobService` | `BlobService` |
| <span data-ttu-id="a372b-126">**Tabelle**</span><span class="sxs-lookup"><span data-stu-id="a372b-126">**Table**</span></span> | `createTableService` | `TableService` |
| <span data-ttu-id="a372b-127">**Warteschlange**</span><span class="sxs-lookup"><span data-stu-id="a372b-127">**Queue**</span></span> | `createQueueService` | `QueueService` |
| <span data-ttu-id="a372b-128">**Datei**</span><span class="sxs-lookup"><span data-stu-id="a372b-128">**File**</span></span> | `createFileService` | `FileService` |

> [!NOTE]
> <span data-ttu-id="a372b-129">Die Clientbibliothek stellt erst eine Verbindung her, wenn ein Vorgang aufgerufen wird, für den eine Verbindung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="a372b-129">The client library will not attempt to connect until an operation is invoked that requires it.</span></span> <span data-ttu-id="a372b-130">Jede dieser `create`-Methoden gibt ein einfaches Objekt zurück, das den Zugriff auf den Speichertyp darstellt. Die Verbindung und der verwendete Zugriffsschlüssel werden dabei nicht überprüft.</span><span class="sxs-lookup"><span data-stu-id="a372b-130">Each of these `create` methods return a lightweight object representing access to the storage type - it does not validate the connection or the access key being used.</span></span> 

<span data-ttu-id="a372b-131">Sobald Sie über ein Dienstobjekt für einen bestimmten Speichertyp verfügen, können Sie mithilfe von Methoden Aufgaben erledigen.</span><span class="sxs-lookup"><span data-stu-id="a372b-131">Once you have a service object to a specific storage type, you can use methods to perform actual work.</span></span> <span data-ttu-id="a372b-132">Methoden für Netzwerkaufrufe sind bewusst asynchron.</span><span class="sxs-lookup"><span data-stu-id="a372b-132">Methods which make network calls are intentionally asynchronous.</span></span> <span data-ttu-id="a372b-133">Die Bibliothek unterstützt _Rückrufe_ für die Rückgabe asynchroner Ergebnisse.</span><span class="sxs-lookup"><span data-stu-id="a372b-133">The library current supports _callbacks_ to return asynchronous results.</span></span> <span data-ttu-id="a372b-134">Hier sehen Sie beispielsweise Code zum Erstellen eines Blobcontainers.</span><span class="sxs-lookup"><span data-stu-id="a372b-134">For example, here is code that creates a blob container.</span></span>

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

<span data-ttu-id="a372b-135">Dieser Ansatz funktioniert, führt allerdings häufig dazu, dass dem Rückruf sehr viel Code hinzugefügt wird, was die Verwaltung erheblich erschweren kann.</span><span class="sxs-lookup"><span data-stu-id="a372b-135">This approach works fine, but tends to lead to a lot of code being added into the callbacks which can get unmanagement.</span></span> <span data-ttu-id="a372b-136">In JavaScript empfiehlt es sich daher, bei diesen Methoden mit _Zusagen_ zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="a372b-136">A better approach in JavaScript is to use _promises_ to work with these methods.</span></span> <span data-ttu-id="a372b-137">Ihnen stehen mehrere hervorragende Bibliotheken zur Verfügung, die Methoden mit Rückruf in Zusagen konvertieren.</span><span class="sxs-lookup"><span data-stu-id="a372b-137">There are several great libraries which will convert callback-style methods into promises - you can pick the one you prefer.</span></span>

<span data-ttu-id="a372b-138">Hier verwenden wir das Feature `util.promisify` von Node sowie `BlobService`, um den Container zu erstellen und eine Datei in den Blobspeicher hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="a372b-138">Here, we'll use the `util.promisify` feature from Node and use the `BlobService` to create the container and upload a file to blob storage.</span></span> <span data-ttu-id="a372b-139">Darüber hinaus verwenden wir die Schlüsselwörter `async` und `await`, um die Arbeit mit Zusagen etwas natürlicher zu gestalten.</span><span class="sxs-lookup"><span data-stu-id="a372b-139">In addition, we'll use the `async` and `await` keywords to work with the promises a bit more naturally.</span></span>

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
<span data-ttu-id="a372b-140">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="a372b-140">::: zone-end</span></span>

<span data-ttu-id="a372b-141">Probieren wir das doch einmal in unserer App aus.</span><span class="sxs-lookup"><span data-stu-id="a372b-141">Let's try this in our app.</span></span>