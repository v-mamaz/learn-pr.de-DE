Aktualisieren wir unsere Funktionsimplementierung zum Aufruf des Textanalyse-API-Diensts und zum Abrufen einer Stimmungsbewertung.

1. Wählen Sie im Funktions-Apps-Portal unsere Funktion [!INCLUDE [func-name-discover](./func-name-discover.md)] aus.

1. Erweitern Sie auf der rechten Bildschirmseite das Menü **Dateien anzeigen**.

1. Klicken Sie auf der Registerkarte **Dateien anzeigen** auf **index.json**, um die Codedatei im Editor zu öffnen.

1. Ersetzen Sie den gesamten Inhalt der Codedatei durch den folgenden JavaScript-Code.

[!code-javascript[](../code/discover-sentiment-sort.js?highlight=7)]

Sehen wir uns an, was in diesem Code geschieht:

- Um den Textanalysedienst aufzurufen, legen Sie `accessKey` (im Codeausschnitt hervorgehoben) auf den zuvor gespeicherten Schlüssel fest.
- Aktualisieren Sie `uri` mit der Region, aus der Sie Ihren Zugriffsschlüssel abgerufen werden – sofern diese von der Region *USA, Westen* in diesem Beispiel abweicht.
- Am Ende der Codedatei haben wir ein `documents`-Array definiert. Dieses Array ist die Nutzlast, die wir an den Textanalysedienst senden. 
- Das `documents`-Array enthält in diesem Fall einen einzelnen Eintrag: die Warteschlangennachricht, die unsere Funktion ausgelöst hat. Wenngleich wir nur über ein Dokument in unserem Array verfügen, bedeutet dies nicht, dass unsere Lösung nur jeweils eine Nachricht verarbeiten kann. Die Azure Functions-Runtime führt Abruf und Verarbeitung von Nachrichten in Batches durch, hierbei werden verschiedene Instanzen unserer Funktion  *parallel* aufgerufen. Aktuell beträgt die standardmäßige Batchgröße 16 und die maximal zulässige Batchgröße 32.
- Die `id` muss innerhalb des Arrays eindeutig sein. Die `language`-Eigenschaft gibt die Sprache des Dokumenttexts an.  
- Anschließend rufen wir unsere Methode `get_sentiments` auf, die das HTTPS-Modul zum Aufrufen der Textanalyse-API verwendet. Beachten Sie, dass wir unseren Abonnement- oder Zugriffsschlüssel im Header jeder Anforderung übergeben.
- Bei Rückgabe durch den Dienst wird `response_handler` aufgerufen, und die Antwort wird unter Verwendung von `context.log` an die Konsole ausgegeben. 

## <a name="try-it-out"></a>Testen

Bevor wir uns mit der Sortierung in Warteschlangen befassen, führen wir mit den vorhandenen Daten zunächst einen Testlauf aus. 

1.  Klicken Sie bei ausgewählter Funktion [!INCLUDE [func-name-discover](./func-name-discover.md)] im Funktionen-Apps-Portal auf das ganz links angezeigte Menüelement für Tests, um es zu erweitern.

2. Wählen Sie das Menüelement **Test** aus, und überprüfen Sie, ob der Testbereich geöffnet ist. Der folgende Screenshot zeigt, wie der Bildschirm aussehen sollte. 

![Screenshot mit erweitertem Bereich für den Funktionstest](../media-draft/test-panel-open-small.png)

3. Fügen Sie wie im Screenshot gezeigt eine Textzeichenfolge in den Anforderungstext ein. 

1.  Klicken Sie unten im Testbereich auf **Ausführen**.

1. Stellen Sie sicher, dass die Registerkarte **Protokolle** im linken unteren Bereich des Hauptbildschirms (unter dem Code-Editor) erweitert ist. 

1. Überprüfen Sie, ob die Registerkarte **Protokolle** anzeigt, dass die Funktion ausgeführt wurde. Das Fenster zeigt außerdem die Antwort des Aufrufs der Textanalyse-API an. 

![Screenshot mit Anzeige des Testbereichs und dem Ergebnis eines erfolgreichen Tests](../media-draft/sentiment-response-log1.png)

Herzlichen Glückwunsch! [!INCLUDE [func-name-discover](./func-name-discover.md)] arbeitet wie vorgesehen. In diesem Beispiel haben wir eine sehr positive Nachricht übergeben und eine Bewertung von über 0,98 erhalten. Ändern Sie die Nachricht ab, sodass sie weniger optimistisch ist, führen Sie den Test erneut aus, und beachten Sie die Antwort.

## <a name="try-it-out-again-optional"></a>Nochmals testen (optional)

Wiederholen wir den Test. Dieses Mal verwenden wir jedoch nicht das Testfenster im Portal, sondern platzieren eine Nachricht in der Eingabewarteschlange und beobachten, was geschieht. 

1. Navigieren Sie im Portalabschnitt **Ressourcengruppen** zu Ihrer Ressourcengruppe.

1. Wählen Sie die in dieser Lektion verwendete Ressourcengruppe aus.

1. Daraufhin öffnet sich der Bereich **Ressourcengruppe**. Wählen Sie hier den Eintrag „Speicherkonto“ aus.

![Screenshot mit ausgewähltem Speicherkonto im Fenster „Ressourcengruppe“](../media-draft/select-storage-account.png)

1. Klicken Sie im linken Menü des Hauptfensters für das Speicherkonto auf **Storage-Explorer (Vorschau)**.  Daraufhin wird im Portal der Azure Storage-Explorer geöffnet. Der Bildschirm sollte nun wie im folgenden Screenshot aussehen. 

![Screenshot des Storage-Explorers mit unserem Speicherkonto, derzeit ohne Warteschlange](../media-draft/sa-no-queue.png)

Wie Sie sehen können, enthält dieses Speicherkonto aktuell keine Warteschlangen. Lassen Sie uns das ändern.

1. Falls Sie sich erinnern, haben wir zu einem früheren Zeitpunkt in dieser Lektion die unserem Trigger zugeordnete Warteschlange mit dem Namen **new-feedback-q** versehen. Klicken Sie im Storage-Explorer mit der rechten Maustaste auf das Element **Warteschlangen**, und wählen Sie *Warteschlange erstellen* aus.

1. Geben Sie im nun geöffneten Dialogfeld **new-feedback-q** ein, und klicken Sie auf **OK**. Jetzt verfügen wir über eine Eingabewarteschlange. 

1. Wählen Sie im linken Menü die neue Warteschlange aus, um den Daten-Explorer für diese Warteschlange anzuzeigen. Wie zu erwarten, ist die Warteschlange leer. Als Nächstes fügen wir der Warteschlange mithilfe des Befehls **Nachricht hinzufügen** am oberen Rand des Fensters eine Nachricht hinzu.

1. Geben Sie im Dialogfeld **Nachricht hinzufügen** den Text „Diese Nachricht kam von unserer Eingabewarteschlange new-feedback-q“ in das Feld **Nachrichtentext** ein, und klicken Sie unten im Dialogfeld auf **OK**. 

1. Beobachten Sie die Nachricht, die der im folgenden Screenshot ähnelt, im Daten-Explorer.
![Screenshot des Storage-Explorers mit Anzeige unseres Speicherkontos und der in der Warteschlange erstellten Nachricht](../media-draft/message-in-input-queue.png)

1. Klicken Sie nach einigen Sekunden auf **Aktualisieren**, um die Ansicht der Warteschlange zu aktualisieren. Beachten Sie, dass die Warteschlange wieder leer ist. Die Nachricht in der Warteschlange muss gelesen worden sein. 

1. Navigieren Sie zurück zu unserer Funktion im Portal, und öffnen Sie die Registerkarte **Überwachung**. Wählen Sie die neueste Meldung in der Liste aus. Beachten Sie, dass unsere Funktion die Warteschlangennachricht verarbeitet hat, die wir an „new-feedback-q“ gesendet haben.

![Screenshot des Überwachungsdashboards mit Anzeige eines Eintrags, der uns darüber informiert, dass unsere Funktion die in „new-feedback-q“ platzierte Nachricht verarbeitet hat](../media-draft/message-in-monitor.png)

In diesem Test haben wir einen vollständigen Durchlauf ausgeführt, indem wir eine Nachricht in unsere Warteschlange eingereiht und dann gesehen haben, wie die Funktion die Nachricht verarbeitet.

Wir machen Fortschritte mit unserer Lösung! Unsere Funktion erfüllt jetzt einen Nutzen. Sie empfängt Text von unserer Eingabewarteschlange und ruft dann den Textanalyse-API-Dienst auf, um eine Bewertung abzurufen.  Darüber hinaus haben wir gelernt, wie wir unsere Funktion über das Azure-Portal und den Storage-Explorer testen. In der nächsten Übung sehen wir uns an, wie einfach es ist, mithilfe von Ausgabebindungen Schreibvorgänge in Warteschlangen durchzuführen.