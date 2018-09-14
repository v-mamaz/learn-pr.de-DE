Nachdem Sie die Funktions-App erstellt haben, erfahren Sie jetzt, wie Sie eine Azure-Funktion erstellen, konfigurieren und ausführen.

### <a name="triggers"></a>Trigger

Funktionen sind ereignisgesteuert, d.h., sie werden als Reaktion auf ein Ereignis ausgeführt.

Die Art Ereignis, die die Funktion startet, wird als *Trigger* bezeichnet. Sie konfigurieren eine Funktion mit genau einem Trigger.

 Azure unterstützt Trigger für die folgenden Dienste.


|Dienst  |Beschreibung des Triggers  |
|---------|---------|
|Blob-Speicher     |  Startet eine Funktion, wenn ein neues oder aktualisiertes Blob erkannt wird.       |
|Cosmos DB     |  Startet eine Funktion, wenn Einfügungen und Aktualisierungen erkannt werden.      |
|Event Grid     |   Startet eine Funktion, wenn ein Ereignis von Event Grid empfangen wird.       |
|HTTP     |   Startet eine Funktion mit einer HTTP-Anforderung.      |
|Microsoft Graph-Ereignisse     |  Startet eine Funktion als Reaktion auf einen von Microsoft Graph eingehenden Webhook. Jede Instanz dieses Triggers kann auf einen Microsoft Graph-Ressourcentyp reagieren.       |
|Queue Storage     |    Startet eine Funktion, wenn ein neues Element in einer Warteschlange eingeht. Die Warteschlangennachricht wird als Eingabe für die Funktion bereitgestellt.      |
|Service Bus     |  Startet eine Funktion als Reaktion auf Nachrichten aus einer Service Bus-Warteschlange.       |
|Timer     |  Startet eine Funktion gemäß einem Zeitplan.       |
|Webhooks     |  Startet eine Funktion mit einer Webhookanforderung.       |

### <a name="bindings"></a>Bindungen

Azure Functions-Bindungen sind eine deklarative Möglichkeit, Daten und Dienste mit Ihrer Funktion zu verbinden. Sie müssen keinen Code in Ihrer Funktion schreiben, um sich mit Datenquellen zu verbinden und Verbindungen zu verwalten. Die Plattform übernimmt diese komplexe Aufgabe für Sie. Eine Bindung hat eine Richtung. Ihr Code liest Daten aus *Eingabe*bindungen und schreibt Daten in *Ausgabe*bindungen. Schauen wir uns ein Beispiel an.

Um Daten aus dem Blob-Speicher zu lesen, konfigurieren Sie eine Eingabebindung des Typs *Blob*. Um eine Nachricht an den Warteschlangenspeicher zu schreiben, konfigurieren Sie eine Ausgabebindung des Typs *Warteschlange*.

Weitere Informationen zu den unterstützten Bindungen und Triggern finden Sie in der [Dokumentation zu Azure](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings).

### <a name="a-sample-trigger-and-binding-functionjson"></a>Beispieltrigger und -bindung (function.json)

Der folgende JSON-Code ist eine Beispieldefinition eines Triggers und einer Bindung für eine Funktion.

```javascript
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

Wie bereits erwähnt wurde, verfügt jede Bindung über eine Richtung, die definiert, ob es sich um eine Eingabe- oder eine Ausgabebindung handelt. Trigger sind stets Eingabebindungen. Das obige Beispiel zeigt eine Funktion, die durch eine Nachricht ausgelöst wird, welche der Warteschlange namens **myqueue-items** hinzugefügt wird. Danach wird der Rückgabewert der Funktion an die Tabelle **outTable** im Azure-Tabellenspeicher gesendet.

## <a name="creating-a-function-in-the-azure-portal"></a>Erstellen einer Funktion im Azure-Portal

Azure stellt vorkonfigurierte Vorlagen für gängige Szenarios mit Azure-Funktionen bereit.

### <a name="quickstart-templates"></a>Schnellstartvorlagen

Um eine Azure-Funktion hinzuzufügen, müssen Sie eine Funktions-App auswählen. Sie erkennen eine Funktions-App am Blitzsymbol zwischen spitzen Klammern.  
![Screenshot einer Funktions-App, die in einer Ressourcengruppe ausgewählt wurde.](../images/5-function-icon.png)

Wenn Sie zum ersten Mal eine Azure-Funktion hinzufügen, wird Ihnen der Bildschirm für den Schnellstart angezeigt. Auf diesem Bildschirm können Sie einen Triggertyp und eine Programmiersprache auswählen. Azure erstellt dann basierend auf Ihrer Auswahl den Funktionscode und die Konfiguration für Sie. 
 
![Schnellstart für Funktion](../images/5-quickstart-form.png)

### <a name="function-templates"></a>Funktionsvorlagen

Die Auswahl von Vorlagen ist nicht auf die Vorlagen beschränkt, die im Schnellstart angezeigt werden. Sie können aus über 30 verschiedenen Vorlagen auswählen. Sie können auf den Bildschirm mit der Vorlagenliste zugreifen, während Sie weitere Funktionen erstellen oder indem Sie auf dem Schnellstartbildschirm die Option **Benutzerdefinierte Funktion** auswählen.  
![Screenshot der Azure Functions-Schnellstartbenutzeroberfläche, die Sie mit einer vorgefertigten Funktion bei den ersten Schritten unterstützt.](../images/5-template-list.png)

## <a name="navigating-to-your-function-and-files"></a>Navigieren zu Ihrer Funktion und Ihren Dateien

Nachdem Sie eine Funktion anhand einer Vorlage erstellt haben, werden mehrere Dateien generiert. Wenn Sie beispielsweise den Schnellstart „Webhook + API“ mit JavaScript gewählt haben, handelt es sich bei den generierten Dateien um eine Konfigurationsdatei, **function.json**, und eine Quellcodedatei, **index.js**. Die Funktionen, die Sie in einer Funktions-App erstellen, werden im Portal für Funktions-Apps unter dem Menüelement „Funktionen“ angezeigt.

Wenn Sie eine Funktion in Ihrer Funktions-App auswählen, wird ein Code-Editor geöffnet, in dem – wie im folgenden Screenshot – der Code für Ihre Funktion angezeigt wird.

![Screenshot der Benutzeroberfläche zur Auswahl von Funktionsvorlagen mit einer Liste von Vorlagen, mit denen Sie die Funktionsentwicklung beschleunigen können.](../images/5-file-navigation.png)

Wie Sie im obigen Screenshot sehen können, gibt es auf der rechten Seite ein Flyoutmenü, das die Registerkarte **Dateien anzeigen** enthält. Wenn Sie diese Registerkarte auswählen, wird die Dateistruktur angezeigt, aus der sich Ihre Funktion zusammensetzt.  

## <a name="execution-options-for-testing-your-azure-function"></a>Ausführungsoptionen zum Testen Ihrer Azure-Funktion

Nachdem Sie eine Funktion erstellt haben, sollten Sie diese testen. Hierzu gibt es verschiedene Verfahren: manuelles Ausführen und Testen im Azure-Portal.

### <a name="manual-execution-of-a-function"></a>Manuelle Ausführung einer Funktion

Sie können eine Funktion starten, indem Sie den konfigurierten Trigger manuell auslösen. Wenn Sie beispielsweise einen HttpTrigger verwenden, können Sie mit einem Tool wie Postman oder cURL eine HTTP-Anforderung an Ihrer Funktionsendpunkt-URL initiieren.  

![Teil-Screenshot der Postman-Anwendungsschnittstelle mit einer im Feld „URL“ eingegebenen Funktions-URL und Beispieltext im Anforderungstextbereich. ](../images/5-postman-execution.png)

Um die Endpunkt-URL zu erhalten, wählen Sie den HTTP-Trigger im linken Navigationsbereich aus, und wählen Sie dann die Schaltfläche **Funktions-URL abrufen** aus.  

![Screenshot des Funktions-Apps-Portals mit einer ausgewählten Funktion und der am oberen Rand der Seite ausgewählten Aktion *Funktions-URL abrufen*.](../images/5-get-function-url.png)

### <a name="testing-a-function-in-the-azure-portal"></a>Testen einer Funktion im Azure-Portal

Im Azure-Portal lassen sich auch Ihre Funktionen bequem testen. Auf der rechten Seite des Codefensters finden Sie ein Flyoutmenü mit Registerkartennavigation. Dieses Menü enthält ein Element **Test**. Das Erweitern des Menüs und das Auswählen dieser Registerkarte ist eine weitere Möglichkeit, Ihre Funktion auszuführen und das Ergebnis anzuzeigen. Wie im HttpTrigger-Szenario können Sie die HTTP-Methode festlegen und der Anforderung Parameter für die Abfragezeichenfolge sowie HTTP-Header hinzufügen. Sie können ferner den Anforderungstext ändern, um weitere Szenarios zu testen. Im folgenden Beispiel ist der Test als HTTP POST-Anforderung mit einem Anforderungstext konfiguriert, der einen Parameter namens *Name* umfasst.
 
![Screenshot des Testfensters im Funktions-Apps-Portal mit einer HTTP POST-Anforderung und einem Beispielanforderungstext. Der Ausgabebereich enthält das Ergebnis eines Funktionsaufrufs mit den Wörtern „Hello Azure“.](../images/5-portal-execution.png)

Wenn Sie in diesem Testfenster auf **Ausführen** klicken, werden die Ergebnisse zusammen mit einem Statuscode im Ausgabefenster angezeigt. 

## <a name="monitoring-an-azure-function"></a>Überwachen einer Azure-Funktion

Die Fähigkeit, Meldungen zu protokollieren und Ihre Funktionen zu überwachen, ist während der Entwicklung und in der Produktion unerlässlich. Im Azure-Portal finden Sie ein Überwachungsdashboard und die Möglichkeit, Ausführungsprotokolle sowie Ausnahmen zu überprüfen, die von Ihren Azure-Funktionen empfangen wurden.

### <a name="log-window"></a>Protokollfenster

Sie können Ihrer Funktion auch Protokollanweisungen hinzufügen. Diese Anweisungen werden im Protokollfenster der Funktion angezeigt. Sie finden das Protokollfenster in einem Flyoutmenü mit Registerkarten, das sich am unteren Rand des Codefensters befindet. Der folgende JavaScript-Codeausschnitt zeigt, wie eine Meldung mit der `context.log`-Methode protokolliert wird.

```javascript
  context.log('Enter your logging statement here');
```  

![Screenshot des Code-Editor-Abschnitts der Azure Functions-Benutzeroberfläche. Eine Codezeile, die die context.log()-Methode verwendet, um eine Meldung im Protokollfenster zu protokollieren, ist ebenfalls hervorgehoben.](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a>Fenster mit Fehlern und Warnungen

Sie finden die Registerkarte für das Fenster mit Fehlern und Warnungen im gleichen Flyoutmenü wie das Protokollfenster. Dieser Fehler zeigt Kompilierungsfehler und -warnungen innerhalb Ihres Codes. Da JavaScript eine dynamische und interpretierte Sprache ist, zeigt die folgende Abbildung einen Kompilierungsfehler in einer C#-Funktion.  

![Screenshot des Code-Editor-Abschnitts der Azure Functions-Benutzeroberfläche, bei dem das Fenster **Protokolle** am unteren Bildschirmrand hervorgehoben ist.](../images/5-errors-window.png)

### <a name="monitoring-dashboard"></a>Überwachungsdashboard

Wenn Sie im Navigationsmenü der Funktions-App den Funktionsknoten erweitern, sehen Sie ein Menüelement **Monitor**. Das Überwachungsdashboard bietet eine schnelle Möglichkeit, den Verlauf von Funktionsausführungen anzuzeigen. Diese Ansicht zeigt den Zeitstempel, den Ergebniscode, die Dauer und die Vorgangs-ID und zeigt ebenfalls an, ob die Ausführung erfolgreich abgeschlossen wurde. Die Daten werden über Azure Application Insights aufgefüllt.  

![Screenshot des Überwachungsdashboards, das über den Funktionsmenüpunkt **Monitor** gestartet wurde, einschließlich einer Liste der erfolgreichen und fehlgeschlagenen Aufrufe der Funktion.](../images/5-monitor-function.png)
