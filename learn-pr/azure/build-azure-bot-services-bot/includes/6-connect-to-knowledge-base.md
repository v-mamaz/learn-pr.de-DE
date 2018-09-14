<span data-ttu-id="cecab-101">In dieser Einheit stellen Sie eine Verbindung Ihres Bots mit der QnA Maker-Wissensdatenbank her, die Sie zuvor erstellt haben, damit der Bot weiterhin intelligente Konversation betreiben kann.</span><span class="sxs-lookup"><span data-stu-id="cecab-101">In this unit, you will connect your bot to the QnA Maker knowledge base you built earlier so the bot can carry on an intelligent conversation.</span></span> <span data-ttu-id="cecab-102">Das Herstellen einer Verbindung mit der Wissensdatenbank ist mit dem Abrufen einiger Informationen aus dem QnA Maker-Portal, deren Kopieren in das Azure-Portal, dem Aktualisieren des Botcodes und dann dem erneuten Bereitstellen des Bots verbunden.</span><span class="sxs-lookup"><span data-stu-id="cecab-102">Connecting to the knowledge base involves retrieving some information from the QnA Maker portal, copying it into the Azure portal, updating the bot code, and then redeploying the bot to Azure.</span></span>

1. <span data-ttu-id="cecab-103">Kehren Sie zum [QnA Maker-Portal](https://www.qnamaker.ai/) zurück, und klicken Sie in der oberen rechten Ecke auf Ihren Namen.</span><span class="sxs-lookup"><span data-stu-id="cecab-103">Return to the [QnA Maker portal](https://www.qnamaker.ai/) and click your name in the upper-right corner.</span></span> <span data-ttu-id="cecab-104">Wählen Sie im dann angezeigten Dropdownmenü **Endpunktschlüssel verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="cecab-104">Select **Manage endpoint keys** from the menu that drops down.</span></span> <span data-ttu-id="cecab-105">Klicken Sie auf **Anzeigen**, um den primären Endpunktschlüssel anzuzeigen, und **Kopieren**, um ihn in die Zwischenablage zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="cecab-105">Click **Show** to show the primary endpoint key, and **Copy** to copy it to the clipboard.</span></span> <span data-ttu-id="cecab-106">Fügen Sie ihn dann in eine Textdatei ein, damit Sie ihn in Kürze problemlos abrufen können.</span><span class="sxs-lookup"><span data-stu-id="cecab-106">Then, paste it into a text file so you can easily retrieve it in a moment.</span></span>

    ![Kopieren des Endpunktschlüssels](../media-draft/6-copy-primary-key.png)

1. <span data-ttu-id="cecab-108">Klicken Sie im Menü am oberen Rand der Seite auf **Meine Wissensdatenbanken**.</span><span class="sxs-lookup"><span data-stu-id="cecab-108">Click **My knowledge bases** in the menu at the top of the page.</span></span> <span data-ttu-id="cecab-109">Klicken Sie dann für die Wissensdatenbank, die Sie zuvor erstellt haben, auf **Code anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="cecab-109">Then, click **View Code** for the knowledge base that you created earlier.</span></span>

    ![Öffnen der Wissensdatenbank](../media-draft/6-open-knowledge-base.png)

1. <span data-ttu-id="cecab-111">Kopieren Sie die Wissensdatenbank-ID aus der ersten Zeile und den Hostnamen aus der zweiten Zeile.</span><span class="sxs-lookup"><span data-stu-id="cecab-111">Copy the knowledge base ID from the first line and the host name from the second line.</span></span> <span data-ttu-id="cecab-112">Fügen Sie beide ebenfalls in eine Textdatei ein.</span><span class="sxs-lookup"><span data-stu-id="cecab-112">Paste them into a text file, as well.</span></span> <span data-ttu-id="cecab-113">Schließen Sie dann das Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="cecab-113">Then, close the dialog.</span></span> <span data-ttu-id="cecab-114">Beziehen Sie das Präfix „https://“ **nicht** in den Hostnamen ein, den Sie kopieren.</span><span class="sxs-lookup"><span data-stu-id="cecab-114">**Do not** include the "https://" prefix in the host name that you copy.</span></span>

    ![Kopieren von Wissensdatenbank-ID und Hostnamen](../media-draft/6-copy-endpoint-info.png)  

1. <span data-ttu-id="cecab-116">Kehren Sie zum Web-App-Bot im Azure-Portal zurück.</span><span class="sxs-lookup"><span data-stu-id="cecab-116">Return to the web app bot in the Azure portal.</span></span> <span data-ttu-id="cecab-117">Klicken Sie im Menü links auf **Anwendungseinstellungen**, und scrollen Sie nach unten zu den Anwendungseinstellungen „QnAKnowledgebaseId“, „QnAAuthKey“ und „QnAEndpointHostName“.</span><span class="sxs-lookup"><span data-stu-id="cecab-117">Click **Application settings** in the menu on the left and scroll down until you find application settings named "QnAKnowledgebaseId," "QnAAuthKey," and "QnAEndpointHostName."</span></span> <span data-ttu-id="cecab-118">Fügen Sie die Wissensdatenbank-ID und den Hostnamen, die Sie in Schritt 3, und den Endpunktschlüssel, den Sie in Schritt 1 abgerufen haben, in diese Felder ein.</span><span class="sxs-lookup"><span data-stu-id="cecab-118">Paste the knowledge base ID and host name obtained in Step 3 and the endpoint key obtained in Step 1 into these fields.</span></span> <span data-ttu-id="cecab-119">Klicken Sie dann auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="cecab-119">Then, click **Save**.</span></span>

    ![Bearbeiten von Anwendungseinstellungen](../media-draft/6-enter-app-settings.png)

1. <span data-ttu-id="cecab-121">Kehren Sie zu Visual Studio Code zurück, und ersetzen Sie den Inhalt von **app.js** durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="cecab-121">Return to Visual Studio Code and replace the contents of **app.js** with the code below.</span></span> <span data-ttu-id="cecab-122">Speichern Sie dann die Datei.</span><span class="sxs-lookup"><span data-stu-id="cecab-122">Then, save the file.</span></span>

    ```JavaScript
    var restify = require('restify');
    var builder = require('botbuilder');
    var botbuilder_azure = require("botbuilder-azure");
    var builder_cognitiveservices = require("botbuilder-cognitiveservices");
    
    // Setup Restify Server
    var server = restify.createServer();
    server.listen(process.env.port || process.env.PORT || 3978, function () {
       console.log('%s listening to %s', server.name, server.url); 
    });
      
    // Create chat connector for communicating with the Bot Framework Service
    var connector = new builder.ChatConnector({
        appId: process.env.MicrosoftAppId,
        appPassword: process.env.MicrosoftAppPassword     
    });
    
    // Listen for messages from users 
    server.post('/api/messages', connector.listen());
     
    // Create your bot with a function to receive messages from the user
    var bot = new builder.UniversalBot(connector);
    
    var recognizer = new builder_cognitiveservices.QnAMakerRecognizer({
        knowledgeBaseId: process.env.QnAKnowledgebaseId, 
        authKey: process.env.QnAAuthKey,
        endpointHostName: process.env.QnAEndpointHostName
    });
    
    var basicQnAMakerDialog = new builder_cognitiveservices.QnAMakerDialog({
        recognizers: [recognizer],
        defaultMessage: "I'm not quite sure what you're asking. Please ask your question again.",
        qnaThreshold: 0.3
    });
    
    bot.dialog('basicQnAMakerDialog', basicQnAMakerDialog);
    
    bot.dialog('/',
    [
        function (session) {
            session.replaceDialog('basicQnAMakerDialog');
        }
    ]);
    ```

    <span data-ttu-id="cecab-123">Beachten Sie den Aufruf zum Erstellen einer `QnAMakerDialog`-Instanz in Zeile 30.</span><span class="sxs-lookup"><span data-stu-id="cecab-123">Note the call to create a `QnAMakerDialog` instance on line 30.</span></span> <span data-ttu-id="cecab-124">Dadurch wird ein Dialog erstellt, der einen mit dem Azure Bot Service erstellten Bot in eine mit Microsoft QnA Maker erstellte Wissensdatenbank integriert.</span><span class="sxs-lookup"><span data-stu-id="cecab-124">This creates a dialog that integrates a bot built with the Azure Bot Service with a knowledge base built Microsoft QnA Maker.</span></span>
 
1. <span data-ttu-id="cecab-125">Klicken Sie in Visual Studio Code in der Aktivitätsleiste auf die **Quellcodeverwaltung**-Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="cecab-125">Click the **Source Control** button in the activity bar in Visual Studio Code.</span></span> <span data-ttu-id="cecab-126">Geben Sie „Connected to knowledge base“ (Mit der Wissensdatenbank verbunden) in das Nachrichtenfeld ein, und klicken Sie dann auf das Häkchen, um Ihre Änderungen zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="cecab-126">Type "Connected to knowledge base" into the message box, and click the check mark to commit your changes.</span></span> <span data-ttu-id="cecab-127">Klicken Sie anschließend auf die Auslassungspunkte, und pushen Sie diese Änderungen mit dem **Branch veröffentlichen**-Befehl in das Remoterepository (und somit </span><span class="sxs-lookup"><span data-stu-id="cecab-127">Then, click the ellipsis and use the **Publish Branch** command to push these changes to the remote repository (and therefore.</span></span> <span data-ttu-id="cecab-128">auch in die Azure-Web-App).</span><span class="sxs-lookup"><span data-stu-id="cecab-128">to the Azure Web App).</span></span>

1. <span data-ttu-id="cecab-129">Kehren Sie zum Web-App-Bot im Azure-Portal zurück, und klicken Sie auf der linken Seite auf **Testen im Web Chat**, um die Testkonsole zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="cecab-129">Return to the web app bot in the Azure portal and click **Test in Web Chat** on the left to open the test console.</span></span> <span data-ttu-id="cecab-130">Geben Sie „What's the most popular software programming language in the world?“ (Was ist die weltweit am häufigsten verwendete Programmiersprache?)</span><span class="sxs-lookup"><span data-stu-id="cecab-130">Type "What's the most popular software programming language in the world?"</span></span> <span data-ttu-id="cecab-131">in das Feld am unteren Rand des Chatfensters ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="cecab-131">into the box at the bottom of the chat window and press **Enter**.</span></span> <span data-ttu-id="cecab-132">Vergewissern Sie sich, dass der Bot wie folgt reagiert:</span><span class="sxs-lookup"><span data-stu-id="cecab-132">Confirm that the bot responds as follows:</span></span>

    ![Testen des Bots](../media-draft/6-portal-testing-chat.png)

<span data-ttu-id="cecab-134">Da der Bot nun mit der Wissensdatenbank verbunden ist, besteht der letzte Schritt im Praxistest.</span><span class="sxs-lookup"><span data-stu-id="cecab-134">Now that the bot is connected to the knowledge base, the final step is to test it in the wild.</span></span> <span data-ttu-id="cecab-135">Und was könnte praktischer sein als ein Test mit Skype?</span><span class="sxs-lookup"><span data-stu-id="cecab-135">And what could be wilder than testing it with Skype?</span></span>