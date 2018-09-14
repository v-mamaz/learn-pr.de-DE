
<span data-ttu-id="9e9d7-101">In dieser Übung verwenden Sie die Azure-Befehlszeilenschnittstelle auf Ihrem lokalen Computer zum Erstellen einer Ressourcengruppe und danach, um in dieser Ressourcengruppe eine Web-App bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-101">In this exercise, you will use the Azure CLI on your local machine to create a resource group, and then to deploy a web app into this resource group.</span></span> 

### <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="9e9d7-102">Schritte zum Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="9e9d7-102">Steps to create a resource group</span></span>
1. <span data-ttu-id="9e9d7-103">Öffnen Sie eine Bash-Shell unter Linux oder macOS, oder öffnen Sie das Fenster „Eingabeaufforderung“ oder PowerShell, wenn Sie unter Windows arbeiten.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-103">Open a bash shell on Linux or macOS, or open the Command Prompt window or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="9e9d7-104">Starten Sie die Azure-Befehlszeilenschnittstelle, und führen Sie den Anmeldebefehl aus.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-104">Start the Azure CLI and run the login command.</span></span>

    ```bash
    az login
    ```
    <span data-ttu-id="9e9d7-105">Wenn sich in Ihrem Webbrowser keine Azure-Anmeldeseite öffnet, befolgen Sie die Befehlszeilenanweisungen, und geben Sie unter [https://aka.ms/devicelogin](https://aka.ms/devicelogin) einen Autorisierungscode ein.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-105">If you do not get an Azure sign-in page in your web browser, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="9e9d7-106">Erstellen Sie eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-106">Create a resource group.</span></span>

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="9e9d7-107">Überprüfen Sie, ob die Ressourcengruppe erfolgreich erstellt wurde, indem Sie alle Ressourcengruppen in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-107">Verify that the resource group was created successfully by listing all your resource groups in a table.</span></span>

    ```bash
    az group list --output table
    ```
1. <span data-ttu-id="9e9d7-108">Optional können Sie bestätigen, dass die Ressource im Azure-Portal erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-108">Optionally, confirm the resource was created in the Azure portal.</span></span> <span data-ttu-id="9e9d7-109">Öffnen Sie einen Webbrowser, melden Sie sich beim Portal an, und navigieren Sie zum Abschnitt **Ressourcengruppen** (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="9e9d7-109">Open a web browser, sign in to the portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="9e9d7-110">Die neue Ressourcengruppe sollte in der Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-110">The new resource group should be displayed in the list.</span></span>

![Auflisten von Ressourcengruppen über das Portal](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="9e9d7-112">Schritte zum Erstellen eines Serviceplans</span><span class="sxs-lookup"><span data-stu-id="9e9d7-112">Steps to create a service plan</span></span>
<span data-ttu-id="9e9d7-113">Beim Ausführen von Web-Apps mithilfe von Azure App Service zahlen Sie für die von der App verwendeten Azure-Computeressourcen, die vom Ihren Web-Apps zugeordneten Service-Plan abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-113">When you run Web Apps, using the Azure App Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="9e9d7-114">Servicepläne bestimmen die Region, die für das Rechenzentrum der App, die Anzahl von verwendeten VMs und Tarife verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-114">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="9e9d7-115">Erstellen Sie einen App Service-Plan, um die App auszuführen.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-115">Create an App Service plan to run your app.</span></span> <span data-ttu-id="9e9d7-116">Der Name der App und des Plans muss eindeutig sein. Ändern Sie deshalb die Zeichenfolge „12345“ in eine zufällige Zahl.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-116">The name of the app and plan must be unique, so change the string "12345" to a random number.</span></span> <span data-ttu-id="9e9d7-117">Der folgende Befehl gibt keinen Tarif oder Details der VM-Instanzen an, weshalb Sie standardmäßig einen **Basic**-Tarif mit einer **kleinen** VM-Instanz erhalten.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-117">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="9e9d7-118">Überprüfen Sie, ob der Serviceplan erfolgreich erstellt wurde, indem Sie alle Pläne in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-118">Verify that the service plan was created successfully by listing all your plans in a table.</span></span>

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="9e9d7-119">Schritte zum Erstellen einer Web-App</span><span class="sxs-lookup"><span data-stu-id="9e9d7-119">Steps to create a web app</span></span>
<span data-ttu-id="9e9d7-120">Als Nächstes erstellen Sie die Web-App in Ihrem Serviceplan.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-120">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="9e9d7-121">Sie können den Code zur gleichen Zeit bereitstellen, aber in unserem Beispiel machen wir dies in separaten Schritten.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-121">You can deploy the code at the same time, but for our example, we'll do this as separate steps.</span></span>

1. <span data-ttu-id="9e9d7-122">Erstellen Sie die Web-App, und ändern Sie die Zeichenfolge „12345“ in die gleiche Zufallszahl, die Sie zuvor verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-122">Create the web app, remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. <span data-ttu-id="9e9d7-123">Überprüfen Sie, ob die App erfolgreich erstellt wurde, indem Sie alle Apps in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-123">Verify that the app was created successfully by listing all your apps in a table.</span></span>

    ```bash
    az webapp list --output table
    ```

1. <span data-ttu-id="9e9d7-124">Notieren Sie sich den Wert von **DefaultHostName**, da Sie diesen später erneut benötigen.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-124">Make a note of the **DefaultHostName**; you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="9e9d7-125">Schritte zum Bereitstellen von Code über GitHub</span><span class="sxs-lookup"><span data-stu-id="9e9d7-125">Steps to deploy code from GitHub</span></span>
1. <span data-ttu-id="9e9d7-126">Im letzten Schritt wird Code über ein GitHub-Repository in der Web-App bereitgestellt, und die Zeichenfolge „12345“ wird erneut in die gleiche zuvor verwendete Zufallszahl geändert.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-126">The final step is to deploy code from a GitHub repository to the web app, again remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="9e9d7-127">Kopieren Sie die folgende URL in einen Browser, um die Web-App anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-127">Copy the following url into a browser to see the web app.</span></span>
<span data-ttu-id="9e9d7-128">http://popupapp12345.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="9e9d7-128">http://popupapp12345.azurewebsites.net</span></span>

1. <span data-ttu-id="9e9d7-129">Auf der Seite wird die Nachricht „HelloWorld!“ angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-129">The page displays "HelloWorld!"</span></span>

1. <span data-ttu-id="9e9d7-130">Schließen Sie das Browserfenster.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-130">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="9e9d7-131">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="9e9d7-131">Summary</span></span>
<span data-ttu-id="9e9d7-132">In dieser Übung wurde ein typisches Muster für eine interaktive Azure CLI-Sitzung veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-132">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="9e9d7-133">Zuerst haben Sie einen Standardbefehl verwendet, um eine neue Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-133">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="9e9d7-134">Danach haben Sie eine Reihe von Befehlen verwendet, um eine Ressource (in diesem Beispiel eine Web-App) in dieser Ressourcengruppe bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-134">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="9e9d7-135">Diese Befehle können einfach in einem Shellskript zusammengefasst und jederzeit ausgeführt werden, wenn Sie die gleiche Ressource erstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="9e9d7-135">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
