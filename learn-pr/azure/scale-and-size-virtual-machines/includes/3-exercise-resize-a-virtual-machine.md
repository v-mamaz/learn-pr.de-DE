In dieser Übung erstellen Sie einen virtuellen Computer und ändern seine Größe. Dazu verwenden Sie das Portal und Azure PowerShell.

## <a name="create-a-vm"></a>Erstellen eines virtuellen Computers

1. Navigieren Sie in Ihrem Webbrowser zum [Azure-Portal](https://portal.azure.com?azure-portal=true), und melden Sie sich bei Ihrem Konto an.

1. Erstellen Sie im Azure-Portal eine neue Ressource. Geben Sie auf dem Blatt **Neu** die Zeichenfolge **virtueller Computer** in das Suchfeld ein, und drücken Sie die EINGABETASTE.

1. Klicken Sie auf dem Blatt **Alles** unter **Ergebnisse** auf **Windows Server 2016 Datacenter**.

1. Klicken Sie auf dem Blatt **Windows Server 2016 Datacenter** auf **Erstellen**.

1. Geben Sie auf dem Blatt **Grundlagen** die folgenden Informationen ein, und klicken Sie anschließend auf **OK**:

    |Einstellung|Wert|
    |---|---|
    |Name|DB01|
    |Benutzername|LocalAdmin|
    |Kennwort und Kennwortbestätigung|Adm1nPa$$word|
    |Ressourcengruppe|ExerciseRG|
    |Standort|USA, Mitte|

1. Wählen Sie auf dem Blatt **Größe auswählen** die Option **D2s_v3** aus, und klicken Sie anschließend auf **Auswählen**.

1. Wählen Sie auf dem Blatt **Einstellungen** unter **Öffentliche Eingangsports hinzufügen** die Optionen **HTTP**, **HTTPS** und **RDP (3389)** aus, klicken Sie unter **Startdiagnose** auf **Deaktiviert**, behalten Sie bei allen anderen Einstellungen die Standardwerte bei, und klicken Sie anschließend auf **OK**.

1. Klicken Sie auf dem Blatt **Erstellen** auf **Erstellen**.

1. Warten Sie, bis die Bereitstellung abgeschlossen ist, bevor Sie mit der Übung fortfahren.

## <a name="resize-using-the-portal"></a>Ändern der Größe über das Portal

1. Navigieren Sie im Azure-Portal zur Ressourcengruppe „ExerciseRG“, und klicken Sie auf dem Blatt **ExerciseRG** auf das VM-Objekt **DB01**.

1. Klicken Sie auf dem Blatt **DB01** auf **Größe**. Hinweis: Die aktuell hervorgehobene Größe ist die Größe, die Sie beim Erstellen des virtuellen Computers ausgewählt haben.

1. Suchen Sie auf dem Blatt **Größe auswählen** nach der Größe **F2s_v2**. Sie sollte in der Größenliste nicht verfügbar sein, da der virtuelle Computer momentan ausgeführt wird und die Größe zu einer anderen Familie gehört. Schließen Sie das Blatt **Größe auswählen**.

1. Klicken Sie auf dem Blatt **DB01** auf **Beenden**. Klicken Sie im Dialogfeld zum **Beenden des virtuellen Computers**auf **Ja**, und warten Sie, bis der virtuelle Computer den Status **Beendet (Zuordnung aufgehoben)** hat.

1. Klicken Sie auf dem Blatt **DB01** auf **Größe**. Wählen Sie auf dem Blatt **Größe auswählen** die Option **F2s_v2** aus, und klicken Sie anschließend auf **Auswählen**. Beachten Sie die Benachrichtigung zur Größenänderung für den virtuellen Computer.

1. Klicken Sie auf dem Blatt **DB01** auf **Übersicht** und anschließend auf **Starten**.

## <a name="resize-using-powershell"></a>Ändern der Größe mithilfe von PowerShell

1. Öffnen Sie Cloud Shell im Azure-Portal.

1. Verwenden Sie das folgende Cmdlet, um die Liste mit den verfügbaren VM-Größen abzurufen.

    ```PowerShell
    Get-AzureRmVMSize -ResourceGroupName ExerciseRG -VMName DB01
    ```

1. Verwenden Sie das folgende Cmdlet, um die Größe des virtuellen Computers in „F4s_v2“ zu ändern.

    ```PowerShell
    $vm = Get-AzureRmVM -ResourceGroupName ExerciseRG -VMName DB01
    $vm.HardwareProfile.VmSize = "Standard_F4s_v2"
    Update-AzureRmVM -VM $vm -ResourceGroupName ExerciseRG
    ```

1. Klicken Sie auf dem Blatt „DB01“ auf die Schaltfläche „Aktualisieren“, während Sie darauf warten, dass die Ausführung des PowerShell-Befehls abgeschlossen wird. Sie sollten sehen, dass der virtuelle Computer neu gestartet wird, um die Größenänderung zu implementieren.

In dieser Übung haben Sie einen virtuellen Computer erstellt und seine Größe mit zwei verschiedenen Tools geändert. Tipp: Denken Sie daran, dass die Zielgröße möglicherweise nicht verfügbar ist, solange der virtuelle Computer ausgeführt wird. Nach Beendigung des virtuellen Computers stehen mehr Größen zur Auswahl.