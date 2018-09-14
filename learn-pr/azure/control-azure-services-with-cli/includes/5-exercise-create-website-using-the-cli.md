<span data-ttu-id="4ac3e-101">Als Nächstes verwenden Sie Azure CLI zum Erstellen einer Ressourcengruppe und anschließend zum Bereitstellen einer Web-App in dieser Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-101">Next, let's use the Azure CLI to create a resource group, and then to deploy a web app into this resource group.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="4ac3e-102">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="4ac3e-102">Create a resource group</span></span>

1. <span data-ttu-id="4ac3e-103">Öffnen Sie eine Bash-Shell unter Linux oder macOS, oder öffnen Sie das Fenster „Eingabeaufforderung“ oder PowerShell, wenn Sie unter Windows arbeiten.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-103">Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="4ac3e-104">Starten Sie die Azure-Befehlszeilenschnittstelle, und führen Sie den Anmeldebefehl aus.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-104">Start the Azure CLI and run the login command.</span></span>

    ```azurecli
    az login
    ```
    <span data-ttu-id="4ac3e-105">Wenn sich in Ihrem Webbrowser keine Azure-Anmeldeseite öffnet, befolgen Sie die Befehlszeilenanweisungen, und geben Sie unter [https://aka.ms/devicelogin](https://aka.ms/devicelogin) einen Autorisierungscode ein.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-105">If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="4ac3e-106">Erstellen Sie eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-106">Create a resource group.</span></span>

    ```azurecli
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="4ac3e-107">Überprüfen Sie, ob die Ressourcengruppe erfolgreich erstellt wurde, indem Sie alle Ressourcengruppen in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```azurecli
    az group list --output table
    ```

> [!TIP]
> <span data-ttu-id="4ac3e-108">Sie können auch im Azure-Portal überprüfen, ob die Ressource erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-108">You can also confirm the resource was created in the Azure portal.</span></span> <span data-ttu-id="4ac3e-109">Öffnen Sie einen Webbrowser, melden Sie sich beim Portal an, und navigieren Sie zum Abschnitt **Ressourcengruppen**.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-109">Open a web browser, sign in to the portal and navigate to the **Resource Groups** section.</span></span> <span data-ttu-id="4ac3e-110">Die neue Ressourcengruppe sollte in der Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-110">The new resource group should be displayed in the list.</span></span>

1. <span data-ttu-id="4ac3e-111">Wenn Sie über viele Elemente in der Gruppe verfügen, können Sie nach den Rückgabewerten filtern, indem Sie eine `--query`-Option hinzufügen. Testen Sie den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="4ac3e-111">If you have a lot of items in the group, you can filter the return values by adding a `--query` option, try this command:</span></span>

    ```azurecli
    az group list --query "[?name == 'popupResGroup']"
    ```

    <span data-ttu-id="4ac3e-112">Die Abfrage wird mit **JMESPath** formatiert, was eine standardmäßige Abfragesprache für JSON-Abfragen ist.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-112">The query is formmated using **JMESPath** which is a standard query language for JSON requests.</span></span> <span data-ttu-id="4ac3e-113">Weitere Informationen über diese leistungsstarke Filtersprache finden Sie unter <http://jmespath.org/>.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-113">You can learn more about this powerful filter language at <http://jmespath.org/>.</span></span> <span data-ttu-id="4ac3e-114">Im Modul **Verwalten von virtuellen Computern mit Azure CLI** werden Abfragen ausführlicher behandelt.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-114">We also cover queries in more depth in the **Manage VMs with the Azure CLI** module.</span></span>

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="4ac3e-115">Schritte zum Erstellen eines Serviceplans</span><span class="sxs-lookup"><span data-stu-id="4ac3e-115">Steps to create a service plan</span></span>

<span data-ttu-id="4ac3e-116">Beim Ausführen von Web-Apps mithilfe von Azure App Service zahlen Sie für die von der App verwendeten Azure-Computeressourcen, die vom Ihren Web-Apps zugeordneten Service-Plan abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-116">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="4ac3e-117">Servicepläne bestimmen die Region, die für das Rechenzentrum der App, die Anzahl von verwendeten VMs und Tarife verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-117">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="4ac3e-118">Erstellen Sie einen App Service-Plan, um die App auszuführen.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-118">Create an App Service plan to run your app.</span></span> <span data-ttu-id="4ac3e-119">Der folgende Befehl gibt weder Tarif noch Details der VM-Instanzen an, weshalb Sie standardmäßig einen **Basic**-Tarif mit einer **kleinen** VM-Instanz erhalten.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-119">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    > [!WARNING]
    > <span data-ttu-id="4ac3e-120">Die Namen der App und des Plans müssen _eindeutig_ sein, fügen Sie den Namen also ein Suffix hinzu, und ersetzen Sie den `<unique>`-Text im folgenden Befehl mit einer Reihe von Zahlen, Ihren Initialen oder einem anderen Text, um sicherzustellen, dass der Name im gesamten Umfang von Azure eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-120">The name of the app and plan must be _unique_, so add a suffix to the name and replace the `<unique>` text in the command below with a set of numbers, your initials, or some other piece of text to make sure it's unique in all of Azure.</span></span> 

    ```azurecli
    az appservice plan create --name popupapp-<unique> --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="4ac3e-121">Überprüfen Sie, ob der Serviceplan erfolgreich erstellt wurde, indem Sie alle Pläne in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-121">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="4ac3e-122">Schritte zum Erstellen einer Web-App</span><span class="sxs-lookup"><span data-stu-id="4ac3e-122">Steps to create a web app</span></span>

<span data-ttu-id="4ac3e-123">Als Nächstes erstellen Sie die Web-App in Ihrem Serviceplan.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-123">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="4ac3e-124">Sie können den Code zur gleichen Zeit bereitstellen, in diesem Beispiel wird dies jedoch in separaten Schritten durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-124">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="4ac3e-125">Erstellen Sie die Web-App, und geben Sie den Namen des zuvor erstellten Plans an.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-125">Create the web app, supply the name of the plan you created above.</span></span> <span data-ttu-id="4ac3e-126">**Der Name der App muss wie der des Plans eindeutig sein. Ersetzen Sie den Marker `<unique>` durch Text, damit der Name global eindeutig ist.**</span><span class="sxs-lookup"><span data-stu-id="4ac3e-126">**Just like the plan, the app name must be unique, replace the `<unique>` marker with some text to make the name globally unique.**</span></span>
    ```azurecli
    az webapp create --name popupapp-<unique> --resource-group popupResGroup --plan popupapp-<unique>
    ```

1. <span data-ttu-id="4ac3e-127">Überprüfen Sie, ob die App erfolgreich erstellt wurde, indem Sie alle Apps in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-127">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```azurecli
    az webapp list --output table
    ```

1. <span data-ttu-id="4ac3e-128">Notieren Sie sich den Wert von **DefaultHostName**, da Sie diesen später erneut benötigen.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-128">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="4ac3e-129">Schritte zum Bereitstellen von Code über GitHub</span><span class="sxs-lookup"><span data-stu-id="4ac3e-129">Steps to deploy code from GitHub</span></span>

1. <span data-ttu-id="4ac3e-130">Der letzte Schritt besteht im Bereitstellen von Code über ein GitHub-Repository in die Web-App.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-130">The final step is to deploy code from a GitHub repository to the web app.</span></span> <span data-ttu-id="4ac3e-131">Sie verwenden hierzu eine einfache PHP-Seite, die im GitHub-Repository „Azure Samples“ verfügbar ist und „HelloWorld!“ anzeigt,</span><span class="sxs-lookup"><span data-stu-id="4ac3e-131">Let's use a simple PHP page available in the Azure Samples Github repository that displays "HelloWorld!"</span></span> <span data-ttu-id="4ac3e-132">wenn sie ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-132">when it executes.</span></span> <span data-ttu-id="4ac3e-133">Stellen Sie sicher, dass Sie den Namen der Web-App verwenden, die Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-133">Make sure to use the web app name you created.</span></span>

    ```azurecli
    az webapp deployment source config --name popupapp-<unique> --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="4ac3e-134">Nach der Bereitstellung wird Ihre Website von Azure über den eindeutigen App-Namen in der `azurewebsites.net`-Domäne zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-134">Once it's deployed, Azure will make your website available through the unique app name in the `azurewebsites.net` domain.</span></span> <span data-ttu-id="4ac3e-135">Wenn der Name beispielsweise „popupapp-mslearn123“ wäre, würde die Adresse der Website wie folgt aussehen: <http://popupapp-mslearn123.azurewebsites.net>.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-135">For example, if my app name was "popupapp-mslearn123", then my website address would be: <http://popupapp-mslearn123.azurewebsites.net>.</span></span> <span data-ttu-id="4ac3e-136">Sie müssen die richtige URL eingeben, um die spezifische Instanz zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-136">You will need to type in the correct URL to hit your specific instance.</span></span>

1. <span data-ttu-id="4ac3e-137">Auf der Seite wird die Nachricht „HelloWorld!“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-137">The page displays "HelloWorld!"</span></span>

1. <span data-ttu-id="4ac3e-138">Schließen Sie das Browserfenster.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-138">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="4ac3e-139">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="4ac3e-139">Summary</span></span>

<span data-ttu-id="4ac3e-140">In dieser Übung wurde ein typisches Muster für eine interaktive Azure CLI-Sitzung veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-140">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="4ac3e-141">Zuerst haben Sie einen Standardbefehl verwendet, um eine neue Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-141">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="4ac3e-142">Danach haben Sie eine Reihe von Befehlen verwendet, um eine Ressource (in diesem Beispiel eine Web-App) in dieser Ressourcengruppe bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-142">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="4ac3e-143">Diese Befehle können einfach in einem Shellskript zusammengefasst und jederzeit ausgeführt werden, wenn Sie die gleiche Ressource erstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="4ac3e-143">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
