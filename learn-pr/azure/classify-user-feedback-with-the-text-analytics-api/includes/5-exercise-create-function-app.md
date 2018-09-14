 Eine Funktions-app stellt einen Kontext für die Verwaltung und Ausführung Ihrer Funktionen bereit. Wir erstellen eine Funktionen-app, und fügen Sie eine Funktion hinzu. 

## <a name="create-a-function-app-to-host-our-function"></a>Erstellen einer Funktionen-App zum Hosten unserer-Funktion

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

1. Wählen Sie die **erstellen Sie eine Ressource** Schaltfläche finden Sie auf der linken oberen Ecke des Azure-Portal, klicken Sie dann auf **Compute** > **Funktions-App**.

1. Geben Sie die Einstellungen der Funktionen-app wie in der folgenden Tabelle angegeben.

    | Einstellung      | Empfohlener Wert  | Beschreibung                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **App-Name** | Global eindeutiger Name | Der Name, der Ihre neue Funktionen-App bezeichnet Gültige Zeichen sind `a-z`, `0-9` und `-`.  | 
    | **Abonnement** | Ihr Abonnement | Das Abonnement, unter dem diese neue Funktions-App erstellt wird. | 
    | **Ressourcengruppe**|  <rgn>[Sandkasten Resource Group-Name]</rgn> | Der Name für die Ressourcengruppe, in dem Sie Ihre Funktionen-app zu erstellen.<br/><br/>Stellen Sie sicher, dass **vorhandene** und die Ressourcengruppe aus der letzten Übung verwenden. Auf diese Weise alle Ressourcen, die wir in diesem Modul vorgenommen werden zusammengehalten. | 
    | **Betriebssystem** | Windows | Das Betriebssystem, das die Funktionen-app hostet.  |
    | **Hosting** |   Verbrauchsplan | Der Hostingplan, der definiert, wie Ihre Ressourcen der Funktionen-App zugewiesen werden Im **Standard-Verbrauchstarif** werden Ressourcen je nach Bedarf der Funktionen dynamisch hinzugefügt. Beim [serverlosen Hosting](https://azure.microsoft.com/overview/serverless-computing/) bezahlen Sie nur die Zeit, in der Ihre Funktionen ausgeführt werden.   |
    | **Standort** | Wählen Sie aus der Liste | Wählen Sie eine [Region](https://azure.microsoft.com/regions/) in Ihrer Nähe oder in der Nähe von anderen Diensten aus, auf die Ihre Funktionen zugreifen.<br/><br/>Wählen Sie die Region, die Sie beim Erstellen der Textanalyse-API-Konto in der letzten Übung verwendet. |
    | **Speicherkonto** |  Global eindeutiger Name |  Der Name des neuen Speicherkontos, das von Ihrer Funktionen-App verwendet wird. Speicherkontonamen müssen zwischen 3 und 24 Zeichen lang sein und dürfen nur Zahlen und Kleinbuchstaben enthalten. Dieses Dialogfeld füllt das Feld mit einem eindeutigen Namen, die nicht mit dem Namen abgeleitet wird Sie die app zugewiesen haben. Allerdings können auch einen anderen Namen oder sogar ein vorhandenes Konto verwenden. |

1. Klicken Sie auf **Erstellen**, um die Funktionen-App bereitzustellen.

1. Wählen Sie das Benachrichtigungssymbol in der oberen rechten Ecke des Portals, und sehen Sie sich für eine **Bereitstellung** Meldung ähnlich der folgenden Meldung.

1. Bereitstellung kann einige Zeit dauern. Also im Notification Hub bleiben, und sehen Sie sich für eine **Bereitstellung erfolgreich** Meldung ähnlich der folgenden angezeigt.

1. Herzlichen Glückwunsch! Sie haben erstellt und Ihrer Funktionen-app bereitgestellt. Wählen Sie **Zu Ressource wechseln**, um Ihre neue Funktionen-App anzuzeigen.

> [!TIP]
> Sollten Sie Ihre Funktions-Apps im Portal nicht finden, können Sie [Funktionen-Apps Ihren Favoriten im Azure-Portal hinzufügen](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite).

## <a name="create-a-function-to-execute-our-logic"></a>Erstellen Sie eine Funktion, um unsere Logik ausführen

Nun, da wir eine Funktions-app haben, ist es Zeit, eine Funktion zu erstellen. Eine Funktion wird durch einen Trigger aktiviert. In diesem Modul werden wir einen warteschlangentrigger verwenden. Die Laufzeit wird eine Warteschlange abrufen und starten dieser Funktion können Sie eine neue Nachricht zu verarbeiten.

1. Erweitern Sie Ihre neue Funktions-app und dann auf die **Funktionen** Auflistung. Aktivieren Sie das Hinzufügen (__+__) Wenn sie angezeigt wird der Prozess der Funktion zu starten.

1. In der **schneller Einstieg** wählen Sie die Seite angezeigt wird, die jetzt und **benutzerdefinierte Funktion**, lädt die Liste der verfügbaren Vorlagen.

1. Wählen Sie **JavaScript** auf die **warteschlangentrigger** Eintrag in der Vorlage.

![Screenshot des Azure Functions-Vorlagen mit JavaScript, die auf den Eintrag der Datenwarteschlange Trigger ausgewählt haben.](../media/quickstart-select-queue-trigger.png)

4. In der **neue Funktion** angezeigten Dialogfeld die folgenden Werte eingeben.

|Eigenschaft  |Wert  |
|---------|---------|
|Sprache     |   **JavaScript**      |
|Name     |   **discover-sentiment-function**      |
|Warteschlangenname     |   **new-feedback-q**      |
|Speicherkontoverbindung        |  **AzureWebJobsDashboard**       |

![Screenshot des Azure Functions-Vorlagen mit JavaScript, die auf den Eintrag der Datenwarteschlange Trigger ausgewählt haben.](../media/new-function-dialog.png)

5. Wählen Sie **erstellen** mit der Funktion Erstellung beginnen.

1. Eine Funktion ist in Ihrer gewählten Sprache, die mithilfe der Vorlage der Warteschlangentrigger-Funktion erstellt. Während wir die Funktion in JavaScript in diesem Modul implementieren müssen, können Sie eine Funktion erstellen, in einem [unterstützte Sprache](https://docs.microsoft.com/azure/azure-functions/supported-languages).

Wenn der Erstellungsvorgang abgeschlossen ist, Code-Editor wird geöffnet, in das Portal und lädt die *"Index.js"* Seite. Diese Datei ist die Codedatei, in dem wir unsere Funktionslogik schreiben.

## <a name="try-it-out"></a>Ausprobieren

Testen Sie nun, was wir bisher haben. Wir noch nicht geschrieben werden, dass jeder Code, damit dieser Test ist, um sicherzustellen, was wir bisher konfiguriert haben ausgeführt wird.

1. Klicken Sie auf **ausführen** am oberen Rand der Code-Editor.

1. Beachten Sie die **Protokolle** Registerkarte, die am unteren Rand des Bildschirms geöffnet wird. Wenn alles funktioniert wie vorgesehen, sehen Sie eine Meldung ähnlich der folgenden angezeigt.
    ![Screenshot der Response-Nachricht von einem erfolgreichen Aufruf unsere-Funktion.](../media/func-default-run.PNG)

Die **ausführen** Schaltfläche unserer Funktion gestartet, und übergeben *Warteschlange Beispieldaten*, den Standardtext aus der **Test** Fenster für die Steuerungsanforderung, unsere-Funktion.

Gut gemacht! Sie haben erfolgreich eine Warteschlange ausgelöste Funktion zu Ihrer Funktions-app hinzugefügt und getestet werden, um sicherzustellen, dass es wie erwartet funktioniert. Wir fügen weitere Funktionen für die Funktion in der nächsten Übung.

Wir betrachten kurz die Funktion der anderen Datei die *"Function.JSON"* Config-Datei. Die Konfigurationsdaten aus dieser Datei werden angezeigt, in der folgenden JSON-Liste.

```json
{
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "new-feedback-q",
      "connection": "AzureWebJobsDashboard"
    }
  ],
  "disabled": false
}
```

Wie Sie sehen können, wird diese Funktion weist eine triggerbindung mit dem Namen **MyQueueItem** des Typs `queueTrigger`. Wenn eine neue Nachricht in der Warteschlange eingeht, wir haben mit dem Namen **Feedback-Q**, unsere-Funktion wird aufgerufen. Wir verweisen auf die neue Nachricht über den MyQueueItem gebundenen Parameter. Bindungen wirklich Teil der Arbeit für uns erledigt!

Im nächsten Schritt fügen wir Code zum Aufrufen des Textanalyse-API-Diensts.

> [!TIP]
> Sie können die Datei "Index.js" und "Function.JSON" anzeigen, indem Sie erweitern die **Ansichtsdateien** im Menü auf der rechten Seite des Panels Funktion im Azure-Portal.

In dieser Übung wurde zu unserer Azure Functions-Infrastruktur vorhanden. Wir haben eine funktionierende-Funktion, gehostet in einer Funktionen-app, die ausgeführt wird, wenn eine neue Nachricht in unserer Warteschlange eingeht, die wir mit dem Namen haben [!INCLUDE [input-q](./q-name-input.md)]. Der Spaß beginnt in der nächsten Übung, wenn wir Code zum Aufrufen einer Microsoft Cognitive Services dazu stimmungsanalysen hinzufügen.