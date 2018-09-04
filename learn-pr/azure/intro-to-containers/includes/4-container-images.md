<span data-ttu-id="e16fc-101">In der letzten Einheit haben Sie mit vorgefertigten Containerimages gearbeitet, um einfache Docker-Vorgänge durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-101">In the last unit, you worked with pre-created container images to perform some basic Docker operations.</span></span> <span data-ttu-id="e16fc-102">In dieser Einheit erstellen Sie benutzerdefinierte Containerimages, übermitteln diese mithilfe von Push an eine öffentliche Containerregistrierung und führen Container über diese Images aus.</span><span class="sxs-lookup"><span data-stu-id="e16fc-102">In this unit, you will create custom container images, push these images to a public container registry, and run containers from these images.</span></span>

<span data-ttu-id="e16fc-103">Containerimages können manuell oder mit einer sogenannten Dockerfile erstellt werden, um den Vorgang zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="e16fc-103">Container images can be created by hand or using what's called a Dockerfile to automate the process.</span></span> <span data-ttu-id="e16fc-104">Es wird empfohlen, eine Dockerfile zu verwenden, aber in dieser Einheit werden beide Methode veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="e16fc-104">The preferred method is using a Dockerfile, but this unit will demonstrate both methods.</span></span> <span data-ttu-id="e16fc-105">Sie sollen verstehen, wie der manuelle Vorgang funktioniert, damit Sie wissen, was bei der Automatisierung mit einer Dockerfile abläuft.</span><span class="sxs-lookup"><span data-stu-id="e16fc-105">The intention is that having an understanding of the manual process will help you to better understand what's occurring when using a Dockerfile for automation.</span></span>

## <a name="manual-image-creation"></a><span data-ttu-id="e16fc-106">Manuelle Imageerstellung</span><span class="sxs-lookup"><span data-stu-id="e16fc-106">Manual image creation</span></span>

<span data-ttu-id="e16fc-107">Wenn Sie ein Containerimage manuell erstellen, werden die folgenden Aktionen durchgeführt:</span><span class="sxs-lookup"><span data-stu-id="e16fc-107">When manually creating a container image, the following actions are taken:</span></span>

- <span data-ttu-id="e16fc-108">Sie starten eine Instanz eines Containers.</span><span class="sxs-lookup"><span data-stu-id="e16fc-108">Start an instance of a container.</span></span>
- <span data-ttu-id="e16fc-109">Sie beginnen eine Terminalsitzung mit dem Container.</span><span class="sxs-lookup"><span data-stu-id="e16fc-109">Establish a terminal session with the container.</span></span>
- <span data-ttu-id="e16fc-110">Sie passen den Container an, indem Sie Software installieren und Konfigurationen ändern.</span><span class="sxs-lookup"><span data-stu-id="e16fc-110">Modify the container by installing software and making configuration changes.</span></span>
- <span data-ttu-id="e16fc-111">Erfassen des Containers in einem neuen Image mit dem Befehl `docker capture`.</span><span class="sxs-lookup"><span data-stu-id="e16fc-111">Capturing the container into a new image using the `docker capture` command.</span></span>

<span data-ttu-id="e16fc-112">In diesem ersten Beispiel starten Sie eine Instanz eines Containers, in dem Python ausgeführt wird, erstellen eine Hallo Welt-Anwendung und erfassen den Container in einem neuen Image.</span><span class="sxs-lookup"><span data-stu-id="e16fc-112">In this first example, you start an instance of a container that's running Python, create a hello world application, and then capture the container to a new image.</span></span>

<span data-ttu-id="e16fc-113">Führen Sie zunächst einen Container über das NGINX-Image aus.</span><span class="sxs-lookup"><span data-stu-id="e16fc-113">First, run a container from the NGINX image.</span></span> <span data-ttu-id="e16fc-114">Dieser Befehl unterscheidet sich etwas von den Befehlen, die Sie in den vorherigen Einheiten ausgeführt haben.</span><span class="sxs-lookup"><span data-stu-id="e16fc-114">This command looks a bit different from the commands that you ran in the previous unit.</span></span> <span data-ttu-id="e16fc-115">Weil Sie eine Terminalsitzung mit dem ausgeführten Container starten möchten, werden die Argumente `-t` und `-i` einbezogen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-115">Because you want to establish a terminal session with the running container, the `-t` and `-i` arguments are provided.</span></span> <span data-ttu-id="e16fc-116">In Kombination weisen diese Argumente Docker an, ein Pseudoterminal zuzuweisen, das weiter ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="e16fc-116">Together, these arguments instruct Docker to allocate a pseudo terminal that will remain in a runnings state.</span></span> <span data-ttu-id="e16fc-117">D.h., die Argumente `-t` und `-i` erstellen eine interaktive Sitzung mit dem ausführten Container.</span><span class="sxs-lookup"><span data-stu-id="e16fc-117">In other words, the `-t` and `-i` arguments create an interactive session with the running container.</span></span>

<span data-ttu-id="e16fc-118">Dann geben Sie an,dass das `python`-Containerimage verwendet werden soll und dass der Prozess, der im Container ausgeführt werden soll, `bash` ist.</span><span class="sxs-lookup"><span data-stu-id="e16fc-118">You then specify that the `python` container image is used, and the process to run inside of the container is `bash`.</span></span>

```bash
docker run --name python-demo -ti python bash
```

<span data-ttu-id="e16fc-119">Nachdem der Befehl ausgeführt wurde, sollte Ihre Terminalsitzung zum Pseudoterminal des Containers wechseln.</span><span class="sxs-lookup"><span data-stu-id="e16fc-119">After the command is run, your terminal session should switch to the containers pseudo terminal.</span></span> <span data-ttu-id="e16fc-120">Dieses erkennen Sie an der Terminalaufforderung, die sich etwa wie folgt geändert haben sollte:</span><span class="sxs-lookup"><span data-stu-id="e16fc-120">This can be seen by the terminal prompt, which should have changed to something similar to the following:</span></span>

```bash
root@d8ccada9c61e:/#
```

<span data-ttu-id="e16fc-121">Jetzt arbeiten Sie im Container.</span><span class="sxs-lookup"><span data-stu-id="e16fc-121">At this point, you're working inside the container.</span></span> <span data-ttu-id="e16fc-122">Sie werden feststellen, dass das Arbeiten in einem Container sich kaum vom Arbeiten in einem virtuellen oder physischen System unterscheidet.</span><span class="sxs-lookup"><span data-stu-id="e16fc-122">You should find that working inside a container is much like working inside a virtual or physical system.</span></span> <span data-ttu-id="e16fc-123">Sie können z.B. Dateien auflisten, erstellen und löschen, Software installieren und Konfigurationen anpassen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-123">For instance, you can list, create, and delete files, install software, and make configuration changes.</span></span> <span data-ttu-id="e16fc-124">In diesem Beispiel wird ein Python-basiertes Hallo Welt-Skript erstellt.</span><span class="sxs-lookup"><span data-stu-id="e16fc-124">For this simple example, a Python-based hello world script is created.</span></span> <span data-ttu-id="e16fc-125">Führen Sie dazu den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="e16fc-125">This can be done with the following command:</span></span>

```bash
echo 'print("Hello World!")' > hello.py
```

<span data-ttu-id="e16fc-126">Führen Sie den folgenden Befehl aus, um das Skript zu testen, während Sie sich noch im Container befinden:</span><span class="sxs-lookup"><span data-stu-id="e16fc-126">To test the script while you're still in the container, run the following command:</span></span>

```bash
python hello.py
```

<span data-ttu-id="e16fc-127">Das erzeugt die folgende Ausgabe:</span><span class="sxs-lookup"><span data-stu-id="e16fc-127">This will produce the following output:</span></span>

```bash
Hello World!
```

<span data-ttu-id="e16fc-128">Wenn das Skript wie erwartet ausgeführt wird, können Sie den Container über den Befehl `exit` verlassen:</span><span class="sxs-lookup"><span data-stu-id="e16fc-128">When you're satisfied that the script functions as expected, exit out of the container by typing `exit`:</span></span>

```bash
exit
```

<span data-ttu-id="e16fc-129">Verwenden Sie im Terminal Ihres lokalen Systems den Befehl `docker ps`, um alle Container aufzulisten, die aufgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="e16fc-129">Back in the terminal of your local system, use the `docker ps` command to list all running containers:</span></span>

```bash
docker ps
```

<span data-ttu-id="e16fc-130">Beachten Sie, dass nichts ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="e16fc-130">Notice that nothing is running.</span></span> <span data-ttu-id="e16fc-131">Wenn Sie `exit` in den ausgeführten Container eingegeben haben, wurde der Bash-Prozess abgeschlossen, wodurch der Container angehalten wurde.</span><span class="sxs-lookup"><span data-stu-id="e16fc-131">When you entered `exit` in the running container, the Bash process completed, which then stopped the container.</span></span> <span data-ttu-id="e16fc-132">Dies entspricht dem erwarteten Verhalten und ist in Ordnung.</span><span class="sxs-lookup"><span data-stu-id="e16fc-132">This is the expected behavior and is ok.</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

<span data-ttu-id="e16fc-133">Verwenden Sie `docker ps` erneut, und schließen Sie das `-a`-Argument mit ein.</span><span class="sxs-lookup"><span data-stu-id="e16fc-133">Use `docker ps` again and include the `-a` argument.</span></span> <span data-ttu-id="e16fc-134">Dieser Befehl gibt eine Liste aller Container zurück, egal ob diese ausgeführt werden oder nicht.</span><span class="sxs-lookup"><span data-stu-id="e16fc-134">This command will return a list of all containers, regardless if they're running.</span></span>

```bash
docker ps -a
```

<span data-ttu-id="e16fc-135">Beachten Sie, dass ein Container mit dem Namen *python-demo* den Status *Beendet* aufweist.</span><span class="sxs-lookup"><span data-stu-id="e16fc-135">Notice that a container with the name *python-demo* has a status of *Exited*.</span></span> <span data-ttu-id="e16fc-136">Dieser Container ist die angehaltene Instanz des Containers, den Sie gerade beendet haben.</span><span class="sxs-lookup"><span data-stu-id="e16fc-136">This container is the stopped instance of the container that you just exited from.</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
cf6ac8e06fd9        python              "bash"              27 seconds ago      Exited (0) 12 seconds ago                       python-demo
```

<span data-ttu-id="e16fc-137">Verwenden Sie den `docker commit`-Befehl, um ein neues Containerimage aus diesem Container zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-137">To create a new container image from this container, use the `docker commit` command.</span></span> <span data-ttu-id="e16fc-138">Das folgende Beispiel weist *docker commit* an, ein Image namens *python-custom* aus den *python-demo*-Containern zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-138">The following example instructs *docker commit* to create an image named *python-custom* from the *python-demo* containers.</span></span>

```bash
docker commit python-demo python-custom
```

<span data-ttu-id="e16fc-139">Nach Abschluss des Befehls sollten Sie eine Ausgabe ähnlich der folgenden erhalten:</span><span class="sxs-lookup"><span data-stu-id="e16fc-139">After the command completes, you should see output similar to the following:</span></span>

```bash
sha256:91a0cf9aa9857bebcd7ebec3418970f97f043e31987fd4a257c8ac8c8418dc38
```

<span data-ttu-id="e16fc-140">Führen Sie nun `docker images` aus, um eine Liste der Containerimages anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="e16fc-140">Now run `docker images` to see a list of container images:</span></span>

```bash
docker images
```

<span data-ttu-id="e16fc-141">Sie sollten nun das benutzerdefinierte Python-Image sehen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-141">You should now see the custom Python image.</span></span>

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
python-custom       latest              1f231e7127a1        6 seconds ago       922MB
python              latest              638817465c7d        24 hours ago        922MB
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

<span data-ttu-id="e16fc-142">Führen Sie einen Container über das neue Image aus.</span><span class="sxs-lookup"><span data-stu-id="e16fc-142">Run a container from the new image.</span></span> <span data-ttu-id="e16fc-143">Sie müssen auch angeben, welcher Befehl oder Prozess innerhalb des Containers ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="e16fc-143">You also need to specify what command or process to run inside of the container.</span></span> <span data-ttu-id="e16fc-144">Führen Sie in diesem Beispiel `python hello.py` aus.</span><span class="sxs-lookup"><span data-stu-id="e16fc-144">With this example, run `python hello.py`.</span></span>


```bash
docker run python-custom python hello.py
```

<span data-ttu-id="e16fc-145">Der Container wird gestartet, und er gibt die Meldung „Hallo, Welt“ aus.</span><span class="sxs-lookup"><span data-stu-id="e16fc-145">The container will start and output the hello world message.</span></span> <span data-ttu-id="e16fc-146">Der Python-Prozess ist dann abgeschlossen, und der Container wird angehalten.</span><span class="sxs-lookup"><span data-stu-id="e16fc-146">The Python process is then complete and the container stops.</span></span>

```bash
Hello World!
```

## <a name="automated-image-creation"></a><span data-ttu-id="e16fc-147">Automatische Imageerstellung</span><span class="sxs-lookup"><span data-stu-id="e16fc-147">Automated image creation</span></span>

<span data-ttu-id="e16fc-148">Im letzten Abschnitt wurde ein Containerimage manuell erstellt.</span><span class="sxs-lookup"><span data-stu-id="e16fc-148">In the last section, a container image was manually created.</span></span> <span data-ttu-id="e16fc-149">Obwohl diese Methode für eine einmalige oder experimentelle Imageerstellung bestens geeignet ist, ist sie in einer Produktionsumgebung nicht tolerierbar.</span><span class="sxs-lookup"><span data-stu-id="e16fc-149">While this method works great for one-off or experiential image creation, it's not sustainable in a production environment.</span></span> <span data-ttu-id="e16fc-150">Die Erstellung eines Containerimages kann mithilfe einer *Dockerfile* und des `docker build`-Befehls automatisiert werden.</span><span class="sxs-lookup"><span data-stu-id="e16fc-150">Container image creation can be automated using a *Dockerfile* and the `docker build` command.</span></span> <span data-ttu-id="e16fc-151">Der *docker build*-Befehl startet im Wesentlichen einen Container, führt die in der *Dockerfile* enthaltenen Anweisungen aus und erfasst anschließend die Ergebnisse für ein neues Containerimage.</span><span class="sxs-lookup"><span data-stu-id="e16fc-151">The *docker build* command essentially starts a container, runs the instructions found in the *Dockerfile*, and then captures the results to a new container image.</span></span>

<span data-ttu-id="e16fc-152">Erstellen Sie eine Datei namens *Dockerfile*, und geben Sie folgenden Text ein:</span><span class="sxs-lookup"><span data-stu-id="e16fc-152">Create a file named *Dockerfile* and enter the following text:</span></span>

```bash
FROM python

WORKDIR ./app

RUN echo 'print("Hello World!")' > hello.py

CMD python hello.py
```

<span data-ttu-id="e16fc-153">Die *FROM*-Anweisung gibt das Basisimage an, das während der Imageerstellung verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="e16fc-153">The *FROM* statement specifies the base image to be used during image creations.</span></span> <span data-ttu-id="e16fc-154">Die *RUN*-Anweisung führt Befehle innerhalb des Containers aus.</span><span class="sxs-lookup"><span data-stu-id="e16fc-154">The *RUN* statement runs commands inside of the container.</span></span> <span data-ttu-id="e16fc-155">*RUN* kann dann zum Installieren von Software, zur Durchführung von Konfigurationsänderungen und zum Bereinigen des Containers vor der Erfassung genutzt werden.</span><span class="sxs-lookup"><span data-stu-id="e16fc-155">*RUN* can be used to install software, make configuration changes, and clean up the container before the capture event.</span></span> <span data-ttu-id="e16fc-156">Die *CMD*-Anweisung gibt den Prozess an, der ausgeführt werden soll, wenn ein Container gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="e16fc-156">The *CMD* statement specifies the process that should run when a container is started.</span></span>

<span data-ttu-id="e16fc-157">Verwenden Sie den `docker build`-Befehl, um ein neues Containerimage mithilfe der in der Dockerfile angegebenen Anweisungen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-157">Use the `docker build` command to create a new container image using the instructions specified in the Dockerfile.</span></span>

```bash
docker build -t python-dockerfile .
```

<span data-ttu-id="e16fc-158">Eine Ausgabe ähnlich der folgenden sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="e16fc-158">You should see output similar to the following.</span></span>

```bash
Sending build context to Docker daemon  2.048kB
Step 1/4 : FROM python
 ---> 638817465c7d
Step 2/4 : WORKDIR ./app
 ---> Running in 990d17e86466
Removing intermediate container 990d17e86466
 ---> 59a074a092cc
Step 3/4 : RUN echo 'print("Hello World!")' > hello.py
 ---> Running in aed707c53bc5
Removing intermediate container aed707c53bc5
 ---> d7f55a9d0e85
Step 4/4 : CMD python hello.py
 ---> Running in e87ec55a8d36
Removing intermediate container e87ec55a8d36
 ---> 98c39b91770f
Successfully built 98c39b91770f
Successfully tagged python-dockerfile:latest
```

<span data-ttu-id="e16fc-159">Verwenden Sie den `docker images`-Befehl, um eine Liste von Containerimages zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="e16fc-159">Use the `docker images` command to return a list of container images.</span></span>

```bash
docker images
```

<span data-ttu-id="e16fc-160">Sie sollten nun das benutzerdefinierte Image sehen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-160">You should now see the custom image.</span></span>

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
python-dockerfile   latest              98c39b91770f        About a minute ago   922MB
python              latest              638817465c7d        26 hours ago         922MB
alpine              latest              11cd0b38bc3c        2 weeks ago          4.41MB
```

<span data-ttu-id="e16fc-161">Verwenden Sie den `docker run`-Befehl, um einen Container aus dem benutzerdefinierten Image auszuführen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-161">Use the `docker run` command to run a container from the custom image.</span></span>

<span data-ttu-id="e16fc-162">Beachten Sie, dass dem Befehl `docker run` keine Argumente bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="e16fc-162">Notice here that no arguments have been provided to the `docker run` command.</span></span> <span data-ttu-id="e16fc-163">Anders als bei der manuellen Erstellung eines Containerimages ermöglicht eine Dockerfile das Einschließen eines Befehls, der beim Containerstart ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="e16fc-163">Unlike when you manually create a container image, a Dockerfile allows you to include a command to run when the container starts.</span></span> <span data-ttu-id="e16fc-164">In diesem Fall ist der spezifische Befehl `python hello.py`, wodurch der Container das Python-Skript ausführt.</span><span class="sxs-lookup"><span data-stu-id="e16fc-164">In this case, the specified command is `python hello.py`, which causes the container to run the Python script.</span></span>

```bash
docker run python-dockerfile
```

<span data-ttu-id="e16fc-165">Nachdem Sie den Befehl ausgeführt haben, sollte die Containerausgabe angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="e16fc-165">After you run the command, you should see the container output.</span></span>

```bash
Hello World!
```

## <a name="push-the-image-to-a-public-registry"></a><span data-ttu-id="e16fc-166">Pushen des Images an eine öffentliche Registrierung</span><span class="sxs-lookup"><span data-stu-id="e16fc-166">Push the image to a public registry</span></span>

<span data-ttu-id="e16fc-167">Docker Hub ist eine öffentliche Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="e16fc-167">Docker Hub is a public container registry.</span></span> <span data-ttu-id="e16fc-168">Damit Containerimages per Push an Docker Hub übertragen werden können, müssen Sie über ein Docker-Konto verfügen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-168">In order to push container images to Docker Hub, you must have a Docker account.</span></span> <span data-ttu-id="e16fc-169">Besuchen Sie ggf. die [Docker Hub-Website](https://hub.docker.com/), um sich für ein Konto zu registrieren.</span><span class="sxs-lookup"><span data-stu-id="e16fc-169">If needed, visit the [Docker Hub site](https://hub.docker.com/) to register for an account.</span></span>

<span data-ttu-id="e16fc-170">Wenn Sie ein Docker Hub-Konto besitzen, muss das Containerimage mit dem Kontonamen gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="e16fc-170">After you have a Docker Hub account, the container image must be tagged with the account name.</span></span> <span data-ttu-id="e16fc-171">Verwenden Sie hierzu den `docker tag`-Befehl.</span><span class="sxs-lookup"><span data-stu-id="e16fc-171">To do so, use the `docker tag` command.</span></span>

<span data-ttu-id="e16fc-172">Im folgenden Beispiel wird das Image *python-dockerfile* mit dem Docker Hub-Kontonamen gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="e16fc-172">In the following example, the *python-dockerfile* image is tagged with a Docker Hub account name.</span></span> <span data-ttu-id="e16fc-173">Ersetzen Sie `<account name>` durch Ihren Docker Hub-Kontonamen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-173">Replace `<account name>` with your Docker Hub account name.</span></span>

```bash
docker tag python-dockerfile <account name>/python-dockerfile
```

<span data-ttu-id="e16fc-174">Stellen Sie dann sicher, dass Sie über den `docker login`-Befehl bei Docker Hub angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="e16fc-174">Next, make sure that you are logged into Docker Hub using the `docker login` command.</span></span>

```bash
docker login
```

<span data-ttu-id="e16fc-175">Übertragen Sie zuletzt das Image *python-dockerfile* mit dem Befehl `docker push` per Push an Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="e16fc-175">Finally push the *python-dockerfile* image to Docker Hub using the `docker push` command.</span></span> <span data-ttu-id="e16fc-176">Ersetzen Sie `<account name>` durch Ihren Docker Hub-Kontonamen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-176">Replace `<account name>` with your Docker Hub account name.</span></span>

```bash
docker push <account name>/python-dockerfile
```

<span data-ttu-id="e16fc-177">Sobald das Containerimage in Docker Hub hochgeladen wurde, wird Ihnen eine Ausgabe ähnlich der folgenden angezeigt:</span><span class="sxs-lookup"><span data-stu-id="e16fc-177">While the container image is being uploaded to Docker Hub, you will see output similar to the following:</span></span>

```bash
The push refers to repository [docker.io/account/python-dockerfile]
f39073ca4d5a: Pushed
9dfcec2738a9: Pushed
ffab8273c674: Mounted from account/python
e6f6cbe5e14e: Mounted from account/python
3eb255f8a6ac: Mounted from account/python
b860b6c48eec: Mounted from account/python
1fa8778eb779: Mounted from account/python
fa0c3f992cbd: Mounted from account/python
ce6466f43b11: Mounted from account/python
719d45669b35: Mounted from account/python
3b10514a95be: Mounted from account/python
```

<span data-ttu-id="e16fc-178">Das Containerimage wird nun in Docker Hub gespeichert, und Sie können von jedem Gerät mit Internetverbindung über `docker pull` oder `docker run` auf dieses zugreifen.</span><span class="sxs-lookup"><span data-stu-id="e16fc-178">The container image is now stored in Docker Hub and can be accessed from any internet-connected machine using `docker pull` or `docker run`.</span></span>

## <a name="summary"></a><span data-ttu-id="e16fc-179">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="e16fc-179">Summary</span></span>

<span data-ttu-id="e16fc-180">In dieser Einheit haben Sie zwei Containerimages erstellt.</span><span class="sxs-lookup"><span data-stu-id="e16fc-180">In this unit, you created two container images.</span></span> <span data-ttu-id="e16fc-181">Das erste wurde manuell erstellt, das zweite über eine Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="e16fc-181">The first was created manually and the second was automated using a Dockerfile.</span></span>
