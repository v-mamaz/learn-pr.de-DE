<span data-ttu-id="a2e14-101">Sobald wir einen Verweis auf ein Blob haben, können wir Daten hoch- und herunterladen.</span><span class="sxs-lookup"><span data-stu-id="a2e14-101">Once we have a reference to a blob, we can upload and download data.</span></span> <span data-ttu-id="a2e14-102">`ICloudBlob`-Objekte verfügen über die Methoden `Upload` und `Download`, die Bytearrays, Datenströme und Dateien als Quellen und Ziele unterstützen.</span><span class="sxs-lookup"><span data-stu-id="a2e14-102">`ICloudBlob` objects have `Upload` and `Download` methods that support byte arrays, streams, and files as sources and targets.</span></span> <span data-ttu-id="a2e14-103">Bestimmte Typen bieten zur Vereinfachung zusätzliche Methoden. `CloudBlockBlob` unterstützt z.B. das Hoch- und Herunterladen von Zeichenfolgen mit `UploadTextAsync` und `DownloadTextAsync`.</span><span class="sxs-lookup"><span data-stu-id="a2e14-103">Specific types have additional methods for convenience &mdash; for example, `CloudBlockBlob` supports uploading and downloading strings with `UploadTextAsync` and `DownloadTextAsync`.</span></span>

## <a name="creating-new-blobs"></a><span data-ttu-id="a2e14-104">Erstellen neuer Blobs</span><span class="sxs-lookup"><span data-stu-id="a2e14-104">Creating new blobs</span></span>

<span data-ttu-id="a2e14-105">Um ein neues Blob zu erstellen, rufen Sie eine der `Upload`-Methoden für ein Blob auf, das nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="a2e14-105">To create a new blob, you call one of the `Upload` methods on a blob that doesn't exist.</span></span> <span data-ttu-id="a2e14-106">Dies bewirkt das Erstellen des Blobs und Hochladen der Daten.</span><span class="sxs-lookup"><span data-stu-id="a2e14-106">This does two things: creates the blob and uploads the data.</span></span> 

## <a name="moving-data-to-and-from-blobs"></a><span data-ttu-id="a2e14-107">Verschieben von Daten in und aus Blobs</span><span class="sxs-lookup"><span data-stu-id="a2e14-107">Moving data to and from blobs</span></span>

<span data-ttu-id="a2e14-108">Das Verschieben von Daten in und aus einem Blob ist ein Netzwerkvorgang, der Zeit benötigt.</span><span class="sxs-lookup"><span data-stu-id="a2e14-108">Moving data to and from a blob is a network operation that takes time.</span></span> <span data-ttu-id="a2e14-109">Im Azure Storage SDK für .NET Core geben alle Methoden, die Netzwerkaktivität erfordern, Aufgaben des Typs `Task` zurück. Stellen Sie deshalb sicher, dass Ihre Controllermethoden entsprechend `async` sind und dass Sie mit `await` und nicht mit `Wait` auf Methodenaufrufe warten.</span><span class="sxs-lookup"><span data-stu-id="a2e14-109">In the Azure Storage SDK for .NET Core, all methods that require network activity return `Task`s, so make sure your controller methods are `async` as appropriate and that you are `await`ing method calls and not `Wait`ing on them.</span></span>

<span data-ttu-id="a2e14-110">Eine gängige Empfehlung beim Arbeiten mit großen Datenobjekten ist die Verwendung von Datenströmen anstelle von In-Memory-Strukturen wie Bytearrays oder Zeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="a2e14-110">A common recommendation when working with large data objects is to use streams instead of in-memory structures like byte arrays or strings.</span></span> <span data-ttu-id="a2e14-111">Dadurch wird vermieden, dass der gesamte Inhalt vor dem Senden zum Ziel im Speicher gepuffert wird.</span><span class="sxs-lookup"><span data-stu-id="a2e14-111">This avoids buffering the full content in memory before sending it to the target.</span></span> <span data-ttu-id="a2e14-112">ASP.NET Core unterstützt das Lesen und Schreiben von Datenströmen aus Anforderungen und Antworten.</span><span class="sxs-lookup"><span data-stu-id="a2e14-112">ASP.NET Core supports reading and writing streams from requests and responses.</span></span>

## <a name="concurrent-access"></a><span data-ttu-id="a2e14-113">Paralleler Zugriff</span><span class="sxs-lookup"><span data-stu-id="a2e14-113">Concurrent access</span></span>

<span data-ttu-id="a2e14-114">Es ist möglich, dass andere Prozesse Blobs hinzufügen, ändern oder löschen, während Ihre App sie verwendet.</span><span class="sxs-lookup"><span data-stu-id="a2e14-114">It is possible that other processes may be adding, changing, or deleting blobs as your app is using them.</span></span> <span data-ttu-id="a2e14-115">Programmieren Sie stets defensiv, und denken Sie an Probleme, die durch Parallelität verursacht werden, wie z.B. Blobs, die direkt gelöscht werden, wenn Sie versuchen, aus ihnen Daten herunterzuladen, oder Blobs, deren Inhalt sich ändert, wenn Sie dies nicht erwarten.</span><span class="sxs-lookup"><span data-stu-id="a2e14-115">Always code defensively and think about problems caused by concurrency, such as blobs that are deleted right as you try to download from them, or blobs whose contents change when you don't expect them to.</span></span> <span data-ttu-id="a2e14-116">Weitere Informationen zur Verwendung von „AccessConditions“ und Leases von Blobs zum Verwalten des parallelen Zugriffs auf Blobs finden Sie im Abschnitt „Weitere Ressourcen“ am Ende dieses Moduls.</span><span class="sxs-lookup"><span data-stu-id="a2e14-116">See the Additional Resources section at the end of this module for information about using AccessConditions and blob leases to manage concurrent blob access.</span></span>

## <a name="exercise"></a><span data-ttu-id="a2e14-117">Übung</span><span class="sxs-lookup"><span data-stu-id="a2e14-117">Exercise</span></span>

<span data-ttu-id="a2e14-118">Lassen Sie uns unsere App fertig stellen, indem wir Code zum Hoch- und Herunterladen hinzufügen und ihn dann zum Testen an Azure App Service verteilen.</span><span class="sxs-lookup"><span data-stu-id="a2e14-118">Let's finish our app by adding upload and download code, then deploy it to Azure App Service for testing.</span></span>

### <a name="upload"></a><span data-ttu-id="a2e14-119">Hochladen</span><span class="sxs-lookup"><span data-stu-id="a2e14-119">Upload</span></span>

<span data-ttu-id="a2e14-120">Um ein Blob hochzuladen, implementieren wir die `BlobStorage.Save`-Methode `GetBlockBlobReference` zum Abrufen von `CloudBlockBlob` aus dem Container.</span><span class="sxs-lookup"><span data-stu-id="a2e14-120">To upload a blob, we'll implement the `BlobStorage.Save` method using `GetBlockBlobReference` to get a `CloudBlockBlob` from the container.</span></span> <span data-ttu-id="a2e14-121">`FilesController.Upload` übergibt den Dateidatenstrom an `Save`, sodass wir `UploadFromStreamAsync` zum Durchführen des Hochladens mit maximaler Effizienz nutzen können.</span><span class="sxs-lookup"><span data-stu-id="a2e14-121">`FilesController.Upload` passes the file stream to `Save`, so we can use `UploadFromStreamAsync` to perform the upload for maximum efficiency.</span></span>

<span data-ttu-id="a2e14-122">Öffnen Sie `BlobStorage.cs` im Editor, und geben Sie die `Save`-Implementierung mit dem folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="a2e14-122">Open `BlobStorage.cs` in the editor and fill in the `Save` implementation with the following code:</span></span>

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> <span data-ttu-id="a2e14-123">Der hier gezeigte datenstrombasierte Uploadcode ist effizienter als das Einlesen der Datei in ein Bytearray, bevor sie an Azure Blob Storage gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="a2e14-123">The stream-based upload code shown here is more efficient than reading the file into a byte array before sending it to Azure Blob storage.</span></span> <span data-ttu-id="a2e14-124">Die Technik `IFormFile`, die wir verwenden, um die Datei vom Client abzurufen, ist jedoch keine echte durchgängige Streamingimplementierung und eignet sich nur für das Hochladen kleiner Dateien.</span><span class="sxs-lookup"><span data-stu-id="a2e14-124">However, the `IFormFile` technique we use to get the file from the client is not a true end-to-end streaming implementation and is only appropriate for handling uploads of small files.</span></span> <span data-ttu-id="a2e14-125">Informationen zu vollständig gestreamten Uploads von Dateien finden Sie im Abschnitt „Weitere Ressourcen“ am Ende dieses Moduls.</span><span class="sxs-lookup"><span data-stu-id="a2e14-125">See the Additional Resources section at the end of this module for information about fully streamed file uploads.</span></span>

### <a name="download"></a><span data-ttu-id="a2e14-126">Herunterladen</span><span class="sxs-lookup"><span data-stu-id="a2e14-126">Download</span></span>

<span data-ttu-id="a2e14-127">`BlobStorage.Load` gibt einen `Stream` zurück, was bedeutet, dass unser Code die Bytes aus dem Blobspeicher überhaupt nicht verschieben muss. Wir müssen nur einen Verweis auf den Blobdatenstrom zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="a2e14-127">`BlobStorage.Load` returns a `Stream`, meaning that our code doesn't need to physically move the bytes from Blob storage at all &mdash; we just need to return a reference to the blob stream.</span></span> <span data-ttu-id="a2e14-128">Dazu verwenden wir `OpenReadAsync`.</span><span class="sxs-lookup"><span data-stu-id="a2e14-128">We can do that with `OpenReadAsync`.</span></span> <span data-ttu-id="a2e14-129">ASP.NET Core übernimmt das Lesen und Schließen des Datenstroms, wenn die Clientantwort erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="a2e14-129">ASP.NET Core will handle reading and closing the stream when it builds the client response.</span></span>

<span data-ttu-id="a2e14-130">Füllen Sie `Load` mit diesem Code aus:</span><span class="sxs-lookup"><span data-stu-id="a2e14-130">Fill in `Load` with this code:</span></span>

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a><span data-ttu-id="a2e14-131">Bereitstellen und Ausführen in Azure</span><span class="sxs-lookup"><span data-stu-id="a2e14-131">Deploy and run in Azure</span></span>

<span data-ttu-id="a2e14-132">Unsere App ist fertig. Lassen Sie sie uns nun bereitstellen und verfolgen, wie sie funktioniert.</span><span class="sxs-lookup"><span data-stu-id="a2e14-132">Our app is finished &mdash; let's deploy it and see it work.</span></span> <span data-ttu-id="a2e14-133">Führen Sie den folgenden Code im Azure Cloud Shell-Terminal aus, um unseren Code zu erstellen und in einer neuen App Service-Instanz bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="a2e14-133">Run the following code in the Azure Cloud Shell terminal to build our code and deploy it to a new App Service instance.</span></span> <span data-ttu-id="a2e14-134">Wir fügen auch die Verbindungszeichenfolge unseres Speicherkontos zur Konfiguration hinzu.</span><span class="sxs-lookup"><span data-stu-id="a2e14-134">We also add our storage account connection string to configuration.</span></span>

```console

```

<span data-ttu-id="a2e14-135">...</span><span class="sxs-lookup"><span data-stu-id="a2e14-135">...</span></span>

<span data-ttu-id="a2e14-136">Laden Sie einige Dateien hoch und herunter, um die App zu testen. Führen Sie dann die folgenden Befehle in der Shell aus, um die hochgeladenen Blobs anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="a2e14-136">Upload and download some files to test the app, then run the following in the shell to see the blobs that have been uploaded:</span></span>

```console

```

<span data-ttu-id="a2e14-137">**TODO pic from portal**</span><span class="sxs-lookup"><span data-stu-id="a2e14-137">**TODO pic from portal**</span></span>