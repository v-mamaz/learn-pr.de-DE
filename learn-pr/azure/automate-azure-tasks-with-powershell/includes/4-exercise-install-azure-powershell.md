
<span data-ttu-id="cf14b-101">In dieser Übung installieren Sie **Azure PowerShell** auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="cf14b-101">In this exercise, you will install **Azure PowerShell** on your local machine.</span></span> <span data-ttu-id="cf14b-102">Wählen Sie die Schritte für Ihr Betriebssystem aus.</span><span class="sxs-lookup"><span data-stu-id="cf14b-102">Please choose the steps for your operating system.</span></span>

## <a name="install-powershell-core"></a><span data-ttu-id="cf14b-103">Installieren von PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="cf14b-103">Install PowerShell Core</span></span>
<span data-ttu-id="cf14b-104">Unter Linux und MacOS wird der erste Schritt zum Installieren **PowerShell Core**.</span><span class="sxs-lookup"><span data-stu-id="cf14b-104">On Linux and macOS, the first step is to install **PowerShell Core**.</span></span>

### <a name="linux"></a><span data-ttu-id="cf14b-105">Linux</span><span class="sxs-lookup"><span data-stu-id="cf14b-105">Linux</span></span>
<span data-ttu-id="cf14b-106">Installieren Sie PowerShell Core auf Ubuntu Linux über das Advanced Packaging Tool (**apt**) und die Bash-Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="cf14b-106">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

> [!NOTE] <span data-ttu-id="cf14b-107">Die unten aufgeführten Befehle sind für Ubuntu-Version 18.04.</span><span class="sxs-lookup"><span data-stu-id="cf14b-107">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="cf14b-108">Wenn Sie eine andere Version von Ubuntu verwenden, müssen Sie ein anderes Repository hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="cf14b-108">If you are using a different version of Ubuntu, you must add a different repository.</span></span> <span data-ttu-id="cf14b-109">Weitere Informationen finden Sie [Installieren von PowerShell Core unter Linux](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-powershell-core-on-linux).</span><span class="sxs-lookup"><span data-stu-id="cf14b-109">For details see [Installing PowerShell Core on Linux](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

1. <span data-ttu-id="cf14b-110">Importieren Sie den Verschlüsselungsschlüssel für das Microsoft-Ubuntu-Repository.</span><span class="sxs-lookup"><span data-stu-id="cf14b-110">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="cf14b-111">Das Paket dadurch Manager, um sicherzustellen, dass das PowerShell Core-Paket, die, das Sie installieren, von Microsoft stammt.</span><span class="sxs-lookup"><span data-stu-id="cf14b-111">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="cf14b-112">Registrieren Sie das Microsoft-Ubuntu-Repository aus, damit das PowerShell Core-Paket mit der Paket-Manager gefunden werden kann.</span><span class="sxs-lookup"><span data-stu-id="cf14b-112">Register the Microsoft Ubuntu repository so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="cf14b-113">Aktualisieren Sie die Liste der Pakete.</span><span class="sxs-lookup"><span data-stu-id="cf14b-113">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="cf14b-114">Installieren Sie PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="cf14b-114">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="cf14b-115">Starten Sie PowerShell, um sicherzustellen, dass die It wurde erfolgreich installiert.</span><span class="sxs-lookup"><span data-stu-id="cf14b-115">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```

### <a name="macos"></a><span data-ttu-id="cf14b-116">macOS</span><span class="sxs-lookup"><span data-stu-id="cf14b-116">macOS</span></span>
<span data-ttu-id="cf14b-117">Installieren Sie als Nächstes **PowerShell Core** unter MacOS unter Verwendung der Homebrew-Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="cf14b-117">Next, install **PowerShell Core** on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT] <span data-ttu-id="cf14b-118">Wenn die **brew** Befehl nicht verfügbar ist, müssen Sie möglicherweise die Homebrew-Paket-Manager zu installieren.</span><span class="sxs-lookup"><span data-stu-id="cf14b-118">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="cf14b-119">Weitere Informationen finden Sie die [Homebrew-Website](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="cf14b-119">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="cf14b-120">Installieren Sie Homebrew-Cask, um weitere Pakete, sowie das PowerShell Core-Paket zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="cf14b-120">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```
1. <span data-ttu-id="cf14b-121">Installieren Sie PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="cf14b-121">Install PowerShell Core:</span></span>

    ```bash
    brew cask install powershell
    ```

1. <span data-ttu-id="cf14b-122">Starten Sie PowerShell Core, um sicherzustellen, dass die It wurde erfolgreich installiert:</span><span class="sxs-lookup"><span data-stu-id="cf14b-122">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a><span data-ttu-id="cf14b-123">Installieren von Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="cf14b-123">Install Azure PowerShell</span></span>
<span data-ttu-id="cf14b-124">Nach der Installation der Basis **PowerShell** Produkt installieren **Azure PowerShell** , die Azure-spezifischen Befehle hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="cf14b-124">After installing the base **PowerShell** product, install **Azure PowerShell** to add the Azure-specific commands.</span></span>

### <a name="windows"></a><span data-ttu-id="cf14b-125">Windows</span><span class="sxs-lookup"><span data-stu-id="cf14b-125">Windows</span></span>
<span data-ttu-id="cf14b-126">Installieren Sie Azure PowerShell zur Verwendung von Windows die **Install-Module** PowerShell-Befehl.</span><span class="sxs-lookup"><span data-stu-id="cf14b-126">Install Azure PowerShell on Windows using the **Install-Module** PowerShell command.</span></span>

> [!IMPORTANT] <span data-ttu-id="cf14b-127">Sie müssen PowerShell, Version 5.0 oder höher zum Installieren von Azure PowerShell verfügen.</span><span class="sxs-lookup"><span data-stu-id="cf14b-127">You must have PowerShell version 5.0 or higher to install Azure PowerShell.</span></span> <span data-ttu-id="cf14b-128">Um Ihre Version von PowerShell zu überprüfen, verwenden Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="cf14b-128">To check your version of PowerShell, use the following command:</span></span> 
>
> `$PSVersionTable.PSVersion` 
>
><span data-ttu-id="cf14b-129">Wenn die Versionsnummer niedriger als 5.0 ist, finden Sie unter [Aktualisieren von vorhandenen Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="cf14b-129">If the version number is lower than 5.0, see [Upgrading existing Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

1. <span data-ttu-id="cf14b-130">Öffnen der **starten** integrierten **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cf14b-130">Open the **Start** menu and type **Windows PowerShell**.</span></span>
1. <span data-ttu-id="cf14b-131">Mit der rechten Maustaste die **Windows PowerShell** Symbol, und wählen **als Administrator ausführen**.</span><span class="sxs-lookup"><span data-stu-id="cf14b-131">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>
1. <span data-ttu-id="cf14b-132">In der **User Account Control** wählen Sie im Dialogfeld **Ja**.</span><span class="sxs-lookup"><span data-stu-id="cf14b-132">In the **User Account Control** dialog, select **Yes**.</span></span>
1. <span data-ttu-id="cf14b-133">Geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="cf14b-133">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```
1. <span data-ttu-id="cf14b-134">Wenn Sie aufgefordert werden, ob Sie Module aus PSGallery vertrauen, beantworten **Ja** oder **Ja, alle**.</span><span class="sxs-lookup"><span data-stu-id="cf14b-134">If you are asked whether you trust modules from PSGallery, answer **Yes** or **Yes to All**.</span></span>

### <a name="linux-or-macos"></a><span data-ttu-id="cf14b-135">Linux oder macOS</span><span class="sxs-lookup"><span data-stu-id="cf14b-135">Linux or macOS</span></span>
<span data-ttu-id="cf14b-136">Installieren Sie Azure PowerShell unter Linux oder MacOS verwenden, die **Install-Module** PowerShell-Befehl.</span><span class="sxs-lookup"><span data-stu-id="cf14b-136">Install Azure PowerShell on either Linux or macOS using the **Install-Module** PowerShell command.</span></span> <span data-ttu-id="cf14b-137">Das Verfahren ist für beide Betriebssysteme gleich.</span><span class="sxs-lookup"><span data-stu-id="cf14b-137">The procedure is the same for both operating systems.</span></span>

1. <span data-ttu-id="cf14b-138">Geben Sie in einem Terminal den folgenden Befehl zum Starten von PowerShell Core mit erhöhten Rechten aus.</span><span class="sxs-lookup"><span data-stu-id="cf14b-138">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="cf14b-139">Führen Sie den folgenden Befehl an der Eingabeaufforderung PowerShell Core, Azure PowerShell installieren.</span><span class="sxs-lookup"><span data-stu-id="cf14b-139">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="cf14b-140">Wenn Sie aufgefordert werden, ob Sie Module aus vertrauen **PSGallery**, Antwort **Ja** oder **Ja, alle**.</span><span class="sxs-lookup"><span data-stu-id="cf14b-140">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

## <a name="summary"></a><span data-ttu-id="cf14b-141">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="cf14b-141">Summary</span></span>
<span data-ttu-id="cf14b-142">Sie richten Sie Ihre lokalen Computer zum Azure-Ressourcen mit Azure PowerShell verwalten.</span><span class="sxs-lookup"><span data-stu-id="cf14b-142">You setup your local machine(s) to administer Azure resources with Azure PowerShell.</span></span> <span data-ttu-id="cf14b-143">Sie können nun Azure PowerShell lokal verwenden, geben Befehle oder Skripts ausführen.</span><span class="sxs-lookup"><span data-stu-id="cf14b-143">You can now use Azure PowerShell locally to enter commands or execute scripts.</span></span> <span data-ttu-id="cf14b-144">Azure PowerShell wird Ihre Befehle aus, um den Azure-Rechenzentren weitergeleitet, wo sie in Ihrem Azure-Abonnement ausgeführt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="cf14b-144">Azure PowerShell will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>