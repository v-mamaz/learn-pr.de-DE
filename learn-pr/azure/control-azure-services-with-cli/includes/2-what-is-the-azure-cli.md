<span data-ttu-id="734ed-101">Die Azure CLI ist ein Befehlszeilenprogramm, über das Sie eine Verbindung mit Azure herstellen und Verwaltungsbefehle für Azure-Ressourcen ausführen können.</span><span class="sxs-lookup"><span data-stu-id="734ed-101">The Azure CLI is a command-line program to connect to Azure and execute administrative commands on Azure resources.</span></span> <span data-ttu-id="734ed-102">Die Azure CLI wird unter Linux, macOS und Windows ausgeführt und ermöglicht es Administratoren und Entwicklern, ihre Befehle über ein Terminal oder eine Eingabeaufforderung (oder ein Skript) anstelle eines Webbrowsers auszuführen.</span><span class="sxs-lookup"><span data-stu-id="734ed-102">It runs on Linux, macOS, and Windows and allows administrators and developers to execute their commands through a terminal or command line prompt (or script!) instead of a web browser.</span></span> <span data-ttu-id="734ed-103">Zum Neustarten einer VM würden Sie beispielsweise einen Befehl wie den folgenden verwenden:</span><span class="sxs-lookup"><span data-stu-id="734ed-103">For example, to restart a virtual machine (VM), you would use a command like the following:</span></span>

 ```azurecli
 az vm restart -g MyResourceGroup -n MyVm
 ```

<span data-ttu-id="734ed-104">Die Azure CLI bietet plattformübergreifende Befehlszeilentools zum Verwalten von Azure-Ressourcen. Sie kann lokal auf Linux-, Mac- und Windows-Computern installiert werden.</span><span class="sxs-lookup"><span data-stu-id="734ed-104">The Azure CLI provides cross-platform command-line tools for managing Azure resources, and can be installed locally on Linux, Mac, or Windows computers.</span></span> <span data-ttu-id="734ed-105">Die Azure CLI kann mit Azure Cloud Shell auch über Browser verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="734ed-105">The Azure CLI can also be used from a browser through the Azure Cloud Shell.</span></span> <span data-ttu-id="734ed-106">In beiden Fällen kann sie interaktiv oder mit Skripts verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="734ed-106">In both cases, it can be used interactively or scripted.</span></span> <span data-ttu-id="734ed-107">Bei der interaktiven Nutzung starten Sie zunächst eine Shell wie cmd.exe unter Windows oder Bash unter Linux oder macOS, und geben Sie dann den Befehl bei der Eingabeaufforderung der Shell ein.</span><span class="sxs-lookup"><span data-stu-id="734ed-107">For interactive use, you first launch a shell such as cmd.exe on Windows or Bash on Linux or macOS and then issue the command at the shell prompt.</span></span> <span data-ttu-id="734ed-108">Um sich wiederholende Aufgaben zu automatisieren, stellen Sie die CLI-Befehle mit der Syntax Ihrer ausgewählten Shell in einem Shellskript zusammen und führen dieses Skript dann aus.</span><span class="sxs-lookup"><span data-stu-id="734ed-108">To automate repetitive tasks, you assemble the CLI commands into a shell script using the script syntax of your chosen shell and then execute the script.</span></span>

## <a name="how-to-install-azure-cli"></a><span data-ttu-id="734ed-109">Installieren der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="734ed-109">How to install Azure CLI</span></span>

<span data-ttu-id="734ed-110">Verwenden Sie unter Linux und macOS einen Paket-Manager, um PowerShell Core zu installieren.</span><span class="sxs-lookup"><span data-stu-id="734ed-110">On both Linux and macOS, you use a package manager to install PowerShell Core.</span></span> <span data-ttu-id="734ed-111">Der empfohlene Paket-Manager unterscheidet sich je nach Betriebssystem und Distribution:</span><span class="sxs-lookup"><span data-stu-id="734ed-111">The recommended package manager differs by OS and distribution:</span></span>
- <span data-ttu-id="734ed-112">Linux: **apt-get** unter Ubuntu, **yum** unter Red Hat und **zypper** unter OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="734ed-112">Linux: **apt-get** on Ubuntu, **yum** on Red Hat, and **zypper** on OpenSUSE</span></span>
- <span data-ttu-id="734ed-113">Mac: **Homebrew**</span><span class="sxs-lookup"><span data-stu-id="734ed-113">Mac: **Homebrew**</span></span>

<span data-ttu-id="734ed-114">Die Azure CLI ist im Microsoft-Repository verfügbar, sodass Sie zuerst dieses Repository dem Paket-Manager hinzufügen müssen.</span><span class="sxs-lookup"><span data-stu-id="734ed-114">The Azure CLI is available in the Microsoft repository, so you'll first need to add that repository to your package manager.</span></span>

<span data-ttu-id="734ed-115">Installieren Sie die Azure CLI unter Windows, indem Sie eine MSI-Datei herunterladen und ausführen.</span><span class="sxs-lookup"><span data-stu-id="734ed-115">On Windows, you install the Azure CLI by downloading and running an MSI file.</span></span>

## <a name="using-the-azure-cli-in-scripts"></a><span data-ttu-id="734ed-116">Verwenden der Azure CLI in Skripts</span><span class="sxs-lookup"><span data-stu-id="734ed-116">Using the Azure CLI in scripts</span></span>

<span data-ttu-id="734ed-117">Wenn Sie Azure CLI-Befehle in Skripts verwenden möchten, müssen Sie die möglichen Probleme in Zusammenhang mit der „Shell“ oder der Ausführungsumgebung kennen.</span><span class="sxs-lookup"><span data-stu-id="734ed-117">If you want to use the Azure CLI commands in scripts, you need to be aware of any issues around the "shell" or environment used for running the script.</span></span> <span data-ttu-id="734ed-118">Beispielsweise werden Variablen in einer Bash-Shell mithilfe der folgenden Syntax festgelegt:</span><span class="sxs-lookup"><span data-stu-id="734ed-118">For example, in a bash shell, the following syntax is used when setting variables:</span></span>

 ```azurecli
 variable="value"
 variable=integer
 ```

<span data-ttu-id="734ed-119">Wenn Sie eine PowerShell-Umgebung zum Ausführen von Azure CLI-Skripts verwenden, müssen Sie diese Syntax für Variablen verwenden:</span><span class="sxs-lookup"><span data-stu-id="734ed-119">If you use a PowerShell environment for running Azure CLI scripts, you'll need to use this syntax for variables:</span></span>

 ```powershell
 $variable="value"
 $variable=integer
 ```

## <a name="summary"></a><span data-ttu-id="734ed-120">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="734ed-120">Summary</span></span>

<span data-ttu-id="734ed-121">Sie müssen die Azure CLI installieren, um mit ihr Azure-Ressourcen von einem lokalen Computer aus zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="734ed-121">The Azure CLI must be installed before it can be used to manage Azure resources from a local computer.</span></span> <span data-ttu-id="734ed-122">Die Installation ist für Windows, Linux und macOS unterschiedlich, allerdings gelten die Befehle nach der Installation plattformübergreifend.</span><span class="sxs-lookup"><span data-stu-id="734ed-122">The installation steps vary for Windows, Linux, and macOS, but once installed, the commands are common across platforms.</span></span> 
