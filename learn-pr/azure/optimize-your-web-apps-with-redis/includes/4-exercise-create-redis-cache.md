<span data-ttu-id="35441-101">Erstellen wir jetzt eine Azure Redis Cache-Instanz zum Speichern und Zurückgeben häufig verwendeter Werte.</span><span class="sxs-lookup"><span data-stu-id="35441-101">Let's create an Azure Redis Cache instance to store and return commonly used values.</span></span>

<!-- TODO: do we need to activate the sandbox here? -->

## <a name="create-a-redis-cache-in-azure"></a><span data-ttu-id="35441-102">Erstellen einer Redis Cache-Instanz in Azure</span><span class="sxs-lookup"><span data-stu-id="35441-102">Create a Redis cache in Azure</span></span>

1. <span data-ttu-id="35441-103">Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="35441-103">Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="35441-104">Klicken Sie dann auf **Ressource erstellen**, **Datenbanken** und **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="35441-104">Click **Create a resource**, click **Databases**, and click **Redis Cache**.</span></span>

    <span data-ttu-id="35441-105">Der folgende Screenshot zeigt den Redis Cache-Standort innerhalb der verschiedenen Optionen für Datenbankressourcen im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="35441-105">The following screenshot shows the Redis Cache location within the various database resource options on the Azure portal.</span></span>

    ![Screenshot mit den Datenbankoptionen im Azure-Portal, mit hervorgehobenen Optionen „Ressource erstellen“, „Datenbank“ und „Redis Cache“](../media/4-create-a-cache-1.png)

### <a name="identify-the-location-for-the-cache"></a><span data-ttu-id="35441-107">Ermitteln des Standorts für den Cache</span><span class="sxs-lookup"><span data-stu-id="35441-107">Identify the location for the cache</span></span>

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="configure-your-cache"></a><span data-ttu-id="35441-108">Konfigurieren Ihres Caches</span><span class="sxs-lookup"><span data-stu-id="35441-108">Configure your cache</span></span>

<span data-ttu-id="35441-109">Legen Sie die folgenden Einstellungen für den Cache fest.</span><span class="sxs-lookup"><span data-stu-id="35441-109">Apply the following settings on the cache.</span></span>

1. <span data-ttu-id="35441-110">**DNS-Name**: Erstellen Sie einen global eindeutigen Namen, z.B. **ContosoSportsApp1028**.</span><span class="sxs-lookup"><span data-stu-id="35441-110">**DNS Name:** Create a globally unique name such as **ContosoSportsApp1028**.</span></span>

1. <span data-ttu-id="35441-111">**Abonnement**: Wählen Sie das Azure Sandbox-Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="35441-111">**Subscription:** Select the Azure Sandbox subscription.</span></span>

1. <span data-ttu-id="35441-112">**Ressourcengruppe**: Wählen Sie <rgn>[Name der Sandbox-Ressourcengruppe]</rgn> als Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="35441-112">**Resource group:** Select <rgn>[Sandbox resource group name]</rgn> for the Resource Group.</span></span>

1. <span data-ttu-id="35441-113">**Standort**: Normalerweise würden Sie einen Standort in der Nähe Ihres Kunden auswählen, in diesem Fall „East Coast“.</span><span class="sxs-lookup"><span data-stu-id="35441-113">**Location:** Normally, you would select a location near your customers - in this case, the East Coast.</span></span> <span data-ttu-id="35441-114">Für Azure Sandbox können jedoch nur bestimmte Regionen für Ressourcen ausgewählt werden, wie oben angegeben.</span><span class="sxs-lookup"><span data-stu-id="35441-114">However, the Azure Sandbox only allows specific regions to be selected for resources as noted above.</span></span> <span data-ttu-id="35441-115">Wählen Sie einen dieser Standorte aus.</span><span class="sxs-lookup"><span data-stu-id="35441-115">Please select one of those locations.</span></span>

1. <span data-ttu-id="35441-116">**Tarif**: Wählen Sie **Basic C0** aus.</span><span class="sxs-lookup"><span data-stu-id="35441-116">**Pricing tier:** Select **Basic C0**.</span></span> <span data-ttu-id="35441-117">Dies ist der niedrigste Tarif, der verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="35441-117">This is the lowest tier you can use.</span></span> <span data-ttu-id="35441-118">Für Produktions-Apps werden wahrscheinlich größere Datenmengen und einige der Premium-Features benötigt, z.B. das Clustering. Hierfür wäre die Auswahl eines höheren Tarifs erforderlich.</span><span class="sxs-lookup"><span data-stu-id="35441-118">Production apps would likely want to store more data and utilize some of the Premium features such as clustering which would require a higher tier selection.</span></span>

1. <span data-ttu-id="35441-119">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="35441-119">Click **Create**.</span></span>

    <span data-ttu-id="35441-120">Der folgende Screenshot zeigt eine repräsentative Konfiguration, die zum Erstellen einer neuen Redis Cache-Ressource verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="35441-120">The following screenshot shows a representative configuration used to create a new Redis Cache resource.</span></span> <span data-ttu-id="35441-121">Beachten Sie, dass Ihre Konfiguration aufgrund von Azure Sandbox leicht abweicht.</span><span class="sxs-lookup"><span data-stu-id="35441-121">Note that yours will be slightly different due to the Azure Sandbox.</span></span>

    ![Screenshot mit dem Azure-Portal-Blatt beim Erstellen einer neuen Redis Cache-Ressource mit DNS-Name, Abonnement, neuer Ressourcengruppe, Speicherort und Tarif der Beispielkonfiguration](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> <span data-ttu-id="35441-123">Warten Sie, bis der Cache bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="35441-123">You will have to wait until the cache is deployed before continuing.</span></span> <span data-ttu-id="35441-124">Dieser Vorgang kann eine Weile dauern.</span><span class="sxs-lookup"><span data-stu-id="35441-124">This process might take some time.</span></span>

## <a name="retrieve-the-access-keys-and-host-name"></a><span data-ttu-id="35441-125">Abrufen der Zugriffsschlüssel und des Hostnamens</span><span class="sxs-lookup"><span data-stu-id="35441-125">Retrieve the access keys and host name</span></span>

1. <span data-ttu-id="35441-126">Navigieren Sie im Azure-Portal zu Ihrer neuen Redis Cache-Instanz, und wählen Sie **Einstellungen** > **Zugriffsschlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="35441-126">Navigate to your new cache instance in the Azure portal and select **Settings** > **Access keys**.</span></span> 

1. <span data-ttu-id="35441-127">Kopieren Sie die **Primäre Verbindungszeichenfolge (StackExchange.Redis)** an einen sicheren Ort. Sie benötigen sie für die nächste Übung.</span><span class="sxs-lookup"><span data-stu-id="35441-127">Copy the **Primary connection string (StackExchange.Redis)** to a safe place, you will need it for the next exercise.</span></span>

    <span data-ttu-id="35441-128">Dieser Schlüssel enthält Ihren Primärschlüssel und Hostnamen in einer vollständigen Verbindungszeichenfolge für die Verwendung in Ihren Anwendungseinstellungen für das **StackExchange.Redis**-Paket, das wir verwenden.</span><span class="sxs-lookup"><span data-stu-id="35441-128">This key includes your primary key and host name in a complete connection string for use within your application settings for the **StackExchange.Redis** package we are going to use.</span></span>

<span data-ttu-id="35441-129">Als Nächstes lernen Sie einige der Befehle zum Abfragen des Caches kennen.</span><span class="sxs-lookup"><span data-stu-id="35441-129">Next, let's learn about some of the commands we can use to interrogate the cache.</span></span>