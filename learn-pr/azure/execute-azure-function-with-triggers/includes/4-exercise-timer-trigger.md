<span data-ttu-id="c3380-101">In dieser Übung erstellen wir eine Azure-Funktion, die alle 20 Sekunden mithilfe eines Zeitgebertriggers aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="c3380-101">In this exercise, we create an Azure function that's invoked every 20 seconds using a timer trigger.</span></span>

> [!NOTE] 
> <span data-ttu-id="c3380-102">Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com/) mit einem gültigen Konto angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="c3380-102">To complete this exercise, make sure you're logged into the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="c3380-103">Erstellen einer Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="c3380-103">Create an Azure function</span></span>

<span data-ttu-id="c3380-104">Wir beginnen, indem wir eine Azure-Funktion im Portal erstellen.</span><span class="sxs-lookup"><span data-stu-id="c3380-104">Let’s start by creating an Azure function in the portal.</span></span>

1. <span data-ttu-id="c3380-105">Klicken Sie im linken Navigationsbereich auf **Ressourcengruppe erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c3380-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="c3380-106">Wählen Sie **Compute** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-106">Select **Compute**.</span></span>

1. <span data-ttu-id="c3380-107">Wechseln Sie zu **Funktionen-App**.</span><span class="sxs-lookup"><span data-stu-id="c3380-107">Locate and select **Function App**.</span></span> <span data-ttu-id="c3380-108">Sie können optional auch die Suchleiste verwenden, um die Vorlage zu finden.</span><span class="sxs-lookup"><span data-stu-id="c3380-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Auswählen von „Funktionen-App“](../media-drafts/4-click-function-app.png)

1. <span data-ttu-id="c3380-110">Geben Sie einen eindeutigen **App-Namen** ein.</span><span class="sxs-lookup"><span data-stu-id="c3380-110">Enter a unique **App name**.</span></span>

1. <span data-ttu-id="c3380-111">Wählen Sie ein **Abonnement** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="c3380-112">Erstellen Sie eine neue **Ressourcengruppe**.</span><span class="sxs-lookup"><span data-stu-id="c3380-112">Create a new **Resource Group**.</span></span>

1. <span data-ttu-id="c3380-113">Wählen Sie **Windows** als Ihr **Betriebssystem** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="c3380-114">Wählen Sie als **Hostingplan** die Option **Verbrauchstarif**.</span><span class="sxs-lookup"><span data-stu-id="c3380-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="c3380-115">Jede Ausführung der Funktion wird Ihnen in Rechnung gestellt.</span><span class="sxs-lookup"><span data-stu-id="c3380-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="c3380-116">Ressourcen werden basierend auf dem Workload Ihrer Anwendung automatisch zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="c3380-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="c3380-117">Wählen Sie einen **Speicherort** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-117">Select a **Location**.</span></span>

1. <span data-ttu-id="c3380-118">Erstellen Sie ein neues **Speicherkonto**.</span><span class="sxs-lookup"><span data-stu-id="c3380-118">Create a new **Storage** account.</span></span> <span data-ttu-id="c3380-119">(Dieser Wert ist erforderlich, wird aber hier nicht verwendet.)</span><span class="sxs-lookup"><span data-stu-id="c3380-119">(This value is required, but we're not going to use it.)</span></span>

1. <span data-ttu-id="c3380-120">Deaktivieren Sie **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="c3380-120">Turn off **Application Insights**.</span></span>

1. <span data-ttu-id="c3380-121">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-121">Select **Create**.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="c3380-122">Erstellen eines Zeitgebertriggers</span><span class="sxs-lookup"><span data-stu-id="c3380-122">Create a timer trigger</span></span>

<span data-ttu-id="c3380-123">Wir erstellen nun in unserer Azure-Funktion einen Zeitgebertrigger.</span><span class="sxs-lookup"><span data-stu-id="c3380-123">Now we're going to create a timer trigger inside our Azure function.</span></span>

1. <span data-ttu-id="c3380-124">Nachdem die Azure-Funktion erstellt wurde, wählen Sie im linken Navigationsbereich **Alle Ressourcen** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-124">After the Azure function is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="c3380-125">Wählen Sie Ihre Azure-Funktion aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-125">Locate and select your Azure function.</span></span>

1. <span data-ttu-id="c3380-126">Zeigen Sie auf dem neuen Blatt auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Auf „Funktionen“ zeigen und Pluszeichen auswählen](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="c3380-128">Wählen Sie **Zeitgeber** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-128">Select **Timer**.</span></span>

1. <span data-ttu-id="c3380-129">Wählen Sie **CSharp** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-129">Select **CSharp** as the language.</span></span>

1. <span data-ttu-id="c3380-130">Wählen Sie **Diese Funktion erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="c3380-131">Konfigurieren des Zeitgebertriggers</span><span class="sxs-lookup"><span data-stu-id="c3380-131">Configure the timer trigger</span></span>

<span data-ttu-id="c3380-132">Wir haben eine Azure-Funktion mit Logik zum Ausgeben einer Meldung im Protokollfenster.</span><span class="sxs-lookup"><span data-stu-id="c3380-132">We have an Azure function with logic to print a message to the log window.</span></span> <span data-ttu-id="c3380-133">Wir stellen den Zeitplan des Zeitgebers so ein, dass er alle 20 Sekunden ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="c3380-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="c3380-134">Wählen Sie **Integrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-134">Select **Integrate**.</span></span>

1. <span data-ttu-id="c3380-135">Geben Sie den folgenden Wert in das Feld **Zeitplan** ein:</span><span class="sxs-lookup"><span data-stu-id="c3380-135">Enter the following value into the **Schedule** box:</span></span>

    ```
    */20 * * * * *
    ```

1. <span data-ttu-id="c3380-136">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="c3380-137">Starten des Zeitgebers</span><span class="sxs-lookup"><span data-stu-id="c3380-137">Start the timer</span></span>

<span data-ttu-id="c3380-138">Nachdem wir den Zeitgeber konfiguriert haben, können wir ihn starten.</span><span class="sxs-lookup"><span data-stu-id="c3380-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="c3380-139">Wählen Sie **TimerTriggerCSharp1** aus.</span><span class="sxs-lookup"><span data-stu-id="c3380-139">Select **TimerTriggerCSharp1**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c3380-140">**TimerTriggerCSharp1** ist ein Standardname.</span><span class="sxs-lookup"><span data-stu-id="c3380-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="c3380-141">Er wird beim Erstellen des Zeitgebers automatisch generiert.</span><span class="sxs-lookup"><span data-stu-id="c3380-141">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="c3380-142">Klicken Sie auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="c3380-142">Select **Run**.</span></span> 

<span data-ttu-id="c3380-143">An diesem Punkt sollte im Protokollfenster alle 20 Sekunden eine Meldung angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c3380-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="c3380-144">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="c3380-144">Clean up</span></span>

<span data-ttu-id="c3380-145">Um sicherzustellen, dass Sie für diese Funktion keine Gebühren anfallen, wählen Sie über das Protokollfenster **Anhalten** aus, um den Zeitgeber anzuhalten.</span><span class="sxs-lookup"><span data-stu-id="c3380-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![Anhalten](../media-drafts/4-pause-timer.png)


