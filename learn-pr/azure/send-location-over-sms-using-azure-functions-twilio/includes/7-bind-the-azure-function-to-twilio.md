<span data-ttu-id="c4d34-101">An diesem Punkt ist die mobile App vollständig und kann den Benutzerstandort und die Liste der Telefonnummern an eine Azure-Funktion senden, die die Daten deserialisieren kann.</span><span class="sxs-lookup"><span data-stu-id="c4d34-101">At this point, the mobile app is complete and it can send the user's location and list of phone numbers to an Azure function that can deserialize the data.</span></span> <span data-ttu-id="c4d34-102">In dieser Einheit binden Sie die Azure-Funktion an Twilio, um SMS zu senden.</span><span class="sxs-lookup"><span data-stu-id="c4d34-102">In this unit, you bind the Azure function to Twilio to send SMS messages.</span></span>

<span data-ttu-id="c4d34-103">Azure Functions kann mit anderen Diensten verbunden werden, entweder mit Diensten in Azure oder mit Drittanbieterdiensten.</span><span class="sxs-lookup"><span data-stu-id="c4d34-103">Azure Functions can be connected to other services, either services in Azure or third-party services.</span></span> <span data-ttu-id="c4d34-104">Diese Verbindungen – sogenannte Bindungen – liegen in zwei Formen vor: als Eingabe- und Ausgabebindungen.</span><span class="sxs-lookup"><span data-stu-id="c4d34-104">These connections, called bindings, exist in two forms - input and output bindings.</span></span> <span data-ttu-id="c4d34-105">Eingabebindungen stellen Daten für Ihre Funktion bereit, Ausgabebindungen empfangen Daten von Ihrer Funktion und senden sie an einen anderen Dienst.</span><span class="sxs-lookup"><span data-stu-id="c4d34-105">Input bindings provide data to your function and output bindings take data from your function and send it to another service.</span></span> <span data-ttu-id="c4d34-106">Weitere Informationen erhalten Sie in der [Dokumentation zu Azure Functions-Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="c4d34-106">You can read about bindings in the [Azure Functions Binding docs](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings?azure-portal=true).</span></span>

<span data-ttu-id="c4d34-107">In Visual Studio erstellte Bindungen für Azure Functions werden mithilfe von Parametern der Funktion definiert, ergänzt durch Attribute.</span><span class="sxs-lookup"><span data-stu-id="c4d34-107">Bindings for Azure Functions created in Visual Studio are defined using parameters to the function, decorated with attributes.</span></span>

## <a name="bind-the-azure-function-to-twilio"></a><span data-ttu-id="c4d34-108">Binden der Azure-Funktion an Twilio</span><span class="sxs-lookup"><span data-stu-id="c4d34-108">Bind the Azure function to Twilio</span></span>

<span data-ttu-id="c4d34-109">Um SMS-Nachrichten über Twilio zu senden, wird eine Ausgabebindung benötigt, die mit der Abonnement-ID Ihres Kontos (SID) und dem Authentifizierungstoken konfiguriert wird.</span><span class="sxs-lookup"><span data-stu-id="c4d34-109">Sending SMS messages via Twilio requires an output binding that is configured with your account subscription ID (SID) and Auth Token.</span></span>

1. <span data-ttu-id="c4d34-110">Beenden Sie die lokale Azure Functions-Runtime, falls diese in der letzten Einheit gestartet wurde und immer noch ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="c4d34-110">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="c4d34-111">Fügen Sie dem `ImHere.Functions`-Projekt das NuGet-Paket „Microsoft.Azure.WebJobs.Extensions.Twilio“ in der Version 3.0.0-rc1 hinzu.</span><span class="sxs-lookup"><span data-stu-id="c4d34-111">Add the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package v3.0.0-rc1 to the `ImHere.Functions` project.</span></span> <span data-ttu-id="c4d34-112">**Verwenden Sie genau diese Version und NICHT 3.0.0, da in der stabilen Version ein Fehler bei Twilio-Bindungen auftritt**.</span><span class="sxs-lookup"><span data-stu-id="c4d34-112">**Use version 3.0.0-rc1, NOT 3.0.0 due to a bug in the stable version with Twilio bindings**.</span></span> <span data-ttu-id="c4d34-113">Dieses NuGet-Paket enthält die relevanten Klassen für die Bindung.</span><span class="sxs-lookup"><span data-stu-id="c4d34-113">This NuGet package contains the relevant classes for the binding.</span></span>

1. <span data-ttu-id="c4d34-114">Fügen Sie der statischen `Run`-Methode in der statischen `SendLocation`-Klasse `messages` einen neuen Parameter hinzu.</span><span class="sxs-lookup"><span data-stu-id="c4d34-114">Add a new parameter to the static `Run` method on the `SendLocation` static class called `messages`.</span></span> <span data-ttu-id="c4d34-115">Dieser Parameter weist den Typ `ICollector<CreateMessageOptions>` auf.</span><span class="sxs-lookup"><span data-stu-id="c4d34-115">This parameter will have a type of `ICollector<CreateMessageOptions>`.</span></span> <span data-ttu-id="c4d34-116">Sie müssen eine `using`-Anweisung für den `Twilio.Rest.Api.V2010.Account`-Namespace hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c4d34-116">You'll need to add a `using` directive for the `Twilio.Rest.Api.V2010.Account` namespace.</span></span>

    ```cs
    [FunctionName("SendLocation")]
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,"get", "post", Route = null)]HttpRequestMessage req,
                                                ICollector<CreateMessageOptions> messages,
                                                ILogger log)
    ```

1. <span data-ttu-id="c4d34-117">Ergänzen Sie den neuen `messages`-Parameter wie folgt um das `TwilioSms`-Attribut:</span><span class="sxs-lookup"><span data-stu-id="c4d34-117">Decorate the new `messages` parameter with the `TwilioSms` attribute as follows:</span></span> 

      ```cs
    [TwilioSms(AccountSidSetting = "TwilioAccountSid",AuthTokenSetting = "TwilioAuthToken", From = "+1xxxxxxxxx")]ICollector<CreateMessageOptions> messages,
    ```
    <span data-ttu-id="c4d34-118">Dieses Attribut umfasst drei Parameter, die Sie festlegen müssen:</span><span class="sxs-lookup"><span data-stu-id="c4d34-118">This attribute has three parameters you need to set:</span></span>

    * <span data-ttu-id="c4d34-119">Legen Sie **AccountSidSetting** auf `"TwilioAccountSid"` fest.</span><span class="sxs-lookup"><span data-stu-id="c4d34-119">**AccountSidSetting** - set this to `"TwilioAccountSid"`</span></span>
  
        <span data-ttu-id="c4d34-120">Dies ist die SID für Ihr Twilio-Konto, die Sie sich zuvor in diesem Modul notiert haben.</span><span class="sxs-lookup"><span data-stu-id="c4d34-120">This is the SID for your Twilio account that you recorded earlier in the module.</span></span> <span data-ttu-id="c4d34-121">Die SID wird nicht direkt, sondern über einen Parameter festgelegt, der dem Namen eines Werts in den Einstellungen der Funktions-App entspricht und zum Abrufen der SID verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="c4d34-121">Rather than set the SID directly, this parameter is the name of a value in the function app settings that will be used to retrieve the SID.</span></span>

    * <span data-ttu-id="c4d34-122">Legen Sie **AuthTokenSetting** auf `"TwilioAuthToken"` fest.</span><span class="sxs-lookup"><span data-stu-id="c4d34-122">**AuthTokenSetting** - set this to `"TwilioAuthToken"`</span></span>

       <span data-ttu-id="c4d34-123">Dies ist das Authentifizierungstoken für Ihr Twilio-Konto an, das Sie sich zuvor in diesem Modul notiert haben.</span><span class="sxs-lookup"><span data-stu-id="c4d34-123">This is the Auth Token for your Twilio account that you recorded earlier in the module.</span></span> <span data-ttu-id="c4d34-124">Das Authentifizierungstoken wird nicht direkt, sondern über diesen Parameter festgelegt, der dem Namen eines Werts in den Einstellungen der Funktions-App entspricht und zum Abrufen des Authentifizierungstokens verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="c4d34-124">Rather than set the Auth Token directly, this parameter is the name of a value in the function app settings that will be used to retrieve the Auth Token.</span></span>

    * <span data-ttu-id="c4d34-125">Legen Sie **From** auf Ihre aktive Twilio-Telefonnummer fest, die Sie sich zuvor in diesem Modul notiert haben.</span><span class="sxs-lookup"><span data-stu-id="c4d34-125">**From** - set this to your Twilio active phone number that you recorded earlier in the module.</span></span>

        <span data-ttu-id="c4d34-126">Die Twilio-Telefonnummer, von der die SMS-Nachrichten gesendet werden. Die Telefonnummer wird im internationalen Format angegeben (+\<Landeskennzahl\>\<Telefonnummer\>, Beispiel: „+1555123456“).</span><span class="sxs-lookup"><span data-stu-id="c4d34-126">The Twilio phone number that the SMS messages will come from in international format (+\<country code\>\<phone number\>, for example "+1555123456").</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c4d34-127">Stellen Sie sicher, dass die Telefonnummer keine Leerzeichen enthält.</span><span class="sxs-lookup"><span data-stu-id="c4d34-127">Make sure to remove all spaces from the phone number.</span></span>


1. <span data-ttu-id="c4d34-128">Einstellungen der Funktions-App können lokal in der `local.settings.json`-Datei konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="c4d34-128">Function app settings can be configured locally inside the `local.settings.json` file.</span></span> <span data-ttu-id="c4d34-129">Fügen Sie die SID für Ihr Twilio-Konto und das Authentifizierungstoken mithilfe der an das `TwilioSMS`-Attribut übergebenen Einstellungsnamen dieser JSON-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="c4d34-129">Add your Twilio account SID and Auth Token to this JSON file using the setting names that were passed to the `TwilioSMS` attribute.</span></span>

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

    <span data-ttu-id="c4d34-130">Ersetzen Sie \<Your SID\> und \<Your Auth Token\> durch die Werte aus Ihrem Twilio-Dashboard.</span><span class="sxs-lookup"><span data-stu-id="c4d34-130">Replace \<Your SID\> and \<Your Auth Token\> with the values from your Twilio dashboard.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4d34-131">Diese lokalen Einstellungen gelten nur für die lokale Ausführung.</span><span class="sxs-lookup"><span data-stu-id="c4d34-131">These local settings will be only for running locally.</span></span> <span data-ttu-id="c4d34-132">In einer Produktions-App entsprechen diese Werte den Anmeldeinformationen für das lokale Entwicklungskonto oder das Testkonto.</span><span class="sxs-lookup"><span data-stu-id="c4d34-132">In a production app, these values would be your local development or test account credentials.</span></span> <span data-ttu-id="c4d34-133">Nachdem die Azure-Funktion in Azure bereitgestellt wurde, können Sie die Produktionswerte konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="c4d34-133">Once the Azure Function has been deployed to Azure, you'll be able to configure the production values.</span></span>

     > [!NOTE]
    > <span data-ttu-id="c4d34-134">Wenn Sie Ihren Code in die Quellcodeverwaltung einchecken, werden diese lokalen Werte für die Anwendungseinstellungen ebenfalls eingecheckt. Seien Sie deshalb vorsichtig, und checken Sie keine tatsächlichen Werte in diese Dateien ein, wenn es sich um Open Source-Code oder öffentlich zugänglichen Code handelt.</span><span class="sxs-lookup"><span data-stu-id="c4d34-134">If you check your code into source control, these local application setting values will be checked in, too, so be careful not to check in any actual values in these files if your code is open source or public in any form.</span></span>
    

## <a name="create-the-sms-messages"></a><span data-ttu-id="c4d34-135">Erstellen der SMS-Nachricht</span><span class="sxs-lookup"><span data-stu-id="c4d34-135">Create the SMS messages</span></span>

<span data-ttu-id="c4d34-136">Der `ICollector<CreateMessageOptions>`-Parameter ist eine Sammlung von `CreateMessageOptions`-Instanzen und wird zum Erfassen der SMS-Nachrichten verwendet, die Sie senden möchten.</span><span class="sxs-lookup"><span data-stu-id="c4d34-136">The `ICollector<CreateMessageOptions>` parameter is a collection of `CreateMessageOptions` instances and is used to collect the SMS messages you want to send.</span></span> <span data-ttu-id="c4d34-137">Nachdem die Funktion ausgeführt wurde, werden alle Instanzen von `CreateMessageOptions`, die dieser Sammlung hinzugefügt wurden, an Twilio übergeben. Mit diesen werden dann Nachrichten erstellt, die an die jeweiligen Empfänger gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="c4d34-137">After the function has finished running, any instances of `CreateMessageOptions` added to this collection are passed to Twilio and used to create messages to be sent to the relevant recipients.</span></span>

1. <span data-ttu-id="c4d34-138">Fügen Sie der `SendLocation`-Funktion Code hinzu, mit dem in einer Schleife die Telefonnummern in `PostData` durchlaufen werden, und erstellen Sie für jede eine SMS-Nachricht.</span><span class="sxs-lookup"><span data-stu-id="c4d34-138">In the `SendLocation` function, add code to loop through the phone numbers in the `PostData` and create an SMS message for each one.</span></span> <span data-ttu-id="c4d34-139">Sie müssen eine using-Anweisung für `Twilio.Types` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c4d34-139">You will need to add a using directive for `Twilio.Types`.</span></span>

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

    <span data-ttu-id="c4d34-140">Für die Nachricht wird eine Zieltelefonnummer und ein Textkörper benötigt, der die Google Maps-URL enthält, die aus dem Benutzerstandort erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="c4d34-140">The message needs the phone number to send to and a body that contains the Google Maps URL created from the user's location.</span></span>

1. <span data-ttu-id="c4d34-141">Protokollieren Sie jede Nachricht, und fügen Sie sie dann der `messages`-Sammlung hinzu.</span><span class="sxs-lookup"><span data-stu-id="c4d34-141">Log each message, and then add it to the `messages` collection.</span></span>

    ```cs
    foreach (string toNo in data.ToNumbers)
    {
        ...
        log.LogInformation($"Creating SMS message to {message.To}, message is '{message.Body}'.");
        messages.Add(message);
    }
    ```

<span data-ttu-id="c4d34-142">Die vollständige `SendLocation`-Methode wird unten gezeigt.</span><span class="sxs-lookup"><span data-stu-id="c4d34-142">The complete `SendLocation` method is shown below.</span></span> <span data-ttu-id="c4d34-143">Der Platzhalter innerhalb des `From`-Parameters müsste durch Ihre aktive Telefonnummer ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="c4d34-143">Your active phone number would replace the placeholder in the `From` parameter.</span></span>

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

## <a name="test-it-out"></a><span data-ttu-id="c4d34-144">Testen</span><span class="sxs-lookup"><span data-stu-id="c4d34-144">Test it out</span></span>

1. <span data-ttu-id="c4d34-145">Legen Sie die `ImHere.Functions`-App als Startprojekt fest, und starten Sie sie ohne Debuggen.</span><span class="sxs-lookup"><span data-stu-id="c4d34-145">Set the `ImHere.Functions` app as the startup project and start it without debugging.</span></span>

1. <span data-ttu-id="c4d34-146">Legen Sie die `ImHere.UWP`-App als Startprojekt fest, und führen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="c4d34-146">Set the `ImHere.UWP` app as the startup project and run it.</span></span>

1. <span data-ttu-id="c4d34-147">Geben Sie Ihre eigene Telefonnummer im internationalen Format (+\<Landeskennzahl\>\<Telefonnummer\>) in der Xamarin.Forms-App an.</span><span class="sxs-lookup"><span data-stu-id="c4d34-147">Enter your own phone number in international format (+\<country code\>\<phone number\>) into the Xamarin.Forms app.</span></span> <span data-ttu-id="c4d34-148">Mit Twilio-Testkonten können Nachrichten nur an überprüfte Telefonnummern gesendet werden, deshalb können Sie bis zum Upgrade auf eine zahlungspflichtiges Konto oder bis zur Überprüfung weiterer Nummern nur Nachrichten an sich selbst senden.</span><span class="sxs-lookup"><span data-stu-id="c4d34-148">Twilio trial accounts can send  messages only to verified phone numbers, so for now, you'll only be able to message yourself unless you upgrade to a paid account or verify other numbers.</span></span>

1. <span data-ttu-id="c4d34-149">Klicken Sie auf die Schaltfläche **Standort senden**.</span><span class="sxs-lookup"><span data-stu-id="c4d34-149">Click the **Send Location** button.</span></span> <span data-ttu-id="c4d34-150">Wenn die SMS-Nachricht erfolgreich gesendet wurde, wird eine Meldung in der Xamarin.Forms-App angezeigt, die den erfolgreichen Versand des Standorts bestätigt.</span><span class="sxs-lookup"><span data-stu-id="c4d34-150">If the SMS message was sent successfully, you'll see a message in the Xamarin.Forms app saying, "Location sent successfully".</span></span>

    ![Die Xamarin.Forms-App zeigt an, dass der Standort gesendet wurde.](../media/7-ui-location-sent.png)

1. <span data-ttu-id="c4d34-152">In den Konsolenprotokollen für die Azure-Funktion wird angezeigt, dass die Nachricht erstellt und gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="c4d34-152">In the console logs for the Azure function, you'll see the message being created and sent.</span></span> <span data-ttu-id="c4d34-153">Wenn es zu Fehlern kommt (beispielsweise, weil die Nummer im falschen Format vorliegt), werden diese hier protokolliert.</span><span class="sxs-lookup"><span data-stu-id="c4d34-153">If any errors occur (such as, the number is in the wrong format), they will be logged out here.</span></span>

    ![Die Konsole der Azure-Funktion zeigt an, dass die Nachricht gesendet wurde.](../media/7-function-message-sent.png)

1. <span data-ttu-id="c4d34-155">Überprüfen Sie Ihr Telefon auf Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="c4d34-155">Check your phone for a message.</span></span> <span data-ttu-id="c4d34-156">Folgen Sie dem Link in der Nachricht, um Ihren Standort anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c4d34-156">Follow the link in the message to see your location.</span></span>

    ![SMS-Nachricht, die auf einem Mobiltelefon empfangen wird](../media/7-message-received.png)

    > [!TIP]
    > <span data-ttu-id="c4d34-158">Der angezeigte Standort ist der Ausführungsort der App und befindet sich in der Nähe des Rechenzentrums, über das der virtuelle Computer ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="c4d34-158">The location you'll see is the location where the app is running, so will be near to the data center that the VM is running from.</span></span> <span data-ttu-id="c4d34-159">Würde diese App auf Ihrem lokalen Gerät ausgeführt, würde Ihr Standort angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c4d34-159">If this app was running on your local device then it would show your location.</span></span>

## <a name="summary"></a><span data-ttu-id="c4d34-160">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c4d34-160">Summary</span></span>

<span data-ttu-id="c4d34-161">In dieser Einheit haben Sie gelernt, wie Sie eine Twilio-Bindung für die Azure-Funktion erstellen und eine SMS-Nachricht mit dem Benutzerstandort an eine Funktion senden, die lokal ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="c4d34-161">In this unit, you learned how to create a Twilio binding for the Azure function and send an SMS message with the user's location to a function that was running locally.</span></span> <span data-ttu-id="c4d34-162">In der nächsten Einheit veröffentlichen Sie die Funktion in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d34-162">In the next unit, you publish the function to Azure.</span></span>
