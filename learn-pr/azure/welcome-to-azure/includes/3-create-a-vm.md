<span data-ttu-id="b2656-101">Sie haben sich wahrscheinlich auf einen bestimmten Fachbereich spezialisiert.</span><span class="sxs-lookup"><span data-stu-id="b2656-101">As a technology professional, you likely have expertise in a specific area.</span></span> <span data-ttu-id="b2656-102">Vielleicht sind Sie Speicheradministrator oder Experte für Virtualisierung, oder Sie beschäftigen sich mit den neusten Sicherheitsmaßnahmen.</span><span class="sxs-lookup"><span data-stu-id="b2656-102">Perhaps you're a storage admin or virtualization expert, or maybe you focus on the latest security practices.</span></span> <span data-ttu-id="b2656-103">Wenn Sie noch studieren, haben Sie sich möglicherweise aber noch gar nicht spezialisiert.</span><span class="sxs-lookup"><span data-stu-id="b2656-103">If you're a student, you may still be exploring what interests you most.</span></span>

<span data-ttu-id="b2656-104">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="b2656-104">::: zone pivot="windows-cloud"</span></span>

<span data-ttu-id="b2656-105">Die meisten Menschen – egal, in welcher Position –, die sich zum ersten Mal mit einer Cloud beschäftigen, erstellen zunächst einmal einen virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="b2656-105">No matter your role, most people get started with the cloud by creating a virtual machine.</span></span> <span data-ttu-id="b2656-106">In diesem Beispiel wird ein virtueller Computer erstellt, der Windows Server 2016 ausführt.</span><span class="sxs-lookup"><span data-stu-id="b2656-106">Here you'll bring up a virtual machine running Windows Server 2016.</span></span>

<span data-ttu-id="b2656-107">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="b2656-107">::: zone-end</span></span>

<span data-ttu-id="b2656-108">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="b2656-108">::: zone pivot="linux-cloud"</span></span>

<span data-ttu-id="b2656-109">Die meisten Menschen – egal, in welcher Position –, die sich zum ersten Mal mit einer Cloud beschäftigen, erstellen zunächst einmal einen virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="b2656-109">No matter your role, most people get started with the cloud by creating a virtual machine.</span></span> <span data-ttu-id="b2656-110">In diesem Beispiel wird ein virtueller Computer erstellt, der Ubuntu 16.04 ausführt.</span><span class="sxs-lookup"><span data-stu-id="b2656-110">Here you'll bring up a virtual machine running Ubuntu 16.04.</span></span>

<span data-ttu-id="b2656-111">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="b2656-111">::: zone-end</span></span>

<span data-ttu-id="b2656-112">Es gibt verschiedene Möglichkeiten, einen virtuellen Computer in Azure zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b2656-112">There are many ways to create a virtual machine on Azure.</span></span> <span data-ttu-id="b2656-113">In diesem Beispiel wird mithilfe eines virtuellen Windows- oder Linux-Computers ein interaktives Terminal namens Cloud Shell erstellt.</span><span class="sxs-lookup"><span data-stu-id="b2656-113">Here, you'll bring up a Windows or Linux virtual machine using an interactive terminal called Cloud Shell.</span></span> <span data-ttu-id="b2656-114">Wenn Sie täglich über das Terminal arbeiten, ist ihnen bestimmt klar, dass dies die schnellste Möglichkeit ist.</span><span class="sxs-lookup"><span data-stu-id="b2656-114">If you work from the terminal on a daily basis, you know this is often the fastest way to get the job done.</span></span>

<span data-ttu-id="b2656-115">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="b2656-115">::: zone pivot="windows-cloud"</span></span>

> [!TIP]
> <span data-ttu-id="b2656-116">Arbeiten Sie lieber mit Linux, oder möchten Sie etwas neues ausprobieren?</span><span class="sxs-lookup"><span data-stu-id="b2656-116">Prefer Linux or want to try something new?</span></span> <span data-ttu-id="b2656-117">Klicken Sie oben auf der Seite auf **Linux**, um einen virtuellen Linux-Computer auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b2656-117">Select **Linux** from the top of this page to run a Linux virtual machine.</span></span>

<span data-ttu-id="b2656-118">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="b2656-118">::: zone-end</span></span>

<span data-ttu-id="b2656-119">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="b2656-119">::: zone pivot="linux-cloud"</span></span>

> [!TIP]
> <span data-ttu-id="b2656-120">Arbeiten Sie lieber mit Windows, oder möchten Sie etwas neues ausprobieren?</span><span class="sxs-lookup"><span data-stu-id="b2656-120">Prefer Windows or want to try something new?</span></span> <span data-ttu-id="b2656-121">Klicken Sie oben auf der Seite auf **Windows**, um einen virtuellen Windows Server-Computer auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b2656-121">Select **Windows** from the top of this page to run a Windows Server virtual machine.</span></span>

<span data-ttu-id="b2656-122">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="b2656-122">::: zone-end</span></span>

<span data-ttu-id="b2656-123">Nachfolgend werden einige Grundbegriffe erläutert, und Sie erfahren, wie Sie Ihren ersten virtuellen Computer starten können.</span><span class="sxs-lookup"><span data-stu-id="b2656-123">Let's review some basic terms and get your first virtual machine up and running.</span></span>

## <a name="what-is-a-virtual-machine"></a><span data-ttu-id="b2656-124">Was ist ein virtueller Computer?</span><span class="sxs-lookup"><span data-stu-id="b2656-124">What is a virtual machine?</span></span>

<span data-ttu-id="b2656-125">Ein virtueller Computer (VM) ist eine Softwareemulation eines physischen Computers.</span><span class="sxs-lookup"><span data-stu-id="b2656-125">A virtual machine, or VM, is a software emulation of a physical computer.</span></span> <span data-ttu-id="b2656-126">Da es sich um Software handelt, können Tausende von Azure-VMs innerhalb einer Minute erstellt und anschließend wieder gelöscht werden, wenn Sie sie nicht mehr brauchen.</span><span class="sxs-lookup"><span data-stu-id="b2656-126">Because VMs exist as software, dozens, hundreds, or even thousands of Azure VMs can be generated in minutes, then deleted when you don't need them anymore.</span></span> <span data-ttu-id="b2656-127">Die Kosten sind gering, und Sie zahlen auf die Minute genau nur dann für die Computeressourcen, wenn Sie sie benötigen.</span><span class="sxs-lookup"><span data-stu-id="b2656-127">With low-cost, per-minute billing, you pay only for the compute resources you use, for as long as you are using them.</span></span> <span data-ttu-id="b2656-128">Außerdem gibt es einige Möglichkeiten, die VMs so zu konfigurieren, dass sie Ihren Ansprüchen gerecht werden.</span><span class="sxs-lookup"><span data-stu-id="b2656-128">Plus, there are many ways to configure the VMs to fit your needs.</span></span>

<span data-ttu-id="b2656-129">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="b2656-129">::: zone pivot="windows-cloud"</span></span>

<span data-ttu-id="b2656-130">Eine Momentaufnahme einer VM, die gerade ausgeführt wird, wird als _Image_ bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="b2656-130">A snapshot of a running VM is called an _image_.</span></span> <span data-ttu-id="b2656-131">Azure stellt Images für Windows sowie für einige Linux-Versionen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="b2656-131">Azure provides images for Windows and several flavors of Linux.</span></span> <span data-ttu-id="b2656-132">Außerdem können Sie eigene vorkonfigurierte Images erstellen, damit Bereitstellungen schneller durchgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="b2656-132">You can also create your own preconfigured images to make deployments go faster.</span></span> <span data-ttu-id="b2656-133">In diesem Beispiel wird eine Windows Server 2016-VM erstellt, die von Microsoft bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="b2656-133">Here you'll bring up a Windows Server 2016 VM, provided by Microsoft.</span></span>

<span data-ttu-id="b2656-134">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="b2656-134">::: zone-end</span></span>

<span data-ttu-id="b2656-135">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="b2656-135">::: zone pivot="linux-cloud"</span></span>

<span data-ttu-id="b2656-136">Eine Momentaufnahme einer VM, die gerade ausgeführt wird, wird als _Image_ bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="b2656-136">A snapshot of a running VM is called an _image_.</span></span> <span data-ttu-id="b2656-137">Azure stellt Images für Windows sowie für einige Linux-Versionen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="b2656-137">Azure provides images for Windows and several flavors of Linux.</span></span> <span data-ttu-id="b2656-138">Außerdem können Sie eigene vorkonfigurierte Images erstellen, damit Bereitstellungen schneller durchgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="b2656-138">You can also create your own preconfigured images to make deployments go faster.</span></span> <span data-ttu-id="b2656-139">In diesem Beispiel wird eine Ubuntu 16.04-VM erstellt, die von Canonical bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="b2656-139">Here you'll bring up an Ubuntu 16.04 VM, provided by Canonical.</span></span>

<span data-ttu-id="b2656-140">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="b2656-140">::: zone-end</span></span>

## <a name="what-defines-a-virtual-machine-on-azure"></a><span data-ttu-id="b2656-141">Was macht einen virtuellen Computer in Azure aus?</span><span class="sxs-lookup"><span data-stu-id="b2656-141">What defines a virtual machine on Azure?</span></span>

<span data-ttu-id="b2656-142">Ein virtueller Computer wird von verschiedenen Faktoren beeinflusst, einschließlich der Größe und dem Standort.</span><span class="sxs-lookup"><span data-stu-id="b2656-142">A virtual machine is defined by a number of factors, including its size and location.</span></span> <span data-ttu-id="b2656-143">Bevor Sie den virtuellen Computer erstellen, werden nachfolgend die wichtigsten Aspekte erläutert.</span><span class="sxs-lookup"><span data-stu-id="b2656-143">Before you bring up your VM, let's briefly cover what's involved.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="b2656-144">**Größe**</span><span class="sxs-lookup"><span data-stu-id="b2656-144">**Size**</span></span>
    :::column-end:::
    <span data-ttu-id="b2656-145">:::column span="3"::: Die Prozessorgeschwindigkeit, die Speicherkapazität, die anfängliche Auslastung des Speichers und die erwartete Netzwerkbandbreite werden von der _Größe_ der VM bestimmt.</span><span class="sxs-lookup"><span data-stu-id="b2656-145">:::column span="3"::: A VM's _size_ defines its processor speed, amount of memory, initial amount of storage, and expected network bandwidth.</span></span> <span data-ttu-id="b2656-146">Einige Größen umfassen sogar spezielle Hardware wie GPUs für intensives Grafikrendering und die Bearbeitung von Videos.</span><span class="sxs-lookup"><span data-stu-id="b2656-146">Some sizes even include specialized hardware such as GPUs for heavy graphics rendering and video editing.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="b2656-147">**Region**</span><span class="sxs-lookup"><span data-stu-id="b2656-147">**Region**</span></span>
    :::column-end:::
    <span data-ttu-id="b2656-148">:::column span="3"::: Azure besteht aus Rechenzentren, die auf der ganzen Welt verteilt sind.</span><span class="sxs-lookup"><span data-stu-id="b2656-148">:::column span="3"::: Azure is made up of data centers distributed throughout the world.</span></span> <span data-ttu-id="b2656-149">Als _Region_ werden mehrere Azure-Rechenzentren in einem geografisch begrenzten Gebiet bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="b2656-149">A _region_ is a set of Azure data centers in a named geographic location.</span></span> <span data-ttu-id="b2656-150">Jede Azure-Ressource, einschließlich virtueller Computer, wird einer Region zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="b2656-150">Every Azure resource, including virtual machines, is assigned a region.</span></span> <span data-ttu-id="b2656-151">Beispiele für Regionen sind „USA, Osten“ und „Europa, Norden“.</span><span class="sxs-lookup"><span data-stu-id="b2656-151">East US and North Europe are examples of regions.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="b2656-152">**Netzwerk**</span><span class="sxs-lookup"><span data-stu-id="b2656-152">**Network**</span></span>
    :::column-end:::
    <span data-ttu-id="b2656-153">:::column span="3"::: Ein _virtuelles Netzwerk_ ist ein logisch isoliertes Netzwerk in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2656-153">:::column span="3"::: A _virtual network_ is a logically isolated network on Azure.</span></span> <span data-ttu-id="b2656-154">Jeder virtuelle Computer in Azure wird einem virtuellen Netzwerk zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="b2656-154">Each virtual machine on Azure is associated with a virtual network.</span></span> <span data-ttu-id="b2656-155">Azure stellt Firewalls auf Cloudebene für Ihre virtuellen Netzwerke (_Netzwerksicherheitsgruppen_) bereit.</span><span class="sxs-lookup"><span data-stu-id="b2656-155">Azure provides cloud-level firewalls for your virtual networks called _network security groups_.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="b2656-156">**Ressourcengruppen**</span><span class="sxs-lookup"><span data-stu-id="b2656-156">**Resource groups**</span></span>
    :::column-end:::
    <span data-ttu-id="b2656-157">:::column span="3"::: Virtuelle Computer und Cloudressourcen werden in logische Container zusammengefasst, die als _Ressourcengruppen_ bezeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="b2656-157">:::column span="3"::: Virtual machines and other cloud resources are grouped into logical containers called _resource groups_.</span></span> <span data-ttu-id="b2656-158">Gruppen werden in der Regel verwendet, um mehrere Ressourcen zu organisieren, die gemeinsam als Bestandteile einer Anwendung oder eines Dienst bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="b2656-158">Groups are typically used to organize sets of resources that are deployed together as part of an application or service.</span></span> <span data-ttu-id="b2656-159">Sie können Ressourcengruppen über den jeweiligen Namen finden.</span><span class="sxs-lookup"><span data-stu-id="b2656-159">You refer to a resource group by its name.</span></span>
    :::column-end:::
:::row-end:::

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="b2656-160">Was ist Azure Cloud Shell?</span><span class="sxs-lookup"><span data-stu-id="b2656-160">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="b2656-161">Azure Cloud Shell ist ein browserbasierter Dienst zum Verwalten und Entwickeln von Azure-Ressourcen über die Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="b2656-161">Azure Cloud Shell is a browser-based command-line experience for managing and developing Azure resources.</span></span> <span data-ttu-id="b2656-162">Stellen Sie sich Cloud Shell als eine interaktive Konsole vor, die in der Cloud ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="b2656-162">Think of Cloud Shell as an interactive console that you run in the cloud.</span></span>

<span data-ttu-id="b2656-163">Cloud Shell stellt zwei Funktionen bereit, aus denen Sie auswählen können: Bash und PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2656-163">Cloud Shell provides two experiences to choose from: Bash and PowerShell.</span></span> <span data-ttu-id="b2656-164">Über beide Funktionen erhalten Sie Zugriff auf die Azure CLI, die Befehlszeilenschnittstelle für Azure.</span><span class="sxs-lookup"><span data-stu-id="b2656-164">Both include access to the Azure CLI, the command-line interface for Azure.</span></span>

<span data-ttu-id="b2656-165">Sie können jede beliebige Verwaltungsschnittstelle von Azure verwenden, einschließlich des Azure-Portals, der Azure CLI und Azure PowerShell, um eine VM (egal, welcher Art) zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="b2656-165">You can use any Azure management interface, including the Azure portal, Azure CLI, and Azure PowerShell, to manage any kind of VM.</span></span> <span data-ttu-id="b2656-166">Zu Lernzwecken wird hier die Azure CLI verwendet, um virtuelle Windows- oder Linux-Computer zu erstellen und zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="b2656-166">For learning purposes, here you'll use the Azure CLI to create and manage either a Windows or Linux VM.</span></span>

<span data-ttu-id="b2656-167">::: zone pivot="windows-cloud"</span><span class="sxs-lookup"><span data-stu-id="b2656-167">::: zone pivot="windows-cloud"</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="b2656-168">Erstellen einer Windows-VM</span><span class="sxs-lookup"><span data-stu-id="b2656-168">Create a Windows VM</span></span>

<span data-ttu-id="b2656-169">Nachfolgend wird erläutert, wie Sie Ihre Windows-VM startbereit machen.</span><span class="sxs-lookup"><span data-stu-id="b2656-169">Let's get your Windows VM up and running.</span></span>

1. <span data-ttu-id="b2656-170">Führen Sie über Cloud Shell rechts auf der Seite den Befehl `az group create` aus, um eine Ressourcengruppe mit dem Namen **myResourceGroup** in der Region „USA, Osten“ zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b2656-170">From Cloud Shell on the right side of this page, run the `az group create` command to create a resource group named **myResourceGroup** in the East US region.</span></span>

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```

1. <span data-ttu-id="b2656-171">Führen Sie den Befehl `az vm create` aus, um die VM zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b2656-171">Run the `az vm create` command to create your VM.</span></span> <span data-ttu-id="b2656-172">Es wird empfohlen, das nachfolgend dargestellte Kennwort zu ändern. Merken Sie sich dieses Kennwort anschließend für später.</span><span class="sxs-lookup"><span data-stu-id="b2656-172">We recommend you change the password shown below to one you'll remember later.</span></span>

      > [!NOTE]
    > <span data-ttu-id="b2656-173">Wählen Sie ein Kennwort aus, das mindestens 8 Zeichen und eine Kombination aus Groß- und Kleinbuchstaben sowie Symbolen umfasst.</span><span class="sxs-lookup"><span data-stu-id="b2656-173">Choose a password that contains at least 8 characters with a combination of upper and lowercase letters, numbers, and symbols.</span></span>

    ```azurecli
    az vm create \
      --name myWindowsVM \
      --resource-group myResourceGroup \
      --image Win2016Datacenter \
      --size Standard_DS2_v2 \
      --location eastus \
      --admin-username azureuser \
      --admin-password "Password1234&"
    ```

    > [!TIP]
    > <span data-ttu-id="b2656-174">Sie können jeden Befehl über die Schaltfläche **Kopieren** kopieren.</span><span class="sxs-lookup"><span data-stu-id="b2656-174">You can use the **Copy** button to copy each command.</span></span> <span data-ttu-id="b2656-175">Klicken Sie zum Einfügen erst mit der rechten Maustaste auf die neue Zeile im Cloud Shell-Fenster und anschließend mit der Linken auf **Einfügen**.</span><span class="sxs-lookup"><span data-stu-id="b2656-175">To paste it, right click on the new line in the Cloud Shell window and select **Paste**.</span></span>

    <span data-ttu-id="b2656-176">Es dauert vier bis fünf Minuten, bis Sie auf die VM zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="b2656-176">Your VM will take four to five minutes to come up.</span></span> <span data-ttu-id="b2656-177">Vergleichen Sie das mit der Zeit, die es dauert, ein System für Ihr Rechenzentrum zu kaufen, es einzubauen und zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="b2656-177">Compare that to the time it takes to purchase, rack, and configure a system in your data center.</span></span> <span data-ttu-id="b2656-178">Der Unterschied ist erheblich.</span><span class="sxs-lookup"><span data-stu-id="b2656-178">Quite a difference!</span></span>

<span data-ttu-id="b2656-179">Solange Sie warten, können Sie sich den Befehl genauer ansehen, den Sie zuvor ausgeführt haben.</span><span class="sxs-lookup"><span data-stu-id="b2656-179">While you're waiting, let's review the command you just ran.</span></span>

* <span data-ttu-id="b2656-180">Die VM hat den Namen **myWindowsVM**.</span><span class="sxs-lookup"><span data-stu-id="b2656-180">The VM is named **myWindowsVM**.</span></span> <span data-ttu-id="b2656-181">Über diesen Namen kann die VM in Azure ermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="b2656-181">This name identifies the VM in Azure.</span></span> <span data-ttu-id="b2656-182">Außerdem handelt es sich um den internen Hostnamen der VM oder den Computernamen.</span><span class="sxs-lookup"><span data-stu-id="b2656-182">It also becomes the VM's internal hostname, or computer name.</span></span>
* <span data-ttu-id="b2656-183">Die Ressourcengruppe bzw. der logische Container der VM wird als **myResourceGroup** bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="b2656-183">The resource group, or the VM's logical container, is named **myResourceGroup**.</span></span>
* <span data-ttu-id="b2656-184">**Win2016Datacenter** ist das Image der Windows Server 2016-VM.</span><span class="sxs-lookup"><span data-stu-id="b2656-184">**Win2016Datacenter** specifies the Windows Server 2016 VM image.</span></span>
* <span data-ttu-id="b2656-185">**Standard_DS2_v2** bezieht sich auf die Größe der VM.</span><span class="sxs-lookup"><span data-stu-id="b2656-185">**Standard_DS2_v2** refers to the size of the VM.</span></span> <span data-ttu-id="b2656-186">Die Größe umfasst zwei virtuelle CPUs und 7 GB Arbeitsspeicher.</span><span class="sxs-lookup"><span data-stu-id="b2656-186">This size has two virtual CPUs and 7 GB of memory.</span></span>
* <span data-ttu-id="b2656-187">Die VM befindet sich am Standort bzw. in der Region **USA, Osten**.</span><span class="sxs-lookup"><span data-stu-id="b2656-187">The VM exists in the **East US** location, or region.</span></span>
* <span data-ttu-id="b2656-188">Über den Benutzernamen und das Kennwort können Sie später eine Verbindung mit der VM herstellen.</span><span class="sxs-lookup"><span data-stu-id="b2656-188">The username and password enable you to connect to your VM later.</span></span> <span data-ttu-id="b2656-189">Sie können beispielsweise über Remotedesktop oder WinRM eine Verbindung herstellen, um mit dem System arbeiten zu können bzw. um dieses zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="b2656-189">For example, you can connect over Remote Desktop or WinRM to work with and configure the system.</span></span>

<span data-ttu-id="b2656-190">Standardmäßig weist Azure Ihrer VM eine öffentliche IP-Adresse zu.</span><span class="sxs-lookup"><span data-stu-id="b2656-190">By default, Azure assigns a public IP address to your VM.</span></span> <span data-ttu-id="b2656-191">Sie können eine VM so konfigurieren, dass man über das Internet oder nur über das interne Netzwerk auf sie zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="b2656-191">You can configure a VM to be accessible from the Internet or only from the internal network.</span></span>

<span data-ttu-id="b2656-192">Sie können sich auch das folgende kurze Video zu den Möglichkeiten zum Erstellen und Verwalten von VMs ansehen.</span><span class="sxs-lookup"><span data-stu-id="b2656-192">You can also check out this short video about some of the options you have to create and manage VMs.</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

<span data-ttu-id="b2656-193">Wenn die VM bereit ist, erhalten Sie eine Mitteilung.</span><span class="sxs-lookup"><span data-stu-id="b2656-193">When the VM is ready, you see information about it.</span></span> <span data-ttu-id="b2656-194">Hier sehen Sie ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="b2656-194">Here's an example.</span></span>

```console
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myWindowsVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1E-1B-3B",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.5",
  "publicIpAddress": "104.211.9.245",
  "resourceGroup": "myResourceGroup",
  "zones": ""
}
```

<span data-ttu-id="b2656-195">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="b2656-195">::: zone-end</span></span>

<span data-ttu-id="b2656-196">::: zone pivot="linux-cloud"</span><span class="sxs-lookup"><span data-stu-id="b2656-196">::: zone pivot="linux-cloud"</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="b2656-197">Erstellen eines virtuellen Linux-Computers</span><span class="sxs-lookup"><span data-stu-id="b2656-197">Create a Linux VM</span></span>

<span data-ttu-id="b2656-198">Nachfolgend wird erläutert, wie Sie Ihre Linux-VM startbereit machen.</span><span class="sxs-lookup"><span data-stu-id="b2656-198">Let's get your Linux VM up and running.</span></span>

1. <span data-ttu-id="b2656-199">Führen Sie über Cloud Shell rechts auf der Seite den Befehl `az group create` aus, um eine Ressourcengruppe mit dem Namen **myResourceGroup** in der Region „USA, Osten“ zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b2656-199">From Cloud Shell on the right side of this page, run the `az group create` command to create a resource group named **myResourceGroup** in the East US region.</span></span>

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```

1. <span data-ttu-id="b2656-200">Führen Sie den Befehl `az vm create` aus, um die VM zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b2656-200">Run the `az vm create` command to create your VM.</span></span>

    ```azurecli
    az vm create \
      --name myLinuxVM \
      --resource-group myResourceGroup \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --location eastus \
      --generate-ssh-keys
    ```

    > [!TIP]
    > <span data-ttu-id="b2656-201">Sie können jeden Befehl über die Schaltfläche **Kopieren** kopieren.</span><span class="sxs-lookup"><span data-stu-id="b2656-201">You can use the **Copy** button to copy each command.</span></span> <span data-ttu-id="b2656-202">Klicken Sie zum Einfügen erst mit der rechten Maustaste auf die neue Zeile im Cloud Shell-Fenster und anschließend mit der Linken auf **Einfügen**.</span><span class="sxs-lookup"><span data-stu-id="b2656-202">To paste it, right click on the new line in the Cloud Shell window and select **Paste**.</span></span>

    <span data-ttu-id="b2656-203">Es dauert etwa zwei Minuten, bis Sie auf die VM zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="b2656-203">Your VM will take about two minutes to come up.</span></span> <span data-ttu-id="b2656-204">Vergleichen Sie das mit der Zeit, die es dauert, ein System für Ihr Rechenzentrum zu kaufen, es einzubauen und zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="b2656-204">Compare that to the time it takes to purchase, rack, and configure a system in your data center.</span></span> <span data-ttu-id="b2656-205">Der Unterschied ist erheblich.</span><span class="sxs-lookup"><span data-stu-id="b2656-205">Quite a difference!</span></span>

<span data-ttu-id="b2656-206">Solange Sie warten, können Sie sich den Befehl genauer ansehen, den Sie zuvor ausgeführt haben.</span><span class="sxs-lookup"><span data-stu-id="b2656-206">While you're waiting, let's review the command you just ran.</span></span>

* <span data-ttu-id="b2656-207">Die VM hat den Namen **myLinuxVM**.</span><span class="sxs-lookup"><span data-stu-id="b2656-207">The VM is named **myLinuxVM**.</span></span> <span data-ttu-id="b2656-208">Über diesen Namen kann die VM in Azure ermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="b2656-208">This name identifies the VM in Azure.</span></span> <span data-ttu-id="b2656-209">Außerdem handelt es sich um den internen Hostnamen der VM oder den Computernamen.</span><span class="sxs-lookup"><span data-stu-id="b2656-209">It also becomes the VM's internal hostname, or computer name.</span></span>
* <span data-ttu-id="b2656-210">Die Ressourcengruppe bzw. der logische Container der VM wird als **myResourceGroup** bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="b2656-210">The resource group, or the VM's logical container, is named **myResourceGroup**.</span></span>
* <span data-ttu-id="b2656-211">**UbuntuLTS** bezeichnet das Image der Ubuntu 16.04 LTS-VM.</span><span class="sxs-lookup"><span data-stu-id="b2656-211">**UbuntuLTS** specifies the Ubuntu 16.04 LTS VM image.</span></span>
* <span data-ttu-id="b2656-212">**Standard_DS2_v2** bezieht sich auf die Größe der VM.</span><span class="sxs-lookup"><span data-stu-id="b2656-212">**Standard_DS2_v2** refers to the size of the VM.</span></span> <span data-ttu-id="b2656-213">Die Größe umfasst zwei virtuelle CPUs und 7 GB Arbeitsspeicher.</span><span class="sxs-lookup"><span data-stu-id="b2656-213">This size has two virtual CPUs and 7 GB of memory.</span></span>
* <span data-ttu-id="b2656-214">Die VM befindet sich am Standort bzw. in der Region **USA, Osten**.</span><span class="sxs-lookup"><span data-stu-id="b2656-214">The VM exists in the **East US** location, or region.</span></span>
* <span data-ttu-id="b2656-215">Über die Option `--generate-ssh-keys` wird ein SSH-Schlüsselpaar erstellt, mit dem Sie sich bei der VM anmelden können.</span><span class="sxs-lookup"><span data-stu-id="b2656-215">The `--generate-ssh-keys` option creates an SSH key pair to enable you to log in to the VM.</span></span>

<span data-ttu-id="b2656-216">Standardmäßig weist Azure Ihrer VM eine öffentliche IP-Adresse zu.</span><span class="sxs-lookup"><span data-stu-id="b2656-216">By default, Azure assigns a public IP address to your VM.</span></span> <span data-ttu-id="b2656-217">Sie können eine VM so konfigurieren, dass man über das Internet oder nur über das interne Netzwerk auf sie zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="b2656-217">You can configure a VM to be accessible from the Internet or only from the internal network.</span></span>

<span data-ttu-id="b2656-218">Sie können sich auch das folgende kurze Video zu den Möglichkeiten zum Erstellen und Verwalten von VMs ansehen.</span><span class="sxs-lookup"><span data-stu-id="b2656-218">You can also check out this short video about some of the options you have to create and manage VMs.</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

<span data-ttu-id="b2656-219">Wenn die VM bereit ist, erhalten Sie eine Mitteilung.</span><span class="sxs-lookup"><span data-stu-id="b2656-219">When the VM is ready, you see information about it.</span></span> <span data-ttu-id="b2656-220">Hier sehen Sie ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="b2656-220">Here's an example.</span></span>

```console
{
    "fqdns": "",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myLinuxVM",
    "location": "eastus",
    "macAddress": "00-0D-3A-1D-EB-02",
    "powerState": "VM running",
    "privateIpAddress": "10.0.0.4",
    "publicIpAddress": "137.135.110.210",
    "resourceGroup": "myResourceGroup",
    "zones": ""
}
```

<span data-ttu-id="b2656-221">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="b2656-221">::: zone-end</span></span>

## <a name="summary"></a><span data-ttu-id="b2656-222">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="b2656-222">Summary</span></span>

<span data-ttu-id="b2656-223">Es bedarf nur wenig, damit Sie innerhalb weniger Minuten in Azure eine VM erstellen können.</span><span class="sxs-lookup"><span data-stu-id="b2656-223">With just a few concepts under your belt, you're able to spin up a VM on Azure in just a few minutes.</span></span> <span data-ttu-id="b2656-224">Mit einigen der benötigten Aspekte wie der Größe einer VM und Firewallregeln sind Sie wahrscheinlich schon vertraut.</span><span class="sxs-lookup"><span data-stu-id="b2656-224">Many of these concepts, such as a VM's size and firewall rules, are likely familiar to you already.</span></span>

<span data-ttu-id="b2656-225">Als nächstes erfahren Sie, wie Sie einen Webserver auf Ihrer VM installieren und diesen konfigurieren, um eine Standardwebsite bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="b2656-225">Next, you'll install a web server on your VM and configure your web server to serve up a basic web site.</span></span>