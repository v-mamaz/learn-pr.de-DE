<span data-ttu-id="1658e-101">In dieser Übung erstellen wir eine Azure-Funktion, die eine HTTP-Anforderung mit einer einzelnen Zeichenfolge akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="1658e-101">In this exercise, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="1658e-102">Die Funktion gibt eine Zeichenfolge an den Aufrufer zurück, um Erfolg oder Fehler darzustellen.</span><span class="sxs-lookup"><span data-stu-id="1658e-102">The function returns a string back to the caller to represent success or failure.</span></span>

> [!NOTE]
> <span data-ttu-id="1658e-103">Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com/) mit einem gültigen Konto angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="1658e-103">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="1658e-104">Erstellen eines HTTP-Triggers</span><span class="sxs-lookup"><span data-stu-id="1658e-104">Create an HTTP trigger</span></span>

<span data-ttu-id="1658e-105">Verwenden Sie Ihre vorhandene Azure Functions-Anwendung, und fügen Sie einen HTTP-Trigger hinzu.</span><span class="sxs-lookup"><span data-stu-id="1658e-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="1658e-106">Zeigen Sie auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.</span><span class="sxs-lookup"><span data-stu-id="1658e-106">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Zeigen auf „Funktionen“ und Auswählen des Pluszeichens](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="1658e-108">Wählen Sie **HTTP-Trigger** aus.</span><span class="sxs-lookup"><span data-stu-id="1658e-108">Select **HTTP trigger**.</span></span>

1. <span data-ttu-id="1658e-109">Wählen Sie **C#** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="1658e-109">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="1658e-110">Behalten Sie für **Name** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="1658e-110">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="1658e-111">Legen Sie die **Autorisierungsstufe** auf **Anonym** fest.</span><span class="sxs-lookup"><span data-stu-id="1658e-111">Set the **Authorization level** to **Anonymous**.</span></span>

1. <span data-ttu-id="1658e-112">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="1658e-112">Select **Create**.</span></span>

1. <span data-ttu-id="1658e-113">Werfen Sie einen kurzen Blick auf den automatisch generierten Code, um sich ein Bild von den Abläufen zu verschaffen.</span><span class="sxs-lookup"><span data-stu-id="1658e-113">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="1658e-114">Der *req*-Parameter stellt die eingehende Anforderung dar und enthält einen *name*-Parameter.</span><span class="sxs-lookup"><span data-stu-id="1658e-114">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="1658e-115">Wir überprüfen, ob *name* einen Wert hat.</span><span class="sxs-lookup"><span data-stu-id="1658e-115">We check to see if *name* has a value.</span></span> <span data-ttu-id="1658e-116">Wenn dies der Fall ist, geben wir einen Gruß zurück.</span><span class="sxs-lookup"><span data-stu-id="1658e-116">If it does, we return a greeting.</span></span> <span data-ttu-id="1658e-117">Andernfalls geben wir eine Fehlermeldung zurück.</span><span class="sxs-lookup"><span data-stu-id="1658e-117">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="1658e-118">Abrufen Ihrer Funktions-URL</span><span class="sxs-lookup"><span data-stu-id="1658e-118">Get your function URL</span></span>

<span data-ttu-id="1658e-119">Da wir nun den HTTP-Trigger erstellt haben, rufen wir die Funktions-URL ab, damit wir beginnen können, eine Anforderung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="1658e-119">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="1658e-120">Wählen Sie Ihren HTTP-Trigger aus, um den Codebildschirm zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="1658e-120">Select your HTTP trigger to open the code screen.</span></span>

1. <span data-ttu-id="1658e-121">Wählen Sie rechts von **Ausführen** die Option **Funktions-URL abrufen** aus.</span><span class="sxs-lookup"><span data-stu-id="1658e-121">To the right of **Run**, select **Get function URL**.</span></span>

1. <span data-ttu-id="1658e-122">Wählen Sie **Kopieren** aus.</span><span class="sxs-lookup"><span data-stu-id="1658e-122">Select **Copy**.</span></span>

1. <span data-ttu-id="1658e-123">Wählen Sie **Ausführen** aus, um Ihre Funktion zu starten.</span><span class="sxs-lookup"><span data-stu-id="1658e-123">Select **Run** to start your function.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="1658e-124">Ausgeben einer GET-Anforderung an Ihren HTTP-Trigger</span><span class="sxs-lookup"><span data-stu-id="1658e-124">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="1658e-125">Wir haben jetzt unsere Funktions-URL in unsere Zwischenablage kopiert.</span><span class="sxs-lookup"><span data-stu-id="1658e-125">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="1658e-126">Nun geben wir eine GET-Anforderung aus, um festzustellen, ob wir eine Antwort erhalten.</span><span class="sxs-lookup"><span data-stu-id="1658e-126">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="1658e-127">Öffnen Sie eine neue Registerkarte in Ihrem Webbrowser.</span><span class="sxs-lookup"><span data-stu-id="1658e-127">Open a new tab in your web browser.</span></span>

1. <span data-ttu-id="1658e-128">Fügen Sie die URL in die Adressleiste ein.</span><span class="sxs-lookup"><span data-stu-id="1658e-128">Paste the URL into the address bar.</span></span>

1. <span data-ttu-id="1658e-129">Fügen Sie einen Abfragezeichenfolgen-Parameter namens *name* mit Ihrem Namen hinzu, z.B.:</span><span class="sxs-lookup"><span data-stu-id="1658e-129">Add a query string parameter called *name* with your name for example:</span></span>

    ```
    .../api/HttpTriggerCSharp1?name=Jesse
    ```

1. <span data-ttu-id="1658e-130">Wählen Sie EINGABE aus, um die Anforderung zu senden.</span><span class="sxs-lookup"><span data-stu-id="1658e-130">Select ENTER to submit the request.</span></span>

## <a name="clean-up"></a><span data-ttu-id="1658e-131">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="1658e-131">Clean up</span></span>

<span data-ttu-id="1658e-132">Um sicherzustellen, dass für diese Funktion keine Gebühren anfallen, wählen Sie über dem Protokollfenster **Anhalten** aus.</span><span class="sxs-lookup"><span data-stu-id="1658e-132">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Anhalten](../media-drafts/4-pause-timer.png)


