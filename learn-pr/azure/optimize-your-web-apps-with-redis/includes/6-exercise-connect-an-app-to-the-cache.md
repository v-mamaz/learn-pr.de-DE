<span data-ttu-id="ba2c0-101">Nachdem wir eine Redis Cache-Instanz in Azure erstellt haben, werden wir jetzt eine Anwendung zur Verwendung von Redis Cache erstellen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-101">Now that we have a Redis cache created in Azure, let's create an application to use it.</span></span> <span data-ttu-id="ba2c0-102">Stellen Sie sicher, dass Sie über die Informationen zu Ihrer Verbindungszeichenfolge aus dem Azure-Portal verfügen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-102">Make sure you have your connection string information from the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="ba2c0-103">Die integrierte Cloud Shell ist auf der rechten Seite verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-103">The integrated Cloud Shell is available on the right.</span></span> <span data-ttu-id="ba2c0-104">Sie können diese Eingabeaufforderung verwenden, um den hier entwickelten Beispielcode zu erstellen und auszuführen. Alternativ können Sie diese Schritte lokal ausführen, wenn Sie eine Entwicklungsumgebung eingerichtet haben.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-104">You can use that command prompt to create and run the example code we are building here, or perform these steps locally if you have a development environment setup.</span></span> <span data-ttu-id="ba2c0-105">Wenn Sie sich für die Cloud Shell entscheiden, wählen Sie die Bash-Shell aus, wenn Sie zu einer Auswahl aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-105">If you decide to use the Cloud Shell, please select the Bash shell if you are prompted for a selection.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="ba2c0-106">Erstellen einer Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="ba2c0-106">Create a Console Application</span></span>

<span data-ttu-id="ba2c0-107">Wir verwenden eine einfache Konsolenanwendung, damit wir uns auf die Redis-Implementierung konzentrieren können.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-107">We'll use a simple Console Application so we can focus on the Redis implementation.</span></span>

1. <span data-ttu-id="ba2c0-108">Erstellen Sie in der Cloud Shell eine neue .NET Core-Konsolenanwendung namens „SportsStatsTracker“.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-108">In the Cloud Shell, create a new .NET Core Console Application, name it "SportsStatsTracker"</span></span>

    ```bash
    dotnet new console --name SportsStatsTracker
    ```
    
1. <span data-ttu-id="ba2c0-109">Hierdurch wird ein Ordner für das Projekt erstellt. Ändern Sie dann das aktuelle Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-109">This will create a folder for the project, go ahead and change the current directory.</span></span>

    ```bash
    cd SportsStatsTracker
    ```
    
## <a name="add-the-connection-string"></a><span data-ttu-id="ba2c0-110">Hinzufügen der Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="ba2c0-110">Add the connection string</span></span>

<span data-ttu-id="ba2c0-111">Jetzt fügen wir die Verbindungszeichenfolge zum Code hinzu, die wir aus dem Azure-Portal abgerufen haben.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-111">Let's add the connection string we got from the Azure portal into the code.</span></span> <span data-ttu-id="ba2c0-112">Speichern Sie niemals Anmeldeinformationen wie diese in Ihrem Quellcode.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-112">Never store credentials like this in your source code.</span></span> <span data-ttu-id="ba2c0-113">Um dieses Beispiel einfach zu halten, verwenden wir eine Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-113">To keep this sample simple, we're going to use a configuration file.</span></span> <span data-ttu-id="ba2c0-114">Ein besserer Ansatz für eine serverseitige Anwendung in Azure wäre die Verwendung von Azure Key Vault mit Zertifikaten.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-114">A better approach for a server-side application in Azure would be to use Azure Key Vault with certificates.</span></span>

1. <span data-ttu-id="ba2c0-115">Erstellen Sie eine Datei **appsettings.json**, um sie zum Projekt hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-115">Create a new **appsettings.json** file to add to the project.</span></span>

    ```bash
    touch appsettings.json
    ```

1. <span data-ttu-id="ba2c0-116">Öffnen Sie den Code-Editor, indem Sie im Projektordner `code .` eingeben.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-116">Open the code editor by typing `code .` in the project folder.</span></span> <span data-ttu-id="ba2c0-117">Wenn Sie lokal arbeiten, wird die Verwendung von **Visual Studio Code** empfohlen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-117">If you are working locally, we recommend using **Visual Studio Code**.</span></span> <span data-ttu-id="ba2c0-118">Die hier gezeigten Verwendungsschritte sind größtenteils gleich.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-118">The steps here will mostly align with it's usage.</span></span>

1. <span data-ttu-id="ba2c0-119">Wählen Sie die Datei **appsettings.json** im Editor aus, und fügen Sie den folgenden Text hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-119">Select the **appsettings.json** file in the editor and add the following text.</span></span> <span data-ttu-id="ba2c0-120">Fügen Sie Ihre Verbindungszeichenfolge in den **Wert** der Einstellung ein.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-120">Paste your connection string into the **value** of the setting.</span></span>

    ```json
    {
      "CacheConnection": "[value-goes-here]"
    }
    ```

1. <span data-ttu-id="ba2c0-121">Speichern Sie die Datei – im Online-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-121">Save the file - in the online editor, there is a menu in the top right corner which has common file operations.</span></span>

1. <span data-ttu-id="ba2c0-122">Fügen Sie den folgenden Konfigurationsblock hinzu, um die neue Datei in das Projekt einzuschließen und sie in den Ausgabeordner zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-122">Add the following configuration block to include the new file in the project and copy it to the output folder.</span></span> <span data-ttu-id="ba2c0-123">Dadurch wird sichergestellt, dass die App-Konfigurationsdatei im Ausgabeverzeichnis platziert wird, wenn die App kompiliert/erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-123">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
       ...
        <ItemGroup>
            <None Update="appsettings.json">
              <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
            </None>
        </ItemGroup>
    </Project>
    ```

1. <span data-ttu-id="ba2c0-124">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-124">Save the file.</span></span> <span data-ttu-id="ba2c0-125">(Wenn Sie die Datei nicht sichern, verlieren Sie die vorgenommenen Änderungen beim Hinzufügen des Pakets weiter unten!)</span><span class="sxs-lookup"><span data-stu-id="ba2c0-125">(Make sure you do this or you will lose the change when you add the package below!)</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="ba2c0-126">Hinzufügen von Unterstützung zum Lesen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="ba2c0-126">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="ba2c0-127">Eine .NET Core-Anwendung benötigt zusätzliche NuGet-Pakete, um eine JSON-Konfigurationsdatei zu lesen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-127">A .NET Core application requires additional NuGet packages to read a JSON configuration file.</span></span>

1. <span data-ttu-id="ba2c0-128">Fügen Sie im Abschnitt der Eingabeaufforderung einen Verweis auf das NuGet-Paket **Microsoft.Extensions.Configuration.Json** hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-128">In the command prompt section of the window, add a reference to the  **Microsoft.Extensions.Configuration.Json** NuGet package.</span></span>

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="ba2c0-129">Hinzufügen von Code zum Lesen der Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="ba2c0-129">Add code to read the configuration file</span></span>

<span data-ttu-id="ba2c0-130">Nachdem wir die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Konsolenanwendung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-130">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="ba2c0-131">Wählen Sie im Editor die Datei **Program.cs** aus.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-131">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="ba2c0-132">Am Anfang der Datei ist die Zeile **using System;** vorhanden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-132">At the top of the file, a **using System;** line is present.</span></span> <span data-ttu-id="ba2c0-133">Fügen Sie unterhalb dieser Zeile die folgenden Codezeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="ba2c0-133">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="ba2c0-134">Ersetzen Sie den Inhalt der Methode **Main** durch den nachstehenden Code.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-134">Replace the contents of the **Main** method with the following code.</span></span> <span data-ttu-id="ba2c0-135">Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-135">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

    ```csharp
    var config = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json")
        .Build();
    ```

<span data-ttu-id="ba2c0-136">Ihre Datei **Program.cs** sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="ba2c0-136">Your **Program.cs** file should now look like the following:</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace SportsStatsTracker
{
    class Program
    {
        static void Main(string[] args)
        {
            var config = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json")
                .Build();
        }
    }
}
```

## <a name="get-the-connection-string-from-configuration"></a><span data-ttu-id="ba2c0-137">Abrufen der Verbindungszeichenfolge aus der Konfiguration</span><span class="sxs-lookup"><span data-stu-id="ba2c0-137">Get the connection string from configuration</span></span>

1. <span data-ttu-id="ba2c0-138">Verwenden Sie in **Program.cs** am Ende der Methode **Main** die neue Variable **config**, um die Verbindungszeichenfolge anzurufen und sie in einer neuen Variable namens **connectionString** zu speichern.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-138">In **Program.cs**, at the end of the **Main** method, use the new **config** variable to retrieve the connection string and store it in a new variable named **connectionString**.</span></span>
    - <span data-ttu-id="ba2c0-139">Die Variable **config** umfasst einen Indexer, an den Sie eine Zeichenfolge übergeben können, die aus Ihrer Datei **appSettings.json** abgerufen werden soll.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-139">The **config** variable has an indexer where you can pass in a string to retrieve from your **appSettings.json** file.</span></span>

    ```csharp
    string connectionString = config["CacheConnection"];
    ```
    
## <a name="add-support-for-the-redis-cache-net-client"></a><span data-ttu-id="ba2c0-140">Hinzufügen von Unterstützung für den Redis Cache-Client für .NET</span><span class="sxs-lookup"><span data-stu-id="ba2c0-140">Add support for the Redis cache .NET client</span></span>

<span data-ttu-id="ba2c0-141">Als Nächstes konfigurieren wir die Konsolenanwendung zur Verwendung des **StackExchange.Redis**-Clients für .NET.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-141">Next, let's configure the console application to use the **StackExchange.Redis** client for .NET.</span></span>

1. <span data-ttu-id="ba2c0-142">Fügen Sie dem Projekt mithilfe der Eingabeaufforderung unten im Cloud Shell-Editor das NuGet-Paket **StackExchange.Redis** hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-142">Add the **StackExchange.Redis** NuGet package to the project using the command prompt at the bottom of the Cloud Shell editor.</span></span>

    ```bash
    dotnet add package StackExchange.Redis
    ```

1. <span data-ttu-id="ba2c0-143">Wählen Sie im Editor **Program.cs** aus, und fügen Sie `using` für den Namespace **StackExchange.Redis** hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-143">Select **Program.cs** in the editor and add a `using` for the namespace **StackExchange.Redis**</span></span>

    ```csharp
    using StackExchange.Redis;
    ```
    
<span data-ttu-id="ba2c0-144">Nach Abschluss der Installation kann der Redis Cache-Client für Ihr Projekt verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-144">Once the installation is completed, the Redis cache client is available to use with your project.</span></span>

## <a name="connect-to-the-cache"></a><span data-ttu-id="ba2c0-145">Herstellen einer Verbindung mit dem Cache</span><span class="sxs-lookup"><span data-stu-id="ba2c0-145">Connect to the cache</span></span>

<span data-ttu-id="ba2c0-146">Fügen wir Code zur Verbindungsherstellung mit dem Cache hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-146">Let's add the code to connect to the cache.</span></span>

1. <span data-ttu-id="ba2c0-147">Wählen Sie im Editor die Datei **Program.cs** aus.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-147">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="ba2c0-148">Erstellen Sie einen `ConnectionMultiplexer` unter Verwendung von `ConnectionMultiplexer.Connect`, indem Sie Ihre Verbindungszeichenfolge übergeben.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-148">Create a `ConnectionMultiplexer` using `ConnectionMultiplexer.Connect` by passing it your connection string.</span></span> <span data-ttu-id="ba2c0-149">Geben Sie dem Rückgabewert den Namen **cache**.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-149">Name the returned value **cache**.</span></span>

1. <span data-ttu-id="ba2c0-150">Die erstellte Verbindung ist _verwerfbar_, umschließen Sie sie deshalb mit einem `using`-Block.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-150">Since the created connection is _disposable_, wrap it in a `using` block.</span></span> <span data-ttu-id="ba2c0-151">Ihr Code sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="ba2c0-151">Your code should look something like:</span></span>

    ```csharp
    string connectionString = config["CacheConnection"];
    
    using (var cache = ConnectionMultiplexer.Connect(connectionString))
    {
        
    }
    ```

> [!NOTE] 
> <span data-ttu-id="ba2c0-152">Die Verbindung mit Azure Redis Cache wird über die `ConnectionMultiplexer`-Klasse verwaltet.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-152">The connection to Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="ba2c0-153">Diese Klasse muss in Ihrer gesamten Clientanwendung freigegeben und wiederverwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-153">This class should be shared and reused throughout your client application.</span></span> <span data-ttu-id="ba2c0-154">Es soll _nicht_ für jeden Vorgang eine neue Verbindung erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-154">We do _not_ want to create a new connection for each operation.</span></span> <span data-ttu-id="ba2c0-155">Stattdessen soll die Verbindung als Feld in unserer Klasse gespeichert und für jeden Vorgang wiederverwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-155">Instead, we want to store it off as a field in our class and reuse it for each operation.</span></span> <span data-ttu-id="ba2c0-156">Hier wird die Verbindung nur in der Methode **Main** verwendet, aber in einer Produktionsanwendung sollte sie in einem Klassenfeld oder in einem Singleton gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-156">Here we are only going to use it in the **Main** method, but in a production application, it should be stored in a class field, or a singleton.</span></span>

## <a name="add-a-value-to-the-cache"></a><span data-ttu-id="ba2c0-157">Hinzufügen eines Werts zum Cache</span><span class="sxs-lookup"><span data-stu-id="ba2c0-157">Add a value to the cache</span></span>

<span data-ttu-id="ba2c0-158">Nun, da eine Verbindung vorhanden ist, fügen wir dem Cache einen Wert hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-158">Now that we have the connection, let's add a value to the cache.</span></span>

1. <span data-ttu-id="ba2c0-159">Verwenden Sie nach der Verbindungsherstellung im Block `using` die Methode `GetDatabase`, um eine `IDatabase`-Instanz abzurufen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-159">Inside the `using` block after the connection has been created, use the `GetDatabase` method to retrieve an `IDatabase` instance.</span></span>

1. <span data-ttu-id="ba2c0-160">Rufen Sie `StringSet` für das `IDatabase`-Objekt auf, um den Schlüssel „test:key“ auf den Wert „some value“ festzulegen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-160">Call `StringSet` on the `IDatabase` object to set the key "test:key" to the value "some value".</span></span>
    - <span data-ttu-id="ba2c0-161">Der Rückgabewert von `StringSet` ist ein Wert vom Typ `bool`, der angibt, ob der Schlüssel hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-161">the return value from `StringSet` is a `bool` indicating whether the key was added.</span></span>

1. <span data-ttu-id="ba2c0-162">Zeigen Sie den Rückgabewert von `StringSet` auf der Konsole an.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-162">Display the return value from `StringSet` onto the console.</span></span>

    ```csharp
    bool setValue = db.StringSet("test:key", "some value");
    Console.WriteLine($"SET: {setValue}");
    ```
    
## <a name="get-a-value-from-the-cache"></a><span data-ttu-id="ba2c0-163">Abrufen eines Werts aus dem Cache</span><span class="sxs-lookup"><span data-stu-id="ba2c0-163">Get a value from the cache</span></span>

1. <span data-ttu-id="ba2c0-164">Als Nächstes rufen wir den Wert mithilfe von `StringGet` ab.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-164">Next, retrieve the value using `StringGet`.</span></span> <span data-ttu-id="ba2c0-165">Hierbei wird der Schlüssel verwendet, um den Wert abzurufen und zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-165">This takes the key to retrieve and returns the value.</span></span>

1. <span data-ttu-id="ba2c0-166">Geben Sie dem Rückgabewert aus.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-166">Output the returned value.</span></span>

    ```csharp
    string getValue = db.StringGet("test:key");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. <span data-ttu-id="ba2c0-167">Ihr Code sollte folgendermaßen aussehen:</span><span class="sxs-lookup"><span data-stu-id="ba2c0-167">Your code should look like this:</span></span>

    ```csharp
    using System;
    using Microsoft.Extensions.Configuration;
    using System.IO;
    using StackExchange.Redis;
    
    namespace SportsStatsTracker
    {
        class Program
        {
            static void Main(string[] args)
            {
                var config = new ConfigurationBuilder()
                    .SetBasePath(Directory.GetCurrentDirectory())
                    .AddJsonFile("appsettings.json")
                    .Build();
    
                string connectionString = config["CacheConnection"];
    
                using (var cache = ConnectionMultiplexer.Connect(connectionString))
                {
                    var db = cache.GetDatabase();
    
                    bool setValue = db.StringSet("test:key", "some value");
                    Console.WriteLine($"SET: {setValue}");
    
                    string getValue = db.StringGet("test:key");
                    Console.WriteLine($"GET: {getValue}");
                }
            }
        }
    }
    ```
    
1. <span data-ttu-id="ba2c0-168">Führen Sie die Anwendung aus, um das Ergebnis anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-168">Run the application to see the result.</span></span> <span data-ttu-id="ba2c0-169">Geben Sie in das Terminalfenster unterhalb des Editors `dotnet run` ein.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-169">Type `dotnet run` into the terminal window below the editor.</span></span> <span data-ttu-id="ba2c0-170">Stellen Sie sicher, dass Sie sich im Projektordner befinden. Ansonsten wird der Code für Erstellung und Ausführung nicht gefunden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-170">Make sure you are in the project folder or it won't find your code to build and run.</span></span>
    
    ```bash
    dotnet run
    ```
    
## <a name="use-the-async-versions-of-the-methods"></a><span data-ttu-id="ba2c0-171">Verwenden der asynchronen Versionen der Methoden</span><span class="sxs-lookup"><span data-stu-id="ba2c0-171">Use the async versions of the methods</span></span>

<span data-ttu-id="ba2c0-172">Wir konnten Werte aus dem Cache abrufen und im Cache festlegen, aber wir verwenden die älteren, synchronen Versionen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-172">We have been able to get and set values from the cache, but we are using the older synchronous versions.</span></span> <span data-ttu-id="ba2c0-173">In serverseitigen Anwendungen bieten diese keine effiziente Verwendung unserer Threads.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-173">In server-side applications, these are not an efficient use of our threads.</span></span> <span data-ttu-id="ba2c0-174">Stattdessen möchten wir die _asynchronen_ Versionen der Methoden verwenden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-174">Instead, we want to use the _asynchronous_ versions of the methods.</span></span> <span data-ttu-id="ba2c0-175">Diese Methodenversionen sind leicht zu erkennen: sie senden immer auf **Async**.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-175">You can easily spot them - they all end in **Async**.</span></span>

<span data-ttu-id="ba2c0-176">Zur einfacheren Arbeit mit diesen Methoden können wir die C#-Schlüsselwörter `async` und `await` verwenden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-176">To make these methods easy to work with, we can use the C# `async` and `await` keywords.</span></span> <span data-ttu-id="ba2c0-177">Wir müssen jedoch _mindestens_ C# 7.1 verwenden, um diese Schlüsselwörter auf unsere **Main**-Methode anwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-177">However, we will need to be using _at least_ C# 7.1 to be able to apply these keywords to our **Main** method.</span></span>

### <a name="switch-to-c-71"></a><span data-ttu-id="ba2c0-178">Umstellung auf C# 7.1</span><span class="sxs-lookup"><span data-stu-id="ba2c0-178">Switch to C# 7.1</span></span>

<span data-ttu-id="ba2c0-179">Die C#-Schlüsselwörter `async` und `await` waren bis C# 7.1 keine gültigen Schlüsselwörter in den **Main**-Methoden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-179">C#'s `async` and `await` keywords were not valid keywords in **Main** methods until C# 7.1.</span></span> <span data-ttu-id="ba2c0-180">Wir können über ein Flag in der Datei **.csproj** ganz einfach auf diesen Compiler umstellen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-180">We can easily switch to that compiler through a flag in the **.csproj** file.</span></span>

1. <span data-ttu-id="ba2c0-181">Öffnen Sie die Datei **SportsStatsTracker.csproj** im Editor.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-181">Open the **SportsStatsTracker.csproj** file in the editor.</span></span>

1. <span data-ttu-id="ba2c0-182">Fügen Sie `<LangVersion>7.1</LangVersion>` in die erste `PropertyGroup` in der Builddatei ein.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-182">Add `<LangVersion>7.1</LangVersion>` into the first `PropertyGroup` in the build file.</span></span> <span data-ttu-id="ba2c0-183">Anschließend sollte die Datei so aussehen, wie nachfolgend gezeigt.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-183">It should look like the following when you are finished.</span></span>
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a><span data-ttu-id="ba2c0-184">Anwenden des async-Schlüsselworts</span><span class="sxs-lookup"><span data-stu-id="ba2c0-184">Apply the async keyword</span></span>

<span data-ttu-id="ba2c0-185">Als Nächstes wenden wir das `async`-Schlüsselwort auf die **Main**-Methode an.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-185">Next, apply the `async` keyword to the **Main** method.</span></span> <span data-ttu-id="ba2c0-186">Wir müssen drei Aufgaben erledigen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-186">We will have to do three things.</span></span>

1. <span data-ttu-id="ba2c0-187">Hinzufügen des Schlüsselworts `async` zur **Main**-Methodensignatur</span><span class="sxs-lookup"><span data-stu-id="ba2c0-187">Add the `async` keyword onto the **Main** method signature.</span></span>
1. <span data-ttu-id="ba2c0-188">Ändern des Rückgabetyps von `void` in `Task`</span><span class="sxs-lookup"><span data-stu-id="ba2c0-188">Change the return type from `void` to `Task`.</span></span>
1. <span data-ttu-id="ba2c0-189">Hinzufügen einer `using`-Anweisung zum Einschließen von `System.Threading.Tasks`</span><span class="sxs-lookup"><span data-stu-id="ba2c0-189">Add a `using` statement to include `System.Threading.Tasks`.</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using StackExchange.Redis;
using System.Threading.Tasks;

namespace SportsStatsTracker
{
    class Program
    {
        static async Task Main(string[] args)
        {
        ...
```

### <a name="get-and-set-values-asynchronously"></a><span data-ttu-id="ba2c0-190">Asynchrones Abrufen und Festlegen von Werten</span><span class="sxs-lookup"><span data-stu-id="ba2c0-190">Get and set values asynchronously</span></span>

1. <span data-ttu-id="ba2c0-191">Verwenden Sie die Methoden `StringSetAsync` und `StringGetAsync`, um einen Schlüssel namens „counter“ festzulegen und abzurufen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-191">Use the `StringSetAsync` and `StringGetAsync` methods to set and retrieve a key named "counter".</span></span> <span data-ttu-id="ba2c0-192">Legen Sie den Wert auf 100 fest.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-192">Set the value to "100".</span></span>

1. <span data-ttu-id="ba2c0-193">Wenden Sie das Schlüsselwort `await` an, um die Ergebnisse von jeder Methode abzurufen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-193">Apply the `await` keyword to get the results from each method.</span></span>

1. <span data-ttu-id="ba2c0-194">Geben Sie die Ergebnisse im Konsolenfenster aus – wie zuvor bei den synchronen Versionen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-194">Output the results to the console window - just as you did with the synchronous versions.</span></span>

    ```csharp
    // Simple get and put of integral data types into the cache
    setValue = await db.StringSetAsync("test", "100");
    Console.WriteLine($"SET: {setValue}");
    
    getValue = await db.StringGetAsync("test");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. <span data-ttu-id="ba2c0-195">Führen Sie jetzt erneut die Anwendung aus. Sie sollte weiterhin funktionieren und jetzt zwei Werte aufweisen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-195">Run the application again - it should still work and now have two values.</span></span>

#### <a name="increment-the-value"></a><span data-ttu-id="ba2c0-196">Erhöhen des Werts</span><span class="sxs-lookup"><span data-stu-id="ba2c0-196">Increment the value</span></span>

1. <span data-ttu-id="ba2c0-197">Verwenden Sie die Methode `StringIncrementAsync`, um Ihren **counter**-Wert zu erhöhen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-197">Use the `StringIncrementAsync` method to increment your **counter** value.</span></span> <span data-ttu-id="ba2c0-198">Übergeben Sie die Zahl **50**, um sie zu „counter“ hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-198">Pass the number **50** to add to the counter.</span></span>
    - <span data-ttu-id="ba2c0-199">Beachten Sie, dass die Methode den Schlüssel _und_ entweder `long` oder `double` verwendet.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-199">Notice that the method takes the key _and_ either a `long` or `double`.</span></span>
    - <span data-ttu-id="ba2c0-200">Je nachdem, welche Parameter übergeben wurden, wird `long` oder `double` zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-200">Depending on the parameters passed, it either returns a `long` or `double`.</span></span>

1. <span data-ttu-id="ba2c0-201">Geben Sie die Ergebnisse der Methode an die Konsole zurück.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-201">Output the results of the method to the console.</span></span>

    ```csharp
    long newValue = await db.StringIncrementAsync("counter", 50);
    Console.WriteLine($"INCR new value = {newValue}");
    ```
    
## <a name="other-operations"></a><span data-ttu-id="ba2c0-202">Weitere Vorgänge</span><span class="sxs-lookup"><span data-stu-id="ba2c0-202">Other operations</span></span>

<span data-ttu-id="ba2c0-203">Abschließend versuchen wir, einige zusätzliche Methoden mit Unterstützung von `ExecuteAsync` auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-203">Finally, let's try executing a few additional methods with the `ExecuteAsync` support.</span></span>

1. <span data-ttu-id="ba2c0-204">Führen Sie „PING“ aus, um die Serververbindung zu testen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-204">Execute "PING" to test the server connection.</span></span> <span data-ttu-id="ba2c0-205">Die Antwort sollte „PONG“ lauten.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-205">It should respond with "PONG".</span></span>
1. <span data-ttu-id="ba2c0-206">Führen Sie „FLUSHDB“ aus, um die Datenbankwerte zu löschen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-206">Execute "FLUSHDB" to clear the database values.</span></span> <span data-ttu-id="ba2c0-207">Die Antwort sollte „OK“ lauten.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-207">It should respond with "OK".</span></span>

```csharp
var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

result = await db.ExecuteAsync("flushdb");
Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
```

## <a name="challenge"></a><span data-ttu-id="ba2c0-208">Herausforderung</span><span class="sxs-lookup"><span data-stu-id="ba2c0-208">Challenge</span></span>

<span data-ttu-id="ba2c0-209">Versuchen Sie, als Herausforderung einen Objekttyp im Cache zu serialisieren.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-209">As a challenge, try serializing an object type to the cache.</span></span> <span data-ttu-id="ba2c0-210">Nachfolgend werden die grundlegenden Schritte gezeigt.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-210">Here are the basic steps.</span></span>

1. <span data-ttu-id="ba2c0-211">Erstellen Sie eine neue `class` mit einigen öffentlichen Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-211">Create a new `class` with some public properties.</span></span> <span data-ttu-id="ba2c0-212">Sie können eine eigene Klasse erfinden (gängig sind z.B. „Person“ oder „Auto“) oder das Beispiel „GameStats“ aus der vorherigen Einheit verwenden.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-212">You can invent one of your own ("Person" or "Car" are popular), or use the "GameStats" example given in the previous unit.</span></span>
1. <span data-ttu-id="ba2c0-213">Fügen Sie mit `dotnet add package` Unterstützung für das NuGet-Paket **Newtonsoft.Json** hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-213">Add support for the **Newtonsoft.Json** NuGet package using `dotnet add package`.</span></span>
1. <span data-ttu-id="ba2c0-214">Fügen Sie `using` für den `Newtonsoft.Json`-Namespace hinzu.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-214">Add a `using` for the `Newtonsoft.Json` namespace.</span></span>
1. <span data-ttu-id="ba2c0-215">Erstellen Sie eines Ihrer Objekte.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-215">Create one of your objects.</span></span>
1. <span data-ttu-id="ba2c0-216">Serialisieren Sie es mit `JsonConvert.SerializeObject`, und verwenden Sie `StringSetAsync`, um es per Push in den Cache zu übertragen.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-216">Serialize it with `JsonConvert.SerializeObject` and use `StringSetAsync` to push it into the cache.</span></span>
1. <span data-ttu-id="ba2c0-217">Rufen Sie das Objekt mit `StringGetAsync` aus dem Cache ab, und deserialisieren Sie es anschließend mit `JsonConvert.DeserializeObject<T>`.</span><span class="sxs-lookup"><span data-stu-id="ba2c0-217">Get it back from the cache with `StringGetAsync` and then deserialize it with `JsonConvert.DeserializeObject<T>`.</span></span>

