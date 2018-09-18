<span data-ttu-id="46cd6-101">Zunächst erstellen Sie einen Redis Cache in Azure und dann eine einfache Transaktion, die zwei Datenwerte in den Cache einfügt.</span><span class="sxs-lookup"><span data-stu-id="46cd6-101">Let's start by creating a Redis cache instance in Azure, then create a simple transaction that inserts two data values into the cache.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="46cd6-102">Erstellen eines Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="46cd6-102">Create an Azure Redis Cache</span></span>

<span data-ttu-id="46cd6-103">Sie beginnen mit der Erstellung eines Azure Redis Cache über die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="46cd6-103">Let's start by creating an Azure Redis Cache with the Azure CLI.</span></span> <span data-ttu-id="46cd6-104">Verwenden Sie Cloud Shell auf der rechten Seite des Browserfensters, um mit Azure zu interagieren.</span><span class="sxs-lookup"><span data-stu-id="46cd6-104">Use the Cloud Shell on the right side of the browser window to interact with Azure.</span></span>

<span data-ttu-id="46cd6-105">Verwenden Sie den Befehl `azure rediscache create`, um einen neuen Azure Redis Cache zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="46cd6-105">We'll use the `azure rediscache create` command to create a new Azure Redis Cache.</span></span> <span data-ttu-id="46cd6-106">Es werden mehrere Parameter benötigt.</span><span class="sxs-lookup"><span data-stu-id="46cd6-106">It takes several parameters.</span></span> <span data-ttu-id="46cd6-107">An dieser Stelle sind die gängigsten aufgeführt (eine vollständige Liste finden Sie in der Dokumentation).</span><span class="sxs-lookup"><span data-stu-id="46cd6-107">Here are the most common (to get a full list, check the documentation).</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="46cd6-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="46cd6-108">Parameter</span></span> | <span data-ttu-id="46cd6-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="46cd6-109">Description</span></span> |
> |-----------|-------------|
> | `--name`    | <span data-ttu-id="46cd6-110">Der Name des Cache: muss global eindeutig sein und sich aus Buchstaben, Zahlen und Bindestrichen zusammensetzen.</span><span class="sxs-lookup"><span data-stu-id="46cd6-110">The name of the cache - this must be globally unique and composed of letters, numbers and dashes.</span></span> |
> | `--resource-group` | <span data-ttu-id="46cd6-111">Verwenden Sie die vorab erstellte Ressourcengruppe <rgn>[Name der Sandbox-Ressourcengruppe]</rgn>, die zur Azure-Sandbox gehört.</span><span class="sxs-lookup"><span data-stu-id="46cd6-111">Use the pre-created Resource Group <rgn>[Sandbox resource group name]</rgn> which is part of the Azure Sandbox.</span></span> |
> | `--location` | <span data-ttu-id="46cd6-112">Geben Sie den Ort an, an dem sich der Cache befinden soll.</span><span class="sxs-lookup"><span data-stu-id="46cd6-112">Specify the location where the cache should be located.</span></span> <span data-ttu-id="46cd6-113">Normalerweise würden Sie wahrscheinlich einen Standort in der Nähe der Datenconsumer wählen.</span><span class="sxs-lookup"><span data-stu-id="46cd6-113">Normally, you will want to choose a location close to the data consumers.</span></span> <span data-ttu-id="46cd6-114">In diesem Fall sind Sie auf die in der Azure-Sandbox verfügbaren Standorte beschränkt.</span><span class="sxs-lookup"><span data-stu-id="46cd6-114">In this case, you are limited to the locations available in the Azure Sandbox.</span></span> <span data-ttu-id="46cd6-115">Wählen Sie den Standort aus, der Ihnen am nächsten liegt.</span><span class="sxs-lookup"><span data-stu-id="46cd6-115">Select the closest one to you.</span></span> |
> | `--size` | <span data-ttu-id="46cd6-116">Die Größe des Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="46cd6-116">Size of the Redis Cache.</span></span> <span data-ttu-id="46cd6-117">Gültige Werte sind [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4].</span><span class="sxs-lookup"><span data-stu-id="46cd6-117">Valid values are [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
> | `--sku` | <span data-ttu-id="46cd6-118">Redis-SKU.</span><span class="sxs-lookup"><span data-stu-id="46cd6-118">Redis SKU.</span></span> <span data-ttu-id="46cd6-119">Gültige Werte sind [Basic, Standard, Premium].</span><span class="sxs-lookup"><span data-stu-id="46cd6-119">Valid values are [Basic, Standard, Premium]</span></span> |
> | `--enable-non-ssl-port` | <span data-ttu-id="46cd6-120">Fügen Sie dieses Flag hinzu, wenn Sie den Nicht-SSL-Port für Ihren Cache aktivieren möchten.</span><span class="sxs-lookup"><span data-stu-id="46cd6-120">Add this flag if you want to enable the Non SSL Port for your cache.</span></span> |

### <a name="selecting-a-location"></a><span data-ttu-id="46cd6-121">Auswahl eines Standorts</span><span class="sxs-lookup"><span data-stu-id="46cd6-121">Selecting a location</span></span>
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="46cd6-122">Erstellen Sie einen Cache mit den folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="46cd6-122">Create a cache using the following options:</span></span>
    - <span data-ttu-id="46cd6-123">Größe: C0</span><span class="sxs-lookup"><span data-stu-id="46cd6-123">Size: C0</span></span>
    - <span data-ttu-id="46cd6-124">SKU: Basic</span><span class="sxs-lookup"><span data-stu-id="46cd6-124">SKU: Basic</span></span>
    - <span data-ttu-id="46cd6-125">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="46cd6-125">EnableNonSslPort</span></span>
    
1. <span data-ttu-id="46cd6-126">Hier ist eine exemplarische Befehlszeile, stellen Sie sicher, dass Sie **[name]** und **[location]** durch gültige Werte ersetzen.</span><span class="sxs-lookup"><span data-stu-id="46cd6-126">Here's an example command line, make sure to replace the **[name]** and **[location]** with valid values.</span></span>

    ```azurecli
    azure rediscache create \
        --name [name] \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location [location] \
        --size C0 --sku Basic
    ```

1. <span data-ttu-id="46cd6-127">Das Erstellen des Cache dauert einige Minuten.</span><span class="sxs-lookup"><span data-stu-id="46cd6-127">It will take a few minutes to create the cache.</span></span>

## <a name="create-a-net-core-console-application"></a><span data-ttu-id="46cd6-128">Erstellen einer .NET Core-Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="46cd6-128">Create a .NET Core Console application</span></span>

<span data-ttu-id="46cd6-129">Als Nächstes erstellen Sie eine C#-basierte .NET Core-Konsolenanwendung, mit der Sie Datenwerte in den Azure Redis Cache einfügen können.</span><span class="sxs-lookup"><span data-stu-id="46cd6-129">Next, create a .NET Core C#-based console application, which will be used to insert data values into our Azure Redis Cache.</span></span>

1. <span data-ttu-id="46cd6-130">Erstellen Sie mithilfe der integrierten Cloud Shell auf der rechten Fensterseite eine neue .NET Core-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="46cd6-130">Create a new .NET Core application using the integrated Cloud Shell on the right hand side of the window.</span></span> <span data-ttu-id="46cd6-131">Nennen Sie sie „RedisData“.</span><span class="sxs-lookup"><span data-stu-id="46cd6-131">Name it "RedisData".</span></span>

    ```bash
    dotnet new console --name RedisData
    ```
    
1. <span data-ttu-id="46cd6-132">Wechseln Sie in das neue Verzeichnis, das für Ihre App erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="46cd6-132">Change into the new directory created for your app.</span></span>

    ```bash
    cd RedisData
    ```
    
1. <span data-ttu-id="46cd6-133">Darin sollten sich eine Projektdatei und eine einzelne Quelldatei namens **Program.cs** befinden.</span><span class="sxs-lookup"><span data-stu-id="46cd6-133">You should find a project file, and a single **Program.cs** source file.</span></span>

1. <span data-ttu-id="46cd6-134">Erstellen Sie die Anwendung, und führen Sie sie aus. Sie sollten „Hello, World!“ als Ausgabe erhalten.</span><span class="sxs-lookup"><span data-stu-id="46cd6-134">Build and run the application - it should output "Hello, World!".</span></span>

    ```bash
    dotnet run
    ```
    
## <a name="add-the-servicestackredis-nuget-package"></a><span data-ttu-id="46cd6-135">Hinzufügen des NuGet-Pakets „ServiceStack.Redis“</span><span class="sxs-lookup"><span data-stu-id="46cd6-135">Add the ServiceStack.Redis NuGet package</span></span>

<span data-ttu-id="46cd6-136">Nachdem nun die Konsolenanwendung fertig erstellt ist, können Sie das NuGet-Paket **ServiceStack.Redis** hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="46cd6-136">Now that we have our console application, we need to add the **ServiceStack.Redis** NuGet package.</span></span> <span data-ttu-id="46cd6-137">Dies ermöglicht es Ihnen, eine Verbindung zum Redis Cache herzustellen und Befehle in C# auszugeben.</span><span class="sxs-lookup"><span data-stu-id="46cd6-137">This will allow us to connect to the Redis Cache and issue commands in C#.</span></span>

1. <span data-ttu-id="46cd6-138">Fügen Sie das NuGet-Paket **ServiceStack.Redis** mithilfe der Terminalshell hinzu.</span><span class="sxs-lookup"><span data-stu-id="46cd6-138">Add the NuGet package **ServiceStack.Redis** using the terminal shell.</span></span>

    ```bash
    dotnet add package ServiceStack.Redis
    ```
    
1. <span data-ttu-id="46cd6-139">Kompilieren und starten Sie die Anwendung erneut, um sicherzustellen, dass alles vollständig kompiliert ist.</span><span class="sxs-lookup"><span data-stu-id="46cd6-139">Build and run the application again to make sure it all compiles.</span></span> <span data-ttu-id="46cd6-140">Wie zuvor, sollte die Ausgabe „Hello, World!“ lauten.</span><span class="sxs-lookup"><span data-stu-id="46cd6-140">It should still output "Hello, World!"</span></span>

## <a name="get-your-azure-redis-cache-connection-string"></a><span data-ttu-id="46cd6-141">Abrufen Ihrer Azure Redis Cache-Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="46cd6-141">Get your Azure Redis Cache connection string</span></span>

<span data-ttu-id="46cd6-142">Für die Verbindung mit Ihrem Azure Redis Cache benötigen Sie eine Verbindungszeichenfolge, die Ihr Kennwort und die URL enthält.</span><span class="sxs-lookup"><span data-stu-id="46cd6-142">To connect to your Azure Redis Cache, you need a connection string that contains your password and URL.</span></span> <span data-ttu-id="46cd6-143">Diese Verbindungszeichenfolge ist für **ServiceStack.Redis** eindeutig und wie folgt aufgebaut: `[password]@[host name]:[port]`</span><span class="sxs-lookup"><span data-stu-id="46cd6-143">This connection string is unique to **ServiceStack.Redis** and is in the form of: `[password]@[host name]:[port]`</span></span>

<span data-ttu-id="46cd6-144">Sie können diesen Schlüssel über das Azure-Portal oder über die Befehlszeile abrufen.</span><span class="sxs-lookup"><span data-stu-id="46cd6-144">You can retrieve this key with the Azure portal, or with the command line.</span></span> <span data-ttu-id="46cd6-145">Verwenden Sie hier die Befehlszeile, da Sie dem Ansatz mit dem Portal bereits im Modul **Optimieren Ihrer Webanwendungen durch das Zwischenspeichern von schreibgeschützten Daten mit Redis** gefolgt sind.</span><span class="sxs-lookup"><span data-stu-id="46cd6-145">Let's use the latter here since we used the portal approach in the **Optimize your web applications by caching read-only data with Redis** module.</span></span>

<span data-ttu-id="46cd6-146">Rufen Sie die Zugriffsschlüssel über den Befehl `azure rediscache list-keys` ab.</span><span class="sxs-lookup"><span data-stu-id="46cd6-146">Use the `azure rediscache list-keys` command to get the access keys.</span></span> <span data-ttu-id="46cd6-147">Sie müssen den Namen und die Ressourcengruppe angeben, wie unten dargestellt:</span><span class="sxs-lookup"><span data-stu-id="46cd6-147">You will need to supply the name and resource group as shown below:</span></span>

```azurecli
azure rediscache list-keys \
    --name [name] \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

<span data-ttu-id="46cd6-148">Die Rückgabe sollte dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="46cd6-148">This will return something like</span></span>

```output
Primary Key   : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
Secondary Key : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
```

1. <span data-ttu-id="46cd6-149">Kopieren Sie Ihren **Primärschlüssel** in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="46cd6-149">Copy your **Primary** key to the clipboard.</span></span>

1. <span data-ttu-id="46cd6-150">Der Hostname ist der Name, den Sie dem Cache beim Erstellen mit dem Suffix `.redis.cache.windows.net` gegeben haben.</span><span class="sxs-lookup"><span data-stu-id="46cd6-150">The hostname will be the name you gave to the cache when you created it with the suffix `.redis.cache.windows.net`.</span></span>

1. <span data-ttu-id="46cd6-151">Der Port muss **6379** sein.</span><span class="sxs-lookup"><span data-stu-id="46cd6-151">The port should be **6379**.</span></span>

1. <span data-ttu-id="46cd6-152">Alle diese Informationen können Sie in der Konsole mit dem Befehl `azure rediscache list` überprüfen, der Ihnen alle Redis Cache-Instanzen in Ihrem aktiven Abonnement (in diesem Fall die Azure-Sandbox) anzeigt.</span><span class="sxs-lookup"><span data-stu-id="46cd6-152">You can verify all of that information in the console with the `azure rediscache list` command which will show you all the Redis cache instances in your active subscription (in this case, the Azure Sandbox).</span></span>

## <a name="add-the-connection-string-to-your-app"></a><span data-ttu-id="46cd6-153">Hinzufügen der Verbindungszeichenfolge zu Ihrer App</span><span class="sxs-lookup"><span data-stu-id="46cd6-153">Add the connection string to your app</span></span>

1. <span data-ttu-id="46cd6-154">Stellen Sie sicher, dass Sie sich im App-Ordner befinden.</span><span class="sxs-lookup"><span data-stu-id="46cd6-154">Make sure you are in the app folder.</span></span> <span data-ttu-id="46cd6-155">Die Datei **Program.cs** sollte sich im aktuellen Ordner befinden, wenn Sie `ls` oder `dir` eingeben.</span><span class="sxs-lookup"><span data-stu-id="46cd6-155">The **Program.cs** should be in the current folder if you type `ls` or `dir`.</span></span>

1. <span data-ttu-id="46cd6-156">Öffnen Sie den integrierten Editor, indem Sie `code .` in den App-Ordner eingeben.</span><span class="sxs-lookup"><span data-stu-id="46cd6-156">Open the built-in editor by typing `code .` in the app folder.</span></span>

1. <span data-ttu-id="46cd6-157">Wählen Sie die Quelldatei **Program.cs** aus.</span><span class="sxs-lookup"><span data-stu-id="46cd6-157">Select the **Program.cs** source file.</span></span>

1. <span data-ttu-id="46cd6-158">Erstellen Sie in der `Program`-Klasse das folgende Feld.</span><span class="sxs-lookup"><span data-stu-id="46cd6-158">Create the following field in the `Program` class.</span></span>

    ```csharp
    static string redisConnectionString = "";
    ```

1. <span data-ttu-id="46cd6-159">Fügen Sie Ihre Verbindungszeichenfolge in das Feld **redisConnectionString** ein, das Sie gerade erstellt haben, und verwenden Sie **6379** als Portnummer.</span><span class="sxs-lookup"><span data-stu-id="46cd6-159">Paste in your connection string in the **redisConnectionString** field you just created and use **6379** as your port number.</span></span> <span data-ttu-id="46cd6-160">Denken Sie daran, Ihre Verbindungszeichenfolge in folgendem Format einzugeben: `[password]@[host name]:[port]`</span><span class="sxs-lookup"><span data-stu-id="46cd6-160">Remember, your connection string is in the form of: `[password]@[host name]:[port]`</span></span>

<span data-ttu-id="46cd6-161">Die Verbindungszeichenfolge sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="46cd6-161">An example connection string would look something like this:</span></span>

```output
ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6379
```
    
## <a name="insert-two-data-values-into-your-azure-redis-cache"></a><span data-ttu-id="46cd6-162">Hinzufügen von zwei Datenwerten in Ihrem Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="46cd6-162">Insert two data values into your Azure Redis Cache</span></span>

<span data-ttu-id="46cd6-163">Abschließend werden Sie nun Daten in Ihrem Azure Redis Cache hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="46cd6-163">Finally, we're going to add data into your Azure Redis Cache.</span></span>

1. <span data-ttu-id="46cd6-164">Fügen Sie oben in der Datei **Program.cs** die folgende using-Anweisung ein.</span><span class="sxs-lookup"><span data-stu-id="46cd6-164">Add the following using statement to the top of the **Program.cs** file.</span></span>

    ```csharp
    using ServiceStack.Redis;
    ```

1. <span data-ttu-id="46cd6-165">In der **Main**-Methode fügen Sie dann den folgenden Codeausschnitt hinzu.</span><span class="sxs-lookup"><span data-stu-id="46cd6-165">Add the following snippet of code in your **Main** method.</span></span> <span data-ttu-id="46cd6-166">Dadurch werden zwei Werte übergangsweise hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="46cd6-166">This will add two values transitionally.</span></span>

    ```csharp
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create the transaction
        var transaction = redisClient.CreateTransaction();

        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        var transactionResult = transaction.Commit();

        if(transactionResult)
            Console.WriteLine("Transaction committed");
        else
            Console.WriteLine("Transaction failed to commit");
    }
    ```
1. <span data-ttu-id="46cd6-167">Führen Sie die Anwendung über die Eingabeaufforderung unten im Editor-Fenster aus, und vergewissern Sie sich, dass in der Konsole **Commit für Transaktion ausgeführt** steht.</span><span class="sxs-lookup"><span data-stu-id="46cd6-167">Run the application through the command prompt at the bottom of the editor window and verify that the console says **Transaction committed**.</span></span> 

    ```bash
    dotnet run
    ```
    
## <a name="verify-your-data"></a><span data-ttu-id="46cd6-168">Überprüfen Ihrer Daten</span><span class="sxs-lookup"><span data-stu-id="46cd6-168">Verify your data</span></span>

<span data-ttu-id="46cd6-169">Als letzten Schritt überprüfen Sie, ob sich die von Ihnen hinzugefügten Daten im Azure Redis Cache befinden.</span><span class="sxs-lookup"><span data-stu-id="46cd6-169">To finish off, let's verify that the data we added is in our Azure Redis Cache.</span></span>

1. <span data-ttu-id="46cd6-170">Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="46cd6-170">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="46cd6-171">Suchen Sie Ihren Redis Cache, indem Sie in der linken Randleiste **Alle Ressourcen** auswählen und auf der linken Seite über das Feld zum Filtern Redis Cache-Instanzen auswählen.</span><span class="sxs-lookup"><span data-stu-id="46cd6-171">Locate your Redis cache by selecting **All Resources** in the left-hand sidebar and using the filter box on the left to select Redis Cache instances.</span></span> <span data-ttu-id="46cd6-172">Alternativ können Sie auch oben das Suchfeld verwenden und den Namen des Cache eingeben.</span><span class="sxs-lookup"><span data-stu-id="46cd6-172">Alternatively, you can use the search box at the top and type the name of the cache.</span></span>

1. <span data-ttu-id="46cd6-173">Wählen Sie Ihre Redis Cache-Instanz aus.</span><span class="sxs-lookup"><span data-stu-id="46cd6-173">Select your Redis cache instance.</span></span>

1. <span data-ttu-id="46cd6-174">Wählen Sie im Blatt **Übersicht** für Ihren Redis Cache die Option **Konsole** aus.</span><span class="sxs-lookup"><span data-stu-id="46cd6-174">In the **Overview** blade for your Redis Cache, select **Console**.</span></span> <span data-ttu-id="46cd6-175">Dadurch wird eine Redis-Konsole geöffnet, in der Sie Low-Level-Redis-Befehle eingeben können.</span><span class="sxs-lookup"><span data-stu-id="46cd6-175">This will open a Redis console, which allows you to enter low-level Redis commands.</span></span>

1. <span data-ttu-id="46cd6-176">Geben Sie **get MyKey1** ein.</span><span class="sxs-lookup"><span data-stu-id="46cd6-176">Type **get MyKey1**.</span></span> <span data-ttu-id="46cd6-177">Vergewissern Sie sich, dass der zurückgegebene Wert **MyValue1** ist.</span><span class="sxs-lookup"><span data-stu-id="46cd6-177">Verify that the value returned is **MyValue1**.</span></span>

1. <span data-ttu-id="46cd6-178">Geben Sie **get MyKey2** ein.</span><span class="sxs-lookup"><span data-stu-id="46cd6-178">Type **get MyKey2**.</span></span> <span data-ttu-id="46cd6-179">Vergewissern Sie sich, dass der zurückgegebene Wert **MyValue2** ist.</span><span class="sxs-lookup"><span data-stu-id="46cd6-179">Verify that the value returned is **MyValue2**.</span></span>

    ![Screenshot der Azure Redis-Konsole mit den Werten von „MyKey1“ und „MyKey2“.](../media/4-redis-console.png)