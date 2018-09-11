<span data-ttu-id="361d0-101">Da sich Ihre App nun einsatzbereit auf Ihrem lokalen Computer befindet, kann sie in Azure veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="361d0-101">Now that you've got your app up and running on your local machine, it's time to get it published to Azure.</span></span> 

<span data-ttu-id="361d0-102">In dieser Übung entwerfen und erstellen Sie eine neue ASP.NET-Webanwendung und führen sie auf dem lokalen Computer aus.</span><span class="sxs-lookup"><span data-stu-id="361d0-102">In this exercise, you will create, build, and run a new ASP.NET web application on your local machine.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="361d0-103">Erstellen eines neuen Projekts</span><span class="sxs-lookup"><span data-stu-id="361d0-103">Create a new project</span></span>

### <a name="visual-studio-for-windows"></a><span data-ttu-id="361d0-104">Visual Studio für Windows</span><span class="sxs-lookup"><span data-stu-id="361d0-104">Visual Studio for Windows</span></span>

<span data-ttu-id="361d0-105">Der erste Schritt ist, Visual Studio zu starten und eine lokale ASP.NET Core-Webanwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="361d0-105">The first step is to start Visual Studio and create a local ASP.NET Core web application.</span></span>

1. <span data-ttu-id="361d0-106">Wählen Sie auf der Startseite von Visual Studio **Datei** aus, und klicken Sie dann auf **Neu** und **Projekt...**.</span><span class="sxs-lookup"><span data-stu-id="361d0-106">On the Visual Studio start page, select **File**, then click **New**, and then click **Project..**.</span></span>

1. <span data-ttu-id="361d0-107">Wählen Sie im Dialogfeld **Neues Projekt** im linken Bereich **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="361d0-107">In the **New Project** dialog box, on the left-hand pane, select **Web**.</span></span>

1. <span data-ttu-id="361d0-108">Klicken Sie im mittleren Bereich auf **ASP.NET Core-Webanwendung**.</span><span class="sxs-lookup"><span data-stu-id="361d0-108">In the center pane, click **ASP.NET Core Web Application**.</span></span>

1. <span data-ttu-id="361d0-109">Geben Sie am unteren Rand des Dialogfelds im Feld **Name** als Namen **Alpine Ski House** ein.</span><span class="sxs-lookup"><span data-stu-id="361d0-109">At the bottom of the dialog box, in the **Name** field, enter **Alpine Ski House**.</span></span>

1. <span data-ttu-id="361d0-110">Wählen Sie einen **Speicherort** für die neue Projektmappe aus.</span><span class="sxs-lookup"><span data-stu-id="361d0-110">Select a **Location** for your new solution.</span></span>

1. <span data-ttu-id="361d0-111">Klicken Sie auf die Schaltfläche **OK**, um Ihr Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="361d0-111">Click the **OK** button to create your project.</span></span>

1. <span data-ttu-id="361d0-112">Im Dialogfeld **Neue ASP.NET Core-Webanwendung** wird Ihnen eine Auswahl von Startvorlagen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="361d0-112">In the **New ASP.NET Core Web Application** dialog box, you will see a selection of starting templates.</span></span> <span data-ttu-id="361d0-113">Wählen Sie für diese Übung **Webanwendung** aus, und klicken Sie dann zum Erstellen Ihres Projekts auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="361d0-113">For this exercise, select **Web Application**, and then click **OK** to create your project.</span></span>

    ![Dialogfeld „Neues Projekt“](../media-draft/3-aspnet-templates.png)

    > [!NOTE]
    > <span data-ttu-id="361d0-115">Sie können auch je nach Ihren Webentwicklungsanforderungen verschiedene Startvorlagen in diesem Dialogfeld auswählen.</span><span class="sxs-lookup"><span data-stu-id="361d0-115">You can also select different starting templates in this dialog box depending on your web development requirements.</span></span> <span data-ttu-id="361d0-116">Am oberen Rand des Dialogfelds können Sie auch die ASP.NET Core-Version auswählen.</span><span class="sxs-lookup"><span data-stu-id="361d0-116">At the top of the dialog box, you are also able to select the version of ASP.NET Core.</span></span> <span data-ttu-id="361d0-117">Wählen Sie ASP.NET Core 2.0 oder höher aus.</span><span class="sxs-lookup"><span data-stu-id="361d0-117">You should select ASP.NET Core 2.0 or later.</span></span>

1. <span data-ttu-id="361d0-118">Sie sollten nun über Ihre neue ASP.NET Core-Webanwendungs-Projektmappe verfügen.</span><span class="sxs-lookup"><span data-stu-id="361d0-118">You should now have your new ASP.NET Core web application solution.</span></span>

    ![Dialogfeld „Neues Projekt“](../media-draft/3-new-solution.png)

### <a name="visual-studio-mac"></a><span data-ttu-id="361d0-120">Visual Studio für Mac</span><span class="sxs-lookup"><span data-stu-id="361d0-120">Visual Studio Mac</span></span>

1. <span data-ttu-id="361d0-121">Wählen Sie auf der Startseite von Visual Studio **Datei** aus, und klicken Sie dann auf **Neu** und **Projekt...**.</span><span class="sxs-lookup"><span data-stu-id="361d0-121">On the Visual Studio start page, select **File**, then click **New**, and then click **Project..**.</span></span>

1. <span data-ttu-id="361d0-122">Wählen Sie unter **.NET Core** eine **ASP.NET Core-Web-App** aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="361d0-122">Under .**NET Core**, select an **ASP.NET Core Web App**, and then click **Next**.</span></span>

1. <span data-ttu-id="361d0-123">Geben Sie als **Projektname** **AlpineSkiHouse** ein.</span><span class="sxs-lookup"><span data-stu-id="361d0-123">For the **Project Name**, type **AlpineSkiHouse**.</span></span> <span data-ttu-id="361d0-124">Damit sollte auch der Projektmappenname automatisch aufgefüllt werden.</span><span class="sxs-lookup"><span data-stu-id="361d0-124">This should also autopopulate the solution name.</span></span>

1. <span data-ttu-id="361d0-125">Wählen Sie einen **Speicherort** auf Ihrem lokalen Computer für das Projekt aus.</span><span class="sxs-lookup"><span data-stu-id="361d0-125">Select a **location** on your local machine for the project.</span></span>

1. <span data-ttu-id="361d0-126">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="361d0-126">Click **Create**.</span></span>

## <a name="build-and-test-on-your-local-machine"></a><span data-ttu-id="361d0-127">Erstellen und Testen auf dem lokalen Computer</span><span class="sxs-lookup"><span data-stu-id="361d0-127">Build and test on your local machine</span></span>

<span data-ttu-id="361d0-128">Nun erstellen und testen Sie das neue Projekt auf dem lokalen Computer, um vor der Bereitstellung in Azure sicherzustellen, dass es lokal erstellt und bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="361d0-128">Now, let's build and test your new project on your local machine to ensure it builds and deploys locally before deploying to Azure.</span></span>

1. <span data-ttu-id="361d0-129">Drücken Sie **F5** zum Ausführen der App im Debugmodus oder **STRG + F5** zum Ausführen ohne Anfügen des Debuggers.</span><span class="sxs-lookup"><span data-stu-id="361d0-129">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger.</span></span>

    ![Dialogfeld „Neues Projekt“](../media-draft/3-webapp-launch.png)

<span data-ttu-id="361d0-131">Visual Studio startet IIS Express und führt die App aus.</span><span class="sxs-lookup"><span data-stu-id="361d0-131">Visual Studio starts IIS Express and runs the app.</span></span> <span data-ttu-id="361d0-132">Wenn Visual Studio ein Webprojekt erstellt, wird ein zufälliger Port für den Webserver verwendet.</span><span class="sxs-lookup"><span data-stu-id="361d0-132">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="361d0-133">In der vorherigen Abbildung ist die Portnummer 44381.</span><span class="sxs-lookup"><span data-stu-id="361d0-133">In the preceding image, the port number is 44381.</span></span> <span data-ttu-id="361d0-134">Wenn Sie die App ausführen, wird wahrscheinlich eine andere Portnummer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="361d0-134">When you run the app, you'll likely see a different port number.</span></span>

> [!TIP]
> <span data-ttu-id="361d0-135">Wenn Sie die App mit **STRG + F5** (Nicht-Debugmodus) starten, können Sie Codeänderungen vornehmen, die Datei speichern, den Browser aktualisieren und die Codeänderungen anzeigen.</span><span class="sxs-lookup"><span data-stu-id="361d0-135">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="361d0-136">Viele Entwickler bevorzugen den Nicht-Debugmodus, um die App schnell zu starten und Änderungen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="361d0-136">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="361d0-137">Vielleicht ist Ihnen der Abschnitt am oberen Rand der Webseite aufgefallen, der für Ihre Datenschutz- und Cookienutzungsrichtlinien vorgesehen ist.</span><span class="sxs-lookup"><span data-stu-id="361d0-137">You might notice the section at the top of the web page that provides a place for your privacy and cookie use policy.</span></span> <span data-ttu-id="361d0-138">Wählen Sie **Akzeptieren** aus, um der Nachverfolgung zuzustimmen.</span><span class="sxs-lookup"><span data-stu-id="361d0-138">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="361d0-139">Diese App verfolgt keine persönlichen Informationen nach.</span><span class="sxs-lookup"><span data-stu-id="361d0-139">This app doesn't track personal information.</span></span> <span data-ttu-id="361d0-140">Der vorlagengenerierte Code enthält Ressourcen zur Einhaltung der Datenschutz-Grundverordnung (DSGVO).</span><span class="sxs-lookup"><span data-stu-id="361d0-140">The template-generated code includes assets to help meet General Data Protection Regulation (GDPR).</span></span>

## <a name="summary"></a><span data-ttu-id="361d0-141">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="361d0-141">Summary</span></span>

<span data-ttu-id="361d0-142">Der erste Schritt, Ihre ASP.NET-Website in Betrieb zu nehmen, ist das lokale Erstellen und Ausführen.</span><span class="sxs-lookup"><span data-stu-id="361d0-142">The first step to getting your ASP.NET site up and running is to create it and run it locally.</span></span> <span data-ttu-id="361d0-143">Da Sie Ihre Website nun erstellt haben, können Sie sie in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="361d0-143">Now that your site is created, you are ready to deploy it to Azure.</span></span>
