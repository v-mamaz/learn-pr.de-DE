In dieser Übung erfahren Sie, wie Sie eine Azure-Funktion erstellen, die eine HTTP-Anforderung mit einer einzelnen Zeichenfolge akzeptiert. Die Funktion gibt eine Zeichenfolge an den Aufrufer zurück, die angibt, ob der Vorgang erfolgreich war. In der nächsten Übung verwenden Sie diese Funktion weiter.

## <a name="create-an-http-trigger"></a>Erstellen eines HTTP-Triggers

Verwenden Sie Ihre vorhandene Azure Functions-Anwendung, und fügen Sie einen HTTP-Trigger hinzu.

1. Stellen Sie sicher, dass Sie beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto angemeldet sind, über das Sie die Sandbox aktiviert haben.

1. Navigieren Sie zur Anzeige **Alle Ressourcen**, und wählen Sie Ihre Funktions-App aus.

1. Zeigen Sie auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).

1. Wählen Sie **HTTP-Trigger** aus.

1. Behalten Sie für **Name** den Standardwert bei.

1. Legen Sie die **Autorisierungsstufe** auf **Anonym** fest.

1. Wählen Sie **Erstellen** aus.

1. Werfen Sie einen kurzen Blick auf den automatisch generierten Code, um sich ein Bild von den Abläufen zu verschaffen. Der *req*-Parameter stellt die eingehende Anforderung dar und enthält einen *name*-Parameter. Wir überprüfen, ob *name* einen Wert hat. Wenn dies der Fall ist, geben wir einen Gruß zurück. Andernfalls geben wir eine Fehlermeldung zurück.

## <a name="get-your-function-url"></a>Abrufen Ihrer Funktions-URL

Da wir nun den HTTP-Trigger erstellt haben, rufen wir die Funktions-URL ab, damit wir beginnen können, eine Anforderung zu stellen.

1. Wählen Sie Ihren HTTP-Trigger aus, um den Codebildschirm zu öffnen.

1. Wählen Sie rechts neben **Ausführen** die Option **Get function URL** (Funktions-URL abrufen) aus.

1. Klicken Sie auf **Kopieren**, und schließen Sie anschließend das Popupfenster „Funktions-URL“.

## <a name="issue-a-get-request-to-your-http-trigger"></a>Übermitteln einer GET-Anforderung an Ihren HTTP-Trigger

Wir haben jetzt unsere Funktions-URL in unsere Zwischenablage kopiert. Nun geben wir eine GET-Anforderung aus, um festzustellen, ob wir eine Antwort erhalten.

1. Öffnen Sie eine neue Registerkarte in Ihrem Webbrowser.

1. Fügen Sie die URL in die Adressleiste ein.

1. Fügen Sie einen Abfragezeichenfolgen-Parameter namens *Name* mit Ihrem Namen hinzu, z.B. `.../api/HttpTriggerCSharp1?name=Jesse`.

1. Drücken Sie die <kbd>EINGABETASTE</kbd>, um die Anforderung zu senden.
