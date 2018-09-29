<span data-ttu-id="6b7b9-101">Bevor einige der grundlegenden Methoden zum Ausführen, Auflisten und Löschen von Containern erläutert werden, sehen Sie sich eine einfache nginx-Konfiguration an, die auf einem Docker-Container ausgeführt wird, der auf einem virtuellen Ubuntu-Computer (VM) gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-101">Before we cover some of the common ways to run, list, and delete containers, let's see a basic Nginx configuration running on a Docker container that's hosted on an Ubuntu virtual machine (VM).</span></span>

<span data-ttu-id="6b7b9-102">In dieser Einheit lernen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="6b7b9-102">In this part, you'll learn how to:</span></span>

1. <span data-ttu-id="6b7b9-103">Erstellen einer Linux-VM, die zum Installieren von Docker beim ersten Start der VM konfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-103">Create a Linux VM that's configured to install Docker when the VM first boots.</span></span>
1. <span data-ttu-id="6b7b9-104">Herstellen einer Verbindung zur VM und Starten eines Docker-Containers, auf dem nginx ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-104">Connect to your VM and start a Docker container running Nginx.</span></span>
1. <span data-ttu-id="6b7b9-105">Verwenden der Portbindung, um den Webserver außerhalb der VM zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-105">Use port binding to make your web server accessible from outside the VM.</span></span>

## <a name="what-are-containers"></a><span data-ttu-id="6b7b9-106">Was sind Container?</span><span class="sxs-lookup"><span data-stu-id="6b7b9-106">What are containers?</span></span>

<span data-ttu-id="6b7b9-107">Ein Container ist eine Virtualisierungsumgebung, die im Gegensatz zu einer VM nicht immer ein vollständiges Betriebssystem enthält.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-107">A container is a virtualization environment but, unlike a virtual machine, it does not always include a full operating system.</span></span> <span data-ttu-id="6b7b9-108">Stattdessen verweist sie auf das Betriebssystem der Hostumgebung, die den Container ausführt.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-108">Instead, it references the operating system of the host environment that runs that container.</span></span> <span data-ttu-id="6b7b9-109">Wenn Sie beispielsweise fünf Container auf einem Server mit einem spezifischen Linux-Kernel ausführen, werden alle fünf Container auf demselben Kernel ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-109">For example, if you run five containers on a server with a specific Linux kernel, all five containers are running on that same kernel.</span></span>

<span data-ttu-id="6b7b9-110">Mit Containern können Sie Ihre Anwendung und alle zur Ausführung erforderlichen Elemente in ein sogenanntes _Containerimage_ packen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-110">Containers enable you to package your application and everything that it needs to run into what's known as a _container image_.</span></span> <span data-ttu-id="6b7b9-111">Container sind isoliert, d.h., sie beeinflussen keine anderen Container auf dem gleichen System.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-111">Containers are isolated, which means they don't interfere with any other container running on the same system.</span></span> <span data-ttu-id="6b7b9-112">Containerimages sind außerdem portierbar.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-112">Container images are also portable.</span></span> <span data-ttu-id="6b7b9-113">Sie können Ihre Images in eine Containerregistrierung hochladen, z.B. Docker Hub oder Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-113">You can upload your images to a container registry, such as Docker Hub or Azure Container Registry.</span></span> <span data-ttu-id="6b7b9-114">Anschließend können Sie Ihre Container in der Cloud ausführen und davon ausgehen, dass sie sich auf die gleiche Weise wie in Ihrer Entwicklungsumgebung verhalten.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-114">You can then run your containers in the cloud and expect them to behave the exact same way as they do in your development environment.</span></span>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yMhY]

<span data-ttu-id="6b7b9-115">Container ermöglichen schnelle Iterationen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-115">Containers enable rapid iteration.</span></span> <span data-ttu-id="6b7b9-116">Da Container kein Betriebssystem enthalten müssen, sind sie in der Regel deutlich kleiner als vollständige VMs.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-116">Because containers don't need to include an operating system, they're typically much smaller than full VMs.</span></span> <span data-ttu-id="6b7b9-117">Dadurch können Sie Container schnell starten und beenden, oft innerhalb von Sekunden.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-117">This enables you to start and stop containers quickly, often in seconds.</span></span>

## <a name="understand-the-setup"></a><span data-ttu-id="6b7b9-118">Grundlegende Informationen zum Aufbau</span><span class="sxs-lookup"><span data-stu-id="6b7b9-118">Understand the setup</span></span>

<span data-ttu-id="6b7b9-119">Ihnen wird eine Sandboxumgebung zu Lernzwecken bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-119">For learning purposes, we provide a sandbox environment for you to work in.</span></span> <span data-ttu-id="6b7b9-120">Diese Umgebung enthält Azure Cloud Shell, ein browserbasierter Dienst zum Verwalten und Entwickeln von Azure-Ressourcen über die Befehlszeile.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-120">This environment includes Azure Cloud Shell, a browser-based command-line experience for managing and developing Azure resources.</span></span>

<span data-ttu-id="6b7b9-121">Über Cloud Shell erstellen Sie eine Linux-VM, die Docker enthält.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-121">From Cloud Shell, you'll create a Linux VM that includes Docker.</span></span> <span data-ttu-id="6b7b9-122">Sie verbinden Ihre Linux-VM per SSH, sodass Sie Docker-Container interaktiv erstellen und verwenden können.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-122">You'll connect to your Linux VM over SSH so that you can interactively create and use Docker containers.</span></span>

<span data-ttu-id="6b7b9-123">Stellen Sie sich diese Linux-VM als Ihre Entwicklungsumgebung zum Kennenlernen von Containern vor.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-123">Think of this Linux VM as your development environment and a space to learn about containers.</span></span> <span data-ttu-id="6b7b9-124">In der Praxis würden Sie Docker auf dem Computer installieren, den Sie zum Entwickeln Ihrer Apps verwenden.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-124">In practice, you would install Docker on the computer you use to develop your apps.</span></span> <span data-ttu-id="6b7b9-125">Docker kann unter Windows, macOS und Linux ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-125">Docker runs on Windows, macOS, and Linux.</span></span>

<span data-ttu-id="6b7b9-126">Am Ende dieses Moduls werden Ihnen Ressourcen bereitgestellt, mit denen Sie mehr über das Ausführen von Docker in Ihrer lokalen Entwicklungsumgebung erfahren können.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-126">We'll provide resources where you can learn more about running Docker in your local development environment at the end of this module.</span></span>

## <a name="what-is-nginx"></a><span data-ttu-id="6b7b9-127">Was ist nginx?</span><span class="sxs-lookup"><span data-stu-id="6b7b9-127">What is Nginx?</span></span>

<span data-ttu-id="6b7b9-128">nginx (ausgesprochen „Engine-x“) ist ein beliebter, kostenloser Open-Source-Webserver, der unter Unix, Linux, macOS und Windows ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-128">Nginx (pronounced "engine-x") is a popular, free, open-source web server that runs on Unix, Linux, macOS, and Windows.</span></span> <span data-ttu-id="6b7b9-129">Das Konfigurieren eines Webservers stellt eine gute Möglichkeit dar, Container in Aktion zu sehen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-129">Configuring a web server is a good way to see containers in action.</span></span> <span data-ttu-id="6b7b9-130">Hier verwenden Sie nginx, um eine einfache Webseite bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-130">Here you'll use Nginx to serve a basic web page.</span></span>

## <a name="what-is-cloud-init"></a><span data-ttu-id="6b7b9-131">Was ist cloud-init?</span><span class="sxs-lookup"><span data-stu-id="6b7b9-131">What is cloud-init?</span></span>

<span data-ttu-id="6b7b9-132">Mit cloud-init können Sie eine Linux-VM während des ersten Starts anpassen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-132">Cloud-init enables you to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="6b7b9-133">Sie können mit cloud-init Pakete installieren und Dateien schreiben oder Benutzer und Sicherheit konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-133">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="6b7b9-134">Hier verwenden Sie ein cloud-init-Skript, um Docker auf Ihrer VM zu installieren.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-134">Here you'll use a cloud-init script to install Docker on your VM.</span></span>

## <a name="what-is-port-binding"></a><span data-ttu-id="6b7b9-135">Was ist Portbindung?</span><span class="sxs-lookup"><span data-stu-id="6b7b9-135">What is port binding?</span></span>

<span data-ttu-id="6b7b9-136">Mit Portbindung können Sie Netzwerkdatenverkehr vom Host an einen Container weiterleiten.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-136">Port binding enables you to forward network traffic to a container from its host.</span></span>

<span data-ttu-id="6b7b9-137">Ein Docker-Container wird auf einem lokalen Netzwerk des Hostsystems des Containers ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-137">A Docker container runs on a local network on the container's host system.</span></span> <span data-ttu-id="6b7b9-138">In diesem Fall befindet sich das Netzwerk des Containers auf Ihrer Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-138">In this case, the container's network will be on your Linux VM.</span></span>

<span data-ttu-id="6b7b9-139">Wie Sie bereits wissen, werden Webanforderungen in der Regel über Port 80 (HTTP) ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-139">You know that web requests typically run over port 80 (HTTP).</span></span> <span data-ttu-id="6b7b9-140">Da der Container auf einem lokalen Netzwerk in der VM ausgeführt wird, ist der Container für die Außenwelt nicht zugänglich.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-140">Because the container is running on a local network inside your VM, the container is not accessible to the outside world.</span></span>

<span data-ttu-id="6b7b9-141">Mit Docker können Sie einen Port außerhalb der VM veröffentlichen oder zur Verfügung stellen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-141">Docker enables you to publish, or expose, a port to make it accessible from outside the VM.</span></span> <span data-ttu-id="6b7b9-142">Hier konfigurieren Sie Ihren Container so, dass der Netzwerkdatenverkehr an Port 8080 Ihrer VM an Port 80 Ihres Containers weitergeleitet wird.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-142">Here, you'll configure your container so that network traffic to port 8080 on your VM will be forwarded to port 80 on your container.</span></span>

## <a name="create-a-virtual-machine-to-host-docker"></a><span data-ttu-id="6b7b9-143">Erstellen eines virtuellen Computers zum Hosten von Docker</span><span class="sxs-lookup"><span data-stu-id="6b7b9-143">Create a virtual machine to host Docker</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="create-the-cloud-init-script"></a><span data-ttu-id="6b7b9-144">Erstellen des cloud-init-Skripts</span><span class="sxs-lookup"><span data-stu-id="6b7b9-144">Create the cloud-init script</span></span>

1. <span data-ttu-id="6b7b9-145">Navigieren Sie zum Ordner **clouddrive**.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-145">Navigate to the **clouddrive** folder.</span></span>

    ```azurecli
    cd clouddrive
    ```

1. <span data-ttu-id="6b7b9-146">Erstellen Sie einen neuen Ordner mit dem Namen **vm-config**.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-146">Create a new folder named **vm-config**.</span></span>

    ```azurecli
    mkdir vm-config
    ```

1. <span data-ttu-id="6b7b9-147">Navigieren Sie zum neuen Ordner.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-147">Navigate to the new folder.</span></span>

    ```azurecli
    cd vm-config
    ```

1. <span data-ttu-id="6b7b9-148">Erstellen Sie eine neue Datei mit dem in Cloud Shell integrierten Editor.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-148">Create a new file using Cloud Shell's integrated editor.</span></span>

    ```azurecli
    code .
    ```

1. <span data-ttu-id="6b7b9-149">Fügen Sie das cloud-init-Skript in den Editor ein.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-149">Paste this cloud-init script into the editor.</span></span>

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```yaml
    #cloud-config
    package_upgrade: true
    write_files:
      - path: /etc/systemd/system/docker.service.d/docker.conf
        content: |
          [Service]
          ExecStart=
          ExecStart=/usr/bin/dockerd
      - path: /etc/docker/daemon.json
        content: |
          {
            "hosts": ["fd://","tcp://127.0.0.1:2375"]
          }
    runcmd:
      - curl -sSL https://get.docker.com/ | sh
      - usermod -aG docker azureuser
    ```

1. <span data-ttu-id="6b7b9-150">Speichern Sie die Datei als **docker-vm-config.txt** (drücken Sie hierzu <kbd>STRG+S</kbd>, oder klicken Sie mit der rechten Maustaste, und wählen Sie dann **Speichern** aus).</span><span class="sxs-lookup"><span data-stu-id="6b7b9-150">Save the file as **docker-vm-config.txt** (<kbd>Ctrl+S</kbd> or right click and select **Save**).</span></span>

1. <span data-ttu-id="6b7b9-151">Schließen Sie den Editor (drücken Sie hierzu <kbd>STRG+Q</kbd>, oder klicken Sie mit der rechten Maustaste, und wählen Sie **Beenden** aus).</span><span class="sxs-lookup"><span data-stu-id="6b7b9-151">Close the editor (<kbd>Ctrl+Q</kbd> or right click and select **Quit**).</span></span>

### <a name="create-the-vm"></a><span data-ttu-id="6b7b9-152">Erstellen des virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="6b7b9-152">Create the VM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b7b9-153">Normalerweise würden Sie mit dem Befehl `az group create` eine Ressourcengruppe für alle Ihre verwandten Azure-Ressourcen erstellen. Für diese Übungen wurde aber bereits eine Ressourcengruppe für Sie erstellt.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-153">Normally, you would create a resource group for all your related Azure resources with the `az group create` command, but for these exercises one has been created for you.</span></span> <span data-ttu-id="6b7b9-154">Verwenden Sie in allen Schritten die Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-154">Use "**<rgn>[sandbox resource group name]</rgn>**" as your resource group in all the steps.</span></span>

1. <span data-ttu-id="6b7b9-155">Führen Sie den folgenden `az vm create`-Befehl aus, um die Linux-VM zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-155">Run this `az vm create` command to create your Linux VM.</span></span>

    ```azurecli
    az vm create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --image UbuntuLTS \
      --admin-username azureuser \
      --generate-ssh-keys \
      --custom-data docker-vm-config.txt
    ```

<span data-ttu-id="6b7b9-156">Das Argument `--custom-data` gibt das cloud-init-Skript an, das Docker beim ersten Start der VM installiert.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-156">The `--custom-data` argument specifies the cloud-init script that installs Docker when the VM first boots.</span></span> <span data-ttu-id="6b7b9-157">Dieser Prozess dauert ein paar Minuten.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-157">The process will take a few minutes to complete.</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="6b7b9-158">Herstellen der Verbindung mit der VM</span><span class="sxs-lookup"><span data-stu-id="6b7b9-158">Connect to the VM</span></span>

<span data-ttu-id="6b7b9-159">Hier erstellen Sie eine SSH-Verbindung mit der VM, damit Sie sie konfigurieren können.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-159">Here you'll create an SSH connection to your VM so that you can configure it.</span></span>

1. <span data-ttu-id="6b7b9-160">Führen Sie den folgenden `az vm show`-Befehl aus, um die IP-Adresse Ihrer VM abzurufen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-160">Run this `az vm show` command to get your VM's IP address.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

1. <span data-ttu-id="6b7b9-161">Stellen Sie eine SSH-Verbindung zur VM her.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-161">SSH into the VM.</span></span> <span data-ttu-id="6b7b9-162">Ersetzen Sie **ip-adress** durch Ihre IP-Adresse.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-162">Replace **ip-address** with yours.</span></span>

    ```bash
    ssh azureuser@ip-address
    ```

1. <span data-ttu-id="6b7b9-163">Überprüfen Sie die Version von Docker.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-163">Verify the Docker version.</span></span>

    ```bash
    docker version
    ```

    > [!NOTE]
    > <span data-ttu-id="6b7b9-164">Wenn der Befehl fehlschlägt, oder eine Fehlermeldung zum Herstellen einer Verbindung mit dem Docker-Daemonsocket angezeigt wird, bedeutet das, dass das cloud-init-Skript noch nicht abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-164">If the command fails, or you see an error message about connecting to the Docker daemon socket, that means that the cloud-init script hasn't yet completed.</span></span> <span data-ttu-id="6b7b9-165">Obwohl es Möglichkeiten gibt, auf den Abschluss des Skripts zu warten, führen Sie fürs Erste `exit` aus, um Ihre SSH-Sitzung zu verlassen und die Verbindung in ein paar Minuten wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-165">Although there are ways to wait for the script to complete, for now run `exit` to leave your SSH session and try reconnecting in a minute or two.</span></span>

## <a name="start-nginx"></a><span data-ttu-id="6b7b9-166">Starten von nginx</span><span class="sxs-lookup"><span data-stu-id="6b7b9-166">Start Nginx</span></span>

<span data-ttu-id="6b7b9-167">Hier starten Sie einen Docker-Container, auf dem nginx ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-167">Here you'll start a Docker container that's running Nginx.</span></span>

1. <span data-ttu-id="6b7b9-168">Führen Sie den folgenden `docker run`-Befehl aus, um einen Docker-Container zu starten, auf dem nginx ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-168">Run this `docker run` command to start a Docker container running Nginx.</span></span>

    ```bash
    docker run -d -p 8080:80 --name nginx nginx
    ```

    <span data-ttu-id="6b7b9-169">Durch diesen Befehl wird ein Docker-Image heruntergeladen, das vom [Docker Hub](https://hub.docker.com/_/nginx?azure-portal=true) mit nginx vorkonfiguriert ist.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-169">The command downloads a Docker image that's preconfigured with Nginx from [Docker Hub](https://hub.docker.com/_/nginx?azure-portal=true).</span></span>

    <span data-ttu-id="6b7b9-170">Das Argument `--name` weist dem Docker-Container den Namen „nginx“ zu, damit Sie ihn später verwenden können.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-170">The `--name` argument assigns the name "nginx" to your Docker container so you can work with it later.</span></span>

    <span data-ttu-id="6b7b9-171">Das Argument `-p` leitet Netzwerkdatenverkehr an Port 8080 Ihrer VM an Port 80 Ihres Containers weiter.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-171">The `-p` argument forwards network traffic to port 8080 on your VM to port 80 on your container.</span></span>

1. <span data-ttu-id="6b7b9-172">Führen Sie den Befehl `curl` aus, um zu überprüfen, ob nginx ausgeführt wird und zugänglich ist.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-172">Run `curl` to verify that Nginx is running and accessible.</span></span>

    ```bash
    curl http://localhost:8080
    ```

1. <span data-ttu-id="6b7b9-173">Beenden Sie Ihre SSH-Sitzung.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-173">Exit your SSH session.</span></span>

    ```bash
    exit
    ```

## <a name="access-your-web-server-from-a-web-browser"></a><span data-ttu-id="6b7b9-174">Zugriff auf Ihren Webserver über einen Webbrowser</span><span class="sxs-lookup"><span data-stu-id="6b7b9-174">Access your web server from a web browser</span></span>

<span data-ttu-id="6b7b9-175">Denken Sie daran, dass Sie Ihren Container so konfiguriert haben, dass der Netzwerkdatenverkehr an Port 8080 an Port 80 Ihres Containers weitergeleitet wird.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-175">Recall that you configured your container so that network traffic on port 8080 is forwarded to port 80 on your container.</span></span>

<span data-ttu-id="6b7b9-176">Im Folgenden öffnen Sie Port 8080 Ihrer VM über Azure Firewall, um die Portzuordnung in Aktion zu sehen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-176">To see port mapping in action, here you'll open port 8080 to your VM through the Azure firewall.</span></span> <span data-ttu-id="6b7b9-177">Anschließend greifen Sie über einen Browser auf Ihren Webserver zu.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-177">Then you'll access your web server from a browser.</span></span>

1. <span data-ttu-id="6b7b9-178">Führen Sie den folgenden `az vm open-port`-Befehl aus, um Port 8080 durch die Firewall Ihrer VM zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-178">Run this `az vm open-port` command to open port 8080 on your VM through the firewall.</span></span>

    ```azurecli
    az vm open-port \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --port 8080 \
      --priority 1001
    ```

1. <span data-ttu-id="6b7b9-179">Navigieren Sie in einem Webbrowser zur IP-Adresse der VM.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-179">From a web browser, navigate to your VM's IP address.</span></span> <span data-ttu-id="6b7b9-180">Stellen Sie sicher, dass Sie Port 8080 in die Adresse einfügen, z.B. **http://40.121.106.164:8080**.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-180">Be sure to include port 8080, for example,  **http://40.121.106.164:8080**.</span></span>

    <span data-ttu-id="6b7b9-181">Die Standardstartseite wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-181">You see the default home page.</span></span>

    ![Die Website im Browser](../media/2-nginx-browser.png)

## <a name="stop-the-container"></a><span data-ttu-id="6b7b9-183">Beenden des Containers</span><span class="sxs-lookup"><span data-stu-id="6b7b9-183">Stop the container</span></span>

<span data-ttu-id="6b7b9-184">Nun beenden Sie den Container.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-184">Now let's stop the container.</span></span>

1. <span data-ttu-id="6b7b9-185">Melden Sie sich zunächst wieder bei Ihrer VM an.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-185">First, log back in to your VM.</span></span> <span data-ttu-id="6b7b9-186">Hier ist eine kleine Erinnerung.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-186">Here's a refresher.</span></span>

    <span data-ttu-id="6b7b9-187">Rufen Sie die IP-Adresse ab.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-187">Get the IP address.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

    <span data-ttu-id="6b7b9-188">Stellen Sie eine SSH-Verbindung zur VM her.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-188">SSH into the VM.</span></span> <span data-ttu-id="6b7b9-189">Ersetzen Sie **ip-adress** durch Ihre IP-Adresse.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-189">Replace **ip-address** with yours.</span></span>

    ```bash
    ssh azureuser@ip-address
    ```

1. <span data-ttu-id="6b7b9-190">Führen Sie den Befehl `docker stop nginx` aus, um den Container namens „nginx“ zu beenden.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-190">Run `docker stop nginx` to stop the container named "nginx".</span></span>

    ```bash
    docker stop nginx
    ```

<span data-ttu-id="6b7b9-191">Lassen Sie die SSH-Verbindung für die nächste Einheit geöffnet.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-191">Keep your SSH connection open for the next part.</span></span>

<span data-ttu-id="6b7b9-192">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="6b7b9-192">Congratulations!</span></span> <span data-ttu-id="6b7b9-193">Sie haben erfolgreich einen virtuellen Computer erstellt und diesen zum Hosten eines nginx-Webservers in einem Container verwendet.</span><span class="sxs-lookup"><span data-stu-id="6b7b9-193">You've successfully created a virtual machine and used it to host an Nginx containerized web server.</span></span>
