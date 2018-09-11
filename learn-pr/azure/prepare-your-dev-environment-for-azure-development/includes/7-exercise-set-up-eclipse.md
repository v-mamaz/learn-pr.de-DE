<span data-ttu-id="269bb-101">In dieser Einheit installieren Sie Eclipse auf Ihrem lokalen Computer. Anschließend installieren Sie das Azure-Toolkit, um die Entwicklung von Java-Anwendungen mit Azure-Integration vorzubereiten.</span><span class="sxs-lookup"><span data-stu-id="269bb-101">In this unit, you will install Eclipse on your local machine and then install the Azure Toolkit, preparing you for developing Java applications with Azure integration.</span></span> <span data-ttu-id="269bb-102">Die Installation erfolgt schnell und einfach.</span><span class="sxs-lookup"><span data-stu-id="269bb-102">The installation is quick and simple.</span></span> <span data-ttu-id="269bb-103">Am Ende der Übung ist alles eingerichtet, was Sie für Ihre erste Java-Anwendung benötigen, für die Sie die Features und Dienste von Azure nutzen können.</span><span class="sxs-lookup"><span data-stu-id="269bb-103">At the end of the exercise, you will have everything set up that you need to start your first Java application, taking advantage of the features and services of Azure.</span></span>

## <a name="install-eclipse-ide"></a><span data-ttu-id="269bb-104">Installieren der Eclipse-IDE</span><span class="sxs-lookup"><span data-stu-id="269bb-104">Install Eclipse IDE</span></span>

1. <span data-ttu-id="269bb-105">Laden Sie die Eclipse-Version von http://www.eclipse.org/downloads/packages/installer herunter, die Ihrem Betriebssystem entspricht.</span><span class="sxs-lookup"><span data-stu-id="269bb-105">Download the Eclipse version that suits your operating system from http://www.eclipse.org/downloads/packages/installer.</span></span>

1. <span data-ttu-id="269bb-106">Starten Sie den Eclipse-Installer nach dem Download.</span><span class="sxs-lookup"><span data-stu-id="269bb-106">Start the Eclipse installer once downloaded.</span></span>

    1. <span data-ttu-id="269bb-107">Doppelklicken Sie unter Windows auf die heruntergeladene Datei.</span><span class="sxs-lookup"><span data-stu-id="269bb-107">On Windows, double-click the downloaded file.</span></span>

    1. <span data-ttu-id="269bb-108">Entpacken Sie den Installer unter macOS und Linux aus der heruntergeladenen Datei.</span><span class="sxs-lookup"><span data-stu-id="269bb-108">On macOS and Linux, unzip the installer from the downloaded file.</span></span> <span data-ttu-id="269bb-109">Starten Sie den Installer anschließend.</span><span class="sxs-lookup"><span data-stu-id="269bb-109">Then start the installer once unzipped.</span></span>

        > [!NOTE]
        > <span data-ttu-id="269bb-110">Wenn das Java Development Kit nicht vorhanden ist, fordert der Installer Sie möglicherweise dazu auf, dieses zu installieren.</span><span class="sxs-lookup"><span data-stu-id="269bb-110">The installer may prompt you to install the Java Development Kit, if it is missing.</span></span>

1. <span data-ttu-id="269bb-111">Wählen Sie die Pakete aus, die installiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="269bb-111">Select the packages to install.</span></span> <span data-ttu-id="269bb-112">Wenn Sie Java-Entwickler sind, wählen Sie die Eclipse-IDE für Java oder Java EE aus.</span><span class="sxs-lookup"><span data-stu-id="269bb-112">For Java developers, choose either the Java or Java EE Eclipse IDE option.</span></span>

1. <span data-ttu-id="269bb-113">Wählen Sie das Installationsziel auf Ihrem Computer aus.</span><span class="sxs-lookup"><span data-stu-id="269bb-113">Select the installation destination on your machine.</span></span>

1. <span data-ttu-id="269bb-114">Starten Sie Eclipse, um zu überprüfen, dass das Programm ordnungsgemäß installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="269bb-114">Launch Eclipse to validate that it installed correctly.</span></span>

## <a name="install-azure-toolkit-for-eclipse"></a><span data-ttu-id="269bb-115">Installieren des Azure-Toolkits für Eclipse</span><span class="sxs-lookup"><span data-stu-id="269bb-115">Install Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="269bb-116">Die Installation des Azure-Toolkits verläuft unter Windows, macOS und Linux gleich.</span><span class="sxs-lookup"><span data-stu-id="269bb-116">Installing the Azure Toolkit is the same across Windows, macOS, and Linux.</span></span>

1. <span data-ttu-id="269bb-117">Starten Sie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="269bb-117">Start Eclipse.</span></span>

1. <span data-ttu-id="269bb-118">Navigieren Sie zu **Help** > **Install New Software...** (Hilfe > Neue Software installieren...).</span><span class="sxs-lookup"><span data-stu-id="269bb-118">Go to **Help** > **Install New Software...**.</span></span>

    <span data-ttu-id="269bb-119">Der folgende Screenshot zeigt die Position von **Install New Software...** (Neue Software installieren...) im Menü an.</span><span class="sxs-lookup"><span data-stu-id="269bb-119">The following screenshot shows the menu location of the **Install New Software...** item.</span></span>

    ![Screenshot der Option „Install New Software“ (Neue Software installieren), die im Hilfemenü von Eclipse hervorgehoben ist.](../media/7-eclipse-install-new-software.png)

1. <span data-ttu-id="269bb-121">Das Dialogfeld **Available Software** (Verfügbare Software) wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="269bb-121">The **Available Software** dialog will open.</span></span> <span data-ttu-id="269bb-122">Geben Sie `http://dl.microsoft.com/eclipse/` in das Textfeld **Work with:** (Arbeiten mit:) ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="269bb-122">In the **Work with:** text box, type `http://dl.microsoft.com/eclipse/` and press Enter.</span></span>

1. <span data-ttu-id="269bb-123">Überprüfen Sie die Option **Azure Toolkit for Java** (Azure-Toolkit für Java) in den Ergebnissen.</span><span class="sxs-lookup"><span data-stu-id="269bb-123">In the results, check the **Azure Toolkit for Java** option.</span></span> <span data-ttu-id="269bb-124">Stellen Sie sicher, dass Sie die Option **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu suchen) deaktivieren, sofern dies noch nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="269bb-124">Make sure you uncheck the **Contact all update sites during install to find required software** option, if it isn't already.</span></span>

    <span data-ttu-id="269bb-125">Im folgenden Screenshot wird die oben beschriebene Installationskonfiguration von **Available Software** (Verfügbare Software) dargestellt.</span><span class="sxs-lookup"><span data-stu-id="269bb-125">The following screenshot shows the **Available Software** install configuration as described above.</span></span>

    ![Screenshot des Fensters „Available Software“ (Verfügbare Software) in Eclipse mit Feldern, die die Konfigurationen hervorheben, die zum Suchen und Installieren des Azure-Toolkits für Java erforderlich sind.](../media/7-eclipse-download-azure-toolkit-for-java.png)

1. <span data-ttu-id="269bb-127">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="269bb-127">Click **Next**.</span></span>

1. <span data-ttu-id="269bb-128">Lesen und akzeptieren Sie die Lizenzbedingungen, wenn Sie dazu aufgefordert werden, und klicken Sie auf **Finish** (Fertig stellen).</span><span class="sxs-lookup"><span data-stu-id="269bb-128">Review and accept the license agreements when prompted, and click **Finish**.</span></span>

1. <span data-ttu-id="269bb-129">Eclipse lädt das Azure-Toolkit herunter und installiert es.</span><span class="sxs-lookup"><span data-stu-id="269bb-129">Eclipse will download and install the Azure Toolkit.</span></span>

1. <span data-ttu-id="269bb-130">Starten Sie Eclipse neu (falls erforderlich).</span><span class="sxs-lookup"><span data-stu-id="269bb-130">Restart Eclipse if required.</span></span>

1. <span data-ttu-id="269bb-131">Überprüfen Sie die Installation des Azure-Toolkits, indem Sie sicherstellen, dass die Menüoption **Tools** > **Azure** in Eclipse vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="269bb-131">Validate installation of Azure Toolkit by verifying that you can find a **Tools** > **Azure** menu option in Eclipse.</span></span>

## <a name="summary"></a><span data-ttu-id="269bb-132">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="269bb-132">Summary</span></span>

<span data-ttu-id="269bb-133">In dieser Einheit haben Sie Eclipse für Java installiert und die Integration mit Azure-Diensten und -Produkten vorbereitet.</span><span class="sxs-lookup"><span data-stu-id="269bb-133">In this unit, you installed Eclipse for Java, and prepared it to take advantage of the integration with Azure services and products.</span></span> <span data-ttu-id="269bb-134">Die Installation erfolgt schnell und einfach, wodurch Eclipse für die Java-Entwicklung mit Integration in Clouddienste optimal geeignet ist.</span><span class="sxs-lookup"><span data-stu-id="269bb-134">The installation is quick and straightforward, making Eclipse ideal for the task of Java development with cloud services integration.</span></span>
