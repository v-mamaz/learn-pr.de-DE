<span data-ttu-id="9f88c-101">Angenommen, Sie verwenden Azure PowerShell als Automatisierungslösung.</span><span class="sxs-lookup"><span data-stu-id="9f88c-101">Suppose you have chosen Azure PowerShell as your automation solution.</span></span> <span data-ttu-id="9f88c-102">Ihre Administratoren führen Skripts lieber lokal als in Azure Cloud Shell aus.</span><span class="sxs-lookup"><span data-stu-id="9f88c-102">Your administrators prefer to run their scripts locally rather than in the Azure Cloud Shell.</span></span> <span data-ttu-id="9f88c-103">Sie verwenden Computer, auf denen Linux, macOS oder Windows ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="9f88c-103">The team uses machines that run Linux, macOS, and Windows.</span></span> <span data-ttu-id="9f88c-104">Azure PowerShell muss auf all diesen Geräten funktionieren.</span><span class="sxs-lookup"><span data-stu-id="9f88c-104">You need to get Azure PowerShell working on all their devices.</span></span> 

## <a name="what-must-be-installed"></a><span data-ttu-id="9f88c-105">Was muss installiert werden?</span><span class="sxs-lookup"><span data-stu-id="9f88c-105">What must be installed?</span></span>
<span data-ttu-id="9f88c-106">Die eigentliche Installationsanleitung folgt im nächsten Teil. Betrachten wir jedoch zunächst die beiden Komponenten, aus denen Azure PowerShell besteht.</span><span class="sxs-lookup"><span data-stu-id="9f88c-106">We'll go through the actual installation instructions in the next unit, but let's look at the two components which make up Azure PowerShell.</span></span>

- <span data-ttu-id="9f88c-107">**Das PowerShell-Basisprodukt** ist in zwei Varianten verfügbar: PowerShell für Windows und PowerShell Core für macOS und Linux.</span><span class="sxs-lookup"><span data-stu-id="9f88c-107">**The base PowerShell product** This comes in two variants: PowerShell on Windows, and PowerShell Core on macOS and Linux.</span></span>
- <span data-ttu-id="9f88c-108">**Das spezielle Azure PowerShell-Modul** muss installiert werden, um PowerShell die Azure-spezifischen Befehle hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="9f88c-108">**The Azure PowerShell module** This extra module must be installed to add the Azure-specific commands to PowerShell.</span></span>

> [!TIP]
> <span data-ttu-id="9f88c-109">PowerShell ist im Lieferumfang von Windows enthalten. Allerdings müssen Sie ggf. ein Update ausführen.</span><span class="sxs-lookup"><span data-stu-id="9f88c-109">PowerShell is included with Windows (but might have an update available).</span></span> <span data-ttu-id="9f88c-110">Installieren Sie für Linux und macOS PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="9f88c-110">You will need to install PowerShell Core on Linux and macOS.</span></span>

<span data-ttu-id="9f88c-111">Sobald das Basisprodukt installiert ist, fügen Sie Ihrer Installation das Azure PowerShell-Modul hinzu.</span><span class="sxs-lookup"><span data-stu-id="9f88c-111">Once the base product is installed, you then add the Azure PowerShell module to your installation.</span></span>

## <a name="how-to-install-powershell-core"></a><span data-ttu-id="9f88c-112">Installieren von PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="9f88c-112">How to install PowerShell Core</span></span>
<span data-ttu-id="9f88c-113">Verwenden Sie unter Linux und macOS einen Paket-Manager, um PowerShell Core zu installieren.</span><span class="sxs-lookup"><span data-stu-id="9f88c-113">On both Linux and macOS, you use a package manager to install PowerShell Core.</span></span> <span data-ttu-id="9f88c-114">Der empfohlene Paket-Manager unterscheidet sich je nach Betriebssystem und Distribution.</span><span class="sxs-lookup"><span data-stu-id="9f88c-114">The recommended package manager differs by OS and distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="9f88c-115">PowerShell Core ist im Microsoft-Repository verfügbar, sodass Sie zuerst dieses Repository dem Paket-Manager hinzufügen müssen.</span><span class="sxs-lookup"><span data-stu-id="9f88c-115">PowerShell Core is available in the Microsoft repository, so you'll first need to add that repository to your package manager.</span></span>

### <a name="linux"></a><span data-ttu-id="9f88c-116">Linux</span><span class="sxs-lookup"><span data-stu-id="9f88c-116">Linux</span></span>
<span data-ttu-id="9f88c-117">Unter Linux unterscheidet sich der Paket-Manager je nach Distribution.</span><span class="sxs-lookup"><span data-stu-id="9f88c-117">On Linux, the package manager will change based on the Linux distribution you choose.</span></span>

| <span data-ttu-id="9f88c-118">Distribution(en)</span><span class="sxs-lookup"><span data-stu-id="9f88c-118">Distribution(s)</span></span>  | <span data-ttu-id="9f88c-119">Paket-Manager</span><span class="sxs-lookup"><span data-stu-id="9f88c-119">Package manager</span></span> |
|------------------|-----------------|
| <span data-ttu-id="9f88c-120">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="9f88c-120">Ubuntu, Debian</span></span>   | `apt-get`       |
| <span data-ttu-id="9f88c-121">Red Hat/CentOS</span><span class="sxs-lookup"><span data-stu-id="9f88c-121">Red Hat, CentOS</span></span>  | `yum`           |
| <span data-ttu-id="9f88c-122">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="9f88c-122">OpenSUSE</span></span>         | `zypper`        |
| <span data-ttu-id="9f88c-123">Fedora</span><span class="sxs-lookup"><span data-stu-id="9f88c-123">Fedora</span></span>           | `dnf`           |

### <a name="mac"></a><span data-ttu-id="9f88c-124">Mac</span><span class="sxs-lookup"><span data-stu-id="9f88c-124">Mac</span></span>
<span data-ttu-id="9f88c-125">Verwenden Sie unter macOS `Homebrew`, um PowerShell Core zu installieren.</span><span class="sxs-lookup"><span data-stu-id="9f88c-125">On macOS, you will use `Homebrew` to install PowerShell Core.</span></span>

<span data-ttu-id="9f88c-126">Der nächste Abschnitt behandelt die einzelnen Installationsschritte auf einigen gängigen Plattformen.</span><span class="sxs-lookup"><span data-stu-id="9f88c-126">In the next section, you will go through the detailed installation steps for some common platforms.</span></span>