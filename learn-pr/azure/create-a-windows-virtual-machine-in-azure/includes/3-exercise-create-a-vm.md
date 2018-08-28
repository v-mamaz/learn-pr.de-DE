<span data-ttu-id="7555a-101">In dieser Übung erstellen Sie einen virtuellen Windows-Computer in Azure.</span><span class="sxs-lookup"><span data-stu-id="7555a-101">In this exercise, you'll create a Windows virtual machine in Azure.</span></span>

## <a name="motivation"></a><span data-ttu-id="7555a-102">Motivation</span><span class="sxs-lookup"><span data-stu-id="7555a-102">Motivation</span></span>

<span data-ttu-id="7555a-103">Gehen wir für diese Übung von einem alternativen Szenario aus.</span><span class="sxs-lookup"><span data-stu-id="7555a-103">Let's consider an alternate scenario for this exercise.</span></span> <span data-ttu-id="7555a-104">In diesem ist Ihre Organisation eine Schule, in der auf virtuellen Windows-Computern Testumgebungen bereitgestellt werden. In diesen haben Schüler die Möglichkeit, Web-Apps zu installieren, Domänen zu konfigurieren und Windows-Dienste und -Features auszuprobieren, ohne die Funktionalität der Schulcomputer zu beeinflussen.</span><span class="sxs-lookup"><span data-stu-id="7555a-104">Here, your organization is a school that uses Windows virtual machines to spin up test environments on which students install web apps, configure domains, and explore Windows services and features without affecting the school's computers.</span></span> <span data-ttu-id="7555a-105">Lehrer können mithilfe von RDP eine Verbindung mit diesen virtuellen Computern herstellen und den Bearbeitungsfortschritt der Schüleraufgaben überprüfen.</span><span class="sxs-lookup"><span data-stu-id="7555a-105">Teachers connect to these VMs by using RDP and check on student progress.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="7555a-106">Erstellen eines virtuellen Windows-Computers</span><span class="sxs-lookup"><span data-stu-id="7555a-106">Create a Windows VM</span></span>

<span data-ttu-id="7555a-107">Gehen Sie zum Erstellen eines virtuellen Windows-Computers wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="7555a-107">To create a Windows VM, complete the following steps:</span></span>

1. <span data-ttu-id="7555a-108">Melden Sie sich über das [Azure-Portal](https://portal.azure.com) bei Azure an.</span><span class="sxs-lookup"><span data-stu-id="7555a-108">Log onto Azure through the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="7555a-109">Klicken Sie im Azure-Portal oben links auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="7555a-109">Click **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="7555a-110">Geben Sie **Windows Server 2016 Datacenter** in der **Suchleiste** ein, und klicken Sie anschließend auf den gleichnamigen Link.</span><span class="sxs-lookup"><span data-stu-id="7555a-110">In the **search bar**, enter  **Windows Server 2016 Datacenter**  and then click on the link with the same title.</span></span>

### <a name="configure-the-vm-settings"></a><span data-ttu-id="7555a-111">Konfigurieren der Einstellungen für den virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="7555a-111">Configure the VM settings</span></span>

1. <span data-ttu-id="7555a-112">Geben Sie unter **Grundeinstellungen** im Feld **Name** einen Namen für Ihren virtuellen Computer ein, z.B. „SchülerVM“.</span><span class="sxs-lookup"><span data-stu-id="7555a-112">Under **Basics**, in the **Name** field, enter a name for your VM, such as "StudentVM."</span></span>

1. <span data-ttu-id="7555a-113">Klicken Sie im Feld **VM-Datenträgertyp** auf das Dropdownmenü, um sich alle Optionen anzeigen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="7555a-113">In the **VM Disk Type** field, click the drop-down menu to see the options.</span></span> <span data-ttu-id="7555a-114">Stellen Sie sicher, dass **SSD** ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="7555a-114">Ensure that **SSD** is selected.</span></span>

1. <span data-ttu-id="7555a-115">Geben Sie im Feld **Benutzername** einen geeigneten Benutzernamen ein, der zur Anmeldung beim virtuellen Computer verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7555a-115">In the **Username** field, enter a suitable user name to use to sign in to the VM.</span></span>

1. <span data-ttu-id="7555a-116">Geben Sie im Feld **Kennwort** ein Kennwort ein, das mindestens zwölf Zeichen lang ist.</span><span class="sxs-lookup"><span data-stu-id="7555a-116">In the **Password** field, enter a password that's at least 12 characters long.</span></span> <span data-ttu-id="7555a-117">Es muss Groß- und Kleinbuchstaben, Ziffern und Sonderzeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="7555a-117">It must also have upper and lowercase characters, numbers, and special characters.</span></span>

1. <span data-ttu-id="7555a-118">Klicken Sie unter **Ressourcengruppe** auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="7555a-118">Under **Resource group**, click **Create new**.</span></span> <span data-ttu-id="7555a-119">Geben Sie für die Ressourcengruppe einen Namen ein, z.B. „MeineTestRG“.</span><span class="sxs-lookup"><span data-stu-id="7555a-119">Give the resource group a name, such as "myTestRG."</span></span>

1. <span data-ttu-id="7555a-120">Wählen Sie einen geeigneten Speicherort für den virtuellen Computer aus, der erstellt werden soll, und klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7555a-120">Select a suitable location for the VM to be created, and then click **OK**.</span></span>

### <a name="select-the-vm-image-size-and-options"></a><span data-ttu-id="7555a-121">Auswählen der Größe und der Optionen des virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="7555a-121">Select the VM image size and options</span></span>

1. <span data-ttu-id="7555a-122">Klicken Sie auf der Seite **Größe auswählen** zuerst auf das Image **B1s** und anschließend auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="7555a-122">In the **Choose a size** page, click the **B1s** image, and then click **Select**.</span></span>

   > [!Note] 
   > <span data-ttu-id="7555a-123">Das B1-Image verfügt nur über 1 GB RAM. Dies führt bei der erstmaligen Anmeldung zu Speicherfehlern.</span><span class="sxs-lookup"><span data-stu-id="7555a-123">The B1 image has only 1 GB of RAM and will result in memory errors when you first sign in.</span></span> <span data-ttu-id="7555a-124">Sie können die Größe des Images jedoch später über eine Registerkarte anpassen.</span><span class="sxs-lookup"><span data-stu-id="7555a-124">However, you can resize the image later as part of a later lab.</span></span>

1. <span data-ttu-id="7555a-125">Klicken Sie auf der Seite **Einstellungen** unter **Öffentliche Eingangsports hinzufügen** auf **No public inbound ports** (Keine öffentlichen Eingangsports).</span><span class="sxs-lookup"><span data-stu-id="7555a-125">In the **Settings** page, under **Select Public Inbound Ports**, select **No public inbound ports**.</span></span> <span data-ttu-id="7555a-126">Den RDP-Zugriff konfigurieren Sie später.</span><span class="sxs-lookup"><span data-stu-id="7555a-126">We'll configure RDP access later.</span></span>

### <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="7555a-127">Abschließen der Konfiguration des virtuellen Computers und Erstellen des Images</span><span class="sxs-lookup"><span data-stu-id="7555a-127">Finish configuring the VM and create the image</span></span>

1. <span data-ttu-id="7555a-128">Scrollen Sie nach unten, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7555a-128">Scroll to the bottom and click **OK**.</span></span>

1. <span data-ttu-id="7555a-129">Überprüfen Sie unter **Erstellen** die konfigurierten Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="7555a-129">Under **Create**, check the settings that you configured.</span></span> <span data-ttu-id="7555a-130">Klicken Sie unten auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="7555a-130">At the bottom, click **Create**.</span></span> <span data-ttu-id="7555a-131">Im Azure-Dashboard wird der virtuelle Computer angezeigt, der aktuell bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="7555a-131">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="7555a-132">Dieser Vorgang kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="7555a-132">This may take several minutes.</span></span>

## <a name="summary"></a><span data-ttu-id="7555a-133">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="7555a-133">Summary</span></span>

<span data-ttu-id="7555a-134">In dieser Übung haben Sie einen virtuellen Windows Server-Computer erstellt, der von Schülern genutzt werden kann und über das Schulnetzwerk erreichbar ist.</span><span class="sxs-lookup"><span data-stu-id="7555a-134">You've now created a Windows Server virtual machine that's suitable for student requirements and accessible from the school network.</span></span> <span data-ttu-id="7555a-135">In der nächsten Lektion erfahren Sie, wie Sie mithilfe von RDP eine Verbindung mit dem virtuellen Computer herstellen und diesen verwalten.</span><span class="sxs-lookup"><span data-stu-id="7555a-135">In the next unit, you will look at how you connect to and manage that VM by using RDP.</span></span>
