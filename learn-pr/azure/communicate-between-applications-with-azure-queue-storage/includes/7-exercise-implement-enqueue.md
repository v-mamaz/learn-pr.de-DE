<span data-ttu-id="6d76d-101">Nun, da alle Anforderungen erfüllt sind, können Sie Code schreiben, mit dem eine neue Speicherwarteschlange erstellt und eine Nachricht hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="6d76d-101">Now that all the requirements are in place, you can write code that creates a new storage queue and adds a message.</span></span> <span data-ttu-id="6d76d-102">Wir fügen diesen Code üblicherweise in unsere Front-End-Anwendungen ein, die die Daten generieren.</span><span class="sxs-lookup"><span data-stu-id="6d76d-102">We would typically place this code in our front-end apps that generate the data.</span></span>

## <a name="add-the-client-library-for-azure-storage"></a><span data-ttu-id="6d76d-103">Hinzufügen der Clientbibliothek für Azure Storage</span><span class="sxs-lookup"><span data-stu-id="6d76d-103">Add the client library for Azure Storage</span></span>

<span data-ttu-id="6d76d-104">Lassen Sie uns beginnen, indem wir unserer App die **Azure Storage-Clientbibliothek für .NET** hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-104">Let's start by adding the **Azure Storage Client Library for .NET** to our app.</span></span> <span data-ttu-id="6d76d-105">Diese kann mit NuGet (einem .NET-Paket-Manager) installiert werden.</span><span class="sxs-lookup"><span data-stu-id="6d76d-105">It can be installed with NuGet (a .NET package manager).</span></span> 

> [!NOTE]
> <span data-ttu-id="6d76d-106">Auch wenn eine neue Cloud Shell erstellt wurde, sind alle Ihre Dateien weiterhin vorhanden.</span><span class="sxs-lookup"><span data-stu-id="6d76d-106">Even though a new Cloud Shell was created, your files are all still present.</span></span> <span data-ttu-id="6d76d-107">Sie müssen jedoch zum Ordner `QueueApp` wechseln, da Sie sich nun im Stammverzeichnis Ihres Speicherbereichs befinden.</span><span class="sxs-lookup"><span data-stu-id="6d76d-107">However you will need to switch into the `QueueApp` folder since you will now be at the root of your storage area.</span></span> <span data-ttu-id="6d76d-108">Geben Sie einfach `cd QueueApp` ein, um Ordner zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="6d76d-108">Just type `cd QueueApp` to switch folders.</span></span> <span data-ttu-id="6d76d-109">Stellen Sie sicher, dass Sie dies tun, bevor Sie versuchen, das Paket hinzuzufügen, da sich die .NET-App in diesem Ordner befindet.</span><span class="sxs-lookup"><span data-stu-id="6d76d-109">Make sure to do this before attempting to add the package since the .NET app is in that folder.</span></span>

1. <span data-ttu-id="6d76d-110">Ändern Sie das aktuelle Verzeichnis in den Ordner `QueueApp`.</span><span class="sxs-lookup"><span data-stu-id="6d76d-110">Change the current directory to the `QueueApp` folder.</span></span>

2. <span data-ttu-id="6d76d-111">Installieren Sie mit dem Befehl `dotnet add package` das Paket `WindowsAzure.Storage` im Projekt.</span><span class="sxs-lookup"><span data-stu-id="6d76d-111">Install the `WindowsAzure.Storage` package to the project with the `dotnet add package` command.</span></span>

```azurecli
dotnet add package WindowsAzure.Storage
```

## <a name="add-a-method-to-send-a-news-alert"></a><span data-ttu-id="6d76d-112">Hinzufügen einer Methode zum Senden neuer Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="6d76d-112">Add a method to send a news alert</span></span>

<span data-ttu-id="6d76d-113">Als Nächstes erstellen wir eine neue Methode, um eine Nachrichtenmeldung in eine Warteschlange zu stellen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-113">Next, let's create a new method to send a news story into a queue.</span></span>

1. <span data-ttu-id="6d76d-114">Öffnen Sie den Code-Editor durch Eingeben von `code .`.</span><span class="sxs-lookup"><span data-stu-id="6d76d-114">Open the code editor by typing `code .`</span></span>

2. <span data-ttu-id="6d76d-115">Öffnen Sie die Datei `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="6d76d-115">Open the `Program.cs` file.</span></span>

3. <span data-ttu-id="6d76d-116">Fügen Sie am Anfang der Datei die folgenden Namespaces hinzu.</span><span class="sxs-lookup"><span data-stu-id="6d76d-116">At the top of the file, add the following namespaces.</span></span> <span data-ttu-id="6d76d-117">Wir verwenden Typen von beiden, um uns mit Azure Storage zu verbinden und dann mit Warteschlangen zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="6d76d-117">We'll be using types from both of these to connect to Azure Storage and then to work with queues.</span></span>
    - <span data-ttu-id="6d76d-118">Microsoft.WindowsAzure.Storage</span><span class="sxs-lookup"><span data-stu-id="6d76d-118">Microsoft.WindowsAzure.Storage</span></span>
    - <span data-ttu-id="6d76d-119">Microsoft.WindowsAzure.Storage.Queue</span><span class="sxs-lookup"><span data-stu-id="6d76d-119">Microsoft.WindowsAzure.Storage.Queue</span></span>


3. <span data-ttu-id="6d76d-120">Erstellen Sie eine statische Methode in der `Program`-Klasse mit dem Namen `SendArticleAsync`, die `string` verwendet und `Task` zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="6d76d-120">Create a static method in the `Program` class named `SendArticleAsync` that takes a `string` and returns a `Task`.</span></span> <span data-ttu-id="6d76d-121">Wir nutzen diese Methode, um eine Nachrichtenmeldung an unseren Dienst zu senden.</span><span class="sxs-lookup"><span data-stu-id="6d76d-121">We'll use this method to send a news article in to our service.</span></span> <span data-ttu-id="6d76d-122">Benennen Sie den Eingabeparameter wie unten dargestellt mit `newsMesasage`.</span><span class="sxs-lookup"><span data-stu-id="6d76d-122">Name the input parameter `newsMesasage` as shown below.</span></span>

    ```csharp
    ...
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Queue; 
    
    class Program
    {
        ...
    
        static async Task SendArticleAsync(string newsMessage)
        {
        }
    }
    ```
    
4. <span data-ttu-id="6d76d-123">Verwenden Sie in Ihrer neuen Methode die statische `CloudStorageAccount.Parse`-Methode zum Analysieren der Verbindungszeichenfolge (beachten Sie, dass wir Sie in einer Konstantenzeichenfolge platziert haben).</span><span class="sxs-lookup"><span data-stu-id="6d76d-123">In your new method, use the static `CloudStorageAccount.Parse` method to parse your connection string (recall we placed it into a constant string).</span></span> <span data-ttu-id="6d76d-124">Diese Methode gibt ein `CloudStorageAccount`-Objekt zurück, das in einer Variablen gespeichert werden muss.</span><span class="sxs-lookup"><span data-stu-id="6d76d-124">This method returns a `CloudStorageAccount` object that needs to be stored in a variable.</span></span>

5. <span data-ttu-id="6d76d-125">Rufen Sie die `CreateCloudQueueClient()`-Methode für das Speicherkontenobjekt auf, um ein Clientobjekt abzurufen und es in einer Variablen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="6d76d-125">Call the `CreateCloudQueueClient()` method on the storage account object to get a client object and store that in a variable.</span></span>

6. <span data-ttu-id="6d76d-126">Rufen Sie als Nächstes die `GetQueueReference`-Methode für das Clientobjekt auf, und übergeben Sie die Zeichenfolge `"newsqueue"` als Warteschlangennamen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-126">Next, call `GetQueueReference` method on the client object and pass the string `"newsqueue"` for the queue name.</span></span> <span data-ttu-id="6d76d-127">Dies gibt ein `CloudQueue`-Objekt zurück, das wir zum Arbeiten mit der Warteschlange verwenden können.</span><span class="sxs-lookup"><span data-stu-id="6d76d-127">This returns a `CloudQueue` object that we can use to work with the queue.</span></span> <span data-ttu-id="6d76d-128">Es ist in Ordnung, wenn die Warteschlange noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6d76d-128">It's OK if the queue does not exist yet.</span></span>

7. <span data-ttu-id="6d76d-129">Rufen Sie `CreateIfNotExistsAsync()` für das `CloudQueue`-Objekt auf, um sicherzustellen, dass die Warteschlange einsatzbereit ist.</span><span class="sxs-lookup"><span data-stu-id="6d76d-129">Call `CreateIfNotExistsAsync()` on the `CloudQueue` object to ensure the queue is ready for use.</span></span> <span data-ttu-id="6d76d-130">Dadurch wird die Warteschlange bei Bedarf erstellt.</span><span class="sxs-lookup"><span data-stu-id="6d76d-130">This will create the queue if necessary.</span></span>
    - <span data-ttu-id="6d76d-131">Da es sich um eine asynchrone Methode handelt, verwenden Sie das C#-Schlüsselwort `await`, um sicherzustellen, dass wir ordnungsgemäß mit ihr arbeiten.</span><span class="sxs-lookup"><span data-stu-id="6d76d-131">Since this is an asynchronous method, use the C# `await` keyword to ensure we work properly with it.</span></span> <span data-ttu-id="6d76d-132">Das bedeutet auch, dass Sie die _Methode_ mit dem Schlüsselwort `async` ergänzen müssen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-132">That also means you need to decorate the _method_ with the `async` keyword.</span></span> 
    - <span data-ttu-id="6d76d-133">`CreateIfNotExistsAsync` gibt den Wert `bool` zurück, der `true` ist, wenn die Warteschlange erstellt wurde, und `false`, wenn sie bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6d76d-133">`CreateIfNotExistsAsync` returns a `bool` value that will be `true` if the queue was created and `false` if it already exists.</span></span> <span data-ttu-id="6d76d-134">Geben Sie eine Nachricht an die Konsole aus, nachdem wir die Warteschlange erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6d76d-134">Output a message to the console if we created the queue.</span></span>
    - <span data-ttu-id="6d76d-135">Es folgt ein Beispiel, wenn Sie Hilfe benötigen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-135">Here's an example if you need some help.</span></span>

```csharp
static async Task SendArticleAsync(string newsMessage)
{
    ...
    bool createdQueue = await queue.CreateIfNotExistsAsync();
    if (createdQueue)
    {
        Console.WriteLine("The queue of news articles was created.");
    }
}
```

8. <span data-ttu-id="6d76d-136">Erstellen Sie eine Instanz von `CloudQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="6d76d-136">Create an instance of a `CloudQueueMessage`.</span></span> 
    - <span data-ttu-id="6d76d-137">Sie verwendet einen `string`-Parameter. Übergeben Sie den Methodenparameter (`newsMessage`).</span><span class="sxs-lookup"><span data-stu-id="6d76d-137">It takes a `string` parameter, pass in the method parameter (`newsMessage`).</span></span> <span data-ttu-id="6d76d-138">Dies wird der _Text_ der Nachricht.</span><span class="sxs-lookup"><span data-stu-id="6d76d-138">This will be the _body_ of the message.</span></span> <span data-ttu-id="6d76d-139">Es gibt auch eine statische Methode, die eine binäre Nachrichtennutzlast erzeugen kann.</span><span class="sxs-lookup"><span data-stu-id="6d76d-139">There is also a static method named  that can create a binary message payload.</span></span>
    

9. <span data-ttu-id="6d76d-140">Rufen Sie `AddMessageAsync` für das `CloudQueue`-Objekt auf, um die Nachricht zur Warteschlange hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-140">Call `AddMessageAsync` on the `CloudQueue` object to add the message to the queue.</span></span> <span data-ttu-id="6d76d-141">Dies ist auch eine asynchrone Methode, weshalb Sie das Schlüsselwort `await` verwenden müssen, um sicherzustellen, dass wir richtig mit ihr interagieren.</span><span class="sxs-lookup"><span data-stu-id="6d76d-141">This is also an asynchronous method and you will need to use the `await` keyword to ensure we properly interact with it.</span></span>

10. <span data-ttu-id="6d76d-142">Speichern Sie die Datei, und erstellen Sie sie, indem Sie `dotnet build` in das Befehlsfenster eingeben.</span><span class="sxs-lookup"><span data-stu-id="6d76d-142">Save the file and build it by typing `dotnet build` into the command window.</span></span> <span data-ttu-id="6d76d-143">Beheben Sie eventuelle Fehler. Sie können den folgenden Code verwenden, um Ihre Arbeit zu prüfen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-143">Fix any errors, you can use the following code to check your work.</span></span>

```csharp
static async Task SendArticleAsync(string newsMessage)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    CloudQueue queue = queueClient.GetQueueReference(QueueName);
    bool createdQueue = await queue.CreateIfNotExistsAsync();
    if (createdQueue)
    {
        Console.WriteLine("The queue of news articles was created.");
    }

    CloudQueueMessage articleMessage = new CloudQueueMessage(newsMessage);
    await queue.AddMessageAsync(articleMessage);
}
```

## <a name="add-code-to-send-a-message"></a><span data-ttu-id="6d76d-144">Hinzufügen von Code zum Senden einer Nachricht</span><span class="sxs-lookup"><span data-stu-id="6d76d-144">Add code to send a message</span></span>

<span data-ttu-id="6d76d-145">Lassen Sie uns die `Main`-Methode modifizieren, indem wir alle empfangenen Parameter an unsere neue Methode übergeben, damit wir unsere neue Sendemethode testen können.</span><span class="sxs-lookup"><span data-stu-id="6d76d-145">Let's modify the `Main` method to pass any parameters received into our new method so we can test our new send method.</span></span>

1. <span data-ttu-id="6d76d-146">Wechseln Sie zur `Main`-Methode.</span><span class="sxs-lookup"><span data-stu-id="6d76d-146">Locate the `Main` method.</span></span>

2. <span data-ttu-id="6d76d-147">Überprüfen Sie den übergebenen Parameter `args`, um zu prüfen, ob Daten an die Befehlszeile übergeben wurden.</span><span class="sxs-lookup"><span data-stu-id="6d76d-147">Check the passed `args` parameter to see if any data was passed to the command line.</span></span> <span data-ttu-id="6d76d-148">Falls ja, verwenden Sie `String.Join` zum Erstellen einer einzelnen Zeichenfolge aus allen Wörtern mit einem Leerzeichen als Trennzeichen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-148">If so, use `String.Join` to create a single string from all the words using a space as the separator.</span></span>

3. <span data-ttu-id="6d76d-149">Übergeben Sie diese an die neue `SendArticleAsync`-Methode.</span><span class="sxs-lookup"><span data-stu-id="6d76d-149">Pass that to the new `SendArticleAsync` method.</span></span> 

4. <span data-ttu-id="6d76d-150">Sobald die Rückgabe erfolgt ist, verwenden Sie `Console.WriteLine`, um die von uns gesendete Nachricht auszugeben.</span><span class="sxs-lookup"><span data-stu-id="6d76d-150">Once it returns, use `Console.WriteLine` to output the message we sent.</span></span>

5. <span data-ttu-id="6d76d-151">Speichern Sie die Datei, und erstellen Sie das Programm (`dotnet build`). Sie können den nachstehenden Code zum Prüfen Ihrer Arbeit nutzen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-151">Save the file and build the program (`dotnet build`), you can use the code below to check your work.</span></span>

> [!NOTE]
> <span data-ttu-id="6d76d-152">Da unsere Methode technisch asynchron ist, würden wir normalerweise das Schlüsselwort `await` verwenden. Doch dieses Feature ist für Ihre `Main`-Methode nur verfügbar, wenn Sie C# 7.2 verwenden (da es ein neues Feature ist).</span><span class="sxs-lookup"><span data-stu-id="6d76d-152">Since our method is technically asynchronous, we normally would want to use the `await` keyword, however that feature isn't available on your `Main` method unless you are using C# 7.2 (it's a new feature).</span></span> <span data-ttu-id="6d76d-153">Um sicherzustellen, dass wir dies bei älteren Versionen der Sprache verwenden können, rufen Sie einfach `Wait()` für die Methode auf, um das Warten auf die Rückgabe der Methode zu blockieren.</span><span class="sxs-lookup"><span data-stu-id="6d76d-153">To ensure we can use this on older versions of the language, just call `Wait()` on the method to actually block waiting for the method to return.</span></span>

```csharp
static void Main(string[] args)
{
    if (args.Length > 0)
    {
        string value = String.Join(" ", args);
        SendArticleAsync(value).Wait();
        Console.WriteLine($"Sent: {value}");
    }
}
```

## <a name="execute-the-application"></a><span data-ttu-id="6d76d-154">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="6d76d-154">Execute the application</span></span>

<span data-ttu-id="6d76d-155">Die Anwendung kann nun Nachrichten senden.</span><span class="sxs-lookup"><span data-stu-id="6d76d-155">The application can now send messages.</span></span> <span data-ttu-id="6d76d-156">Um Sie zu testen, können Sie sie über die Befehlszeile mit dem Befehl `dotnet run` ausführen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-156">To test it, you can run it from the command line with the `dotnet run` command.</span></span> <span data-ttu-id="6d76d-157">Zusätzliche Zeichenfolgen werden als Parameter an die Anwendung übergeben.</span><span class="sxs-lookup"><span data-stu-id="6d76d-157">Any additional strings are passed as parameters to the application.</span></span> <span data-ttu-id="6d76d-158">Sie können beispielsweise Folgendes eingeben:</span><span class="sxs-lookup"><span data-stu-id="6d76d-158">As an example, you can type:</span></span>

```azurecli
dotnet run Send this message
```

> [!WARNING]
> <span data-ttu-id="6d76d-159">Vergewissern Sie sich, dass Sie alle Dateien im Online-Editor gespeichert haben, bevor Sie das Programm erstellen und ausführen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-159">Make sure you have saved all the files in the online editor before you build and run the program.</span></span>

<span data-ttu-id="6d76d-160">Dies sollte die Zeichenfolge `"Send this message"` der Warteschlange hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-160">This should add the string `"Send this message"` into the queue.</span></span>

## <a name="check-your-results"></a><span data-ttu-id="6d76d-161">Überprüfen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="6d76d-161">Check your results</span></span>

<span data-ttu-id="6d76d-162">Sie können Warteschlangen im Azure-Portal mit dem **Storage-Explorer** überprüfen. Wenn Sie dieses Produkt öffnen, können Sie die Daten in jedem Ihrer Speicherkonten untersuchen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-162">You can check queues in the Azure portal using the **Storage Explorer**, if you open that product it will let you explore the data in each storage account you own.</span></span>

<span data-ttu-id="6d76d-163">Alternativ können Sie auch die Azure CLI oder PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="6d76d-163">Alternatively, you can use the Azure CLI or PowerShell.</span></span> <span data-ttu-id="6d76d-164">Probieren Sie diesen Befehl in der Shell aus, indem Sie den Wert `<connection-string>` durch Ihre spezifische Verbindungszeichenfolge ersetzen:</span><span class="sxs-lookup"><span data-stu-id="6d76d-164">Try this command in the shell, replacing the `<connection-string>` value with your specific connection string:</span></span>

```azurecli
az storage message peek --queue-name newsqueue --connection-string <connection-string> 
```

<span data-ttu-id="6d76d-165">Dies sollte die Informationen für Ihre Nachricht ausgeben, die ungefähr so aussieht:</span><span class="sxs-lookup"><span data-stu-id="6d76d-165">This should dump the information for your message, which will look something like this:</span></span>

```json
[
  {
    "content": "U2VuZCB0aGlzIG1lc3NhZ2U=",
    "dequeueCount": 0,
    "expirationTime": "2018-09-05T02:43:40+00:00",
    "id": "b47cbe9f-a246-4a81-86ae-fa02ea8d98bc",
    "insertionTime": "2018-09-24T02:43:40+00:00",
    "popReceipt": null,
    "timeNextVisible": null
  }
]
```

<span data-ttu-id="6d76d-166">Es gibt noch einige andere Befehle, die Sie mit den Tools ausprobieren können. Sehen Sie sich sowohl `az storage queue --help` als auch `az storage message --help` an, um sie zu erkunden.</span><span class="sxs-lookup"><span data-stu-id="6d76d-166">There are several other commands available that you can try with the tools - check out both `az storage queue --help` and `az storage message --help` to explore them.</span></span>

> [!NOTE]
> <span data-ttu-id="6d76d-167">Geben Sie den Wert Ihrer Verbindungszeichenfolge in eine Umgebungsvariable namens `AZURE_STORAGE_CONNECTION_STRING` ein, damit Sie den Parameter `--connection-string` nicht jedes Mal eingeben müssen!</span><span class="sxs-lookup"><span data-stu-id="6d76d-167">Put your connection string value into an environment variable named `AZURE_STORAGE_CONNECTION_STRING` to save yourself from having to type the `--connection-string` parameter every time!</span></span>

<span data-ttu-id="6d76d-168">Nachdem wir nun eine Nachricht gesendet haben, ist der letzte Schritt, Unterstützung für das _Empfangen_ der Nachricht hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="6d76d-168">Now that we have sent a message, the last step is to add support to _receive_ the message.</span></span>