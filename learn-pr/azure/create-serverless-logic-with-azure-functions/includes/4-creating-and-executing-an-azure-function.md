Nachdem Sie die Funktions-App erstellt haben, lassen Sie uns einen Blick darauf werfen, wie eine Azure-Funktion erstellt, konfiguriert und ausgeführt wird.

### <a name="triggers"></a>Trigger

Funktionen sind ereignisgesteuert, d.h., sie werden als Reaktion auf ein Ereignis ausgeführt.

Die Art von Ereignis, die die Funktion startet, wird als *Trigger* bezeichnet. Sie müssen eine Funktion mit genau einem Trigger konfigurieren.

Azure unterstützt Trigger für die folgenden Dienste.

| Dienst                 | Beschreibung des Triggers  |
|-------------------------|---------|
| Blob Storage            | Startet eine Funktion, wenn ein neues oder aktualisiertes Blob erkannt wird.       |
| Cosmos DB               | Startet eine Funktion, wenn Einfügungen und Aktualisierungen erkannt werden.      |
| Event Grid              | Startet eine Funktion, wenn ein Ereignis von Event Grid empfangen wird.       |
| HTTP                    | Startet eine Funktion mit einer HTTP-Anforderung.      |
| Microsoft Graph-Ereignisse  | Startet eine Funktion als Reaktion auf einen von Microsoft Graph eingehenden Webhook. Jede Instanz dieses Triggers kann auf einen Microsoft Graph-Ressourcentyp reagieren.       |
| Queue Storage           | Startet eine Funktion, wenn ein neues Element in einer Warteschlange eingeht. Die Warteschlangennachricht wird als Eingabe für die Funktion bereitgestellt.      |
| Service Bus             | Startet eine Funktion als Reaktion auf Nachrichten aus einer Service Bus-Warteschlange.       |
| Timer                   | Startet eine Funktion gemäß einem Zeitplan.       |
| Webhooks                | Startet eine Funktion mit einer Webhookanforderung.       |

### <a name="bindings"></a>Bindungen

Bindungen sind eine deklarative Möglichkeit, Daten und Dienste mit Ihrer Funktion zu verbinden. Bindungen sind in der Lage, mit verschiedenen Diensten zu kommunizieren. Das bedeutet, dass Sie keinen Code in Ihrer Funktion schreiben müssen, um sich mit Datenquellen zu verbinden und Verbindungen zu verwalten. Die Plattform nimmt Ihnen diese komplexen Aufgaben als Teil des Bindungscodes ab. Jede Bindung hat eine Richtung. Ihr Code liest Daten aus *Eingabe*bindungen und schreibt Daten in *Ausgabe*bindungen. Jede Funktion kann null oder mehr Bindungen haben, um die von der Funktion verarbeiteten Ein- und Ausgabedaten zu verwalten.

> [!NOTE]
> Technisch gesehen ist ein Trigger eine spezielle Art von Eingabebindung, die zusätzlich die Möglichkeit bietet, die Ausführung einzuleiten.

Azure bietet eine [große Anzahl von Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings) zum Herstellen von Verbindungen mit anderen Speicher- und Messagingdiensten.

### <a name="a-sample-binding-definition"></a>Beispieldefinition einer Bindung

Sehen wir uns ein Beispiel zum Konfigurieren einer Funktion mit einer Eingabebindung (Trigger) und einer Ausgabebindung an. Angenommen, wir möchten Daten aus Blob Storage lesen, sie in unserer Funktion verarbeiten und dann eine Nachricht in eine Warteschlange schreiben. Konfigurieren Sie eine _Eingabebindung_ des Typs *Blob* und eine _Ausgabebindung_ des Typs *Warteschlange*.

Bindungen können im Azure-Portal definiert werden und werden als JSON-Dateien gespeichert, die Sie auch direkt bearbeiten können. Der folgende JSON-Code ist eine Beispieldefinition eines Triggers und einer Bindung für eine Funktion.

```json
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

Dieses Beispiel zeigt eine Funktion, die durch eine Nachricht ausgelöst wird, die der Warteschlange namens **myqueue-items** hinzugefügt wird. Danach wird der Rückgabewert der Funktion an die Tabelle **outTable** in Azure Table Storage gesendet. Dies ist ein sehr einfaches Beispiel. Wir könnten die Ausgabe mithilfe einer SendGrid-Bindung in eine E-Mail umwandeln. Oder wir könnten ein Ereignis in einer Service Bus-Instanz ablegen, um eine andere Komponente in unserer Architektur zu benachrichtigen, oder sogar mehrere Ausgabebindungen einrichten, um Daten an verschiedene Dienste weiterzuleiten.

## <a name="creating-a-function-in-the-azure-portal"></a>Erstellen einer Funktion im Azure-Portal

Azure bietet für gängige Szenarien mehrere vorgefertigte Funktionsvorlagen.

### <a name="quickstart-templates"></a>Schnellstartvorlagen

Wenn Sie zum ersten Mal eine Funktion hinzufügen, wird Ihnen ein Bildschirm für den Schnellstart angezeigt. Auf diesem Bildschirm können Sie einen Triggertyp (HTTP, Timer oder Daten) und die Programmiersprache (C#, JavaScript, F# oder Java) auswählen. Auf der Grundlage Ihrer Auswahl generiert Azure anschließend den Funktionscode und die Konfiguration für Sie mit einem Beispielcode, um die im Protokoll empfangenen Eingabedaten anzuzeigen. 
 
### <a name="custom-function-templates"></a>Benutzerdefinierte Funktionsvorlagen

Die Auswahl von Schnellstartvorlagen ermöglicht einen einfachen Zugriff auf die gängigsten Szenarien. Azure bietet jedoch mehr als 30 zusätzliche Vorlagen, mit denen Sie loslegen können. Diese können auf dem Bildschirm mit der Vorlagenliste ausgewählt werden, während Sie weitere Funktionen erstellen oder indem Sie auf dem Schnellstartbildschirm die Option **Benutzerdefinierte Funktion** auswählen.

- HTTP-Trigger mit C#, F# oder JavaScript
- Timertrigger mit C#, F# oder JavaScript
- Warteschlangentrigger mit C#, F# oder JavaScript
- Service Bus-Warteschlangentrigger mit C#, F# oder JavaScript
- Cosmos DB-Trigger mit C# oder JavaScript
- IoT Hub (Event Hub) mit C#, F# oder JavaScript
- ... und viele mehr

## <a name="navigating-to-your-function-and-files"></a>Navigieren zu Ihrer Funktion und Ihren Dateien

Nachdem Sie eine Funktion anhand einer Vorlage erstellt haben, werden mehrere Dateien generiert. Wenn Sie z.B. den Schnellstart „Webhook + API“ mit JavaScript gewählt haben, sind die generierten Dateien eine Konfigurationsdatei, **function.json**, und eine Quellcodedatei, **index.js**. Die Funktionen, die Sie in einer Funktions-App erstellen, werden im Portal für Funktions-Apps unter dem Menüpunkt **Funktionen** angezeigt.

Wenn Sie eine Funktion in Ihrer Funktions-App auswählen, wird ein Code-Editor geöffnet, in dem der Code für Ihre Funktion angezeigt wird, wie im folgenden Screenshot dargestellt.

![Benutzeroberfläche zur Auswahl von Funktionsvorlagen mit einer Liste von Vorlagen, mit denen Sie die Funktionsentwicklung beschleunigen können.](../media-draft/4-file-navigation.png)

Wie Sie im vorherigen Screenshot sehen können, gibt es auf der rechten Seite ein Flyoutmenü, das die Registerkarte **Dateien anzeigen** enthält. Wenn Sie diese Registerkarte auswählen, wird die Dateistruktur angezeigt, aus der sich Ihre Funktion zusammensetzt.  

## <a name="testing-your-azure-function"></a>Testen der Azure-Funktion

Nachdem Sie eine Funktion erstellt haben, sollten Sie es testen. Es gibt verschiedene Verfahren dafür: manuelles Ausführen und Testen im Azure-Portal selbst.

### <a name="manual-execution"></a>Manuelle Ausführung

Sie können eine Funktion starten, indem Sie den konfigurierten Trigger manuell auslösen. Wenn Sie z.B. einen HTTP-Trigger verwenden, können Sie ein Tool wie Postman oder cURL einsetzen, um eine HTTP-Anforderung an die URL Ihres Funktionsendpunkts auszulösen, die in der Definition des HTTP-Triggers verfügbar ist (**Funktions-URL abrufen**).  

### <a name="testing-in-the-azure-portal"></a>Testen im Azure-Portal

Das Azure-Portal bietet auch eine praktische Möglichkeit, Ihre Funktionen zu testen. Auf der rechten Seite des Codefensters finden Sie ein Flyoutmenü mit Registerkartennavigation. Dieses Menü enthält ein Element **Test**. Das Erweitern des Menüs und Auswählen dieser Registerkarte ist eine weitere Möglichkeit, Ihre Funktion auszuführen und das Ergebnis anzuzeigen. Wenn Sie in diesem Testfenster auf **Ausführen** klicken, werden die Ergebnisse zusammen mit einem Statuscode im Ausgabefenster angezeigt. 

## <a name="monitoring-dashboard"></a>Überwachungsdashboard

Die Fähigkeit, Ihre Funktionen zu überwachen, ist während der Entwicklung und in der Produktion unerlässlich. Das Azure-Portal bietet ein Überwachungsdashboard, wenn Sie die Application Insights-Integration aktivieren. Wenn Sie im Navigationsmenü der Funktions-App den Funktionsknoten erweitern, sehen Sie das Menüelement **Monitor**. Dieses Dashboard „Monitor“ bietet eine schnelle Möglichkeit, den Verlauf der Funktionsausführungen anzuzeigen, und zeigt den Zeitstempel, den Ergebniscode, die Dauer und die Vorgangs-ID, die von Application Insights aufgefüllt werden.

![Screenshot des Dashboards „Monitor“, das über den Funktionsmenüpunkt „Monitor“ gestartet wurde und eine Liste der erfolgreichen und fehlgeschlagenen Aufrufe der Funktion zeigt.](../media-draft/4-monitor-function.png)

## <a name="streaming-log-window"></a>Fenster mit dem Streamingprotokoll

Zu Debugzwecken können Sie Ihrer Funktion im Azure-Portal auch Protokollierungsanweisungen hinzufügen. Die aufgerufenen Methoden für jede Sprache werden mit einem Protokollierungsobjekt übergeben, das verwendet werden kann, um Informationen im Protokollfenster zu protokollieren. Dieses befindet sich in einem Flyoutmenü mit Registerkarten am unteren Rand des Codefensters. 

Der folgende JavaScript-Codeausschnitt zeigt, wie eine Nachricht mit der `context.log`-Methode protokolliert wird (das `context`-Objekt wird an den Ereignishandler übergeben).

```javascript
  context.log('Enter your logging statement here');
```  

In C# ist dasselbe mit der `log.Info`-Methode möglich. In diesem Fall wird das `log`-Objekt an die C#-Methode übergeben, die die Funktion verarbeitet.

```csharp
  log.Info("Enter your logging statement here");
```

### <a name="errors-and-warnings-window"></a>Fenster „Fehlern und Warnungen“

Sie finden die Registerkarte für das Fenster mit Fehlern und Warnungen im gleichen Flyoutmenü wie das Protokollfenster. Dieses Fenster zeigt Kompilierungsfehler und -warnungen innerhalb Ihres Codes.

