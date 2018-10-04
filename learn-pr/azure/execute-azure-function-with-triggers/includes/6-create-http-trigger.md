<span data-ttu-id="90463-101">In dieser Übung erfahren Sie, wie Sie eine Azure-Funktion erstellen, die eine HTTP-Anforderung mit einer einzelnen Zeichenfolge akzeptiert.</span><span class="sxs-lookup"><span data-stu-id="90463-101">In this unit, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="90463-102">Die Funktion gibt eine Zeichenfolge an den Aufrufer zurück, die angibt, ob der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="90463-102">The function returns a string back to the caller to represent success or failure.</span></span> <span data-ttu-id="90463-103">In der nächsten Übung verwenden Sie diese Funktion weiter.</span><span class="sxs-lookup"><span data-stu-id="90463-103">We'll continue working on the function from the previous exercise.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="90463-104">Erstellen eines HTTP-Triggers</span><span class="sxs-lookup"><span data-stu-id="90463-104">Create an HTTP trigger</span></span>

<span data-ttu-id="90463-105">Verwenden Sie Ihre vorhandene Azure Functions-Anwendung, und fügen Sie einen HTTP-Trigger hinzu.</span><span class="sxs-lookup"><span data-stu-id="90463-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="90463-106">Stellen Sie sicher, dass Sie beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto angemeldet sind, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="90463-106">Make sure you are signed into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="90463-107">Navigieren Sie zur Anzeige **Alle Ressourcen**, und wählen Sie Ihre Funktions-App aus.</span><span class="sxs-lookup"><span data-stu-id="90463-107">Navigate to the **All resources** screen and select your function app.</span></span>

1. <span data-ttu-id="90463-108">Zeigen Sie auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).</span><span class="sxs-lookup"><span data-stu-id="90463-108">Point to **Functions** and select the plus (+) icon.</span></span>

1. <span data-ttu-id="90463-109">Wählen Sie **HTTP-Trigger** aus.</span><span class="sxs-lookup"><span data-stu-id="90463-109">Select **HTTP trigger**.</span></span>

1. <span data-ttu-id="90463-110">Behalten Sie für **Name** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="90463-110">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="90463-111">Legen Sie die **Autorisierungsstufe** auf **Anonym** fest.</span><span class="sxs-lookup"><span data-stu-id="90463-111">Set the **Authorization level** to **Anonymous**.</span></span>

1. <span data-ttu-id="90463-112">Wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="90463-112">Select **Create**.</span></span>

1. <span data-ttu-id="90463-113">Werfen Sie einen kurzen Blick auf den automatisch generierten Code, um sich ein Bild von den Abläufen zu verschaffen.</span><span class="sxs-lookup"><span data-stu-id="90463-113">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="90463-114">Der *req*-Parameter stellt die eingehende Anforderung dar und enthält einen *name*-Parameter.</span><span class="sxs-lookup"><span data-stu-id="90463-114">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="90463-115">Wir überprüfen, ob *name* einen Wert hat.</span><span class="sxs-lookup"><span data-stu-id="90463-115">We check to see if *name* has a value.</span></span> <span data-ttu-id="90463-116">Wenn dies der Fall ist, geben wir einen Gruß zurück.</span><span class="sxs-lookup"><span data-stu-id="90463-116">If it does, we return a greeting.</span></span> <span data-ttu-id="90463-117">Andernfalls geben wir eine Fehlermeldung zurück.</span><span class="sxs-lookup"><span data-stu-id="90463-117">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="90463-118">Abrufen Ihrer Funktions-URL</span><span class="sxs-lookup"><span data-stu-id="90463-118">Get your function URL</span></span>

<span data-ttu-id="90463-119">Da wir nun den HTTP-Trigger erstellt haben, rufen wir die Funktions-URL ab, damit wir beginnen können, eine Anforderung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="90463-119">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="90463-120">Wählen Sie Ihren HTTP-Trigger aus, um den Codebildschirm zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="90463-120">Select your HTTP trigger to open the code screen.</span></span>

1. <span data-ttu-id="90463-121">Wählen Sie rechts neben **Ausführen** die Option **Get function URL** (Funktions-URL abrufen) aus.</span><span class="sxs-lookup"><span data-stu-id="90463-121">To the right of **Run**, select **Get function URL**.</span></span>

1. <span data-ttu-id="90463-122">Klicken Sie auf **Kopieren**, und schließen Sie anschließend das Popupfenster „Funktions-URL“.</span><span class="sxs-lookup"><span data-stu-id="90463-122">Select **Copy**, then close the function URL popup.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="90463-123">Übermitteln einer GET-Anforderung an Ihren HTTP-Trigger</span><span class="sxs-lookup"><span data-stu-id="90463-123">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="90463-124">Wir haben jetzt unsere Funktions-URL in unsere Zwischenablage kopiert.</span><span class="sxs-lookup"><span data-stu-id="90463-124">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="90463-125">Nun geben wir eine GET-Anforderung aus, um festzustellen, ob wir eine Antwort erhalten.</span><span class="sxs-lookup"><span data-stu-id="90463-125">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="90463-126">Öffnen Sie eine neue Registerkarte in Ihrem Webbrowser.</span><span class="sxs-lookup"><span data-stu-id="90463-126">Open a new tab in your web browser.</span></span>

1. <span data-ttu-id="90463-127">Fügen Sie die URL in die Adressleiste ein.</span><span class="sxs-lookup"><span data-stu-id="90463-127">Paste the URL into the address bar.</span></span>

1. <span data-ttu-id="90463-128">Fügen Sie einen Abfragezeichenfolgen-Parameter namens *Name* mit Ihrem Namen hinzu, z.B. `.../api/HttpTriggerCSharp1?name=Jesse`.</span><span class="sxs-lookup"><span data-stu-id="90463-128">Add a query string parameter called *name* with your name for example `.../api/HttpTriggerCSharp1?name=Jesse`</span></span>

1. <span data-ttu-id="90463-129">Drücken Sie die <kbd>EINGABETASTE</kbd>, um die Anforderung zu senden.</span><span class="sxs-lookup"><span data-stu-id="90463-129">Press <kbd>ENTER</kbd> to submit the request.</span></span>
