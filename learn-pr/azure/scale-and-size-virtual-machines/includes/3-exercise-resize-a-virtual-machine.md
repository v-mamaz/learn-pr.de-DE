<span data-ttu-id="de253-101">In dieser Übung erstellen Sie einen virtuellen Computer und ändern seine Größe. Dazu verwenden Sie das Portal und Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de253-101">In this exercise, you will create a virtual machine and then resize it using the portal and Azure PowerShell.</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="de253-102">Erstellen eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="de253-102">Create a VM</span></span>

1. <span data-ttu-id="de253-103">Navigieren Sie in Ihrem Webbrowser zum [Azure-Portal](https://portal.azure.com?azure-portal=true), und melden Sie sich bei Ihrem Konto an.</span><span class="sxs-lookup"><span data-stu-id="de253-103">In your web browser, navigate to the [Azure Portal](https://portal.azure.com?azure-portal=true) and sign into your account.</span></span>

1. <span data-ttu-id="de253-104">Erstellen Sie im Azure-Portal eine neue Ressource.</span><span class="sxs-lookup"><span data-stu-id="de253-104">In the Azure portal, create a new resource.</span></span> <span data-ttu-id="de253-105">Geben Sie auf dem Blatt **Neu** die Zeichenfolge **virtueller Computer** in das Suchfeld ein, und drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="de253-105">In the **New** blade, type **virtual machine** in the search box, and then press ENTER.</span></span>

1. <span data-ttu-id="de253-106">Klicken Sie auf dem Blatt **Alles** unter **Ergebnisse** auf **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="de253-106">In the **Everything** blade, under **Results**, click **Windows Server 2016 Datacenter**.</span></span>

1. <span data-ttu-id="de253-107">Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="de253-107">In the **Windows Server 2016 Datacenter** blade, click **Create**.</span></span>

1. <span data-ttu-id="de253-108">Geben Sie auf dem Blatt **Grundlagen** die folgenden Informationen ein, und klicken Sie anschließend auf **OK**:</span><span class="sxs-lookup"><span data-stu-id="de253-108">In the **Basics** blade, complete the details using the following information, and then click **OK**.</span></span>

    |<span data-ttu-id="de253-109">Einstellung</span><span class="sxs-lookup"><span data-stu-id="de253-109">Setting</span></span>|<span data-ttu-id="de253-110">Wert</span><span class="sxs-lookup"><span data-stu-id="de253-110">Value</span></span>|
    |---|---|
    |<span data-ttu-id="de253-111">Name</span><span class="sxs-lookup"><span data-stu-id="de253-111">Name</span></span>|<span data-ttu-id="de253-112">DB01</span><span class="sxs-lookup"><span data-stu-id="de253-112">DB01</span></span>|
    |<span data-ttu-id="de253-113">Benutzername</span><span class="sxs-lookup"><span data-stu-id="de253-113">Username</span></span>|<span data-ttu-id="de253-114">LocalAdmin</span><span class="sxs-lookup"><span data-stu-id="de253-114">LocalAdmin</span></span>|
    |<span data-ttu-id="de253-115">Kennwort und Kennwortbestätigung</span><span class="sxs-lookup"><span data-stu-id="de253-115">Password and Confirm password</span></span>|<span data-ttu-id="de253-116">Adm1nPa$$word</span><span class="sxs-lookup"><span data-stu-id="de253-116">Adm1nPa$$word</span></span>|
    |<span data-ttu-id="de253-117">Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="de253-117">Resource group</span></span>|<span data-ttu-id="de253-118">ExerciseRG</span><span class="sxs-lookup"><span data-stu-id="de253-118">ExerciseRG</span></span>|
    |<span data-ttu-id="de253-119">Standort</span><span class="sxs-lookup"><span data-stu-id="de253-119">Location</span></span>|<span data-ttu-id="de253-120">USA, Mitte</span><span class="sxs-lookup"><span data-stu-id="de253-120">Central US</span></span>|

1. <span data-ttu-id="de253-121">Wählen Sie auf dem Blatt **Größe auswählen** die Option **D2s_v3** aus, und klicken Sie anschließend auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="de253-121">On the **Choose a size** blade, select **D2s_v3**, and then click **Select**.</span></span>

1. <span data-ttu-id="de253-122">Wählen Sie auf dem Blatt **Einstellungen** unter **Öffentliche Eingangsports hinzufügen** die Optionen **HTTP**, **HTTPS** und **RDP (3389)** aus, klicken Sie unter **Startdiagnose** auf **Deaktiviert**, behalten Sie bei allen anderen Einstellungen die Standardwerte bei, und klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="de253-122">On the **Settings** blade, under **Select public inbound ports** select **HTTP**, **HTTPS**, and **RDP (3389)**, under **Boot diagnostics** click **Disabled**, leave all other settings at the default value, and then click **OK**.</span></span>

1. <span data-ttu-id="de253-123">Klicken Sie auf dem Blatt **Erstellen** auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="de253-123">On the **Create** blade, click **Create**.</span></span>

1. <span data-ttu-id="de253-124">Warten Sie, bis die Bereitstellung abgeschlossen ist, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="de253-124">Wait until the deployment is complete before continuing the exercise.</span></span>

## <a name="resize-using-the-portal"></a><span data-ttu-id="de253-125">Ändern der Größe über das Portal</span><span class="sxs-lookup"><span data-stu-id="de253-125">Resize using the portal</span></span>

1. <span data-ttu-id="de253-126">Navigieren Sie im Azure-Portal zur Ressourcengruppe „ExerciseRG“, und klicken Sie auf dem Blatt **ExerciseRG** auf das VM-Objekt **DB01**.</span><span class="sxs-lookup"><span data-stu-id="de253-126">In the Azure portal, browse to the ExerciseRG resource group, and in the **ExerciseRG** blade, click the **DB01** virtual machine object.</span></span>

1. <span data-ttu-id="de253-127">Klicken Sie auf dem Blatt **DB01** auf **Größe**.</span><span class="sxs-lookup"><span data-stu-id="de253-127">On the **DB01** blade, click **Size**.</span></span> <span data-ttu-id="de253-128">Hinweis: Die aktuell hervorgehobene Größe ist die Größe, die Sie beim Erstellen des virtuellen Computers ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="de253-128">Note the currently highlighted size is the size you selected when creating the virtual machine.</span></span>

1. <span data-ttu-id="de253-129">Suchen Sie auf dem Blatt **Größe auswählen** nach der Größe **F2s_v2**. Sie sollte in der Größenliste nicht verfügbar sein, da der virtuelle Computer momentan ausgeführt wird und die Größe zu einer anderen Familie gehört.</span><span class="sxs-lookup"><span data-stu-id="de253-129">On the **Choose a size** blade, try to find the **F2s_v2** size - it should not be available in the list of sizes because the VM is currently running and that size is from a different family.</span></span> <span data-ttu-id="de253-130">Schließen Sie das Blatt **Größe auswählen**.</span><span class="sxs-lookup"><span data-stu-id="de253-130">Close the **Choose a size** blade.</span></span>

1. <span data-ttu-id="de253-131">Klicken Sie auf dem Blatt **DB01** auf **Beenden**.</span><span class="sxs-lookup"><span data-stu-id="de253-131">In the **DB01** blade, click **Stop**.</span></span> <span data-ttu-id="de253-132">Klicken Sie im Dialogfeld zum **Beenden des virtuellen Computers**auf **Ja**, und warten Sie, bis der virtuelle Computer den Status **Beendet (Zuordnung aufgehoben)** hat.</span><span class="sxs-lookup"><span data-stu-id="de253-132">In the **Stop this virtual machine** dialog box, click **Yes**, and wait for the virtual machine status to show **Stopped (deallocated)**.</span></span>

1. <span data-ttu-id="de253-133">Klicken Sie auf dem Blatt **DB01** auf **Größe**.</span><span class="sxs-lookup"><span data-stu-id="de253-133">On the **DB01** blade, click **Size**.</span></span> <span data-ttu-id="de253-134">Wählen Sie auf dem Blatt **Größe auswählen** die Option **F2s_v2** aus, und klicken Sie anschließend auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="de253-134">On the **Choose a size** blade, select **F2s_v2** and then click **Select**.</span></span> <span data-ttu-id="de253-135">Beachten Sie die Benachrichtigung zur Größenänderung für den virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="de253-135">Notice the notification about resizing the virtual machine.</span></span>

1. <span data-ttu-id="de253-136">Klicken Sie auf dem Blatt **DB01** auf **Übersicht** und anschließend auf **Starten**.</span><span class="sxs-lookup"><span data-stu-id="de253-136">On the **DB01** blade, click **Overview**, then click **Start**.</span></span>

## <a name="resize-using-powershell"></a><span data-ttu-id="de253-137">Ändern der Größe mithilfe von PowerShell</span><span class="sxs-lookup"><span data-stu-id="de253-137">Resize using PowerShell</span></span>

1. <span data-ttu-id="de253-138">Öffnen Sie Cloud Shell im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="de253-138">In the Azure portal, open the Cloud Shell.</span></span>

1. <span data-ttu-id="de253-139">Verwenden Sie das folgende Cmdlet, um die Liste mit den verfügbaren VM-Größen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="de253-139">Use the following cmdlet to get the list of available virtual machine sizes.</span></span>

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName ExerciseRG -VMName DB01
    ```

1. <span data-ttu-id="de253-140">Verwenden Sie das folgende Cmdlet, um die Größe des virtuellen Computers in „F4s_v2“ zu ändern.</span><span class="sxs-lookup"><span data-stu-id="de253-140">Use the following cmdlet to resize the virtual machine to an F4s_v2 size.</span></span>

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName ExerciseRG -VMName DB01
    $vm.HardwareProfile.VmSize = "Standard_F4s_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName ExerciseRG
    ```

1. <span data-ttu-id="de253-141">Klicken Sie auf dem Blatt „DB01“ auf die Schaltfläche „Aktualisieren“, während Sie darauf warten, dass die Ausführung des PowerShell-Befehls abgeschlossen wird. Sie sollten sehen, dass der virtuelle Computer neu gestartet wird, um die Größenänderung zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="de253-141">Click the Refresh button in the DB01 blade while you are waiting for the PowerShell command to complete - you should notice that the virtual machine is restarting to accommodate the change in size.</span></span>

<span data-ttu-id="de253-142">In dieser Übung haben Sie einen virtuellen Computer erstellt und seine Größe mit zwei verschiedenen Tools geändert.</span><span class="sxs-lookup"><span data-stu-id="de253-142">In this exercise, you created a virtual machine and resized it with two different tools.</span></span> <span data-ttu-id="de253-143">Tipp: Denken Sie daran, dass die Zielgröße möglicherweise nicht verfügbar ist, solange der virtuelle Computer ausgeführt wird. Nach Beendigung des virtuellen Computers stehen mehr Größen zur Auswahl.</span><span class="sxs-lookup"><span data-stu-id="de253-143">A good tip to keep in mind is that the target size may not be available while the virtual machine is running; stopping the virtual machine lets you choose more sizes.</span></span>