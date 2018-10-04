[!INCLUDE [0-vm-note](0-vm-note.md)]

Wie bei jedem von Ihnen geschriebenen Anwendungscode müssen an Botcodes vorgenommene Änderungen lokal getestet und gedebuggt werden, bevor der Anwendungscode in der Produktionsumgebung bereitgestellt wird. Zur Vereinfachung des Debuggens von Bots bietet Microsoft den Bot Framework Emulator. In dieser Einheit lernen Sie, wie Sie Ihre Bots mit Visual Studio Code und dem Emulator debuggen.

1. Führen Sie im integrierten Terminal von Visual Studio Code den folgenden Befehl aus, um [Restify](http://restify.com/) zu installieren. Dies ist ein beliebtes Node.js-Paket zum Erstellen und Nutzen von RESTful-Webdiensten:

    ```bash
    npm install restify
    ```

1. Wiederholen Sie diesen Schritt für die folgenden Befehle, um das [Microsoft Bot Framework Bot Builder SDK für Node.js](https://docs.microsoft.com/bot-framework/nodejs/bot-builder-nodejs-quickstart) zu installieren:

    ```bash
    npm install botbuilder
    npm install botbuilder-azure
    npm install botbuilder-cognitiveservices
    ```

1. Wählen Sie in der Aktivitätsleiste von Visual Studio Code die Schaltfläche **Explorer** aus. 
1. Wählen Sie anschließend **app.js** aus, um die Datei im Code-Editor zu öffnen. Diese Datei enthält den Code, der den Bot steuert – Code, der vom Azure Bot Service generiert und aus dem Azure-Portal heruntergeladen wurde.

1. Ersetzen Sie die Inhalte der Datei **app.js** durch den folgenden Code. Speichern Sie anschließend die Datei.

    ```JavaScript
    "use strict";
    var builder = require("botbuilder");
    var botbuilder_azure = require("botbuilder-azure");

    var useEmulator = true;
    var userName = "";
    var yearsCoding = "";
    var selectedLanguage = "";

    var connector = useEmulator ? new builder.ChatConnector() : new botbuilder_azure.BotServiceConnector({
        appId: process.env.MicrosoftAppId,
        appPassword: process.env.MicrosoftAppPassword
    });

    var bot = new builder.UniversalBot(connector);

    bot.dialog('/', [

    function (session) {
        builder.Prompts.text(session, "Hello, and welcome to QnA Factbot! What's your name?");
    },

    function (session, results) {
        userName = results.response;
        builder.Prompts.number(session, "Hi " + userName + ", how many years have you been writing code?");
    },

    function (session, results) {
        yearsCoding = results.response;
        builder.Prompts.choice(session, "What language do you love the most?", ["C#", "Python", "Node.js", "Visual FoxPro"]);
    },

    function (session, results) {
        selectedLanguage = results.response.entity;

        session.send("Okay, " + userName + ", I think I've got it:" +
            " You've been writing code for " + yearsCoding + " years," +
            " and prefer to use " + selectedLanguage + ".");
    }]);

    var restify = require('restify');
    var server = restify.createServer();

    server.listen(3978, function() {
        console.log('test bot endpoint at http://localhost:3978/api/messages');
    });

    server.post('/api/messages', connector.listen());
    ```

1. Legen Sie für die Zeilen 20, 25 und 30 (`builder.Prompts...`-Aufrufe) Haltepunkte fest, indem Sie diese am Rand auf der linken Seite auswählen.

1. Wählen Sie in der Aktivitätsleiste die Schaltfläche **Debuggen** und anschließend die Schaltfläche mit dem grünen Pfeil (**Debuggen starten**) aus, um eine Debugsitzung zu starten. Überprüfen Sie, ob „Bot-Endpunkt bei http://localhost:3978/api/messages testen“ in der Debugkonsole angezeigt wird.

    ![Screenshot von Visual Studio Code mit dem Debugsystem mit hervorgehobenem Navigationselement „Debuggen“ und der Debug-Wiedergabeschaltfläche, die zum Starten einer Debugsitzung verwendet wird.](../media/5-vs-launch-debugger.png)

    Ihr Botcode wird jetzt lokal ausgeführt.

1. Starten Sie über das Startmenü den **Bot Framework Emulator**.

1. Wählen Sie das Feld **Enter your endpoint URL** (Geben Sie Ihre Endpunkt-URL ein) aus. Geben Sie den Botnamen und die Bot-URL ein, die im vorherigen Schritt in der Debugkonsole angezeigt wurden.

1. Lassen Sie die Felder „Microsoft App ID“ (Microsoft App-ID), „Microsoft App Password“ (Microsoft App-Kennwort) und „Gebietsschema“ leer, und wählen Sie **CONNECT** (Verbinden) aus.

1. Wählen Sie anschließend **Speichern und verbinden** aus, und speichern Sie die Konfigurationsdatei am Speicherort Ihrer Wahl.

    >[!NOTE]
    > In Zukunft können Sie die Verbindung mit dem Bot wiederherstellen, indem Sie einfach unter „Meine Bots“ den Namen des Bots auswählen.

    ![Screenshot: Bot Framework Emulator mit der Konfigurationsanzeige „Neuer Bot“ mit hervorgehobener Schaltfläche „Speichern und verbinden“.](../media/5-new-bot-configuration.png)

1. Geben Sie „hi“ in das Feld am unteren Rand des Emulators ein, und drücken Sie die **EINGABETASTE**. Vergewissern Sie sich, dass Visual Studio Code in Zeile 20 der Datei **app.js** anhält. Klicken Sie anschließend in der Debugsymbolleiste von Visual Studio Code auf **Weiter**, und kehren Sie zum Emulator zurück, um die Antwort des Bots anzuzeigen.

1. Der Bot wird Ihnen eine Reihe von Fragen stellen. Beantworten Sie diese, und klicken Sie in Visual Studio Code jedes Mal, wenn ein Haltepunkt erreicht wird, auf **Weiter**. Wenn Sie fertig sind, klicken Sie zum Beenden der Debugsitzung in der Debugsymbolleiste auf **Beenden**.

An diesem Punkt verfügen Sie über einen voll funktionsfähigen Bot und wissen, wie Sie diesen durch lokale Ausführung im Microsoft Bot Framework Emulator debuggen können. Der nächste Schritt besteht darin, den Bot durch Herstellen einer Verbindung mit der Wissensdatenbank, die Sie veröffentlicht haben, intelligenter zu machen.