Jede Funktion muss es sich um einen und nur einen Trigger haben. Es wird definiert, wie unser Code ausgelöst wird, führen Sie. Zusätzlich zu einem Trigger können wir die Bindungen definieren, die uns die Verbindungen zu Datenquellen herstellen. Wenn Sie in unserem Diagramm der Lösung vergessen haben, Senden von Nachrichten an drei Warteschlangen werden sollten. Daher müssen wir diese Verbindungen als ausgabebindungen in unserer Funktion definieren. Wir konnten diese Bindungen durch Erstellen der **Ausgabebindung** Benutzeroberfläche. Allerdings um Zeit zu sparen bearbeiten wir die Config-Datei direkt.

1. Wählen Sie unsere-Funktion, [!INCLUDE [func-name-discover](./func-name-discover.md)], in der Funktions-Apps-Portal.

1. Erweitern Sie die **Ansichtsdateien** im Menü auf der rechten Seite des Bildschirms.

1. Unter den **Ansichtsdateien** Registerkarte **"Function.JSON"** auf die Config-Datei im Editor zu öffnen.

1. Ersetzen Sie den gesamten Inhalt der Config-Datei mit den folgenden JSON-Code.

[!code-json[](../code/function.json)]

Wir haben drei neue Bindungen auf die Konfiguration hinzugefügt.

- Jede neue Bindung ist vom Typ `queue`. Diese Bindungen sind für die drei Warteschlangen, die wir mit unserem feedbacknachrichten an auffüllen müssen, sobald wir wissen, dass die Stimmung des Feedbacks.
- Jede Bindung hat eine Richtung, definiert als `out`, da wir Nachrichten an diese Warteschlangen senden müssen.
- Jede Bindung wird die Verbindung mit unserem Speicherkonto verwendet.
- Jede Bindung hat einen eindeutigen `queueName` und `name`.

Veröffentlichen einer Nachricht an eine Warteschlange ist beispielsweise so einfach wie selbstverständlich `context.bindings.negativeFeedbackQueueItem = "<message>"`.

## <a name="update-implementation-to-sort-feedback-into-queues-based-on-sentiment-score"></a>Update-Implementierung, die Feedback in Warteschlangen basierend auf dem stimmungswert sortieren

Das Ziel der unsere Feedback-Sortierer ist Feedback in drei Buckets, die positive, neutral und negative sortiert. Bisher haben wir unsere Eingabewarteschlange, unser Code zum Aufrufen der Textanalyse-API, und wir haben unsere Warteschlangen Ausgabe definiert. In diesem Abschnitt fügen wir die Logik zum Verschieben von Nachrichten in diese Warteschlangen basierend auf Stimmung.

1. Navigieren Sie zu unserer Funktion [!INCLUDE [func-name-discover](./func-name-discover.md)], und öffnen Sie `index.js` im Code-Editor erneut.

1. Ersetzen Sie die Implementierung durch das folgende Update an.

[!code-javascript[](../code/discover-sentiment+sort.js?highlight=25-48)]

Wir haben unsere Implementierung den hervorgehobenen Code hinzugefügt. Der Code analysiert die Antwort der cognitive Services-Textanalyse-API. Basierend auf dem stimmungswert, wird die Nachricht an eine der weitergeleitet oder drei Warteschlangen ausgegeben. Der Code zum Veröffentlichen der Nachricht wird nur den korrekte Bindungsparameter festlegen.

## <a name="try-it-out"></a>Ausprobieren

Um die aktualisierte Implementierung zu testen, müssen wir zurück an den Storage-Explorer navigieren.

1. Navigieren Sie zu Ihrer Ressourcengruppe in der **Ressourcengruppen** -Abschnitt des Portals.

1. Wählen Sie die Ressourcengruppe, die in dieser Lektion verwendet.

1. In der **Ressourcengruppe** Bereich, der geöffnet wird, suchen Sie den Storage-Konto-Eintrag, und wählen Sie ihn.
    ![Bildschirmabbildung von Storage-Konto in das Fenster für die Ressourcengruppe ausgewählt.](../media/select-storage-account.png)

1. Wählen Sie **Storage-Explorer (Vorschau)** im linken Menü des Hauptfensters Storage-Konto.  Dadurch wird Azure Storage-Explorer im Portal geöffnet. Ihr Bildschirm sollte zu diesem Zeitpunkt wie im folgenden Screenshot aussehen.
    ![Screenshot des Storage-Explorer mit unserem Speicherkonto mit dem derzeit eine Warteschlange.](../media/storage-explorer-menu-inputq.png)

Wir haben eine Warteschlange aufgeführt, unter dem **Warteschlangen** Auflistung. Diese Warteschlange ist [!INCLUDE [input-q](./q-name-input.md)], die Eingabewarteschlange, die wir im vorherigen Abschnitt des Moduls definiert.

1. Wählen Sie [!INCLUDE [input-q](./q-name-input.md)] im linken Menü auf der Daten-Explorer für diese Warteschlange finden Sie unter. Erwartungsgemäß funktioniert, mussten die Warteschlange keine Daten. Fügen Sie eine Nachricht an die Warteschlange mithilfe der **Nachricht hinzufügen** -Befehls am oberen Rand des Fensters.

1. In der **Nachricht hinzufügen** Dialogfeld Geben Sie "Ich bin spielerisch mit dieser Übung!" in der **Meldungstext** ein, und klicken Sie auf **OK** am unteren Rand des Dialogfelds.

1. Die Meldung wird angezeigt, in das Fenster für [!INCLUDE [input-q](./q-name-input.md)]. Klicken Sie nach einigen Sekunden auf **aktualisieren** am oberen Rand der Datensicht, um die Ansicht der Warteschlange zu aktualisieren. Beachten Sie, dass die Nachricht nach einer Weile wird nicht mehr angezeigt. Daher kopiert, in denen sie?

1. Mit der rechten Maustaste auf die **WARTESCHLANGEN** Auflistung im linken Menü. Beachten Sie, dass eine *neue* Warteschlange wird angezeigt.
    ![Screenshot des Storage-Explorer mit der eine neue Warteschlange wurde in der Auflistung erstellt. Die Warteschlange weist eine Nachricht an.](../media/sa-new-output-q.png)

Die Warteschlange [!INCLUDE [positive-q](./q-name-positive.md)] wurde automatisch erstellt, wenn eine Nachricht zum ersten Mal an sie zurückgesendet wurde. Mit Azure Functions-Warteschlangen-ausgabebindungen müssen Sie keine die Ausgabewarteschlange vor der erneuten Bereitstellung, manuell zu erstellen! Nun, wir sehen eine eingehende Nachricht wurde von unseren-Funktion in sortiert [!INCLUDE [positive-q](./q-name-positive.md)], sehen wir uns an, in denen Folgendes Land Nachrichten.

1. Mithilfe der gleichen Schritte wie oben beschrieben, die folgenden Nachrichten hinzufügen [!INCLUDE [input-q](./q-name-input.md)].

- "Ich like Broccoli!"
- "Microsoft ist ein Unternehmen."

1. Klicken Sie auf **aktualisieren** bis [!INCLUDE [input-q](./q-name-input.md)] wieder leer ist. Dieser Vorgang kann einige Zeit in Anspruch nehmen und erfordern mehrere aktualisiert.

1. Mit der rechten Maustaste auf die **WARTESCHLANGEN** Sammlung, und beobachten Sie zwei weitere Warteschlangen angezeigt werden. Die Warteschlangen heißen [!INCLUDE [neutral-q](./q-name-neutral.md)] und [!INCLUDE [negative-q](./q-name-negative.md)]. Dies kann einige Sekunden dauern, daher weiterhin aktualisiert die **WARTESCHLANGEN** Auflistung bis neue Warteschlangen. Nach Abschluss des Vorgangs sollte Ihre Warteschlangenliste wie folgt aussehen.

![Screenshot des Storage-Explorers im Menü mit vier Warteschlangen in der WARTESCHLANGEN-Sammlung.](../media/sa-final-q-list.png)

Klicken Sie auf jede Warteschlange in der Liste aus, um festzustellen, ob sie Nachrichten verfügen. Wenn Sie die vorgeschlagenen Nachrichten hinzugefügt haben, sollten Sie sehen, dass eine Nachricht in [!INCLUDE [positive-q](./q-name-positive.md)], [!INCLUDE [neutral-q](./q-name-neutral.md)], und [!INCLUDE [negative-q](./q-name-negative.md)].

Herzlichen Glückwunsch! Wir verfügen jetzt über eine funktionierende Feedback Sortierer! Beim Eintreffen von Nachrichten in der Eingabewarteschlange verwendet unsere-Funktion den Textanalyse-API-Dienst, um einen stimmungswert zwischen abzurufen. Die Funktion basierend auf dieses Ergebnis, leitet die Nachrichten an die entsprechende Warteschlange weiter. Während es z. B. die Funktion Prozesse nur ein Element zu einem Zeitpunkt scheint, Azure Functions-Laufzeit tatsächlich Batches von Warteschlangenelementen liest und richten Sie andere Instanzen von unserer Funktion parallel verarbeiten.