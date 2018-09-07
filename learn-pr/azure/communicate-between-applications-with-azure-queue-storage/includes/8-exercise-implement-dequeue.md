<span data-ttu-id="86ebc-101">Nun wollen wir die Anwendung komplettieren, indem wir Code schreiben, um die nächste Nachricht in der Warteschlange zu lesen, sie zu verarbeiten und dann aus der Warteschlange zu löschen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-101">Now we want to complete the application by writing code to read the next message in the queue, processes it, and then delete it from the queue.</span></span> 

<span data-ttu-id="86ebc-102">Wir binden diesen Code in die gleiche Anwendung ein und führen ihn aus, wenn Sie keine Parameter übergeben. Aber in unserem Nachrichtenservice-Szenario fügen wir diesen Code unseren Servern auf mittlerer Ebene zu, um die Meldungen weiterzuverarbeiten.</span><span class="sxs-lookup"><span data-stu-id="86ebc-102">We're going to place this code into the same application and execute it when you don't pass any parameters, however in our news service scenario, we would really place this code into our middle-tier servers to process the stories.</span></span>

## <a name="dequeue-a-message"></a><span data-ttu-id="86ebc-103">Entfernen einer Nachricht aus der Warteschlange</span><span class="sxs-lookup"><span data-stu-id="86ebc-103">Dequeue a message</span></span>

<span data-ttu-id="86ebc-104">Lassen Sie uns eine neue Methode hinzufügen, die die nächste Nachricht aus der Warteschlange abruft.</span><span class="sxs-lookup"><span data-stu-id="86ebc-104">Let's add a new method that retrieves the next message from the queue.</span></span>

1. <span data-ttu-id="86ebc-105">Wechseln Sie in der Cloud Shell zum Ordner `QueueApp` und geben Sie `code .` ein, um den Online-Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-105">Switch to the `QueueApp` folder in the Cloud Shell and type `code .` to open the online editor.</span></span>
 
1. <span data-ttu-id="86ebc-106">Öffnen Sie die Quelldatei `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="86ebc-106">Open the `Program.cs` source file.</span></span>

1. <span data-ttu-id="86ebc-107">Erstellen Sie eine statische Methode in der `Program`-Klasse mit dem Namen `ReceiveArticleAsync`, die keine Parameter verwendet und `Task<string>` zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="86ebc-107">Create a static method in the `Program` class named `ReceiveArticleAsync` that takes no parameters and returns a `Task<string>`.</span></span> <span data-ttu-id="86ebc-108">Wir nutzen diese Methode, um eine Nachrichtenmeldung der Warteschlange zu entnehmen und zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="86ebc-108">We'll use this method to pull a news article from the queue and return it.</span></span>
    - <span data-ttu-id="86ebc-109">Fahren Sie fort, indem Sie das Schlüsselwort `async` der Methode hinzufügen, da wir einige asynchrone, auf `Task` basierende Methoden verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="86ebc-109">Go ahead and add the `async` keyword to the method since we'll be using some asynchronous `Task`-based methods.</span></span>

    ```csharp
    static async Task<string> ReceiveArticleAsync()
    {
    }

1. All of the setup code to get a `CloudQueue` will be identical to what we did in the last exercise. Code duplication is a bad habit, even in samples so go ahead and, refactor the code that obtains the `CloudQueue` to a new method named `GetQueue` and change the `SendArticleAsync` to use your new method.
     - Make sure to leave the code that _creates_ the queue in the `SendArticleAsync` method; remember only the **publisher** should create the queue.

    ```csharp
    const string ConnectionString = ...;
    // ...

    static CloudQueue GetQueue()
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        return queueClient.GetQueueReference("newsqueue");
    }
    ```
    
1. <span data-ttu-id="86ebc-110">Rufen Sie in Ihrer `ReceiveArticleAsync`-Methode die neue `GetQueue`-Methode auf, um Ihren Warteschlangenverweis abzurufen und ihn einer Variablen zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-110">In your `ReceiveArticleAsync` method, call the new `GetQueue` method to retrieve your queue reference and assign it to a variable.</span></span>

1. <span data-ttu-id="86ebc-111">Rufen Sie als Nächstes die `ExistsAsync`-Methode für das `CloudQueue`-Objekt auf, die zurückgibt, ob die Warteschlange erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="86ebc-111">Next, call the `ExistsAsync` method on the `CloudQueue` object; this will return whether the queue has been created.</span></span> <span data-ttu-id="86ebc-112">Wenn wir versuchen, eine Nachricht aus einer nicht vorhandenen Warteschlange abzurufen, löst die API eine Ausnahme aus.</span><span class="sxs-lookup"><span data-stu-id="86ebc-112">If we attempt to retrieve a message from a non-existent queue, the API will throw an exception.</span></span>
    - <span data-ttu-id="86ebc-113">Diese Methode ist asynchron, weshalb Sie `await` verwenden, um den Rückgabewert abzurufen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-113">This method is asynchronous so use `await` to get the return value.</span></span>
    - <span data-ttu-id="86ebc-114">Das Schlüsselwort `async` sollte bereits für die `ReceiveArticleAsync`-Methode vorhanden sein. Falls nicht, fügen Sie es jetzt hinzu.</span><span class="sxs-lookup"><span data-stu-id="86ebc-114">You should already have the `async` keyword on the `ReceiveArticleAsync` method, but if not add it now.</span></span>


1. <span data-ttu-id="86ebc-115">Fügen Sie einen `if`-Block hinzu, der den Rückgabewert von `ExistsAsync` verwendet.</span><span class="sxs-lookup"><span data-stu-id="86ebc-115">Add an `if` block that uses the return value from `ExistsAsync`.</span></span> <span data-ttu-id="86ebc-116">Wir fügen unseren Code hinzu, um einen Wert aus der Warteschlange in den Block einzulesen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-116">We'll add our code to read a value from the queue into the block.</span></span> <span data-ttu-id="86ebc-117">Fügen Sie eine abschließende Rückgabezeichenfolge zur Methode hinzu, die angibt, dass kein Wert gelesen wurde.</span><span class="sxs-lookup"><span data-stu-id="86ebc-117">Add a final return string to the method that indicates no value was read.</span></span> <span data-ttu-id="86ebc-118">Ihre Methode sollte in etwa so aussehen:</span><span class="sxs-lookup"><span data-stu-id="86ebc-118">Your method should be looking something like this:</span></span>

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
    }

    return "<queue empty or not created>";
}
```

1. <span data-ttu-id="86ebc-119">Rufen Sie `GetMessageAsync` für das `CloudQueue`-Objekt auf, um die erste `CloudQueueMessage` aus der Warteschlange abzurufen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-119">Call `GetMessageAsync` on the `CloudQueue` object to get the first `CloudQueueMessage` from the queue.</span></span> <span data-ttu-id="86ebc-120">Der zurückgegebene Wert ist `null`, wenn die Warteschlange leer ist.</span><span class="sxs-lookup"><span data-stu-id="86ebc-120">The return value will be `null` if the queue is empty.</span></span>

1. <span data-ttu-id="86ebc-121">Falls nicht NULL, verwenden Sie die `AsString`-Eigenschaft für das `CloudQueueMessage`-Objekt, um den Inhalt der Nachricht abzurufen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-121">If it's non-null, use the `AsString` property on the `CloudQueueMessage` object to get the contents of the message.</span></span>

1. <span data-ttu-id="86ebc-122">Rufen Sie `DeleteMessageAsync` für das `CloudQueue`-Objekt auf, um die Nachricht aus der Warteschlange zu löschen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-122">Call `DeleteMessageAsync` on the `CloudQueue` object to delete the message from the queue.</span></span>

<span data-ttu-id="86ebc-123">Die letzte Implementierung der Methode sollte so aussehen:</span><span class="sxs-lookup"><span data-stu-id="86ebc-123">The final method implementation should resemble:</span></span>

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
        CloudQueueMessage retrievedArticle = await queue.GetMessageAsync();
        if (retrievedArticle != null)
        {
            string newsMessage = retrievedArticle.AsString;
            await queue.DeleteMessageAsync(retrievedArticle);
            return newsMessage;
        }
    }

    return "<queue empty or not created>";
}
```

## <a name="call-the-receivearticleasync-method"></a><span data-ttu-id="86ebc-124">Aufrufen der ReceiveArticleAsync-Methode</span><span class="sxs-lookup"><span data-stu-id="86ebc-124">Call the ReceiveArticleAsync method</span></span>

<span data-ttu-id="86ebc-125">Abschließend fügen wir noch Unterstützung zum Aufrufen unserer neuen Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="86ebc-125">Finally, let's add support to invoke our new method.</span></span> <span data-ttu-id="86ebc-126">Dies erfolgt, wenn wir keine Parameter an das Programm übergeben.</span><span class="sxs-lookup"><span data-stu-id="86ebc-126">We'll do this when we don't pass any parameters into the program.</span></span>

1. <span data-ttu-id="86ebc-127">Navigieren Sie zur `Main`-Methode und insbesondere zum `if`-Block, den Sie zuvor hinzugefügt haben, um nach Parametern zu suchen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-127">Locate the `Main` method and specifically the `if` block you added earlier to look for parameters.</span></span>

1. <span data-ttu-id="86ebc-128">Fügen Sie eine `else`-Bedingung hinzu, und rufen die `ReceiveArticleAsync`-Methode auf.</span><span class="sxs-lookup"><span data-stu-id="86ebc-128">Add an `else` condition and call the `ReceiveArticleAsync` method.</span></span> 

1. <span data-ttu-id="86ebc-129">Da sie asynchron ist, würden wir normalerweise `await` verwenden. Wie jedoch bereits erläutert, funktioniert das nicht in allen Versionen von C#. Nutzen Sie also einfach die `Result`-Eigenschaft, um den Rückgabewert abzurufen und ihn im Konsolenfenster auszugeben.</span><span class="sxs-lookup"><span data-stu-id="86ebc-129">Since it's asynchronous, we would normally want to use `await`, however as explained earlier that doesn't work in all versions of C# - so just use the `Result` property to get the return value and print it to the console window.</span></span>

<span data-ttu-id="86ebc-130">Ihr Code sollte ungefähr wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="86ebc-130">Your code should look something like:</span></span>

```csharp
if (args.Length > 0)
{
    // ...
}
else
{
    string value = ReceiveArticleAsync().Result;
    Console.WriteLine($"Received {value}");
}
```

## <a name="execute-the-application"></a><span data-ttu-id="86ebc-131">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="86ebc-131">Execute the application</span></span>

<span data-ttu-id="86ebc-132">Der Code ist nun vollständig.</span><span class="sxs-lookup"><span data-stu-id="86ebc-132">The code is now complete.</span></span> <span data-ttu-id="86ebc-133">Er kann jetzt Nachrichten senden und abrufen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-133">It can now send and retrieve messages.</span></span> <span data-ttu-id="86ebc-134">Um ihn zu testen, verwenden Sie `dotnet run`, und übergeben Sie Parameter, um Nachrichten zu senden, und lassen Sie Parameter weg, um eine einzelne Nachricht zu lesen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-134">To test it, use `dotnet run` and pass parameters to send messages, and leave off parameters to read a single message.</span></span>

<span data-ttu-id="86ebc-135">Falls Sie testen möchten, wenn keine Warteschlange vorhanden ist, können Sie die Warteschlange (und alle Daten) mit der Azure CLI löschen.</span><span class="sxs-lookup"><span data-stu-id="86ebc-135">If you want to test when a queue doesn't exist, you can delete the queue (and all the data) with the Azure CLI.</span></span> <span data-ttu-id="86ebc-136">Ersetzen Sie unbedingt den Parameter `<connection-string>` (oder legen Sie die Umgebungsvariable fest).</span><span class="sxs-lookup"><span data-stu-id="86ebc-136">Make sure to replace the `<connection-string>` parameter (or set the environment variable).</span></span>

```azurecli
az storage queue delete --name newsqueue --connection-string <connection-string> 
```

<span data-ttu-id="86ebc-137">Beim nächsten Hinzufügen einer Nachricht muss die Warteschlange neu erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="86ebc-137">The next time you add a message, the queue should be re-created.</span></span>