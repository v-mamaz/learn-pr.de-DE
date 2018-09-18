<span data-ttu-id="96e34-101">In dieser Übung erstellen Sie in Microsoft Azure ein virtuelles Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="96e34-101">In this exercise, you will create a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="96e34-102">Anschließend erstellen Sie zwei virtuelle Computer und verwenden das virtuelle Netzwerk, um die virtuellen Computer miteinander und mit dem Internet zu verbinden.</span><span class="sxs-lookup"><span data-stu-id="96e34-102">You will then create two virtual machines and use the virtual network to connect the virtual machines to each other and to the internet.</span></span>

<span data-ttu-id="96e34-103">Vor Beginn dieser Einheit müssen Sie sich mit den Anmeldeinformationen Ihres Testabonnements bei [Azure Cloud Shell](https://shell.azure.com) anmelden.</span><span class="sxs-lookup"><span data-stu-id="96e34-103">Before you begin this unit, you will need to log into [Azure Cloud Shell](https://shell.azure.com) with your trial subscription credentials.</span></span> <span data-ttu-id="96e34-104">Wir verwenden Azure Cloud Shell, um die Ressourcengruppen, die virtuellen Netzwerke und die virtuellen Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="96e34-104">We will use Azure Cloud Shell to create the resource groups, virtual networks, and virtual machines.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="96e34-105">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="96e34-105">Create a resource group</span></span>

1. <span data-ttu-id="96e34-106">Klicken Sie im Fenster **Welcome to Azure Cloud Shell** (Willkommen bei Azure Cloud Shell) auf **PowerShell (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="96e34-106">In the **Welcome to Azure Cloud Shell** window, click **PowerShell (Linux)**.</span></span>

1. <span data-ttu-id="96e34-107">Klicken Sie im Fenster **You have no storage mounted** (Sie haben keinen Speicher bereitgestellt) auf **Speicher erstellen**.</span><span class="sxs-lookup"><span data-stu-id="96e34-107">In the **you have no storage mounted** window, click **Create Storage**.</span></span>

1. <span data-ttu-id="96e34-108">Geben Sie an der Azure PowerShell-Eingabeaufforderung den folgenden Code ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="96e34-108">In the Azure PowerShell command-line prompt, type the following code and press Enter.</span></span>

    ```PowerShell
    az group create --name myResourceGroup --location eastus
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="96e34-109">Erstellen eines virtuellen Netzwerks</span><span class="sxs-lookup"><span data-stu-id="96e34-109">Create a virtual network</span></span>

1. <span data-ttu-id="96e34-110">Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE, um ein virtuelles Netzwerk zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="96e34-110">To create a virtual network, enter the following command and press Enter.</span></span>

    ```PowerShell
    az network vnet create --name myVirtualNetwork --resource-group myResourceGroup --subnet-name default
    ```

## <a name="create-two-virtual-machines"></a><span data-ttu-id="96e34-111">Erstellen von zwei virtuellen Computern</span><span class="sxs-lookup"><span data-stu-id="96e34-111">Create two virtual machines</span></span>

1. <span data-ttu-id="96e34-112">Erstellen Sie den ersten virtuellen Computer. Führen Sie dazu den folgenden Befehl aus, um einen virtuellen Windows-Computer mit einer öffentlichen IP-Adresse zu erstellen, auf die über den Port 3389 (Remotedesktop) zugegriffen werden kann:</span><span class="sxs-lookup"><span data-stu-id="96e34-112">To create the first virtual machine, execute the following command to create a Windows VM with a public IP address that is accessible over port 3389 (Remote Desktop):</span></span>

    ``` PowerShell
    az vm create --name dataProcessingStage1 --resource-group MyResourceGroup --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. <span data-ttu-id="96e34-113">Geben Sie an den Eingabeaufforderungen Werte für Ihr Kennwort ein.</span><span class="sxs-lookup"><span data-stu-id="96e34-113">Supply values for your password at the prompts.</span></span>

1. <span data-ttu-id="96e34-114">Führen Sie den folgenden Befehl aus, um einen virtuellen Windows-Computer ohne öffentliche IP-Adresse zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="96e34-114">Execute the following command to create a Windows VM without a public IP address:</span></span>

    ```PowerShell
    az vm create -n dataProcessingStage2 -g MyResourceGroup --public-ip-address '' --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. <span data-ttu-id="96e34-115">Nach Abschluss des Vorgangs enthält die Ausgabe des zweiten Befehls einen Wert für „publicIpAddress“.</span><span class="sxs-lookup"><span data-stu-id="96e34-115">When completed, the output from the second command will return a value for publicIpAddress.</span></span>

## <a name="connect-to-dataprocessingstage1-using-remote-desktop"></a><span data-ttu-id="96e34-116">Herstellen einer Remotedesktopverbindung mit „dataProcessingStage1“</span><span class="sxs-lookup"><span data-stu-id="96e34-116">Connect to dataProcessingStage1 using Remote Desktop</span></span>

1. <span data-ttu-id="96e34-117">Drücken Sie auf Ihrem Clientcomputer die Windows-Taste, und geben Sie „RDP“ ein.</span><span class="sxs-lookup"><span data-stu-id="96e34-117">On your client computer, press the Windows key and type RDP.</span></span>

1. <span data-ttu-id="96e34-118">Vergewissern Sie sich, dass die App **Remotedesktopverbindung** ausgewählt ist, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="96e34-118">Ensure that **Remote Desktop Connection** app is selected, and then press Enter.</span></span>

1. <span data-ttu-id="96e34-119">Geben Sie im Dialogfeld **Remotedesktopverbindung** im Feld **Computer** den Wert von „dataProcessingStage1PublicIPAddress“ ein, und klicken Sie anschließend auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="96e34-119">In the **Remote Desktop Connection** dialog box, in the **Computer** field, enter the value of dataProcessingStage1PublicIPAddress, and then click **Connect**.</span></span>

1. <span data-ttu-id="96e34-120">Klicken **Sie im Dialogfeld mit der Frage, ob Sie dieser Remoteverbindung**vertrauen, auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="96e34-120">In the **Do you trust this remote connection?** dialog box, click **Connect**.</span></span>

1. <span data-ttu-id="96e34-121">Geben Sie im Dialogfeld **Windows-Sicherheit** den Benutzernamen und das Kennwort ein, den bzw. das Sie bei der Erstellung von „dataProcessingStage1“ verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="96e34-121">In the **Windows Security** dialog box, enter the user name and password you used when you created dataProcessingStage1.</span></span>

1. <span data-ttu-id="96e34-122">Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="96e34-122">In the **Remote Desktop Connection** dialog box, click **OK**.</span></span>

1. <span data-ttu-id="96e34-123">Melden Sie sich bei dem Remotecomputer in Azure an.</span><span class="sxs-lookup"><span data-stu-id="96e34-123">Sign in to the remote computer in Azure.</span></span>

1. <span data-ttu-id="96e34-124">Klicken Sie in der Meldung **Netzwerke** auf **Nein**.</span><span class="sxs-lookup"><span data-stu-id="96e34-124">When the **Networks** message appears, click **No**.</span></span>

1. <span data-ttu-id="96e34-125">Schließen Sie den Server-Manager.</span><span class="sxs-lookup"><span data-stu-id="96e34-125">Close Server Manager.</span></span>

1. <span data-ttu-id="96e34-126">Klicken Sie in der Remotesitzung mit der rechten Maustaste auf das Startmenü, und klicken Sie auf **Eingabeaufforderung**.</span><span class="sxs-lookup"><span data-stu-id="96e34-126">In the remote session, right-click the Windows key and click **Command Prompt**.</span></span>

1. <span data-ttu-id="96e34-127">Geben Sie im Eingabeaufforderungsfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="96e34-127">In the command prompt window, type the following command and press Enter.</span></span>

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. <span data-ttu-id="96e34-128">Vom Remotecomputer sollte keine Antwort zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="96e34-128">There should be no response from the remote computer.</span></span> <span data-ttu-id="96e34-129">Das liegt daran, dass ICMP-Antworten standardmäßig von der Windows-Firewall blockiert werden.</span><span class="sxs-lookup"><span data-stu-id="96e34-129">This is because by default, Windows Firewall prevents ICMP responses.</span></span>

## <a name="connect-to-dataprocessingstage2-using-remote-desktop"></a><span data-ttu-id="96e34-130">Herstellen einer Remotedesktopverbindung mit „dataProcessingStage2“</span><span class="sxs-lookup"><span data-stu-id="96e34-130">Connect to dataProcessingStage2 using Remote Desktop</span></span>

1. <span data-ttu-id="96e34-131">Drücken Sie auf Ihrem Clientcomputer die Windows-Taste, und geben Sie **RDP** ein.</span><span class="sxs-lookup"><span data-stu-id="96e34-131">On your client computer, press the Windows key and type **RDP**.</span></span> <span data-ttu-id="96e34-132">Wählen Sie die App **Remotedesktopverbindung** aus, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="96e34-132">Select the **Remote Desktop Connection** app and press Enter.</span></span>

1. <span data-ttu-id="96e34-133">Geben Sie im Feld **Computer** den Wert von „dataProcessingStage2PublicIPAddress“ ein, und klicken Sie anschließend auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="96e34-133">In the **Computer** field, enter the value of dataProcessingStage2PublicIPAddress, and then click **Connect**.</span></span>

1. <span data-ttu-id="96e34-134">Klicken **Sie im Dialogfeld mit der Frage, ob Sie dieser Remoteverbindung**vertrauen, auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="96e34-134">In the **Do you trust this remote connection?** dialog box, click **Connect**.</span></span>

1. <span data-ttu-id="96e34-135">Geben Sie im Dialogfeld **Windows-Sicherheit** den Benutzernamen und das Kennwort ein, den bzw. das Sie bei der Erstellung von „dataProcessingStage2“ verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="96e34-135">In the **Windows Security** dialog box, enter the user name and password you used when you created dataProcessingStage2.</span></span>

1. <span data-ttu-id="96e34-136">Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="96e34-136">In the **Remote Desktop Connection** dialog box, click **OK**.</span></span> <span data-ttu-id="96e34-137">Melden Sie sich nun bei dem Remotecomputer in Azure an.</span><span class="sxs-lookup"><span data-stu-id="96e34-137">You now sign in to the remote computer in Azure.</span></span>

1. <span data-ttu-id="96e34-138">Klicken Sie in der Meldung **Netzwerke** auf **Nein**.</span><span class="sxs-lookup"><span data-stu-id="96e34-138">When the **Networks** message appears, click **No**.</span></span>

1. <span data-ttu-id="96e34-139">Schließen Sie den Server-Manager.</span><span class="sxs-lookup"><span data-stu-id="96e34-139">Close Server Manager.</span></span>

1. <span data-ttu-id="96e34-140">Drücken Sie auf „DataProcessingStage2“ die Windows-Taste, geben Sie **Firewall** ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="96e34-140">On dataProcessingStage2, press the Windows key, type **Firewall**, and press Enter.</span></span> <span data-ttu-id="96e34-141">Die Konsole **Windows-Firewall mit erweiterter Sicherheit** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="96e34-141">The **Windows Firewall with Advanced Security** console appears.</span></span>

1. <span data-ttu-id="96e34-142">Klicken Sie im linken Bereich auf **Eingehende Regeln**.</span><span class="sxs-lookup"><span data-stu-id="96e34-142">In the left-hand pane, click **Inbound Rules**.</span></span>

1. <span data-ttu-id="96e34-143">Scrollen Sie im rechten Bereich nach unten, klicken Sie mit der rechten Maustaste auf **Datei- und Druckerfreigabe (Echoanforderung – ICMPv4 eingehend)**, und klicken Sie anschließend auf **Regel aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="96e34-143">In the right-hand pane, scroll down and right-click **File and Printer Sharing (Echo Request - ICMPv4-In)**, and then click **Enable Rule**.</span></span>

1. <span data-ttu-id="96e34-144">Wechseln Sie wieder zur Konsole „dataProcessingStage1“, geben Sie im Eingabeaufforderungsfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="96e34-144">Switch back to the dataProcessingStage1 console and in the command prompt window, type the following command and press Enter.</span></span>

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. <span data-ttu-id="96e34-145">„dataProcessingStage2“ gibt vier Antworten zurück und bestätigt so die Konnektivität zwischen den beiden virtuellen Computern.</span><span class="sxs-lookup"><span data-stu-id="96e34-145">dataProcessingStage2 responds with four replies, demonstrating connectivity between the two VMs.</span></span>

## <a name="summary"></a><span data-ttu-id="96e34-146">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="96e34-146">Summary</span></span>

<span data-ttu-id="96e34-147">Sie haben erfolgreich ein virtuelles Netzwerk und zwei virtuelle Computer erstellt, die an das virtuelle Netzwerk angefügt sind. Darüber hinaus haben Sie eine Verbindung mit einem der virtuellen Computer hergestellt und die Netzwerkkonnektivität mit dem anderen virtuellen Computer im gleichen virtuellen Netzwerk überprüft.</span><span class="sxs-lookup"><span data-stu-id="96e34-147">You have successfully created a virtual network, created two VMs that are attached to that virtual network, connected to one of the VMs and shown network connectivity to the other VM within the same virtual network.</span></span> <span data-ttu-id="96e34-148">Sie können Azure Virtual Network verwenden, um Ressourcen innerhalb des Azure-Netzwerks zu verbinden.</span><span class="sxs-lookup"><span data-stu-id="96e34-148">You can use Azure Virtual Network to connect resources within the Azure network.</span></span> <span data-ttu-id="96e34-149">Diese Ressourcen müssen sich jedoch innerhalb der gleichen Ressourcengruppe und innerhalb des gleichen Abonnements befinden.</span><span class="sxs-lookup"><span data-stu-id="96e34-149">However, those resources need to be within the same resource group and subscription.</span></span> <span data-ttu-id="96e34-150">Als Nächstes beschäftigen wir uns mit VPN-Gateways. Mit einem VPN-Gateway können Sie virtuelle Netzwerk in unterschiedlichen Ressourcengruppen, Abonnements und sogar geografischen Regionen verbinden.</span><span class="sxs-lookup"><span data-stu-id="96e34-150">Next, we will look at VPN gateways, which enable you to connect virtual network in different resource groups, subscriptions, and even geographical regions.</span></span>
