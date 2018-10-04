<span data-ttu-id="06e7e-101">In dieser Einheit erfahren Sie, wie Sie eine Azure-Funktions-App erstellen, die alle 20 Sekunden mithilfe eines Timertriggers aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="06e7e-101">In this unit, we create an Azure function app that's invoked every 20 seconds using a timer trigger.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="06e7e-102">Erstellen einer Azure-Funktions-App</span><span class="sxs-lookup"><span data-stu-id="06e7e-102">Create an Azure function app</span></span>

<span data-ttu-id="06e7e-103">Erstellen Sie zuerst eine Azure-Funktions-App im Portal.</span><span class="sxs-lookup"><span data-stu-id="06e7e-103">Let’s start by creating an Azure Function app in the portal.</span></span>

1. <span data-ttu-id="06e7e-104">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="06e7e-104">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="06e7e-105">Wählen Sie im linken Navigationsbereich **Ressource erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="06e7e-106">Wählen Sie **Compute** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-106">Select **Compute**.</span></span>

1. <span data-ttu-id="06e7e-107">Wechseln Sie zu **Funktionen-App**.</span><span class="sxs-lookup"><span data-stu-id="06e7e-107">Locate and select **Function App**.</span></span> <span data-ttu-id="06e7e-108">Sie können optional auch die Suchleiste verwenden, um die Vorlage zu finden.</span><span class="sxs-lookup"><span data-stu-id="06e7e-108">You can also optionally use the search bar to locate the template.</span></span>

    ![Screenshot: Blatt „Ressource erstellen“ im Azure-Portal mit hervorgehobener Funktions-App.](../media/4-click-function-app.png)

1. <span data-ttu-id="06e7e-110">Geben Sie einen global eindeutigen **App-Namen** ein.</span><span class="sxs-lookup"><span data-stu-id="06e7e-110">Enter a globally unique **App name**.</span></span>

1. <span data-ttu-id="06e7e-111">Wählen Sie ein **Abonnement** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="06e7e-112">Wählen Sie die vorhandene **Ressourcengruppe** <rgn>[Name der Sandboxressourcengruppe]</rgn> aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-112">Select the existing **Resource group** <rgn>[sandbox resource group name]</rgn>.</span></span>

1. <span data-ttu-id="06e7e-113">Wählen Sie **Windows** als Ihr **Betriebssystem** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="06e7e-114">Wählen Sie als **Hostingplan** die Option **Verbrauchstarif**.</span><span class="sxs-lookup"><span data-stu-id="06e7e-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="06e7e-115">Jede Ausführung der Funktion wird Ihnen in Rechnung gestellt.</span><span class="sxs-lookup"><span data-stu-id="06e7e-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="06e7e-116">Ressourcen werden basierend auf dem Workload Ihrer Anwendung automatisch zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="06e7e-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="06e7e-117">Wählen Sie aus der unten verfügbaren Liste einen **Standort** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-117">Select a **Location** from the available list below.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. <span data-ttu-id="06e7e-118">Behalten Sie für **Laufzeitstapel** *.NET* als Standard bei. In dieser Sprache werden die Funktionsbeispiele in dieser Übung implementiert.</span><span class="sxs-lookup"><span data-stu-id="06e7e-118">For **Runtime Stack**, leave as default *.NET*, which is the language in which we implement the function examples in this exercise.</span></span>

1. <span data-ttu-id="06e7e-119">Erstellen Sie ein neues **Speicherkonto**. Sie können den Namen des Kontos bei Bedarf ändern. Standardmäßig wird eine Variation des App-Namens ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="06e7e-119">Create a new **Storage** account, you can change the name if you like - it will default to a variation of the App name.</span></span>

1. <span data-ttu-id="06e7e-120">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-120">Select **Create**.</span></span> <span data-ttu-id="06e7e-121">Sobald die Funktions-App bereitgestellt ist, wechseln Sie im Portal zu **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="06e7e-121">Once the function app is deployed, go to **All resources** in the portal.</span></span> <span data-ttu-id="06e7e-122">Die Funktions-App wird mit dem Typ **App Service** aufgelistet und hat den Namen, den Sie ihr gegeben haben.</span><span class="sxs-lookup"><span data-stu-id="06e7e-122">The function app will be listed with type **App Service** and has the name you gave it.</span></span>
 
<!-- Start temporary fix for issue #2498. -->
> [!IMPORTANT]
> <span data-ttu-id="06e7e-123">Die Übungen in diesem Modul können derzeit mit Azure Functions V1 ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="06e7e-123">The exercises in this module currently work with Azure Functions V1.</span></span> <span data-ttu-id="06e7e-124">Befolgen Sie diese Schritte sorgfältig, um sicherzustellen, dass Ihre Funktions-App die V1-Runtimeversion verwendet.</span><span class="sxs-lookup"><span data-stu-id="06e7e-124">Please follow these steps carefully to make sure your function app uses the V1 runtime version.</span></span> 

1. <span data-ttu-id="06e7e-125">Wählen Sie nach dem Erstellen der Funktions-App im linken Navigationsbereich die Option **Alle Ressourcen** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-125">After the function app is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="06e7e-126">Wählen Sie aus der Liste **Funktions-Apps** Ihre Funktions-App aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-126">Select your function app in the **Function Apps** list.</span></span>
1. <span data-ttu-id="06e7e-127">Wählen Sie **Plattformfeatures** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-127">Select **Platform features**.</span></span>
1. <span data-ttu-id="06e7e-128">Wählen Sie in der Anzeige **Plattformfeatures** unter **Allgemeine Einstellungen** die **Einstellungen für Funktions-Apps** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-128">In the **Platform features** screen, select **Function app settings** under **General Settings**.</span></span>
1. <span data-ttu-id="06e7e-129">Wählen Sie in der **Runtimeversion** den Eintrag *~1* aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-129">Select *~1* in the **Runtime version** .</span></span>
1. <span data-ttu-id="06e7e-130">Schließen Sie die **Einstellungen für Funktions-Apps**.</span><span class="sxs-lookup"><span data-stu-id="06e7e-130">Close **Function app settings**.</span></span>

<span data-ttu-id="06e7e-131">Die Funktions-App ist nun für die Verwendung der Azure Functions V1-Runtime konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="06e7e-131">Our function app is now configured to use the Azure Functions V1 runtime.</span></span> <span data-ttu-id="06e7e-132">Wir können nun mit der Erstellung unserer ersten Funktion fortfahren.</span><span class="sxs-lookup"><span data-stu-id="06e7e-132">We can now continue to create our first function.</span></span>
<!-- End temporary fix for issue #2498. --> 

## <a name="create-a-timer-trigger"></a><span data-ttu-id="06e7e-133">Erstellen eines Zeitgebertriggers</span><span class="sxs-lookup"><span data-stu-id="06e7e-133">Create a timer trigger</span></span>

<span data-ttu-id="06e7e-134">Wir erstellen nun in unserer Funktion einen Zeitgebertrigger.</span><span class="sxs-lookup"><span data-stu-id="06e7e-134">Now we're going to create a timer trigger inside our function.</span></span>



1. <span data-ttu-id="06e7e-135">Zeigen Sie auf dem neuen Blatt mit dem Cursor auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).</span><span class="sxs-lookup"><span data-stu-id="06e7e-135">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![Screenshot: Blatt „Funktions-App“ im Azure-Portal mit hervorgehobenem Pluszeichen (+) im Untermenü „Funktionen“](../media/4-hover-function.png)

1. <span data-ttu-id="06e7e-137">Wählen Sie **Zeitgeber** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-137">Select **Timer**.</span></span>

1. <span data-ttu-id="06e7e-138">Wählen Sie **Diese Funktion erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-138">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="06e7e-139">Konfigurieren des Timertriggers</span><span class="sxs-lookup"><span data-stu-id="06e7e-139">Configure the timer trigger</span></span>

<span data-ttu-id="06e7e-140">Wir verfügen über eine Azure-Funktions-App mit Logik zum Ausgeben einer Meldung im Protokollfenster.</span><span class="sxs-lookup"><span data-stu-id="06e7e-140">We have an Azure function app with logic to print a message to the log window.</span></span> <span data-ttu-id="06e7e-141">Der Zeitplan des Timers wird so eingestellt, dass er alle 20 Sekunden ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="06e7e-141">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="06e7e-142">Wählen Sie **Integrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-142">Select **Integrate**.</span></span>

1. <span data-ttu-id="06e7e-143">Geben Sie den folgenden Wert in das Feld **Zeitplan** ein:</span><span class="sxs-lookup"><span data-stu-id="06e7e-143">Enter the following value into the **Schedule** box:</span></span>

    ```log
    */20 * * * * *
    ```

1. <span data-ttu-id="06e7e-144">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-144">Select **Save**.</span></span>

## <a name="test-the-timer"></a><span data-ttu-id="06e7e-145">Testen des Timers</span><span class="sxs-lookup"><span data-stu-id="06e7e-145">Test the timer</span></span>

<span data-ttu-id="06e7e-146">Nachdem Sie nun den Timer konfiguriert haben, ruft er die Funktion in dem von uns definierten Intervall auf.</span><span class="sxs-lookup"><span data-stu-id="06e7e-146">Now that we've configured the timer, it will invoke the function on the interval we defined.</span></span>

1. <span data-ttu-id="06e7e-147">Wählen Sie **TimerTriggerCSharp1** aus.</span><span class="sxs-lookup"><span data-stu-id="06e7e-147">Select **TimerTriggerCSharp1**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="06e7e-148">**TimerTriggerCSharp1** ist ein Standardname.</span><span class="sxs-lookup"><span data-stu-id="06e7e-148">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="06e7e-149">Er wird beim Erstellen des Triggers automatisch generiert.</span><span class="sxs-lookup"><span data-stu-id="06e7e-149">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="06e7e-150">Öffnen Sie unten in der Anzeige den Bereich **Protokolle**.</span><span class="sxs-lookup"><span data-stu-id="06e7e-150">Open the **Logs** panel at the bottom of the screen.</span></span>

1. <span data-ttu-id="06e7e-151">Beobachten Sie, wie alle 20 Sekunden neue Meldungen im Protokollfenster eingehen.</span><span class="sxs-lookup"><span data-stu-id="06e7e-151">Observe new messages arrive every 20 seconds in the log window.</span></span>

1. <span data-ttu-id="06e7e-152">Damit die Funktion nicht mehr länger ausgeführt wird, wählen Sie **Verwalten**, und ändern Sie dann den **Funktionszustand** in *Deaktiviert*.</span><span class="sxs-lookup"><span data-stu-id="06e7e-152">To stop the function from running, select **Manage** and then switch **Function State** to *Disabled*.</span></span>
