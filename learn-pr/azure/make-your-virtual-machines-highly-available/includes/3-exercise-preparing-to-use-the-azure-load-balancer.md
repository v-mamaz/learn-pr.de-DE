<span data-ttu-id="ff5c5-101">In dieser Übung erstellen Sie einen Lastenausgleich, ein virtuelles Netzwerk und mehrere virtuelle Computer über das Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-101">In this exercise, you will create a load balancer, a virtual network, and multiple virtual machines using the Azure portal.</span></span>

<span data-ttu-id="ff5c5-102">Angenommen, Sie arbeiten bei der Woodgrove Bank – einem Start-Up-Unternehmen, das Onlinebankingdienste anbieten möchte.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-102">Suppose you work for Woodgrove Bank, a startup that is about to launch online banking services.</span></span> <span data-ttu-id="ff5c5-103">Aufgrund des hohen Wettbewerbsdrucks in dieser Branche müssen Sie eine Verfügbarkeit von 99,99 Prozent gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-103">This sector is highly competitive, so you need to guarantee of a minimum of 99.99% service availability.</span></span> <span data-ttu-id="ff5c5-104">Sie haben ermittelt, dass Sie eine Azure Load Balancer-Instanz mit einem Pool von drei virtuellen Computern benötigen, um dieses Ziel zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-104">You have determined that an Azure Load Balancer with a pool of three virtual machines will meet this goal.</span></span>

## <a name="create-a-public-load-balancer"></a><span data-ttu-id="ff5c5-105">Erstellen eines öffentlichen Lastenausgleichs</span><span class="sxs-lookup"><span data-stu-id="ff5c5-105">Create a public load balancer</span></span>

1. <span data-ttu-id="ff5c5-106">Navigieren Sie in einem Browser zum [Azure-Portal](https://portal.azure.com/?azure-portal=true), und melden Sie sich bei Ihrem Konto an.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-106">In a browser, navigate to the [Azure portal](https://portal.azure.com/?azure-portal=true) and sign in to your account.</span></span>

1. <span data-ttu-id="ff5c5-107">Klicken Sie auf der Seitenleiste auf **Ressource erstellen**, klicken Sie auf dem Blatt **Neu** auf **Netzwerk**, und klicken Sie anschließend auf **Lastenausgleich**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-107">In the sidebar, click **Create a resource**, then in the **New** blade, click **Networking**, and then click **Load Balancer**.</span></span>

1. <span data-ttu-id="ff5c5-108">Geben Sie auf dem Blatt „Lastenausgleich erstellen“ folgende Informationen ein, bzw. wählen Sie sie aus:</span><span class="sxs-lookup"><span data-stu-id="ff5c5-108">In the Create load balancer blade, enter or select the following information:</span></span>
    - <span data-ttu-id="ff5c5-109">Name: **woodgrove-LB**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-109">Name: **woodgrove-LB**</span></span>
    - <span data-ttu-id="ff5c5-110">Typ: **Öffentlich**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-110">Type: **Public**</span></span>
    - <span data-ttu-id="ff5c5-111">SKU: **Basic**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-111">SKU: **Basic**</span></span>
    - <span data-ttu-id="ff5c5-112">Öffentliche IP-Adresse: Klicken Sie auf **Neu erstellen**, geben Sie **woodgrove-LB-ip** in das Textfeld ein, und behalten Sie die Zuweisung **Dynamisch** bei.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-112">Public IP address: Select **Create new** and in the text box, type **woodgrove-LB-ip** in the text box, and leave the Assignment as **Dynamic**</span></span>
    - <span data-ttu-id="ff5c5-113">Ressourcengruppe: Klicken Sie auf **Neu erstellen**, und geben Sie **woodgrove-RG** in das Feld ein.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-113">Resource group: Select **Create new**, and in the box, type **woodgrove-RG**</span></span>
    - <span data-ttu-id="ff5c5-114">Standort: Wählen Sie eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-114">Location: Select a region near you</span></span>

1. <span data-ttu-id="ff5c5-115">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-115">Click **Create**.</span></span>

1. <span data-ttu-id="ff5c5-116">Warten Sie, bis der Lastenausgleich bereitgestellt wurde, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-116">Wait until the load balancer has deployed before continuing with the exercise.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="ff5c5-117">Erstellen eines virtuellen Netzwerks</span><span class="sxs-lookup"><span data-stu-id="ff5c5-117">Create a Virtual Network</span></span>

1. <span data-ttu-id="ff5c5-118">Klicken Sie im linken Menü auf **Ressource erstellen**, klicken Sie auf dem Blatt **Neu** auf **Netzwerk**, und klicken Sie anschließend auf **Virtuelles Netzwerk**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-118">In the left menu, click **Create a resource**, then in the **New** blade, click **Networking**, and then click **Virtual network**.</span></span>

1. <span data-ttu-id="ff5c5-119">Geben Sie auf dem Blatt **Virtuelles Netzwerk erstellen** folgende Informationen ein, bzw. wählen Sie sie aus:</span><span class="sxs-lookup"><span data-stu-id="ff5c5-119">In the **Create virtual network** blade, enter or select the following information:</span></span>
    - <span data-ttu-id="ff5c5-120">Name: **woodgrove-VNET**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-120">Name: **woodgrove-VNET**</span></span>
    - <span data-ttu-id="ff5c5-121">Adressraum: **172.20.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-121">Address space: **172.20.0.0/16**</span></span>
    - <span data-ttu-id="ff5c5-122">Ressourcengruppe: Klicken Sie auf **Vorhandene verwenden**, und wählen Sie **woodgrove-RG** aus.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-122">Resource group: Select **Use existing**, and select **woodgrove-RG**.</span></span>
    - <span data-ttu-id="ff5c5-123">Subnetz: **backendSubnet**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-123">Subnet: **backendSubnet**</span></span>
    - <span data-ttu-id="ff5c5-124">Adressraum: **172.20.0.0/24**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-124">Address space: **172.20.0.0/24**</span></span>
    - <span data-ttu-id="ff5c5-125">DDoS-Schutz: **Basic**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-125">DDoS protection: **Basic**</span></span>
    - <span data-ttu-id="ff5c5-126">Dienstendpunkte: **Deaktiviert**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-126">Service endpoints: **Disabled**</span></span>

1. <span data-ttu-id="ff5c5-127">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-127">Click **Create**.</span></span>

1. <span data-ttu-id="ff5c5-128">Warten Sie, bis das virtuelle Netzwerk bereitgestellt wurde, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-128">Wait until the virtual network has deployed before continuing with the exercise.</span></span>

## <a name="create-a-vm-template"></a><span data-ttu-id="ff5c5-129">Erstellen einer VM-Vorlage</span><span class="sxs-lookup"><span data-stu-id="ff5c5-129">Create a VM template</span></span>

<span data-ttu-id="ff5c5-130">Definieren Sie zunächst die grundlegenden Informationen für den virtuellen Computer:</span><span class="sxs-lookup"><span data-stu-id="ff5c5-130">Start by defining the basic VM information:</span></span>

1. <span data-ttu-id="ff5c5-131">Klicken Sie im linken Menü des Azure-Portals auf **Virtuelle Computer** und anschließend auf **Virtuellen Computer erstellen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-131">In the Azure portal, in the left menu, click **Virtual machines**, and then click **Create virtual machine**.</span></span>

1. <span data-ttu-id="ff5c5-132">Klicken Sie auf dem Blatt „Compute“ im Abschnitt **Empfohlen** auf **Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-132">On the Compute blade, in the **Recommended** section, click **Windows Server**.</span></span>

1. <span data-ttu-id="ff5c5-133">Klicken Sie auf dem Blatt **Windows Server** auf **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-133">In the **Windows Server** blade, click **Windows Server 2016 Datacenter**.</span></span>

1. <span data-ttu-id="ff5c5-134">Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-134">In the **Windows Server 2016 Datacenter** blade, click **Create**.</span></span>

1. <span data-ttu-id="ff5c5-135">Geben Sie auf dem Blatt **Grundlagen** im Feld **Name** den Namen **woodgrove-SVR01** ein.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-135">In the **Basics** blade, in the **Name** box, type **woodgrove-SVR01**.</span></span>

1. <span data-ttu-id="ff5c5-136">Geben Sie in den Feldern **Benutzername** und **Kennwort** einen sicheren Namen und ein sicheres Kennwort für ein Administratorkonto auf diesem Server ein.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-136">In the **Username** and **Password boxes**, type a secure name and password for an administrator account on this server.</span></span>

1. <span data-ttu-id="ff5c5-137">Wählen Sie im Feld **Abonnement** Ihr Azure-Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-137">In the **Subscription** box, select your Azure subscription.</span></span>

1. <span data-ttu-id="ff5c5-138">Klicken Sie unter **Ressourcengruppe** auf **Vorhandene verwenden**, und wählen Sie in der Liste die Option **woodgrove-RG** aus.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-138">Under **Resource group**, select **Use existing**, and in the list, select **woodgrove-RG**.</span></span>

1. <span data-ttu-id="ff5c5-139">Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-139">In the **Location** drop-down list, select a region near you.SAME</span></span>

1. <span data-ttu-id="ff5c5-140">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-140">Click **OK**.</span></span>

<span data-ttu-id="ff5c5-141">Wählen Sie eine Größe für den virtuellen Computer aus, und konfigurieren Sie die Einstellungen:</span><span class="sxs-lookup"><span data-stu-id="ff5c5-141">Choose a size for the VM and configure settings:</span></span>

1. <span data-ttu-id="ff5c5-142">Wählen Sie auf dem Blatt **Größe auswählen** eine SKU vom Typ **Standard** aus (etwa **D2s_v3**), und klicken Sie auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-142">On the **Choose a size** blade, select a **Standard** SKU, such as **D2s_v3**, and then click **Select**.</span></span>

1. <span data-ttu-id="ff5c5-143">Klicken Sie auf dem Blatt **Einstellungen** auf **Verfügbarkeitsgruppe**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-143">On the **Settings** blade, click **Availability set**.</span></span>

1. <span data-ttu-id="ff5c5-144">Klicken Sie auf dem Blatt **Verfügbarkeitsgruppe ändern** auf **Neu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-144">On the **Change availability set** blade, click **Create new**.</span></span>

1. <span data-ttu-id="ff5c5-145">Geben Sie auf dem Blatt **Neu erstellen** im Feld **Name** den Namen **woodgrove-AS** ein, und klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-145">On the **Create new** blade, in the **Name** box, type **woodgrove-AS**, and then click **OK**.</span></span>

1. <span data-ttu-id="ff5c5-146">Klicken Sie auf dem Blatt **Einstellungen** unter **Netzwerksicherheitsgruppe** auf **Erweitert** und anschließend auf **(neu) woodgrove-SVR01-nsg**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-146">On the **Settings** blade, under **Network Security Group**, click **Advanced**, and then click **(new) woodgrove-SVR01-nsg**.</span></span>

1. <span data-ttu-id="ff5c5-147">Ändern Sie auf dem Blatt **Netzwerksicherheitsgruppe erstellen** den Namen im Feld **Name** in **woodgrove-NSG**, und klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-147">On the **Create network Security group** blade, in the **Name** box, change the name to **woodgrove-NSG**, and then click **OK**.</span></span>

1. <span data-ttu-id="ff5c5-148">Klicken Sie auf dem Blatt **Einstellungen** auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-148">On the **Settings** blade, click **OK**.</span></span>

<span data-ttu-id="ff5c5-149">Speichern Sie die Einstellungen in einer Vorlage, um komfortabel mehrere virtuelle Computer bereitstellen zu können.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-149">Save the settings to a template, so that you easily deploy multiple VMs.</span></span>

1. <span data-ttu-id="ff5c5-150">Klicken Sie auf dem Blatt **Erstellen** auf **Vorlage und Parameter herunterladen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-150">On the **Create** blade, click **Download template and parameters**.</span></span>

1. <span data-ttu-id="ff5c5-151">Klicken Sie auf dem Blatt **Vorlage** auf **Zu Bibliothek hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-151">On the **Template** blade, click **Add to library**.</span></span>

1. <span data-ttu-id="ff5c5-152">Geben Sie auf dem Blatt **Vorlage speichern** in den Feldern **Name** und **Beschreibung** jeweils **woodgrove-server-template** ein, und klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-152">On the **Save template** blade, in the **Name** and **Description** boxes, type **woodgrove-server-template**, and then click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="ff5c5-153">Wenn Sie nach dieser Vorlage suchen möchten, klicken Sie im linken Menü auf **Alle Dienste**, geben Sie **Vorlage** in das Filterfeld ein, und klicken Sie auf **Vorlagen (VORSCHAU)**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-153">If you need to find this template, click **All services** in the left menu, type **template** in the filter box, and then click **Templates (PREVIEW)**.</span></span>

## <a name="use-the-template-to-provision-the-first-vm"></a><span data-ttu-id="ff5c5-154">Bereitstellen des ersten virtuellen Computers mit der Vorlage</span><span class="sxs-lookup"><span data-stu-id="ff5c5-154">Use the template to provision the first VM</span></span>

1. <span data-ttu-id="ff5c5-155">Klicken Sie auf dem Blatt **Vorlage** auf **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-155">On the **Template** blade, click **Deploy**.</span></span>

1. <span data-ttu-id="ff5c5-156">Klicken Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** unter **Ressourcengruppe** auf **Vorhandene verwenden**, und wählen Sie in der Liste die Option **woodgrove-RG** aus.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-156">On the **Custom deployment** blade, under **Resource Group**, select **Use existing**, and in the list, select **woodgrove-RG**.</span></span>

1. <span data-ttu-id="ff5c5-157">Geben Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** im Feld **Administratorkennwort** das gleiche Kennwort ein wie vorhin.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-157">On the **Custom deployment** blade, in the **Admin password** box, type the same password that you used previously.</span></span>

1. <span data-ttu-id="ff5c5-158">Aktivieren Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** das Kontrollkästchen **Ich stimme den oben genannten Geschäftsbedingungen zu**, und klicken Sie anschließend auf **Kaufen**. (Dabei fallen die normalen Azure-Computegebühren an. Diese orientieren sich am VM-Tarif.)</span><span class="sxs-lookup"><span data-stu-id="ff5c5-158">On the **Custom deployment** blade, select the **I agree to the terms and conditions** check box, and then click **Purchase** (the cost is the regular Azure compute charge, which depends on the VM pricing tier).</span></span>

1. <span data-ttu-id="ff5c5-159">Warten Sie, bis der virtuelle Computer bereitgestellt wurde, bevor Sie mit der Übung fortfahren. So können Sie sich vor der Bereitstellung weiterer virtueller Computer vergewissern, dass die Vorlage ordnungsgemäß konfiguriert ist und alle dazugehörigen Ressourcen erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-159">Wait until the VM has deployed before continuing with the exercise; this is so you can be sure the template is correctly configured before you use it to provision additional VMs, and all the associated resources have been created.</span></span>

## <a name="use-the-template-to-provision-two-additional-vms"></a><span data-ttu-id="ff5c5-160">Bereitstellen zwei weiterer virtueller Computer mit der Vorlage</span><span class="sxs-lookup"><span data-stu-id="ff5c5-160">Use the template to provision two additional VMs</span></span>

1. <span data-ttu-id="ff5c5-161">Klicken Sie im Azure-Portal auf dem Blatt **Vorlage** auf **Bereitstellen**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-161">In the Azure portal, on the **Template** blade, click **Deploy**.</span></span>

1. <span data-ttu-id="ff5c5-162">Klicken Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** unter **Ressourcengruppe** auf **Vorhandene verwenden**, und wählen Sie in der Liste die Option **woodgrove-RG** aus.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-162">On the **Custom deployment** blade, under **Resource Group**, select **Use existing**, and in the list, select **woodgrove-RG**.</span></span>

1. <span data-ttu-id="ff5c5-163">Ändern Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** den Namen im Feld **Name des virtuellen Computers** in **woodgrove-SVR02**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-163">On the **Custom deployment** blade, in the **Virtual Machine Name** box, change the name to **woodgrove-SVR02**.</span></span>

1. <span data-ttu-id="ff5c5-164">Ändern Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** den Namen im Feld **Network Interface Name** (Name der Netzwerkschnittstelle) in **woodgrovesvr02222**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-164">On the **Custom deployment** blade, in the **Network Interface Name** box, change the name to **woodgrovesvr02222**.</span></span>

1. <span data-ttu-id="ff5c5-165">Geben Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** im Feld **Administratorkennwort** das gleiche Kennwort ein wie vorhin.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-165">On the **Custom deployment** blade, in the **Admin password** box, type the same password that you used previously.</span></span>

1. <span data-ttu-id="ff5c5-166">Ändern Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** den Namen im Feld **Öffentliche IP-Adresse** in **woodgrove-SVR02-ip**.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-166">On the **Custom deployment** blade, in the **Public Ip Address Name** box, change the name to **woodgrove-SVR02-ip**.</span></span>

1. <span data-ttu-id="ff5c5-167">Aktivieren Sie auf dem Blatt **Benutzerdefinierte Bereitstellung** das Kontrollkästchen **Ich stimme den oben genannten Geschäftsbedingungen zu**, und klicken Sie anschließend auf **Kaufen**. (Dabei fallen die normalen Azure-Computegebühren an. Diese orientieren sich am VM-Tarif.)</span><span class="sxs-lookup"><span data-stu-id="ff5c5-167">On the **Custom deployment** blade, select the **I agree to the terms and conditions** check box, and then click **Purchase** (the cost is the regular Azure compute charge, which depends on the VM pricing tier).</span></span>

1. <span data-ttu-id="ff5c5-168">Wiederholen Sie die Schritte 1 bis 7 mit den folgenden Informationen:</span><span class="sxs-lookup"><span data-stu-id="ff5c5-168">Repeat steps 1 - 7, using the following information:</span></span>
    - <span data-ttu-id="ff5c5-169">Name des virtuellen Computers: **woodgrove-SVR03**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-169">Virtual Machine Name: **woodgrove-SVR03**</span></span>
    - <span data-ttu-id="ff5c5-170">Name der Netzwerkschnittstelle: **woodgrovesvr03333**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-170">Network Interface Name: **woodgrovesvr03333**</span></span>
    - <span data-ttu-id="ff5c5-171">Name der öffentliche IP-Adresse: **woodgrove-SVRr03-ip**</span><span class="sxs-lookup"><span data-stu-id="ff5c5-171">Public Ip Address Name: **woodgrove-SVRr03-ip**</span></span>

1. <span data-ttu-id="ff5c5-172">Warten Sie, bis die virtuellen Computer bereitgestellt wurden, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-172">Wait until the VMs have deployed before continuing with the exercise.</span></span>

<span data-ttu-id="ff5c5-173">Sie verfügen nun über einen konfigurationsbereiten öffentlichen Lastenausgleich sowie über drei virtuelle Computer, die Sie mit diesem Lastenausgleich verwenden können.</span><span class="sxs-lookup"><span data-stu-id="ff5c5-173">You now have a public load balancer ready to configure, and three VMs ready to use with this load balancer.</span></span>