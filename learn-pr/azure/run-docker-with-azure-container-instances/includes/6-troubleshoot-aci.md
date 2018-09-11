<span data-ttu-id="6e618-101">In dieser Einheit führen Sie einige grundlegende Problembehandlungsvorgänge durch, z.B. das Abrufen von Containerprotokollen und Containerereignissen sowie das Anfügen dieser an eine Containerinstanz.</span><span class="sxs-lookup"><span data-stu-id="6e618-101">In this unit, you will perform some basic troubleshooting operations such as pulling container logs, container events, and attaching to a container instance.</span></span> <span data-ttu-id="6e618-102">Nach Abschluss dieses Moduls sollten Sie mit den grundlegenden Funktionen für die Problembehandlung von Containerinstanzen vertraut sein.</span><span class="sxs-lookup"><span data-stu-id="6e618-102">By the end of this module, you should understand basic capabilities for troubleshooting container instances.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="6e618-103">Erstellen eines Containers</span><span class="sxs-lookup"><span data-stu-id="6e618-103">Create a container</span></span>

<span data-ttu-id="6e618-104">Erstellen Sie zunächst einen Container, den Sie für diese Einheit verwenden.</span><span class="sxs-lookup"><span data-stu-id="6e618-104">Start by creating a container to use in this unit.</span></span> <span data-ttu-id="6e618-105">Sie können diesen Schritt überspringen, wenn Sie noch über den ersten Container verfügen, den Sie im Rahmen dieses Moduls erstellt haben:</span><span class="sxs-lookup"><span data-stu-id="6e618-105">If you still have the first container created in this module, skip this step:</span></span>

```azurecli
az container create --resource-group myResourceGroup --name mycontainer --image microsoft/aci-helloworld --ports 80 --ip-address Public
```

## <a name="get-logs-from-a-container-instance"></a><span data-ttu-id="6e618-106">Abrufen von Protokollen aus einer Containerinstanz</span><span class="sxs-lookup"><span data-stu-id="6e618-106">Get logs from a container instance</span></span>

<span data-ttu-id="6e618-107">Die können den Befehl `az container logs` verwenden, um Protokolle aus Ihrem Anwendungscode in einem Container anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="6e618-107">To view logs from your application code within a container, you can use the `az container logs` command:</span></span>

```azazurecli
az container logs --resource-group myResourceGroup --name mycontainer
```

<span data-ttu-id="6e618-108">Es folgt die Protokollausgabe des Beispielcontainers, nachdem mehrmals auf eine Web-App zugegriffen wurde:</span><span class="sxs-lookup"><span data-stu-id="6e618-108">The following is log output from the example container after the web app has been accessed a few times:</span></span>

```bash
listening on port 80
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:24 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:24 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://23.101.136.193/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:25 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:27 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
```

## <a name="get-container-events"></a><span data-ttu-id="6e618-109">Abrufen von Containerereignissen</span><span class="sxs-lookup"><span data-stu-id="6e618-109">Get container events</span></span>

<span data-ttu-id="6e618-110">Der Befehl `az container attach` stellt während des Startvorgangs des Containers Diagnoseinformationen bereit.</span><span class="sxs-lookup"><span data-stu-id="6e618-110">The `az container attach` command provides diagnostic information during container startup.</span></span> <span data-ttu-id="6e618-111">Nachdem der Container gestartet wurde, werden auch STDOUT und STDERR auf Ihre lokale Konsole gestreamt:</span><span class="sxs-lookup"><span data-stu-id="6e618-111">Once the container has started, it also streams STDOUT and STDERR to your local console:</span></span>

```azazurecli
az container attach --resource-group myResourceGroup --name mycontainer
```

<span data-ttu-id="6e618-112">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="6e618-112">Example output:</span></span>


```bash
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-08-20 21:43:26+00:00) pulling image "microsoft/aci-helloworld"
(count: 1) (last timestamp: 2018-08-20 21:43:32+00:00) Successfully pulled image "microsoft/aci-helloworld"
(count: 1) (last timestamp: 2018-08-20 21:43:33+00:00) Created container
(count: 1) (last timestamp: 2018-08-20 21:43:33+00:00) Started container

Start streaming logs:
listening on port 80
listening on port 80
```

## <a name="execute-a-command-in-a-container"></a><span data-ttu-id="6e618-113">Ausführen eines Befehls in einem Container</span><span class="sxs-lookup"><span data-stu-id="6e618-113">Execute a command in a container</span></span>

<span data-ttu-id="6e618-114">Azure Container Instances unterstützt die Ausführung eines Befehls in einem ausgeführten Container.</span><span class="sxs-lookup"><span data-stu-id="6e618-114">Azure Container Instances supports executing a command in a running container.</span></span> <span data-ttu-id="6e618-115">Die Ausführung eines Befehls in einem bereits gestarteten Container ist besonders bei der Anwendungsentwicklung und Problembehandlung von großem Nutzen.</span><span class="sxs-lookup"><span data-stu-id="6e618-115">Running a command in a container you've already started is especially helpful during application development and troubleshooting.</span></span> <span data-ttu-id="6e618-116">Am häufigsten wird dieses Feature zum Starten einer interaktiven Befehlsshell verwendet, sodass Probleme in einem ausgeführten Container behoben werden können.</span><span class="sxs-lookup"><span data-stu-id="6e618-116">The most common use of this feature is to launch an interactive shell, so that you can debug issues in a running container.</span></span>

<span data-ttu-id="6e618-117">In diesem Beispiel wird eine interaktive Terminalsitzung mit dem ausgeführten Container gestartet:</span><span class="sxs-lookup"><span data-stu-id="6e618-117">This example starts an interactive terminal session with the running container:</span></span>

```azurecli
az container exec --resource-group myResourceGroup --name mycontainer --exec-command /bin/sh
```

<span data-ttu-id="6e618-118">Sobald der Befehl abgeschlossen ist, arbeiten Sie effektiv innerhalb des Containers.</span><span class="sxs-lookup"><span data-stu-id="6e618-118">Once the command has completed, you are effectively working inside of the container.</span></span> <span data-ttu-id="6e618-119">In diesem Beispiel wurde der `ls`-Befehl ausgeführt, um den Inhalt des Arbeitsverzeichnisses anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="6e618-119">In this example, the `ls` command was run to display the contents of the working directory:</span></span>

```bash
usr/src/app # ls
index.html         node_modules       package.json
index.js           package-lock.json
```

<span data-ttu-id="6e618-120">Geben Sie `exit` ein, um die Remotesitzung zu beenden.</span><span class="sxs-lookup"><span data-stu-id="6e618-120">Enter `exit` to stop the remote session.</span></span>

## <a name="monitor-container-cpu-and-memory"></a><span data-ttu-id="6e618-121">Überwachen von Container-CPU und -Arbeitsspeicher</span><span class="sxs-lookup"><span data-stu-id="6e618-121">Monitor container CPU and memory</span></span>

<span data-ttu-id="6e618-122">Sie sollten die Metriken zur CPU- und Arbeitsspeicherauslastung abrufen.</span><span class="sxs-lookup"><span data-stu-id="6e618-122">You may want to pull metrics on CPU and memory usage.</span></span> <span data-ttu-id="6e618-123">Zu diesem Zweck müssen Sie zuerst die ID der Azure-Containerinstanz abrufen.</span><span class="sxs-lookup"><span data-stu-id="6e618-123">To do so, first get the ID of the Azure container instance.</span></span> <span data-ttu-id="6e618-124">In diesem Beispiel wird die ID in einer Variable namens `CONTAINER_ID` platziert:</span><span class="sxs-lookup"><span data-stu-id="6e618-124">In this example, the ID is placed in a variable named `CONTAINER_ID`:</span></span>

```azurecli
CONTAINER_ID=$(az container show --resource-group myResourceGroup --name mycontainer --query id --output tsv)
```

<span data-ttu-id="6e618-125">Verwenden Sie nun den `az monitor metrics list`-Befehl, um die Informationen zur CPU-Auslastung abzurufen:</span><span class="sxs-lookup"><span data-stu-id="6e618-125">Now, use the `az monitor metrics list` command to pull back CPU usage information:</span></span>

```azurecli
az monitor metrics list --resource $CONTAINER_ID --metric CPUUsage --output table
```

<span data-ttu-id="6e618-126">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="6e618-126">Example output:</span></span>

```bash
Timestamp            Name              Average
-------------------  ------------  -----------
2018-08-20 21:39:00  CPU Usage
2018-08-20 21:40:00  CPU Usage
2018-08-20 21:41:00  CPU Usage
2018-08-20 21:42:00  CPU Usage
2018-08-20 21:43:00  CPU Usage      0.375
2018-08-20 21:44:00  CPU Usage      0.875
2018-08-20 21:45:00  CPU Usage      1
2018-08-20 21:46:00  CPU Usage      3.625
2018-08-20 21:47:00  CPU Usage      1.5
2018-08-20 21:48:00  CPU Usage      2.75
2018-08-20 21:49:00  CPU Usage      1.625
2018-08-20 21:50:00  CPU Usage      0.625
2018-08-20 21:51:00  CPU Usage      0.5
2018-08-20 21:52:00  CPU Usage      0.5
2018-08-20 21:53:00  CPU Usage      0.5
```

<span data-ttu-id="6e618-127">Der folgende Befehl kann zum Abrufen der Informationen zur Arbeitsspeicherauslastung verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="6e618-127">The following command can be used to get memory usage information:</span></span>

```azurecli
az monitor metrics list --resource $CONTAINER_ID --metric MemoryUsage --output table
```

<span data-ttu-id="6e618-128">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="6e618-128">Example output:</span></span>

```bash
Timestamp            Name              Average
-------------------  ------------  -----------
2018-08-20 21:43:00  Memory Usage
2018-08-20 21:44:00  Memory Usage  0.0
2018-08-20 21:45:00  Memory Usage  15917056.0
2018-08-20 21:46:00  Memory Usage  16744448.0
2018-08-20 21:47:00  Memory Usage  16842752.0
2018-08-20 21:48:00  Memory Usage  17190912.0
2018-08-20 21:49:00  Memory Usage  17506304.0
2018-08-20 21:50:00  Memory Usage  17702912.0
2018-08-20 21:51:00  Memory Usage  17965056.0
2018-08-20 21:52:00  Memory Usage  18509824.0
2018-08-20 21:53:00  Memory Usage  18649088.0
2018-08-20 21:54:00  Memory Usage  18845696.0
2018-08-20 21:55:00  Memory Usage  19181568.0
```

<span data-ttu-id="6e618-129">Diese Informationen stehen Ihnen auch im Azure-Portal zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="6e618-129">This information is also available in the Azure portal.</span></span> <span data-ttu-id="6e618-130">Öffnen Sie im Azure-Portal die Übersichtsseite einer Containerinstanz, um eine grafische Darstellung der Informationen zur CPU- und Arbeitsspeicherauslastung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="6e618-130">To see graphical representation of CPU and memory usage information, visit the Azure portal overview page for a container instance.</span></span>

![Ansicht der Informationen zu der CPU- und Arbeitsspeicherauslastung von Azure Container Instances im Azure-Portal](../media-draft/cpu-memory.png)

## <a name="clean-up"></a><span data-ttu-id="6e618-132">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="6e618-132">Clean up</span></span>
<!---TODO: Do we need to include cleanup for the free education tier?--->

<span data-ttu-id="6e618-133">Dies ist die letzte Einheit des Azure Container Instances-Lernmoduls.</span><span class="sxs-lookup"><span data-stu-id="6e618-133">This is the last unit of the Azure Container Instances learning module.</span></span> <span data-ttu-id="6e618-134">Sie können nun die erstellten Ressourcen bereinigen, indem Sie die Ressourcengruppe löschen.</span><span class="sxs-lookup"><span data-stu-id="6e618-134">At this point, you can cleanup the created resources by deleting the resource group.</span></span> <span data-ttu-id="6e618-135">Verwenden Sie hierzu den Befehl **az group delete**:</span><span class="sxs-lookup"><span data-stu-id="6e618-135">To do so, use the **az group delete** command:</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a><span data-ttu-id="6e618-136">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="6e618-136">Summary</span></span>

<span data-ttu-id="6e618-137">In dieser Einheit haben Sie einige Problembehandlungsvorgänge kennengelernt, z.B. das Abrufen von Containerprotokollen und Containerereignissen sowie das Anfügen dieser an eine Containerinstanz.</span><span class="sxs-lookup"><span data-stu-id="6e618-137">In this unit, you learned about several troubleshooting operations such as pulling container logs, container events, and attaching to a container instance.</span></span>