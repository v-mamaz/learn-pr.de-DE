An diesem Punkt ist die mobile App vollständig und kann den Benutzerstandort und die Liste der Telefonnummern an eine Azure-Funktion senden, die die Daten deserialisieren kann. In dieser Einheit binden Sie die Azure-Funktion an Twilio, um SMS zu senden.

Azure Functions kann mit anderen Diensten verbunden werden, entweder mit Diensten in Azure oder mit Drittanbieterdiensten. Diese Verbindungen – sogenannte Bindungen – liegen in zwei Formen vor: als Eingabe- und Ausgabebindungen. Eingabebindungen stellen Daten für Ihre Funktion bereit, Ausgabebindungen empfangen Daten von Ihrer Funktion und senden sie an einen anderen Dienst. Weitere Informationen erhalten Sie in der [Dokumentation zu Azure Functions-Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true).

In Visual Studio erstellte Bindungen für Azure Functions werden mithilfe von Parametern der Funktion definiert, ergänzt durch Attribute.

## <a name="bind-the-azure-function-to-twilio"></a>Binden der Azure-Funktion an Twilio

Um SMS-Nachrichten über Twilio zu senden, wird eine Ausgabebindung benötigt, die mit der Abonnement-ID Ihres Kontos (SID) und dem Authentifizierungstoken konfiguriert wird.

1. Beenden Sie die lokale Azure Functions-Runtime, wenn diese noch von der vorherigen Einheit ausgeführt wird.

2. Fügen Sie dem `ImHere.Functions`-Projekt das NuGet-Paket „Microsoft.Azure.WebJobs.Extensions.Twilio“ hinzu. Dieses NuGet-Paket enthält die relevanten Klassen für die Bindung.

3. Fügen Sie der statischen `Run`-Methode in der statischen `SendLocation`-Klasse `messages` einen neuen Parameter hinzu. Dieser Parameter weist den Typ `ICollector<CreateMessageOptions>` auf. Sie müssen eine `using`-Anweisung für den `Twilio.Rest.Api.V2010.Account`-Namespace hinzufügen.

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,"get", "post", Route = null)]HttpRequestMessage req,
                                                ICollector<CreateMessageOptions> messages,
                                                ILogger log)
    ```

4. Ergänzen Sie den neuen `messages`-Parameter wie folgt um das `TwilioSms`-Attribut: 

      ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",AuthTokenSetting = "TwilioAuthToken", From = "+1xxxxxxxxx")]ICollector<CreateMessageOptions> messages,
    ```
    Dieses Attribut umfasst drei Parameter, die Sie festlegen müssen:

    * Legen Sie **AccountSidSetting** auf `"TwilioAccountSid"` fest.
  
        Dies ist die SID für Ihr Twilio-Konto, die Sie sich zuvor in diesem Modul notiert haben. Die SID wird nicht direkt, sondern über einen Parameter festgelegt, der dem Namen eines Werts in den Einstellungen der Funktions-App entspricht und zum Abrufen der SID verwendet wird.

    * Legen Sie **AuthTokenSetting** auf `"TwilioAuthToken"` fest.

       Dies ist das Authentifizierungstoken für Ihr Twilio-Konto an, das Sie sich zuvor in diesem Modul notiert haben. Das Authentifizierungstoken wird nicht direkt, sondern über diesen Parameter festgelegt, der dem Namen eines Werts in den Einstellungen der Funktions-App entspricht und zum Abrufen des Authentifizierungstokens verwendet wird.

    * Legen Sie **From** auf Ihre aktive Twilio-Telefonnummer fest, die Sie sich zuvor in diesem Modul notiert haben.

        Die Twilio-Telefonnummer, von der die SMS-Nachrichten gesendet werden. Die Telefonnummer wird im internationalen Format angegeben (+\<Landeskennzahl\>\<Telefonnummer\>, Beispiel: „+1555123456“).

    > [!IMPORTANT]
    > Stellen Sie sicher, dass die Telefonnummer keine Leerzeichen enthält.

5. Einstellungen der Funktions-App können lokal in der `local.settings.json`-Datei konfiguriert werden. Fügen Sie die SID für Ihr Twilio-Konto und das Authentifizierungstoken mithilfe der an das `TwilioSMS`-Attribut übergebenen Einstellungsnamen dieser JSON-Datei hinzu.

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "FUNCTIONS_WORKER_RUNTIME": "dotnet",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

    Ersetzen Sie \<Your SID\> und \<Your Auth Token\> durch die Werte aus Ihrem Twilio-Dashboard.

    > [!NOTE]
    > Diese lokalen Einstellungen gelten nur für die lokale Ausführung. In einer Produktions-App entsprechen diese Werte den Anmeldeinformationen für das lokale Entwicklungskonto oder das Testkonto. Nachdem die Azure-Funktion in Azure bereitgestellt wurde, können Sie die Produktionswerte konfigurieren.

    > [!NOTE]
    > Wenn Sie Ihren Code in die Quellcodeverwaltung einchecken, werden diese lokalen Werte für die Anwendungseinstellungen ebenfalls eingecheckt. Seien Sie deshalb vorsichtig, und checken Sie keine tatsächlichen Werte in diese Dateien ein, wenn es sich um Open Source-Code oder öffentlich zugänglichen Code handelt.

## <a name="create-the-sms-messages"></a>Erstellen der SMS-Nachricht

Der `ICollector<CreateMessageOptions>`-Parameter ist eine Sammlung von `CreateMessageOptions`-Instanzen und wird zum Erfassen der SMS-Nachrichten verwendet, die Sie senden möchten. Nachdem die Funktion ausgeführt wurde, werden alle Instanzen von `CreateMessageOptions`, die dieser Sammlung hinzugefügt wurden, an Twilio übergeben. Mit diesen werden dann Nachrichten erstellt, die an die jeweiligen Empfänger gesendet werden.

1. Fügen Sie der `SendLocation`-Funktion Code hinzu, mit dem in einer Schleife die Telefonnummern in `PostData` durchlaufen werden, und erstellen Sie für jede eine SMS-Nachricht. Sie müssen eine using-Anweisung für `Twilio.Types` hinzufügen.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        PhoneNumber number = new PhoneNumber(toNo);
        CreateMessageOptions message = new CreateMessageOptions(number)
        {
            Body = $"I'm here! {url}"
        };
    }
    ```

    Für die Nachricht wird eine Zieltelefonnummer und ein Textkörper benötigt, der die Google Maps-URL enthält, die aus dem Benutzerstandort erstellt wurde.

1. Protokollieren Sie jede Nachricht, und fügen Sie sie dann der `messages`-Sammlung hinzu.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

Die vollständige `SendLocation`-Methode wird unten gezeigt. Der Platzhalter innerhalb des `From`-Parameters müsste durch Ihre aktive Telefonnummer ersetzt werden.

```cs
[FunctionName("SendLocation")]
public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                         "get", "post",
                                                         Route = null)]HttpRequest req,
                                            [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                       AuthTokenSetting = "TwilioAuthToken",
                                                       From = "+1xxxxxxxxx")] ICollector<CreateMessageOptions> messages,
                                            ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.LogInformation($"URL created - {url}");

    foreach (string toNo in data.ToNumbers)
    {
        PhoneNumber number = new PhoneNumber(toNo);
        CreateMessageOptions message = new CreateMessageOptions(number)
        {
            Body = $"I'm here! {url}"
        };
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }

    return new OkResult();
}
```

## <a name="test-it-out"></a>Testen

1. Legen Sie die `ImHere.Functions`-App als Startprojekt fest, und starten Sie sie ohne Debuggen.

1. Legen Sie die `ImHere.UWP`-App als Startprojekt fest, und führen Sie sie aus.

1. Geben Sie Ihre eigene Telefonnummer im internationalen Format (+\<Landeskennzahl\>\<Telefonnummer\>) in der Xamarin.Forms-App an. Mit Twilio-Testkonten können Nachrichten nur an überprüfte Telefonnummern gesendet werden, deshalb können Sie bis zum Upgrade auf eine zahlungspflichtiges Konto oder bis zur Überprüfung weiterer Nummern nur Nachrichten an sich selbst senden.

1. Klicken Sie auf die Schaltfläche **Standort senden**. Wenn die SMS-Nachricht erfolgreich gesendet wurde, wird eine Meldung in der Xamarin.Forms-App angezeigt, die den erfolgreichen Versand des Standorts bestätigt.

    ![Die Xamarin.Forms-App zeigt an, dass der Standort gesendet wurde.](../media/7-ui-location-sent.png)

1. In den Konsolenprotokollen für die Azure-Funktion wird angezeigt, dass die Nachricht erstellt und gesendet wurde. Wenn es zu Fehlern kommt (beispielsweise, weil die Nummer im falschen Format vorliegt), werden diese hier protokolliert.

    ![Die Konsole der Azure-Funktion zeigt an, dass die Nachricht gesendet wurde.](../media/7-function-message-sent.png)

1. Überprüfen Sie Ihr Telefon auf Nachrichten. Folgen Sie dem Link in der Nachricht, um Ihren Standort anzuzeigen.

    ![SMS-Nachricht, die auf einem Mobiltelefon empfangen wird](../media/7-message-received.png)

    > [!TIP]
    > Der angezeigte Standort ist der Ausführungsort der App und befindet sich in der Nähe des Rechenzentrums, über das der virtuelle Computer ausgeführt wird. Würde diese App auf Ihrem lokalen Gerät ausgeführt, würde Ihr Standort angezeigt werden.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie eine Twilio-Bindung für die Azure-Funktion erstellen und eine SMS-Nachricht mit dem Benutzerstandort an eine Funktion senden, die lokal ausgeführt wird. In der nächsten Einheit veröffentlichen Sie die Funktion in Azure.
