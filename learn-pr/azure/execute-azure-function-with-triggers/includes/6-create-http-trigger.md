In dieser Übung erstellen wir eine Azure-Funktion, die eine HTTP-Anforderung mit einer einzelnen Zeichenfolge akzeptiert. Die Funktion gibt eine Zeichenfolge an den Aufrufer zurück, mit der angegeben wird, ob der Vorgang erfolgreich war oder nicht.

> [!NOTE]
> Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) mit einem gültigen Konto angemeldet sind.

## <a name="create-an-http-trigger"></a>Erstellen eines HTTP-Triggers

Verwenden Sie Ihre vorhandene Azure Functions-Anwendung, und fügen Sie einen HTTP-Trigger hinzu.

1. Zeigen Sie auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.

    ![Zeigen auf „Funktionen“ und Auswählen des Pluszeichens](../media-drafts/4-hover-function.png)

2. Wählen Sie **HTTP-Trigger** aus.

3. Wählen Sie **C#** als Sprache aus. 

4. Behalten Sie für **Name** den Standardwert bei.

5. Legen Sie die **Autorisierungsstufe** auf **Anonym** fest.

6. Klicken Sie auf **Erstellen**.

7. Werfen Sie einen kurzen Blick auf den automatisch generierten Code, um sich ein Bild von den Abläufen zu verschaffen. Der *req*-Parameter stellt die eingehende Anforderung dar und enthält einen *name*-Parameter. Wir überprüfen, ob *name* einen Wert hat. Wenn dies der Fall ist, geben wir einen Gruß zurück. Andernfalls geben wir eine Fehlermeldung zurück.

## <a name="get-your-function-url"></a>Abrufen Ihrer Funktions-URL

Da wir nun den HTTP-Trigger erstellt haben, rufen wir die Funktions-URL ab, damit wir beginnen können, eine Anforderung zu stellen.

1. Wählen Sie Ihren HTTP-Trigger aus, um den Codebildschirm zu öffnen.

2. Wählen Sie rechts von **Ausführen** die Option **Funktions-URL abrufen** aus.

3. Wählen Sie **Kopieren** aus.

4. Wählen Sie **Ausführen** aus, um Ihre Funktion zu starten.

## <a name="issue-a-get-request-to-your-http-trigger"></a>Ausgeben einer GET-Anforderung an Ihren HTTP-Trigger

Wir haben jetzt unsere Funktions-URL in unsere Zwischenablage kopiert. Nun geben wir eine GET-Anforderung aus, um festzustellen, ob wir eine Antwort erhalten.

1. Öffnen Sie eine neue Registerkarte in Ihrem Webbrowser.

2. Fügen Sie die URL in die Adressleiste ein.

3. Fügen Sie einen Abfragezeichenfolgen-Parameter namens *name* mit Ihrem Namen hinzu, z.B. `.../api/HttpTriggerCSharp1?name=Jesse`.

4. Drücken Sie die EINGABETASTE, um die Anforderung zu senden.

## <a name="clean-up"></a>Bereinigen

Um sicherzustellen, dass für diese Funktion keine Gebühren anfallen, wählen Sie über dem Protokollfenster **Anhalten** aus.

![Anhalten](../media-drafts/4-pause-timer.png)