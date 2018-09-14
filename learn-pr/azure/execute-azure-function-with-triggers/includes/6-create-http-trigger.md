<span data-ttu-id="af09a-101">In dieser Übung erfahren Sie, wie Sie eine Azure-Funktion erstellen, die eine HTTP-Anforderung mit einer einzelnen Zeichenfolge akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="af09a-101">In this unit, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="af09a-102">Die Funktion gibt eine Zeichenfolge an den Aufrufer zurück, die angibt, ob der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="af09a-102">The function returns a string back to the caller to represent success or failure.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="af09a-103">Erstellen eines HTTP-Triggers</span><span class="sxs-lookup"><span data-stu-id="af09a-103">Create an HTTP trigger</span></span>

<span data-ttu-id="af09a-104">Verwenden Sie Ihre vorhandene Azure Functions-Anwendung, und fügen Sie einen HTTP-Trigger hinzu.</span><span class="sxs-lookup"><span data-stu-id="af09a-104">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="af09a-105">Melden Sie sich im [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="af09a-105">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="af09a-106">Zeigen Sie auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).</span><span class="sxs-lookup"><span data-stu-id="af09a-106">Point to **Functions** and select the plus (+) icon.</span></span>

1. <span data-ttu-id="af09a-107">Klicken Sie auf **HTTP-Trigger**.</span><span class="sxs-lookup"><span data-stu-id="af09a-107">Select **HTTP trigger**.</span></span>

1. <span data-ttu-id="af09a-108">Wählen Sie **C#** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="af09a-108">Select **C#** as the language.</span></span>

1. <span data-ttu-id="af09a-109">Behalten Sie für **Name** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="af09a-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="af09a-110">Legen Sie die **Autorisierungsstufe** auf **Anonym** fest.</span><span class="sxs-lookup"><span data-stu-id="af09a-110">Set the **Authorization level** to **Anonymous**.</span></span>

1. <span data-ttu-id="af09a-111">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="af09a-111">Select **Create**.</span></span>

1. <span data-ttu-id="af09a-112">Werfen Sie einen kurzen Blick auf den automatisch generierten Code, um sich ein Bild von den Abläufen zu verschaffen.</span><span class="sxs-lookup"><span data-stu-id="af09a-112">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="af09a-113">Der *req*-Parameter stellt die eingehende Anforderung dar und enthält einen *name*-Parameter.</span><span class="sxs-lookup"><span data-stu-id="af09a-113">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="af09a-114">Wir überprüfen, ob *name* einen Wert hat.</span><span class="sxs-lookup"><span data-stu-id="af09a-114">We check to see if *name* has a value.</span></span> <span data-ttu-id="af09a-115">Wenn dies der Fall ist, geben wir einen Gruß zurück.</span><span class="sxs-lookup"><span data-stu-id="af09a-115">If it does, we return a greeting.</span></span> <span data-ttu-id="af09a-116">Andernfalls geben wir eine Fehlermeldung zurück.</span><span class="sxs-lookup"><span data-stu-id="af09a-116">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="af09a-117">Abrufen Ihrer Funktions-URL</span><span class="sxs-lookup"><span data-stu-id="af09a-117">Get your function URL</span></span>

<span data-ttu-id="af09a-118">Da wir nun den HTTP-Trigger erstellt haben, rufen wir die Funktions-URL ab, damit wir beginnen können, eine Anforderung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="af09a-118">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="af09a-119">Wählen Sie Ihren HTTP-Trigger aus, um den Codebildschirm zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="af09a-119">Select your HTTP trigger to open the code screen.</span></span>

1. <span data-ttu-id="af09a-120">Wählen Sie rechts von **Ausführen** die Option **Funktions-URL abrufen** aus.</span><span class="sxs-lookup"><span data-stu-id="af09a-120">To the right of **Run**, select **Get function URL**.</span></span>

1. <span data-ttu-id="af09a-121">Wählen Sie **Kopieren** aus.</span><span class="sxs-lookup"><span data-stu-id="af09a-121">Select **Copy**.</span></span>

1. <span data-ttu-id="af09a-122">Wählen Sie **Ausführen** aus, um Ihre Funktion zu starten.</span><span class="sxs-lookup"><span data-stu-id="af09a-122">Select **Run** to start your function.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="af09a-123">Ausgeben einer GET-Anforderung an Ihren HTTP-Trigger</span><span class="sxs-lookup"><span data-stu-id="af09a-123">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="af09a-124">Wir haben jetzt unsere Funktions-URL in unsere Zwischenablage kopiert.</span><span class="sxs-lookup"><span data-stu-id="af09a-124">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="af09a-125">Nun geben wir eine GET-Anforderung aus, um festzustellen, ob wir eine Antwort erhalten.</span><span class="sxs-lookup"><span data-stu-id="af09a-125">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="af09a-126">Öffnen Sie eine neue Registerkarte in Ihrem Webbrowser.</span><span class="sxs-lookup"><span data-stu-id="af09a-126">Open a new tab in your web browser.</span></span>

1. <span data-ttu-id="af09a-127">Fügen Sie die URL in die Adressleiste ein.</span><span class="sxs-lookup"><span data-stu-id="af09a-127">Paste the URL into the address bar.</span></span>

1. <span data-ttu-id="af09a-128">Fügen Sie einen Abfragezeichenfolgen-Parameter namens *name* mit Ihrem Namen hinzu, z.B. `.../api/HttpTriggerCSharp1?name=Jesse`.</span><span class="sxs-lookup"><span data-stu-id="af09a-128">Add a query string parameter called *name* with your name for example `.../api/HttpTriggerCSharp1?name=Jesse`</span></span>

1. <span data-ttu-id="af09a-129">Drücken Sie die EINGABETASTE, um die Anforderung zu senden.</span><span class="sxs-lookup"><span data-stu-id="af09a-129">Select ENTER to submit the request.</span></span>

## <a name="clean-up"></a><span data-ttu-id="af09a-130">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="af09a-130">Clean up</span></span>
<!---TODO: Update for sandbox?--->

<span data-ttu-id="af09a-131">Klicken Sie über dem Protokollfenster auf **Anhalten**, um sicherzustellen, dass für diese Funktion keine Gebühren anfallen.</span><span class="sxs-lookup"><span data-stu-id="af09a-131">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>
