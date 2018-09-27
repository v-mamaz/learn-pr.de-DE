<span data-ttu-id="5091d-101">Unsere Anwaltskanzlei ist dabei, ihre Fallzahl zu erhöhen, weshalb Sie mit der Einrichtung eines neuen Linux-Webservers beauftragt wurden, auf dem kritische Dokumente aus einer Vielzahl von Quellen gespeichert werden sollen. Dies können Klienten, anderen Kanzleien und Strafverfolgungsbehörden sein.</span><span class="sxs-lookup"><span data-stu-id="5091d-101">Our law firm is expanding it's case load and you have been tasked with putting up a new Linux web server to store critical documents from a variety of sources - clients, other law firms, and law enforcement offices.</span></span> <span data-ttu-id="5091d-102">Unser Server kann Uploads empfangen, die er auf Datenträger speichern soll.</span><span class="sxs-lookup"><span data-stu-id="5091d-102">Our server can accept uploads and needs to store them on disk.</span></span>

> [!TIP]
> <span data-ttu-id="5091d-103">In dieser Übung wird Linux als Beispiel verwendet, aber der grundlegende Prozess der Erstellung von VMs und des Hinzufügens von Datenträgern ist für Windows identisch.</span><span class="sxs-lookup"><span data-stu-id="5091d-103">This exercise uses Linux as the example, but the basic process of creating VMs and adding disks is the same for Windows.</span></span> <span data-ttu-id="5091d-104">Der Hauptunterschied besteht in der Partitionierung und Formatierung des Datenträgers, was in einer Remotedesktopsitzung mithilfe der integrierten Tools zur Datenträgerverwaltung erfolgen würde.</span><span class="sxs-lookup"><span data-stu-id="5091d-104">The primary difference would be in partitioning and formatting the disk - that would be done in a Remote Desktop session using the built-in Disk Management tools.</span></span>

<span data-ttu-id="5091d-105">Ziel dieser Übung ist, einen virtuellen Linux-Computer (VM) zu erstellen und eine neue virtuelle Festplatte (VHD) namens „uploadDataDisk1“ anzufügen, auf der das Verzeichnis „uploads“ gespeichert wird.</span><span class="sxs-lookup"><span data-stu-id="5091d-105">The goal of the exercise is to create a Linux virtual machine (VM) and attach a new virtual hard disk (VHD) named "uploadDataDisk1" to store the "uploads" directory.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-linux-vm"></a><span data-ttu-id="5091d-106">Erstellen eines virtuellen Linux-Computers</span><span class="sxs-lookup"><span data-stu-id="5091d-106">Create a Linux VM</span></span>

<span data-ttu-id="5091d-107">Wir erstellen mithilfe der Azure CLI eine Linux-VM zum Hosten unseres Webservers.</span><span class="sxs-lookup"><span data-stu-id="5091d-107">Let's create a Linux VM to host our web server using the Azure CLI.</span></span>

1. <span data-ttu-id="5091d-108">Legen Sie zuerst einige Standardeinstellungen für diese Sitzung fest.</span><span class="sxs-lookup"><span data-stu-id="5091d-108">Start by setting some defaults for this session.</span></span> <span data-ttu-id="5091d-109">Als Erstes müssen Sie die _Region_ der VM festlegen.</span><span class="sxs-lookup"><span data-stu-id="5091d-109">The first thing you need to decide is the _location_ to place the VM.</span></span> <span data-ttu-id="5091d-110">Im Idealfall befindet sich diese in der Nähe Ihrer Kunden.</span><span class="sxs-lookup"><span data-stu-id="5091d-110">Ideally this would be close to your clients.</span></span> <span data-ttu-id="5091d-111">Wählen Sie in diesem Fall die Region aus, die den für die Azure-Sandbox verfügbaren Standorten am nächsten ist.</span><span class="sxs-lookup"><span data-stu-id="5091d-111">In this case, select the closest region from the locations available to the Azure sandbox.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. <span data-ttu-id="5091d-112">Legen Sie mit dem Befehl `az configure` den gewünschte Standardstandort fest.</span><span class="sxs-lookup"><span data-stu-id="5091d-112">Use the `az configure` command to set the default location you want to use.</span></span> <span data-ttu-id="5091d-113">Ersetzen Sie „eastus“ durch diesen Standort.</span><span class="sxs-lookup"><span data-stu-id="5091d-113">Replace "eastus" with the location.</span></span>

    ```azurecli
    az configure --defaults location=eastus
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. <span data-ttu-id="5091d-114">Legen Sie den Standardwert für die Ressourcengruppe auf die vorkonfigurierte Ressourcengruppe fest, die für die Azure-Sandbox erstellt wurde: **<rgn>[Sandboxressourcengruppe]</rgn>**</span><span class="sxs-lookup"><span data-stu-id="5091d-114">Set the default resource group value to the pre-configured resource group created for the Azure sandbox: **<rgn>[sandbox resource group]</rgn>**</span></span>

    ```azurecli
    az configure --defaults group="<rgn>[sandbox Resource Group]</rgn>"
    ```

1. <span data-ttu-id="5091d-115">Erstellen Sie als Nächstes mit dem Befehl `vm create` eine neue Ubuntu Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="5091d-115">Next, use the `vm create` command to create a new Ubuntu Linux VM.</span></span>
    - <span data-ttu-id="5091d-116">Nennen Sie sie „support-web-vm01“.</span><span class="sxs-lookup"><span data-stu-id="5091d-116">Name it "support-web-vm01".</span></span>
    - <span data-ttu-id="5091d-117">Legen Sie **Größe** auf _Standard_DS2_v2_ fest.</span><span class="sxs-lookup"><span data-stu-id="5091d-117">Set the **size** to _Standard_DS2_v2_.</span></span>
    - <span data-ttu-id="5091d-118">Legen Sie den **Administratorbenutzernamen** auf „azureuser“ (oder einen Namen Ihrer Wahl fest).</span><span class="sxs-lookup"><span data-stu-id="5091d-118">Set the **admin-username** to "azureuser" (or whatever you prefer).</span></span>
    - <span data-ttu-id="5091d-119">Generieren Sie mit dem Parameter `--generate-ssh-keys` SSH-Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="5091d-119">Generate SSH keys with the `--generate-ssh-keys` parameter.</span></span>

    ```azurecli
    az vm create --name support-web-vm01 \
        --image UbuntuLTS \
        --size Standard_DS2_v2 \
        --admin-username azureuser \
        --generate-ssh-keys
    ```
    
    > [!TIP]
    > <span data-ttu-id="5091d-120">Das Erstellen Ihrer VM und deren Bereitstellung in Azure kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="5091d-120">Creating your VM and deploying it in Azure can take a few minutes.</span></span> <span data-ttu-id="5091d-121">Sie können den Fortschritt in Cloud Shell überwachen.</span><span class="sxs-lookup"><span data-stu-id="5091d-121">You can watch the progress in the Cloud Shell.</span></span>
    
1. <span data-ttu-id="5091d-122">Das Ergebnis ist ein JSON-Block mit den Details zur erstellten VM.</span><span class="sxs-lookup"><span data-stu-id="5091d-122">This will result in a JSON block with the details about the created VM.</span></span>

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
    <span data-ttu-id="5091d-123">Notieren Sie sich **publicIpAddress** in der Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="5091d-123">Note of the **publicIpAddress** in your output.</span></span> <span data-ttu-id="5091d-124">Hierüber können wir remote auf die VM zugreifen.</span><span class="sxs-lookup"><span data-stu-id="5091d-124">This is how we can access the VM remotely.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5091d-125">Wir verwenden diese VM, um uns mit der Verwaltung von Datenträgern vertraut zu machen.</span><span class="sxs-lookup"><span data-stu-id="5091d-125">We are using this VM to learn how to manage disks.</span></span> <span data-ttu-id="5091d-126">Wenn wir sie tatsächlich als Webserver verwenden würden, würden wir mit dem Befehl `az vm open-port` zusätzliche Ports öffnen und Webserversoftware installieren.</span><span class="sxs-lookup"><span data-stu-id="5091d-126">If we were truly going to use it as a web server, we'd want to open up additional ports with the `az vm open-port` command, and install web server software.</span></span> <span data-ttu-id="5091d-127">Diese Aufgaben sind nicht Bestandteil dieses Moduls, doch im Modul **Verwalten virtueller Computer mit der Azure CLI** erfahren Sie, wie diese Schritte erfolgen.</span><span class="sxs-lookup"><span data-stu-id="5091d-127">These tasks are outside the scope of this module, but you can go through the **Manage virtual machines with the Azure CLI** module to learn how to do these steps.</span></span> 

## <a name="add-an-empty-data-disk-to-our-vm"></a><span data-ttu-id="5091d-128">Hinzufügen eines leeren Datenträgers zur VM</span><span class="sxs-lookup"><span data-stu-id="5091d-128">Add an empty data disk to our VM</span></span>

<span data-ttu-id="5091d-129">Wir nennen den Datenträger, auf dem das Verzeichnis „uploads“ für Ihren Webserver gespeichert wird, „uploadDataDisk1“.</span><span class="sxs-lookup"><span data-stu-id="5091d-129">We're going to name the disk that stores the "uploads" directory for your web server "uploadDataDisk1".</span></span> 

> [!TIP]
> <span data-ttu-id="5091d-130">Sie können Datenträger hinzufügen, wenn die VM erstellt wird, indem Sie im Befehl `vm create` den Parameter `--data-disk-sizes-gb` angeben.</span><span class="sxs-lookup"><span data-stu-id="5091d-130">You can add data disks when the VM is created using the `--data-disk-sizes-gb` parameter on the `vm create` command.</span></span>

1. <span data-ttu-id="5091d-131">Fügen Sie einen neuen leeren Datenträger mit dem Befehl `vm disk attach` an den Server an.</span><span class="sxs-lookup"><span data-stu-id="5091d-131">Add a new empty disk to the server with the `vm disk attach` command.</span></span>
    - <span data-ttu-id="5091d-132">Nennen Sie ihn „uploadDataDisk1“.</span><span class="sxs-lookup"><span data-stu-id="5091d-132">Name it "uploadDataDisk1"</span></span>
    - <span data-ttu-id="5091d-133">Legen Sie seine Größe auf 64 GB fest.</span><span class="sxs-lookup"><span data-stu-id="5091d-133">Set it to be 64 GB.</span></span>
    - <span data-ttu-id="5091d-134">Legen Sie **sku** auf _Premium_LRS_ fest, damit wir Storage Premium mit lokaler Redundanz nutzen können.</span><span class="sxs-lookup"><span data-stu-id="5091d-134">Set the **sku** to "_Premium_LRS_" so we use premium storage with local redundancy.</span></span>

    ```azurecli
    az vm disk attach \
        --vm-name support-web-vm01 \
        --disk uploadDataDisk1 \
        --size-gb 64 \
        --sku Premium_LRS \
        --new
    ```
    
<span data-ttu-id="5091d-135">Wir haben soeben einen Datenträger namens „uploadDataDisk1“ definiert.</span><span class="sxs-lookup"><span data-stu-id="5091d-135">We've now defined a disk named "uploadDataDisk1" .</span></span> <span data-ttu-id="5091d-136">Um den Datenträger verwenden zu können, müssen wir ihn partitionieren und formatieren.</span><span class="sxs-lookup"><span data-stu-id="5091d-136">To use the disk, we'll need to partition and format it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="5091d-137">Initialisieren von Laufwerken</span><span class="sxs-lookup"><span data-stu-id="5091d-137">Initialize data disks</span></span>

<span data-ttu-id="5091d-138">Alle zusätzlichen Laufwerke, die Sie neu erstellen, müssen initialisiert und formatiert werden.</span><span class="sxs-lookup"><span data-stu-id="5091d-138">Any additional drives you create from scratch will need to be initialized and formatted.</span></span> <span data-ttu-id="5091d-139">Der Prozess ist der gleiche wie bei einem physischen Datenträger:</span><span class="sxs-lookup"><span data-stu-id="5091d-139">The process for doing this is identical to a physical disk:</span></span>

1. <span data-ttu-id="5091d-140">Stellen Sie zuerst über SSH eine Verbindung mit dem Linux-Server her, indem Sie die öffentliche IP-Adresse verwenden, die Sie bei der ersten Erstellung der VM erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="5091d-140">First, SSH into the Linux server using the public IP address you got back from the original VM creation response.</span></span> <span data-ttu-id="5091d-141">Wenn Ihnen diese nicht vorliegt, können Sie den folgenden Befehl verwenden, um die IP-Adresse abzurufen:</span><span class="sxs-lookup"><span data-stu-id="5091d-141">If you don't have that, you can use the following command to get the IP address:</span></span>

    ```azurecli
    az vm list-ip-addresses -n support-web-vm01
    ```

1. <span data-ttu-id="5091d-142">Verwenden Sie SSH mit der öffentlichen IP-Adresse und dem Benutzernamen, den Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="5091d-142">Use SSH with the public IP and the username you created.</span></span>

    ```bash
    ssh azureuser@40.76.193.249
    ```

1. <span data-ttu-id="5091d-143">Identifizieren Sie dann den Datenträger mit dem Befehl `lsblk`, um alle Blockgeräte aufzulisten – hier sehen Sie die vorhandenen Laufwerke.</span><span class="sxs-lookup"><span data-stu-id="5091d-143">Next, identify the disk with the `lsblk` command to list all the block devices - here you will see your drives.</span></span>

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

<span data-ttu-id="5091d-144">Suchen Sie nach dem 64-GB-Laufwerk, das wir erstellt haben. Hier sehen Sie, dass es **sdc** heißt und nicht bereitgestellt ist. Das liegt daran, dass es nicht initialisiert wurde.</span><span class="sxs-lookup"><span data-stu-id="5091d-144">Look for the 64 GB drive we created - here you can see it's **sdc** and it's not mounted - this is because it's not been initialized.</span></span>

1. <span data-ttu-id="5091d-145">Sobald Sie das Laufwerk (**sdc**) kennen, das initialisiert werden muss, können Sie `fdisk` zu diesem Zweck verwenden.</span><span class="sxs-lookup"><span data-stu-id="5091d-145">Once you know the drive (**sdc**) you need to initialize, you can use `fdisk` to do that.</span></span> <span data-ttu-id="5091d-146">Sie müssen den Befehl mit `sudo` ausführen und den Datenträger angeben, der partitioniert werden soll:</span><span class="sxs-lookup"><span data-stu-id="5091d-146">You will need to run the command with `sudo` and supply the disk you want to partition:</span></span>

    ```bash
    sudo fdisk /dev/sdc
    ```

1. <span data-ttu-id="5091d-147">Verwenden Sie den Befehl <kbd>n</kbd>, um eine neue Partition hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="5091d-147">Use the <kbd>n</kbd> command to add a new partition.</span></span> <span data-ttu-id="5091d-148">In diesem Beispiel haben wir auch <kbd>p</kbd> als primäre Partition ausgewählt und übernehmen den Rest der Standardwerte.</span><span class="sxs-lookup"><span data-stu-id="5091d-148">In this example, we also choose <kbd>p</kbd> for a primary partition and accept the rest of the default values.</span></span> <span data-ttu-id="5091d-149">Die Ausgabe entspricht etwa folgendem Beispiel:</span><span class="sxs-lookup"><span data-stu-id="5091d-149">The output will be similar to the following example:</span></span>   

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

1. <span data-ttu-id="5091d-150">Geben Sie die Partitionstabelle mit dem Befehl <kbd>p</kbd> aus.</span><span class="sxs-lookup"><span data-stu-id="5091d-150">Print the partition table with the <kbd>p</kbd> command.</span></span> <span data-ttu-id="5091d-151">Sie sollte in etwa so aussehen:</span><span class="sxs-lookup"><span data-stu-id="5091d-151">It should look something like this:</span></span>

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

1. <span data-ttu-id="5091d-152">Schreiben Sie die Änderungen mit dem Befehl <kbd>w<kbd>.</span><span class="sxs-lookup"><span data-stu-id="5091d-152">Write the changes with the <kbd>w<kbd> command.</span></span> <span data-ttu-id="5091d-153">Dadurch wird das Tool beendet.</span><span class="sxs-lookup"><span data-stu-id="5091d-153">This will exit the tool.</span></span>

1. <span data-ttu-id="5091d-154">Im nächsten Schritt schreiben Sie jetzt mit dem Befehl `mkfs` ein Dateisystem auf die Partition.</span><span class="sxs-lookup"><span data-stu-id="5091d-154">Next, we need to write a file system to the partition with the `mkfs` command.</span></span> <span data-ttu-id="5091d-155">Wir müssen den Dateisystemtyp und den Gerätenamen angeben, den wir aus der Ausgabe `fdisk` erhalten haben:</span><span class="sxs-lookup"><span data-stu-id="5091d-155">We will need to specify the file system type and device name that we got from the `fdisk` output:</span></span>
    - <span data-ttu-id="5091d-156">Übergeben Sie `-t ext4`, um ein _ext4_-Dateisystem zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5091d-156">Pass `-t ext4` to create an _ext4_ filesystem.</span></span>
    - <span data-ttu-id="5091d-157">Der Gerätename ist `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="5091d-157">The device name is `/dev/sdc`.</span></span>

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
    
    <span data-ttu-id="5091d-158">Die Ausführung dieses Befehls kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="5091d-158">This command will take a minute or so to complete.</span></span>

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
    
1. <span data-ttu-id="5091d-159">Erstellen Sie im nächsten Schritt ein Verzeichnis, das als Bereitstellungspunkt verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="5091d-159">Next, create a directory we will use as our mount point.</span></span> <span data-ttu-id="5091d-160">Angenommen, es ist ein Ordner `uploads` vorhanden:</span><span class="sxs-lookup"><span data-stu-id="5091d-160">Let's assume we will have a `uploads` folder:</span></span>

    ```bash
    sudo mkdir /uploads
    ```
1. <span data-ttu-id="5091d-161">Verwenden Sie abschließend `mount` zum Anfügen des Datenträgers an den Bereitstellungspunkt:</span><span class="sxs-lookup"><span data-stu-id="5091d-161">Finally, use `mount` to attach the disk to the mount point:</span></span>

    ```bash
    sudo mount /dev/sdc1 /uploads
    ```
    <span data-ttu-id="5091d-162">Sie sollten `lsblk` verwenden können, um das bereitgestellte Laufwerk jetzt anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="5091d-162">You should be able to use `lsblk` to see the mounted drive now:</span></span>
    
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
    
### <a name="mounting-the-drive-automatically"></a><span data-ttu-id="5091d-163">Automatisches Bereitstellen des Laufwerks</span><span class="sxs-lookup"><span data-stu-id="5091d-163">Mounting the drive automatically</span></span>

<span data-ttu-id="5091d-164">Um sicherzustellen, dass das Laufwerk nach einem Neustart automatisch bereitgestellt wird, muss es der Datei `/etc/fstab` hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="5091d-164">To ensure that the drive is mounted automatically after a reboot, it must be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="5091d-165">Außerdem wird dringend empfohlen, den UUID (Universally Unique Identifier) in `/etc/fstab` zu verwenden, um auf das Laufwerk und nicht auf den Gerätenamen (z.B. `/dev/sdc1`) zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="5091d-165">It is also highly recommended that the UUID (universally unique identifier) is used in `/etc/fstab` to refer to the drive rather than just the device name (such as `/dev/sdc1`).</span></span> <span data-ttu-id="5091d-166">Wenn das Betriebssystem während des Starts einen Datenträgerfehler erkennt, wird durch den UUID verhindert, dass an einem bestimmten Ort der falsche Datenträger bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="5091d-166">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="5091d-167">Die verbleibenden Datenträger werden dann diesen Geräte-IDs zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="5091d-167">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="5091d-168">Verwenden Sie das Hilfsprogramm `blkid`, um den UUID des neuen Laufwerks herauszufinden:</span><span class="sxs-lookup"><span data-stu-id="5091d-168">To find the UUID of the new drive, use the `blkid` utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="5091d-169">Die Rückgabe ähnelt dem folgenden Beispiel:</span><span class="sxs-lookup"><span data-stu-id="5091d-169">It will return something like:</span></span>

```output
/dev/sda1: UUID="36a59c42-c04c-4632-b83f-7015abd10358" TYPE="ext4"
/dev/sdb1: UUID="21092a62-79d4-4d8c-91de-4dd4e8b97d83" TYPE="ext4"
/dev/sdc1: UUID="e311c905-e0d9-43ab-af63-7f4ee4ef108e" TYPE="ext4"
```

1. <span data-ttu-id="5091d-170">Kopieren Sie den UUID für das Laufwerk `/dev/sdc1`, und öffnen Sie die Datei `/etc/fstab` in einem Text-Editor:</span><span class="sxs-lookup"><span data-stu-id="5091d-170">Copy the UUID for the `/dev/sdc1` drive and open the `/etc/fstab` file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

> [!WARNING]
> <span data-ttu-id="5091d-171">Eine fehlerhafte Bearbeitung der Datei `/etc/fstab` kann zu einem nicht startfähigen System führen.</span><span class="sxs-lookup"><span data-stu-id="5091d-171">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="5091d-172">Wenn Sie sich nicht sicher sind, helfen Ihnen die Informationen zur richtigen Bearbeitung dieser Datei in der Dokumentation weiter.</span><span class="sxs-lookup"><span data-stu-id="5091d-172">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="5091d-173">Außerdem wird empfohlen, eine Sicherung der Datei zu erstellen, bevor Sie sie bearbeiten, wenn Sie mit Produktionssystemen arbeiten.</span><span class="sxs-lookup"><span data-stu-id="5091d-173">It is also recommended that a backup of the file is created before editing when you are working with production systems.</span></span>

1. <span data-ttu-id="5091d-174">Drücken Sie <kbd>G</kbd>, um zur letzten Zeile in der Datei zu gelangen.</span><span class="sxs-lookup"><span data-stu-id="5091d-174">Press <kbd>G</kbd> to move to the last line in the file.</span></span>

1. <span data-ttu-id="5091d-175">Drücken Sie <kbd>I</kbd>, um in den Einfügemodus zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="5091d-175">Press <kbd>I</kbd> to enter INSERT mode.</span></span> <span data-ttu-id="5091d-176">Der Modus sollte am unteren Rand des Bildschirms angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5091d-176">It should indicate the mode at the bottom of the screen.</span></span>

1. <span data-ttu-id="5091d-177">Drücken Sie die <kbd>ENDE</kbd>-TASTE, um an das Ende der Zeile zu gelangen.</span><span class="sxs-lookup"><span data-stu-id="5091d-177">Press the <kbd>END</kbd> key to move to the end of the line.</span></span> <span data-ttu-id="5091d-178">Alternativ können Sie auch die Pfeiltasten verwenden.</span><span class="sxs-lookup"><span data-stu-id="5091d-178">Alternatively, you can use the arrow keys.</span></span> <span data-ttu-id="5091d-179">Drücken Sie die <kbd>EINGABETASTE</kbd>, um in eine neue Zeile zu wechseln.</span><span class="sxs-lookup"><span data-stu-id="5091d-179">Press <kbd>ENTER</kbd> to move to a new line.</span></span>

1. <span data-ttu-id="5091d-180">Geben Sie die folgende Zeile in den Editor ein.</span><span class="sxs-lookup"><span data-stu-id="5091d-180">Type the following line into the editor.</span></span> <span data-ttu-id="5091d-181">Die Werte können durch Leerzeichen oder Tabstopps getrennt werden.</span><span class="sxs-lookup"><span data-stu-id="5091d-181">The values can be space or tab separated.</span></span> <span data-ttu-id="5091d-182">Weitere Informationen zu jeder der Spalten finden Sie in der Dokumentation:</span><span class="sxs-lookup"><span data-stu-id="5091d-182">Check the documentation for more information on each of the columns:</span></span>

    ```output
    UUID=<uuid-goes-here>    /uploads    ext4    defaults,nofail    1    2
    ```
1. <span data-ttu-id="5091d-183">Drücken Sie **ESC**, und geben Sie dann **:w!** ein,</span><span class="sxs-lookup"><span data-stu-id="5091d-183">Press **ESC**, then type **:w!**</span></span> <span data-ttu-id="5091d-184">um die Datei zu schreiben, und **:q** zum Beenden des Editors.</span><span class="sxs-lookup"><span data-stu-id="5091d-184">to write the file and **:q** to quit the editor.</span></span>

1. <span data-ttu-id="5091d-185">Abschließend überprüfen wir, ob der Eintrag richtig ist, indem wir das Betriebssystem auffordern, die Bereitstellungspunkte zu aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="5091d-185">Finally, let's check to make sure the entry is correct by asking the OS to refresh the mount points:</span></span>

    ```bash
    sudo mount -a
    ```

    <span data-ttu-id="5091d-186">Wenn ein Fehler zurückgegeben wird, bearbeiten Sie die Datei, um das Problem zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="5091d-186">If it returns an error, edit the file to find the problem.</span></span>

> [!TIP]
> <span data-ttu-id="5091d-187">Einige Linux-Kernel unterstützen TRIM zum Verwerfen ungenutzter Blöcke auf dem Datenträger.</span><span class="sxs-lookup"><span data-stu-id="5091d-187">Some Linux kernels support TRIM to discard unused blocks on disks.</span></span> <span data-ttu-id="5091d-188">Dieses Feature ist für Azure-Datenträger verfügbar und kann Ihnen Geld sparen, wenn Sie große Dateien erstellen und diese dann löschen.</span><span class="sxs-lookup"><span data-stu-id="5091d-188">This feature is available on Azure disks and can save you money if you create large files and then delete them.</span></span> <span data-ttu-id="5091d-189">Erfahren Sie in unserer Dokumentation, wie [dieses Feature aktiviert wird](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure).</span><span class="sxs-lookup"><span data-stu-id="5091d-189">Learn how to [turn this feature on](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure) in our documentation.</span></span>

<span data-ttu-id="5091d-190">Nachdem Sie erfahren haben, wie einfach es ist, Datenträger zu Ihren VMs hinzuzufügen, schauen wir uns nun an, welche Arten von Datenträgern Sie erstellen können.</span><span class="sxs-lookup"><span data-stu-id="5091d-190">Now that you've seen how easy it is to add disks to your VMs, let's explore a bit more about the types of disks you might create.</span></span> <span data-ttu-id="5091d-191">Wir beschäftigen uns insbesondere mit dem Unterschied zwischen den Storage-Tarifen Standard und Premium.</span><span class="sxs-lookup"><span data-stu-id="5091d-191">In particular the choice between Standard and Premium storage.</span></span>