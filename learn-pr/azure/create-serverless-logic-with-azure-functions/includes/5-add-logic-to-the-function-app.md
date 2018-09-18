<span data-ttu-id="34003-101">Lassen Sie uns wir mit unserem Zahnradsteuerungs-Beispiel fortfahren und die Logik für den Temperaturdienst hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="34003-101">Let's continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="34003-102">Insbesondere werden wir Daten von einer HTTP-Anforderung empfangen.</span><span class="sxs-lookup"><span data-stu-id="34003-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="34003-103">Anforderungen an die Funktion</span><span class="sxs-lookup"><span data-stu-id="34003-103">Function requirements</span></span>

<span data-ttu-id="34003-104">Zuerst müssen wir einige Anforderungen an unsere Logik definieren:</span><span class="sxs-lookup"><span data-stu-id="34003-104">First, we need to define some requirements for our logic:</span></span>

- <span data-ttu-id="34003-105">Temperaturen von 0 bis 25 sollen mit **OK** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="34003-105">Temperatures between 0-25 should be flagged as **OK**.</span></span>
- <span data-ttu-id="34003-106">Temperaturen von 26 bis 50 sollen mit **CAUTION** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="34003-106">Temperatures between 26-50 should be flagged as **CAUTION**.</span></span>
- <span data-ttu-id="34003-107">Temperaturen über 50 sollen mit **DANGER** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="34003-107">Temperatures above 50 should be flagged as **DANGER**.</span></span>

## <a name="add-a-function-to-our-function-app"></a><span data-ttu-id="34003-108">Hinzufügen einer Funktion zu unserer Funktions-App</span><span class="sxs-lookup"><span data-stu-id="34003-108">Add a function to our function app</span></span>

<span data-ttu-id="34003-109">Wie in der vorherigen Einheit bereits erläutert wurde, verfügt Azure über Vorlagen, die Ihnen das Erstellen von Funktionen erleichtern.</span><span class="sxs-lookup"><span data-stu-id="34003-109">As we discussed in the preceding unit, Azure provides templates that help you get started building functions.</span></span> <span data-ttu-id="34003-110">In dieser Einheit verwenden wir die Vorlage `HttpTrigger`, um den Temperaturdienst zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="34003-110">In this unit, we'll use the `HttpTrigger` template to implement the temperature service.</span></span>

1. <span data-ttu-id="34003-111">Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="34003-111">Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true) using your Azure account.</span></span>

2. <span data-ttu-id="34003-112">Wählen Sie durch Auswahl von **Alle Ressourcen** im linken Menü die Ressourcengruppe aus, die Sie in der ersten Übung erstellt haben, und wählen Sie dann **escalator-functions-group** aus.</span><span class="sxs-lookup"><span data-stu-id="34003-112">Select the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>

3. <span data-ttu-id="34003-113">Die Ressourcen für die Gruppe werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="34003-113">The resources for the group will then be displayed.</span></span> <span data-ttu-id="34003-114">Klicken Sie auf den Namen der Funktions-App, die Sie in der vorherigen Übung erstellt haben, indem Sie das Element **escalator-functions-xxxxxxx** (auch durch das Blitzsymbol gekennzeichnet) auswählen.</span><span class="sxs-lookup"><span data-stu-id="34003-114">Click the name of the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt Function icon).</span></span>

  ![Screenshot: Das hervorgehobene Blatt „Alle Ressourcen“ sowie die von Ihnen erstellten Funktions-App „escalator“ im Azure-Portal.](../media/5-access-function-app.png)

4. <span data-ttu-id="34003-116">Im linken Menü wird der Name Ihrer Funktions-App und ein Untermenü mit den folgenden drei Elementen angezeigt: *Funktionen*, *Proxys* und *Slots*.</span><span class="sxs-lookup"><span data-stu-id="34003-116">The left-side menu displays your function app name and a submenu with three items: *Functions*, *Proxies*, and *Slots*.</span></span>  <span data-ttu-id="34003-117">Klicken Sie auf **Funktionen**, und klicken Sie dann am oberen Rand der angezeigten Seite auf **Neue Funktion**.</span><span class="sxs-lookup"><span data-stu-id="34003-117">To start creating our first function, select **Functions** and click  the **New function** button at the top of the resulting page.</span></span>

  ![Screenshot: Funktionsliste für die Funktions-App im Azure-Portal, wobei das Menüelement „Funktionen“ und die Schaltfläche „Neue Funktion“ hervorgehoben sind.](../media/5-function-add-button.png)

5. <span data-ttu-id="34003-119">Klicken Sie auf dem Bildschirm „Schnellstart“ im Abschnitt **Get started on your own** (Selbstständig einsteigen) auf den Link **Benutzerdefinierte Funktion** (wie im folgenden Screenshot).</span><span class="sxs-lookup"><span data-stu-id="34003-119">In the Quickstart screen, select the **Custom function** link in the **Get started on your own** section as shown in the following screenshot.</span></span> <span data-ttu-id="34003-120">Wenn der Bildschirm „Schnellstart“ nicht angezeigt wird, klicken Sie am oberen Rand der Seite auf den Link **Go to the quickstart** (Zum Schnellstart wechseln).</span><span class="sxs-lookup"><span data-stu-id="34003-120">If you don't see the Quickstart screen, click on the **go to the quickstart** link at the top of the page.</span></span>

  ![Screenshot: Das Blatt „Schnellstart“ im Azure-Portal mit der hervorgehobenen Schaltfläche „Benutzerdefinierte Funktion“ im Abschnitt „Selbstständig einsteigen“.](../media/5-custom-function.png)

6. <span data-ttu-id="34003-122">Wählen Sie wie im folgenden Screenshot gezeigt die **JavaScript**-Implementierung der Vorlage **HTTP-Trigger** aus der auf dem Bildschirm angezeigten Liste von Vorlagen aus.</span><span class="sxs-lookup"><span data-stu-id="34003-122">From the list of templates displayed on the screen, select the **JavaScript** implementation of the **HTTP trigger** template as shown in the following screenshot.</span></span>

7. <span data-ttu-id="34003-123">Geben Sie **DriveGearTemperatureService** in das Feld „Name“ des nun angezeigten Dialogfelds **Neue Funktion** ein.</span><span class="sxs-lookup"><span data-stu-id="34003-123">Enter **DriveGearTemperatureService** in the name field of the **New Function** dialog that appears.</span></span> <span data-ttu-id="34003-124">Belassen Sie die Autorisierungsstufe auf „Funktion“, und klicken Sie auf die Schaltfläche **Erstellen**, um die Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="34003-124">Leave the Authorization level as "Function" and press the **Create** button to create the function.</span></span>

  ![Screenshot: Das Azure-Portal mit den neuen Funktionsoptionen für HTTP-Trigger, das Feld für die Sprache ist auf JavaScript und der Name ist auf DriveGearTemperatureService festgelegt.](../media/5-create-httptrigger-form.png)

8. <span data-ttu-id="34003-126">Nach Abschluss der Funktionserstellung wird der Code-Editor mit dem Inhalt der Codedatei *index.js* geöffnet.</span><span class="sxs-lookup"><span data-stu-id="34003-126">When your function creation completes, the code editor opens with the contents of the *index.js* code file.</span></span> <span data-ttu-id="34003-127">Der Standardcode, den die Vorlage für uns generiert hat, wird im folgenden Codeausschnitt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="34003-127">The default code that the template generated for us is listed in the following snippet.</span></span>

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

<span data-ttu-id="34003-128">Unsere-Funktion erwartet einen Namen, der entweder über die Abfragezeichenfolge der HTTP-Anforderung oder als Teil des Anforderungstexts übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="34003-128">Our function expects a name to be passed in either through the HTTP request query string or as part of the request body.</span></span> <span data-ttu-id="34003-129">Die Funktion antwortet mit der Meldung **Hello, {Name}**, die den in der Anforderung gesendeten Namen wiedergibt.</span><span class="sxs-lookup"><span data-stu-id="34003-129">The function responds by returning the message  **Hello, {name}**, echoing back the name that was sent in the request.</span></span>

<span data-ttu-id="34003-130">Auf der rechten Seite der Quellansicht sehen Sie zwei Registerkarten.</span><span class="sxs-lookup"><span data-stu-id="34003-130">On the right-hand side of the source view, you'll find two tabs.</span></span> <span data-ttu-id="34003-131">Auf der Registerkarte **Datei anzeigen** werden der Code und die Konfigurationsdatei Ihrer Funktion aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="34003-131">The **View files** tab lists the code and config file for your function.</span></span>  <span data-ttu-id="34003-132">Wählen Sie **function.json** aus, um die Konfiguration der Funktion anzuzeigen, die in etwa wie folgt aussehen sollte:</span><span class="sxs-lookup"><span data-stu-id="34003-132">Select **function.json** to view the configuration of the function, which should look like the following:</span></span>

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

<span data-ttu-id="34003-133">Diese Konfiguration deklariert, dass die Funktion ausgeführt wird, sobald sie eine HTTP-Anforderung empfängt.</span><span class="sxs-lookup"><span data-stu-id="34003-133">This configuration declares that the function runs when it receives an HTTP request.</span></span> <span data-ttu-id="34003-134">Die Ausgabebindung deklariert, dass die Antwort als HTTP-Antwort gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="34003-134">The output binding declares that the response will be sent as an HTTP response.</span></span>

## <a name="test-the-function-using-curl"></a><span data-ttu-id="34003-135">Testen der Funktion mit cURL</span><span class="sxs-lookup"><span data-stu-id="34003-135">Test the function using cURL</span></span>

> [!TIP]
> <span data-ttu-id="34003-136">**cURL** ist ein Befehlszeilentool, das zum Senden und Empfangen von Dateien verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="34003-136">**cURL** is a command line tool that can be used to send or receive files.</span></span> <span data-ttu-id="34003-137">Es ist in Linux, MacOS und Windows 10 enthalten und kann für die meisten anderen Betriebssysteme heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="34003-137">It's included with Linux, macOS, and Windows 10, and can be downloaded for most other operating systems.</span></span> <span data-ttu-id="34003-138">cURL unterstützt zahlreiche Protokolle wie HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 usw. Weitere Informationen finden Sie unter den unten angegebenen Links:</span><span class="sxs-lookup"><span data-stu-id="34003-138">cURL supports numerous protocols like HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3, etc. For more information, please refer to the links below:</span></span>
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

<span data-ttu-id="34003-139">Zum Testen der Funktion können Sie über die Befehlszeile mit cURL eine HTTP-Anforderung an die Funktions-URL senden.</span><span class="sxs-lookup"><span data-stu-id="34003-139">To test the function, you can send an HTTP request to the function URL using cURL on the command line.</span></span> <span data-ttu-id="34003-140">Um die Endpunkt-URL der Funktion zu finden, kehren Sie zu Ihrem Funktionscode zurück, und klicken Sie wie im folgenden Screenshot gezeigt auf den Link **Funktions-URL abrufen**.</span><span class="sxs-lookup"><span data-stu-id="34003-140">To find the endpoint URL of the function, return to your function code and select the **Get function URL** link, as shown in the following screenshot.</span></span> <span data-ttu-id="34003-141">Speichern Sie diesen Link vorübergehend.</span><span class="sxs-lookup"><span data-stu-id="34003-141">Save this link temporarily.</span></span>

 ![Screenshot: Der Funktionen-Editor im Azure-Portal mit der hervorgehobenen Schaltfläche „Funktions-URL abrufen“.](../media/5-get-function-url.png)

### <a name="securing-http-triggers"></a><span data-ttu-id="34003-143">Schützen von HTTP-Triggern</span><span class="sxs-lookup"><span data-stu-id="34003-143">Securing HTTP triggers</span></span>

<span data-ttu-id="34003-144">Mit HTTP-Triggern können Sie API-Schlüssel verwenden, um unbekannte Aufrufer zu blockieren, indem Sie verlangen, dass der Schlüssel bei jeder Anforderung vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="34003-144">HTTP triggers let you use API keys to block unknown callers by requiring the key to be present on each request.</span></span> <span data-ttu-id="34003-145">Beim Erstellen einer Funktion wählen Sie die _Autorisierungsstufe_ aus.</span><span class="sxs-lookup"><span data-stu-id="34003-145">When you create a function, you select the _authorization level_.</span></span> <span data-ttu-id="34003-146">Standardmäßig ist diese auf „Funktion“ festgelegt, was einen funktionsspezifischen API-Schlüssel erfordert. Sie kann aber auch auf „Administrator“ festgelegt werden, um einen globalen „Hauptschlüssel“ zu verwenden, oder auf „Anonym“, um anzugeben, dass kein Schlüssel benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="34003-146">By default, it's set to "Function", which requires a function-specific API key, but it can also be set to "Admin" to use a global "master" key, or "Anonymous" to indicate that no key is required.</span></span> <span data-ttu-id="34003-147">Sie können die Autorisierungsstufe auch nach dem Erstellen über die Funktionseigenschaften ändern.</span><span class="sxs-lookup"><span data-stu-id="34003-147">You can also change the authorization level through the function properties after creation.</span></span>

<span data-ttu-id="34003-148">Da wir bei der Erstellung dieser Funktion „Funktion“ angegeben haben, müssen wir beim Senden der HTTP-Anforderung den Schlüssel angeben.</span><span class="sxs-lookup"><span data-stu-id="34003-148">Since we specified "Function" when we created this function, we will need to supply the key when we send the HTTP request.</span></span> <span data-ttu-id="34003-149">Sie können ihn als Parameter mit einer Abfragezeichenfolge mit dem Namen `code` oder als HTTP-Header (bevorzugt) mit dem Namen `x-functions-key` senden.</span><span class="sxs-lookup"><span data-stu-id="34003-149">You can send it as a query string parameter named `code`, or as an HTTP header (preferred) named `x-functions-key`.</span></span>

<span data-ttu-id="34003-150">Funktions- und Masterschlüssel finden Sie im Abschnitt **Verwalten**, wenn die Funktion erweitert wird.</span><span class="sxs-lookup"><span data-stu-id="34003-150">The function and master keys are found in the **Manage** section when the function is expanded.</span></span> <span data-ttu-id="34003-151">Standardmäßig sind sie ausgeblendet, sodass Sie sie einblenden müssen.</span><span class="sxs-lookup"><span data-stu-id="34003-151">By default, they are hidden, and you need to display them.</span></span>

1. <span data-ttu-id="34003-152">Erweitern Sie Ihre Funktion, und wählen Sie den Abschnitt **Verwalten** aus. Zeigen Sie den Standardfunktionsschlüssel an, und kopieren Sie ihn in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="34003-152">Expand your function and select the **Manage** section, show the default Function Key, and copy it to the clipboard.</span></span>

![Screenshot: Blatt „Verwalten“ im Azure-Portal mit hervorgehobenem eingeblendeten Funktionsschlüssel.](../media/5-get-function-key.png)

1. <span data-ttu-id="34003-154">Formatieren Sie anschließend einen cURL-Befehl mit der URL Ihrer Funktion und dem Funktionsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="34003-154">Next, format a cURL command with the URL for your function, and the Function key.</span></span>

    - <span data-ttu-id="34003-155">Verwenden Sie eine `POST`-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="34003-155">Use a `POST` request.</span></span>
    - <span data-ttu-id="34003-156">Fügen Sie einen Headerwert für `Content-Type` des Typs `application/json` hinzu.</span><span class="sxs-lookup"><span data-stu-id="34003-156">Add a `Content-Type` header value of type `application/json`.</span></span>
    - <span data-ttu-id="34003-157">Achten Sie darauf, dass Sie die URL durch Ihre eigene ersetzen.</span><span class="sxs-lookup"><span data-stu-id="34003-157">Make sure to replace the URL below with your own.</span></span>
    - <span data-ttu-id="34003-158">Übergeben Sie den Funktionsschlüssel als den Headerwert `x-functions-key`.</span><span class="sxs-lookup"><span data-stu-id="34003-158">Pass the Function Key as the header value `x-functions-key`.</span></span>

    ```bash
    curl --header "Content-Type: application/json" --header "x-functions-key: <your-function-key>" --request POST --data "{\"name\": \"Azure Function\"}" https://<your-url-here>/api/DriveGearTemperatureService
    ```

<span data-ttu-id="34003-159">Die Funktion antwortet mit dem Text `"Hello Azure Function"`.</span><span class="sxs-lookup"><span data-stu-id="34003-159">The function will respond back with the text `"Hello Azure Function"`.</span></span>

## <a name="add-business-logic-to-the-function"></a><span data-ttu-id="34003-160">Hinzufügen von Geschäftslogik zur Funktion</span><span class="sxs-lookup"><span data-stu-id="34003-160">Add business logic to the function</span></span>

<span data-ttu-id="34003-161">Als Nächstes fügen wir die Logik zur Funktion hinzu, die die empfangenen Temperaturmesswerte überprüft und für jeden einen Status festlegt.</span><span class="sxs-lookup"><span data-stu-id="34003-161">Next, let's add the logic to the function that checks temperature readings that it receives and sets a status for each.</span></span>

<span data-ttu-id="34003-162">Unsere Funktion erwartet ein Array von Temperaturmesswerten.</span><span class="sxs-lookup"><span data-stu-id="34003-162">Our function is expecting an array of temperature readings.</span></span> <span data-ttu-id="34003-163">Der folgende JSON-Codeausschnitt ist ein Beispiel für den Anforderungstext, den wir an unsere Funktion senden.</span><span class="sxs-lookup"><span data-stu-id="34003-163">The following JSON snippet is an example of the request body that we'll send to our function.</span></span> <span data-ttu-id="34003-164">Jeder `reading`-Eintrag verfügt über ID, Zeitstempel und Temperatur.</span><span class="sxs-lookup"><span data-stu-id="34003-164">Each `reading` entry has an ID, timestamp, and temperature.</span></span>

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

<span data-ttu-id="34003-165">Als Nächstes ersetzen wir den Standardcode in unserer Funktion durch den folgenden Code, der unsere Geschäftslogik implementiert.</span><span class="sxs-lookup"><span data-stu-id="34003-165">Next, we'll replace the default code in our function with the following code that implements our business logic.</span></span>

1. <span data-ttu-id="34003-166">Öffnen Sie die Datei **index.js**, und ersetzen Sie sie durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="34003-166">Open the **index.js** file and replace it with the following code.</span></span>

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

<span data-ttu-id="34003-167">Die Logik, die wir hinzugefügt haben, ist einfach.</span><span class="sxs-lookup"><span data-stu-id="34003-167">The logic we added is straightforward.</span></span> <span data-ttu-id="34003-168">Wir iterieren über das Array der Messwerte und überprüfen das Temperaturfeld.</span><span class="sxs-lookup"><span data-stu-id="34003-168">We iterate over the array of readings and check the temperature field.</span></span> <span data-ttu-id="34003-169">Abhängig vom Wert dieses Felds wird der Status **OK**, **CAUTION** oder **DANGER** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="34003-169">Depending on the value of that field, we set a status of **OK**, **CAUTION**, or **DANGER**.</span></span> <span data-ttu-id="34003-170">Wir senden dann das Array der Messwerte mit einem zu jedem Eintrag hinzugefügten Statusfeld zurück.</span><span class="sxs-lookup"><span data-stu-id="34003-170">We then send back the array of readings with a status field added to each entry.</span></span>

<span data-ttu-id="34003-171">Beachten Sie die `log`-Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="34003-171">Notice the `log` statements.</span></span> <span data-ttu-id="34003-172">Wenn die Funktion ausgeführt wird, fügen diese Anweisungen Meldungen im Protokollfenster hinzu.</span><span class="sxs-lookup"><span data-stu-id="34003-172">When the function runs, these statements will add messages in the log window.</span></span>

## <a name="test-our-business-logic"></a><span data-ttu-id="34003-173">Testen der Geschäftslogik</span><span class="sxs-lookup"><span data-stu-id="34003-173">Test our business logic</span></span>

<span data-ttu-id="34003-174">In diesem Fall verwenden wir den Bereich **Test** im Portal, um unsere Funktion zu testen.</span><span class="sxs-lookup"><span data-stu-id="34003-174">In this case, we're going to use the **Test** pane in the portal to test our function.</span></span>

1. <span data-ttu-id="34003-175">Öffnen Sie das Fenster **Test** im rechten Flyoutmenü.</span><span class="sxs-lookup"><span data-stu-id="34003-175">Open the **Test** window from the right-hand side flyout menu.</span></span>

1. <span data-ttu-id="34003-176">Fügen Sie die Beispielanforderung in das Feld für den Anforderungstext ein.</span><span class="sxs-lookup"><span data-stu-id="34003-176">Paste the sample request into the request body text box.</span></span>

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

1. <span data-ttu-id="34003-177">Klicken Sie auf **Ausführen**, und zeigen Sie die Antwort im Ausgabebereich an.</span><span class="sxs-lookup"><span data-stu-id="34003-177">Select **Run** and view the response in the output pane.</span></span> <span data-ttu-id="34003-178">Um Protokollmeldungen anzuzeigen, öffnen Sie die Registerkarte **Protokolle** im Flyoutmenü unten auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="34003-178">To see log messages, open the **Logs** tab in the bottom flyout of the page.</span></span> <span data-ttu-id="34003-179">Im folgenden Screenshot wird eine Beispielantwort im Ausgabebereich und Nachrichten im Bereich **Protokolle** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="34003-179">The following screenshot shows an example response in the output pane and messages in the  **Logs** pane.</span></span>

![Screenshot: Blatt „Funktionen-Editor“ im Azure-Portal mit den angezeigten Registerkarten „Test“ und „Protokolle“.](../media/5-portal-testing.png)

<span data-ttu-id="34003-182">Im Ausgabebereich sehen Sie, dass unser Statusfeld korrekt zu jedem Messwert hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="34003-182">You can see in the output pane that our status field has been correctly added to each of the readings.</span></span>

<span data-ttu-id="34003-183">Sie können auch auf dem **Dashboard „Monitor“** prüfen, ob die Anforderung in Application Insights protokolliert wurde.</span><span class="sxs-lookup"><span data-stu-id="34003-183">If you navigate to the **Monitor** dashboard, you'll see that the request has been logged to Application Insights.</span></span>

![Screenshot: Die vorherigen Testergebnisse im Dashboard „Monitor“ im Azure-Portal.](../media/5-app-insights.png)
