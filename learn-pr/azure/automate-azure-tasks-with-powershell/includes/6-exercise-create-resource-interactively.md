Wiederholen wir unser ursprüngliches Szenario – Erstellen von VMs zum Testen unserer CRM-Software. Wenn ein neuer Build verfügbar ist, möchten wir eine neue VM einrichten, damit wir die vollständige Installation anhand eines sauberen Image testen können. Wenn wir fertig sind, möchten wir Sie die VM löschen.

Probieren Sie die Befehle aus, die Sie zum Erstellen einer VM verwenden.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm-with-azure-powershell"></a>Erstellen einer Linux-VM mithilfe von Azure PowerShell

Da wir die Azure-Sandbox verwenden, müssen Sie keine Ressourcengruppe erstellen. Verwenden Sie stattdessen die Ressourcengruppe **<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>**. Achten Sie darüber hinaus auf Speicherorteinschränkungen.

Erstellen wir eine neue Azure-VM mit PowerShell.

1. Verwenden Sie das `New-AzureRmVm`-Cmdlet zum Erstellen einer VM.
    - Verwenden Sie die Ressourcengruppe **<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>**.
    - Geben Sie der VM einen Namen – verwenden Sie einen aussagekräftigen Namen, der den Zweck der VM, den Speicherort und (wenn es mehr als eine gibt) die Instanznummer angibt. Wir verwenden „testvm-eus-01“ für „Test VM in East US, instance 1“. Sie können auch einen eigenen Namen basierend auf dem VM-Speicherort eingeben.
    - Wählen Sie in der Azure-Sandbox aus der folgenden Liste einen Speicherort in Ihrer Nähe. Achten Sie darauf, den Wert im folgenden Beispielbefehl zu ändern, wenn Sie ihn kopieren und einfügen.

        [!include[](../../../includes/azure-sandbox-regions-note.md)]

    - Verwenden Sie „UbuntuLTS“ für das Image – dies ist Ubuntu Linux.
    - Verwenden Sie das `Get-Credential`-Cmdlet und geben Sie die Ergebnisse in den `Credential`-Parameter ein.
    - Fügen Sie den `-OpenPorts`-Parameter hinzu, und übergeben Sie „22“ als Port – auf diese Weise können wir SSH auf dem Computer verwenden.
 
    ```powershell
    New-AzureRmVm -ResourceGroupName <rgn>[Sandbox resource group name]</rgn> -Name "testvm-eus-01" -Credential (Get-Credential) -Location "East US" -Image UbuntuLTS -OpenPorts 22
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
    
1. Der Erstellungsvorgang dauert ein paar Minuten. Nach Abschluss können Sie einen Abfrage durchführen und das VM-Objekt einer Variable (`$vm`) zuweisen.

    ```powershell
    $vm = Get-AzureRmVM -Name "testvm-eus-01" -ResourceGroupName <rgn>[Sandbox resource group name]</rgn>
    ```
    
1. Fragen Sie anschließend den Wert ab, um die Informationen über die VM zu sichern:

    ```powershell
    $vm
    ```

    Die Ausgabe sollte folgendermaßen aussehen:

    ```output
    ResourceGroupName : <rgn>[Sandbox resource group name]</rgn>
    Id                : /subscriptions/xxxxxxxx-xxxx-aaaa-bbbb-cccccccccccc/resourceGroups/<rgn>[Sandbox resource group name]</rgn>/providers/Microsoft.Compute/virtualMachines/testvm-eus-01
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
    
1. Über eine Punktsyntax („.“) können Sie komplexe Objekte erreichen. Um beispielsweise die Eigenschaften im Objekt `VMSize` zu sehen, das dem Abschnitt „HardwareProfile“ zugeordnet ist, können Sie Folgendes eingeben:

    ```powershell
    $vm.HardwareProfile
    ```

1. Oder rufen Sie Informationen auf einem Datenträger ab:

    ```powershell
    $vm.StorageProfile.OsDisk
    ```

1. Sie können auch das VM-Objekt an andere Cmdlets übergeben. Beispielsweise können Sie so die öffentliche IP-Adresse von Ihrer VM abrufen:

    ```powershell
    $vm | Get-AzureRmPublicIpAddress
    ```

1. Über die IP-Adresse können Sie sich mit SSH mit Ihrer VM verbinden. Wenn Sie beispielsweise den Benutzernamen „bob“ verwendet haben und die IP-Adresse „205.22.16.5“ lautet, dann würde sich dieser Befehl mit dem Linux-Rechner verbinden:

```powershell
ssh bob@205.22.16.5
```

## <a name="delete-a-vm"></a>Löschen einer VM

Um weitere Befehle auszuprobieren, werden wir die VM jetzt löschen. Zunächst fahren wir sie herunter.

```powershell
Stop-AzureRmVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

Jetzt löschen wir die VM mit dem `Remove-AzureRmVM`-Cmdlet:

```powershell
Remove-AzureRmVM -Name $vm.Name -ResourceGroup $vm.ResourceGroupName
```

Verwenden Sie diesen Befehl, um die Ressourcen in Ihrer Ressourcengruppe aufzulisten:

```powershell
Get-AzureRmResource -ResourceGroupName $vm.ResourceGroupName | ft
```

Daraufhin sollte eine Reihe von Ressourcen (Datenträger, virtuellen Netzwerken usw.) angezeigt werden, die alle noch vorhanden sind. 

```output
Microsoft.Compute/disks
Microsoft.Network/networkInterfaces
Microsoft.Network/networkSecurityGroups
Microsoft.Network/publicIPAddresses
Microsoft.Network/virtualNetworks
```

Grund hierfür ist, dass mit dem `Remove-AzureRmVM`-Befehl _nur die VM gelöscht wird_. Es werden keine weiteren Ressourcen bereinigt. An dieser Stelle möchten wir nur die Ressourcengruppe löschen. Lassen Sie uns jedoch einfach die Übung durchlaufen, um sie manuell zu bereinigen. Sie sollten ein Muster in den Befehlen erkennen.

1. Löschen Sie die Netzwerkschnittstelle.

    ```powershell
    $vm | Remove-AzureRmNetworkInterface –Force
    ```
    
1. Löschen Sie den verwalteten Betriebssystemdatenträger und das Speicherkonto.

    ```powershell
    Get-AzureRmDisk -ResourceGroupName $vm.ResourceGroupName -DiskName $vm.StorageProfile.OSDisk.Name | Remove-AzureRmDisk -Force
    ```

1. Löschen Sie anschließend das virtuelle Netzwerk.

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmVirtualNetwork -Force
    ```

1. Löschen Sie die Netzwerksicherheitsgruppe.

    ```powershell
    Get-AzureRmNetworkSecurityGroup -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmNetworkSecurityGroup -Force
    ```

1. Und abschließend die öffentlichen IP-Adresse.

    ```powershell
    Get-AzureRmPublicIpAddress -ResourceGroup $vm.ResourceGroupName | Remove-AzureRmPublicIpAddress -Force
    ```

Wir sollten alle erstellten Ressourcen erfasst haben. Überprüfen Sie die Ressourcengruppe, nur um sicher zu gehen. Wir haben hier viele manuelle Befehle ausgeführt, aber ein besserer Ansatz wäre gewesen, ein _Skript_ zu schreiben, damit wir diese Logik später wiederverwenden können, um eine VM zu erstellen oder zu löschen. Schauen wir uns die Skripterstellung mit PowerShell an.