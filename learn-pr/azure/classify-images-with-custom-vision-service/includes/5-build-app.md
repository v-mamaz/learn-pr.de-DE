<span data-ttu-id="91ee7-101">Die wahre Leistungsstärke von Microsoft Custom Vision Service ist die Leichtigkeit, mit der Entwickler unter Verwendung der [Custom Vision Vorhersage-API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) seine Intelligenz in ihre eigenen Anwendungen integrieren können.</span><span class="sxs-lookup"><span data-stu-id="91ee7-101">The true power of the Microsoft Custom Vision Service is the ease with which developers can incorporate its intelligence into their own applications using the [Custom Vision Prediction API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814).</span></span> <span data-ttu-id="91ee7-102">In dieser Einheit ändern Sie mit Visual Studio Code eine App namens „Artwork“, um das Modell zu verwenden, das Sie in vorhergehenden Übungen erstellt und trainiert haben.</span><span class="sxs-lookup"><span data-stu-id="91ee7-102">In this unit, you will use Visual Studio Code to modify an app named Artwork to use the model you built and trained in previous exercises.</span></span>

1. <span data-ttu-id="91ee7-103">Wenn Node.js nicht auf Ihrem System installiert ist, fahren Sie mit https://nodejs.org fort, und installieren Sie die neueste LTS-Version für Ihr Betriebssystem.</span><span class="sxs-lookup"><span data-stu-id="91ee7-103">If Node.js isn't installed on your system, go to https://nodejs.org and install the latest LTS version for your operating system.</span></span>

   > <span data-ttu-id="91ee7-104">Wenn Sie nicht sicher sind, ob Node.js installiert ist, öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, und geben Sie **node -v** ein.</span><span class="sxs-lookup"><span data-stu-id="91ee7-104">If you aren't sure whether Node.js is installed, open a command prompt or terminal window and type **node -v**.</span></span> <span data-ttu-id="91ee7-105">Wenn Sie keine Node.js-Versionsnummer sehen, ist Node.js nicht installiert.</span><span class="sxs-lookup"><span data-stu-id="91ee7-105">If you don't see a Node.js version number, then Node.js isn't installed.</span></span> <span data-ttu-id="91ee7-106">Wenn eine ältere Version als 6.0 von Node.js installiert ist, sollten Sie unbedingt die neueste Version herunterladen und installieren.</span><span class="sxs-lookup"><span data-stu-id="91ee7-106">If a version of Node.js older than 6.0 is installed, we highly recommend that you download and install the latest version.</span></span>

1. <span data-ttu-id="91ee7-107">Wenn Visual Studio Code nicht auf Ihrer Arbeitsstation installiert ist, fahren Sie mit http://code.visualstudio.com fort, und installieren Sie es jetzt.</span><span class="sxs-lookup"><span data-stu-id="91ee7-107">If Visual Studio Code isn't installed on your workstation, go to http://code.visualstudio.com and install it now.</span></span>

1. <span data-ttu-id="91ee7-108">Starten Sie Visual Studio Code, und wählen Sie **Ordner öffnen...** im Menü **Datei** aus.</span><span class="sxs-lookup"><span data-stu-id="91ee7-108">Start Visual Studio Code and select **Open Folder...** from the **File** menu.</span></span> <span data-ttu-id="91ee7-109">Wählen Sie im folgenden Dialogfeld den in den Modulressourcen enthaltenen Ordner „Client\Artworks“ aus.</span><span class="sxs-lookup"><span data-stu-id="91ee7-109">In the ensuing dialog, select the "Client\Artworks" folder included in the module resources.</span></span>

    ![Auswahl des Ordners „Artworks“](../media/5-fe-select-folder.png)

1. <span data-ttu-id="91ee7-111">Öffnen Sie mit dem Befehl **Ansicht** > **Integriertes Terminal** in Visual Studio Code ein integriertes Terminalfenster.</span><span class="sxs-lookup"><span data-stu-id="91ee7-111">Use the **View** > **Integrated Terminal** command to open an integrated terminal window in Visual Studio Code.</span></span> <span data-ttu-id="91ee7-112">Führen Sie dann den folgenden Befehl in dem integrierten Terminal aus, um die von der App benötigten Pakete zu laden:</span><span class="sxs-lookup"><span data-stu-id="91ee7-112">Then execute the following command in the integrated terminal to load the packages required by the app:</span></span>

    ```console
    npm install
    ```

1. <span data-ttu-id="91ee7-113">Kehren Sie zum Projekt „Artwork“ im Custom Vision Service-Portal zurück, und klicken Sie auf **Leistung** und dann auf **Als Standard festlegen**, um sicherzustellen, dass die aktuelle Iteration des Modells die Standarditeration ist.</span><span class="sxs-lookup"><span data-stu-id="91ee7-113">Return to the Artwork project in the Custom Vision Service portal, click **Performance**, and then click **Make default** to make sure the latest iteration of the model is the default iteration.</span></span>

    ![Angeben der Standarditeration](../media/5-portal-make-default.png)

1. <span data-ttu-id="91ee7-115">Bevor Sie die App ausführen und zum Aufrufen des Custom Vision Service verwenden können, muss sie geändert werden, um Endpunkt- und Autorisierungsschlüsselinformationen einzubeziehen.</span><span class="sxs-lookup"><span data-stu-id="91ee7-115">Before you can run the app and use it to call the Custom Vision Service, it must be modified to include endpoint and authorization information.</span></span> <span data-ttu-id="91ee7-116">Zu diesem Zweck klicken Sie auf **Vorhersage-URL**.</span><span class="sxs-lookup"><span data-stu-id="91ee7-116">To that end, click **Prediction URL**.</span></span>

    ![Anzeigen von Vorhersage-URL-Informationen](../media/5-portal-prediction-url.png)

1. <span data-ttu-id="91ee7-118">Im folgenden Dialogfeld werden zwei URLs aufgelistet: eine für das Hochladen von Bildern über die URL und eine weitere für das Hochladen lokaler Bilder.</span><span class="sxs-lookup"><span data-stu-id="91ee7-118">The ensuing dialog lists two URLs: one for uploading images via URL, and another for uploading local images.</span></span> <span data-ttu-id="91ee7-119">Kopieren Sie die Vorhersage-API-URL für Bilddateien in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="91ee7-119">Copy the Prediction API URL for image files to the clipboard.</span></span>

    ![Kopieren der Vorhersage-API-URL](../media/5-copy-prediction-url.png)

1. <span data-ttu-id="91ee7-121">Kehren Sie zu Visual Studio Code zurück, und klicken Sie auf **predict.js**, um die Datei im Code-Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="91ee7-121">Return to Visual Studio Code and click **predict.js** to open it in the code editor.</span></span>

    ![Öffnen von „predict.js“](../media/5-vs-predict-file.png)

1. <span data-ttu-id="91ee7-123">Ersetzen Sie „PREDICTION_ENDPOINT“ in Zeile 3 durch die URL in der Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="91ee7-123">Replace "PREDICTION_ENDPOINT" in line 3 with the URL on the clipboard.</span></span>

    ![Hinzufügen der Vorhersage-API-URL](../media/5-vs-prediction-endpoint.png)

1. <span data-ttu-id="91ee7-125">Kehren Sie zum Custom Vision Service-Portal zurück, und kopieren Sie den Vorhersage-API-Schlüssel in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="91ee7-125">Return to the Custom Vision Service portal and copy the Prediction API key to the clipboard.</span></span>

    ![Kopieren des Vorhersage-API-Schlüssels](../media/5-copy-prediction-key.png)

1. <span data-ttu-id="91ee7-127">Kehren Sie zu Visual Studio Code zurück, und ersetzen Sie „PREDICTION_KEY“ in Zeile 4 von **predict.js** durch den API-Schlüssel in der Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="91ee7-127">Return to Visual Studio Code and replace "PREDICTION_KEY" in line 4 of **predict.js** with the API key on the clipboard.</span></span>

    ![Hinzufügen des Vorhersage-API-Schlüssels](../media/5-vs-prediction-key.png)

1. <span data-ttu-id="91ee7-129">Scrollen Sie in **predict.js** nach unten, und untersuchen Sie den Codeblock, der in Zeile 34 beginnt.</span><span class="sxs-lookup"><span data-stu-id="91ee7-129">Scroll down in **predict.js** and examine the block of code that begins on line 34.</span></span> <span data-ttu-id="91ee7-130">Dies ist der Code, der mithilfe von AJAX den Custom Vision Service aufruft.</span><span class="sxs-lookup"><span data-stu-id="91ee7-130">This is the code that calls out to the Custom Vision Service using AJAX.</span></span> <span data-ttu-id="91ee7-131">Die Verwendung der Custom Vision-Vorhersage-API ist so einfach wie das Erstellen eines einfachen, authentifizierten POST an einem REST-Endpunkt.</span><span class="sxs-lookup"><span data-stu-id="91ee7-131">Using the Custom Vision Prediction API is as easy as making a simple, authenticated POST to a REST endpoint.</span></span>

    ![Aufruf einer Vorhersage-API](../media/5-vs-code-block.png)

1. <span data-ttu-id="91ee7-133">Kehren Sie zu dem integrierten Terminal in Visual Studio Code zurück, und führen Sie den folgenden Befehl zum Starten der App aus:</span><span class="sxs-lookup"><span data-stu-id="91ee7-133">Return to the integrated terminal in Visual Studio Code and execute the following command to start the app:</span></span>

    ```console
    npm start
    ```

1. <span data-ttu-id="91ee7-134">Vergewissern Sie sich, dass die Artworks-App gestartet wird und ein Fenster wie dieses anzeigt:</span><span class="sxs-lookup"><span data-stu-id="91ee7-134">Confirm that the Artworks app starts and displays a window like this one:</span></span>

    ![Die Artworks-App](../media/5-app-startup.png)

<span data-ttu-id="91ee7-136">„Artworks“ ist eine plattformübergreifende, in Node.js und [Electron](https://electron.atom.io/) geschriebene App.</span><span class="sxs-lookup"><span data-stu-id="91ee7-136">Artworks is a cross-platform app written with Node.js and [Electron](https://electron.atom.io/).</span></span> <span data-ttu-id="91ee7-137">Daher kann sie unter Windows, macOS und Linux ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="91ee7-137">As such, it is equally capable of running on Windows, macOS, and Linux.</span></span> <span data-ttu-id="91ee7-138">In der nächsten Übung verwenden Sie sie, um Bilder nach den Künstlern zu klassifizieren, die sie gemalt haben.</span><span class="sxs-lookup"><span data-stu-id="91ee7-138">In the next exercise, you will use it to classify images by the artists who painted them.</span></span>