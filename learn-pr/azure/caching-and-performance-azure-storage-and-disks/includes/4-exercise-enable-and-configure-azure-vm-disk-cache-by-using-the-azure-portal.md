
<span data-ttu-id="e48f9-101">Angenommen, Sie betreiben eine Website zum Teilen von Fotos, bei der Daten auf virtuellen Azure-Maschinen (VMs) mit SQL Server und benutzerdefinierten Anwendungen gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="e48f9-101">Suppose you run a photo sharing site, with data stored on Azure virtual machines (VMs) running SQL Server and custom applications.</span></span> <span data-ttu-id="e48f9-102">Sie möchten die folgenden Anpassungen vornehmen:</span><span class="sxs-lookup"><span data-stu-id="e48f9-102">You want to make the following adjustments:</span></span>

- <span data-ttu-id="e48f9-103">Sie müssen die Einstellungen für den Datenträgercache auf einer VM ändern.</span><span class="sxs-lookup"><span data-stu-id="e48f9-103">You need to change the disk cache settings on a VM.</span></span>
- <span data-ttu-id="e48f9-104">Sie möchten einen neuen Datenträger für Daten zur VM mit aktivierter Zwischenspeicherung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="e48f9-104">You want to add a new data disk to the VM with caching enabled.</span></span>

<span data-ttu-id="e48f9-105">Sie haben sich dafür entschieden, diese Änderungen über das Azure-Portal vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="e48f9-105">You've decided to make these changes through the Azure portal.</span></span>

<span data-ttu-id="e48f9-106">In dieser Übung wird Schritt für Schritt erklärt, wie Sie die Änderungen an einer VM vornehmen, die oben beschrieben wurde.</span><span class="sxs-lookup"><span data-stu-id="e48f9-106">In this exercise, we'll walk through making the changes to a VM that we described above.</span></span> <span data-ttu-id="e48f9-107">Zuerst melden Sie sich am Portal an und erstellen eine VM.</span><span class="sxs-lookup"><span data-stu-id="e48f9-107">First, let's sign in to the portal and create a VM.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-virtual-machine"></a><span data-ttu-id="e48f9-108">Erstellen einer virtuellen Maschine</span><span class="sxs-lookup"><span data-stu-id="e48f9-108">Create a virtual machine</span></span>

<span data-ttu-id="e48f9-109">In diesem Schritt erstellen wir eine VM mit den folgenden Eigenschaften:</span><span class="sxs-lookup"><span data-stu-id="e48f9-109">In this step, we're going to create a VM with the following properties:</span></span>

| <span data-ttu-id="e48f9-110">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="e48f9-110">Property</span></span>        | <span data-ttu-id="e48f9-111">Wert</span><span class="sxs-lookup"><span data-stu-id="e48f9-111">Value</span></span>   |
|-----------------|---------|
| <span data-ttu-id="e48f9-112">Image</span><span class="sxs-lookup"><span data-stu-id="e48f9-112">Image</span></span>           | <span data-ttu-id="e48f9-113">**Windows Server 2016 Datacenter**</span><span class="sxs-lookup"><span data-stu-id="e48f9-113">**Windows Server 2016 Datacenter**</span></span> |
| <span data-ttu-id="e48f9-114">Name</span><span class="sxs-lookup"><span data-stu-id="e48f9-114">Name</span></span>            | <span data-ttu-id="e48f9-115">**fotoshareVM**</span><span class="sxs-lookup"><span data-stu-id="e48f9-115">**fotoshareVM**</span></span> |
| <span data-ttu-id="e48f9-116">Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="e48f9-116">Resource group</span></span>  |   <span data-ttu-id="e48f9-117">**<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>**</span><span class="sxs-lookup"><span data-stu-id="e48f9-117">**<rgn>[Sandbox resource group name]</rgn>**</span></span> |
| <span data-ttu-id="e48f9-118">Speicherort</span><span class="sxs-lookup"><span data-stu-id="e48f9-118">Location</span></span>        | <span data-ttu-id="e48f9-119">Siehe unten.</span><span class="sxs-lookup"><span data-stu-id="e48f9-119">See below.</span></span> |

1. <span data-ttu-id="e48f9-120">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="e48f9-120">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="e48f9-121">Wählen Sie im Menü in der Randleiste **Ressource erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="e48f9-121">Select **Create a resource** in the sidebar menu on the left.</span></span>

1. <span data-ttu-id="e48f9-122">_Windows Server 2016 VM_ befindet sich in der Liste der **beliebten** Marketplace-Elemente.</span><span class="sxs-lookup"><span data-stu-id="e48f9-122">_Windows Server 2016 VM_ should be in the list of **Popular** Marketplace elements.</span></span> <span data-ttu-id="e48f9-123">Wenn dies nicht der Fall ist, suchen Sie über das Suchfeld oben nach „Windows Server 2016 DataCenter“.</span><span class="sxs-lookup"><span data-stu-id="e48f9-123">If not, try searching for "Windows Server 2016 DataCenter" using the search box on the top.</span></span>

1. <span data-ttu-id="e48f9-124">Wählen Sie die Windows-VM, und klicken Sie auf **Erstellen** um den VM-Erstellungsprozesses zu starten.</span><span class="sxs-lookup"><span data-stu-id="e48f9-124">Select the Windows VM and click **Create** to start the VM creation process.</span></span>

1. <span data-ttu-id="e48f9-125">Vergewissern Sie sich im Bereich **Grundlagen**, dass das ausgewählte **Abonnement** _Concierge-Abonnement_ ist.</span><span class="sxs-lookup"><span data-stu-id="e48f9-125">In the **Basics** panel, verify the selected **Subscription** is _Concierge Subscription_.</span></span>

1. <span data-ttu-id="e48f9-126">Wählen Sie unter **Ressourcengruppe** die Option **Vorhandene verwenden** aus, und klicken Sie auf _<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>_.</span><span class="sxs-lookup"><span data-stu-id="e48f9-126">Under **Resource Group**, select **Use Existing** and choose _<rgn>[Sandbox resource group name]</rgn>_.</span></span>

1. <span data-ttu-id="e48f9-127">Geben Sie in **Name der virtuellen Maschine** _fotoshareVM_ ein.</span><span class="sxs-lookup"><span data-stu-id="e48f9-127">In the **Virtual machine name** box, enter _fotoshareVM_.</span></span>

1. <span data-ttu-id="e48f9-128">Wählen Sie in der Dropdownliste **Speicherort** die nächstgelegene Region aus der folgenden Liste.</span><span class="sxs-lookup"><span data-stu-id="e48f9-128">In the **Location** drop-down list, select the closest region to you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="e48f9-129">Der Standard unter **Größe** der VM ist **DS1 v2**. Mit erhalten Sie eine Einzel-CPU und 3,5 GB Speicher.</span><span class="sxs-lookup"><span data-stu-id="e48f9-129">For the VM **Size**, the default is **DS1 v2** which gives you a single CPU and 3.5 GB of memory.</span></span> <span data-ttu-id="e48f9-130">Das reicht für dieses Beispiel.</span><span class="sxs-lookup"><span data-stu-id="e48f9-130">That's fine for this example.</span></span>

1. <span data-ttu-id="e48f9-131">Geben Sie im Abschnitt **ADMINISTRATOR ACCOUNT** einen **Benutzernamen** und **Kennwort** ein, und /**Bestätigen Sie das Kennwort** für ein Administratorkonto auf der neuen VM.</span><span class="sxs-lookup"><span data-stu-id="e48f9-131">In **ADMINISTRATOR ACCOUNT** section, enter a **Username** and **Password**/**Confirm password** for an administrator account on the new VM.</span></span>

1. <span data-ttu-id="e48f9-132">Hier ist ein Beispiel für eine ausgefüllte Konfiguration vom Typ **Grundlagen** angegeben. Behalten Sie die Standardwerte für die verbleibenden Registerkarten und Felder bei, und klicken Sie auf **Überprüfen + Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e48f9-132">The following image is an example of what the **Basics** configuration looks like when filled out. Leave the defaults for the remaining tabs and fields and click **Review + create**.</span></span>

    ![Screenshot des Azure-Portals mit dem Blatt „Erstellen einer virtuellen Maschine“ mit einigen Beispielen für eine ausgefüllte Konfiguration „Grundlagen“.](../media/4-basics-vm.png)

1. <span data-ttu-id="e48f9-134">Nachdem Sie Ihre neuen VM-Einstellungen überprüft haben, klicken Sie auf **Erstellen**, um die Bereitstellung Ihrer neuen VM zu starten.</span><span class="sxs-lookup"><span data-stu-id="e48f9-134">After reviewing your new VM settings, click **Create** to start the deploying your new VM.</span></span>

<span data-ttu-id="e48f9-135">Die VM-Erstellung kann einige Minuten dauern, da alle verschiedenen Ressourcen (Speicher, Netzwerkschnittstelle usw.) zur Unterstützung der virtuellen Maschine erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="e48f9-135">VM creation can take a few minutes as it creates all the various resources (storage, network interface, etc.) to support the virtual machine.</span></span> <span data-ttu-id="e48f9-136">Warten Sie, bis die virtuelle Maschine bereitgestellt wurde, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="e48f9-136">Wait until the VM has deployed before continuing with the exercise.</span></span>

## <a name="view-os-disk-cache-status-in-the-portal"></a><span data-ttu-id="e48f9-137">Anzeigen des Betriebssystemdatenträger-Cachestatus im Portal</span><span class="sxs-lookup"><span data-stu-id="e48f9-137">View OS disk cache status in the portal</span></span>

<span data-ttu-id="e48f9-138">Nachdem unsere VM bereitgestellt wurde, können wir den Cachestatus des Betriebssystemdatenträgers mit den folgenden Schritten bestätigen:</span><span class="sxs-lookup"><span data-stu-id="e48f9-138">Once our VM is deployed, we can confirm the caching status of the OS disk using the following steps:</span></span>

1. <span data-ttu-id="e48f9-139">Wählen Sie die **fotoshareVM**-Ressource, um die VM-Details im Portal zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="e48f9-139">Select the **fotoshareVM** resource to open the VM details in the portal.</span></span> <span data-ttu-id="e48f9-140">Sie können auch in der linken Randleiste auf **Alle Ressourcen** klicken und dann die VM **fotoshareVM** auswählen.</span><span class="sxs-lookup"><span data-stu-id="e48f9-140">Alternatively, you can click **All resources** in the left sidebar, and then select your VM, **fotoshareVM**.</span></span>

1. <span data-ttu-id="e48f9-141">Wählen Sie unter **Einstellungen** die Option **Datenträger** aus.</span><span class="sxs-lookup"><span data-stu-id="e48f9-141">Under **Settings**, select **Disks**.</span></span>

1. <span data-ttu-id="e48f9-142">Im Bereich **Datenträger** verfügt die virtuelle Maschine über einen Datenträger, nämlich den Betriebssystemdatenträger.</span><span class="sxs-lookup"><span data-stu-id="e48f9-142">On the **Disks** pane, the VM has one disk, the OS disk.</span></span> <span data-ttu-id="e48f9-143">Der Cachetyp ist derzeit auf den Standardwert **Lesen/Schreiben** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e48f9-143">Its cache type is currently set to the default value of **Read/write**.</span></span>

![Screenshot des Azure-Portals mit dem Abschnitt „Datenträger“ eines VM-Blatts, wobei der BS-Datenträger angezeigt und die schreibgeschützte Zwischenspeicherung aktiviert ist.](../media/4-os-disk-rw.PNG)

## <a name="change-the-cache-settings-of-the-os-disk-in-the-portal"></a><span data-ttu-id="e48f9-145">Ändern der Cacheeinstellungen des Betriebssystemdatenträgers im Portal</span><span class="sxs-lookup"><span data-stu-id="e48f9-145">Change the cache settings of the OS disk in the portal</span></span>

1. <span data-ttu-id="e48f9-146">Wählen Sie im Bereich **Datenträger** oben links die Option **Bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="e48f9-146">On the **Disks** pane, select **Edit** in the upper left of the screen.</span></span>

1. <span data-ttu-id="e48f9-147">Ändern Sie den Wert **HOSTZWISCHENSPEICHERUNG** für den Betriebssystemdatenträger in **Schreibgeschützt**, indem Sie die Dropdownliste verwenden, und wählen Sie dann oben links die Option **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="e48f9-147">Change the **HOST CACHING** value for the OS disk to **Read-only** using the drop-down list, and then select **Save** in the upper left of the screen.</span></span>

1. <span data-ttu-id="e48f9-148">Dieses Update kann einige Zeit in Anspruch nehmen.</span><span class="sxs-lookup"><span data-stu-id="e48f9-148">This update can take some time.</span></span> <span data-ttu-id="e48f9-149">Der Grund hierfür ist, dass der Zieldatenträger durch das Ändern der Cacheeinstellung eines Azure-Datenträgers getrennt und dann erneut angefügt wird.</span><span class="sxs-lookup"><span data-stu-id="e48f9-149">The reason is that changing the cache setting of an Azure disk detaches and reattaches the target disk.</span></span> <span data-ttu-id="e48f9-150">Wenn es sich um den Betriebssystemdatenträger handelt, wird auch die virtuelle Maschine neu gestartet.</span><span class="sxs-lookup"><span data-stu-id="e48f9-150">If it's the operating system disk, the VM is also restarted.</span></span> <span data-ttu-id="e48f9-151">Wenn der Vorgang abgeschlossen ist, erhalten Sie eine Benachrichtigung, dass die VM-Datenträger aktualisiert wurden.</span><span class="sxs-lookup"><span data-stu-id="e48f9-151">When the operation completes, you'll get a notification saying the VM disks have been updated.</span></span>

1. <span data-ttu-id="e48f9-152">Wenn der Vorgang abgeschlossen ist, ist der Cachetyp des Betriebssystemdatenträgers auf **Schreibgeschützt** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e48f9-152">Once complete, the OS disk cache type is set to **Read-only**.</span></span>

<span data-ttu-id="e48f9-153">Als Nächstes führen wir die Konfiguration des Caches für den für Daten bestimmten Datenträger durch.</span><span class="sxs-lookup"><span data-stu-id="e48f9-153">Let's move on to data disk cache configuration.</span></span> <span data-ttu-id="e48f9-154">Wir müssen zunächst einen Datenträger erstellen, um ihn konfigurieren zu können.</span><span class="sxs-lookup"><span data-stu-id="e48f9-154">To configure a disk, we'll need first to create one.</span></span>

## <a name="add-a-data-disk-to-the-vm-and-set-caching-type"></a><span data-ttu-id="e48f9-155">Hinzufügen eines Datenträgers zur virtuellen Maschine und Festlegen des Cachetyps</span><span class="sxs-lookup"><span data-stu-id="e48f9-155">Add a data disk to the VM and set caching type</span></span>

1. <span data-ttu-id="e48f9-156">In der Ansicht **Datenträger** unserer VM im Portal können Sie jetzt die auf die Option **Datenträger hinzufügen** klicken.</span><span class="sxs-lookup"><span data-stu-id="e48f9-156">Back on the **Disks** view of our VM in the portal, go ahead and click **Add data disk**.</span></span> <span data-ttu-id="e48f9-157">Im Feld **Name** wird sofort ein Fehler mit dem Hinweis angezeigt, dass das Feld nicht leer sein darf.</span><span class="sxs-lookup"><span data-stu-id="e48f9-157">An error immediately appears in the **Name** field, telling us that the field can't be empty.</span></span> <span data-ttu-id="e48f9-158">Da wir noch nicht über einen Datenträger für Daten verfügen, erstellen wir ihn jetzt.</span><span class="sxs-lookup"><span data-stu-id="e48f9-158">We don't have a data disk yet, so let's create one.</span></span>

1. <span data-ttu-id="e48f9-159">Klicken Sie in die Liste **Namen** und dann auf **Datenträger erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e48f9-159">Click in the **Name** list, and then click **Create disk**.</span></span>

1. <span data-ttu-id="e48f9-160">Geben Sie im Bereich **Verwalteten Datenträger erstellen** im Feld **Name** den Namen **fotoshareVM-data** ein.</span><span class="sxs-lookup"><span data-stu-id="e48f9-160">In the **Create managed disk** pane, in the **Name** box, type **fotosharesVM-data**.</span></span>

1. <span data-ttu-id="e48f9-161">Wählen Sie unter **Ressourcengruppe** zuerst **Vorhandene verwenden** und anschließend _<rgn>[Sandbox-Ressourcengruppenname]</rgn>_ aus.</span><span class="sxs-lookup"><span data-stu-id="e48f9-161">Under **Resource Group**, select **Use existing**, and select _<rgn>[Sandbox resource group name]</rgn>_.</span></span>

1. <span data-ttu-id="e48f9-162">Notieren Sie die Standardwerte für die verbleibenden Felder:</span><span class="sxs-lookup"><span data-stu-id="e48f9-162">Note the defaults for the remaining fields:</span></span>
    - <span data-ttu-id="e48f9-163">SSD Premium</span><span class="sxs-lookup"><span data-stu-id="e48f9-163">Premium SSD</span></span>
    - <span data-ttu-id="e48f9-164">Größe von 1.023 GB</span><span class="sxs-lookup"><span data-stu-id="e48f9-164">1023 GB in size</span></span>
    - <span data-ttu-id="e48f9-165">Am gleichen Speicherort wie die VM (kann nicht geändert werden).</span><span class="sxs-lookup"><span data-stu-id="e48f9-165">In the same location as the VM (not changeable).</span></span>
    - <span data-ttu-id="e48f9-166">IOPS-Grenzwert – 5.000</span><span class="sxs-lookup"><span data-stu-id="e48f9-166">IOPS limit - 5000</span></span>
    - <span data-ttu-id="e48f9-167">Durchsatzbegrenzung (MB/s) – 200</span><span class="sxs-lookup"><span data-stu-id="e48f9-167">Throughput limit (MB/s) - 200</span></span>

1. <span data-ttu-id="e48f9-168">Klicken Sie am unteren Rand des Bildschirms auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e48f9-168">Click **Create** at the bottom of the screen.</span></span> 

    <span data-ttu-id="e48f9-169">Warten Sie, bis der Datenträger erstellt wurde, bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="e48f9-169">Wait until the disk has been created before continuing.</span></span>

1. <span data-ttu-id="e48f9-170">Ändern Sie den Wert **HOSTZWISCHENSPEICHERUNG** für den neuen Datenträger in **Schreibgeschützt**, indem Sie die Dropdownliste verwenden (ist ggf schon festgelegt), und klicken Sie dann oben links auf die Option **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="e48f9-170">Change the **HOST CACHING** value for our new data disk to **Read-only** using the drop-down list (it might be set already), and then click **Save** in the upper left of the screen.</span></span>

    <span data-ttu-id="e48f9-171">Warten Sie, bis die VM den neuen Datenträger aktualisiert hat.</span><span class="sxs-lookup"><span data-stu-id="e48f9-171">Wait for the VM to finish updating the new data disk.</span></span> <span data-ttu-id="e48f9-172">Nach Abschluss des Vorgangs haben Sie einen neuen Datenträger auf Ihrer virtuellen Maschine.</span><span class="sxs-lookup"><span data-stu-id="e48f9-172">Once complete, you will have a new data disk on your virtual machine.</span></span>

<span data-ttu-id="e48f9-173">In dieser Übung haben wir das Azure-Portal verwendet, um die Zwischenspeicherung auf einer neuen virtuellen Maschine zu konfigurieren, die Cacheeinstellungen auf einem vorhandenen Datenträger zu ändern und die Zwischenspeicherung auf einem neuen Datenträger zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="e48f9-173">In this exercise, we used the Azure portal to configure caching on a new VM, change cache settings on an existing disk, and configure caching on a new data disk.</span></span> <span data-ttu-id="e48f9-174">Im folgenden Screenshot ist die endgültige Konfiguration dargestellt:</span><span class="sxs-lookup"><span data-stu-id="e48f9-174">The following screenshot shows the final configuration:</span></span>

![Screenshot des Azure-Portals mit dem BS-Datenträger und dem neuen Datenträger im Abschnitt „Datenträger“ auf dem Blatt „VM“, wobei für beide Datenträger die schreibgeschützte Zwischenspeicherung aktiviert ist.](../media/disks-final-config-portal.PNG)
