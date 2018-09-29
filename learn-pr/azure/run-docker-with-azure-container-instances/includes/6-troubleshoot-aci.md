<span data-ttu-id="270b9-101">Im Folgenden führen Sie einige grundlegende Problembehandlungsvorgänge durch, z.B. das Abrufen von Containerprotokollen und Containerereignissen sowie das Anfügen dieser an eine Containerinstanz.</span><span class="sxs-lookup"><span data-stu-id="270b9-101">Here, you will perform some basic troubleshooting operations such as pulling container logs, container events, and attaching to a container instance.</span></span> <span data-ttu-id="270b9-102">Nach Abschluss dieses Moduls sollten Sie mit den grundlegenden Funktionen für die Problembehandlung bei Containerinstanzen vertraut sein.</span><span class="sxs-lookup"><span data-stu-id="270b9-102">By the end of this module, you should understand basic capabilities for troubleshooting container instances.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="270b9-103">Erstellen eines Containers</span><span class="sxs-lookup"><span data-stu-id="270b9-103">Create a container</span></span>

<span data-ttu-id="270b9-104">Beginnen Sie mit der Erstellung des folgenden Containers:</span><span class="sxs-lookup"><span data-stu-id="270b9-104">Start by creating the following container:</span></span> 

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --image microsoft/sample-aks-helloworld \
    --ports 80 \
    --ip-address Public \
    --location eastus
```

## <a name="get-logs-from-a-container-instance"></a><span data-ttu-id="270b9-105">Abrufen von Protokollen aus einer Containerinstanz</span><span class="sxs-lookup"><span data-stu-id="270b9-105">Get logs from a container instance</span></span>

<span data-ttu-id="270b9-106">Sie können den Befehl `az container logs` verwenden, um Protokolle aus Ihrem Anwendungscode in einem Container anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="270b9-106">To view logs from your application code within a container, you can use the `az container logs` command:</span></span>

```azurecli
az container logs \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer
```

<span data-ttu-id="270b9-107">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="270b9-107">Example output:</span></span>

```output
Checking for script in /app/prestart.sh
Running script /app/prestart.sh
Running inside /app/prestart.sh, you could add migrations to this file, e.g.:

#! /usr/bin/env bash

# Let the DB start
sleep 10;
# Run migrations
alembic upgrade head
```

## <a name="get-container-events"></a><span data-ttu-id="270b9-108">Abrufen von Containerereignissen</span><span class="sxs-lookup"><span data-stu-id="270b9-108">Get container events</span></span>

<span data-ttu-id="270b9-109">Der Befehl `az container attach` stellt während des Startvorgangs des Containers Diagnoseinformationen bereit.</span><span class="sxs-lookup"><span data-stu-id="270b9-109">The `az container attach` command provides diagnostic information during container startup.</span></span> <span data-ttu-id="270b9-110">Nachdem der Container gestartet wurde, werden auch STDOUT und STDERR auf Ihre lokale Konsole gestreamt:</span><span class="sxs-lookup"><span data-stu-id="270b9-110">Once the container has started, it also streams STDOUT and STDERR to your local console:</span></span>

```azurecli
az container attach \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer
```

<span data-ttu-id="270b9-111">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="270b9-111">Example output:</span></span>

```output
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-09-21 23:48:14+00:00) pulling image "microsoft/sample-aks-helloworld"
(count: 1) (last timestamp: 2018-09-21 23:49:09+00:00) Successfully pulled image "microsoft/sample-aks-helloworld"
(count: 1) (last timestamp: 2018-09-21 23:49:12+00:00) Created container
(count: 1) (last timestamp: 2018-09-21 23:49:13+00:00) Started container

Start streaming logs:
Checking for script in /app/prestart.sh
Running script /app/prestart.sh
```

> [!TIP]
> <span data-ttu-id="270b9-112">Drücken Sie zum Trennen der Verbindung mit einem angefügten Container <kbd>STRG+C</kbd>.</span><span class="sxs-lookup"><span data-stu-id="270b9-112">To disconnect from an attached container, press <kbd>Ctrl+C</kbd>.</span></span>

## <a name="execute-a-command-in-a-container"></a><span data-ttu-id="270b9-113">Ausführen eines Befehls in einem Container</span><span class="sxs-lookup"><span data-stu-id="270b9-113">Execute a command in a container</span></span>

<span data-ttu-id="270b9-114">Azure Container Instances unterstützt die Ausführung eines Befehls in einem ausgeführten Container.</span><span class="sxs-lookup"><span data-stu-id="270b9-114">Azure Container Instances supports executing a command in a running container.</span></span> <span data-ttu-id="270b9-115">Die Ausführung eines Befehls in einem bereits gestarteten Container ist besonders bei der Anwendungsentwicklung und Problembehandlung von großem Nutzen.</span><span class="sxs-lookup"><span data-stu-id="270b9-115">Running a command in a container you've already started is especially helpful during application development and troubleshooting.</span></span> <span data-ttu-id="270b9-116">Am häufigsten wird dieses Feature zum Starten einer interaktiven Shell zum Debuggen von Problemen in einem ausgeführten Container verwendet.</span><span class="sxs-lookup"><span data-stu-id="270b9-116">The most common use of this feature is to launch an interactive shell so that you can debug issues in a running container.</span></span>

<span data-ttu-id="270b9-117">In diesem Beispiel wird eine interaktive Terminalsitzung mit dem ausgeführten Container gestartet:</span><span class="sxs-lookup"><span data-stu-id="270b9-117">This example starts an interactive terminal session with the running container:</span></span>

```azurecli
az container exec \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --exec-command /bin/sh
```

<span data-ttu-id="270b9-118">Sobald der Befehl ausgeführt wurde, arbeiten Sie effektiv innerhalb des Containers.</span><span class="sxs-lookup"><span data-stu-id="270b9-118">Once the command has completed, you are effectively working inside of the container.</span></span> <span data-ttu-id="270b9-119">In diesem Beispiel wurde der `ls`-Befehl ausgeführt, um den Inhalt des Arbeitsverzeichnisses anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="270b9-119">In this example, the `ls` command was run to display the contents of the working directory:</span></span>

```output
# ls
__pycache__  main.py  prestart.sh  static  templates  uwsgi.ini
```

<span data-ttu-id="270b9-120">Führen Sie `exit` aus, um die Remotesitzung zu beenden.</span><span class="sxs-lookup"><span data-stu-id="270b9-120">Run `exit` to stop the remote session.</span></span>

## <a name="monitor-container-cpu-and-memory"></a><span data-ttu-id="270b9-121">Überwachen von Container-CPU und -speicher</span><span class="sxs-lookup"><span data-stu-id="270b9-121">Monitor container CPU and memory</span></span>

<span data-ttu-id="270b9-122">Sie sollten die Metriken zur CPU- und Speicherauslastung abrufen.</span><span class="sxs-lookup"><span data-stu-id="270b9-122">You may want to pull metrics on CPU and memory usage.</span></span> <span data-ttu-id="270b9-123">Zu diesem Zweck müssen Sie zuerst die ID der Azure-Containerinstanz abrufen.</span><span class="sxs-lookup"><span data-stu-id="270b9-123">To do so, first get the ID of the Azure container instance.</span></span> <span data-ttu-id="270b9-124">In diesem Beispiel wird die ID in einer Variable namens `CONTAINER_ID` platziert:</span><span class="sxs-lookup"><span data-stu-id="270b9-124">In this example, the ID is placed in a variable named `CONTAINER_ID`:</span></span>

```azurecli
CONTAINER_ID=$(az container show --resource-group <rgn>[sandbox resource group name]</rgn> --name mycontainer --query id --output tsv)
```

<span data-ttu-id="270b9-125">Verwenden Sie nun den `az monitor metrics list`-Befehl, um die Informationen zur CPU-Auslastung abzurufen:</span><span class="sxs-lookup"><span data-stu-id="270b9-125">Now, use the `az monitor metrics list` command to pull back CPU usage information:</span></span>

```azurecli
az monitor metrics list \
    --resource $CONTAINER_ID \
    --metric CPUUsage \
    --output table
```

<span data-ttu-id="270b9-126">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="270b9-126">Example output:</span></span>

```output
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

<span data-ttu-id="270b9-127">Der folgende Befehl kann zum Abrufen der Informationen zur Speicherauslastung verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="270b9-127">The following command can be used to get memory usage information:</span></span>

```azurecli
az monitor metrics list \
    --resource $CONTAINER_ID \
    --metric MemoryUsage \
    --output table
```

<span data-ttu-id="270b9-128">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="270b9-128">Example output:</span></span>

```output
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

<span data-ttu-id="270b9-129">Diese Informationen stehen Ihnen auch im Azure-Portal zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="270b9-129">This information is also available in the Azure portal.</span></span> <span data-ttu-id="270b9-130">Öffnen Sie im Azure-Portal die Übersichtsseite einer Containerinstanz, um eine visuelle Darstellung der Informationen zur CPU- und Speicherauslastung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="270b9-130">To see a visual representation of CPU and memory usage information, visit the Azure portal overview page for a container instance.</span></span>

![Ansicht der Informationen zur CPU- und Speicherauslastung von Azure Container Instances im Azure-Portal](../media/6-cpu-memory.png)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
