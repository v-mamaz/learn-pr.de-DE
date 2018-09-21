<span data-ttu-id="699b0-101">In dieser Einheit installieren Sie **Azure PowerShell** auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="699b0-101">In this unit, you will install **PowerShell** on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="699b0-102">Diese Übung führt Sie durch die lokale Installation der PowerShell-Tools.</span><span class="sxs-lookup"><span data-stu-id="699b0-102">This exercise guides you through installing the PowerShell tools locally.</span></span> <span data-ttu-id="699b0-103">Im restlichen Teil des Moduls verwenden Sie Azure Cloud Shell, um den kostenlosen Abonnementsupport in Microsoft Learn nutzen zu können.</span><span class="sxs-lookup"><span data-stu-id="699b0-103">The remainder of the module will use the Azure Cloud Shell so you can leverage the free subscription support in Microsoft Learn.</span></span> <span data-ttu-id="699b0-104">Sie können diese Übung als optionale Aktivität betrachten und ggf. nur die Anweisungen lesen.</span><span class="sxs-lookup"><span data-stu-id="699b0-104">You can consider this exercise as an optional activity and just review the instructions if you prefer.</span></span>

<span data-ttu-id="699b0-105">::: zone pivot="linux"</span><span class="sxs-lookup"><span data-stu-id="699b0-105">::: zone pivot="linux"</span></span>

## <a name="linux"></a><span data-ttu-id="699b0-106">Linux</span><span class="sxs-lookup"><span data-stu-id="699b0-106">Linux</span></span>

<span data-ttu-id="699b0-107">PowerShell für Linux wird über einen Paket-Manager installiert.</span><span class="sxs-lookup"><span data-stu-id="699b0-107">Installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="699b0-108">Wir verwenden für dieses Beispiel **Ubuntu 18.04**. [Detaillierte Anweisungen für andere Versionen und Distributionen finden Sie in unserer Dokumentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span><span class="sxs-lookup"><span data-stu-id="699b0-108">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="699b0-109">Sie installieren PowerShell Core unter Ubuntu Linux mit dem Advanced Packaging Tool (**apt**) und der Bash-Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="699b0-109">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="699b0-110">Importieren Sie den Verschlüsselungsschlüssel für das Microsoft Ubuntu-Repository.</span><span class="sxs-lookup"><span data-stu-id="699b0-110">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="699b0-111">So kann der Paket-Manager sicherstellen, dass das PowerShell Core-Paket, das Sie installieren, wirklich von Microsoft stammt.</span><span class="sxs-lookup"><span data-stu-id="699b0-111">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="699b0-112">Registrieren Sie das **Microsoft Ubuntu-Repository**, sodass der Paket-Manager das PowerShell Core-Paket finden kann.</span><span class="sxs-lookup"><span data-stu-id="699b0-112">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="699b0-113">Aktualisieren Sie die Liste der Pakete.</span><span class="sxs-lookup"><span data-stu-id="699b0-113">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="699b0-114">Installieren Sie PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="699b0-114">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="699b0-115">Starten Sie PowerShell, um sich zu vergewissern, dass es erfolgreich installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="699b0-115">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```
<span data-ttu-id="699b0-116">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="699b0-116">::: zone-end</span></span>

<span data-ttu-id="699b0-117">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="699b0-117">::: zone pivot="macos"</span></span>

## <a name="macos"></a><span data-ttu-id="699b0-118">macOS</span><span class="sxs-lookup"><span data-stu-id="699b0-118">MacOS</span></span>

<span data-ttu-id="699b0-119">Unter macOS muss zunächst **PowerShell Core** installiert werden.</span><span class="sxs-lookup"><span data-stu-id="699b0-119">On macOS, the first step is to install **PowerShell Core**.</span></span> <span data-ttu-id="699b0-120">Hierzu wird der Homebrew-Paket-Manager verwendet.</span><span class="sxs-lookup"><span data-stu-id="699b0-120">This is done using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="699b0-121">Sollte der Befehl **brew** nicht verfügbar sein, müssen Sie möglicherweise den Homebrew-Paket-Manager installieren.</span><span class="sxs-lookup"><span data-stu-id="699b0-121">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="699b0-122">Informationen dazu finden Sie auf der [Website von Homebrew](https://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="699b0-122">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="699b0-123">Installieren Sie „Homebrew-Cask“, um weitere Pakete abzurufen, einschließlich des PowerShell Core-Pakets:</span><span class="sxs-lookup"><span data-stu-id="699b0-123">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```

1. <span data-ttu-id="699b0-124">Installieren von PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="699b0-124">Install PowerShell Core:</span></span>

    ```bash
    brew cask install powershell
    ```

1. <span data-ttu-id="699b0-125">Starten Sie PowerShell Core, um sich zu vergewissern, dass es erfolgreich installiert wurde:</span><span class="sxs-lookup"><span data-stu-id="699b0-125">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

<span data-ttu-id="699b0-126">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="699b0-126">::: zone-end</span></span>

<span data-ttu-id="699b0-127">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="699b0-127">::: zone pivot="windows"</span></span>

## <a name="windows"></a><span data-ttu-id="699b0-128">Windows</span><span class="sxs-lookup"><span data-stu-id="699b0-128">Windows</span></span>
<span data-ttu-id="699b0-129">PowerShell ist in Windows enthalten. Es ist jedoch möglicherweise ein Update für Ihren Computer verfügbar.</span><span class="sxs-lookup"><span data-stu-id="699b0-129">PowerShell is included with Windows, however there may be an update available for your machine.</span></span> <span data-ttu-id="699b0-130">Für den Azure-Support, den wir verwenden möchten, benötigen wir mindestens PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="699b0-130">The Azure support we are going to use requires PowerShell version 5.0 or higher.</span></span> <span data-ttu-id="699b0-131">Die installierte Version können Sie wie folgt ermitteln:</span><span class="sxs-lookup"><span data-stu-id="699b0-131">You can check the version you have installed through the following steps:</span></span>

1. <span data-ttu-id="699b0-132">Öffnen Sie das **Startmenü**, und geben Sie **Windows PowerShell** ein.</span><span class="sxs-lookup"><span data-stu-id="699b0-132">Open the **Start** menu and type **Windows PowerShell**.</span></span> <span data-ttu-id="699b0-133">Unter Umständen stehen mehrere Verknüpfungslinks zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="699b0-133">There may be multiple shortcut links available:</span></span>
    - <span data-ttu-id="699b0-134">Windows PowerShell: Dies ist die 64-Bit-Version und in der Regel die Option, die Sie auswählen sollten.</span><span class="sxs-lookup"><span data-stu-id="699b0-134">Windows PowerShell - this is the 64-bit version and generally what you should choose.</span></span>
    - <span data-ttu-id="699b0-135">Windows PowerShell (x86): Dies ist eine 32-Bit-Version, die unter Windows mit 64 Bit installiert ist.</span><span class="sxs-lookup"><span data-stu-id="699b0-135">Windows PowerShell (x86) - this is a 32-bit version installed on 64-bit Windows.</span></span>
    - <span data-ttu-id="699b0-136">Windows PowerShell ISE: Integrated Scripting Environment (ISE) dient zum Schreiben von Skripts in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="699b0-136">Windows PowerShell ISE - The Integrated Scripting Environment (ISE) is used for writing scripts in PowerShell.</span></span> 
    - <span data-ttu-id="699b0-137">Windows PowerShell ISE (x86): Eine 32-Bit-Version von ISE.</span><span class="sxs-lookup"><span data-stu-id="699b0-137">Windows PowerShell ISE (x86) - A 32-bit version of the ISE.</span></span>

1. <span data-ttu-id="699b0-138">Klicken Sie auf das Windows PowerShell-Symbol.</span><span class="sxs-lookup"><span data-stu-id="699b0-138">Select the Windows PowerShell icon.</span></span>

1. <span data-ttu-id="699b0-139">Geben Sie den folgenden Befehl ein, um die installierte PowerShell-Version zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="699b0-139">Type the following command to determine the version of PowerShell installed.</span></span>

    ```powershell
    $PSVersionTable.PSVersion
    ```
    
<span data-ttu-id="699b0-140">Ist die Versionsnummer niedriger als 5.0, führen Sie die Schritte zum [Upgraden einer vorhandenen Windows PowerShell-Instanz](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell) aus.</span><span class="sxs-lookup"><span data-stu-id="699b0-140">If the version number is lower than 5.0, follow these instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

<span data-ttu-id="699b0-141">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="699b0-141">::: zone-end</span></span>

<span data-ttu-id="699b0-142">Sie haben die Unterstützung von PowerShell für Ihre lokalen Computer eingerichtet.</span><span class="sxs-lookup"><span data-stu-id="699b0-142">You have setup your local machine(s) to support PowerShell.</span></span> <span data-ttu-id="699b0-143">Als Nächstes beschäftigen wir uns mit zusätzlichen Befehlen, die Sie hinzufügen können (einschließlich des Azure-Moduls).</span><span class="sxs-lookup"><span data-stu-id="699b0-143">Next, we will talk about additional commands you can add including the Azure module.</span></span>