<span data-ttu-id="14d6c-101">Als Nächstes verwenden wir die Azure-Befehlszeilenschnittstelle, um eine Ressourcengruppe zu erstellen und anschließend eine Web-App in dieser Ressourcengruppe bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="14d6c-101">Next, let's use the Azure CLI to create a resource group, and then to deploy a web app into this resource group.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="using-a-resource-group"></a><span data-ttu-id="14d6c-102">Verwenden einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="14d6c-102">Using a resource group</span></span>

<span data-ttu-id="14d6c-103">Wenn Sie Ihren eigenen Computer und Ihr eigenes Azure-Abonnement verwenden, müssen Sie sich zuerst mithilfe des `az login`-Befehls bei Azure anmelden.</span><span class="sxs-lookup"><span data-stu-id="14d6c-103">When you are working with your own machine and Azure subscription you will need to first login to Azure using the `az login` command.</span></span> <span data-ttu-id="14d6c-104">Mit der Cloud Shell-Umgebung ist dies nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="14d6c-104">This is unnecessary with the Cloud Shell environment.</span></span>

<span data-ttu-id="14d6c-105">Als Nächstes würden Sie normalerweise mit einem Befehl vom Typ `az group create` eine Ressourcengruppe für alle Ihre verwandten Azure-Ressourcen erstellen. Für diese Übungen wurde aber bereits eine Ressourcengruppe für Sie erstellt.</span><span class="sxs-lookup"><span data-stu-id="14d6c-105">Next, you would normally create a resource group for all your related Azure resources with an `az group create` command, but for these exercises one has been created for you.</span></span> <span data-ttu-id="14d6c-106">Verwenden Sie **<rgn>[Name der Sandboxressourcengruppe]</rgn>** für Ihre Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="14d6c-106">Use **<rgn>[sandbox resource group name]</rgn>** for your resource group.</span></span>

1. <span data-ttu-id="14d6c-107">Mithilfe der Azure-Befehlszeilenschnittstelle können Sie alle Ihre Ressourcengruppen in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="14d6c-107">You can ask the Azure CLI to list all your resource groups in a table.</span></span> <span data-ttu-id="14d6c-108">Es sollte eine Ressourcengruppe vorhanden sein, wenn Sie die kostenlose Azure-Sandbox verwenden.</span><span class="sxs-lookup"><span data-stu-id="14d6c-108">There should just be one while you are in the free Azure sandbox.</span></span>

    ```azurecli
    az group list --output table
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="14d6c-109">Im Zuge der Azure-Entwicklung können nach und nach mehrere Ressourcengruppen zusammenkommen.</span><span class="sxs-lookup"><span data-stu-id="14d6c-109">As you do more Azure development, you can end up with several resource groups.</span></span> <span data-ttu-id="14d6c-110">Falls die Gruppenliste mehrere Elemente enthält, können Sie die Rückgabewerte filtern, indem Sie eine Option vom Typ `--query` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="14d6c-110">If you have several items in the group list, you can filter the return values by adding a `--query` option.</span></span> <span data-ttu-id="14d6c-111">Verwenden Sie den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="14d6c-111">Try this command:</span></span>

    ```azurecli
    az group list --query "[?name == '<rgn>[sandbox resource group name]</rgn>']"
    ```

    <span data-ttu-id="14d6c-112">Die Abfrage wird mit **JMESPath** (einer Standardabfragesprache für JSON-Abfragen) formatiert.</span><span class="sxs-lookup"><span data-stu-id="14d6c-112">The query is formated using **JMESPath** which is a standard query language for JSON requests.</span></span> <span data-ttu-id="14d6c-113">Weitere Informationen zu dieser leistungsstarken Filtersprache finden Sie unter <http://jmespath.org/>.</span><span class="sxs-lookup"><span data-stu-id="14d6c-113">You can learn more about this powerful filter language at <http://jmespath.org/>.</span></span> <span data-ttu-id="14d6c-114">Im Modul **Verwalten von virtuellen Computern mit Azure CLI** werden Abfragen ausführlicher behandelt.</span><span class="sxs-lookup"><span data-stu-id="14d6c-114">We also cover queries in more depth in the **Manage VMs with the Azure CLI** module.</span></span>

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="14d6c-115">Schritte zum Erstellen eines Serviceplans</span><span class="sxs-lookup"><span data-stu-id="14d6c-115">Steps to create a service plan</span></span>

<span data-ttu-id="14d6c-116">Beim Ausführen von Web-Apps mithilfe von Azure App Service zahlen Sie für die von der App verwendeten Azure-Computeressourcen, die vom Ihren Web-Apps zugeordneten Service-Plan abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="14d6c-116">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="14d6c-117">Servicepläne bestimmen die Region, die für das Rechenzentrum der App, die Anzahl von verwendeten VMs und Tarife verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="14d6c-117">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="14d6c-118">Erstellen Sie einen App Service-Plan, um die App auszuführen.</span><span class="sxs-lookup"><span data-stu-id="14d6c-118">Create an App Service plan to run your app.</span></span> <span data-ttu-id="14d6c-119">Der folgende Befehl gibt weder Tarif noch Details der VM-Instanzen an, weshalb Sie standardmäßig einen **Basic**-Tarif mit einer **kleinen** VM-Instanz erhalten.</span><span class="sxs-lookup"><span data-stu-id="14d6c-119">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    > [!WARNING]
    > <span data-ttu-id="14d6c-120">Der Name der App und des Plans muss _eindeutig_ sein. Fügen Sie dem Namen also ein Suffix hinzu, und ersetzen Sie den Text `<unique>` im folgenden Befehl durch eine Reihe von Zahlen, Ihre Initialen oder anderen Text, um sicherzustellen, dass der Name in Azure eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="14d6c-120">The name of the app and plan must be _unique_, so add a suffix to the name and replace the `<unique>` text in the command below with a set of numbers, your initials, or some other piece of text to make sure it's unique in all of Azure.</span></span>

    <span data-ttu-id="14d6c-121">Verwenden Sie für den `--location`-Parameter einen der folgenden Standortwerte.</span><span class="sxs-lookup"><span data-stu-id="14d6c-121">For the `--location` parameter, use one of the below location values.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    az appservice plan create --name popupappplan-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --location <location>
    ```

    <span data-ttu-id="14d6c-122">Die Ausführung dieses Befehls kann mehrere Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="14d6c-122">This command can take several minutes to complete.</span></span>

1. <span data-ttu-id="14d6c-123">Überprüfen Sie, ob der Serviceplan erfolgreich erstellt wurde, indem Sie alle Pläne in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="14d6c-123">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="14d6c-124">Schritte zum Erstellen einer Web-App</span><span class="sxs-lookup"><span data-stu-id="14d6c-124">Steps to create a web app</span></span>

<span data-ttu-id="14d6c-125">Als Nächstes erstellen Sie die Web-App in Ihrem Serviceplan.</span><span class="sxs-lookup"><span data-stu-id="14d6c-125">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="14d6c-126">Sie können den Code zur gleichen Zeit bereitstellen, in diesem Beispiel wird dies jedoch in separaten Schritten durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="14d6c-126">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="14d6c-127">Erstellen Sie die Web-App, und geben Sie den Namen des zuvor erstellten Plans an.</span><span class="sxs-lookup"><span data-stu-id="14d6c-127">Create the web app, supply the name of the plan you created above.</span></span> <span data-ttu-id="14d6c-128">**Der Name der App muss wie der des Plans eindeutig sein.** Ersetzen Sie den `<unique>`-Marker durch Text, damit der Name global eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="14d6c-128">**Just like the plan, the app name must be unique**, replace the `<unique>` marker with some text to make the name globally unique.</span></span>

    ```azurecli
    az webapp create --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --plan popupappplan-<unique>
    ```

1. <span data-ttu-id="14d6c-129">Überprüfen Sie, ob die App erfolgreich erstellt wurde, indem Sie alle Apps in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="14d6c-129">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```azurecli
    az webapp list --output table
    ```

1. <span data-ttu-id="14d6c-130">Notieren Sie sich den Wert von **DefaultHostName** in der Tabelle. Dies ist die erreichbare Webadresse der neuen Website.</span><span class="sxs-lookup"><span data-stu-id="14d6c-130">Make a note of the **DefaultHostName** listed in the table; this is the reachable web address for the new website.</span></span> <span data-ttu-id="14d6c-131">Ihre Website wird von Azure über den eindeutigen App-Namen in der `azurewebsites.net`-Domäne zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="14d6c-131">Azure will make your website available through the unique app name in the `azurewebsites.net` domain.</span></span> <span data-ttu-id="14d6c-132">Wenn der Name beispielsweise „popupwebapp-mslearn123“ wäre, würde die Website-URL wie folgt aussehen: `http://popupwebapp-mslearn123.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="14d6c-132">For example, if my app name was "popupwebapp-mslearn123", then my website URL would be: `http://popupwebapp-mslearn123.azurewebsites.net`.</span></span>

1. <span data-ttu-id="14d6c-133">Ihre Website verfügt über die Seite "QuickStart", die von Azure erstellt wurde und die Sie entweder in einem Browser oder mit cURL anzeigen können, indem Sie **DefaultHostName** verwenden.</span><span class="sxs-lookup"><span data-stu-id="14d6c-133">Your site has a "QuickStart" page created by Azure that you can see either in a browser, or with CURL, just use the **DefaultHostName**:</span></span>

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="14d6c-134">Schritte zum Bereitstellen von Code über GitHub</span><span class="sxs-lookup"><span data-stu-id="14d6c-134">Steps to deploy code from GitHub</span></span>

1. <span data-ttu-id="14d6c-135">Der letzte Schritt besteht im Bereitstellen von Code über ein GitHub-Repository in die Web-App.</span><span class="sxs-lookup"><span data-stu-id="14d6c-135">The final step is to deploy code from a GitHub repository to the web app.</span></span> <span data-ttu-id="14d6c-136">Sie verwenden hierzu eine einfache PHP-Seite, die im GitHub-Repository „Azure Samples“ verfügbar ist und „HelloWorld!“ anzeigt,</span><span class="sxs-lookup"><span data-stu-id="14d6c-136">Let's use a simple PHP page available in the Azure Samples Github repository that displays "HelloWorld!"</span></span> <span data-ttu-id="14d6c-137">wenn sie ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="14d6c-137">when it executes.</span></span> <span data-ttu-id="14d6c-138">Stellen Sie sicher, dass Sie den Namen der Web-App verwenden, die Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="14d6c-138">Make sure to use the web app name you created.</span></span>

    ```azurecli
    az webapp deployment source config --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="14d6c-139">Besuchen Sie Ihre Website nach der Bereitstellung erneut über einen Browser oder cURL.</span><span class="sxs-lookup"><span data-stu-id="14d6c-139">Once it's deployed, hit your site again with a browser or CURL.</span></span>

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
    <span data-ttu-id="14d6c-140">Auf der Seite wird die Nachricht „Hello World!“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="14d6c-140">The page displays "Hello World!"</span></span>

    ```output
    Hello World!
    ```

<span data-ttu-id="14d6c-141">In dieser Übung wurde ein typisches Muster für eine interaktive Azure CLI-Sitzung gezeigt.</span><span class="sxs-lookup"><span data-stu-id="14d6c-141">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="14d6c-142">Zuerst haben Sie einen Standardbefehl verwendet, um eine neue Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="14d6c-142">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="14d6c-143">Danach haben Sie eine Reihe von Befehlen verwendet, um eine Ressource (in diesem Beispiel eine Web-App) in dieser Ressourcengruppe bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="14d6c-143">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="14d6c-144">Diese Befehle können einfach in einem Shellskript zusammengefasst und jederzeit ausgeführt werden, wenn Sie die gleiche Ressource erstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="14d6c-144">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>