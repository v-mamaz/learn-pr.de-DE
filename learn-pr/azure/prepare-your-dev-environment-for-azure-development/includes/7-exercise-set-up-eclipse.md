<span data-ttu-id="3dcfc-101">In dieser Einheit installieren Sie Eclipse und das Azure-Toolkit auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-101">In this unit, you will install Eclipse and the Azure Toolkit on your local machine.</span></span> <span data-ttu-id="3dcfc-102">Die Installation erfolgt schnell und einfach.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-102">The installation is quick and simple.</span></span> <span data-ttu-id="3dcfc-103">Am Ende der Übung verfügen Sie über alles, was Sie benötigen, um Ihre erste Java-Anwendung in Azure zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-103">At the end of the exercise, you will have everything you need to create your first Java application on Azure.</span></span>

## <a name="install-eclipse-ide"></a><span data-ttu-id="3dcfc-104">Installieren der Eclipse-IDE</span><span class="sxs-lookup"><span data-stu-id="3dcfc-104">Install Eclipse IDE</span></span>

1. <span data-ttu-id="3dcfc-105">Laden Sie die Eclipse-Version von http://www.eclipse.org/downloads/packages/installer herunter, die Ihrem Betriebssystem entspricht.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-105">Download the Eclipse version that suits your operating system from http://www.eclipse.org/downloads/packages/installer.</span></span>

1. <span data-ttu-id="3dcfc-106">Starten Sie den Eclipse-Installer nach dem Download.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-106">Start the Eclipse installer once downloaded.</span></span>

    1. <span data-ttu-id="3dcfc-107">Doppelklicken Sie unter Windows auf die heruntergeladene Datei.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-107">On Windows, double-click the downloaded file.</span></span>

    1. <span data-ttu-id="3dcfc-108">Entpacken Sie den Installer unter macOS und Linux aus der heruntergeladenen Datei, und führen Sie ihn aus.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-108">On macOS and Linux, unzip the installer from the downloaded file and run it.</span></span>

        > [!NOTE]
        > <span data-ttu-id="3dcfc-109">Wenn das Java Development Kit nicht vorhanden ist, fordert der Installer Sie möglicherweise dazu auf, dieses zu installieren.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-109">The installer may prompt you to install the Java Development Kit, if it is missing.</span></span>

1. <span data-ttu-id="3dcfc-110">Wählen Sie die Pakete aus, die installiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-110">Select the packages to install.</span></span> <span data-ttu-id="3dcfc-111">Wenn Sie Java-Entwickler sind, wählen Sie die Eclipse-IDE für Java oder Java EE aus.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-111">For Java developers, choose either the Java or Java EE Eclipse IDE option.</span></span>

1. <span data-ttu-id="3dcfc-112">Wählen Sie das Installationsziel auf Ihrem Computer aus.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-112">Select the installation destination on your machine.</span></span>

1. <span data-ttu-id="3dcfc-113">Starten Sie Eclipse, um zu überprüfen, dass das Programm ordnungsgemäß installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-113">Launch Eclipse to validate that it installed correctly.</span></span>

## <a name="install-azure-toolkit-for-eclipse"></a><span data-ttu-id="3dcfc-114">Installieren des Azure-Toolkits für Eclipse</span><span class="sxs-lookup"><span data-stu-id="3dcfc-114">Install Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="3dcfc-115">Die Installation des Azure-Toolkits verläuft unter Windows, macOS und Linux gleich.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-115">Installing the Azure Toolkit is the same across Windows, macOS, and Linux.</span></span>

1. <span data-ttu-id="3dcfc-116">Starten Sie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-116">Start Eclipse.</span></span>

1. <span data-ttu-id="3dcfc-117">Navigieren Sie zu **Help** > **Install New Software...** (Hilfe > Neue Software installieren...).</span><span class="sxs-lookup"><span data-stu-id="3dcfc-117">Go to **Help** > **Install New Software...**.</span></span>

    <span data-ttu-id="3dcfc-118">Der folgende Screenshot zeigt die Position von **Install New Software...** (Neue Software installieren...) im Menü an.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-118">The following screenshot shows the menu location of the **Install New Software...** item.</span></span>

    ![Screenshot der Option „Install New Software“ (Neue Software installieren), die im Hilfemenü von Eclipse hervorgehoben ist.](../media/7-eclipse-install-new-software.png)

1. <span data-ttu-id="3dcfc-120">Das Dialogfeld **Available Software** (Verfügbare Software) wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-120">The **Available Software** dialog will open.</span></span> <span data-ttu-id="3dcfc-121">Geben Sie `http://dl.microsoft.com/eclipse/` in das Textfeld **Work with:** (Arbeiten mit:) ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-121">In the **Work with:** text box, type `http://dl.microsoft.com/eclipse/` and press Enter.</span></span>

1. <span data-ttu-id="3dcfc-122">Überprüfen Sie die Option **Azure Toolkit for Java** (Azure-Toolkit für Java) in den Ergebnissen.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-122">In the results, check the **Azure Toolkit for Java** option.</span></span> <span data-ttu-id="3dcfc-123">Stellen Sie sicher, dass Sie die Option **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu suchen) deaktivieren, sofern dies noch nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-123">Make sure you uncheck the **Contact all update sites during install to find required software** option, if it isn't already.</span></span>

    <span data-ttu-id="3dcfc-124">Im folgenden Screenshot wird die oben beschriebene Installationskonfiguration von **Available Software** (Verfügbare Software) dargestellt.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-124">The following screenshot shows the **Available Software** install configuration as described above.</span></span>

    ![Screenshot des Fensters „Available Software“ (Verfügbare Software) in Eclipse mit Feldern, die die Konfigurationen hervorheben, die zum Suchen und Installieren des Azure-Toolkits für Java erforderlich sind.](../media/7-eclipse-download-azure-toolkit-for-java.png)

1. <span data-ttu-id="3dcfc-126">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-126">Click **Next**.</span></span>

1. <span data-ttu-id="3dcfc-127">Lesen und akzeptieren Sie die Lizenzbedingungen, wenn Sie dazu aufgefordert werden, und klicken Sie auf **Finish** (Fertig stellen).</span><span class="sxs-lookup"><span data-stu-id="3dcfc-127">Review and accept the license agreements when prompted, and click **Finish**.</span></span>

1. <span data-ttu-id="3dcfc-128">Eclipse lädt das Azure-Toolkit herunter und installiert es.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-128">Eclipse will download and install the Azure Toolkit.</span></span>

1. <span data-ttu-id="3dcfc-129">Starten Sie Eclipse neu (falls erforderlich).</span><span class="sxs-lookup"><span data-stu-id="3dcfc-129">Restart Eclipse if required.</span></span>

1. <span data-ttu-id="3dcfc-130">Überprüfen Sie die Installation des Azure-Toolkits, indem Sie sicherstellen, dass die Menüoption **Tools** > **Azure** in Eclipse vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-130">Validate the Azure Toolkit installation by verifying that you can find a **Tools** > **Azure** menu option in Eclipse.</span></span>

## <a name="summary"></a><span data-ttu-id="3dcfc-131">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="3dcfc-131">Summary</span></span>

<span data-ttu-id="3dcfc-132">In dieser Einheit haben Sie Eclipse installiert und die Integration mit Azure-Diensten und -Produkten vorbereitet.</span><span class="sxs-lookup"><span data-stu-id="3dcfc-132">In this unit, you installed Eclipse and prepared it to take advantage of the integration with Azure services and products.</span></span>