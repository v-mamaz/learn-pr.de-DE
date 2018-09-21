Lassen Sie uns wir mit unserem Zahnradsteuerungs-Beispiel fortfahren und die Logik für den Temperaturdienst hinzufügen. Insbesondere werden wir Daten von einer HTTP-Anforderung empfangen.

## <a name="function-requirements"></a>Anforderungen an die Funktion

Zuerst müssen wir einige Anforderungen an unsere Logik definieren:

- Temperaturen von 0 bis 25 sollen mit **OK** gekennzeichnet werden.
- Temperaturen von 26 bis 50 sollen mit **CAUTION** gekennzeichnet werden.
- Temperaturen über 50 sollen mit **DANGER** gekennzeichnet werden.

## <a name="add-a-function-to-our-function-app"></a>Hinzufügen einer Funktion zu unserer Funktions-App

Wie in der vorherigen Einheit bereits erläutert wurde, verfügt Azure über Vorlagen, die Ihnen das Erstellen von Funktionen erleichtern. In dieser Einheit verwenden wir die Vorlage `HttpTrigger`, um den Temperaturdienst zu implementieren.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) an.

1. Wählen Sie durch Auswahl von **Alle Ressourcen** im linken Menü die Ressourcengruppe aus der ersten Übung und dann **<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>** aus.

1. Daraufhin werden die Ressourcen für die Gruppe angezeigt. Klicken Sie auf den Namen der Funktions-App, die Sie in der vorherigen Übung erstellt haben, indem Sie das Element **escalator-functions-xxxxxxx** (auch durch das Blitzsymbol gekennzeichnet) auswählen.

  ![Screenshot: Das hervorgehobene Blatt „Alle Ressourcen“ sowie die von Ihnen erstellten Funktions-App „escalator“ im Azure-Portal.](../media/5-access-function-app.png)

1. Im linken Menü wird der Name Ihrer Funktions-App und ein Untermenü mit den folgenden drei Elementen angezeigt: *Funktionen*, *Proxys* und *Slots*.  Klicken Sie auf **Funktionen**, und klicken Sie dann am oberen Rand der angezeigten Seite auf **Neue Funktion**.

  ![Screenshot: Funktionsliste für die Funktions-App im Azure-Portal, wobei das Menüelement „Funktionen“ und die Schaltfläche „Neue Funktion“ hervorgehoben sind.](../media/5-function-add-button.png)

1. Klicken Sie auf dem Bildschirm „Schnellstart“ im Abschnitt **Get started on your own** (Selbstständig einsteigen) auf den Link **Benutzerdefinierte Funktion** (wie im folgenden Screenshot). Wenn der Bildschirm „Schnellstart“ nicht angezeigt wird, klicken Sie am oberen Rand der Seite auf den Link **Go to the quickstart** (Zum Schnellstart wechseln).

  ![Screenshot: Das Blatt „Schnellstart“ im Azure-Portal mit der hervorgehobenen Schaltfläche „Benutzerdefinierte Funktion“ im Abschnitt „Selbstständig einsteigen“.](../media/5-custom-function.png)

1. Wählen Sie wie im folgenden Screenshot gezeigt die **JavaScript**-Implementierung der Vorlage **HTTP-Trigger** aus der auf dem Bildschirm angezeigten Liste von Vorlagen aus.

1. Geben Sie **DriveGearTemperatureService** in das Feld „Name“ des nun angezeigten Dialogfelds **Neue Funktion** ein. Belassen Sie die Autorisierungsstufe auf „Funktion“, und klicken Sie auf die Schaltfläche **Erstellen**, um die Funktion zu erstellen.

  ![Screenshot: Das Azure-Portal mit den neuen Funktionsoptionen für HTTP-Trigger, das Feld für die Sprache ist auf JavaScript und der Name ist auf DriveGearTemperatureService festgelegt.](../media/5-create-httptrigger-form.png)

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

Unsere-Funktion erwartet einen Namen, der entweder über die Abfragezeichenfolge der HTTP-Anforderung oder als Teil des Anforderungstexts übergeben wird. Die Funktion antwortet mit der Meldung **Hello, {Name}**, die den in der Anforderung gesendeten Namen wiedergibt.

Auf der rechten Seite der Quellansicht sehen Sie zwei Registerkarten. Auf der Registerkarte **Datei anzeigen** werden der Code und die Konfigurationsdatei Ihrer Funktion aufgelistet.  Wählen Sie **function.json** aus, um die Konfiguration der Funktion anzuzeigen, die in etwa wie folgt aussehen sollte:

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

Diese Konfiguration deklariert, dass die Funktion ausgeführt wird, sobald sie eine HTTP-Anforderung empfängt. Die Ausgabebindung deklariert, dass die Antwort als HTTP-Antwort gesendet wird.

## <a name="test-the-function"></a>Testen der Funktion

> [!TIP]
> **cURL** ist ein Befehlszeilentool, das zum Senden und Empfangen von Dateien verwendet werden kann. Es ist in Linux, MacOS und Windows 10 enthalten und kann für die meisten anderen Betriebssysteme heruntergeladen werden. cURL unterstützt zahlreiche Protokolle wie HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 usw. Weitere Informationen finden Sie unter den unten angegebenen Links:
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/>

Zum Testen der Funktion können Sie über die Befehlszeile mit cURL eine HTTP-Anforderung an die Funktions-URL senden. Um die Endpunkt-URL der Funktion zu finden, kehren Sie zu Ihrem Funktionscode zurück, und klicken Sie wie im folgenden Screenshot gezeigt auf den Link **Funktions-URL abrufen**. Speichern Sie diesen Link vorübergehend.

![Screenshot: Der Funktionen-Editor im Azure-Portal mit der hervorgehobenen Schaltfläche „Funktions-URL abrufen“.](../media/5-get-function-url.png)

### <a name="securing-http-triggers"></a>Schützen von HTTP-Triggern

Mit HTTP-Triggern können Sie API-Schlüssel verwenden, um unbekannte Aufrufer zu blockieren, indem Sie verlangen, dass der Schlüssel bei jeder Anforderung vorhanden ist. Beim Erstellen einer Funktion wählen Sie die _Autorisierungsstufe_ aus. Standardmäßig ist diese auf „Funktion“ festgelegt, was einen funktionsspezifischen API-Schlüssel erfordert. Sie kann aber auch auf „Administrator“ festgelegt werden, um einen globalen „Hauptschlüssel“ zu verwenden, oder auf „Anonym“, um anzugeben, dass kein Schlüssel benötigt wird. Sie können die Autorisierungsstufe auch nach dem Erstellen über die Funktionseigenschaften ändern.

Da wir bei der Erstellung dieser Funktion „Funktion“ angegeben haben, müssen wir beim Senden der HTTP-Anforderung den Schlüssel angeben. Sie können ihn als Parameter mit einer Abfragezeichenfolge mit dem Namen `code` oder als HTTP-Header (bevorzugt) mit dem Namen `x-functions-key` senden.

Funktions- und Masterschlüssel finden Sie im Abschnitt **Verwalten**, wenn die Funktion erweitert wird. Standardmäßig sind sie ausgeblendet, sodass Sie sie einblenden müssen.

1. Erweitern Sie Ihre Funktion, und wählen Sie den Abschnitt **Verwalten** aus. Zeigen Sie den Standardfunktionsschlüssel an, und kopieren Sie ihn in die Zwischenablage.

  ![Screenshot des Blatts „Verwalten“ im Azure-Portal mit hervorgehobenem eingeblendeten Funktionsschlüssel.](../media/5-get-function-key.png)

1. Formatieren Sie als Nächstes über die Befehlszeile, in der Sie das **cURL**-Tool installiert haben, einen cURL-Befehl mit der URL für Ihre Funktion und den Funktionsschlüssel.

    - Verwenden Sie eine `POST`-Anforderung.
    - Fügen Sie einen Headerwert für `Content-Type` des Typs `application/json` hinzu.
    - Achten Sie darauf, dass Sie die URL durch Ihre eigene ersetzen.
    - Übergeben Sie den Funktionsschlüssel als den Headerwert `x-functions-key`.

    ```bash
    curl --header "Content-Type: application/json" --header "x-functions-key: <your-function-key>" --request POST --data "{\"name\": \"Azure Function\"}" https://<your-url-here>/api/DriveGearTemperatureService
    ```

Die Funktion antwortet mit dem Text `"Hello Azure Function"`.

> [!NOTE]
> Sie können auch über den Abschnitt mit der Registerkarte **Testen** der jeweiligen Funktion einen Test für eine ausgewählte Funktion durchführen, jedoch nicht überprüfen, ob das Funktionsschlüsselsystem funktioniert, da es in diesem Fall nicht erforderlich ist. Fügen Sie die entsprechenden Header- und Parameterwerte in die Testschnittstelle ein, und klicken Sie auf die Schaltfläche **Ausführen**, um die Testausgabe anzuzeigen.

## <a name="add-business-logic-to-the-function"></a>Hinzufügen von Geschäftslogik zur Funktion

Als Nächstes fügen wir die Logik zur Funktion hinzu, die die empfangenen Temperaturmesswerte überprüft und für jeden einen Status festlegt.

Unsere Funktion erwartet ein Array von Temperaturmesswerten. Der folgende JSON-Codeausschnitt ist ein Beispiel für den Anforderungstext, den wir an unsere Funktion senden. Jeder `reading`-Eintrag verfügt über ID, Zeitstempel und Temperatur.

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

Beachten Sie die `log`-Anweisungen. Wenn die Funktion ausgeführt wird, fügen diese Anweisungen Meldungen im Protokollfenster hinzu.

## <a name="test-our-business-logic"></a>Testen der Geschäftslogik

In diesem Fall verwenden wir den Bereich **Test** im Portal, um unsere Funktion zu testen.

1. Öffnen Sie das Fenster **Test** im rechten Flyoutmenü.

1. Fügen Sie die Beispielanforderung in das Feld für den Anforderungstext ein.

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

1. Klicken Sie auf **Ausführen**, und zeigen Sie die Antwort im Ausgabebereich an. Um Protokollmeldungen anzuzeigen, öffnen Sie die Registerkarte **Protokolle** im Flyoutmenü unten auf der Seite. Im folgenden Screenshot wird eine Beispielantwort im Ausgabebereich und Nachrichten im Bereich **Protokolle** angezeigt.

![Screenshot: Blatt „Funktionen-Editor“ im Azure-Portal mit den angezeigten Registerkarten „Test“ und „Protokolle“. Eine Beispielantwort der Funktion wird im Ausgabebereich angezeigt.](../media/5-portal-testing.png)

Im Ausgabebereich sehen Sie, dass unser Statusfeld korrekt zu jedem Messwert hinzugefügt wurde.

Sie können auch auf dem **Dashboard „Monitor“** prüfen, ob die Anforderung in Application Insights protokolliert wurde.

![Screenshot: Die vorherigen Testergebnisse im Dashboard „Monitor“ im Azure-Portal.](../media/5-app-insights.png)
