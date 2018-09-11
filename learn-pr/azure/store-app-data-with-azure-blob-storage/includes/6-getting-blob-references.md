<span data-ttu-id="8cda2-101">Arbeiten mit einem einzelnen Blob im Azure Storage SDK für .NET Core erfordert einen *Blobverweis* &mdash; eine Instanz eines `ICloudBlob`-Objekts.</span><span class="sxs-lookup"><span data-stu-id="8cda2-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="8cda2-102">Sie erhalten ein `ICloudBlob`, wenn Sie es mit den Namen des Blobs anfordern oder aus einer Liste von Blobs im Container auswählen.</span><span class="sxs-lookup"><span data-stu-id="8cda2-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="8cda2-103">Beide erfordern einen `CloudBlobContainer` – in der letzten Einheit haben wir erfahren, wie wir ihn bekommen.</span><span class="sxs-lookup"><span data-stu-id="8cda2-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="8cda2-104">Abrufen von Blobs anhand des Namens</span><span class="sxs-lookup"><span data-stu-id="8cda2-104">Getting blobs by name</span></span>

<span data-ttu-id="8cda2-105">Rufen Sie eine der `GetXXXReference`-Methoden auf einem `CloudBlobContainer` auf, um ein `ICloudBlob` anhand des Namens abzurufen.</span><span class="sxs-lookup"><span data-stu-id="8cda2-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="8cda2-106">Wenn Sie den Typ des Blobs kennen, den Sie abrufen, verwenden Sie eine der spezifischen Methoden (`GetBlockBlobReference`, `GetAppendBlobReference` oder `GetPageBlobReference`) zum Abrufen eines Objekts, das für diesen Blobtyp zugeschnittene Methoden und Eigenschaften enthält.</span><span class="sxs-lookup"><span data-stu-id="8cda2-106">If you know the type of the blob you are retrieving, use one of the specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`) to get an object that includes methods and properties tailored for that blob type.</span></span>

<span data-ttu-id="8cda2-107">Keine dieser Methoden führt Netzwerkaufrufe durch oder bestätigt, ob das Zielblob tatsächlich vorhanden ist oder nicht.</span><span class="sxs-lookup"><span data-stu-id="8cda2-107">None of these methods make network calls, nor do they confirm whether or not the targeted blob actually exists.</span></span> <span data-ttu-id="8cda2-108">Sie erstellen nur ein lokales Blobverweisobjekt, das anschließend zum Aufrufen von Methoden verwendet werden kann, die *tatsächlich* über das Netzwerk ausgeführt werden und mit Blobs im Speicher interagieren.</span><span class="sxs-lookup"><span data-stu-id="8cda2-108">They only create a blob reference object locally, which can then be used to call methods that *do* operate over the network and interact with blobs in storage.</span></span> <span data-ttu-id="8cda2-109">Die separate Methode `GetBlobReferenceFromServerAsync` ruft die Blobspeicher-API auf und löst eine Ausnahme aus, wenn das Blob noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="8cda2-109">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="8cda2-110">Auflisten von Blobs in einem Container</span><span class="sxs-lookup"><span data-stu-id="8cda2-110">Listing blobs in a container</span></span>

<span data-ttu-id="8cda2-111">Sie erhalten eine Liste der Blobs in einem Container mit `CloudBlobContainer` der `ListBlobsSegmentedAsync`-Methode.</span><span class="sxs-lookup"><span data-stu-id="8cda2-111">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="8cda2-112">*Segmented* bezieht sich auf die separaten Seiten von zurückgegebenen Ergebnissen &mdash; es ist nie garantiert, dass ein einzelner Aufruf von `ListBlobsSegmentedAsync` alle Ergebnisse in einer einzelnen Seite zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="8cda2-112">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="8cda2-113">Möglicherweise ist ein wiederholtes Aufrufen mithilfe des zurückgegebenen `ContinuationToken` erforderlich, um alle Seiten zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="8cda2-113">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="8cda2-114">Dadurch wird der Code für das Auflisten von Blobs ein wenig komplexer als der Code zum Hoch- oder Herunterladen, aber Sie können ein Standardmuster verwenden, um jedes Blob in einem Container zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="8cda2-114">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

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

<span data-ttu-id="8cda2-115">Dies wiederholt den Aufruf von `ListBlobsSegmentedAsync` so lange, bis `continuationToken` den Wert `null` hat, wodurch das Ende der Ergebnisse signalisiert wird.</span><span class="sxs-lookup"><span data-stu-id="8cda2-115">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cda2-116">Gehen Sie nicht davon aus, dass `ListBlobsSegmentedAsync`-Ergebnisse auf einer einzelnen Seite zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="8cda2-116">Never assume that `ListBlobsSegmentedAsync` results will arrive in a single page.</span></span> <span data-ttu-id="8cda2-117">Überprüfen Sie stattdessen immer, ob ein Fortsetzungstoken vorhanden ist, und verwenden Sie es gegebenenfalls.</span><span class="sxs-lookup"><span data-stu-id="8cda2-117">Always check for a continuation token and use it if it's present.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="8cda2-118">Verarbeiten von Listenergebnissen</span><span class="sxs-lookup"><span data-stu-id="8cda2-118">Processing list results</span></span>

<span data-ttu-id="8cda2-119">Das von `ListBlobsSegmentedAsync` zurückgegebene Objekt enthält eine `Results`-Eigenschaft vom Typ `IEnumerable<IListBlobItem>`.</span><span class="sxs-lookup"><span data-stu-id="8cda2-119">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="8cda2-120">Die `IListBlobItem`-Schnittstelle enthält nur wenige Eigenschaften zum Container und der URL des Blobs und ist daher für sich genommen nicht sehr nützlich.</span><span class="sxs-lookup"><span data-stu-id="8cda2-120">The `IListBlobItem` interface includes only a handful of properties about the blob's container and URL, and isn't very useful by itself.</span></span>

<span data-ttu-id="8cda2-121">Für nützliche Blobs aus `Results` können Sie die `OfType<>`-Methode zum Filtern und Umwandeln der Ergebnisse in spezifischere Typen von Blobs verwenden.</span><span class="sxs-lookup"><span data-stu-id="8cda2-121">To get useful blob objects out of `Results`, you can use the `OfType<>` method to filter and cast the results to more specific blob object types.</span></span> <span data-ttu-id="8cda2-122">Hier sind einige Beispiele:</span><span class="sxs-lookup"><span data-stu-id="8cda2-122">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

> [!TIP]
> <span data-ttu-id="8cda2-123">Die Verwendung von `OfType<>` erfordert einen Verweis auf den `System.Linq`-Namespace (`using System.Linq;`).</span><span class="sxs-lookup"><span data-stu-id="8cda2-123">Using `OfType<>` requires a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="8cda2-124">Übung</span><span class="sxs-lookup"><span data-stu-id="8cda2-124">Exercise</span></span>

<span data-ttu-id="8cda2-125">Eines der Features in unserer App erfordert das Abrufen einer Liste von Blobs aus der API.</span><span class="sxs-lookup"><span data-stu-id="8cda2-125">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="8cda2-126">Wir verwenden das oben gezeigte Muster, um alle Blobs in unserem Container aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="8cda2-126">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="8cda2-127">Bei der Verarbeitung der Liste erhalten Sie die Namen der einzelnen Blobs.</span><span class="sxs-lookup"><span data-stu-id="8cda2-127">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="8cda2-128">Öffnen Sie `BlobStorage.cs` im Editor, ersetzen Sie `GetNames` durch den folgenden Code, und speichern Sie die Änderungen.</span><span class="sxs-lookup"><span data-stu-id="8cda2-128">Open `BlobStorage.cs` in the editor, replace `GetNames` with the following code and save your changes.</span></span>

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

> [!TIP]
> <span data-ttu-id="8cda2-129">Beachten Sie, dass in der Signatur der Methode nun `async` angegeben sein muss.</span><span class="sxs-lookup"><span data-stu-id="8cda2-129">Note that the method signature now needs to specify `async`.</span></span>

<span data-ttu-id="8cda2-130">Die von dieser Methode zurückgegebenen Namen werden von `FilesController` verarbeitet, um sie in URLs umzuwandeln.</span><span class="sxs-lookup"><span data-stu-id="8cda2-130">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="8cda2-131">Wenn sie an den Client zurückgegeben werden, werden sie als Hyperlinks auf der Seite gerendert.</span><span class="sxs-lookup"><span data-stu-id="8cda2-131">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>