<span data-ttu-id="eb306-101">In dieser Übung erstellen Sie einen virtuellen Computer und ändern seine Größe. Dazu verwenden Sie das Portal und Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb306-101">In this exercise, you will create a virtual machine and then resize it using the portal and Azure PowerShell.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-vm-with-powershell"></a><span data-ttu-id="eb306-102">Erstellen eines virtuellen Computers mit PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb306-102">Create a VM with PowerShell</span></span>

1. <span data-ttu-id="eb306-103">Verwenden Sie das Cmdlet `New-AzureRmVm` in Azure PowerShell, um einen virtuellen Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="eb306-103">Let's use the `New-AzureRmVm` cmdlet in Azure PowerShell to create a VM.</span></span>
    - <span data-ttu-id="eb306-104">Verwenden Sie die Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.</span><span class="sxs-lookup"><span data-stu-id="eb306-104">Use the Resource Group **<rgn>[sandbox resource group name]</rgn>**.</span></span>
    - <span data-ttu-id="eb306-105">Nennen Sie ihn „my-test-vm“.</span><span class="sxs-lookup"><span data-stu-id="eb306-105">Name it "my-test-vm".</span></span>
    - <span data-ttu-id="eb306-106">Übergeben Sie _Standard_DS2_v2_ für den **Size**-Parameter.</span><span class="sxs-lookup"><span data-stu-id="eb306-106">Pass in _Standard_DS2_v2_ for the **Size** parameter.</span></span>
    - <span data-ttu-id="eb306-107">Wählen Sie in der Azure-Sandbox aus der folgenden Liste einen Standort in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="eb306-107">Select a location close to you from the following list available in the Azure sandbox.</span></span> <span data-ttu-id="eb306-108">Achten Sie darauf, den Wert im folgenden Beispielbefehl zu ändern, wenn Sie ihn kopieren und einfügen.</span><span class="sxs-lookup"><span data-stu-id="eb306-108">Make sure to change the value in the below example command if you are using copy and paste.</span></span>

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - <span data-ttu-id="eb306-109">Verwenden Sie das `Get-Credential`-Cmdlet, und geben Sie die Ergebnisse wie unten gezeigt in den `Credential`-Parameter ein.</span><span class="sxs-lookup"><span data-stu-id="eb306-109">Use the `Get-Credential` cmdlet and feed the results into the `Credential` parameter as shown below.</span></span>

       <span data-ttu-id="eb306-110">Wenn Sie zur Eingabe der Anmeldeinformationen aufgefordert werden, verwenden Sie „LocalAdmin“ als Benutzernamen und „Adm1nPa$$Word“ als Kennwort.</span><span class="sxs-lookup"><span data-stu-id="eb306-110">When prompted to enter credentials, use LocalAdmin as the user name and Adm1nPa$$word as the password.</span></span>

    ```powershell
    New-AzureRmVm `
        -ResourceGroupName <rgn>[sandbox resource group name]</rgn> `
        -Name my-test-vm `
        -Credential (Get-Credential) `
        -Size "Standard_DS2_v2" `
        -Location eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


1. <span data-ttu-id="eb306-111">Warten Sie, bis die Bereitstellung abgeschlossen ist, bevor Sie mit der Übung fortfahren.</span><span class="sxs-lookup"><span data-stu-id="eb306-111">Wait until the deployment is complete before continuing the exercise.</span></span>

## <a name="resize-using-the-portal"></a><span data-ttu-id="eb306-112">Ändern der Größe über das Portal</span><span class="sxs-lookup"><span data-stu-id="eb306-112">Resize using the portal</span></span>

1. <span data-ttu-id="eb306-113">Melden Sie sich beim [Azure-Portal für die Sandbox](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit demselben Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="eb306-113">Sign into the [Azure portal for sandbox](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="eb306-114">Wählen Sie in der linken Seitenleiste **Ressourcengruppen** aus.</span><span class="sxs-lookup"><span data-stu-id="eb306-114">Select **Resource Groups** from the left side bar.</span></span>

1. <span data-ttu-id="eb306-115">Wählen Sie die Ressourcengruppe <rgn>[Name der Sandboxressourcengruppe]</rgn> aus, und klicken Sie in der Übersicht auf das virtuelle Computerobjekt **my-test-vm**.</span><span class="sxs-lookup"><span data-stu-id="eb306-115">Select the <rgn>[sandbox resource group name]</rgn> resource group, and in the overview, click the **my-test-vm** virtual machine object.</span></span>

1. <span data-ttu-id="eb306-116">Beachten Sie in der **Übersicht** des virtuellen Computers, dass die aktuelle Größe der VM _Standard DS2 v2 (2 vCPUs, 7 GB Arbeitsspeicher)_ entspricht. Dabei handelt es sich um die VM, die Sie vorhin erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="eb306-116">On the **Overview** of the virtual machine, notice that the current size of the VM is _Standard DS2 v2 (2 vcpus, 7 GB memory)_ which is what we created a moment ago.</span></span>

1. <span data-ttu-id="eb306-117">Klicken Sie im Abschnitt **Einstellungen** auf die Option **Größe**.</span><span class="sxs-lookup"><span data-stu-id="eb306-117">In the **Settings** section, select **Size**.</span></span>

1. <span data-ttu-id="eb306-118">Suchen Sie auf dem Blatt **Größe auswählen** nach der Größe **F2s_v2**.</span><span class="sxs-lookup"><span data-stu-id="eb306-118">On the **Choose a size** blade, try to find the **F2s_v2** size.</span></span> <span data-ttu-id="eb306-119">Sie werden sie nicht in der Liste der verfügbaren Größen finden, da die VM derzeit ausgeführt wird und die Größe aus einer anderen Familie stammt.</span><span class="sxs-lookup"><span data-stu-id="eb306-119">You will not see it in the list of available sizes because the VM is currently running and that size is from a different family.</span></span> <span data-ttu-id="eb306-120">In einigen Fällen müssen Sie die VM beenden, um alle verfügbaren VM-Größen anzeigen zu können.</span><span class="sxs-lookup"><span data-stu-id="eb306-120">In some cases, you will need to stop the VM in order to see all available VM sizes.</span></span>

1. <span data-ttu-id="eb306-121">Wählen Sie eine Größe aus, die verfügbar ist, während dieser virtuelle Computer ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="eb306-121">Let's choose a size that is currently available while this VM is running.</span></span> <span data-ttu-id="eb306-122">Wählen Sie auf dem Blatt **Größe auswählen** die Option _DS3_v2 Standard_ aus, und klicken Sie anschließend auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="eb306-122">While still on the **Choose a size** blade, select _DS3_v2 Standard_ and then click **Select**.</span></span> <span data-ttu-id="eb306-123">Beachten Sie die Benachrichtigung zur Größenänderung für den virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="eb306-123">Notice the notification about resizing the virtual machine.</span></span>

1. <span data-ttu-id="eb306-124">Bestätigen Sie auf dem Panel **Übersicht**, dass die Größe der VM in _Standard DS3 v2 (4 vCPUs, 14 GB Arbeitsspeicher)_ geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="eb306-124">On the **Overview** panel, confirm that the VM has been resized to _Standard DS3 v2 (4 vcpus, 14 GB memory)_.</span></span>

## <a name="resize-using-powershell"></a><span data-ttu-id="eb306-125">Ändern der Größe mithilfe von PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb306-125">Resize using PowerShell</span></span>

1. <span data-ttu-id="eb306-126">Öffnen Sie im Azure-Portal Azure Cloud Shell, indem Sie auf die Cloud Shell-Schaltfläche in der oberen Symbolleiste klicken.</span><span class="sxs-lookup"><span data-stu-id="eb306-126">In the Azure portal, open Azure Cloud Shell by clicking the Cloud Shell button in the top toolbar.</span></span>

    <span data-ttu-id="eb306-127">Stellen Sie oben links im Cloud Shell-Fenster sicher, dass die Cloud Shell automatisch PowerShell verwendet, nicht Bash.</span><span class="sxs-lookup"><span data-stu-id="eb306-127">Ensure that the Cloud Shell is set to use PowerShell and not Bash, in the top left of the Cloud Shell window.</span></span>

1. <span data-ttu-id="eb306-128">Verwenden Sie das folgende Cmdlet, um die Liste mit den verfügbaren VM-Größen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="eb306-128">Use the following cmdlet to get the list of available virtual machine sizes.</span></span>

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -VMName my-test-vm
    ```

1. <span data-ttu-id="eb306-129">Verwenden Sie das folgende Cmdlet, um die Größe des virtuellen Computers in _DS2_v2_ zurückzuändern.</span><span class="sxs-lookup"><span data-stu-id="eb306-129">Use the following cmdlet to resize the virtual machine back to a _DS2_v2_ size.</span></span>

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -VMName my-test-vm
    $vm.HardwareProfile.VmSize = "Standard_DS2_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName <rgn>[sandbox resource group name]</rgn>
    ```

1. <span data-ttu-id="eb306-130">Klicken Sie auf dem Blatt **my-test-vm** auf die Schaltfläche **Aktualisieren**, während Sie darauf warten, dass der PowerShell-Befehl zu Ende ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="eb306-130">Click the **Refresh** button in the **my-test-vm** blade while you are waiting for the PowerShell command to finish.</span></span> <span data-ttu-id="eb306-131">Der virtuelle Computer sollte nun neu gestartet werden, um die Größenänderung zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="eb306-131">You should notice that the virtual machine is restarting to accommodate the change in size.</span></span>

<span data-ttu-id="eb306-132">In dieser Übung haben Sie einen virtuellen Computer erstellt und seine Größe mit zwei verschiedenen Tools geändert.</span><span class="sxs-lookup"><span data-stu-id="eb306-132">In this exercise, you created a virtual machine and resized it with two different tools.</span></span> <span data-ttu-id="eb306-133">Tipp: Denken Sie daran, dass die Zielgröße möglicherweise nicht verfügbar ist, solange der virtuelle Computer ausgeführt wird. Nach Beendigung des virtuellen Computers stehen mehr Größen zur Auswahl.</span><span class="sxs-lookup"><span data-stu-id="eb306-133">A good tip to keep in mind is that the target size may not be available while the virtual machine is running; stopping the virtual machine lets you choose more sizes.</span></span>