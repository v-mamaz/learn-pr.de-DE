Sehen Sie noch einmal die Lösungsarchitektur an.

![Konzeptionelle Darstellung einer Architektur zum Sortieren von Feedback](../media/proposed-solution.PNG)

Wie Sie auf der rechten Seite des Diagramms sehen können, sollen Nachrichten an drei Warteschlangen gesendet werden. Wir definieren daher diese Verbindungen als Ausgabebindungen in unserer Funktion. Diese Bindungen könnten wir über die Benutzeroberfläche **Ausgabebindung** erstellen. Aus Zeitgründen bearbeiten wir jedoch die Konfigurationsdatei direkt.

## <a name="add-output-bindings-to-functionjson"></a>Hinzufügen von Ausgabebindungen in der function.json-Datei

1. Wählen Sie im Funktions-Apps-Portal die Funktion [!INCLUDE [func-name-discover](./func-name-discover.md)] aus.

1. Erweitern Sie auf der rechten Bildschirmseite das Menü **Dateien anzeigen**.

1. Klicken Sie auf der Registerkarte **Dateien anzeigen** auf **function.json**, um die Konfigurationsdatei im Editor zu öffnen.

1. Ersetzen Sie den gesamten Inhalt von **function.json** mit dem folgenden JSON-Code, und wählen Sie **Speichern** aus.

[!code-json[](../code/function.json)]

Sie haben der Konfiguration drei neue Bindungen hinzugefügt.

- Die neuen Bindungen sind jeweils vom Typ `queue`. Diese Bindungen sind für die drei Warteschlangen vorgesehen, die Sie mit den Feedbacknachrichten auffüllen, sobald Sie den Stimmungswert des Feedbacks kennen.
- Jede Bindung verfügt über eine als `out` definierte Richtung, da Sie Nachrichten an diese Warteschlangen übermitteln.
- Jede Bindung verwendet die gleiche Verbindung mit unserem Speicherkonto.
- Jede Bindung besitzt einen eindeutigen Warteschlangennamen (`queueName`) und einen eindeutigen Namen (`name`).

Eine Nachricht kann ganz einfach an eine Warteschlange übermittelt werden. Beispielsweise so: `context.bindings.negativeFeedbackQueueItem = "<message>"`.

## <a name="update-the-function-implementation-to-sort-feedback-into-queues-based-on-sentiment-score"></a>Aktualisieren der Funktionsimplementierung, um Feedback auf der Grundlage des Stimmungswerts in Warteschlangen einzusortieren

Der Feedbacksortierer soll Feedback in drei Buckets (positiv, neutral und negativ) einsortieren. Sie verfügen bislang über eine Eingabewarteschlange sowie über Code zum Aufrufen der Textanalyse-API. Außerdem haben Sie die Ausgabewarteschlangen definiert. In diesem Abschnitt fügen Sie Logik hinzu, um Nachrichten auf der Grundlage der Stimmung in diese Warteschlangen zu verschieben.

1. Navigieren Sie zur Funktion [!INCLUDE [func-name-discover](./func-name-discover.md)], und öffnen Sie erneut `index.js` im Code-Editor.

1. Ersetzen Sie die Implementierung durch folgenden Code.

[!code-javascript[](../code/discover-sentiment+sort.js?highlight=26-48)]

Sie haben der Implementierung den hervorgehobenen Code hinzugefügt. Der Code analysiert die Antwort der Textanalyse-API von Cognitive Services. Die Nachricht wird auf der Grundlage des Stimmungswerts an eine der drei Ausgabewarteschlangen weitergeleitet. Mit dem Code zum Übermitteln der Nachricht wird lediglich der korrekte Bindungsparameter festgelegt.

## <a name="try-it-out"></a>Ausprobieren

Um die aktualisierte Implementierung zu testen, kehren wir zum Storage-Explorer zurück.

1. Navigieren Sie im Portal im Abschnitt **Ressourcengruppen** zu Ihrer Ressourcengruppe.

1. Wählen Sie <rgn>[Name der Sandboxressourcengruppe]</rgn> aus, die in dieser Lektion verwendete Ressourcengruppe.

1. Daraufhin wird der Bereich **Ressourcengruppe** geöffnet. Wählen Sie hier den Eintrag „Speicherkonto“ aus.
    ![Screenshot mit ausgewähltem Speicherkonto im Fenster „Ressourcengruppe“](../media/select-storage-account.png)

1. Klicken Sie im linken Menü des Hauptfensters für das Speicherkonto auf **Storage-Explorer (Vorschau)**. Daraufhin wird im Portal der Azure Storage-Explorer geöffnet.

    ![Storage-Explorer-Screenshot mit dem Speicherkonto und aktuell einer Warteschlange](../media/storage-explorer-menu-inputq.png)

    Unter der Sammlung **Warteschlangen** befindet sich eine einzelne Warteschlange. Dabei handelt es sich um [!INCLUDE [input-q](./q-name-input.md)], also die Eingabewarteschlange, die Sie im vorherigen Testabschnitt des Moduls definiert haben.        

1. Klicken Sie im linken Menü auf [!INCLUDE [input-q](./q-name-input.md)], um den Daten-Explorer für diese Warteschlange anzuzeigen. Wie nicht anders zu erwarten, enthält die Warteschlange keine Daten. Als Nächstes fügen wir der Warteschlange mithilfe des Befehls **Nachricht hinzufügen** am oberen Rand des Fensters eine Nachricht hinzu.

1. Geben Sie im Dialogfeld **Nachricht hinzufügen** den Text „Diese Übung macht Spaß.“ in das Feld **Nachrichtentext** ein, und klicken Sie am unteren Rand des Dialogfelds auf **OK**.

1. Die Nachricht wird im Datenfenster für [!INCLUDE [input-q](./q-name-input.md)] angezeigt. Klicken Sie nach einigen Sekunden am oberen Rand der Datenansicht auf **Aktualisieren**, um die Ansicht der Warteschlange zu aktualisieren. Wie Sie sehen, verschwindet die Nachricht nach einer Weile. Aber wohin?

1. Klicken Sie im linken Menü mit der rechten Maustaste auf die Sammlung **WARTESCHLANGEN**. Dort sehen Sie, dass eine *neue* Warteschlange vorhanden ist.
    ![Storage-Explorer-Screenshot mit einer neu erstellten Warteschlange in der Sammlung Die Warteschlange enthält eine einzelne Nachricht.](../media/sa-new-output-q.png)

    Die Warteschlange [!INCLUDE [positive-q](./q-name-positive.md)] wurde automatisch erstellt, als erstmals eine Nachricht an sie gesendet wurde. Mit Ausgabebindungen für Azure Functions-Warteschlangen müssen Sie die Ausgabewarteschlange nicht erst manuell erstellen, bevor Sie etwas an sie senden. Nachdem durch unsere Funktion offenbar eine eingehende Nachricht in [!INCLUDE [positive-q](./q-name-positive.md)] einsortiert wurde, sehen wir uns als Nächstes an, wo die folgenden Nachrichten platziert werden.    

1. Fügen Sie [!INCLUDE [input-q](./q-name-input.md)] mithilfe der oben beschriebenen Schritte folgende Nachrichten hinzu.

    - „I hate broccoli!“
    - „Microsoft is a company“

1. Klicken Sie auf **Aktualisieren**, bis [!INCLUDE [input-q](./q-name-input.md)] wieder leer ist. Das kann etwas dauern und mehrere Aktualisierungen erfordern.

1. Klicken Sie mit der rechten Maustaste auf die Sammlung **WARTESCHLANGEN**. Hier werden nun zwei weitere Warteschlangen angezeigt. Die Warteschlangen heißen [!INCLUDE [neutral-q](./q-name-neutral.md)] und [!INCLUDE [negative-q](./q-name-negative.md)]. Der Vorgang dauert unter Umständen einige Sekunden. Aktualisiert Sie die Sammlung **WARTESCHLANGEN**, bis die neuen Warteschlangen angezeigt werden. Danach sollte Ihre Warteschlangenliste wie folgt aussehen.

    ![Screenshot des Storage-Explorer-Menüs mit vier Warteschlangen in der Sammlung „WARTESCHLANGEN“.](../media/sa-final-q-list.png)

1. Klicken Sie auf die einzelnen Warteschlangen in der Liste, um zu sehen, ob sie über Nachrichten verfügen. Wenn Sie die vorgeschlagenen Nachrichten hinzugefügt haben, sollte in [!INCLUDE [positive-q](./q-name-positive.md)], [!INCLUDE [neutral-q](./q-name-neutral.md)] und [!INCLUDE [negative-q](./q-name-negative.md)] jeweils eine enthalten sein.

Herzlichen Glückwunsch! Sie verfügen nun über einen funktionierenden Feedbacksortierer. Wenn Nachrichten bei der Eingabewarteschlange eingehen, ruft unsere Funktion mithilfe des Textanalyse-API-Diensts einen Stimmungswert ab. Anschließend werden die Nachrichten auf der Grundlage dieses Werts an die entsprechende Warteschlange weitergeleitet. Es sieht vielleicht so aus, als würde die Funktion immer nur ein Warteschlangenelement verarbeiten. Tatsächlich liest die Azure Functions-Laufzeit aber Batches mit Warteschlangenelementen und startet weitere Instanzen unserer Funktion, um sie parallel zu verarbeiten.