<span data-ttu-id="52c92-101">In dieser Übung installieren Sie **Azure PowerShell** auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="52c92-101">In this exercise, you will install **Azure PowerShell** on your local machine.</span></span> <span data-ttu-id="52c92-102">Wählen Sie den entsprechenden Abschnitt für Ihr Betriebssystem.</span><span class="sxs-lookup"><span data-stu-id="52c92-102">Choose the appropriate section for your operating system.</span></span>

## <a name="linux-and-mac"></a><span data-ttu-id="52c92-103">Linux und Mac</span><span class="sxs-lookup"><span data-stu-id="52c92-103">Linux and Mac</span></span>
<span data-ttu-id="52c92-104">Unter Linux und macOS besteht der erste Schritt darin, **PowerShell Core** zu installieren.</span><span class="sxs-lookup"><span data-stu-id="52c92-104">On Linux and macOS, the first step is to install **PowerShell Core**.</span></span>

### <a name="linux"></a><span data-ttu-id="52c92-105">Linux</span><span class="sxs-lookup"><span data-stu-id="52c92-105">Linux</span></span>
<span data-ttu-id="52c92-106">Wie in der letzten Übungseinheit erläutert, wird PowerShell für Linux über einen Paket-Manager installiert.</span><span class="sxs-lookup"><span data-stu-id="52c92-106">As mentioned in the last unit, installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="52c92-107">Wir verwenden für dieses Beispiel **Ubuntu 18.04**. [Detaillierte Anweisungen für andere Versionen und Distributionen finden Sie in unserer Dokumentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span><span class="sxs-lookup"><span data-stu-id="52c92-107">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="52c92-108">Sie installieren PowerShell Core unter Ubuntu Linux mit dem Advanced Packaging Tool (**apt**) und der Bash-Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="52c92-108">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="52c92-109">Importieren Sie den Verschlüsselungsschlüssel für das Microsoft Ubuntu-Repository.</span><span class="sxs-lookup"><span data-stu-id="52c92-109">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="52c92-110">So kann der Paket-Manager sicherstellen, dass das PowerShell Core-Paket, das Sie installieren, wirklich von Microsoft stammt.</span><span class="sxs-lookup"><span data-stu-id="52c92-110">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. <span data-ttu-id="52c92-111">Registrieren Sie das **Microsoft Ubuntu-Repository**, sodass der Paket-Manager das PowerShell Core-Paket finden kann.</span><span class="sxs-lookup"><span data-stu-id="52c92-111">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="52c92-112">Aktualisieren Sie die Liste der Pakete.</span><span class="sxs-lookup"><span data-stu-id="52c92-112">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="52c92-113">Installieren Sie PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="52c92-113">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="52c92-114">Starten Sie PowerShell, um sicherzustellen, dass es erfolgreich installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="52c92-114">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```

### <a name="macos"></a><span data-ttu-id="52c92-115">macOS</span><span class="sxs-lookup"><span data-stu-id="52c92-115">macOS</span></span>
<span data-ttu-id="52c92-116">Installieren Sie als Nächstes **PowerShell Core** mit dem Homebrew-Paket-Manager unter macOS.</span><span class="sxs-lookup"><span data-stu-id="52c92-116">Next, install **PowerShell Core** on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52c92-117">Wenn der Befehl **brew** nicht verfügbar ist, müssen Sie möglicherweise den Homebrew-Paket-Manager installieren.</span><span class="sxs-lookup"><span data-stu-id="52c92-117">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="52c92-118">Informationen dazu finden Sie auf der [Website von Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="52c92-118">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="52c92-119">Installieren Sie „Homebrew-Cask“, um weitere Pakete abzurufen, einschließlich des PowerShell Core-Pakets:</span><span class="sxs-lookup"><span data-stu-id="52c92-119">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```
1. <span data-ttu-id="52c92-120">Installieren von PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="52c92-120">Install PowerShell Core:</span></span>

    ```bash
    brew cask installs powershell
    ```

1. <span data-ttu-id="52c92-121">Starten Sie PowerShell Core, um sicherzustellen, dass es erfolgreich installiert wurde:</span><span class="sxs-lookup"><span data-stu-id="52c92-121">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a><span data-ttu-id="52c92-122">Installieren von Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52c92-122">Install Azure PowerShell</span></span>
<span data-ttu-id="52c92-123">Installieren Sie nach dem **PowerShell**-Basisprodukt **Azure PowerShell**, um die Azure-spezifischen Befehle zu installieren.</span><span class="sxs-lookup"><span data-stu-id="52c92-123">After installing the base **PowerShell** product, install **Azure PowerShell** to add the Azure-specific commands.</span></span>

### <a name="windows"></a><span data-ttu-id="52c92-124">Windows</span><span class="sxs-lookup"><span data-stu-id="52c92-124">Windows</span></span>
<span data-ttu-id="52c92-125">Installieren Sie Azure PowerShell unter Windows mit dem PowerShell-Befehl „`Install-Module`“.</span><span class="sxs-lookup"><span data-stu-id="52c92-125">Install Azure PowerShell on Windows using the `Install-Module` PowerShell command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52c92-126">Für die Installation von Azure PowerShell benötigen Sie PowerShell Version 5.0 oder höher.</span><span class="sxs-lookup"><span data-stu-id="52c92-126">You must have PowerShell version 5.0 or higher to install Azure PowerShell.</span></span> <span data-ttu-id="52c92-127">Um Ihre PowerShell-Version zu überprüfen, verwenden Sie folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="52c92-127">To check your version of PowerShell, use the following command:</span></span> 
>
> `$PSVersionTable.PSVersion` 
>
><span data-ttu-id="52c92-128">Wenn die Versionsnummer niedriger ist als 5.0, befolgen Sie die Anweisungen zum [Durchführen eines Upgrades einer vorhandenen Windows PowerShell-Version](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="52c92-128">If the version number is lower than 5.0, follow the instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

1. <span data-ttu-id="52c92-129">Öffnen Sie das **Startmenü**, und geben Sie **Windows PowerShell** ein.</span><span class="sxs-lookup"><span data-stu-id="52c92-129">Open the **Start** menu and type **Windows PowerShell**.</span></span>
2. <span data-ttu-id="52c92-130">Klicken Sie mit der rechten Maustaste auf das Symbol **Windows PowerShell**, und wählen Sie **Als Administrator ausführen** aus.</span><span class="sxs-lookup"><span data-stu-id="52c92-130">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>
3. <span data-ttu-id="52c92-131">Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="52c92-131">In the **User Account Control** dialog, select **Yes**.</span></span>
4. <span data-ttu-id="52c92-132">Geben Sie den folgenden Befehl ein, und drücken Sie die Eingabetaste:</span><span class="sxs-lookup"><span data-stu-id="52c92-132">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```
5. <span data-ttu-id="52c92-133">Wenn Sie gefragt werden, ob Sie Modulen von PSGallery vertrauen, antworten Sie **Ja** oder **Ja, allen**.</span><span class="sxs-lookup"><span data-stu-id="52c92-133">If you are asked whether you trust modules from PSGallery, answer **Yes** or **Yes to All**.</span></span>

> [!NOTE]
> <span data-ttu-id="52c92-134">Wenn Sie in einer Fehlermeldung darauf hingewiesen werden, dass bereits eine Version des Azure PowerShell-Moduls installiert ist, können Sie diese mit dem folgenden Befehl auf die _neueste_ Version aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="52c92-134">If you get an error message indicating that a version of the Azure PowerShell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>
> 
> `Update-Module -Name AzureRM`
> 
> <span data-ttu-id="52c92-135">Antworten Sie ebenso wie beim `Install-Module`-Befehl auf die Frage, ob Sie dem Modul vertrauen, mit **Ja** oder **Ja, alle**.</span><span class="sxs-lookup"><span data-stu-id="52c92-135">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span>

### <a name="linux-or-macos"></a><span data-ttu-id="52c92-136">Linux oder macOS</span><span class="sxs-lookup"><span data-stu-id="52c92-136">Linux or macOS</span></span>
<span data-ttu-id="52c92-137">Zum Installieren von Azure PowerShell unter Linux oder macOS verwenden wir das gleiche grundlegende Verfahren.</span><span class="sxs-lookup"><span data-stu-id="52c92-137">We use the same basic process to install the Azure PowerShell on either Linux or macOS.</span></span> <span data-ttu-id="52c92-138">Das Procedere ist für beide Betriebssysteme gleich.</span><span class="sxs-lookup"><span data-stu-id="52c92-138">The procedure is the same for both operating systems.</span></span> <span data-ttu-id="52c92-139">Der Unterschied besteht darin, eine PowerShell Core-Sitzung mit erhöhten Rechten zu starten.</span><span class="sxs-lookup"><span data-stu-id="52c92-139">The difference is in getting an elevated PowerShell Core session.</span></span>

1. <span data-ttu-id="52c92-140">Geben Sie auf einem Terminal den folgenden Befehl ein, um PowerShell Core mit erhöhten Rechten zu starten.</span><span class="sxs-lookup"><span data-stu-id="52c92-140">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="52c92-141">Um Azure PowerShell zu installieren, führen Sie an der PowerShell Core-Eingabeaufforderung den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="52c92-141">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="52c92-142">Wenn Sie gefragt werden, ob Sie Modulen von **PSGallery** vertrauen, antworten Sie **Ja** oder **Ja, alle**.</span><span class="sxs-lookup"><span data-stu-id="52c92-142">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

## <a name="summary"></a><span data-ttu-id="52c92-143">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="52c92-143">Summary</span></span>
<span data-ttu-id="52c92-144">Sie haben Ihre(n) lokalen Computer für die Verwaltung von Azure-Ressourcen mithilfe von Azure PowerShell eingerichtet.</span><span class="sxs-lookup"><span data-stu-id="52c92-144">You have setup your local machine(s) to administer Azure resources with Azure PowerShell.</span></span> <span data-ttu-id="52c92-145">Sie können Azure PowerShell jetzt lokal zum Eingeben von Befehlen oder Ausführen von Skripts verwenden.</span><span class="sxs-lookup"><span data-stu-id="52c92-145">You can now use Azure PowerShell locally to enter commands or execute scripts.</span></span> <span data-ttu-id="52c92-146">Azure PowerShell leitet Ihre Befehle an die Azure-Rechenzentren weiter, wo sie in Ihren Azure-Abonnements ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="52c92-146">Azure PowerShell will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>
