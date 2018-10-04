[!INCLUDE [0-vm-note](0-vm-note.md)]

In dieser Einheit stellen Sie eine Verbindung zwischen Ihrem Bot und der QnA Maker-Wissensdatenbank her, die Sie zuvor erstellt haben, damit der Bot weiterhin intelligente Konversation betreiben kann. Das Herstellen einer Verbindung mit der Wissensdatenbank ist mit dem Abrufen einiger Informationen aus dem QnA Maker-Portal, deren Kopieren in das Azure-Portal, dem Aktualisieren des Botcodes und dann dem erneuten Bereitstellen des Bots verbunden.

1. Kehren Sie zum QnA Maker-Portal unter https://www.qnamaker.ai im VM-Browser zurück, und klicken Sie auf die Schaltfläche „Konto“ in der oberen rechten Ecke.
1. Wählen Sie im dann angezeigten Dropdownmenü **Endpunktschlüssel verwalten** aus.
1. Klicken Sie auf **Anzeigen**, um den **primären** Endpunktschlüssel anzuzeigen, und **Kopieren**, um ihn in die Zwischenablage zu kopieren. Fügen Sie ihn in eine Textdatei ein, damit Sie ihn in Kürze problemlos abrufen können.

    > [!NOTE]
    > Sie müssen abhängig von Ihren Browsereinstellungen möglicherweise Cookies von Drittanbietern zulassen, um diese Einheit durchführen zu können.

1. Klicken Sie im Menü am oberen Rand der Seite auf **Meine Wissensdatenbanken**.
1. Klicken Sie dann für die Wissensdatenbank, die Sie zuvor erstellt haben, auf **Code anzeigen**.

1. Kopieren Sie die Wissensdatenbank-ID aus der ersten Zeile und den Hostnamen aus der zweiten Zeile. Fügen Sie beide ebenfalls in eine Textdatei ein. Schließen Sie dann das Dialogfeld. Beziehen Sie das Präfix „https://“ **nicht** in den Hostnamen ein, den Sie kopieren.

    ![Screenshot des QnA Maker-Portals mit der HTTP-Beispielanforderung mit Hervorhebung der Wissensdatenbank-ID des Endpunkts und des Hostnamens.](../media/6-copy-endpoint-info.png)

1. Kehren Sie zum Web-App-Bot im Azure-Portal zurück. Klicken Sie im Menü links auf **Anwendungseinstellungen**, und scrollen Sie nach unten zu den Anwendungseinstellungen „QnAKnowledgebaseId“, „QnAAuthKey“ und „QnAEndpointHostName“. Fügen Sie die Wissensdatenbank-ID, den Hostnamen und den Endpunktschlüssel, die bzw. den Sie zuvor erhalten haben, in diese Felder ein. Klicken Sie anschließend oben auf **Speichern**.

    ![Screenshot des Azure-Portals mit dem Blatt „Bot“ und Details zu Anwendungseinstellungen mit Hervorhebung des Menüelements „Anwendungseinstellungen“ und der entsprechenden Einstellungsschlüssel.](../media/6-enter-app-settings.png)

1. Kehren Sie zu **Visual Studio Code** zurück, und ersetzen Sie den Inhalt von **app.js** durch den folgenden Code. Speichern Sie dann die Datei.

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
        appPassword: process.env.MicrosoftAppPassword,
        openIdMetadata: process.env.BotOpenIdMetadata
    });

    // Listen for messages from users
    server.post('/api/messages', connector.listen());

    var tableName = 'botdata';
    var azureTableClient = new botbuilder_azure.AzureTableClient(tableName, process.env['AzureWebJobsStorage']);
    var tableStorage = new botbuilder_azure.AzureBotStorage({ gzipData: false }, azureTableClient);

    // Create your bot with a function to receive messages from the user
    var bot = new builder.UniversalBot(connector);
    bot.set('storage', tableStorage);

    // Recognizer and and Dialog for preview QnAMaker service
    var previewRecognizer = new builder_cognitiveservices.QnAMakerRecognizer({
        knowledgeBaseId: process.env.QnAKnowledgebaseId,
        authKey: process.env.QnAAuthKey || process.env.QnASubscriptionKey
    });

    var basicQnAMakerPreviewDialog = new builder_cognitiveservices.QnAMakerDialog({
        recognizers: [previewRecognizer],
        defaultMessage: 'No match! Try changing the query terms!',
        qnaThreshold: 0.3
    }
    );

    bot.dialog('basicQnAMakerPreviewDialog', basicQnAMakerPreviewDialog);

    // Recognizer and and Dialog for GA QnAMaker service
    var recognizer = new builder_cognitiveservices.QnAMakerRecognizer({
        knowledgeBaseId: process.env.QnAKnowledgebaseId,
        authKey: process.env.QnAAuthKey || process.env.QnASubscriptionKey, // Backward compatibility with QnAMaker (Preview)
        endpointHostName: process.env.QnAEndpointHostName
    });

    var basicQnAMakerDialog = new builder_cognitiveservices.QnAMakerDialog({
        recognizers: [recognizer],
        defaultMessage: "I'm not quite sure what you're asking. Please ask your question again.",
        qnaThreshold: 0.3
    });

    bot.dialog('basicQnAMakerDialog', basicQnAMakerDialog);

    bot.dialog('/', //basicQnAMakerDialog);
        [
            function (session) {
                var qnaKnowledgebaseId = process.env.QnAKnowledgebaseId;
                var qnaAuthKey = process.env.QnAAuthKey || process.env.QnASubscriptionKey;
                var endpointHostName = process.env.QnAEndpointHostName;

                // QnA Subscription Key and KnowledgeBase Id null verification
                if ((qnaAuthKey == null || qnaAuthKey == '') || (qnaKnowledgebaseId == null || qnaKnowledgebaseId == ''))
                    session.send('Please set QnAKnowledgebaseId, QnAAuthKey and QnAEndpointHostName (if applicable) in App Settings. Learn how to get them at https://aka.ms/qnaabssetup.');
                else {
                    if (endpointHostName == null || endpointHostName == '')
                        // Replace with Preview QnAMakerDialog service
                        session.replaceDialog('basicQnAMakerPreviewDialog');
                    else
                        // Replace with GA QnAMakerDialog service
                        session.replaceDialog('basicQnAMakerDialog');
                }
            }
        ]);
    ```

    > [!NOTE]
    > Beachten Sie den Aufruf zum Erstellen einer `QnAMakerDialog`-Instanz in Zeile 30. Dadurch wird ein Dialogfeld erstellt, das einen mit dem Azure Bot Service erstellten Bot in eine über Microsoft QnA Maker erstellte Wissensdatenbank integriert.

1. Klicken Sie in Visual Studio Code in der Aktivitätsleiste auf die Schaltfläche **Quellcodeverwaltung**.
1. Zeigen Sie mit der Maus auf die Datei **app.js**, und wählen Sie die Schaltfläche __+__ aus, um die Dateiänderungen für den nächsten Commit bereitzustellen.
1. Geben Sie „Connected to knowledge base“ (Mit der Wissensdatenbank verbunden) in das Nachrichtenfeld ein, und klicken Sie dann auf das Häkchen, um Ihre Änderungen zu übernehmen.

    > [!Warning]
    > Wenn Sie Änderungen an einer **package.json**-Datei sehen, stellen Sie sicher, dass Sie diese NICHT in Ihren Commit einbeziehen. Ihr Commit darf nur Ihre Änderungen für **app.js** enthalten.

1. Klicken Sie anschließend auf die Schaltfläche mit den Auslassungspunkten (__...__), und pushen Sie diese Änderungen mit **Publish Branch** (Branch veröffentlichen) in das Remoterepository und in die Azure-Web-App.

1. Kehren Sie zum Web-App-Bot im Azure-Portal zurück, und klicken Sie auf der linken Seite auf **Test in Web Chat** (Im Webchat testen), um die Testkonsole zu öffnen. Geben Sie „What's the most popular software programming language in the world?“ (Was ist die weltweit am häufigsten verwendete Programmiersprache?) ein. in das Feld am unteren Rand des Chatfensters ein, und drücken Sie die **EINGABETASTE**. Vergewissern Sie sich, dass der Bot reagiert.

Herzlichen Glückwunsch! Ihr Bot ist mit der Wissensdatenbank verbunden und kann auf Fragen antworten.
