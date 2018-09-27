In dieser Übung erstellen Sie einen virtuellen Computer und ändern seine Größe. Dazu verwenden Sie das Portal und Azure PowerShell.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-vm-with-powershell"></a>Erstellen eines virtuellen Computers mit PowerShell

1. Verwenden Sie das Cmdlet `New-AzureRmVm` in Azure PowerShell, um einen virtuellen Computer zu erstellen.
    - Verwenden Sie die Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.
    - Nennen Sie ihn „my-test-vm“.
    - Übergeben Sie _Standard_DS2_v2_ für den **Size**-Parameter.
    - Wählen Sie in der Azure-Sandbox aus der folgenden Liste einen Standort in Ihrer Nähe aus. Achten Sie darauf, den Wert im folgenden Beispielbefehl zu ändern, wenn Sie ihn kopieren und einfügen.

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - Verwenden Sie das `Get-Credential`-Cmdlet, und geben Sie die Ergebnisse wie unten gezeigt in den `Credential`-Parameter ein.

       Wenn Sie zur Eingabe der Anmeldeinformationen aufgefordert werden, verwenden Sie „LocalAdmin“ als Benutzernamen und „Adm1nPa$$Word“ als Kennwort.

    ```powershell
    New-AzureRmVm `
        -ResourceGroupName <rgn>[sandbox resource group name]</rgn> `
        -Name my-test-vm `
        -Credential (Get-Credential) `
        -Size "Standard_DS2_v2" `
        -Location eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


1. Warten Sie, bis die Bereitstellung abgeschlossen ist, bevor Sie mit der Übung fortfahren.

## <a name="resize-using-the-portal"></a>Ändern der Größe über das Portal

1. Melden Sie sich beim [Azure-Portal für die Sandbox](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit demselben Konto an, über das Sie die Sandbox aktiviert haben.

1. Wählen Sie in der linken Seitenleiste **Ressourcengruppen** aus.

1. Wählen Sie die Ressourcengruppe <rgn>[Name der Sandboxressourcengruppe]</rgn> aus, und klicken Sie in der Übersicht auf das virtuelle Computerobjekt **my-test-vm**.

1. Beachten Sie in der **Übersicht** des virtuellen Computers, dass die aktuelle Größe der VM _Standard DS2 v2 (2 vCPUs, 7 GB Arbeitsspeicher)_ entspricht. Dabei handelt es sich um die VM, die Sie vorhin erstellt haben.

1. Klicken Sie im Abschnitt **Einstellungen** auf die Option **Größe**.

1. Suchen Sie auf dem Blatt **Größe auswählen** nach der Größe **F2s_v2**. Sie werden sie nicht in der Liste der verfügbaren Größen finden, da die VM derzeit ausgeführt wird und die Größe aus einer anderen Familie stammt. In einigen Fällen müssen Sie die VM beenden, um alle verfügbaren VM-Größen anzeigen zu können.

1. Wählen Sie eine Größe aus, die verfügbar ist, während dieser virtuelle Computer ausgeführt wird. Wählen Sie auf dem Blatt **Größe auswählen** die Option _DS3_v2 Standard_ aus, und klicken Sie anschließend auf **Auswählen**. Beachten Sie die Benachrichtigung zur Größenänderung für den virtuellen Computer.

1. Bestätigen Sie auf dem Panel **Übersicht**, dass die Größe der VM in _Standard DS3 v2 (4 vCPUs, 14 GB Arbeitsspeicher)_ geändert wurde.

## <a name="resize-using-powershell"></a>Ändern der Größe mithilfe von PowerShell

1. Öffnen Sie im Azure-Portal Azure Cloud Shell, indem Sie auf die Cloud Shell-Schaltfläche in der oberen Symbolleiste klicken.

    Stellen Sie oben links im Cloud Shell-Fenster sicher, dass die Cloud Shell automatisch PowerShell verwendet, nicht Bash.

1. Verwenden Sie das folgende Cmdlet, um die Liste mit den verfügbaren VM-Größen abzurufen.

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -VMName my-test-vm
    ```

1. Verwenden Sie das folgende Cmdlet, um die Größe des virtuellen Computers in _DS2_v2_ zurückzuändern.

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName <rgn>[sandbox resource group name]</rgn> -VMName my-test-vm
    $vm.HardwareProfile.VmSize = "Standard_DS2_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName <rgn>[sandbox resource group name]</rgn>
    ```

1. Klicken Sie auf dem Blatt **my-test-vm** auf die Schaltfläche **Aktualisieren**, während Sie darauf warten, dass der PowerShell-Befehl zu Ende ausgeführt wird. Der virtuelle Computer sollte nun neu gestartet werden, um die Größenänderung zu ermöglichen.

In dieser Übung haben Sie einen virtuellen Computer erstellt und seine Größe mit zwei verschiedenen Tools geändert. Tipp: Denken Sie daran, dass die Zielgröße möglicherweise nicht verfügbar ist, solange der virtuelle Computer ausgeführt wird. Nach Beendigung des virtuellen Computers stehen mehr Größen zur Auswahl.