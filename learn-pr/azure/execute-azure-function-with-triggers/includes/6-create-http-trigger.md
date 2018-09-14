In dieser Übung erfahren Sie, wie Sie eine Azure-Funktion erstellen, die eine HTTP-Anforderung mit einer einzelnen Zeichenfolge akzeptiert. Die Funktion gibt eine Zeichenfolge an den Aufrufer zurück, die angibt, ob der Vorgang erfolgreich war. Wir werden weiterhin für die Funktion aus der vorhergehenden Übung.

## <a name="create-an-http-trigger"></a>Erstellen eines HTTP-Triggers

Verwenden Sie Ihre vorhandene Azure Functions-Anwendung, und fügen Sie einen HTTP-Trigger hinzu.

1. Melden Sie sich im [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Zeigen Sie auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).

1. Klicken Sie auf **HTTP-Trigger**.

1. Wählen Sie **C#** als Sprache aus.

1. Behalten Sie für **Name** den Standardwert bei.

1. Legen Sie die **Autorisierungsstufe** auf **Anonym** fest.

1. Wählen Sie **Erstellen** aus.

1. Werfen Sie einen kurzen Blick auf den automatisch generierten Code, um sich ein Bild von den Abläufen zu verschaffen. Der *req*-Parameter stellt die eingehende Anforderung dar und enthält einen *name*-Parameter. Wir überprüfen, ob *name* einen Wert hat. Wenn dies der Fall ist, geben wir einen Gruß zurück. Andernfalls geben wir eine Fehlermeldung zurück.

## <a name="get-your-function-url"></a>Abrufen Ihrer Funktions-URL

Da wir nun den HTTP-Trigger erstellt haben, rufen wir die Funktions-URL ab, damit wir beginnen können, eine Anforderung zu stellen.

1. Wählen Sie Ihren HTTP-Trigger aus, um den Codebildschirm zu öffnen.

1. Wählen Sie rechts von **Ausführen** die Option **Funktions-URL abrufen** aus.

1. Wählen Sie **Kopieren** aus.

1. Wählen Sie **Ausführen** aus, um Ihre Funktion zu starten.

## <a name="issue-a-get-request-to-your-http-trigger"></a>Ausgeben einer GET-Anforderung an Ihren HTTP-Trigger

Wir haben jetzt unsere Funktions-URL in unsere Zwischenablage kopiert. Nun geben wir eine GET-Anforderung aus, um festzustellen, ob wir eine Antwort erhalten.

1. Öffnen Sie eine neue Registerkarte in Ihrem Webbrowser.

1. Fügen Sie die URL in die Adressleiste ein.

1. Fügen Sie einen Abfragezeichenfolgen-Parameter namens *name* mit Ihrem Namen hinzu, z.B. `.../api/HttpTriggerCSharp1?name=Jesse`.

1. Drücken Sie die EINGABETASTE, um die Anforderung zu senden.

## <a name="clean-up"></a>Bereinigen

Klicken Sie über dem Protokollfenster auf **Anhalten**, um sicherzustellen, dass für diese Funktion keine Gebühren anfallen.
