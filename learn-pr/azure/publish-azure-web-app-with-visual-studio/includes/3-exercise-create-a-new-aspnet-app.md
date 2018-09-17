<span data-ttu-id="20790-101">Da sich Ihre App nun einsatzbereit auf Ihrem lokalen Computer befindet, kann sie in Azure veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="20790-101">Now that you've got your app up and running on your local machine, it's time to get it published to Azure.</span></span> 

<span data-ttu-id="20790-102">In dieser Einheit entwerfen und erstellen Sie eine neue ASP.NET-Webanwendung und führen sie auf dem lokalen Computer aus.</span><span class="sxs-lookup"><span data-stu-id="20790-102">In this unit, you will create, build, and run a new ASP.NET web application on your local machine.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="20790-103">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="20790-103">Create a new project</span></span>

### <a name="visual-studio-for-windows"></a><span data-ttu-id="20790-104">Visual Studio für Windows</span><span class="sxs-lookup"><span data-stu-id="20790-104">Visual Studio for Windows</span></span>

<span data-ttu-id="20790-105">Im ersten Schritt wird Visual Studio gestartet und eine lokale ASP.NET Core-Webanwendung erstellt.</span><span class="sxs-lookup"><span data-stu-id="20790-105">The first step is to start Visual Studio and create a local ASP.NET Core web application.</span></span>

1. <span data-ttu-id="20790-106">Klicken Sie auf der Startseite von Visual Studio auf **Datei** und anschließend auf **Neu** > **Projekt...**.</span><span class="sxs-lookup"><span data-stu-id="20790-106">On the Visual Studio start page, select **File**, then click **New**, and then click **Project..**.</span></span>

1. <span data-ttu-id="20790-107">Klicken Sie im linken Bereich des Dialogfelds **Neues Projekt** auf **Web**.</span><span class="sxs-lookup"><span data-stu-id="20790-107">In the **New Project** dialog box, on the left-hand pane, select **Web**.</span></span>

1. <span data-ttu-id="20790-108">Klicken Sie im mittleren Bereich auf **ASP.NET Core-Webanwendung**.</span><span class="sxs-lookup"><span data-stu-id="20790-108">In the center pane, click **ASP.NET Core Web Application**.</span></span>

1. <span data-ttu-id="20790-109">Geben Sie am unteren Rand des Dialogfelds im Feld **Name** den Namen **Alpine Ski House** ein.</span><span class="sxs-lookup"><span data-stu-id="20790-109">At the bottom of the dialog box, in the **Name** field, enter **Alpine Ski House**.</span></span>

1. <span data-ttu-id="20790-110">Wählen Sie einen **Speicherort** für die neue Projektmappe aus.</span><span class="sxs-lookup"><span data-stu-id="20790-110">Select a **Location** for your new solution.</span></span>

1. <span data-ttu-id="20790-111">Klicken Sie auf die Schaltfläche **OK**, um Ihr Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="20790-111">Click the **OK** button to create your project.</span></span>

1. <span data-ttu-id="20790-112">Im Dialogfeld **Neue ASP.NET Core-Webanwendung** wird Ihnen eine Auswahl von Startvorlagen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="20790-112">In the **New ASP.NET Core Web Application** dialog box, you will see a selection of starting templates.</span></span> <span data-ttu-id="20790-113">Wählen Sie für diese Übung **Webanwendung** aus, und klicken Sie dann zum Erstellen Ihres Projekts auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="20790-113">For this exercise, select **Web Application**, and then click **OK** to create your project.</span></span>

    ![Dialogfeld „Neues Projekt“](../media-draft/3-aspnet-templates.png)

    > [!NOTE]
    > <span data-ttu-id="20790-115">Sie können je nach Webentwicklungsanforderungen auch andere Startvorlagen in diesem Dialogfeld auswählen.</span><span class="sxs-lookup"><span data-stu-id="20790-115">You can also select different starting templates in this dialog box depending on your web development requirements.</span></span> <span data-ttu-id="20790-116">Am oberen Rand des Dialogfelds können Sie auch die ASP.NET Core-Version auswählen.</span><span class="sxs-lookup"><span data-stu-id="20790-116">At the top of the dialog box, you are also able to select the version of ASP.NET Core.</span></span> <span data-ttu-id="20790-117">Wählen Sie mindestens ASP.NET Core 2.0 aus.</span><span class="sxs-lookup"><span data-stu-id="20790-117">You should select ASP.NET Core 2.0 or later.</span></span>

1. <span data-ttu-id="20790-118">Sie verfügen nun über eine neue Projektmappe für eine ASP.NET Core-Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="20790-118">You should now have your new ASP.NET Core web application solution.</span></span>

    ![Dialogfeld „Neues Projekt“](../media-draft/3-new-solution.png)

### <a name="visual-studio-mac"></a><span data-ttu-id="20790-120">Visual Studio für Mac</span><span class="sxs-lookup"><span data-stu-id="20790-120">Visual Studio Mac</span></span>

1. <span data-ttu-id="20790-121">Klicken Sie auf der Startseite von Visual Studio auf **Datei** und anschließend auf **Neu** > **Projekt...**.</span><span class="sxs-lookup"><span data-stu-id="20790-121">On the Visual Studio start page, select **File**, then click **New**, and then click **Project..**.</span></span>

1. <span data-ttu-id="20790-122">Wählen Sie unter **.NET Core** eine **ASP.NET Core-Web-App** aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="20790-122">Under .**NET Core**, select an **ASP.NET Core Web App**, and then click **Next**.</span></span>

1. <span data-ttu-id="20790-123">Geben Sie unter **Projektname** die Zeichenfolge **AlpineSkiHouse** ein.</span><span class="sxs-lookup"><span data-stu-id="20790-123">For the **Project Name**, type **AlpineSkiHouse**.</span></span> <span data-ttu-id="20790-124">Damit sollte auch der Projektmappenname automatisch aufgefüllt werden.</span><span class="sxs-lookup"><span data-stu-id="20790-124">This should also auto-populate the solution name.</span></span>

1. <span data-ttu-id="20790-125">Wählen Sie für das Projekt einen **Speicherort** auf Ihrem lokalen Computer aus.</span><span class="sxs-lookup"><span data-stu-id="20790-125">Select a **location** on your local machine for the project.</span></span>

1. <span data-ttu-id="20790-126">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="20790-126">Click **Create**.</span></span>

## <a name="build-and-test-on-your-local-machine"></a><span data-ttu-id="20790-127">Erstellen und Testen auf dem lokalen Computer</span><span class="sxs-lookup"><span data-stu-id="20790-127">Build and test on your local machine</span></span>

<span data-ttu-id="20790-128">Nun erstellen und testen Sie das neue Projekt auf dem lokalen Computer, um vor der Bereitstellung in Azure sicherzustellen, dass es lokal erstellt und bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="20790-128">Now, let's build and test your new project on your local machine to ensure it builds and deploys locally before deploying to Azure.</span></span>

1. <span data-ttu-id="20790-129">Drücken Sie **F5**, um die App im Debugmodus auszuführen, oder **STRG+F5**, um sie ohne Debugger auszuführen.</span><span class="sxs-lookup"><span data-stu-id="20790-129">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger.</span></span>

    ![Dialogfeld „Neues Projekt“](../media-draft/3-webapp-launch.png)

<span data-ttu-id="20790-131">Visual Studio startet IIS Express und führt die App aus.</span><span class="sxs-lookup"><span data-stu-id="20790-131">Visual Studio starts IIS Express and runs the app.</span></span> <span data-ttu-id="20790-132">Wenn Visual Studio ein Webprojekt erstellt, wird ein nach dem Zufallsprinzip ausgewählter Port für den Webserver verwendet.</span><span class="sxs-lookup"><span data-stu-id="20790-132">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="20790-133">In der vorherigen Abbildung wird die Portnummer 44381 verwendet.</span><span class="sxs-lookup"><span data-stu-id="20790-133">In the preceding image, the port number is 44381.</span></span> <span data-ttu-id="20790-134">Wenn Sie die App ausführen, wird wahrscheinlich eine andere Portnummer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="20790-134">When you run the app, you'll likely see a different port number.</span></span>

> [!TIP]
> <span data-ttu-id="20790-135">Wenn Sie die App mit **STRG+F5** (Modus oder Debugger) starten, können Sie Codeänderungen vornehmen, die Datei speichern, den Browser aktualisieren und die Codeänderungen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="20790-135">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="20790-136">Viele Entwickler bevorzugen den Modus ohne Debugger, um die App schnell starten und Änderungen anzeigen zu können.</span><span class="sxs-lookup"><span data-stu-id="20790-136">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20790-137">Vielleicht ist Ihnen der Abschnitt am oberen Rand der Webseite aufgefallen, der für Ihre Datenschutz- und Cookienutzungsrichtlinie vorgesehen ist.</span><span class="sxs-lookup"><span data-stu-id="20790-137">You might notice the section at the top of the web page that provides a place for your privacy and cookie use policy.</span></span> <span data-ttu-id="20790-138">Klicken Sie auf **Akzeptieren**, um der Nachverfolgung zuzustimmen.</span><span class="sxs-lookup"><span data-stu-id="20790-138">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="20790-139">Diese App verfolgt keine persönlichen Informationen nach.</span><span class="sxs-lookup"><span data-stu-id="20790-139">This app doesn't track personal information.</span></span> <span data-ttu-id="20790-140">Der vorlagengenerierte Code enthält Ressourcen zur Einhaltung der Datenschutz-Grundverordnung (DSGVO).</span><span class="sxs-lookup"><span data-stu-id="20790-140">The template-generated code includes assets to help meet General Data Protection Regulation (GDPR).</span></span>

## <a name="summary"></a><span data-ttu-id="20790-141">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="20790-141">Summary</span></span>

<span data-ttu-id="20790-142">Im ersten Einrichtungsschritt wird Ihre ASP.NET-Website erstellt und lokal ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="20790-142">The first step to getting your ASP.NET site up and running is to create it and run it locally.</span></span> <span data-ttu-id="20790-143">Nachdem Sie Ihre Website nun erstellt haben, können Sie sie in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="20790-143">Now that your site is created, you are ready to deploy it to Azure.</span></span>
