In dieser Übung fahren wir mit unserem Zahnradsteuerungs-Beispiel fort und fügen die Logik für den Temperaturdienst hinzu. Insbesondere werden wir Daten von einer HTTP-Anforderung empfangen.

## <a name="function-requirements"></a>Anforderungen an die Funktion
Lassen Sie uns einige Anforderungen für unsere Logik definieren:
- Temperaturen zwischen 0 und 25 sollten mit **OK** gekennzeichnet werden.
- Temperaturen zwischen 26 und 50 sollten mit **CAUTION** gekennzeichnet werden.
- Temperaturen über 50 sollten mit **DANGER** gekennzeichnet werden.

## <a name="add-a-function-to-an-azure-function-app"></a>Hinzufügen einer Funktion zu einer Azure-Funktions-App

Wie in der vorherigen Einheit bereits erläutert wurde, verfügt Azure über Vorlagen, die Ihnen das Erstellen von Funktionen erleichtern. In dieser Übung verwenden Sie die Vorlage HttpTrigger, um den Temperaturdienst zu implementieren.

1. Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.
1. Wählen Sie durch Auswahl von **Alle Ressourcen** im linken Menü die Ressourcengruppe aus, die Sie in der ersten Übung erstellt haben, und wählen Sie dann **escalator-functions-group** aus.
1. Die Ressourcen für die Gruppe werden angezeigt. Greifen Sie durch Auswahl von **escalator-functions-xxxxxxx** (auch durch das Blitzsymbol gekennzeichnet) auf die Funktions-App zu, die Sie in der vorherigen Übung erstellt haben.
  ![Screenshot von „Alle Ressourcen“ im Portal, mit Hervorhebung der von uns erstellten „escalator-functions-group“ und Funktions-App.](../images/6-access-function-app.png)
1. Im linken Menü werden der Name Ihrer Funktions-App und ein Untermenü mit drei Elementen angezeigt – *Funktionen*, *Proxys* und *Slots*.  Um unsere erste Funktion zu erstellen, bewegen Sie den Mauszeiger in der Navigationsstruktur über **Funktionen**, und klicken Sie auf die dann angezeigte Schaltfläche **+**.
  ![Screenshot mit Pluszeichen (+), das angezeigt wird, wenn Sie mit der Maus über das Menüelement „Funktionen“ fahren, welches beim Anklicken die Funktionserstellung startet.](../images/5-function-add-button.png)
1. Wählen Sie auf dem Schnellstartbildschirm den Link **Benutzerdefinierte Funktion** im Abschnitt **Selbstständig einsteigen** wie im folgenden Screenshot gezeigt aus.
  ![Screenshot des Schnellstartbildschirms mit hervorgehobener Schaltfläche „Benutzerdefinierte Funktion“.](../images/6-custom-function.png)
1. Wählen Sie, wie im folgenden Screenshot gezeigt, aus der Liste der auf dem Bildschirm angezeigten Vorlagen die JavaScript-Implementierung der Vorlage „HTTP-Trigger“ aus.
  ![Screenshot der Vorlagenliste, bei dem der HTTP-Trigger und die JavaScript-Option hervorgehoben sind.](../images/6-httptrigger-template.png)
1.  Geben Sie **DriveGearTemperatureService** in das Feld „Name“ des nun angezeigten Dialogfelds **Neue Funktion** ein. Wählen Sie, nachdem Sie Ihre Funktion benannt haben, wie im folgenden Screenshot gezeigt die Schaltfläche **Erstellen** aus.
  ![Screenshot des Formulars „Neue Funktion“, bei dem das Feld „Name“ hervorgehoben ist und das mit dem Wert „DriveGearTemperatureService“ eingerichtet wurde](../images/6-create-httptrigger-form.png)
1. Nach Abschluss der Funktionserstellung wird der Code-Editor mit dem Inhalt der Codedatei *index.js* geöffnet. Der Standardcode, den die Vorlage für uns generiert hat, wird im folgenden Codeausschnitt aufgeführt.

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

Unsere-Funktion erwartet einen Namen, der entweder über die Abfragezeichenfolge der HTTP-Anforderung oder als Teil des Anforderungstexts übergeben wird. Die Funktion antwortet, indem sie die Nachricht **Hello, {name}** ausgibt und dabei den Namen verwendet, der in der Anforderung gesendet wurde.

1. Auf der rechten Seite der Quellenansicht sehen Sie zwei Registerkarten. Die Datei **View listet den Code und die Konfigurationsdatei für Ihre Funktion auf.  Wählen Sie **function.json** aus, um die Konfiguration der Funktion anzuzeigen. Der folgende Codeausschnitt zeigt den Inhalt der Datei **function.json**. Diese Konfiguration deklariert, dass die Funktion ausgeführt wird, wenn sie eine HTTP-Anforderung empfängt. Die Ausgabebindung deklariert, dass die Antwort als HTTP-Antwort gesendet wird.

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
> Beachten Sie, dass der Trigger in der obigen JSON-Datei in einem Array von Bindungen definiert wurde. Ein Trigger ist also eigentlich eine besondere Art von Bindung.

## <a name="run-our-function"></a>Ausführen Ihrer Funktion

> [!TIP]
> **cURL** ist ein Befehlszeilentool, das zum Senden oder Empfangen von Dateien verwendet werden kann. cURL.exe unterstützt zahlreiche Protokolle wie HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 usw. Weitere Informationen finden Sie unter den unten angegebenen Links:
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

Um unsere-Funktion zu testen, können Sie eine HTTP-Anforderung an die Funktions-URL senden und dabei cURL in der Befehlszeile verwenden. Um die Endpunkt-URL der Funktion zu finden, kehren Sie zu Ihrem Funktionscode zurück, und wählen Sie wie im folgenden Screenshot gezeigt den Link **Funktions-URL abrufen** aus. Kopieren Sie diesen Link in die Zwischenablage.  

 ![Screenshot des Code-Editors im Funktions-Apps-Bereich des Portals. Der Befehl „Funktions-URL abrufen“ ist in der rechten oberen Ecke hervorgehoben.](../images/6-get-function-url.png)

Führen Sie unter Verwendung dieser Funktions-URL den folgenden cURL-Befehl in der Befehlszeile aus. Ersetzen Sie dabei die URL durch Ihre eigene URL.

```bash
curl --header "Content-Type: application/json" --request POST --data "{\"name\": \"Azure Function\"}" https://escalator-functions-xxxxxxx.azurewebsites.net/api/DriveGearTemperatureService?code=RMt1K0AfulJmF4Ui8OSNLXsI3AFjbHznS8BcJsinBox3nDEKEwy1sg==
```

Der folgende Screenshot zeigt ein Beispiel für die Antwort, die Sie von der Standardimplementierung in der Befehlszeile erhalten.

![Screenshot eines Beispiel-cURL-Befehls und der Antwort in einer Befehlszeile.](../images/6-premadefunction-curl.png)

## <a name="add-business-logic-to-the-function"></a>Hinzufügen von Geschäftslogik zur Funktion

Nun wird es Zeit, die Logik zur Funktion hinzuzufügen, die die empfangenen Temperaturmesswerte überprüft und für jeden einen Status festlegt.

Unsere Funktion erwartet ein Array von Temperaturmesswerten. Der folgende JSON-Codeausschnitt ist ein Beispiel für den Anforderungstext, den wir an unsere Funktion senden. Jeder `reading`-Eintrag verfügt über ID, Zeitstempel und Temperatur.

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

Als Nächstes ersetzen wir den Standardcode in unserer Funktion durch den folgenden Code, der unsere Geschäftslogik implementiert. 

1. Öffnen Sie die Datei **index.js**, und ersetzen Sie sie durch den folgenden Code.

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
Die Logik, die wir hinzugefügt haben, ist einfach. Wir iterieren über das Array der Messwerte und überprüfen das Temperaturfeld. Abhängig vom Wert dieses Felds wird der Status **OK**, **CAUTION** oder **DANGER** festgelegt. Wir senden dann das Array der Messwerte mit einem zu jedem Eintrag hinzugefügten Statusfeld zurück.

Beachten Sie die Protokollanweisungen. Wenn die Funktion ausgeführt wird, fügen diese Anweisungen Meldungen im Protokollfenster hinzu.

## <a name="test-our-business-logic"></a>Testen der Geschäftslogik

In diesem Fall verwenden wir den Bereich **Test** im Portal, um unsere Funktion zu testen.

1. Öffnen Sie das Fenster **Test** im rechten Flyoutmenü.
1. Fügen Sie die obige Beispielanforderung in das Feld für den Anforderungstext ein. 
1. Wählen Sie **Ausführen** aus, und zeigen Sie die Antwort im Ausgabebereich an. Um Protokollmeldungen anzuzeigen, öffnen Sie die Registerkarte **Protokolle** im Flyout unten auf der Seite. Der folgende Screenshot zeigt eine Beispielantwort im Ausgabebereich und Meldungen im Bereich **Protokolle**.

![Screenshot der Registerkarten „Test“ und „Protokolle“ der Benutzeroberfläche „Funktionen“ im Portal. Eine Beispielantwort der Funktion wird im Ausgabebereich auf der Registerkarte „Test“ angezeigt.](../images/6-portal-testing.png)

Im Ausgabebereich sehen Sie, dass unser Statusfeld korrekt zu jedem Messwert hinzugefügt wurde.

Sie können auch auf dem Dashboard **Monitor** prüfen, ob die Anforderung in Application Insights protokolliert wurde.

![Screenshot von Teilen des Dashboards „Monitor“ mit einer Erfolgsmeldung unserer Funktion.](../images/6-app-insights.png)

