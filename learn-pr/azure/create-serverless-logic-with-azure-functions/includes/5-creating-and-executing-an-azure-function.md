Nachdem Sie die Funktions-App erstellt haben, erfahren Sie jetzt, wie Sie eine Azure-Funktion erstellen, konfigurieren und ausführen.

### <a name="triggers"></a>Trigger
Azure-Funktionen sind ereignisgesteuert und werden als Reaktion auf ein Ereignis ausgeführt, wie z.B. der Empfang einer HTTP-Anforderung oder das Hinzufügen einer Nachricht zu einer Warteschlange. 

Die Art Ereignis, die eine Funktion initiiert, wird als Trigger bezeichnet. Für Azure-Funktionen muss mindestens ein Trigger konfiguriert werden. Andernfalls gibt es keine Möglichkeit, die Funktion auszuführen.

 Azure unterstützt eine Vielzahl von Triggern, beispielsweise die folgenden:
* HTTPTrigger
* TimerTrigger
* GitHub-Webhook
* CosmosDBTrigger
* BlobTrigger
* QueueTrigger
* EventHubTrigger
* ServiceBusQueueTrigger
* ServiceBusTopicTrigger

### <a name="bindings"></a>Bindungen
Azure-Funktionsbindungen sind eine deklarative Möglichkeit, programmgesteuert eine Verbindung zwischen Ihren Daten und Ihrer Funktion herzustellen.

Bindungen sind die Verbindung mit Ihren Datendiensten. Eine Azure-Funktion mit null, einer oder mehreren Bindungen ermöglicht Ihnen den Zugriff auf mehrere Datenquellen. Sie können sie auch als Eingabe- oder Ausgabebindungen oder als Lese- oder Schreibbindungen definieren.

Angenommen, Sie verfügen über einen QueueTrigger, der eine Funktion initiiert, wenn einer Warteschlange ein Blob hinzugefügt wird. Zum Herstellen der Verbindung mit Azure Blob Storage wird eine Eingabeblobbindung verwendet. 

Ausgabebindungen werden zum Speichern von Daten verwendet. Sie senden beispielsweise den Rückgabewert der Funktion an Azure Table Storage.

Eine vollständige Liste der verfügbaren Bindungen finden Sie in der [Azure-Dokumentation](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings).

### <a name="a-sample-trigger-and-binding-functionjson"></a>Beispieltrigger und -bindung (function.json)
Dies ist eine Beispieldefinition eines Triggers und einer Bindung für eine Funktion. Sie werden feststellen, dass je nach Art der Bindung, die Sie beschreiben, verschiedene Eigenschaftswerte festgelegt werden müssen. Jede Bindung verfügt auch über eine Richtung, die definiert, ob es sich um Eingabe- oder Ausgabebindung handelt. Trigger sind immer Eingabebindungen. Dieses Beispiel zeigt eine Funktion, die durch eine Nachricht ausgelöst wird, die der Warteschlange namens **myqueue-items** hinzugefügt wird. Danach wird der Rückgabewert der Funktion an die **outTable**-Tabelle in Azure Table Storage gesendet.

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
## <a name="premade-functions-and-templates"></a>Vorkonfigurierte Funktionen und Vorlagen
Azure stellt vorkonfigurierte Vorlagen für häufige Szenarien mit Azure-Funktionen bereit.

### <a name="quickstart-templates"></a>Schnellstartvorlagen
Um eine Azure-Funktion hinzuzufügen, müssen Sie eine Funktions-App auswählen. Sie erkennen eine Funktions-App am Symbol eines Blitzes zwischen spitzen Klammern.  
![Symbol für Funktion](../images/5-function-icon.png)

Wenn Sie zum ersten Mal eine Azure-Funktion hinzufügen, wird Ihnen ein Bildschirm für den Schnellstart angezeigt. Auf diesem Bildschirm können Sie den gewünschten Triggertyp und die gewünschte Programmiersprache auswählen. Azure erstellt dann basierend auf Ihrer Auswahl den Funktionscode und die Konfiguration für Sie.  
![Schnellstart für Funktion](../images/5-quickstart-form.png)

### <a name="function-templates"></a>Funktionsvorlagen
Die Auswahl von Vorlagen ist nicht auf diejenigen beschränkt, die im Schnellstart verfügbar sind. Sie können aus über 30 verschiedenen Vorlagen auswählen. Sie können auf den Bildschirm mit der Vorlagenliste zugreifen, während Sie weitere Funktionen erstellen oder indem Sie auf dem Schnellstartbildschirm die Option **Benutzerdefinierte Funktion** auswählen.  
![Funktionsvorlagen](../images/5-template-list.png)

## <a name="navigating-to-your-function-and-files"></a>Navigieren zu Ihrer Funktion und Ihren Dateien
Nachdem Sie eine Funktion aus einer Vorlage erstellt haben, werden mehrere Dateien generiert. Ein Beispiel: Sie haben ausgewählt, dass die Schnellstartvorlage für Webhook + API sowie JavaScript verwendet werden sollen. Bei den generierten Dateien handelt es sich um eine Konfigurationsdatei, **function.json** und eine Quellcodedatei, **index.js**. Beim Zugriff auf die Funktions-App wird Ihnen eine Menüstruktur mit den Funktionen angezeigt, die in der App erstellt wurden. In diesem Menüelement **Funktionen** können Sie der Funktions-App weitere Funktionen hinzufügen (beim Zeigen auf das Menüelement wird ein Pluszeichen angezeigt).  
![Schaltfläche „Funktion hinzufügen“](../images/5-function-add-button.png) 

Wenn Sie im Fall der oben erwähnten Schnellstartvorlage das Element **Funktionen** in der Strukturansicht erweitern, wird eine Funktion mit dem Standardnamen **HttpTriggerJS1** angezeigt (auch durch das f-Symbol für Funktion angegeben). Durch Auswahl dieser Funktion wird ein Codefenster mit der Quelldatei **index.js** geöffnet. Auf der rechten Seite des Codefensters befindet sich ein Flyoutmenü mit einer Registerkarte namens **Dateien anzeigen**. Durch Auswahl dieser Registerkarte wird die Dateistruktur (nachgebildet im Speicher) angezeigt, die Ihre Funktion bildet.  
![Funktionsvorlagen](../images/5-file-navigation.png)

## <a name="execution-options-for-testing-your-azure-function"></a>Ausführungsoptionen zum Testen Ihrer Azure-Funktion
Sobald Sie eine Azure-Funktion erstellt haben, müssen Sie wissen, wie Sie diese testen. Es gibt verschiedene Verfahren dafür: manuelles Ausführen und Testen im Azure-Portal selbst.

### <a name="manual-execution-of-a-function"></a>Manuelle Ausführung einer Funktion
Sie können die Ausführung einer Funktion initiieren, indem Sie den konfigurierten Trigger manuell auslösen. Wenn Sie z.B. einen HttpTrigger verwenden, können Sie ein Tool wie Postman oder cURL verwenden, um eine HTTP-Anforderung an Ihrem Funktionsendpunkt-URL zu initiieren.  
![Postman-Ausführung einer Funktion](../images/5-postman-execution.png): Sie können die Endpunkt-URL abrufen, indem Sie im linken Navigationsbereich Ihren HTTP-Trigger auswählen und dann auf die Schaltfläche **Funktions-URL abrufen** klicken.  
![Abrufen der Funktions-URL](../images/5-get-function-url.png)

### <a name="testing-a-function-in-the-azure-portal"></a>Testen einer Funktion im Azure-Portal
Auch das Azure-Portal bietet eine praktische Möglichkeit, Ihre Funktionen zu testen. Auf der rechten Seite des Codefensters finden Sie ein Flyoutmenü mit Registerkartennavigation. Dieses Menü enthält ein Element **Test**. Das Erweitern des Menüs und Auswählen dieser Registerkarte ist eine weitere Möglichkeit, Ihre Funktion auszuführen und das Ergebnis anzuzeigen. Wie im HttpTrigger-Szenario können Sie die HTTP-Methode festlegen und der Anforderung Parameter für die Abfragezeichenfolge sowie HTTP-Header hinzufügen. Sie können auch den Anforderungstext ändern, um weitere Szenarien zu testen. Im Ausgabefenster wird das Ergebnis der Funktion angezeigt.  
![Ausführung einer Funktion im Portal](../images/5-portal-execution.png)

## <a name="monitoring-an-azure-function"></a>Überwachen einer Azure-Funktion
Bei der Entwicklung von Azure-Funktionen ist es sehr wichtig, dass Sie Meldungen protokollieren und Ausnahmeszenarien bestimmen können, um sicherzustellen, dass Ihre Funktionen Produktionsreife erreichen. In einem Produktionsszenario ist dies ebenso wichtig, um die Ursache für einen Fehler zu finden. Auf der Benutzeroberfläche des Azure-Portals finden Sie ein Überwachungsdashboard und die Möglichkeit, Ausführungsprotokolle sowie Ausnahmen zu überprüfen, die von Ihren Azure-Funktionen empfangen wurden.

### <a name="monitoring-dashboard"></a>Überwachungsdashboard
Wenn Sie im Navigationsmenü der Funktions-App den Funktionsknoten erweitern, sehen Sie ein Menüelement **Monitor**. Das Überwachungsdashboard bietet eine schnelle Möglichkeit, den Verlauf von Funktionsausführungen anzuzeigen. Diese Ansicht zeigt den Zeitstempel, den Ergebniscode, die Dauer und die Vorgangs-ID und zeigt ebenfalls an, ob die Ausführung erfolgreich abgeschlossen wurde. Die Daten werden über Azure Application Insights aufgefüllt.  
![Funktionsmonitor](../images/5-monitor-function.png)

### <a name="log-window"></a>Protokollfenster
Sie können Ihrer Funktion auch Protokollanweisungen hinzufügen. Diese Anweisungen werden im Protokollfenster der Funktion angezeigt. Sie finden das Protokollfenster in einem Flyoutmenü mit Registerkarten, das sich am unteren Rand des Codefensters befindet. Wenn Sie eine JavaScript-basierte Funktion verwenden, fügen Sie eine Protokollanweisung mit der folgenden Syntax hinzu:
```javascript
  context.log('Enter your logging statement here');
```  
![Protokollfenster](../images/5-log-window.png)

### <a name="errors-and-warnings-window"></a>Fenster mit Fehlern und Warnungen
Sie finden die Registerkarte für das Fenster mit Fehlern und Warnungen im gleichen Flyoutmenü wie das Protokollfenster. Dieser Fehler zeigt Kompilierungsfehler und -warnungen innerhalb Ihres Codes. Da JavaScript eine dynamische und interpretierte Sprache ist, zeigt die folgende Abbildung einen Kompilierungsfehler in einer C#-Funktion.  
![Fenster mit Fehlern und Warnungen](../images/5-errors-window.png)
