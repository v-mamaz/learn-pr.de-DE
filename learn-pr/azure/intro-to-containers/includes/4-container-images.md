<span data-ttu-id="ee224-101">Bisher haben Sie Docker-Images heruntergeladen und ausgeführt, die von anderen Benutzern erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="ee224-101">Up until now, you downloaded and ran Docker images created by others.</span></span> <span data-ttu-id="ee224-102">In dieser Einheit erstellen Sie eigene Containerimages.</span><span class="sxs-lookup"><span data-stu-id="ee224-102">Here, you'll build your own container images.</span></span> <span data-ttu-id="ee224-103">Sie lernen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="ee224-103">You'll learn how to:</span></span>

* <span data-ttu-id="ee224-104">Das manuelle Erstellen eines Images</span><span class="sxs-lookup"><span data-stu-id="ee224-104">Create an image using a manual process.</span></span>
* <span data-ttu-id="ee224-105">Das Erstellen des gleichen Images mithilfe eines stärker automatisierten Prozesses in Form einer Dockerfile</span><span class="sxs-lookup"><span data-stu-id="ee224-105">Create the same image using a more automated process, called a Dockerfile.</span></span>
* <span data-ttu-id="ee224-106">Das Veröffentlichen Ihres Images auf Docker Hub, einer öffentlichen Containerregistrierung</span><span class="sxs-lookup"><span data-stu-id="ee224-106">Publish your image to Docker Hub, a public container registry.</span></span>

## <a name="what-is-a-dockerfile"></a><span data-ttu-id="ee224-107">Was ist eine Dockerfile?</span><span class="sxs-lookup"><span data-stu-id="ee224-107">What is a Dockerfile?</span></span>

<span data-ttu-id="ee224-108">Eine Dockerfile ist eine Textdatei, die alle Voraussetzungen für das Ausführen Ihres Containers enthält.</span><span class="sxs-lookup"><span data-stu-id="ee224-108">A Dockerfile is a text file that describes everything your container needs to run.</span></span>

<span data-ttu-id="ee224-109">Eine Anweisung in der Dockerfile kann Folgendes definieren:</span><span class="sxs-lookup"><span data-stu-id="ee224-109">An instruction in the Dockerfile can define:</span></span>

* <span data-ttu-id="ee224-110">Das übergeordnete Image, auf dem Ihr Image basiert</span><span class="sxs-lookup"><span data-stu-id="ee224-110">The parent image your image is based on.</span></span>
* <span data-ttu-id="ee224-111">Ein zu installierendes Softwarepaket</span><span class="sxs-lookup"><span data-stu-id="ee224-111">A software package to install.</span></span>
* <span data-ttu-id="ee224-112">Eine Konfigurationsdatei oder eine andere Datei, die für die Ausführung Ihrer App erforderlich ist</span><span class="sxs-lookup"><span data-stu-id="ee224-112">A configuration or other file your app needs to run.</span></span>
* <span data-ttu-id="ee224-113">Netzwerkeinstellungen, z.B. der Port, der zur Verfügung gestellt werden soll</span><span class="sxs-lookup"><span data-stu-id="ee224-113">Networking settings, such as a port you want to make available.</span></span>
* <span data-ttu-id="ee224-114">Der Befehl, der beim Start des Containers ausgeführt werden soll</span><span class="sxs-lookup"><span data-stu-id="ee224-114">The command to run when the container starts.</span></span>

<span data-ttu-id="ee224-115">Sie können ein Containerimage manuell oder mithilfe einer Dockerfile erstellen, um den Prozess zu automatisieren.</span><span class="sxs-lookup"><span data-stu-id="ee224-115">You can create a container image using a manual process or use a Dockerfile to automate the process.</span></span> <span data-ttu-id="ee224-116">Das manuelle Erstellen eines Docker-Images ist gut geeignet, um die Vorgehensweise zu erlernen.</span><span class="sxs-lookup"><span data-stu-id="ee224-116">Creating a Docker image manually is a good way to understand the process.</span></span> <span data-ttu-id="ee224-117">Durch das Erstellen einer Dockerfile wird der Prozess beschleunigt und kann einfacher wiederholt werden.</span><span class="sxs-lookup"><span data-stu-id="ee224-117">Using a Dockerfile makes the process faster and easier to repeat.</span></span>

## <a name="what-is-docker-hub"></a><span data-ttu-id="ee224-118">Was ist Docker Hub?</span><span class="sxs-lookup"><span data-stu-id="ee224-118">What is Docker Hub?</span></span>

<span data-ttu-id="ee224-119">Docker Hub ist ein Ort, an dem Sie Docker-Images speichern und herunterladen können.</span><span class="sxs-lookup"><span data-stu-id="ee224-119">Docker Hub is a place for you to store and download Docker images.</span></span> <span data-ttu-id="ee224-120">Sie können Docker-Images herunterladen, die von Docker und der Docker-Community erstellt wurden, z.B. das nginx-Image, das Sie zuvor verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="ee224-120">You can download Docker images that have been created by Docker and the Docker community, such as the Nginx image you used previously.</span></span> <span data-ttu-id="ee224-121">Sie können ebenfalls eigene Images für die Docker-Community oder nur für Ihr Team freigeben.</span><span class="sxs-lookup"><span data-stu-id="ee224-121">You can also share your own images with the Docker community or just with your team.</span></span>

## <a name="create-an-image-manually"></a><span data-ttu-id="ee224-122">Manuelles Erstellen eines Images</span><span class="sxs-lookup"><span data-stu-id="ee224-122">Create an image manually</span></span>

<span data-ttu-id="ee224-123">In dieser Einheit erstellen Sie ein Docker-Image, das eine einfache Python-Anwendung ausführt.</span><span class="sxs-lookup"><span data-stu-id="ee224-123">Here you'll create a Docker image that runs a basic Python application.</span></span>

1. <span data-ttu-id="ee224-124">Beginnen Sie mit dem Einbinden einer Containerinstanz aus dem [python](https://hub.docker.com/_/python/?azure-portal=true)-Image.</span><span class="sxs-lookup"><span data-stu-id="ee224-124">Start by bringing up a container instance from the [python](https://hub.docker.com/_/python/?azure-portal=true) image.</span></span>

    ```bash
    docker run --name python-demo -it python bash
    ```

    <span data-ttu-id="ee224-125">Es dauert einen Moment, bis Docker das Image von Docker Hub heruntergeladen hat.</span><span class="sxs-lookup"><span data-stu-id="ee224-125">It'll take a few moments for Docker to pull down this image from Docker Hub.</span></span> <span data-ttu-id="ee224-126">Während der Wartezeit können Sie sich mit der Funktionsweise des Befehls vertraut machen.</span><span class="sxs-lookup"><span data-stu-id="ee224-126">While you wait, let's look at what the command does.</span></span>

    * <span data-ttu-id="ee224-127">Das Argument `--name` gibt den Namen Ihres Containers an, „python-demo“.</span><span class="sxs-lookup"><span data-stu-id="ee224-127">The `--name` argument specifies your container's name, "python-demo".</span></span>
    * <span data-ttu-id="ee224-128">Die Argumente `-i` und `-t` werden zu einem Argument, `-it`, kombiniert.</span><span class="sxs-lookup"><span data-stu-id="ee224-128">The `-i` and `-t` arguments are combined into one argument, `-it`.</span></span> <span data-ttu-id="ee224-129">Mit diesen Argumenten wird eine interaktive Sitzung mit dem ausgeführten Container erstellt.</span><span class="sxs-lookup"><span data-stu-id="ee224-129">These arguments create an interactive session with the running container.</span></span>
      * <span data-ttu-id="ee224-130">`-i` erstellt eine interaktive Sitzung mit dem Container.</span><span class="sxs-lookup"><span data-stu-id="ee224-130">`-i` creates an interactive session with the container.</span></span>
      * <span data-ttu-id="ee224-131">`-t` erstellt ein Pseudoterminal, das dauerhaft ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="ee224-131">`-t` creates a pseudo terminal that remains in a running state.</span></span>
    * <span data-ttu-id="ee224-132">`python` gibt das Basisimage an.</span><span class="sxs-lookup"><span data-stu-id="ee224-132">`python` specifies the base image.</span></span> <span data-ttu-id="ee224-133">Docker lädt dieses Image von Docker Hub herunter.</span><span class="sxs-lookup"><span data-stu-id="ee224-133">Docker downloads this image from Docker Hub.</span></span> <span data-ttu-id="ee224-134">Dieses Image ist mit einer Umgebung für die Python-Programmierung vorkonfiguriert.</span><span class="sxs-lookup"><span data-stu-id="ee224-134">This image is preconfigued with an environment for Python programming.</span></span>
    * <span data-ttu-id="ee224-135">`bash` gibt das Programm an, das ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="ee224-135">`bash` specifies the program to run.</span></span>

    <span data-ttu-id="ee224-136">Stellen Sie sich dieses Setup als interaktive Umgebung vor, in der Sie Python-Apps schreiben.</span><span class="sxs-lookup"><span data-stu-id="ee224-136">Think of this setup as an interactive environment for you to write Python apps.</span></span> <span data-ttu-id="ee224-137">Sobald Ihre App fertig ist und ausgeführt wird, können Sie ein Image oder eine Momentaufnahme Ihrer Umgebung erstellen.</span><span class="sxs-lookup"><span data-stu-id="ee224-137">Once you have your app up and running, you can capture an image, or snapshot, of your environment.</span></span> <span data-ttu-id="ee224-138">Wenn Sie Ihre App weiter verbessern, können Sie zusätzliche Images für sich und Ihr Team erstellen.</span><span class="sxs-lookup"><span data-stu-id="ee224-138">As you improve your app, you can create additional images for you or your team.</span></span>

    <span data-ttu-id="ee224-139">Ihre Terminalsitzung wechselt zum Pseudoterminal des Containers.</span><span class="sxs-lookup"><span data-stu-id="ee224-139">Your terminal session switches to the container's pseudo terminal.</span></span> <span data-ttu-id="ee224-140">Ihnen wird Folgendes angezeigt:</span><span class="sxs-lookup"><span data-stu-id="ee224-140">Your prompt resembles this:</span></span>

    ```docker
    root@d8ccada9c61e:/#
    ```

1. <span data-ttu-id="ee224-141">Führen Sie Folgendes über Ihre Docker-Sitzung aus, um ein Verzeichnis namens `./app` zu erstellen. Wechseln Sie anschließend in dieses Verzeichnis.</span><span class="sxs-lookup"><span data-stu-id="ee224-141">From your Docker session, run this to create a directory named `./app` and move to it.</span></span>

    ```bash
    mkdir ./app && cd ./app
    ```

    <span data-ttu-id="ee224-142">Obwohl es nicht zwingend erforderlich ist, können Sie Ihren Python-Code über das Verzeichnis `./app` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="ee224-142">Although not required, the `./app` directory gives you a place to add your Python code.</span></span>

1. <span data-ttu-id="ee224-143">Führen Sie Folgendes aus, um ein einfaches Python-Programm zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ee224-143">Run this to create a very basic Python program.</span></span>

    ```bash
    echo 'print("Hello World!")' > hello.py
    ```

    <span data-ttu-id="ee224-144">Dieses Programm gibt „Hello World!“</span><span class="sxs-lookup"><span data-stu-id="ee224-144">This program prints "Hello World!"</span></span> <span data-ttu-id="ee224-145">im Terminal aus.</span><span class="sxs-lookup"><span data-stu-id="ee224-145">to the terminal.</span></span>

    > [!TIP]
    > <span data-ttu-id="ee224-146">In der Praxis können Sie ein Verzeichnis in Ihrer Arbeitsstation in ein Verzeichnis in Ihrem Container _einbinden_.</span><span class="sxs-lookup"><span data-stu-id="ee224-146">In practice, you can _mount_ a directory on your workstation to a directory on your container.</span></span> <span data-ttu-id="ee224-147">Dadurch können Sie Ihren bevorzugten Editor verwenden, um Code auf Ihrer Arbeitsstation zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="ee224-147">This enables you to use your favorite editor on your workstation to write code.</span></span> <span data-ttu-id="ee224-148">Wenn Sie die Datei speichern, wird diese auch im Container angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ee224-148">When you save your file, that file also appears on your container.</span></span>

1. <span data-ttu-id="ee224-149">Führen Sie Folgendes aus, um Ihr Python-Programm zu testen.</span><span class="sxs-lookup"><span data-stu-id="ee224-149">Run the following to try out your Python program.</span></span>

    ```bash
    python hello.py
    ```

    <span data-ttu-id="ee224-150">Sie sehen Folgendes.</span><span class="sxs-lookup"><span data-stu-id="ee224-150">You see this.</span></span>

    ```output
    Hello World!
    ```

1. <span data-ttu-id="ee224-151">Beenden Sie die interaktive Sitzung.</span><span class="sxs-lookup"><span data-stu-id="ee224-151">Exit your interactive session.</span></span>

    ```bash
    exit
    ```

1. <span data-ttu-id="ee224-152">Führen Sie über Ihren virtuellen Linux-Computer `docker ps` aus, um alle ausgeführten Container aufzulisten:</span><span class="sxs-lookup"><span data-stu-id="ee224-152">From your Linux VM, run `docker ps` to list all running containers:</span></span>

    ```bash
    docker ps
    ```

    <span data-ttu-id="ee224-153">Sie sehen, dass keine Container ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="ee224-153">You see that nothing is running.</span></span> 

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    ```

    <span data-ttu-id="ee224-154">Das liegt daran, dass das Beenden des Containers auch Ihre Bash-Sitzung beendet.</span><span class="sxs-lookup"><span data-stu-id="ee224-154">That's because exiting the container ends your Bash session.</span></span> <span data-ttu-id="ee224-155">Wenn die Anwendung oder der Dienst, den Ihr Container ausführt, beendet wird, hält Docker den Container an.</span><span class="sxs-lookup"><span data-stu-id="ee224-155">When the application or service your container runs exits, Docker stops the container.</span></span>

1. <span data-ttu-id="ee224-156">Führen Sie `docker ps` erneut aus, und fügen Sie das Argument `-a` hinzu.</span><span class="sxs-lookup"><span data-stu-id="ee224-156">Run `docker ps` a second time and include the `-a` argument.</span></span> <span data-ttu-id="ee224-157">Dieser Befehl gibt alle ausgeführten und angehaltenen Container zurück.</span><span class="sxs-lookup"><span data-stu-id="ee224-157">This command returns all containers, running or stopped.</span></span>

    ```bash
    docker ps -a
    ```

    <span data-ttu-id="ee224-158">Folgendes sollte angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="ee224-158">You see something like this:</span></span>

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
    cf6ac8e06fd9        python              "bash"              27 seconds ago      Exited (0) 12 seconds ago                       python-demo
    ```

   <span data-ttu-id="ee224-159">Ihr Container, **python-demo**, weist den Status **Exited** (Beendet) auf.</span><span class="sxs-lookup"><span data-stu-id="ee224-159">Your container, **python-demo**, has a status of **Exited**.</span></span>

1. <span data-ttu-id="ee224-160">Führen Sie `docker commit` aus, um ein Image Ihres Containers zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ee224-160">Run `docker commit` to create an image from your container.</span></span>

   ```bash
   docker commit python-demo python-custom
   ```

   <span data-ttu-id="ee224-161">In diesem Fall erstellt Docker ein Image namens **python-custom** aus dem Container namens **python-demo**.</span><span class="sxs-lookup"><span data-stu-id="ee224-161">Here, Docker creates an image named **python-custom** from your container named **python-demo**.</span></span> <span data-ttu-id="ee224-162">Den Namen des Images können Sie nach Belieben ändern.</span><span class="sxs-lookup"><span data-stu-id="ee224-162">The image name can be whatever you want.</span></span>

1. <span data-ttu-id="ee224-163">Führen Sie `docker images` aus, um Ihre Images aufzuführen.</span><span class="sxs-lookup"><span data-stu-id="ee224-163">Run `docker images` to list your images.</span></span>

    ```bash
    docker images
    ```

    <span data-ttu-id="ee224-164">Das Image **python-custom** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ee224-164">You see the **python-custom** image.</span></span>

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    python-custom       latest              1f231e7127a1        6 seconds ago       922MB
    python              latest              638817465c7d        24 hours ago        922MB
    ```

1. <span data-ttu-id="ee224-165">Verwenden Sie `docker run`, um Ihr Image zu testen.</span><span class="sxs-lookup"><span data-stu-id="ee224-165">Use `docker run` to test out your image.</span></span>

    ```bash
    docker run python-custom python app/hello.py
    ```

    <span data-ttu-id="ee224-166">Denken Sie daran, dass `docker run` den auszuführenden Befehl als letztes Argument verwendet.</span><span class="sxs-lookup"><span data-stu-id="ee224-166">Recall that `docker run` takes the command to run as its final argument.</span></span> <span data-ttu-id="ee224-167">In diesem Fall ist der Befehl `python app/hello.py`.</span><span class="sxs-lookup"><span data-stu-id="ee224-167">Here, the command is `python app/hello.py`.</span></span>

    <span data-ttu-id="ee224-168">Sie sehen Folgendes.</span><span class="sxs-lookup"><span data-stu-id="ee224-168">You see this.</span></span>

    ```output
    Hello World!
    ```

    <span data-ttu-id="ee224-169">Da Sie diesen Container nicht interaktiv ausführen, wird das Python-Programm beendet, und der Container wird angehalten.</span><span class="sxs-lookup"><span data-stu-id="ee224-169">Because you're not running this container interactively, the Python program runs and the container stops.</span></span>

## <a name="use-a-dockerfile-to-create-an-image-automatically"></a><span data-ttu-id="ee224-170">Verwenden einer Dockerfile zum automatischen Erstellen eines Images</span><span class="sxs-lookup"><span data-stu-id="ee224-170">Use a Dockerfile to create an image automatically</span></span>

<span data-ttu-id="ee224-171">In diesem Fall verwenden Sie einen stärker automatisierten Prozess, um das gleiche Docker-Image zu erstellen, das das Python-Programm ausführt.</span><span class="sxs-lookup"><span data-stu-id="ee224-171">Here you'll use a more automated process to create the same Docker image that runs your Python program.</span></span>

<span data-ttu-id="ee224-172">Das manuelle Erstellen eines Images ist optimal dafür geeignet, neue Features zu entdecken und mit diesen zu experimentieren.</span><span class="sxs-lookup"><span data-stu-id="ee224-172">Building an image manually is a great way to experiment and explore new features.</span></span> <span data-ttu-id="ee224-173">Angenommen, Sie möchten den Prozess für Ihr Team freigeben oder diesen wiederholbar gestalten.</span><span class="sxs-lookup"><span data-stu-id="ee224-173">But say you want to share the process with your team or make it repeatable.</span></span> <span data-ttu-id="ee224-174">Dies kann der Fall sein, wenn Sie jeden Abend ein neues Image erstellen möchten, das die neueste Version der Software ausführt, die Ihr Team erstellt.</span><span class="sxs-lookup"><span data-stu-id="ee224-174">For example, say you want to create a new image each evening that runs the latest version of the software your team is building.</span></span>

<span data-ttu-id="ee224-175">An diesem Punkt kommt die Dockerfile ins Spiel.</span><span class="sxs-lookup"><span data-stu-id="ee224-175">That's where the Dockerfile comes in.</span></span> <span data-ttu-id="ee224-176">Stellen Sie sich eine Dockerfile als Möglichkeit vor, um Anweisungen festzuhalten, die Sie normalerweise manuell ausführen würden.</span><span class="sxs-lookup"><span data-stu-id="ee224-176">Think of a Dockerfile as a way to describe instructions you would otherwise do manually.</span></span>

1. <span data-ttu-id="ee224-177">Führen Sie diesen Befehl über Ihren virtuellen Linux-Computer aus, um eine Dockerfile zu erstellen, die Ihr Python-Programm ausführt.</span><span class="sxs-lookup"><span data-stu-id="ee224-177">From your Linux VM, run this command to create a Dockerfile that runs your Python program.</span></span>

    ```bash
    cat << EOF > Dockerfile
    FROM python
    
    WORKDIR ./app
    
    RUN echo 'print("Hello World!")' > hello.py
    
    CMD python hello.py
    EOF
    ```

    <span data-ttu-id="ee224-178">In diesem Beispiel wird nur eine einfache Möglichkeit zum Erstellen der Datei vorgestellt.</span><span class="sxs-lookup"><span data-stu-id="ee224-178">This example is just an easy way for you to create the file.</span></span> <span data-ttu-id="ee224-179">In der Praxis würden Sie Ihren bevorzugten Code-Editor für die Erstellung verwenden.</span><span class="sxs-lookup"><span data-stu-id="ee224-179">In practice, you would use your favorite code editor to create it.</span></span>

    <span data-ttu-id="ee224-180">Geben Sie die Dockerfile in der Konsole aus.</span><span class="sxs-lookup"><span data-stu-id="ee224-180">Print your Dockerfile to the console.</span></span>

    ```bash
    cat Dockerfile
    ```

    <span data-ttu-id="ee224-181">Sie sehen Folgendes.</span><span class="sxs-lookup"><span data-stu-id="ee224-181">You see this.</span></span>

    ```output
    FROM python
    
    WORKDIR ./app
    
    RUN echo 'print("Hello World!")' > hello.py
    
    CMD python hello.py
    ```

    <span data-ttu-id="ee224-182">Im Folgenden finden Sie einen Überblick über die Funktionen einer Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="ee224-182">Let's break down what the Dockerfile does.</span></span>

    * <span data-ttu-id="ee224-183">`FROM` gibt das übergeordnete Image an, auf dem dieses Image basieren soll.</span><span class="sxs-lookup"><span data-stu-id="ee224-183">`FROM` specifies the parent image to base this image on.</span></span> <span data-ttu-id="ee224-184">In diesem Fall ist **python** das übergeordnete Image.</span><span class="sxs-lookup"><span data-stu-id="ee224-184">Here, the parent image is **python**.</span></span>
    * <span data-ttu-id="ee224-185">`WORKDIR` gibt das Arbeitsverzeichnis für alle `RUN`- und `CMD`-Anweisungen an, die später in der Dockerfile angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="ee224-185">`WORKDIR` specifies the working directory for any `RUN` and `CMD` statements that appear later in the Dockerfile.</span></span> <span data-ttu-id="ee224-186">Docker erstellt dieses Verzeichnis für Sie, in diesem Fall `./app`.</span><span class="sxs-lookup"><span data-stu-id="ee224-186">Docker creates this directory for you, in this case, `./app`.</span></span>
    * <span data-ttu-id="ee224-187">`RUN` gibt einen Befehl an, der im Container ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="ee224-187">`RUN` specifies a command to run in the container.</span></span> <span data-ttu-id="ee224-188">Sie können `RUN` zum Installieren von Software, zum Durchführen von Konfigurationsänderungen und zum Bereinigen des Containers vor der Erfassung verwenden.</span><span class="sxs-lookup"><span data-stu-id="ee224-188">You can use `RUN` to install software, make configuration changes, and cleanup the container before it's captured.</span></span> <span data-ttu-id="ee224-189">In dieser Einheit schreiben wir ein einfaches Python-Programm unter `./app/hello.py`.</span><span class="sxs-lookup"><span data-stu-id="ee224-189">Here, we write a basic Python program to `./app/hello.py`.</span></span>
    * <span data-ttu-id="ee224-190">`CMD` gibt den Prozess an, der beim Start des Containers ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="ee224-190">`CMD` specifies the process to run when the container starts.</span></span> <span data-ttu-id="ee224-191">In diesem Fall wird `python hello.py` über das Verzeichnis `/.app` ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="ee224-191">Here, we run `python hello.py` from the `/.app` directory.</span></span>

    <span data-ttu-id="ee224-192">Sie haben wahrscheinlich bemerkt, dass diese Schritte nahezu identisch mit denen sind, die Sie zum manuellen Erstellen des Images durchgeführt haben.</span><span class="sxs-lookup"><span data-stu-id="ee224-192">You've probably noticed that these are nearly the exact same steps you took to build the image manually.</span></span> <span data-ttu-id="ee224-193">Indem Sie diese Schritte in Form von Code ausdrücken, kann der Prozess einfacher freigegeben und wiederholt werden.</span><span class="sxs-lookup"><span data-stu-id="ee224-193">Expressing these steps as code makes the process easier to share and repeat.</span></span>

1. <span data-ttu-id="ee224-194">Führen Sie `docker build` aus, um das Image mithilfe der Anweisungen zu erstellen, die in der Dockerfile enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="ee224-194">Run `docker build` to create the image, using the instructions specified in the Dockerfile.</span></span>

    ```bash
    docker build -t python-dockerfile .
    ```

    <span data-ttu-id="ee224-195">Es dauert in der Regel nur wenige Sekunden, bis Docker Ihr Image erstellt hat.</span><span class="sxs-lookup"><span data-stu-id="ee224-195">It will typically take only a few seconds for Docker to build your image.</span></span>

    <span data-ttu-id="ee224-196">Ihnen sollte eine Ausgabe wie die folgende angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="ee224-196">You see output like the following.</span></span>

    ```output
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

1. <span data-ttu-id="ee224-197">Verwenden Sie `docker images`, um Ihre Images aufzuführen.</span><span class="sxs-lookup"><span data-stu-id="ee224-197">Use the `docker images` to list your images.</span></span>

    ```bash
    docker images
    ```

    <span data-ttu-id="ee224-198">Sie sehen das Image **python-dockerfile**, das Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="ee224-198">You see the **python-dockerfile** image you just built.</span></span>

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    python-dockerfile   latest              8ed5f85c5e5b        24 seconds ago      923MB
    python-custom       latest              6789cbe2cceb        4 minutes ago       923MB
    python              latest              a9d071760c82        2 weeks ago         923MB
    ```

1. <span data-ttu-id="ee224-199">Verwenden Sie `docker run`, um Ihren Container zu testen.</span><span class="sxs-lookup"><span data-stu-id="ee224-199">Use `docker run` to test out your container.</span></span>

    ```bash
    docker run python-dockerfile
    ```

    <span data-ttu-id="ee224-200">Sie sehen Folgendes.</span><span class="sxs-lookup"><span data-stu-id="ee224-200">You see this.</span></span>

    ```output
    Hello World!
    ```

    <span data-ttu-id="ee224-201">Im Gegensatz zum Testen eines manuell erstellten Images geben Sie hier nicht den Befehl an, der ausgeführt werden soll (`python app/hello.py`).</span><span class="sxs-lookup"><span data-stu-id="ee224-201">Unlike when you tested the image you created manually, here you don't specify the command to run, `python app/hello.py`.</span></span> <span data-ttu-id="ee224-202">Dieser ist in Ihrer Dockerfile enthalten, der Befehl ist also im Image integriert.</span><span class="sxs-lookup"><span data-stu-id="ee224-202">Your Dockerfile specifies that, so the command is built into the image.</span></span>

## <a name="publish-your-image-to-docker-hub"></a><span data-ttu-id="ee224-203">Veröffentlichen Ihres Images auf Docker Hub</span><span class="sxs-lookup"><span data-stu-id="ee224-203">Publish your image to Docker Hub</span></span>

<span data-ttu-id="ee224-204">Sie benötigen ein Konto, um ein Image auf Docker Hub zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="ee224-204">To publish an image to Docker Hub, you need an account.</span></span> <span data-ttu-id="ee224-205">In diesem Abschnitt richten Sie ein Docker Hub-Konto ein und veröffentlichen das Image **python-dockerfile** auf Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="ee224-205">Here you'll set up your Docker Hub account and publish your **python-dockerfile** image to Docker Hub.</span></span>

1. <span data-ttu-id="ee224-206">[Erstellen Sie ein Docker Hub-Konto](https://hub.docker.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="ee224-206">[Create your Docker Hub account](https://hub.docker.com?azure-portal=true).</span></span>

1. <span data-ttu-id="ee224-207">Exportieren Sie den Docker Hub-Kontonamen als Umgebungsvariable.</span><span class="sxs-lookup"><span data-stu-id="ee224-207">Export your Docker Hub account name as an environment variable.</span></span> <span data-ttu-id="ee224-208">Ersetzen Sie **account-name** durch den Namen Ihres Kontos.</span><span class="sxs-lookup"><span data-stu-id="ee224-208">Replace **account-name** with your account name.</span></span>

    ```bash
    export docker_account=account-name
    ```

    <span data-ttu-id="ee224-209">Diese Umgebungsvariable erleichtert das Ausführen der folgenden Befehle.</span><span class="sxs-lookup"><span data-stu-id="ee224-209">This environment variable will make it easier for you to run the commands that follow.</span></span>

1. <span data-ttu-id="ee224-210">Führen Sie `docker tag` aus, um das Image mit Ihrem Docker Hub-Kontonamen zu versehen.</span><span class="sxs-lookup"><span data-stu-id="ee224-210">Run `docker tag` to tag your image with your Docker Hub account name.</span></span>

    ```bash
    docker tag python-dockerfile $docker_account/python-dockerfile
    ```

1. <span data-ttu-id="ee224-211">Führen Sie `docker login` aus, um sich bei Docker Hub anzumelden.</span><span class="sxs-lookup"><span data-stu-id="ee224-211">Run `docker login` to log in to Docker Hub.</span></span>

    ```bash
    docker login
    ```

    <span data-ttu-id="ee224-212">Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="ee224-212">When prompted, enter your username and password.</span></span>

1. <span data-ttu-id="ee224-213">Führen Sie `docker push` aus, um das Image **python-dockerfile** in Docker Hub hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="ee224-213">Run `docker push` to push, or upload, your **python-dockerfile** image to Docker Hub.</span></span>

    ```bash
    docker push $docker_account/python-dockerfile
    ```

    <span data-ttu-id="ee224-214">Ihnen wird daraufhin eine Ausgabe angezeigt, die in etwa wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="ee224-214">You see output similar to the following:</span></span>

    ```output
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
    latest: digest: sha256:b816c32382d06ac74530d56f2a7b83000c86174218f430c6bb5039fdcfba38aa size: 2631
    ```

    <span data-ttu-id="ee224-215">Ihr Docker-Image ist nun in Docker Hub gespeichert.</span><span class="sxs-lookup"><span data-stu-id="ee224-215">Your Docker image is now stored in Docker Hub.</span></span> <span data-ttu-id="ee224-216">Sie können `docker pull` oder `docker run` von einem anderen Computer aus verwenden, um Ihr Image herunterzuladen oder über Docker Hub auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ee224-216">You can use `docker pull` or `docker run` from another computer to download or run your image from Docker Hub.</span></span> <span data-ttu-id="ee224-217">Hier sind zwei Beispiele:</span><span class="sxs-lookup"><span data-stu-id="ee224-217">Here are two examples:</span></span>

    1. <span data-ttu-id="ee224-218">In diesem Beispiel wird das aktuelle Image von Docker Hub heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="ee224-218">This example pulls the latest image from Docker Hub.</span></span>

        ```bash
        docker pull $docker_account/python-dockerfile
        ```

    1. <span data-ttu-id="ee224-219">In diesem Beispiel wird der Container ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="ee224-219">This example runs the container.</span></span>

        ```bash
        docker run $docker_account/python-dockerfile
        ```

1. <span data-ttu-id="ee224-220">Testen Sie Ihren Container.</span><span class="sxs-lookup"><span data-stu-id="ee224-220">Test out your container.</span></span>

    <span data-ttu-id="ee224-221">Navigieren Sie zu [Ihrem Docker Hub-Konto](https://hub.docker.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="ee224-221">Navigate to [your Docker Hub account](https://hub.docker.com?azure-portal=true).</span></span> <span data-ttu-id="ee224-222">Ihr Docker-Image wird auf der Registerkarte **Repositories** (Repositorys) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ee224-222">From the **Repositories** tab, you see your Docker image.</span></span>

    ![Das Docker-Image auf Docker Hub](../media/4-docker-hub-python-dockerfile.png)
