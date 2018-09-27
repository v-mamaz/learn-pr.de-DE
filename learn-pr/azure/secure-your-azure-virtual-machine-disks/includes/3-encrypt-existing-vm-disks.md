Angenommen, Ihr Unternehmen hat sich entschieden, Azure Disk Encryption (ADE) auf allen VMs zu implementieren. In diesem Fall müssen Sie evaluieren, wie Sie die Verschlüsselung auf allen vorhandenen VM-Volumes durchführen. Hier werden die Anforderungen für ADE und die Schritte zum Verschlüsseln von Datenträgern auf vorhandenen Linux- und Windows-VMs beschrieben.

## <a name="azure-disk-encryption-prerequisites"></a>Azure Disk Encryption: Voraussetzungen

Bevor Sie Ihre VM-Datenträger verschlüsseln können, müssen Sie folgende Schritte durchführen:

1. Erstellen Sie einen Schlüsseltresor.
1. Richten Sie die Zugriffsrichtlinie des Schlüsseltresors so ein, dass Datenträgerverschlüsselung unterstützt wird.
1. Verwenden Sie den Schlüsseltresor, um die Verschlüsselungsschlüssel für ADE zu speichern.

### <a name="azure-key-vault"></a>Azure Key Vault

Die von ADE verwendeten Verschlüsselungsschlüssel können in einer Azure Key Vault-Instanz gespeichert werden. Azure Key Vault ist ein Tool zum sicheren Speichern von Geheimnissen und Zugreifen darauf. Als Geheimnis werden alle Elemente bezeichnet, für die Sie den Zugriff streng kontrollieren möchten, z.B. API-Schlüssel, Kennwörter oder Zertifikate. Hiermit wird die hoch verfügbare und skalierbare sichere Speicherung in Hardwaresicherheitsmodulen (HSMs) mit Überprüfung gemäß Federal Information Processing Standards (FIPS) 140-2 Level 2 ermöglicht. Mit Key Vault erhalten Sie die vollständige Kontrolle über die Schlüssel, die zum Verschlüsseln Ihrer Daten verwendet werden, und Sie können Ihre Schlüsselnutzung verwalten und überwachen. 

> [!NOTE]
> Für Azure Disk Encryption müssen sich Ihre Key Vault-Instanz und Ihre VMs in derselben Azure-Region befinden. So wird sichergestellt, dass Verschlüsselungsgeheimnisse nicht über Grenzen von Regionen hinweg verwendet werden.

Sie können Ihren Schlüsseltresor mithilfe der folgenden Dienste konfigurieren und verwalten:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmKeyVault -Location <location> `
    -ResourceGroupName <resource-group> `
    -VaultName "myKeyVault" `
    -EnabledForDiskEncryption
```

### <a name="azure-cli"></a>die Azure CLI

```azurecli
az keyvault create \
    --name "myKeyVault" \
    --resource-group <resource-group> \
    --location <location> \
    --enabled-for-disk-encryption True
```

### <a name="azure-portal"></a>das Azure-Portal

Azure Key Vault ist eine Ressource, die im Azure-Portal mithilfe des normalen Prozesses zur Ressourcenerstellung erstellt werden kann.

1. Klicken Sie auf der Seitenleiste links auf **Ressource erstellen**.

1. Suchen Sie nach „Key Vault“. Klicken Sie im Detailfenster auf **Erstellen**.

    ![Screenshot von Key Vault im Azure Marketplace](../media/3-create-keyvault.png)

1. Geben Sie die Details für den neuen Schlüsseltresor ein:
    - Geben Sie unter **Name** einen Namen für den Schlüsseltresor ein.
    - Wählen Sie das Abonnement aus, in dem der Schlüsseltresor platziert werden soll. (Standardmäßig wird der Schlüsseltresor in Ihrem aktuellen Abonnement platziert.)
    - Wählen Sie eine **Ressourcengruppe** aus, oder erstellen Sie eine neue Ressourcengruppe, um Besitzer des Schlüsseltresors zu werden.
    - Wählen Sie einen **Standort** für den Schlüsseltresor aus. Stellen Sie sicher, dass Sie den Standort der VM auswählen.
    - Sie können zwischen den Tarifen „Standard“ und „Premium“ wählen. Der Hauptunterschied besteht darin, dass beim Tarif „Premium“ die Hardwareverschlüsselung von gesicherten Schlüsseln möglich ist.

1. Sie müssen die Zugriffsrichtlinien ändern, um die Datenträgerverschlüsselung zu unterstützen. Standardmäßig wird _Ihr Konto_ der Richtlinie hinzugefügt.
    - Wählen Sie die **Zugriffsrichtlinien** aus.
    - Klicken Sie auf **Erweiterte Zugriffsrichtlinien**.
    - Aktivieren Sie die Option **Zugriff auf Azure Disk Encryption für Volumenverschlüsselung aktivieren**.
    - Wenn Sie möchten, können Sie Ihr Konto entfernen, da es zum Verwenden des Schlüsseltresors für die Datenträgerverschlüsselung nicht erforderlich ist.
    - Klicken Sie zum Speichern der Änderungen auf **OK**.

    ![Screenshot von den erweiterten Eigenschaften für Key Vault mit aktivierter und hervorgehobener Azure Disk Encryption-Option](../media/3-configure-access-policy.png)

1. Klicken Sie auf **Erstellen**, um den neuen Schlüsseltresor zu erstellen.

## <a name="enabling-access-policies-in-the-key-vault"></a>Aktivieren von Zugriffsrichtlinien im Schlüsseltresor
Azure benötigt Zugriff auf die Verschlüsselungsschlüssel oder geheimen Schlüssel in Ihrem Schlüsseltresor, um sie für die VM zur Verfügung zu stellen, damit die Volumes gestartet und entschlüsselt werden können. Hinsichtlich des Portals wurde dies bereits weiter oben behandelt, als wir **Erweiterte Zugriffsrichtlinien** geändert haben.

Sie können drei verschiedene Richtlinien aktivieren:
1. **Datenträgerverschlüsselung:** Ist für die Azure Disk-Verschlüsselung erforderlich.
1. **Bereitstellung (Optional):** Der Ressourcenanbieter „Microsoft.Compute“ wird aktiviert, um Geheimnisse aus diesem Schlüsseltresor abzurufen, wenn auf diesen Schlüsseltresor bei der Ressourcenerstellung (z.B. beim Erstellen einer VM) verwiesen wird.
1. **Vorlagenbereitstellung (Optional):** Azure Resource Manager kann aus diesem Schlüsseltresor Geheimnisse abrufen, wenn auf diesen Schlüsseltresor in einer Vorlagenbereitstellung verwiesen wird.

Hier erfahren Sie, wie Sie die Datenträgerverschlüsselungsrichtlinie aktivieren: Die beiden anderen sind zwar ähnlich, verwenden jedoch unterschiedliche Flags.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <keyvault-name> -ResourceGroupName <resource-group> -EnabledForDiskEncryption
```

```azurecli
az keyvault update --name <keyvault-name> --resource-group <resource-group> --enabled-for-disk-encryption "true"
```

## <a name="encrypting-an-existing-vm-disk"></a>Verschlüsseln eines vorhandenen VM-Datenträgers

Nachdem Key Vault eingerichtet ist, können Sie die VM verschlüsseln, indem Sie entweder die Azure CLI oder Azure PowerShell verwenden. Beim ersten Verschlüsseln einer Windows-VM können Sie auswählen, ob Sie alle Datenträger oder nur den Betriebssystemdatenträger verschlüsseln möchten. In einigen Linux-Distributionen können nur die Datenträger für Daten verschlüsselt werden. Um für die Verschlüsselung geeignet zu sein, müssen Ihre Windows-Datenträger als NTFS-Volumes formatiert sein.

> [!WARNING]
> Sie müssen eine Momentaufnahme oder eine Sicherung von verwalteten Datenträgern erstellen, bevor Sie die Verschlüsselung aktivieren. Das unten angegebene `SkipVmBackup`-Flag weist das Tool darauf hin, dass die Sicherung auf den verwalteten Datenträgern abgeschlossen ist. Ohne die Sicherung können Sie die VM nicht wiederherstellen, wenn die Verschlüsselung aus irgendeinem Grund fehlschlägt.

Verwenden Sie in PowerShell das `Set-AzureRmVmDiskEncryptionExtension`-Cmdlet, um die Verschlüsselung zu aktivieren.

```powershell

Set-AzureRmVmDiskEncryptionExtension `
    -ResourceGroupName <resource-group> `
    -VMName <vm-name> `
    -VolumeType [All | OS | Data]
    -DiskEncryptionKeyVaultId <keyVault.ResourceId> `
    -DiskEncryptionKeyVaultUrl <keyVault.VaultUri> `
     -SkipVmBackup
```

Verwenden Sie für die Azure CLI den `az vm encryption enable`-Befehl, um die Verschlüsselung zu aktivieren.

```azurecli
az vm encryption enable \
    --resource-group <resource-group> \
    --name <vm-name> \
    --disk-encryption-keyvault <keyvault-name> \
    --volume-type [all | os | data] \
    --skipvmbackup
```

## <a name="viewing-the-status-of-the-disk"></a>Anzeigen des Status des Datenträgers

Sie können überprüfen, ob bestimmte Datenträger verschlüsselt werden oder nicht.

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName <resource-group> -VMName <vm-name>
```

```azurecli
az vm encryption status --resource-group <resource-group> --name <vm-name>
```

Beide Befehle geben den Status eines jeden an die angegebene VM angefügten Datenträgers zurück.

## <a name="decrypting-drives"></a>Entschlüsseln von Laufwerken

Mithilfe von `Disable-AzureRmVMDiskEncryption` können Sie die Verschlüsselung durch PowerShell umkehren.

```powershell
Disable-AzureRmVMDiskEncryption -ResourceGroupName <resource-group> -VMName <vm-name>
```

Verwenden Sie für die Azure CLI den Befehl `vm encryption disable`.

```azurecli
az vm encryption disable --resource-group <resource-group> --name <vm-name>
```

Diese Befehle deaktivieren die Verschlüsselungen für Volumes jeder Art für die angegebene VM. Wie bei der Version zum Verschlüsseln können Sie den `-VolumeType`-Parameter `[All | OS | Data]` angeben, um festzulegen, welche Datenträger entschlüsselt werden sollen. Wenn nichts anderes angegeben wird, ist diese Einstellung standardmäßig auf `All` festgelegt.

> [!WARNING]
> Das Deaktivieren der Datenträgerverschlüsselung auf einer Windows-VM funktioniert nicht wie erwartet, wenn sowohl das Betriebssystem als auch die Datenträger verschlüsselt wurden. Stattdessen müssen Sie die Verschlüsselung auf allen Datenträgern deaktivieren.

Probieren Sie einige dieser Befehle auf einer neuen VM aus.