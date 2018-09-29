<span data-ttu-id="92eb4-101">An diesem Punkt ist die mobile App vollständig und kann den Benutzerstandort und die Liste der Telefonnummern an eine Azure-Funktion senden, die die Daten deserialisieren kann.</span><span class="sxs-lookup"><span data-stu-id="92eb4-101">At this point, the mobile app is complete and it can send the user's location and list of phone numbers to an Azure function that can deserialize the data.</span></span> <span data-ttu-id="92eb4-102">In dieser Einheit binden Sie die Azure-Funktion an Twilio, um SMS zu senden.</span><span class="sxs-lookup"><span data-stu-id="92eb4-102">In this unit, you bind the Azure function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="92eb4-103">Azure Functions kann mit anderen Diensten verbunden werden, entweder mit Diensten in Azure oder mit Drittanbieterdiensten.</span><span class="sxs-lookup"><span data-stu-id="92eb4-103">Azure Functions can be connected to other services, either services in Azure or third-party services.</span></span> <span data-ttu-id="92eb4-104">Diese Verbindungen – sogenannte Bindungen – liegen in zwei Formen vor: als Eingabe- und Ausgabebindungen.</span><span class="sxs-lookup"><span data-stu-id="92eb4-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="92eb4-105">Eingabebindungen stellen Daten für Ihre Funktion bereit, Ausgabebindungen empfangen Daten von Ihrer Funktion und senden sie an einen anderen Dienst.</span><span class="sxs-lookup"><span data-stu-id="92eb4-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="92eb4-106">Weitere Informationen erhalten Sie in der [Dokumentation zu Azure Functions-Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="92eb4-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true).</span></span>

<span data-ttu-id="92eb4-107">In Visual Studio erstellte Bindungen für Azure Functions werden mithilfe von Parametern der Funktion definiert, ergänzt durch Attribute.</span><span class="sxs-lookup"><span data-stu-id="92eb4-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-function-to-twilio"></a><span data-ttu-id="92eb4-108">Binden der Azure-Funktion an Twilio</span><span class="sxs-lookup"><span data-stu-id="92eb4-108">Bind the Azure function to Twilio</span></span>

<span data-ttu-id="92eb4-109">Um SMS-Nachrichten über Twilio zu senden, wird eine Ausgabebindung benötigt, die mit der Abonnement-ID Ihres Kontos (SID) und dem Authentifizierungstoken konfiguriert wird.</span><span class="sxs-lookup"><span data-stu-id="92eb4-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="92eb4-110">Beenden Sie die lokale Azure Functions-Runtime, wenn diese noch von der vorherigen Einheit ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="92eb4-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

2. <span data-ttu-id="92eb4-111">Fügen Sie dem `ImHere.Functions`-Projekt das NuGet-Paket „Microsoft.Azure.WebJobs.Extensions.Twilio“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="92eb4-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package to the `ImHere.Functions` project.</span></span> <span data-ttu-id="92eb4-112">Dieses NuGet-Paket enthält die relevanten Klassen für die Bindung.</span><span class="sxs-lookup"><span data-stu-id="92eb4-112">This NuGet package contains the relevant classes for the binding.</span></span>

3. <span data-ttu-id="92eb4-113">Fügen Sie der statischen `Run`-Methode in der statischen `SendLocation`-Klasse `messages` einen neuen Parameter hinzu.</span><span class="sxs-lookup"><span data-stu-id="92eb4-113">Add a new parameter to the static `Run` method on the `SendLocation` static class called `messages`.</span></span> <span data-ttu-id="92eb4-114">Dieser Parameter weist den Typ `ICollector<CreateMessageOptions>` auf.</span><span class="sxs-lookup"><span data-stu-id="92eb4-114">This parameter will have a type of `ICollector<CreateMessageOptions>`.</span></span> <span data-ttu-id="92eb4-115">Sie müssen eine `using`-Anweisung für den `Twilio.Rest.Api.V2010.Account`-Namespace hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="92eb4-115">You'll need to add a `using` directive for the `Twilio.Rest.Api.V2010.Account` namespace.</span></span>

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,"get", "post", Route = null)]HttpRequestMessage req,
                                                ICollector<CreateMessageOptions> messages,
                                                ILogger log)
    ```

4. <span data-ttu-id="92eb4-116">Ergänzen Sie den neuen `messages`-Parameter wie folgt um das `TwilioSms`-Attribut:</span><span class="sxs-lookup"><span data-stu-id="92eb4-116">Decorate the new `messages` parameter with the `TwilioSms` attribute as follows:</span></span> 

      ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",AuthTokenSetting = "TwilioAuthToken", From = "+1xxxxxxxxx")]ICollector<CreateMessageOptions> messages,
    ```
    <span data-ttu-id="92eb4-117">Dieses Attribut umfasst drei Parameter, die Sie festlegen müssen:</span><span class="sxs-lookup"><span data-stu-id="92eb4-117">This attribute has three parameters you need to set:</span></span>

    * <span data-ttu-id="92eb4-118">Legen Sie **AccountSidSetting** auf `"TwilioAccountSid"` fest.</span><span class="sxs-lookup"><span data-stu-id="92eb4-118">**AccountSidSetting** - set this to `"TwilioAccountSid"`</span></span>
  
        <span data-ttu-id="92eb4-119">Dies ist die SID für Ihr Twilio-Konto, die Sie sich zuvor in diesem Modul notiert haben.</span><span class="sxs-lookup"><span data-stu-id="92eb4-119">This is the SID for your Twilio account that you recorded earlier in the module.</span></span> <span data-ttu-id="92eb4-120">Die SID wird nicht direkt, sondern über einen Parameter festgelegt, der dem Namen eines Werts in den Einstellungen der Funktions-App entspricht und zum Abrufen der SID verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="92eb4-120">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span>

    * <span data-ttu-id="92eb4-121">Legen Sie **AuthTokenSetting** auf `"TwilioAuthToken"` fest.</span><span class="sxs-lookup"><span data-stu-id="92eb4-121">**AuthTokenSetting** - set this to `"TwilioAuthToken"`</span></span>

       <span data-ttu-id="92eb4-122">Dies ist das Authentifizierungstoken für Ihr Twilio-Konto an, das Sie sich zuvor in diesem Modul notiert haben.</span><span class="sxs-lookup"><span data-stu-id="92eb4-122">This is the Auth Token for your Twilio account that you recorded earlier in the module.</span></span> <span data-ttu-id="92eb4-123">Das Authentifizierungstoken wird nicht direkt, sondern über diesen Parameter festgelegt, der dem Namen eines Werts in den Einstellungen der Funktions-App entspricht und zum Abrufen des Authentifizierungstokens verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="92eb4-123">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span>

    * <span data-ttu-id="92eb4-124">Legen Sie **From** auf Ihre aktive Twilio-Telefonnummer fest, die Sie sich zuvor in diesem Modul notiert haben.</span><span class="sxs-lookup"><span data-stu-id="92eb4-124">**From** - set this to your Twilio active phone number that you recorded earlier in the module.</span></span>

        <span data-ttu-id="92eb4-125">Die Twilio-Telefonnummer, von der die SMS-Nachrichten gesendet werden. Die Telefonnummer wird im internationalen Format angegeben (+\<Landeskennzahl\>\<Telefonnummer\>, Beispiel: „+1555123456“).</span><span class="sxs-lookup"><span data-stu-id="92eb4-125">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="92eb4-126">Stellen Sie sicher, dass die Telefonnummer keine Leerzeichen enthält.</span><span class="sxs-lookup"><span data-stu-id="92eb4-126">Make sure to remove all spaces from the phone number.</span></span>

5. <span data-ttu-id="92eb4-127">Einstellungen der Funktions-App können lokal in der `local.settings.json`-Datei konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="92eb4-127">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="92eb4-128">Fügen Sie die SID für Ihr Twilio-Konto und das Authentifizierungstoken mithilfe der an das `TwilioSMS`-Attribut übergebenen Einstellungsnamen dieser JSON-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="92eb4-128">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

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

    <span data-ttu-id="92eb4-129">Ersetzen Sie \<Your SID\> und \<Your Auth Token\> durch die Werte aus Ihrem Twilio-Dashboard.</span><span class="sxs-lookup"><span data-stu-id="92eb4-129">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92eb4-130">Diese lokalen Einstellungen gelten nur für die lokale Ausführung.</span><span class="sxs-lookup"><span data-stu-id="92eb4-130">These local settings will be only for running locally.</span></span> <span data-ttu-id="92eb4-131">In einer Produktions-App entsprechen diese Werte den Anmeldeinformationen für das lokale Entwicklungskonto oder das Testkonto.</span><span class="sxs-lookup"><span data-stu-id="92eb4-131">In a production app, these values would be your local development or test account credentials.</span></span> <span data-ttu-id="92eb4-132">Nachdem die Azure-Funktion in Azure bereitgestellt wurde, können Sie die Produktionswerte konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="92eb4-132">Once the Azure Function has been deployed to Azure, you'll be able to configure the production values.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92eb4-133">Wenn Sie Ihren Code in die Quellcodeverwaltung einchecken, werden diese lokalen Werte für die Anwendungseinstellungen ebenfalls eingecheckt. Seien Sie deshalb vorsichtig, und checken Sie keine tatsächlichen Werte in diese Dateien ein, wenn es sich um Open Source-Code oder öffentlich zugänglichen Code handelt.</span><span class="sxs-lookup"><span data-stu-id="92eb4-133">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>

## <a name="create-the-sms-messages"></a><span data-ttu-id="92eb4-134">Erstellen der SMS-Nachricht</span><span class="sxs-lookup"><span data-stu-id="92eb4-134">Create the SMS messages</span></span>

<span data-ttu-id="92eb4-135">Der `ICollector<CreateMessageOptions>`-Parameter ist eine Sammlung von `CreateMessageOptions`-Instanzen und wird zum Erfassen der SMS-Nachrichten verwendet, die Sie senden möchten.</span><span class="sxs-lookup"><span data-stu-id="92eb4-135">The `ICollector<CreateMessageOptions>` parameter is a collection of `CreateMessageOptions` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="92eb4-136">Nachdem die Funktion ausgeführt wurde, werden alle Instanzen von `CreateMessageOptions`, die dieser Sammlung hinzugefügt wurden, an Twilio übergeben. Mit diesen werden dann Nachrichten erstellt, die an die jeweiligen Empfänger gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="92eb4-136">After the function has finished running, any instances of `CreateMessageOptions` added to this collection are passed to Twilio and used to create messages to be sent to the relevant recipients.</span></span>

1. <span data-ttu-id="92eb4-137">Fügen Sie der `SendLocation`-Funktion Code hinzu, mit dem in einer Schleife die Telefonnummern in `PostData` durchlaufen werden, und erstellen Sie für jede eine SMS-Nachricht.</span><span class="sxs-lookup"><span data-stu-id="92eb4-137">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span> <span data-ttu-id="92eb4-138">Sie müssen eine using-Anweisung für `Twilio.Types` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="92eb4-138">You will need to add a using directive for `Twilio.Types`.</span></span>

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

    <span data-ttu-id="92eb4-139">Für die Nachricht wird eine Zieltelefonnummer und ein Textkörper benötigt, der die Google Maps-URL enthält, die aus dem Benutzerstandort erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="92eb4-139">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

1. <span data-ttu-id="92eb4-140">Protokollieren Sie jede Nachricht, und fügen Sie sie dann der `messages`-Sammlung hinzu.</span><span class="sxs-lookup"><span data-stu-id="92eb4-140">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="92eb4-141">Die vollständige `SendLocation`-Methode wird unten gezeigt.</span><span class="sxs-lookup"><span data-stu-id="92eb4-141">The complete `SendLocation` method is shown below.</span></span> <span data-ttu-id="92eb4-142">Der Platzhalter innerhalb des `From`-Parameters müsste durch Ihre aktive Telefonnummer ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="92eb4-142">Your active phone number would replace the placeholder in the `From` parameter.</span></span>

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

## <a name="test-it-out"></a><span data-ttu-id="92eb4-143">Testen</span><span class="sxs-lookup"><span data-stu-id="92eb4-143">Test it out</span></span>

1. <span data-ttu-id="92eb4-144">Legen Sie die `ImHere.Functions`-App als Startprojekt fest, und starten Sie sie ohne Debuggen.</span><span class="sxs-lookup"><span data-stu-id="92eb4-144">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

1. <span data-ttu-id="92eb4-145">Legen Sie die `ImHere.UWP`-App als Startprojekt fest, und führen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="92eb4-145">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

1. <span data-ttu-id="92eb4-146">Geben Sie Ihre eigene Telefonnummer im internationalen Format (+\<Landeskennzahl\>\<Telefonnummer\>) in der Xamarin.Forms-App an.</span><span class="sxs-lookup"><span data-stu-id="92eb4-146">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="92eb4-147">Mit Twilio-Testkonten können Nachrichten nur an überprüfte Telefonnummern gesendet werden, deshalb können Sie bis zum Upgrade auf eine zahlungspflichtiges Konto oder bis zur Überprüfung weiterer Nummern nur Nachrichten an sich selbst senden.</span><span class="sxs-lookup"><span data-stu-id="92eb4-147">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

1. <span data-ttu-id="92eb4-148">Klicken Sie auf die Schaltfläche **Standort senden**.</span><span class="sxs-lookup"><span data-stu-id="92eb4-148">Click the **Send Location** button.</span></span> <span data-ttu-id="92eb4-149">Wenn die SMS-Nachricht erfolgreich gesendet wurde, wird eine Meldung in der Xamarin.Forms-App angezeigt, die den erfolgreichen Versand des Standorts bestätigt.</span><span class="sxs-lookup"><span data-stu-id="92eb4-149">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying, "Location sent successfully".</span></span>

    ![Die Xamarin.Forms-App zeigt an, dass der Standort gesendet wurde.](../media/7-ui-location-sent.png)

1. <span data-ttu-id="92eb4-151">In den Konsolenprotokollen für die Azure-Funktion wird angezeigt, dass die Nachricht erstellt und gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="92eb4-151">In the console logs for the Azure function, you'll see the message being created and sent.</span></span> <span data-ttu-id="92eb4-152">Wenn es zu Fehlern kommt (beispielsweise, weil die Nummer im falschen Format vorliegt), werden diese hier protokolliert.</span><span class="sxs-lookup"><span data-stu-id="92eb4-152">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![Die Konsole der Azure-Funktion zeigt an, dass die Nachricht gesendet wurde.](../media/7-function-message-sent.png)

1. <span data-ttu-id="92eb4-154">Überprüfen Sie Ihr Telefon auf Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="92eb4-154">Check your phone for a message.</span></span> <span data-ttu-id="92eb4-155">Folgen Sie dem Link in der Nachricht, um Ihren Standort anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="92eb4-155">Follow the link in the message to see your location.</span></span>

    ![SMS-Nachricht, die auf einem Mobiltelefon empfangen wird](../media/7-message-received.png)

    > [!TIP]
    > <span data-ttu-id="92eb4-157">Der angezeigte Standort ist der Ausführungsort der App und befindet sich in der Nähe des Rechenzentrums, über das der virtuelle Computer ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="92eb4-157">The location you'll see is the location where the app is running, so will be near to the data center that the VM is running from.</span></span> <span data-ttu-id="92eb4-158">Würde diese App auf Ihrem lokalen Gerät ausgeführt, würde Ihr Standort angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="92eb4-158">If this app was running on your local device then it would show your location.</span></span>

## <a name="summary"></a><span data-ttu-id="92eb4-159">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="92eb4-159">Summary</span></span>

<span data-ttu-id="92eb4-160">In dieser Einheit haben Sie gelernt, wie Sie eine Twilio-Bindung für die Azure-Funktion erstellen und eine SMS-Nachricht mit dem Benutzerstandort an eine Funktion senden, die lokal ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="92eb4-160">In this unit, you learned how to create a Twilio binding for the Azure function and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="92eb4-161">In der nächsten Einheit veröffentlichen Sie die Funktion in Azure.</span><span class="sxs-lookup"><span data-stu-id="92eb4-161">In the next unit, you publish the function to Azure.</span></span>
