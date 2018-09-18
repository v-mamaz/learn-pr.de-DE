<span data-ttu-id="30a50-101">Angenommen, Sie betreiben eine Website zum Teilen von Fotos, bei der Daten auf virtuellen Azure-Computern (VMs) mit SQL Server und benutzerdefinierten Anwendungen gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="30a50-101">Suppose you run a photo sharing site, with data stored on Azure virtual machines (VMs) running SQL Server and custom applications.</span></span> <span data-ttu-id="30a50-102">Sie möchten die folgenden Anpassungen vornehmen.</span><span class="sxs-lookup"><span data-stu-id="30a50-102">You want to make the following adjustments.</span></span>

- <span data-ttu-id="30a50-103">Ändern der Einstellungen für den Datenträgercache auf einer VM</span><span class="sxs-lookup"><span data-stu-id="30a50-103">You need change the disk cache settings on a VM</span></span>
- <span data-ttu-id="30a50-104">Hinzufügen eines neuen Datenträgers für Daten zur VM mit aktivierter Zwischenspeicherung</span><span class="sxs-lookup"><span data-stu-id="30a50-104">You want dd a new data disk to the VM with caching enabled</span></span>

<span data-ttu-id="30a50-105">Sie haben sich dafür entschieden, diese Änderungen über das Azure-Portal vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="30a50-105">You've decided to make these changes through the Azure portal.</span></span>

<span data-ttu-id="30a50-106">In dieser Übung wird Schritt für Schritt erklärt, wie Sie die Änderungen an einer VM vornehmen, die oben beschrieben wurde.</span><span class="sxs-lookup"><span data-stu-id="30a50-106">In this exercise, we'll walk through making the changes to a VM that we described above.</span></span> <span data-ttu-id="30a50-107">Zuerst melden Sie sich am Portal an und erstellen eine VM.</span><span class="sxs-lookup"><span data-stu-id="30a50-107">First, let's sign in to the portal and create a VM.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="30a50-108">Anmelden am Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="30a50-108">Sign in to the Azure portal</span></span>
<!---TODO: Update for sandbox?--->

1. <span data-ttu-id="30a50-109">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="30a50-109">Sign in to the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="30a50-110">Erstellen eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="30a50-110">Create a virtual machine</span></span>

<span data-ttu-id="30a50-111">In diesem Schritt erstellen wir eine VM mit den folgenden Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="30a50-111">In this step, we're going to create a VM with the following properties.</span></span>

|<span data-ttu-id="30a50-112">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="30a50-112">Property</span></span>  |<span data-ttu-id="30a50-113">Wert</span><span class="sxs-lookup"><span data-stu-id="30a50-113">Value</span></span>  |
|---------|---------|
|<span data-ttu-id="30a50-114">Image</span><span class="sxs-lookup"><span data-stu-id="30a50-114">Image</span></span>     |   <span data-ttu-id="30a50-115">**Windows Server 2016 Datacenter**</span><span class="sxs-lookup"><span data-stu-id="30a50-115">**Windows Server 2016 Datacenter**</span></span>      |
|<span data-ttu-id="30a50-116">Name</span><span class="sxs-lookup"><span data-stu-id="30a50-116">Name</span></span>     |   <span data-ttu-id="30a50-117">**fotoshareVM**</span><span class="sxs-lookup"><span data-stu-id="30a50-117">**fotoshareVM**</span></span>     |
|<span data-ttu-id="30a50-118">Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="30a50-118">Resource group</span></span>     |   <span data-ttu-id="30a50-119">**fotoshare-rg**</span><span class="sxs-lookup"><span data-stu-id="30a50-119">**fotoshare-rg**</span></span>      |


1. <span data-ttu-id="30a50-120">Wählen Sie im linken Menü des Portals die Option **Virtuelle Computer**.</span><span class="sxs-lookup"><span data-stu-id="30a50-120">In the left menu of the portal, select **Virtual machines**</span></span>

1. <span data-ttu-id="30a50-121">Wählen Sie anschließend oben links auf dem Bildschirm **Virtuelle Computer** die Option **+ Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="30a50-121">Now select **+ Add** in the top left of the **Virtual machines** screen.</span></span> <span data-ttu-id="30a50-122">Mit dieser Aktion wird der Erstellungsvorgang gestartet.</span><span class="sxs-lookup"><span data-stu-id="30a50-122">This action starts the creation process.</span></span>

1. <span data-ttu-id="30a50-123">Geben Sie im Panel „Compute“, in dem die verfügbaren VM-Images aufgeführt sind, im Suchfeld *Windows Server 2016 Datacenter* ein.</span><span class="sxs-lookup"><span data-stu-id="30a50-123">On the Compute panel that lists available VM images, type *Windows Server 2016 Datacenter* into the search box.</span></span>

1. <span data-ttu-id="30a50-124">Wählen Sie in den Suchergebnissen den Eintrag **Windows Server 2016 Datacenter** und dann die Option **Erstellen**, um den Prozess für die VM-Erstellung zu starten.</span><span class="sxs-lookup"><span data-stu-id="30a50-124">Select **Windows Server 2016 Datacenter** from the search results and then select **Create** to start the VM creation process.</span></span>

1. <span data-ttu-id="30a50-125">Geben Sie im Panel **Grundlagen** im Feld **Name** den Namen **fotoshareVM** ein.</span><span class="sxs-lookup"><span data-stu-id="30a50-125">In the **Basics** panel, in the **Name** box, enter **fotoshareVM**</span></span>

1. <span data-ttu-id="30a50-126">Geben Sie in den Feldern **Benutzername** und **Kennwort** einen Namen und ein Kennwort für ein Administratorkonto auf diesem Server ein.</span><span class="sxs-lookup"><span data-stu-id="30a50-126">In the **Username** and **Password boxes**, enter a name and password for an administrator account on this server.</span></span>

1. <span data-ttu-id="30a50-127">Wählen Sie in der Dropdownliste **Abonnement** Ihr Azure-Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="30a50-127">In the **Subscription** dropdown, select your Azure subscription.</span></span>

1. <span data-ttu-id="30a50-128">Wählen Sie unter **Ressourcengruppe** die Option **Neu erstellen**, und geben Sie im Feld den Namen **fotoshare-rg** ein.</span><span class="sxs-lookup"><span data-stu-id="30a50-128">Under **Resource Group**, select **Create new**, and in the box, type **fotoshare-rg**.</span></span>

1. <span data-ttu-id="30a50-129">Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="30a50-129">In the **Location** drop-down list, select a region near you.</span></span>

<span data-ttu-id="30a50-130">Hier ist ein Beispiel für eine ausgefüllte Konfiguration vom Typ **Grundlagen** angegeben.</span><span class="sxs-lookup"><span data-stu-id="30a50-130">The following is an example of what the **Basics** configuration looks like when filled out.</span></span>

![Screenshot: Ausgefüllte Konfiguration „Grundlagen“](../media-draft/vm-basics-settings.PNG)

1. <span data-ttu-id="30a50-132">Wählen Sie **OK**, um mit dem nächsten Schritt fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="30a50-132">Select **OK** to move onto the next step.</span></span>

<span data-ttu-id="30a50-133">Als Nächstes wählen Sie eine Größe für die VM aus und starten die Bereitstellung:</span><span class="sxs-lookup"><span data-stu-id="30a50-133">You now need to choose a size for the VM, and then start the deployment:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30a50-134">Beachten Sie hierbei, dass die Datenträgerzwischenspeicherung für virtuelle Computer der L- und B-Serie nicht geändert werden kann.</span><span class="sxs-lookup"><span data-stu-id="30a50-134">Remember that disk caching can't be changed for L-Series and B-series virtual machines.</span></span> <span data-ttu-id="30a50-135">Wir wählen eine andere Größe.</span><span class="sxs-lookup"><span data-stu-id="30a50-135">We'll select a different size.</span></span>

1. <span data-ttu-id="30a50-136">Wählen Sie im Abschnitt **Größe auswählen** die SKU vom Typ **Standard** aus, z.B. **F1s**, und wählen Sie anschließend die Option **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="30a50-136">In the **Choose a size** section, select a **Standard** SKU, such as **F1s**, and then choose **Select**.</span></span>

1. <span data-ttu-id="30a50-137">Scrollen Sie im Bereich **Einstellungen** nach unten. Sie sehen, dass keine Option zum Konfigurieren der Datenträgerzwischenspeicherung vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="30a50-137">Scroll down the **Settings** pane and observe that there is no option to configure disk caching.</span></span> <span data-ttu-id="30a50-138">Akzeptieren Sie in diesem Schritt die Standardeinstellungen, und wählen Sie unten im Bereich **OK**.</span><span class="sxs-lookup"><span data-stu-id="30a50-138">Let's accept the defaults on this step and choose **OK** at the bottom of the pane.</span></span>

1. <span data-ttu-id="30a50-139">Sehen Sie sich im Panel **Erstellen** die Übersicht an, und wählen Sie anschließend die Option **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="30a50-139">On the **Create** panel, review the summary, and then choose **Create**.</span></span>

1. <span data-ttu-id="30a50-140">Die VM-Erstellung kann ein Weile dauern.</span><span class="sxs-lookup"><span data-stu-id="30a50-140">VM creation can take a while.</span></span> <span data-ttu-id="30a50-141">Warten Sie die Bereitstellung des virtuellen Computers ab, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="30a50-141">Wait until the VM has deployed before continuing with the exercise.</span></span> <span data-ttu-id="30a50-142">Sie erhalten im Notification Hub eine Nachricht, wenn der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="30a50-142">You'll get a message in the Notification hub when the process is complete.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30a50-143">Da wir diesen virtuellen Computer in der nächsten Lektion verwenden, sollten Sie ihn vorerst beibehalten.</span><span class="sxs-lookup"><span data-stu-id="30a50-143">We'll use this VM in the next lesson, so keep it around for a while!</span></span>

## <a name="view-os-disk-cache-status-in-the-portal"></a><span data-ttu-id="30a50-144">Anzeigen des Betriebssystemdatenträger-Cachestatus im Portal</span><span class="sxs-lookup"><span data-stu-id="30a50-144">View OS disk cache status in the portal</span></span>

<span data-ttu-id="30a50-145">Nachdem unsere VM bereitgestellt wurde, können wir den Cachestatus des Betriebssystemdatenträgers mit den folgenden Schritten bestätigen.</span><span class="sxs-lookup"><span data-stu-id="30a50-145">Once our VM is deployed, we can confirm the caching status of the OS disk using the following steps.</span></span>

1. <span data-ttu-id="30a50-146">Klicken Sie im linken Menü auf **Alle Ressourcen**, und wählen Sie dann die VM **fotoshareVM** aus.</span><span class="sxs-lookup"><span data-stu-id="30a50-146">In the left menu, click **All resources**, and then select your VM,  **fotoshareVM**.</span></span>

1. <span data-ttu-id="30a50-147">Wählen Sie auf dem Bildschirm **Virtueller Computer** unter **EINSTELLUNGEN** die Option **Datenträger**.</span><span class="sxs-lookup"><span data-stu-id="30a50-147">On the **Virtual machine** screen, under **SETTINGS**, select **Disks**.</span></span>

1. <span data-ttu-id="30a50-148">Im Bereich **Datenträger** verfügt der virtuelle Computer über einen Datenträger, nämlich den Betriebssystemdatenträger.</span><span class="sxs-lookup"><span data-stu-id="30a50-148">On the **Disks** pane, the VM has one disk, the OS disk.</span></span> <span data-ttu-id="30a50-149">Der Cachetyp ist derzeit auf den Standardwert **Lesen/Schreiben** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="30a50-149">Its cache type is currently set to the default value of **Read/write**.</span></span>

![Screenshot: Betriebssystemdatenträger und Datenträger, jeweils mit schreibgeschütztem Caching](../media-draft/os-disk-rw.PNG)

## <a name="change-the-cache-settings-of-the-os-disk-in-the-portal"></a><span data-ttu-id="30a50-151">Ändern der Cacheeinstellungen des Betriebssystemdatenträgers im Portal</span><span class="sxs-lookup"><span data-stu-id="30a50-151">Change the cache settings of the OS disk in the portal</span></span>

1. <span data-ttu-id="30a50-152">Wählen Sie im Bereich **Datenträger** oben links die Option **Bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="30a50-152">On the **Disks** pane, select **Edit** in the upper left of the screen.</span></span>

1. <span data-ttu-id="30a50-153">Ändern Sie den Wert **HOSTZWISCHENSPEICHERUNG** für den Betriebssystemdatenträger in **Schreibgeschützt**, indem Sie die Dropdownliste verwenden, und wählen Sie dann oben links die Option **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="30a50-153">Change the **HOST CACHING** value for the OS disk to **Read-only** using the dropdown and then select **Save** in the upper left of the screen.</span></span>

1. <span data-ttu-id="30a50-154">Dieses Update dauert eine Weile.</span><span class="sxs-lookup"><span data-stu-id="30a50-154">This update takes a while.</span></span> <span data-ttu-id="30a50-155">Der Grund hierfür ist, dass der Zieldatenträger durch das Ändern der Cacheeinstellung eines Azure-Datenträgers getrennt und dann erneut angefügt wird.</span><span class="sxs-lookup"><span data-stu-id="30a50-155">The reason is that changing the cache setting of an Azure disk detaches and reattaches the target disk.</span></span> <span data-ttu-id="30a50-156">Wenn es sich um den Betriebssystemdatenträger handelt, wird auch der virtuelle Computer neu gestartet.</span><span class="sxs-lookup"><span data-stu-id="30a50-156">If it's the operating system disk, the VM is also restarted.</span></span> <span data-ttu-id="30a50-157">Wenn das Update abgeschlossen ist, erhalten Sie eine Benachrichtigung, die dem folgenden Beispiel ähnelt.</span><span class="sxs-lookup"><span data-stu-id="30a50-157">You'll get a message similar to the following notification when the update has finished.</span></span>

![Beispiel für eine Benachrichtigung nach Abschluss des Updatevorgangs für die Cacheeinstellung](../media-draft/vm-disk-update-complete.PNG)

4. <span data-ttu-id="30a50-159">Wenn der Vorgang abgeschlossen ist, ist der Cachetyp des Betriebssystemdatenträgers auf **Schreibgeschützt** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="30a50-159">Once complete, the OS disk cache type is set to **Read-only**.</span></span>

<span data-ttu-id="30a50-160">Als Nächstes führen wir die Konfiguration des Caches für den für Daten bestimmten Datenträger durch.</span><span class="sxs-lookup"><span data-stu-id="30a50-160">Let's move on to data disk cache configuration.</span></span> <span data-ttu-id="30a50-161">Wir müssen zunächst einen Datenträger erstellen, um ihn konfigurieren zu können.</span><span class="sxs-lookup"><span data-stu-id="30a50-161">To configure a disk, we'll need to first create one.</span></span>

## <a name="add-a-data-disk-to-the-vm-and-set-caching-type"></a><span data-ttu-id="30a50-162">Hinzufügen eines Datenträgers zum virtuellen Computer und Festlegen des Cachetyps</span><span class="sxs-lookup"><span data-stu-id="30a50-162">Add a data disk to the VM and set caching type</span></span>

1. <span data-ttu-id="30a50-163">In der Ansicht **Datenträger** unserer VM im Portal können Sie jetzt die Option **Datenträger hinzufügen** wählen.</span><span class="sxs-lookup"><span data-stu-id="30a50-163">Back on the **Disks** view of our VM in the portal, go ahead and select **Add data disk**.</span></span> <span data-ttu-id="30a50-164">Im Feld **Name** wird sofort ein Fehler mit dem Hinweis angezeigt, dass das Feld nicht leer sein darf.</span><span class="sxs-lookup"><span data-stu-id="30a50-164">An error immediately appears in the **Name** field telling us that the field can't be empty.</span></span> <span data-ttu-id="30a50-165">Da wir noch nicht über einen Datenträger für Daten verfügen, erstellen wir ihn jetzt.</span><span class="sxs-lookup"><span data-stu-id="30a50-165">We don't have a data disk yet, so let's create one.</span></span>

1. <span data-ttu-id="30a50-166">Klicken Sie in die Liste **Namen** und dann auf **Datenträger erstellen**.</span><span class="sxs-lookup"><span data-stu-id="30a50-166">Click in the **Name** list, and then click **Create disk**.</span></span>

1. <span data-ttu-id="30a50-167">Geben Sie im Bereich **Verwalteten Datenträger erstellen** im Feld **Name** den Namen **fotosharesVM-data** ein.</span><span class="sxs-lookup"><span data-stu-id="30a50-167">In the **Create managed disk** pane, in the **Name** box, type **fotosharesVM-data**.</span></span>

1. <span data-ttu-id="30a50-168">Wählen Sie unter **Ressourcengruppe** die Option **Vorhandene verwenden** und dann im Dropdownmenü die Option **fotoshare-rg**.</span><span class="sxs-lookup"><span data-stu-id="30a50-168">Under **Resource Group**, select **Use existing**, and select **fotoshare-rg** from the dropdown menu.</span></span>

1. <span data-ttu-id="30a50-169">Wählen Sie unten auf dem Bildschirm die Option **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="30a50-169">Select **Create** at the bottom of the screen.</span></span>

1. <span data-ttu-id="30a50-170">Warten Sie, bis der Datenträger erstellt wurde, bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="30a50-170">Wait until the disk has been created before continuing.</span></span>

1. <span data-ttu-id="30a50-171">Ändern Sie den Wert **HOSTZWISCHENSPEICHERUNG** für den neuen Datenträger in **Schreibgeschützt**, indem Sie die Dropdownliste verwenden, und wählen Sie dann oben links die Option **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="30a50-171">Change the **HOST CACHING** value for our new data disk to **Read-only** using the dropdown and then select **Save** in the upper left of the screen.</span></span>

1. <span data-ttu-id="30a50-172">Warten Sie, bis der virtuelle Computer aktualisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="30a50-172">Wait for the VM to update.</span></span> <span data-ttu-id="30a50-173">Die Aktualisierung dauert eine Weile, weil Azure die Zuordnung des Datenträgers aufhebt und ihn dann neu zuordnet, um diese Einstellung zu ändern.</span><span class="sxs-lookup"><span data-stu-id="30a50-173">Updating takes a while because Azure detaches and reattaches the data disk to change this setting.</span></span>

1. <span data-ttu-id="30a50-174">Wenn der Vorgang abgeschlossen ist, ist der Cachetyp des Datenträgers auf **Schreibgeschützt** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="30a50-174">Once complete, the data disk cache type is set to **Read-only**.</span></span>

<span data-ttu-id="30a50-175">In dieser Übung haben wir das Azure-Portal verwendet, um die Zwischenspeicherung auf einem neuen virtuellen Computer zu konfigurieren, die Cacheeinstellungen auf einem vorhandenen Datenträger zu ändern und die Zwischenspeicherung auf einem neuen Datenträger zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="30a50-175">In this exercise, we used the Azure portal to configure caching on a new VM, change cache settings on an existing disk, and to configure caching on a new data disk.</span></span> <span data-ttu-id="30a50-176">Im folgenden Screenshot ist die endgültige Konfiguration dargestellt.</span><span class="sxs-lookup"><span data-stu-id="30a50-176">The following screenshot shows the final configuration.</span></span> 

![Screenshot: Betriebssystemdatenträger und Datenträger, jeweils mit schreibgeschütztem Caching](../media-draft/disks-final-config-portal.PNG)