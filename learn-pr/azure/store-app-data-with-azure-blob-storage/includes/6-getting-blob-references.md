<span data-ttu-id="95820-101">Arbeiten mit einem einzelnen Blob im Azure Storage SDK für .NET Core erfordert einen *Blobverweis* &mdash; eine Instanz eines `ICloudBlob`-Objekts.</span><span class="sxs-lookup"><span data-stu-id="95820-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="95820-102">Sie erhalten ein `ICloudBlob`, wenn Sie es mit den Namen des Blobs anfordern oder aus einer Liste von Blobs im Container auswählen.</span><span class="sxs-lookup"><span data-stu-id="95820-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="95820-103">Beide erfordern einen `CloudBlobContainer` – in der letzten Einheit haben wir erfahren, wie wir ihn bekommen.</span><span class="sxs-lookup"><span data-stu-id="95820-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="95820-104">Abrufen von Blobs anhand des Namens</span><span class="sxs-lookup"><span data-stu-id="95820-104">Getting blobs by name</span></span>

<span data-ttu-id="95820-105">Rufen Sie eine der `GetXXXReference`-Methoden auf einem `CloudBlobContainer` auf, um ein `ICloudBlob` anhand des Namens abzurufen.</span><span class="sxs-lookup"><span data-stu-id="95820-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="95820-106">Wenn Sie den Typ des Blobs kennen, das Sie abrufen, verwenden Sie vorzugsweise eine der spezifischeren Methoden (`GetBlockBlobReference`, `GetAppendBlobReference` oder `GetPageBlobReference`).</span><span class="sxs-lookup"><span data-stu-id="95820-106">If you know the type of the blob you are retrieving, prefer using one of the more specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`).</span></span>

<span data-ttu-id="95820-107">Keine dieser Methoden führt einen Netzwerkaufruf durch, noch bestätigen sie, ob das Blob tatsächlich vorhanden ist oder nicht.</span><span class="sxs-lookup"><span data-stu-id="95820-107">None of these methods make a network call, nor do they confirm whether or not the blob actually exists.</span></span> <span data-ttu-id="95820-108">Eine separate Methode, `GetBlobReferenceFromServerAsync`, ruft die Blobspeicher-API auf und löst eine Ausnahme aus, wenn das Blob noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="95820-108">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="95820-109">Auflisten von Blobs in einem Container</span><span class="sxs-lookup"><span data-stu-id="95820-109">Listing blobs in a container</span></span>

<span data-ttu-id="95820-110">Sie erhalten eine Liste der Blobs in einem Container mit `CloudBlobContainer` der `ListBlobsSegmentedAsync`-Methode.</span><span class="sxs-lookup"><span data-stu-id="95820-110">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="95820-111">*Segmented* bezieht sich auf die separaten Seiten von zurückgegebenen Ergebnissen &mdash; es ist nie garantiert, dass ein einzelner Aufruf von `ListBlobsSegmentedAsync` alle Ergebnisse in einer einzelnen Seite zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="95820-111">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="95820-112">Möglicherweise ist ein wiederholtes Aufrufen mithilfe des zurückgegebenen `ContinuationToken` erforderlich, um alle Seiten zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="95820-112">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="95820-113">Dadurch wird der Code für das Auflisten von Blobs ein wenig komplexer als der Code zum Hoch- oder Herunterladen, aber Sie können ein Standardmuster verwenden, um jedes Blob in einem Container zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="95820-113">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null; 

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

<span data-ttu-id="95820-114">Dies ruft `ListBlobsSegmentedAsync` solange wiederholt auf, bis `continuationToken` den Wert `null` hat, was das Ende der Ergebnisse signalisiert.</span><span class="sxs-lookup"><span data-stu-id="95820-114">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="95820-115">Verarbeiten von Listenergebnissen</span><span class="sxs-lookup"><span data-stu-id="95820-115">Processing list results</span></span>

<span data-ttu-id="95820-116">Das Objekt, das `ListBlobsSegmentedAsync` zurückgibt, enthält eine `Results`-Eigenschaft vom Typ `IEnumerable<IListBlobItem>`.</span><span class="sxs-lookup"><span data-stu-id="95820-116">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="95820-117">`IListBlobItem`s enthalten eine Reihe von Eigenschaften von Container und URL des Blobs, aber keine Methoden zum Hoch- oder Herunterladen.</span><span class="sxs-lookup"><span data-stu-id="95820-117">`IListBlobItem`s contain a handful of properties about the blob's container and URL, but no upload or download methods.</span></span> <span data-ttu-id="95820-118">Der Grund hierfür ist, dass einige der Ergebnisobjekte möglicherweise `CloudBlobDirectory`-Objekte sind, die eher virtuelle Verzeichnisse anstatt einzelner Blobs darstellen.</span><span class="sxs-lookup"><span data-stu-id="95820-118">This is because some of the result objects may be `CloudBlobDirectory` objects that represent virtual directories rather than individual blobs.</span></span>

<span data-ttu-id="95820-119">Wenn Sie nur an einzelnen Blobs interessiert sind, können Sie die Ergebnisse mithilfe der `OfType<>`-Methode filtern.</span><span class="sxs-lookup"><span data-stu-id="95820-119">If you are only interested in individual blobs, you can use the `OfType<>` method to filter the results.</span></span> <span data-ttu-id="95820-120">Hier sind einige Beispiele:</span><span class="sxs-lookup"><span data-stu-id="95820-120">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

<span data-ttu-id="95820-121">Die Verwendung von `OfType<>` erfordert einen Verweis auf den `System.Linq`-Namespace (`using System.Linq;`).</span><span class="sxs-lookup"><span data-stu-id="95820-121">Using `OfType<>` will require a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="95820-122">Übung</span><span class="sxs-lookup"><span data-stu-id="95820-122">Exercise</span></span>

<span data-ttu-id="95820-123">Eines der Features in unserer App erfordert das Abrufen einer Liste von Blobs aus der API.</span><span class="sxs-lookup"><span data-stu-id="95820-123">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="95820-124">Wir verwenden das oben gezeigte Muster, um alle Blobs in unserem Container aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="95820-124">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="95820-125">Bei Verarbeitung der Liste erhalten wir die Namen der einzelnen Blobs.</span><span class="sxs-lookup"><span data-stu-id="95820-125">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="95820-126">Öffnen Sie `BlobStorage.cs` im Editor, und geben Sie in `GetNames` folgenden Code ein:</span><span class="sxs-lookup"><span data-stu-id="95820-126">Open `BlobStorage.cs` in the editor and fill in `GetNames` with the following code:</span></span>

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

<span data-ttu-id="95820-127">Die von dieser Methode zurückgegebenen Namen werden von `FilesController` verarbeitet, um sie in URLs umzuwandeln.</span><span class="sxs-lookup"><span data-stu-id="95820-127">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="95820-128">Wenn sie an den Client zurückgegeben werden, werden sie als Hyperlinks auf der Seite gerendert.</span><span class="sxs-lookup"><span data-stu-id="95820-128">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>