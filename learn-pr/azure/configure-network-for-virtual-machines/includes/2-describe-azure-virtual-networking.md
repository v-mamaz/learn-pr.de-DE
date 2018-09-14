<span data-ttu-id="d2900-101">Sie verfügen über ein lokales Rechenzentrum, das erhalten bleiben soll, und möchten Datenverkehrsspitzen an in Azure gehostete virtuelle Computer (Virtual Machines, VMs) auslagern.</span><span class="sxs-lookup"><span data-stu-id="d2900-101">You have an on-premises datacenter that you plan to keep, but you want to use Azure to offload peak traffic using virtual machines (VMs) hosted in Azure.</span></span> <span data-ttu-id="d2900-102">Sie möchten wissen, ob Sie Ihr bisheriges IP-Adressierungsschema und Ihre Netzwerkgeräte behalten und gleichzeitig die Sicherheit sämtlicher Datenübertragungen sicherstellen können.</span><span class="sxs-lookup"><span data-stu-id="d2900-102">You need to know if you can keep your existing IP addressing scheme and network appliances, while ensuring that any data transfer is secure.</span></span>

## <a name="what-is-azure-virtual-networking"></a><span data-ttu-id="d2900-103">Was sind virtuelle Azure-Netzwerke?</span><span class="sxs-lookup"><span data-stu-id="d2900-103">What is Azure virtual networking?</span></span>

<span data-ttu-id="d2900-104">Mit **virtuellen Azure-Netzwerken** können Azure-Ressourcen wie etwa virtuelle Computer, Web-Apps und Datenbanken untereinander, mit Benutzern im Internet sowie mit lokalen Clientcomputern kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-104">**Azure virtual networks** enable Azure resources, such as virtual machines, web apps, and databases, to communicate with: each other, users on the internet, and on-premises client computers.</span></span> <span data-ttu-id="d2900-105">Ein Azure-Netzwerk können Sie sich als eine Gruppe von Ressourcen vorstellen, die andere Azure-Ressourcen miteinander verbindet.</span><span class="sxs-lookup"><span data-stu-id="d2900-105">You can think of an Azure network as a set of resources that links other Azure resources.</span></span>

<span data-ttu-id="d2900-106">Virtuelle Azure-Netzwerke bieten wichtige Netzwerkfunktionen:</span><span class="sxs-lookup"><span data-stu-id="d2900-106">Azure virtual networks provide key networking capabilities:</span></span>

- <span data-ttu-id="d2900-107">Isolation und Segmentierung</span><span class="sxs-lookup"><span data-stu-id="d2900-107">Isolation and segmentation</span></span>
- <span data-ttu-id="d2900-108">Internetkommunikation</span><span class="sxs-lookup"><span data-stu-id="d2900-108">Internet communications</span></span>
- <span data-ttu-id="d2900-109">Kommunikation zwischen Azure-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d2900-109">Communicate between Azure resources</span></span>
- <span data-ttu-id="d2900-110">Kommunikation mit lokalen Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d2900-110">Communicate with on-premises resources</span></span>
- <span data-ttu-id="d2900-111">Weiterleitung von Netzwerkdatenverkehr</span><span class="sxs-lookup"><span data-stu-id="d2900-111">Route network traffic</span></span>
- <span data-ttu-id="d2900-112">Filterung von Netzwerkdatenverkehr</span><span class="sxs-lookup"><span data-stu-id="d2900-112">Filter network traffic</span></span>
- <span data-ttu-id="d2900-113">Verbindung virtueller Netzwerke</span><span class="sxs-lookup"><span data-stu-id="d2900-113">Connect virtual networks</span></span>

### <a name="isolation-and-segmentation"></a><span data-ttu-id="d2900-114">Isolation und Segmentierung</span><span class="sxs-lookup"><span data-stu-id="d2900-114">Isolation and segmentation</span></span>

<span data-ttu-id="d2900-115">Azure ermöglicht die Erstellung mehrerer isolierter virtueller Netzwerke.</span><span class="sxs-lookup"><span data-stu-id="d2900-115">Azure allows you to create multiple isolated virtual networks.</span></span> <span data-ttu-id="d2900-116">Wenn Sie ein virtuelles Netzwerk einrichten, definieren Sie einen privaten IP-Adressraum (Internetprotokoll) mit öffentlichen oder privaten IP-Adressbereichen.</span><span class="sxs-lookup"><span data-stu-id="d2900-116">When you set up a virtual network, you define a private Internet Protocol (IP) address space, using either public or private IP address ranges.</span></span> <span data-ttu-id="d2900-117">Diesen IP-Adressraum können Sie dann in Subnetze unterteilen und den einzelnen benannten Subnetzen jeweils einen Teil des definierten Adressraums zuordnen.</span><span class="sxs-lookup"><span data-stu-id="d2900-117">You can then segment that IP address space into subnets, and allocate part of the defined address space to each named subnet.</span></span>

<span data-ttu-id="d2900-118">Für die Namensauflösung können Sie den in Azure integrierten Namensauflösungsdienst oder das virtuelle Netzwerk für die Verwendung eines internen oder externen DNS-Servers (Domain Name System) konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-118">For name resolution, you can use the name resolution service that's built in to Azure, or you can configure the virtual network to use either an internal or an external Domain Name System (DNS) server.</span></span>

### <a name="internet-communications"></a><span data-ttu-id="d2900-119">Internetkommunikation</span><span class="sxs-lookup"><span data-stu-id="d2900-119">Internet communications</span></span>

<span data-ttu-id="d2900-120">Ein virtueller Computer in Azure kann standardmäßig eine Internetverbindung herstellen.</span><span class="sxs-lookup"><span data-stu-id="d2900-120">A VM in Azure can connect to the internet by default.</span></span> <span data-ttu-id="d2900-121">Sie müssen jedoch eine Verbindung mit diesem virtuellen Computer herstellen und ihn steuern. Hierzu können Sie entweder die Azure CLI, das Remotedesktopprotokoll (RDP) oder Secure Shell (SSH) verwenden.</span><span class="sxs-lookup"><span data-stu-id="d2900-121">However, you need to connect to and control that VM, with either the Azure CLI, Remote Desktop Protocol (RDP), or Secure Shell (SSH).</span></span> <span data-ttu-id="d2900-122">Sie können eingehende Kommunikation ermöglichen, indem Sie eine öffentliche IP-Adresse oder einen öffentlichen Load Balancer definieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-122">You can enable incoming communications by defining a public IP address or a public load balancer.</span></span>

### <a name="communicate-between-azure-resources"></a><span data-ttu-id="d2900-123">Kommunikation zwischen Azure-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d2900-123">Communicate between Azure resources</span></span>

<span data-ttu-id="d2900-124">Es empfiehlt sich, eine sichere Kommunikation zwischen Azure-Ressourcen zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="d2900-124">You will want to enable Azure resources to communicate securely with each other.</span></span> <span data-ttu-id="d2900-125">Dazu haben Sie zwei Möglichkeiten:</span><span class="sxs-lookup"><span data-stu-id="d2900-125">You can do that in one of two ways:</span></span>

- <span data-ttu-id="d2900-126">**Virtuelle Netzwerke**</span><span class="sxs-lookup"><span data-stu-id="d2900-126">**Virtual networks**</span></span>
    
    <span data-ttu-id="d2900-127">Virtuelle Netzwerke können nicht nur eine Verbindung mit virtuellen Computern herstellen, sondern auch mit anderen Ressourcen. Hierzu zählen beispielsweise App Service-Umgebungen, Azure Kubernetes Service und Azure-VM-Skalierungsgruppen.</span><span class="sxs-lookup"><span data-stu-id="d2900-127">Virtual networks can connect not only VMs, but other Azure resources, such as the App Service Environment, Azure Kubernetes Service, and Azure virtual machine scale sets.</span></span>

- <span data-ttu-id="d2900-128">**Dienstendpunkte**</span><span class="sxs-lookup"><span data-stu-id="d2900-128">**Service endpoints**</span></span>
     
     <span data-ttu-id="d2900-129">Mithilfe von Dienstendpunkten können Sie eine Verbindung mit anderen Azure-Ressourcentypen (wie etwa Azure SQL-Datenbanken und Speicherkonten) herstellen.</span><span class="sxs-lookup"><span data-stu-id="d2900-129">You can use service endpoints to connect to other Azure resource types, such as Azure SQL databases and storage accounts.</span></span> <span data-ttu-id="d2900-130">Bei diesem Ansatz können Sie mehrere Azure-Ressourcen mit virtuellen Netzwerken verknüpfen und so die Sicherheit erhöhen und ein optimales Routing zwischen Ressourcen sicherstellen.</span><span class="sxs-lookup"><span data-stu-id="d2900-130">This approach enables you to link multiple Azure resources to virtual networks, thereby improving security and providing optimal routing between resources.</span></span>

### <a name="communicate-with-on-premises-resources"></a><span data-ttu-id="d2900-131">Kommunikation mit lokalen Ressourcen</span><span class="sxs-lookup"><span data-stu-id="d2900-131">Communicate with on-premises resources</span></span>

<span data-ttu-id="d2900-132">Virtuelle Azure-Netzwerke ermöglichen es Ihnen, Ressourcen in Ihrer lokalen Umgebung und in Ihrem Azure-Abonnement miteinander zu verknüpfen und so ein Netzwerk zu erstellen, das sowohl Ihre lokale Umgebung als auch Ihre Cloudumgebung abdeckt.</span><span class="sxs-lookup"><span data-stu-id="d2900-132">Azure virtual networks enable you to link resources together in your on-premises environment and within your Azure subscription, in effect creating a network that spans both your local and cloud environments.</span></span> <span data-ttu-id="d2900-133">Für diese Konnektivität stehen drei Mechanismen zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="d2900-133">There are three mechanisms for you to achieve this connectivity:</span></span>

- <span data-ttu-id="d2900-134">**Point-to-Site-VPNs**</span><span class="sxs-lookup"><span data-stu-id="d2900-134">**Point-to-site VPNs**</span></span>

   <span data-ttu-id="d2900-135">Dieser Ansatz gleicht einer VPN-Verbindung, die ein Computer außerhalb Ihrer Organisation mit Ihrem Unternehmensnetzwerk herstellt – allerdings in entgegengesetzter Richtung.</span><span class="sxs-lookup"><span data-stu-id="d2900-135">This approach is like a VPN connection that a computer outside your organization makes back into your corporate network, except that it's working in the opposite direction.</span></span> <span data-ttu-id="d2900-136">In diesem Fall initiiert der Clientcomputer eine verschlüsselte VPN-Verbindung mit Azure, um den Computer mit dem virtuellen Azure-Netzwerk zu verbinden.</span><span class="sxs-lookup"><span data-stu-id="d2900-136">In this case, the client computer initiates an encrypted VPN connection to Azure, connecting that computer to the Azure virtual network.</span></span>

- <span data-ttu-id="d2900-137">**Site-to-Site-VPNs** Ein Site-to-Site-VPN verknüpft Ihr lokales VPN-Gerät oder -Gateway mit dem Azure-VPN-Gateway in einem virtuellen Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="d2900-137">**Site-to-site VPNs** A site-to-site VPN links your on-premises VPN device or gateway to the Azure VPN gateway in a virtual network.</span></span> <span data-ttu-id="d2900-138">Dadurch entsteht bisweilen der Eindruck, die Geräte in Azure befänden sich tatsächlich im lokalen Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="d2900-138">In effect, the devices in Azure can appear as being on the local network.</span></span> <span data-ttu-id="d2900-139">Die Verbindung ist verschlüsselt und internetbasiert.</span><span class="sxs-lookup"><span data-stu-id="d2900-139">The connection is encrypted and works over the internet.</span></span>

- <span data-ttu-id="d2900-140">**Azure ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="d2900-140">**Azure ExpressRoute**</span></span>

    <span data-ttu-id="d2900-141">Für Umgebungen, in denen Sie eine höhere Bandbreite und ein noch höheres Maß an Sicherheit benötigen, ist Azure ExpressRoute die beste Lösung.</span><span class="sxs-lookup"><span data-stu-id="d2900-141">For environments where you need greater bandwidth and even higher levels of security, Azure ExpressRoute is the best approach.</span></span> <span data-ttu-id="d2900-142">Azure ExpressRoute bietet dedizierte private Konnektivität mit Azure ohne internetbasierte Datenübertragung.</span><span class="sxs-lookup"><span data-stu-id="d2900-142">Azure ExpressRoute provides dedicated private connectivity to Azure that does not travel over the internet.</span></span>

### <a name="route-network-traffic"></a><span data-ttu-id="d2900-143">Weiterleitung von Netzwerkdatenverkehr</span><span class="sxs-lookup"><span data-stu-id="d2900-143">Route network traffic</span></span>

<span data-ttu-id="d2900-144">Azure leitet standardmäßig Datenverkehr zwischen Subnetzen in beliebigen verbundenen virtuellen Netzwerken, lokalen Netzwerken und dem Internet weiter.</span><span class="sxs-lookup"><span data-stu-id="d2900-144">By default, Azure will route traffic between subnets on any connected virtual networks, on-premises networks, and the internet.</span></span> <span data-ttu-id="d2900-145">Sie können das Routing jedoch steuern und die Einstellungen mit folgen Methoden überschreiben:</span><span class="sxs-lookup"><span data-stu-id="d2900-145">However, you can control routing and override those settings as follows:</span></span>

- <span data-ttu-id="d2900-146">**Routingtabellen**</span><span class="sxs-lookup"><span data-stu-id="d2900-146">**Route tables**</span></span>

    <span data-ttu-id="d2900-147">Mit einer Routingtabelle können Sie Regeln für die Weiterleitung von Datenverkehr definieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-147">A route table allows you to define rules as to how traffic should be directed.</span></span> <span data-ttu-id="d2900-148">Sie können benutzerdefinierte Routingtabellen erstellen, die steuern, wie Pakete zwischen Subnetzen weitergeleitet werden.</span><span class="sxs-lookup"><span data-stu-id="d2900-148">You can create custom route tables that control how packets are routed between subnets.</span></span>

- <span data-ttu-id="d2900-149">**Border Gateway Protocol**</span><span class="sxs-lookup"><span data-stu-id="d2900-149">**Border Gateway Protocol**</span></span>

    <span data-ttu-id="d2900-150">Border Gateway Protocol (BGP) kann für Azure-VPN-Gateways oder ExpressRoute verwendet werden, um lokale BGP-Routen zu virtuellen Azure-Netzwerken zu verteilen.</span><span class="sxs-lookup"><span data-stu-id="d2900-150">Border Gateway Protocol (BGP) works with Azure VPN gateways or ExpressRoute to propagate on-premises BGP routes to Azure virtual networks.</span></span>

### <a name="filter-network-traffic"></a><span data-ttu-id="d2900-151">Filterung von Netzwerkdatenverkehr</span><span class="sxs-lookup"><span data-stu-id="d2900-151">Filter network traffic</span></span>

<span data-ttu-id="d2900-152">Mit virtuellen Azure-Netzwerken können Sie Datenverkehr zwischen Subnetzen wie folgt filtern:</span><span class="sxs-lookup"><span data-stu-id="d2900-152">Azure virtual networks enable you to filter traffic between subnets by using the following approaches:</span></span>

- <span data-ttu-id="d2900-153">**Netzwerksicherheitsgruppen**</span><span class="sxs-lookup"><span data-stu-id="d2900-153">**Network security groups**</span></span>

    <span data-ttu-id="d2900-154">Eine Netzwerksicherheitsgruppe ist eine Azure-Ressource, die mehrere Eingangs- und Ausgangssicherheitsregeln enthalten kann.</span><span class="sxs-lookup"><span data-stu-id="d2900-154">A network security group is an Azure resource that can contain multiple inbound and outbound security rules.</span></span> <span data-ttu-id="d2900-155">Sie können diese Regeln definieren, um Datenverkehr auf der Grundlage von Faktoren wie Quell- und Ziel-IP-Adresse, Port und Protokoll zuzulassen oder zu blockieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-155">You can define these rules to allow or block traffic, based on factors such as source and destination IP address, port, and protocol.</span></span>

- <span data-ttu-id="d2900-156">**Virtuelle Netzwerkgeräte**</span><span class="sxs-lookup"><span data-stu-id="d2900-156">**Network virtual appliances**</span></span>
    
    <span data-ttu-id="d2900-157">Ein virtuelles Netzwerkgerät ist ein spezieller virtueller Computer, der mit einem gehärteten Netzwerkgerät vergleichbar ist.</span><span class="sxs-lookup"><span data-stu-id="d2900-157">A network virtual appliance is a specialized VM that can be compared to a hardened network appliance.</span></span> <span data-ttu-id="d2900-158">Ein virtuelles Netzwerkgerät führt eine bestimmte Netzwerkfunktion aus (beispielsweise eine Firewall oder eine WAN-Optimierung).</span><span class="sxs-lookup"><span data-stu-id="d2900-158">A network virtual appliance carries out a particular network function, such as running a firewall or performing WAN optimization.</span></span>

## <a name="connect-virtual-networks"></a><span data-ttu-id="d2900-159">Verbindung virtueller Netzwerke</span><span class="sxs-lookup"><span data-stu-id="d2900-159">Connect virtual networks</span></span>

<span data-ttu-id="d2900-160">Virtuelle Netzwerke können mittels _Peering_ miteinander verknüpft werden.</span><span class="sxs-lookup"><span data-stu-id="d2900-160">You can link virtual networks together using virtual network _peering_.</span></span> <span data-ttu-id="d2900-161">Peering ermöglicht es Ressourcen in den einzelnen virtuellen Netzwerken, miteinander zu kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-161">Peering enables resources in each virtual network to communicate with each other.</span></span> <span data-ttu-id="d2900-162">Da sich diese virtuellen Netzwerke in unterschiedlichen Regionen befinden können, können Sie so über Azure ein globales, miteinander verbundenes Netzwerk erstellen.</span><span class="sxs-lookup"><span data-stu-id="d2900-162">These virtual networks can be in separate regions, allowing you to create a global interconnected network through Azure.</span></span>

## <a name="azure-virtual-network-settings"></a><span data-ttu-id="d2900-163">Einstellungen für virtuelle Azure-Netzwerke</span><span class="sxs-lookup"><span data-stu-id="d2900-163">Azure virtual network settings</span></span>

<span data-ttu-id="d2900-164">Virtuelle Azure-Netzwerke können über das Azure-Portal, mithilfe von Azure PowerShell auf Ihrem lokalen Computer oder mithilfe von Azure Cloud Shell erstellt und konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="d2900-164">You can create and configure Azure virtual networks from the Azure portal, Azure PowerShell on your local computer, or Azure Cloud Shell.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="d2900-165">Erstellen eines virtuellen Netzwerks</span><span class="sxs-lookup"><span data-stu-id="d2900-165">Create a virtual network</span></span>

<span data-ttu-id="d2900-166">Bei der Erstellung eines virtuellen Azure-Netzwerks muss eine Reihe von grundlegenden Einstellungen konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="d2900-166">When you create an Azure virtual network, you configure a number of basic settings.</span></span> <span data-ttu-id="d2900-167">Sie haben auch die Möglichkeit, erweiterte Einstellungen wie mehrere Subnetze, DDoS-Schutz (Distributed Denial of Service, verteilter Denial-of-Service-Angriff) und Dienstendpunkte zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-167">You also have the option to configure advanced settings, such as multiple subnets, distributed denial of service (DDoS) protection, and service endpoints.</span></span>

![Screenshot des Azure-Portals mit einem Beispiel der Felder des Blatts „Virtuelles Netzwerk erstellen“.](../media/2-create-virtual-network.PNG)

<span data-ttu-id="d2900-169">Für ein einfaches virtuelles Netzwerk müssen folgende Einstellungen konfiguriert werden:</span><span class="sxs-lookup"><span data-stu-id="d2900-169">Settings that you need to configure for a basic virtual network are:</span></span>

- <span data-ttu-id="d2900-170">**Netzwerkname**</span><span class="sxs-lookup"><span data-stu-id="d2900-170">**Network name**</span></span>

    <span data-ttu-id="d2900-171">Dieser Name muss in Ihrem Abonnement (aber nicht global) eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="d2900-171">This name must be unique in your subscription but does not need to be globally unique.</span></span> <span data-ttu-id="d2900-172">Verwenden Sie einen aussagekräftigen, einprägsamen Namen, der einfach von anderen virtuellen Netzwerken zu unterscheiden ist.</span><span class="sxs-lookup"><span data-stu-id="d2900-172">Make the name a descriptive one that is easy to remember and distinguish from other virtual networks.</span></span>

- <span data-ttu-id="d2900-173">**Adressraum**</span><span class="sxs-lookup"><span data-stu-id="d2900-173">**Address space**</span></span>
    
    <span data-ttu-id="d2900-174">Beim Einrichten eines virtuellen Netzwerks definieren Sie den internen Adressbereich im CIDR-Format (Classless Interdomain Routing, klassenloses domänenübergreifendes Routing).</span><span class="sxs-lookup"><span data-stu-id="d2900-174">When you set up a virtual network, you define the internal address space in Classless Interdomain Routing (CIDR) format.</span></span> <span data-ttu-id="d2900-175">Dieser Adressraum muss innerhalb Ihres Abonnements eindeutig sein. Es ist also beispielsweise nicht möglich, für ein virtuelles Netzwerk den Adressraum 10.0.0.0/24 und für ein anderes den Adressraum 10.1.0.0/8 festzulegen, da sich das Netzwerk 10.1.0.0/8 mit 10.0.0.0/24 überschneidet.</span><span class="sxs-lookup"><span data-stu-id="d2900-175">This address space needs to be unique within your subscription, so you cannot define an address space of, say, 10.0.0.0/24 for one virtual network and then 10.1.0.0/8 for another, as the 10.1.0.0/8 network will overlap 10.0.0.0/24.</span></span> <span data-ttu-id="d2900-176">Sie können jedoch beispielsweise 10.0.0.0/16 und 10.1.0.0/16 verwenden.</span><span class="sxs-lookup"><span data-stu-id="d2900-176">However, you can have 10.0.0.0/16 and 10.1.0.0/16, etc.</span></span> 
    > [!NOTE] 
    > <span data-ttu-id="d2900-177">Adressräume können nach der Erstellung des virtuellen Netzwerks hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="d2900-177">You can add address spaces after creating the virtual network.</span></span>

- <span data-ttu-id="d2900-178">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="d2900-178">**Subscription**</span></span>

    <span data-ttu-id="d2900-179">Gilt nur, wenn Sie über mehrere Abonnements verfügen.</span><span class="sxs-lookup"><span data-stu-id="d2900-179">Only applies if you have multiple subscriptions to choose from.</span></span>

- <span data-ttu-id="d2900-180">**Ressourcengruppe**</span><span class="sxs-lookup"><span data-stu-id="d2900-180">**Resource group**</span></span>
    
    <span data-ttu-id="d2900-181">Ein virtuelles Netzwerk muss sich genau wie jede andere Azure-Ressource in einer Ressourcengruppe befinden.</span><span class="sxs-lookup"><span data-stu-id="d2900-181">Like any other Azure resource, a virtual network needs to exist in a resource group.</span></span> <span data-ttu-id="d2900-182">Sie können entweder eine vorhandene Ressourcengruppe auswählen oder eine neue Ressourcengruppe erstellen.</span><span class="sxs-lookup"><span data-stu-id="d2900-182">You can either select an existing RG or create a new one.</span></span>
    
- <span data-ttu-id="d2900-183">**Standort**</span><span class="sxs-lookup"><span data-stu-id="d2900-183">**Location**</span></span>

    <span data-ttu-id="d2900-184">Wählen Sie den gewünschten Standort für das virtuelle Netzwerk aus.</span><span class="sxs-lookup"><span data-stu-id="d2900-184">Select the location where you want the virtual network to exist.</span></span>

- <span data-ttu-id="d2900-185">**Subnetz**</span><span class="sxs-lookup"><span data-stu-id="d2900-185">**Subnet**</span></span>
    
    <span data-ttu-id="d2900-186">Innerhalb der einzelnen Adressbereiche von virtuellen Netzwerken können Sie einzelne oder mehrere Subnetze erstellen, um den Adressraum des virtuellen Netzwerks zu partitionieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-186">Within each virtual network address range, you can create one or more subnets that partition the virtual network's address space.</span></span> <span data-ttu-id="d2900-187">Das Routing zwischen den Subnetzen basiert dann auf den standardmäßigen Datenverkehrsrouten. Sie können aber auch benutzerdefinierte Routen definieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-187">Routing between subnets will then depend on the default traffic routes, or you can define custom routes.</span></span> <span data-ttu-id="d2900-188">Alternativ können Sie ein Subnetz definieren, das alle Adressbereiche der virtuellen Netzwerke umfasst.</span><span class="sxs-lookup"><span data-stu-id="d2900-188">Alternatively, you can define one subnet that encompasses all the virtual networks' address ranges.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d2900-189">Subnetznamen müssen mit einem Buchstaben oder einer Zahl beginnen, mit einem Buchstaben, einer Zahl oder einem Unterstrich enden und dürfen nur Buchstaben, Zahlen, Unterstriche, Punkte oder Bindestriche enthalten.</span><span class="sxs-lookup"><span data-stu-id="d2900-189">Subnet names must begin with a letter or number, end with a letter, number or underscore, and may contain only letters, numbers, underscores, periods, or hyphens.</span></span>

- <span data-ttu-id="d2900-190">**DDoS-Schutz**</span><span class="sxs-lookup"><span data-stu-id="d2900-190">**DDoS protection**</span></span>

    <span data-ttu-id="d2900-191">Sie haben die Wahl zwischen zwei Optionen: „Basic“ und "Standard“.</span><span class="sxs-lookup"><span data-stu-id="d2900-191">You can select either Basic or Standard DDoS protection.</span></span> <span data-ttu-id="d2900-192">Der DDoS-Schutz „Standard“ ist ein Premium-Dienst.</span><span class="sxs-lookup"><span data-stu-id="d2900-192">Standard DDoS Protection is a premium service.</span></span> <span data-ttu-id="d2900-193">Weitere Informationen zum DDoS-Schutz „Standard“.</span><span class="sxs-lookup"><span data-stu-id="d2900-193">For more information on Standard DDoS protection.</span></span>

- <span data-ttu-id="d2900-194">**Dienstendpunkte**</span><span class="sxs-lookup"><span data-stu-id="d2900-194">**Service Endpoints**</span></span>
    
    <span data-ttu-id="d2900-195">Hier können Sie Dienstendpunkte aktivieren und in einer Liste auswählen, welche Azure-Dienstendpunkte Sie aktivieren möchten.</span><span class="sxs-lookup"><span data-stu-id="d2900-195">Here, you enable service endpoints, and then select from the list which Azure service endpoints you want to enable.</span></span> <span data-ttu-id="d2900-196">Mögliche Optionen sind beispielsweise Azure Cosmos DB, Azure Service Bus, Azure Key Vault und Ähnliches.</span><span class="sxs-lookup"><span data-stu-id="d2900-196">Options include Azure Cosmos DB, Azure Service Bus, Azure Key Vault, and so on.</span></span>

<span data-ttu-id="d2900-197">Klicken Sie nach dem Konfigurieren dieser Einstellungen auf die Schaltfläche **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="d2900-197">When you have configured these settings, click the **Create** button.</span></span>

### <a name="define-additional-settings"></a><span data-ttu-id="d2900-198">Definieren zusätzlicher Einstellungen</span><span class="sxs-lookup"><span data-stu-id="d2900-198">Define additional settings</span></span>

<span data-ttu-id="d2900-199">Nach dem Erstellen eines virtuellen Netzwerks können Sie weitere Einstellungen definieren.</span><span class="sxs-lookup"><span data-stu-id="d2900-199">After creating a virtual network, you can then define further settings.</span></span> <span data-ttu-id="d2900-200">Dazu zählen unter anderem folgende:</span><span class="sxs-lookup"><span data-stu-id="d2900-200">These include:</span></span>

- <span data-ttu-id="d2900-201">**Netzwerksicherheitsgruppe**</span><span class="sxs-lookup"><span data-stu-id="d2900-201">**Network security group**</span></span>
    
    <span data-ttu-id="d2900-202">Netzwerksicherheitsgruppen bieten Sicherheitsregeln, mit denen Sie den Typ des ein- und ausgehenden Netzwerkdatenverkehrs von Subnetzen virtueller Netzwerke und Netzwerkschnittstellen filtern können.</span><span class="sxs-lookup"><span data-stu-id="d2900-202">Network security groups have security rules that enable you to filter the type of network traffic that can flow in and out of virtual network subnets and network interfaces.</span></span> <span data-ttu-id="d2900-203">Die Netzwerksicherheitsgruppe muss separat erstellt und anschließend dem virtuellen Netzwerk zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="d2900-203">You create the network security group separately, and then associate it with the virtual network.</span></span>

- <span data-ttu-id="d2900-204">**Routingtabelle**</span><span class="sxs-lookup"><span data-stu-id="d2900-204">**Route table**</span></span>

    <span data-ttu-id="d2900-205">Azure erstellt automatisch eine Routentabelle für jedes Subnetz in einem virtuellen Azure-Netzwerk und fügt der Tabelle Systemstandardrouten hinzu.</span><span class="sxs-lookup"><span data-stu-id="d2900-205">Azure automatically creates a route table for each subnet within an Azure virtual network and adds system default routes to the table.</span></span> <span data-ttu-id="d2900-206">Sie können jedoch benutzerdefinierte Routingtabellen hinzufügen, um den Datenverkehr zwischen virtuellen Netzwerken zu ändern.</span><span class="sxs-lookup"><span data-stu-id="d2900-206">However, you can add custom route tables to modify traffic between virtual networks.</span></span>

<span data-ttu-id="d2900-207">Außerdem können Sie die Dienstendpunkte ändern.</span><span class="sxs-lookup"><span data-stu-id="d2900-207">You can also amend the service endpoints.</span></span>

![Screenshot des Azure-Portals mit einem Beispielblatt zum Bearbeiten der Einstellungen virtueller Netzwerke.](../media/2-virtual-network-additional-settings.PNG)

### <a name="configure-virtual-networks"></a><span data-ttu-id="d2900-209">Konfigurieren virtueller Netzwerke</span><span class="sxs-lookup"><span data-stu-id="d2900-209">Configure virtual networks</span></span>

<span data-ttu-id="d2900-210">Wenn Sie ein virtuelles Netzwerk erstellt haben, können Sie alle weiteren Einstellungsänderungen im Azure-Portal auf dem Blatt „Virtuelle Netzwerke“ vornehmen.</span><span class="sxs-lookup"><span data-stu-id="d2900-210">When you have created a virtual network, you can change any further settings from the Virtual Networks blade in the Azure portal.</span></span> <span data-ttu-id="d2900-211">Alternativ können Sie die Änderungen mithilfe von PowerShell-Befehlen oder mithilfe von Befehlen in Cloud Shell vornehmen.</span><span class="sxs-lookup"><span data-stu-id="d2900-211">Alternatively, you can use PowerShell commands or commands in Cloud Shell to make changes.</span></span>

![Screenshot des Azure-Portals mit einem Beispielblatt zum Konfigurieren eines virtuellen Netzwerks.](../media/2-configure-virtual-network.PNG)

<span data-ttu-id="d2900-213">Anschließend können Sie Einstellungen auf weiteren untergeordneten Blättern überprüfen und ändern.</span><span class="sxs-lookup"><span data-stu-id="d2900-213">You can then review and change settings in further sub-blades.</span></span>
<span data-ttu-id="d2900-214">Zu diesen Einstellungen zählen:</span><span class="sxs-lookup"><span data-stu-id="d2900-214">These settings include:</span></span>

- <span data-ttu-id="d2900-215">Adressräume</span><span class="sxs-lookup"><span data-stu-id="d2900-215">Address spaces</span></span>

    <span data-ttu-id="d2900-216">Sie können der ursprünglichen Definition weitere Adressräume hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d2900-216">You can add further address spaces to the initial definition</span></span>

- <span data-ttu-id="d2900-217">Verbundene Geräte</span><span class="sxs-lookup"><span data-stu-id="d2900-217">Connected devices</span></span>

    <span data-ttu-id="d2900-218">Verbinden Sie Computer über das virtuelle Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="d2900-218">Use the virtual network to connect machines</span></span>

- <span data-ttu-id="d2900-219">Subnetze</span><span class="sxs-lookup"><span data-stu-id="d2900-219">Subnets</span></span>

    <span data-ttu-id="d2900-220">Fügen Sie weitere Subnetze hinzu.</span><span class="sxs-lookup"><span data-stu-id="d2900-220">Add further subnets</span></span>

- <span data-ttu-id="d2900-221">Peerings</span><span class="sxs-lookup"><span data-stu-id="d2900-221">Peerings</span></span>

    <span data-ttu-id="d2900-222">Verknüpfen Sie virtuelle Netzwerke mittels Peering.</span><span class="sxs-lookup"><span data-stu-id="d2900-222">Link virtual networks in peering arrangements</span></span>

<span data-ttu-id="d2900-223">Sie können auch virtuelle Netzwerke überwachen und Probleme mit virtuellen Netzwerken behandeln oder ein Automatisierungsskript für die Generierung des aktuellen virtuellen Netzwerks erstellen.</span><span class="sxs-lookup"><span data-stu-id="d2900-223">You can also monitor and troubleshoot virtual networks, or create an automation script to generate the current virtual network.</span></span>

## <a name="summary"></a><span data-ttu-id="d2900-224">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="d2900-224">Summary</span></span>

<span data-ttu-id="d2900-225">Virtuelle Netzwerke sind leistungsstarke und präzise konfigurierbare Mechanismen für die Verbindungsherstellung zwischen Entitäten in Azure.</span><span class="sxs-lookup"><span data-stu-id="d2900-225">Virtual networks are powerful and highly configurable mechanisms for connecting entities in Azure.</span></span> <span data-ttu-id="d2900-226">Sie können Azure-Ressourcen untereinander oder mit lokalen Ressourcen verbinden.</span><span class="sxs-lookup"><span data-stu-id="d2900-226">You can connect Azure resources to one another or to resources you have on-premises.</span></span> <span data-ttu-id="d2900-227">Außerdem können Sie Netzwerkdatenverkehr isolieren, filtern und weiterleiten und mithilfe von Azure bei Bedarf die Sicherheit erhöhen.</span><span class="sxs-lookup"><span data-stu-id="d2900-227">You can isolate, filter and route your network traffic, and Azure allows you to increase security where you feel you need it.</span></span>
