In dieser Übung werden Sie einen virtuellen Computer erstellen und ändern zu können mit dem Portal und Azure PowerShell.

## <a name="create-a-vm"></a>Erstellen einer VM

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

1. Erstellen Sie eine neue Ressource im Azure-Portal. In der **neu** auf dem Blatt "," Typ **VM** in das Suchfeld ein, und drücken Sie dann die EINGABETASTE.

1. Auf der **alles** Blatt unter **Ergebnisse**, klicken Sie auf **Windows Server 2016 Datacenter**.

1. Auf der **Windows Server 2016 Datacenter** auf dem Blatt klicken Sie auf **erstellen**.

1. Auf der **Grundlagen** auf dem Blatt, füllen Sie die Details, die mit den folgenden Informationen, und klicken Sie dann auf **OK**.

    |Einstellung|Wert|
    |---|---|
    |Name|DB01|
    |Username|LocalAdmin|
    |Kennwort und Kennwortbestätigung|Adm1nPa$$word|
    |Ressourcengruppe|<rgn>[Sandkasten Resource Group-Name]</rgn>|
    |Standort|*Wählen Sie eine Region aus der Liste*|

1. Auf der **wählen Sie eine Größe** Blatt **D2s_v3**, und klicken Sie dann auf **wählen**.

1. Auf der **Einstellungen** Blatt unter **öffentliche Eingangsports hinzufügen** wählen **HTTP**, **HTTPS**, und **RDP (3389)**. Klicken Sie unter **Startdiagnose**, klicken Sie auf **deaktiviert**. Behalten Sie den Standardwert für alle anderen Einstellungen, und klicken Sie dann auf **OK**.

1. Klicken Sie auf dem Blatt **Erstellen** auf **Erstellen**.

1. Warten Sie, bis die Bereitstellung abgeschlossen ist, bevor Sie Sie in dieser Übung fortfahren.

## <a name="resize-using-the-portal"></a>Ändern der Größe über das portal

1. Navigieren Sie im Azure-Portal zur Ressourcengruppe ExerciseRG und in der **ExerciseRG** auf dem Blatt klicken Sie auf die **DB01** Objekt virtueller Maschinen.

1. Auf der **DB01** auf dem Blatt klicken Sie auf **Größe**. Beachten Sie, dass die aktuell hervorgehobene Größe die Größe, die Sie beim Erstellen des virtuellen Computers ausgewählt haben.

1. Auf der **wählen Sie eine Größe** Blatt Suchen der **F2s_v2** Größe – es sollte nicht in der Liste der Größen verfügbar, da der virtuelle Computer derzeit ausgeführt wird, und diese Größe von einer anderen Familie ist. Schließen der **wählen Sie eine Größe** Blatt.

1. In der **DB01** auf dem Blatt klicken Sie auf **beenden**. In der **diesen virtuellen Computer beenden** Dialogfeld klicken Sie auf **Ja**, und warten Sie, bis der Status der virtuellen Maschine angezeigt **beendet (Zuordnung aufgehoben)**.

1. Auf der **DB01** auf dem Blatt klicken Sie auf **Größe**. Auf der **wählen Sie eine Größe** Blatt **F2s_v2** , und klicken Sie dann auf **wählen**. Beachten Sie, dass die Benachrichtigung zum Ändern der Größe der virtuellen Computer.

1. Auf der **DB01** auf dem Blatt klicken Sie auf **Übersicht**, und klicken Sie dann auf **starten**.

## <a name="resize-using-powershell"></a>Ändern der Größe mithilfe von PowerShell

1. Öffnen Sie im Azure-Portal Azure Cloud Shell ein.

1. Verwenden Sie das folgende Cmdlet aus, um die Liste der verfügbaren Größen virtueller Computer zu erhalten.

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName ExerciseRG -VMName DB01
    ```

1. Verwenden Sie das folgende Cmdlet, um den virtuellen Computer auf eine Größe F4s_v2.

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName ExerciseRG -VMName DB01
    $vm.HardwareProfile.VmSize = "Standard_F4s_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName ExerciseRG
    ```

1. Klicken Sie auf die Schaltfläche "Aktualisieren" auf dem Blatt des DB01, während Sie, die PowerShell-Befehl warten, um den Vorgang abzuschließen. Sie sollten feststellen, dass der virtuelle Computer neu gestartet wird, um die Änderung der Größe zu ermöglichen.

In dieser Übung haben Sie einen virtuellen Computer erstellt und ihre Größe mit zwei verschiedenen Tools geändert hat. Ein guter Tipp zu bedenken ist, dass die Zielgröße möglicherweise nicht verfügbar ist, während die virtuelle Maschine ausgeführt wird. Herunterfahren des virtuellen Computers können Sie Weitere Größen wählen.