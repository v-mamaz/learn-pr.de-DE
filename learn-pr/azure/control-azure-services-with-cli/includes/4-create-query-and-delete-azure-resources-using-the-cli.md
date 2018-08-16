## <a name="motivation"></a><span data-ttu-id="f9b16-101">Motivation</span><span class="sxs-lookup"><span data-stu-id="f9b16-101">Motivation</span></span>
<span data-ttu-id="f9b16-102">Der Azure-Befehlszeilenschnittstelle können Sie die Befehle schreiben, und führen Sie sie.</span><span class="sxs-lookup"><span data-stu-id="f9b16-102">The Azure CLI lets you write commands and execute them immediately.</span></span> <span data-ttu-id="f9b16-103">Denken Sie daran, dass das Ziel im Software Development Beispiel besteht darin, neue Builds zum Testen einer Web-app bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="f9b16-103">Recall that the overall goal in the software development example is to deploy new builds of a web app for testing.</span></span> <span data-ttu-id="f9b16-104">Der erste Schritt ist die Erstellung eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="f9b16-104">The first step is to create a resource group.</span></span> <span data-ttu-id="f9b16-105">Denken Sie daran, dass das Ziel hierbei ist, um diese Ressourcen, die mit einer lokalen Installation der Azure-Befehlszeilenschnittstelle zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f9b16-105">Remember that the goal here is to create these resources using a local installation of the Azure CLI.</span></span> 

<span data-ttu-id="f9b16-106">Diese Einheit erfahren Sie, wie Sie mit der Azure-CLI melden Sie sich bei Ihrem Azure-Abonnement, und Erstellen einer neuen Ressource.</span><span class="sxs-lookup"><span data-stu-id="f9b16-106">This unit shows you how to use the Azure CLI to log in to your Azure subscription and create a new resource.</span></span>

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a><span data-ttu-id="f9b16-107">Welche Azure-Ressourcen können mithilfe der Azure CLI verwaltet werden?</span><span class="sxs-lookup"><span data-stu-id="f9b16-107">What Azure resources can be managed using the Azure CLI?</span></span>
<span data-ttu-id="f9b16-108">Der Azure-Befehlszeilenschnittstelle können Sie fast jeden Aspekt aller Azure-Ressourcen zu steuern.</span><span class="sxs-lookup"><span data-stu-id="f9b16-108">The Azure CLI lets you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="f9b16-109">Sie können mit Ressourcengruppen, Speicher, virtuelle Computer, Azure Active Directory, Container, Machine Learning und So weiter arbeiten.</span><span class="sxs-lookup"><span data-stu-id="f9b16-109">You can work with resource groups, storage, virtual machines, Azure Active Directory, containers, machine learning, and so on.</span></span>

<span data-ttu-id="f9b16-110">Befehle in der CLI sind in Gruppen und Untergruppen aufgebaut.</span><span class="sxs-lookup"><span data-stu-id="f9b16-110">Commands in the CLI are structured in groups and subgroups.</span></span> <span data-ttu-id="f9b16-111">Jede Gruppe stellt einen von Azure bereitgestellten Dienst dar, und die Untergruppen unterteilen Befehle für diese Dienste in logische Gruppierungen.</span><span class="sxs-lookup"><span data-stu-id="f9b16-111">Each group represents a service provided by Azure, and the subgroups divide commands for these services into logical groupings.</span></span> <span data-ttu-id="f9b16-112">Z. B. die **Storage** Gruppe enthält, einschließlich Untergruppen **Konto**, **Blob**, **Storage**, und **Warteschlange**.</span><span class="sxs-lookup"><span data-stu-id="f9b16-112">For example, the **storage** group contains subgroups including **account**, **blob**, **storage**, and **queue**.</span></span>

<span data-ttu-id="f9b16-113">Also wie finden Sie die bestimmte Befehle, die Sie benötigen?</span><span class="sxs-lookup"><span data-stu-id="f9b16-113">So, how do you find the particular commands you need?</span></span> <span data-ttu-id="f9b16-114">Eine Möglichkeit ist die Verwendung **az Find**.</span><span class="sxs-lookup"><span data-stu-id="f9b16-114">One way is to use **az find**.</span></span> <span data-ttu-id="f9b16-115">Angenommen, Sie suchen, Befehle, mit denen Sie einen Speicher verwalten möchten **Blob**, würden Sie die folgenden Find-Befehl verwenden:</span><span class="sxs-lookup"><span data-stu-id="f9b16-115">For example, if you want to find commands that might help you manage a storage **blob**, you'd use the following find command:</span></span>

```bash
az find -q blob
```

<span data-ttu-id="f9b16-116">Wenn Sie bereits den Namen des Befehls sollen wissen, die **– Hilfe** Argument für diesen Befehl kann nützlicher sein.</span><span class="sxs-lookup"><span data-stu-id="f9b16-116">If you already know the name of the command you want, the **--help** argument for that command may be more useful.</span></span> <span data-ttu-id="f9b16-117">Sie erhalten ausführliche Informationen zum Befehl "", und klicken Sie für eine Befehlsgruppe, die eine Liste der verfügbaren Unterbefehle.</span><span class="sxs-lookup"><span data-stu-id="f9b16-117">You get detailed information on the command, and for a command group, a list of the available subcommands.</span></span> <span data-ttu-id="f9b16-118">Mit unserem Beispiel Speicher also hier, wie Sie eine Liste mit den Untergruppen und Befehle zum Verwalten von BLOB-Speicher abrufen können</span><span class="sxs-lookup"><span data-stu-id="f9b16-118">So, with our storage example, here's how you can get a list of the subgroups and commands for managing blob storage</span></span>

```bash
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a><span data-ttu-id="f9b16-119">Vorgehensweise: erstellen eine Azure-Ressource</span><span class="sxs-lookup"><span data-stu-id="f9b16-119">How to create an Azure resource</span></span>
<span data-ttu-id="f9b16-120">Wenn Sie eine neue Azure-Ressource zu erstellen, in der Regel drei Schritte sind: eine Verbindung mit Ihrem Azure-Abonnement herstellen, erstellen Sie die Ressource, und stellen Sie sicher, dass die Erstellung erfolgreich (siehe unten) wurde.</span><span class="sxs-lookup"><span data-stu-id="f9b16-120">When creating a new Azure resource, there are typically three steps: connect to your Azure subscription, create the resource, and verify that creation was successful (see below).</span></span>

![Schritte zum Erstellen einer Ressource, die mithilfe der Azure CLI](../images/create-resources-overview.png)

<span data-ttu-id="f9b16-122">Jeder Schritt entspricht zu einem anderen Azure-CLI-Befehl.</span><span class="sxs-lookup"><span data-stu-id="f9b16-122">Each step corresponds to a different Azure CLI command.</span></span>

### <a name="connect"></a><span data-ttu-id="f9b16-123">Verbinden</span><span class="sxs-lookup"><span data-stu-id="f9b16-123">Connect</span></span>
<span data-ttu-id="f9b16-124">Da Sie mit einer lokalen Installation der Azure-Befehlszeilenschnittstelle verwenden, müssen Sie authentifizieren, bevor Sie Azure-Befehle ausführen können, mithilfe der Azure-Befehlszeilenschnittstelle **Anmeldung** Befehl.</span><span class="sxs-lookup"><span data-stu-id="f9b16-124">Since you're working with a local install of the Azure CLI, you'll need to authenticate before you can execute Azure commands, by using the Azure CLI **login** command.</span></span> 

```bash
az login
```

<span data-ttu-id="f9b16-125">Der Azure-Befehlszeilenschnittstelle startet den Standardbrowser zum Öffnen von Azure in der Regel Anmeldeseite.</span><span class="sxs-lookup"><span data-stu-id="f9b16-125">The Azure CLI will typically launch your default browser to open the Azure sign in page.</span></span> <span data-ttu-id="f9b16-126">Wenn dies nicht funktioniert, befolgen Sie die Anweisungen über die Befehlszeile, und geben Sie einen Autorisierungscode an [ https://aka.ms/devicelogin ](https://aka.ms/devicelogin).</span><span class="sxs-lookup"><span data-stu-id="f9b16-126">If this doesn't work, follow the command line instructions and enter an authorization code at [https://aka.ms/devicelogin](https://aka.ms/devicelogin).</span></span>

<span data-ttu-id="f9b16-127">Nach ein erfolgreicher Anmeldung werden Sie mit Ihrem Azure-Abonnement verbunden sein.</span><span class="sxs-lookup"><span data-stu-id="f9b16-127">After a succesful sign in, you'll be connected to your Azure subscription.</span></span> 

### <a name="create"></a><span data-ttu-id="f9b16-128">Erstellen</span><span class="sxs-lookup"><span data-stu-id="f9b16-128">Create</span></span>
<span data-ttu-id="f9b16-129">Häufig müssen Sie eine neue Ressourcengruppe zu erstellen, bevor Sie einen neuen Dienst erstellen, deshalb Ressourcengruppen als Beispiel wir verwenden veranschaulichen, wie Sie Azure-Ressourcen über die Befehlszeilenschnittstelle erstellen.</span><span class="sxs-lookup"><span data-stu-id="f9b16-129">You'll often need to create a new resource group before you create a new Azure service so we'll use resource groups as example to show how to create Azure resources from the CLI.</span></span>

<span data-ttu-id="f9b16-130">Der Azure-Befehlszeilenschnittstelle **Gruppe erstellen** Befehl erstellt eine Ressourcengruppe aus.</span><span class="sxs-lookup"><span data-stu-id="f9b16-130">The Azure CLI **group create** command creates a resource group.</span></span> <span data-ttu-id="f9b16-131">Sie müssen einen Namen und Speicherort angeben.</span><span class="sxs-lookup"><span data-stu-id="f9b16-131">You must specify a name and location.</span></span> <span data-ttu-id="f9b16-132">Der Name muss innerhalb Ihres Abonnements eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="f9b16-132">The name must be unique within your subscription.</span></span> <span data-ttu-id="f9b16-133">Die Position bestimmt, wo die Metadaten für Ihre Ressourcengruppe gespeichert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f9b16-133">The location determines where the metadata for your resource group will be stored.</span></span> <span data-ttu-id="f9b16-134">Sie verwenden Zeichenfolgen wie "USA, Westen", "Nordeuropa" und "Indien (Westen)", um den Speicherort anzugeben. Alternativ können Sie einzelne Wort-Entsprechungen, z. B. USA, Westen, Northeurope oder Westindia verwenden.</span><span class="sxs-lookup"><span data-stu-id="f9b16-134">You use strings like "West US", "North Europe", or "West India" to specify the location; alternatively, you can use single word equivalents, such as westus, northeurope, or westindia.</span></span> <span data-ttu-id="f9b16-135">Die Core-Syntax lautet:</span><span class="sxs-lookup"><span data-stu-id="f9b16-135">The core syntax is:</span></span>

```bash
az group create --name <name> --location <location>
```

### <a name="verify"></a><span data-ttu-id="f9b16-136">Überprüfen</span><span class="sxs-lookup"><span data-stu-id="f9b16-136">Verify</span></span>
<span data-ttu-id="f9b16-137">Für viele Azure-Ressourcen, die Azure-Befehlszeilenschnittstelle bietet eine **Liste** Unterbefehl Ressourcendetails anzeigen.</span><span class="sxs-lookup"><span data-stu-id="f9b16-137">For many Azure resources, Azure CLI provides a **list** subcommand to view resource details.</span></span> <span data-ttu-id="f9b16-138">Z. B. der Azure-Befehlszeilenschnittstelle **Gruppenliste** Befehl Listet Ihre Azure-Ressourcengruppen.</span><span class="sxs-lookup"><span data-stu-id="f9b16-138">For example, the Azure CLI **group list** command lists your Azure resource groups.</span></span> <span data-ttu-id="f9b16-139">Dies ist hier hilfreich zu überprüfen, ob die Erstellung der Ressourcengruppe erfolgreich war:</span><span class="sxs-lookup"><span data-stu-id="f9b16-139">This is useful here to verify whether creation of the resource group was successful:</span></span>

```bash
az group list
```

<span data-ttu-id="f9b16-140">Um eine präzisere Ansicht zu erhalten, können Sie die Ausgabe als eine einfache Tabelle formatieren:</span><span class="sxs-lookup"><span data-stu-id="f9b16-140">To get a more concise view, you can format the output as a simple table:</span></span>

```bash
az group list --output table
```
