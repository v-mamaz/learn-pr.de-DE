In dieser Übung fahren wir mit unserem Zahnradsteuerungs-Beispiel fort und fügen die Logik für den Temperaturdienst hinzu. Insbesondere werden wir Daten von einer HTTP-Anforderung empfangen.

## <a name="function-requirements"></a>Anforderungen an die Funktion
Lassen Sie uns einige Anforderungen für unsere Logik definieren:
- Temperaturen zwischen 0 und 25 sollten mit **OK** gekennzeichnet werden.
- Temperaturen zwischen 26 und 50 sollten mit **CAUTION** gekennzeichnet werden.
- Temperaturen über 50 sollten mit **DANGER** gekennzeichnet werden.

## <a name="adding-a-function-to-an-azure-function-app"></a>Hinzufügen einer Funktion zu einer Azure-Funktions-App

Wie wir bereits erfahren haben, bietet Azure Unterstützung beim Lernen mit Azure Functions zu arbeiten. Ein hervorragendes Feature, Functions kennenzulernen, ist das Generieren einer Funktion mit einer der vielen Vorlagen. In dieser Übung implementieren Sie mit der Vorlage HttpTrigger den Temperaturdienst.

1. Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com) an.
1. Greifen Sie durch Auswahl von **Alle Ressourcen** im linken Menü auf die Ressourcengruppe zu, die Sie in der ersten Übung erstellt haben, und wählen Sie dann **escalator-functions-group** aus.
1. Die Ressourcen für die Gruppe werden angezeigt. Greifen Sie durch Auswahl von **escalator-functions-xxxxxxx** (auch durch das Blitzsymbol gekennzeichnet) auf die Funktions-App zu, die Sie in der vorherigen Übung erstellt haben.
  ![Zugreifen auf die Funktions-App](../images/6-access-function-app.png)
1. Das Blatt zeigt einen Überblick über Ihre Funktions-App. Es gibt auch eine Navigationsstruktur auf der linken Seite, die alle Funktionen, Proxys oder Slots anzeigt, die definiert sind. Da wir noch keine Funktion haben, ist sie leer. Um eine Funktion zu erstellen, bewegen Sie den Mauszeiger in der Navigationsstruktur über **Funktion**, und klicken Sie auf die dann angezeigte Schaltfläche **+**.
  ![Navigation zum Hinzufügen einer Funktion](../images/5-function-add-button.png)
1. Wählen Sie im vordefinierten Schnellstart-Funktionsformular den Link **Benutzerdefinierte Funktion** im Abschnitt **Selbstständig einsteigen**.
  ![Vordefiniertes Funktionsformular](../images/6-custom-function.png)
1. Jetzt wird eine Liste der Vorlagen angezeigt. Wählen Sie die JavaScript-Implementierung der die HTTP-Triggervorlage aus.
  ![HTTP-Triggervorlage](../images/6-httptrigger-template.png)
1. Ein Blatt wird angezeigt, auf dem Sie definieren, können, was die Vorlage generieren soll. In diesem Fall möchten Sie eine JavaScript-Funktion mit dem Namen **DriveGearTemperatureService** generieren. Nachdem Sie Ihre Funktion benannt haben, drücken Sie die Schaltfläche **Erstellen**.
  ![Formular zum Erstellen eines HTTP-Triggers](../images/6-create-httptrigger-form.png)
1. Nach einigen Augenblicken wird der auf der Vorlage basierende Quellcode für Ihre Funktion angezeigt. Die vordefinierte Funktion erwartet, dass ein Name übergeben wird, und sie gibt **Hello, {Name}** zurück.

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

1. Auf der rechten Seite der Quellenansicht sehen Sie zwei Registerkarten. Alle Dateien, die die Funktion unterstützen, werden auf der Registerkarte **Dateien anzeigen** angezeigt. Sie können **function.json** auswählen, um die Konfiguration der Funktion anzuzeigen. Hier sehen Sie den definierten httpTrigger sowie die Ausgabebindung. Diese Konfiguration beschreibt, dass die Funktion durch eine HTTP-Anforderung initiiert wird, und die Ausgabebindung beschreibt, dass die Antwort als HTTP-Antwort gesendet wird.

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

## <a name="running-the-premade-azure-function"></a>Ausführen der vordefinierten Azure-Funktion

Um die Funktion auszuführen, können Sie an einer Eingabeaufforderung eine HTTP-Anforderung von cURL initiieren. Um die Endpunkt-URL zu finden, kehren Sie zu Ihrem Funktionscode zurück, und wählen Sie den Link **Funktions-URL abrufen** aus. Kopieren Sie diesen Link in die Zwischenablage.  Die URL sollte etwa wie folgt aussehen: https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg== ![Endpunkt-URL abrufen](../images/6-get-function-url.png)

Führen Sie mit dieser URL einen cURL-Befehl aus, um Ihre Funktion zu initiieren (ersetzen Sie die URL durch Ihre eigene):

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

![Vordefinierte Funktions-cURL-Antwort](../images/6-premadefunction-curl.png)

## <a name="adding-business-logic-to-the-function"></a>Hinzufügen von Geschäftslogik zur Funktion

Unsere Funktion erwartet ein Array von Temperaturmesswerten vom Kunden. Dies ist ein Beispiel des Anforderungstexts:

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

Ändern Sie den Code der vordefinierten Funktion, um die erforderliche Geschäftslogik zu implementieren. Öffnen Sie die Datei „index.js“, und ersetzen Sie sie durch die folgende Liste:

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

Beachten Sie die Protokollanweisungen. Wenn die Funktion ausgeführt wird, werden sie Meldungen im Protokollfenster hinzufügen.

## <a name="testing-your-business-logic"></a>Testen Ihrer Geschäftslogik

Öffnen Sie das Testfenster rechts im Flyout-Menü, und fügen Sie die Beispielanforderung von oben in das Anforderungstextfeld ein. Betätigen Sie die Schaltfläche **Ausführen**, und betrachten Sie die Ausgabe. Sie können das Protokollfenster auch im unteren Flyout-Menü öffnen, um die Protokollierungsanweisungen im Protokoll zu sehen.
![Testen der Geschäftslogik](../images/6-portal-testing.png) Die JSON-Daten im Ausgabefenster zeigen, dass unser Temperaturstatusfeld jedem der einzelnen Messwerte ordnungsgemäß hinzugefügt wurde. Sie können auch auf dem Monitor-Dashboard prüfen, ob die Anforderung in Application Insights protokolliert wurde.
![Anforderung in Application Insights](../images/6-app-insights.png)
