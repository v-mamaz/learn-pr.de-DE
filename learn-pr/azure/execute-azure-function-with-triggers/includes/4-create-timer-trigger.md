<span data-ttu-id="2987a-101">In dieser Übung erstellen wir eine Azure-Funktion, die alle 20 Sekunden mithilfe eines Zeitgebertriggers aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="2987a-101">In this exercise, we create an Azure function that's invoked every 20 seconds using a timer trigger.</span></span>

> [!NOTE] 
> <span data-ttu-id="2987a-102">Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) mit einem gültigen Konto angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="2987a-102">To complete this exercise, make sure you're logged into the [Azure portal](https://portal.azure.com?azure-portal=true) with a valid account.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="2987a-103">Erstellen einer Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="2987a-103">Create an Azure function</span></span>

<span data-ttu-id="2987a-104">Wir beginnen, indem wir eine Azure-Funktion im Portal erstellen.</span><span class="sxs-lookup"><span data-stu-id="2987a-104">Let’s start by creating an Azure Function in the portal.</span></span>

1. <span data-ttu-id="2987a-105">Klicken Sie im linken Navigationsbereich auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2987a-105">In the left navigation, select **Create a resource**.</span></span>

2. <span data-ttu-id="2987a-106">Wählen Sie **Compute** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-106">Select **Compute**.</span></span>

3. <span data-ttu-id="2987a-107">Wechseln Sie zu **Funktionen-App**.</span><span class="sxs-lookup"><span data-stu-id="2987a-107">Locate and select **Function App**.</span></span> <span data-ttu-id="2987a-108">Sie können optional auch die Suchleiste verwenden, um die Vorlage zu finden.</span><span class="sxs-lookup"><span data-stu-id="2987a-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Auswählen von „Funktionen-App“](../media-drafts/4-click-function-app.png)

4. <span data-ttu-id="2987a-110">Geben Sie einen eindeutigen **App-Namen** ein.</span><span class="sxs-lookup"><span data-stu-id="2987a-110">Enter a unique **App name**.</span></span>

5. <span data-ttu-id="2987a-111">Wählen Sie ein **Abonnement** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-111">Select a **Subscription**.</span></span>

6. <span data-ttu-id="2987a-112">Erstellen Sie eine neue **Ressourcengruppe**.</span><span class="sxs-lookup"><span data-stu-id="2987a-112">Create a new **Resource Group**.</span></span>

7. <span data-ttu-id="2987a-113">Wählen Sie **Windows** als Ihr **Betriebssystem** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-113">Choose **Windows** as your **OS**.</span></span>

8. <span data-ttu-id="2987a-114">Wählen Sie als **Hostingplan** die Option **Verbrauchstarif**.</span><span class="sxs-lookup"><span data-stu-id="2987a-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="2987a-115">Jede Ausführung der Funktion wird Ihnen in Rechnung gestellt.</span><span class="sxs-lookup"><span data-stu-id="2987a-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="2987a-116">Ressourcen werden basierend auf dem Workload Ihrer Anwendung automatisch zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="2987a-116">Resources are automatically allocated based on your application workload.</span></span>

9. <span data-ttu-id="2987a-117">Wählen Sie einen **Standort** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-117">Select a **Location**.</span></span>

10. <span data-ttu-id="2987a-118">Erstellen Sie ein neues **Speicherkonto**. Sie können den Namen des Kontos ändern, wenn Sie möchten. Standardmäßig wird eine Variation des App-Namens ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="2987a-118">Create a new **Storage** account, you can change the name if you like - it will default to a variation of the App name</span></span>

11. <span data-ttu-id="2987a-119">Deaktivieren Sie **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="2987a-119">Turn off **Application Insights**.</span></span>

12. <span data-ttu-id="2987a-120">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="2987a-120">Select **Create**.</span></span> <span data-ttu-id="2987a-121">Der Erstellungsvorgang nimmt einige Minuten in Anspruch. Sie können den Fortschritt über das Symbol **Benachrichtigungen** im Symbolleistenbereich nachverfolgen. Sobald die Ressource erstellt wurde, wird eine Schaltfläche zum Öffnen der Ressource im Azure-Portal angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2987a-121">This will take a few minutes to complete, you can watch the **Notifications** icon in the toolbar area - once it has finished creating the resource it will have a button there to open it in the Azure Portal.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="2987a-122">Erstellen eines Zeitgebertriggers</span><span class="sxs-lookup"><span data-stu-id="2987a-122">Create a timer trigger</span></span>

<span data-ttu-id="2987a-123">Wir erstellen nun in unserer Azure-Funktion einen Zeitgebertrigger.</span><span class="sxs-lookup"><span data-stu-id="2987a-123">Now we're going to create a timer trigger inside our Azure function.</span></span>

1. <span data-ttu-id="2987a-124">Nachdem die Azure-Funktion erstellt wurde, wählen Sie im linken Navigationsbereich **Alle Ressourcen** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-124">After the Azure function is created, select **All resources** from the left navigation.</span></span>

2. <span data-ttu-id="2987a-125">Wählen Sie Ihre Azure-Funktion aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-125">Locate and select your Azure function.</span></span>

3. <span data-ttu-id="2987a-126">Zeigen Sie auf dem neuen Blatt auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Auf „Funktionen“ zeigen und Pluszeichen auswählen](../media-drafts/4-hover-function.png)

4. <span data-ttu-id="2987a-128">Wählen Sie **Zeitgeber** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-128">Select **Timer**.</span></span>

5. <span data-ttu-id="2987a-129">Wählen Sie **CSharp** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-129">Select **CSharp** as the language.</span></span>

6. <span data-ttu-id="2987a-130">Wählen Sie **Diese Funktion erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="2987a-131">Konfigurieren des Zeitgebertriggers</span><span class="sxs-lookup"><span data-stu-id="2987a-131">Configure the timer trigger</span></span>

<span data-ttu-id="2987a-132">Wir haben eine Azure-Funktion mit Logik zum Ausgeben einer Meldung im Protokollfenster.</span><span class="sxs-lookup"><span data-stu-id="2987a-132">We have an Azure function with logic to print a message to the log window.</span></span> <span data-ttu-id="2987a-133">Wir stellen den Zeitplan des Zeitgebers so ein, dass er alle 20 Sekunden ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="2987a-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="2987a-134">Wählen Sie **Integrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-134">Select **Integrate**.</span></span>

2. <span data-ttu-id="2987a-135">Geben Sie den folgenden Wert in das Feld **Zeitplan** ein:</span><span class="sxs-lookup"><span data-stu-id="2987a-135">Enter the following value into the **Schedule** box:</span></span>

    ```
    */20 * * * * *
    ```

3. <span data-ttu-id="2987a-136">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="2987a-137">Starten des Zeitgebers</span><span class="sxs-lookup"><span data-stu-id="2987a-137">Start the timer</span></span>

<span data-ttu-id="2987a-138">Nachdem wir den Zeitgeber konfiguriert haben, können wir ihn starten.</span><span class="sxs-lookup"><span data-stu-id="2987a-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="2987a-139">Wählen Sie **TimerTriggerCSharp1** aus.</span><span class="sxs-lookup"><span data-stu-id="2987a-139">Select **TimerTriggerCSharp1**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="2987a-140">**TimerTriggerCSharp1** ist ein Standardname.</span><span class="sxs-lookup"><span data-stu-id="2987a-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="2987a-141">Er wird beim Erstellen des Zeitgebers automatisch generiert.</span><span class="sxs-lookup"><span data-stu-id="2987a-141">It's automatically selected when you create the trigger.</span></span>

2. <span data-ttu-id="2987a-142">Klicken Sie auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="2987a-142">Select **Run**.</span></span> 

<span data-ttu-id="2987a-143">An diesem Punkt sollte im Protokollfenster alle 20 Sekunden eine Meldung angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="2987a-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="2987a-144">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="2987a-144">Clean up</span></span>

<span data-ttu-id="2987a-145">Um sicherzustellen, dass Sie für diese Funktion keine Gebühren anfallen, wählen Sie über das Protokollfenster **Anhalten** aus, um den Zeitgeber anzuhalten.</span><span class="sxs-lookup"><span data-stu-id="2987a-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![Anhalten](../media-drafts/4-pause-timer.png)


