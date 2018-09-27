<span data-ttu-id="cb2ff-101">Angenommen, Sie entwickeln eine Anwendung zur Finanzverwaltung für neue Startupunternehmen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-101">Suppose you are developing a financial management application for new business startups.</span></span> <span data-ttu-id="cb2ff-102">Sie möchten sicherstellen, dass all ihre Kundendaten geschützt sind. Daher haben Sie sich entschieden, Azure Disk Encryption (ADE) durchgängig für alle (Betriebssystem-)Datenträger auf den Servern einzusetzen, auf denen die Anwendung gehostet ist.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-102">You want to ensure that all your customers' data is secured, so you have decided to implement Azure Disk Encryption (ADE) across all OS and data disks on the servers that will host this application.</span></span> <span data-ttu-id="cb2ff-103">Im Rahmen Ihrer Complianceanforderungen müssen Sie zudem selbst die Verantwortung für die Verwaltung Ihrer eigenen Verschlüsselungsschlüssel tragen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-103">As part of your compliance requirements, you also need to be responsible for your own encryption key management.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="cb2ff-104">In dieser Einheit verschlüsseln Sie Datenträger auf vorhandenen virtuellen Computern und verwalten die Verschlüsselungsschlüssel mithilfe Ihrer eigenen Azure Key Vault-Instanz.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-104">In this unit, you'll encrypt disks on an existing virtual machine, and manage the encryption keys using your own Azure Key Vault.</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="cb2ff-105">Vorbereiten der Umgebung</span><span class="sxs-lookup"><span data-stu-id="cb2ff-105">Prepare the environment</span></span>

<span data-ttu-id="cb2ff-106">Zunächst wird ein neuer virtueller Windows-Computer auf einem virtuellen Azure-Computer bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-106">We'll start by deploying a new Windows VM in an Azure Virtual Machine.</span></span>

### <a name="deploy-windows-vm"></a><span data-ttu-id="cb2ff-107">Bereitstellen eines virtuellen Windows-Computers</span><span class="sxs-lookup"><span data-stu-id="cb2ff-107">Deploy Windows VM</span></span>

<span data-ttu-id="cb2ff-108">Erstellen Sie einen neuen virtuellen Windows-Computer mit Azure PowerShell, und stellen Sie diesen bereit.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-108">Use the Azure PowerShell to create and deploy a new Windows virtual machine.</span></span>

1. <span data-ttu-id="cb2ff-109">Überlegen Sie zunächst, wo die neuen Ressourcen untergebracht werden sollen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-109">Start by deciding where to place the new resources.</span></span> <span data-ttu-id="cb2ff-110">Wählen Sie aus der folgenden Liste einen Standort in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-110">Select a location near you from the following list.</span></span>

    <span data-ttu-id="cb2ff-111"><!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]</span><span class="sxs-lookup"><span data-stu-id="cb2ff-111"><!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]</span></span>
    

1. <span data-ttu-id="cb2ff-112">Definieren Sie eine PowerShell-Variable, die den ausgewählten Standort enthalten soll.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-112">Define a PowerShell variable to hold the selected location.</span></span> <span data-ttu-id="cb2ff-113">Hier ist „USA, Osten“ als Standort definiert. Ändern Sie diese Angabe in Ihren bevorzugten Standort.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-113">It's defined as "East US" here, change it to your preferred location.</span></span>

    ```powershell
    $location = "eastus"
    ```
    
    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="cb2ff-114">Definieren Sie als Nächstes einige zweckdienlichere Variablen zum Erfassen des _Namens_ des virtuellen Computers sowie der _Ressourcengruppe_.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-114">Next, define a few more convenient variables to capture the _name_ of the VM and the _resource group_.</span></span> <span data-ttu-id="cb2ff-115">Beachten Sie, dass hier die vorab erstellte Ressourcengruppe verwendet wird. Normalerweise würden Sie in Ihrem Abonnement mithilfe von `New-AzureRmResourceGroup` eine _neue_ Ressourcengruppe erstellen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-115">Note that we are using the pre-created resource group here, normally you would create a _new_ resource group in your subscription using `New-AzureRmResourceGroup`.</span></span>

    ```powershell
    $vmName = "fmdata-vm01"
    $rgName = "<rgn>[sandbox Resource Group]</rgn>"
    ```
    
1. <span data-ttu-id="cb2ff-116">Erstellen Sie mit `New-AzureRmVm` einen neuen virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-116">Use `New-AzureRmVm` to create a new virtual machine.</span></span>
    
    ```powershell
    New-AzureRmVm `
        -ResourceGroupName $rgName `
        -Name $vmName `
        -Location $location `
        -OpenPorts 3389
    ```
    
    <span data-ttu-id="cb2ff-117">Geben Sie einen Benutzernamen und ein Kennwort für den virtuellen Computer ein, wenn Sie von Cloud Shell dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-117">Enter a username and password for the VM when you are prompted by the Cloud Shell.</span></span> <span data-ttu-id="cb2ff-118">Diese werden für das erste Konto verwendet, das für den virtuellen Computer erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-118">This will be used as the initial account created for the VM.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cb2ff-119">Dieser Befehl verwendet einige Standardeinstellungen, da eine Reihe von Optionen nicht bereitgestellt wurde.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-119">This command will use some defaults since we didn't supply a bunch of options.</span></span> <span data-ttu-id="cb2ff-120">Dadurch wird insbesondere ein _Windows 2016 Server_-Image mit der Größe _Standard_DS1_v2_ erstellt.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-120">Specifically, this will create a _Windows 2016 Server_ image with the size to _Standard_DS1_v2_.</span></span> <span data-ttu-id="cb2ff-121">Beachten Sie, dass die virtuellen Computer der Basisebene ADE nicht unterstützen, wenn Sie die Größe des virtuellen Computer angeben möchten.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-121">Remember that the Basic tier VMs do not support ADE if you decide to specify the VM size.</span></span>

1. <span data-ttu-id="cb2ff-122">Sobald der virtuelle Computer die Bereitstellung abgeschlossen hat, können Sie die Details zum virtuellen Computer in einer Variablen erfassen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-122">Once the VM finishes deploying, capture the VM details in a variable.</span></span> <span data-ttu-id="cb2ff-123">Sie können mithilfe dieser Variable die erstellten Komponenten untersuchen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-123">You can use this variable to explore what was created.</span></span>

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```
    
1. <span data-ttu-id="cb2ff-124">Sie können den an den virtuellen Computer angefügten Betriebssystem-Datenträger sehen:</span><span class="sxs-lookup"><span data-stu-id="cb2ff-124">You can see the OS disk attached to the VM:</span></span>

    ```powershell
    $vm.StorageProfile.OSDisk
    ```

    ```output
    OsType                  : Windows
    EncryptionSettings      :
    Name                    : fmdata-vm01_OsDisk_1_6bcf8dcd49794aa785bad45221ec4433
    Vhd                     :
    Image                   :
    Caching                 : ReadWrite
    WriteAcceleratorEnabled :
    CreateOption            : FromImage
    DiskSizeGB              : 127
    ManagedDisk             : Microsoft.Azure.Management.Compute.Models.ManagedDiskP
                              arameters
    ```
        
1. <span data-ttu-id="cb2ff-125">Überprüfen Sie den aktuellen Status der Verschlüsselung auf dem Betriebssystem-Datenträger (und auf allen anderen Datenträgern).</span><span class="sxs-lookup"><span data-stu-id="cb2ff-125">Check the current status of encryption on the OS disk (and any data disks).</span></span>

    ```powershell
    Get-AzureRmVmDiskEncryptionStatus  `
        -ResourceGroupName $rgName `
        -VMName $vmName
    ```

    <span data-ttu-id="cb2ff-126">Wie Sie sehen können, sind die Datenträger aktuell _unverschlüsselt_.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-126">As you can see the disks are current _unencrypted_.</span></span> 

    ```output
    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : NotEncrypted
    OsVolumeEncryptionSettings :
    ProgressMessage            : No Encryption extension or metadata found on the VM
    ```
    
<span data-ttu-id="cb2ff-127">Ändern wir das.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-127">Let's change that.</span></span>
    
## <a name="encrypt-the-vm-disks-with-azure-disk-encryption"></a><span data-ttu-id="cb2ff-128">Verschlüsseln der Datenträger des virtuellen Computers mithilfe von Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="cb2ff-128">Encrypt the VM disks with Azure Disk Encryption</span></span>

<span data-ttu-id="cb2ff-129">Da wir diese Daten schützen müssen, sollten wir die Datenträger verschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-129">We need to protect this data, so let's encrypt the disks.</span></span> <span data-ttu-id="cb2ff-130">Denken Sie daran, dass hierzu mehrere Schritte erforderlich sind:</span><span class="sxs-lookup"><span data-stu-id="cb2ff-130">Recall that there are several steps we need to perform:</span></span>

1. <span data-ttu-id="cb2ff-131">Erstellen Sie einen Schlüsseltresor.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-131">Create a key vault.</span></span>
1. <span data-ttu-id="cb2ff-132">Richten Sie den Schlüsseltresor so ein, dass Datenträgerverschlüsselung unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-132">Set the key vault up to support disk encryption.</span></span>
1. <span data-ttu-id="cb2ff-133">Erteilen Sie Azure den Befehl, die Datenträger des virtuellen Computers mithilfe des im Schlüsseltresor gespeicherten Schlüssels zu verschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-133">Tell Azure to encrypt the VM disks using the key stored in the Key Vault.</span></span>

> [!TIP]
> <span data-ttu-id="cb2ff-134">Wir werden uns die Schritte im Detail ansehen. Wenn Sie diese Aufgabe jedoch in Ihrem eigenen Abonnement ausführen, können Sie ein praktisches PowerShell-Skript verwenden, das in der Zusammenfassung dieses Moduls verlinkt ist.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-134">We're going to walk through the steps individually, but when you're doing this task in your own subscription, you can use a handy PowerShell script which is linked in the Summary of this module.</span></span>

### <a name="create-a-key-vault"></a><span data-ttu-id="cb2ff-135">Erstellen eines Schlüsseltresors</span><span class="sxs-lookup"><span data-stu-id="cb2ff-135">Create a key vault</span></span>

<span data-ttu-id="cb2ff-136">Zum Erstellen einer Azure Key Vault-Instanz müssen wir den Dienst in unserem Abonnement aktivieren.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-136">To create an Azure Key Vault, we need to enable the service in our subscription.</span></span> <span data-ttu-id="cb2ff-137">Dies ist eine einmalige Anforderung.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-137">This is a one-time requirement.</span></span>

> [!TIP]
> <span data-ttu-id="cb2ff-138">Je nach Abonnement müssen Sie möglicherweise den **Microsoft.KeyVault**-Anbieter mit dem `Register-AzureRmResourceProvider`-Cmdlet aktivieren.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-138">Depending on your subscription, you might need to enable the **Microsoft.KeyVault** provider with the `Register-AzureRmResourceProvider` cmdlet.</span></span> <span data-ttu-id="cb2ff-139">Dies ist beim Azure-Sandboxabonnement nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-139">This is not necessary in the Azure sandbox subscription.</span></span>

1. <span data-ttu-id="cb2ff-140">Geben Sie Ihrem neuen Schlüsseltresor einen Namen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-140">Decide on a name for your new key vault.</span></span> <span data-ttu-id="cb2ff-141">Der Name muss eindeutig sein, zwischen 3 und 24 Zeichen lang sein und sich aus Zahlen, Buchstaben und Bindestrichen zusammensetzen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-141">It must be unique and can be between 3 and 24 characters, composed of numbers, letters, and and dashes.</span></span> <span data-ttu-id="cb2ff-142">Versuchen Sie, einige Zufallszahlen am Ende hinzuzufügen, durch die die nachfolgend aufgeführte Zahl „1234“ ersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-142">Try adding some random numbers to the end, replacing the "1234" below.</span></span>

    ```powershell
    $keyVaultName = "mvmdsk-kv-1234"
    ```
        
1. <span data-ttu-id="cb2ff-143">Erstellen Sie mit `New-AzureRmKeyVault` eine Azure Key Vault-Instanz.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-143">Create an Azure Key Vault with `New-AzureRmKeyVault`.</span></span>
    - <span data-ttu-id="cb2ff-144">Stellen Sie sicher, dass sich diese in derselben Ressourcengruppe _und_ am selben Ort wie Ihr virtueller Computer befindet.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-144">Make sure it's placed in the same resource group _and_ location as your VM.</span></span>
    - <span data-ttu-id="cb2ff-145">Aktivieren Sie die Key Vault-Instanz für die Verwendung mit der Datenträgerverschlüsselung.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-145">Enable the Key Vault for use with disk encryption.</span></span> 
    - <span data-ttu-id="cb2ff-146">Geben Sie einen eindeutigen Namen für die Key Vault-Instanz an.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-146">Specify a unique Key Vault name.</span></span>

    ```powershell
    New-AzureRmKeyVault -VaultName $keyVaultName `
        -Location $location `
        -ResourceGroupName $rgName `
        -EnabledForDiskEncryption
    ```

    <span data-ttu-id="cb2ff-147">Nach der Ausführung dieses Befehls wird eine Warnung angezeigt, in der darauf hingewiesen wird, dass kein Benutzer Zugriff hat.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-147">You will get a warning from this command about no users having access.</span></span>

    ```output
    WARNING: Access policy is not set. No user or application have access permission to use this vault. This can happen if the vault was created by a service principal. Please use Set-AzureRmKeyVaultAccessPolicy to set access policies.
    ```

    <span data-ttu-id="cb2ff-148">Dies ist kein Problem, da der Tresor nur verwendet wird, um die Verschlüsselungsschlüssel für den virtuellen Computer zu speichern, und die Benutzer nicht auf diese Daten zugreifen müssen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-148">This is ok since we are just using the vault to store the encryption keys for the VM and users won't need to access this data.</span></span>

### <a name="encrypt-the-disk"></a><span data-ttu-id="cb2ff-149">Verschlüsseln des Datenträgers</span><span class="sxs-lookup"><span data-stu-id="cb2ff-149">Encrypt the disk</span></span>

<span data-ttu-id="cb2ff-150">Sie können gleich mit der Verschlüsselung der Datenträger beginnen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-150">We are almost ready to encrypt the disks.</span></span> <span data-ttu-id="cb2ff-151">Zuvor jedoch ein Wort der Warnung hinsichtlich der Erstellung von Sicherungen:</span><span class="sxs-lookup"><span data-stu-id="cb2ff-151">Before we do, a warning about creating backups.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb2ff-152">Wenn es sich hierbei um ein Produktionssystem handeln würde, müssten Sie eine Sicherung der verwalteten Datenträger vornehmen – entweder mit Azure Backup oder durch das Erstellen einer Momentaufnahme.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-152">If this were a production system, we would need to perform a backup of the managed disks - either using Azure Backup, or by creating a snapshot.</span></span> <span data-ttu-id="cb2ff-153">Sie können Momentaufnahmen im Azure-Portal oder über die Befehlszeile erstellen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-153">You can create snapshots in the Azure portal, or through the command line.</span></span> <span data-ttu-id="cb2ff-154">Verwenden Sie in PowerShell das `New-AzureRmSnapshot`-Cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-154">In PowerShell, use the `New-AzureRmSnapshot` cmdlet.</span></span> <span data-ttu-id="cb2ff-155">Da dies eine einfache Übung ist und wir diese Daten löschen werden, wenn Sie fertig sind, werden wir diesen Schritt überspringen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-155">Since this is a simple exercise and we're going to throw this data away when you're done, we're going to skip this step.</span></span> 

1. <span data-ttu-id="cb2ff-156">Definieren Sie zunächst eine Variable zum Speichern der Key Vault-Informationen.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-156">Start by defining a variable to hold the Key Vault information.</span></span>

    ```powershell
    $keyVault = Get-AzureRmKeyVault `
        -VaultName $keyVaultName `
        -ResourceGroupName $rgName
    ```

1. <span data-ttu-id="cb2ff-157">Verwenden Sie anschließend das `Set-AzureRmVmDiskEncryptionExtension`-Cmdlet, um die Datenträger des virtuellen Computers zu verschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-157">Then, use the `Set-AzureRmVmDiskEncryptionExtension` cmdlet to encrypt the VM disks.</span></span>
    - <span data-ttu-id="cb2ff-158">Mithilfe des Parameters `VolumeType` können Sie angeben, welche Datenträger verschlüsselt werden sollen: [_All (Alle)_ | _OS (Betriebssystem)_ | _Data (Daten)_].</span><span class="sxs-lookup"><span data-stu-id="cb2ff-158">The `VolumeType` parameter allows you to specify which disks to encrypt: [_All_ | _OS_ | _Data_].</span></span> <span data-ttu-id="cb2ff-159">Der Standardwert ist _All_ (Alle).</span><span class="sxs-lookup"><span data-stu-id="cb2ff-159">It will default to _All_.</span></span> <span data-ttu-id="cb2ff-160">Datenträger können nicht unter allen Linux-Distributionen verschlüsselt werden.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-160">You can only encrypt data disks for some distributions of Linux.</span></span>
    - <span data-ttu-id="cb2ff-161">Sie müssen für verwaltete Datenträger das Flag `SkipVmBackup` angeben. Andernfalls schlägt der Befehl fehl, da keine Momentaufnahme vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-161">You have to supply the `SkipVmBackup` flag for managed disks or the command will fail because there is no snapshot.</span></span>

    ```powershell
    Set-AzureRmVmDiskEncryptionExtension `
        -ResourceGroupName $rgName `
        -VMName $vmName `
        -VolumeType All `
        -DiskEncryptionKeyVaultId $keyVault.ResourceId `
        -DiskEncryptionKeyVaultUrl $keyVault.VaultUri `
        -SkipVmBackup
    ```

1. <span data-ttu-id="cb2ff-162">Dieses Cmdlet gibt als Warnung aus, dass der virtuelle Computer offline geschaltet werden muss und der Vorgang einige Minuten in Anspruch nehmen kann.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-162">The cmdlet will warn you that the VM must be taken offline, and that the task may take several minutes to complete.</span></span> <span data-ttu-id="cb2ff-163">Setzen Sie den Vorgang fort.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-163">Go ahead and let it continue.</span></span>

    ```output
    Enable AzureDiskEncryption on the VM
    This cmdlet prepares the VM and enables encryption which may reboot the machine and takes 10-15 minutes to
    finish. Please save your work on the VM before confirming. Do you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
    ```
    
1. <span data-ttu-id="cb2ff-164">Überprüfen Sie nach Abschluss des Vorgangs erneut den Verschlüsselungsstatus.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-164">Once it's complete, check the encryption status again.</span></span>

    ```powershell
    Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
    ```

    <span data-ttu-id="cb2ff-165">Der Betriebssystem-Datenträger sollte jetzt verschlüsselt sein.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-165">Now the OS disk should be encrypted.</span></span> <span data-ttu-id="cb2ff-166">Sämtliche angefügte Datenträger, die für Windows sichtbar sind, werden ebenfalls verschlüsselt.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-166">Any attached data disks that are visible to Windows will also be encrypted.</span></span>

    ```output
    OsVolumeEncrypted          : Encrypted
    DataVolumesEncrypted       : NoDiskFound
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : Provisioning succeeded
    ```

> [!NOTE]        
> <span data-ttu-id="cb2ff-167">Werden nach der Verschlüsselung neue Datenträger hinzugefügt, werden diese _nicht_ automatisch verschlüsselt.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-167">New disks added after encryption will _not_ be automatically encrypted.</span></span> <span data-ttu-id="cb2ff-168">Sie können das `Set-AzureRmVMDiskEncryptionExtension`-Cmdlet erneut ausführen, um die neuen Datenträger zu verschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-168">You can re-run the `Set-AzureRmVMDiskEncryptionExtension` cmdlet to encrypt new disks.</span></span> <span data-ttu-id="cb2ff-169">Achten Sie darauf, eine neue Sequenznummer anzugeben, wenn Sie Datenträger einem virtuellen Computer hinzufügen, auf dem bereits Datenträger verschlüsselt wurden.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-169">Make sure to provide a new sequence number if you add disks to a VM that has already had disks encrypted.</span></span> <span data-ttu-id="cb2ff-170">Beachten Sie außerdem, dass Datenträger, die nicht für das Betriebssystem sichtbar sind, nicht verschlüsselt werden. Der Datenträger muss ordnungsgemäß partitioniert, formatiert und eingebunden sein, damit er von der BitLocker-Erweiterung erkannt wird.</span><span class="sxs-lookup"><span data-stu-id="cb2ff-170">In addition, disks that are not visible to the operating system will not be encrypted - the disk must be properly partitioned, formatted, and mounted to be seen by the Bitlocker extension.</span></span>