<span data-ttu-id="1d593-101">Da Sie jetzt über eine funktionierende Umgebung für die Containerentwicklung verfügen, können wir uns einige häufig verwendete Möglichkeiten zum Ausführen, Auflisten und Löschen von Containern ansehen.</span><span class="sxs-lookup"><span data-stu-id="1d593-101">Now that you have a functioning container development environment, let's look at some common ways to run, list, and delete containers.</span></span>

<span data-ttu-id="1d593-102">In dieser Einheit lernen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="1d593-102">Here, you'll learn how to:</span></span>

* <span data-ttu-id="1d593-103">Ausführen von Standardcontainern</span><span class="sxs-lookup"><span data-stu-id="1d593-103">Run basic containers.</span></span>
* <span data-ttu-id="1d593-104">Herunterladen von Containerimages</span><span class="sxs-lookup"><span data-stu-id="1d593-104">Download container images.</span></span>
* <span data-ttu-id="1d593-105">Löschen von Containern und den zugehörigen Images</span><span class="sxs-lookup"><span data-stu-id="1d593-105">Delete containers and their associated images.</span></span>

## <a name="whats-a-container-image"></a><span data-ttu-id="1d593-106">Was ist ein Containerimage?</span><span class="sxs-lookup"><span data-stu-id="1d593-106">What's a container image?</span></span>

<span data-ttu-id="1d593-107">Ein _Containerimage_ umfasst das Basisbetriebssystem und alle zusätzlichen Prozesse, Anwendungen und Konfigurationen.</span><span class="sxs-lookup"><span data-stu-id="1d593-107">A container _image_ includes the base operating system and any additional processes, applications, and configurations.</span></span> <span data-ttu-id="1d593-108">Ein _Container_ führt ähnlich wie ein virtueller Computer (VM) eine Instanz eines Images aus.</span><span class="sxs-lookup"><span data-stu-id="1d593-108">Much like a virtual machine, a _container_ is a running instance of an image.</span></span>

## <a name="connect-to-your-linux-vm"></a><span data-ttu-id="1d593-109">Herstellen einer Verbindung mit der Linux-VM</span><span class="sxs-lookup"><span data-stu-id="1d593-109">Connect to your Linux VM</span></span>

<span data-ttu-id="1d593-110">Wenn Sie die Verbindung zur SSH-Sitzung, die Sie im vorherigen Teil erstellt haben, getrennt haben, müssen Sie sich anmelden.</span><span class="sxs-lookup"><span data-stu-id="1d593-110">If you disconnected from the SSH session you created in the last part, you will need to log in.</span></span> <span data-ttu-id="1d593-111">Hier ist eine kleine Erinnerung.</span><span class="sxs-lookup"><span data-stu-id="1d593-111">Here's a refresher.</span></span>

1. <span data-ttu-id="1d593-112">Rufen Sie die IP-Adresse ab.</span><span class="sxs-lookup"><span data-stu-id="1d593-112">Get the IP address.</span></span>

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

1. <span data-ttu-id="1d593-113">Stellen Sie eine SSH-Verbindung zur VM her.</span><span class="sxs-lookup"><span data-stu-id="1d593-113">SSH into the VM.</span></span> <span data-ttu-id="1d593-114">Ersetzen Sie **ip-adress** durch Ihre IP-Adresse.</span><span class="sxs-lookup"><span data-stu-id="1d593-114">Replace **ip-address** with yours.</span></span>

    ```bash
    ssh azureuser@ip-address
    ```

## <a name="create-and-run-a-basic-container"></a><span data-ttu-id="1d593-115">Erstellen und Ausführen eines einfachen Containers</span><span class="sxs-lookup"><span data-stu-id="1d593-115">Create and run a basic container</span></span>

<span data-ttu-id="1d593-116">Im Folgenden führen Sie einen Container aus, der auf Alpine Linux basiert.</span><span class="sxs-lookup"><span data-stu-id="1d593-116">Here you'll run a container that's based on Alpine Linux.</span></span> <span data-ttu-id="1d593-117">Alpine Linux ist aufgrund der Größe beliebt. Containerimages können bis zu 5 MB klein sein.</span><span class="sxs-lookup"><span data-stu-id="1d593-117">Alpine Linux is popular because of its size &mdash; container images can be as small as 5 MB.</span></span>

<span data-ttu-id="1d593-118">Führen Sie diesen `docker run`-Befehl aus, um einen Container zu erstellen, der auf Alpine Linux basiert.</span><span class="sxs-lookup"><span data-stu-id="1d593-118">Run this `docker run` command to create a container based on Alpine Linux.</span></span>

```bash
docker run alpine echo "Hello World"
```

<span data-ttu-id="1d593-119">Ihnen sollte eine Ausgabe angezeigt werden, die wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="1d593-119">You see output similar to this:</span></span>

```output
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
8e3ba11ec2a2: Pull complete
Digest: sha256:7043076348bf5040220df6ad703798fd8593a0918d06d3ce30c6c93be117e430
Status: Downloaded newer image for alpine:latest
Hello World
```

<span data-ttu-id="1d593-120">Mit dem `docker run`-Befehl wird ein Container erstellt, der angegebene Befehl ausgeführt und der Container anschließend gelöscht.</span><span class="sxs-lookup"><span data-stu-id="1d593-120">The `docker run` command creates a container, runs the provided command, and then destroys the container.</span></span>

<span data-ttu-id="1d593-121">Hier lädt Docker das [alpine](https://hub.docker.com/_/alpine?azure-portal=true)-Image vom Docker Hub herunter, startet den Container und gibt dann „Hello World“ über die Konsole aus.</span><span class="sxs-lookup"><span data-stu-id="1d593-121">Here, Docker downloads the [alpine](https://hub.docker.com/_/alpine?azure-portal=true) image from Docker Hub, starts the container, and then prints "Hello World" to the console.</span></span>

<span data-ttu-id="1d593-122">In diesem Fall wird der Befehl `echo` vorübergehend ausgeführt und dann beendet.</span><span class="sxs-lookup"><span data-stu-id="1d593-122">In this case, the `echo` command runs briefly and then exits.</span></span> <span data-ttu-id="1d593-123">Im vorherigen Teil wurde nginx im Vordergrund ausgeführt, wodurch Ihre Container aktiv blieben, bis Sie den Container oder den nginx-Dienst beendet haben.</span><span class="sxs-lookup"><span data-stu-id="1d593-123">In the previous part, Nginx runs in the foreground and therefore keeps your container alive until you stop the container or stop the Nginx service.</span></span>

## <a name="get-container-images"></a><span data-ttu-id="1d593-124">Abrufen von Containerimages</span><span class="sxs-lookup"><span data-stu-id="1d593-124">Get container images</span></span>

<span data-ttu-id="1d593-125">Containerimages werden in einer Containerimageregistrierung gespeichert.</span><span class="sxs-lookup"><span data-stu-id="1d593-125">Container images are stored in a container image registry.</span></span> <span data-ttu-id="1d593-126">Im vorherigen Beispiel hat Docker das **alpine**-Image vom Docker Hub per Pull abgerufen. Docker Hub ist die öffentliche Containerregistrierung von Docker.</span><span class="sxs-lookup"><span data-stu-id="1d593-126">In the previous example, Docker pulls the **alpine** image from Docker Hub, Docker's public container registry.</span></span>

<span data-ttu-id="1d593-127">Führen Sie den Befehl `docker images` aus, um eine Liste von Images anzuzeigen, die heruntergeladen und auf Ihrem System gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="1d593-127">Run `docker images` to see a list of images that have been downloaded to your system.</span></span>

```bash
docker images
```

<span data-ttu-id="1d593-128">Ihnen werden zwei Images angezeigt: **alpine** und **nginx**.</span><span class="sxs-lookup"><span data-stu-id="1d593-128">You see two images &mdash; **alpine** and **nginx**.</span></span>

```output
REPOSITORY          TAG                 IMAGE ID            CREATEDSIZE
alpine              latest              196d12cf6ab1        8 days ago4.41MB
nginx               latest              06144b287844        2 weeks ago109MB
```

<span data-ttu-id="1d593-129">Verwenden Sie den Befehl `docker search`, um nach einem Containerimage zu suchen.</span><span class="sxs-lookup"><span data-stu-id="1d593-129">To search for a container image, use the `docker search` command.</span></span> <span data-ttu-id="1d593-130">Beispielsweise können Sie den folgenden Befehl ausführen, um alle Containerimages aufzulisten, die `nginx` im Namen enthalten.</span><span class="sxs-lookup"><span data-stu-id="1d593-130">For example, run the following to list all container images that include `nginx` in their names.</span></span>

```bash
docker search nginx --limit 5
```

<span data-ttu-id="1d593-131">In diesem Beispiel schränkt das Argument `--limit` den Suchvorgang auf die ersten fünf Ergebnisse ein.</span><span class="sxs-lookup"><span data-stu-id="1d593-131">The `--limit` argument in this example restricts the search operation to the first five results.</span></span>

<span data-ttu-id="1d593-132">Die Ausgabe sollte wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="1d593-132">You see something similar to this.</span></span>

```output
NAME                                     DESCRIPTION         STARS               OFFICIAL            AUTOMATED
nginx                                    Official build of Nginx.         9672                [OK]
jwilder/nginx-proxy                      Automated Nginx reverse proxy for docker con…   1415                                    [OK]
richarvey/nginx-php-fpm                  Container running Nginx + PHP-FPM capable of…   615                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion   LetsEncrypt container to use with nginx as p…   411                                     [OK]
bitnami/nginx                            Bitnami nginx Docker Image         58                                      [OK]
```

<span data-ttu-id="1d593-133">Befehle wie `docker run` rufen das Image für Sie ab, wenn es nicht lokal vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="1d593-133">Commands like `docker run` pull down the image for you if you don't have it locally.</span></span> <span data-ttu-id="1d593-134">Es ist jedoch üblich, ein Image herunterzuladen, bevor Sie es verwenden.</span><span class="sxs-lookup"><span data-stu-id="1d593-134">But it's common to download an image before you use it.</span></span> <span data-ttu-id="1d593-135">Damit wird sichergestellt, dass Sie über die neueste Version verfügen.</span><span class="sxs-lookup"><span data-stu-id="1d593-135">This ensures you have the latest version.</span></span>

<span data-ttu-id="1d593-136">Verwenden Sie hierzu den `docker pull`-Befehl.</span><span class="sxs-lookup"><span data-stu-id="1d593-136">To do so, you use the `docker pull` command.</span></span> <span data-ttu-id="1d593-137">Führen Sie Folgendes aus, um das neueste **nginx**-Image vom Docker Hub zu abzurufen.</span><span class="sxs-lookup"><span data-stu-id="1d593-137">Run the following to pull the latest **nginx** image from Docker Hub.</span></span>

```bash
docker pull nginx
```

<span data-ttu-id="1d593-138">In diesem Beispiel wird gezeigt, dass Sie über die neuste Version des **nginx**-Images verfügen.</span><span class="sxs-lookup"><span data-stu-id="1d593-138">This example shows that you have the latest version of the **nginx** image.</span></span>

```output
Using default tag: latest
latest: Pulling from library/nginx
Digest: sha256:24a0c4b4a4c0eb97a1aabb8e29f18e917d05abfe1b7a7c07857230879ce7d3d3
Status: Image is up to date for nginx:latest
```

## <a name="run-and-list-a-container"></a><span data-ttu-id="1d593-139">Ausführen und Auflisten eines Containers</span><span class="sxs-lookup"><span data-stu-id="1d593-139">Run and list a container</span></span>

<span data-ttu-id="1d593-140">Im vorherigen Teil haben Sie den `docker run`-Befehl verwendet, um nginx aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="1d593-140">In the previous part, you used the `docker run` command to bring up Nginx.</span></span> <span data-ttu-id="1d593-141">Führen Sie den Befehl ein zweites Mal aus, und sehen Sie sich genauer an, was passiert.</span><span class="sxs-lookup"><span data-stu-id="1d593-141">Let's run that command a second time and take a closer look into what's happening.</span></span>

1. <span data-ttu-id="1d593-142">Führen Sie diesen Befehl über Ihre SSH-Verbindung aus, um einen Container aufzurufen, der nginx ausführt.</span><span class="sxs-lookup"><span data-stu-id="1d593-142">From your SSH connection, run this command to bring up a container running Nginx.</span></span>

    ```bash
    docker run -d -p 8080:80 nginx
    ```

    * <span data-ttu-id="1d593-143">Das `-d`-Argument gibt an, dass der Container im Modus „Getrennt“ ausgeführt wird, d.h., der Container wird im Hintergrund ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="1d593-143">The `-d` argument specifies that the container will run in a detached mode, which means the container runs in the background.</span></span> <span data-ttu-id="1d593-144">Wenn der nginx-Prozess beendet wird oder abstürzt, wird auch der Container beendet.</span><span class="sxs-lookup"><span data-stu-id="1d593-144">If the Nginx process stops or crashes, the container itself is also stopped.</span></span>
    * <span data-ttu-id="1d593-145">Das `-p`-Argument gibt an, dass Netzwerkdatenverkehr, den der Port 8080 des Containerhosts empfängt (in diesem Fall Ihre Linux-VM), an Port 80 des Containers weitergeleitet wird.</span><span class="sxs-lookup"><span data-stu-id="1d593-145">The `-p` argument specifies that network traffic arriving to port 8080 on the container host, your Linux VM in this case, is forwarded to port 80 on the container.</span></span> <span data-ttu-id="1d593-146">Sie haben dieses Argument im vorherigen Teil verwendet, um über Ihren Browser auf den Webserver zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="1d593-146">You used this argument in the previous part to access the web server from your browser.</span></span>
    * <span data-ttu-id="1d593-147">Beim `nginx`-Argument handelt es sich um den Namen des Containerimages, das ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="1d593-147">The `nginx` argument is the name of the container image to run.</span></span>

    <span data-ttu-id="1d593-148">Eine vollständige Liste der `docker run`-Optionen finden Sie in der [Referenz zu „docker run“](https://docs.docker.com/engine/reference/run?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="1d593-148">Later, you can explore the complete list of `docker run` options in the [docker run reference](https://docs.docker.com/engine/reference/run?azure-portal=true).</span></span>

    <span data-ttu-id="1d593-149">Der Befehl `docker run` zeigt einen eindeutigen Bezeichner für den Container an.</span><span class="sxs-lookup"><span data-stu-id="1d593-149">The `docker run` command displays a unique identifier for the container.</span></span> <span data-ttu-id="1d593-150">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1d593-150">For example:</span></span>

    ```output
    9d7327e3121200cfe2dccb627544db1442a4e02ed3151f30681db4e538ef9466
    ```

1. <span data-ttu-id="1d593-151">Führen Sie den Befehl `docker ps` aus, um die Container aufzulisten, die auf Ihrem System ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="1d593-151">Run `docker ps` to list the running containers on your system.</span></span>

    ```bash
    docker ps
    ```

    <span data-ttu-id="1d593-152">Der soeben gestartete nginx-Container sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="1d593-152">You see the Nginx container you just started.</span></span> <span data-ttu-id="1d593-153">Beachten Sie, dass der Container sowohl über eine ID als auch über einen Namen verfügt.</span><span class="sxs-lookup"><span data-stu-id="1d593-153">Notice that the container has both an ID and a name.</span></span> <span data-ttu-id="1d593-154">Sie können einen dieser Werte zum Verwalten des Containers verwenden.</span><span class="sxs-lookup"><span data-stu-id="1d593-154">You can use either one of these values to manage the container.</span></span> <span data-ttu-id="1d593-155">Notieren Sie sich die Container-ID.</span><span class="sxs-lookup"><span data-stu-id="1d593-155">Note the container ID.</span></span> <span data-ttu-id="1d593-156">Sie werden sie später benötigen.</span><span class="sxs-lookup"><span data-stu-id="1d593-156">You'll use it later.</span></span>

    ```output
    CONTAINER ID        IMAGE               COMMAND                  CREATED     STATUS              PORTS                  NAMES
    9d7327e31212        nginx               "nginx -g 'daemon of…"   4 minutes ago     Up 4 minutes        0.0.0.0:8080->80/tcp   compassionate_allen
    ```

1. <span data-ttu-id="1d593-157">Sie können den ausgeführten Webserver wie zuvor mit der IP-Adresse der VM im Browser anzeigen.</span><span class="sxs-lookup"><span data-stu-id="1d593-157">As you did previously, you can navigate to your VM's IP address in a browser to see the running web server.</span></span> <span data-ttu-id="1d593-158">Vergessen Sie nicht, Port 8080 als Teil der URL anzugeben.</span><span class="sxs-lookup"><span data-stu-id="1d593-158">Don't forget to specify port 8080 as part of the URL.</span></span>

    ![Die Website im Browser](../media/2-nginx-browser.png)

## <a name="delete-containers"></a><span data-ttu-id="1d593-160">Löschen von Containern</span><span class="sxs-lookup"><span data-stu-id="1d593-160">Delete containers</span></span>

<span data-ttu-id="1d593-161">Mit dem Befehl `docker rm` können Sie einen Container löschen.</span><span class="sxs-lookup"><span data-stu-id="1d593-161">You use the `docker rm` command to delete a container.</span></span> <span data-ttu-id="1d593-162">Sie können den zu löschenden Container anhand seines Namens oder seiner ID angeben.</span><span class="sxs-lookup"><span data-stu-id="1d593-162">You can specify the container by its name or ID.</span></span>

1. <span data-ttu-id="1d593-163">Versuchen Sie, den Befehl `docker rm` auszuführen, um den Container zu löschen, der nginx ausführt.</span><span class="sxs-lookup"><span data-stu-id="1d593-163">Try running `docker rm` to delete your container running Nginx.</span></span> <span data-ttu-id="1d593-164">Führen Sie den Befehl `docker ps` aus, wenn Sie die ID abrufen müssen.</span><span class="sxs-lookup"><span data-stu-id="1d593-164">Run `docker ps` if you need to find the ID.</span></span> <span data-ttu-id="1d593-165">Hier sehen Sie ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="1d593-165">Here's an example.</span></span>

    ```bash
    docker rm 9d7327e31212
    ```

    <span data-ttu-id="1d593-166">Wie Sie sehen, kann der Container nicht entfernt werden, da er sich im Ausführungszustand befindet.</span><span class="sxs-lookup"><span data-stu-id="1d593-166">You see that the container can't be removed because it's in the running state.</span></span>

    ```output
    Error response from daemon: You cannot remove a running container 9d7327e3121200cfe2dccb627544db1442a4e02ed3151f30681db4e538ef9466. Stop the container before attempting removal or force remove
    ```

1. <span data-ttu-id="1d593-167">Führen Sie den Befehl `docker stop` aus, um den Container zu beenden.</span><span class="sxs-lookup"><span data-stu-id="1d593-167">Run `docker stop` to stop the container.</span></span> <span data-ttu-id="1d593-168">Hier sehen Sie ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="1d593-168">Here's an example.</span></span>

    ```bash
    docker stop 9d7327e31212
    ```
    
1. <span data-ttu-id="1d593-169">Führen Sie den Befehl `docker ps` aus, um sicherzustellen, dass der Container nicht mehr ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="1d593-169">Run `docker ps` to verify that the container is no longer running.</span></span>

    ```bash
    docker ps
    ```

    <span data-ttu-id="1d593-170">Sie sehen Folgendes.</span><span class="sxs-lookup"><span data-stu-id="1d593-170">You see this.</span></span>

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATEDSTATUS              PORTS               NAMES
    ```

1. <span data-ttu-id="1d593-171">Führen Sie den Befehl `docker ps` ein weiteres Mal aus, jedoch geben Sie diesmal das Flag `-a` an.</span><span class="sxs-lookup"><span data-stu-id="1d593-171">Run `docker ps` a second time, but this time provide th `-a` flag.</span></span> <span data-ttu-id="1d593-172">Damit werden alle Container aufgelistet, auch die, die beendet wurden.</span><span class="sxs-lookup"><span data-stu-id="1d593-172">This lists all containers, even those that are stopped.</span></span>

    ```bash
    docker ps -a
    ```

    <span data-ttu-id="1d593-173">Ihnen sollte eine Ausgabe angezeigt werden, die wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="1d593-173">You see output similar to this:</span></span>

    ```output
    CONTAINER ID        IMAGE               COMMAND                  CREATED     STATUS                          PORTS               NAMES
    9d7327e31212        nginx               "nginx -g 'daemon of…"   11 minutes ago     Exited (0) About a minute ago                       compassionate_allen
    df8aeea0320f        alpine              "echo 'Hello World'"     About an hour ago   Exited (0) About an hour ago                        objective_payne
    3a7efb75c288        nginx               "nginx -g 'daemon of…"   About an hour ago   Exited (0) About an hour ago                        nginx
    ```

    <span data-ttu-id="1d593-174">Die Ausgabe enthält den nginx-Container, den Sie soeben beendet haben, sowie die anderen Container, die Sie vorher ausgeführt haben.</span><span class="sxs-lookup"><span data-stu-id="1d593-174">The output includes the Nginx container you just stopped as well as the other containers you ran prior.</span></span>

1. <span data-ttu-id="1d593-175">Führen Sie `docker rm` ein weiteres Mal aus.</span><span class="sxs-lookup"><span data-stu-id="1d593-175">Run `docker rm` a second time.</span></span> <span data-ttu-id="1d593-176">Ersetzen Sie die angezeigte ID durch eine Ihrer IDs.</span><span class="sxs-lookup"><span data-stu-id="1d593-176">Replace the ID shown with one of yours.</span></span>

    ```bash
    docker rm 9d7327e31212
    ```

1. <span data-ttu-id="1d593-177">Führen Sie den folgenden `docker rm`-Befehl aus, um _alle_ aktiven Container zu löschen.</span><span class="sxs-lookup"><span data-stu-id="1d593-177">Run the following `docker rm` command to delete _all_ active containers.</span></span>

    ```bash
    docker rm $(docker ps -aq)
    ```

1. <span data-ttu-id="1d593-178">Führen Sie `docker ps -a` erneut aus. Dann wird angezeigt, dass keine aktiven Container ausgeführt oder beendet werden.</span><span class="sxs-lookup"><span data-stu-id="1d593-178">Run `docker ps -a` again and you see that there are no active containers running or stopped.</span></span>

    ```bash
    docker ps -a
    ```

## <a name="delete-a-container-image"></a><span data-ttu-id="1d593-179">Löschen eines Containerimages</span><span class="sxs-lookup"><span data-stu-id="1d593-179">Delete a container image</span></span>

<span data-ttu-id="1d593-180">Mit dem Befehl `docker rmi` können Sie ein Containerimage löschen.</span><span class="sxs-lookup"><span data-stu-id="1d593-180">You use the `docker rmi` command to delete a container image.</span></span>

<span data-ttu-id="1d593-181">Sie können ein Image nur löschen, wenn kein Container, der über dieses Image gestartet wurde, aktiv ist, unabhängig davon, ob er ausgeführt oder beendet wird.</span><span class="sxs-lookup"><span data-stu-id="1d593-181">You can only delete an image if no container started from that image, running or stopped, is active.</span></span> <span data-ttu-id="1d593-182">Allerdings erzwingt das `-f`-Argument die Entfernung aller zugehörigen Container und entfernt anschließend das Containerimage.</span><span class="sxs-lookup"><span data-stu-id="1d593-182">However, the `-f` argument forces the removal of all associated containers and will then remove the container image.</span></span>

1. <span data-ttu-id="1d593-183">Führen Sie den Befehl `docker rmi nginx` aus, um das nginx-Image aus Ihrer Linux-VM zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="1d593-183">Run `docker rmi nginx` to remove the Nginx image from your Linux VM.</span></span>

    ```bash
    docker rmi nginx
    ```

    <span data-ttu-id="1d593-184">Die angezeigte Ausgabe sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="1d593-184">The output you see resembles this:</span></span>

    ```output
    Untagged: nginx:latest
    Untagged: nginx@sha256:24a0c4b4a4c0eb97a1aabb8e29f18e917d05abfe1b7a7c07857230879ce7d3d3
    Deleted: sha256:06144b2878448774e55577ae7d66b5f43a87c2e44322b3884e4e6c70d070b262
    Deleted: sha256:824a442ee3c96744d75be3737a22cc6a47aebad1b30be67f3c2f8f29cb0aa879
    Deleted: sha256:8e3d1e9e4945f930c93c30617512998437f6edafd86676770d29b1581f2520bb
    Deleted: sha256:8b15606a9e3e430cb7ba739fde2fbb3734a19f8a59a825ffa877f9be49059817
    ```

1. <span data-ttu-id="1d593-185">Führen Sie den Befehl `docker images` aus, um die Images auf der VM aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="1d593-185">Run `docker images` to list the images on your VM.</span></span> 

    ```bash
    docker images
    ```

    <span data-ttu-id="1d593-186">Das **alpine**-Image wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="1d593-186">You see the **alpine** image.</span></span>

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATEDSIZE
    alpine              latest              196d12cf6ab1        8 days ago4.41MB
    ```

1. <span data-ttu-id="1d593-187">Führen Sie den folgenden `docker rmi`-Befehl aus, um _alle_ Images von der VM zu löschen.</span><span class="sxs-lookup"><span data-stu-id="1d593-187">Run the following `docker rmi` command to delete _all_ images from your VM.</span></span>

    ```bash
    docker rmi $(docker images -q)
    ```

1. <span data-ttu-id="1d593-188">Führen Sie den Befehl `docker images` erneut aus, und Sie werden sehen, dass keine Images auf der VM vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="1d593-188">Run `docker images` again and you see that there are no images on the VM.</span></span>

    ```bash
    docker images
    ```
