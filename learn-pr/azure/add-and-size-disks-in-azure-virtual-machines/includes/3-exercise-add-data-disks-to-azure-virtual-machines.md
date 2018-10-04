Unsere Anwaltskanzlei ist dabei, ihre Fallzahl zu erhöhen, weshalb Sie mit der Einrichtung eines neuen Linux-Webservers beauftragt wurden, auf dem kritische Dokumente aus einer Vielzahl von Quellen gespeichert werden sollen. Dies können Klienten, anderen Kanzleien und Strafverfolgungsbehörden sein. Unser Server kann Uploads empfangen, die er auf Datenträger speichern soll.

> [!TIP]
> In dieser Übung wird Linux als Beispiel verwendet, aber der grundlegende Prozess der Erstellung von VMs und des Hinzufügens von Datenträgern ist für Windows identisch. Der Hauptunterschied besteht in der Partitionierung und Formatierung des Datenträgers, was in einer Remotedesktopsitzung mithilfe der integrierten Tools zur Datenträgerverwaltung erfolgen würde.

Ziel dieser Übung ist, einen virtuellen Linux-Computer (VM) zu erstellen und eine neue virtuelle Festplatte (VHD) namens „uploadDataDisk1“ anzufügen, auf der das Verzeichnis „uploads“ gespeichert wird.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm"></a>Erstellen eines virtuellen Linux-Computers

Wir erstellen mithilfe der Azure CLI eine Linux-VM zum Hosten unseres Webservers.

1. Legen Sie zuerst einige Standardeinstellungen für diese Sitzung fest. Als Erstes müssen Sie die _Region_ der VM festlegen. Im Idealfall befindet sich diese in der Nähe Ihrer Kunden. Wählen Sie in diesem Fall die Region aus, die den für die Azure-Sandbox verfügbaren Standorten am nächsten ist.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Legen Sie mit dem Befehl `az configure` den gewünschte Standardstandort fest. Ersetzen Sie „eastus“ durch diesen Standort.

    ```azurecli
    az configure --defaults location=eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. Legen Sie den Standardwert für die Ressourcengruppe auf die vorkonfigurierte Ressourcengruppe fest, die für die Azure-Sandbox erstellt wurde: **<rgn>[Sandboxressourcengruppe]</rgn>**

    ```azurecli
    az configure --defaults group="<rgn>[sandbox Resource Group]</rgn>"
    ```

1. Erstellen Sie als Nächstes mit dem Befehl `vm create` eine neue Ubuntu Linux-VM.
    - Nennen Sie sie „support-web-vm01“.
    - Legen Sie **Größe** auf _Standard_DS2_v2_ fest.
    - Legen Sie den **Administratorbenutzernamen** auf „azureuser“ (oder einen Namen Ihrer Wahl fest).
    - Generieren Sie mit dem Parameter `--generate-ssh-keys` SSH-Schlüssel.

    ```azurecli
    az vm create --name support-web-vm01 \
        --image UbuntuLTS \
        --size Standard_DS2_v2 \
        --admin-username azureuser \
        --generate-ssh-keys
    ```
    
    > [!TIP]
    > Das Erstellen Ihrer VM und deren Bereitstellung in Azure kann einige Minuten dauern. Sie können den Fortschritt in Cloud Shell überwachen.
    
1. Das Ergebnis ist ein JSON-Block mit den Details zur erstellten VM.

    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/xxx/resourceGroups/<rgn>[sandbox resource group]</rgn>/providers/Microsoft.Compute/virtualMachines/support-web-vm01",
        "location": "eastus",
        "macAddress": "00-0D-3A-18-DE-B4",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "40.76.193.249",
        "resourceGroup": "<rgn>[sandbox resource group]</rgn>",
        "zones": ""
    }
    ```
    Notieren Sie sich **publicIpAddress** in der Ausgabe. Hierüber können wir remote auf die VM zugreifen.

    > [!NOTE]
    > Wir verwenden diese VM, um uns mit der Verwaltung von Datenträgern vertraut zu machen. Wenn wir sie tatsächlich als Webserver verwenden würden, würden wir mit dem Befehl `az vm open-port` zusätzliche Ports öffnen und Webserversoftware installieren. Diese Aufgaben sind nicht Bestandteil dieses Moduls, doch im Modul **Verwalten virtueller Computer mit der Azure CLI** erfahren Sie, wie diese Schritte erfolgen. 

## <a name="add-an-empty-data-disk-to-our-vm"></a>Hinzufügen eines leeren Datenträgers zur VM

Wir nennen den Datenträger, auf dem das Verzeichnis „uploads“ für Ihren Webserver gespeichert wird, „uploadDataDisk1“. 

> [!TIP]
> Sie können Datenträger hinzufügen, wenn die VM erstellt wird, indem Sie im Befehl `vm create` den Parameter `--data-disk-sizes-gb` angeben.

1. Fügen Sie einen neuen leeren Datenträger mit dem Befehl `vm disk attach` an den Server an.
    - Nennen Sie ihn „uploadDataDisk1“.
    - Legen Sie seine Größe auf 64 GB fest.
    - Legen Sie **sku** auf _Premium_LRS_ fest, damit wir Storage Premium mit lokaler Redundanz nutzen können.

    ```azurecli
    az vm disk attach \
        --vm-name support-web-vm01 \
        --disk uploadDataDisk1 \
        --size-gb 64 \
        --sku Premium_LRS \
        --new
    ```
    
Wir haben soeben einen Datenträger namens „uploadDataDisk1“ definiert. Um den Datenträger verwenden zu können, müssen wir ihn partitionieren und formatieren.

## <a name="initialize-data-disks"></a>Initialisieren von Laufwerken

Alle zusätzlichen Laufwerke, die Sie neu erstellen, müssen initialisiert und formatiert werden. Der Prozess ist der gleiche wie bei einem physischen Datenträger:

1. Stellen Sie zuerst über SSH eine Verbindung mit dem Linux-Server her, indem Sie die öffentliche IP-Adresse verwenden, die Sie bei der ersten Erstellung der VM erhalten haben. Wenn Ihnen diese nicht vorliegt, können Sie den folgenden Befehl verwenden, um die IP-Adresse abzurufen:

    ```azurecli
    az vm list-ip-addresses -n support-web-vm01
    ```

1. Verwenden Sie SSH mit der öffentlichen IP-Adresse und dem Benutzernamen, den Sie erstellt haben.

    ```bash
    ssh azureuser@40.76.193.249
    ```

1. Identifizieren Sie dann den Datenträger mit dem Befehl `lsblk`, um alle Blockgeräte aufzulisten – hier sehen Sie die vorhandenen Laufwerke.

    ```bash
    lsblk
    ```

    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk
    └─sdb1   8:17   0   14G  0 part /mnt
    sr0     11:0    1  628K  0 rom
    sdc      8:32   0   64G  0 disk
    sda      8:0    0   30G  0 disk
    └─sda1   8:1    0   30G  0 part /
    ```

Suchen Sie nach dem 64-GB-Laufwerk, das wir erstellt haben. Hier sehen Sie, dass es **sdc** heißt und nicht bereitgestellt ist. Das liegt daran, dass es nicht initialisiert wurde.

1. Sobald Sie das Laufwerk (**sdc**) kennen, das initialisiert werden muss, können Sie `fdisk` zu diesem Zweck verwenden. Sie müssen den Befehl mit `sudo` ausführen und den Datenträger angeben, der partitioniert werden soll:

    ```bash
    sudo fdisk /dev/sdc
    ```

1. Verwenden Sie den Befehl <kbd>n</kbd>, um eine neue Partition hinzuzufügen. In diesem Beispiel haben wir auch <kbd>p</kbd> als primäre Partition ausgewählt und übernehmen den Rest der Standardwerte. Die Ausgabe entspricht etwa folgendem Beispiel:   

    ```output
    Device does not contain a recognized partition table.
    Created a new DOS disklabel with disk identifier 0x3b44089f.
    
    Command (m for help): n
    Partition type
       p   primary (0 primary, 0 extended, 4 free)
       e   extended (container for logical partitions)
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-268435455, default 2048):
    Last sector, +sectors or +size{K,M,G,T,P} ...
    Created a new partition 1 of type 'Linux' and of size 64 GiB.    
    ```

1. Geben Sie die Partitionstabelle mit dem Befehl <kbd>p</kbd> aus. Sie sollte in etwa so aussehen:

    ```output
    Disk /dev/sdc: 64 GiB ...
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 4096 bytes
    I/O size (minimum/optimal): 4096 bytes / 4096 bytes
    Disklabel type: dos
    Disk identifier: 0x3b44089f
    
    Device     Boot Start ... Size Id Type
    /dev/sdc1        2048 ... 64G 83 Linux
    ```

1. Schreiben Sie die Änderungen mit dem Befehl <kbd>w<kbd>. Dadurch wird das Tool beendet.

1. Im nächsten Schritt schreiben Sie jetzt mit dem Befehl `mkfs` ein Dateisystem auf die Partition. Wir müssen den Dateisystemtyp und den Gerätenamen angeben, den wir aus der Ausgabe `fdisk` erhalten haben:
    - Übergeben Sie `-t ext4`, um ein _ext4_-Dateisystem zu erstellen.
    - Der Gerätename lautet `/dev/sdc1`.

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
    
    Die Ausführung dieses Befehls kann einige Minuten dauern.

    ```output
    mke2fs 1.42.13 (17-May-2015)
    Discarding device blocks: done
    Creating filesystem with 16777088 4k blocks and 4194304 inodes
    ...
    Allocating group tables: done
    Writing inode tables: done
    Creating journal (32768 blocks): done
    Writing superblocks and filesystem accounting information: done
    ```
    
1. Erstellen Sie im nächsten Schritt ein Verzeichnis, das als Bereitstellungspunkt verwendet wird. Angenommen, es ist ein Ordner `uploads` vorhanden:

    ```bash
    sudo mkdir /uploads
    ```
1. Verwenden Sie abschließend `mount` zum Anfügen des Datenträgers an den Bereitstellungspunkt:

    ```bash
    sudo mount /dev/sdc1 /uploads
    ```
    Sie sollten `lsblk` verwenden können, um das bereitgestellte Laufwerk jetzt anzuzeigen:
    
    ```output
    NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sdb      8:16   0   14G  0 disk
    └─sdb1   8:17   0   14G  0 part /mnt
    sr0     11:0    1  628K  0 rom
    sdc      8:32   0   64G  0 disk
    └─sdc1   8:33   0   64G  0 part /uploads
    sda      8:0    0   30G  0 disk
    └─sda1   8:1    0   30G  0 part /
    ```
    
### <a name="mounting-the-drive-automatically"></a>Automatisches Bereitstellen des Laufwerks

Um sicherzustellen, dass das Laufwerk nach einem Neustart automatisch bereitgestellt wird, muss es der Datei `/etc/fstab` hinzugefügt werden. Außerdem wird dringend empfohlen, den UUID (Universally Unique Identifier) in `/etc/fstab` zu verwenden, um auf das Laufwerk und nicht auf den Gerätenamen (z.B. `/dev/sdc1`) zu verweisen. Wenn das Betriebssystem während des Starts einen Datenträgerfehler erkennt, wird durch den UUID verhindert, dass an einem bestimmten Ort der falsche Datenträger bereitgestellt wird. Die verbleibenden Datenträger werden dann diesen Geräte-IDs zugewiesen. Verwenden Sie das Hilfsprogramm `blkid`, um den UUID des neuen Laufwerks herauszufinden:

```bash
sudo -i blkid
```

Die Rückgabe ähnelt dem folgenden Beispiel:

```output
/dev/sda1: UUID="36a59c42-c04c-4632-b83f-7015abd10358" TYPE="ext4"
/dev/sdb1: UUID="21092a62-79d4-4d8c-91de-4dd4e8b97d83" TYPE="ext4"
/dev/sdc1: UUID="e311c905-e0d9-43ab-af63-7f4ee4ef108e" TYPE="ext4"
```

1. Kopieren Sie den UUID für das Laufwerk `/dev/sdc1`, und öffnen Sie die Datei `/etc/fstab` in einem Text-Editor:

    ```bash
    sudo vi /etc/fstab
    ```

> [!WARNING]
> Eine fehlerhafte Bearbeitung der Datei `/etc/fstab` kann zu einem nicht startfähigen System führen. Wenn Sie sich nicht sicher sind, helfen Ihnen die Informationen zur richtigen Bearbeitung dieser Datei in der Dokumentation weiter. Außerdem wird empfohlen, eine Sicherung der Datei zu erstellen, bevor Sie sie bearbeiten, wenn Sie mit Produktionssystemen arbeiten.

1. Drücken Sie <kbd>G</kbd>, um zur letzten Zeile in der Datei zu gelangen.

1. Drücken Sie <kbd>I</kbd>, um in den Einfügemodus zu wechseln. Der Modus sollte am unteren Rand des Bildschirms angegeben werden.

1. Drücken Sie die <kbd>ENDE</kbd>-TASTE, um an das Ende der Zeile zu gelangen. Alternativ können Sie auch die Pfeiltasten verwenden. Drücken Sie die <kbd>EINGABETASTE</kbd>, um in eine neue Zeile zu wechseln.

1. Geben Sie die folgende Zeile in den Editor ein. Die Werte können durch Leerzeichen oder Tabstopps getrennt werden. Weitere Informationen zu jeder der Spalten finden Sie in der Dokumentation:

    ```output
    UUID=<uuid-goes-here>    /uploads    ext4    defaults,nofail    1    2
    ```
1. Drücken Sie **ESC**, und geben Sie dann **:w!** ein, um die Datei zu schreiben, und **:q** zum Beenden des Editors.

1. Abschließend überprüfen wir, ob der Eintrag richtig ist, indem wir das Betriebssystem auffordern, die Bereitstellungspunkte zu aktualisieren:

    ```bash
    sudo mount -a
    ```

    Wenn ein Fehler zurückgegeben wird, bearbeiten Sie die Datei, um das Problem zu ermitteln.

> [!TIP]
> Einige Linux-Kernel unterstützen TRIM zum Verwerfen ungenutzter Blöcke auf dem Datenträger. Dieses Feature ist für Azure-Datenträger verfügbar und kann Ihnen Geld sparen, wenn Sie große Dateien erstellen und diese dann löschen. Erfahren Sie in unserer Dokumentation, wie [dieses Feature aktiviert wird](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure).

Nachdem Sie erfahren haben, wie einfach es ist, Datenträger zu Ihren VMs hinzuzufügen, schauen wir uns nun an, welche Arten von Datenträgern Sie erstellen können. Wir beschäftigen uns insbesondere mit dem Unterschied zwischen den Storage-Tarifen Standard und Premium.