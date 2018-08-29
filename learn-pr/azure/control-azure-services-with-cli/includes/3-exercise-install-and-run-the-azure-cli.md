
<span data-ttu-id="bb61b-101">In dieser Übung installieren Sie die Azure CLI auf Ihrem lokalen Computer und führen dann einen einfachen Befehl aus, um die Installation zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="bb61b-101">In this exercise, you will install the Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> 

## <a name="installing-the-azure-cli"></a><span data-ttu-id="bb61b-102">Installieren der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb61b-102">Installing the Azure CLI</span></span>
<span data-ttu-id="bb61b-103">Mit welcher Methode Sie die Azure CLI installieren, hängt vom Betriebssystem Ihres Computers ab.</span><span class="sxs-lookup"><span data-stu-id="bb61b-103">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="bb61b-104">Wählen Sie die entsprechenden Schritte für Ihr Betriebssystem aus.</span><span class="sxs-lookup"><span data-stu-id="bb61b-104">Please choose the steps for your operating system.</span></span>

### <a name="linux"></a><span data-ttu-id="bb61b-105">Linux</span><span class="sxs-lookup"><span data-stu-id="bb61b-105">Linux</span></span>
<span data-ttu-id="bb61b-106">Hier installieren Sie die Azure CLI unter Ubuntu Linux mit dem Advanced Packaging Tool (**apt**) und der Bash-Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="bb61b-106">Here you will install the Azure CLI on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!NOTE]
> <span data-ttu-id="bb61b-107">Die unten aufgeführten Befehle gelten für Ubuntu, Version 18.04.</span><span class="sxs-lookup"><span data-stu-id="bb61b-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="bb61b-108">Wenn Sie eine andere Ubuntu-Version verwenden, müssen Sie ein anderes Repository hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="bb61b-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="bb61b-109">Details finden Sie unter [Installieren der Azure CLI 2.0 mit apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span><span class="sxs-lookup"><span data-stu-id="bb61b-109">For details see [Install the Azure CLI 2.0 with apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span></span>

1. <span data-ttu-id="bb61b-110">Bearbeiten Sie Ihre Quellenliste, sodass das Microsoft-Repository registriert wird und der Paket-Manager das Azure CLI-Paket ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="bb61b-110">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. <span data-ttu-id="bb61b-111">Importieren Sie den Verschlüsselungsschlüssel für das Microsoft Ubuntu-Repository.</span><span class="sxs-lookup"><span data-stu-id="bb61b-111">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="bb61b-112">So kann der Paket-Manager sicherstellen, dass das Azure CLI-Paket, das Sie installieren, wirklich von Microsoft stammt.</span><span class="sxs-lookup"><span data-stu-id="bb61b-112">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="bb61b-113">Installieren Sie die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bb61b-113">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a><span data-ttu-id="bb61b-114">macOS</span><span class="sxs-lookup"><span data-stu-id="bb61b-114">macOS</span></span>
<span data-ttu-id="bb61b-115">Hier installieren Sie die Azure CLI mit dem Homebrew-Paket-Manager unter macOS.</span><span class="sxs-lookup"><span data-stu-id="bb61b-115">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb61b-116">Wenn der Befehl **brew** nicht verfügbar ist, müssen Sie möglicherweise den Homebrew-Paket-Manager installieren.</span><span class="sxs-lookup"><span data-stu-id="bb61b-116">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="bb61b-117">Informationen dazu finden Sie auf der [Website von Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="bb61b-117">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="bb61b-118">Aktualisieren Sie Ihr brew-Repository, um sicherzustellen, dass Sie das neueste Azure CLI-Paket abrufen.</span><span class="sxs-lookup"><span data-stu-id="bb61b-118">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```
1. <span data-ttu-id="bb61b-119">Installieren Sie die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="bb61b-119">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a><span data-ttu-id="bb61b-120">Windows</span><span class="sxs-lookup"><span data-stu-id="bb61b-120">Windows</span></span>
<span data-ttu-id="bb61b-121">Hier installieren Sie die Azure CLI mit dem Microsoft Installer (MSI) unter Windows.</span><span class="sxs-lookup"><span data-stu-id="bb61b-121">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="bb61b-122">Wechseln Sie zu „[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)“, und klicken Sie im Sicherheitsdialogfeld des Browsers auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="bb61b-122">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="bb61b-123">Akzeptieren Sie die Lizenzbedingungen im Installer, und klicken Sie dann auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="bb61b-123">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="bb61b-124">Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="bb61b-124">In the **User Account Control** dialog, select **Yes**.</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="bb61b-125">Ausführen der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb61b-125">Running the Azure CLI</span></span>
<span data-ttu-id="bb61b-126">Unter Linux und macOS führen Sie die Azure CLI aus, indem Sie eine Bash-Shell öffnen. Unter Windows führen Sie die CLI von der Eingabeaufforderung oder über PowerShell aus.</span><span class="sxs-lookup"><span data-stu-id="bb61b-126">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="bb61b-127">Starten Sie die Azure CLI, und überprüfen Sie Ihre Installation, indem Sie die Versionsprüfung ausführen.</span><span class="sxs-lookup"><span data-stu-id="bb61b-127">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```bash
    az --version
    ```

> [!NOTE]
> <span data-ttu-id="bb61b-128">Unter Windows bietet die Ausführung der Azure CLI von PowerShell einige Vorteile gegenüber der Ausführung von der Eingabeaufforderung: PowerShell bietet beispielsweise mehr Features zum Vervollständigen per TABULATORTASTE als die Eingabeaufforderung.</span><span class="sxs-lookup"><span data-stu-id="bb61b-128">In Windows, running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the command prompt; for example, PowerShell provides additional tab completion features over those available from the command prompt.</span></span> 

## <a name="summary"></a><span data-ttu-id="bb61b-129">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="bb61b-129">Summary</span></span>
<span data-ttu-id="bb61b-130">Sie richten Ihre lokalen Computer für die Verwaltung von Azure-Ressourcen mithilfe der Azure CLI ein.</span><span class="sxs-lookup"><span data-stu-id="bb61b-130">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="bb61b-131">Sie können die Azure CLI jetzt lokal verwenden, um Befehle einzugeben oder Skripts auszuführen.</span><span class="sxs-lookup"><span data-stu-id="bb61b-131">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="bb61b-132">Die Azure CLI leitet Ihre Befehle an die Azure-Rechenzentren weiter, wo sie in Ihren Azure-Abonnements ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="bb61b-132">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>
