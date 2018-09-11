<span data-ttu-id="32e2e-101">An diesem Punkt ist die mobile App vollständig und kann den Benutzerstandort und die Liste der Telefonnummern an eine Azure-Funktion senden, die die Daten deserialisieren kann.</span><span class="sxs-lookup"><span data-stu-id="32e2e-101">At this point, the mobile app is complete and it can send the user's location and list of phone numbers to an Azure function that can deserialize the data.</span></span> <span data-ttu-id="32e2e-102">In dieser Einheit binden Sie die Azure-Funktion an Twilio, um SMS-Nachrichten zu senden.</span><span class="sxs-lookup"><span data-stu-id="32e2e-102">In this unit, you bind the Azure function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="32e2e-103">Azure Functions kann mit anderen Diensten verbunden werden, entweder mit Diensten in Azure oder mit Drittanbieterdiensten.</span><span class="sxs-lookup"><span data-stu-id="32e2e-103">Azure Functions can be connected to other services, either services in Azure or third-party services.</span></span> <span data-ttu-id="32e2e-104">Diese Verbindungen – sogenannte Bindungen – liegen in zwei Formen vor: als Eingabe- und Ausgabebindungen.</span><span class="sxs-lookup"><span data-stu-id="32e2e-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="32e2e-105">Eingabebindungen stellen Daten für Ihre Funktion bereit, Ausgabebindungen empfangen Daten von Ihrer Funktion und senden sie an einen anderen Dienst.</span><span class="sxs-lookup"><span data-stu-id="32e2e-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="32e2e-106">Weitere Informationen erhalten Sie in der [Dokumentation zu Azure Functions-Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span><span class="sxs-lookup"><span data-stu-id="32e2e-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).</span></span>

<span data-ttu-id="32e2e-107">In Visual Studio erstellte Bindungen für Azure Functions werden mithilfe von Parametern der Funktion definiert, ergänzt durch Attribute.</span><span class="sxs-lookup"><span data-stu-id="32e2e-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-function-to-twilio"></a><span data-ttu-id="32e2e-108">Binden der Azure-Funktion an Twilio</span><span class="sxs-lookup"><span data-stu-id="32e2e-108">Bind the Azure function to Twilio</span></span>

<span data-ttu-id="32e2e-109">Um SMS-Nachrichten über Twilio zu senden, wird eine Ausgabebindung benötigt, die mit der Abonnement-ID Ihres Kontos (SID) und dem Authentifizierungstoken konfiguriert wird.</span><span class="sxs-lookup"><span data-stu-id="32e2e-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="32e2e-110">Beenden Sie die lokale Azure Functions-Runtime, wenn diese noch von der vorherigen Einheit ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="32e2e-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="32e2e-111">Fügen Sie dem `ImHere.Functions`-Projekt das NuGet-Paket „Microsoft.Azure.WebJobs.Extensions.Twilio“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="32e2e-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package to the `ImHere.Functions` project.</span></span> <span data-ttu-id="32e2e-112">Dieses NuGet-Paket enthält die relevanten Klassen für die Bindung.</span><span class="sxs-lookup"><span data-stu-id="32e2e-112">This NuGet package contains the relevant classes for the binding.</span></span>

1. <span data-ttu-id="32e2e-113">Fügen Sie der statischen `Run`-Methode in der statischen `SendLocation`-Klasse `messages` einen neuen Parameter hinzu.</span><span class="sxs-lookup"><span data-stu-id="32e2e-113">Add a new parameter to the static `Run` method on the `SendLocation` static class called `messages`.</span></span> <span data-ttu-id="32e2e-114">Dieser Parameter weist den Typ `ICollector<SMSMessage>` auf.</span><span class="sxs-lookup"><span data-stu-id="32e2e-114">This parameter will have a type of `ICollector<SMSMessage>`.</span></span> <span data-ttu-id="32e2e-115">Sie müssen eine using-Anweisung für den `Twilio`-Namespace hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="32e2e-115">You'll need to add a using directive for the `Twilio` namespace.</span></span>

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                   "get", "post",
                                                                   Route = null)]HttpRequestMessage req,
                                                      ICollector<SMSMessage> messages,
                                                      TraceWriter log)
    ```

1. <span data-ttu-id="32e2e-116">Ergänzen Sie den neuen `messages`-Parameter mit dem `TwilioSms`-Attribut.</span><span class="sxs-lookup"><span data-stu-id="32e2e-116">Decorate the new `messages` parameter with the `TwilioSms` attribute.</span></span> <span data-ttu-id="32e2e-117">Dieses Attribut umfasst drei Parameter, die Sie festlegen müssen.</span><span class="sxs-lookup"><span data-stu-id="32e2e-117">This attribute has three parameters you need to set.</span></span>

    | <span data-ttu-id="32e2e-118">Einstellung</span><span class="sxs-lookup"><span data-stu-id="32e2e-118">Setting</span></span>      |  <span data-ttu-id="32e2e-119">Wert</span><span class="sxs-lookup"><span data-stu-id="32e2e-119">Value</span></span>   | <span data-ttu-id="32e2e-120">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="32e2e-120">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="32e2e-121">**AccountSidSetting**</span><span class="sxs-lookup"><span data-stu-id="32e2e-121">**AccountSidSetting**</span></span> | <span data-ttu-id="32e2e-122">„TwilioAccountSid“</span><span class="sxs-lookup"><span data-stu-id="32e2e-122">"TwilioAccountSid"</span></span> | <span data-ttu-id="32e2e-123">Die SID für Ihr Twilio-Konto.</span><span class="sxs-lookup"><span data-stu-id="32e2e-123">The SID for your Twilio account.</span></span> <span data-ttu-id="32e2e-124">Anstatt die SID direkt festzulegen, entspricht dieser Parameter dem Namen eines Werts in den Einstellungen der Funktions-App, der zum Abrufen der SID verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="32e2e-124">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span> |
    | <span data-ttu-id="32e2e-125">**AuthTokenSetting**</span><span class="sxs-lookup"><span data-stu-id="32e2e-125">**AuthTokenSetting**</span></span> | <span data-ttu-id="32e2e-126">„TwilioAuthToken“</span><span class="sxs-lookup"><span data-stu-id="32e2e-126">"TwilioAuthToken"</span></span> | <span data-ttu-id="32e2e-127">Das Authentifizierungstoken für Ihr Twilio-Konto.</span><span class="sxs-lookup"><span data-stu-id="32e2e-127">The Auth Token for your Twilio account.</span></span> <span data-ttu-id="32e2e-128">Anstatt das Authentifizierungstoken direkt festzulegen, entspricht dieser Parameter dem Namen eines Werts in den Einstellungen der Funktions-App, der zum Abrufen des Authentifizierungstokens verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="32e2e-128">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span> |
    | <span data-ttu-id="32e2e-129">**From**</span><span class="sxs-lookup"><span data-stu-id="32e2e-129">**From**</span></span> | <span data-ttu-id="32e2e-130">Ihre Twilio-Telefonnummer.</span><span class="sxs-lookup"><span data-stu-id="32e2e-130">Your Twilio phone number</span></span> | <span data-ttu-id="32e2e-131">Die Twilio-Telefonnummer, von der aus die SMS-Nachricht gesendet wird. Die Telefonnummer wird im internationalen Format angegeben (+\<Landeskennzahl\>\<Telefonnummer\>, Beispiel: „+1555123456“).</span><span class="sxs-lookup"><span data-stu-id="32e2e-131">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span> |

    <span data-ttu-id="32e2e-132">Wenn Sie ein Twilio-Konto erstellen, wird Ihnen eine Telefonnummer zugewiesen, über die Sie Nachrichten senden können.</span><span class="sxs-lookup"><span data-stu-id="32e2e-132">When you create a Twilio account, you are assigned a phone number that you can send messages from.</span></span> <span data-ttu-id="32e2e-133">Sie finden diese Telefonnummer im Twilio-Dashboard **Phone Numbers** (Telefonnummern).</span><span class="sxs-lookup"><span data-stu-id="32e2e-133">You can find this phone number on the Twilio **Phone Numbers** dashboard.</span></span> <span data-ttu-id="32e2e-134">Wählen Sie auf der Twilio-Website die Auslassungspunkte im unteren Bereich des links angezeigten Menüs aus.</span><span class="sxs-lookup"><span data-stu-id="32e2e-134">From the Twilio site, select the ellipses at the bottom of the left-hand menu.</span></span> <span data-ttu-id="32e2e-135">Wählen Sie dann *SUPER NETWORK > Phone Numbers* (SUPERNETZWERK > Telefonnummern) aus.</span><span class="sxs-lookup"><span data-stu-id="32e2e-135">Then, select *SUPER NETWORK->Phone Numbers*.</span></span> <span data-ttu-id="32e2e-136">Sie können dieses Dashboard mithilfe des Stecknadelsymbols an das Menü im linken Bereich anheften.</span><span class="sxs-lookup"><span data-stu-id="32e2e-136">You can pin this dashboard to the left-hand menu using the pin icon.</span></span> <span data-ttu-id="32e2e-137">Ihre Twilio-Nummer befindet sich unterhalb von *Manage Numbers > Active Numbers* (Nummern verwalten > Aktive Nummern).</span><span class="sxs-lookup"><span data-stu-id="32e2e-137">Your Twilio number will be under *Manage Numbers->Active Numbers*.</span></span> <span data-ttu-id="32e2e-138">Eventuell in der Nummer vorhandene Leerzeichen müssen entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="32e2e-138">You'll need to remove any spaces from the number.</span></span>

    ![Ermitteln Ihrer Twilio-Nummer](../media-drafts/7-twilio-find-number.png)

    ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",
               AuthTokenSetting = "TwilioAuthToken",
               From = "+1xxxxxxxxx")]ICollector<SMSMessage> messages,
    ```

1. <span data-ttu-id="32e2e-140">Einstellungen der Funktions-App können lokal in der `local.settings.json`-Datei konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="32e2e-140">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="32e2e-141">Fügen Sie die SID für Ihr Twilio-Konto und das Authentifizierungstoken mithilfe der an das `TwilioSMS`-Attribut übergebenen Einstellungsnamen dieser JSON-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="32e2e-141">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

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

    <span data-ttu-id="32e2e-142">Ersetzen Sie \<Your SID\> und \<Your Auth Token\> durch die Werte aus Ihrem Twilio-Dashboard.</span><span class="sxs-lookup"><span data-stu-id="32e2e-142">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > <span data-ttu-id="32e2e-143">Diese lokalen Einstellungen gelten nur für die lokale Ausführung.</span><span class="sxs-lookup"><span data-stu-id="32e2e-143">These local settings will be only for running locally.</span></span> <span data-ttu-id="32e2e-144">In einer Produktions-App entsprechen diese Werte den Anmeldeinformationen für das lokale Entwicklungskonto oder das Testkonto.</span><span class="sxs-lookup"><span data-stu-id="32e2e-144">In a production app, these values would be your local development or test account credentials.</span></span> <span data-ttu-id="32e2e-145">Nachdem die Azure-Funktion in Azure bereitgestellt wurde, können Sie die Produktionswerte konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="32e2e-145">Once the Azure Function has been deployed to Azure, you'll be able to configure the production values.</span></span>
    > <span data-ttu-id="32e2e-146">Wenn Sie Ihren Code in die Quellcodeverwaltung einchecken, werden diese lokalen Werte für die Anwendungseinstellungen ebenfalls eingecheckt. Seien Sie deshalb vorsichtig, und checken Sie keine tatsächlichen Werte in diese Dateien ein, wenn es sich um Open Source-Code oder öffentlich zugänglichen Code handelt.</span><span class="sxs-lookup"><span data-stu-id="32e2e-146">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>

## <a name="create-the-sms-messages"></a><span data-ttu-id="32e2e-147">Erstellen der SMS-Nachricht</span><span class="sxs-lookup"><span data-stu-id="32e2e-147">Create the SMS messages</span></span>

<span data-ttu-id="32e2e-148">Der `ICollector<SMSMessage>`-Parameter ist eine Sammlung aus `SMSMessage`-Instanzen und wird zum Erfassen der SMS-Nachrichten verwendet, die Sie senden möchten.</span><span class="sxs-lookup"><span data-stu-id="32e2e-148">The `ICollector<SMSMessage>` parameter is a collection of `SMSMessage` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="32e2e-149">Nachdem die Funktion ausgeführt wurde, werden alle Instanzen von `SMSMessage`, die dieser Sammlung hinzugefügt wurden, an Twilio übergeben und an die jeweiligen Empfänger gesendet.</span><span class="sxs-lookup"><span data-stu-id="32e2e-149">After the function has finished running, any instances of `SMSMessage` added to this collection are passed to Twilio and sent to the relevant recipients.</span></span>

1. <span data-ttu-id="32e2e-150">Fügen Sie in der `SendLocation`-Funktion Code hinzu, um die Telefonnummern in `PostData` zu durchlaufen und für jede dieser eine SMS-Nachricht zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="32e2e-150">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span>

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

    <span data-ttu-id="32e2e-151">Für die Nachricht wird eine Zieltelefonnummer und ein Textkörper benötigt, der die Google Maps-URL enthält, die aus dem Benutzerstandort erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="32e2e-151">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

1. <span data-ttu-id="32e2e-152">Protokollieren Sie jede Nachricht, und fügen Sie sie dann der `messages`-Sammlung hinzu.</span><span class="sxs-lookup"><span data-stu-id="32e2e-152">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.Info($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="32e2e-153">Die vollständige `SendLocation`-Methode wird unten gezeigt.</span><span class="sxs-lookup"><span data-stu-id="32e2e-153">The complete `SendLocation` method is shown below.</span></span>

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

## <a name="test-it-out"></a><span data-ttu-id="32e2e-154">Testen</span><span class="sxs-lookup"><span data-stu-id="32e2e-154">Test it out</span></span>

1. <span data-ttu-id="32e2e-155">Legen Sie die `ImHere.Functions`-App als Startprojekt fest, und starten Sie sie ohne Debuggen.</span><span class="sxs-lookup"><span data-stu-id="32e2e-155">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

1. <span data-ttu-id="32e2e-156">Legen Sie die `ImHere.UWP`-App als Startprojekt fest, und führen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="32e2e-156">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

1. <span data-ttu-id="32e2e-157">Geben Sie Ihre eigene Telefonnummer im internationalen Format (+\<Landeskennzahl\>\<Telefonnummer\>) in der Xamarin.Forms-App an.</span><span class="sxs-lookup"><span data-stu-id="32e2e-157">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="32e2e-158">Mit Twilio-Testkonten können Nachrichten nur an überprüfte Telefonnummern gesendet werden, deshalb können Sie bis zum Upgrade auf eine zahlungspflichtiges Konto oder bis zur Überprüfung weiterer Nummern nur Nachrichten an sich selbst senden.</span><span class="sxs-lookup"><span data-stu-id="32e2e-158">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

1. <span data-ttu-id="32e2e-159">Klicken Sie auf die Schaltfläche **Standort senden**.</span><span class="sxs-lookup"><span data-stu-id="32e2e-159">Click the **Send Location** button.</span></span> <span data-ttu-id="32e2e-160">Wenn die SMS-Nachricht erfolgreich gesendet wurde, wird eine Meldung in der Xamarin.Forms-App angezeigt, die den erfolgreichen Versand des Standorts bestätigt.</span><span class="sxs-lookup"><span data-stu-id="32e2e-160">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying, "Location sent successfully".</span></span>

    ![Die Xamarin.Forms-App zeigt an, dass der Standort gesendet wurde.](../media-drafts/7-ui-location-sent.png)

1. <span data-ttu-id="32e2e-162">In den Konsolenprotokollen für die Azure-Funktion wird angezeigt, dass die Nachricht erstellt und gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="32e2e-162">In the console logs for the Azure function, you'll see the message being created and sent.</span></span> <span data-ttu-id="32e2e-163">Wenn es zu Fehlern kommt (beispielsweise, weil die Nummer im falschen Format vorliegt), werden diese hier protokolliert.</span><span class="sxs-lookup"><span data-stu-id="32e2e-163">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![Die Konsole der Azure-Funktion zeigt an, dass die Nachricht gesendet wurde.](../media-drafts/7-function-message-sent.png)

1. <span data-ttu-id="32e2e-165">Überprüfen Sie Ihr Telefon auf Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="32e2e-165">Check your phone for a message.</span></span> <span data-ttu-id="32e2e-166">Folgen Sie dem Link in der Nachricht, um Ihren Standort anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="32e2e-166">Follow the link in the message to see your location.</span></span>

    ![SMS-Nachricht, die auf einem Mobiltelefon empfangen wird](../media-drafts/7-message-received.png)

## <a name="summary"></a><span data-ttu-id="32e2e-168">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="32e2e-168">Summary</span></span>

<span data-ttu-id="32e2e-169">In dieser Einheit haben Sie gelernt, wie Sie eine Twilio-Bindung für die Azure-Funktion erstellen und eine SMS-Nachricht mit dem Benutzerstandort an eine Funktion senden, die lokal ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="32e2e-169">In this unit, you learned how to create a Twilio binding for the Azure function and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="32e2e-170">In der nächsten Einheit veröffentlichen Sie die Funktion in Azure.</span><span class="sxs-lookup"><span data-stu-id="32e2e-170">In the next unit, you publish the function to Azure.</span></span>