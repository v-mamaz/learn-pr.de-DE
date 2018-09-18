Die folgende Illustration bietet eine Übersicht darüber, was Sie in dieser Übung kompilieren werden.

![Visuelle Darstellung des standardmäßig verwendeten HTTP-Triggers, der HTTP-Anforderung und -Antwort sowie der entsprechenden req- und res-Bindungsparameter](../media-draft/default-http-trigger-visual-small.PNG)

Sie werden eine Funktion erstellen, die startet, sobald sie eine HTTP-Anforderung empfängt, und auf jede Anforderung mit einer Nachricht antwortet. Bei den Parametern `req` und `res` handelt es sich um die Triggerbindung bzw. die Ausgabebindung. Los geht's!

Melden Sie sich mit Ihrem Azure-Konto beim Azure-Portal unter [https://portal.azure.com](https://portal.azure.com?azure-portal=true) an.

### <a name="create-a-function-app"></a>Erstellen einer Funktions-App

Beginnen Sie mit der Erstellung einer Funktions-App, die Sie im gesamten Modul verwenden werden. Mit einer Funktions-App können Sie Funktionen in logischen Einheiten gruppieren. Dies erleichtert die Verwaltung, Bereitstellung und Freigabe von Ressourcen.

[!INCLUDE [resource-group-note](./rg-notice.md)]

1. Wählen Sie in der linken oberen Ecke des Azure-Portals die Schaltfläche **Ressource erstellen** und dann **Compute** > **Funktions-App** aus.
1. Legen Sie die Funktions-App-Eigenschaften wie folgt fest:


    | Eigenschaft      | Empfohlener Wert  | Beschreibung                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **App-Name** | Global eindeutiger Name | Der Name, der Ihre neue Funktions-App bezeichnet. Gültige Zeichen sind `a-z`, `0-9` und `-`.  | 
    | **Abonnement** | Ihr Abonnement | Das Abonnement, unter dem diese neue Funktions-App erstellt wird. | 
    | **Ressourcengruppe**|  [!INCLUDE [resource-group-name](./rg-name.md)] | Der Name der neuen Ressourcengruppe, in der die Funktions-App erstellt wird. | 
    | **Betriebssystem** | Windows | Das Betriebssystem, das die Funktions-App hostet.  |
    | **Hosting** |   Verbrauchstarif | Der Hostingplan, der definiert, wie Ihre Ressourcen der Funktions-App zugewiesen werden Im standardmäßigen **Verbrauchstarif** werden Ressourcen je nach Bedarf der Funktionen dynamisch hinzugefügt. Bei diesem [serverlosen Hosting](https://azure.microsoft.com/overview/serverless-computing/) bezahlen Sie nur die Zeit, in der Ihre Funktionen ausgeführt werden.   |
    | **Standort** | Europa, Westen | Wählen Sie eine [Region](https://azure.microsoft.com/regions/) in Ihrer Nähe oder in der Nähe von anderen Diensten aus, auf die Ihre Funktionen zugreifen. |
    | **Speicherkonto** |  Global eindeutiger Name |  Der Name des neuen Speicherkontos, das von Ihrer Funktions-App verwendet wird. Speicherkontonamen müssen zwischen 3 und 24 Zeichen lang sein und dürfen nur Zahlen und Kleinbuchstaben enthalten. In diesem Dialogfeld wird das Feld automatisch mit einem eindeutigen Namen gefüllt, der aus dem Namen abgeleitet wird, den Sie der App gegeben haben. Sie können jedoch auch einen anderen Namen oder sogar ein vorhandenes Konto verwenden. |


3. Klicken Sie auf **Erstellen**, um die Funktions-App bereitzustellen.

4. Wählen Sie oben rechts im Portal das Benachrichtigungssymbol aus. Achten Sie auf eine Meldung vom Typ **Die Bereitstellung wird ausgeführt**, die der folgenden Meldung ähnelt.

![Benachrichtigung, dass die Funktions-App bereitgestellt wird.](../media-draft/func-app-deploy-progress-small.PNG)

5. Die Bereitstellung kann einige Zeit in Anspruch nehmen. Belieben Sie daher im Notification Hub, und warten Sie auf eine Meldung vom Typ **Die Bereitstellung war erfolgreich** ähnlich der folgenden Meldung.

![Benachrichtigung, dass die Bereitstellung der Funktions-App abgeschlossen wurde.](../media-draft/func-app-deploy-success-small.PNG)

6. Herzlichen Glückwunsch! Sie haben Ihre Funktions-App erstellt und bereitgestellt. Wählen Sie **Zu Ressource wechseln** aus, um Ihre neue Funktions-App anzuzeigen.

>[!TIP]
>Sollten Sie Ihre Funktions-Apps im Portal nicht finden, können Sie [Funktions-Apps Ihren Favoriten im Azure-Portal hinzufügen](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#favorite).

### <a name="create-a-function"></a>Erstellen einer Funktion

Nun, da Sie über eine Funktions-App verfügen, ist es an der Zeit, eine Funktion zu erstellen. Eine Funktion wird durch einen Trigger aktiviert. In diesem Modul verwenden Sie einen HTTP-Trigger.

1. Erweitern Sie die neue Funktions-App, zeigen Sie auf die Funktionssammlung, und klicken Sie dann auf die Schaltfläche „Hinzufügen“ (**+**) neben **Funktionen**. Durch diese Aktion wird der Vorgang der Funktionserstellung gestartet. Die folgende Animation veranschaulicht diese Aktion.

![Animation des Pluszeichens, das angezeigt wird, wenn der Benutzer mit der Maus auf das Menüelement „Funktionen“ zeigt](../media-draft/func-app-plus-hover-small.gif)

2. Wählen Sie auf der Seite **Get started quickly** (Schnelleinstieg) die Option **WebHook + API** aus, wählen Sie eine Sprache für die Funktion aus, und klicken Sie dann auf **Create this function** (Diese Funktion erstellen).

3. Eine Funktion wird in Ihrer gewählten Sprache anhand der Vorlage für eine per HTTP ausgelöste Funktion erstellt. In dieser Übung erstellen Sie eine JavaScript-Funktion.

### <a name="try-it-out"></a>Testen

Testen Sie nun, was Sie bisher erstellt haben, indem Sie die folgenden Schritte ausführen:

1. Klicken Sie in der neuen Funktion rechts oben auf **</> Abrufen der Funktions-URL**, wählen Sie **default (Function key)** (Standard (Funktionsschlüssel)) aus, und klicken Sie dann auf **Kopieren**.

2. Fügen Sie die kopierte Funktions-URL in die Adressleiste Ihres Browsers ein. Fügen Sie den Wert der Abfragezeichenfolge `&name=<yourname>` am Ende der URL hinzu, und drücken Sie die Taste `Enter` auf Ihrer Tastatur, um die Anforderung auszuführen. Sie sollten eine Antwort ähnlich der folgenden Antwort sehen, die von der Funktion zurückgegeben und in Ihrem Browser angezeigt wird.  

Gut gemacht! Sie haben jetzt eine per HTTP ausgelöste Funktion zu Ihrer Funktions-App hinzugefügt und getestet, um sicherzustellen, dass sie wie erwartet funktioniert.

![Screenshot der Antwortnachricht von einem erfolgreichen Aufruf Ihrer Funktion](../media-draft/default-http-trigger-response-small.PNG)

Wie Sie aus dieser bisherigen Übung erkennen können, müssen Sie beim Erstellen einer Funktion einen Triggertyp auswählen. Jede Funktion verfügt über genau eine Triggerbindung. In diesem Beispiel verwenden Sie einen HTTP-Trigger, d.h. die Funktion startet, wenn sie eine HTTP-Anforderung empfängt. Die Standardimplementierung, die im folgenden Screenshot in JavaScript dargestellt ist, antwortet mit dem Wert eines Parameters *name*, den sie in der Abfragezeichenfolge oder dem Textkörper der Anforderung erhalten hat. Wenn keine Zeichenfolge angegeben wurde, antwortet die Funktion mit einer Meldung, in der der Aufrufer aufgefordert wird, einen Wert für den Namen anzugeben.

![Screenshot der JavaScript-Standardimplementierung einer per HTTP ausgelösten Azure-Funktion](../media-draft/default-http-trigger-implementation-small.PNG)

Der gesamte Code befindet sich im Ordner dieser Funktion in der Datei *index.js*. Sehen Sie sich kurz die andere Datei der Funktion an, die Konfigurationsdatei *function.json*. Diese Konfigurationsdaten sind in der folgenden JSON-Liste aufgeführt.

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

Wie Sie sehen können, verfügt diese Funktion über eine Triggerbindung namens **req** vom Typ `httpTrigger` und eine Ausgabebindung namens **res** vom Typ `HTTP`. Im vorangehenden Code für Ihre Funktion haben Sie gesehen, wie der Zugriff über den **req**-Parameter auf die Nutzlast der eingehenden HTTP-Anforderung erfolgte. Auf ähnliche Weise haben Sie eine HTTP-Antwort gesendet, indem Sie einfach ihren **res**-Parameter gesetzt haben. Bindungen erledigen wirklich einen Großteil der harten Arbeit für uns.

>[!TIP]
>Sie können die Dateien „index.js“ und „function.json“ sehen, indem Sie auf der rechten Seite des Funktionspanels im Azure-Portal das Menü **Dateien anzeigen** erweitern.  

### <a name="explore-binding-types"></a>Erkunden von Bindungstypen

1. Beachten Sie unter dem Funktionseintrag, dass es eine ganze Reihe von Menüelementen gibt, wie im folgenden Screenshot gezeigt.

![Screenshot mit Menüelementen unter einer Funktion im Bereich „Funktions-Apps“](../media-draft/func-menu-small.PNG)

2. Wählen Sie das Menüelement „Integrieren“, um die Registerkarte für die Integration der Funktion zu öffnen. Wenn Sie jeden Schritt in diesem Modul ausgeführt haben, sollte die Registerkarte „Integration“ in etwa wie im folgenden Screenshot aussehen.

![Screenshot mit Benutzeroberfläche bzw. Registerkarte für die Integration](../media-draft/func-integrate-tab-small.PNG)

Beachten Sie, dass bereits ein Trigger und eine Ausgabebindung definiert sind, wie in diesem Screenshot gezeigt. Sie können auch sehen, dass Sie nicht mehr als einen Trigger hinzufügen können. Um den Trigger für Ihre Funktion zu ändern, müssten Sie zuerst den Trigger löschen und einen neuen erstellen.

Andererseits wird in den Abschnitten **Eingaben** und **Ausgaben** dieses Formulars ein Pluszeichen `+` angezeigt, um weitere Verknüpfungen hinzuzufügen.

3. Wählen Sie unter der Spalte **Eingaben** die Option **+ Neue Eingabe** aus. Eine Liste aller möglichen Eingabebindungstypen wird angezeigt, wie im folgenden Screenshot zu sehen ist.

![Screenshot mit der Liste der möglichen Eingabebindungen](../media-draft/func-input-bindings-selector-small.PNG)

Nehmen Sie sich einen Moment Zeit, um jede dieser Eingabebindungen näher zu betrachten und darüber nachzudenken, wie Sie sie in einer Lösung einsetzen könnten. Es stehen eine ganze Reihe von Möglichkeiten zur Auswahl. Diese Liste kann sich zum jetzigen Zeitpunkt bereits geändert haben, da immer mehr Datenquellen unterstützt werden.

4. Wählen Sie **Abbrechen** aus, um diese Liste zu schließen.

5. Klicken Sie unter der Spalte **Ausgaben** auf die Option **+ New Output** (+ Neue Ausgabe). Eine Liste aller möglichen Ausgabebindungstypen wird angezeigt, wie im folgenden Screenshot zu sehen ist.

![Screenshot mit der Liste der möglichen Ausgabebindungen](../media-draft/func-output-bindings-selector-small.PNG)

Auch hier können Sie aus so vielen Optionen wählen, dass sogar eine Scrollleiste rechts in diesem Screenshot erforderlich ist.

>[!TIP]
>Weitere Informationen zu den unterstützten Bindungen finden Sie in der Dokumentation zu Azure Functions in der [Liste der unterstützten Bindungen](https://docs.microsoft.com/azure/azure-functions/functions-versions).

Bisher haben Sie gelernt, eine Funktions-App zu erstellen und zu dieser eine Funktion hinzuzufügen. Sie haben eine einfache Funktion in Aktion gesehen, die ausgeführt wird, sobald eine HTTP-Anforderung an sie gesendet wird. Darüber hinaus haben Sie sich mit der Benutzeroberfläche des Portals und den Typen der Eingabe- und Ausgabebindungen beschäftigt, die Ihren Funktionen zur Verfügung stehen. In der nächsten Einheit werden Sie eine Eingabebindung verwenden, um Text aus einer Datenbank zu lesen.