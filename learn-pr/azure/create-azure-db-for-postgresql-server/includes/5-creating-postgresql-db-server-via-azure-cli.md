<span data-ttu-id="fdfde-101">Angenommen, Sie arbeiten mit einer lokalen PostgreSQL-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="fdfde-101">Let's assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="fdfde-102">Ihr Unternehmen plant jetzt, die Geräteunterstützung, Verfügbarkeit, Datennachverfolgung und Verarbeitungsfunktionen zu erweitern, indem Ihr Server nach Azure verschoben wird.</span><span class="sxs-lookup"><span data-stu-id="fdfde-102">Your company is now looking at expanding device support, availability, data tracking, and processing features by moving your server into Azure.</span></span> <span data-ttu-id="fdfde-103">Sie untersuchen, wie hoch der Aufwand für das Automatisieren der Erstellung einer Azure Database for PostgreSQL-Instanz ist.</span><span class="sxs-lookup"><span data-stu-id="fdfde-103">You'll investigate how much effort it takes to automate the creation of an Azure Database for PostgreSQL.</span></span>

<span data-ttu-id="fdfde-104">Das Erstellen eines einzelnen Azure Database for PostgreSQL-Servers mit dem Azure-Portal ist einfach.</span><span class="sxs-lookup"><span data-stu-id="fdfde-104">Creating a single Azure Database for PostgreSQL server using the Azure portal is easy.</span></span> <span data-ttu-id="fdfde-105">Das Erstellen von mehr als einer Datenbank und das Durchführen der laufenden Wartung ausschließlich mit dem Portal kann aber mühsam werden.</span><span class="sxs-lookup"><span data-stu-id="fdfde-105">Creating more than one database and running ongoing maintenance using only the portal may become tedious.</span></span> <span data-ttu-id="fdfde-106">Sie verwenden die Azure CLI, um Skripts zu erstellen, wenn Sie Verwaltungsaufgaben automatisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="fdfde-106">You'll use the Azure CLI to create scripts when you want to automate management tasks.</span></span>

<span data-ttu-id="fdfde-107">Die Erstellung nahezu aller Ressourcen in Microsoft Azure kann per Azure CLI automatisiert werden.</span><span class="sxs-lookup"><span data-stu-id="fdfde-107">Creating almost any resource within Microsoft Azure can be automated using the Azure CLI.</span></span> <span data-ttu-id="fdfde-108">In dieser Einheit erfahren Sie, wie Sie die Verwaltung Ihrer Azure Database for PostgreSQL-Server mit der Azure CLI automatisieren.</span><span class="sxs-lookup"><span data-stu-id="fdfde-108">In this unit, you'll learn how to automate management of your Azure Database for PostgreSQL servers using the Azure CLI.</span></span>

## <a name="what-is-azure-cli"></a><span data-ttu-id="fdfde-109">Was ist die Azure CLI?</span><span class="sxs-lookup"><span data-stu-id="fdfde-109">What is Azure CLI?</span></span>

<span data-ttu-id="fdfde-110">Die [Azure CLI](https://docs.microsoft.com/cli/azure/) (Azure-Befehlszeilenschnittstelle) ist die plattformübergreifende Befehlszeilenumgebung von Microsoft zum Verwalten von Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="fdfde-110">[Azure CLI](https://docs.microsoft.com/cli/azure/) is Microsoft’s cross-platform command-line environment for managing Azure resources.</span></span> <span data-ttu-id="fdfde-111">Sie können die Azure CLI in Ihrem Browser per Azure Cloud Shell verwenden oder die Azure CLI unter Mac OS X, Linux oder Windows lokal installieren.</span><span class="sxs-lookup"><span data-stu-id="fdfde-111">You can use the Azure CLI from your browser with Azure Cloud Shell, or you can install Azure CLI locally on Mac OS X, Linux, or Windows.</span></span> <span data-ttu-id="fdfde-112">Die Azure CLI wird mit Bash oder PowerShell über eine lokale Befehlszeile ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="fdfde-112">The Azure CLI is run from a local command line using bash or Powershell.</span></span> <span data-ttu-id="fdfde-113">Für die lokale Ausführung der Azure CLI ist aber ein zusätzliches Setup erforderlich.</span><span class="sxs-lookup"><span data-stu-id="fdfde-113">Running Azure CLI locally however requires additional setup.</span></span> <span data-ttu-id="fdfde-114">Wir verwenden Azure Cloud Shell, um Azure CLI-Befehle auszuführen.</span><span class="sxs-lookup"><span data-stu-id="fdfde-114">We'll use the Azure Cloud Shell for executing Azure CLI commands.</span></span>

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="fdfde-115">Was ist Azure Cloud Shell?</span><span class="sxs-lookup"><span data-stu-id="fdfde-115">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="fdfde-116">Azure Cloud Shell ist eine browserbasierte Shell, die in der Cloud gehostet wird und es Ihnen ermöglicht, über eine authentifizierte Sitzung eine Verbindung mit Azure herzustellen.</span><span class="sxs-lookup"><span data-stu-id="fdfde-116">Azure Cloud Shell is a browser-based shell experience that is hosted in the cloud and allows you to connect to Azure using an authenticated session.</span></span> <span data-ttu-id="fdfde-117">Sie können Azure CLI-Befehle ausführen, um die Verwaltung einer Azure Database for PostgreSQL-Instanz zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="fdfde-117">You can execute Azure CLI commands to automate the management of an Azure Database for PostgreSQL.</span></span> <span data-ttu-id="fdfde-118">Allgemeine Azure CLI-Tools sind in Cloud Shell vorinstalliert und für die Verwendung mit Ihrem Konto konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="fdfde-118">Common Azure CLI tools are pre-installed and configured in Cloud Shell for you to use with your account.</span></span>

> [!NOTE]
> <span data-ttu-id="fdfde-119">Für Cloud Shell ist eine Azure-Speicherressource erforderlich, damit Sie bei der Arbeit in Cloud Shell die erstellten Dateien aufbewahren können.</span><span class="sxs-lookup"><span data-stu-id="fdfde-119">Cloud Shell requires an Azure storage resource to persist any files you create while working in the Cloud Shell.</span></span> <span data-ttu-id="fdfde-120">Beim ersten Start werden Sie von Cloud Shell darauf hingewiesen, dass für Sie eine Ressourcengruppe, ein Speicherkonto und eine Azure Files-Freigabe erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="fdfde-120">On first launch Cloud Shell prompts to create a resource group, storage account, and Azure Files share on your behalf.</span></span> <span data-ttu-id="fdfde-121">Dieser Schritt ist nur einmal erforderlich. Die Komponenten werden für alle zukünftigen Cloud Shell-Sitzungen automatisch angefügt.</span><span class="sxs-lookup"><span data-stu-id="fdfde-121">This is a one-time step and will be automatically attached for all future Cloud Shell sessions.</span></span>

## <a name="create-an-azure-database-for-postgresql-server-using-azure-cli"></a><span data-ttu-id="fdfde-122">Erstellen eines Azure Database for PostgreSQL-Servers mit der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fdfde-122">Create an Azure Database for PostgreSQL server using Azure CLI</span></span>

<span data-ttu-id="fdfde-123">Sie verwenden Azure Cloud Shell, um einen Azure Database for PostgreSQL-Server über die Azure CLI zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="fdfde-123">You'll use Azure Cloud Shell to create an Azure Database for PostgreSQL server using Azure CLI.</span></span> <span data-ttu-id="fdfde-124">Wir sehen uns diese Schritte nun an.</span><span class="sxs-lookup"><span data-stu-id="fdfde-124">Let's look at the steps you'll take.</span></span>

<span data-ttu-id="fdfde-125">Melden Sie sich zuerst am Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="fdfde-125">First, sign into the Azure portal.</span></span>

<span data-ttu-id="fdfde-126">Öffnen Sie Cloud Shell über das Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="fdfde-126">Open the Cloud Shell from the Azure portal.</span></span> <span data-ttu-id="fdfde-127">Öffnen Sie Ihren Browser, und navigieren Sie zum [Azure-Portal](https://portal.azure.com?azure-portal=true). Klicken Sie auf die Schaltfläche zum Öffnen von Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="fdfde-127">Open your browser and go to [Azure portal](https://portal.azure.com?azure-portal=true) and click the Open Cloud Shell button:</span></span>

![Schaltfläche „Cloud Shell“](../media-draft/cloud-shell-button.png)

<span data-ttu-id="fdfde-129">Cloud Shell ermöglicht es Ihnen, Ihre Befehle entweder in `bash` oder `PowerShell` auszuführen.</span><span class="sxs-lookup"><span data-stu-id="fdfde-129">Cloud Shell allows you to run your commands either in `bash` or `PowerShell`.</span></span> <span data-ttu-id="fdfde-130">Wir verwenden für alle Beispiele die Befehlszeilenoption `bash`.</span><span class="sxs-lookup"><span data-stu-id="fdfde-130">We'll use the `bash` command-line option for all examples.</span></span>

<span data-ttu-id="fdfde-131">Wenn Sie über mehrere Abonnements verfügen, sollten Sie sicherstellen, dass Sie mit dem folgenden Befehl das richtige Abonnement aktivieren. Ersetzen Sie die Nullen durch Ihre Abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="fdfde-131">If you have several subscriptions, make sure you activate the appropriate subscription with the following command, replacing the zeros with your subscription identifier.</span></span>

   ```bash
   az account set --subscription 00000000-0000-0000-0000-000000000000
   ```

<span data-ttu-id="fdfde-132">Sie führen den folgenden Befehl aus, um alle Abonnements aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="fdfde-132">You'll run the following command to list all your subscriptions.</span></span>

   ```bash
   az account list --output table
   ```

<span data-ttu-id="fdfde-133">Der nächste Schritt ist das Erstellen einer Ressourcengruppe zum Verwalten des Servers und das Angeben des Speicherorts für die Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="fdfde-133">The next step is to create a resource group to manage the server and where the resource group will be located.</span></span> <span data-ttu-id="fdfde-134">Sie werden sich sicherlich erinnern, dass Sie eine Ressourcengruppe verwenden, um alle Ressourcen im Zusammenhang mit dem Server zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="fdfde-134">Recall, you'll use a resource group to manage all the resources related to your server.</span></span> <span data-ttu-id="fdfde-135">Mit der Option für den Ort (location) können Sie angeben, wo der Server physisch erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="fdfde-135">The location option allows you to specify where the server is created physically.</span></span> <span data-ttu-id="fdfde-136">Sie führen den nächsten Befehl aus und ersetzen `<resource_group_name>` bzw. `<location>` durch die passenden Werte.</span><span class="sxs-lookup"><span data-stu-id="fdfde-136">You'll run the next command and replace the `<resource_group_name>` and `<location>` respectively with appropriate values.</span></span>

   ```bash
   az group create --name <resourcegroup> --location <location>
   ```

<span data-ttu-id="fdfde-137">Der letzte Schritt ist die Erstellung des Azure Database for PostgreSQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="fdfde-137">The last step is to create the Azure Database for PostgreSQL server.</span></span>

   <span data-ttu-id="fdfde-138">Die Azure CLI-Hilfe zum Befehl für die Servererstellung mit allen verfügbaren Parametern sieht wie im folgenden Beispiel aus:</span><span class="sxs-lookup"><span data-stu-id="fdfde-138">The Azure CLI server creation command usage help showing all available parameters looks like the following example:</span></span>

   ```bash
   az postgres server create [-h] [--verbose] [--debug]
                             [--output {json,jsonc,table,tsv}]
                             [--query JMESPATH]
                              --resource-group RESOURCE_GROUP_NAME --name SERVER_NAME
                              --sku-name SKU_NAME [--location LOCATION]
                              --admin-user ADMINISTRATOR_LOGIN
                              [--admin-password ADMINISTRATOR_LOGIN_PASSWORD]
                              [--backup-retention BACKUP_RETENTION]
                              [--geo-redundant-backup GEO_REDUNDANT_BACKUP]
                              [--ssl-enforcement {Enabled,Disabled}]
                              [--storage-size STORAGE_MB]
                              [--tags [TAGS [TAGS ...]]]
                              [--version VERSION]
                              [--subscription _SUBSCRIPTION]

   ```

   <span data-ttu-id="fdfde-139">Mit der folgenden Befehlszeile werden die Parameter angezeigt, die zum Erstellen eines Azure Database for PostgreSQL-Servers erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="fdfde-139">The following command line shows the required set of parameters to create an Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="fdfde-140">Sie werden sehen, dass einige Parameter optional und nicht aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="fdfde-140">You'll notice some are optional parameters and aren't listed.</span></span>

   ```bash
   az postgres server create --resource-group <resource_group_name> --name <new_server_name> --admin-user <admin_user_name> --admin-password <server_admin_password> --sku-name <sku> --version <version_number>  --location <region_name> --storage-size <size> --backup-retention <days>
   ```

### <a name="parameter-descriptions"></a><span data-ttu-id="fdfde-141">Beschreibungen der Parameter</span><span class="sxs-lookup"><span data-stu-id="fdfde-141">Parameter descriptions</span></span>

<span data-ttu-id="fdfde-142">Mit dem Parameter `--resource-group <resource_group_name>` wird die Ressourcengruppe angegeben, in der der Server erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="fdfde-142">The `--resource-group <resource_group_name>` parameter specifies the resource group within which to create the server.</span></span>

<span data-ttu-id="fdfde-143">Die Elemente `admin-user` und `admin-password` für den Server, die Sie angeben, werden für die Anmeldung am Server und den zugehörigen Datenbanken benötigt.</span><span class="sxs-lookup"><span data-stu-id="fdfde-143">The server `admin-user` and `admin-password` that you specify is required to sign in to the server and its databases.</span></span> <span data-ttu-id="fdfde-144">Es ist ratsam, dass Sie sich diese Informationen für die spätere Interaktion mit dem Server merken bzw. notieren.</span><span class="sxs-lookup"><span data-stu-id="fdfde-144">Remember or record this information for later when interacting with the new server.</span></span>

<span data-ttu-id="fdfde-145">Sie verwenden den Parameter `--sku-name`, um einen Teil des Tarifs anzugeben. In diesem Fall ist dies die Computeressource.</span><span class="sxs-lookup"><span data-stu-id="fdfde-145">You use the `--sku-name` parameter is used to specify part of the pricing tier, in this case compute resource.</span></span> <span data-ttu-id="fdfde-146">Für den Wert wird die Konvention `{pricing tier}_{compute generation}_{vCores}` verwendet.</span><span class="sxs-lookup"><span data-stu-id="fdfde-146">The value follows the convention `{pricing tier}_{compute generation}_{vCores}`.</span></span>

<span data-ttu-id="fdfde-147">Beispiele:</span><span class="sxs-lookup"><span data-stu-id="fdfde-147">Examples:</span></span>

- <span data-ttu-id="fdfde-148">`--sku-name B_Gen4_4` ist „Basic“, „Gen 4“ und „4 V-Kerne“ zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="fdfde-148">`--sku-name B_Gen4_4` maps to Basic, Gen 4, and 4 vCores.</span></span>
- <span data-ttu-id="fdfde-149">`--sku-name GP_Gen5_32` ist „Universell“, „Gen 5“ und „32 V-Kerne“ zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="fdfde-149">`--sku-name GP_Gen5_32` maps to General Purpose, Gen 5, and 32 vCores.</span></span>
- <span data-ttu-id="fdfde-150">`--sku-name MO_Gen5_2` ist „Arbeitsspeicheroptimiert“, „Gen 5“ und „2 V-Kerne“ zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="fdfde-150">`--sku-name MO_Gen5_2` maps to Memory Optimized, Gen 5, and 2 vCores.</span></span>

<span data-ttu-id="fdfde-151">Zur Erinnerung: Die drei Tarife wurden in der Einheit beschrieben, in der wir mit dem Portal den Server erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="fdfde-151">Recall, we discussed the three pricing tiers in the unit where we create the server using the portal.</span></span>

<span data-ttu-id="fdfde-152">Angenommen, Sie möchten eine Computeressource vom Typ „Basic, Gen 5, 1 V-Kern“ verwenden. In diesem Fall geben Sie für den Parameter `--sku-name B_Gen5_1` an.</span><span class="sxs-lookup"><span data-stu-id="fdfde-152">Let's assume you want to use a Basic, Gen 5, and 1 vCore compute resource, you'll then specify the parameter as `--sku-name B_Gen5_1`.</span></span>

<span data-ttu-id="fdfde-153">Außerdem nutzen Sie den Parameter `--storage-size`, um einen Teil des Tarifs anzugeben.</span><span class="sxs-lookup"><span data-stu-id="fdfde-153">You use the `--storage-size` parameter is also used the specify part of the pricing tier.</span></span> <span data-ttu-id="fdfde-154">Wenn der Wert nicht angegeben wird, wird standardmäßig 5.120 MB verwendet.</span><span class="sxs-lookup"><span data-stu-id="fdfde-154">If the value isn't specified, then it defaults to 5,120 MB.</span></span> <span data-ttu-id="fdfde-155">Die gültigen Speichergrößen reichen von 5.120 MB in Inkrementen von 1.024 MB bis 1.048.576 MB.</span><span class="sxs-lookup"><span data-stu-id="fdfde-155">Valid storage sizes range from 5,120 MB and increases in additional increments of 1,024 MB up to 1,048,576 MB.</span></span>

<span data-ttu-id="fdfde-156">Der Parameter `--backup-retention` wird verwendet, wenn Sie den Aufbewahrungszeitraum für Sicherungen in Tagen angeben müssen.</span><span class="sxs-lookup"><span data-stu-id="fdfde-156">The `--backup-retention` parameter is used when you need to specify the retention period for backups specified in days.</span></span> <span data-ttu-id="fdfde-157">Wenn der Wert nicht angegeben wird, werden standardmäßig sieben Tage verwendet.</span><span class="sxs-lookup"><span data-stu-id="fdfde-157">If the value isn't specified, then it defaults to seven days.</span></span>

<span data-ttu-id="fdfde-158">Sie nutzen den Parameter `--version`, um die gewünschte Hauptversion von PostgreSQL anzugeben.</span><span class="sxs-lookup"><span data-stu-id="fdfde-158">You use the `--version` parameter is used to specify the major version of PostgreSQL you would like to use.</span></span>

<span data-ttu-id="fdfde-159">Sie haben nun die Schritte kennengelernt, mit denen Sie per Azure CLI eine Azure Database for PostgreSQL-Instanz erstellen.</span><span class="sxs-lookup"><span data-stu-id="fdfde-159">You've now seen the steps to create an Azure Database for PostgreSQL using Azure CLI.</span></span> <span data-ttu-id="fdfde-160">In der nächsten Einheit erstellen Sie mit der Azure CLI einen Azure Database for PostgreSQL-Server.</span><span class="sxs-lookup"><span data-stu-id="fdfde-160">In the next unit, you'll create an Azure Database for PostgreSQL server using Azure CLI.</span></span>