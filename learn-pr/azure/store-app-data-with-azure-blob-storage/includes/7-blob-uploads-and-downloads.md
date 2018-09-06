<span data-ttu-id="e3a29-101">Sobald wir einen Verweis auf ein Blob haben, können wir Daten hoch- und herunterladen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-101">Once we have a reference to a blob, we can upload and download data.</span></span> <span data-ttu-id="e3a29-102">`ICloudBlob`-Objekte verfügen über die Methoden `Upload` und `Download`, die Bytearrays, Datenströme und Dateien als Quellen und Ziele unterstützen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-102">`ICloudBlob` objects have `Upload` and `Download` methods that support byte arrays, streams, and files as sources and targets.</span></span> <span data-ttu-id="e3a29-103">Bestimmte Typen bieten zur Vereinfachung zusätzliche Methoden. `CloudBlockBlob` unterstützt z.B. das Hoch- und Herunterladen von Zeichenfolgen mit `UploadTextAsync` und `DownloadTextAsync`.</span><span class="sxs-lookup"><span data-stu-id="e3a29-103">Specific types have additional methods for convenience &mdash; for example, `CloudBlockBlob` supports uploading and downloading strings with `UploadTextAsync` and `DownloadTextAsync`.</span></span>

## <a name="creating-new-blobs"></a><span data-ttu-id="e3a29-104">Erstellen neuer Blobs</span><span class="sxs-lookup"><span data-stu-id="e3a29-104">Creating new blobs</span></span>

<span data-ttu-id="e3a29-105">Rufen Sie eine der `Upload`-Methoden für einen Verweis auf ein Blob auf, das nicht im Speicher vorhanden ist, um ein neues Blob zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-105">To create a new blob, you call one of the `Upload` methods on a reference to a blob that doesn't exist in storage.</span></span> <span data-ttu-id="e3a29-106">Dadurch werden die Daten hochgeladen und das Blob wird erstellt.</span><span class="sxs-lookup"><span data-stu-id="e3a29-106">This does two things: creates the blob in storage and uploads the data.</span></span>

## <a name="moving-data-to-and-from-blobs"></a><span data-ttu-id="e3a29-107">Verschieben von Daten in und aus Blobs</span><span class="sxs-lookup"><span data-stu-id="e3a29-107">Moving data to and from blobs</span></span>

<span data-ttu-id="e3a29-108">Das Verschieben von Daten in und aus einem Blob ist ein Netzwerkvorgang, der Zeit in Anspruch nimmt.</span><span class="sxs-lookup"><span data-stu-id="e3a29-108">Moving data to and from a blob is a network operation that takes time.</span></span> <span data-ttu-id="e3a29-109">Im Azure Storage SDK für .NET Core geben alle Methoden, die Netzwerkaktivität erfordern, Aufgaben des Typs `Task` zurück. Stellen Sie deshalb sicher, dass Sie `await` entsprechend in Ihren Controllermethoden verwenden.</span><span class="sxs-lookup"><span data-stu-id="e3a29-109">In the Azure Storage SDK for .NET Core, all methods that require network activity return `Task`s, so make sure you use `await` in your controller methods appropriately.</span></span>

<span data-ttu-id="e3a29-110">Eine gängige Empfehlung beim Arbeiten mit großen Datenobjekten ist die Verwendung von Datenströmen anstelle von In-Memory-Strukturen wie Bytearrays oder Zeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-110">A common recommendation when working with large data objects is to use streams instead of in-memory structures like byte arrays or strings.</span></span> <span data-ttu-id="e3a29-111">Dadurch wird vermieden, dass der gesamte Inhalt vor dem Senden zum Ziel im Speicher gepuffert wird.</span><span class="sxs-lookup"><span data-stu-id="e3a29-111">This avoids buffering the full content in memory before sending it to the target.</span></span> <span data-ttu-id="e3a29-112">ASP.NET Core unterstützt das Lesen und Schreiben von Datenströmen aus Anforderungen und Antworten.</span><span class="sxs-lookup"><span data-stu-id="e3a29-112">ASP.NET Core supports reading and writing streams from requests and responses.</span></span>

## <a name="concurrent-access"></a><span data-ttu-id="e3a29-113">Paralleler Zugriff</span><span class="sxs-lookup"><span data-stu-id="e3a29-113">Concurrent access</span></span>

<span data-ttu-id="e3a29-114">Andere Prozesse können Blobs hinzufügen, ändern oder löschen, während Ihre App sie verwendet.</span><span class="sxs-lookup"><span data-stu-id="e3a29-114">Other processes may be adding, changing, or deleting blobs as your app is using them.</span></span> <span data-ttu-id="e3a29-115">Programmieren Sie stets defensiv, und denken Sie an Probleme, die durch Parallelität verursacht werden, z.B. Blobs, die direkt gelöscht werden, wenn Sie versuchen, aus ihnen Daten herunterzuladen, oder Blobs, deren Inhalt sich ändert, wenn Sie dies nicht erwarten.</span><span class="sxs-lookup"><span data-stu-id="e3a29-115">Always code defensively and think about problems caused by concurrency, such as blobs that are deleted right as you try to download from them, or blobs whose contents change when you don't expect them to.</span></span> <span data-ttu-id="e3a29-116">Weitere Informationen zur Verwendung von „AccessConditions“ und Leases von Blobs zum Verwalten des parallelen Zugriffs auf Blobs finden Sie im Abschnitt „Weitere Informationen“ am Ende dieses Moduls.</span><span class="sxs-lookup"><span data-stu-id="e3a29-116">See the Further Reading section at the end of this module for information about using AccessConditions and blob leases to manage concurrent blob access.</span></span>

## <a name="exercise"></a><span data-ttu-id="e3a29-117">Übung</span><span class="sxs-lookup"><span data-stu-id="e3a29-117">Exercise</span></span>

<span data-ttu-id="e3a29-118">Lassen Sie uns unsere App fertig stellen, indem wir Code zum Hoch- und Herunterladen hinzufügen und ihn dann zum Testen an Azure App Service verteilen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-118">Let's finish our app by adding upload and download code, then deploy it to Azure App Service for testing.</span></span>

### <a name="upload"></a><span data-ttu-id="e3a29-119">Hochladen</span><span class="sxs-lookup"><span data-stu-id="e3a29-119">Upload</span></span>

<span data-ttu-id="e3a29-120">Um ein Blob hochzuladen, implementieren wir die `BlobStorage.Save`-Methode `GetBlockBlobReference` zum Abrufen von `CloudBlockBlob` aus dem Container.</span><span class="sxs-lookup"><span data-stu-id="e3a29-120">To upload a blob, we'll implement the `BlobStorage.Save` method using `GetBlockBlobReference` to get a `CloudBlockBlob` from the container.</span></span> <span data-ttu-id="e3a29-121">`FilesController.Upload` übergibt den Dateidatenstrom an `Save`, sodass Sie `UploadFromStreamAsync` zum Durchführen des Hochladens mit maximaler Effizienz nutzen können.</span><span class="sxs-lookup"><span data-stu-id="e3a29-121">`FilesController.Upload` passes the file stream to `Save`, so we can use `UploadFromStreamAsync` to perform the upload for maximum efficiency.</span></span>

<span data-ttu-id="e3a29-122">Öffnen Sie `BlobStorage.cs` im Editor, und ersetzen Sie `Save` durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="e3a29-122">Open `BlobStorage.cs` in the editor and replace `Save` with the following code:</span></span>

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
> <span data-ttu-id="e3a29-123">Der hier gezeigte datenstrombasierte Uploadcode ist effizienter als das Einlesen der Datei in ein Bytearray, bevor sie an Azure Blob Storage gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="e3a29-123">The stream-based upload code shown here is more efficient than reading the file into a byte array before sending it to Azure Blob storage.</span></span> <span data-ttu-id="e3a29-124">Die ASP.NET Core-Technik `IFormFile`, die wir verwenden, um die Datei vom Client abzurufen, ist jedoch keine echte durchgängige Streamingimplementierung und eignet sich nur für das Hochladen kleiner Dateien.</span><span class="sxs-lookup"><span data-stu-id="e3a29-124">However, the ASP.NET Core `IFormFile` technique we use to get the file from the client is not a true end-to-end streaming implementation and is only appropriate for handling uploads of small files.</span></span> <span data-ttu-id="e3a29-125">Informationen zu vollständig gestreamten Uploads von Dateien finden Sie im Abschnitt „Weitere Informationen“ am Ende dieses Moduls.</span><span class="sxs-lookup"><span data-stu-id="e3a29-125">See the Further Reading section at the end of this module for information about fully streamed file uploads.</span></span>

### <a name="download"></a><span data-ttu-id="e3a29-126">Herunterladen</span><span class="sxs-lookup"><span data-stu-id="e3a29-126">Download</span></span>

<span data-ttu-id="e3a29-127">`BlobStorage.Load` gibt einen `Stream` zurück, was bedeutet, dass unser Code die Bytes aus dem Blobspeicher überhaupt nicht verschieben muss. Wir müssen nur einen Verweis auf den Blobdatenstrom zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="e3a29-127">`BlobStorage.Load` returns a `Stream`, meaning that our code doesn't need to physically move the bytes from Blob storage at all &mdash; we just need to return a reference to the blob stream.</span></span> <span data-ttu-id="e3a29-128">Dazu verwenden wir `OpenReadAsync`.</span><span class="sxs-lookup"><span data-stu-id="e3a29-128">We can do that with `OpenReadAsync`.</span></span> <span data-ttu-id="e3a29-129">ASP.NET Core übernimmt das Lesen und Schließen des Datenstroms, wenn die Clientantwort erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="e3a29-129">ASP.NET Core will handle reading and closing the stream when it builds the client response.</span></span>

<span data-ttu-id="e3a29-130">Ersetzen Sie `Load` durch den folgenden Code, und speichern Sie Ihre Arbeit:</span><span class="sxs-lookup"><span data-stu-id="e3a29-130">Replace `Load` with this code and save your work:</span></span>

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a><span data-ttu-id="e3a29-131">Bereitstellen und Ausführen in Azure</span><span class="sxs-lookup"><span data-stu-id="e3a29-131">Deploy and run in Azure</span></span>

<span data-ttu-id="e3a29-132">Ihre App ist fertig. Stellen Sie sie bereit, und sehen Sie sich an, wie sie funktioniert.</span><span class="sxs-lookup"><span data-stu-id="e3a29-132">Our app is finished &mdash; let's deploy it and see it work.</span></span> <span data-ttu-id="e3a29-133">Erstellen Sie eine App Service-App, und konfigurieren Sie diese mit den Anwendungseinstellungen für die Verbindungszeichenfolge und den Containernamen des Speicherkontos.</span><span class="sxs-lookup"><span data-stu-id="e3a29-133">Create an App Service app and configure it with application settings for our storage account connection string and container name.</span></span> <span data-ttu-id="e3a29-134">Rufen Sie mit `az storage account show-connection-string` die Verbindungszeichenfolge des Speicherkontos ab, und legen Sie `files` für den Namen des Containers fest.</span><span class="sxs-lookup"><span data-stu-id="e3a29-134">Get the storage account's connection string with `az storage account show-connection-string` and set the name of the container to be `files`.</span></span>

<span data-ttu-id="e3a29-135">Der App-Name muss global eindeutig sein. Daher müssen Sie für `<your-unique-app-name>` einen eigenen Namen auswählen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-135">The app name needs to be globally unique, so you'll need to choose your own name to fill in `<your-unique-app-name>`.</span></span>

```azurecli
az appservice plan create --name blob-exercise-plan --resource-group blob-exercise-group
az webapp create --name <your-unique-app-name> --plan blob-exercise-plan --resource-group blob-exercise-group
CONNECTIONSTRING=$(az storage account show-connection-string --name <your-unique-storage-account-name> --output tsv)
az webapp config appsettings set --name <your-unique-app-name> --resource-group blob-exercise-group --settings AzureStorageConfig:ConnectionString=$CONNECTIONSTRING AzureStorageConfig:FileContainerName=files
```

<span data-ttu-id="e3a29-136">Jetzt stellen Sie die App bereit.</span><span class="sxs-lookup"><span data-stu-id="e3a29-136">Now we'll deploy our app.</span></span> <span data-ttu-id="e3a29-137">Mit den folgenden Befehlen wird die Site im Ordner `pub` veröffentlicht, in `site.zip` komprimiert und die ZIP-Datei in App Service bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="e3a29-137">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="e3a29-138">Stellen Sie sicher, dass Ihre Shell sich im `FileUploader`-Verzeichnis für die folgenden Befehle befindet.</span><span class="sxs-lookup"><span data-stu-id="e3a29-138">Make sure your shell is in the `FileUploader` directory for the following commands.</span></span>

```azurecli
dotnet publish -o pub
cd pub
zip -r ../site.zip *
az webapp deployment source config-zip --src ../site.zip --name <your-unique-app-name> --resource-group blob-exercise-group
```

<span data-ttu-id="e3a29-139">Öffnen Sie `https://<your-unique-app-name>.azurewebsites.net` in einem Browser, um die ausgeführte App anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-139">Open `https://<your-unique-app-name>.azurewebsites.net` in a browser to see the running app.</span></span> <span data-ttu-id="e3a29-140">Es sollte etwa wie im folgenden Bild aussehen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-140">It should look like the image below.</span></span>

![Screenshot der FileUploader-Web-App](../media/7-fileuploader-empty.PNG)

<span data-ttu-id="e3a29-142">Versuchen Sie, einige Dateien hochzuladen und herunterzuladen, um die App zu testen.</span><span class="sxs-lookup"><span data-stu-id="e3a29-142">Try uploading and downloading some files to test the app.</span></span> <span data-ttu-id="e3a29-143">Nachdem Sie einige Dateien hochgeladen haben, führen Sie Folgendes in der Shell aus, um die Blobs anzuzeigen, die in den Container hochgeladen wurden:</span><span class="sxs-lookup"><span data-stu-id="e3a29-143">After you've uploaded a few files, run the following in the shell to see the blobs that have been uploaded to the container:</span></span>

```console
az storage blob list --account-name <your-unique-storage-account-name> --container-name files --query [].{Name:name} --output table
```