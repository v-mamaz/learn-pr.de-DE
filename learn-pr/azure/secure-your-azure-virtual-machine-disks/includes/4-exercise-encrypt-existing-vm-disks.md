Angenommen, Sie entwickeln eine Anwendung zur Finanzverwaltung für neue Startupunternehmen. Sie möchten sicherstellen, dass alle ihre Kundendaten geschützt sind, daher haben Sie sich entschieden, ADE durchgängig für alle Betriebssystem- und Daten-Datenträger auf den Servern einzusetzen, auf denen die Anwendung gehostet ist. Im Rahmen Ihrer Complianceanforderungen müssen Sie außerdem selbst für die Verwaltung Ihrer eigenen Verschlüsselungsschlüssel zuständig sein.

In dieser Übungseinheit verschlüsseln Sie Datenträger auf vorhandenen Windows-VMs und verwalten die Verschlüsselungsschlüssel mithilfe Ihres eigenen Azure Key Vaults.

> [!IMPORTANT] 
> Bei dieser Übung wird davon ausgegangen, dass Azure PowerShell auf Ihrem Computer installiert ist; Informationen zum Installieren von Azure PowerShell finden Sie unter [Installieren von Azure PowerShell unter Windows mit PowerShellGet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0).

## <a name="prepare-the-environment"></a>Vorbereiten der Umgebung

Wir beginnen, indem wir eine Windows-VM in einer neuen Ressourcengruppe bereitstellen und dann der VM einen Daten-Datenträger hinzufügen.

### <a name="deploy-windows-vm-using-azure-portal"></a>Bereitstellen eines virtuellen Windows-Computers über das Azure-Portal

Hier verwenden Sie das Azure-Portal, um einen virtuellen Windows-Computer zu erstellen und bereitzustellen. Definieren Sie zunächst die grundlegenden Informationen über den virtuellen Computer:

1. Navigieren Sie im Browser zum [Azure-Portal](http://portal.azure.com), und melden Sie sich mit Ihren normalen Anmeldeinformationen an.

1. Klicken Sie auf der Randleiste auf **Virtuelle Computer**, und klicken Sie dann auf **Virtuellen Computer erstellen**.

1. Klicken Sie auf dem Blatt „Compute“ im Abschnitt **Empfohlen** auf **Windows Server**.

1. Klicken Sie auf dem Blatt **Windows Server** auf **Windows Server 2016 Datacenter**.

1. Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.

1. Geben Sie auf dem Blatt **Grundlagen** im Feld **Name** **moneyappsvr01** ein.

1. Geben Sie in den Feldern **Benutzername** und **Kennwort** einen Namen und ein Kennwort für ein Administratorkonto auf diesem Server ein.

1. Wählen Sie im Feld **Abonnement** Ihr Azure-Abonnement aus.

1. Wählen Sie unter **Ressourcengruppe** **Neu erstellen** aus, und geben Sie im Feld **moneyapprg** ein.

1. Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.

1. Klicken Sie auf **OK**.

### <a name="choose-a-size-for-the-vm-and-start-the-deployment"></a>Wählen Sie eine Größe für die VM aus, und beginnen Sie mit der Bereitstellung.

> [!IMPORTANT]
> Beachten Sie, dass ADE im Basic-Tarif nicht unterstützt wird.

1. Wählen Sie auf dem Blatt **Größe auswählen** eine **Standard**-SKU aus, z. B. **B1s**, und klicken Sie dann auf **Auswählen**.

1. Klicken Sie auf dem Blatt **Einstellungen** in der Liste **Öffentliche Eingangsports hinzufügen** auf **RDP**, scrollen Sie dann nach unten, und klicken Sie auf **OK**.

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

1. Klicken Sie auf dem Blatt **Datenträger** auf **Speichern**. Beachten Sie, dass der Verschlüsselungsstatus des Datenträgers aktuell **_Nicht aktiviert_** ist.

## <a name="configure-disk-encryption-pre-requisites"></a>Voraussetzungen zum Konfigurieren der Datenträgerverschlüsselung

Sie verwenden jetzt das Konfigurationsskript für die Voraussetzungen zum Konfigurieren der Azure-Datenträgerverschlüsselung, um alle Voraussetzungen für die Datenträgerverschlüsselung zu konfigurieren. Durch dieses Skript wird ein Key Vault in der gleichen Region wie Ihre VM erstellt und vorbereitet.

### <a name="prepare-the-azure-disk-encryption-prerequisite-setup-script"></a>Vorbereiten des Setupskripts für Azure Disk Encryption – Voraussetzungen

1. Navigieren Sie zur GitHub-Seite [Azure Disk Encryption Prerequisite Setup Script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1) (Setupskript für Azure Disk Encryption – Voraussetzungen).

1. Klicken Sie auf der GibHub-Seite auf **Raw** (unformatiert).

1. Verwenden Sie STRG+A, um den gesamten Text auf der Seite auszuwählen, und anschließend STRG+C, um den gesamten Text auf der Seite in die Zwischenablage zu kopieren.

1. Klicken Sie auf Ihrem Computer auf **Start**, und suchen Sie dann nach **Windows PowerShell ISE**.

1. Klicken Sie mit der rechten Maustaste auf **Windows PowerShell ISE** und anschließend auf **Als Administrator ausführen**.

1. Klicken Sie im Fenster „Administrator: Windows PowerShell ISE“ auf **Ansicht** und anschließend auf **Skriptbereich anzeigen**.

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

### <a name="run-the-azure-disk-encryption-prerequisite-setup-script"></a>Ausführen des Setupskripts für Azure Disk Encryption – Voraussetzungen

1. Geben Sie im Bereich der PowerShell ISE-Konsole den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:

   ```console
   cd <path to your folder containing ADEPrereqScript.ps1>
   ```

1. Geben Sie im Bereich der PowerShell ISE-Konsole den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:

   ```powershell
   Set-ExecutionPolicy Unrestricted
   ```

   Wenn ein Dialogfeld **Ausführungsrichtlinie ändern** angezeigt wird, klicken Sie entweder auf **Alle ja** oder auf **Ja** (wenn die Option _Alle ja_ nicht angezeigt wird).

1. Geben Sie im Bereich der PowerShell ISE-Konsole den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:

   ```powershell
   Login-AzureRmAccount
   ```

1. Geben Sie Ihre Azure-Anmeldeinformationen ein.

1. Wählen Sie Ihre **Abonnement-ID**-Zeichenfolge aus, und kopieren Sie sie in die Zwischenablage.

1. Klicken Sie in der PowerShell ISE auf **Datei** und dann auf **Ausführen**.

1. Geben Sie im Konsolenfenster an der Aufforderung **resourceGroupName:** **moneyapprg** ein, und drücken Sie die **EINGABETASTE**.

1. Geben Sie im Konsolenfenster an der Aufforderung **keyVaultName:** **moneyappkv** ein, und drücken Sie die **EINGABETASTE**.

1. Geben Sie im Konsolenfenster an der Aufforderung **location:** den Speicherort ein, den Sie beim Erstellen Ihrer VM verwendet haben.

1. Fügen Sie im Konsolenfenster an der Aufforderung **subscriptionId:** Ihre Abonnement-ID ein.

1. Der **moneyappkv**-Schlüsseltresor wird jetzt erstellt. Wenn dieser Vorgang abgeschlossen ist, wählen Sie den Zusammenfassungstext aus (grün dargestellt), und kopieren Sie ihn in Editor.

1. Drücken Sie die **EINGABETASTE**, um fortzufahren.

1. Geben Sie im Konsolenfenster an der Aufforderung **aadAppName:** **moneyapp** ein, und drücken Sie die **EINGABETASTE**.

1. Die Azure AD-Anwendung **moneyapp** wird jetzt erstellt. Wenn dieser Vorgang abgeschlossen ist, wählen Sie den Zusammenfassungstext aus (grün dargestellt), und kopieren Sie ihn in Editor.

1. Drücken Sie die **EINGABETASTE**, um fortzufahren.

### <a name="encrypt-your-vm-disks-with-powershell"></a>Verschlüsseln Ihrer VM-Datenträger mit PowerShell

Überprüfen Sie den Verschlüsselungsstatus der Betriebssystem- und Daten-Datenträger:

1. Geben Sie im PowerShell ISE-Konsolenfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```powershell
    $vmName = 'moneyappsvr01'
    ```

    > [!NOTE]
    > Der Name der VM muss in einfache Anführungszeichen eingeschlossen sein.

1. Geben Sie im PowerShell ISE-Skriptfenster den folgenden Befehl ein, und drücken Sie die EINGABETASTE:

    ```powershell
    Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
    ```

1. Klicken Sie im Dialogfeld **Enable AzureDiskEncryption on the VM** (Azure-Datenträgerverschlüsselung für die VM aktivieren) auf **Ja**, und achten Sie auf die Nachricht, dass der Abschluss der Verschlüsselung 10–15 Minuten in Anspruch nehmen kann.

>[!IMPORTANT]
> Warten Sie auf den Abschluss des Befehls, bevor Sie mit dieser Übung fortfahren

### <a name="verify-the-encryption-status-of-your-vm-disks"></a>Überprüfen des Verschlüsselungsstatus Ihrer VM-Datenträger

Wechseln Sie zum Azure-Portal, und beachten Sie auf dem Blatt **Datenträger** für **moneyappsvr01**, dass der Datenträger-Verschlüsselungsstatus für die Betriebssystem- und Daten-Datenträger jetzt **Aktiviert** ist.
