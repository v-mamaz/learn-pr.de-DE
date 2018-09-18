<span data-ttu-id="1880b-101">::: zone pivot="csharp" Lassen Sie uns Code hinzufügen, um die Verbindungszeichenfolge aus der Konfiguration abzurufen und sie für das Herstellen einer Verbindung mit dem Azure Storage-Konto zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="1880b-101">::: zone pivot="csharp" Let's add code to retrieve the connection string from configuration and use it to connect to the Azure storage account.</span></span>

## <a name="retrieve-the-connection-string"></a><span data-ttu-id="1880b-102">Abrufen der Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="1880b-102">Retrieve the connection string</span></span>

1. <span data-ttu-id="1880b-103">Wählen Sie dann **Program.cs** aus, um die Datei im Code-Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="1880b-103">Select **Program.cs** to open it in the code editor.</span></span>

1. <span data-ttu-id="1880b-104">Fügen Sie eine `using`-Anweisung am Anfang der Datei hinzu, um auf den Namespace `Microsoft.WindowsAzure.Storage` zu verweisen:</span><span class="sxs-lookup"><span data-stu-id="1880b-104">Add a `using` statement at the top of the file to reference the `Microsoft.WindowsAzure.Storage` namespace:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. <span data-ttu-id="1880b-105">Fügen Sie am Ende der `Main`-Methode die folgende Zeile hinzu, um die Verbindungszeichenfolge des Azure Storage-Kontos aus der Konfigurationsdatei abzurufen.</span><span class="sxs-lookup"><span data-stu-id="1880b-105">At the end of the `Main` method, add the following line to retrieve the Azure storage account connection string from the configuration file.</span></span> <span data-ttu-id="1880b-106">Der übergebene _Schlüssel_ muss mit dem Namen übereinstimmen, den Sie in Ihrer Datei **appsettings.json** verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="1880b-106">The passed _key_ must match the name used in your **appsettings.json** file.</span></span>

    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a><span data-ttu-id="1880b-107">Erstellen eines Blobclients</span><span class="sxs-lookup"><span data-stu-id="1880b-107">Create a blob client</span></span>

1. <span data-ttu-id="1880b-108">Verwenden Sie die statische `CloudStorageAccount.TryParse`-Methode zum Erstellen eines `CloudStorageAccount`-Objekts. Es verwendet die Verbindungszeichenfolge und einen `out`-Parameter, um das erstellte Objekt zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="1880b-108">Use the static `CloudStorageAccount.TryParse` method to create a `CloudStorageAccount` object - it takes the connection string and an `out` parameter to return the created object.</span></span> <span data-ttu-id="1880b-109">Es gibt einen `bool`-Wert zurück, der angibt, ob die Zeichenkette erfolgreich analysiert wurde.</span><span class="sxs-lookup"><span data-stu-id="1880b-109">It returns a `bool` value indicating whether it successfully parsed the string.</span></span>
    - <span data-ttu-id="1880b-110">Geben Sie bei einem Fehler eine Meldung an die Konsole aus, und kehren Sie von der Methode zurück.</span><span class="sxs-lookup"><span data-stu-id="1880b-110">If it fails, output a message to the console and return from the method.</span></span>

    ```csharp
    if (!CloudStorageAccount.TryParse(connectionString, 
            out CloudStorageAccount storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    ```

1. <span data-ttu-id="1880b-111">Verwenden Sie das zurückgegebene `CloudStorageAccount`-Objekt, um einen Blobclient zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1880b-111">Use the returned `CloudStorageAccount` object to create a blob client.</span></span>

    ```csharp
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="1880b-112">Als Nächstes verwenden Sie den Blobclient, um einen Verweis auf einen Container namens „photoblobs“ abzurufen.</span><span class="sxs-lookup"><span data-stu-id="1880b-112">Next, use the blob client to retrieve a reference to a container named "photoblobs".</span></span> <span data-ttu-id="1880b-113">Ähnlich wie Kontonamen müssen Blobcontainernamen kleingeschrieben sein und aus Buchstaben und Zahlen bestehen.</span><span class="sxs-lookup"><span data-stu-id="1880b-113">Much like the account names, the Blob container names must be lowercase and composed of letters and numbers.</span></span>

    ```csharp
    var blobContainer = blobClient.GetContainerReference("photoblobs");
    ```

1. <span data-ttu-id="1880b-114">Verwenden Sie die `CreateIfNotExistsAsync`-Methode, um den Container zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1880b-114">Use the `CreateIfNotExistsAsync` method to create the container.</span></span> <span data-ttu-id="1880b-115">Dies gibt einen `bool`-Wert zurück, der angibt, ob der Container erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="1880b-115">This returns a `bool` indicating whether the container was created.</span></span> <span data-ttu-id="1880b-116">Speichern Sie diesen in einer Variablen namens `created`.</span><span class="sxs-lookup"><span data-stu-id="1880b-116">Store this in a variable named `created`.</span></span>
    - <span data-ttu-id="1880b-117">Beachten Sie, dass es sich hierbei um eine **asynchrone** Methode handelt, die daher den tatsächlichen Netzwerkaufruf durchführt.</span><span class="sxs-lookup"><span data-stu-id="1880b-117">Notice that this is an **async** method - that means it will perform an actual network call.</span></span>
    - <span data-ttu-id="1880b-118">Sie müssen `await`-Schlüsselwörter zum Abrufen des `bool`-Ergebnisses verwenden.</span><span class="sxs-lookup"><span data-stu-id="1880b-118">You will need to use the `await` keywords to get the `bool` result.</span></span>

    ```csharp
    bool created = await blobContainer.CreateIfNotExistsAsync();
    ```

1. <span data-ttu-id="1880b-119">Da wir das Schlüsselwort `await` verwenden, ändern Sie nun die Signatur der `Main`-Methode in `async`, und geben Sie `Task` zurück.</span><span class="sxs-lookup"><span data-stu-id="1880b-119">Because we are using the `await` keyword, go ahead and change the signature for the `Main` method to be `async` and return a `Task`.</span></span>

    ```csharp
    static async Task Main(string[] args)
    {
        ...
    }
    ```

1. <span data-ttu-id="1880b-120">Prüfen Sie abschließend, ob wir einen Blobcontainer erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1880b-120">Finally, output whether we created the Blob container.</span></span>

    ```csharp
    Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
    ```

1. <span data-ttu-id="1880b-121">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="1880b-121">Save the file.</span></span>

<span data-ttu-id="1880b-122">Die endgültige Datei sollte wie folgt aussehen, wenn Sie Ihr Ergebnis überprüfen möchten.</span><span class="sxs-lookup"><span data-stu-id="1880b-122">The final file should look like this if you'd like to check your work.</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using System.Threading.Tasks;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;

namespace PhotoSharingApp
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();
            var connectionString = configuration["StorageAccountConnectionString"];

            if (!CloudStorageAccount.TryParse(connectionString, out CloudStorageAccount storageAccount))
            {
                Console.WriteLine("Unable to parse connection string");
                return;
            }

            var blobClient = storageAccount.CreateCloudBlobClient();
            var blobContainer = blobClient.GetContainerReference("photoblobs");
            bool created = await blobContainer.CreateIfNotExistsAsync();

            Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
        }
    }
}
```

## <a name="use-c-71-to-build-our-app"></a><span data-ttu-id="1880b-123">Verwenden von C# 7.1 zum Erstellen unserer App</span><span class="sxs-lookup"><span data-stu-id="1880b-123">Use C# 7.1 to build our app</span></span>

<span data-ttu-id="1880b-124">C# 7.1 unterstütz nun `async` und `await` für `Main`-Methoden.</span><span class="sxs-lookup"><span data-stu-id="1880b-124">Support for `async` and `await` on `Main` methods was added to C# 7.1.</span></span> <span data-ttu-id="1880b-125">Dies ist möglicherweise nicht die Standardversion des Compilers, den Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="1880b-125">This might not be the default version of the compiler you are using.</span></span> <span data-ttu-id="1880b-126">Lassen Sie uns sicherstellen, dass wir diese Version des Compilers verwenden, indem wir sie in unserer Konfigurationsdatei festlegen.</span><span class="sxs-lookup"><span data-stu-id="1880b-126">Let's make sure we use that version of the compiler by setting it in our configuration file.</span></span>

1. <span data-ttu-id="1880b-127">Öffnen Sie `PhotoSharingApp.csproj`, und fügen Sie `<LangVersion>7.1</LangVersion>` zu `PropertyGroup` hinzu, die das `TargetFramework` angibt.</span><span class="sxs-lookup"><span data-stu-id="1880b-127">Open the `PhotoSharingApp.csproj` and add `<LangVersion>7.1</LangVersion>` to the `PropertyGroup` that specifies the `TargetFramework`.</span></span> <span data-ttu-id="1880b-128">Nach Ausführung dieser Schritte sollte das Ergebnis so aussehen:</span><span class="sxs-lookup"><span data-stu-id="1880b-128">It should look like this when you're finished:</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <LangVersion>7.1</LangVersion> 
        <TargetFramework>netcoreapp2.0</TargetFramework>
      </PropertyGroup>
      ...
    </Project>
    ```

1. <span data-ttu-id="1880b-129">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="1880b-129">Save the file.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="1880b-130">Ausführen der App</span><span class="sxs-lookup"><span data-stu-id="1880b-130">Run the app</span></span>

1. <span data-ttu-id="1880b-131">Erstellen Sie die Anwendung, und führen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="1880b-131">Build and run the application.</span></span> <span data-ttu-id="1880b-132">**Hinweis:** Vergewissern Sie sich, dass Sie sich im richtigen Arbeitsverzeichnis befinden.</span><span class="sxs-lookup"><span data-stu-id="1880b-132">**Note:** make sure you're in the correct working directory.</span></span>

    ```bash
    dotnet run
    ```

<span data-ttu-id="1880b-133">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="1880b-133">::: zone-end</span></span>

<span data-ttu-id="1880b-134">::: zone-pivot="javascript" Fügen wir nun Code hinzu, um über unsere gespeicherte Verbindungszeichenfolge eine Verbindung mit dem Azure Storage-Konto herzustellen.</span><span class="sxs-lookup"><span data-stu-id="1880b-134">::: zone-pivot="javascript" Let's add code to connect to the Azure storage account using our stored connection string.</span></span> <span data-ttu-id="1880b-135">Die Azure-Clientbibliothek verwendet zum Abrufen der Verbindungszeichenfolge automatisch die Umgebungsvariable **AZURE_STORAGE_CONNECTION_STRING**.</span><span class="sxs-lookup"><span data-stu-id="1880b-135">The Azure client library will automatically use the **AZURE_STORAGE_CONNECTION_STRING** environment variable to get the connection string.</span></span>

## <a name="create-a-blob-client"></a><span data-ttu-id="1880b-136">Erstellen eines Blobclients</span><span class="sxs-lookup"><span data-stu-id="1880b-136">Create a blob client</span></span>

1. <span data-ttu-id="1880b-137">Öffnen Sie **index.js** im Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="1880b-137">Open **index.js** in the code editor.</span></span>

1. <span data-ttu-id="1880b-138">Beginnen Sie mit dem Hinzufügen des Moduls **azure-storage**.</span><span class="sxs-lookup"><span data-stu-id="1880b-138">Start by including the **azure-storage** module.</span></span> <span data-ttu-id="1880b-139">Speichern Sie das Modul in einer Variablen mit dem Namen **storage**.</span><span class="sxs-lookup"><span data-stu-id="1880b-139">Store the module in a variable named **storage**.</span></span>

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    
    const storage = require('azure-storage');
    ```

1. <span data-ttu-id="1880b-140">Verwenden Sie im Anschluss das Objekt **storage**, um das Objekt `BlobService` zu erstellen und es in einem globalen Element namens **blobService** zu speichern.</span><span class="sxs-lookup"><span data-stu-id="1880b-140">Next, right after that, use the **storage** object to create the `BlobService` object and store it in a global named **blobService**.</span></span> <span data-ttu-id="1880b-141">Denken Sie daran, dass es sich hierbei um vereinfachte Objekte handelt, die den Zugriff auf das Speicherkonto darstellen.</span><span class="sxs-lookup"><span data-stu-id="1880b-141">Remember, these are light-weight objects representing access to the storage account.</span></span>

    ```javascript
    const blobService = storage.createBlobService();
    ```

1. <span data-ttu-id="1880b-142">Fügen Sie eine Konstante hinzu, die den Container darstellt, den wir erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="1880b-142">Add a constant to represent the container we want to create.</span></span> <span data-ttu-id="1880b-143">Den Container nennen wir „photoblobs“.</span><span class="sxs-lookup"><span data-stu-id="1880b-143">We'll name the container "photoblobs".</span></span>

    ```javascript
    const containerName = 'photoblobs';
    ```

## <a name="create-a-container"></a><span data-ttu-id="1880b-144">Erstellen eines Containers</span><span class="sxs-lookup"><span data-stu-id="1880b-144">Create a container</span></span>

<span data-ttu-id="1880b-145">Wir können das `BlobService`-Objekt zum Arbeiten mit Blob-APIs in Azure Storage verwenden.</span><span class="sxs-lookup"><span data-stu-id="1880b-145">We can use the `BlobService` object to work with blob APIs in Azure storage.</span></span> <span data-ttu-id="1880b-146">Wie bereits erwähnt, sind alle APIs, die Netzwerkaufrufe ausführen, asynchron, um die App reaktionsschnell zu halten.</span><span class="sxs-lookup"><span data-stu-id="1880b-146">As mentioned before, all the APIs that make network calls are asynchronous to keep the app responsive.</span></span> <span data-ttu-id="1880b-147">Die `createContainerIfNotExists`-Methode ist eine dieser Methoden.</span><span class="sxs-lookup"><span data-stu-id="1880b-147">The `createContainerIfNotExists` method is one such method.</span></span> <span data-ttu-id="1880b-148">Wir verwenden _Zusagen_, um den Rückruf zu verarbeiten, der die Antwort enthält.</span><span class="sxs-lookup"><span data-stu-id="1880b-148">We'll use _promises_ to handle the callback which contains the response.</span></span>

1. <span data-ttu-id="1880b-149">Verwenden Sie `util.promisify`, um die Rückrufversion von `createContainerIfNotExists` zu nutzen und sie in eine Methode zur Rückgabe von Zusagen umzuwandeln.</span><span class="sxs-lookup"><span data-stu-id="1880b-149">Use `util.promisify` to take the callback version of `createContainerIfNotExists` and turn it into a promise-returning method.</span></span>
    - <span data-ttu-id="1880b-150">Da die Rückrufmethode für ein Objekt gilt, stellen Sie sicher, dass Sie am Ende einen `bind`-Aufruf hinzufügen, um sie mit diesem Kontext zu verbinden.</span><span class="sxs-lookup"><span data-stu-id="1880b-150">Since the callback method is on an object, make sure to add a `bind` call at the end to connect it to that context.</span></span>
    - <span data-ttu-id="1880b-151">Weisen Sie den Rückgabewert einer Konstanten am Anfang der Datei namens `createContainerAsync` zu, wie unten gezeigt.</span><span class="sxs-lookup"><span data-stu-id="1880b-151">Assign the return value to a constant at the top of the file named `createContainerAsync` as shown below.</span></span>

```javascript
const storage = require('azure-storage');
const blobService = storage.createBlobService();

const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';
```

1. <span data-ttu-id="1880b-152">Entfernen Sie die Ausgabe „Hello, World!“</span><span class="sxs-lookup"><span data-stu-id="1880b-152">Remove the "Hello, World!"</span></span> <span data-ttu-id="1880b-153">aus `main()`.</span><span class="sxs-lookup"><span data-stu-id="1880b-153">output from `main()`.</span></span>

1. <span data-ttu-id="1880b-154">Rufen Sie Ihre neue `createContainerAsync`-Zusage auf.</span><span class="sxs-lookup"><span data-stu-id="1880b-154">Call your new `createContainerAsync` promise.</span></span>
    - <span data-ttu-id="1880b-155">Übergeben Sie an sie die Konstante **containerName**.</span><span class="sxs-lookup"><span data-stu-id="1880b-155">Pass it the **containerName** constant.</span></span>
    - <span data-ttu-id="1880b-156">Wenden Sie das Schlüsselwort `await` auf den Aufruf an.</span><span class="sxs-lookup"><span data-stu-id="1880b-156">Apply the `await` keyword to the call.</span></span>
    - <span data-ttu-id="1880b-157">Umschließen Sie den Aufruf in einem Konstrukt des Typs `try` / `catch`, und geben Sie Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="1880b-157">Wrap the call in a `try` / `catch` construct and output any error.</span></span>

    ```javascript
    try {
        await createContainerAsync(containerName);
    }
    catch (err) {
        console.log(err.message);
    }
    ```
    
1. <span data-ttu-id="1880b-158">Die Zusage `createContainerAsync` gibt den ersten Wert aus dem zugrunde liegenden `createContainerIfNotExists` zurück, der das Containerergebnis ist.</span><span class="sxs-lookup"><span data-stu-id="1880b-158">The `createContainerAsync` promise returns the first value from the underlying `createContainerIfNotExists` which is the container result.</span></span> <span data-ttu-id="1880b-159">Dies umfasst Informationen dazu, ob der Container erstellt wurde oder nicht.</span><span class="sxs-lookup"><span data-stu-id="1880b-159">This includes information on whether the container was created or not.</span></span> <span data-ttu-id="1880b-160">Erfassen Sie das Ergebnis in einer Variablen, und geben Sie aus, ob der Container basierend auf der `result.created`-Eigenschaft erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="1880b-160">Capture the result in a variable and output whether the container was created based on the `result.created` property.</span></span>

    ```javascript
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
    ```

1. <span data-ttu-id="1880b-161">Ergänzen Sie schließlich die `main`-Funktion mit dem Schlüsselwort `async`.</span><span class="sxs-lookup"><span data-stu-id="1880b-161">Finally, decorate the `main` function with the `async` keyword.</span></span>
        
1. <span data-ttu-id="1880b-162">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="1880b-162">Save the file.</span></span>

<span data-ttu-id="1880b-163">Die endgültige Datei sollte wie folgt aussehen, wenn Sie Ihr Ergebnis überprüfen möchten.</span><span class="sxs-lookup"><span data-stu-id="1880b-163">The final file should look like this if you'd like to check your work.</span></span>

```javascript
#!/usr/bin/env node

require('dotenv').load();

const util = require('util');

const storage = require('azure-storage');
const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';

async function run() {
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
}

run();
```

## <a name="run-the-app"></a><span data-ttu-id="1880b-164">Ausführen der App</span><span class="sxs-lookup"><span data-stu-id="1880b-164">Run the app</span></span>

1. <span data-ttu-id="1880b-165">Erstellen Sie die Anwendung, und führen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="1880b-165">Build and run the application.</span></span> <span data-ttu-id="1880b-166">**Hinweis:** Vergewissern Sie sich, dass Sie sich im richtigen Arbeitsverzeichnis befinden.</span><span class="sxs-lookup"><span data-stu-id="1880b-166">**Note:** make sure you're in the correct working directory.</span></span>

    ```bash
    node index.js
    ```

<span data-ttu-id="1880b-167">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="1880b-167">::: zone-end</span></span>

<span data-ttu-id="1880b-168">Es sollte gemeldet werden, dass der Blobcontainer erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="1880b-168">It should report that the blob container was created.</span></span> <span data-ttu-id="1880b-169">Bei der zweiten Ausführung sollte gemeldet werden, dass er bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="1880b-169">If you run it a second time, it should tell you it already exists.</span></span>

<span data-ttu-id="1880b-170">So überprüfen Sie den Container</span><span class="sxs-lookup"><span data-stu-id="1880b-170">To verify the container:</span></span>

1. <span data-ttu-id="1880b-171">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="1880b-171">Sign in to the [Azure Portal](https://portal.azure.com/?azure-portal=true).</span></span>

1. <span data-ttu-id="1880b-172">Navigieren Sie zu Ihrem Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="1880b-172">Navigate to your storage account.</span></span> <span data-ttu-id="1880b-173">Sie können den Abschnitt **Alle Ressourcen** verwenden, um das Speicherkonto zu finden, oder es anhand des Namens im _Suchfeld_ oben im Portalfenster suchen.</span><span class="sxs-lookup"><span data-stu-id="1880b-173">You can use the **All Resources** section to find the storage account, or search by name from the _search box_ at the top of the portal window.</span></span> 

1. <span data-ttu-id="1880b-174">Wählen Sie im Abschnitt **Blobdienste** den Eintrag **Blobs** des Speicherkontos aus.</span><span class="sxs-lookup"><span data-stu-id="1880b-174">Select the **Blobs** entry of the storage account in the **Blob services** section.</span></span>

1. <span data-ttu-id="1880b-175">Im Bereich „Blobs“ sollte Ihr Container **photoblobs** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="1880b-175">You should see your **photoblobs** container in the Blobs panel.</span></span> <span data-ttu-id="1880b-176">Sie können den Container über das Menü „...“ rechts neben dem Eintrag löschen, um zu versuchen, ihn mit Ihrer App neu zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1880b-176">You can delete the container through the "..." menu on the right hand side of the entry to try re-creating it with your app.</span></span>

> [!NOTE]
> <span data-ttu-id="1880b-177">Der Container verschwindet sehr schnell aus dem Portal, aber das eigentliche Löschen dauert einige Minuten.</span><span class="sxs-lookup"><span data-stu-id="1880b-177">The container will disappear from the portal very quickly, but it takes a few minutes to actually delete.</span></span> <span data-ttu-id="1880b-178">Wenn Sie versuchen, ihn während des Löschvorgangs wiederherzustellen, erhalten Sie von Azure eine Fehlermeldung.</span><span class="sxs-lookup"><span data-stu-id="1880b-178">You will get an error response from Azure while it is being deleted if you attempt to recreate it.</span></span>

## <a name="delete-the-app"></a><span data-ttu-id="1880b-179">Löschen der App</span><span class="sxs-lookup"><span data-stu-id="1880b-179">Delete the app</span></span>
<span data-ttu-id="1880b-180">Wenn Sie sich entscheiden, den Anwendungsquellcode nicht in Ihrer Cloud Shell-Umgebung zu behalten, können Sie mit dem folgenden Befehl den Ordner und alle Inhalte entfernen.</span><span class="sxs-lookup"><span data-stu-id="1880b-180">If you decide you don't want to keep the application source code in your Cloud Shell environment, you can use the following command to remove the folder and all the contents.</span></span>

```bash
rm -r PhotoSharingApp/
```
