In dieser Einheit stellen Sie eine Verbindung Ihres Bots mit der QnA Maker-Wissensdatenbank her, die Sie zuvor erstellt haben, damit der Bot weiterhin intelligente Konversation betreiben kann. Das Herstellen einer Verbindung mit der Wissensdatenbank ist mit dem Abrufen einiger Informationen aus dem QnA Maker-Portal, deren Kopieren in das Azure-Portal, dem Aktualisieren des Botcodes und dann dem erneuten Bereitstellen des Bots verbunden.

1. Kehren Sie zum [QnA Maker-Portal](https://www.qnamaker.ai/) zurück, und klicken Sie in der oberen rechten Ecke auf Ihren Namen. Wählen Sie im dann angezeigten Dropdownmenü **Endpunktschlüssel verwalten** aus. Klicken Sie auf **Anzeigen**, um den primären Endpunktschlüssel anzuzeigen, und **Kopieren**, um ihn in die Zwischenablage zu kopieren. Fügen Sie ihn dann in eine Textdatei ein, damit Sie ihn in Kürze problemlos abrufen können.

    ![Kopieren des Endpunktschlüssels](../media-draft/6-copy-primary-key.png)

1. Klicken Sie im Menü am oberen Rand der Seite auf **Meine Wissensdatenbanken**. Klicken Sie dann für die Wissensdatenbank, die Sie zuvor erstellt haben, auf **Code anzeigen**.

    ![Öffnen der Wissensdatenbank](../media-draft/6-open-knowledge-base.png)

1. Kopieren Sie die Wissensdatenbank-ID aus der ersten Zeile und den Hostnamen aus der zweiten Zeile. Fügen Sie beide ebenfalls in eine Textdatei ein. Schließen Sie dann das Dialogfeld. Beziehen Sie das Präfix „https://“ **nicht** in den Hostnamen ein, den Sie kopieren.

    ![Kopieren von Wissensdatenbank-ID und Hostnamen](../media-draft/6-copy-endpoint-info.png)  

1. Kehren Sie zum Web-App-Bot im Azure-Portal zurück. Klicken Sie im Menü links auf **Anwendungseinstellungen**, und scrollen Sie nach unten zu den Anwendungseinstellungen „QnAKnowledgebaseId“, „QnAAuthKey“ und „QnAEndpointHostName“. Fügen Sie die Wissensdatenbank-ID und den Hostnamen, die Sie in Schritt 3, und den Endpunktschlüssel, den Sie in Schritt 1 abgerufen haben, in diese Felder ein. Klicken Sie dann auf **Speichern**.

    ![Bearbeiten von Anwendungseinstellungen](../media-draft/6-enter-app-settings.png)

1. Kehren Sie zu Visual Studio Code zurück, und ersetzen Sie den Inhalt von **app.js** durch den folgenden Code. Speichern Sie dann die Datei.

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

    Beachten Sie den Aufruf zum Erstellen einer `QnAMakerDialog`-Instanz in Zeile 30. Dadurch wird ein Dialog erstellt, der einen mit dem Azure Bot Service erstellten Bot in eine mit Microsoft QnA Maker erstellte Wissensdatenbank integriert.
 
1. Klicken Sie in Visual Studio Code in der Aktivitätsleiste auf die **Quellcodeverwaltung**-Schaltfläche. Geben Sie „Connected to knowledge base“ (Mit der Wissensdatenbank verbunden) in das Nachrichtenfeld ein, und klicken Sie dann auf das Häkchen, um Ihre Änderungen zu übernehmen. Klicken Sie anschließend auf die Auslassungspunkte, und pushen Sie diese Änderungen mit dem **Branch veröffentlichen**-Befehl in das Remoterepository (und somit  auch in die Azure-Web-App).

1. Kehren Sie zum Web-App-Bot im Azure-Portal zurück, und klicken Sie auf der linken Seite auf **Testen im Web Chat**, um die Testkonsole zu öffnen. Geben Sie „What's the most popular software programming language in the world?“ (Was ist die weltweit am häufigsten verwendete Programmiersprache?) in das Feld am unteren Rand des Chatfensters ein, und drücken Sie die **EINGABETASTE**. Vergewissern Sie sich, dass der Bot wie folgt reagiert:

    ![Testen des Bots](../media-draft/6-portal-testing-chat.png)

Da der Bot nun mit der Wissensdatenbank verbunden ist, besteht der letzte Schritt im Praxistest. Und was könnte praktischer sein als ein Test mit Skype?