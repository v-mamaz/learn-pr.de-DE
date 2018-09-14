Wir haben die erforderlichen Azure-Funktionen erstellt, und wir können sie lokal ausführen.

In diesem Vortrag, unsere Azure-Funktionen mit Slack hergestellt, und erstellen Sie eine Slack _Schrägstrich_ Befehl ruft unsere Azure-Funktion auf und zeigt das resultierende Mojified-Image im Fenster "slack".

Am Ende dieser Vorlesung lernen Sie Folgendes:

- So erstellen eine Slack-app und verbinden einen Schrägstrich-Befehl mit einem Endpunkt des Azure-Funktion.
- Wie Ihre Schrägstrich-Befehl lokal zu testen, ohne in die Cloud bereitzustellen.

## <a name="using-ngrok-to-develop-with-slash-commands"></a>Verwenden Ngrok zur Entwicklung mit Schrägstrich-Befehle

Unsere Azure-Funktionen sind derzeit nur lokal; ausgeführt. Allerdings führt Slack in der Cloud, auf das Internet.

Wenn wir eine Slack richten _Schrägstrich_ Befehl im nächsten Abschnitt, sondern stellen Sie für eine öffentliche URL, die sie aufruft, wenn ein Benutzer führt einen Schrägstrich-Befehl.

Wir möchten ihnen gerne unseren `RespondToSlackCommand` URL, die jedoch nur auf unserem lokalen Computer vorhanden ist.

Wie können Sie Dienste in der cloudzugriff auf Ressourcen auf dem lokalen Computer für die Entwicklung gewähren?

Ist eine hervorragende Lösung für dieses Problem `ngrok` Dies ist ein Tool, das sichere Tunnel über das Internet auf Ihren lokalen Computer wird erstellt.

1. Besuchen Sie https://ngrok.com/download
2. Befolgen Sie die Anweisungen zum Herunterladen und Installieren der `ngrok` Paket auf Ihrem lokalen Computer.
3. Führen Sie `ngrok http 7071` in einem Terminal aus.
   ![ngrok](/media-drafts/9.ngrok.png)
4. Dies gibt eine öffentliche URL Endung `ngrok.io` z. B. `http://bbade778.ngrok.io`, notieren Sie diese im nächsten Abschnitt benötigen.

> **Hinweis**
>
> Dies `http://*.ngrock.io` URL können Sie genau, wie Sie verwendet `http://localhost:7071`, probieren Sie es mit einem Bild wie folgt `http://[ngrok-url]/api/MojifyImage?imageUrl=[url-to-an-image]`

## <a name="create-a-slack-app"></a>Erstellen einer slack-app

Ein Schrägstrich-Befehl vorhanden ist, als Teil einer slack-app eine Slack _Bot_.

Besuchen Sie [Slack-App erstellen](https://api.slack.com/apps/new)

Wählen Sie eine `App Name` und ordnen Sie sie der `Workspace` Sie erstellt haben, zu Beginn dieses Tutorials und drücken Sie dann die `Create App`, wie folgt:

![Slack-App erstellen](/media-drafts/9.create-slack-app.png)

Sobald erstellt, müssen wir in unseren slack-app wechseln, und erstellen Sie einen Schrägstrich-Befehl.

## <a name="create-a-slash-command"></a>Erstellen Sie einen Schrägstrich-Befehl

Klicken Sie auf die `Slash Commands` Menüelement.

![Schrägstrich-Befehle](/media-drafts/9.slash-commands.png)

Klicken Sie auf `Create New Command`.

- Geben Sie den Namen für den Schrägstrich-Befehl in der `command` Feld.
- Geben Sie die öffentliche Ngrok-URL in die `Request URL` Feld

  > **WICHTIGE**
  >
  > Denken Sie daran, fügen Sie `/api/RespondToSlackCommand` an die URL

- Fügen Sie eine kurze Beschreibung und Nutzung Hinweis hinzu.
- Drücken Sie `Save`

![Schrägstrich-Befehle](/media-drafts/9.create-slash-command.png)

Nach dem Speichern sollten Sie einen Bildschirm sehen wie folgt:

![Schrägstrich-Befehle erfolgreich](/media-drafts/9.create-slash-commands-success.png)

## <a name="install-the-slack-app-to-the-workspace"></a>Installieren Sie die slack-app, auf den Arbeitsbereich

Bevor wir unseren slack-app in unseren Arbeitsbereich verwenden können, müssen wir es zu installieren.

1. Wählen Sie die `Basic Information` Menüelement

2. Erweitern der `Install your app to your workspace` Option, und drücken Sie die `Install app to workspace` Schaltfläche.

   ![Installieren Sie die App zum Arbeitsbereich](/media-drafts/9.install-app-to-workspace.png)

3. Es fordert Sie möglicherweise auf Ihre Anwendung authentifizieren wie folgt:

   ![Authentifizieren mit Arbeitsbereich-App](/media-drafts/9.authenticate-slack-app.png)

## <a name="try-it-out"></a>Ausprobieren

Nun, dass der Schrägstrich-Befehl wurde erstellt und mit unserem lokal ausgeführten Instanz von Azure Functions über den Ngrok-Link verbunden sind, lassen Sie uns testen.

1. Wechseln Sie zu der slack-Arbeitsbereich, den Sie mit Ihrer slack-app verknüpft.
2. Wechseln Sie zu jeder Chatfenster, und geben `/mojify` (oder den Namen die app zugewiesen)
3. Wenn alles ordnungsgemäß funktioniert hat, sollten Sie sehen `mojify` als Option

   ![Überprüfen Sie Mojify](/media-drafts/9.slack-check-mojify.png)

4. Geben Sie nun `/mojify` und fügen Sie eine Bild-URL ein, und drücken Sie die EINGABETASTE, etwa so:

   ![Typ Mojify](/media-drafts/9.slack-type-mojify.png)
