<span data-ttu-id="e9ad5-101">Lassen Sie uns wir mit unserem Zahnradsteuerungs-Beispiel fortfahren und die Logik für den Temperaturdienst hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-101">Let's continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="e9ad5-102">Insbesondere werden wir Daten von einer HTTP-Anforderung empfangen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="e9ad5-103">Anforderungen an die Funktion</span><span class="sxs-lookup"><span data-stu-id="e9ad5-103">Function requirements</span></span>

<span data-ttu-id="e9ad5-104">Zuerst müssen wir einige Anforderungen an unsere Logik definieren:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-104">First, we need to define some requirements for our logic:</span></span>

- <span data-ttu-id="e9ad5-105">Temperaturen von 0 bis 25 sollen mit **OK** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-105">Temperatures between 0-25 should be flagged as **OK**.</span></span>
- <span data-ttu-id="e9ad5-106">Temperaturen von 26 bis 50 sollen mit **CAUTION** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-106">Temperatures between 26-50 should be flagged as **CAUTION**.</span></span>
- <span data-ttu-id="e9ad5-107">Temperaturen über 50 sollen mit **DANGER** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-107">Temperatures above 50 should be flagged as **DANGER**.</span></span>

## <a name="add-a-function-to-our-function-app"></a><span data-ttu-id="e9ad5-108">Hinzufügen einer Funktion zu unserer Funktions-App</span><span class="sxs-lookup"><span data-stu-id="e9ad5-108">Add a function to our function app</span></span>

<span data-ttu-id="e9ad5-109">Wie in der vorherigen Einheit bereits erläutert wurde, verfügt Azure über Vorlagen, die Ihnen das Erstellen von Funktionen erleichtern.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-109">As we discussed in the preceding unit, Azure provides templates that help you get started building functions.</span></span> <span data-ttu-id="e9ad5-110">In dieser Einheit verwenden wir die Vorlage `HttpTrigger`, um den Temperaturdienst zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-110">In this unit, we'll use the `HttpTrigger` template to implement the temperature service.</span></span>

1. <span data-ttu-id="e9ad5-111">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-111">Sign in to the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true).</span></span>

1. <span data-ttu-id="e9ad5-112">Wählen Sie durch Auswahl von **Alle Ressourcen** im linken Menü die Ressourcengruppe aus der ersten Übung und dann **<rgn>[Name der Sandboxressourcengruppe]</rgn>** aus.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-112">Select the resource group from the first exercise by choosing **All resources** in the left-hand menu, and then selecting "**<rgn>[sandbox resource group name]</rgn>**".</span></span>

1. <span data-ttu-id="e9ad5-113">Daraufhin werden die Ressourcen für die Gruppe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-113">The resources for the group will then be displayed.</span></span> <span data-ttu-id="e9ad5-114">Klicken Sie auf den Namen der Funktions-App, die Sie in der vorherigen Übung erstellt haben, indem Sie das Element **escalator-functions-xxxxxxx** (auch durch das Blitzsymbol gekennzeichnet) auswählen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-114">Click the name of the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt Function icon).</span></span>

    ![Screenshot: Das hervorgehobene Blatt „Alle Ressourcen“ sowie die erstellte App „escalator-functions“ im Azure-Portal.](../media/5-access-function-app.png)

1. <span data-ttu-id="e9ad5-116">Klicken Sie neben **Funktionen** auf die Schaltfläche „Hinzufügen“ (**+**).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-116">Select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="e9ad5-117">Durch diese Aktion wird die Funktionserstellung gestartet.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-117">This action starts the function creation process.</span></span>

1. <span data-ttu-id="e9ad5-118">Wählen Sie auf der Seite **Azure Functions for JavaScript - getting started** (Erste Schritte mit Azure Functions für JavaScript) die Option **Im Portal** und anschließend **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-118">On the **Azure Functions for JavaScript - getting started** page, select **In-portal** and then select **continue**.</span></span>

1. <span data-ttu-id="e9ad5-119">Klicken Sie im Schritt **Create a function** (Funktion erstellen) auf **More templates...** (Mehr Vorlagen...) und dann auf **Finish and view templates** (Fertig stellen und Vorlagen anzeigen).</span><span class="sxs-lookup"><span data-stu-id="e9ad5-119">In the **Create a function** step, select **More templates...** and then select **Finish and view templates**.</span></span>

1. <span data-ttu-id="e9ad5-120">Wählen Sie aus der Liste aller für die Funktions-App verfügbaren Vorlagen **HTTP trigger** (HTTP-Trigger) aus.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-120">In the list of all templates available to this function app, select **Http trigger** .</span></span>

1. <span data-ttu-id="e9ad5-121">Geben Sie im angezeigten Dialogfeld **Neue Funktion** **DriveGearTemperatureService** in das Namensfeld ein.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-121">Enter **DriveGearTemperatureService** in the name field of the **New Function** dialog that appears.</span></span> <span data-ttu-id="e9ad5-122">Belassen Sie die Autorisierungsstufe auf „Funktion“, und klicken Sie auf die Schaltfläche **Erstellen**, um die Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-122">Leave the Authorization level as "Function" and press the **Create** button to create the function.</span></span>

1. <span data-ttu-id="e9ad5-123">Nach Abschluss der Funktionserstellung wird der Code-Editor mit dem Inhalt der Codedatei *index.js* geöffnet.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-123">When your function creation completes, the code editor opens with the contents of the *index.js* code file.</span></span> <span data-ttu-id="e9ad5-124">Der Standardcode, den die Vorlage für uns generiert hat, wird im folgenden Codeausschnitt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-124">The default code that the template generated for us is listed in the following snippet.</span></span>

    ```javascript
    module.exports = function (context, req) {
        context.log('JavaScript HTTP trigger function processed a request.');
    
        if (req.query.name || (req.body && req.body.name)) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "Hello " + (req.query.name || req.body.name)
            };
        }
        else {
            context.res = {
                status: 400,
                body: "Please pass a name on the query string or in the request body"
            };
        }
        context.done();
    };
    ```

    <span data-ttu-id="e9ad5-125">Unsere-Funktion erwartet einen Namen, der entweder über die Abfragezeichenfolge der HTTP-Anforderung oder als Teil des Anforderungstexts übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-125">Our function expects a name to be passed in either through the HTTP request query string or as part of the request body.</span></span> <span data-ttu-id="e9ad5-126">Die Funktion antwortet mit der Meldung **Hello, {Name}**, die den in der Anforderung gesendeten Namen wiedergibt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-126">The function responds by returning the message  **Hello, {name}**, echoing back the name that was sent in the request.</span></span>

    <span data-ttu-id="e9ad5-127">Auf der rechten Seite der Quellansicht sehen Sie zwei Registerkarten.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-127">On the right-hand side of the source view, you'll find two tabs.</span></span> <span data-ttu-id="e9ad5-128">Auf der Registerkarte **Datei anzeigen** werden der Code und die Konfigurationsdatei Ihrer Funktion aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-128">The **View files** tab lists the code and config file for your function.</span></span>  <span data-ttu-id="e9ad5-129">Wählen Sie **function.json** aus, um die Konfiguration der Funktion anzuzeigen, die in etwa wie folgt aussehen sollte:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-129">Select **function.json** to view the configuration of the function, which should look like the following:</span></span>

    ```javascript
    {
        "disabled": false,
        "bindings": [
        {
            "authLevel": "function",
            "type": "httpTrigger",
            "direction": "in",
            "name": "req"
        },
        {
            "type": "http",
            "direction": "out",
            "name": "res"
        }
        ]
    }
    ```

    <span data-ttu-id="e9ad5-130">Diese Konfiguration deklariert, dass die Funktion ausgeführt wird, sobald sie eine HTTP-Anforderung empfängt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-130">This configuration declares that the function runs when it receives an HTTP request.</span></span> <span data-ttu-id="e9ad5-131">Die Ausgabebindung deklariert, dass die Antwort als HTTP-Antwort gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-131">The output binding declares that the response will be sent as an HTTP response.</span></span>    

## <a name="test-the-function"></a><span data-ttu-id="e9ad5-132">Testen der Funktion</span><span class="sxs-lookup"><span data-stu-id="e9ad5-132">Test the function</span></span>

> [!TIP]
> <span data-ttu-id="e9ad5-133">**cURL** ist ein Befehlszeilentool, das zum Senden und Empfangen von Dateien verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-133">**cURL** is a command line tool that can be used to send or receive files.</span></span> <span data-ttu-id="e9ad5-134">Es ist in Linux, MacOS und Windows 10 enthalten und kann für die meisten anderen Betriebssysteme heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-134">It's included with Linux, macOS, and Windows 10, and can be downloaded for most other operating systems.</span></span> <span data-ttu-id="e9ad5-135">cURL unterstützt zahlreiche Protokolle wie HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 usw. Weitere Informationen finden Sie unter den unten angegebenen Links:</span><span class="sxs-lookup"><span data-stu-id="e9ad5-135">cURL supports numerous protocols like HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3, etc. For more information, refer to the links below:</span></span>
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

<span data-ttu-id="e9ad5-136">Zum Testen der Funktion können Sie über die Befehlszeile mit cURL eine HTTP-Anforderung an die Funktions-URL senden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-136">To test the function, you can send an HTTP request to the function URL using cURL on the command line.</span></span> <span data-ttu-id="e9ad5-137">Um die Endpunkt-URL der Funktion zu finden, kehren Sie zu Ihrem Funktionscode zurück, und klicken Sie wie im folgenden Screenshot gezeigt auf den Link **Funktions-URL abrufen**.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-137">To find the endpoint URL of the function, return to your function code and select the **Get function URL** link, as shown in the following screenshot.</span></span> <span data-ttu-id="e9ad5-138">Speichern Sie diesen Link vorübergehend.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-138">Save this link temporarily.</span></span>

![Screenshot: Der Funktionen-Editor im Azure-Portal mit der hervorgehobenen Schaltfläche „Funktions-URL abrufen“.](../media/5-get-function-url.png)

### <a name="securing-http-triggers"></a><span data-ttu-id="e9ad5-140">Schützen von HTTP-Triggern</span><span class="sxs-lookup"><span data-stu-id="e9ad5-140">Securing HTTP triggers</span></span>

<span data-ttu-id="e9ad5-141">Mit HTTP-Triggern können Sie API-Schlüssel verwenden, um unbekannte Aufrufer zu blockieren, indem Sie verlangen, dass der Schlüssel bei jeder Anforderung vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-141">HTTP triggers let you use API keys to block unknown callers by requiring the key to be present on each request.</span></span> <span data-ttu-id="e9ad5-142">Beim Erstellen einer Funktion wählen Sie die _Autorisierungsstufe_ aus.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-142">When you create a function, you select the _authorization level_.</span></span> <span data-ttu-id="e9ad5-143">Standardmäßig ist diese auf „Funktion“ festgelegt, was einen funktionsspezifischen API-Schlüssel erfordert. Sie kann aber auch auf „Administrator“ festgelegt werden, um einen globalen „Hauptschlüssel“ zu verwenden, oder auf „Anonym“, um anzugeben, dass kein Schlüssel benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-143">By default, it's set to "Function", which requires a function-specific API key, but it can also be set to "Admin" to use a global "master" key, or "Anonymous" to indicate that no key is required.</span></span> <span data-ttu-id="e9ad5-144">Sie können die Autorisierungsstufe auch nach dem Erstellen über die Funktionseigenschaften ändern.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-144">You can also change the authorization level through the function properties after creation.</span></span>

<span data-ttu-id="e9ad5-145">Da wir bei der Erstellung dieser Funktion „Funktion“ angegeben haben, müssen wir beim Senden der HTTP-Anforderung den Schlüssel angeben.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-145">Since we specified "Function" when we created this function, we will need to supply the key when we send the HTTP request.</span></span> <span data-ttu-id="e9ad5-146">Sie können ihn als Parameter mit einer Abfragezeichenfolge mit dem Namen `code` oder als HTTP-Header (bevorzugt) mit dem Namen `x-functions-key` senden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-146">You can send it as a query string parameter named `code`, or as an HTTP header (preferred) named `x-functions-key`.</span></span>

<span data-ttu-id="e9ad5-147">Funktions- und Masterschlüssel finden Sie im Abschnitt **Verwalten**, wenn die Funktion erweitert wird.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-147">The function and master keys are found in the **Manage** section when the function is expanded.</span></span> <span data-ttu-id="e9ad5-148">Standardmäßig sind sie ausgeblendet, sodass Sie sie einblenden müssen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-148">By default, they are hidden, and you need to display them.</span></span>

1. <span data-ttu-id="e9ad5-149">Erweitern Sie Ihre Funktion, und wählen Sie den Abschnitt **Verwalten** aus. Zeigen Sie den Standardfunktionsschlüssel an, und kopieren Sie ihn in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-149">Expand your function and select the **Manage** section, show the default Function Key, and copy it to the clipboard.</span></span>

    ![Screenshot des Blatts „Verwalten“ im Azure-Portal mit hervorgehobenem eingeblendeten Funktionsschlüssel.](../media/5-get-function-key.png)

1. <span data-ttu-id="e9ad5-151">Formatieren Sie als Nächstes über die Befehlszeile, in der Sie das **cURL**-Tool installiert haben, einen cURL-Befehl mit der URL für Ihre Funktion und den Funktionsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-151">Next, from the command line where you installed the **cURL** tool, format a cURL command with the URL for your function, and the Function key.</span></span>

    - <span data-ttu-id="e9ad5-152">Verwenden Sie eine `POST`-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-152">Use a `POST` request.</span></span>
    - <span data-ttu-id="e9ad5-153">Fügen Sie einen Headerwert für `Content-Type` des Typs `application/json` hinzu.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-153">Add a `Content-Type` header value of type `application/json`.</span></span>
    - <span data-ttu-id="e9ad5-154">Achten Sie darauf, dass Sie die URL durch Ihre eigene ersetzen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-154">Make sure to replace the URL below with your own.</span></span>
    - <span data-ttu-id="e9ad5-155">Übergeben Sie den Funktionsschlüssel als den Headerwert `x-functions-key`.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-155">Pass the Function Key as the header value `x-functions-key`.</span></span>

    ```bash
    curl --header "Content-Type: application/json" --header "x-functions-key: <your-function-key>" --request POST --data "{\"name\": \"Azure Function\"}" https://<your-url-here>/api/DriveGearTemperatureService
    ```

<span data-ttu-id="e9ad5-156">Die Funktion antwortet mit dem Text `"Hello Azure Function"`.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-156">The function will respond back with the text `"Hello Azure Function"`.</span></span>

> [!CAUTION]
> <span data-ttu-id="e9ad5-157">Wenn Sie Windows verwenden, führen Sie `cURL` über die Befehlszeile aus.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-157">If you are on Windows, please run  `cURL` from the command prompt.</span></span> <span data-ttu-id="e9ad5-158">PowerShell verfügt über einen *curl*-Befehl. Dies ist jedoch ein Alias für „Invoke-WebRequest“ und ist nicht mit `cURL` identisch.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-158">PowerShell has a *curl* command, but it's an alias for Invoke-WebRequest and is not the same as `cURL`.</span></span>

> [!NOTE]
> <span data-ttu-id="e9ad5-159">Sie können auch über den Abschnitt mit der Registerkarte **Testen** der jeweiligen Funktion einen Test für eine ausgewählte Funktion durchführen. Allerdings können Sie nicht überprüfen, ob das Funktionsschlüsselsystem funktioniert, da es in diesem Fall nicht erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-159">You can also test from an individual function's section with the **Test** tab on the side of a selected function, though you won't be able to verify the function key system is working, as it is not required here.</span></span> <span data-ttu-id="e9ad5-160">Fügen Sie die entsprechenden Header- und Parameterwerte in die Testschnittstelle ein, und klicken Sie auf die Schaltfläche **Ausführen**, um die Testausgabe anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-160">Add the appropriate header and parameter values in the Test interface and click the **Run** button to see the test output.</span></span>

## <a name="add-business-logic-to-the-function"></a><span data-ttu-id="e9ad5-161">Hinzufügen von Geschäftslogik zur Funktion</span><span class="sxs-lookup"><span data-stu-id="e9ad5-161">Add business logic to the function</span></span>

<span data-ttu-id="e9ad5-162">Als Nächstes fügen wir die Logik zur Funktion hinzu, die die empfangenen Temperaturmesswerte überprüft und für jeden einen Status festlegt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-162">Next, let's add the logic to the function that checks temperature readings that it receives and sets a status for each.</span></span>

<span data-ttu-id="e9ad5-163">Unsere Funktion erwartet ein Array von Temperaturmesswerten.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-163">Our function is expecting an array of temperature readings.</span></span> <span data-ttu-id="e9ad5-164">Der folgende JSON-Codeausschnitt ist ein Beispiel für den Anforderungstext, den wir an unsere Funktion senden.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-164">The following JSON snippet is an example of the request body that we'll send to our function.</span></span> <span data-ttu-id="e9ad5-165">Jeder `reading`-Eintrag verfügt über ID, Zeitstempel und Temperatur.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-165">Each `reading` entry has an ID, timestamp, and temperature.</span></span>

```json
{
    "readings": [
        {
            "driveGearId": 1,
            "timestamp": 1534263995,
            "temperature": 23
        },
        {
            "driveGearId": 3,
            "timestamp": 1534264048,
            "temperature": 45
        },
        {
            "driveGearId": 18,
            "timestamp": 1534264050,
            "temperature": 55
        }
    ]
}
```

<span data-ttu-id="e9ad5-166">Als Nächstes ersetzen wir den Standardcode in unserer Funktion durch den folgenden Code, der unsere Geschäftslogik implementiert.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-166">Next, we'll replace the default code in our function with the following code that implements our business logic.</span></span>

1. <span data-ttu-id="e9ad5-167">Öffnen Sie die Datei **index.js**, und ersetzen Sie sie durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-167">Open the **index.js** file and replace it with the following code.</span></span>

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        req.body.readings.forEach(function(reading) {

            if(reading.temperature<=25) {
                reading.status = 'OK';
            } else if (reading.temperature<=50) {
                reading.status = 'CAUTION';
            } else {
                reading.status = 'DANGER'
            }
            context.log('Reading is ' + reading.status);
        });

        context.res = {
            // status: 200, /* Defaults to 200 */
            body: {
                "readings": req.body.readings
            }
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please send an array of readings in the request body"
        };
    }
    context.done();
};
```

<span data-ttu-id="e9ad5-168">Die Logik, die wir hinzugefügt haben, ist einfach.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-168">The logic we added is straightforward.</span></span> <span data-ttu-id="e9ad5-169">Wir iterieren über das Array der Messwerte und überprüfen das Temperaturfeld.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-169">We iterate over the array of readings and check the temperature field.</span></span> <span data-ttu-id="e9ad5-170">Abhängig vom Wert dieses Felds wird der Status **OK**, **CAUTION** oder **DANGER** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-170">Depending on the value of that field, we set a status of **OK**, **CAUTION**, or **DANGER**.</span></span> <span data-ttu-id="e9ad5-171">Wir senden dann das Array der Messwerte mit einem zu jedem Eintrag hinzugefügten Statusfeld zurück.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-171">We then send back the array of readings with a status field added to each entry.</span></span>

<span data-ttu-id="e9ad5-172">Beachten Sie die `log`-Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-172">Notice the `log` statements.</span></span> <span data-ttu-id="e9ad5-173">Wenn die Funktion ausgeführt wird, fügen diese Anweisungen Meldungen im Protokollfenster hinzu.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-173">When the function runs, these statements will add messages in the log window.</span></span>

## <a name="test-our-business-logic"></a><span data-ttu-id="e9ad5-174">Testen der Geschäftslogik</span><span class="sxs-lookup"><span data-stu-id="e9ad5-174">Test our business logic</span></span>

<span data-ttu-id="e9ad5-175">In diesem Fall verwenden wir den Bereich **Test** im Portal, um unsere Funktion zu testen.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-175">In this case, we're going to use the **Test** pane in the portal to test our function.</span></span>

1. <span data-ttu-id="e9ad5-176">Öffnen Sie das Fenster **Test** im rechten Flyoutmenü.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-176">Open the **Test** window from the right-hand side flyout menu.</span></span>

1. <span data-ttu-id="e9ad5-177">Fügen Sie die Beispielanforderung in das Feld für den Anforderungstext ein.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-177">Paste the sample request into the request body text box.</span></span>

    ```json
    {
        "readings": [
            {
                "driveGearId": 1,
                "timestamp": 1534263995,
                "temperature": 23
            },
            {
                "driveGearId": 3,
                "timestamp": 1534264048,
                "temperature": 45
            },
            {
                "driveGearId": 18,
                "timestamp": 1534264050,
                "temperature": 55
            }
        ]
    }
    ```

1. <span data-ttu-id="e9ad5-178">Klicken Sie auf **Ausführen**, und zeigen Sie die Antwort im Ausgabebereich an.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-178">Select **Run** and view the response in the output pane.</span></span> <span data-ttu-id="e9ad5-179">Um Protokollmeldungen anzuzeigen, öffnen Sie die Registerkarte **Protokolle** im Flyoutmenü unten auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-179">To see log messages, open the **Logs** tab in the bottom flyout of the page.</span></span> <span data-ttu-id="e9ad5-180">Im folgenden Screenshot wird eine Beispielantwort im Ausgabebereich und Nachrichten im Bereich **Protokolle** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-180">The following screenshot shows an example response in the output pane and messages in the  **Logs** pane.</span></span>

    ![Screenshot: Blatt „Funktionen-Editor“ im Azure-Portal mit den angezeigten Registerkarten „Test“ und „Protokolle“.](../media/5-portal-testing.png)

    <span data-ttu-id="e9ad5-183">Im Ausgabebereich sehen Sie, dass unser Statusfeld korrekt zu jedem Messwert hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-183">You can see in the output pane that our status field has been correctly added to each of the readings.</span></span>

    <span data-ttu-id="e9ad5-184">Sie können auch auf dem **Dashboard „Monitor“** prüfen, ob die Anforderung in Application Insights protokolliert wurde.</span><span class="sxs-lookup"><span data-stu-id="e9ad5-184">If you navigate to the **Monitor** dashboard, you'll see that the request has been logged to Application Insights.</span></span>

    ![Screenshot: Die vorherigen Testergebnisse im Dashboard „Monitor“ im Azure-Portal.](../media/5-app-insights.png)
