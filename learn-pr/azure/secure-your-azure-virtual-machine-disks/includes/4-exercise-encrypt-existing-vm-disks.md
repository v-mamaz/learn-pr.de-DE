Angenommen, Sie entwickeln eine Anwendung zur Finanzverwaltung für neue Startupunternehmen. Sie möchten, stellen Sie sicher, dass die Daten Ihrer Kunden geschützt ist, damit Sie sich entschieden haben, um Azure Disk Encryption (ADE) auf allen Datenträgern mit Betriebssystem und Daten auf den Servern zu implementieren, die diese Anwendung hostet. Im Rahmen Ihrer Complianceanforderungen müssen Sie außerdem selbst für die Verwaltung Ihrer eigenen Verschlüsselungsschlüssel zuständig sein.

Sie werden in dieser Einheit Verschlüsseln von Datenträgern auf vorhandene Windows-VMs und Verwaltung der Verschlüsselungsschlüssel, die mit Ihren eigenen Azure Key Vault.

> [!IMPORTANT] 
> In dieser Übung wird davon ausgegangen, dass Azure PowerShell auf Ihrem Computer installiert ist. Wechseln Sie zu [Installieren des Azure PowerShell unter Windows mit PowerShellGet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0) Informationen dazu, wie Sie Azure PowerShell installieren.

## <a name="prepare-the-environment"></a>Vorbereiten der Umgebung

Wir starten, indem Sie eine Windows-VM bereitstellen, um eine neue Ressourcengruppe, und fügen Sie dann mit dem virtuellen Computer einen Datenträger hinzu.

### <a name="deploy-windows-vm-using-the-azure-portal"></a>Bereitstellen von Windows-VM über das Azure-portal

Hier verwenden Sie das Azure-Portal zum Erstellen und Bereitstellen einer Windows-VM. Definieren Sie zunächst die grundlegenden Informationen über den virtuellen Computer:

1. Navigieren Sie im Browser zum [Azure-Portal](http://portal.azure.com), und melden Sie sich mit Ihren normalen Anmeldeinformationen an.

1. Klicken Sie auf der Randleiste auf **Virtuelle Computer**, und klicken Sie dann auf **Virtuellen Computer erstellen**.

1. Klicken Sie auf dem Blatt „Compute“ im Abschnitt **Empfohlen** auf **Windows Server**.

1. Klicken Sie auf dem Blatt **Windows Server** auf **Windows Server 2016 Datacenter**.

1. Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.

1. Geben Sie auf dem Blatt **Grundlagen** im Feld **Name** **moneyappsvr01** ein.

1. Geben Sie in den Feldern **Benutzername** und **Kennwort** einen Namen und ein Kennwort für ein Administratorkonto auf diesem Server ein.

1. Wählen Sie im Feld **Abonnement** Ihr Azure-Abonnement aus.

1. Klicken Sie unter **Ressourcengruppe**Option **neu erstellen**. Geben Sie im Feld **Moneyapprg**.

1. Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.

1. Klicken Sie auf **OK**.

### <a name="choose-a-size-for-the-vm-and-start-the-deployment"></a>Wählen Sie eine Größe für die VM aus, und beginnen Sie mit der Bereitstellung.

> [!IMPORTANT]
> Denken Sie daran, dass ADE von Tarif "basic"-VMs nicht unterstützt werden.

1. Auf der **wählen Sie eine Größe** Blatt eine **Standard** SKU, z. B. **B1s**. Klicken Sie dann auf **Auswählen**.

1. Auf der **Einstellungen** Blatt in der **öffentliche Eingangsports hinzufügen** auf **RDP**. Scrollen Sie nach unten, und klicken Sie auf **OK**.

1. Klicken Sie auf dem Blatt **Erstellen** auf **Erstellen**.

1. Warten Sie die Bereitstellung des virtuellen Computers ab, bevor Sie mit der Übung fortfahren.

### <a name="add-a-data-disk-to-the-vm"></a>Hinzufügen eines Datenträgers zur VM

1. Klicken Sie im linken Menü auf **Alle Ressourcen** und dann auf **moneyappsvr01**.

1. Klicken Sie auf dem Blatt **Virtueller Computer** unter **EINSTELLUNGEN** auf **Datenträger**.

1. Beachten Sie auf dem Blatt **Datenträger**, dass der Verschlüsselungsstatus des Betriebssystem-Datenträgers aktuell **Nicht aktiviert** ist, und klicken Sie dann auf **Datenträger hinzufügen**.

1. Klicken Sie in die Liste **Namen**, und klicken Sie dann auf **Datenträger erstellen**.

1. Geben Sie auf dem Blatt **Verwalteten Datenträger erstellen** im Feld **Name** **moneyappsvr01_data** ein.

1. Wählen Sie unter **Ressourcengruppe** **Vorhandene verwenden** aus, und wählen Sie in der Liste **moneyapprg** aus.

1. Klicken Sie auf **Erstellen**.

1. Warten Sie, bis der Datenträger erstellt wurde, bevor Sie fortfahren.

1. Klicken Sie auf dem Blatt **Datenträger** auf **Speichern**. Beachten Sie, dass der Status der Verschlüsselung der Datenträger befindet sich derzeit **nicht aktiviert**.

## <a name="configure-disk-encryption-prerequisites"></a>Disk Encryption erforderliche konfigurieren

Sie verwenden jetzt die Azure Disk Encryption erforderliche Konfigurationsskript, um alle Disk Encryption erforderliche konfigurieren. Dieses Skript erstellt und eine Key Vault-Instanz in der gleichen Region wie Ihr virtueller Computer vorbereiten.

### <a name="prepare-the-azure-disk-encryption-prerequisite-setup-script"></a>Vorbereiten der Azure Disk Encryption erforderliche Setupskript

1. Wechseln Sie zu der [Azure Disk Encryption erforderliche Setupskript](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1) GitHub-Seite.

1. Klicken Sie auf der GibHub-Seite auf **Raw** (unformatiert).

1. Verwenden Sie STRG + A Markieren Sie den Text auf der Seite, und klicken Sie dann STRG + C verwenden, um den gesamten Text auf der Seite in die Zwischenablage zu kopieren.

1. Klicken Sie auf dem Computer, auf **starten**, und navigieren Sie zum **Windows PowerShell ISE**.

1. Mit der rechten Maustaste **Windows PowerShell ISE**, und klicken Sie auf **als Administrator ausführen**.

1. In der Administrator: Windows PowerShell ISE-Fensters, klicken Sie auf **Ansicht**, und klicken Sie dann auf **Skriptbereich anzeigen**.

1. Fügen Sie den kopierten Text in den Skriptbereich ein.

1. Suchen Sie im Skriptbereich nach dem folgenden Codeblock:

    ```powershell
    [Parameter(Mandatory = $false,
            HelpMessage="Name of the AAD application that will be used to write secrets to KeyVault. A new application with this name will be created if one doesn't exist. If this app already exists, pass aadClientSecret parameter to the script")]
    [ValidateNotNullOrEmpty()]
    [string]$aadAppName,
    ```
1. Ändern Sie im Codeblock `$false` in `$true`.

1. Klicken Sie auf **Datei**, klicken Sie dann auf **Speichern**, und navigieren Sie zu dem Ordner, den Sie zum Speichern des Skripts verwenden möchten.

1. Geben Sie im Feld **Dateiname** **ADEPrereqScript.ps1** ein, und klicken Sie auf **Speichern**.

### <a name="run-the-azure-disk-encryption-prerequisite-setup-script"></a>Führen Sie die Azure Disk Encryption erforderliche Setupskript

1. In der PowerShell ISE-Konsole im Bereich "," Geben Sie den folgenden Befehl, und drücken Sie **EINGABETASTE**:

   ```console
   cd <path to your folder containing ADEPrereqScript.ps1>
   ```

1. In der PowerShell ISE-Konsole im Bereich "," Geben Sie den folgenden Befehl, und drücken Sie **EINGABETASTE**:

   ```powershell
   Set-ExecutionPolicy Unrestricted
   ```

   Wenn ein Dialogfeld **Ausführungsrichtlinie ändern** angezeigt wird, klicken Sie entweder auf **Alle ja** oder auf **Ja** (wenn die Option _Alle ja_ nicht angezeigt wird).

1. In der PowerShell ISE-Konsole im Bereich "," Geben Sie den folgenden Befehl, und drücken Sie **EINGABETASTE**:

   ```powershell
   Login-AzureRmAccount
   ```

1. Geben Sie Ihre Azure-Anmeldeinformationen ein.

1. Wählen Sie Ihre **Abonnement-ID**-Zeichenfolge aus, und kopieren Sie sie in die Zwischenablage.

1. Klicken Sie in der PowerShell ISE auf **Datei**, und klicken Sie dann auf **ausführen**.

1. In der Konsolenstruktur unter den **ResourceGroupName:** dazu aufgefordert werden, geben Sie **Moneyapprg**. Drücken Sie dann die **EINGABETASTE**.

1. In der Konsolenstruktur unter den **KeyVaultName:** dazu aufgefordert werden, geben Sie **Moneyappkv**. Drücken Sie dann die **EINGABETASTE**.

1. Geben Sie im Konsolenfenster an der Aufforderung **location:** den Speicherort ein, den Sie beim Erstellen Ihrer VM verwendet haben.

1. Fügen Sie im Konsolenfenster an der Aufforderung **subscriptionId:** Ihre Abonnement-ID ein.

1. Der **moneyappkv**-Schlüsseltresor wird jetzt erstellt. Wenn dieser Vorgang abgeschlossen ist, wählen Sie den Zusammenfassungstext aus (grün dargestellt), und kopieren Sie ihn in Editor.

1. Drücken Sie **EINGABETASTE** um den Vorgang fortzusetzen.

1. In der Konsolenstruktur unter den **AadAppName:** dazu aufgefordert werden, geben Sie **Moneyapp**. Drücken Sie dann die **EINGABETASTE**.

1. Die Azure AD-Anwendung **moneyapp** wird jetzt erstellt. Wenn dieser Vorgang abgeschlossen ist, wählen Sie den Zusammenfassungstext aus (grün dargestellt), und kopieren Sie ihn in Editor.

1. Drücken Sie **EINGABETASTE** um den Vorgang fortzusetzen.

### <a name="encrypt-your-vm-disks-with-powershell"></a>Verschlüsseln Ihrer VM-Datenträger mit PowerShell

Überprüfen Sie den Verschlüsselungsstatus der Betriebssystem- und Daten-Datenträger:

1. In der PowerShell ISE-Konsole im Bereich "," Geben Sie den folgenden Befehl, und drücken Sie **EINGABETASTE**:

    ```powershell
    $vmName = 'moneyappsvr01'
    ```

    > [!NOTE]
    > Der Name der VM muss in einfache Anführungszeichen eingeschlossen sein.

1. In der PowerShell ISE-Skriptbereich, geben Sie in den folgenden Befehl aus, und drücken Sie **EINGABETASTE**:

    ```powershell
    Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
    ```

1. Klicken Sie im Dialogfeld **Enable AzureDiskEncryption on the VM** (Azure-Datenträgerverschlüsselung für die VM aktivieren) auf **Ja**, und achten Sie auf die Nachricht, dass der Abschluss der Verschlüsselung 10–15 Minuten in Anspruch nehmen kann.

>[!IMPORTANT]
> Warten Sie, bis der Befehl ausgeführt wurde, bevor Sie mit dieser Übung fortfahren.

### <a name="verify-the-encryption-status-of-your-vm-disks"></a>Überprüfen des Verschlüsselungsstatus Ihrer VM-Datenträger

Wechseln Sie zum Azure-Portal. Auf der **Datenträger** Blatt **moneyappsvr01**, beachten Sie, dass der Status der datenträgerverschlüsselung für den Betriebssystemdatenträger und sonstige Datenträger jetzt **aktiviert**.
