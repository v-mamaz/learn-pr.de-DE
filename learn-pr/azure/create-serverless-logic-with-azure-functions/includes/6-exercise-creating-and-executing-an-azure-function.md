<span data-ttu-id="79a2f-101">In dieser Übung fahren wir mit unserem Zahnradsteuerungs-Beispiel fort und fügen die Logik für den Temperaturdienst hinzu.</span><span class="sxs-lookup"><span data-stu-id="79a2f-101">In this exercise, we'll continue with our gear drive example and add the logic for the temperature service.</span></span> <span data-ttu-id="79a2f-102">Insbesondere werden wir Daten von einer HTTP-Anforderung empfangen.</span><span class="sxs-lookup"><span data-stu-id="79a2f-102">Specifically, we're going to receive data from an HTTP request.</span></span>

## <a name="function-requirements"></a><span data-ttu-id="79a2f-103">Anforderungen an die Funktion</span><span class="sxs-lookup"><span data-stu-id="79a2f-103">Function requirements</span></span>
<span data-ttu-id="79a2f-104">Lassen Sie uns einige Anforderungen für unsere Logik definieren:</span><span class="sxs-lookup"><span data-stu-id="79a2f-104">Let's define some requirements for our logic:</span></span>
- <span data-ttu-id="79a2f-105">Temperaturen zwischen 0 und 25 sollten mit **OK** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="79a2f-105">temperatures between 0-25 should be flagged as **OK**</span></span>
- <span data-ttu-id="79a2f-106">Temperaturen zwischen 26 und 50 sollten mit **CAUTION** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="79a2f-106">temperatures between 26-50 should be flagged as **CAUTION**</span></span>
- <span data-ttu-id="79a2f-107">Temperaturen über 50 sollten mit **DANGER** gekennzeichnet werden.</span><span class="sxs-lookup"><span data-stu-id="79a2f-107">temperatures above 50 should be flagged as **DANGER**</span></span>

## <a name="adding-a-function-to-an-azure-function-app"></a><span data-ttu-id="79a2f-108">Hinzufügen einer Funktion zu einer Azure-Funktions-App</span><span class="sxs-lookup"><span data-stu-id="79a2f-108">Adding a function to an Azure function app</span></span>

<span data-ttu-id="79a2f-109">Wie wir bereits erfahren haben, bietet Azure Unterstützung beim Lernen mit Azure Functions zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="79a2f-109">As we have already learned, Azure provides a helping hand when you're learning how to work with Azure Functions.</span></span> <span data-ttu-id="79a2f-110">Ein hervorragendes Feature, Functions kennenzulernen, ist das Generieren einer Funktion mit einer der vielen Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="79a2f-110">One great feature to get your feet wet with Functions is to generate one using one of many templates.</span></span> <span data-ttu-id="79a2f-111">In dieser Übung implementieren Sie mit der Vorlage HttpTrigger den Temperaturdienst.</span><span class="sxs-lookup"><span data-stu-id="79a2f-111">In this exercise, you will be using the HttpTrigger template to implement the temperature service.</span></span>

1. <span data-ttu-id="79a2f-112">Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com) an.</span><span class="sxs-lookup"><span data-stu-id="79a2f-112">Sign in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
1. <span data-ttu-id="79a2f-113">Greifen Sie durch Auswahl von **Alle Ressourcen** im linken Menü auf die Ressourcengruppe zu, die Sie in der ersten Übung erstellt haben, und wählen Sie dann **escalator-functions-group** aus.</span><span class="sxs-lookup"><span data-stu-id="79a2f-113">Access the resource group you created in the first exercise by choosing **All resources** in the left-hand menu, and then selecting **escalator-functions-group**.</span></span>
1. <span data-ttu-id="79a2f-114">Die Ressourcen für die Gruppe werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="79a2f-114">The resources for the group will then be displayed.</span></span> <span data-ttu-id="79a2f-115">Greifen Sie durch Auswahl von **escalator-functions-xxxxxxx** (auch durch das Blitzsymbol gekennzeichnet) auf die Funktions-App zu, die Sie in der vorherigen Übung erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="79a2f-115">Access the function app that you created in the previous exercise by selecting the **escalator-functions-xxxxxxx** item (also indicated by the lightning bolt icon).</span></span>
  <span data-ttu-id="79a2f-116">![Zugreifen auf die Funktions-App](../images/6-access-function-app.png)</span><span class="sxs-lookup"><span data-stu-id="79a2f-116">![Access the function app](../images/6-access-function-app.png)</span></span>
1. <span data-ttu-id="79a2f-117">Das Blatt zeigt einen Überblick über Ihre Funktions-App.</span><span class="sxs-lookup"><span data-stu-id="79a2f-117">The blade will show an overview of your function app.</span></span> <span data-ttu-id="79a2f-118">Es gibt auch eine Navigationsstruktur auf der linken Seite, die alle Funktionen, Proxys oder Slots anzeigt, die definiert sind.</span><span class="sxs-lookup"><span data-stu-id="79a2f-118">There is also a navigation tree on the left that shows any functions, proxies or slots that are defined.</span></span> <span data-ttu-id="79a2f-119">Da wir noch keine Funktion haben, ist sie leer.</span><span class="sxs-lookup"><span data-stu-id="79a2f-119">We don't have a function yet, so this  will be empty.</span></span> <span data-ttu-id="79a2f-120">Um eine Funktion zu erstellen, bewegen Sie den Mauszeiger in der Navigationsstruktur über **Funktion**, und klicken Sie auf die dann angezeigte Schaltfläche **+**.</span><span class="sxs-lookup"><span data-stu-id="79a2f-120">To create a function, move your mouse over **Function** in the navigation tree and click  the **+** button that appears.</span></span>
  <span data-ttu-id="79a2f-121">![Navigation zum Hinzufügen einer Funktion](../images/5-function-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="79a2f-121">![Add function navigation](../images/5-function-add-button.png)</span></span>
1. <span data-ttu-id="79a2f-122">Wählen Sie im vordefinierten Schnellstart-Funktionsformular den Link **Benutzerdefinierte Funktion** im Abschnitt **Selbstständig einsteigen**.</span><span class="sxs-lookup"><span data-stu-id="79a2f-122">In the quickstart premade function form, select the **Custom function** link in the **Get started on your own** section.</span></span>
  <span data-ttu-id="79a2f-123">![Vordefiniertes Funktionsformular](../images/6-custom-function.png)</span><span class="sxs-lookup"><span data-stu-id="79a2f-123">![Premade function form](../images/6-custom-function.png)</span></span>
1. <span data-ttu-id="79a2f-124">Jetzt wird eine Liste der Vorlagen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="79a2f-124">You are now presented with a list of templates.</span></span> <span data-ttu-id="79a2f-125">Wählen Sie die JavaScript-Implementierung der die HTTP-Triggervorlage aus.</span><span class="sxs-lookup"><span data-stu-id="79a2f-125">Select the JavaScript implementation of the HTTP trigger template.</span></span>
  <span data-ttu-id="79a2f-126">![HTTP-Triggervorlage](../images/6-httptrigger-template.png)</span><span class="sxs-lookup"><span data-stu-id="79a2f-126">![HTTP trigger template](../images/6-httptrigger-template.png)</span></span>
1. <span data-ttu-id="79a2f-127">Ein Blatt wird angezeigt, auf dem Sie definieren, können, was die Vorlage generieren soll.</span><span class="sxs-lookup"><span data-stu-id="79a2f-127">A blade will appear, allowing you to define what the template will generate.</span></span> <span data-ttu-id="79a2f-128">In diesem Fall möchten Sie eine JavaScript-Funktion mit dem Namen **DriveGearTemperatureService** generieren.</span><span class="sxs-lookup"><span data-stu-id="79a2f-128">In this case, you are interested in generating a JavaScript function named **DriveGearTemperatureService**.</span></span> <span data-ttu-id="79a2f-129">Nachdem Sie Ihre Funktion benannt haben, drücken Sie die Schaltfläche **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="79a2f-129">After you have named your function, press the **Create** button.</span></span>
  <span data-ttu-id="79a2f-130">![Formular zum Erstellen eines HTTP-Triggers](../images/6-create-httptrigger-form.png)</span><span class="sxs-lookup"><span data-stu-id="79a2f-130">![Create HTTP trigger form](../images/6-create-httptrigger-form.png)</span></span>
1. <span data-ttu-id="79a2f-131">Nach einigen Augenblicken wird der auf der Vorlage basierende Quellcode für Ihre Funktion angezeigt.</span><span class="sxs-lookup"><span data-stu-id="79a2f-131">After a few moments, you will be presented with the templated source code for your function.</span></span> <span data-ttu-id="79a2f-132">Die vordefinierte Funktion erwartet, dass ein Name übergeben wird, und sie gibt **Hello, {Name}** zurück.</span><span class="sxs-lookup"><span data-stu-id="79a2f-132">The premade function expects a name to be passed in, and it will return **Hello, {name}**.</span></span>

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

1. <span data-ttu-id="79a2f-133">Auf der rechten Seite der Quellenansicht sehen Sie zwei Registerkarten.</span><span class="sxs-lookup"><span data-stu-id="79a2f-133">On the right-hand side of the source view, you will see two tabs.</span></span> <span data-ttu-id="79a2f-134">Alle Dateien, die die Funktion unterstützen, werden auf der Registerkarte **Dateien anzeigen** angezeigt. Sie können **function.json** auswählen, um die Konfiguration der Funktion anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="79a2f-134">You are able to view all the files supporting the function in the **View files** tab. You can select **function.json** to view the configuration of the function.</span></span> <span data-ttu-id="79a2f-135">Hier sehen Sie den definierten httpTrigger sowie die Ausgabebindung.</span><span class="sxs-lookup"><span data-stu-id="79a2f-135">Here you can see the httpTrigger defined, as well as the output binding.</span></span> <span data-ttu-id="79a2f-136">Diese Konfiguration beschreibt, dass die Funktion durch eine HTTP-Anforderung initiiert wird, und die Ausgabebindung beschreibt, dass die Antwort als HTTP-Antwort gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="79a2f-136">This configuration describes that the function is initiated by an HTTP request, and the output binding describes that the response will be sent as an HTTP response.</span></span>

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

## <a name="running-the-premade-azure-function"></a><span data-ttu-id="79a2f-137">Ausführen der vordefinierten Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="79a2f-137">Running the premade Azure function</span></span>

<span data-ttu-id="79a2f-138">Um die Funktion auszuführen, können Sie an einer Eingabeaufforderung eine HTTP-Anforderung von cURL initiieren.</span><span class="sxs-lookup"><span data-stu-id="79a2f-138">To run the function, you can initiate an HTTP request from cURL from a command prompt.</span></span> <span data-ttu-id="79a2f-139">Um die Endpunkt-URL zu finden, kehren Sie zu Ihrem Funktionscode zurück, und wählen Sie den Link **Funktions-URL abrufen** aus.</span><span class="sxs-lookup"><span data-stu-id="79a2f-139">To find the endpoint URL, return to your function code and select the **Get function URL** link.</span></span> <span data-ttu-id="79a2f-140">Kopieren Sie diesen Link in die Zwischenablage.</span><span class="sxs-lookup"><span data-stu-id="79a2f-140">Copy this link to your clipboard.</span></span>  <span data-ttu-id="79a2f-141">Die URL sollte etwa wie folgt aussehen: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Endpunkt-URL abrufen](../images/6-get-function-url.png)</span><span class="sxs-lookup"><span data-stu-id="79a2f-141">Your URL should look something similar to the following: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Get endpoint URL](../images/6-get-function-url.png)</span></span>

<span data-ttu-id="79a2f-142">Führen Sie mit dieser URL einen cURL-Befehl aus, um Ihre Funktion zu initiieren (ersetzen Sie die URL durch Ihre eigene):</span><span class="sxs-lookup"><span data-stu-id="79a2f-142">With that URL, run a cURL command to initiate your function (replacing the URL with your own):</span></span>

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![Vordefinierte Funktions-cURL-Antwort](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a><span data-ttu-id="79a2f-144">Hinzufügen von Geschäftslogik zur Funktion</span><span class="sxs-lookup"><span data-stu-id="79a2f-144">Adding business logic to the function</span></span>

<span data-ttu-id="79a2f-145">Unsere Funktion erwartet ein Array von Temperaturmesswerten vom Kunden.</span><span class="sxs-lookup"><span data-stu-id="79a2f-145">Our function is expecting an array of temperature readings from the customer.</span></span> <span data-ttu-id="79a2f-146">Dies ist ein Beispiel des Anforderungstexts:</span><span class="sxs-lookup"><span data-stu-id="79a2f-146">This is an example of the request body:</span></span>

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

<span data-ttu-id="79a2f-147">Ändern Sie den Code der vordefinierten Funktion, um die erforderliche Geschäftslogik zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="79a2f-147">Modify the premade function code to implement the required business logic.</span></span> <span data-ttu-id="79a2f-148">Öffnen Sie die Datei „index.js“, und ersetzen Sie sie durch die folgende Liste:</span><span class="sxs-lookup"><span data-stu-id="79a2f-148">Open the index.js file, and replace it with the following listing:</span></span>

```javascript
module.exports = function (context, req) {
    context.log('Drive Gear Temperature Service triggered');
    if (req.body && req.body.readings) {
        for(var i=0; i<req.body.readings.length; i++){
            var reading = req.body.readings[i];
            if(reading.temperature<=25){
                context.log('Reading is OK');
                reading.status = 'OK';
                continue;
            }
            if(reading.temperature<=50){
                context.log('Reading is CAUTION');
                reading.status = 'CAUTION';
                continue;
            }
            context.log('Reading is DANGER');
            reading.status = 'DANGER'
        }
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

<span data-ttu-id="79a2f-149">Beachten Sie die Protokollanweisungen.</span><span class="sxs-lookup"><span data-stu-id="79a2f-149">Notice the log statements.</span></span> <span data-ttu-id="79a2f-150">Wenn die Funktion ausgeführt wird, werden sie Meldungen im Protokollfenster hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="79a2f-150">When the function runs, they will add messages in the log window.</span></span>

## <a name="testing-your-business-logic"></a><span data-ttu-id="79a2f-151">Testen Ihrer Geschäftslogik</span><span class="sxs-lookup"><span data-stu-id="79a2f-151">Testing your business logic</span></span>

<span data-ttu-id="79a2f-152">Öffnen Sie das Testfenster rechts im Flyout-Menü, und fügen Sie die Beispielanforderung von oben in das Anforderungstextfeld ein.</span><span class="sxs-lookup"><span data-stu-id="79a2f-152">Open the test window from the right-hand side flyout menu, and paste the sample request from above into the request body text box.</span></span> <span data-ttu-id="79a2f-153">Betätigen Sie die Schaltfläche **Ausführen**, und betrachten Sie die Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="79a2f-153">Press the **Run** button and view the output.</span></span> <span data-ttu-id="79a2f-154">Sie können das Protokollfenster auch im unteren Flyout-Menü öffnen, um die Protokollierungsanweisungen im Protokoll zu sehen.</span><span class="sxs-lookup"><span data-stu-id="79a2f-154">You can also open the log window from the bottom flyout menu to see the logging statements in the log.</span></span>
<span data-ttu-id="79a2f-155">![Testen der Geschäftslogik](../images/6-portal-testing.png) Die JSON-Daten im Ausgabefenster zeigen, dass unser Temperaturstatusfeld jedem der einzelnen Messwerte ordnungsgemäß hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="79a2f-155">![Testing the business Logic](../images/6-portal-testing.png) You can see from the JSON data in the output window that our temperature status field has been added to each of the readings correctly.</span></span> <span data-ttu-id="79a2f-156">Sie können auch auf dem Monitor-Dashboard prüfen, ob die Anforderung in Application Insights protokolliert wurde.</span><span class="sxs-lookup"><span data-stu-id="79a2f-156">You may also visit the Monitor dashboard to see that the request has been logged to Application Insights.</span></span>
<span data-ttu-id="79a2f-157">![Anforderung in Application Insights](../images/6-app-insights.png)</span><span class="sxs-lookup"><span data-stu-id="79a2f-157">![Request in Application Insights](../images/6-app-insights.png)</span></span>
