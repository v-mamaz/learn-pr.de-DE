Jede Funktion muss genau eine Triggerbindung besitzen. Sie definiert, wie die Ausführung des Codes ausgelöst wird. Zusätzlich zu einem Trigger können wir auch Bindungen zur Verbindungsherstellung mit Datenquellen definieren. Wie in dem Lösungsdiagramm zu sehen, möchten wir Nachrichten an drei Warteschlangen senden. Wir definieren daher diese Verbindungen als Ausgabebindungen in unserer Funktion. Diese Bindungen könnten wir über die Benutzeroberfläche **Ausgabebindung** erstellen. Aus Zeitgründen bearbeiten wir jedoch die Konfigurationsdatei direkt.

1. Wählen Sie im Funktions-Apps-Portal die Funktion [!INCLUDE [func-name-discover](./func-name-discover.md)] aus.

1. Erweitern Sie auf der rechten Bildschirmseite das Menü **Dateien anzeigen**.

1. Klicken Sie auf der Registerkarte **Dateien anzeigen** auf **function.json**, um die Konfigurationsdatei im Editor zu öffnen.

1. Ersetzen Sie den gesamten Inhalt der Konfigurationsdatei durch den folgenden JSON-Code. 

[!code-json[](../code/function.json)]

Wir haben der Konfiguration drei neue Bindungen hinzugefügt.

- Die neuen Bindungen sind jeweils vom Typ `queue`. Diese Bindungen sind für die drei Warteschlangen vorgesehen, die wir mit unseren Feedbacknachrichten auffüllen, sobald wir die Stimmung des Feedbacks kennen.
- Jede Bindung verfügt über eine als `out` definierte Richtung, da wir Nachrichten an diese Warteschlangen übermitteln möchten.
- Jede Bindung verwendet die gleiche Verbindung mit unserem Speicherkonto.
- Jede Bindung besitzt einen eindeutigen Warteschlangennamen (`queueName`) und einen eindeutigen Namen (`name`).

Eine Nachricht kann ganz einfach an eine Warteschlange übermittelt werden. Beispielsweise so: `context.bindings.negativeFeedbackQueueItem = "<message>"`.

## <a name="update-implementation-to-sort-feedback-into-queues-based-on-sentiment-score"></a>Aktualisieren der Implementierung, um Feedback auf der Grundlage des Stimmungswerts in Warteschlangen einzusortieren

Unser Feedbacksortierer soll Feedback in drei Buckets (positiv, neutral und negativ) sortieren. Wir verfügen bislang über eine Eingabewarteschlange sowie über Code zum Aufrufen der Textanalyse-API und haben unsere Ausgabewarteschlangen definiert. In diesem Abschnitt fügen wir die erforderliche Logik hinzu, um Nachrichten auf der Grundlage der Stimmung in diese Warteschlangen zu verschieben.

1. Navigieren Sie zur Funktion [!INCLUDE [func-name-discover](./func-name-discover.md)], und öffnen Sie erneut `index.js` im Code-Editor.

1. Ersetzen Sie die Implementierung durch die folgende Aktualisierung.
[!code-javascript[](../code/discover-sentiment+sort.js?highlight=25-48)]

Wir haben der Implementierung den hervorgehobenen Code hinzugefügt. Der Code analysiert die Antwort der Textanalyse-API von Cognitive Services. Die Nachricht wird auf der Grundlage des Stimmungswerts an eine der drei Ausgabewarteschlangen weitergeleitet. Der Code zum Veröffentlichen der Nachricht legt lediglich den korrekten Bindungsparameter fest.

## <a name="try-it-out"></a>Ausprobieren

Um die aktualisierte Implementierung zu testen, kehren wir zum Storage-Explorer zurück. 

1. Navigieren Sie im Portal im Abschnitt **Ressourcengruppen** zu Ihrer Ressourcengruppe.

1. Wählen Sie die in dieser Lektion verwendete Ressourcengruppe aus.

1. Daraufhin öffnet sich der Bereich **Ressourcengruppe**. Wählen Sie hier den Eintrag „Speicherkonto“ aus.
![Screenshot: Ausgewähltes Speicherkonto im Fenster „Ressourcengruppe“.](../media-draft/select-storage-account.png)

1. Klicken Sie im linken Menü des Hauptfensters „Speicherkonto“ auf **Storage-Explorer (Vorschau)**.  Daraufhin wird im Portal der Azure Storage-Explorer geöffnet. Der Bildschirm sollte nun wie im folgenden Screenshot aussehen.
![Screenshot des Storage-Explorers mit unserem Speicherkonto und einer Warteschlange.](../media-draft/storage-explorer-menu-inputq.png)

Unter der Sammlung **Warteschlangen** befindet sich eine einzelne Warteschlange. Dabei handelt es sich um [!INCLUDE [input-q](./q-name-input.md)] (die Eingabewarteschlange, die wir im vorherigen Testabschnitt des Moduls definiert haben).

1. Klicken Sie im linken Menü auf [!INCLUDE [input-q](./q-name-input.md)], um den Daten-Explorer für diese Warteschlange anzuzeigen. Wie nicht anders zu erwarten, enthält die Warteschlange keine Daten. Als Nächstes fügen wir der Warteschlange mithilfe des Befehls **Nachricht hinzufügen** am oberen Rand des Fensters eine Nachricht hinzu. 

1. Geben Sie im Dialogfeld **Nachricht hinzufügen** den Text „I'm having fun with this exercise!“ in das Feld **Nachrichtentext** ein, und klicken Sie am unteren Rand des Dialogfelds auf **OK**. 

1. Die Nachricht wird im Datenfenster für [!INCLUDE [input-q](./q-name-input.md)] angezeigt. Klicken Sie nach einigen Sekunden am oberen Rand der Datenansicht auf **Aktualisieren**, um die Ansicht der Warteschlange zu aktualisieren. Wie Sie sehen, verschwindet die Nachricht nach einer Weile. Aber wohin?

1. Klicken Sie im linken Menü mit der rechten Maustaste auf die Sammlung **WARTESCHLANGEN**. Dort sehen Sie, dass eine *neue* Warteschlange vorhanden ist.
![Screenshot des Storage-Explorers mit einer neuen Warteschlange in der Sammlung. Die Warteschlange enthält eine einzelne Nachricht.](../media-draft/sa-new-output-q.png)

Die Warteschlange [!INCLUDE [positive-q](./q-name-positive.md)] wurde automatisch erstellt, als erstmals eine Nachricht an sie gesendet wurde. Mit Ausgabebindungen für Azure Functions-Warteschlangen müssen Sie die Ausgabewarteschlange nicht erst manuell erstellen, bevor Sie etwas an sie senden. Nachdem durch unsere Funktion offenbar eine eingehende Nachricht in [!INCLUDE [positive-q](./q-name-positive.md)] einsortiert wurde, sehen wir uns als Nächstes an, wo die folgenden Nachrichten platziert werden.

5. Fügen Sie [!INCLUDE [input-q](./q-name-input.md)] mithilfe der Schritte von weiter oben folgende Nachrichten hinzu.

- „I like broccoli!“
- „Microsoft is a company“

6. Klicken Sie auf **Aktualisieren**, bis [!INCLUDE [input-q](./q-name-input.md)] wieder leer ist. Das kann etwas dauern und mehrere Aktualisierungen erfordern.

1. Klicken Sie mit der rechten Maustaste auf die Sammlung **WARTESCHLANGEN**. Hier werden nun zwei weitere Warteschlangen angezeigt. Die Warteschlangen heißen [!INCLUDE [neutral-q](./q-name-neutral.md)] und [!INCLUDE [negative-q](./q-name-negative.md)]. Der Vorgang dauert unter Umständen etwas. Aktualisiert Sie die Sammlung **WARTESCHLANGEN**, bis die neuen Warteschlangen angezeigt werden. Danach sollte Ihre Warteschlangenliste wie folgt aussehen:

![Screenshot des Storage-Explorer-Menüs mit vier Warteschlangen in der Sammlung „WARTESCHLANGEN“.](../media-draft/sa-final-q-list.png)

Klicken Sie auf die einzelnen Warteschlangen in der Liste, um zu sehen, ob sie über Nachrichten verfügen. Wenn Sie die vorgeschlagenen Nachrichten hinzugefügt haben, sollte in [!INCLUDE [positive-q](./q-name-positive.md)], [!INCLUDE [neutral-q](./q-name-neutral.md)] und [!INCLUDE [negative-q](./q-name-negative.md)] jeweils eine Nachricht enthalten sein.

Herzlichen Glückwunsch! Sie verfügen nun über einen funktionierenden Feedbacksortierer. Wenn Nachrichten bei der Eingabewarteschlange eingehen, ruft unsere Funktion mithilfe des Textanalyse-API-Diensts einen Stimmungswert ab. Anschließend werden die Nachrichten auf der Grundlage dieses Werts an die entsprechende Warteschlange weitergeleitet. Es sieht vielleicht so aus, als würde die Funktion immer nur ein Warteschlangenelement verarbeiten. Tatsächlich liest die Azure Functions-Laufzeit aber Batches mit Warteschlangenelementen und startet weitere Instanzen unserer Funktion, um sie parallel zu verarbeiten. 