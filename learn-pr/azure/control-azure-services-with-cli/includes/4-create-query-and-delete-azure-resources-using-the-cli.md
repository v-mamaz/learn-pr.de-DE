## <a name="motivation"></a><span data-ttu-id="8220e-101">Motivation</span><span class="sxs-lookup"><span data-stu-id="8220e-101">Motivation</span></span>
<span data-ttu-id="8220e-102">Mit der Azure CLI können Sie Befehle schreiben und diese sofort ausführen.</span><span class="sxs-lookup"><span data-stu-id="8220e-102">The Azure CLI lets you write commands and execute them immediately.</span></span> <span data-ttu-id="8220e-103">Beachten Sie, dass das Ziel bei der Softwareentwicklung darin besteht, neue Builds einer Web-App zum Testen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="8220e-103">Recall that the overall goal in the software development example is to deploy new builds of a web app for testing.</span></span> <span data-ttu-id="8220e-104">Hierzu wird im ersten Schritt eine Ressourcengruppe erstellt.</span><span class="sxs-lookup"><span data-stu-id="8220e-104">The first step is to create a resource group.</span></span> <span data-ttu-id="8220e-105">Denken Sie daran, dass diese Ressourcen mithilfe einer lokalen Installation der Azure CLI erstellt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8220e-105">Remember that the goal here is to create these resources using a local installation of the Azure CLI.</span></span> 

<span data-ttu-id="8220e-106">In dieser Einheit erfahren Sie, wie Sie sich mithilfe der Azure CLI bei Ihrem Azure-Abonnement anmelden und eine neue Ressource erstellen.</span><span class="sxs-lookup"><span data-stu-id="8220e-106">This unit shows you how to use the Azure CLI to sign in to your Azure subscription and create a new resource.</span></span>

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a><span data-ttu-id="8220e-107">Welche Azure-Ressourcen können unter Verwendung der Azure CLI verwaltet werden?</span><span class="sxs-lookup"><span data-stu-id="8220e-107">What Azure resources can be managed using the Azure CLI?</span></span>
<span data-ttu-id="8220e-108">Mithilfe der Azure CLI können Sie nahezu alle Aspekte jeder Azure-Ressource steuern.</span><span class="sxs-lookup"><span data-stu-id="8220e-108">The Azure CLI lets you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="8220e-109">Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory (Azure AD), Containern, Machine Learning usw. arbeiten.</span><span class="sxs-lookup"><span data-stu-id="8220e-109">You can work with resource groups, storage, virtual machines, Azure Active Directory (Azure AD), containers, machine learning, and so on.</span></span>

<span data-ttu-id="8220e-110">Befehle in der CLI sind in Gruppen und Untergruppen strukturiert.</span><span class="sxs-lookup"><span data-stu-id="8220e-110">Commands in the CLI are structured in groups and subgroups.</span></span> <span data-ttu-id="8220e-111">Jede Gruppe stellt einen von Azure bereitgestellten Dienst dar, und die Untergruppen unterteilen Befehle für diese Dienste in logische Gruppierungen.</span><span class="sxs-lookup"><span data-stu-id="8220e-111">Each group represents a service provided by Azure, and the subgroups divide commands for these services into logical groupings.</span></span> <span data-ttu-id="8220e-112">Beispielsweise enthält die Gruppe **storage** Untergruppen wie **account**, **blob**, **storage** und **queue**.</span><span class="sxs-lookup"><span data-stu-id="8220e-112">For example, the **storage** group contains subgroups including **account**, **blob**, **storage**, and **queue**.</span></span>

<span data-ttu-id="8220e-113">Wie können die benötigten Befehle ermittelt werden?</span><span class="sxs-lookup"><span data-stu-id="8220e-113">So, how do you find the particular commands you need?</span></span> <span data-ttu-id="8220e-114">Eine Möglichkeit ist die Verwendung von **az find**.</span><span class="sxs-lookup"><span data-stu-id="8220e-114">One way is to use **az find**.</span></span> <span data-ttu-id="8220e-115">Wenn Sie etwa nach Befehlen im Zusammenhang mit der Verwaltung eines **Speicherblobs** suchen möchten, verwenden Sie hierzu den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="8220e-115">For example, if you want to find commands that might help you manage a storage **blob**, you'd use the following find command:</span></span>

```bash
az find -q blob
```

<span data-ttu-id="8220e-116">Wenn Sie den Namen des gewünschten Befehls bereits kennen, kann das Argument **--help** für diesen Befehl nützlicher sein.</span><span class="sxs-lookup"><span data-stu-id="8220e-116">If you already know the name of the command you want, the **--help** argument for that command may be more useful.</span></span> <span data-ttu-id="8220e-117">Sie erhalten ausführliche Informationen zum Befehl, und für eine Befehlsgruppe wird eine Liste der verfügbaren Unterbefehle angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8220e-117">You get detailed information on the command, and for a command group, a list of the available subcommands.</span></span> <span data-ttu-id="8220e-118">In unserem Speicherbeispiel können Sie folgendermaßen eine Liste der Untergruppen und Befehle zum Verwalten von Blobspeicher abrufen:</span><span class="sxs-lookup"><span data-stu-id="8220e-118">So, with our storage example, here's how you can get a list of the subgroups and commands for managing blob storage:</span></span>

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a><span data-ttu-id="8220e-119">Erstellen einer Azure-Ressource</span><span class="sxs-lookup"><span data-stu-id="8220e-119">How to create an Azure resource</span></span>
<span data-ttu-id="8220e-120">Beim Erstellen einer neuen Azure-Ressource werden typischerweise drei Schritte durchlaufen: Verbindungsherstellung mit Ihrem Azure-Abonnement, Erstellung der Ressource und Überprüfung der erfolgreichen Erstellung (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="8220e-120">When creating a new Azure resource, there are typically three steps: connect to your Azure subscription, create the resource, and verify that creation was successful (see below).</span></span>

![Schritte zum Erstellen einer Ressource mit der Azure CLI](../media-drafts/4-create-resources-overview.png)

<span data-ttu-id="8220e-122">Jeder Schritt entspricht einem anderen Azure CLI-Befehl.</span><span class="sxs-lookup"><span data-stu-id="8220e-122">Each step corresponds to a different Azure CLI command.</span></span>

### <a name="connect"></a><span data-ttu-id="8220e-123">Verbinden</span><span class="sxs-lookup"><span data-stu-id="8220e-123">Connect</span></span>
<span data-ttu-id="8220e-124">Da Sie mit einer lokalen Installation der Azure CLI arbeiten, müssen Sie sich zunächst mithilfe des Azure CLI-Befehls **login** authentifizieren, um Azure-Befehle ausführen zu können.</span><span class="sxs-lookup"><span data-stu-id="8220e-124">Since you're working with a local install of the Azure CLI, you'll need to authenticate before you can execute Azure commands, by using the Azure CLI **login** command.</span></span> 

```bash
az login
```

<span data-ttu-id="8220e-125">Die Azure CLI verwendet typischerweise Ihren Standardbrowser, um die Seite für die Azure-Anmeldung zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="8220e-125">The Azure CLI will typically launch your default browser to open the Azure sign-in page.</span></span> <span data-ttu-id="8220e-126">Falls dies nicht funktioniert, folgen Sie den Befehlszeilenanweisungen, und geben Sie unter [https://aka.ms/devicelogin](https://aka.ms/devicelogin) einen Autorisierungscode ein.</span><span class="sxs-lookup"><span data-stu-id="8220e-126">If this doesn't work, follow the command-line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

<span data-ttu-id="8220e-127">Nach der erfolgreichen Anmeldung wird eine Verbindung mit Ihrem Azure-Abonnement hergestellt.</span><span class="sxs-lookup"><span data-stu-id="8220e-127">After a successful sign in, you'll be connected to your Azure subscription.</span></span> 

### <a name="create"></a><span data-ttu-id="8220e-128">Erstellen</span><span class="sxs-lookup"><span data-stu-id="8220e-128">Create</span></span>
<span data-ttu-id="8220e-129">Häufig müssen Sie eine neue Ressourcengruppe erstellen, bevor Sie einen neuen Azure-Dienst erstellen. Deshalb verwenden wir Ressourcengruppen als Beispiel dafür, wie Azure-Ressourcen über die CLI erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="8220e-129">You'll often need to create a new resource group before you create a new Azure service, so we'll use resource groups as an example to show how to create Azure resources from the CLI.</span></span>

<span data-ttu-id="8220e-130">Mit dem Azure CLI-Befehl **group create** wird eine Ressourcengruppe erstellt.</span><span class="sxs-lookup"><span data-stu-id="8220e-130">The Azure CLI **group create** command creates a resource group.</span></span> <span data-ttu-id="8220e-131">Sie müssen einen Namen und einen Standort angeben.</span><span class="sxs-lookup"><span data-stu-id="8220e-131">You must specify a name and location.</span></span> <span data-ttu-id="8220e-132">Der Name muss innerhalb Ihres Abonnements eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="8220e-132">The name must be unique within your subscription.</span></span> <span data-ttu-id="8220e-133">Der Standort bestimmt, wo die Metadaten für Ihre Ressourcengruppe gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="8220e-133">The location determines where the metadata for your resource group will be stored.</span></span> <span data-ttu-id="8220e-134">Sie verwenden Zeichenfolgen wie „West US“, „North Europe“ oder „West India“, um den Standort anzugeben. Alternativ können Sie aus einem Wort bestehende Äquivalente eingeben, z.B. „westus“, „northeurope“ oder „westindia“.</span><span class="sxs-lookup"><span data-stu-id="8220e-134">You use strings like "West US", "North Europe", or "West India" to specify the location; alternatively, you can use single word equivalents, such as westus, northeurope, or westindia.</span></span> <span data-ttu-id="8220e-135">Die grundlegende Syntax lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="8220e-135">The core syntax is:</span></span>

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a><span data-ttu-id="8220e-136">Überprüfen</span><span class="sxs-lookup"><span data-stu-id="8220e-136">Verify</span></span>
<span data-ttu-id="8220e-137">Für viele Azure-Ressourcen stellt die Azure CLI einen Unterbefehl **list** bereit, mit dem Ressourcendetails angezeigt werden können.</span><span class="sxs-lookup"><span data-stu-id="8220e-137">For many Azure resources, the Azure CLI provides a **list** subcommand to view resource details.</span></span> <span data-ttu-id="8220e-138">Beispielsweise können Sie mit dem Azure CLI-Befehl **group list** Ihre Azure-Ressourcengruppen auflisten.</span><span class="sxs-lookup"><span data-stu-id="8220e-138">For example, the Azure CLI **group list** command lists your Azure resource groups.</span></span> <span data-ttu-id="8220e-139">So können wir hier überprüfen, ob die Ressourcengruppe erfolgreich erstellt wurde:</span><span class="sxs-lookup"><span data-stu-id="8220e-139">This is useful here to verify whether creation of the resource group was successful:</span></span>

```bash
az group list
```

<span data-ttu-id="8220e-140">Um eine kompaktere Ansicht zu erhalten, können Sie die Ausgabe als einfache Tabelle formatieren:</span><span class="sxs-lookup"><span data-stu-id="8220e-140">To get a more concise view, you can format the output as a simple table:</span></span>

```bash
az group list --output table
```
