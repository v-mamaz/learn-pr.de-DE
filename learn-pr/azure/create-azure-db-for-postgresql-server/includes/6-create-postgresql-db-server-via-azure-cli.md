<span data-ttu-id="7e378-101">Sie entscheiden sich für die Erstellung einer Azure Database for PostgreSQL-Instanz, um Routen zu speichern, die durch Fitnessgeräte von Läufern erfasst wurden.</span><span class="sxs-lookup"><span data-stu-id="7e378-101">You decide to create an Azure Database for PostgreSQL to store routes captured from runners' fitness devices.</span></span> <span data-ttu-id="7e378-102">Aufgrund des Verlaufs der Erfassung von Datenvolumes wissen Sie, dass für Ihren Serverspeicher mindestens 20 GB benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="7e378-102">Based on historic captured data volumes, you know your server storage requirements should be set at 20 GB.</span></span> <span data-ttu-id="7e378-103">Zur Unterstützung Ihrer Verarbeitungsanforderungen ist die Unterstützung von Compute Gen 5 mit einem virtuellen Kern erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7e378-103">To support your processing requirements, you need compute Gen 5 support with 1 vCore.</span></span> <span data-ttu-id="7e378-104">Außerdem wissen Sie, dass für Datensicherungen eine Aufbewahrungsdauer von 15 Tagen erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="7e378-104">You also know that you require a retention period of 15 days for data backups.</span></span>

> [!TIP]
> <span data-ttu-id="7e378-105">Alle Übungen in Microsoft Learn sind kostenlos. Wenn Sie jedoch eigenständig weitere Funktionen nutzen möchten, benötigen Sie ein Azure-Abonnement.</span><span class="sxs-lookup"><span data-stu-id="7e378-105">All of the exercises you do in Microsoft Learn are free, but once you start exploring on your own, you will need an Azure subscription.</span></span> <span data-ttu-id="7e378-106">Wenn Sie noch nicht über ein Abonnement verfügen, können Sie in wenigen Minuten ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen.</span><span class="sxs-lookup"><span data-stu-id="7e378-106">If you don't have one yet, take a couple of minutes and create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="7e378-107">Legen wir los.</span><span class="sxs-lookup"><span data-stu-id="7e378-107">Let's begin.</span></span>

<span data-ttu-id="7e378-108">Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="7e378-108">Sign in to [the Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

<span data-ttu-id="7e378-109">Zur Erinnerung: Sie müssen eine Azure Cloud Shell-Sitzung starten.</span><span class="sxs-lookup"><span data-stu-id="7e378-109">Recall that you'll need to start an Azure Cloud Shell session.</span></span> <span data-ttu-id="7e378-110">Klicken Sie auf das Cloud Shell-Symbol am oberen Bildschirmrand, um die Sitzung zu starten.</span><span class="sxs-lookup"><span data-stu-id="7e378-110">Select the Cloud Shell icon at the top of the screen to start the session.</span></span>

![Cloud Shell-Schaltfläche](../media-draft/cloud-shell-button.png)

<span data-ttu-id="7e378-112">Wenn Sie noch nicht über ein Speicherkonto für die Verwendung mit Cloud Shell verfügen, müssen Sie beim ersten Zugriff eines erstellen.</span><span class="sxs-lookup"><span data-stu-id="7e378-112">If you don't already have a storage account to use with Cloud Shell, you'll need to create one with first access.</span></span> <span data-ttu-id="7e378-113">Die Portaloberfläche führt Sie Schritt für Schritt durch die Speicherkontoerstellung.</span><span class="sxs-lookup"><span data-stu-id="7e378-113">The portal interface will step you through the process of creating a storage account.</span></span>

<span data-ttu-id="7e378-114">In diesem Lab wird `bash` als Befehlszeilenumgebung verwendet.</span><span class="sxs-lookup"><span data-stu-id="7e378-114">This lab uses `bash` as the command-line environment.</span></span>

1. <span data-ttu-id="7e378-115">Wählen Sie das Abonnement aus, das Sie zum Erstellen des Servers verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="7e378-115">Select the subscription you'll use to create the server.</span></span>

    <span data-ttu-id="7e378-116">Wenn Sie über mehrere Abonnements verfügen, verwenden Sie den folgenden Befehl, um das richtige Abonnement zu aktivieren. Ersetzen Sie dabei die Nullen durch Ihre Abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="7e378-116">If you have several subscriptions, make sure you activate the appropriate subscription with the following command, replacing the zeros with your subscription identifier.</span></span>

    ``` bash
    az account set --subscription "00000000-0000-0000-0000-000000000000"
    ```

    <span data-ttu-id="7e378-117">Zur Erinnerung: Mithilfe des Befehls `az account list --output table` können Sie alle Ihre Abonnements auflisten.</span><span class="sxs-lookup"><span data-stu-id="7e378-117">Recall, you can list all your subscriptions using the `az account list --output table` command.</span></span> <span data-ttu-id="7e378-118">Wählen Sie die gewünschte Abonnement-ID aus dieser Liste aus.</span><span class="sxs-lookup"><span data-stu-id="7e378-118">Pick the subscription identifier from this list that you'd like to use.</span></span>

1. <span data-ttu-id="7e378-119">Erstellen Sie eine Ressourcengruppe, sofern Sie nicht bereits eine in einer vorherigen Einheit erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="7e378-119">If you haven't already done so in a previous unit, create a resource group.</span></span> <span data-ttu-id="7e378-120">Führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="7e378-120">You'll run the following command.</span></span>

    ```bash
    az group create --name <resource_group_name> --location <location>
    ```

    > [!Note]
    > <span data-ttu-id="7e378-121">Mithilfe des Befehls `az account list-locations` können Sie eine Liste mit allen Standorten abrufen.</span><span class="sxs-lookup"><span data-stu-id="7e378-121">You can retrieve a list of all locations using this command `az account list-locations`.</span></span> <span data-ttu-id="7e378-122">Verwenden Sie den Wert `displayName` oder `name` für den Parameter `<location>`.</span><span class="sxs-lookup"><span data-stu-id="7e378-122">Select the `displayName` or `name` value and use it for the `<location>` parameter.</span></span>

1. <span data-ttu-id="7e378-123">Nun können Sie den Befehl `az postgres server create` ausführen.</span><span class="sxs-lookup"><span data-stu-id="7e378-123">You're now ready to run the `az postgres server create` command.</span></span>

    <span data-ttu-id="7e378-124">Denken Sie daran, dass Sie die Speichergröße des Servers auf 20 GB festlegen, Compute Gen 5-Unterstützung mit einem virtuellen Kern konfigurieren und für Datensicherungen eine Aufbewahrungsdauer von 15 Tagen festlegen möchten.</span><span class="sxs-lookup"><span data-stu-id="7e378-124">Keep in mind you want to set your server storage size at 20 GB, compute Gen 5 support with 1 vCore and a retention period of 15 days for data backups.</span></span>

    <span data-ttu-id="7e378-125">Dazu geben Sie mehrere Parameter an:</span><span class="sxs-lookup"><span data-stu-id="7e378-125">There are several parameters that you'll specify:</span></span>

    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`

    <span data-ttu-id="7e378-126">Versuchen Sie, den Befehl und die Parameter zu erstellen, ohne sich die weiter unten bereitgestellte Lösung anzusehen.</span><span class="sxs-lookup"><span data-stu-id="7e378-126">See if you can write the command and complete the parameters without looking at the solution below.</span></span> <span data-ttu-id="7e378-127">Ersetzen Sie die Werte in `<>` durch Ihre eigenen Werte.</span><span class="sxs-lookup"><span data-stu-id="7e378-127">Replace the values in `<>` with your own values.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7e378-128">Mithilfe des Befehls `az account list-locations` können Sie eine Liste mit allen Standorten abrufen.</span><span class="sxs-lookup"><span data-stu-id="7e378-128">You can retrieve a list of all locations using this command `az account list-locations`.</span></span> <span data-ttu-id="7e378-129">Verwenden Sie den Wert `displayName` oder `name` für den Parameter `<location>`.</span><span class="sxs-lookup"><span data-stu-id="7e378-129">Select the `displayName` or `name` value and use it for the `<location>` parameter.</span></span>

    ```bash
    az postgres server create --resource-group <resource_group_name> --name <unique_server_name>  --location "UK West" --admin-user <server_admin_login_id> --admin-password <server_admin_password> --sku-name B_Gen5_1 --storage-size 20480 --backup-retention 15 --version 10
    ```

<span data-ttu-id="7e378-130">Die Verarbeitung der Informationen dauert einen Moment.</span><span class="sxs-lookup"><span data-stu-id="7e378-130">You'll see the system take a few moments to process the information when executed.</span></span> <span data-ttu-id="7e378-131">Wenn der Server erstellt wurde, wird eine JSON-Zeichenfolge (Java Script Object Notation) zurückgegeben, die den Server beschreibt.</span><span class="sxs-lookup"><span data-stu-id="7e378-131">A Java Script Object Notation (JSON) string that describes the server is returned if the server was created.</span></span> <span data-ttu-id="7e378-132">Wurde der Server nicht erstellt, wird eine Fehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7e378-132">An error message is displayed if the server isn't created.</span></span> <span data-ttu-id="7e378-133">Anhand der Fehlerinformationen können Sie Ihre Befehlsparameter überprüfen und korrigieren.</span><span class="sxs-lookup"><span data-stu-id="7e378-133">You'll use this error information to review and fix your command parameters.</span></span>

<span data-ttu-id="7e378-134">Sie haben erfolgreich einen PostgreSQL-Server mithilfe der Azure-Befehlszeilenschnittstelle erstellt.</span><span class="sxs-lookup"><span data-stu-id="7e378-134">You've successfully created a PostgreSQL server using the Azure CLI.</span></span> <span data-ttu-id="7e378-135">In der nächsten Einheit erfahren Sie, wie Sie die Sicherheitseinstellungen Ihres Servers konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="7e378-135">In the next unit, you'll see how to configure your server's security settings.</span></span>
