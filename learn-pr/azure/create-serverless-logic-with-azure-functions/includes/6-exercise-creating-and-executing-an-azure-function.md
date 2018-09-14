<span data-ttu-id="2e476-101">In dieser Übung fahren wir mit unserem Zahnradsteuerungs-Beispiel fort und fügen die Logik für den Temperaturdienst hinzu.</span><span class="sxs-lookup"><span data-stu-id="2e476-101">In this exercise, we'll continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="2e476-102">Insbesondere werden wir Daten von einer HTTP-Anforderung empfangen.</span><span class="sxs-lookup"><span data-stu-id="2e476-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="2e476-103">Anforderungen an die Funktion</span><span class="sxs-lookup"><span data-stu-id="2e476-103">Function requirements</span></span>
<span data-ttu-id="2e476-104">Lassen Sie uns einige Anforderungen für unsere Logik definieren:</span><span class="sxs-lookup"><span data-stu-id="2e476-104">Let's define some requirements for our logic:</span></span>
- <span data-ttu-id="2e476-105">Temperaturen zwischen 0 und 25 sollten mit **OK** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="2e476-105">temperatures between 0-25 should be flagged as **OK**</span></span>
- <span data-ttu-id="2e476-106">Temperaturen zwischen 26 und 50 sollten mit **CAUTION** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="2e476-106">temperatures between 26-50 should be flagged as **CAUTION**</span></span>
- <span data-ttu-id="2e476-107">Temperaturen über 50 sollten mit **DANGER** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="2e476-107">temperatures above 50 should be flagged as **DANGER**</span></span>

## <a name="add-a-function-to-an-azure-function-app"></a><span data-ttu-id="2e476-108">Hinzufügen einer Funktion zu einer Azure-Funktions-App</span><span class="sxs-lookup"><span data-stu-id="2e476-108">Add a function to an Azure function app</span></span>

<span data-ttu-id="2e476-109">Wie in der vorherigen Einheit bereits erläutert wurde, verfügt Azure über Vorlagen, die Ihnen das Erstellen von Funktionen erleichtern.</span><span class="sxs-lookup"><span data-stu-id="2e476-109">As we discussed in the preceding unit, Azure provides templates that help you get started building functions.</span></span> <span data-ttu-id="2e476-110">In dieser Übung verwenden Sie die Vorlage HttpTrigger, um den Temperaturdienst zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="2e476-110">In this exercise, we'll use the HttpTrigger template to implement the temperature service.</span></span>

1. <span data-ttu-id="2e476-111">Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="2e476-111">Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true) using your Azure account.</span></span>
1. <span data-ttu-id="2e476-112">Wählen Sie durch Auswahl von **Alle Ressourcen** im linken Menü die Ressourcengruppe aus, die Sie in der ersten Übung erstellt haben, und wählen Sie dann **escalator-functions-group** aus.</span><span class="sxs-lookup"><span data-stu-id="2e476-112">Select the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>
1. <span data-ttu-id="2e476-113">Die Ressourcen für die Gruppe werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e476-113">The resources for the group will then be displayed.</span></span> <span data-ttu-id="2e476-114">Greifen Sie durch Auswahl von **escalator-functions-xxxxxxx** (auch durch das Blitzsymbol gekennzeichnet) auf die Funktions-App zu, die Sie in der vorherigen Übung erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="2e476-114">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>
  <span data-ttu-id="2e476-115">![Screenshot von „Alle Ressourcen“ im Portal, mit Hervorhebung der von uns erstellten „escalator-functions-group“ und Funktions-App.](../images/6-access-function-app.png)</span><span class="sxs-lookup"><span data-stu-id="2e476-115">![Screenshot of All Resources in the portal highlighting the escalator-functions-group and the function app we created.](../images/6-access-function-app.png)</span></span>
1. <span data-ttu-id="2e476-116">Im linken Menü werden der Name Ihrer Funktions-App und ein Untermenü mit drei Elementen angezeigt – *Funktionen*, *Proxys* und *Slots*.</span><span class="sxs-lookup"><span data-stu-id="2e476-116">The left-side menu displays your function app name and a submenu with three items - *Functions*, *Proxies*, and *Slots*.</span></span>  <span data-ttu-id="2e476-117">Um unsere erste Funktion zu erstellen, bewegen Sie den Mauszeiger in der Navigationsstruktur über **Funktionen**, und klicken Sie auf die dann angezeigte Schaltfläche **+**.</span><span class="sxs-lookup"><span data-stu-id="2e476-117">To start creating our first function, move your mouse over **Functions** in the navigation tree and click  the **+** button that appears.</span></span>
  <span data-ttu-id="2e476-118">![Screenshot mit Pluszeichen (+), das angezeigt wird, wenn Sie mit der Maus über das Menüelement „Funktionen“ fahren, welches beim Anklicken die Funktionserstellung startet.](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="2e476-118">![Screenshot showing plus sign when you hover over the Functions menu item that, when clicked, starts the function creation procedure.](../images/5-function-add-button.png)</span></span>
1. <span data-ttu-id="2e476-119">Wählen Sie auf dem Schnellstartbildschirm den Link **Benutzerdefinierte Funktion** im Abschnitt **Selbstständig einsteigen** wie im folgenden Screenshot gezeigt aus.</span><span class="sxs-lookup"><span data-stu-id="2e476-119">In the Quickstart screen, select the **Custom function** link in the **Get started on your own** section as shown in the following screenshot.</span></span>
  <span data-ttu-id="2e476-120">![Screenshot des Schnellstartbildschirms mit hervorgehobener Schaltfläche „Benutzerdefinierte Funktion“.](../images/6-custom-function.png)</span><span class="sxs-lookup"><span data-stu-id="2e476-120">![Screenshot of Quickstart screen with the "Custom function" button highlighted.](../images/6-custom-function.png)</span></span>
1. <span data-ttu-id="2e476-121">Wählen Sie, wie im folgenden Screenshot gezeigt, aus der Liste der auf dem Bildschirm angezeigten Vorlagen die JavaScript-Implementierung der Vorlage „HTTP-Trigger“ aus.</span><span class="sxs-lookup"><span data-stu-id="2e476-121">From the list of templates displayed on the screen, select the JavaScript implementation of the HTTP trigger template as shown in the following screenshot.</span></span>
  <span data-ttu-id="2e476-122">![Screenshot der Vorlagenliste, bei dem der HTTP-Trigger und die JavaScript-Option hervorgehoben sind.](../images/6-httptrigger-template.png)</span><span class="sxs-lookup"><span data-stu-id="2e476-122">![Screenshot of template list, with the HTTP trigger and JavaScript option highlighted.](../images/6-httptrigger-template.png)</span></span>
1.  <span data-ttu-id="2e476-123">Geben Sie **DriveGearTemperatureService** in das Feld „Name“ des nun angezeigten Dialogfelds **Neue Funktion** ein.</span><span class="sxs-lookup"><span data-stu-id="2e476-123">Enter **DriveGearTemperatureService** in the name field of the **New Function** dialog that appears.</span></span> <span data-ttu-id="2e476-124">Wählen Sie, nachdem Sie Ihre Funktion benannt haben, wie im folgenden Screenshot gezeigt die Schaltfläche **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="2e476-124">After you have named your function, press the **Create** button, as illustrated in te following screenshot.</span></span>
  <span data-ttu-id="2e476-125">![Screenshot des Formulars „Neue Funktion“, bei dem das Feld „Name“ hervorgehoben ist und das mit dem Wert „DriveGearTemperatureService“ eingerichtet wurde](../images/6-create-httptrigger-form.png)</span><span class="sxs-lookup"><span data-stu-id="2e476-125">![Screenshot of New Function form, showing Name field highlighted and set with the value "DriveGearTemperatureService"](../images/6-create-httptrigger-form.png)</span></span>
1. <span data-ttu-id="2e476-126">Nach Abschluss der Funktionserstellung wird der Code-Editor mit dem Inhalt der Codedatei *index.js* geöffnet.</span><span class="sxs-lookup"><span data-stu-id="2e476-126">When your function creation completes, the code editor opens with the contents of the *index.js* code file.</span></span> <span data-ttu-id="2e476-127">Der Standardcode, den die Vorlage für uns generiert hat, wird im folgenden Codeausschnitt aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="2e476-127">The default code that the template generated for us is listed in the following snippet.</span></span>

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

<span data-ttu-id="2e476-128">Unsere-Funktion erwartet einen Namen, der entweder über die Abfragezeichenfolge der HTTP-Anforderung oder als Teil des Anforderungstexts übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="2e476-128">Our function expects a name to be passed in either through the HTTP request query string or as part of the request body.</span></span> <span data-ttu-id="2e476-129">Die Funktion antwortet, indem sie die Nachricht **Hello, {name}** ausgibt und dabei den Namen verwendet, der in der Anforderung gesendet wurde.</span><span class="sxs-lookup"><span data-stu-id="2e476-129">The function responds by returning the message  **Hello, {name}**, echoing back the name that was sent in the request.</span></span>

1. <span data-ttu-id="2e476-130">Auf der rechten Seite der Quellenansicht sehen Sie zwei Registerkarten.</span><span class="sxs-lookup"><span data-stu-id="2e476-130">On the right-hand side of the source view, you'll see two tabs.</span></span> <span data-ttu-id="2e476-131">Die Datei \*\*View listet den Code und die Konfigurationsdatei für Ihre Funktion auf.</span><span class="sxs-lookup"><span data-stu-id="2e476-131">The \*\*View file lists the code and config file for your function.</span></span>  <span data-ttu-id="2e476-132">Wählen Sie **function.json** aus, um die Konfiguration der Funktion anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="2e476-132">Select **function.json** to view the configuration of the function.</span></span> <span data-ttu-id="2e476-133">Der folgende Codeausschnitt zeigt den Inhalt der Datei **function.json**.</span><span class="sxs-lookup"><span data-stu-id="2e476-133">The following snippet shows the contents of the **function.json** file.</span></span> <span data-ttu-id="2e476-134">Diese Konfiguration deklariert, dass die Funktion ausgeführt wird, wenn sie eine HTTP-Anforderung empfängt.</span><span class="sxs-lookup"><span data-stu-id="2e476-134">This configuration declares that the function is runs when it receives an HTTP request.</span></span> <span data-ttu-id="2e476-135">Die Ausgabebindung deklariert, dass die Antwort als HTTP-Antwort gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="2e476-135">The output binding declares that the response will be sent as an HTTP response.</span></span>

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
> [!TIP]
> <span data-ttu-id="2e476-136">Beachten Sie, dass der Trigger in der obigen JSON-Datei in einem Array von Bindungen definiert wurde.</span><span class="sxs-lookup"><span data-stu-id="2e476-136">Notice in the preceding JSON file that the trigger is defined in an array of bindings.</span></span> <span data-ttu-id="2e476-137">Ein Trigger ist also eigentlich eine besondere Art von Bindung.</span><span class="sxs-lookup"><span data-stu-id="2e476-137">So, a trigger is actually a special type of binding.</span></span>

## <a name="run-our-function"></a><span data-ttu-id="2e476-138">Ausführen Ihrer Funktion</span><span class="sxs-lookup"><span data-stu-id="2e476-138">Run our function</span></span>

> [!TIP]
> <span data-ttu-id="2e476-139">**cURL** ist ein Befehlszeilentool, das zum Senden oder Empfangen von Dateien verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="2e476-139">**cURL** is a command line tool that can be used to send or receive files.</span></span> <span data-ttu-id="2e476-140">cURL.exe unterstützt zahlreiche Protokolle wie HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 usw. Weitere Informationen finden Sie unter den unten angegebenen Links:</span><span class="sxs-lookup"><span data-stu-id="2e476-140">cURL.exe supports numerous protocols like HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 etc. For more information please refer the below links:</span></span>
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

<span data-ttu-id="2e476-141">Um unsere-Funktion zu testen, können Sie eine HTTP-Anforderung an die Funktions-URL senden und dabei cURL in der Befehlszeile verwenden.</span><span class="sxs-lookup"><span data-stu-id="2e476-141">To test our function, you can send an HTTP request to the function URL using cURL on the command line.</span></span> <span data-ttu-id="2e476-142">Um die Endpunkt-URL der Funktion zu finden, kehren Sie zu Ihrem Funktionscode zurück, und wählen Sie wie im folgenden Screenshot gezeigt den Link **Funktions-URL abrufen** aus.</span><span class="sxs-lookup"><span data-stu-id="2e476-142">To find the endpoint URL of the function, return to your function code and select the **Get function URL** link, as shown in the following screenshot.</span></span> <span data-ttu-id="2e476-143">Kopieren Sie diesen Link in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="2e476-143">Copy this link to your clipboard.</span></span>  

 ![Screenshot des Code-Editors im Funktions-Apps-Bereich des Portals.](../images/6-get-function-url.png)

<span data-ttu-id="2e476-146">Führen Sie unter Verwendung dieser Funktions-URL den folgenden cURL-Befehl in der Befehlszeile aus. Ersetzen Sie dabei die URL durch Ihre eigene URL.</span><span class="sxs-lookup"><span data-stu-id="2e476-146">Using this function URL, run the following cURL command from your command line, replacing the URL with your own.</span></span>

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

<span data-ttu-id="2e476-147">Der folgende Screenshot zeigt ein Beispiel für die Antwort, die Sie von der Standardimplementierung in der Befehlszeile erhalten.</span><span class="sxs-lookup"><span data-stu-id="2e476-147">The following screenshot shows an example of the response you receive from the default implementation in the command line.</span></span>

![Screenshot eines Beispiel-cURL-Befehls und der Antwort in einer Befehlszeile.](../images/6-premadefunction-curl.png)

## <a name="add-business-logic-to-the-function"></a><span data-ttu-id="2e476-149">Hinzufügen von Geschäftslogik zur Funktion</span><span class="sxs-lookup"><span data-stu-id="2e476-149">Add business logic to the function</span></span>

<span data-ttu-id="2e476-150">Nun wird es Zeit, die Logik zur Funktion hinzuzufügen, die die empfangenen Temperaturmesswerte überprüft und für jeden einen Status festlegt.</span><span class="sxs-lookup"><span data-stu-id="2e476-150">It's time to add the logic to the function that checks temperature readings that it receives and sets a status for each.</span></span>

<span data-ttu-id="2e476-151">Unsere Funktion erwartet ein Array von Temperaturmesswerten.</span><span class="sxs-lookup"><span data-stu-id="2e476-151">Our function is expecting an array of temperature readings.</span></span> <span data-ttu-id="2e476-152">Der folgende JSON-Codeausschnitt ist ein Beispiel für den Anforderungstext, den wir an unsere Funktion senden.</span><span class="sxs-lookup"><span data-stu-id="2e476-152">The following JSON snippet is an example of the request body that we'll send to our function.</span></span> <span data-ttu-id="2e476-153">Jeder `reading`-Eintrag verfügt über ID, Zeitstempel und Temperatur.</span><span class="sxs-lookup"><span data-stu-id="2e476-153">Each `reading` entry has an ID, timestamp, and temperature.</span></span>

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

<span data-ttu-id="2e476-154">Als Nächstes ersetzen wir den Standardcode in unserer Funktion durch den folgenden Code, der unsere Geschäftslogik implementiert.</span><span class="sxs-lookup"><span data-stu-id="2e476-154">Next, we'll replace the default code in our function with the following code that implements our business logic.</span></span> 

1. <span data-ttu-id="2e476-155">Öffnen Sie die Datei **index.js**, und ersetzen Sie sie durch den folgenden Code.</span><span class="sxs-lookup"><span data-stu-id="2e476-155">Open the **index.js** file, and replace it with the following code.</span></span>

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
<span data-ttu-id="2e476-156">Die Logik, die wir hinzugefügt haben, ist einfach.</span><span class="sxs-lookup"><span data-stu-id="2e476-156">The logic we added is straightforward.</span></span> <span data-ttu-id="2e476-157">Wir iterieren über das Array der Messwerte und überprüfen das Temperaturfeld.</span><span class="sxs-lookup"><span data-stu-id="2e476-157">We iterate over the array of readings and check the temperature field.</span></span> <span data-ttu-id="2e476-158">Abhängig vom Wert dieses Felds wird der Status **OK**, **CAUTION** oder **DANGER** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="2e476-158">Depending on the value of that field, we set a status of **OK**, **CAUTION**, or **DANGER**.</span></span> <span data-ttu-id="2e476-159">Wir senden dann das Array der Messwerte mit einem zu jedem Eintrag hinzugefügten Statusfeld zurück.</span><span class="sxs-lookup"><span data-stu-id="2e476-159">We then send back the array of readings with a status field added to each entry.</span></span>

<span data-ttu-id="2e476-160">Beachten Sie die Protokollanweisungen.</span><span class="sxs-lookup"><span data-stu-id="2e476-160">Notice the log statements.</span></span> <span data-ttu-id="2e476-161">Wenn die Funktion ausgeführt wird, fügen diese Anweisungen Meldungen im Protokollfenster hinzu.</span><span class="sxs-lookup"><span data-stu-id="2e476-161">When the function runs, these statements will add messages in the log window.</span></span>

## <a name="test-our-business-logic"></a><span data-ttu-id="2e476-162">Testen der Geschäftslogik</span><span class="sxs-lookup"><span data-stu-id="2e476-162">Test our business logic</span></span>

<span data-ttu-id="2e476-163">In diesem Fall verwenden wir den Bereich **Test** im Portal, um unsere Funktion zu testen.</span><span class="sxs-lookup"><span data-stu-id="2e476-163">In this case, we're going to use the **Test** pane in the portal to test our function.</span></span>

1. <span data-ttu-id="2e476-164">Öffnen Sie das Fenster **Test** im rechten Flyoutmenü.</span><span class="sxs-lookup"><span data-stu-id="2e476-164">Open the **Test** window from the right-hand side flyout menu.</span></span>
1. <span data-ttu-id="2e476-165">Fügen Sie die obige Beispielanforderung in das Feld für den Anforderungstext ein.</span><span class="sxs-lookup"><span data-stu-id="2e476-165">Paste the sample request from above into the request body text box.</span></span> 
1. <span data-ttu-id="2e476-166">Wählen Sie **Ausführen** aus, und zeigen Sie die Antwort im Ausgabebereich an.</span><span class="sxs-lookup"><span data-stu-id="2e476-166">Select **Run** and view the response in the output pane.</span></span> <span data-ttu-id="2e476-167">Um Protokollmeldungen anzuzeigen, öffnen Sie die Registerkarte **Protokolle** im Flyoutmenü unten auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="2e476-167">To see log messages, open the **Logs** tab in the bottom flyout of the page.</span></span> <span data-ttu-id="2e476-168">Der folgende Screenshot zeigt eine Beispielantwort im Ausgabebereich und Meldungen im Bereich **Protokolle**.</span><span class="sxs-lookup"><span data-stu-id="2e476-168">The following screenshot shows an example response in the output pane and messages in the  **Logs** pane.</span></span>

![Screenshot der Registerkarten „Test“ und „Protokolle“ auf der Benutzeroberfläche „Funktionen“ im Portal.](../images/6-portal-testing.png)

<span data-ttu-id="2e476-171">Im Ausgabebereich sehen Sie, dass unser Statusfeld korrekt zu jedem Messwert hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="2e476-171">You can see in the output pane that our status field has been correctly added to each of the readings.</span></span>

<span data-ttu-id="2e476-172">Sie können auch auf dem Dashboard **Monitor** prüfen, ob die Anforderung in Application Insights protokolliert wurde.</span><span class="sxs-lookup"><span data-stu-id="2e476-172">If you navigate to the **Monitor** dashboard, you'll see that the request has been logged to Application Insights.</span></span>

![Screenshot von Teilen des Dashboards „Monitor“ mit einer Erfolgsmeldung unserer Funktion.](../images/6-app-insights.png)

