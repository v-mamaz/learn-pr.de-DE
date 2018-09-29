<span data-ttu-id="d8e0b-101">Zunächst erstellen Sie eine Instanz von Azure Redis Cache und dann eine einfache Transaktion, die zwei Datenwerte in den Cache einfügt.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-101">Let's start by creating an instance of Azure Redis Cache, and then create a simple transaction that inserts two data values into the cache.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="d8e0b-102">Erstellen einer Azure Redis Cache-Instanz</span><span class="sxs-lookup"><span data-stu-id="d8e0b-102">Create an Azure Redis Cache</span></span>

<span data-ttu-id="d8e0b-103">Sie beginnen mit der Erstellung eines Azure Redis Cache über die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-103">Let's start by creating an Azure Redis Cache with the Azure CLI.</span></span> <span data-ttu-id="d8e0b-104">Verwenden Sie Cloud Shell auf der rechten Seite des Browserfensters, um mit Azure zu interagieren.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-104">Use the Cloud Shell on the right side of the browser window to interact with Azure.</span></span>

<span data-ttu-id="d8e0b-105">Verwenden Sie den Befehl `az redis create`, um einen neuen Azure Redis Cache zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-105">We'll use the `az redis create` command to create a new Azure Redis Cache.</span></span> <span data-ttu-id="d8e0b-106">Es werden mehrere Parameter benötigt.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-106">It takes several parameters.</span></span> <span data-ttu-id="d8e0b-107">An dieser Stelle sind die gängigsten aufgeführt (eine vollständige Liste finden Sie in der Dokumentation).</span><span class="sxs-lookup"><span data-stu-id="d8e0b-107">Here are the most common (to get a full list, check the documentation).</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="d8e0b-108">Parameter</span><span class="sxs-lookup"><span data-stu-id="d8e0b-108">Parameter</span></span> | <span data-ttu-id="d8e0b-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d8e0b-109">Description</span></span> |
> |-----------|-------------|
> | `--name`    | <span data-ttu-id="d8e0b-110">Der Cachename muss global eindeutig sein und aus Buchstaben, Zahlen und Bindestrichen bestehen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-110">The name of the cache - this must be globally unique and composed of letters, numbers, and dashes.</span></span> |
> | `--resource-group` | <span data-ttu-id="d8e0b-111">Verwenden Sie die vorab erstellte Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**, die zur Azure-Sandbox gehört.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-111">Use the pre-created Resource Group **<rgn>[sandbox resource group name]</rgn>**, which is part of the Azure sandbox.</span></span> |
> | `--location` | <span data-ttu-id="d8e0b-112">Geben Sie den Ort an, an dem sich der Cache befinden soll.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-112">Specify the location where the cache should be located.</span></span> <span data-ttu-id="d8e0b-113">Normalerweise würden Sie wahrscheinlich einen Standort in der Nähe der Datenconsumer wählen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-113">Normally, you will want to choose a location close to the data consumers.</span></span> <span data-ttu-id="d8e0b-114">In diesem Fall sind Sie auf die in der Azure-Sandbox verfügbaren Standorte beschränkt.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-114">In this case, you are limited to the locations available in the Azure sandbox.</span></span> <span data-ttu-id="d8e0b-115">Wählen Sie den Standort aus, der Ihnen am nächsten liegt.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-115">Select the closest one to you.</span></span> |
> | `--size` | <span data-ttu-id="d8e0b-116">Die Größe der Azure Redis Cache-Instanz.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-116">The size of the Azure Redis Cache.</span></span> <span data-ttu-id="d8e0b-117">Gültige Werte sind [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4].</span><span class="sxs-lookup"><span data-stu-id="d8e0b-117">Valid values are [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4].</span></span> |
> | `--sku` | <span data-ttu-id="d8e0b-118">Die Azure Redis Cache SKU.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-118">The Azure Redis Cache SKU.</span></span> <span data-ttu-id="d8e0b-119">Gültige Werte sind [Basic, Standard, Premium].</span><span class="sxs-lookup"><span data-stu-id="d8e0b-119">Valid values are [Basic, Standard, Premium].</span></span> |

### <a name="select-a-location"></a><span data-ttu-id="d8e0b-120">Auswählen eines Standorts</span><span class="sxs-lookup"><span data-stu-id="d8e0b-120">Select a location</span></span>
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="d8e0b-121">Erstellen Sie einen Cache mit den folgenden Optionen:</span><span class="sxs-lookup"><span data-stu-id="d8e0b-121">Create a cache using the following options:</span></span>
    - <span data-ttu-id="d8e0b-122">Größe: C0</span><span class="sxs-lookup"><span data-stu-id="d8e0b-122">Size: C0</span></span>
    - <span data-ttu-id="d8e0b-123">SKU: Basic</span><span class="sxs-lookup"><span data-stu-id="d8e0b-123">SKU: Basic</span></span>

1. <span data-ttu-id="d8e0b-124">Hier ein Beispiel einer Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-124">Here's an example command line.</span></span> <span data-ttu-id="d8e0b-125">Ersetzen Sie unbedingt den Parameter `[name]` durch einen eindeutigen Namen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-125">Make sure to replace the `[name]` parameter with a unique name.</span></span> <span data-ttu-id="d8e0b-126">Sie können den Standort ersetzen, wenn Sie eine andere Region als USA, Osten wünschen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-126">You can replace the location if you want a different region than East US.</span></span>

    ```azurecli
    REDIS_NAME=[name]

    az redis create \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --location eastus \
        --vm-size C0 \
        --sku Basic \
    ```

## <a name="create-a-net-core-console-application"></a><span data-ttu-id="d8e0b-127">Erstellen einer .NET Core-Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="d8e0b-127">Create a .NET Core console application</span></span>

<span data-ttu-id="d8e0b-128">Als Nächstes erstellen Sie eine .NET Core-Konsolenanwendung, mit der Sie Datenwerte in Ihre Azure Redis Cache-Instanz einfügen können.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-128">Next, create a .NET Core console application, which will be used to insert data values into our Azure Redis Cache.</span></span>

1. <span data-ttu-id="d8e0b-129">Erstellen Sie mithilfe der integrierten Cloud Shell auf der rechten Fensterseite eine neue .NET Core-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-129">Create a new .NET Core application using the integrated Cloud Shell on the right hand side of the window.</span></span> <span data-ttu-id="d8e0b-130">Nennen Sie sie „RedisData“.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-130">Name it "RedisData".</span></span>

    ```bash
    cd ~
    dotnet new console --name RedisData
    ```

1. <span data-ttu-id="d8e0b-131">Wechseln Sie in das neue Verzeichnis, das für Ihre App erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-131">Change into the new directory created for your app.</span></span>

    ```bash
    cd RedisData
    ```

1. <span data-ttu-id="d8e0b-132">Kompilieren Sie die Anwendung, und führen Sie sie aus. Sie sollten „Hello, World!“ als Ausgabe erhalten.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-132">Build and run the application - it should output "Hello World!"</span></span>

    ```bash
    dotnet run
    ```

## <a name="add-the-servicestackredis-nuget-package"></a><span data-ttu-id="d8e0b-133">Hinzufügen des NuGet-Pakets „ServiceStack.Redis“</span><span class="sxs-lookup"><span data-stu-id="d8e0b-133">Add the ServiceStack.Redis NuGet package</span></span>

<span data-ttu-id="d8e0b-134">Nachdem nun die Konsolenanwendung fertig erstellt ist, können Sie das NuGet-Paket **ServiceStack.Redis** hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-134">Now that we have our console application, we need to add the **ServiceStack.Redis** NuGet package.</span></span> <span data-ttu-id="d8e0b-135">Dies ermöglicht Ihnen, eine Verbindung mit der Azure Redis Cache-Instanz herzustellen und Befehle in C# aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-135">This will allow us to connect to the Azure Redis Cache and issue commands in C#.</span></span>

1. <span data-ttu-id="d8e0b-136">Fügen Sie das NuGet-Paket **ServiceStack.Redis** mithilfe der Terminalshell hinzu.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-136">Add the NuGet package **ServiceStack.Redis** using the terminal shell.</span></span>

    ```bash
    dotnet add package ServiceStack.Redis
    ```

1. <span data-ttu-id="d8e0b-137">Kompilieren und starten Sie die Anwendung erneut, um sicherzustellen, dass alles vollständig kompiliert ist.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-137">Build and run the application again to make sure it all compiles.</span></span> <span data-ttu-id="d8e0b-138">Wie zuvor sollte die Ausgabe „Hello, World!“ lauten.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-138">It should still output "Hello World!"</span></span>

## <a name="get-your-azure-redis-cache-connection-string"></a><span data-ttu-id="d8e0b-139">Abrufen Ihrer Azure Redis Cache-Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="d8e0b-139">Get your Azure Redis Cache connection string</span></span>

<span data-ttu-id="d8e0b-140">Für die Verbindung mit Ihrer Azure Redis Cache-Instanz benötigen Sie eine Verbindungszeichenfolge, die Ihr Kennwort und die URL enthält.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-140">To connect to your Azure Redis Cache, you need a connection string that contains your password and URL.</span></span> <span data-ttu-id="d8e0b-141">**ServiceStack.Redis** hat ein eigenes Format für Verbindungszeichenfolgen: `[password]@[hostname]:[sslport]?ssl=true`.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-141">**ServiceStack.Redis** has its own connection string format: `[password]@[hostname]:[sslport]?ssl=true`.</span></span>

<span data-ttu-id="d8e0b-142">Sie können Ihr Kennwort über das Azure-Portal oder die Befehlszeile abrufen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-142">You can retrieve your password with the Azure portal, or with the command line.</span></span> <span data-ttu-id="d8e0b-143">Verwenden Sie hier die Befehlszeile, da Sie dem Ansatz mit dem Portal bereits im Modul „Optimieren Ihrer Webanwendungen durch das Zwischenspeichern von schreibgeschützten Daten mit Redis“ gefolgt sind.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-143">Let's use the latter here, since we used the portal approach in the "Optimize your web applications by caching read-only data with Redis" module.</span></span>

<span data-ttu-id="d8e0b-144">Rufen Sie die Zugriffsschlüssel über den Befehl `az redis list-keys` ab.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-144">Use the `az redis list-keys` command to get the access keys.</span></span> <span data-ttu-id="d8e0b-145">Führen Sie diese Befehle aus, um den Primärschlüssel abzurufen, ihn in einer Variablen namens `REDIS_KEY` zu speichern und anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="d8e0b-145">Run these commands to get the primary key, store it in a variable called `REDIS_KEY`, and display it:</span></span>

```azurecli
REDIS_KEY=$(az redis list-keys \
    --name "$REDIS_NAME" \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query primaryKey \
    --output tsv)

echo $REDIS_KEY
```

<span data-ttu-id="d8e0b-146">Führen Sie anschließend diesen Befehl aus, um die Verbindungszeichenfolge zusammenzusetzen und in der Befehlszeile anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-146">Next, run this command to put the connection string together and display it on the command line.</span></span> <span data-ttu-id="d8e0b-147">Beachten Sie, dass der Hostname der Name des Cache ist, gefolgt von `.redis.cache.windows.net`. Der Port ist **6380**, der Standard-SSL-Port von Redis.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-147">Note that the hostname is the name of the cache followed by `.redis.cache.windows.net`, and the port is **6380**, the default Redis SSL port.</span></span>

```bash
echo "$REDIS_KEY"@"$REDIS_NAME".redis.cache.windows.net:6380?ssl=true
```

<span data-ttu-id="d8e0b-148">Kopieren Sie die Verbindungszeichenfolge in die Zwischenablage. Sie verwenden sie im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-148">Copy the connection string to the clipboard &mdash; you'll be using it in the next step.</span></span>

## <a name="add-the-connection-string-to-your-app"></a><span data-ttu-id="d8e0b-149">Hinzufügen der Verbindungszeichenfolge zu Ihrer App</span><span class="sxs-lookup"><span data-stu-id="d8e0b-149">Add the connection string to your app</span></span>

1. <span data-ttu-id="d8e0b-150">Öffnen Sie den Cloud Shell-Editor im Anwendungsordner.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-150">Open the Cloud Shell editor from the application folder.</span></span>

    ```bash
    cd ~/RedisData
    code .
    ```

1. <span data-ttu-id="d8e0b-151">Wählen Sie die Quelldatei **Program.cs** aus.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-151">Select the **Program.cs** source file.</span></span>

1. <span data-ttu-id="d8e0b-152">Erstellen Sie das folgende Feld in der `Program`-Klasse, und fügen Sie Ihre Verbindungszeichenfolge als Wert ein.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-152">Create the following field in the `Program` class and paste in your connection string as the value.</span></span>

    ```csharp
    static string redisConnectionString = "<connection string>";
    ```

    <span data-ttu-id="d8e0b-153">Ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d8e0b-153">Here's an example:</span></span>

    ```csharp
    static string redisConnectionString = "ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6380?ssl=true";
    ```

## <a name="insert-two-data-values-into-your-azure-redis-cache"></a><span data-ttu-id="d8e0b-154">Einfügen von zwei Datenwerten in Ihre Azure Redis Cache-Instanz</span><span class="sxs-lookup"><span data-stu-id="d8e0b-154">Insert two data values into your Azure Redis Cache</span></span>

<span data-ttu-id="d8e0b-155">Abschließend werden Sie Ihrer Azure Redis Cache-Instanz nun Daten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-155">Finally, we're going to add data into your Azure Redis Cache.</span></span>

1. <span data-ttu-id="d8e0b-156">Fügen Sie am Anfang der Datei **Program.cs** die folgende `using`-Anweisung hinzu.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-156">Add the following `using` statement to the top of the **Program.cs** file.</span></span>

    ```csharp
    using ServiceStack.Redis;
    ```

1. <span data-ttu-id="d8e0b-157">Ersetzen Sie den Inhalt der `Main`-Methode durch den nachstehenden Code.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-157">Replace the contents of the `Main` method with the following code.</span></span> <span data-ttu-id="d8e0b-158">Hierbei wird eine Transaktion verwendet, um zwei Werte hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-158">This will use a transaction to add two values.</span></span>

    ```csharp
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    if (transactionResult)
    {
        Console.WriteLine("Transaction committed");
    }
    else
    {
        Console.WriteLine("Transaction failed to commit");
    }
    ```

1. <span data-ttu-id="d8e0b-159">Bevor Sie die Anwendung kompilieren und ausführen, stellen Sie sicher, dass der Redis-Cache vollständig bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-159">Before building and running the application, check to make sure that the Redis cache has been fully provisioned.</span></span> <span data-ttu-id="d8e0b-160">Nach Abschluss von `az redis create` kann dies manchmal einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-160">It can sometimes take a few minutes after `az redis create` completes.</span></span> <span data-ttu-id="d8e0b-161">Führen Sie den folgenden Befehl aus, um den Status zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-161">Run the following command to check the status.</span></span>

    ```azcli
    az redis show \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --query provisioningState
    ```

    <span data-ttu-id="d8e0b-162">Wenn der Status `Creating` ist, versuchen Sie es in ein paar Minuten noch einmal.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-162">If the status is `Creating`, try checking again in a couple of minutes.</span></span> <span data-ttu-id="d8e0b-163">Nach Abschluss wird `Succeeded` angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-163">It will show `Succeeded` when finished.</span></span>

1. <span data-ttu-id="d8e0b-164">Führen Sie die Anwendung aus, und bestätigen Sie, dass in der Konsole **Commit für Transaktion ausgeführt** ausgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-164">Run the application and verify that the console says **Transaction committed**.</span></span>

    ```bash
    dotnet run
    ```

## <a name="verify-your-data"></a><span data-ttu-id="d8e0b-165">Überprüfen Ihrer Daten</span><span class="sxs-lookup"><span data-stu-id="d8e0b-165">Verify your data</span></span>

<span data-ttu-id="d8e0b-166">Als letzten Schritt überprüfen Sie, ob sich die von Ihnen hinzugefügten Daten in Ihrer Azure Redis Cache-Instanz befinden.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-166">To finish off, let's verify that the data we added is in our Azure Redis Cache.</span></span>

1. <span data-ttu-id="d8e0b-167">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-167">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="d8e0b-168">Suchen Sie Ihre Azure Redis Cache-Instanz, indem Sie auf der linken Randleiste auf **Alle Ressourcen** klicken und über das Filterfeld auf der linken Seite Azure Redis Cache-Instanzen auswählen.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-168">Locate your Azure Redis Cache by selecting **All Resources** in the left-hand sidebar, and using the filter box on the left to select Azure Redis Cache instances.</span></span> <span data-ttu-id="d8e0b-169">Alternativ können Sie auch oben das Suchfeld verwenden und den Namen des Cache eingeben.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-169">Alternatively, you can use the search box at the top, and type the name of the cache.</span></span>

1. <span data-ttu-id="d8e0b-170">Wählen Sie Ihre Azure Redis Cache-Instanz aus.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-170">Select your Azure Redis Cache instance.</span></span>

1. <span data-ttu-id="d8e0b-171">Wählen Sie im Blatt **Übersicht** für Ihre Azure Redis Cache-Instanz die Option **Konsole** aus.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-171">In the **Overview** blade for your Azure Redis Cache, select **Console**.</span></span> <span data-ttu-id="d8e0b-172">Dadurch wird eine Azure Redis Cache-Konsole geöffnet, in der Sie detaillierte Azure Redis Cache-Befehle eingeben können.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-172">This will open an Azure Redis Cache console, which allows you to enter low-level Azure Redis Cache commands.</span></span>

1. <span data-ttu-id="d8e0b-173">Geben Sie **get MyKey1** ein.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-173">Type **get MyKey1**.</span></span> <span data-ttu-id="d8e0b-174">Vergewissern Sie sich, dass der zurückgegebene Wert **MyValue1** ist.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-174">Verify that the value returned is **MyValue1**.</span></span>

1. <span data-ttu-id="d8e0b-175">Geben Sie **get MyKey2** ein.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-175">Type **get MyKey2**.</span></span> <span data-ttu-id="d8e0b-176">Vergewissern Sie sich, dass der zurückgegebene Wert **MyValue2** ist.</span><span class="sxs-lookup"><span data-stu-id="d8e0b-176">Verify that the value returned is **MyValue2**.</span></span>

    ![Screenshot der Azure Redis Cache-Konsole mit den Werten von „MyKey1“ und „MyKey2“.](../media/4-redis-console.png)