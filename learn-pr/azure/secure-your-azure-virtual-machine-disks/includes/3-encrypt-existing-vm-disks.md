<span data-ttu-id="26277-101">Angenommen, Ihr Unternehmen hat sich entschieden, Azure Disk Encryption (ADE) auf allen VMs zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="26277-101">Suppose your company has decided to implement Azure Disk Encryption (ADE) across all VMs.</span></span> <span data-ttu-id="26277-102">In diesem Fall müssen Sie evaluieren, wie Sie die Verschlüsselung auf allen vorhandenen VM-Volumes durchführen.</span><span class="sxs-lookup"><span data-stu-id="26277-102">You need to evaluate how to roll out encryption to existing VM volumes.</span></span> <span data-ttu-id="26277-103">Hier werden die Anforderungen für ADE und die Schritte zum Verschlüsseln von Datenträgern auf vorhandenen Linux- und Windows-VMs beschrieben.</span><span class="sxs-lookup"><span data-stu-id="26277-103">Here, we'll look at the requirements for ADE, and the steps involved in encrypting disks on existing Linux and Windows VMs.</span></span>

## <a name="azure-disk-encryption-prerequisites"></a><span data-ttu-id="26277-104">Azure Disk Encryption: Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="26277-104">Azure Disk Encryption prerequisites</span></span>

<span data-ttu-id="26277-105">Bevor Sie Ihre VM-Datenträger verschlüsseln können, müssen Sie folgende Schritte durchführen:</span><span class="sxs-lookup"><span data-stu-id="26277-105">Before you can encrypt your VM disks, you need to:</span></span>

1. <span data-ttu-id="26277-106">Erstellen Sie einen Schlüsseltresor.</span><span class="sxs-lookup"><span data-stu-id="26277-106">Create a key vault.</span></span>
1. <span data-ttu-id="26277-107">Richten Sie die Zugriffsrichtlinie des Schlüsseltresors so ein, dass Datenträgerverschlüsselung unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="26277-107">Set the key vault access policy to support disk encryption.</span></span>
1. <span data-ttu-id="26277-108">Verwenden Sie den Schlüsseltresor, um die Verschlüsselungsschlüssel für ADE zu speichern.</span><span class="sxs-lookup"><span data-stu-id="26277-108">Use the key vault to store the encryption keys for ADE.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="26277-109">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="26277-109">Azure Key Vault</span></span>

<span data-ttu-id="26277-110">Die von ADE verwendeten Verschlüsselungsschlüssel können in einer Azure Key Vault-Instanz gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="26277-110">The encryption keys used by ADE can be stored in Azure Key Vault.</span></span> <span data-ttu-id="26277-111">Azure Key Vault ist ein Tool zum sicheren Speichern von Geheimnissen und Zugreifen darauf.</span><span class="sxs-lookup"><span data-stu-id="26277-111">Azure Key Vault is a tool for securely storing and accessing secrets.</span></span> <span data-ttu-id="26277-112">Als Geheimnis werden alle Elemente bezeichnet, für die Sie den Zugriff streng kontrollieren möchten, z.B. API-Schlüssel, Kennwörter oder Zertifikate.</span><span class="sxs-lookup"><span data-stu-id="26277-112">A secret is anything that you want to tightly control access to, such as API keys, passwords, or certificates.</span></span> <span data-ttu-id="26277-113">Hiermit wird die hoch verfügbare und skalierbare sichere Speicherung in Hardwaresicherheitsmodulen (HSMs) mit Überprüfung gemäß Federal Information Processing Standards (FIPS) 140-2 Level 2 ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="26277-113">This provides highly available and scalable secure storage, as defined in Federal Information Processing Standards (FIPS) 140-2 Level 2 validated Hardware Security Modules (HSMs).</span></span> <span data-ttu-id="26277-114">Mit Key Vault erhalten Sie die vollständige Kontrolle über die Schlüssel, die zum Verschlüsseln Ihrer Daten verwendet werden, und Sie können Ihre Schlüsselnutzung verwalten und überwachen.</span><span class="sxs-lookup"><span data-stu-id="26277-114">Using Key Vault, you keep full control of the keys used to encrypt your data, and you can manage and audit your key usage.</span></span> 

> [!NOTE]
> <span data-ttu-id="26277-115">Für Azure Disk Encryption müssen sich Ihre Key Vault-Instanz und Ihre VMs in derselben Azure-Region befinden. So wird sichergestellt, dass Verschlüsselungsgeheimnisse nicht über Grenzen von Regionen hinweg verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="26277-115">Azure Disk Encryption requires that your key vault and your VMs are in the same Azure region; this ensures that encryption secrets do not cross regional boundaries.</span></span>

<span data-ttu-id="26277-116">Sie können Ihren Schlüsseltresor mithilfe der folgenden Dienste konfigurieren und verwalten:</span><span class="sxs-lookup"><span data-stu-id="26277-116">You can configure and manage your key vault with:</span></span>

#### <a name="powershell"></a><span data-ttu-id="26277-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26277-117">Powershell</span></span>

```powershell
New-AzureRmKeyVault -Location <location> `
    -ResourceGroupName <resource-group> `
    -VaultName "myKeyVault" `
    -EnabledForDiskEncryption
```

### <a name="azure-cli"></a><span data-ttu-id="26277-118">die Azure CLI</span><span class="sxs-lookup"><span data-stu-id="26277-118">Azure CLI</span></span>

```azurecli
az keyvault create \
    --name "myKeyVault" \
    --resource-group <resource-group> \
    --location <location> \
    --enabled-for-disk-encryption True
```

### <a name="azure-portal"></a><span data-ttu-id="26277-119">das Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="26277-119">Azure portal</span></span>

<span data-ttu-id="26277-120">Azure Key Vault ist eine Ressource, die im Azure-Portal mithilfe des normalen Prozesses zur Ressourcenerstellung erstellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="26277-120">An Azure Key Vault is a resource that can be created in the Azure portal using the normal resource creation process.</span></span>

1. <span data-ttu-id="26277-121">Klicken Sie auf der Seitenleiste links auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="26277-121">Click **Create a resource** in the sidebar on the left.</span></span>

1. <span data-ttu-id="26277-122">Suchen Sie nach „Key Vault“.</span><span class="sxs-lookup"><span data-stu-id="26277-122">Search for "Key vault".</span></span> <span data-ttu-id="26277-123">Klicken Sie im Detailfenster auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="26277-123">Click **Create** in the details window.</span></span>

    ![Screenshot von Key Vault im Azure Marketplace](../media/3-create-keyvault.png)

1. <span data-ttu-id="26277-125">Geben Sie die Details für den neuen Schlüsseltresor ein:</span><span class="sxs-lookup"><span data-stu-id="26277-125">Enter the details for the new Key Vault:</span></span>
    - <span data-ttu-id="26277-126">Geben Sie unter **Name** einen Namen für den Schlüsseltresor ein.</span><span class="sxs-lookup"><span data-stu-id="26277-126">Enter a **Name** for the Key Vault</span></span>
    - <span data-ttu-id="26277-127">Wählen Sie das Abonnement aus, in dem der Schlüsseltresor platziert werden soll. (Standardmäßig wird der Schlüsseltresor in Ihrem aktuellen Abonnement platziert.)</span><span class="sxs-lookup"><span data-stu-id="26277-127">Select the subscription to place it in (defaults to your current subscription).</span></span>
    - <span data-ttu-id="26277-128">Wählen Sie eine **Ressourcengruppe** aus, oder erstellen Sie eine neue Ressourcengruppe, um Besitzer des Schlüsseltresors zu werden.</span><span class="sxs-lookup"><span data-stu-id="26277-128">Select a **Resource Group**, or create a new resource group to own the Key Vault.</span></span>
    - <span data-ttu-id="26277-129">Wählen Sie einen **Standort** für den Schlüsseltresor aus.</span><span class="sxs-lookup"><span data-stu-id="26277-129">Select a **Location** for the Key Vault.</span></span> <span data-ttu-id="26277-130">Stellen Sie sicher, dass Sie den Standort der VM auswählen.</span><span class="sxs-lookup"><span data-stu-id="26277-130">Make sure to select the location the VM is in.</span></span>
    - <span data-ttu-id="26277-131">Sie können zwischen den Tarifen „Standard“ und „Premium“ wählen.</span><span class="sxs-lookup"><span data-stu-id="26277-131">You can choose either Standard or Premium for the pricing tier.</span></span> <span data-ttu-id="26277-132">Der Hauptunterschied besteht darin, dass beim Tarif „Premium“ die Hardwareverschlüsselung von gesicherten Schlüsseln möglich ist.</span><span class="sxs-lookup"><span data-stu-id="26277-132">The main difference is that the premium tier allows for Hardware-encryption backed keys.</span></span>

1. <span data-ttu-id="26277-133">Sie müssen die Zugriffsrichtlinien ändern, um die Datenträgerverschlüsselung zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="26277-133">You must change the Access policies to support Disk Encryption.</span></span> <span data-ttu-id="26277-134">Standardmäßig wird _Ihr Konto_ der Richtlinie hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="26277-134">By default it adds _your_ account to the policy.</span></span>
    - <span data-ttu-id="26277-135">Wählen Sie die **Zugriffsrichtlinien** aus.</span><span class="sxs-lookup"><span data-stu-id="26277-135">Select **Access policies**</span></span>
    - <span data-ttu-id="26277-136">Klicken Sie auf **Erweiterte Zugriffsrichtlinien**.</span><span class="sxs-lookup"><span data-stu-id="26277-136">Click **Advanced access policies**.</span></span>
    - <span data-ttu-id="26277-137">Aktivieren Sie die Option **Zugriff auf Azure Disk Encryption für Volumenverschlüsselung aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="26277-137">Check the **Enable access to Azure Disk Encryption for volume encryption**.</span></span>
    - <span data-ttu-id="26277-138">Wenn Sie möchten, können Sie Ihr Konto entfernen, da es zum Verwenden des Schlüsseltresors für die Datenträgerverschlüsselung nicht erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="26277-138">You can remove your account if you like, it's not necessary if you only intend to use the Key Vault for disk encryption.</span></span>
    - <span data-ttu-id="26277-139">Klicken Sie zum Speichern der Änderungen auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="26277-139">Click **OK** to save the changes.</span></span>

    ![Screenshot von den erweiterten Eigenschaften für Key Vault mit aktivierter und hervorgehobener Azure Disk Encryption-Option](../media/3-configure-access-policy.png)

1. <span data-ttu-id="26277-141">Klicken Sie auf **Erstellen**, um den neuen Schlüsseltresor zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="26277-141">Click **Create** to create the new Key Vault.</span></span>

## <a name="enabling-access-policies-in-the-key-vault"></a><span data-ttu-id="26277-142">Aktivieren von Zugriffsrichtlinien im Schlüsseltresor</span><span class="sxs-lookup"><span data-stu-id="26277-142">Enabling access policies in the key vault</span></span>
<span data-ttu-id="26277-143">Azure benötigt Zugriff auf die Verschlüsselungsschlüssel oder geheimen Schlüssel in Ihrem Schlüsseltresor, um sie für die VM zur Verfügung zu stellen, damit die Volumes gestartet und entschlüsselt werden können.</span><span class="sxs-lookup"><span data-stu-id="26277-143">Azure needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="26277-144">Hinsichtlich des Portals wurde dies bereits weiter oben behandelt, als wir **Erweiterte Zugriffsrichtlinien** geändert haben.</span><span class="sxs-lookup"><span data-stu-id="26277-144">We covered this for the portal when we changed the **Advanced access policies** above.</span></span>

<span data-ttu-id="26277-145">Sie können drei verschiedene Richtlinien aktivieren:</span><span class="sxs-lookup"><span data-stu-id="26277-145">There are three policies you can enable.</span></span>
1. <span data-ttu-id="26277-146">**Datenträgerverschlüsselung:** Ist für die Azure Disk-Verschlüsselung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="26277-146">**Disk encryption** - Required for Azure Disk encryption.</span></span>
1. <span data-ttu-id="26277-147">**Bereitstellung (Optional):** Der Ressourcenanbieter „Microsoft.Compute“ wird aktiviert, um Geheimnisse aus diesem Schlüsseltresor abzurufen, wenn auf diesen Schlüsseltresor bei der Ressourcenerstellung (z.B. beim Erstellen einer VM) verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="26277-147">**Deployment** - (Optional) Enables the Microsoft.Compute resource provider to retrieve secrets from this key vault when this key vault is referenced in resource creation, for example when creating a virtual machine.</span></span>
1. <span data-ttu-id="26277-148">**Vorlagenbereitstellung (Optional):** Azure Resource Manager kann aus diesem Schlüsseltresor Geheimnisse abrufen, wenn auf diesen Schlüsseltresor in einer Vorlagenbereitstellung verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="26277-148">**Template deployment** - (Optional) Enables Azure Resource Manager to get secrets from this key vault when this key vault is referenced in a template deployment.</span></span>

<span data-ttu-id="26277-149">Hier erfahren Sie, wie Sie die Datenträgerverschlüsselungsrichtlinie aktivieren:</span><span class="sxs-lookup"><span data-stu-id="26277-149">Here's how to enable the disk encryption policy.</span></span> <span data-ttu-id="26277-150">Die beiden anderen sind zwar ähnlich, verwenden jedoch unterschiedliche Flags.</span><span class="sxs-lookup"><span data-stu-id="26277-150">The other two are similar but use different flags.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <keyvault-name> -ResourceGroupName <resource-group> -EnabledForDiskEncryption
```

```azurecli
az keyvault update --name <keyvault-name> --resource-group <resource-group> --enabled-for-disk-encryption "true"
```

## <a name="encrypting-an-existing-vm-disk"></a><span data-ttu-id="26277-151">Verschlüsseln eines vorhandenen VM-Datenträgers</span><span class="sxs-lookup"><span data-stu-id="26277-151">Encrypting an existing VM disk</span></span>

<span data-ttu-id="26277-152">Nachdem Key Vault eingerichtet ist, können Sie die VM verschlüsseln, indem Sie entweder die Azure CLI oder Azure PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="26277-152">Once you have the Key Vault setup, you can encrypt the VM using either Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="26277-153">Beim ersten Verschlüsseln einer Windows-VM können Sie auswählen, ob Sie alle Datenträger oder nur den Betriebssystemdatenträger verschlüsseln möchten.</span><span class="sxs-lookup"><span data-stu-id="26277-153">The first time you encrypt a Windows VM, you can choose to encrypt either all disks or the OS disk only.</span></span> <span data-ttu-id="26277-154">In einigen Linux-Distributionen können nur die Datenträger für Daten verschlüsselt werden.</span><span class="sxs-lookup"><span data-stu-id="26277-154">On some Linux distributions, only the data disks may be encrypted.</span></span> <span data-ttu-id="26277-155">Um für die Verschlüsselung geeignet zu sein, müssen Ihre Windows-Datenträger als NTFS-Volumes formatiert sein.</span><span class="sxs-lookup"><span data-stu-id="26277-155">To be eligible for encryption, your Windows disks must be formatted as NTFS volumes.</span></span>

> [!WARNING]
> <span data-ttu-id="26277-156">Sie müssen eine Momentaufnahme oder eine Sicherung von verwalteten Datenträgern erstellen, bevor Sie die Verschlüsselung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="26277-156">You must take a snapshot or a backup of managed disks before you can turn on encryption.</span></span> <span data-ttu-id="26277-157">Das unten angegebene `SkipVmBackup`-Flag weist das Tool darauf hin, dass die Sicherung auf den verwalteten Datenträgern abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="26277-157">The `SkipVmBackup` flag specified below tells the tool that the backup is complete on managed disks.</span></span> <span data-ttu-id="26277-158">Ohne die Sicherung können Sie die VM nicht wiederherstellen, wenn die Verschlüsselung aus irgendeinem Grund fehlschlägt.</span><span class="sxs-lookup"><span data-stu-id="26277-158">Without the backup, you will be unable to recover the VM if the encryption fails for some reason.</span></span>

<span data-ttu-id="26277-159">Verwenden Sie in PowerShell das `Set-AzureRmVmDiskEncryptionExtension`-Cmdlet, um die Verschlüsselung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="26277-159">With PowerShell, use the `Set-AzureRmVmDiskEncryptionExtension` cmdlet to enable encryption.</span></span>

```powershell

Set-AzureRmVmDiskEncryptionExtension `
    -ResourceGroupName <resource-group> `
    -VMName <vm-name> `
    -VolumeType [All | OS | Data]
    -DiskEncryptionKeyVaultId <keyVault.ResourceId> `
    -DiskEncryptionKeyVaultUrl <keyVault.VaultUri> `
     -SkipVmBackup
```

<span data-ttu-id="26277-160">Verwenden Sie für die Azure CLI den `az vm encryption enable`-Befehl, um die Verschlüsselung zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="26277-160">For the Azure CLI, use the `az vm encryption enable` command to enable encryption.</span></span>

```azurecli
az vm encryption enable \
    --resource-group <resource-group> \
    --name <vm-name> \
    --disk-encryption-keyvault <keyvault-name> \
    --volume-type [all | os | data] \
    --skipvmbackup
```

## <a name="viewing-the-status-of-the-disk"></a><span data-ttu-id="26277-161">Anzeigen des Status des Datenträgers</span><span class="sxs-lookup"><span data-stu-id="26277-161">Viewing the status of the disk</span></span>

<span data-ttu-id="26277-162">Sie können überprüfen, ob bestimmte Datenträger verschlüsselt werden oder nicht.</span><span class="sxs-lookup"><span data-stu-id="26277-162">You can check whether specific disks are encrypted or not.</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName <resource-group> -VMName <vm-name>
```

```azurecli
az vm encryption status --resource-group <resource-group> --name <vm-name>
```

<span data-ttu-id="26277-163">Beide Befehle geben den Status eines jeden an die angegebene VM angefügten Datenträgers zurück.</span><span class="sxs-lookup"><span data-stu-id="26277-163">Both of these commands will return the status of each disk attached to the specified VM.</span></span>

## <a name="decrypting-drives"></a><span data-ttu-id="26277-164">Entschlüsseln von Laufwerken</span><span class="sxs-lookup"><span data-stu-id="26277-164">Decrypting drives</span></span>

<span data-ttu-id="26277-165">Mithilfe von `Disable-AzureRmVMDiskEncryption` können Sie die Verschlüsselung durch PowerShell umkehren.</span><span class="sxs-lookup"><span data-stu-id="26277-165">You can reverse the encryption through PowerShell using `Disable-AzureRmVMDiskEncryption`.</span></span>

```powershell
Disable-AzureRmVMDiskEncryption -ResourceGroupName <resource-group> -VMName <vm-name>
```

<span data-ttu-id="26277-166">Verwenden Sie für die Azure CLI den Befehl `vm encryption disable`.</span><span class="sxs-lookup"><span data-stu-id="26277-166">For the Azure CLI, use the `vm encryption disable` command.</span></span>

```azurecli
az vm encryption disable --resource-group <resource-group> --name <vm-name>
```

<span data-ttu-id="26277-167">Diese Befehle deaktivieren die Verschlüsselungen für Volumes jeder Art für die angegebene VM.</span><span class="sxs-lookup"><span data-stu-id="26277-167">These commands disable encryption for volumes of type all for the specified virtual machine.</span></span> <span data-ttu-id="26277-168">Wie bei der Version zum Verschlüsseln können Sie den `-VolumeType`-Parameter `[All | OS | Data]` angeben, um festzulegen, welche Datenträger entschlüsselt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="26277-168">Just like the encrypt version, you can specify a `-VolumeType` parameter `[All | OS | Data]` to decide what disks to decrypt.</span></span> <span data-ttu-id="26277-169">Wenn nichts anderes angegeben wird, ist diese Einstellung standardmäßig auf `All` festgelegt.</span><span class="sxs-lookup"><span data-stu-id="26277-169">It defaults to `All` if not supplied.</span></span>

> [!WARNING]
> <span data-ttu-id="26277-170">Das Deaktivieren der Datenträgerverschlüsselung auf einer Windows-VM funktioniert nicht wie erwartet, wenn sowohl das Betriebssystem als auch die Datenträger verschlüsselt wurden.</span><span class="sxs-lookup"><span data-stu-id="26277-170">Disabling data disk encryption on Windows VM when both OS and data disks have been encrypted doesn't work as expected.</span></span> <span data-ttu-id="26277-171">Stattdessen müssen Sie die Verschlüsselung auf allen Datenträgern deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="26277-171">You must disable encryption on all disks instead.</span></span>

<span data-ttu-id="26277-172">Probieren Sie einige dieser Befehle auf einer neuen VM aus.</span><span class="sxs-lookup"><span data-stu-id="26277-172">Let's try some of these commands out on a new VM.</span></span>