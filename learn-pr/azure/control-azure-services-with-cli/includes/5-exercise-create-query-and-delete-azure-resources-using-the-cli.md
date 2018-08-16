
<span data-ttu-id="6e330-101">In dieser Übung verwenden Sie einen der Azure-Befehlszeilenschnittstelle auf Ihrem lokalen Computer zum Erstellen einer Ressourcengruppe aus, und klicken Sie dann auf, um eine Web-App in dieser Ressourcengruppe bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="6e330-101">In this exercise, you will use the Azure CLI on your local machine to create a resource group, and then to deploy a Web App into this resource group.</span></span> 

### <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="6e330-102">Schritte zum Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="6e330-102">Steps to create a resource group</span></span>
1. <span data-ttu-id="6e330-103">Öffnen Sie eine Bash-Shell unter Linux oder MacOS, oder öffnen Sie die Eingabeaufforderung oder PowerShell ein, wenn von Windows zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="6e330-103">Open a bash shell on Linux or macOS, or open the Command Prompt or PowerShell if working from Windows.</span></span>

1. <span data-ttu-id="6e330-104">Starten Sie die Azure-Befehlszeilenschnittstelle, und führen Sie den Login-Befehl.</span><span class="sxs-lookup"><span data-stu-id="6e330-104">Start the Azure CLI and run the login command.</span></span>

    ```bash
    az login
    ```
    <span data-ttu-id="6e330-105">Wenn Sie ein Azure-Registrierung nicht erhalten Seite in Ihrem Webbrowser, folgen Sie den Anweisungen über die Befehlszeile, und geben Sie einen Autorisierungscode an [ https://aka.ms/devicelogin ](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="6e330-105">If you do not get an Azure sign in page in your web browser, follow the command line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

1. <span data-ttu-id="6e330-106">Erstellen Sie eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="6e330-106">Create a resource group.</span></span>

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. <span data-ttu-id="6e330-107">Stellen Sie sicher, dass die Ressourcengruppe erfolgreich erstellt wurde, indem Sie alle Ressourcengruppen in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="6e330-107">Verify that the resource group was created successfully, by listing all your resource groups in a table.</span></span>

    ```bash
    az group list --output table
    ```
1. <span data-ttu-id="6e330-108">Optional: Überprüfen Sie, dass die Ressource im Azure-Portal erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="6e330-108">Optionally, confirm the resource was created in the Azure Portal.</span></span> <span data-ttu-id="6e330-109">Öffnen Sie einen Webbrowser, melden Sie sich im Portal, und navigieren Sie zu der **Ressourcengruppen** Abschnitt (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="6e330-109">Open a web browser, login to the Portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="6e330-110">Die neue Ressourcengruppe sollte in der Liste angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="6e330-110">The new resource group should be displayed in the list.</span></span>

![Verwenden des Portals zum Auflisten von Ressourcengruppen](../images/listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a><span data-ttu-id="6e330-112">Schritte zum Erstellen eines Service-Plans</span><span class="sxs-lookup"><span data-stu-id="6e330-112">Steps to create a service plan</span></span>
<span data-ttu-id="6e330-113">Beim Ausführen von Web-Apps mithilfe des Azure-Apps-Diensts, Zahlen Sie für die Azure Compute-Ressourcen, die von der app verwendet, und dies hängt von der App Service-Plans, der Ihre Web-Apps zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="6e330-113">When you run Web Apps, using the Azure Apps Service, you pay for the Azure compute resources used by the app, and this depends on the App Service plan associated with your Web Apps.</span></span> <span data-ttu-id="6e330-114">Service-Pläne bestimmen Sie die Region für die app-Datencenter, die Anzahl von virtuellen Computern verwendet und Tarif.</span><span class="sxs-lookup"><span data-stu-id="6e330-114">Service plans determine the region used for the app datacenter, number of VMs used, and pricing tier.</span></span>

1. <span data-ttu-id="6e330-115">Erstellen Sie einen App Service-Plan, um die Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="6e330-115">Create an App Service plan to run your app.</span></span> <span data-ttu-id="6e330-116">Der Name der app und den Plan muss eindeutig sein, so ändern Sie die Zeichenfolge "12345", um eine zufällige Zahl ist.</span><span class="sxs-lookup"><span data-stu-id="6e330-116">The name of the app and plan must be unique, so change the string "12345" to a random number.</span></span> <span data-ttu-id="6e330-117">Der folgende Befehl gibt keinen Tarif oder die Details der VM-Instanzen, von Standard, erhalten Sie eine **grundlegende** Plan mit 1 **kleine** VM-Instanz.</span><span class="sxs-lookup"><span data-stu-id="6e330-117">The following command does not specify a pricing tier or VM instance details, so by default, you'll get a **Basic** plan with 1 **Small** VM instance.</span></span>

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. <span data-ttu-id="6e330-118">Stellen Sie sicher, dass der Service-Plan erfolgreich erstellt wurde, indem Sie die Pläne in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="6e330-118">Verify that the service plan was created successfully, by listing all your plans in a table.</span></span>

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a><span data-ttu-id="6e330-119">Schritte zum Erstellen einer Web-app</span><span class="sxs-lookup"><span data-stu-id="6e330-119">Steps to create a web app</span></span>
<span data-ttu-id="6e330-120">Als Nächstes erstellen Sie die Web-app in Ihrem Service-Plan.</span><span class="sxs-lookup"><span data-stu-id="6e330-120">Next, you'll create the web app in your service plan.</span></span> <span data-ttu-id="6e330-121">Sie können den Code bereitstellen, zur gleichen Zeit, aber in unserem Beispiel machen wir dies als separater Schritt.</span><span class="sxs-lookup"><span data-stu-id="6e330-121">You can deploy the code at the same time, but for our example, we'll do this as separate step.</span></span>

1. <span data-ttu-id="6e330-122">Denken Sie daran, die die Zeichenfolge "12345" in der gleichen Zufallszahl zu ändern, die Sie zuvor die Web-app zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6e330-122">Create the web app, remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. <span data-ttu-id="6e330-123">Stellen Sie sicher, dass die app erfolgreich erstellt wurde, indem Sie alle Ihre apps in einer Tabelle auflisten.</span><span class="sxs-lookup"><span data-stu-id="6e330-123">Verify that the app was created successfully, by listing all your apps in a table.</span></span>

    ```bash
    az webapp list --output table
    ```

1. <span data-ttu-id="6e330-124">Notieren Sie sich die **DefaultHostName**, Sie benötigen diesen später noch mal.</span><span class="sxs-lookup"><span data-stu-id="6e330-124">Make a note of the **DefaultHostName**, you will need this later.</span></span>

### <a name="steps-to-deploy-code-from-github"></a><span data-ttu-id="6e330-125">Schritte zum Bereitstellen von Code über GitHub</span><span class="sxs-lookup"><span data-stu-id="6e330-125">Steps to deploy code from GitHub</span></span>
1. <span data-ttu-id="6e330-126">Der letzte Schritt ist zum Bereitstellen von Code über ein GitHub-Repository in der Web-App erneut Denken Sie daran, die die Zeichenfolge "12345" in der gleichen Zufallszahl zu ändern, die Sie zuvor.</span><span class="sxs-lookup"><span data-stu-id="6e330-126">The final step is to deploy code from a GitHub repository to the Web App, again remembering to change the string "12345" to the same random number you used earlier.</span></span>
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. <span data-ttu-id="6e330-127">Kopieren Sie die folgende Url in einem Browser, um die Web-app finden Sie unter.</span><span class="sxs-lookup"><span data-stu-id="6e330-127">Copy the following url into a browser to see the web app.</span></span>
<span data-ttu-id="6e330-128">http://popupapp12345.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="6e330-128">http://popupapp12345.azurewebsites.net</span></span>

1. <span data-ttu-id="6e330-129">Die angezeigte Seite "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="6e330-129">The page display "HelloWorld!"</span></span>

1. <span data-ttu-id="6e330-130">Schließen Sie das Browserfenster.</span><span class="sxs-lookup"><span data-stu-id="6e330-130">Close the browser window.</span></span>

## <a name="summary"></a><span data-ttu-id="6e330-131">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="6e330-131">Summary</span></span>
<span data-ttu-id="6e330-132">In dieser Übung veranschaulicht ein typisches Muster für eine interaktive Azure CLI-Sitzung.</span><span class="sxs-lookup"><span data-stu-id="6e330-132">This exercise demonstrated a typical pattern for an interactive Azure CLI session.</span></span> <span data-ttu-id="6e330-133">Zuerst verwendet Sie einen standard-Befehl, um eine neue Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6e330-133">You first used a standard command to create a new resource group.</span></span> <span data-ttu-id="6e330-134">Danach haben Sie verwendet eine Reihe von Befehlen zum Bereitstellen einer Ressource (in diesem Beispiel eine Web-app) in dieser Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="6e330-134">You then used a set of commands to deploy a resource (in this example, a web app) into this resource group.</span></span> <span data-ttu-id="6e330-135">Dieser Satz von Befehlen werden einfach in einem Shell-Skript zusammengefasst, und jedes Mal ausgeführt, müssen Sie die gleiche Ressource zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6e330-135">This set of commands could easily be combined into a shell script, and executed every time you need to create the same resource.</span></span>
