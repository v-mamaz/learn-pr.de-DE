Folgendes ist eine übersichtsdarstellung der wir werden uns in dieser Übung erstellen.

![Visuelle Darstellung der Standard-HTTP-Trigger, mit HTTP-Anforderung und Antwort sowie entsprechende Req und Res Bindungsparameter.](../media-draft/default-http-trigger-visual-small.PNG)

Wir erstellen eine Funktion, die gestartet wird, sobald er eine HTTP-Anforderung empfängt und durch Senden einer Nachricht für jede Anforderung reagiert. Die Parameter `req` und `res` werden die triggerbindung und ausgabebindung bzw. Legen wir los!

### <a name="create-a-function-app"></a>Erstellen einer Funktions-App

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

Erstellen wir eine Funktions-app, die wir in diesem gesamten Modul verwenden. Eine Funktion-app können Sie Funktionen zu einer logischen Einheit für die einfachere Verwaltung, Bereitstellung und Freigabe von Ressourcen gruppieren.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.
1. Wählen Sie die **erstellen Sie eine Ressource** Schaltfläche finden Sie auf der linken oberen Ecke des Azure-Portal, klicken Sie dann auf **Compute** > **Funktions-App**.
1. Legen Sie die Funktion-app-Eigenschaften wie folgt:

    | Eigenschaft      | Empfohlener Wert  | Beschreibung                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **App-Name** | Global eindeutiger Name | Der Name, der Ihre neue Funktionen-App bezeichnet Gültige Zeichen sind `a-z`, `0-9` und `-`.  | 
    | **Abonnement** | Ihr Abonnement | Das Abonnement, unter dem diese neue Funktions-App erstellt wird. | 
    | **Ressourcengruppe**|  Wählen Sie **vorhandene** , und wählen Sie <rgn>[Sandkasten Resource Group-Name]</rgn> | Name der Ressourcengruppe, in der die Funktions-App erstellt wird. | 
    | **Betriebssystem** | Windows | Das Betriebssystem, das die Funktionen-app hostet.  |
    | **Hosting** |   Verbrauchsplan | Der Hostingplan, der definiert, wie Ihre Ressourcen der Funktionen-App zugewiesen werden Im **Standard-Verbrauchstarif** werden Ressourcen je nach Bedarf der Funktionen dynamisch hinzugefügt. Beim [serverlosen Hosting](https://azure.microsoft.com/overview/serverless-computing/) bezahlen Sie nur die Zeit, in der Ihre Funktionen ausgeführt werden.   |
    | **Standort** | Wählen Sie aus der Liste | Wählen Sie eine [Region](https://azure.microsoft.com/regions/) in Ihrer Nähe oder in der Nähe von anderen Diensten aus, auf die Ihre Funktionen zugreifen. |
    | **Speicherkonto** |  Global eindeutiger Name |  Der Name des neuen Speicherkontos, das von Ihrer Funktionen-App verwendet wird. Speicherkontonamen müssen zwischen 3 und 24 Zeichen lang sein und dürfen nur Zahlen und Kleinbuchstaben enthalten. Dieses Dialogfeld füllt das Feld mit einem eindeutigen Namen, die nicht mit dem Namen abgeleitet wird Sie die app zugewiesen haben. Allerdings können auch einen anderen Namen oder sogar ein vorhandenes Konto verwenden. |


3. Klicken Sie auf **Erstellen**, um die Funktionen-App bereitzustellen.

4. Wählen Sie das Benachrichtigungssymbol in der oberen rechten Ecke des Portals, und sehen Sie sich für eine **Bereitstellung** Meldung ähnlich der folgenden Meldung.

![Benachrichtigung, die Bereitstellung der Funktionen-app ausgeführt wird](../media-draft/func-app-deploy-progress-small.PNG)

5. Bereitstellung kann einige Zeit dauern. Also im Notification Hub bleiben, und sehen Sie sich für eine **Bereitstellung erfolgreich** Meldung ähnlich der folgenden angezeigt.

![Benachrichtigung, die Funktion von app-Bereitstellung wurde abgeschlossen.](../media-draft/func-app-deploy-success-small.PNG)

6. Herzlichen Glückwunsch! Sie haben erstellt und Ihrer Funktionen-app bereitgestellt. Wählen Sie **Zu Ressource wechseln**, um Ihre neue Funktionen-App anzuzeigen.

>[!TIP]
>Wenn Sie Probleme beim Suchen Ihrer Funktionen-apps im Portal sind, erfahren Sie, wie Sie [Hinzufügen von Function Apps zu Ihren Favoriten im Portal](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite).

### <a name="create-a-function"></a>Erstellen einer Funktion

Nun, da wir eine Funktions-app haben, ist es Zeit, eine Funktion zu erstellen. Eine Funktion wird durch einen Trigger aktiviert. In diesem Modul verwenden wir einen HTTP-Trigger.

1. Erweitern Sie Ihre neue Funktionen-app, und klicken Sie dann zeigen Sie auf die Auflistung von Funktionen aus, und wählen Sie die hinzufügen (**+**) neben **Funktionen**. Diese Aktion wird der Prozess der Funktion gestartet. Die folgende Animation veranschaulicht dieses Aktion.

![Die Animation von dem Pluszeichen (+) angezeigt wird, wenn der Benutzer auf das Menüelement Funktionen zeigt.](../media-draft/func-app-plus-hover-small.gif)

2. In der **schneller Einstieg** Seite **WebHook + API**, wählen Sie eine Sprache für Ihre Funktion aus, und klicken Sie auf **diese Funktion erstellen**.

3. Eine Funktion wird in Ihrer gewählten Sprache anhand der Vorlage für eine Funktion mit Auslösung per HTTP erstellt. In dieser Übung erstellen wir eine JavaScript-Funktion.

### <a name="try-it-out"></a>Ausprobieren

Testen Sie nun, was wir haben bisher mit den folgenden Schritten:

1. Klicken Sie in der neuen Funktion rechts oben auf **</> Funktions-URL abrufen**, wählen Sie **default (Function key)** (Standard (Funktionsschlüssel)) aus, und klicken Sie dann auf **Kopieren**.

2. Fügen Sie die Funktions-URL, die Sie in der Adressleiste des Browsers kopiert haben. Fügen Sie den Wert der Abfragezeichenfolge `&name=<yourname>` am Ende der URL hinzu, und drücken Sie die Taste `Enter` auf Ihrer Tastatur, um die Anforderung auszuführen. Daraufhin sollte eine Ausgabe ähnlich der folgenden Antwort zurückgegeben, die von der Funktion, die in Ihrem Browser angezeigt.  

Gut gemacht! Sie haben jetzt eine per HTTP ausgelöste Funktion zu Ihrer Funktions-app hinzugefügt und getestet werden, um sicherzustellen, dass es wie erwartet funktioniert.

![Screenshot der Response-Nachricht von einem erfolgreichen Aufruf unsere-Funktion.](../media-draft/default-http-trigger-response-small.PNG)

Wie Sie aus dieser Übung bisher sehen können, müssen Sie einen Triggertyp wählen Sie beim Erstellen einer Funktion. Jede Funktion verfügt über ein, und nur ein Trigger. In diesem Beispiel verwenden wir einen HTTP-Trigger, was, dass unsere-Funktion wird gestartet bedeutet, wenn sie eine HTTP-Anforderung empfängt. Die Standardimplementierung, die im folgenden Screenshot in JavaScript dargestellt antwortet mit dem Wert eines Parameters *Namen* er in der Abfragezeichenfolge oder der Textkörper der Anforderung empfangen hat. Wenn keine Zeichenfolge angegeben wurde, antwortet die Funktion, mit einer Meldung gefragt, Personen aufgerufen wird, einen Namenswert angeben.

![Screenshot des Standard-JavaScript-Implementierung von Azure per HTTP ausgelöste Funktion.](../media-draft/default-http-trigger-implementation-small.PNG)

All dieser Code befindet sich in der *"Index.js"* -Datei im Ordner mit dieser Funktion. Wir betrachten kurz die Funktion der anderen Datei die *"Function.JSON"* Config-Datei. Diese Konfigurationsdaten werden angezeigt, in der folgenden JSON-Liste.

```json
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

Wie Sie sehen können, wird diese Funktion weist eine triggerbindung mit dem Namen **Req** des Typs `httpTrigger` und einer ausgabebindung, die mit dem Namen **Res** des Typs `HTTP`. Im vorangehenden Code für unsere Funktion erläutert, wie wir die Nutzlast des eingehenden HTTP-Anforderung über Zugriff auf unsere **Req** Parameter. Auf ähnliche Weise, wir eine HTTP-Antwort gesendet, einfach durch Festlegen von unserem **Res** Parameter. Bindungen wirklich Teil der Arbeit für uns erledigt!

>[!TIP]
>Sie können die Datei "Index.js" und "Function.JSON" anzeigen, indem Sie erweitern die **Ansichtsdateien** im Menü auf der rechten Seite des Panels Funktion im Azure-Portal.  

### <a name="explore-binding-types"></a>Erkunden Sie Bindungstypen

1. Beachten Sie, dass unter dem Eintrag für die Funktion, dass ein Satz von Menüelementen vorhanden ist, wie im folgenden Screenshot gezeigt.

![Screenshot der Menüelemente in einer Funktion in das Blatt "Funktionen-Apps".](../media-draft/func-menu-small.PNG)

2. Wählen Sie das Menüelement "Integrieren", öffnen Sie die Registerkarte "Integration" für unsere-Funktion. Wenn Sie zusammen mit dieser Einheit durchgearbeitet haben, sollte die Registerkarte "Integration" sehr ähnlich dem folgenden Bildschirmfoto aussehen.

![Screenshot der integrieren Benutzeroberfläche oder Registerkarte.](../media-draft/func-integrate-tab-small.PNG)

Beachten Sie, dass wir bereits einen Trigger und ausgabebindung definiert haben, wie in diesem Screenshot gezeigt. Sie können auch sehen, dass wir nicht mehr als einen Trigger hinzufügen. In der Tat zum Ändern des Triggers für unsere Funktion müssten wir zunächst löschen Sie den Trigger, und erstellen eine neue Ressourcengruppe.

Auf der anderen Seite der **Eingaben** und **Ausgaben** Teile dieses Formular zeigt ein Pluszeichen `+` anmelden, um weitere Bindungen hinzuzufügen.

3. Wählen Sie **+ neue Eingabe** unter der **Eingaben** Spalte. Eine Liste aller möglichen eingabebindung Typen wird angezeigt, wie im folgenden Screenshot gezeigt.

![Screenshot: Liste der möglichen eingabebindungen.](../media-draft/func-input-bindings-selector-small.PNG)

Nehmen Sie einen Moment Zeit, zu berücksichtigen, jeder dieser Eingabe Bindungen und wie Sie diese in einer Projektmappe verwenden. Es gibt eine große Auswahl an. Diese Liste kann auch mit der Zeit geändert haben, die Sie dieses Modul lesen, während wir damit fortfahren, Weitere Datenquellen unterstützen.

4. Wählen Sie **Abbrechen** zu dieser Liste zu schließen.

5. Wählen Sie **+ neue Ausgabe** unter der **Ausgaben** Spalte. Eine Liste von allen Bindungstypen für mögliche Ausgabe wird angezeigt, wie im folgenden Screenshot gezeigt.

![Screenshot: Liste der möglichen ausgabebindungen.](../media-draft/func-output-bindings-selector-small.PNG)

In diesem Fall müssen Sie einer Vielzahl von Optionen, wie durch die Notwendigkeit für eine Bildlaufleiste rechts in diesem Screenshot gezeigt.

>[!TIP]
>Weitere Informationen zu den Bindungen finden Sie, die unterstützt werden, sehen Sie sich die [Liste der unterstützten Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-versions) in der Dokumentation zu Azure Functions.

Bisher haben wir gelernt, wie Sie eine Funktions-app erstellen, und fügen eine Funktion hinzu. Wir haben eine einfache Funktion in Aktion gesehen, die ausgeführt wird, wenn eine HTTP-Anforderung an die sie vorgenommen wird. Wir haben auch die Portal-Benutzeroberfläche und Typen von Eingabe- und ausgabebindung, die unsere Funktionen zur Verfügung stehen, untersucht. In der nächsten Einheit verwenden wir eine eingabebindung zum Lesen von Text aus einer Datenbank.