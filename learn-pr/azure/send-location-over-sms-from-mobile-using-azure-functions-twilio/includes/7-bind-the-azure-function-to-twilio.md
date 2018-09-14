An diesem Punkt ist die mobile App vollständig und kann den Benutzerstandort und die Liste der Telefonnummern an eine Azure-Funktion senden, die die Daten deserialisieren kann. In dieser Einheit binden Sie die Azure-Funktion an Twilio, um SMS zu senden.

Azure Functions kann mit anderen Diensten verbunden werden, entweder mit Diensten in Azure oder mit Drittanbieterdiensten. Diese Verbindungen – sogenannte Bindungen – liegen in zwei Formen vor: als Eingabe- und Ausgabebindungen. Eingabebindungen stellen Daten für Ihre Funktion bereit, Ausgabebindungen empfangen Daten von Ihrer Funktion und senden sie an einen anderen Dienst. Weitere Informationen erhalten Sie in der [Dokumentation zu Azure Functions-Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

In Visual Studio erstellte Bindungen für Azure Functions werden mithilfe von Parametern der Funktion definiert, ergänzt durch Attribute.

## <a name="bind-the-azure-function-to-twilio"></a>Binden der Azure-Funktion an Twilio

Um SMS-Nachrichten über Twilio zu senden, wird eine Ausgabebindung benötigt, die mit der Abonnement-ID Ihres Kontos (SID) und dem Authentifizierungstoken konfiguriert wird.

1. Beenden Sie die lokale Azure Functions-Runtime, wenn diese noch von der vorherigen Einheit ausgeführt wird.

1. Fügen Sie dem `ImHere.Functions`-Projekt das NuGet-Paket „Microsoft.Azure.WebJobs.Extensions.Twilio“ hinzu. Dieses NuGet-Paket enthält die relevanten Klassen für die Bindung.

1. Fügen Sie der statischen `Run`-Methode in der statischen `SendLocation`-Klasse `messages` einen neuen Parameter hinzu. Dieser Parameter weist den Typ `ICollector<SMSMessage>` auf. Sie müssen eine using-Anweisung für den `Twilio`-Namespace hinzufügen.

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

1. Ergänzen Sie den neuen `messages`-Parameter mit dem `TwilioSms`-Attribut. Dieses Attribut umfasst drei Parameter, die Sie festlegen müssen.

    | Einstellung      |  Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **AccountSidSetting** | „TwilioAccountSid“ | Die SID für Ihr Twilio-Konto. Anstatt die SID direkt festzulegen, entspricht dieser Parameter dem Namen eines Werts in den Einstellungen der Funktions-App, der zum Abrufen der SID verwendet wird. |
    | **AuthTokenSetting** | „TwilioAuthToken“ | Das Authentifizierungstoken für Ihr Twilio-Konto. Anstatt das Authentifizierungstoken direkt festzulegen, entspricht dieser Parameter dem Namen eines Werts in den Einstellungen der Funktions-App, der zum Abrufen des Authentifizierungstokens verwendet wird. |
    | **From** | Ihre Twilio-Telefonnummer. | Die Twilio-Telefonnummer, von der aus die SMS-Nachricht gesendet wird. Die Telefonnummer wird im internationalen Format angegeben (+\<Landeskennzahl\>\<Telefonnummer\>, Beispiel: „+1555123456“). |

    Wenn Sie ein Twilio-Konto erstellen, wird Ihnen eine Telefonnummer zugewiesen, über die Sie Nachrichten senden können. Sie finden diese Telefonnummer im Twilio-Dashboard **Phone Numbers** (Telefonnummern). Wählen Sie auf der Twilio-Website die Auslassungspunkte im unteren Bereich des links angezeigten Menüs aus. Wählen Sie dann *SUPER NETWORK > Phone Numbers* (SUPERNETZWERK > Telefonnummern) aus. Sie können dieses Dashboard mithilfe des Stecknadelsymbols an das Menü im linken Bereich anheften. Ihre Twilio-Nummer befindet sich unterhalb von *Manage Numbers > Active Numbers* (Nummern verwalten > Aktive Nummern). Eventuell in der Nummer vorhandene Leerzeichen müssen entfernt werden.

    ![Ermitteln Ihrer Twilio-Nummer](../media-drafts/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

1. Einstellungen der Funktions-App können lokal in der `local.settings.json`-Datei konfiguriert werden. Fügen Sie die SID für Ihr Twilio-Konto und das Authentifizierungstoken mithilfe der an das `TwilioSMS`-Attribut übergebenen Einstellungsnamen dieser JSON-Datei hinzu.

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "AzureWebJobsDashboard": "UseDevelopmentStorage=true",
            "TwilioAccountSid": "<Your SID>",
            "TwilioAuthToken": "<Your Auth Token>"
        }
    }
    ```

    Ersetzen Sie \<Your SID\> und \<Your Auth Token\> durch die Werte aus Ihrem Twilio-Dashboard.

    > Diese lokalen Einstellungen gelten nur für die lokale Ausführung. In einer Produktions-App entsprechen diese Werte den Anmeldeinformationen für das lokale Entwicklungskonto oder das Testkonto. Nachdem die Azure-Funktion in Azure bereitgestellt wurde, können Sie die Produktionswerte konfigurieren.
    > Wenn Sie Ihren Code in die Quellcodeverwaltung einchecken, werden diese lokalen Werte für die Anwendungseinstellungen ebenfalls eingecheckt. Seien Sie deshalb vorsichtig, und checken Sie keine tatsächlichen Werte in diese Dateien ein, wenn es sich um Open Source-Code oder öffentlich zugänglichen Code handelt.

## <a name="create-the-sms-messages"></a>Erstellen der SMS-Nachricht

Der `ICollector<SMSMessage>`-Parameter ist eine Sammlung aus `SMSMessage`-Instanzen und wird zum Erfassen der SMS-Nachrichten verwendet, die Sie senden möchten. Nachdem die Funktion ausgeführt wurde, werden alle Instanzen von `SMSMessage`, die dieser Sammlung hinzugefügt wurden, an Twilio übergeben und an die jeweiligen Empfänger gesendet.

1. Fügen Sie in der `SendLocation`-Funktion Code hinzu, um die Telefonnummern in `PostData` zu durchlaufen und für jede dieser eine SMS-Nachricht zu erstellen.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
    }
    ```

    Für die Nachricht wird eine Zieltelefonnummer und ein Textkörper benötigt, der die Google Maps-URL enthält, die aus dem Benutzerstandort erstellt wurde.

1. Protokollieren Sie jede Nachricht, und fügen Sie sie dann der `messages`-Sammlung hinzu.

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

Die vollständige `SendLocation`-Methode wird unten gezeigt.

```cs
[FunctionName("SendLocation")]
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                                Route = null)]HttpRequestMessage req,
                                                    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
                                                                AuthTokenSetting = "TwilioAuthToken",
                                                                From = "<your Twilio phone number>")]ICollector<SMSMessage> messages,
                                                    TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");
    PostData data = await req.Content.ReadAsAsync<PostData>();
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.Info($"URL created - {url}");
    foreach (string toNo in data.ToNumbers)
    {
        SMSMessage message = new SMSMessage
        {
            Body = $"I'm here! {url}",
            To = toNo
        };
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    return req.CreateResponse(HttpStatusCode.OK);
}
```

## <a name="test-it-out"></a>Testen

1. Legen Sie die `ImHere.Functions`-App als Startprojekt fest, und starten Sie sie ohne Debuggen.

1. Legen Sie die `ImHere.UWP`-App als Startprojekt fest, und führen Sie sie aus.

1. Geben Sie Ihre eigene Telefonnummer im internationalen Format (+\<Landeskennzahl\>\<Telefonnummer\>) in der Xamarin.Forms-App an. Mit Twilio-Testkonten können Nachrichten nur an überprüfte Telefonnummern gesendet werden, deshalb können Sie bis zum Upgrade auf eine zahlungspflichtiges Konto oder bis zur Überprüfung weiterer Nummern nur Nachrichten an sich selbst senden.

1. Klicken Sie auf die Schaltfläche **Standort senden**. Wenn die SMS-Nachricht erfolgreich gesendet wurde, wird eine Meldung in der Xamarin.Forms-App angezeigt, die den erfolgreichen Versand des Standorts bestätigt.

    ![Die Xamarin.Forms-App zeigt an, dass der Standort gesendet wurde.](../media-drafts/7-ui-location-sent.png)

1. In den Konsolenprotokollen für die Azure-Funktion wird angezeigt, dass die Nachricht erstellt und gesendet wurde. Wenn es zu Fehlern kommt (beispielsweise, weil die Nummer im falschen Format vorliegt), werden diese hier protokolliert.

    ![Die Konsole der Azure-Funktion zeigt an, dass die Nachricht gesendet wurde.](../media-drafts/7-function-message-sent.png)

1. Überprüfen Sie Ihr Telefon auf Nachrichten. Folgen Sie dem Link in der Nachricht, um Ihren Standort anzuzeigen.

    ![SMS-Nachricht, die auf einem Mobiltelefon empfangen wird](../media-drafts/7-message-received.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie eine Twilio-Bindung für die Azure-Funktion erstellen und eine SMS-Nachricht mit dem Benutzerstandort an eine Funktion senden, die lokal ausgeführt wird. In der nächsten Einheit veröffentlichen Sie die Funktion in Azure.