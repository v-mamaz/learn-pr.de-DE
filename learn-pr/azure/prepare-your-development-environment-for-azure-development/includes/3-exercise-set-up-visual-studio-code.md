<span data-ttu-id="dc667-101">In dieser Übung installieren Sie Visual Studio Code und die Azure App Service-Erweiterung. Dadurch können Sie für Microsoft Azure entwickeln und eine Web-App bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="dc667-101">In this exercise, you will install Visual Studio Code and the Azure App Service extension, which will get you ready to develop for Microsoft Azure and to deploy a web app.</span></span>

## <a name="exercise-steps"></a><span data-ttu-id="dc667-102">Schritte</span><span class="sxs-lookup"><span data-stu-id="dc667-102">Exercise steps</span></span>

<span data-ttu-id="dc667-103">Finden Sie zunächst heraus, welches Betriebssystem Sie verwenden, und befolgen Sie die Schritte in den entsprechenden Abschnitten, um Visual Studio Code zu installieren.</span><span class="sxs-lookup"><span data-stu-id="dc667-103">First, identify which operating system you are using, and follow the steps in the appropriate section below to install Visual Studio Code.</span></span>

### <a name="windows"></a><span data-ttu-id="dc667-104">Windows</span><span class="sxs-lookup"><span data-stu-id="dc667-104">Windows</span></span>

1. <span data-ttu-id="dc667-105">Laden Sie den Visual Studio Code-Installer für Windows herunter.</span><span class="sxs-lookup"><span data-stu-id="dc667-105">Download the Visual Studio Code installer for Windows.</span></span>
2. <span data-ttu-id="dc667-106">Führen Sie das Installationsprogramm aus.</span><span class="sxs-lookup"><span data-stu-id="dc667-106">Run the installer.</span></span> <span data-ttu-id="dc667-107">Die Ausführung wird nicht lange dauern.</span><span class="sxs-lookup"><span data-stu-id="dc667-107">This won't take long.</span></span>
3. <span data-ttu-id="dc667-108">Öffnen Sie Visual Studio Code, indem Sie zum Installationsordner navigieren (Standardpfad auf einem 64-Bit-Computer: C:\Programme\Microsoft VS Code).</span><span class="sxs-lookup"><span data-stu-id="dc667-108">Open VS Code by navigating to the installation folder (the default path is C:\Program Files\Microsoft VS Code for a 64-bit machine).</span></span>

### <a name="macos"></a><span data-ttu-id="dc667-109">macOS</span><span class="sxs-lookup"><span data-stu-id="dc667-109">macOS</span></span>

1. <span data-ttu-id="dc667-110">Laden Sie Visual Studio Code für macOS herunter.</span><span class="sxs-lookup"><span data-stu-id="dc667-110">Download Visual Studio Code for macOS.</span></span>
2. <span data-ttu-id="dc667-111">Doppelklicken Sie auf das heruntergeladene Archiv, um den Inhalt zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="dc667-111">Double-click on the downloaded archive to expand the contents.</span></span>
3. <span data-ttu-id="dc667-112">Ziehen Sie „Visual Studio Code.app“ in den Ordner „Programme“. Dadurch wird die Datei im Launchpad verfügbar.</span><span class="sxs-lookup"><span data-stu-id="dc667-112">Drag Visual Studio Code.app to the Applications folder, making it available in the Launchpad.</span></span>
4. <span data-ttu-id="dc667-113">Fügen Sie Visual Studio Code zu Ihrem Dock hinzu, indem Sie mit der rechten Maustaste auf das Symbol und dann auf „Optionen > Im Dock belassen“.</span><span class="sxs-lookup"><span data-stu-id="dc667-113">Add VS Code to your Dock by right-clicking on the icon, and choosing Options > Keep in Dock.</span></span>

### <a name="linux--debian-and-ubuntu"></a><span data-ttu-id="dc667-114">Linux – Debian und Ubuntu</span><span class="sxs-lookup"><span data-stu-id="dc667-114">Linux – Debian and Ubuntu</span></span>

1. <span data-ttu-id="dc667-115">Laden Sie das [DEB-Paket (64-Bit)](https://go.microsoft.com/fwlink/?LinkID=760868) herunter, und installieren Sie es entweder über das grafische Softwarecenter (falls verfügbar) oder über die Befehlszeile (ersetzen Sie `<file>` durch den Namen der heruntergeladenen DEB-Datei):</span><span class="sxs-lookup"><span data-stu-id="dc667-115">Download and install the [.deb package (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760868), either through the graphical software center, if it's available, or through the command line (replacing `<file>` with the .deb filename you downloaded):</span></span>

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

### <a name="linux--rhel-fedora-and-centos"></a><span data-ttu-id="dc667-116">Linux – RHEL, Fedora und CentOS</span><span class="sxs-lookup"><span data-stu-id="dc667-116">Linux – RHEL, Fedora, and CentOS</span></span>

1. <span data-ttu-id="dc667-117">Verwenden Sie folgendes Skript, um Schlüssel und Repository zu installieren:</span><span class="sxs-lookup"><span data-stu-id="dc667-117">Use the following script to install the key and repository:</span></span>

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    ```

1. <span data-ttu-id="dc667-118">Aktualisieren Sie den Paketcache, und installieren Sie das Paket mithilfe von „dnf“ (Fedora 22 und höher):</span><span class="sxs-lookup"><span data-stu-id="dc667-118">Update the package cache, and install the package by using dnf (Fedora 22 and above):</span></span>

    ```bash
    dnf check-update
    sudo dnf install code
    ```

### <a name="linux--opensuse-and-sle"></a><span data-ttu-id="dc667-119">Linux – openSUSE und SLE</span><span class="sxs-lookup"><span data-stu-id="dc667-119">Linux – openSUSE and SLE</span></span>

1. <span data-ttu-id="dc667-120">Das yum-Repository funktioniert ebenfalls für openSUSE- und SLE-basierte Systeme.</span><span class="sxs-lookup"><span data-stu-id="dc667-120">The yum repository also works for openSUSE and SLE based systems.</span></span> <span data-ttu-id="dc667-121">Mit folgendem Skript werden der Schlüssel und das Repository installiert:</span><span class="sxs-lookup"><span data-stu-id="dc667-121">The following script will install the key and repository:</span></span>

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
    ```

1. <span data-ttu-id="dc667-122">Aktualisieren Sie den Paketcache, und installieren Sie das Paket folgendermaßen:</span><span class="sxs-lookup"><span data-stu-id="dc667-122">Update the package cache and install the package by using:</span></span>

    ```bash
    sudo zypper refresh
    sudo zypper install code
    ```

> [!NOTE]
> <span data-ttu-id="dc667-123">Weitere Informationen zum Installieren oder Updaten von Visual Studio Code auf den verschiedenen Linux-Distributionen finden Sie in der Dokumentation [Running VS Code on Linux (Ausführen von Visual Studio Code unter Linux)](https://code.visualstudio.com/docs/setup/linux).</span><span class="sxs-lookup"><span data-stu-id="dc667-123">For further details about installing or updating VS Code on various Linux distributions, please see the [Running VS Code on Linux documentation](https://code.visualstudio.com/docs/setup/linux).</span></span>

## <a name="install-azure-app-service-extension"></a><span data-ttu-id="dc667-124">Installieren der Azure App Service-Erweiterung</span><span class="sxs-lookup"><span data-stu-id="dc667-124">Install Azure App Service extension</span></span>

<span data-ttu-id="dc667-125">Öffnen Sie Visual Studio Code, sobald die Installation abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="dc667-125">Once you have installed VS Code, open it.</span></span>

1. <span data-ttu-id="dc667-126">Navigieren Sie zur Registerkarte „Extensions“ (Erweiterungen)</span><span class="sxs-lookup"><span data-stu-id="dc667-126">Go to the Extensions tab.</span></span>
2. <span data-ttu-id="dc667-127">Suchen Sie nach „Azure App Service“.</span><span class="sxs-lookup"><span data-stu-id="dc667-127">Search for Azure App Service.</span></span>
3. <span data-ttu-id="dc667-128">Klicken Sie auf „Installieren“.</span><span class="sxs-lookup"><span data-stu-id="dc667-128">Click Install.</span></span>

    <span data-ttu-id="dc667-129">Der folgende Screenshot stellt die Azure App Service-Erweiterung dar, die in den Suchergebnissen für Visual Studio Code-Erweiterungen ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="dc667-129">The following screenshot shows the Azure App Service extension selected from the Visual Studio Code extension search results.</span></span>

    ![Screenshot von Visual Studio Code, der die Registerkarte „Erweiterungen“ mit der in den Suchergebnissen hervorgehobenen Azure App Service-Erweiterung darstellt.](../media/3-install-azure-extension.png)

<span data-ttu-id="dc667-131">Dadurch wird die Erweiterung installiert.</span><span class="sxs-lookup"><span data-stu-id="dc667-131">This will install the extension.</span></span> <span data-ttu-id="dc667-132">Sie können nun Ihr Azure-Abonnement verknüpfen, Web-Apps, mobile Apps oder API-Apps entwickeln und diese in Azure App Service bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="dc667-132">You will be ready to connect to your Azure subscription, and develop for and deploy your web, mobile, or API app to an Azure App Service.</span></span>
