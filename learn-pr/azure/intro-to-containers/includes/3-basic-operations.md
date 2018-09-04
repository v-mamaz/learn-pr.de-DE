<span data-ttu-id="fcf84-101">Sie verfügen jetzt über eine funktionsfähige Umgebung für die Entwicklung von Containern und können sich nachfolgend über einige grundlegende Containervorgänge informieren.</span><span class="sxs-lookup"><span data-stu-id="fcf84-101">Now that you have a functioning container development environment, lets take a quick spin through some basic container operations.</span></span> <span data-ttu-id="fcf84-102">Diese Einheit umfasst nicht einmal ansatzweise alle verfügbaren Docker-Funktionen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-102">This unit doesn't include a complete list of Docker capabilities (not even close).</span></span> <span data-ttu-id="fcf84-103">Allerdings erfahren Sie, wie Sie Container ausführen, auflisten und löschen können.</span><span class="sxs-lookup"><span data-stu-id="fcf84-103">This unit will prepare you to run, list, and delete containers.</span></span> <span data-ttu-id="fcf84-104">Im Laufe dieses Moduls erhalten Sie zusätzliche Informationen zu Containervorgängen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-104">Throughout the remainder of this module, you will gain additional exposure to container operations.</span></span>

## <a name="run-a-basic-container"></a><span data-ttu-id="fcf84-105">Ausführen eines Standardcontainers</span><span class="sxs-lookup"><span data-stu-id="fcf84-105">Run a basic container</span></span>

<span data-ttu-id="fcf84-106">Bevor Sie mehr zu den Einzelheiten zum Ausführen und Verwalten von Containern erfahren, erhalten Sie zunächst grundlegende Informationen zum Ausführen eines Containers.</span><span class="sxs-lookup"><span data-stu-id="fcf84-106">Before digging into the details of running and managing containers, let's quickly see just how easy it is to run a container.</span></span>

<span data-ttu-id="fcf84-107">Erstellen Sie Ihren ersten Container über den folgenden Befehl.</span><span class="sxs-lookup"><span data-stu-id="fcf84-107">Create your first container with the following command.</span></span>

```bash
docker run alpine echo "Hello World"
```

<span data-ttu-id="fcf84-108">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fcf84-108">You should see output similar to the following:</span></span>

```bash
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
8e3ba11ec2a2: Pull complete
Digest: sha256:7043076348bf5040220df6ad703798fd8593a0918d06d3ce30c6c93be117e430
Status: Downloaded newer image for alpine:latest
Hello World
```

<span data-ttu-id="fcf84-109">Der Befehl `docker run` erstellt eine Instanz eines Containers.</span><span class="sxs-lookup"><span data-stu-id="fcf84-109">The `docker run` command creates an instance of a container.</span></span> <span data-ttu-id="fcf84-110">In diesem Fall wurde der Container aus einem Containerimage mit dem Namen `alpine` erstellt. Dieses wurde heruntergeladen und in Ihrem lokalen System gespeichert.</span><span class="sxs-lookup"><span data-stu-id="fcf84-110">In this case, the container was created from a container image named `alpine`, which was downloaded to your local system.</span></span> <span data-ttu-id="fcf84-111">Nachdem der Container gestartet wurde, wurde der Befehl `echo "Hello World"` innerhalb des Containers ausgeführt und die Ausgabe an Ihr Terminal übergeben.</span><span class="sxs-lookup"><span data-stu-id="fcf84-111">After the container started, the `echo "Hello World"` command was run inside of the container and the output echoed to your terminal.</span></span>

<span data-ttu-id="fcf84-112">Noch müssen Sie sich keine Gedanken zu den technischen Details der einzelnen Aktionen machen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-112">At this point, don't worry about the technical details of each of these actions.</span></span> <span data-ttu-id="fcf84-113">Diese werden im Laufe dieses Moduls näher erläutert.</span><span class="sxs-lookup"><span data-stu-id="fcf84-113">They will be detailed throughout this module.</span></span>

## <a name="get-container-images"></a><span data-ttu-id="fcf84-114">Aufrufen von Containerimages</span><span class="sxs-lookup"><span data-stu-id="fcf84-114">Get container images</span></span>

<span data-ttu-id="fcf84-115">Container werden wie im Beispiel „Hallo Welt“ dargestellt über ein Containerimage ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="fcf84-115">As you saw in the hello world example, containers are run from a container image.</span></span> <span data-ttu-id="fcf84-116">Dieses Image umfasst das containerbasierte Betriebssystem und jegliche zusätzlichen Prozesse, Anwendungen und Konfigurationen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-116">These images include the container base operating system and any additional processes, applications, and configurations.</span></span> <span data-ttu-id="fcf84-117">Containerimages werden in einer Containerimageregistrierung gespeichert.</span><span class="sxs-lookup"><span data-stu-id="fcf84-117">Container images are stored in a container image registry.</span></span> <span data-ttu-id="fcf84-118">In dem Beispiel „Hallo Welt“ wurde das Image *Alpine* aus Docker Hub entnommen. Es handelt sich dabei um eine öffentliche Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="fcf84-118">In the hello world example, the *alpine* image was pulled from Docker Hub, which is a public container registry.</span></span>

<span data-ttu-id="fcf84-119">Nachfolgend wird erläutert, wie Sie ein zuvor erstelltes Containerimage suchen und herunterladen können.</span><span class="sxs-lookup"><span data-stu-id="fcf84-119">Let's see how to search for and download a pre-created container image.</span></span>

<span data-ttu-id="fcf84-120">Führen Sie den folgenden Befehl aus, um eine Liste mit Images abzurufen, die heruntergeladen und in Ihrem System gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="fcf84-120">Run the following command to see a list of images that have been downloaded to your system.</span></span>

```bash
docker images
```

<span data-ttu-id="fcf84-121">Wenn Sie alle Schritte wie beschrieben ausgeführt haben, sollte das Image „Alpin“ angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="fcf84-121">If you've been following along, you should see the alpine image.</span></span> <span data-ttu-id="fcf84-122">Dieses Image wurde heruntergeladen, als das Beispiel „Hallo Welt“ ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="fcf84-122">This image was downloaded when the hello world example was run.</span></span>

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

<span data-ttu-id="fcf84-123">Verwenden Sie den Befehl `docker search`, um nach einem Containerimage zu suchen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-123">To search for a container image, use the `docker search` command.</span></span> <span data-ttu-id="fcf84-124">Sie können das folgende Beispiel verwenden, um alle Containerimages aufzulisten, deren Namen `nginx` enthält.</span><span class="sxs-lookup"><span data-stu-id="fcf84-124">For instance, use the following example to list all container images that include `nginx` in the name.</span></span>

```bash
docker search nginx
```

<span data-ttu-id="fcf84-125">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fcf84-125">The output should look similar to the following:</span></span>

```bash
NAME                                                   DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                                                  Official build of Nginx.                        9071                [OK]
jwilder/nginx-proxy                                    Automated Nginx reverse proxy for docker con…   1365                                    [OK]
richarvey/nginx-php-fpm                                Container running Nginx + PHP-FPM capable of…   593                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion                 LetsEncrypt container to use with nginx as p…   390                                     [OK]
kong                                                   Open-source Microservice & API Management la…   207                 [OK]
webdevops/php-nginx                                    Nginx with PHP-FPM                              106                                     [OK]
kitematic/hello-world-nginx                            A light-weight nginx container that demonstr…   102
zabbix/zabbix-web-nginx-mysql                          Zabbix frontend based on Nginx web-server wi…   60                                      [OK]
bitnami/nginx                                          Bitnami nginx Docker Image                      54                                      [OK]
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          38                                      [OK]
linuxserver/nginx                                      An Nginx container, brought to you by LinuxS…   37
tobi312/rpi-nginx                                      NGINX on Raspberry Pi / armhf                   20                                      [OK]
nginxdemos/nginx-ingress                               NGINX Ingress Controller for Kubernetes . Th…   11
blacklabelops/nginx                                    Dockerized Nginx Reverse Proxy Server.          10                                      [OK]
wodby/drupal-nginx                                     Nginx for Drupal container image                9                                       [OK]
webdevops/nginx                                        Nginx container                                 8                                       [OK]
nginxdemos/hello                                       NGINX webserver that serves a simple page co…   7                                       [OK]
centos/nginx-18-centos7                                Platform for running nginx 1.8 or building n…   6
1science/nginx                                         Nginx Docker images that include Consul Temp…   4                                       [OK]
centos/nginx-112-centos7                               Platform for running nginx 1.12 or building …   3
pebbletech/nginx-proxy                                 nginx-proxy sets up a container running ngin…   2                                       [OK]
travix/nginx                                           NGinx reverse proxy                             1                                       [OK]
toccoag/openshift-nginx                                Nginx reverse proxy for Nice running on same…   1                                       [OK]
ansibleplaybookbundle/nginx-apb                        An APB to deploy NGINX                          0                                       [OK]
mailu/nginx                                            Mailu nginx frontend                            0                                       [OK]
```

<span data-ttu-id="fcf84-126">Wenn Sie ein Image erst herunterladen möchten, bevor Sie es ausführen, verwenden Sie den Befehl `docker pull`.</span><span class="sxs-lookup"><span data-stu-id="fcf84-126">If you'd like to pre-download an image prior to running it, use the `docker pull` command.</span></span> <span data-ttu-id="fcf84-127">Das folgende Beispiel pullt das *NGINX*-Image in Ihr System.</span><span class="sxs-lookup"><span data-stu-id="fcf84-127">The following example pulls the *nginx* image to your system.</span></span>

```bash
docker pull nginx
```

<span data-ttu-id="fcf84-128">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fcf84-128">The output should look similar to the following:</span></span>

```bash
Using default tag: latest
latest: Pulling from library/nginx
be8881be8156: Pull complete
f2f27ed9664f: Extracting [===============>                                   ]  6.652MB/22.14MB
54ff137eb1b2: Download complete
```

<span data-ttu-id="fcf84-129">Führen Sie `docker images` erneut aus, um alle Images in Ihrem System aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="fcf84-129">Run `docker images` again to list all of the images on your system.</span></span> <span data-ttu-id="fcf84-130">Dann sollten Sie sehen, dass das *NGINX*-Image zu Ihrem System hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="fcf84-130">You'll see that the *nginx* image has been added to your system.</span></span>

```bash
docker images
```

<span data-ttu-id="fcf84-131">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fcf84-131">The output should look similar to the following:</span></span>

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              c82521676580        26 hours ago        109MB
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

## <a name="run-containers"></a><span data-ttu-id="fcf84-132">Ausführen von Containern</span><span class="sxs-lookup"><span data-stu-id="fcf84-132">Run containers</span></span>

<span data-ttu-id="fcf84-133">Da Sie jetzt das *NGINX*-Image ermittelt und heruntergeladen haben, können Sie jetzt darüber einen Container ausführen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-133">Now that you've identified and downloaded the *nginx* image, run a container from the image.</span></span> <span data-ttu-id="fcf84-134">Wenn Sie die Docker-CLI verwenden, um ein Containerimage auszuführen, greifen Sie auf den Befehl `docker run` zurück.</span><span class="sxs-lookup"><span data-stu-id="fcf84-134">When using the Docker CLI to run a container image, use the `docker run` command.</span></span>

<span data-ttu-id="fcf84-135">Im folgenden Beispiel gibt das Argument `-d` an, dass der Container im Modus „Getrennt“ ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="fcf84-135">In the following example, the `-d` argument specifies that the container will run in a detached mode.</span></span> <span data-ttu-id="fcf84-136">In dieser Konfiguration führt der Container einen festgelegten Prozess aus.</span><span class="sxs-lookup"><span data-stu-id="fcf84-136">In this configuration, the container runs a specified process.</span></span> <span data-ttu-id="fcf84-137">Wenn dieser Prozess anhält oder abstürzt, wird auch der Container angehalten.</span><span class="sxs-lookup"><span data-stu-id="fcf84-137">If that process stops or crashes, the container itself is stopped.</span></span> <span data-ttu-id="fcf84-138">Das `-p 8080:80`-Argument gibt an, dass Netzwerkdatenverkehr, den der Port 8080 auf dem Containerhost empfängt (in diesem fall Ihr Entwicklungssystem), an Port 80 auf dem Container weitergeleitet wird.</span><span class="sxs-lookup"><span data-stu-id="fcf84-138">The `-p 8080:80` argument species that network traffic arriving to port 8080 on the container host, your development system in this case, is forwarded to port 80 of the container.</span></span> <span data-ttu-id="fcf84-139">Bei Argument `ngingx` handelt es sich um den Namen, des Containerimages, das ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="fcf84-139">Finally, the `ngingx` argument is the name of the container image to run.</span></span>

<span data-ttu-id="fcf84-140">Eine vollständige Liste mit `docker run`-Argumenten finden Sie in der [Referenz zur Ausführung von Docker](https://docs.docker.com/engine/reference/run/).</span><span class="sxs-lookup"><span data-stu-id="fcf84-140">For a complete list of `docker run` arguments, see the [docker run reference](https://docs.docker.com/engine/reference/run/).</span></span>

```bash
docker run -d -p 8080:80 nginx
```

<span data-ttu-id="fcf84-141">Dieser Vorgang gibt die vollständige Container-ID zurück.</span><span class="sxs-lookup"><span data-stu-id="fcf84-141">This operation returns the full container ID.</span></span>

```bash
bd2424bfe7a5423d7d65efdf0b1622770d59e212db7b82862c3129fb630b5721
```

<span data-ttu-id="fcf84-142">Listen Sie die Container, die auf Ihrem System ausgeführt werden, mithilfe des Befehls `docker ps` auf.</span><span class="sxs-lookup"><span data-stu-id="fcf84-142">List the running containers on your system using the `docker ps` command.</span></span>

```bash
docker ps
```

<span data-ttu-id="fcf84-143">Es sollte ein einzelner Container angezeigt werden, der ausgeführt wird. Dabei handelt es sich um den NGINX-Container, der im letzten Schritt ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="fcf84-143">You should see a single running container, which is the NGINX container run in the last step.</span></span> <span data-ttu-id="fcf84-144">Beachten Sie, dass der Container sowohl über eine ID als auch über einen Namen verfügt.</span><span class="sxs-lookup"><span data-stu-id="fcf84-144">Notice that the container has both an ID and a Name.</span></span> <span data-ttu-id="fcf84-145">Beide Werte können verwendet werden, um den Container zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="fcf84-145">Either one of these values can be used to manage the container.</span></span> <span data-ttu-id="fcf84-146">Notieren Sie sich die Container-ID.</span><span class="sxs-lookup"><span data-stu-id="fcf84-146">Take note of the container ID.</span></span> <span data-ttu-id="fcf84-147">Dieser Wert wird in der nächsten Einheit verwendet.</span><span class="sxs-lookup"><span data-stu-id="fcf84-147">This value will be used later in the unit.</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
bd2424bfe7a5        nginx               "nginx -g 'daemon of…"   37 minutes ago      Up 37 minutes       0.0.0.0:8080->80/tcp   gallant_engelbart
```

<span data-ttu-id="fcf84-148">Öffnen Sie einen Internetbrowser, und geben Sie die Adresse http://localhost:8080 ein, um den Container zu testen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-148">To test the container, open an internet browser and enter http://localhost:8080 for the address.</span></span> <span data-ttu-id="fcf84-149">Anschließend sollte die Standardwebsite von NGINX angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="fcf84-149">After it completes, you should see the NGINX default website.</span></span>

![Microsoft Edge mit dem Begrüßungsbildschirm von NGINX](../media-draft/3-nginx.png)

## <a name="delete-containers"></a><span data-ttu-id="fcf84-151">Löschen von Containern</span><span class="sxs-lookup"><span data-stu-id="fcf84-151">Delete containers</span></span>

<span data-ttu-id="fcf84-152">Wenn Sie einen Container nicht mehr verwenden möchten, können Sie diesen löschen, indem Sie den Namen oder die ID des Containers zum Befehl `docker rm` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-152">When you're done working with a container, it can be deleted by providing the container name or ID to the `docker rm` command.</span></span> <span data-ttu-id="fcf84-153">Testen Sie dies mit der ID des Containers, der NGINX ausführt.</span><span class="sxs-lookup"><span data-stu-id="fcf84-153">Try out this operation with the container ID of the container running NGINX.</span></span> <span data-ttu-id="fcf84-154">Ersetzen Sie die ID in diesem Beispiel durch die ID aus Ihrer Umgebung.</span><span class="sxs-lookup"><span data-stu-id="fcf84-154">Replace the ID in this example with the ID from your environment.</span></span>

```bash
docker rm bd2424bfe7a5
```

<span data-ttu-id="fcf84-155">Beachten Sie, dass der Container nicht entfernt werden kann, da er sich im Ausführungszustand befindet.</span><span class="sxs-lookup"><span data-stu-id="fcf84-155">Notice that the container can't be removed because it's in a running state.</span></span>

```bash
Error response from daemon: You cannot remove a running container a31c5a5f2a8d6e420435bfcadbe158fa6a26ed29c005a892171505cc0c2861b2. Stop the container before attempting removal or force remove
```

<span data-ttu-id="fcf84-156">Halten Sie den Container über den Befehl `docker stop` an.</span><span class="sxs-lookup"><span data-stu-id="fcf84-156">Stop the container with the `docker stop` command.</span></span>

```bash
docker stop bd2424bfe7a5
```

<span data-ttu-id="fcf84-157">Beachten Sie dabei, dass der NGINX-Container nicht aufgeführt wird, wenn Sie `docker ps` ausführen, um alle Container aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="fcf84-157">Notice at this point, if you run `docker ps` to list all containers, the nginx container is not listed.</span></span>

```bash
docker ps
```

<span data-ttu-id="fcf84-158">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fcf84-158">The output should look similar to the following:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

<span data-ttu-id="fcf84-159">Fügen Sie dem Befehl `docker ps` das Argument `-a` hinzu, um eine Liste aller Container zurückzugeben, einschließlich der Container, die angehalten wurden.</span><span class="sxs-lookup"><span data-stu-id="fcf84-159">To return a list of all containers, including containers in a stopped state, add the `-a` argument to the `docker ps` command.</span></span>

```bash
docker ps -a
```

<span data-ttu-id="fcf84-160">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fcf84-160">The output should look similar to the following:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS               NAMES
bd2424bfe7a5        nginx               "nginx -g 'daemon of…"   13 seconds ago      Exited (0) 3 seconds ago                       focused_spence
```

<span data-ttu-id="fcf84-161">Versuchen Sie erneut, den Löschvorgang auszuführen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-161">Try the delete operation again.</span></span> <span data-ttu-id="fcf84-162">Ersetzen Sie die ID in diesem Beispiel durch die ID aus Ihrer Umgebung.</span><span class="sxs-lookup"><span data-stu-id="fcf84-162">Replace the ID in this example with the ID from your environment.</span></span>

```bash
docker rm bd2424bfe7a5
```

<span data-ttu-id="fcf84-163">Dieser Vorgang gibt die Container-ID zurück.</span><span class="sxs-lookup"><span data-stu-id="fcf84-163">This operation returns the container ID.</span></span>

```bash
bd2424bfe7a5
```

## <a name="delete-a-container-image"></a><span data-ttu-id="fcf84-164">Löschen eines Containerimage</span><span class="sxs-lookup"><span data-stu-id="fcf84-164">Delete a container image</span></span>

<span data-ttu-id="fcf84-165">Wenn Sie ein Containerimage nicht mehr verwenden, können Sie es über den Befehl `docker rmi` entfernen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-165">When you're done working with a container image, it can be removed with the `docker rmi` command.</span></span> <span data-ttu-id="fcf84-166">Wenn ein Container über das Containerimage gestartet wurde, kann dieses nicht gelöscht werden. Dabei spielt es keine Rolle, ob der Container noch ausgeführt wird oder angehalten wurde.</span><span class="sxs-lookup"><span data-stu-id="fcf84-166">If any container (running or stopped) has been started from the container image, the image can't be deleted.</span></span> <span data-ttu-id="fcf84-167">Sie müssen zunächst die Container entfernen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-167">The containers first need to be removed.</span></span> <span data-ttu-id="fcf84-168">Wenn Sie das Argument `-f` zum Befehl `docker rmi` hinzufügen, wird erzwungen, dass alle zugeordneten Container entfernt werden. Anschließend wird auch das Containerimage entfernt.</span><span class="sxs-lookup"><span data-stu-id="fcf84-168">Adding the `-f` argument to the `docker rmi` command will force the removal of all associated containers, and will then remove the container image.</span></span>

<span data-ttu-id="fcf84-169">Entfernen Sie das NGINX-Containerimage mithilfe des folgenden Befehls.</span><span class="sxs-lookup"><span data-stu-id="fcf84-169">Remove the NGINX container image with the following command.</span></span>

```bash
docker rmi nginx
```

<span data-ttu-id="fcf84-170">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="fcf84-170">The output should look similar to the following:</span></span>

```bash
Untagged: nginx:latest
Untagged: nginx@sha256:4a5573037f358b6cdfa2f3e8a9c33a5cf11bcd1675ca72ca76fbe5bd77d0d682
Deleted: sha256:8b89e48b5f157d9455c963b57c85d21e2337c58b8c983bc06f88476610adc129
Deleted: sha256:119ded3eca5e85ef43ee966e74564c604ccda064d955a8c5ed762e1d5e87f428
Deleted: sha256:6ece91c2763d826487e707f7b8ec063742ad0ee56cc9e605465cce95550c9a7f
Deleted: sha256:cdb3f9544e4c61d45da1ea44f7d92386639a052c620d1550376f22f5b46981af
```

## <a name="summary"></a><span data-ttu-id="fcf84-171">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="fcf84-171">Summary</span></span>

<span data-ttu-id="fcf84-172">In dieser Einheit wurden einige grundlegende Docker-Vorgänge erläutert.</span><span class="sxs-lookup"><span data-stu-id="fcf84-172">In this unit, you learned about some basic Docker operations.</span></span> <span data-ttu-id="fcf84-173">In der nächsten Einheit erfahren Sie, wie Sie ein benutzerdefiniertes Containerimage erstellen.</span><span class="sxs-lookup"><span data-stu-id="fcf84-173">In the next unit, you will create a custom container image.</span></span>