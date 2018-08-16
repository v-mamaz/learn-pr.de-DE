
<span data-ttu-id="4fdcb-101">Sie werden in dieser Übung installieren Azure-Befehlszeilenschnittstelle auf Ihrem lokalen Computer und führen Sie dann einen einfachen Befehl für Ihre Installation zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-101">In this exercise, you will install Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> 

## <a name="installing-the-azure-cli"></a><span data-ttu-id="4fdcb-102">Installieren der Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="4fdcb-102">Installing the Azure CLI</span></span>
<span data-ttu-id="4fdcb-103">Die Methode, die Sie für die Installation der Azure-Befehlszeilenschnittstelle verwenden, hängt von das Betriebssystem des Computers ab.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-103">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="4fdcb-104">Wählen Sie die Schritte für Ihr Betriebssystem aus.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-104">Please choose the steps for your operating system.</span></span>

### <a name="linux"></a><span data-ttu-id="4fdcb-105"> Linux</span><span class="sxs-lookup"><span data-stu-id="4fdcb-105">Linux</span></span>
<span data-ttu-id="4fdcb-106">Hier installieren Sie Azure-Befehlszeilenschnittstelle unter Ubuntu Linux über das Advanced Packaging Tool (**apt**) und die Bash-Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-106">Here you will install Azure CLI on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!NOTE] <span data-ttu-id="4fdcb-107">Die unten aufgeführten Befehle sind für Ubuntu-Version 18.04.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="4fdcb-108">Wenn Sie eine andere Version von Ubuntu verwenden, müssen Sie ein anderes Repository hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="4fdcb-109">Weitere Informationen finden Sie [Installieren der Azure CLI 2.0 mit apt](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt).</span><span class="sxs-lookup"><span data-stu-id="4fdcb-109">For details see [Install Azure CLI 2.0 with apt](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt).</span></span>

1. <span data-ttu-id="4fdcb-110">Ändern Sie die Quellenliste, sodass das Microsoft-Repository registriert ist und der Paket-Manager kann das Azure-CLI-Paket suchen.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-110">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. <span data-ttu-id="4fdcb-111">Importieren Sie den Verschlüsselungsschlüssel für das Microsoft-Ubuntu-Repository.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-111">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="4fdcb-112">Das Paket dadurch Manager, um sicherzustellen, dass das Azure-CLI-Paket, die, das Sie installieren, von Microsoft stammt.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-112">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="4fdcb-113">Installieren der Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-113">Install Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a><span data-ttu-id="4fdcb-114">macOS</span><span class="sxs-lookup"><span data-stu-id="4fdcb-114">macOS</span></span>
<span data-ttu-id="4fdcb-115">Hier installieren Sie Azure CLI unter MacOS unter Verwendung der Homebrew-Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-115">Here you will install Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT] <span data-ttu-id="4fdcb-116">Wenn die **brew** Befehl nicht verfügbar ist, müssen Sie möglicherweise die Homebrew-Paket-Manager zu installieren.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-116">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="4fdcb-117">Weitere Informationen finden Sie die [Homebrew-Website](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="4fdcb-117">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="4fdcb-118">Aktualisieren Sie Ihre Brew-Repository, um sicherzustellen, dass Sie das neueste Azure CLI-Paket erhalten.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-118">Update your brew repository, to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```
1. <span data-ttu-id="4fdcb-119">Installieren der Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-119">Install Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a><span data-ttu-id="4fdcb-120"> Windows</span><span class="sxs-lookup"><span data-stu-id="4fdcb-120">Windows</span></span>
<span data-ttu-id="4fdcb-121">Hier installieren Sie Azure-Befehlszeilenschnittstelle für Windows, die mit dem MSI-Installer.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-121">Here you will install Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="4fdcb-122">Wechseln Sie zu [ https://aka.ms/installazurecliwindows ](https://aka.ms/installazurecliwindows), und klicken Sie in das Dialogfeld Sicherheit Browser auf **ausführen**.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-122">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="4fdcb-123">Im Installationsprogramm akzeptiere die Lizenzbedingungen, und klicken Sie dann auf **installieren**.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-123">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="4fdcb-124">In der **User Account Control** wählen Sie im Dialogfeld **Ja**.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-124">In the **User Account Control** dialog, select **Yes**.</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="4fdcb-125">Der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4fdcb-125">Running the Azure CLI</span></span>
<span data-ttu-id="4fdcb-126">Sie haben die Azure CLI ausführen, durch Öffnen einer Bash-Shell (Linux und MacOS) oder über die Eingabeaufforderung oder PowerShell (Windows).</span><span class="sxs-lookup"><span data-stu-id="4fdcb-126">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the Command Prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="4fdcb-127">Starten Sie die Azure-Befehlszeilenschnittstelle, und überprüfen Sie die Installation, indem Sie die Überprüfung der Version ausführen.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-127">Start the Azure CLI and verify your installation, by running the version check.</span></span>

    ```bash
    az --version
    ```

> [!NOTE] <span data-ttu-id="4fdcb-128">In Windows hat das Ausführen der Azure-Befehlszeilenschnittstelle über PowerShell einige Vorteile gegenüber der Azure-Befehlszeilenschnittstelle ausführen, an der Eingabeaufforderung aus; Beispielsweise bietet PowerShell zusätzliche Registerkarte Abschluss Features im Vergleich zu, von der Befehlszeile aus.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-128">In Windows, running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the Command Prompt; for example, PowerShell provides additional tab completion features over those available from the Command Prompt.</span></span> 

## <a name="summary"></a><span data-ttu-id="4fdcb-129">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="4fdcb-129">Summary</span></span>
<span data-ttu-id="4fdcb-130">Sie richten Sie Ihre lokalen Computer zum Verwalten von Azure-Ressourcen mit Azure-Befehlszeilenschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-130">You setup your local machines to administer Azure resources with Azure CLI.</span></span> <span data-ttu-id="4fdcb-131">Sie können jetzt Azure CLI lokal verwenden, geben Befehle oder Skripts ausführen.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-131">You can now use Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="4fdcb-132">Azure-Befehlszeilenschnittstelle wird Ihre Befehle aus, um den Azure-Rechenzentren weitergeleitet, wo sie in Ihrem Azure-Abonnement ausgeführt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="4fdcb-132">Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>
