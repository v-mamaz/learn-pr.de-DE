<span data-ttu-id="5a3a4-101">In dieser Einheit erstellen wir eine Azure-Funktionen-app, die aufgerufen wird, dass Sie alle 20 Sekunden, die über einen Trigger mit Timer.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-101">In this unit, we create an Azure function app that's invoked every 20 seconds using a timer trigger.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="5a3a4-102">Erstellen einer Azure-Funktionen-app</span><span class="sxs-lookup"><span data-stu-id="5a3a4-102">Create an Azure function app</span></span>

<span data-ttu-id="5a3a4-103">Wir erstellen zunächst eine Azure-Funktions-app im Portal.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-103">Let’s start by creating an Azure Function app in the portal.</span></span>

1. <span data-ttu-id="5a3a4-104">Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-104">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="5a3a4-105">Klicken Sie im linken Navigationsbereich auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="5a3a4-106">Wählen Sie **Compute** aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-106">Select **Compute**.</span></span>

1. <span data-ttu-id="5a3a4-107">Wechseln Sie zu **Funktionen-App**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-107">Locate and select **Function App**.</span></span> <span data-ttu-id="5a3a4-108">Sie können optional auch die Suchleiste verwenden, um die Vorlage zu finden.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Screenshot: Blatt „Ressource erstellen“ im Azure-Portal mit hervorgehobener Funktions-App.](../media/4-click-function-app.png)

1. <span data-ttu-id="5a3a4-110">Geben Sie einen global eindeutigen **Anwendungsnamen**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-110">Enter a globally unique **App name**.</span></span>

1. <span data-ttu-id="5a3a4-111">Wählen Sie ein **Abonnement** aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="5a3a4-112">Erstellen Sie eine neue **Ressourcengruppe**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-112">Create a new **Resource Group**.</span></span>

1. <span data-ttu-id="5a3a4-113">Wählen Sie **Windows** als Ihr **Betriebssystem** aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="5a3a4-114">Wählen Sie als **Hostingplan** die Option **Verbrauchstarif**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="5a3a4-115">Jede Ausführung der Funktion wird Ihnen in Rechnung gestellt.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="5a3a4-116">Ressourcen werden basierend auf dem Workload Ihrer Anwendung automatisch zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="5a3a4-117">Wählen Sie einen **Standort** aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-117">Select a **Location**.</span></span>

1. <span data-ttu-id="5a3a4-118">Erstellen Sie ein neues **Speicherkonto**. Sie können den Namen des Kontos ändern, wenn Sie möchten. Standardmäßig wird eine Variation des App-Namens ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-118">Create a new **Storage** account, you can change the name if you like - it will default to a variation of the App name</span></span>

1. <span data-ttu-id="5a3a4-119">Deaktivieren Sie **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-119">Turn off **Application Insights**.</span></span>

1. <span data-ttu-id="5a3a4-120">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-120">Select **Create**.</span></span> <span data-ttu-id="5a3a4-121">Der Erstellungsvorgang nimmt einige Minuten in Anspruch. Sie können den Fortschritt über das Symbol **Benachrichtigungen** im Symbolleistenbereich nachverfolgen. Sobald die Ressource erstellt wurde, wird eine Schaltfläche zum Öffnen der Ressource im Azure-Portal angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-121">This will take a few minutes to complete, you can watch the **Notifications** icon in the toolbar area - once it has finished creating the resource it will have a button there to open it in the Azure Portal.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="5a3a4-122">Erstellen eines Zeitgebertriggers</span><span class="sxs-lookup"><span data-stu-id="5a3a4-122">Create a timer trigger</span></span>

<span data-ttu-id="5a3a4-123">Jetzt werden wir einen Trigger mit Timer in unserer Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-123">Now we're going to create a timer trigger inside our function.</span></span>

1. <span data-ttu-id="5a3a4-124">Nachdem die Funktion erstellt wird, wählen Sie **alle Ressourcen** im linken Navigationsbereich.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-124">After the function is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="5a3a4-125">Suchen Sie, und wählen Sie die Funktion.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-125">Locate and select your function.</span></span>

1. <span data-ttu-id="5a3a4-126">Zeigen Sie auf dem neuen Blatt auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).</span><span class="sxs-lookup"><span data-stu-id="5a3a4-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Screenshot: Blatt „Funktions-App“ im Azure-Portal mit hervorgehobenem Pluszeichen (+) im Untermenü „Funktionen“](../media/4-hover-function.png)

1. <span data-ttu-id="5a3a4-128">Klicken Sie auf **Zeitgeber**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-128">Select **Timer**.</span></span>

1. <span data-ttu-id="5a3a4-129">Wählen Sie **CSharp** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-129">Select **CSharp** as the language.</span></span>

1. <span data-ttu-id="5a3a4-130">Wählen Sie **Diese Funktion erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="5a3a4-131">Konfigurieren des Zeitgebertriggers</span><span class="sxs-lookup"><span data-stu-id="5a3a4-131">Configure the timer trigger</span></span>

<span data-ttu-id="5a3a4-132">Wir haben eine Azure-Funktionen-app mit Logik, um eine Meldung an das Protokollfenster ausgeben.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-132">We have an Azure function app with logic to print a message to the log window.</span></span> <span data-ttu-id="5a3a4-133">Wir stellen den Zeitplan des Zeitgebers so ein, dass er alle 20 Sekunden ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="5a3a4-134">Wählen Sie **Integrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-134">Select **Integrate**.</span></span>

1. <span data-ttu-id="5a3a4-135">Geben Sie den folgenden Wert in das Feld **Zeitplan** ein:</span><span class="sxs-lookup"><span data-stu-id="5a3a4-135">Enter the following value into the **Schedule** box:</span></span>

    ```log
    */20 * * * * *
    ```

1. <span data-ttu-id="5a3a4-136">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="5a3a4-137">Starten des Zeitgebers</span><span class="sxs-lookup"><span data-stu-id="5a3a4-137">Start the timer</span></span>

<span data-ttu-id="5a3a4-138">Nachdem wir den Zeitgeber konfiguriert haben, können wir ihn starten.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="5a3a4-139">Wählen Sie **TimerTriggerCSharp1** aus.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-139">Select **TimerTriggerCSharp1**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5a3a4-140">**TimerTriggerCSharp1** ist ein Standardname.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="5a3a4-141">Er wird beim Erstellen des Zeitgebers automatisch generiert.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-141">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="5a3a4-142">Klicken Sie auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-142">Select **Run**.</span></span>

<span data-ttu-id="5a3a4-143">An diesem Punkt sollte im Protokollfenster alle 20 Sekunden eine Meldung angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="5a3a4-144">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="5a3a4-144">Clean up</span></span>
<!---TODO: Update for sandbox?--->

<span data-ttu-id="5a3a4-145">Klicken Sie über dem Protokollfenster auf **Anhalten**, und halten Sie den Zeitgeber an, um sicherzustellen, dass für diese Funktion keine Gebühren anfallen.</span><span class="sxs-lookup"><span data-stu-id="5a3a4-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![Screenshot: Protokollausgabebereich der Funktions-App mit hervorgehobener Schaltfläche „Anhalten“](../media/4-pause-timer.png)
