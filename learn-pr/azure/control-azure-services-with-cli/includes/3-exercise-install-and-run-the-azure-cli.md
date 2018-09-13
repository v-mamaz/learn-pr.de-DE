<span data-ttu-id="4b2d2-101">Installieren Sie die Azure CLI auf Ihrem lokalen Computer, und führen Sie dann einen einfachen Befehl aus, um die Installation zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-101">Let's install the Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> <span data-ttu-id="4b2d2-102">Mit welcher Methode Sie die Azure CLI installieren, hängt vom Betriebssystem Ihres Computers ab.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-102">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="4b2d2-103">Wählen Sie die entsprechenden Schritte für Ihr Betriebssystem aus.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-103">Please choose the steps for your operating system.</span></span>

> [!NOTE]
> <span data-ttu-id="4b2d2-104">In dieser Übung lernen Sie die lokale Installation des Azure CLI-Tools kennen.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-104">This exercise guides you through installing the Azure CLI tool locally.</span></span> <span data-ttu-id="4b2d2-105">Im restlichen Teil des Moduls verwenden Sie die Azure Cloud Shell, sodass Sie die kostenlose Abonnementsupport in Microsoft Learn nutzen können.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-105">The remainder of the module will use the Azure Cloud Shell so you can leverage the free subscription support in Microsoft Learn.</span></span> <span data-ttu-id="4b2d2-106">Sie können diese Übung als optionale Aktivität betrachten und ggf. nur die Anweisungen lesen.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-106">You can consider this exercise as an optional activity and just review the instructions if you prefer.</span></span>

<span data-ttu-id="4b2d2-107">::: zone pivot="linux"</span><span class="sxs-lookup"><span data-stu-id="4b2d2-107">::: zone pivot="linux"</span></span>

### <a name="linux"></a><span data-ttu-id="4b2d2-108">Linux</span><span class="sxs-lookup"><span data-stu-id="4b2d2-108">Linux</span></span>

<span data-ttu-id="4b2d2-109">Hier installieren Sie die Azure CLI unter **Ubuntu Linux** mit dem Advanced Packaging Tool (**apt**) und der Bash-Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-109">Here you will install the Azure CLI on **Ubuntu Linux** using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!TIP]
> <span data-ttu-id="4b2d2-110">Die unten aufgeführten Befehle gelten für Ubuntu-Version 18.04.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-110">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="4b2d2-111">Für andere Versionen und Distributionen von Linux gelten andere Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-111">Other versions and distributions of Linux have different instructions.</span></span> <span data-ttu-id="4b2d2-112">Falls Sie eine andere Linux-Version verwenden, finden Sie entsprechende Informationen in der [offiziellen Dokumentation](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4b2d2-112">Check the [official documentation](https://docs.microsoft.com/cli/azure/install-azure-cli) if you are using a different Linux version.</span></span>

1. <span data-ttu-id="4b2d2-113">Bearbeiten Sie Ihre Quellenliste, sodass das Microsoft-Repository registriert wird und der Paket-Manager das Azure CLI-Paket ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-113">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

1. <span data-ttu-id="4b2d2-114">Importieren Sie den Verschlüsselungsschlüssel für das Microsoft Ubuntu-Repository.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-114">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="4b2d2-115">So kann der Paket-Manager sicherstellen, dass das Azure CLI-Paket, das Sie installieren, wirklich von Microsoft stammt.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-115">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="4b2d2-116">Installieren Sie die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-116">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

<span data-ttu-id="4b2d2-117">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="4b2d2-117">::: zone-end</span></span>

<span data-ttu-id="4b2d2-118">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="4b2d2-118">::: zone pivot="macos"</span></span>

### <a name="macos"></a><span data-ttu-id="4b2d2-119">macOS</span><span class="sxs-lookup"><span data-stu-id="4b2d2-119">macOS</span></span>

<span data-ttu-id="4b2d2-120">Hier installieren Sie die Azure CLI mit dem Homebrew-Paket-Manager unter macOS.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-120">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b2d2-121">Wenn der Befehl **brew** nicht verfügbar ist, müssen Sie möglicherweise den Homebrew-Paket-Manager installieren.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-121">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="4b2d2-122">Informationen dazu finden Sie auf der [Website von Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="4b2d2-122">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="4b2d2-123">Aktualisieren Sie Ihr brew-Repository, um sicherzustellen, dass Sie das neueste Azure CLI-Paket abrufen.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-123">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```

1. <span data-ttu-id="4b2d2-124">Installieren Sie die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-124">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

<span data-ttu-id="4b2d2-125">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="4b2d2-125">::: zone-end</span></span>

<span data-ttu-id="4b2d2-126">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="4b2d2-126">::: zone pivot="windows"</span></span>

### <a name="windows"></a><span data-ttu-id="4b2d2-127">Windows</span><span class="sxs-lookup"><span data-stu-id="4b2d2-127">Windows</span></span>

<span data-ttu-id="4b2d2-128">Hier installieren Sie die Azure CLI mit dem Microsoft Installer (MSI) unter Windows.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-128">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="4b2d2-129">Wechseln Sie zu „[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)“, und klicken Sie im Sicherheitsdialogfeld des Browsers auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-129">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="4b2d2-130">Akzeptieren Sie die Lizenzbedingungen im Installer, und klicken Sie dann auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-130">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="4b2d2-131">Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-131">In the **User Account Control** dialog, select **Yes**.</span></span>

<span data-ttu-id="4b2d2-132">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="4b2d2-132">::: zone-end</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="4b2d2-133">Ausführen der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4b2d2-133">Running the Azure CLI</span></span>

<span data-ttu-id="4b2d2-134">Unter Linux und macOS führen Sie die Azure CLI aus, indem Sie eine Bash-Shell öffnen. Unter Windows führen Sie die CLI von der Eingabeaufforderung oder über PowerShell aus.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-134">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="4b2d2-135">Starten Sie die Azure CLI, und überprüfen Sie Ihre Installation, indem Sie die Versionsprüfung ausführen.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-135">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```azurecli
    az --version
    ```

<span data-ttu-id="4b2d2-136">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="4b2d2-136">::: zone pivot="windows"</span></span>

> [!TIP]
> <span data-ttu-id="4b2d2-137">Die Ausführung der Azure CLI über PowerShell bietet im Vergleich zur Ausführung der Azure CLI über die Windows-Eingabeaufforderung einige Vorteile.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-137">Running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the Windows command prompt.</span></span> <span data-ttu-id="4b2d2-138">Zusätzlich zu den in der Eingabeaufforderung verfügbaren Features stellt PowerShell weitere Features zur Vervollständigung mit der TAB-Taste zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-138">PowerShell provides additional tab completion features over those available from the command prompt.</span></span> 

<span data-ttu-id="4b2d2-139">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="4b2d2-139">::: zone-end</span></span>

## <a name="summary"></a><span data-ttu-id="4b2d2-140">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="4b2d2-140">Summary</span></span>

<span data-ttu-id="4b2d2-141">Sie richten Ihre lokalen Computer für die Verwaltung von Azure-Ressourcen mithilfe der Azure CLI ein.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-141">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="4b2d2-142">Sie können die Azure CLI jetzt lokal verwenden, um Befehle einzugeben oder Skripts auszuführen.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-142">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="4b2d2-143">Die Azure CLI leitet Ihre Befehle an die Azure-Rechenzentren weiter, wo sie in Ihren Azure-Abonnements ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="4b2d2-143">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>