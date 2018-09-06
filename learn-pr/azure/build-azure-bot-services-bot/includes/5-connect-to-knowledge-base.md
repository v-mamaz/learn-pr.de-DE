### <a name="exercise-5-connect-the-bot-to-the-knowledge-base"></a><span data-ttu-id="a30e3-101">Übung 5: Herstellen einer Verbindung zwischen dem Bot und der Wissensdatenbank</span><span class="sxs-lookup"><span data-stu-id="a30e3-101">Exercise 5: Connect the bot to the knowledge base</span></span>

<span data-ttu-id="a30e3-102">In dieser Übung stellen Sie eine Verbindung Ihres Bots mit der QnA Maker-Wissensdatenbank her, die Sie zuvor erstellt haben, damit der Bot weiterhin intelligente Konversation betreiben kann.</span><span class="sxs-lookup"><span data-stu-id="a30e3-102">In this exercise, you will connect your bot to the QnA Maker knowledge base you built earlier so the bot can carry on an intelligent conversation.</span></span> <span data-ttu-id="a30e3-103">Das Herstellen einer Verbindung mit der Wissensdatenbank ist mit dem Abrufen einiger Informationen aus dem QnA Maker-Portal, deren Kopieren in das Azure-Portal, dem Aktualisieren des Botcodes und dann dem erneuten Bereitstellen des Bots verbunden.</span><span class="sxs-lookup"><span data-stu-id="a30e3-103">Connecting to the knowledge base involves retrieving some information from the QnA Maker portal, copying it into the Azure portal, updating the bot code, and then redeploying the bot to Azure.</span></span>

1. <span data-ttu-id="a30e3-104">Kehren Sie zum [QnA Maker-Portal](https://www.qnamaker.ai/) zurück, und klicken Sie in der oberen rechten Ecke auf Ihren Namen.</span><span class="sxs-lookup"><span data-stu-id="a30e3-104">Return to the [QnA Maker portal](https://www.qnamaker.ai/) and click your name in the upper-right corner.</span></span> <span data-ttu-id="a30e3-105">Wählen Sie im dann angezeigten Dropdownmenü **Endpunktschlüssel verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="a30e3-105">Select **Manage endpoint keys** from the menu that drops down.</span></span> <span data-ttu-id="a30e3-106">Klicken Sie auf **Anzeigen**, um den primären Endpunktschlüssel anzuzeigen, und **Kopieren**, um ihn in die Zwischenablage zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="a30e3-106">Click **Show** to show the primary endpoint key, and **Copy** to copy it to the clipboard.</span></span> <span data-ttu-id="a30e3-107">Fügen Sie ihn dann in eine Textdatei ein, damit Sie ihn in Kürze problemlos abrufen können.</span><span class="sxs-lookup"><span data-stu-id="a30e3-107">Then paste it into a text file so you can easily retrieve it in a moment.</span></span>

    ![Kopieren des Endpunktschlüssels](../images/copy-primary-key.png)
    
    <span data-ttu-id="a30e3-109">_Kopieren des Endpunktschlüssels_</span><span class="sxs-lookup"><span data-stu-id="a30e3-109">_Copying the endpoint key_</span></span> 

1. <span data-ttu-id="a30e3-110">Klicken Sie im Menü am oberen Rand der Seite auf **Meine Wissensdatenbanken**.</span><span class="sxs-lookup"><span data-stu-id="a30e3-110">Click **My knowledge bases** in the menu at the top of the page.</span></span> <span data-ttu-id="a30e3-111">Klicken Sie dann für die Wissensdatenbank, die Sie zuvor erstellt haben, auf **Code anzeigen**.</span><span class="sxs-lookup"><span data-stu-id="a30e3-111">Then click **View Code** for the knowledge base that you created earlier.</span></span>

    ![Öffnen der Wissensdatenbank](../images/open-knowledge-base.png)

    <span data-ttu-id="a30e3-113">_Öffnen der Wissensdatenbank_</span><span class="sxs-lookup"><span data-stu-id="a30e3-113">_Opening the knowledge base_</span></span>

1. <span data-ttu-id="a30e3-114">Kopieren Sie die Wissensdatenbank-ID aus der ersten Zeile und den Hostnamen aus der zweiten Zeile, und fügen Sie sie ebenfalls in eine Textdatei ein.</span><span class="sxs-lookup"><span data-stu-id="a30e3-114">Copy the knowledge base ID from the first line and the host name from the second line and paste them into a text file as well.</span></span> <span data-ttu-id="a30e3-115">Schließen Sie dann das Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="a30e3-115">Then close the dialog.</span></span> <span data-ttu-id="a30e3-116">Beziehen Sie das Präfix „https://“ **nicht** in den Hostnamen ein, den Sie kopieren.</span><span class="sxs-lookup"><span data-stu-id="a30e3-116">**Do not** include the "https://" prefix in the host name that you copy.</span></span>

    ![Kopieren von Wissensdatenbank-ID und Hostostnamen](../images/copy-endpoint-info.png)
    
    <span data-ttu-id="a30e3-118">_Kopieren von Wissensdatenbank-ID und Hostostnamen_</span><span class="sxs-lookup"><span data-stu-id="a30e3-118">_Copying the knowledge base ID and host name_</span></span>  

1. <span data-ttu-id="a30e3-119">Kehren Sie zum Web-App-Bot im Azure-Portal zurück.</span><span class="sxs-lookup"><span data-stu-id="a30e3-119">Return to the Web App Bot in the Azure portal.</span></span> <span data-ttu-id="a30e3-120">Klicken Sie im Menü links auf **Anwendungseinstellungen**, und scrollen Sie nach unten, bis Sie die Anwendungseinstellungen „QnAKnowledgebaseId“, „QnAAuthKey“ und „QnAEndpointHostName“ finden.</span><span class="sxs-lookup"><span data-stu-id="a30e3-120">Click **Application settings** in the menu on the left and scroll down until you find application settings named "QnAKnowledgebaseId," "QnAAuthKey,", and "QnAEndpointHostName."</span></span> <span data-ttu-id="a30e3-121">Fügen Sie die Wissensdatenbank-ID und den Hostnamen, die Sie in Schritt 3, und den Endpunktschlüssel, den Sie in Schritt 1 abgerufen haben, in diese Felder ein.</span><span class="sxs-lookup"><span data-stu-id="a30e3-121">Paste the knowledge base ID and host name obtained in Step 3 and the endpoint key obtained in Step 1 into these fields.</span></span> <span data-ttu-id="a30e3-122">Klicken Sie anschließend auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="a30e3-122">Then click **Save**.</span></span>

    ![Bearbeiten von Anwendungseinstellungen](../images/enter-app-settings.png)

    <span data-ttu-id="a30e3-124">_Bearbeiten von Anwendungseinstellungen_</span><span class="sxs-lookup"><span data-stu-id="a30e3-124">_Editing application settings_</span></span> 
 
1. <span data-ttu-id="a30e3-125">Kehren Sie zu Visual Studio Code zurück, und ersetzen Sie den Inhalt von **app.js** durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="a30e3-125">Return to Visual Studio Code and replace the contents of **app.js** with the code below.</span></span> <span data-ttu-id="a30e3-126">Speichern Sie dann die Datei.</span><span class="sxs-lookup"><span data-stu-id="a30e3-126">Then save the file.</span></span>

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

    <span data-ttu-id="a30e3-127">Beachten Sie den Aufruf zum Erstellen einer ```QnAMakerDialog```-Instanz in Zeile 30.</span><span class="sxs-lookup"><span data-stu-id="a30e3-127">Note the call to create a ```QnAMakerDialog``` instance on line 30.</span></span> <span data-ttu-id="a30e3-128">Dadurch wird ein Dialog erstellt, der einen mit dem Azure Bot Service erstellten Bot in eine mit Microsoft QnA Maker erstellte Wissensdatenbank integriert.</span><span class="sxs-lookup"><span data-stu-id="a30e3-128">This creates a dialog that integrates a bot built with the Azure Bot Service with a knowledge base built Microsoft QnA Maker.</span></span>
 
1. <span data-ttu-id="a30e3-129">Klicken Sie in Visual Studio Code in der Aktivitätsleiste auf die **Quellcodeverwaltung**-Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="a30e3-129">Click the **Source Control** button in the activity bar in Visual Studio Code.</span></span> <span data-ttu-id="a30e3-130">Geben Sie „Connected to knowledge base“ (Mit der Wissensdatenbank verbunden) in das Nachrichtenfeld ein, und klicken Sie dann auf das Häkchen, um Ihre Änderungen zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="a30e3-130">Type "Connected to knowledge base" into the message box, and click the check mark to commit your changes.</span></span> <span data-ttu-id="a30e3-131">Klicken Sie anschließend auf die Auslassungspunkte, und pushen Sie diese Änderungen mit dem **Branch veröffentlichen**-Befehl in das Remoterepository (und somit auch in die Azure-Web-App).</span><span class="sxs-lookup"><span data-stu-id="a30e3-131">Then click the ellipsis and use the **Publish Branch** command to push these changes to the remote repository (and therefore to the Azure Web App).</span></span>

1. <span data-ttu-id="a30e3-132">Kehren Sie zum Web-App-Bot im Azure-Portal zurück, und klicken Sie auf der linken Seite auf **Testen im Web Chat**, um die Testkonsole zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="a30e3-132">Return to the Web App Bot in the Azure portal and click **Test in Web Chat** on the left to open the test console.</span></span> <span data-ttu-id="a30e3-133">Geben Sie „What's the most popular software programming language in the world?“ (Was ist die weltweit am häufigsten verwendete Programmiersprache?)</span><span class="sxs-lookup"><span data-stu-id="a30e3-133">Type "What's the most popular software programming language in the world?"</span></span> <span data-ttu-id="a30e3-134">in das Feld am unteren Rand des Chatfensters ein, und drücken Sie die **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="a30e3-134">into the box at the bottom of the chat window and press **Enter**.</span></span> <span data-ttu-id="a30e3-135">Vergewissern Sie sich, dass der Bot wie folgt reagiert:</span><span class="sxs-lookup"><span data-stu-id="a30e3-135">Confirm that the bot responds as follows:</span></span>

    ![Testen des Bots](../images/portal-testing-chat.png)

    <span data-ttu-id="a30e3-137">_Testen des Bots_</span><span class="sxs-lookup"><span data-stu-id="a30e3-137">_Testing the bot_</span></span>

<span data-ttu-id="a30e3-138">Da der Bot nun mit der Wissensdatenbank verbunden ist, besteht der letzte Schritt im Praxistest.</span><span class="sxs-lookup"><span data-stu-id="a30e3-138">Now that the bot is connected to the knowledge base, the final step is to test it in the wild.</span></span> <span data-ttu-id="a30e3-139">Und was könnte praktischer sein als ein Test mit Skype?</span><span class="sxs-lookup"><span data-stu-id="a30e3-139">And what could be wilder than testing it with Skype?</span></span>