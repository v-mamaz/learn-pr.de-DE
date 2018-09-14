In der vorherigen Übung ausgeführt wir mithilfe von Azure-Portal die folgenden Aufgaben aus:

- Ansicht Betriebssystem-Datenträger-Cache-status
- Ändern der cacheeinstellungen für Betriebssystem-Datenträger
- Hinzufügen eines Datenträgers zur VM
- Ändern des cachetyps auf einen neuen Datenträger

Versuchen Sie es selbst diese Vorgänge mithilfe von Azure PowerShell. Wir werden den virtuellen Computer verwenden wir in der vorherigen Übung erstellt haben. Die Vorgänge in dieser Übung wird davon ausgegangen:

- Der virtuellen Computer vorhanden ist, und wird aufgerufen, **FotoshareVM**
- VM befindet sich in einer Ressourcengruppe namens  **<rgn>[Sandkasten Resource Group-Name]</rgn>**

Wenn Sie mit einem anderen Satz von Namen bearbeitet haben, ersetzen Sie nur diese Werte durch Ihre eigenen.

Hier ist der aktuelle Zustand der virtuellen Computer Datenträger aus der letzten Übung:

![Screenshot der Betriebssystemdatenträger und sonstige Datenträger, die sowohl für das caching von nur-Lese festgelegt werden.](../media/disks-final-config-portal.PNG)

Wir haben mithilfe des Portals Festlegen der **HOSTZWISCHENSPEICHERN** Feld für das Betriebssystem und Daten-Datenträger. Behalten Sie diesen Ausgangszustand im Hinterkopf, wir arbeiten, über die folgenden Schritte aus.

### <a name="set-up-some-variables"></a>Richten Sie einige Variablen

Zunächst sehen wir einige Ressourcennamen speichern, damit wir sie später verwenden können.

Verwenden Sie das Azure Cloud Shell-Terminal auf der rechten Seite, um die folgenden PowerShell-Befehle ausführen:

> [!NOTE]
> Wechseln Sie Ihre Cloud Shell-Sitzung zum **PowerShell** bevor Sie diese Befehle versuchen, falls bereits nicht.

```powershell
$myRgName = "<rgn>[Sandbox resource group name]</rgn>"
$myVMName = "fotoshareVM"
```

> [!TIP]
> Sie müssen diese Variablen erneut ein, wenn die Cloud Shell-Sitzung eine auftritt Zeitüberschreitung. Also, wenn möglich, Durcharbeiten dieser ganzen Übung in einer einzigen Sitzung.

### <a name="get-info-about-our-vm"></a>Abrufen von Informationen zu den virtuellen Computer

Führen Sie den folgenden Befehl aus, um die Eigenschaften der VM wieder zu erhalten:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVmName
```

Wir speichern die Antwort in unserer `$myVM` Variable. Wir können nur uns die Eigenschaften anzeigen, die wir hier geben Sie den folgenden Befehl ausführen:

```powershell
$myVM | select-object -property ResourceGroupName, Name, Type, Location
```

Wie der folgende Screenshot zeigt, ist dieser virtuelle Computer tatsächlich den virtuellen Computer, die wir nach. Daher machen wir weiter.

![Screenshot des Azure PowerShell-Konsole, die Ergebnisse der letzten vier Befehle angezeigt.](../media/6-ps-commands-1.PNG)

### <a name="view-os-disk-cache-status"></a>Ansicht Betriebssystem-Datenträger-Cache-status

Wir sehen die zwischenspeicherungseinstellung über die `StorageProfile` Objekt wie folgt:

```powershell
$myVM.StorageProfile.OsDisk.Caching
```

In diesem Beispiel wird der aktuelle Wert `None`. Ändern Sie ihn sehen wir wieder auf den Standardwert für ein Betriebssystem-Datenträger.

![Screenshot der Azure-PowerShell-Konsole mit unserem Betriebssystem-Datenträger, die mit dem Zwischenspeichern Wert "None".](../media/6-ps-oscaching-none.PNG)

### <a name="change-the-cache-settings-of-the-os-disk"></a>Ändern der cacheeinstellungen für Betriebssystem-Datenträger

Wir können den Wert festlegen, für den Cachetyp, der mit dem gleichen `StorageProfile` Objekt wie folgt:

```powershell
$myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
```

Dieser Befehl führt schneller, das sollte Sie erkennen Sie, dass es lokal maßgeblich zu verbessern. Der Befehl ändert die Eigenschaft nur auf die `myVM` Objekt. Wie im folgenden Screenshot gezeigt, aktualisieren Sie die `$myVM` Variablen, die Zwischenspeicherung Wert wird nicht auf dem virtuellen Computer geändert haben:

![Screenshot der Azure-PowerShell-Konsole anzeigen, aktualisieren das Objekt "MyVM" wird zurückgesetzt, das Zwischenspeichern auf "none", da wir den virtuellen Computer nicht tatsächlich aktualisiert hat.](../media/6-ps-commands-2.PNG)

Damit die Änderung auf dem virtuellen Computer selbst, rufen `Update-AzureRmVM`wie folgt:

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

Beachten Sie, dass dieser Aufruf die Zeit in Anspruch nimmt. Der Grund ist den eigentlichen virtuellen Computer werden aktualisiert, und Azure neu gestartet, wird des virtuelle Computers, um die Änderung vorzunehmen.

![Screenshot der Azure-PowerShell-Konsole mit unserem Betriebssystem-Datenträger, die mit dem Zwischenspeichern Wert "None".](../media/6-ps-oscaching-rw.PNG)

Wenn Sie aktualisieren die `$myVM` Variablen in diesem Fall sehen Sie die Änderung für das Objekt. Betrachten den Datenträger im Portal aus, würden Sie auch die Änderung gibt es sehen. Betrachten wir nun einen neuen Datenträger erstellen.

### <a name="list-data-disk-info"></a>Datenträgerinformationen für Liste-Daten

Um welche Datenträger für Daten anzuzeigen, auf dem virtuellen Computer haben, führen Sie den folgenden Befehl aus:

```powershell
$myVM.StorageProfile.DataDisks
```

Wir haben nur einen Datenträger für Daten im Moment. Die `Lun` Feld ist wichtig. Es ist die eindeutige **L**ogisches **U**übertreibenden **N**Anzahl. Wenn wir einen weiteren Datenträger hinzufügen, erhalten sie einen eindeutigen `Lun` Wert.

### <a name="add-a-new-data-disk-to-our-vm"></a>Fügen Sie einen neuen Datenträger an den virtuellen Computer

Der Einfachheit halber speichern wir unserer neuen Datenträgernamen:

```powershell
$newDiskName = "fotoshareVM-data2"
```

Führen Sie den folgenden `Add-AzureRmVMDataDisk` Befehl aus, um einen neuen Datenträger zu definieren:

```powershell
Add-AzureRmVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
```

Wir diesen Datenträger gegeben haben eine `Lun` Wert `1` , da er nicht ausgeführt wird. Definiert den Datenträger erstellt werden soll, daher ist es Zeit zum Ausführen `Update-AzureRmVM` die eigentliche Änderung vornehmen:

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

Sehen wir uns unsere Daten Datenträgerinformationen erneut:

```powershell
$myVM.StorageProfile.DataDisks
```

![Screenshot der unsere zwei Datenträger für Daten mit Azure PowerShell-Konsole.](../media/2-data-disks-part1.png)

Wir verfügen jetzt über zwei Datenträger. Unsere neue Datenträger hat eine `Lun` von `1` und der Standardwert für `Caching` ist `None`. Diesen Wert ändern.

### <a name="change-cache-settings-of-new-data-disk"></a>Ändern von cacheeinstellungen des neuen Datenträgers

Wir ändern die Eigenschaften einer VM-Datenträger mit der `Set-AzureRmVMDataDisk` -Cmdlet wie folgt:

```powershell
Set-AzureRmVMDataDisk -VM $myVM -Lun "1" -Caching ReadWrite
```

Wie immer die Änderungen mit `Update-AzureRmVM`:

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

Hier ist eine Ansicht aus dem Portal dafür, was wir in dieser Übung erreicht haben. Der virtuellen Computer verfügt nun über zwei Datenträger, und wir haben alle angepasst **HOSTZWISCHENSPEICHERN** Einstellungen. Wir haben alles mit nur wenigen Befehlen. Dies ist die Leistungsfähigkeit von Azure PowerShell.

![Screenshot des Azure-Portal mit der Datenträger Teil unserer VM-Blatt mit zwei Datenträger für Daten.](../media/disks-final-config-portal2.png)
