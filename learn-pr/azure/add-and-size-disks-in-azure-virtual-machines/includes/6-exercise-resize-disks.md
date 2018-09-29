<span data-ttu-id="a6288-101">Wir haben die Größe einiger der Uploads unterschätzt, weshalb unser Datenträger für Uploads keinen Speicherplatz mehr hat.</span><span class="sxs-lookup"><span data-stu-id="a6288-101">We underestimated how big some of the uploads would be and our upload disk is running out of space.</span></span> <span data-ttu-id="a6288-102">Sie beschließen, den Speicherplatz zu verdoppeln und ihn von 64 GB auf 128 GB zu vergrößern.</span><span class="sxs-lookup"><span data-stu-id="a6288-102">You decide to double the space and upgrade it from 64 GB to 128 GB.</span></span>

## <a name="resize-the-data-disk"></a><span data-ttu-id="a6288-103">Ändern der Größe des Datenträgers</span><span class="sxs-lookup"><span data-stu-id="a6288-103">Resize the data disk</span></span>

<span data-ttu-id="a6288-104">Zum Ändern der Größe eines Datenträgers benötigen wir die ID oder den Namen des Datenträgers.</span><span class="sxs-lookup"><span data-stu-id="a6288-104">To resize a disk, we need the ID or name of the disk.</span></span> <span data-ttu-id="a6288-105">In diesem Fall kennen wir den Namen (uploadDataDisk1) bereits.</span><span class="sxs-lookup"><span data-stu-id="a6288-105">In this case we already know the name (uploadDataDisk1).</span></span> <span data-ttu-id="a6288-106">Aber für den Fall, dass Sie sich nicht daran erinnern oder er von jemand anderem festgelegt wurde, können wir mit dem Befehl `az disk list` eine Liste der Datenträger abrufen.</span><span class="sxs-lookup"><span data-stu-id="a6288-106">But in case we didn't remember that, or it was created by someone else we can get a list of disks using the `az disk list` command.</span></span>

1. <span data-ttu-id="a6288-107">Beginnen Sie, indem Sie eine Liste der verwalteten Datenträger in der Ressourcengruppe abrufen. Dies kann auch andere Datenträger umfassen, wenn in einer einzelnen Ressourcengruppe mehrere VMs vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="a6288-107">Start by getting a list of the managed disks in the resource group; this might include other disks if you have multiple VMs in a single resource group.</span></span> <span data-ttu-id="a6288-108">Bei unserem Beispiel sollte es nur unseren Webserver geben.</span><span class="sxs-lookup"><span data-stu-id="a6288-108">For our example, there should just be our web server.</span></span>

    ```azurecli
    az disk list \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

1. <span data-ttu-id="a6288-109">Beenden Sie als Nächstes die VM, und heben Sie mit `az vm deallocate` ihre Zuordnung auf.</span><span class="sxs-lookup"><span data-stu-id="a6288-109">Next, stop and deallocate the VM using `az vm deallocate`.</span></span> 

    ```azurecli
    az vm deallocate --name support-web-vm01
    ```
1. <span data-ttu-id="a6288-110">Nun können wir die Größe des Datenträgers mit dem Befehl `az disk update` ändern.</span><span class="sxs-lookup"><span data-stu-id="a6288-110">Now we can resize the disk with the `az disk update` command.</span></span>

    ```azurecli
    az disk update --name uploadDataDisk1 --size-gb 128
    ```
    
1. <span data-ttu-id="a6288-111">Starten Sie die VM nach Abschluss der Größenänderung neu.</span><span class="sxs-lookup"><span data-stu-id="a6288-111">Once the resize operation has completed, restart the VM.</span></span>

    ```azurecli
    az vm start --name support-web-vm01
    ```

## <a name="expand-the-disk-partition"></a><span data-ttu-id="a6288-112">Erweitern der Datenträgerpartition</span><span class="sxs-lookup"><span data-stu-id="a6288-112">Expand the disk partition</span></span>

<span data-ttu-id="a6288-113">Der letzte Schritt besteht darin, das Betriebssystem über den verfügbaren Speicherplatz zu informieren.</span><span class="sxs-lookup"><span data-stu-id="a6288-113">The final step is to tell the OS about the available space.</span></span> <span data-ttu-id="a6288-114">Genau wie bei den vorherigen Partitionierungs- und Formatierungsschritten ist dieser Prozess für die Erweiterung lokaler Datenträger identisch.</span><span class="sxs-lookup"><span data-stu-id="a6288-114">Just like the partitioning and format steps we did earlier, this process is identical for on-premise disk expansions.</span></span> 

1. <span data-ttu-id="a6288-115">Rufen Sie zunächst die öffentliche IP-Adresse Ihrer VM ab.</span><span class="sxs-lookup"><span data-stu-id="a6288-115">First, get the public IP address of your VM.</span></span> <span data-ttu-id="a6288-116">Da sie neu gestartet wurde, hat sie sich wahrscheinlich geändert.</span><span class="sxs-lookup"><span data-stu-id="a6288-116">Since it was rebooted, it has likely changed.</span></span> <span data-ttu-id="a6288-117">Versuchen wir es diesmal mit einem anderen Ansatz, indem wir `az vm show` mit einem Filter verwenden, um die öffentliche IP-Adresse zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="a6288-117">Let's try a different approach this time and use `az vm show` with a filter to return the public IP address.</span></span>

    > [!TIP]
    > <span data-ttu-id="a6288-118">IP-Adressen sind standardmäßig dynamisch.</span><span class="sxs-lookup"><span data-stu-id="a6288-118">IP addresses are dynamic by default.</span></span> <span data-ttu-id="a6288-119">Azure DNS gleicht die Änderung der IP-Adresse automatisch aus, oder Sie können das Verhalten ändern, indem Sie statische IP-Adressen verwenden.</span><span class="sxs-lookup"><span data-stu-id="a6288-119">Azure DNS will automatically compensate for the IP change, or you can alter the behavior by using static IP addresses.</span></span>

    ```azurecli
    az vm show --name support-web-vm01 -d --query [publicIps] --o tsv
    ```
    
1. <span data-ttu-id="a6288-120">Verbinden Sie sich per SSH mit der Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="a6288-120">SSH into the Linux machine.</span></span> <span data-ttu-id="a6288-121">Sie müssen die richtige IP-Adresse angeben.</span><span class="sxs-lookup"><span data-stu-id="a6288-121">You will need to supply your correct IP address.</span></span>

    ```bash
    ssh azureuser@40.76.193.249
    ```

1. <span data-ttu-id="a6288-122">Heben Sie die Bereitstellung des Datenträgers auf.</span><span class="sxs-lookup"><span data-stu-id="a6288-122">Unmount the disk.</span></span> <span data-ttu-id="a6288-123">Zur Erinnerung: Der Name war `/dev/sdc1`.</span><span class="sxs-lookup"><span data-stu-id="a6288-123">Recall that it was `/dev/sdc1`.</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

1. <span data-ttu-id="a6288-124">Starten Sie `parted` in einer Shell mit erhöhten Rechten.</span><span class="sxs-lookup"><span data-stu-id="a6288-124">Launch `parted` in an elevated shell</span></span>

    ```bash
    sudo parted /dev/sdc
    ```
    
1. <span data-ttu-id="a6288-125">Erweitern Sie die Partition mit dem Befehl `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="a6288-125">Expand the partition with the `resizepart` command.</span></span> <span data-ttu-id="a6288-126">Geben Sie Partition 1 und die neue Größe (128 GB) ein.</span><span class="sxs-lookup"><span data-stu-id="a6288-126">Enter partition 1 and the new size (128GB).</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [64GB]? 128GB
    ```

    > [!WARNING]
    > <span data-ttu-id="a6288-127">Achten Sie auf die Größe.</span><span class="sxs-lookup"><span data-stu-id="a6288-127">Be careful about the size.</span></span> <span data-ttu-id="a6288-128">Die Größenänderung der Partition ermöglicht Ihnen, auch eine Partition zu verkleinern, was wahrscheinlich zu Datenverlust führen wird.</span><span class="sxs-lookup"><span data-stu-id="a6288-128">Resizing the partition allows you to shrink a partition too, and that will likely result in data loss.</span></span>
    
1. <span data-ttu-id="a6288-129">Beenden Sie das Tool durch Eingabe von `quit`.</span><span class="sxs-lookup"><span data-stu-id="a6288-129">Exit the tool by typing `quit`.</span></span>

1. <span data-ttu-id="a6288-130">Das Partitionierungstool stellt das Laufwerk automatisch _erneut bereit_.</span><span class="sxs-lookup"><span data-stu-id="a6288-130">The partition tool will automatically _remount_ the drive.</span></span> <span data-ttu-id="a6288-131">Heben Sie deshalb die Bereitstellung erneut auf, damit es formatiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="a6288-131">So unmount it again so we can format it.</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```
    
1. <span data-ttu-id="a6288-132">Überprüfen Sie die Partitionskonsistenz mit `e2fsck`.</span><span class="sxs-lookup"><span data-stu-id="a6288-132">Verify the partition consistency with `e2fsck`.</span></span> <span data-ttu-id="a6288-133">Dieser Schritt ist absolut notwendig, aber auch immer dann eine gute Idee, wenn Sie Größen auf einem Datenträgervolume ändern.</span><span class="sxs-lookup"><span data-stu-id="a6288-133">This step is absolutely necessary but is a good idea any time you are changing sizes on a disk volume.</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

1. <span data-ttu-id="a6288-134">Ändern Sie die Größe des Dateisystems mit `resize2fs`.</span><span class="sxs-lookup"><span data-stu-id="a6288-134">Resize the filesystem with `resize2fs`.</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

1. <span data-ttu-id="a6288-135">Stellen Sie das Laufwerk schließlich wieder am Bereitstellungspunkt bereit.</span><span class="sxs-lookup"><span data-stu-id="a6288-135">Finally, mount the drive back to the mount point.</span></span>

    ```bash
    sudo mount /dev/sdc1 /uploads
    ```

<span data-ttu-id="a6288-136">Verwenden Sie `df -h`, um zu überprüfen, ob die Größe des Betriebssystem-Datenträgers geändert wurde.</span><span class="sxs-lookup"><span data-stu-id="a6288-136">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="a6288-137">Sie sollte nun mit 128 GB angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="a6288-137">It should now show that the drive is 128 GB.</span></span>
