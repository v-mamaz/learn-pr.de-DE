<span data-ttu-id="4efba-101">Der virtuelle Linux-Computer wurde bereitgestellt und wird ausgeführt, aber noch nicht für die Arbeit konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="4efba-101">We have our Linux VM deployed and running, but it's not configured to do any work.</span></span> <span data-ttu-id="4efba-102">Stellen wir eine Verbindung mit SSH her, und konfigurieren wir Apache, damit wir über einen Webserver verfügen, der ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="4efba-102">Let's connect to it with SSH and configure Apache, so we have a running web server.</span></span>

## <a name="connect-to-the-vm-with-ssh"></a><span data-ttu-id="4efba-103">Herstellen einer Verbindung mit dem virtuellen Computer mit SSH</span><span class="sxs-lookup"><span data-stu-id="4efba-103">Connect to the VM with SSH</span></span>

<span data-ttu-id="4efba-104">Zum Herstellen der Verbindung eines virtuellen Azure-Computers mit einem SSH-Client benötigen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="4efba-104">To connect to an Azure VM with an SSH client, you will need:</span></span>

- <span data-ttu-id="4efba-105">SSH-Clientsoftware (in den meisten modernen Betriebssystemen vorhanden)</span><span class="sxs-lookup"><span data-stu-id="4efba-105">SSH client software (present on most modern operating systems)</span></span>
- <span data-ttu-id="4efba-106">Die öffentliche IP-Adresse des virtuellen Computers (oder die private, wenn der virtuelle Computer dafür konfiguriert ist, eine Verbindung mit Ihrem Netzwerk herzustellen)</span><span class="sxs-lookup"><span data-stu-id="4efba-106">The public IP address of the VM (or private if the VM is configured to connect to your network)</span></span>

### <a name="get-the-public-ip-address"></a><span data-ttu-id="4efba-107">Abrufen der öffentlichen IP-Adresse</span><span class="sxs-lookup"><span data-stu-id="4efba-107">Get the public IP address</span></span>

1. <span data-ttu-id="4efba-108">Stellen Sie im [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) sicher, dass der Bereich **Übersicht** für den zuvor erstellten virtuellen Computer geöffnet ist.</span><span class="sxs-lookup"><span data-stu-id="4efba-108">In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), ensure the **Overview** panel for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="4efba-109">Sie finden den virtuellen Computer unter **Alle Ressourcen**, falls Sie diesen öffnen müssen.</span><span class="sxs-lookup"><span data-stu-id="4efba-109">You can find the VM under **All Resources** if you need to open it.</span></span> <span data-ttu-id="4efba-110">Im Bereich „Übersicht“ finden Sie zahlreiche Informationen zum virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="4efba-110">The overview panel has a lot of information about the VM.</span></span>

    - <span data-ttu-id="4efba-111">Sie können sehen, ob er ausgeführt wird</span><span class="sxs-lookup"><span data-stu-id="4efba-111">You can see whether the VM is running</span></span>
    - <span data-ttu-id="4efba-112">Sie können ihn beenden oder neu starten</span><span class="sxs-lookup"><span data-stu-id="4efba-112">Stop or restart it</span></span>
    - <span data-ttu-id="4efba-113">Sie können die öffentliche IP-Adresse abrufen, um eine Verbindung mit dem virtuellen Computer herzustellen</span><span class="sxs-lookup"><span data-stu-id="4efba-113">Get the public IP address to connect to the VM</span></span>
    - <span data-ttu-id="4efba-114">Sie können die Aktivität von CPU, Festplatte und Netzwerk anzeigen</span><span class="sxs-lookup"><span data-stu-id="4efba-114">See the activity of the CPU, disk, and network</span></span>

1. <span data-ttu-id="4efba-115">Klicken Sie oben im Bereich auf die Schaltfläche **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="4efba-115">Click the **Connect** button at the top of the pane.</span></span>

1. <span data-ttu-id="4efba-116">Notieren Sie sich die Einstellungen für die **IP-Adresse** und die **Portnummer** auf dem Blatt **Verbindung mit virtuellem Computer herstellen**.</span><span class="sxs-lookup"><span data-stu-id="4efba-116">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings.</span></span> <span data-ttu-id="4efba-117">Auf der Registerkarte **SSH** finden Sie auch den Befehl, den Sie lokal ausführen müssen, um eine Verbindung mit dem virtuellen Computer herzustellen.</span><span class="sxs-lookup"><span data-stu-id="4efba-117">On the **SSH** tab, you will also find the command you need to execute locally to connect to the VM.</span></span> <span data-ttu-id="4efba-118">Kopieren Sie diesen in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="4efba-118">Copy this to the clipboard.</span></span>

## <a name="connect-with-ssh"></a><span data-ttu-id="4efba-119">Verbinden mit SSH</span><span class="sxs-lookup"><span data-stu-id="4efba-119">Connect with SSH</span></span>

1. <span data-ttu-id="4efba-120">Fügen Sie die Befehlszeile, die Sie von der Registerkarte „SSH“ abgerufen haben, in Azure Cloud Shell ein.</span><span class="sxs-lookup"><span data-stu-id="4efba-120">Paste the command line you got from the SSH tab into Azure Cloud Shell.</span></span> <span data-ttu-id="4efba-121">Das Ergebnis sollte in etwa wie folgt aussehen. Es wird jedoch eine andere IP-Adresse verwendet (und möglicherweise ein anderer Benutzername, wenn Sie nicht **jim** angegeben haben)</span><span class="sxs-lookup"><span data-stu-id="4efba-121">It should look something like this; however, it will have a different IP address (and perhaps a different username if you didn't use **jim**!):</span></span>

    ```bash
    ssh jim@137.117.101.249
    ```

1. <span data-ttu-id="4efba-122">Mit diesem Befehl wird eine Secure Shell-Verbindung geöffnet, und es wird eine herkömmliche Shell-Eingabeaufforderung für Linux angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4efba-122">This command will open a Secure Shell connection and place you at a traditional shell command prompt for Linux.</span></span>

1. <span data-ttu-id="4efba-123">Führen Sie einige Linux-Befehle aus:</span><span class="sxs-lookup"><span data-stu-id="4efba-123">Try executing a few Linux commands</span></span>
    - <span data-ttu-id="4efba-124">`ls -la /`, um den Stamm des Datenträgers anzuzeigen</span><span class="sxs-lookup"><span data-stu-id="4efba-124">`ls -la /` to show the root of the disk</span></span>
    - <span data-ttu-id="4efba-125">`ps -l`, um alle ausgeführten Prozesse anzuzeigen</span><span class="sxs-lookup"><span data-stu-id="4efba-125">`ps -l` to show all the running processes</span></span>
    - <span data-ttu-id="4efba-126">`dmesg`, um alle Kernelnachrichten aufzulisten</span><span class="sxs-lookup"><span data-stu-id="4efba-126">`dmesg` to list all the kernel messages</span></span>
    - <span data-ttu-id="4efba-127">`lsblk`, um alle Blockgeräte aufzulisten. Hier werden Ihre Laufwerke angezeigt</span><span class="sxs-lookup"><span data-stu-id="4efba-127">`lsblk` to list all the block devices - here you will see your drives</span></span>

<span data-ttu-id="4efba-128">Interessanter ist das, was in der Liste der Laufwerke _fehlt_.</span><span class="sxs-lookup"><span data-stu-id="4efba-128">The more interesting thing to observe in the list of drives is what is _missing_.</span></span> <span data-ttu-id="4efba-129">Beachten Sie, dass unser **Daten**laufwerk (`sdc`) zwar vorhanden, nicht aber im Dateisystem bereitgestellt ist.</span><span class="sxs-lookup"><span data-stu-id="4efba-129">Notice that our **Data** drive (`sdc`) is present but not mounted into the file system.</span></span> <span data-ttu-id="4efba-130">Azure hat eine VHD hinzugefügt, aber nicht initialisiert.</span><span class="sxs-lookup"><span data-stu-id="4efba-130">Azure added a VHD but didn't initialize it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="4efba-131">Initialisieren von Laufwerken</span><span class="sxs-lookup"><span data-stu-id="4efba-131">Initialize data disks</span></span>

<span data-ttu-id="4efba-132">Alle zusätzlichen Laufwerke, die Sie neu erstellen, müssen initialisiert und formatiert werden.</span><span class="sxs-lookup"><span data-stu-id="4efba-132">Any additional drives you create from scratch will need to be initialized and formatted.</span></span> <span data-ttu-id="4efba-133">Der Prozess ist der gleiche wie bei einem physischen Datenträger:</span><span class="sxs-lookup"><span data-stu-id="4efba-133">The process for doing this is identical to a physical disk:</span></span>

1. <span data-ttu-id="4efba-134">Identifizieren Sie zuerst den Datenträger.</span><span class="sxs-lookup"><span data-stu-id="4efba-134">First, identify the disk.</span></span> <span data-ttu-id="4efba-135">Dies ist weiter oben erfolgt.</span><span class="sxs-lookup"><span data-stu-id="4efba-135">We did that above.</span></span> <span data-ttu-id="4efba-136">Sie können auch `dmesg | grep SCSI` verwenden, um alle Nachrichten aus dem Kernel für SCSI-Geräte aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="4efba-136">You could also use `dmesg | grep SCSI`, which will list all the messages from the kernel for SCSI devices.</span></span>

1. <span data-ttu-id="4efba-137">Sobald Sie das Laufwerk (`sdc`) kennen, das initialisiert werden muss, können Sie `fdisk` zu diesem Zweck verwenden.</span><span class="sxs-lookup"><span data-stu-id="4efba-137">Once you know the drive (`sdc`) you need to initialize, you can use `fdisk` to do that.</span></span> <span data-ttu-id="4efba-138">Sie müssen den Befehl mit `sudo` ausführen und den Datenträger angeben, der partitioniert werden soll.</span><span class="sxs-lookup"><span data-stu-id="4efba-138">You will need to run the command with `sudo` and supply the disk you want to partition.</span></span> <span data-ttu-id="4efba-139">Wir können den folgenden Befehl verwenden, um eine neue primäre Partition zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="4efba-139">We can use the following command to create a new primary partition:</span></span>

    ```bash
    (echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
    ```

1. <span data-ttu-id="4efba-140">Im nächsten Schritt schreiben Sie jetzt mit dem Befehl `mkfs` ein Dateisystem auf die Partition.</span><span class="sxs-lookup"><span data-stu-id="4efba-140">Next, we need to write a file system to the partition with the `mkfs` command.</span></span>

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```

1. <span data-ttu-id="4efba-141">Abschließend müssen wir das Laufwerk im Dateisystem bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="4efba-141">Finally, we need to mount the drive to the file system.</span></span> <span data-ttu-id="4efba-142">Angenommen, es ist ein Ordner `data` vorhanden.</span><span class="sxs-lookup"><span data-stu-id="4efba-142">Let's assume we will have a `data` folder.</span></span> <span data-ttu-id="4efba-143">Wir erstellen den Bereitstellungspunktordner und stellen das Laufwerk bereit.</span><span class="sxs-lookup"><span data-stu-id="4efba-143">Let's create the mount point folder and mount the drive.</span></span>

    ```bash
    sudo mkdir /data & sudo mount /dev/sdc1 /data
    ```

    > [!TIP]
    > <span data-ttu-id="4efba-144">Wir haben den Datenträger initialisiert und bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="4efba-144">We initialized the disk and mounted it.</span></span> <span data-ttu-id="4efba-145">Falls Sie an weiteren Informationen zu diesem Prozess interessiert sind, können Sie das Modul **Hinzufügen und Ändern der Größe von Datenträgern in Azure Virtual Machines** verwenden.</span><span class="sxs-lookup"><span data-stu-id="4efba-145">If you are interested in more details on this process go through the **Add and size disks in Azure virtual machines** module.</span></span> <span data-ttu-id="4efba-146">Darin wird diese Aufgabe ausführlicher behandelt.</span><span class="sxs-lookup"><span data-stu-id="4efba-146">This task is covered in more detail there.</span></span>

## <a name="install-software-onto-the-vm"></a><span data-ttu-id="4efba-147">Installieren von Software auf dem virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="4efba-147">Install software onto the VM</span></span>

<span data-ttu-id="4efba-148">Wie Sie sehen können, erlaubt SSH Ihnen die Arbeit mit dem virtuellen Linux-Computer wie mit einem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="4efba-148">As you can see, SSH allows you to work with the Linux VM just like a local computer.</span></span> <span data-ttu-id="4efba-149">Sie können diesen virtuellen Computer wie jeden anderen Linux-Computer verwalten: Software installieren, Rollen konfigurieren, Features anpassen und andere alltägliche Aufgaben durchführen.</span><span class="sxs-lookup"><span data-stu-id="4efba-149">You can administer this VM as you would any other Linux computer: installing software, configuring roles, adjusting features, and other everyday tasks.</span></span> <span data-ttu-id="4efba-150">Wir beschäftigen uns hier erst einmal mit dem Installieren der Software.</span><span class="sxs-lookup"><span data-stu-id="4efba-150">Let's focus on installing software for a moment.</span></span>

<span data-ttu-id="4efba-151">Es gibt mehrere Optionen zum Installieren von Software auf dem virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="4efba-151">You have several options to install software onto the VM.</span></span> <span data-ttu-id="4efba-152">Zunächst können Sie (wie bereits erwähnt) `scp` zum Kopieren lokaler Dateien von Ihrem Computer auf den virtuellen Computer verwenden.</span><span class="sxs-lookup"><span data-stu-id="4efba-152">First, as mentioned, you can use `scp` to copy local files from your machine to the VM.</span></span> <span data-ttu-id="4efba-153">Damit können Sie Daten oder benutzerdefinierte Anwendungen kopieren, die Sie ausführen möchten.</span><span class="sxs-lookup"><span data-stu-id="4efba-153">This lets you copy over data or custom applications you want to run.</span></span>

<span data-ttu-id="4efba-154">Sie können Software auch über Secure Shell installieren.</span><span class="sxs-lookup"><span data-stu-id="4efba-154">You can also install software through Secure Shell.</span></span> <span data-ttu-id="4efba-155">Azure-Computer sind standardmäßig mit dem Internet verbunden.</span><span class="sxs-lookup"><span data-stu-id="4efba-155">Azure machines are, by default, internet connected.</span></span> <span data-ttu-id="4efba-156">Sie können die Standardbefehle verwenden, um beliebte Softwarepakete direkt aus Standardrepositorys zu installieren.</span><span class="sxs-lookup"><span data-stu-id="4efba-156">You can use standard commands to install popular software packages directly from standard repositories.</span></span> <span data-ttu-id="4efba-157">Wir verwenden diesen Ansatz hier zum Installieren von Apache.</span><span class="sxs-lookup"><span data-stu-id="4efba-157">Let's use this approach to install Apache.</span></span>

### <a name="install-the-apache-web-server"></a><span data-ttu-id="4efba-158">Installieren des Apache-Webservers</span><span class="sxs-lookup"><span data-stu-id="4efba-158">Install the Apache web server</span></span>

<span data-ttu-id="4efba-159">Apache ist in den Standardsoftwarerepositorys von Ubuntu verfügbar. Daher erfolgt die Installation mit herkömmlichen Paketverwaltungstools:</span><span class="sxs-lookup"><span data-stu-id="4efba-159">Apache is available within Ubuntu's default software repositories, so we will install it using conventional package management tools:</span></span>

1. <span data-ttu-id="4efba-160">Starten Sie, indem Sie den lokalen Paketindex aktualisieren, um die neuesten Upstreamänderungen widerzuspiegeln:</span><span class="sxs-lookup"><span data-stu-id="4efba-160">Start by updating the local package index to reflect the latest upstream changes:</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="4efba-161">Installieren Sie im nächsten Schritt Apache:</span><span class="sxs-lookup"><span data-stu-id="4efba-161">Next, install Apache:</span></span>

    ```bash
    sudo apt-get install apache2 -y
    ```

1. <span data-ttu-id="4efba-162">Der Start sollte automatisch erfolgen. Sie können den Status mit `systemctl` überprüfen:</span><span class="sxs-lookup"><span data-stu-id="4efba-162">It should start automatically - we can check the status using `systemctl`:</span></span>

    ```bash
    sudo systemctl status apache2 --no-pager
    ```

    <span data-ttu-id="4efba-163">Die Rückgabe sollte dem folgenden Beispiel ähneln:</span><span class="sxs-lookup"><span data-stu-id="4efba-163">This should return something like:</span></span>

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
    > [!NOTE]
    > <span data-ttu-id="4efba-164">Die Ausführung dieser Art von Befehlen ist einfach, aber es handelt sich um einen manuellen Prozess. Wenn Sie häufig Software installieren müssen, sollten Sie die Automatisierung des Prozesses mithilfe von Skripts in Betracht ziehen.</span><span class="sxs-lookup"><span data-stu-id="4efba-164">It's trivial to execute commands like this, however it's a manual process - if we always need to install some software, you might consider automating the process using scripting.</span></span>

1. <span data-ttu-id="4efba-165">Abschließend können wir versuchen, die Standardseite über die öffentliche IP-Adresse abzurufen.</span><span class="sxs-lookup"><span data-stu-id="4efba-165">Finally, we can try retrieving the default page through the public IP address.</span></span> <span data-ttu-id="4efba-166">Aber obwohl der Webserver auf der VM ausgeführt wird, erhalten Sie keine gültige Verbindung oder Antwort.</span><span class="sxs-lookup"><span data-stu-id="4efba-166">However, even though the web server is running on the VM, you won't get a valid connection or response.</span></span> <span data-ttu-id="4efba-167">Kennen Sie den Grund?</span><span class="sxs-lookup"><span data-stu-id="4efba-167">Do you know why?</span></span>

<span data-ttu-id="4efba-168">Wir müssen einen weiteren Schritt ausführen, um mit dem Webserver interagieren zu können.</span><span class="sxs-lookup"><span data-stu-id="4efba-168">We need to perform one more step to be able to interact with the web server.</span></span> <span data-ttu-id="4efba-169">Unser virtuelles Netzwerk blockiert die eingehende Anforderung. Dies ist das Standardverhalten.</span><span class="sxs-lookup"><span data-stu-id="4efba-169">Our virtual network is blocking the inbound request - this is the default behavior.</span></span> <span data-ttu-id="4efba-170">Wir können dies über die Konfiguration ändern.</span><span class="sxs-lookup"><span data-stu-id="4efba-170">We can change that through configuration.</span></span> <span data-ttu-id="4efba-171">Dies sehen wir uns als Nächstes an.</span><span class="sxs-lookup"><span data-stu-id="4efba-171">Let's look at that next.</span></span>