<span data-ttu-id="dc3ac-101">In dieser Einheit erfahren Sie, wie Sie eine Azure-Funktions-App erstellen, die alle 20 Sekunden mithilfe eines Timertriggers aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-101">In this unit, we create an Azure function app that's invoked every 20 seconds using a timer trigger.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="dc3ac-102">Erstellen einer Azure-Funktions-App</span><span class="sxs-lookup"><span data-stu-id="dc3ac-102">Create an Azure function app</span></span>

<span data-ttu-id="dc3ac-103">Erstellen Sie zuerst eine Azure-Funktions-App im Portal.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-103">Let’s start by creating an Azure Function app in the portal.</span></span>

1. <span data-ttu-id="dc3ac-104">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-104">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="dc3ac-105">Wählen Sie im linken Navigationsbereich **Ressource erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="dc3ac-106">Wählen Sie **Compute** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-106">Select **Compute**.</span></span>

1. <span data-ttu-id="dc3ac-107">Wechseln Sie zu **Funktionen-App**.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-107">Locate and select **Function App**.</span></span> <span data-ttu-id="dc3ac-108">Sie können optional auch die Suchleiste verwenden, um die Vorlage zu finden.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Screenshot: Blatt „Ressource erstellen“ im Azure-Portal mit hervorgehobener Funktions-App.](../media/4-click-function-app.png)

1. <span data-ttu-id="dc3ac-110">Geben Sie einen global eindeutigen **App-Namen** ein.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-110">Enter a globally unique **App name**.</span></span>

1. <span data-ttu-id="dc3ac-111">Wählen Sie ein **Abonnement** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="dc3ac-112">Wählen Sie die vorhandene **Ressourcengruppe** <rgn>[Name der Sandboxressourcengruppe]</rgn> aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-112">Select the existing **Resource group** <rgn>[sandbox resource group name]</rgn>.</span></span>

1. <span data-ttu-id="dc3ac-113">Wählen Sie **Windows** als Ihr **Betriebssystem** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="dc3ac-114">Wählen Sie als **Hostingplan** die Option **Verbrauchstarif**.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="dc3ac-115">Jede Ausführung der Funktion wird Ihnen in Rechnung gestellt.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="dc3ac-116">Ressourcen werden basierend auf dem Workload Ihrer Anwendung automatisch zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="dc3ac-117">Wählen Sie einen **Standort** aus der unten verfügbaren Liste aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-117">Select a **Location** from the available list below.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="dc3ac-118">Erstellen Sie ein neues **Speicherkonto**. Sie können den Namen des Kontos ändern, wenn Sie möchten. Standardmäßig wird eine Variation des App-Namens ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-118">Create a new **Storage** account, you can change the name if you like - it will default to a variation of the App name.</span></span>

1. <span data-ttu-id="dc3ac-119">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-119">Select **Create**.</span></span> <span data-ttu-id="dc3ac-120">Sobald die Funktions-App bereitgestellt ist, wechseln Sie im Portal zu **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-120">Once the function app is deployed, go to **All resources** in the portal.</span></span> <span data-ttu-id="dc3ac-121">Die Funktions-App wird mit dem Typ **App Service** aufgelistet und hat den Namen, den Sie ihr gegeben haben.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-121">The function app will be listed with type **App Service** and has the name you gave it.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="dc3ac-122">Erstellen eines Timertriggers</span><span class="sxs-lookup"><span data-stu-id="dc3ac-122">Create a timer trigger</span></span>

<span data-ttu-id="dc3ac-123">Wir erstellen nun in unserer Funktion einen Timertrigger.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-123">Now we're going to create a timer trigger inside our function.</span></span>

1. <span data-ttu-id="dc3ac-124">Wenn die Funktion erstellt wurde, klicken Sie im linken Navigationsbereich auf **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-124">After the function is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="dc3ac-125">Suchen Sie in der Liste nach der Funktions-App, und wählen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-125">Find your function app in the list and select it.</span></span>

1. <span data-ttu-id="dc3ac-126">Zeigen Sie auf dem neuen Blatt auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).</span><span class="sxs-lookup"><span data-stu-id="dc3ac-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Screenshot: Blatt „Funktions-App“ im Azure-Portal mit hervorgehobenem Pluszeichen (+) im Untermenü „Funktionen“](../media/4-hover-function.png)

1. <span data-ttu-id="dc3ac-128">Klicken Sie auf **Zeitgeber**.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-128">Select **Timer**.</span></span>

1. <span data-ttu-id="dc3ac-129">Wählen Sie **CSharp** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-129">Select **CSharp** as the language.</span></span>

1. <span data-ttu-id="dc3ac-130">Wählen Sie **Diese Funktion erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="dc3ac-131">Konfigurieren des Timertriggers</span><span class="sxs-lookup"><span data-stu-id="dc3ac-131">Configure the timer trigger</span></span>

<span data-ttu-id="dc3ac-132">Wir verfügen über eine Azure-Funktions-App mit Logik zum Ausgeben einer Meldung im Protokollfenster.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-132">We have an Azure function app with logic to print a message to the log window.</span></span> <span data-ttu-id="dc3ac-133">Der Zeitplan des Timers wird so eingestellt, dass er alle 20 Sekunden ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="dc3ac-134">Wählen Sie **Integrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-134">Select **Integrate**.</span></span>

1. <span data-ttu-id="dc3ac-135">Geben Sie den folgenden Wert in das Feld **Zeitplan** ein:</span><span class="sxs-lookup"><span data-stu-id="dc3ac-135">Enter the following value into the **Schedule** box:</span></span>

    ```log
    */20 * * * * *
    ```

1. <span data-ttu-id="dc3ac-136">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-136">Select **Save**.</span></span>

## <a name="test-the-timer"></a><span data-ttu-id="dc3ac-137">Testen des Timers</span><span class="sxs-lookup"><span data-stu-id="dc3ac-137">Test the timer</span></span>

<span data-ttu-id="dc3ac-138">Nachdem Sie nun den Timer konfiguriert haben, ruft er die Funktion in dem von uns definierten Intervall auf.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-138">Now that we've configured the timer, it will invoke the function on the interval we defined.</span></span>

1. <span data-ttu-id="dc3ac-139">Wählen Sie **TimerTriggerCSharp1** aus.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-139">Select **TimerTriggerCSharp1**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc3ac-140">**TimerTriggerCSharp1** ist ein Standardname.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="dc3ac-141">Er wird beim Erstellen des Triggers automatisch generiert.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-141">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="dc3ac-142">Öffnen Sie unten in der Anzeige den Bereich **Protokolle**.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-142">Open the **Logs** panel at the bottom of the screen.</span></span>

1. <span data-ttu-id="dc3ac-143">Beobachten Sie, wie alle 20 Sekunden neue Meldungen im Protokollfenster eingehen.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-143">Observe new messages arrive every 20 seconds in the log window.</span></span>

1. <span data-ttu-id="dc3ac-144">Damit die Funktion nicht mehr länger ausgeführt wird, wählen Sie **Verwalten**, und ändern Sie dann den **Funktionszustand** in *Deaktiviert*.</span><span class="sxs-lookup"><span data-stu-id="dc3ac-144">To stop the function from running, select **Manage** and then switch **Function State** to *Disabled*.</span></span>
