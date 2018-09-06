---
zone_pivot_groups: platform
ms.openlocfilehash: 5e0a236b9cf0c3c0b23beb1324f35a34dade2e92
ms.sourcegitcommit: 926510a198d738c5726081f6d7994fe9b6fc6edb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/29/2018
ms.locfileid: "43179827"
---
<span data-ttu-id="0196c-101">Installieren Sie die Azure CLI auf Ihrem lokalen Computer, und führen Sie dann einen einfachen Befehl aus, um die Installation zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="0196c-101">Let's install the Azure CLI on your local machine, and then run a simple command to verify your installation.</span></span> <span data-ttu-id="0196c-102">Mit welcher Methode Sie die Azure CLI installieren, hängt vom Betriebssystem Ihres Computers ab.</span><span class="sxs-lookup"><span data-stu-id="0196c-102">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="0196c-103">Wählen Sie die entsprechenden Schritte für Ihr Betriebssystem aus.</span><span class="sxs-lookup"><span data-stu-id="0196c-103">Please choose the steps for your operating system.</span></span>

<span data-ttu-id="0196c-104">::: zone pivot="linux"</span><span class="sxs-lookup"><span data-stu-id="0196c-104">::: zone pivot="linux"</span></span>

### <a name="linux"></a><span data-ttu-id="0196c-105">Linux</span><span class="sxs-lookup"><span data-stu-id="0196c-105">Linux</span></span>
<span data-ttu-id="0196c-106">Hier installieren Sie die Azure CLI unter **Ubuntu Linux** mit dem Advanced Packaging Tool (**apt**) und der Bash-Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="0196c-106">Here you will install the Azure CLI on **Ubuntu Linux** using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!WARNING]
> <span data-ttu-id="0196c-107">Die unten aufgeführten Befehle gelten für Ubuntu-Version 18.04.</span><span class="sxs-lookup"><span data-stu-id="0196c-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="0196c-108">Wenn Sie eine andere Ubuntu-Version verwenden, müssen Sie ein anderes Repository hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="0196c-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="0196c-109">Details finden Sie unter [Installieren der Azure CLI 2.0 mit apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span><span class="sxs-lookup"><span data-stu-id="0196c-109">For details see [Install the Azure CLI 2.0 with apt](https://docs.microsoft.com/cli/azure/install-azure-cli-apt).</span></span>

1. <span data-ttu-id="0196c-110">Bearbeiten Sie Ihre Quellenliste, sodass das Microsoft-Repository registriert wird und der Paket-Manager das Azure CLI-Paket ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="0196c-110">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

1. <span data-ttu-id="0196c-111">Importieren Sie den Verschlüsselungsschlüssel für das Microsoft Ubuntu-Repository.</span><span class="sxs-lookup"><span data-stu-id="0196c-111">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="0196c-112">So kann der Paket-Manager sicherstellen, dass das Azure CLI-Paket, das Sie installieren, wirklich von Microsoft stammt.</span><span class="sxs-lookup"><span data-stu-id="0196c-112">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="0196c-113">Installieren Sie die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0196c-113">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

<span data-ttu-id="0196c-114">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="0196c-114">::: zone-end</span></span>

<span data-ttu-id="0196c-115">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="0196c-115">::: zone pivot="macos"</span></span>

### <a name="macos"></a><span data-ttu-id="0196c-116">macOS</span><span class="sxs-lookup"><span data-stu-id="0196c-116">macOS</span></span>
<span data-ttu-id="0196c-117">Hier installieren Sie die Azure CLI mit dem Homebrew-Paket-Manager unter macOS.</span><span class="sxs-lookup"><span data-stu-id="0196c-117">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0196c-118">Wenn der Befehl **brew** nicht verfügbar ist, müssen Sie möglicherweise den Homebrew-Paket-Manager installieren.</span><span class="sxs-lookup"><span data-stu-id="0196c-118">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="0196c-119">Informationen dazu finden Sie auf der [Website von Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="0196c-119">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="0196c-120">Aktualisieren Sie Ihr brew-Repository, um sicherzustellen, dass Sie das neueste Azure CLI-Paket abrufen.</span><span class="sxs-lookup"><span data-stu-id="0196c-120">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```

1. <span data-ttu-id="0196c-121">Installieren Sie die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0196c-121">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

<span data-ttu-id="0196c-122">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="0196c-122">::: zone-end</span></span>

<span data-ttu-id="0196c-123">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="0196c-123">::: zone pivot="windows"</span></span>

### <a name="windows"></a><span data-ttu-id="0196c-124">Windows</span><span class="sxs-lookup"><span data-stu-id="0196c-124">Windows</span></span>
<span data-ttu-id="0196c-125">Hier installieren Sie die Azure CLI mit dem Microsoft Installer (MSI) unter Windows.</span><span class="sxs-lookup"><span data-stu-id="0196c-125">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="0196c-126">Wechseln Sie zu „[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)“, und klicken Sie im Sicherheitsdialogfeld des Browsers auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="0196c-126">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="0196c-127">Akzeptieren Sie die Lizenzbedingungen im Installer, und klicken Sie dann auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="0196c-127">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="0196c-128">Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="0196c-128">In the **User Account Control** dialog, select **Yes**.</span></span>

<span data-ttu-id="0196c-129">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="0196c-129">::: zone-end</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="0196c-130">Ausführen der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0196c-130">Running the Azure CLI</span></span>
<span data-ttu-id="0196c-131">Unter Linux und macOS führen Sie die Azure CLI aus, indem Sie eine Bash-Shell öffnen. Unter Windows führen Sie die CLI von der Eingabeaufforderung oder über PowerShell aus.</span><span class="sxs-lookup"><span data-stu-id="0196c-131">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="0196c-132">Starten Sie die Azure CLI, und überprüfen Sie Ihre Installation, indem Sie die Versionsprüfung ausführen.</span><span class="sxs-lookup"><span data-stu-id="0196c-132">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```bash
    az --version
    ```

<span data-ttu-id="0196c-133">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="0196c-133">::: zone pivot="windows"</span></span>

> [!NOTE]
> <span data-ttu-id="0196c-134">Die Ausführung der Azure CLI über PowerShell bietet im Vergleich zur Ausführung der Azure CLI über die Windows-Eingabeaufforderung einige Vorteile.</span><span class="sxs-lookup"><span data-stu-id="0196c-134">Running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the Windows command prompt.</span></span> <span data-ttu-id="0196c-135">Zusätzlich zu den in der Eingabeaufforderung verfügbaren Features stellt PowerShell weitere Features zur Vervollständigung mit der TAB-Taste zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="0196c-135">PowerShell provides additional tab completion features over those available from the command prompt.</span></span> 

<span data-ttu-id="0196c-136">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="0196c-136">::: zone-end</span></span>

## <a name="summary"></a><span data-ttu-id="0196c-137">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="0196c-137">Summary</span></span>
<span data-ttu-id="0196c-138">Sie richten Ihre lokalen Computer für die Verwaltung von Azure-Ressourcen mithilfe der Azure CLI ein.</span><span class="sxs-lookup"><span data-stu-id="0196c-138">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="0196c-139">Sie können die Azure CLI jetzt lokal verwenden, um Befehle einzugeben oder Skripts auszuführen.</span><span class="sxs-lookup"><span data-stu-id="0196c-139">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="0196c-140">Die Azure CLI leitet Ihre Befehle an die Azure-Rechenzentren weiter, wo sie in Ihren Azure-Abonnements ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="0196c-140">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>