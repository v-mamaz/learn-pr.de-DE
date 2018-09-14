<span data-ttu-id="5a9e1-101">Da Container in Azure Container Instances sehr schnell und bequem bereitgestellt werden können, ist dies eine ideale Plattform zum Ausführen von einmaligen Aufgaben, wie dem Erstellen, Testen und Rendern von Images in einer Containerinstanz.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-101">The ease and speed of deploying containers in Azure Container Instances provides a compelling platform for executing run-once tasks like build, test, and image rendering in a container instance.</span></span>

<span data-ttu-id="5a9e1-102">Mit einer konfigurierbaren Neustartrichtlinie können Sie angeben, dass Container nach dem Abschluss ihrer Prozesse beendet werden.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-102">With a configurable restart policy, you can specify that your containers are stopped when their processes have completed.</span></span> <span data-ttu-id="5a9e1-103">Da Containerinstanzen nach Sekunden abgerechnet werden, fallen nur Gebühren für die Computerressourcen an, die beim Ausführen des Containers verwendet werden, der Ihre Aufgabe ausführt.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-103">Because container instances are billed by the second, you're charged only for the compute resources used while the container executing your task is running.</span></span>

## <a name="container-restart-policies"></a><span data-ttu-id="5a9e1-104">Neustartrichtlinien für Container</span><span class="sxs-lookup"><span data-stu-id="5a9e1-104">Container restart policies</span></span>

<span data-ttu-id="5a9e1-105">Wenn Sie in Azure Container Instances einen Container erstellen, können Sie eine von drei Einstellungen für Neustartrichtlinien festlegen:</span><span class="sxs-lookup"><span data-stu-id="5a9e1-105">When you create a container in Azure Container Instances, you can specify one of three restart policy settings:</span></span>

| <span data-ttu-id="5a9e1-106">Neustartrichtlinie</span><span class="sxs-lookup"><span data-stu-id="5a9e1-106">Restart policy</span></span>   | <span data-ttu-id="5a9e1-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="5a9e1-107">Description</span></span> |
| ---------------- | :---------- |
| `Always` | <span data-ttu-id="5a9e1-108">Container in der Containergruppe werden immer neu gestartet.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-108">Containers in the container group are always restarted.</span></span> <span data-ttu-id="5a9e1-109">Dies ist die **Standardeinstellung**, wenn beim Erstellen des Containers keine Neustartrichtlinie angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-109">This is the **default** setting applied when no restart policy is specified at container creation.</span></span> |
| `Never` | <span data-ttu-id="5a9e1-110">Container in der Containergruppe werden nie neu gestartet.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-110">Containers in the container group are never restarted.</span></span> <span data-ttu-id="5a9e1-111">Die Container werden höchstens einmal ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-111">The containers run at most once.</span></span> |
| `OnFailure` | <span data-ttu-id="5a9e1-112">Container in der Containergruppe werden nur dann neu gestartet, wenn bei dem im Container ausgeführten Prozess ein Fehler auftritt (wenn er also mit einem Exitcode ungleich 0 beendet wird).</span><span class="sxs-lookup"><span data-stu-id="5a9e1-112">Containers in the container group are restarted only when the process executed in the container fails (when it terminates with a nonzero exit code).</span></span> <span data-ttu-id="5a9e1-113">Die Container werden mindestens einmal ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-113">The containers are run at least once.</span></span> |

<span data-ttu-id="5a9e1-114">In der vorherigen Einheit dieses Moduls wurde ein Container ohne Angabe einer Neustartrichtlinie erstellt.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-114">In the previous unit of this module, a container was created without a specified restart policy.</span></span> <span data-ttu-id="5a9e1-115">Die Standardeinstellung der Neustartrichtlinie für diesen Container lautete *Always*.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-115">By default, this container received the *Always* restart policy.</span></span> <span data-ttu-id="5a9e1-116">Diese Richtlinie ist sinnvoll, da die Arbeitsauslastung im Container eine lange Ausführungsdauer aufweist (ein Webserver).</span><span class="sxs-lookup"><span data-stu-id="5a9e1-116">Because the workload in the container is long running (a web server), this policy makes sense.</span></span>

## <a name="run-to-completion"></a><span data-ttu-id="5a9e1-117">Ausführen bis zum Abschluss</span><span class="sxs-lookup"><span data-stu-id="5a9e1-117">Run to completion</span></span>

<span data-ttu-id="5a9e1-118">Wenn Sie die Richtlinie für den Neustart in der Praxis sehen möchten, erstellen Sie eine Containerinstanz aus dem Image *microsoft/aci-wordcount*, und geben Sie die Neustartrichtlinie *OnFailure* an.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-118">To see the restart policy in action, create a container instance from the *microsoft/aci-wordcount* image and specify the *OnFailure* restart policy.</span></span> <span data-ttu-id="5a9e1-119">Bei diesem Beispielcontainer wird ein Python-Skript ausgeführt, das den Text von Shakespeares „Hamlet“ analysiert, die zehn häufigsten Wörter in STDOUT schreibt und dann beendet wird.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-119">This example container runs a Python script that analyzes the text of Shakespeare's Hamlet, writes the 10 most common words to STDOUT, and then exits.</span></span>

<span data-ttu-id="5a9e1-120">Führen Sie den Beispielcontainer mit dem folgenden `az container create`-Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="5a9e1-120">Run the example container with the following `az container create` command:</span></span>

```azureclu
az container create \
    --resource-group myResourceGroup \
    --name mycontainer-restart-demo \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure
```

<span data-ttu-id="5a9e1-121">Azure Container Instances startet den Container und beendet ihn, wenn die Anwendung (oder wie in diesem Fall das Skript) beendet wird.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-121">Azure Container Instances starts the container and then stops it when its application (or script, in this case) exits.</span></span> <span data-ttu-id="5a9e1-122">Wenn Azure Container Instances einen Container beendet, dessen Neustartrichtlinie *Never* oder *OnFailure* lautet, wird der Status des Containers auf **Beendet** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-122">When Azure Container Instances stops a container whose restart policy is *Never* or *OnFailure*, the container's status is set to **Terminated**.</span></span>

<span data-ttu-id="5a9e1-123">Sie können den Status des Containers mit dem Befehl `az container show` überprüfen:</span><span class="sxs-lookup"><span data-stu-id="5a9e1-123">You can check a container's status with the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group myResourceGroup \
    --name mycontainer-restart-demo \
    --query containers[0].instanceView.currentState.state
```

<span data-ttu-id="5a9e1-124">Sobald der Status des Beispielcontainers **Beendet** lautet, können Sie die Taskausgabe in den Containerprotokollen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-124">Once the example container's status shows **Terminated**, you can see its task output by viewing the container logs.</span></span> <span data-ttu-id="5a9e1-125">Führen Sie den Befehl **az container logs** aus, um die Ausgabe des Skripts anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="5a9e1-125">Run the **az container logs** command to view the script's output:</span></span>

```azurecli
az container logs --resource-group myResourceGroup --name mycontainer-restart-demo
```

<span data-ttu-id="5a9e1-126">Ausgabe:</span><span class="sxs-lookup"><span data-stu-id="5a9e1-126">Output:</span></span>

```bash
[('the', 990),
 ('and', 702),
 ('of', 628),
 ('to', 610),
 ('I', 544),
 ('you', 495),
 ('a', 453),
 ('my', 441),
 ('in', 399),
 ('HAMLET', 386)]
```

## <a name="summary"></a><span data-ttu-id="5a9e1-127">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="5a9e1-127">Summary</span></span>

<span data-ttu-id="5a9e1-128">In dieser Einheit haben Sie eine Containerinstanz mit der Neustartrichtlinie *OnFailure* erstellt.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-128">In this unit, you created a container instance with a restart policy of *OnFailure*.</span></span> <span data-ttu-id="5a9e1-129">Diese Konfiguration eignet sich für Container mit kurzlebigen Aufgaben.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-129">This configuration works well for containers that run short-lived tasks.</span></span>

<span data-ttu-id="5a9e1-130">In der nächsten Einheit erfahren Sie, wie Umgebungsvariablen in Azure Container Instances festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="5a9e1-130">In the next unit, you will set environment variables in Azure Container Instances.</span></span>
