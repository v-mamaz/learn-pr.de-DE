<span data-ttu-id="3159e-101">In dieser Übung erstellen Sie eine Azure Redis Cache-Instanz zum Speichern und Zurückgeben häufig verwendeter Werte.</span><span class="sxs-lookup"><span data-stu-id="3159e-101">In this exercise, you'll create an Azure Redis Cache instance to store and return commonly used values.</span></span>

## <a name="create-a-cache"></a><span data-ttu-id="3159e-102">Erstellen eines Caches</span><span class="sxs-lookup"><span data-stu-id="3159e-102">Create a cache</span></span>

1. <span data-ttu-id="3159e-103">Melden Sie sich beim Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="3159e-103">Sign in to the Azure portal.</span></span> <span data-ttu-id="3159e-104">Klicken Sie dann auf **Ressource erstellen**, **Datenbanken** und **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="3159e-104">Then click **Create a resource**, click **Databases**, and click **Redis Cache**.</span></span>

    <span data-ttu-id="3159e-105">Der folgende Screenshot zeigt den Redis Cache-Speicherort innerhalb der verschiedenen Datenbankressourcen-Optionen im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="3159e-105">The following screenshot shows the Redis Cache location within the various database resource options on the Azure portal.</span></span>

    ![Screenshot mit den Datenbankoptionen des Azure-Portals, wobei die Optionen „Ressource erstellen“, „Datenbank“ und „Redis Cache“ hervorgehoben sind.](../media/4-create-a-cache-1.png)

## <a name="configure-your-cache"></a><span data-ttu-id="3159e-107">Konfigurieren Ihres Caches</span><span class="sxs-lookup"><span data-stu-id="3159e-107">Configure your cache</span></span>

1. <span data-ttu-id="3159e-108">**DNS-Name**: Erstellen Sie einen global eindeutigen Namen, z.B. **ContosoSportsApp1028**.</span><span class="sxs-lookup"><span data-stu-id="3159e-108">**DNS Name:** Create a globally unique name such as **ContosoSportsApp1028**.</span></span>
1. <span data-ttu-id="3159e-109">**Abonnement**: Wählen Sie Ihr Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="3159e-109">**Subscription:** Select your subscription.</span></span>
1. <span data-ttu-id="3159e-110">**Ressourcengruppe**: Erstellen Sie eine neue Ressourcengruppe, und geben Sie ihr einen Namen.</span><span class="sxs-lookup"><span data-stu-id="3159e-110">**Resource group:** Create a new resource group and give it a name.</span></span>
1. <span data-ttu-id="3159e-111">**Speicherort**: Da die meisten Ihrer Kunden sich im Bereich New York befinden, wählen Sie **USA, Osten** aus.</span><span class="sxs-lookup"><span data-stu-id="3159e-111">**Location:** Because most of your customers are in the New York area, you should select **East US**.</span></span>
1. <span data-ttu-id="3159e-112">**Tarif**: Wählen Sie **Basic C0** aus.</span><span class="sxs-lookup"><span data-stu-id="3159e-112">**Pricing tier:** Select **Basic C0**.</span></span>
1. <span data-ttu-id="3159e-113">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="3159e-113">Click **Create**.</span></span>

    <span data-ttu-id="3159e-114">Der folgende Screenshot zeigt eine repräsentative Konfiguration, die zum Erstellen einer neuen Redis Cache-Ressource verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="3159e-114">The following screenshot shows a representative configuration used to create a new Redis Cache resource.</span></span>

    ![Screenshot mit dem Azure-Portal-Blatt beim Erstellen einer neuen Redis Cache-Ressource mit Beispielkonfigurations-DNS-Name, Abonnement, neuer Ressourcengruppe, Speicherort und Tarif.](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> <span data-ttu-id="3159e-116">Bevor Sie fortfahren, müssen Sie warten, bis der Cache bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="3159e-116">You will have to wait until the cache is deployed before continuing.</span></span> <span data-ttu-id="3159e-117">Dieser Vorgang kann eine Weile dauern.</span><span class="sxs-lookup"><span data-stu-id="3159e-117">This process might take some time.</span></span>

## <a name="retrieve-the-access-keys-and-host-name"></a><span data-ttu-id="3159e-118">Abrufen der Zugriffsschlüssel und des Hostnamens</span><span class="sxs-lookup"><span data-stu-id="3159e-118">Retrieve the access keys and host name</span></span>

1. <span data-ttu-id="3159e-119">Navigieren Sie im Azure-Portal zu Ihrem Cache, und wählen Sie **Einstellungen** > **Zugriffsschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="3159e-119">In the Azure portal, browse to your cache and select **Settings** > **Access keys**.</span></span> <span data-ttu-id="3159e-120">Notieren Sie sich die **primäre Verbindungszeichenfolge (StackExchange.Redis)**.</span><span class="sxs-lookup"><span data-stu-id="3159e-120">Write down the **Primary connection string (StackExchange.Redis)**.</span></span>

    <span data-ttu-id="3159e-121">Dieser Schlüssel enthält Ihren Primärschlüssel und Hostnamen in einer vollständigen Verbindungszeichenfolge für die Verwendung in Ihren Anwendungseinstellungen für das StackExchange.Redis-Paket, das wir verwenden.</span><span class="sxs-lookup"><span data-stu-id="3159e-121">This key includes your primary key and host name in a complete connection string for use within your application settings for the StackExchange.Redis package we are using.</span></span>

1. <span data-ttu-id="3159e-122">Starten Sie den Editor oder einen anderen Texteditor auf Ihrem Computer.</span><span class="sxs-lookup"><span data-stu-id="3159e-122">Start Notepad or another text editor on your computer.</span></span>
1. <span data-ttu-id="3159e-123">Fügen Sie folgenden Inhalt hinzu:</span><span class="sxs-lookup"><span data-stu-id="3159e-123">Add the following contents:</span></span>

    <span data-ttu-id="3159e-124">Ersetzen Sie `<connection-string>` durch die primäre Verbindungszeichenfolge Ihres Caches von oben.</span><span class="sxs-lookup"><span data-stu-id="3159e-124">Replace `<connection-string>` with your cache's primary connection string from above.</span></span>

    ```xml
    <appSettings>
        <add key="CacheConnection" value="<connection-string>"/>
    </appSettings>
    ```

1. <span data-ttu-id="3159e-125">Speichern Sie die Datei an einem Ort, an dem sie nicht in den Quellcode Ihrer Beispielanwendung einbezogen wird.</span><span class="sxs-lookup"><span data-stu-id="3159e-125">Save the file in a location where it won't be included within the source code of your sample application.</span></span> <span data-ttu-id="3159e-126">In diesem Tutorial speichern wir die Datei unter `C:\AppSecrets\CacheSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="3159e-126">For this tutorial, we will save the file as `C:\AppSecrets\CacheSecrets.config`.</span></span>

## <a name="create-a-console-app"></a><span data-ttu-id="3159e-127">Erstellen einer Konsolen-App</span><span class="sxs-lookup"><span data-stu-id="3159e-127">Create a console app</span></span>

1. <span data-ttu-id="3159e-128">Starten Sie Visual Studio, und klicken Sie auf das Menüelement **Datei** > **Neu** > **Projekt...**.</span><span class="sxs-lookup"><span data-stu-id="3159e-128">Start Visual Studio and click the **File** > **New** > **Project...** menu item.</span></span>
1. <span data-ttu-id="3159e-129">Wählen Sie die Vorlage **Visual C#** > **Windows Desktop** > **Konsolen-App** aus.</span><span class="sxs-lookup"><span data-stu-id="3159e-129">Select the **Visual C#** > **Windows Desktop** > **Console App** template.</span></span>
1. <span data-ttu-id="3159e-130">Geben Sie Ihrer App einen Namen, und klicken Sie auf **OK**, um eine neue Konsolenanwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="3159e-130">Give your app a name and click **OK** to create a new console application.</span></span>

## <a name="configure-the-cache-client"></a><span data-ttu-id="3159e-131">Konfigurieren des Cacheclients</span><span class="sxs-lookup"><span data-stu-id="3159e-131">Configure the cache client</span></span>

<span data-ttu-id="3159e-132">In diesem Abschnitt konfigurieren Sie die Konsolenanwendung zur Verwendung des **StackExchange.Redis**-Clients für .NET.</span><span class="sxs-lookup"><span data-stu-id="3159e-132">In this section, you will configure the console application to use the **StackExchange.Redis** client for .NET.</span></span>

1. <span data-ttu-id="3159e-133">Klicken Sie in Visual Studio auf **Tools**, zeigen Sie auf **NuGet-Paket-Manager**, klicken Sie auf **Paket-Manager-Konsole**, und führen Sie im Fenster der Paket-Manager-Konsole den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="3159e-133">In Visual Studio, click **Tools**, point to **NuGet Package Manager**, click **Package Manager Console**, and run the following command from the Package Manager Console window:</span></span>

    ```powershell
    Install-Package StackExchange.Redis
    ```

<span data-ttu-id="3159e-134">Nach Abschluss der Installation kann der StackExchange.Redis-Cacheclient für Ihr Projekt verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3159e-134">Once the installation is completed, the StackExchange.Redis cache client is available to use with your project.</span></span>

## <a name="connect-to-the-cache"></a><span data-ttu-id="3159e-135">Herstellen einer Verbindung mit dem Cache</span><span class="sxs-lookup"><span data-stu-id="3159e-135">Connect to the cache</span></span>

1. <span data-ttu-id="3159e-136">Öffnen Sie in Visual Studio die Datei **App.config** im **Projektmappen-Explorer**, und aktualisieren Sie sie, sodass sie ein **appSettings**-Dateiattribut enthält, das auf die Datei **CacheSecrets.config** verweist.</span><span class="sxs-lookup"><span data-stu-id="3159e-136">In Visual Studio, open the **App.config** file within the **Solution Explorer** and update it to include an **appSettings** file attribute that references the **CacheSecrets.config** file.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.1" />
        </startup>

        <appSettings file="C:\AppSecrets\CacheSecrets.config"></appSettings>

    </configuration>
    ```

1. <span data-ttu-id="3159e-137">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Verweise**, und klicken Sie anschließend auf **Verweis hinzufügen...**. Wählen Sie **System.Configuration** in der Liste **Assemblys** > **Framework** aus, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="3159e-137">In Solution Explorer, right-click **References** and click **Add Reference...**. Select **System.Configuration** from the **Assemblies** > **Framework** list and click **OK**.</span></span>

1. <span data-ttu-id="3159e-138">Fügen Sie der Datei **Program.cs** die folgenden `using`-Anweisungen hinzu:</span><span class="sxs-lookup"><span data-stu-id="3159e-138">Add the following `using` statements to **Program.cs**:</span></span>

    ```csharp
    using StackExchange.Redis;
    using System.Configuration;
    ```

<span data-ttu-id="3159e-139">Die Verbindung mit Azure Redis Cache wird von der ConnectionMultiplexer-Klasse verwaltet.</span><span class="sxs-lookup"><span data-stu-id="3159e-139">The connection to Azure Redis Cache is managed by the ConnectionMultiplexer class.</span></span> <span data-ttu-id="3159e-140">Diese Klasse sollte für Ihre gesamte Clientanwendung genutzt und wiederverwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3159e-140">This class should be shared and reused throughout your client application.</span></span> <span data-ttu-id="3159e-141">Erstellen Sie nicht für jeden Vorgang eine neue Verbindung.</span><span class="sxs-lookup"><span data-stu-id="3159e-141">Do not create a new connection for each operation.</span></span>

<span data-ttu-id="3159e-142">Speichern Sie niemals Anmeldeinformationen im Quellcode.</span><span class="sxs-lookup"><span data-stu-id="3159e-142">Never store credentials in source code.</span></span> <span data-ttu-id="3159e-143">Hier wird nur eine externe Konfigurationsdatei für Geheimnisse verwendet, um dieses Beispiel einfach zu halten.</span><span class="sxs-lookup"><span data-stu-id="3159e-143">To keep this sample simple, we're only using an external secrets config file.</span></span> <span data-ttu-id="3159e-144">Ein besserer Ansatz wäre die Nutzung von Azure Key Vault mit Zertifikaten.</span><span class="sxs-lookup"><span data-stu-id="3159e-144">A better approach would be to use Azure Key Vault with certificates.</span></span>

1. <span data-ttu-id="3159e-145">Fügen Sie in der Datei **Program.cs** der Program-Klasse Ihrer Konsolenanwendung die folgenden Member hinzu:</span><span class="sxs-lookup"><span data-stu-id="3159e-145">In **Program.cs**, add the following members to the Program class of your console application:</span></span>

    ```csharp
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

<span data-ttu-id="3159e-146">Bei diesem Ansatz zum Freigeben einer ConnectionMultiplexer-Instanz in Ihrer Anwendung wird eine statische Eigenschaft verwendet, die eine verbundene Instanz zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="3159e-146">This approach to sharing a ConnectionMultiplexer instance in your application uses a static property that returns a connected instance.</span></span> <span data-ttu-id="3159e-147">Dieser Code ist eine threadsichere Möglichkeit, um nur eine einzelne verbundene ConnectionMultiplexer-Instanz zu initialisieren.</span><span class="sxs-lookup"><span data-stu-id="3159e-147">The code provides a thread-safe way to initialize only a single connected ConnectionMultiplexer instance.</span></span> <span data-ttu-id="3159e-148">**abortConnect** ist auf „false“ festgelegt. Dies bedeutet, dass der Aufruf erfolgreich ist, auch wenn keine Verbindung mit Azure Redis Cache hergestellt wird.</span><span class="sxs-lookup"><span data-stu-id="3159e-148">**abortConnect** is set to false, which means that the call succeeds even if a connection to Azure Redis Cache is not established.</span></span> <span data-ttu-id="3159e-149">Eine wichtige Funktion von ConnectionMultiplexer ist, dass die Verbindung mit dem Cache automatisch wiederhergestellt wird, sobald das Netzwerkproblem oder andere Ursachen beseitigt wurden.</span><span class="sxs-lookup"><span data-stu-id="3159e-149">One key feature of ConnectionMultiplexer is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

<span data-ttu-id="3159e-150">Der Wert der appSetting-Einstellung **CacheConnection** wird verwendet, um über das Azure-Portal auf die Cacheverbindungszeichenfolge als Kennwortparameter zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="3159e-150">The value of the **CacheConnection** appSetting value is used to reference the cache connection string from the Azure portal as the password parameter.</span></span>
