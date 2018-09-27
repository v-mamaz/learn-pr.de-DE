<span data-ttu-id="5f6ec-101">Zur Erinnerung: Sie arbeiten bei der Woodgrove Bank und möchten Onlinebankingdienste anbieten.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-101">Recall that you work for Woodgrove Bank, and that you are about to launch online banking services.</span></span> <span data-ttu-id="5f6ec-102">Aufgrund des hohen Wettbewerbsdrucks in dieser Branche müssen Sie eine Dienstverfügbarkeit von 99,99 % gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-102">This sector is highly competitive, so you need to guarantee of a minimum of 99.99% service availability.</span></span> <span data-ttu-id="5f6ec-103">Sie haben ermittelt, dass Sie Azure Load Balancer mit einem Pool von drei virtuellen Computern benötigen, um dieses Ziel zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-103">You have determined that Azure Load Balancer with a pool of three virtual machines will meet this goal.</span></span>

<span data-ttu-id="5f6ec-104">In dieser Übung erstellen Sie einen Lastenausgleich und ein virtuelles Netzwerk über das Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-104">In this exercise, you will create a load balancer and a virtual network using the Azure portal.</span></span> <span data-ttu-id="5f6ec-105">Sie können zwischen diesen beiden Optionen wählen und diese mithilfe des Portals ganz einfach erstellen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-105">Since we only need one of these, the portal is an easy way to create it.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-public-load-balancer"></a><span data-ttu-id="5f6ec-106">Erstellen eines öffentlichen Lastenausgleichs</span><span class="sxs-lookup"><span data-stu-id="5f6ec-106">Create a public load balancer</span></span>

1. <span data-ttu-id="5f6ec-107">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-107">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="5f6ec-108">Klicken Sie in der Randleiste auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-108">In the sidebar, click **Create a resource**.</span></span>

1. <span data-ttu-id="5f6ec-109">Wählen Sie den Abschnitt **Netzwerk** aus, und klicken Sie dann auf **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-109">Select the **Networking** section, and then click **Load Balancer**.</span></span> <span data-ttu-id="5f6ec-110">Wenn diese Auswahl nicht angezeigt wird, können Sie das Suchfeld verwenden.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-110">If you don't see that choice, you can use the search box.</span></span>

    ![Screenshot vom Azure Marketplace mit dem ausgewählten Abschnitt „Netzwerk“ und dem hervorgehobenen Load Balancer](../media/3-azure-marketplace.png)

1. <span data-ttu-id="5f6ec-112">Geben Sie auf dem Blatt **Lastenausgleich erstellen** folgende Informationen ein, oder wählen Sie sie aus:</span><span class="sxs-lookup"><span data-stu-id="5f6ec-112">In the **Create load balancer** blade, enter or select the following information:</span></span>
    - <span data-ttu-id="5f6ec-113">**Name:** _woodgrove-LB_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-113">**Name:** _woodgrove-LB_</span></span>
    - <span data-ttu-id="5f6ec-114">**Typ:** _Öffentlich_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-114">**Type:** _Public_</span></span>
    - <span data-ttu-id="5f6ec-115">**SKU:** _Basic_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-115">**SKU:** _Basic_</span></span>
    - <span data-ttu-id="5f6ec-116">**Öffentliche IP-Adresse:** Klicken Sie auf **Neu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-116">**Public IP address:** Select **Create new**.</span></span> <span data-ttu-id="5f6ec-117">Geben Sie im Textfeld _woodgrove-LB-ip_ ein.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-117">In the text box, type _woodgrove-LB-ip_.</span></span> <span data-ttu-id="5f6ec-118">Übernehmen Sie für „Zuweisung“ den Wert _Dynamisch_.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-118">Leave the Assignment as _Dynamic_.</span></span>
    - <span data-ttu-id="5f6ec-119">**Abonnement:** Das _Concierge-Abonnement_ sollte bereits ausgewählt sein.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-119">**Subscription:** It should already have _Concierge Subscription_ selected.</span></span>
    - <span data-ttu-id="5f6ec-120">**Ressourcengruppe:** Wählen Sie zuerst **Vorhandene verwenden** und anschließend _<rgn>[Name der Sandboxressourcengruppe]</rgn>_ aus.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-120">**Resource group:** Select **Use existing** and choose _<rgn>[sandbox resource group name]</rgn>_.</span></span>
    - <span data-ttu-id="5f6ec-121">**Standort:** Wählen Sie aus der folgenden Liste eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-121">**Location:** Select a region near you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    ![Screenshot vom Bildschirm der Erstellung eines neuen Lastenausgleichs](../media/3-create-load-balancer.png)

1. <span data-ttu-id="5f6ec-123">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-123">Click **Create**.</span></span>

<span data-ttu-id="5f6ec-124">Während die Lastenausgleichsressource erstellt und bereitgestellt wird, können wir das Azure Virtual Network erstellen, das wir für das Back-End-Subnetz verwenden.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-124">While the load balancer resource is being created and deployed, let's create the Azure Virtual Network we'll use for the backend subnet.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="5f6ec-125">Erstellen eines virtuellen Netzwerks</span><span class="sxs-lookup"><span data-stu-id="5f6ec-125">Create a virtual network</span></span>

1. <span data-ttu-id="5f6ec-126">Klicken Sie im Menü links auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-126">In the left menu, click **Create a resource**.</span></span> <span data-ttu-id="5f6ec-127">Klicken Sie auf dem Blatt **Neu** zuerst auf **Netzwerk** und anschließend auf **Virtuelles Netzwerk**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-127">In the **New** blade, click **Networking**, and then click **Virtual network**.</span></span>

    ![Screenshot vom Azure Marketplace mit dem ausgewählten Abschnitt „Netzwerk“ und dem hervorgehobenen Load Balancer](../media/3-azure-marketplace-2.png)

1. <span data-ttu-id="5f6ec-129">Geben Sie auf dem Blatt **Virtuelles Netzwerk erstellen** folgende Informationen ein, oder wählen Sie sie aus:</span><span class="sxs-lookup"><span data-stu-id="5f6ec-129">In the **Create virtual network** blade, enter or select the following information:</span></span>
    - <span data-ttu-id="5f6ec-130">**Name:** _woodgrove-VNET_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-130">**Name:** _woodgrove-VNET_</span></span>
    - <span data-ttu-id="5f6ec-131">**Adressraum:** _172.20.0.0/16_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-131">**Address space:** _172.20.0.0/16_</span></span>
    - <span data-ttu-id="5f6ec-132">**Abonnement:** Das _Concierge-Abonnement_ sollte bereits ausgewählt sein.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-132">**Subscription:** It should already have _Concierge Subscription_ selected.</span></span>
    - <span data-ttu-id="5f6ec-133">**Ressourcengruppe:** Wählen Sie aus der Liste die vorhandene Ressourcengruppe _<rgn>[Ressourcengruppenname]</rgn>_ aus.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-133">**Resource group:** Select the existing _<rgn>[Resource Group Name]</rgn>_ resource group from the list.</span></span>
    - <span data-ttu-id="5f6ec-134">**Subnetzname:** _backendSubnet_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-134">**Subnet name:** _backendSubnet_</span></span>
    - <span data-ttu-id="5f6ec-135">**Subnetzadressbereich:** _172.20.0.0/24_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-135">**Subnet address range:** _172.20.0.0/24_</span></span>
    - <span data-ttu-id="5f6ec-136">**DDoS-Schutz:** _Basic_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-136">**DDoS protection:** _Basic_</span></span>
    - <span data-ttu-id="5f6ec-137">**Dienstendpunkte:** _Deaktiviert_</span><span class="sxs-lookup"><span data-stu-id="5f6ec-137">**Service endpoints:** _Disabled_</span></span>

    ![Screenshot vom Bildschirm der Erstellung eines neuen Lastenausgleichs](../media/3-create-vnet.png)

1. <span data-ttu-id="5f6ec-139">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-139">Click **Create**.</span></span>

<span data-ttu-id="5f6ec-140">Während das virtuelle Netzwerk bereitgestellt wird, erstellen wir eine Netzwerksicherheitsgruppe.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-140">While the virtual network is being deployed, let's create one more thing: a network security group.</span></span>

## <a name="create-and-configure-a-network-security-group"></a><span data-ttu-id="5f6ec-141">Erstellen und Konfigurieren einer Netzwerksicherheitsgruppe</span><span class="sxs-lookup"><span data-stu-id="5f6ec-141">Create and configure a network security group</span></span>

1. <span data-ttu-id="5f6ec-142">Klicken Sie auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-142">Click **Create a resource**</span></span>

1. <span data-ttu-id="5f6ec-143">Wählen Sie die Gruppe **Netzwerk** aus, und klicken Sie auf das Element **Netzwerksicherheitsgruppe**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-143">Select the **Networking** group, and Click on the **Network security group** item.</span></span>

    ![Screenshot vom Azure Marketplace mit dem ausgewählten Abschnitt „Netzwerk“ und der hervorgehobenen Netzwerksicherheitsgruppe](../media/3-azure-marketplace-3.png)


1. <span data-ttu-id="5f6ec-145">Geben Sie ihr den Namen **woodgrove-NSG**, und platzieren Sie sie in der Ressourcengruppe der Azure-Sandbox.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-145">Give it the name **woodgrove-NSG** and put it into the Azure sandbox resource group.</span></span>

1. <span data-ttu-id="5f6ec-146">Stellen Sie sicher, dass sie sich am gleichen Standort wie der Azure Load Balancer befindet.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-146">Make sure it's in the same location as the Azure Load Balancer.</span></span>

    ![Screenshot vom Bildschirm der Erstellung einer Netzwerksicherheitsgruppe](../media/3-create-nsg.png)

1. <span data-ttu-id="5f6ec-148">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-148">Click **Create**.</span></span>

<span data-ttu-id="5f6ec-149">Warten Sie, bis der Lastenausgleich, das virtuelle Netzwerk und die Netzwerksicherheitsgruppe (NSG) bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-149">Wait until the load balancer, virtual network, and NSG are deployed.</span></span> <span data-ttu-id="5f6ec-150">Dann können Sie die Netzwerksicherheitsgruppe konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-150">Then we can configure the network security.</span></span>

## <a name="configure-the-network-security-group"></a><span data-ttu-id="5f6ec-151">Konfigurieren der Netzwerksicherheitsgruppe</span><span class="sxs-lookup"><span data-stu-id="5f6ec-151">Configure the network security group</span></span>

1. <span data-ttu-id="5f6ec-152">Wählen Sie die neue Netzwerksicherheitsgruppe entweder über die Bereitstellungsbenachrichtigung oder über die Suchleiste am oberen Rand des Azure-Portals aus.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-152">Select your new network security group - either from the deployment notification, or through the search bar at the top of the Azure portal.</span></span>

    ![Screenshot von der erfolgreichen Bereitstellung im Panel „Benachrichtigung“](../media/3-deployment-success.png)

1. <span data-ttu-id="5f6ec-154">Wählen Sie den Abschnitt **Einstellungen** > **Eingangssicherheitsregeln** aus.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-154">Select the **Settings** > **Inbound security rules** section.</span></span> <span data-ttu-id="5f6ec-155">Beachten Sie, dass es drei vordefinierte Regeln gibt, die immer angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-155">Notice that we have three pre-defined rules that are always applied.</span></span> <span data-ttu-id="5f6ec-156">Zu diesen Regeln gehören:</span><span class="sxs-lookup"><span data-stu-id="5f6ec-156">These rules are:</span></span>
    - <span data-ttu-id="5f6ec-157">**AllowVnetInbound:** Zulassen des gesamten internen Datenverkehrs im virtuellen Netzwerk</span><span class="sxs-lookup"><span data-stu-id="5f6ec-157">**AllowVnetInbound** - Allow all internal traffic flowing on the virtual network.</span></span> <span data-ttu-id="5f6ec-158">Diese Regel erlaubt es den VMs, die sich in einem Netzwerk befinden, miteinander zu kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-158">This rule allows VMs that share the network to talk to each other.</span></span>
    - <span data-ttu-id="5f6ec-159">**AllowAzureLoadBalancerInBound:** Erlaubt es dem Lastenausgleich, Dienste im Netzwerk zu „pingen“, um herauszufinden, ob diese aktiv sind.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-159">**AllowAzureLoadBalancerInBound** - Allow the load balancer to "ping" services on the network to see whether they are alive.</span></span>
    - <span data-ttu-id="5f6ec-160">**DenyAllInbound:** Verweigern des gesamten anderen Datenverkehrs.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-160">**DenyAllInbound** - Deny all other traffic.</span></span>

    <span data-ttu-id="5f6ec-161">Die **DenyAllInbound**-Regel ist besonders wichtig, da dadurch sichergestellt wird, dass sämtlicher eingehender Datenverkehr, der keine Regel mit höherer Priorität hat, blockiert wird.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-161">The **DenyAllInbound** rule is particularly important - it ensures that all inbound traffic that doesn't have a higher priority rule is blocked.</span></span> <span data-ttu-id="5f6ec-162">Daher muss eine neue Regel hinzugefügt werden, um HTTP-Datenverkehr (Port 80) für die Webserver zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-162">That's why we will need to add a new rule to allow HTTP (80) traffic for our web servers.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f6ec-163">Die Priorität in NSG-Regeln liegt zwischen 0 und 65500, und Regeln werden der Reihe nach ausgewertet.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-163">Priority in NSG rules goes from 0 - 65500 and rules are evaluated in order.</span></span> <span data-ttu-id="5f6ec-164">Die erste übereinstimmende Regel wird Entscheidungsträger.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-164">The first matching rule becomes the decision maker.</span></span> <span data-ttu-id="5f6ec-165">Sie sollten für Ihre Regeln immer recht niedrige Prioritäten festlegen (ca. 1000), sodass diese Vorrang vor den vordefinierten Regeln haben.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-165">You will always want to place your rules fairly low - starting around 1000 so they take precedence over the pre-defined ones.</span></span>

1. <span data-ttu-id="5f6ec-166">Klicken Sie auf **Hinzufügen**, um eine neue Regel hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-166">Click **Add** to add a new rule.</span></span>

    ![Screenshot von den eingehenden Netzwerksicherheitsregeln mit hervorgehobener Schaltfläche „Hinzufügen“](../media/3-inbound-security-rules.png)

1. <span data-ttu-id="5f6ec-168">Klicken Sie ganz oben auf die Schaltfläche **Basic**, um zur Ansicht „Basic“ zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-168">Click the **Basic** button at the top to switch the the "basic" view.</span></span>

1. <span data-ttu-id="5f6ec-169">Geben Sie die Details für die neue Regel an.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-169">Fill in the details for the new rule.</span></span>
    - <span data-ttu-id="5f6ec-170">Wählen Sie für den **Dienst** _HTTP_ aus.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-170">Select _HTTP_ for the **Service**.</span></span>
    - <span data-ttu-id="5f6ec-171">Legen Sie die **Priorität** auf _1000_ fest.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-171">Set the **Priority** to _1000_.</span></span>
    - <span data-ttu-id="5f6ec-172">Geben Sie der Regel einen Namen (oder übernehmen Sie den Standardnamen).</span><span class="sxs-lookup"><span data-stu-id="5f6ec-172">Give the rule a name (or leave the default).</span></span>

    ![Screenshot von dem mit HTTP-Details ausgefüllten Dialogfeld „Eingangssicherheitsregel hinzufügen“](../media/3-add-inbound-rule.png)

1. <span data-ttu-id="5f6ec-174">Klicken Sie auf **Hinzufügen**, um die Regel hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-174">Click **Add** to add the rule.</span></span>

    ![Screenshot von der neu hinzugefügten HTTP-Regel in der Liste von NSG-Regeln](../media/3-new-added-rule.png)

## <a name="apply-the-network-security-group-to-the-vnet"></a><span data-ttu-id="5f6ec-176">Anwenden der Netzwerksicherheitsgruppe auf das VNet</span><span class="sxs-lookup"><span data-stu-id="5f6ec-176">Apply the network security group to the VNet</span></span>

<span data-ttu-id="5f6ec-177">Als Nächstes wenden Sie diese Netzwerksicherheitsgruppe auf das virtuelle Netzwerk an.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-177">Next, let's apply this NSG to the virtual network.</span></span>

1. <span data-ttu-id="5f6ec-178">Suchen Sie Ihr virtuelles Netzwerk, indem Sie das Suchfeld oben verwenden.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-178">Find your virtual network - you can use the search box at the top.</span></span> <span data-ttu-id="5f6ec-179">Der Name lautet **woodgrove-VNET**.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-179">It's named **woodgrove-VNET**.</span></span>

1. <span data-ttu-id="5f6ec-180">Wählen Sie **Einstellungen** > **Subnetze** aus, um die definierten Subnetze zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-180">Select **Settings** > **Subnets** to get to your defined subnets.</span></span>

1. <span data-ttu-id="5f6ec-181">Klicken Sie auf den Eintrag **backendSubnet**, um die Eigenschaften zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-181">Click the **backendSubnet** entry to open the properties.</span></span>

    ![Screenshot von den backendSubnet-Einträgen im Bereich „Subnetze“ der Subnetze](../media/3-subnets.png)

1. <span data-ttu-id="5f6ec-183">Klicken Sie in der **Netzwerksicherheitsgruppe** auf den Eintrag „Keine“.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-183">Click the "None" entry on the **Network security group**</span></span>

    ![Screenshot von der leeren Netzwerksicherheitsgruppe im backendSubnet](../media/3-add-network-security-group.png)

1. <span data-ttu-id="5f6ec-185">Wählen Sie die **woodgrove-NSG** aus, um sie diesem VNet hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-185">Select the **woodgrove-NSG** to add it to this VNET.</span></span>

1. <span data-ttu-id="5f6ec-186">Klicken Sie auf **Speichern**, um die Änderungen zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-186">Click **Save** to apply the change.</span></span>

<span data-ttu-id="5f6ec-187">Da das Netzwerk jetzt eingerichtet ist, können Sie virtuelle Computer im Netzwerk erstellen.</span><span class="sxs-lookup"><span data-stu-id="5f6ec-187">Now that our network is ready, let's create some virtual machines to sit on this network!</span></span>