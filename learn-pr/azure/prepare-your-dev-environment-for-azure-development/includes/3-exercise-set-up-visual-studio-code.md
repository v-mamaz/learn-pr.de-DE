<span data-ttu-id="68b65-101">Um Visual Studio Code für die Azure-Entwicklung verwenden zu können, müssen Sie Visual Studio Code lokal und mindestens eine weitere Azure-Erweiterung installieren.</span><span class="sxs-lookup"><span data-stu-id="68b65-101">To use Visual Studio Code for Azure development, you'll need to install Visual Studio Code locally and one or more Azure extensions.</span></span> <span data-ttu-id="68b65-102">In dieser Übung fügen wir die **Azure App Service**-Erweiterung hinzu.</span><span class="sxs-lookup"><span data-stu-id="68b65-102">In this exercise, we'll add the **Azure App Service** extension.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="68b65-103">Installieren von Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="68b65-103">Install Visual Studio Code</span></span>

<span data-ttu-id="68b65-104">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="68b65-104">::: zone pivot="windows"</span></span>

### <a name="windows"></a><span data-ttu-id="68b65-105">Windows</span><span class="sxs-lookup"><span data-stu-id="68b65-105">Windows</span></span>

1. <span data-ttu-id="68b65-106">[Laden Sie den Visual Studio Code-Installer für Windows herunter.](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="68b65-106">[Download the Visual Studio Code installer for Windows](https://code.visualstudio.com/).</span></span>

1. <span data-ttu-id="68b65-107">Führen Sie das Installationsprogramm aus.</span><span class="sxs-lookup"><span data-stu-id="68b65-107">Run the installer.</span></span>

1. <span data-ttu-id="68b65-108">Öffnen Sie Visual Studio Code, indem Sie die Windows-Taste drücken oder auf das Windows-Symbol auf der Taskleiste klicken, „Visual Studio Code“ eingeben und auf das Ergebnis **Visual Studio Code** klicken.</span><span class="sxs-lookup"><span data-stu-id="68b65-108">Open Visual Studio Code by pressing the Windows key or clicking the Windows icon on the task bar, typing "Visual Studio Code" and clicking on the **Visual Studio Code** result.</span></span>

<span data-ttu-id="68b65-109">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="68b65-109">::: zone-end</span></span>

<span data-ttu-id="68b65-110">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="68b65-110">::: zone pivot="macos"</span></span>

### <a name="macos"></a><span data-ttu-id="68b65-111">macOS</span><span class="sxs-lookup"><span data-stu-id="68b65-111">macOS</span></span>

1. <span data-ttu-id="68b65-112">[Laden Sie Visual Studio Code für macOS herunter.](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="68b65-112">[Download Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span>

1. <span data-ttu-id="68b65-113">Doppelklicken Sie auf das heruntergeladene Archiv, um den Inhalt zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="68b65-113">Double-click on the downloaded archive to expand the contents.</span></span>

1. <span data-ttu-id="68b65-114">Ziehen Sie „Visual Studio Code.app“ in den Ordner „Programme“.</span><span class="sxs-lookup"><span data-stu-id="68b65-114">Drag Visual Studio Code.app to the Applications folder.</span></span>

1. <span data-ttu-id="68b65-115">Öffnen Sie Visual Studio Code, indem Sie auf das Symbol im Abschnitt „Apps“ klicken oder nach Visual Studio Code in Spotlight suchen.</span><span class="sxs-lookup"><span data-stu-id="68b65-115">Open Visual Studio Code by clicking on the icon the Apps section or by searching for Visual Studio Code in Spotlight.</span></span>

<span data-ttu-id="68b65-116">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="68b65-116">::: zone-end</span></span>

<span data-ttu-id="68b65-117">::: zone pivot="linux"</span><span class="sxs-lookup"><span data-stu-id="68b65-117">::: zone pivot="linux"</span></span>

### <a name="linux"></a><span data-ttu-id="68b65-118">Linux</span><span class="sxs-lookup"><span data-stu-id="68b65-118">Linux</span></span> 

#### <a name="debian-and-ubuntu"></a><span data-ttu-id="68b65-119">Debian und Ubuntu</span><span class="sxs-lookup"><span data-stu-id="68b65-119">Debian and Ubuntu</span></span>

1. <span data-ttu-id="68b65-120">Laden Sie das [DEB-Paket (64-Bit)](https://go.microsoft.com/fwlink/?LinkID=760868) herunter, und installieren Sie es über das grafische Softwarecenter (falls verfügbar) oder über die Befehlszeile (ersetzen Sie `<file>` durch den Namen der heruntergeladenen DEB-Datei):</span><span class="sxs-lookup"><span data-stu-id="68b65-120">Download and install the [.deb package (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760868) through the graphical software center, if it's available, or through the command line (replacing `<file>` with the .deb filename you downloaded):</span></span>

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

#### <a name="rhel-fedora-and-centos"></a><span data-ttu-id="68b65-121">RHEL, Fedora und CentOS</span><span class="sxs-lookup"><span data-stu-id="68b65-121">RHEL, Fedora, and CentOS</span></span>

1. <span data-ttu-id="68b65-122">Verwenden Sie folgendes Skript, um Schlüssel und Repository zu installieren:</span><span class="sxs-lookup"><span data-stu-id="68b65-122">Use the following script to install the key and repository:</span></span>

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    ```

1. <span data-ttu-id="68b65-123">Aktualisieren Sie den Paketcache, und installieren Sie das Paket mithilfe von „dnf“ (Fedora 22 und höher):</span><span class="sxs-lookup"><span data-stu-id="68b65-123">Update the package cache, and install the package by using dnf (Fedora 22 and above):</span></span>

    ```bash
    dnf check-update
    sudo dnf install code
    ```

#### <a name="opensuse-and-sle"></a><span data-ttu-id="68b65-124">openSUSE und SLE</span><span class="sxs-lookup"><span data-stu-id="68b65-124">openSUSE and SLE</span></span>

1. <span data-ttu-id="68b65-125">Das yum-Repository funktioniert ebenfalls für openSUSE- und SLE-basierte Systeme.</span><span class="sxs-lookup"><span data-stu-id="68b65-125">The yum repository also works for openSUSE and SLE based systems.</span></span> <span data-ttu-id="68b65-126">Mit folgendem Skript werden der Schlüssel und das Repository installiert:</span><span class="sxs-lookup"><span data-stu-id="68b65-126">The following script will install the key and repository:</span></span>

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
    ```

1. <span data-ttu-id="68b65-127">Aktualisieren Sie den Paketcache, und installieren Sie das Paket folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="68b65-127">Update the package cache and install the package by using:</span></span>

    ```bash
    sudo zypper refresh
    sudo zypper install code
    ```

> [!NOTE]
> <span data-ttu-id="68b65-128">Weitere Informationen zum Installieren oder Aktualisieren von Visual Studio Code auf den verschiedenen Linux-Distributionen finden Sie in der Dokumentation [Running Visual Studio Code on Linux (Ausführen von Visual Studio Code unter Linux)](https://code.visualstudio.com/docs/setup/linux).</span><span class="sxs-lookup"><span data-stu-id="68b65-128">For further details about installing or updating Visual Studio Code on various Linux distributions, please see the [Running Visual Studio Code on Linux documentation](https://code.visualstudio.com/docs/setup/linux).</span></span>

<span data-ttu-id="68b65-129">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="68b65-129">::: zone-end</span></span>

## <a name="install-azure-app-service-extension"></a><span data-ttu-id="68b65-130">Installieren der Azure App Service-Erweiterung</span><span class="sxs-lookup"><span data-stu-id="68b65-130">Install Azure App Service extension</span></span>

1. <span data-ttu-id="68b65-131">Öffnen Sie Visual Studio Code, wenn Sie dies noch nicht getan haben.</span><span class="sxs-lookup"><span data-stu-id="68b65-131">If you haven't already, open Visual Studio Code.</span></span>

1. <span data-ttu-id="68b65-132">Öffnen Sie den Browser „Erweiterungen“, auf den über das Menü auf der linken Seite zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="68b65-132">Open the Extensions browser; it's accessed via the menu on the left.</span></span>

1. <span data-ttu-id="68b65-133">Suchen Sie nach **Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="68b65-133">Search for **Azure App Service**.</span></span>

1. <span data-ttu-id="68b65-134">Wählen Sie das Ergebnis **Azure App Service** aus, und klicken Sie auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="68b65-134">Select the **Azure App Service** result and click **Install**.</span></span>

    <span data-ttu-id="68b65-135">Der folgende Screenshot stellt die Azure App Service-Erweiterung dar, die in den Suchergebnissen für Visual Studio Code-Erweiterungen ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="68b65-135">The following screenshot shows the Azure App Service extension selected from the Visual Studio Code extension search results.</span></span>

    ![Screenshot von Visual Studio Code, der die Registerkarte „Erweiterungen“ mit der in den Suchergebnissen hervorgehobenen Azure App Service-Erweiterung darstellt.](../media/3-install-azure-extension.png)

<span data-ttu-id="68b65-137">Dadurch wird die Erweiterung installiert.</span><span class="sxs-lookup"><span data-stu-id="68b65-137">This will install the extension.</span></span> <span data-ttu-id="68b65-138">Sie sind nun bereit, eine Verbindung mit Ihrem Azure-Abonnement herzustellen und Web-Apps, mobile Apps oder API-Apps in Azure App Service bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="68b65-138">You're now ready to connect to your Azure subscription and deploy a web, mobile, or API app to an Azure App Service.</span></span>
