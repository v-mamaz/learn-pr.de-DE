Angenommen, Sie entwickeln eine Anwendung zur Finanzverwaltung für neue Startupunternehmen. Sie möchten sicherstellen, dass all ihre Kundendaten geschützt sind. Daher haben Sie sich entschieden, Azure Disk Encryption (ADE) durchgängig für alle (Betriebssystem-)Datenträger auf den Servern einzusetzen, auf denen die Anwendung gehostet ist. Im Rahmen Ihrer Complianceanforderungen müssen Sie zudem selbst die Verantwortung für die Verwaltung Ihrer eigenen Verschlüsselungsschlüssel tragen.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

In dieser Einheit verschlüsseln Sie Datenträger auf vorhandenen virtuellen Computern und verwalten die Verschlüsselungsschlüssel mithilfe Ihrer eigenen Azure Key Vault-Instanz.

## <a name="prepare-the-environment"></a>Vorbereiten der Umgebung

Zunächst wird ein neuer virtueller Windows-Computer auf einem virtuellen Azure-Computer bereitgestellt.

### <a name="deploy-windows-vm"></a>Bereitstellen eines virtuellen Windows-Computers

Erstellen Sie einen neuen virtuellen Windows-Computer mit Azure PowerShell, und stellen Sie diesen bereit.

1. Überlegen Sie zunächst, wo die neuen Ressourcen untergebracht werden sollen. Wählen Sie aus der folgenden Liste einen Standort in Ihrer Nähe aus.

    <!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]
    

1. Definieren Sie eine PowerShell-Variable, die den ausgewählten Standort enthalten soll. Hier ist „USA, Osten“ als Standort definiert. Ändern Sie diese Angabe in Ihren bevorzugten Standort.

    ```powershell
    $location = "eastus"
    ```
    
    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. Definieren Sie als Nächstes einige zweckdienlichere Variablen zum Erfassen des _Namens_ des virtuellen Computers sowie der _Ressourcengruppe_. Beachten Sie, dass hier die vorab erstellte Ressourcengruppe verwendet wird. Normalerweise würden Sie in Ihrem Abonnement mithilfe von `New-AzureRmResourceGroup` eine _neue_ Ressourcengruppe erstellen.

    ```powershell
    $vmName = "fmdata-vm01"
    $rgName = "<rgn>[sandbox Resource Group]</rgn>"
    ```
    
1. Erstellen Sie mit `New-AzureRmVm` einen neuen virtuellen Computer.
    
    ```powershell
    New-AzureRmVm `
        -ResourceGroupName $rgName `
        -Name $vmName `
        -Location $location `
        -OpenPorts 3389
    ```
    
    Geben Sie einen Benutzernamen und ein Kennwort für den virtuellen Computer ein, wenn Sie von Cloud Shell dazu aufgefordert werden. Diese werden für das erste Konto verwendet, das für den virtuellen Computer erstellt wird.
    
    > [!NOTE]
    > Dieser Befehl verwendet einige Standardeinstellungen, da eine Reihe von Optionen nicht bereitgestellt wurde. Dadurch wird insbesondere ein _Windows 2016 Server_-Image mit der Größe _Standard_DS1_v2_ erstellt. Beachten Sie, dass die virtuellen Computer der Basisebene ADE nicht unterstützen, wenn Sie die Größe des virtuellen Computer angeben möchten.

1. Sobald der virtuelle Computer die Bereitstellung abgeschlossen hat, können Sie die Details zum virtuellen Computer in einer Variablen erfassen. Sie können mithilfe dieser Variable die erstellten Komponenten untersuchen.

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```
    
1. Sie können den an den virtuellen Computer angefügten Betriebssystem-Datenträger sehen:

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
        
1. Überprüfen Sie den aktuellen Status der Verschlüsselung auf dem Betriebssystem-Datenträger (und auf allen anderen Datenträgern).

    ```powershell
    Get-AzureRmVmDiskEncryptionStatus  `
        -ResourceGroupName $rgName `
        -VMName $vmName
    ```

    Wie Sie sehen können, sind die Datenträger aktuell _unverschlüsselt_. 

    ```output
    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : NotEncrypted
    OsVolumeEncryptionSettings :
    ProgressMessage            : No Encryption extension or metadata found on the VM
    ```
    
Ändern wir das.
    
## <a name="encrypt-the-vm-disks-with-azure-disk-encryption"></a>Verschlüsseln der Datenträger des virtuellen Computers mithilfe von Azure Disk Encryption

Da wir diese Daten schützen müssen, sollten wir die Datenträger verschlüsseln. Denken Sie daran, dass hierzu mehrere Schritte erforderlich sind:

1. Erstellen Sie einen Schlüsseltresor.
1. Richten Sie den Schlüsseltresor so ein, dass Datenträgerverschlüsselung unterstützt wird.
1. Erteilen Sie Azure den Befehl, die Datenträger des virtuellen Computers mithilfe des im Schlüsseltresor gespeicherten Schlüssels zu verschlüsseln.

> [!TIP]
> Wir werden uns die Schritte im Detail ansehen. Wenn Sie diese Aufgabe jedoch in Ihrem eigenen Abonnement ausführen, können Sie ein praktisches PowerShell-Skript verwenden, das in der Zusammenfassung dieses Moduls verlinkt ist.

### <a name="create-a-key-vault"></a>Erstellen eines Schlüsseltresors

Zum Erstellen einer Azure Key Vault-Instanz müssen wir den Dienst in unserem Abonnement aktivieren. Dies ist eine einmalige Anforderung.

> [!TIP]
> Je nach Abonnement müssen Sie möglicherweise den **Microsoft.KeyVault**-Anbieter mit dem `Register-AzureRmResourceProvider`-Cmdlet aktivieren. Dies ist beim Azure-Sandboxabonnement nicht erforderlich.

1. Geben Sie Ihrem neuen Schlüsseltresor einen Namen. Der Name muss eindeutig sein, zwischen 3 und 24 Zeichen lang sein und sich aus Zahlen, Buchstaben und Bindestrichen zusammensetzen. Versuchen Sie, einige Zufallszahlen am Ende hinzuzufügen, durch die die nachfolgend aufgeführte Zahl „1234“ ersetzt wird.

    ```powershell
    $keyVaultName = "mvmdsk-kv-1234"
    ```
        
1. Erstellen Sie mit `New-AzureRmKeyVault` eine Azure Key Vault-Instanz.
    - Stellen Sie sicher, dass sich diese in derselben Ressourcengruppe _und_ am selben Ort wie Ihr virtueller Computer befindet.
    - Aktivieren Sie die Key Vault-Instanz für die Verwendung mit der Datenträgerverschlüsselung. 
    - Geben Sie einen eindeutigen Namen für die Key Vault-Instanz an.

    ```powershell
    New-AzureRmKeyVault -VaultName $keyVaultName `
        -Location $location `
        -ResourceGroupName $rgName `
        -EnabledForDiskEncryption
    ```

    Nach der Ausführung dieses Befehls wird eine Warnung angezeigt, in der darauf hingewiesen wird, dass kein Benutzer Zugriff hat.

    ```output
    WARNING: Access policy is not set. No user or application have access permission to use this vault. This can happen if the vault was created by a service principal. Please use Set-AzureRmKeyVaultAccessPolicy to set access policies.
    ```

    Dies ist kein Problem, da der Tresor nur verwendet wird, um die Verschlüsselungsschlüssel für den virtuellen Computer zu speichern, und die Benutzer nicht auf diese Daten zugreifen müssen.

### <a name="encrypt-the-disk"></a>Verschlüsseln des Datenträgers

Sie können gleich mit der Verschlüsselung der Datenträger beginnen. Zuvor jedoch ein Wort der Warnung hinsichtlich der Erstellung von Sicherungen:

> [!IMPORTANT]
> Wenn es sich hierbei um ein Produktionssystem handeln würde, müssten Sie eine Sicherung der verwalteten Datenträger vornehmen – entweder mit Azure Backup oder durch das Erstellen einer Momentaufnahme. Sie können Momentaufnahmen im Azure-Portal oder über die Befehlszeile erstellen. Verwenden Sie in PowerShell das `New-AzureRmSnapshot`-Cmdlet. Da dies eine einfache Übung ist und wir diese Daten löschen werden, wenn Sie fertig sind, werden wir diesen Schritt überspringen. 

1. Definieren Sie zunächst eine Variable zum Speichern der Key Vault-Informationen.

    ```powershell
    $keyVault = Get-AzureRmKeyVault `
        -VaultName $keyVaultName `
        -ResourceGroupName $rgName
    ```

1. Verwenden Sie anschließend das `Set-AzureRmVmDiskEncryptionExtension`-Cmdlet, um die Datenträger des virtuellen Computers zu verschlüsseln.
    - Mithilfe des Parameters `VolumeType` können Sie angeben, welche Datenträger verschlüsselt werden sollen: [_All (Alle)_ | _OS (Betriebssystem)_ | _Data (Daten)_]. Der Standardwert ist _All_ (Alle). Datenträger können nicht unter allen Linux-Distributionen verschlüsselt werden.
    - Sie müssen für verwaltete Datenträger das Flag `SkipVmBackup` angeben. Andernfalls schlägt der Befehl fehl, da keine Momentaufnahme vorhanden ist.

    ```powershell
    Set-AzureRmVmDiskEncryptionExtension `
        -ResourceGroupName $rgName `
        -VMName $vmName `
        -VolumeType All `
        -DiskEncryptionKeyVaultId $keyVault.ResourceId `
        -DiskEncryptionKeyVaultUrl $keyVault.VaultUri `
        -SkipVmBackup
    ```

1. Dieses Cmdlet gibt als Warnung aus, dass der virtuelle Computer offline geschaltet werden muss und der Vorgang einige Minuten in Anspruch nehmen kann. Setzen Sie den Vorgang fort.

    ```output
    Enable AzureDiskEncryption on the VM
    This cmdlet prepares the VM and enables encryption which may reboot the machine and takes 10-15 minutes to
    finish. Please save your work on the VM before confirming. Do you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
    ```
    
1. Überprüfen Sie nach Abschluss des Vorgangs erneut den Verschlüsselungsstatus.

    ```powershell
    Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
    ```

    Der Betriebssystem-Datenträger sollte jetzt verschlüsselt sein. Sämtliche angefügte Datenträger, die für Windows sichtbar sind, werden ebenfalls verschlüsselt.

    ```output
    OsVolumeEncrypted          : Encrypted
    DataVolumesEncrypted       : NoDiskFound
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : Provisioning succeeded
    ```

> [!NOTE]        
> Werden nach der Verschlüsselung neue Datenträger hinzugefügt, werden diese _nicht_ automatisch verschlüsselt. Sie können das `Set-AzureRmVMDiskEncryptionExtension`-Cmdlet erneut ausführen, um die neuen Datenträger zu verschlüsseln. Achten Sie darauf, eine neue Sequenznummer anzugeben, wenn Sie Datenträger einem virtuellen Computer hinzufügen, auf dem bereits Datenträger verschlüsselt wurden. Beachten Sie außerdem, dass Datenträger, die nicht für das Betriebssystem sichtbar sind, nicht verschlüsselt werden. Der Datenträger muss ordnungsgemäß partitioniert, formatiert und eingebunden sein, damit er von der BitLocker-Erweiterung erkannt wird.