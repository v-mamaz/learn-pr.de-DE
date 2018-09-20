<span data-ttu-id="09914-101">Nun, da alle Anforderungen erfüllt sind, können Sie Code schreiben, mit dem eine neue Speicherwarteschlange erstellt und eine Nachricht hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="09914-101">Now that all the requirements are in place, you can write code that creates a new storage queue and adds a message.</span></span> <span data-ttu-id="09914-102">Wir fügen diesen Code üblicherweise in unsere Front-End-Anwendungen ein, die die Daten generieren.</span><span class="sxs-lookup"><span data-stu-id="09914-102">We would typically place this code in our front-end apps that generate the data.</span></span>

## <a name="add-the-client-library-for-azure-storage"></a><span data-ttu-id="09914-103">Hinzufügen der Clientbibliothek für Azure Storage</span><span class="sxs-lookup"><span data-stu-id="09914-103">Add the client library for Azure Storage</span></span>

<span data-ttu-id="09914-104">Lassen Sie uns beginnen, indem wir unserer App die **Azure Storage-Clientbibliothek für .NET** hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="09914-104">Let's start by adding the **Azure Storage Client Library for .NET** to our app.</span></span> <span data-ttu-id="09914-105">Diese kann mit NuGet (einem .NET-Paket-Manager) installiert werden.</span><span class="sxs-lookup"><span data-stu-id="09914-105">It can be installed with NuGet (a .NET package manager).</span></span> 

1. <span data-ttu-id="09914-106">Installieren Sie mit dem Befehl `dotnet add package` das Paket `WindowsAzure.Storage` im Projekt.</span><span class="sxs-lookup"><span data-stu-id="09914-106">Install the `WindowsAzure.Storage` package to the project with the `dotnet add package` command.</span></span> <span data-ttu-id="09914-107">Sie können dies im Terminalfenster _unterhalb_ von Cloud Shell durchführen. Falls Sie auf Ihrem lokalen Computer arbeiten, können Sie ein Terminal- bzw. Konsolenfenster verwenden, das sich in demselben Ordner wie das Projekt befindet.</span><span class="sxs-lookup"><span data-stu-id="09914-107">You can do this in the terminal window _below_ the Cloud Shell, or if you are working on your local computer, in a terminal/console window in the same folder as the project.</span></span>

```azurecli
dotnet add package WindowsAzure.Storage
```

## <a name="add-a-method-to-send-a-news-alert"></a><span data-ttu-id="09914-108">Hinzufügen einer Methode zum Senden neuer Benachrichtigungen</span><span class="sxs-lookup"><span data-stu-id="09914-108">Add a method to send a news alert</span></span>

<span data-ttu-id="09914-109">Als Nächstes erstellen wir eine neue Methode, um eine Nachrichtenmeldung in eine Warteschlange zu stellen.</span><span class="sxs-lookup"><span data-stu-id="09914-109">Next, let's create a new method to send a news story into a queue.</span></span>

1. <span data-ttu-id="09914-110">Öffnen Sie die Datei `Program.cs` in Ihrem Code-Editor.</span><span class="sxs-lookup"><span data-stu-id="09914-110">Open the `Program.cs` file in your code editor.</span></span>

1. <span data-ttu-id="09914-111">Fügen Sie am Anfang der Datei die folgenden Namespaces hinzu.</span><span class="sxs-lookup"><span data-stu-id="09914-111">At the top of the file, add the following namespaces.</span></span> <span data-ttu-id="09914-112">Wir verwenden Typen von beiden Namespaces, um uns mit Azure Storage zu verbinden und dann mit Warteschlangen zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="09914-112">We'll be using types from both of these to connect to Azure Storage and then to work with queues.</span></span>

    - `System.Threading.Tasks`
    - `Microsoft.WindowsAzure.Storage`
    - `Microsoft.WindowsAzure.Storage.Queue`

1. <span data-ttu-id="09914-113">Erstellen Sie eine statische Methode in der `Program`-Klasse mit dem Namen `SendArticleAsync`, die `string` verwendet und `Task` zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="09914-113">Create a static method in the `Program` class named `SendArticleAsync` that takes a `string` and returns a `Task`.</span></span> <span data-ttu-id="09914-114">Wir nutzen diese Methode, um eine Nachrichtenmeldung an unseren Dienst zu senden.</span><span class="sxs-lookup"><span data-stu-id="09914-114">We'll use this method to send a news article in to our service.</span></span> <span data-ttu-id="09914-115">Benennen Sie den Eingabeparameter wie unten dargestellt mit `newsMessage`.</span><span class="sxs-lookup"><span data-stu-id="09914-115">Name the input parameter `newsMessage` as shown below.</span></span>

    ```csharp
    ...
    using System.Threading.Tasks;
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
    
1. <span data-ttu-id="09914-116">Verwenden Sie in Ihrer neuen Methode die statische `CloudStorageAccount.Parse`-Methode zum Analysieren der Verbindungszeichenfolge (beachten Sie, dass wir Sie in einer Konstantenzeichenfolge platziert haben).</span><span class="sxs-lookup"><span data-stu-id="09914-116">In your new method, use the static `CloudStorageAccount.Parse` method to parse your connection string (recall we placed it into a constant string).</span></span> <span data-ttu-id="09914-117">Diese Methode gibt ein `CloudStorageAccount`-Objekt zurück, das in einer Variablen gespeichert werden muss.</span><span class="sxs-lookup"><span data-stu-id="09914-117">This method returns a `CloudStorageAccount` object that needs to be stored in a variable.</span></span>

1. <span data-ttu-id="09914-118">Rufen Sie die `CreateCloudQueueClient()`-Methode für das Speicherkontenobjekt auf, um ein Clientobjekt abzurufen und es in einer Variablen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="09914-118">Call the `CreateCloudQueueClient()` method on the storage account object to get a client object and store that in a variable.</span></span>

1. <span data-ttu-id="09914-119">Rufen Sie als Nächstes die `GetQueueReference`-Methode für das Clientobjekt auf, und übergeben Sie die Zeichenfolge „newsqueue“ als Warteschlangennamen.</span><span class="sxs-lookup"><span data-stu-id="09914-119">Next, call `GetQueueReference` method on the client object and pass the string "newsqueue" for the queue name.</span></span> <span data-ttu-id="09914-120">Dies gibt ein `CloudQueue`-Objekt zurück, das wir zum Arbeiten mit der Warteschlange verwenden können.</span><span class="sxs-lookup"><span data-stu-id="09914-120">This returns a `CloudQueue` object that we can use to work with the queue.</span></span> <span data-ttu-id="09914-121">Es ist in Ordnung, wenn die Warteschlange noch nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="09914-121">It's OK if the queue does not exist yet.</span></span>

1. <span data-ttu-id="09914-122">Rufen Sie `CreateIfNotExistsAsync()` für das `CloudQueue`-Objekt auf, um sicherzustellen, dass die Warteschlange einsatzbereit ist.</span><span class="sxs-lookup"><span data-stu-id="09914-122">Call `CreateIfNotExistsAsync()` on the `CloudQueue` object to ensure the queue is ready for use.</span></span> <span data-ttu-id="09914-123">Dadurch wird die Warteschlange bei Bedarf erstellt.</span><span class="sxs-lookup"><span data-stu-id="09914-123">This will create the queue if necessary.</span></span>
    - <span data-ttu-id="09914-124">Da es sich um eine asynchrone Methode handelt, verwenden Sie das C#-Schlüsselwort `await`, um sicherzustellen, dass wir ordnungsgemäß mit ihr arbeiten.</span><span class="sxs-lookup"><span data-stu-id="09914-124">Since this is an asynchronous method, use the C# `await` keyword to ensure we work properly with it.</span></span> <span data-ttu-id="09914-125">Das bedeutet auch, dass Sie die _Methode_ mit dem Schlüsselwort `async` ergänzen müssen.</span><span class="sxs-lookup"><span data-stu-id="09914-125">That also means you need to decorate the _method_ with the `async` keyword.</span></span> 
    - <span data-ttu-id="09914-126">`CreateIfNotExistsAsync` gibt den Wert `bool` zurück, der `true` ist, wenn die Warteschlange erstellt wurde, und `false`, wenn sie bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="09914-126">`CreateIfNotExistsAsync` returns a `bool` value that will be `true` if the queue was created and `false` if it already exists.</span></span> <span data-ttu-id="09914-127">Geben Sie eine Nachricht an die Konsole aus, nachdem wir die Warteschlange erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="09914-127">Output a message to the console if we created the queue.</span></span>
    - <span data-ttu-id="09914-128">Es folgt ein Beispiel, wenn Sie Hilfe benötigen.</span><span class="sxs-lookup"><span data-stu-id="09914-128">Here's an example if you need some help.</span></span>

    ```csharp
    static async Task SendArticleAsync(string newsMessage)
    {
        // Not Shown here - code from prior steps
        ...
        bool createdQueue = await queue.CreateIfNotExistsAsync();
        if (createdQueue)
        {
            Console.WriteLine("The queue of news articles was created.");
        }
    }
    ```

1. <span data-ttu-id="09914-129">Erstellen Sie eine Instanz von `CloudQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="09914-129">Create an instance of a `CloudQueueMessage`.</span></span> 
    - <span data-ttu-id="09914-130">Sie verwendet einen `string`-Parameter. Übergeben Sie den Methodenparameter (`newsMessage`).</span><span class="sxs-lookup"><span data-stu-id="09914-130">It takes a `string` parameter, pass in the method parameter (`newsMessage`).</span></span> <span data-ttu-id="09914-131">Dies wird der _Text_ der Nachricht.</span><span class="sxs-lookup"><span data-stu-id="09914-131">This will be the _body_ of the message.</span></span> <span data-ttu-id="09914-132">Es gibt auch eine statische Methode, die eine binäre Nachrichtennutzlast erzeugen kann.</span><span class="sxs-lookup"><span data-stu-id="09914-132">There is also a static method named  that can create a binary message payload.</span></span>

1. <span data-ttu-id="09914-133">Rufen Sie `AddMessageAsync` für das `CloudQueue`-Objekt auf, um die Nachricht zur Warteschlange hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="09914-133">Call `AddMessageAsync` on the `CloudQueue` object to add the message to the queue.</span></span> <span data-ttu-id="09914-134">Dies ist auch eine asynchrone Methode, weshalb Sie das Schlüsselwort `await` verwenden müssen, um sicherzustellen, dass wir richtig mit ihr interagieren.</span><span class="sxs-lookup"><span data-stu-id="09914-134">This is also an asynchronous method and you will need to use the `await` keyword to ensure we properly interact with it.</span></span>

1. <span data-ttu-id="09914-135">Speichern Sie die Datei, und erstellen Sie sie, indem Sie `dotnet build` in das Befehlsfenster eingeben.</span><span class="sxs-lookup"><span data-stu-id="09914-135">Save the file and build it by typing `dotnet build` into the command window.</span></span> <span data-ttu-id="09914-136">Beheben Sie eventuelle Fehler. Sie können den folgenden Code verwenden, um Ihre Arbeit zu prüfen.</span><span class="sxs-lookup"><span data-stu-id="09914-136">Fix any errors, you can use the following code to check your work.</span></span>

    ```csharp
    static async Task SendArticleAsync(string newsMessage)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    
        CloudQueue queue = queueClient.GetQueueReference("newsqueue");
        bool createdQueue = await queue.CreateIfNotExistsAsync();
        if (createdQueue)
        {
            Console.WriteLine("The queue of news articles was created.");
        }
    
        CloudQueueMessage articleMessage = new CloudQueueMessage(newsMessage);
        await queue.AddMessageAsync(articleMessage);
    }
    ```

## <a name="add-code-to-send-a-message"></a><span data-ttu-id="09914-137">Hinzufügen von Code zum Senden einer Nachricht</span><span class="sxs-lookup"><span data-stu-id="09914-137">Add code to send a message</span></span>

<span data-ttu-id="09914-138">Lassen Sie uns die `Main`-Methode modifizieren, indem wir alle empfangenen Parameter an unsere neue Methode übergeben, damit wir unsere neue Sendemethode testen können.</span><span class="sxs-lookup"><span data-stu-id="09914-138">Let's modify the `Main` method to pass any parameters received into our new method so we can test our new send method.</span></span>

1. <span data-ttu-id="09914-139">Wechseln Sie zur `Main`-Methode.</span><span class="sxs-lookup"><span data-stu-id="09914-139">Locate the `Main` method.</span></span>

1. <span data-ttu-id="09914-140">Überprüfen Sie den übergebenen Parameter `args`, um zu prüfen, ob Daten an die Befehlszeile übergeben wurden.</span><span class="sxs-lookup"><span data-stu-id="09914-140">Check the passed `args` parameter to see if any data was passed to the command line.</span></span> <span data-ttu-id="09914-141">Falls ja, verwenden Sie `String.Join` zum Erstellen einer einzelnen Zeichenfolge aus allen Wörtern mit einem Leerzeichen als Trennzeichen.</span><span class="sxs-lookup"><span data-stu-id="09914-141">If so, use `String.Join` to create a single string from all the words using a space as the separator.</span></span>

1. <span data-ttu-id="09914-142">Übergeben Sie diese an die neue `SendArticleAsync`-Methode.</span><span class="sxs-lookup"><span data-stu-id="09914-142">Pass that to the new `SendArticleAsync` method.</span></span> 

1. <span data-ttu-id="09914-143">Sobald die Rückgabe erfolgt ist, verwenden Sie `Console.WriteLine`, um die von uns gesendete Nachricht auszugeben.</span><span class="sxs-lookup"><span data-stu-id="09914-143">Once it returns, use `Console.WriteLine` to output the message we sent.</span></span>

1. <span data-ttu-id="09914-144">Speichern Sie die Datei, und erstellen Sie das Programm (`dotnet build`). Sie können den nachstehenden Code zum Prüfen Ihrer Arbeit nutzen.</span><span class="sxs-lookup"><span data-stu-id="09914-144">Save the file and build the program (`dotnet build`), you can use the code below to check your work.</span></span>

    > [!NOTE]
    > <span data-ttu-id="09914-145">Da unsere Methode technisch asynchron ist, sollten wir das Schlüsselwort `await` verwenden. Dieses Feature ist für Ihre `Main`-Methode aber nur verfügbar, wenn Sie C# 7.1 oder höher verwenden.</span><span class="sxs-lookup"><span data-stu-id="09914-145">Since our method is technically asynchronous, we will want to use the `await` keyword, however that feature isn't available on your `Main` method unless you are using C# 7.1 or later.</span></span> <span data-ttu-id="09914-146">Rufen Sie für die Methode einfach `Wait()` auf, um das Warten auf die Rückgabe der Methode zu blockieren. Wir beheben dies in Kürze.</span><span class="sxs-lookup"><span data-stu-id="09914-146">Just call `Wait()` on the method to actually block waiting for the method to return, we'll fix that in a minute.</span></span>

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

## <a name="execute-the-application"></a><span data-ttu-id="09914-147">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="09914-147">Execute the application</span></span>

<span data-ttu-id="09914-148">Die Anwendung kann nun Nachrichten senden.</span><span class="sxs-lookup"><span data-stu-id="09914-148">The application can now send messages.</span></span> <span data-ttu-id="09914-149">Um Sie zu testen, können Sie sie über die Befehlszeile mit dem Befehl `dotnet run` ausführen.</span><span class="sxs-lookup"><span data-stu-id="09914-149">To test it, you can run it from the command line with the `dotnet run` command.</span></span> <span data-ttu-id="09914-150">Zusätzliche Zeichenfolgen werden als Parameter an die Anwendung übergeben.</span><span class="sxs-lookup"><span data-stu-id="09914-150">Any additional strings are passed as parameters to the application.</span></span> 

> [!WARNING]
> <span data-ttu-id="09914-151">Vergewissern Sie sich, dass Sie alle Dateien im Online-Editor gespeichert haben, bevor Sie das Programm erstellen und ausführen.</span><span class="sxs-lookup"><span data-stu-id="09914-151">Make sure you have saved all the files in the online editor before you build and run the program.</span></span>

<span data-ttu-id="09914-152">Sie können beispielsweise Folgendes eingeben:</span><span class="sxs-lookup"><span data-stu-id="09914-152">As an example, you can type:</span></span>

```azurecli
dotnet run Send this message
```

<span data-ttu-id="09914-153">Dies sollte die Zeichenfolge `"Send this message"` der Warteschlange hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="09914-153">This should add the string `"Send this message"` into the queue.</span></span>

## <a name="check-your-results"></a><span data-ttu-id="09914-154">Überprüfen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="09914-154">Check your results</span></span>

<span data-ttu-id="09914-155">Sie können Warteschlangen im Azure-Portal mit dem **Storage-Explorer** überprüfen. Wenn Sie dieses Produkt öffnen, können Sie die Daten in jedem Ihrer Speicherkonten untersuchen.</span><span class="sxs-lookup"><span data-stu-id="09914-155">You can check queues in the Azure portal using the **Storage Explorer**, if you open that product it will let you explore the data in each storage account you own.</span></span>

<span data-ttu-id="09914-156">Alternativ können Sie auch die Azure CLI oder PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="09914-156">Alternatively, you can use the Azure CLI or PowerShell.</span></span> <span data-ttu-id="09914-157">Probieren Sie diesen Befehl in der Shell aus, indem Sie den Wert `<connection-string>` durch Ihre spezifische Verbindungszeichenfolge ersetzen:</span><span class="sxs-lookup"><span data-stu-id="09914-157">Try this command in the shell, replacing the `<connection-string>` value with your specific connection string:</span></span>

```azurecli
az storage message peek --queue-name newsqueue --connection-string <connection-string> 
```

<span data-ttu-id="09914-158">Dies sollte die Informationen für Ihre Nachricht ausgeben, die ungefähr so aussieht:</span><span class="sxs-lookup"><span data-stu-id="09914-158">This should dump the information for your message, which will look something like this:</span></span>

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

<span data-ttu-id="09914-159">Es gibt noch einige andere Befehle, die Sie mit den Tools ausprobieren können. Sehen Sie sich sowohl `az storage queue --help` als auch `az storage message --help` an, um sie zu erkunden.</span><span class="sxs-lookup"><span data-stu-id="09914-159">There are several other commands available that you can try with the tools - check out both `az storage queue --help` and `az storage message --help` to explore them.</span></span>

> [!TIP]
> <span data-ttu-id="09914-160">Geben Sie den Wert Ihrer Verbindungszeichenfolge in eine Umgebungsvariable namens `AZURE_STORAGE_CONNECTION_STRING` ein, damit Sie den Parameter `--connection-string` nicht jedes Mal eingeben müssen!</span><span class="sxs-lookup"><span data-stu-id="09914-160">Put your connection string value into an environment variable named `AZURE_STORAGE_CONNECTION_STRING` to save yourself from having to type the `--connection-string` parameter every time!</span></span>

## <a name="optional---use-the-async-versions-of-the-methods"></a><span data-ttu-id="09914-161">Optional – Verwenden der asynchronen Versionen der Methoden</span><span class="sxs-lookup"><span data-stu-id="09914-161">Optional - Use the async versions of the methods</span></span>

<span data-ttu-id="09914-162">Wir haben `Wait()` für die obige Send-Methode verwendet, aber dies stellt keine effiziente Nutzung unserer Computingressourcen dar.</span><span class="sxs-lookup"><span data-stu-id="09914-162">We used `Wait()` on the send method above but that's not an efficient use of our computing resources.</span></span> <span data-ttu-id="09914-163">Stattdessen sollten wir die C#-Methoden `async` und `await` verwenden.</span><span class="sxs-lookup"><span data-stu-id="09914-163">Instead, we want to use the C# `async` and `await` methods.</span></span> <span data-ttu-id="09914-164">Wir müssen jedoch _mindestens_ C# 7.1 verwenden, um diese Schlüsselwörter auf unsere **Main**-Methode anwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="09914-164">However, we will need to be using _at least_ C# 7.1 to be able to apply these keywords to our **Main** method.</span></span>

### <a name="switch-to-c-71"></a><span data-ttu-id="09914-165">Umstellung auf C# 7.1</span><span class="sxs-lookup"><span data-stu-id="09914-165">Switch to C# 7.1</span></span>

<span data-ttu-id="09914-166">Die C#-Schlüsselwörter `async` und `await` waren bis C# 7.1 keine gültigen Schlüsselwörter in den **Main**-Methoden.</span><span class="sxs-lookup"><span data-stu-id="09914-166">C#'s `async` and `await` keywords were not valid keywords in **Main** methods until C# 7.1.</span></span> <span data-ttu-id="09914-167">Wir können über ein Flag in der Datei **.csproj** ganz einfach auf diesen Compiler umstellen.</span><span class="sxs-lookup"><span data-stu-id="09914-167">We can easily switch to that compiler through a flag in the **.csproj** file.</span></span>

1. <span data-ttu-id="09914-168">Öffnen Sie die Datei **QueueApp.csproj** im Editor.</span><span class="sxs-lookup"><span data-stu-id="09914-168">Open the **QueueApp.csproj** file in the editor.</span></span>

1. <span data-ttu-id="09914-169">Fügen Sie `<LangVersion>7.1</LangVersion>` in die erste `PropertyGroup` in der Builddatei ein.</span><span class="sxs-lookup"><span data-stu-id="09914-169">Add `<LangVersion>7.1</LangVersion>` into the first `PropertyGroup` in the build file.</span></span> <span data-ttu-id="09914-170">Anschließend sollte die Datei so aussehen, wie nachfolgend gezeigt.</span><span class="sxs-lookup"><span data-stu-id="09914-170">It should look like the following when you are finished.</span></span>
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a><span data-ttu-id="09914-171">Anwenden des async-Schlüsselworts</span><span class="sxs-lookup"><span data-stu-id="09914-171">Apply the async keyword</span></span>

<span data-ttu-id="09914-172">Als Nächstes wenden wir das `async`-Schlüsselwort auf die **Main**-Methode an.</span><span class="sxs-lookup"><span data-stu-id="09914-172">Next, apply the `async` keyword to the **Main** method.</span></span> <span data-ttu-id="09914-173">Wir müssen drei Aufgaben erledigen.</span><span class="sxs-lookup"><span data-stu-id="09914-173">We will have to do three things.</span></span>

1. <span data-ttu-id="09914-174">Hinzufügen des Schlüsselworts `async` zur **Main**-Methodensignatur</span><span class="sxs-lookup"><span data-stu-id="09914-174">Add the `async` keyword onto the **Main** method signature.</span></span>
1. <span data-ttu-id="09914-175">Ändern des Rückgabetyps von `void` in `Task`</span><span class="sxs-lookup"><span data-stu-id="09914-175">Change the return type from `void` to `Task`.</span></span>
1. <span data-ttu-id="09914-176">Entfernen des Aufrufs von `Wait()` für den Aufruf von `SendArticleAsync` und Ersetzen durch `await`</span><span class="sxs-lookup"><span data-stu-id="09914-176">Remove the call to `Wait()` on the call to `SendArticleAsync` and replace it with `await`.</span></span>

<span data-ttu-id="09914-177">Versuchen Sie erneut, die App auszuführen. Sie sollte weiterhin wie zuvor funktionieren, aber jetzt kann der Code den Thread wieder für den .NET-Threadpool freigeben, während wir für die Nachricht auf das Einreihen in die Warteschlange warten.</span><span class="sxs-lookup"><span data-stu-id="09914-177">Try running the app again - it should still work exactly as before, but now the code is able to release the thread back to the .NET threadpool while we wait for the message to be queued.</span></span>

<span data-ttu-id="09914-178">Nachdem wir nun eine Nachricht gesendet haben, ist der letzte Schritt, Unterstützung für das _Empfangen_ der Nachricht hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="09914-178">Now that we have sent a message, the last step is to add support to _receive_ the message.</span></span>