In Azure werden Ihre VHD-Images in einem Azure Storage-Konto als Seitenblobs gespeichert. Bei verwalteten Datenträgern übernimmt Azure die Verwaltung des Speichers in Ihrem Auftrag. Dies ist einer der besten Gründe, sich für verwaltete Datenträger zu entscheiden.

Wenn Sie die VM erstellen, wird eine Größe für den Betriebssystem-Datenträger gewählt. Die genaue Größe basiert auf dem Image, das Sie auswählen. Unter Linux ist die Größe meist ca. 30 GB, unter Windows 127 GB.

Sie können Datenträger hinzufügen, um zusätzlichen Speicherplatz bereitzustellen. Sie können aber auch einen vorhandenen Datenträger erweitern. Möglicherweise kann eine ältere Anwendung ihre Daten nicht auf Laufwerke verteilen, oder Sie migrieren das Laufwerk eines physischen PCs nach Azure und benötigen ein größeres Betriebssystem-Laufwerk.

> [!NOTE]
> Sie können einen Datenträger nur _vergrößern_. Das Verkleinern verwalteter Datenträger wird derzeit nicht unterstützt.

Durch das Ändern der Größe des Datenträgers kann sich auch die Ebene des Datenträgers ändern (z.B. von P10 in P20). Denken Sie daran, da dies für leistungsbezogene Upgrades von Vorteil sein kann. Es fallen aber auch höhere Kosten an, wenn Sie sich im Premium-Tarif nach oben bewegen.

## <a name="vm-size-vs-disk-size"></a>Größe der VM im Vergleich mit der Datenträgergröße

Die VM-Größe, die Sie auswählen, wenn Sie die VM erstellen, bestimmt, wie viele Ressourcen ihr zugewiesen werden können. Bei der Speicherung steuert die Größe die Anzahl der Datenträger, die Sie der VM hinzufügen können, und die maximale Größe der einzelnen Datenträger. 

Wie in der vorherigen Einheit bereits erwähnt, unterstützen einige VM-Größen nur Standard-Speicherlaufwerke, was die E/A-Leistung einschränkt.

Wenn Sie feststellen, dass Sie mehr Speicherplatz benötigen, als Ihre VM-Größe zulässt, können Sie die VM-Größe ändern. Wir behandeln dieses Thema im Modul **Einführung in Azure Virtual Machines**.

## <a name="expanding-a-disk-using-the-azure-cli"></a>Erweitern eines Datenträgers mit der Azure CLI

> [!WARNING]
> Bevor Sie Änderungen an der Größe von Datenträgern vornehmen, sollten Sie Ihre Daten unbedingt immer zunächst sichern!

Vorgänge auf VHDs können nicht durchgeführt werden, wenn die VM ausgeführt wird. Der erste Schritt besteht darin, die VM zu beenden und die Zuordnung mit `az vm deallocate` unter Angabe des Namens der VM und der Ressourcengruppe aufzuheben.

Bei der Aufhebung der Zuordnung einer VM werden anders als beim bloßen _Beenden_ einer VM die zugehörigen IT-Ressourcen freigegeben, sodass Azure Konfigurationsänderungen an der virtualisierten Hardware vornehmen kann.

```azurecli
az vm deallocate --resource-group <resource-group-name> --name <vm-name>
```

Um anschließend die Größe eines Datenträgers zu ändern, verwenden Sie `az disk update` und übergeben den Datenträgernamen, den Namen der Ressourcengruppe und die neu angeforderte Größe. Wenn Sie einen verwalteten Datenträger erweitern, wird die angegebene Größe der nächsten verwalteten Datenträgergröße zugeordnet.

```azurecli
az disk update \
    --resource-group <resource-group-name> \
    --name <disk-name> \
    --size-gb 200
```

Abschließend starten Sie die VM mit `az vm start` neu:

```azurecli
az vm start --resource-group <resource-group-name> --name <vm-name>
```

## <a name="expanding-a-disk-using-the-azure-portal"></a>Erweitern eines Datenträgers im Azure-Portal

Das Erweitern eines Datenträgers im Azure-Portal ist noch einfacher.

1. Beenden Sie die VM in ihrer Ansicht **Übersicht** über die Schaltfläche **Beenden** auf der Symbolleiste.

1. Klicken Sie im Abschnitt **Einstellungen** auf **Datenträger**.

1. Wählen Sie den Datenträger aus, dessen Größe Sie ändern möchten.

    ![Screenshot des Abschnitts „Datenträger“ einer VM mit hervorgehobener VHD, die wir bearbeiten möchten](../media/5-portal-disks.png)

1. Geben Sie in den Datenträgerdetails eine Größe ein, die _höher_ als die aktuelle Größe ist. Sie können hier auch von Premium zu Standard (oder umgekehrt) wechseln. Diese Einstellungen wirken sich auf Ihre Leistung aus, wie im Abschnitt über die vorhergesagten IOPS gezeigt.

    ![Screenshot mit Bildschirm zum Bearbeiten der VHD mit hervorgehobenem Feld mit der neuen Größe](../media/5-resize-disk.png)

1. Klicken Sie zum Speichern der Änderungen auf **Speichern**.

1. Starten Sie die VM neu.


### <a name="expanding-the-partition"></a>Erweitern der Partition

Genau wie beim Hinzufügen eines neuen Datenträgers wird mit einem erweiterten Datenträger erst dann nutzbarer Speicherplatz hinzugefügt, wenn Sie die Partition und das Dateisystem erweitern. Dies muss mit den der VM zur Verfügung stehenden Betriebssystemtools erfolgen. 

Unter Windows verwenden wir das Tool „Datenträgerverwaltung“ oder Befehlszeilentool `diskpart`.

Unter Linux verwenden Sie `parted` und `resize2fs`.

Lassen Sie uns einige dieser Befehle ausprobieren.