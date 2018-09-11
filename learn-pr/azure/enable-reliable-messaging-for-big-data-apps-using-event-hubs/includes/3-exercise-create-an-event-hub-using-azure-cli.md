<span data-ttu-id="1a139-101">Sie können nun einen neuen Event Hub erstellen.</span><span class="sxs-lookup"><span data-stu-id="1a139-101">You're now ready to create a new event hub.</span></span> <span data-ttu-id="1a139-102">Nachdem der Event Hub erstellt wurde, verwenden Sie das Azure-Portal, um Ihren neuen Hub anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="1a139-102">After creating the event hub, you'll use the Azure portal to view your new hub.</span></span>

<span data-ttu-id="1a139-103">Erstellen Sie einen Event Hub mit Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1a139-103">You'll create an event hub using the Azure CLI.</span></span> <span data-ttu-id="1a139-104">Verwenden Sie für diese Übung Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="1a139-104">For this exercise, use the Azure CLI 2.0.</span></span> 

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="1a139-105">Erstellen eines Event Hubs-Namespace</span><span class="sxs-lookup"><span data-stu-id="1a139-105">Create an Event Hubs namespace</span></span>

<span data-ttu-id="1a139-106">Mit den folgenden Schritten können Sie einen Event Hubs-Namespace mithilfe der von Azure Cloud Shell unterstützten Bash-Shell erstellen.</span><span class="sxs-lookup"><span data-stu-id="1a139-106">Use the following steps to create an Event Hubs namespace using Bash shell supported by Azure Cloud shell:</span></span>

1. <span data-ttu-id="1a139-107">Melden Sie sich bei Cloud Shell (Bash) an.</span><span class="sxs-lookup"><span data-stu-id="1a139-107">Sign in to the Cloud Shell (Bash).</span></span>  

1. <span data-ttu-id="1a139-108">Erstellen Sie mithilfe des folgenden Befehls eine Azure-Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="1a139-108">Create an Azure resource group using the following command:</span></span>

    ```azurecli
        az group create --name <resource group name> --location <location>
    ```

    |<span data-ttu-id="1a139-109">Parameter</span><span class="sxs-lookup"><span data-stu-id="1a139-109">Parameter</span></span>      |<span data-ttu-id="1a139-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a139-110">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="1a139-111">--name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-111">--name (required)</span></span>      |<span data-ttu-id="1a139-112">Geben Sie einen neuen Namen für die Ressourcengruppe ein.</span><span class="sxs-lookup"><span data-stu-id="1a139-112">Enter a new resource group name.</span></span>|
    |<span data-ttu-id="1a139-113">--location (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-113">--location (required)</span></span>     |<span data-ttu-id="1a139-114">Geben Sie den Standort Ihres nächsten Azure-Rechenzentrums an, z.B. „westus“.</span><span class="sxs-lookup"><span data-stu-id="1a139-114">Enter the location of your nearest Azure datacenter, for example, westus.</span></span>|

1. <span data-ttu-id="1a139-115">Erstellen Sie mit dem folgenden Befehl den Event Hubs-Namespace:</span><span class="sxs-lookup"><span data-stu-id="1a139-115">Create the Event Hubs namespace using the following command:</span></span>

    ```azurecli
        az eventhubs namespace create --name <Event Hubs namespace name> --resource-group <resource group name> -l <location>
    ```

    |<span data-ttu-id="1a139-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="1a139-116">Parameter</span></span>      |<span data-ttu-id="1a139-117">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a139-117">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="1a139-118">--name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-118">--name (required)</span></span>      |<span data-ttu-id="1a139-119">Geben Sie Ihrem Event Hubs-Namespace einen eindeutigen Namen, der zwischen 6 und 50 Zeichen lang ist.</span><span class="sxs-lookup"><span data-stu-id="1a139-119">Enter a 6-50 characters-long unique name for your Event Hubs namespace.</span></span> <span data-ttu-id="1a139-120">Der Name darf nur Buchstaben, Zahlen und Bindestriche enthalten.</span><span class="sxs-lookup"><span data-stu-id="1a139-120">The name should contain only letters, numbers, and hyphens.</span></span> <span data-ttu-id="1a139-121">Er muss zudem mit einem Buchstaben beginnen und mit einem Buchstaben oder einer Zahl enden.</span><span class="sxs-lookup"><span data-stu-id="1a139-121">It should start with a letter and end with a letter or number.</span></span>|
    |<span data-ttu-id="1a139-122">--resource-group (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-122">--resource-group (required)</span></span>  |<span data-ttu-id="1a139-123">Geben Sie die Ressourcengruppe ein, die Sie in Schritt 1 erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1a139-123">Enter the resource group you created in step 1.</span></span>
    |<span data-ttu-id="1a139-124">--l (optional)</span><span class="sxs-lookup"><span data-stu-id="1a139-124">--l (optional)</span></span>     |<span data-ttu-id="1a139-125">Geben Sie den Standort Ihres nächsten Azure-Rechenzentrums an, z.B. „westus“.</span><span class="sxs-lookup"><span data-stu-id="1a139-125">Enter the location of your nearest Azure datacenter, for example, westus.</span></span>|

1. <span data-ttu-id="1a139-126">Rufen Sie die Verbindungszeichenfolge für Ihren Event Hubs-Namespace mithilfe des folgenden Befehls ab.</span><span class="sxs-lookup"><span data-stu-id="1a139-126">Fetch the connection string for your Event Hubs namespace using the following command.</span></span> <span data-ttu-id="1a139-127">Sie benötigen diese, wenn Sie Anwendungen zum Senden und Empfangen von Nachrichten über Ihren Event Hub konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="1a139-127">You'll need this to configure applications to send and receive messages using your event hub.</span></span>

    ```azurecli
        az eventhubs namespace authorization-rule keys list --resource-group <resource group name> --namespace-name <EventHub namespace name> --name RootManageSharedAccessKey
    ```

    |<span data-ttu-id="1a139-128">Parameter</span><span class="sxs-lookup"><span data-stu-id="1a139-128">Parameter</span></span>      |<span data-ttu-id="1a139-129">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a139-129">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="1a139-130">--resource-group (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-130">--resource-group (required)</span></span>  |<span data-ttu-id="1a139-131">Geben Sie die Ressourcengruppe ein, die Sie in Schritt 1 erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1a139-131">Enter the resource group you created in step 1.</span></span>|
    |<span data-ttu-id="1a139-132">--namespace-name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-132">--namespace-name (required)</span></span>      |<span data-ttu-id="1a139-133">Geben Sie den Namespace ein, den Sie in Schritt 2 erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1a139-133">Enter the namespace you created in step 2.</span></span>|

    <span data-ttu-id="1a139-134">Dieser Befehl gibt die Verbindungszeichenfolge für Ihren Event Hubs-Namespace zurück, den Sie später zum Konfigurieren Ihrer Herausgeber- und Consumeranwendungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="1a139-134">This command returns the connection string for your Event Hubs namespace that you'll use later to configure your publisher and consumer applications.</span></span> <span data-ttu-id="1a139-135">Speichern Sie den Wert der folgenden Schlüssel für den späteren Gebrauch.</span><span class="sxs-lookup"><span data-stu-id="1a139-135">Save the value of the following keys for later use.</span></span>

    - <span data-ttu-id="1a139-136">**primaryConnectionString**</span><span class="sxs-lookup"><span data-stu-id="1a139-136">**primaryConnectionString**</span></span>
    - <span data-ttu-id="1a139-137">**primaryKey**</span><span class="sxs-lookup"><span data-stu-id="1a139-137">**primaryKey**</span></span>

## <a name="create-an-event-hub"></a><span data-ttu-id="1a139-138">Erstellen eines Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1a139-138">Create an event hub</span></span>

<span data-ttu-id="1a139-139">Führen Sie die folgenden Schritte aus, um Ihren neuen Event Hub zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="1a139-139">Use the following steps to create your new event hub:</span></span>

1. <span data-ttu-id="1a139-140">Erstellen Sie einen neuen Event Hub über den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="1a139-140">Create a new event hub using the following command:</span></span>

    ```azurecli
        az eventhubs eventhub create --name <event hub name> --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name>
    ```

    |<span data-ttu-id="1a139-141">Parameter</span><span class="sxs-lookup"><span data-stu-id="1a139-141">Parameter</span></span>      |<span data-ttu-id="1a139-142">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a139-142">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="1a139-143">--name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-143">--name (required)</span></span>  |<span data-ttu-id="1a139-144">Geben Sie einen Namen für Ihren Event Hub ein.</span><span class="sxs-lookup"><span data-stu-id="1a139-144">Enter a name for your event hub.</span></span>|
    |<span data-ttu-id="1a139-145">--resource-group (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-145">--resource-group (required)</span></span>  |<span data-ttu-id="1a139-146">Geben Sie die Ressourcengruppe ein, die Sie im vorherigen Abschnitt erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1a139-146">Enter the resource group you created in the previous procedure.</span></span>|
    |<span data-ttu-id="1a139-147">--namespace-name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-147">--namespace-name (required)</span></span>      |<span data-ttu-id="1a139-148">Geben Sie den Namespace ein, den Sie im vorherigen Abschnitt erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1a139-148">Enter the namespace you created in the previous procedure.</span></span>|

1. <span data-ttu-id="1a139-149">Zeigen Sie über folgenden Befehl die Informationen Ihres Event Hubs an:</span><span class="sxs-lookup"><span data-stu-id="1a139-149">View the details of your event hub using the following command:</span></span> 

    ```azurecli
        az eventhubs eventhub show --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name> --name <event hub name>
    ```

    |<span data-ttu-id="1a139-150">Parameter</span><span class="sxs-lookup"><span data-stu-id="1a139-150">Parameter</span></span>      |<span data-ttu-id="1a139-151">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a139-151">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="1a139-152">--resource-group (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-152">--resource-group (required)</span></span>  |<span data-ttu-id="1a139-153">Geben Sie die Ressourcengruppe ein, die Sie im vorherigen Abschnitt erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1a139-153">Enter the resource group that you created in the previous procedure.</span></span>|
    |<span data-ttu-id="1a139-154">--namespace-name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-154">--namespace-name (required)</span></span>      |<span data-ttu-id="1a139-155">Geben Sie den Namespace ein, den Sie im vorherigen Abschnitt erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1a139-155">Enter the namespace you created in the previous procedure.</span></span>|
    |<span data-ttu-id="1a139-156">--name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="1a139-156">--name  (required)</span></span>|<span data-ttu-id="1a139-157">Geben Sie den Namen des Event Hubs ein, den Sie in Schritt 1 erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="1a139-157">Enter the name of the event hub you created in step 1.</span></span>|

## <a name="view-the-event-hub-in-the-azure-portal"></a><span data-ttu-id="1a139-158">Anzeigen des Event Hubs im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="1a139-158">View the event hub in the Azure portal</span></span>

<span data-ttu-id="1a139-159">Befolgen Sie diese Schritte, um Ihren Event Hub im Azure-Portal anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="1a139-159">Use the following steps view your event hub in the Azure portal.</span></span>

1. <span data-ttu-id="1a139-160">Suchen Sie über die Suchleiste am oberen Rand des [Azure-Portals](https://portal.azure.com?azure-portal=true) nach Ihrem Event Hubs-Namespace.</span><span class="sxs-lookup"><span data-stu-id="1a139-160">Find your Event Hubs namespace using the Search bar at the top of the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="1a139-161">Klicken Sie auf den Namespace, um ihn zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="1a139-161">Click your namespace to open it.</span></span>

1. <span data-ttu-id="1a139-162">Klicken Sie auf den **Event Hubs-Namespace** > **ENTITÄTEN** und dann auf **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="1a139-162">From **Event Hubs Namespace** > **ENTITIES**, click **Event Hubs**.</span></span>
    <span data-ttu-id="1a139-163">Ihr Event Hub wird mit dem Zustand **Aktiv** angezeigt sowie mit den Standardwerten für die **Nachrichtenaufbewahrung** (*7*) und der **Anzahl der Partitionen** (*4*).</span><span class="sxs-lookup"><span data-stu-id="1a139-163">Your event hub displays with a status of **Active**, and default values for **Message Retention** (*7*) and **Partition Count** of (*4*).</span></span>

    ![Event Hub, der im Azure-Portal angezeigt wird](../media-draft/3-event-hub.png)

## <a name="summary"></a><span data-ttu-id="1a139-165">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="1a139-165">Summary</span></span>

<span data-ttu-id="1a139-166">Sie haben nun einen neuen Event Hub erstellt. Sie verfügen über alle erforderlichen Informationen zum Konfigurieren Ihrer Herausgeber- und Consumeranwendungen.</span><span class="sxs-lookup"><span data-stu-id="1a139-166">You've now created a new event hub, and you've all the necessary information ready to configure your publisher and consumer applications.</span></span>
