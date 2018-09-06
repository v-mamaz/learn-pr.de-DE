<span data-ttu-id="95ae9-101">Lassen Sie uns mit unserem Zahnradsteuerungs-Beispiel fortfahren und die Logik für den Temperaturdienst hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="95ae9-101">Let's continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="95ae9-102">Insbesondere werden wir Daten von einer HTTP-Anforderung empfangen.</span><span class="sxs-lookup"><span data-stu-id="95ae9-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="95ae9-103">Anforderungen an die Funktion</span><span class="sxs-lookup"><span data-stu-id="95ae9-103">Function requirements</span></span>
<span data-ttu-id="95ae9-104">Zunächst müssen wir einige Anforderungen an unsere Logik definieren:</span><span class="sxs-lookup"><span data-stu-id="95ae9-104">First, we need to define some requirements for our logic:</span></span>

- <span data-ttu-id="95ae9-105">Temperaturen von 0 bis 25 sollen mit **OK** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="95ae9-105">Temperatures between 0-25 should be flagged as **OK**.</span></span>
- <span data-ttu-id="95ae9-106">Temperaturen von 26 bis 50 sollen mit **CAUTION** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="95ae9-106">Temperatures between 26-50 should be flagged as **CAUTION**.</span></span>
- <span data-ttu-id="95ae9-107">Temperaturen über 50 sollen mit **DANGER** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="95ae9-107">Temperatures above 50 should be flagged as **DANGER**.</span></span>

## <a name="add-a-function-to-our-function-app"></a><span data-ttu-id="95ae9-108">Hinzufügen einer Funktion zu unserer Funktions-App</span><span class="sxs-lookup"><span data-stu-id="95ae9-108">Add a function to our function app</span></span>

<span data-ttu-id="95ae9-109">Wie bereits in der vorhergehenden Einheit beschrieben, bietet Azure Vorlagen zur Verfügung, die Ihnen den Einstieg in die Erstellung von Funktionen erleichtern.</span><span class="sxs-lookup"><span data-stu-id="95ae9-109">As we discussed in the preceding unit, Azure provides templates that help you get started building functions.</span></span> <span data-ttu-id="95ae9-110">In dieser Übung verwenden wir die Vorlage `HttpTrigger`, um den Temperaturdienst zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="95ae9-110">In this exercise, we'll use the `HttpTrigger` template to implement the temperature service.</span></span>

1. <span data-ttu-id="95ae9-111">Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="95ae9-111">Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true) using your Azure account.</span></span>

2. <span data-ttu-id="95ae9-112">Wählen Sie die Ressourcengruppe aus, die Sie in der ersten Übung erstellt haben, indem Sie im linken Menü **Alle Ressourcen** und dann **escalator-functions-group** auswählen.</span><span class="sxs-lookup"><span data-stu-id="95ae9-112">Select the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>

3. <span data-ttu-id="95ae9-113">Die Ressourcen für die Gruppe werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="95ae9-113">The resources for the group will then be displayed.</span></span> <span data-ttu-id="95ae9-114">Greifen Sie durch Auswahl von **escalator-functions-xxxxxxx** (auch durch das Blitzsymbol gekennzeichnet) auf die Funktions-App zu, die Sie in der vorherigen Übung erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="95ae9-114">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>

  ![Screenshot von „Alle Ressourcen“ im Portal mit Hervorhebung von „escalator-functions-group“ und der von uns erstellten Funktions-App.](../media-draft/5-access-function-app.png)

4. <span data-ttu-id="95ae9-116">Das linke Menü enthält den Namen Ihrer Funktions-App und ein Untermenü mit drei Punkten: *Funktionen*, *Proxys* und *Slots*.</span><span class="sxs-lookup"><span data-stu-id="95ae9-116">The left-side menu displays your function app name and a submenu with three items: *Functions*, *Proxies*, and *Slots*.</span></span>  <span data-ttu-id="95ae9-117">Um unsere erste Funktion zu erstellen, bewegen Sie den Mauszeiger in der Navigationsstruktur über **Funktion**, und klicken Sie auf die dann angezeigte Schaltfläche **+**.</span><span class="sxs-lookup"><span data-stu-id="95ae9-117">To start creating our first function, move your mouse over **Functions** in the navigation tree and click  the **+** button that appears.</span></span>

  ![Screenshot mit Pluszeichen, wenn Sie den Mauszeiger über den Menüpunkt „Funktionen“ bewegen, der, wenn darauf geklickt wird, die Funktionserstellung startet.](../media-draft/5-function-add-button.png)

5. <span data-ttu-id="95ae9-119">Klicken Sie auf dem Bildschirm „Schnellstart“ im Abschnitt **Selbstständig einsteigen** auf den Link **Benutzerdefinierte Funktion** (siehe den folgenden Screenshot).</span><span class="sxs-lookup"><span data-stu-id="95ae9-119">In the Quickstart screen, select the **Custom function** link in the **Get started on your own** section as shown in the following screenshot.</span></span>
 
  ![Screenshot des Bildschirms „Schnellstart“ mit hervorgehobener Schaltfläche „Benutzerdefinierte Funktion“.](../media-draft/5-custom-function.png)

6. <span data-ttu-id="95ae9-121">Wählen Sie in der Liste der auf dem Bildschirm angezeigten Vorlagen die JavaScript-Implementierung der HTTP-Triggervorlage aus, wie im folgenden Screenshot gezeigt.</span><span class="sxs-lookup"><span data-stu-id="95ae9-121">From the list of templates displayed on the screen, select the JavaScript implementation of the HTTP trigger template as shown in the following screenshot.</span></span>

  ![Screenshot der Vorlagenliste mit Hervorhebung von HTTP-Trigger und der Option „JavaScript“.](../media-draft/5-httptrigger-template.png)

7.  <span data-ttu-id="95ae9-123">Geben Sie **DriveGearTemperatureService** in das Feld „Name“ des eingeblendeten Dialogfelds **Neue Funktion** ein.</span><span class="sxs-lookup"><span data-stu-id="95ae9-123">Enter **DriveGearTemperatureService** in the name field of the **New Function** dialog that appears.</span></span> <span data-ttu-id="95ae9-124">Belassen Sie die Autorisierungsstufe auf „Funktion“, und klicken Sie auf die Schaltfläche **Erstellen**, um die Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="95ae9-124">Leave the Authorization level as "Function" and press the **Create** button to create the function.</span></span>

  ![Screenshot des Formulars „Neue Funktion“ mit hervorgehobenem Feld „Name“ und festgelegtem Wert „DriveGearTemperatureService“](../media-draft/5-create-httptrigger-form.png)

8. <span data-ttu-id="95ae9-126">Wenn die Erstellung Ihrer Funktion abgeschlossen ist, öffnet sich der Code-Editor mit dem Inhalt der Codedatei *index.js*.</span><span class="sxs-lookup"><span data-stu-id="95ae9-126">When your function creation completes, the code editor opens with the contents of the *index.js* code file.</span></span> <span data-ttu-id="95ae9-127">Der Standardcode, den die Vorlage für uns generiert hat, ist im folgenden Codeausschnitt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="95ae9-127">The default code that the template generated for us is listed in the following snippet.</span></span>

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

<span data-ttu-id="95ae9-128">Unsere Funktion erwartet, dass ein Name entweder über die Abfragezeichenfolge der HTTP-Anforderung oder als Teil des Anforderungstexts übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="95ae9-128">Our function expects a name to be passed in either through the HTTP request query string or as part of the request body.</span></span> <span data-ttu-id="95ae9-129">Die Funktion antwortet mit der Meldung **Hello, {Name}**, die den in der Anforderung gesendeten Namen wiedergibt.</span><span class="sxs-lookup"><span data-stu-id="95ae9-129">The function responds by returning the message  **Hello, {name}**, echoing back the name that was sent in the request.</span></span>

<span data-ttu-id="95ae9-130">Auf der rechten Seite der Quellansicht sehen Sie zwei Registerkarten.</span><span class="sxs-lookup"><span data-stu-id="95ae9-130">On the right-hand side of the source view, you'll find two tabs.</span></span> <span data-ttu-id="95ae9-131">Unter **Datei anzeigen** werden der Code und Konfigurationsdatei Ihrer Funktion aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="95ae9-131">The **View file** lists the code and config file for your function.</span></span>  <span data-ttu-id="95ae9-132">Wählen Sie **function.json** aus, um die Konfiguration der Funktion anzuzeigen, die in etwa so aussehen sollte:</span><span class="sxs-lookup"><span data-stu-id="95ae9-132">Select **function.json** to view the configuration of the function which should look like the following:</span></span> 

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

<span data-ttu-id="95ae9-133">Diese Konfiguration deklariert, dass die Funktion ausgeführt wird, sobald sie eine HTTP-Anforderung empfängt.</span><span class="sxs-lookup"><span data-stu-id="95ae9-133">This configuration declares that the function runs when it receives an HTTP request.</span></span> <span data-ttu-id="95ae9-134">Die Ausgabebindung deklariert, dass die Antwort als HTTP-Antwort gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="95ae9-134">The output binding declares that the response will be sent as an HTTP response.</span></span>

## <a name="test-the-function-using-curl"></a><span data-ttu-id="95ae9-135">Testen der Funktion mit cURL</span><span class="sxs-lookup"><span data-stu-id="95ae9-135">Test the function using cURL</span></span>

> [!TIP]
> <span data-ttu-id="95ae9-136">**cURL** ist ein Befehlszeilentool, das zum Senden und Empfangen von Dateien verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="95ae9-136">**cURL** is a command line tool that can be used to send or receive files.</span></span> <span data-ttu-id="95ae9-137">Es ist in Linux, MacOS und Windows 10 enthalten und kann für die meisten anderen Betriebssysteme heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="95ae9-137">It's included with Linux, macOS, and Windows 10, and can be downloaded for most other operating systems.</span></span> <span data-ttu-id="95ae9-138">cURL unterstützt zahlreiche Protokolle wie HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 usw. Weitere Informationen finden Sie unter den unten angegebenen Links:</span><span class="sxs-lookup"><span data-stu-id="95ae9-138">cURL supports numerous protocols like HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3, etc. For more information, please refer to the links below:</span></span>
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

<span data-ttu-id="95ae9-139">Zum Testen der Funktion können Sie über die Befehlszeile mit cURL eine HTTP-Anforderung an die Funktions-URL senden.</span><span class="sxs-lookup"><span data-stu-id="95ae9-139">To test the function, you can send an HTTP request to the function URL using cURL on the command line.</span></span> <span data-ttu-id="95ae9-140">Um die Endpunkt-URL der Funktion zu finden, kehren Sie zu Ihrem Funktionscode zurück, und wählen Sie den Link **Funktions-URL abrufen** aus (siehe den folgenden Screenshot).</span><span class="sxs-lookup"><span data-stu-id="95ae9-140">To find the endpoint URL of the function, return to your function code and select the **Get function URL** link, as shown in the following screenshot.</span></span> <span data-ttu-id="95ae9-141">Speichern Sie diesen Link vorübergehend.</span><span class="sxs-lookup"><span data-stu-id="95ae9-141">Save this link off temporarily.</span></span>  

 ![Screenshot des Code-Editors im Abschnitt „Funktionen-Apps“ des Portals.](../media-draft/5-get-function-url.png)

### <a name="securing-http-triggers"></a><span data-ttu-id="95ae9-144">Schützen von HTTP-Triggern</span><span class="sxs-lookup"><span data-stu-id="95ae9-144">Securing HTTP triggers</span></span>
<span data-ttu-id="95ae9-145">Mit HTTP-Triggern können Sie API-Schlüssel verwenden, um unbekannte Aufrufer zu blockieren, indem Sie verlangen, dass der Schlüssel bei jeder Anforderung vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="95ae9-145">HTTP triggers let you use API keys to block unknown callers by requiring the key to be present on each request.</span></span> <span data-ttu-id="95ae9-146">Wenn Sie eine Funktion erstellen, wählen Sie die _Autorisierungsstufe_.</span><span class="sxs-lookup"><span data-stu-id="95ae9-146">When you create a function, you select the _authorization level_.</span></span> <span data-ttu-id="95ae9-147">Standardmäßig ist diese auf „Funktion“ festgelegt, was einen funktionsspezifischen API-Schlüssel erfordert. Sie kann aber auch auf „Admin“ festgelegt werden, um einen globalen „Master“-Schlüssel zu verwenden, oder auf „Anonym“, um anzugeben, dass kein Schlüssel benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="95ae9-147">By default, it's set to "Function" which requires a function-specific API key, but it can also be set to "Admin" to use a global "master" key, or "Anonymous" to indicate that no key is required.</span></span> <span data-ttu-id="95ae9-148">Sie können die Autorisierungsstufe auch nach dem Erstellen über die Funktionseigenschaften ändern.</span><span class="sxs-lookup"><span data-stu-id="95ae9-148">You can also change the authorization level through the function properties after creation.</span></span>

<span data-ttu-id="95ae9-149">Da wir bei der Erstellung dieser Funktion „Funktion“ angegeben haben, müssen wir beim Senden der HTTP-Anforderung den Schlüssel angeben.</span><span class="sxs-lookup"><span data-stu-id="95ae9-149">Since we specified "Function" when we created this function, we will need to supply the key when we send the HTTP request.</span></span> <span data-ttu-id="95ae9-150">Sie können ihn als Parameter mit einer Abfragezeichenfolge mit dem Namen `code` oder als HTTP-Header (bevorzugt) mit dem Namen `x-functions-key` senden.</span><span class="sxs-lookup"><span data-stu-id="95ae9-150">You can send it as a query string parameter named `code`, or as an HTTP header (preferred) named `x-functions-key`.</span></span>

<span data-ttu-id="95ae9-151">Funktions- und Masterschlüssel finden Sie im Abschnitt **Verwalten**, wenn die Funktion erweitert wird.</span><span class="sxs-lookup"><span data-stu-id="95ae9-151">The function and master keys are found in the **Manage** section when the function is expanded.</span></span> <span data-ttu-id="95ae9-152">Standardmäßig sind sie ausgeblendet, sodass Sie sie einblenden müssen.</span><span class="sxs-lookup"><span data-stu-id="95ae9-152">By default, they are hidden, and you need to display them.</span></span>

1. <span data-ttu-id="95ae9-153">Erweitern Sie Ihre Funktion, und wählen Sie den Abschnitt **Verwalten** aus. Zeigen Sie den standardmäßigen Funktionsschlüssel an, und kopieren Sie ihn in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="95ae9-153">Expand your function and select the **Manage** section, show the default Function Key and copy it to the clipboard.</span></span>

![Blatt zum Abrufen des Funktionsschlüssels aus dem Azure-Portal](../media-draft/5-get-function-key.png)

2. <span data-ttu-id="95ae9-155">Formatieren Sie anschließend einen cURL-Befehl mit der URL Ihrer Funktion und dem Funktionsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="95ae9-155">Next, format a cURL command with the URL for your function, and the Function key.</span></span>
    - <span data-ttu-id="95ae9-156">Verwenden Sie eine `POST`-Anforderung.</span><span class="sxs-lookup"><span data-stu-id="95ae9-156">Use a `POST` request.</span></span>
    - <span data-ttu-id="95ae9-157">Fügen Sie einen Headerwert für `Content-Type` des Typs `application/json` hinzu.</span><span class="sxs-lookup"><span data-stu-id="95ae9-157">Add a `Content-Type` header value of type `application/json`.</span></span>
    - <span data-ttu-id="95ae9-158">Achten Sie darauf, dass Sie die URL durch Ihre eigene ersetzen.</span><span class="sxs-lookup"><span data-stu-id="95ae9-158">Make sure to replace the URL below with your own.</span></span>
    - <span data-ttu-id="95ae9-159">Übergeben Sie den Funktionsschlüssel als den Headerwert `x-functions-key`.</span><span class="sxs-lookup"><span data-stu-id="95ae9-159">Pass the Function Key as the header value `x-functions-key`.</span></span>

```bash
curl --header "Content-Type: application/json" --header "x-functions-key: VCWjWkBTvWBsnvw0TlbIbtsav3P3J80m/PKe8WclH0C3RSmvG4Sy8w==" --request POST --data "{\"name\": \"Azure Function\"}" https://<your-url-here>/api/DriveGearTemperatureService
```

<span data-ttu-id="95ae9-160">Die Funktion antwortet mit dem Text `"Hello Azure Function"`.</span><span class="sxs-lookup"><span data-stu-id="95ae9-160">The function will respond back with the text `"Hello Azure Function"`.</span></span>

## <a name="add-business-logic-to-the-function"></a><span data-ttu-id="95ae9-161">Hinzufügen von Geschäftslogik zur Funktion</span><span class="sxs-lookup"><span data-stu-id="95ae9-161">Add business logic to the function</span></span>

<span data-ttu-id="95ae9-162">Als Nächstes fügen wir die Logik zur Funktion hinzu, die die empfangenen Temperaturmesswerte überprüft und für jeden einen Status festlegt.</span><span class="sxs-lookup"><span data-stu-id="95ae9-162">Next, let's add the logic to the function that checks temperature readings that it receives and sets a status for each.</span></span>

<span data-ttu-id="95ae9-163">Unsere Funktion erwartet ein Array von Temperaturmesswerten.</span><span class="sxs-lookup"><span data-stu-id="95ae9-163">Our function is expecting an array of temperature readings.</span></span> <span data-ttu-id="95ae9-164">Der folgende JSON-Codeausschnitt ist ein Beispiel für den Anforderungstext, den wir an unsere Funktion senden.</span><span class="sxs-lookup"><span data-stu-id="95ae9-164">The following JSON snippet is an example of the request body that we'll send to our function.</span></span> <span data-ttu-id="95ae9-165">Jeder `reading`-Eintrag verfügt über ID, Zeitstempel und Temperatur.</span><span class="sxs-lookup"><span data-stu-id="95ae9-165">Each `reading` entry has an ID, timestamp, and temperature.</span></span>

```javascript
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

<span data-ttu-id="95ae9-166">Als Nächstes ersetzen wir den Standardcode in unserer Funktion durch den folgenden Code, der unsere Geschäftslogik implementiert.</span><span class="sxs-lookup"><span data-stu-id="95ae9-166">Next, we'll replace the default code in our function with the following code that implements our business logic.</span></span> 

1. <span data-ttu-id="95ae9-167">Öffnen Sie die Datei **index.js**, und ersetzen Sie sie durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="95ae9-167">Open the **index.js** file and replace it with the following code.</span></span>

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

<span data-ttu-id="95ae9-168">Die Logik, die wir hinzugefügt haben, ist einfach.</span><span class="sxs-lookup"><span data-stu-id="95ae9-168">The logic we added is straightforward.</span></span> <span data-ttu-id="95ae9-169">Wir iterieren über das Feld der Messwerte und überprüfen das Temperaturfeld.</span><span class="sxs-lookup"><span data-stu-id="95ae9-169">We iterate over the array of readings and check the temperature field.</span></span> <span data-ttu-id="95ae9-170">Abhängig vom Wert dieses Felds wird der Status **OK**, **CAUTION** oder **DANGER** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="95ae9-170">Depending on the value of that field, we set a status of **OK**, **CAUTION**, or **DANGER**.</span></span> <span data-ttu-id="95ae9-171">Wir senden dann das Array der Messwerte mit einem zu jedem Eintrag hinzugefügten Statusfeld zurück.</span><span class="sxs-lookup"><span data-stu-id="95ae9-171">We then send back the array of readings with a status field added to each entry.</span></span>

<span data-ttu-id="95ae9-172">Beachten Sie die `log`-Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="95ae9-172">Notice the `log` statements.</span></span> <span data-ttu-id="95ae9-173">Wenn die Funktion ausgeführt wird, fügen diese Anweisungen Meldungen im Protokollfenster hinzu.</span><span class="sxs-lookup"><span data-stu-id="95ae9-173">When the function runs, these statements will add messages in the log window.</span></span>

## <a name="test-our-business-logic"></a><span data-ttu-id="95ae9-174">Testen der Geschäftslogik</span><span class="sxs-lookup"><span data-stu-id="95ae9-174">Test our business logic</span></span>

<span data-ttu-id="95ae9-175">In diesem Fall verwenden wir den Bereich **Test** im Portal, um unsere Funktion zu testen.</span><span class="sxs-lookup"><span data-stu-id="95ae9-175">In this case, we're going to use the **Test** pane in the portal to test our function.</span></span>

1. <span data-ttu-id="95ae9-176">Öffnen Sie das Fenster **Test** im rechten Flyoutmenü.</span><span class="sxs-lookup"><span data-stu-id="95ae9-176">Open the **Test** window from the right-hand side flyout menu.</span></span>

2. <span data-ttu-id="95ae9-177">Fügen Sie die Beispielanforderung von oben in das Feld für den Anforderungstext ein.</span><span class="sxs-lookup"><span data-stu-id="95ae9-177">Paste the sample request from above into the request body text box.</span></span> 

3. <span data-ttu-id="95ae9-178">Klicken Sie auf **Ausführen**, und zeigen Sie die Antwort im Ausgabebereich an.</span><span class="sxs-lookup"><span data-stu-id="95ae9-178">Select **Run** and view the response in the output pane.</span></span> <span data-ttu-id="95ae9-179">Um Protokollmeldungen anzuzeigen, öffnen Sie die Registerkarte **Protokolle** im Flyoutmenü unten auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="95ae9-179">To see log messages, open the **Logs** tab in the bottom flyout of the page.</span></span> <span data-ttu-id="95ae9-180">Der folgende Screenshot zeigt eine Beispielantwort im Ausgabebereich und Meldungen im Bereich **Protokolle**.</span><span class="sxs-lookup"><span data-stu-id="95ae9-180">The following screenshot shows an example response in the output pane and messages in the  **Logs** pane.</span></span>

![Screenshot der Registerkarten „Test“ und „Protokolle“ auf der Benutzeroberfläche „Funktionen“ im Portal.](../media-draft/5-portal-testing.png)

<span data-ttu-id="95ae9-183">Im Ausgabebereich sehen Sie, dass unser Statusfeld jedem Messwert ordnungsgemäß hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="95ae9-183">You can see in the output pane that our status field has been correctly added to each of the readings.</span></span>

<span data-ttu-id="95ae9-184">Sie können auch auf dem Dashboard **Monitor** prüfen, ob die Anforderung in Application Insights protokolliert wurde.</span><span class="sxs-lookup"><span data-stu-id="95ae9-184">If you navigate to the **Monitor** dashboard, you'll see that the request has been logged to Application Insights.</span></span>

![Screenshot von Teilen des Dashboards „Monitor“ mit einer Erfolgsmeldung unserer Funktion.](../media-draft/5-app-insights.png)

