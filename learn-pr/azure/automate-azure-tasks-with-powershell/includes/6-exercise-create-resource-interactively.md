<span data-ttu-id="244c5-101">Wiederholen wir unser ursprüngliches Szenario – Erstellen von VMs zum Testen unserer CRM-Software.</span><span class="sxs-lookup"><span data-stu-id="244c5-101">Recall our original scenario - creating VMs to test our CRM software.</span></span> <span data-ttu-id="244c5-102">Wenn ein neuer Build verfügbar ist, möchten wir eine neue VM einrichten, damit wir die vollständige Installation anhand eines sauberen Image testen können.</span><span class="sxs-lookup"><span data-stu-id="244c5-102">When a new build is available, we want to spin up a new VM so we can test the full install experience from a clean image.</span></span> <span data-ttu-id="244c5-103">Wenn wir fertig sind, möchten wir Sie die VM löschen.</span><span class="sxs-lookup"><span data-stu-id="244c5-103">Then when we are finished, we want to delete the VM.</span></span>

<span data-ttu-id="244c5-104">Probieren Sie die Befehle aus, die Sie zum Erstellen einer VM verwenden.</span><span class="sxs-lookup"><span data-stu-id="244c5-104">Let's try the commands you would use to create a VM.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm-with-azure-powershell"></a><span data-ttu-id="244c5-105">Erstellen einer Linux-VM mithilfe von Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="244c5-105">Create a Linux VM with Azure PowerShell</span></span>

<span data-ttu-id="244c5-106">Da wir die Azure-Sandbox verwenden, müssen Sie keine Ressourcengruppe erstellen.</span><span class="sxs-lookup"><span data-stu-id="244c5-106">Since we are using the Azure sandbox, you won't have to create a Resource Group.</span></span> <span data-ttu-id="244c5-107">Verwenden Sie stattdessen die Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.</span><span class="sxs-lookup"><span data-stu-id="244c5-107">Instead, use the Resource Group **<rgn>[sandbox resource group name]</rgn>**.</span></span> <span data-ttu-id="244c5-108">Achten Sie darüber hinaus auf Standorteinschränkungen.</span><span class="sxs-lookup"><span data-stu-id="244c5-108">In addition, be aware of the location restrictions.</span></span>

<span data-ttu-id="244c5-109">Erstellen wir eine neue Azure-VM mit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="244c5-109">Let's create a new Azure VM with PowerShell.</span></span>

1. <span data-ttu-id="244c5-110">Verwenden Sie das `New-AzureRmVm`-Cmdlet zum Erstellen einer VM.</span><span class="sxs-lookup"><span data-stu-id="244c5-110">Use the `New-AzureRmVm` cmdlet to create a VM.</span></span>
    - <span data-ttu-id="244c5-111">Verwenden Sie die Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.</span><span class="sxs-lookup"><span data-stu-id="244c5-111">Use the Resource Group **<rgn>[sandbox resource group name]</rgn>**.</span></span>
    - <span data-ttu-id="244c5-112">Geben Sie der VM einen Namen. Verwenden Sie einen aussagekräftigen Namen, der den Zweck der VM, den Standort und (wenn es mehr als eine gibt) die Instanznummer angibt.</span><span class="sxs-lookup"><span data-stu-id="244c5-112">Give the VM a name - typically you want to use something meaningful that identifies the purposes of the VM, location, and (if there is more than one) instance number.</span></span> <span data-ttu-id="244c5-113">Wir verwenden „testvm-eus-01“ für „Test VM in East US, instance 1“.</span><span class="sxs-lookup"><span data-stu-id="244c5-113">We'll use "testvm-eus-01" for "Test VM in East US, instance 1".</span></span> <span data-ttu-id="244c5-114">Sie können auch einen eigenen Namen basierend auf dem VM-Speicherort eingeben.</span><span class="sxs-lookup"><span data-stu-id="244c5-114">Come up with your own name based on where you place the VM.</span></span>
    - <span data-ttu-id="244c5-115">Wählen Sie in der Azure-Sandbox aus der folgenden Liste einen Standort in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="244c5-115">Select a location close to you from the following list available in the Azure sandbox.</span></span> <span data-ttu-id="244c5-116">Achten Sie darauf, den Wert im folgenden Beispielbefehl zu ändern, wenn Sie ihn kopieren und einfügen.</span><span class="sxs-lookup"><span data-stu-id="244c5-116">Make sure to change the value in the below example command if you are using copy and paste.</span></span>

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - <span data-ttu-id="244c5-117">Verwenden Sie „UbuntuLTS“ für das Image – dies ist Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="244c5-117">Use "UbuntuLTS" for the image - this is Ubuntu Linux.</span></span>
    - <span data-ttu-id="244c5-118">Verwenden Sie das `Get-Credential`-Cmdlet und geben Sie die Ergebnisse in den `Credential`-Parameter ein.</span><span class="sxs-lookup"><span data-stu-id="244c5-118">Use the `Get-Credential` cmdlet and feed the results into the `Credential` parameter.</span></span>
    - <span data-ttu-id="244c5-119">Fügen Sie den `-OpenPorts`-Parameter hinzu, und übergeben Sie „22“ als Port – auf diese Weise können wir SSH auf dem Computer verwenden.</span><span class="sxs-lookup"><span data-stu-id="244c5-119">Add the `-OpenPorts` parameter and pass "22" as the port - this will let us SSH into the machine.</span></span>
 
    ```powershell
    New-AzureRmVm -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -Name "testvm-eus-01" -Credential (Get-Credential) -Location "East US" -Image UbuntuLTS -OpenPorts 22
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
    
1. <span data-ttu-id="244c5-120">Der Erstellungsvorgang dauert ein paar Minuten.</span><span class="sxs-lookup"><span data-stu-id="244c5-120">This will take a few minutes to complete.</span></span> <span data-ttu-id="244c5-121">Nach Abschluss können Sie einen Abfrage durchführen und das VM-Objekt einer Variable (`$vm`) zuweisen.</span><span class="sxs-lookup"><span data-stu-id="244c5-121">Once it does, you can query it and assign the VM object to a variable (`$vm`).</span></span>

    ```powershell
    $vm = Get-AzureRmVM -Name "testvm-eus-01" -ResourceGroupName <rgn>[sandbox resource group name]</rgn>
    ```
    
1. <span data-ttu-id="244c5-122">Fragen Sie anschließend den Wert ab, um die Informationen über die VM zu sichern:</span><span class="sxs-lookup"><span data-stu-id="244c5-122">Then query the value to dump out the information about the VM:</span></span>

    ```powershell
    $vm
    ```

    <span data-ttu-id="244c5-123">Die Ausgabe sollte folgendermaßen aussehen:</span><span class="sxs-lookup"><span data-stu-id="244c5-123">You should see something like:</span></span>

    ```output
    ResourceGroupName : <rgn>[sandbox resource group name]</rgn>
    Id                : /subscriptions/xxxxxxxx-xxxx-aaaa-bbbb-cccccccccccc/resourceGroups/<rgn>[sandbox resource group name]</rgn>/providers/Microsoft.Compute/virtualMachines/testvm-eus-01
    VmId              : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    Name              : testvm-eus-01
    Type              : Microsoft.Compute/virtualMachines
    Location          : eastus
    Tags              : {}
    HardwareProfile   : {VmSize}
    NetworkProfile    : {NetworkInterfaces}
    OSProfile         : {ComputerName, AdminUsername, LinuxConfiguration, Secrets}
    ProvisioningState : Succeeded
    StorageProfile    : {ImageReference, OsDisk, DataDisks}
    ```
    
1. <span data-ttu-id="244c5-124">Über eine Punktsyntax („.“) können Sie komplexe Objekte erreichen.</span><span class="sxs-lookup"><span data-stu-id="244c5-124">You can reach into complex objects through a dot (".") syntax.</span></span> <span data-ttu-id="244c5-125">Um beispielsweise die Eigenschaften im Objekt `VMSize` zu sehen, das dem Abschnitt „HardwareProfile“ zugeordnet ist, können Sie Folgendes eingeben:</span><span class="sxs-lookup"><span data-stu-id="244c5-125">For example, to see the properties in the `VMSize` object associated with the HardwareProfile section you can type:</span></span>

    ```powershell
    $vm.HardwareProfile
    ```

1. <span data-ttu-id="244c5-126">Oder rufen Sie Informationen auf einem Datenträger ab:</span><span class="sxs-lookup"><span data-stu-id="244c5-126">Or to get information on one of the disks:</span></span>

    ```powershell
    $vm.StorageProfile.OsDisk
    ```

1. <span data-ttu-id="244c5-127">Sie können auch das VM-Objekt an andere Cmdlets übergeben.</span><span class="sxs-lookup"><span data-stu-id="244c5-127">You can even pass the VM object into other cmdlets.</span></span> <span data-ttu-id="244c5-128">Beispielsweise können Sie so die öffentliche IP-Adresse von Ihrer VM abrufen:</span><span class="sxs-lookup"><span data-stu-id="244c5-128">For example, this will retrieve the public IP address of your VM:</span></span>

    ```powershell
    $vm | Get-AzureRmPublicIpAddress
    ```

1. <span data-ttu-id="244c5-129">Über die IP-Adresse können Sie sich mit SSH mit Ihrer VM verbinden.</span><span class="sxs-lookup"><span data-stu-id="244c5-129">With the IP address, you can connect to the VM with SSH.</span></span> <span data-ttu-id="244c5-130">Wenn Sie beispielsweise den Benutzernamen „bob“ verwendet haben und die IP-Adresse „205.22.16.5“ lautet, dann würde über diesen Befehl eine Verbindung mit dem Linux-Rechner hergestellt werden:</span><span class="sxs-lookup"><span data-stu-id="244c5-130">For example, if you used the username "bob", and the IP address is "205.22.16.5", then this command would connect to the Linux machine:</span></span>

    ```powershell
    ssh bob@205.22.16.5
    ```

    <span data-ttu-id="244c5-131">Melden Sie sich anschließend ab, indem Sie `exit` eingeben.</span><span class="sxs-lookup"><span data-stu-id="244c5-131">Go ahead and log out by typing `exit`.</span></span>


## <a name="delete-a-vm"></a><span data-ttu-id="244c5-132">Löschen einer VM</span><span class="sxs-lookup"><span data-stu-id="244c5-132">Delete a VM</span></span>

<span data-ttu-id="244c5-133">Um weitere Befehle auszuprobieren, werden wir die VM jetzt löschen.</span><span class="sxs-lookup"><span data-stu-id="244c5-133">Just to try out some more commands, let's delete the VM.</span></span> <span data-ttu-id="244c5-134">Zunächst fahren wir sie herunter.</span><span class="sxs-lookup"><span data-stu-id="244c5-134">We'll shut it down first.</span></span>

```powershell
Stop-AzureRmVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

<span data-ttu-id="244c5-135">Jetzt löschen wir die VM mit dem `Remove-AzureRmVM`-Cmdlet:</span><span class="sxs-lookup"><span data-stu-id="244c5-135">Now, let's delete the VM with the `Remove-AzureRmVM` cmdlet:</span></span>

```powershell
Remove-AzureRmVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

<span data-ttu-id="244c5-136">Verwenden Sie diesen Befehl, um die Ressourcen in Ihrer Ressourcengruppe aufzulisten:</span><span class="sxs-lookup"><span data-stu-id="244c5-136">Try this command to list all the resources in your resource group:</span></span>

```powershell
Get-AzureRmResource -ResourceGroupName $vm.ResourceGroupName | ft
```

<span data-ttu-id="244c5-137">Daraufhin sollte eine Reihe von Ressourcen (Datenträger, virtuellen Netzwerken usw.) angezeigt werden, die alle noch vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="244c5-137">You should see a bunch of resources (disks, virtual networks, etc.) that all still exist.</span></span> 

```output
Microsoft.Compute/disks
Microsoft.Network/networkInterfaces
Microsoft.Network/networkSecurityGroups
Microsoft.Network/publicIPAddresses
Microsoft.Network/virtualNetworks
```

<span data-ttu-id="244c5-138">Grund hierfür ist, dass mit dem `Remove-AzureRmVM`-Befehl _nur die VM gelöscht wird_.</span><span class="sxs-lookup"><span data-stu-id="244c5-138">This is because the `Remove-AzureRmVM` command _just deletes the VM_.</span></span> <span data-ttu-id="244c5-139">Es werden keine weiteren Ressourcen bereinigt.</span><span class="sxs-lookup"><span data-stu-id="244c5-139">It doesn't cleanup any of the other resources!</span></span> <span data-ttu-id="244c5-140">An dieser Stelle möchten wir nur die Ressourcengruppe löschen.</span><span class="sxs-lookup"><span data-stu-id="244c5-140">At this point, we'd likely just delete the Resource Group itself and be done with it.</span></span> <span data-ttu-id="244c5-141">Lassen Sie uns jedoch einfach die Übung durchlaufen, um sie manuell zu bereinigen.</span><span class="sxs-lookup"><span data-stu-id="244c5-141">However, let's just run through the exercise to clean it up manually.</span></span> <span data-ttu-id="244c5-142">Sie sollten ein Muster in den Befehlen erkennen.</span><span class="sxs-lookup"><span data-stu-id="244c5-142">You should see a pattern in the commands.</span></span>

1. <span data-ttu-id="244c5-143">Löschen Sie die Netzwerkschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="244c5-143">Delete the Network Interface.</span></span>

    ```powershell
    $vm | Remove-AzureRmNetworkInterface –Force
    ```
    
1. <span data-ttu-id="244c5-144">Löschen Sie den verwalteten Betriebssystemdatenträger und das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="244c5-144">Delete the managed OS disks and storage account</span></span>

    ```powershell
    Get-AzureRmDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzureRmDisk -Force
    ```

1. <span data-ttu-id="244c5-145">Löschen Sie anschließend das virtuelle Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="244c5-145">Next, delete the virtual network.</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmVirtualNetwork -Force
    ```

1. <span data-ttu-id="244c5-146">Löschen Sie die Netzwerksicherheitsgruppe.</span><span class="sxs-lookup"><span data-stu-id="244c5-146">Delete the network security group.</span></span>

    ```powershell
    Get-AzureRmNetworkSecurityGroup -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmNetworkSecurityGroup -Force
    ```

1. <span data-ttu-id="244c5-147">Und abschließend die öffentlichen IP-Adresse.</span><span class="sxs-lookup"><span data-stu-id="244c5-147">And finally, the public IP address.</span></span>

    ```powershell
    Get-AzureRmPublicIpAddress -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmPublicIpAddress -Force
    ```

<span data-ttu-id="244c5-148">Wir sollten alle erstellten Ressourcen erfasst haben. Überprüfen Sie die Ressourcengruppe, nur um sicher zu gehen.</span><span class="sxs-lookup"><span data-stu-id="244c5-148">We should have caught all the created resources; check the resource group just to be sure.</span></span> <span data-ttu-id="244c5-149">Wir haben hier viele manuelle Befehle ausgeführt, aber ein besserer Ansatz wäre gewesen, ein _Skript_ zu schreiben, damit wir diese Logik später wiederverwenden können, um eine VM zu erstellen oder zu löschen.</span><span class="sxs-lookup"><span data-stu-id="244c5-149">We did a lot of manual commands here but a better approach would have been to write a _script_ so we could reuse this logic later to create or delete a VM.</span></span> <span data-ttu-id="244c5-150">Schauen wir uns die Skripterstellung mit PowerShell an.</span><span class="sxs-lookup"><span data-stu-id="244c5-150">Let's look at scripting with PowerShell.</span></span>