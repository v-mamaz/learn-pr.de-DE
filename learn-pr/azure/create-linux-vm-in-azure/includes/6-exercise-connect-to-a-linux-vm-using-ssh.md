<span data-ttu-id="89339-101">Der virtuelle Linux-Computer wurde bereitgestellt und wird ausgeführt, aber noch nicht für die Arbeit konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="89339-101">We have our Linux VM deployed and running, but it's not configured to do any work.</span></span> <span data-ttu-id="89339-102">Stellen wir eine Verbindung mit SSH her, und konfigurieren wir Apache, damit wir über einen Webserver verfügen, der ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="89339-102">Let's connect to it with SSH and configure Apache, so we have a running web server.</span></span>

## <a name="connect-to-the-vm-with-ssh"></a><span data-ttu-id="89339-103">Herstellen einer Verbindung mit dem virtuellen Computer mit SSH</span><span class="sxs-lookup"><span data-stu-id="89339-103">Connect to the VM with SSH</span></span>

<span data-ttu-id="89339-104">Zum Herstellen der Verbindung eines virtuellen Azure-Computers mit einem SSH-Client benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="89339-104">To connect to an Azure VM with an SSH client, you will need:</span></span>

- <span data-ttu-id="89339-105">SSH-Clientsoftware (in den meisten modernen Betriebssystemen vorhanden)</span><span class="sxs-lookup"><span data-stu-id="89339-105">SSH client software (present on most modern operating systems)</span></span>
- <span data-ttu-id="89339-106">Die öffentliche IP-Adresse des virtuellen Computers (oder die private, wenn der virtuelle Computer dafür konfiguriert ist, eine Verbindung mit Ihrem Netzwerk herzustellen)</span><span class="sxs-lookup"><span data-stu-id="89339-106">The public IP address of the VM (or private if the VM is configured to connect to your network)</span></span>

### <a name="get-the-public-ip-address"></a><span data-ttu-id="89339-107">Abrufen der öffentlichen IP-Adresse</span><span class="sxs-lookup"><span data-stu-id="89339-107">Get the public IP address</span></span>

1. <span data-ttu-id="89339-108">Stellen Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) sicher, dass der Bereich **Übersicht** für den zuvor erstellten virtuellen Computer geöffnet ist.</span><span class="sxs-lookup"><span data-stu-id="89339-108">In the [Azure portal](https://portal.azure.com?azure-portal=true), ensure the **Overview** panel for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="89339-109">Sie finden den virtuellen Computer unter **Alle Ressourcen**, falls Sie diesen öffnen müssen.</span><span class="sxs-lookup"><span data-stu-id="89339-109">You can find the VM under **All Resources** if you need to open it.</span></span> <span data-ttu-id="89339-110">Im Bereich „Übersicht“ finden Sie zahlreiche Informationen zum virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="89339-110">The overview panel has a lot of information about the VM.</span></span>

    - <span data-ttu-id="89339-111">Sie können sehen, ob er ausgeführt wird</span><span class="sxs-lookup"><span data-stu-id="89339-111">You can see whether the VM is running</span></span>
    - <span data-ttu-id="89339-112">Sie können ihn beenden oder neu starten</span><span class="sxs-lookup"><span data-stu-id="89339-112">Stop or restart it</span></span>
    - <span data-ttu-id="89339-113">Sie können die öffentliche IP-Adresse abrufen, um eine Verbindung mit dem virtuellen Computer herzustellen</span><span class="sxs-lookup"><span data-stu-id="89339-113">Get the public IP address to connect to the VM</span></span>
    - <span data-ttu-id="89339-114">Sie können die Aktivität von CPU, Festplatte und Netzwerk anzeigen</span><span class="sxs-lookup"><span data-stu-id="89339-114">See the activity of the CPU, disk, and network</span></span>

1. <span data-ttu-id="89339-115">Klicken Sie oben im Bereich auf die Schaltfläche **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="89339-115">Click the **Connect** button at the top of the pane.</span></span>

1. <span data-ttu-id="89339-116">Notieren Sie sich die Einstellungen für die **IP-Adresse** und die **Portnummer** auf dem Blatt **Verbindung mit virtuellem Computer herstellen**.</span><span class="sxs-lookup"><span data-stu-id="89339-116">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings.</span></span> <span data-ttu-id="89339-117">Auf der Registerkarte **SSH** finden Sie auch den Befehl, den Sie lokal ausführen müssen, um eine Verbindung mit dem virtuellen Computer herzustellen.</span><span class="sxs-lookup"><span data-stu-id="89339-117">On the **SSH** tab, you will also find the command you need to execute locally to connect to the VM.</span></span> <span data-ttu-id="89339-118">Kopieren Sie diesen in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="89339-118">Copy this to the clipboard.</span></span>

<!-- TODO: this will be necessary if we ever have inline portal integration 

### Open the Azure Cloud Shell

Let's use the Cloud Shell in the Azure Portal. If you generated the SSH key locally, you need to use your local session since the private key won't be in your storage account.

1. Switch back to the **Dashboard** by clicking the Dashboard button in the Azure sidebar.

1. Open the Cloud Shell by clicking the shell button in the top toolbar.

    ![Open the Azure Cloud Shell](../media-drafts/6-cloud-shell.png)

1. Select **Bash** as the shell type. PowerShell is also available if you are a Windows administrator.

    ![Select bash shell in the portal](../media-drafts/6-use-bash-shell.png)

-->

## <a name="connect-with-ssh"></a><span data-ttu-id="89339-119">Verbinden mit SSH</span><span class="sxs-lookup"><span data-stu-id="89339-119">Connect with SSH</span></span>

1. <span data-ttu-id="89339-120">Fügen Sie die Befehlszeile, die Sie auf der Registerkarte „SSH“ abgerufen haben, in die Cloud Shell ein.</span><span class="sxs-lookup"><span data-stu-id="89339-120">Paste the command line you got from the SSH tab into the Cloud Shell.</span></span> <span data-ttu-id="89339-121">Das Ergebnis sollte in etwa wie folgt aussehen. Es wird jedoch eine andere IP-Adresse verwendet (und möglicherweise ein anderer Benutzername, wenn Sie nicht **jim** angegeben haben)</span><span class="sxs-lookup"><span data-stu-id="89339-121">It should look something like this; however it will have a different IP address (and perhaps a different username if you didn't use **jim**!)</span></span>

    ```bash
    ssh jim@137.117.101.249
    ```

1. <span data-ttu-id="89339-122">Mit diesem Befehl wird eine Secure Shell-Verbindung geöffnet, und es wird eine herkömmliche Shell-Eingabeaufforderung für Linux angezeigt.</span><span class="sxs-lookup"><span data-stu-id="89339-122">This command will open a secure shell connection and place you at a traditional shell command prompt for Linux.</span></span>

1. <span data-ttu-id="89339-123">Führen Sie einige Linux-Befehle aus</span><span class="sxs-lookup"><span data-stu-id="89339-123">Try executing a few Linux commands</span></span>
    - <span data-ttu-id="89339-124">`ls -la /`, um den Stamm des Datenträgers anzuzeigen</span><span class="sxs-lookup"><span data-stu-id="89339-124">`ls -la /` to show the root of the disk</span></span>
    - <span data-ttu-id="89339-125">`ps -l`, um alle ausgeführten Prozesse anzuzeigen</span><span class="sxs-lookup"><span data-stu-id="89339-125">`ps -l` to show all the running processes</span></span>
    - <span data-ttu-id="89339-126">`dmesg`, um alle Kernelnachrichten aufzulisten</span><span class="sxs-lookup"><span data-stu-id="89339-126">`dmesg` to list all the kernel messages</span></span>
    - <span data-ttu-id="89339-127">`lsblk`, um alle Blockgeräte aufzulisten. Hier werden Ihre Laufwerke angezeigt</span><span class="sxs-lookup"><span data-stu-id="89339-127">`lsblk` to list all the block devices - here you will see your drives</span></span>

<span data-ttu-id="89339-128">Interessanter ist das, was in der Liste der Laufwerke _fehlt_.</span><span class="sxs-lookup"><span data-stu-id="89339-128">The more interesting thing to observe in the list of drives is what is _missing_.</span></span> <span data-ttu-id="89339-129">Beachten Sie, dass unser **Daten**laufwerk (`sdc`) zwar vorhanden, nicht aber im Dateisystem bereitgestellt ist.</span><span class="sxs-lookup"><span data-stu-id="89339-129">Notice that our **Data** drive (`sdc`) is present but not mounted into the file system.</span></span> <span data-ttu-id="89339-130">Azure hat eine VHD hinzugefügt, aber nicht initialisiert.</span><span class="sxs-lookup"><span data-stu-id="89339-130">Azure added a VHD but didn't initialize it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="89339-131">Initialisieren von Laufwerken</span><span class="sxs-lookup"><span data-stu-id="89339-131">Initialize data disks</span></span>

<span data-ttu-id="89339-132">Alle zusätzlichen Laufwerke, die Sie neu erstellen, müssen initialisiert und formatiert werden.</span><span class="sxs-lookup"><span data-stu-id="89339-132">Any additional drives you create from scratch will need to be initialized and formatted.</span></span> <span data-ttu-id="89339-133">Der Prozess ist der gleiche wie bei einem physischen Datenträger.</span><span class="sxs-lookup"><span data-stu-id="89339-133">The process for doing this is identical to a physical disk.</span></span>

1. <span data-ttu-id="89339-134">Identifizieren Sie zuerst den Datenträger.</span><span class="sxs-lookup"><span data-stu-id="89339-134">First, identify the disk.</span></span> <span data-ttu-id="89339-135">Dies ist weiter oben erfolgt.</span><span class="sxs-lookup"><span data-stu-id="89339-135">We did that above.</span></span> <span data-ttu-id="89339-136">Sie können auch `dmesg | grep SCSI` verwenden, um alle Nachrichten aus dem Kernel für SCSI-Geräte aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="89339-136">You could also use `dmesg | grep SCSI` which will list all the messages from the kernel for SCSI devices.</span></span>

1. <span data-ttu-id="89339-137">Sobald Sie das Laufwerk (`sdc`) kennen, das initialisiert werden muss, können Sie `fdisk` zu diesem Zweck verwenden.</span><span class="sxs-lookup"><span data-stu-id="89339-137">Once you know the drive (`sdc`) you need to initialize, you can use `fdisk` to do that.</span></span> <span data-ttu-id="89339-138">Sie müssen den Befehl mit `sudo` ausführen und den Datenträger angeben, der partitioniert werden soll.</span><span class="sxs-lookup"><span data-stu-id="89339-138">You will need to run the command with `sudo` and supply the disk you want to partition.</span></span>

    ```bash
    sudo fdisk /dev/sdc
    ```
1. <span data-ttu-id="89339-139">Verwenden Sie den Befehl `n`, um eine neue Partition hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="89339-139">Use the `n` command to add a new partition.</span></span>  <span data-ttu-id="89339-140">In diesem Beispiel haben wir auch „p“ als primäre Partition ausgewählt und akzeptieren den Rest der Standardwerte.</span><span class="sxs-lookup"><span data-stu-id="89339-140">In this example, we also choose p for a primary partition and accept the rest of the default values.</span></span> <span data-ttu-id="89339-141">Die Ausgabe entspricht etwa folgendem Beispiel:</span><span class="sxs-lookup"><span data-stu-id="89339-141">The output will be similar to the following example:</span></span>   

    ```output
    Device does not contain a recognized partition table.
    Created a new DOS disklabel with disk identifier 0x1f2d0c46.
    
    Command (m for help): n
    Partition type
       p   primary (0 primary, 0 extended, 4 free)
       e   extended (container for logical partitions)
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-2145386495, default 2048):
    Last sector, +sectors or +size{K,M,G,T,P} (2048-2145386495, default 2145386495):
    
    Created a new partition 1 of type 'Linux' and of size 1023 GiB.
    ```    

1. <span data-ttu-id="89339-142">Geben Sie die Partitionstabelle mit dem Befehl `p` aus.</span><span class="sxs-lookup"><span data-stu-id="89339-142">Print the partition table with the `p` command.</span></span> <span data-ttu-id="89339-143">Das sollte in etwa so aussehen:</span><span class="sxs-lookup"><span data-stu-id="89339-143">It should look something like this:</span></span>

    ```output
    Disk /dev/sdc: 1023 GiB, 1098437885952 bytes, 2145386496 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 4096 bytes
    I/O size (minimum/optimal): 4096 bytes / 4096 bytes
    Disklabel type: dos
    Disk identifier: 0x1f2d0c46
    
    Device     Boot Start        End    Sectors  Size Id Type
    /dev/sdc1        2048 2145386495 2145384448 1023G 83 Linux
    ```
    
1. <span data-ttu-id="89339-144">Schreiben Sie die Änderungen mit dem Befehl `w`.</span><span class="sxs-lookup"><span data-stu-id="89339-144">Write the changes with the `w` command.</span></span> <span data-ttu-id="89339-145">Dadurch wird das Tool beendet.</span><span class="sxs-lookup"><span data-stu-id="89339-145">This will exit the tool.</span></span>

1. <span data-ttu-id="89339-146">Im nächsten Schritt schreiben Sie jetzt mit dem Befehl `mkfs` ein Dateisystem auf die Partition.</span><span class="sxs-lookup"><span data-stu-id="89339-146">Next, we need to write a file system to the partition with the `mkfs` command.</span></span> <span data-ttu-id="89339-147">Wir müssen den Dateisystemtyp und den Gerätenamen angeben, den wir aus der Ausgabe `fdisk` erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="89339-147">We will need to specify the file system type and device name which we got from the `fdisk` output.</span></span>
    - <span data-ttu-id="89339-148">Übergeben Sie `-t ext4`, um ein _ext4_-Dateisystem zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="89339-148">Pass `-t ext4` to create an _ext4_ filesystem.</span></span>
    - <span data-ttu-id="89339-149">Der Gerätename ist `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="89339-149">The device name is `/dev/sdc`.</span></span>

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
    
    <span data-ttu-id="89339-150">Die Ausführung dieses Befehls kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="89339-150">This command will take a few minutes to complete.</span></span>

    ```output
    mke2fs 1.44.1 (24-Mar-2018)
    Discarding device blocks: done
    Creating filesystem with 268173056 4k blocks and 67043328 inodes
    Filesystem UUID: e311c905-e0d9-43ab-af63-7f4ee4ef108e
    Superblock backups stored on blocks:
            32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
            4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968,
            102400000, 214990848
    
    Allocating group tables: done
    Writing inode tables: done
    Creating journal (262144 blocks): done
    Writing superblocks and filesystem accounting information: done
    ```

1. <span data-ttu-id="89339-151">Erstellen Sie im nächsten Schritt ein Verzeichnis, das als Bereitstellungspunkt verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="89339-151">Next, create a directory we will use as out mount point.</span></span> <span data-ttu-id="89339-152">Angenommen, es ist ein Ordner `data` vorhanden.</span><span class="sxs-lookup"><span data-stu-id="89339-152">Let's assume we will have a `data` folder.</span></span>

    ```bash
    sudo mkdir /data
    ```
1. <span data-ttu-id="89339-153">Verwenden Sie abschließend `mount` zum Anfügen des Datenträgers an den Bereitstellungspunkt.</span><span class="sxs-lookup"><span data-stu-id="89339-153">Finally, use `mount` to attach the disk to the mount point.</span></span>

    ```bash
    sudo mount /dev/sdc1 /data
    ```
    <span data-ttu-id="89339-154">Sie sollten `lsblk` verwenden können, um das bereitgestellte Laufwerk jetzt anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="89339-154">You should be able to use `lsblk` to see the mounted drive now.</span></span>
    
    ```output
    NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sda       8:0    0   30G  0 disk
    ├─sda1    8:1    0 29.9G  0 part /
    ├─sda14   8:14   0    4M  0 part
    └─sda15   8:15   0  106M  0 part /boot/efi
    sdb       8:16   0   16G  0 disk
    └─sdb1    8:17   0   16G  0 part /mnt
    sdc       8:32   0 1023G  0 disk
    └─sdc1    8:33   0 1023G  0 part /data
    sr0      11:0    1  628K  0 rom
    ```

### <a name="mounting-the-drive-automatically"></a><span data-ttu-id="89339-155">Automatisches Bereitstellen des Laufwerks</span><span class="sxs-lookup"><span data-stu-id="89339-155">Mounting the drive automatically</span></span>

<span data-ttu-id="89339-156">Um sicherzustellen, dass das Laufwerk nach einem Neustart automatisch bereitgestellt wird, muss es der Datei `/etc/fstab` hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="89339-156">To ensure that the drive is mounted automatically after a reboot, it must be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="89339-157">Außerdem wird dringend empfohlen, den UUID (Universally Unique Identifier) in `/etc/fstab` zu verwenden, um auf das Laufwerk und nicht auf den Gerätenamen (z.B. `/dev/sdc1`) zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="89339-157">It is also highly recommended that the UUID (Universally Unique Identifier) is used in `/etc/fstab` to refer to the drive rather than just the device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="89339-158">Wenn das Betriebssystem während des Starts einen Datenträgerfehler erkennt, wird durch den UUID verhindert, dass an einem bestimmten Ort der falsche Datenträger bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="89339-158">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="89339-159">Die verbleibenden Datenträger werden dann diesen Geräte-IDs zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="89339-159">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="89339-160">Verwenden Sie das Hilfsprogramm `blkid`, um den UUID des neuen Laufwerks herauszufinden:</span><span class="sxs-lookup"><span data-stu-id="89339-160">To find the UUID of the new drive, use the `blkid` utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="89339-161">Die Rückgabe ähnelt dem folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="89339-161">It will return something like:</span></span>

```output
/dev/sda1: UUID="36a59c42-c04c-4632-b83f-7015abd10358" TYPE="ext4"
/dev/sdb1: UUID="21092a62-79d4-4d8c-91de-4dd4e8b97d83" TYPE="ext4"
/dev/sdc1: UUID="e311c905-e0d9-43ab-af63-7f4ee4ef108e" TYPE="ext4"
```

1. <span data-ttu-id="89339-162">Kopieren Sie den UUID für das `/dev/sdc1`-Laufwerk, und öffnen Sie die Datei `/etc/fstab` in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="89339-162">Copy the UUID for the `/dev/sdc1` drive and open the `/etc/fstab` file in a text editor.</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

> [!WARNING]
> <span data-ttu-id="89339-163">Eine fehlerhafte Bearbeitung der Datei `/etc/fstab` könnte zu einem nicht startfähigen System führen.</span><span class="sxs-lookup"><span data-stu-id="89339-163">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="89339-164">Wenn Sie sich nicht sicher sind, helfen Ihnen die Informationen zur richtigen Bearbeitung dieser Datei in der Dokumentation weiter.</span><span class="sxs-lookup"><span data-stu-id="89339-164">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="89339-165">Außerdem wird empfohlen, eine Sicherung der Datei zu erstellen, bevor Sie sie bearbeiten, wenn Sie mit Produktionssystemen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="89339-165">It is also recommended that a backup of the file is created before editing when you are working with production systems.</span></span>

1. <span data-ttu-id="89339-166">Drücken Sie **G**, um zur letzten Zeile in der Datei zu gelangen.</span><span class="sxs-lookup"><span data-stu-id="89339-166">Press **G** to move to the last line in the file.</span></span>

1. <span data-ttu-id="89339-167">Drücken Sie **I**, um in den Einfügemodus zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="89339-167">Press **I** to enter INSERT mode.</span></span> <span data-ttu-id="89339-168">Der Modus sollte am unteren Rand des Bildschirms angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="89339-168">It should indicate the mode at the bottom of the screen.</span></span>

1. <span data-ttu-id="89339-169">Drücken Sie die **ENDE**-TASTE, um an das Ende der Zeile zu gelangen.</span><span class="sxs-lookup"><span data-stu-id="89339-169">Press the **END** key to move to the end of the line.</span></span> <span data-ttu-id="89339-170">Alternativ können Sie auch die Pfeiltasten verwenden.</span><span class="sxs-lookup"><span data-stu-id="89339-170">Alternatively, you can use the arrow keys.</span></span> <span data-ttu-id="89339-171">Drücken Sie die **EINGABETASTE**, um in eine neue Zeile zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="89339-171">Press **ENTER** to move to a new line.</span></span>

1. <span data-ttu-id="89339-172">Geben Sie die folgende Zeile in den Editor ein.</span><span class="sxs-lookup"><span data-stu-id="89339-172">Type the following line into the editor.</span></span> <span data-ttu-id="89339-173">Die Werte können durch Leerzeichen oder Tabstopps getrennt werden.</span><span class="sxs-lookup"><span data-stu-id="89339-173">The values can be space or tab separated.</span></span> <span data-ttu-id="89339-174">Weitere Informationen zu jeder der Spalten finden Sie in der Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="89339-174">Check the documentation for more information on each of the columns.</span></span>

    ```output
    UUID=<uuid-goes-here>    /data    ext4    defaults,nofail    1    2
    ```
1. <span data-ttu-id="89339-175">Drücken Sie **ESC**, und geben Sie dann **:w!** ein,</span><span class="sxs-lookup"><span data-stu-id="89339-175">Press **ESC**, then type **:w!**</span></span> <span data-ttu-id="89339-176">um die Datei zu schreiben, und **:q** zum Beenden des Editors.</span><span class="sxs-lookup"><span data-stu-id="89339-176">to write the file, and **:q** to quit the editor.</span></span>

1. <span data-ttu-id="89339-177">Abschließend überprüfen wir, ob der Eintrag richtig ist, indem wir das Betriebssystem auffordern, die Bereitstellungspunkte zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="89339-177">Finally, let's check to make sure the entry is correct by asking the OS to refresh the mount points.</span></span>

    ```bash
    sudo mount -a
    ```
    
    <span data-ttu-id="89339-178">Wenn ein Fehler zurückgegeben wird, bearbeiten Sie die Datei, um das Problem zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="89339-178">If it returns an error, edit the file to find the problem.</span></span>

> [!TIP]
> <span data-ttu-id="89339-179">Einige Linux-Kernel unterstützen TRIM zum Verwerfen ungenutzter Blöcke auf dem Datenträger.</span><span class="sxs-lookup"><span data-stu-id="89339-179">Some Linux kernels support TRIM to discard unused blocks on disks.</span></span> <span data-ttu-id="89339-180">Dieses Feature ist für Azure-Datenträger verfügbar und kann Ihnen Geld sparen, wenn Sie große Dateien erstellen und diese dann löschen.</span><span class="sxs-lookup"><span data-stu-id="89339-180">This feature is available on Azure disks and can save you money if you create large files and then delete them.</span></span> <span data-ttu-id="89339-181">Erfahren Sie in unserer Dokumentation, wie [dieses Feature aktiviert wird](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure).</span><span class="sxs-lookup"><span data-stu-id="89339-181">Learn how to [turn this feature on](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure) in our documentation.</span></span>

## <a name="install-software-onto-the-vm"></a><span data-ttu-id="89339-182">Installieren von Software auf dem virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="89339-182">Install software onto the VM</span></span>

<span data-ttu-id="89339-183">Es gibt mehrere Optionen zum Installieren von Software auf dem virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="89339-183">You have several options to install software onto the VM.</span></span> <span data-ttu-id="89339-184">Zunächst können Sie (wie bereits erwähnt) `scp` zum Kopieren lokaler Dateien von Ihrem Computer auf den virtuellen Computer verwenden.</span><span class="sxs-lookup"><span data-stu-id="89339-184">First, as mentioned, you can use `scp` to copy local files from your machine to the VM.</span></span> <span data-ttu-id="89339-185">Damit können Sie Daten oder benutzerdefinierte Anwendungen kopieren, die Sie ausführen möchten.</span><span class="sxs-lookup"><span data-stu-id="89339-185">This lets you copy over data, or custom applications you want to run.</span></span>

<span data-ttu-id="89339-186">Sie können auch Software über Secure Shell installieren.</span><span class="sxs-lookup"><span data-stu-id="89339-186">You can also install software through the secure shell.</span></span> <span data-ttu-id="89339-187">Azure-Computer sind standardmäßig mit dem Internet verbunden.</span><span class="sxs-lookup"><span data-stu-id="89339-187">Azure machines are by default, Internet-connected.</span></span> <span data-ttu-id="89339-188">Sie können die Standardbefehle verwenden, um beliebte Softwarepakete direkt aus den Standardrepositorys zu installieren.</span><span class="sxs-lookup"><span data-stu-id="89339-188">You can use standard commands to install popular software packages directly from standard repositories.</span></span> <span data-ttu-id="89339-189">Wir verwenden diesen Ansatz hier zum Installieren von Apache.</span><span class="sxs-lookup"><span data-stu-id="89339-189">Let's use this approach to install Apache.</span></span>

### <a name="install-apache-web-server"></a><span data-ttu-id="89339-190">Installieren des Apache-Webservers</span><span class="sxs-lookup"><span data-stu-id="89339-190">Install Apache web server</span></span>

<span data-ttu-id="89339-191">Apache ist in den Standardsoftwarerepositorys von Ubuntu verfügbar. Daher erfolgt die Installation mit herkömmlichen Paketverwaltungstools.</span><span class="sxs-lookup"><span data-stu-id="89339-191">Apache is available within Ubuntu's default software repositories, so we will install it using conventional package management tools.</span></span>

1. <span data-ttu-id="89339-192">Starten Sie, indem Sie den lokalen Paketindex aktualisieren, um die neuesten Upstreamänderungen widerzuspiegeln.</span><span class="sxs-lookup"><span data-stu-id="89339-192">Start by updating the local package index to reflect the latest upstream changes.</span></span>

    ```bash
    sudo apt-get update
    ```
    
1. <span data-ttu-id="89339-193">Installieren Sie im nächsten Schritt Apache.</span><span class="sxs-lookup"><span data-stu-id="89339-193">Next, install Apache.</span></span>

    ```bash
    sudo apt-get install apache2
    ```
    
1. <span data-ttu-id="89339-194">Der Start sollte automatisch erfolgen. Sie können den Status mit `systemctl` überprüfen:</span><span class="sxs-lookup"><span data-stu-id="89339-194">It should start automatically - we can check the status using `systemctl`:</span></span>

    ```bash
    sudo systemctl status apache2
    ```

    <span data-ttu-id="89339-195">Die Rückgabe sollte dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="89339-195">This should return something like:</span></span>

    ```output
    apache2.service - The Apache HTTP Server
       Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
      Drop-In: /lib/systemd/system/apache2.service.d
               └─apache2-systemd.conf
       Active: active (running) since Mon 2018-09-03 21:00:03 UTC; 1min 34s ago
     Main PID: 11156 (apache2)
        Tasks: 55 (limit: 4915)
       CGroup: /system.slice/apache2.service
               ├─11156 /usr/sbin/apache2 -k start
               ├─11158 /usr/sbin/apache2 -k start
               └─11159 /usr/sbin/apache2 -k start
    
    test-web-eus-vm1 systemd[1]: Starting The Apache HTTP Server...
    test-web-eus-vm1 apachectl[11129]: AH00558: apache2: Could not reliably determine the server's fully qua
    test-web-eus-vm1 systemd[1]: Started The Apache HTTP Server.
    ```

1. <span data-ttu-id="89339-196">Schließlich können wir versuchen, die Standardseite über die öffentliche IP-Adresse abzurufen.</span><span class="sxs-lookup"><span data-stu-id="89339-196">Finally, we can try retrieving the default page through the public IP address.</span></span> <span data-ttu-id="89339-197">Es sollte eine Standardseite zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="89339-197">It should return a default page.</span></span>

    ![Apache-Standardwebseite](../media-drafts/6-apache-works.png)

<span data-ttu-id="89339-199">Wie Sie sehen können, erlaubt SSH Ihnen die Arbeit mit dem virtuellen Linux-Computer wie mit einem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="89339-199">As you can see, SSH allows you to work with the Linux VM just like a local computer.</span></span> <span data-ttu-id="89339-200">Sie können diesen virtuellen Computer wie jeden anderen Linux-Computer verwalten: Sie können Software installieren, Rollen konfigurieren, Features anpassen und andere alltägliche Aufgaben ausführen.</span><span class="sxs-lookup"><span data-stu-id="89339-200">You can administer this VM as you would any other Linux computer: installing software, configuring roles, adjusting features and other everyday tasks.</span></span> <span data-ttu-id="89339-201">Allerdings handelt es sich um einen manuellen Prozess. Wenn Sie häufig Software installieren müssen, sollten Sie die Automatisierung des Prozesses mithilfe von Skripts in Betracht ziehen.</span><span class="sxs-lookup"><span data-stu-id="89339-201">However, it's a manual process - if we always need to install some software, you might consider automating the process using scripting.</span></span>
