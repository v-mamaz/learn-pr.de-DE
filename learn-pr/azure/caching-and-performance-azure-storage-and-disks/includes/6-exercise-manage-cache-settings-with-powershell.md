
In der vorherigen Übung haben wir mit dem Azure-Portal die folgenden Aufgaben durchgeführt.

- Anzeigen des Cachestatus für den Betriebssystemdatenträger
- Ändern der Cacheeinstellungen des Betriebssystemdatenträgers
- Hinzufügen eines Datenträgers zum virtuellen Computer
- Ändern des Cachetyps auf einem neuen Datenträger

Wir üben diese Vorgänge nun mit Azure PowerShell. Wir verwenden den virtuellen Computer, den wir in der vorherigen Übung erstellt haben. Für die Vorgänge in dieser Übung wird Folgendes vorausgesetzt:

- Der virtuelle Computer ist vorhanden und hat den Namen **fotoshareVM**.
- Der virtuelle Computer ist in einer Ressourcengruppe mit dem Namen **fotoshare-rg** enthalten.

Falls Sie andere Namen verwendet haben, können Sie diese Werte einfach entsprechend ersetzen. 

Hier ist der aktuelle Status unserer VM-Datenträger aus der letzten Übung angegeben. 

![Screenshot: Betriebssystemdatenträger und Datenträger, jeweils mit schreibgeschütztem Caching](../media-draft/disks-final-config-portal.PNG)

Wir haben das Portal verwendet, um das Feld **HOSTZWISCHENSPEICHERUNG** für den Betriebssystemdatenträger und den anderen Datenträger festzulegen. Behalten Sie diesen Ausgangszustand im Hinterkopf, während wir die folgenden Schritte durcharbeiten. 

### <a name="set-up-some-variables"></a>Einrichten einiger Variablen
Zuerst speichern wir einige Ressourcennamen zur späteren Verwendung.

Verwenden Sie das Azure Cloud Shell-Terminalfenster auf der rechten Seite, um die folgenden PowerShell-Befehle auszuführen. 

```powershell
$myRgName = "fotoshare-rg"
$myVMName = "fotoshareVM"
```

> [!TIP]
> Sie müssen diese Variablen erneut festlegen, wenn der Timeout für Ihre Cloud Shell-Sitzung erreicht ist. Nach Möglichkeit sollten Sie die gesamte Übung also in einer Sitzung durcharbeiten. 

### <a name="get-info-about-our-vm"></a>Abrufen von Informationen zum virtuellen Computer

Führen Sie den folgenden Befehl aus, um die Eigenschaften für den virtuellen Computer zu erhalten.
 
```powershell
$myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVMName
```
Wir speichern die Antwort in der Variablen `$myVM`. Wir können den folgenden Befehl ausführen, um nur die hier angegebenen Eigenschaften anzuzeigen.

```powershell
$myVM | select-object -property ResourceGroupName, Name, Type, Location
```

Wie im folgenden Screenshot zu sehen ist, ist dies der gewünschte virtuelle Computer. Wir fahren also fort. 

![In der PowerShell-Konsole werden die letzten vier Befehle angezeigt, die wir ausgeführt haben.](../media-draft/ps-commands-1.PNG)

### <a name="view-os-disk-cache-status"></a>Anzeigen des Cachestatus für den Betriebssystemdatenträger

Wir können die Cacheeinstellung wie folgt über das `StorageProfile`-Objekt überprüfen.

```powershell
$myVM.StorageProfile.OsDisk.Caching
```
In diesem Beispiel lautet der aktuelle Wert **None** (Keine). Wir ändern ihn wieder in die Standardeinstellung für einen Betriebssystemdatenträger.

![PowerShell-Konsole mit dem Cachewert „None“ (Keine) für den Betriebssystemdatenträger](../media-draft/ps-oscaching-none.PNG)

### <a name="change-the-cache-settings-of-the-os-disk"></a>Ändern der Cacheeinstellungen des Betriebssystemdatenträgers

Wir können den Wert für den Cachetyp festlegen, indem wir wie folgt dasselbe StorageProfile-Objekt verwenden.
 
```powershell
$myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
```

Dieser Befehl wird schneller ausgeführt. Dies deutet darauf hin, dass der Vorgang lokal erfolgt. Mit dem Befehl wird nur die Eigenschaft für das myVM-Objekt geändert. Wie im folgenden Screenshot zu sehen ist, gilt Folgendes: Wenn Sie die Variable `$myVM` aktualisieren, hat sich der Cachewert für den virtuellen Computer nicht geändert.

![PowerShell-Konsole: Durch die Aktualisierung des „myVM“-Objekts wird die Zwischenspeicherung auf „None“ zurückgesetzt, da der virtuelle Computer nicht aktualisiert wurde.](../media-draft/ps-commands-2.PNG)

Rufen Sie `Update-AzureRmVM` wie folgt auf, um die Änderung auf dem virtuellen Computer durchzuführen.

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

Beachten Sie, dass es eine Weile dauert, bis dieser Aufruf abgeschlossen wurde. Dies liegt daran, dass wir den eigentlichen virtuellen Computer aktualisieren und Azure den virtuellen Computer neu startet, um die Änderung vorzunehmen.

![PowerShell-Konsole mit dem Cachewert „None“ (Keine) für den Betriebssystemdatenträger](../media-draft/ps-oscaching-rw.PNG)

Wenn Sie die Variable `$myVM` erneut aktualisieren, sehen Sie die Änderung für das Objekt. Wenn Sie sich den Datenträger im Portal ansehen, können Sie die Änderung dort auch erkennen. Wir fahren nun mit dem Erstellen eines neuen Datenträgers fort.  

### <a name="list-data-disk-info"></a>Auflisten von Datenträgerinformationen

Führen Sie den folgenden Befehl aus, um anzuzeigen, welche für Daten bestimmte Datenträger auf unserem virtuellen Computer vorhanden sind. 

```powershell
$myVM.StorageProfile.DataDisks
```

Derzeit wird nur ein Datenträger verwendet. Das Feld `Lun` ist wichtig. „Lun“ steht für die eindeutige „**L**ogical **U**nit **N**umber“ (Logische Gerätenummer). Wenn wir einen weiteren Datenträger hinzufügen, vergeben wir dafür einen eindeutigen `Lun`-Wert. 

### <a name="add-a-new-data-disk-to-our-vm"></a>Hinzufügen eines neuen Datenträgers zum virtuellen Computer 

Der Einfachheit halber speichern wir den Namen des neuen Datenträgers.

```powershell
$newDiskName = "fotoshareVM-data2"
```

Führen Sie den folgenden Befehl `Add-AzureRmVMDataDisk` aus, um einen neuen Datenträger zu definieren. 

```powershell
Add-AzureRmVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
```

Wir haben für diesen Datenträger den Lun-Wert „1“ vergeben, da er noch frei ist. Wir haben jetzt den Datenträger definiert, der erstellt werden soll. Es ist also an der Zeit `Update-AzureRmVM` auszuführen, um die eigentliche Änderung vorzunehmen. 

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

Wir sehen uns nun erneut die Datenträgerinformationen an.

```powershell
$myVM.StorageProfile.DataDisks
```

![PowerShell-Konsole mit zwei Datenträgern für Daten](../media-draft/2-data-disks-part1.png)

Wir verfügen jetzt über zwei Datenträger. Der neue Datenträger hat den **Lun**-Wert „1“, und der Standardwert für **Caching** lautet **None** (Keine). Wir ändern diesen Wert.

### <a name="change-cache-settings-of-new-data-disk"></a>Ändern der Cacheeinstellungen des neuen Datenträgers

Wir ändern die Eigenschaften eines VM-Datenträgers wie folgt mit dem Cmdlet `Set-AzureRmVMDataDisk`.

```powershell
Set-AzureRmVMDataDisk -Lun "1" -Caching ReadWrite
```

Die Änderungen committen wir wie immer mit `Update-AzureRmVM`.

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

Hier ist eine Ansicht aus dem Portal angegeben, die verdeutlicht, was wir in dieser Übung erreicht haben. Der virtuelle Computer verfügt nun über zwei Datenträger für Daten, und wir haben die Einstellungen für **Hostzwischenspeicherung** angepasst. Hierfür haben wir nur wenige Befehle benötigt. Dies liegt an der hohen Leistungsfähigkeit von Azure PowerShell.

![PowerShell-Konsole mit zwei Datenträgern für Daten](../media-draft/disks-final-config-portal2.png)
