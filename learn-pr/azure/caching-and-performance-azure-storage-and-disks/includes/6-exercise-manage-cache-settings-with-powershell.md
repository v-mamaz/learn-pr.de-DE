In der vorherigen Übung haben wir mit dem Azure-Portal die folgenden Aufgaben durchgeführt:

- Anzeigen des Cachestatus für den Betriebssystemdatenträger
- Ändern der Cacheeinstellungen des Betriebssystemdatenträgers
- Hinzufügen eines Datenträgers zum virtuellen Computer
- Ändern des Cachetyps auf einem neuen Datenträger

Wir üben diese Vorgänge nun mit Azure PowerShell. 

> [!NOTE]
> Wir werden Azure PowerShell verwenden, aber Sie können auch die Azure-Befehlszeilenschnittstelle verwenden, deren Funktionalität einem Tool auf Konsolenbasis ähnelt. Sie wird unter macOS, Linux und Windows ausgeführt. Weitere Informationen über die Azure-Befehlszeilenschnittstelle erfahren Sie in dem Modul **Verwalten von virtuellen Computern mit der Azure CLI**.

Wir verwenden den virtuellen Computer, den wir in der vorherigen Übung erstellt haben. Für die Vorgänge in dieser Übung wird Folgendes vorausgesetzt:

- Der virtuelle Computer ist vorhanden und hat den Namen **fotoshareVM**.
- Der virtuelle Computer ist in einer Ressourcengruppe mit dem Namen **<rgn>[Name der Sandboxressourcengruppe]</rgn>** enthalten.

Falls Sie andere Namen verwendet haben, können Sie diese Werte entsprechend ersetzen.

Hier ist der aktuelle Status unserer VM-Datenträger aus der letzten Übung angegeben:

![Screenshot: Betriebssystemdatenträger und Datenträger, jeweils mit schreibgeschütztem Zwischenspeichern.](../media/disks-final-config-portal.PNG)

Wir haben das Portal verwendet, um das Feld **HOSTZWISCHENSPEICHERUNG** für den Betriebssystemdatenträger und den Datenträger für Daten festzulegen. Behalten Sie diesen Ausgangszustand im Hinterkopf, während wir die folgenden Schritte durcharbeiten.

### <a name="set-up-some-variables"></a>Einrichten einiger Variablen

Zuerst speichern wir einige Ressourcennamen zur späteren Verwendung.

1. Verwenden Sie das Azure Cloud Shell-Terminalfenster auf der rechten Seite, um die folgenden PowerShell-Befehle auszuführen:

    > [!NOTE]
    > Falls noch nicht geschehen, wechseln Sie von der Cloud Shell-Sitzung zu **PowerShell**, bevor Sie diese Befehle ausprobieren.
    
    ```powershell
    $myRgName = "<rgn>[sandbox resource group name]</rgn>"
    $myVMName = "fotoshareVM"
    ```
    
    > [!TIP]
    > Sie müssen diese Variablen erneut festlegen, wenn der Timeout für Ihre Cloud Shell-Sitzung erreicht ist. Nach Möglichkeit sollten Sie die gesamte Übung also in einer Sitzung durcharbeiten.
    
### <a name="get-info-about-our-vm"></a>Abrufen von Informationen zum virtuellen Computer

1. Führen Sie den folgenden Befehl aus, um die Eigenschaften des virtuellen Computers abzurufen:

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVmName
    ```
    
1. Wir speichern die Antwort in der Variablen `$myVM`. Wir können die Ausgabe an das `select-object`-Cmdlet weiterreichen, um die Anzeige nach bestimmten Eigenschaften zu filtern:

    ```powershell
    $myVM | select-object -property ResourceGroupName, Name, Type, Location
    ```
    
1. Folgendes sollte angezeigt werden:

    ```output
    ResourceGroupName Name        Type                              Location
    ----------------- ----        ----                              --------
    <rgn>[sandbox resource group name]</rgn> fotoshareVM Microsoft.Compute/virtualMachines eastus
    ```
    
### <a name="view-os-disk-cache-status"></a>Anzeigen des Cachestatus für den Betriebssystemdatenträger

1. Wir können die Cacheeinstellung wie folgt über das `StorageProfile`-Objekt überprüfen:

    ```powershell
    $myVM.StorageProfile.OsDisk.Caching
    ```

    ```output
    ReadOnly
    ```
   
1. Wir ändern ihn wieder in die Standardeinstellung _ReadWrite_ für einen Betriebssystemdatenträger.

### <a name="change-the-cache-settings-of-the-os-disk"></a>Ändern der Cacheeinstellungen des Betriebssystemdatenträgers

1. Wir können den Wert für den Cachetyp wie folgt mithilfe desselben `StorageProfile`-Objekts festlegen:

    ```powershell
    $myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
    ```
    
    Dieser Befehl wird schnell ausgeführt. Dies deutet darauf hin, dass der Vorgang lokal erfolgt. Mit dem Befehl wird nur die Eigenschaft für das `myVM`-Objekt geändert. Wie im folgenden Screenshot zu sehen ist, gilt Folgendes: Wenn Sie die Variable `$myVM` aktualisieren, indem Sie sie mit dem `Get-AzureRmVM`-Cmdlet neu zuweisen, hat sich der Cachewert für den virtuellen Computer nicht geändert.

1. Rufen Sie `Update-AzureRmVM` wie folgt auf, um die Änderung auf dem virtuellen Computer durchzuführen:

    ```powershell
    Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
    Beachten Sie, dass es eine Weile dauert, bis dieser Aufruf abgeschlossen ist. Dies liegt daran, dass wir den eigentlichen virtuellen Computer aktualisieren und Azure den virtuellen Computer neu startet, um die Änderung vorzunehmen.

    ```output
    RequestId IsSuccessStatusCode StatusCode ReasonPhrase
    --------- ------------------- ---------- ------------
                             True         OK OK
    ```
    
1. Wenn Sie die Variable `$myVM` erneut aktualisieren, sehen Sie die Änderung für das Objekt. Wenn Sie sich den Datenträger im Portal ansehen, können Sie die Änderung dort auch erkennen. 

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVmName
    $myVM.StorageProfile.OsDisk.Caching
    ```
    
    ```output
    ReadWrite
    ```
    
### <a name="list-data-disk-info"></a>Auflisten von Datenträgerinformationen

1. Führen Sie den folgenden Befehl aus, um anzuzeigen, welche für Daten bestimmte Datenträger auf unserem virtuellen Computer vorhanden sind:

    ```powershell
    $myVM.StorageProfile.DataDisks
    ```
    
    ```output
    Name            : fotosharesVM-data
    DiskSizeGB      : 1023
    Lun             : 0
    Caching         : ReadOnly
    CreateOption    : Attach
    SourceImage     :
    VirtualHardDisk :
    ```
    
Derzeit wird nur ein Datenträger für Daten verwendet. Das Feld `Lun` ist wichtig. „Lun“ steht für die eindeutige „**L**ogical **U**nit **N**umber“ (Logische Gerätenummer). Wenn wir einen weiteren Datenträger hinzufügen, vergeben wir dafür einen eindeutigen `Lun`-Wert.

### <a name="add-a-new-data-disk-to-our-vm"></a>Hinzufügen eines neuen Datenträgers für Daten zum virtuellen Computer

1. Der Einfachheit halber speichern wir den Namen des neuen Datenträgers:

    ```powershell
    $newDiskName = "fotoshareVM-data2"
    ```
    
1. Führen Sie den folgenden Befehl `Add-AzureRmVMDataDisk` aus, um einen neuen leeren 1-GB-Datenträger zu definieren:

    ```powershell
    Add-AzureRmVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
    ```
    Die Antwort lautet etwa:

    ```output
    ResourceGroupName  : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx
    Id                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxx-xxxxxxx/resourceGroups/<rgn>[sandbox resource group name]</rgn>/providers/Microsoft.Compute/virtualMachines/fotoshareVM
    VmId               : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx
    Name               : fotoshareVM
    Type               : Microsoft.Compute/virtualMachines
    Location           : eastus
    Tags               : {}
    DiagnosticsProfile : {BootDiagnostics}
    HardwareProfile    : {VmSize}
    NetworkProfile     : {NetworkInterfaces}
    OSProfile          : {ComputerName, AdminUsername, WindowsConfiguration, Secrets}
    ProvisioningState  : Succeeded
    StorageProfile     : {ImageReference, OsDisk, DataDisks}
        ```
    
1. We've given this disk a `Lun` value of `1` because it's not taken. We defined the disk we want to create, so it's time to run `Update-AzureRmVM` to make the actual change:

    ```powershell
    Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
1. Wir sehen uns nun erneut die Datenträgerinformationen an:

    ```powershell
    $myVM.StorageProfile.DataDisks
    ```
    
    ```output
    Name            : fotosharesVM-data
    DiskSizeGB      : 1023
    Lun             : 0
    Caching         : ReadOnly
    CreateOption    : Attach
    SourceImage     :
    VirtualHardDisk :
    
    Name            : fotoshareVM-data2
    DiskSizeGB      : 1
    Lun             : 1
    Caching         : None
    CreateOption    : Empty
    SourceImage     :
    VirtualHardDisk :
    ```

Wir verfügen jetzt über zwei Datenträger. Unser neuer Datenträger hat eine `Lun` von `1`, und der Standardwert für `Caching` ist `None`. Wir ändern diesen Wert.

### <a name="change-cache-settings-of-new-data-disk"></a>Ändern der Cacheeinstellungen des neuen Datenträgers

1. Wir ändern die Eigenschaften eines VM-Datenträgers wie folgt mit dem Cmdlet `Set-AzureRmVMDataDisk`:

    ```powershell
    Set-AzureRmVMDataDisk -VM $myVM -Lun "1" -Caching ReadWrite
    ```
    
1. Die Änderungen committen wir wie immer mit `Update-AzureRmVM`:

    ```powershell
    Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
    ```
    
Hier ist eine Ansicht aus dem Portal angegeben, die verdeutlicht, was wir in dieser Übung erreicht haben. Der virtuelle Computer verfügt nun über zwei Datenträger für Daten, und wir haben die Einstellungen für **HOSTZWISCHENSPEICHERUNG** angepasst. Hierfür haben wir nur wenige Befehle benötigt. Dies liegt an der hohen Leistungsfähigkeit von Azure PowerShell.

![Screenshot des Azure-Portals mit dem Abschnitt „Datenträger“ auf dem Blatt unseres virtuellen Computers mit zwei Datenträgern für Daten.](../media/disks-final-config-portal2.png)
