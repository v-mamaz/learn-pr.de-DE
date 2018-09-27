 Eine Funktions-App stellt einen Kontext für die Verwaltung und Ausführung Ihrer Funktionen bereit. Erstellen Sie nun eine Funktions-App, und fügen Sie eine Funktion hinzu.

## <a name="create-a-function-app-to-host-our-function"></a>Erstellen einer Funktions-App zum Hosten der Funktion

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.

1. Klicken Sie in der linken oberen Ecke des Azure-Portals auf die Schaltfläche **Ressource erstellen** und dann auf **Compute** > **Funktions-App**.

1. Geben Sie die Einstellungen für die Funktions-App in die folgende Tabelle ein.

    | Einstellung      | Wert  | Beschreibung                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **App-Name** | Global eindeutiger Name | Der Name Ihrer neuen Funktions-App. Gültige Zeichen sind `a-z`, `0-9` und `-`.  |
    | **Abonnement** | **Concierge-Abonnement** | Das Abonnement, unter dem diese neue Funktions-App erstellt wird. |
    | **Ressourcengruppe**|  **<rgn>[Name der Sandboxressourcengruppe]</rgn>** | Der Name der Ressourcengruppe, in der die Funktions-App erstellt wird.<br/><br/>Achten Sie darauf, die Option **Vorhandene verwenden** auszuwählen und die Ressourcengruppe aus der letzten Übung zu verwenden. Auf diese Weise bleiben alle Ressourcen zusammen, die in diesem Modul erstellt wurden. |
    | **Betriebssystem** | Windows | Das Betriebssystem, das die Funktions-App hostet.  |
    | **Hosting** |   Verbrauchsplan | Der Hostingplan, der definiert, wie Ihre Ressourcen der Funktionen-App zugewiesen werden Im **Standard-Verbrauchstarif** werden Ressourcen je nach Bedarf der Funktionen dynamisch hinzugefügt. Beim [serverlosen Hosting](https://azure.microsoft.com/overview/serverless-computing/) bezahlen Sie nur die Zeit, in der Ihre Funktionen ausgeführt werden.   |
    | **Speicherort** | Wählen Sie den gleichen Standort wie zuvor aus. | Wählen Sie eine Region in Ihrer Nähe oder in der Nähe von anderen Diensten aus, auf die Ihre Funktionen zugreifen.<br/><br/>Wählen Sie dieselbe Region aus, die Sie in der letzten Übung beim Erstellen des Textanalyse-API-Kontos verwendet haben. |
    | **Speicherkonto** |  Global eindeutiger Name |  Der Name des neuen Speicherkontos, das von Ihrer Funktions-App verwendet wird. Speicherkontonamen müssen zwischen 3 und 24 Zeichen lang sein und dürfen nur Zahlen und Kleinbuchstaben enthalten. In diesem Dialogfeld wird das Feld automatisch mit einem eindeutigen Namen gefüllt, der aus dem Namen abgeleitet wird, den Sie der App gegeben haben. Sie können aber auch einen anderen Namen oder sogar ein vorhandenes Konto verwenden. |

1. Klicken Sie auf **Erstellen**, um die Funktions-App bereitzustellen.

1. Wählen Sie oben rechts im Portal das Benachrichtigungssymbol aus, und achten Sie auf eine Meldung des Typs **Deployment in progress** (Bereitstellung wird ausgeführt).

1. Die Bereitstellung kann einige Zeit in Anspruch nehmen. Bleiben Sie daher im Notification Hub, und warten Sie auf eine Meldung vom Typ **Bereitstellung erfolgreich**.

1. Sobald die Funktions-App bereitgestellt ist, wechseln Sie im Portal zu **Alle Ressourcen**. Die Funktions-App wird mit dem Typ **App Service** aufgelistet und hat den Namen, den Sie ihr gegeben haben. Wählen Sie die Funktions-App in der Liste aus, um sie zu öffnen.

    Herzlichen Glückwunsch! Sie haben Ihre Funktions-App erstellt und bereitgestellt.

> [!TIP]
> Können Sie Ihre Funktions-App nicht im Portal finden? Versuchen Sie, [die Funktions-Apps zu Ihren Favoriten im Azure-Portal hinzuzufügen](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite).

## <a name="create-a-function-to-execute-our-logic"></a>Erstellen einer Funktion zum Ausführen der Logik

Da Sie nun über eine Funktions-App verfügen, ist es an der Zeit, eine Funktion zu erstellen. Eine Funktion wird durch einen Trigger aktiviert. In diesem Modul verwenden Sie einen Warteschlangentrigger. Die Runtime fragt eine Warteschlange ab und startet diese Funktion, um eine neue Nachricht zu verarbeiten.

1. Erweitern Sie Ihre neue Funktions-App, und bewegen Sie den Mauszeiger dann auf die Sammlung **Funktionen**. Klicken Sie auf die Schaltfläche „Hinzufügen“ (__+__), wenn sie angezeigt wird, um die Erstellung der Funktion zu starten.

1. Klicken Sie auf der Seite **Get started quickly** (Schneller Einstieg), die angezeigt wird, unten auf die Option **Benutzerdefinierte Funktion**, mit der die Liste mit den verfügbaren Funktionsvorlagen geladen wird.

1. Wählen Sie unter dem Eintrag **Warteschlangentrigger** der Vorlagenliste die Option **JavaScript** aus.

    ![Screenshot: Azure Functions-Vorlagen mit Auswahl von JavaScript unter dem Eintrag „Warteschlangentrigger“](../media/quickstart-select-queue-trigger.png)

4. Geben Sie im angezeigten Dialogfeld **Neue Funktion** die folgenden Werte ein.

    |Eigenschaft  |Wert  |
    |---------|---------|
    |Sprache     |   **JavaScript**      |
    |Name     |   **discover-sentiment-function**      |
    |Warteschlangenname     |   **new-feedback-q**      |
    |Speicherkontoverbindung        |  **AzureWebJobsDashboard**       |

5. Klicken Sie auf **Erstellen**, um mit dem Prozess zum Erstellen von Funktionen zu beginnen.

1. Mit der Warteschlangentrigger-Funktionsvorlage wird eine Funktion in der ausgewählten Sprache erstellt. In diesem Modul implementieren wir die Funktion in JavaScript, aber Sie können in jeder [unterstützten Sprache](https://docs.microsoft.com/azure/azure-functions/supported-languages) eine Funktion erstellen.

Wenn der Erstellungsvorgang abgeschlossen ist, wird im Portal der Code-Editor geöffnet und die Seite *index.js* geladen. Diese Datei ist die Codedatei, in der wir unsere Funktionslogik schreiben.

## <a name="try-it-out"></a>Testen

Wir testen jetzt den bisherigen Stand. Da wir noch keinen Code geschrieben haben, soll mit diesem Test sichergestellt werden, dass die Ausführung der bisher konfigurierten Komponenten funktioniert.

1. Klicken Sie oben im Code-Editor auf **Ausführen**.

1. Beachten Sie die Registerkarte **Protokolle**, die unten auf dem Bildschirm geöffnet wird. Wenn alles wie geplant funktioniert, wird in etwa die folgende Nachricht angezeigt.
    ![Screenshot: Antwortnachricht für einen erfolgreichen Aufruf Ihrer Funktion](../media/func-default-run.PNG)

    Über die Schaltfläche **Ausführen** wird unsere Funktion gestartet, und die *Beispielwarteschlangendaten* (Standardtext aus dem **Test**-Anforderungsfenster) werden an unsere Funktion übergeben.

Gut gemacht! Sie haben Ihrer Funktions-App erfolgreich eine per Warteschlange ausgelöste Funktion hinzugefügt und sie getestet, um sicherzustellen, dass alles wie erwartet funktioniert. Wir fügen der Funktion in der nächsten Übung weitere Funktionalität hinzu.

Schauen Sie sich kurz die andere Datei der Funktion an (Konfigurationsdatei *function.json*). Die Konfigurationsdaten aus dieser Datei sind in der folgenden JSON-Liste aufgeführt.

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

Wie Sie sehen, verfügt diese Funktion über eine Triggerbindung mit dem Namen **myQueueItem** vom Typ `queueTrigger`. Wenn in der Warteschlange eine neue Nachricht eingeht, der wir den Namen **new-feedback-q** gegeben haben, wird unsere Funktion aufgerufen. Wir verweisen über den Bindungsparameter myQueueItem auf die neue Nachricht. Bindungen erledigen wirklich einen Großteil der harten Arbeit für uns.

Im nächsten Schritt fügen wir Code zum Aufrufen des Textanalyse-API-Diensts hinzu.

> [!TIP]
> Sie können die Dateien „index.js“ und „function.json“ anzeigen, indem Sie auf der rechten Seite des Funktionspanels im Azure-Portal das Menü **Dateien anzeigen** erweitern.

In dieser Übung ging es darum, die Azure Functions-Infrastruktur einzurichten. Wir verfügen über eine funktionierende Funktion, die in einer Funktions-App gehostet wird. Sie wird ausgeführt, wenn eine neue Nachricht in der Warteschlange eintrifft, der wir den Namen [!INCLUDE [input-q](./q-name-input.md)] gegeben haben. Richtig spannend wird es in der nächsten Übung, wenn wir Code zum Aufrufen eines Azure Cognitive Services-Diensts hinzufügen, um eine Standpunktanalyse durchzuführen.