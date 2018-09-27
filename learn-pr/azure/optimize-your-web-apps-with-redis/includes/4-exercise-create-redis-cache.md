<span data-ttu-id="90b61-101">Erstellen wir jetzt eine Azure Redis Cache-Instanz zum Speichern und Zurückgeben häufig verwendeter Werte.</span><span class="sxs-lookup"><span data-stu-id="90b61-101">Let's create an Azure Redis Cache instance to store and return commonly used values.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-redis-cache-in-azure"></a><span data-ttu-id="90b61-102">Erstellen einer Redis Cache-Instanz in Azure</span><span class="sxs-lookup"><span data-stu-id="90b61-102">Create a Redis cache in Azure</span></span>

1. <span data-ttu-id="90b61-103">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="90b61-103">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="90b61-104">Klicken Sie dann auf **Ressource erstellen**, **Datenbanken** und **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="90b61-104">Click **Create a resource**, click **Databases**, and click **Redis Cache**.</span></span>

    <span data-ttu-id="90b61-105">Der folgende Screenshot zeigt den Redis Cache-Standort innerhalb der verschiedenen Optionen für Datenbankressourcen im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="90b61-105">The following screenshot shows the Redis Cache location within the various database resource options on the Azure portal.</span></span>

    ![Screenshot mit den Datenbankoptionen des Azure-Portals, wobei die Optionen „Ressource erstellen“, „Datenbank“ und „Redis Cache“ hervorgehoben sind.](../media/4-create-a-cache-1.png)

### <a name="configure-your-cache"></a><span data-ttu-id="90b61-107">Konfigurieren Ihres Caches</span><span class="sxs-lookup"><span data-stu-id="90b61-107">Configure your cache</span></span>

<span data-ttu-id="90b61-108">Legen Sie die folgenden Einstellungen für den Cache fest.</span><span class="sxs-lookup"><span data-stu-id="90b61-108">Apply the following settings on the cache.</span></span>

1. <span data-ttu-id="90b61-109">**DNS-Name:** Erstellen Sie einen global eindeutigen Namen wie z.B. **ContosoSportsApp[nnn]**, wobei `[nnn]` durch zufällige Zahlen ersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="90b61-109">**DNS Name:** Create a globally unique name such as **ContosoSportsApp[nnn]**, where `[nnn]` is replaced with random numbers.</span></span>

1. <span data-ttu-id="90b61-110">**Abonnement:** Wählen Sie das Concierge-Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="90b61-110">**Subscription:** Select the Concierge subscription.</span></span>

1. <span data-ttu-id="90b61-111">**Ressourcengruppe:** Wählen Sie <rgn>[Name der Sandboxressourcengruppe]</rgn> als Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="90b61-111">**Resource group:** Select <rgn>[sandbox resource group name]</rgn> for the Resource Group.</span></span>

1. <span data-ttu-id="90b61-112">**Standort:** Normalerweise würden Sie einen Standort in der Nähe Ihres Kunden auswählen, in diesem Fall „East Coast“.</span><span class="sxs-lookup"><span data-stu-id="90b61-112">**Location:** Normally, you would select a location near your customers - in this case, the East Coast.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-note-friendly.md)]

5. <span data-ttu-id="90b61-113">**Tarif:** Wählen Sie **Basic C0** aus.</span><span class="sxs-lookup"><span data-stu-id="90b61-113">**Pricing tier:** Select **Basic C0**.</span></span> <span data-ttu-id="90b61-114">Dies ist der niedrigste Tarif, der verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="90b61-114">This is the lowest tier you can use.</span></span> <span data-ttu-id="90b61-115">Für Produktions-Apps werden wahrscheinlich größere Datenmengen und einige der Premium-Features benötigt, z.B. das Clustering. Hierfür wäre die Auswahl eines höheren Tarifs erforderlich.</span><span class="sxs-lookup"><span data-stu-id="90b61-115">Production apps would likely want to store more data and utilize some of the Premium features such as clustering which would require a higher tier selection.</span></span>

1. <span data-ttu-id="90b61-116">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="90b61-116">Click **Create**.</span></span> <span data-ttu-id="90b61-117">Azure erstellt die Redis Cache-Instanz und stellt sie Ihnen bereit.</span><span class="sxs-lookup"><span data-stu-id="90b61-117">Azure will create and deploy the Redis Cache instance for you.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="90b61-118">Normalerweise wird die Redis-Cache-Ressource sehr schnell erstellt und im Azure-Portal angezeigt, aber der Cache selbst ist erst nach einigen Minuten verfügbar.</span><span class="sxs-lookup"><span data-stu-id="90b61-118">Usually, the Redis cache resource will be created and viewable in the Azure portal very quickly, but the cache itself will not be available for a few minutes.</span></span> <span data-ttu-id="90b61-119">Die nächsten Schritte zeigen, wie der Status des Caches überprüft wird.</span><span class="sxs-lookup"><span data-stu-id="90b61-119">The next steps show how to check the status of your cache.</span></span>

## <a name="verify-your-data"></a><span data-ttu-id="90b61-120">Überprüfen Ihrer Daten</span><span class="sxs-lookup"><span data-stu-id="90b61-120">Verify your data</span></span>

<span data-ttu-id="90b61-121">Über die **Konsole** im Azure-Portal können Sie Befehle für Ihre Redis Cache-Instanz ausführen, nachdem diese erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="90b61-121">You can use the **Console** feature in the Azure portal to issue commands to your Redis cache instance after it has been created.</span></span>

1. <span data-ttu-id="90b61-122">Suchen Sie Ihren Redis Cache nach Abschluss der Bereitstellung mithilfe des Popups **Benachrichtigung** oder indem Sie auf der linken Randleiste auf **Alle Ressourcen** klicken und über das Filterfeld auf der linken Seite Redis Cache-Instanzen auswählen.</span><span class="sxs-lookup"><span data-stu-id="90b61-122">Locate your Redis cache through the **Notification** popup when it finishes deployment, or by selecting **All Resources** in the left-hand sidebar and using the filter box on the left to select Redis Cache instances.</span></span> <span data-ttu-id="90b61-123">Alternativ können Sie auch oben das Suchfeld verwenden und den Namen des Cache eingeben.</span><span class="sxs-lookup"><span data-stu-id="90b61-123">Alternatively, you can use the search box at the top and type the name of the cache.</span></span>

1. <span data-ttu-id="90b61-124">Wählen Sie Ihre Redis Cache-Instanz aus.</span><span class="sxs-lookup"><span data-stu-id="90b61-124">Select your Redis cache instance.</span></span>

1. <span data-ttu-id="90b61-125">Überprüfen Sie den Wert des Felds „Status“.</span><span class="sxs-lookup"><span data-stu-id="90b61-125">Check the value of the "Status" field.</span></span> <span data-ttu-id="90b61-126">Der Cache ist erst aktiv, wenn der Status „Wird ausgeführt“ lautet.</span><span class="sxs-lookup"><span data-stu-id="90b61-126">The cache is not ready until the status is "Running".</span></span> <span data-ttu-id="90b61-127">Sie müssen ggf. einige Minuten warten, ehe Sie fortfahren können.</span><span class="sxs-lookup"><span data-stu-id="90b61-127">You might have to wait for a few minutes before proceeding.</span></span>

1. <span data-ttu-id="90b61-128">Sobald der Cache aktiviert ist, klicken Sie auf der Symbolleiste auf dem Blatt **Übersicht** für Ihre Redis Cache-Instanz auf die Schaltfläche `>_ Console`.</span><span class="sxs-lookup"><span data-stu-id="90b61-128">Once the cache is running, Click the `>_ Console` button in the toolbar on the **Overview** blade for your Redis Cache.</span></span> <span data-ttu-id="90b61-129">Dadurch wird eine Redis-Konsole geöffnet, in der Sie detaillierte Redis-Befehle eingeben können.</span><span class="sxs-lookup"><span data-stu-id="90b61-129">This will open a Redis console, which allows you to enter low-level Redis commands.</span></span> <span data-ttu-id="90b61-130">Versuchen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="90b61-130">Try some of the following:</span></span>

    ```console
    ping
    ```

    ```output
    PONG
    ```

    ```console
    set test one
    ```

    ```output
    OK
    ```

    ```console
    get test
    ```

    ```output
    "one"
    ```

<span data-ttu-id="90b61-131">Kehren Sie zum Panel **Übersicht** zurück. Verwenden Sie dazu entweder die Breadcrumb-Leiste im oberen Bereich, oder verschieben Sie die Ansicht mithilfe der Scrollleiste wieder nach links.</span><span class="sxs-lookup"><span data-stu-id="90b61-131">Switch back to the **Overview** panel either through the breadcrumb bar on the top, or use the scrollbar to slide the view back to the left.</span></span>

## <a name="retrieve-the-access-keys-and-host-name"></a><span data-ttu-id="90b61-132">Abrufen der Zugriffsschlüssel und des Hostnamens</span><span class="sxs-lookup"><span data-stu-id="90b61-132">Retrieve the access keys and host name</span></span>

1. <span data-ttu-id="90b61-133">Klicken Sie auf **Einstellungen** > **Zugriffsschlüssel**.</span><span class="sxs-lookup"><span data-stu-id="90b61-133">Select **Settings** > **Access keys**.</span></span>

1. <span data-ttu-id="90b61-134">Kopieren Sie die **Primäre Verbindungszeichenfolge (StackExchange.Redis)** an einen sicheren Ort. Sie benötigen sie für die nächste Übung.</span><span class="sxs-lookup"><span data-stu-id="90b61-134">Copy the **Primary connection string (StackExchange.Redis)** to a safe place, you will need it for the next exercise.</span></span>

    <span data-ttu-id="90b61-135">Dieser Schlüssel enthält Ihren Primärschlüssel und Hostnamen in einer vollständigen Verbindungszeichenfolge für die Verwendung in Ihren Anwendungseinstellungen für das **StackExchange.Redis**-Paket, das wir verwenden.</span><span class="sxs-lookup"><span data-stu-id="90b61-135">This key includes your primary key and host name in a complete connection string for use within your application settings for the **StackExchange.Redis** package we are going to use.</span></span>

<span data-ttu-id="90b61-136">Als Nächstes lernen Sie einige der Befehle zum Abfragen des Caches kennen.</span><span class="sxs-lookup"><span data-stu-id="90b61-136">Next, let's learn about some of the commands we can use to interrogate the cache.</span></span>