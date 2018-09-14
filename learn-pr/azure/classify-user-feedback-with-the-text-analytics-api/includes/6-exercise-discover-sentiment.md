Aktualisieren wir unsere Implementierung der Funktion zum Aufrufen des Textanalyse-API-Diensts und einen stimmungswert zu erhalten.

1. Wählen Sie unsere-Funktion, [!INCLUDE [func-name-discover](./func-name-discover.md)], in unserem Funktions-app im Portal.

1. Erweitern Sie die **Ansichtsdateien** im Menü auf der rechten Seite des Bildschirms.

1. Unter den **Ansichtsdateien** Registerkarte **"Index.js"** auf die Codedatei im Editor zu öffnen.

1. Ersetzen Sie den gesamten Inhalt des **"Index.js"** mit den folgenden JavaScript-Code und **speichern**.

[!code-javascript[](../code/discover-sentiment-sort.js?highlight=7)]

Sehen wir uns, was in diesem Code passiert:

- Um den Text Analytics-Dienst aufzurufen, legen Sie `accessKey`, ist markiert, in dem Codeausschnitt, auf den Schlüssel, die Sie zuvor gespeichert haben.
- Update `uri` in die Region aus der Sie Ihren Zugriffsschlüssel, abgerufen, wenn diese Region unterscheidet *Westus* in diesem Beispiel gezeigt.
- Am unteren Rand der Codedatei zu verlassen, haben wir definierten ein `documents` Array. Dieses Array ist die Nutzlast, die wir zum Text Analytics-Dienst zu senden.
- Die `documents` Array verfügt über einen einzelnen Eintrag in diesem Fall der die Warteschlangen-Nachricht, die unsere Funktion ausgelöst wird. Obwohl wir nur ein Dokument in diesem Array ist, bedeutet nicht, dass unsere Lösung nur eine Nachricht gleichzeitig verarbeitet werden kann. Azure Functions-Laufzeit abruft und verarbeitet die Nachrichten in Batches, die mehrere Instanzen von unserer Funktion aufrufen *parallel*. Derzeit die standardbatchgröße ist 16, und die maximale Batchgröße ist 32.
- Die `id` in das Array muss eindeutig sein. Die `language` Eigenschaft gibt die Sprache der Text des Dokuments.
- Dann rufen wir unsere Methode `get_sentiments`, die das HTTPS-Modul verwendet, um die Textanalyse-API aufrufen. Beachten Sie, dass wir unsere Abonnement und Zugriff auf Schlüssel im Header jeder Anforderung zu übergeben.
- Wenn der Dienst zurückgibt, unsere `response_handler` wird aufgerufen, und melden Sie sich die Antwort an die Konsole verwenden `context.log`


## <a name="try-it-out"></a>Ausprobieren

Bevor wir Sortieren in Warteschlangen ansehen, sehen wir uns, was wir für einen Test ausführen müssen.

1. Mit unserer Funktion [!INCLUDE [func-name-discover](./func-name-discover.md)], klicken Sie mit der im Portal Funktions-Apps aktiviert ist, auf das Menüelement "Test" ganz links um ihn zu erweitern.

1. Wählen Sie die **testen** Menü Element aus, und überprüfen Sie, ob Sie den Testbereich zu öffnen. Der folgende Screenshot zeigt, wie es aussehen sollte.

    ![Screenshot mit der Funktion Testbereich erweitert.](../media/test-panel-open-small.png)

1. Hinzufügen einer Textzeichenfolge in den Anforderungstext an, wie im Screenshot dargestellt.

1.  Klicken Sie auf **ausführen** am unteren Rand der Testbereich.

1. Stellen Sie sicher, dass die **Protokolle** Registerkarte am linken unteren Rand des Hauptbildschirms, im Code-Editor erweitert wird.

1. Überprüfen Sie, ob die **Protokolle** Registerkarte zeigt die Protokollinformationen, die die Funktion abgeschlossen. Die Antwort von der Textanalyse-API-Aufruf im Fenster auch angezeigt.

![Screenshot der Bereich zu testen und das Ergebnis der Test erfolgreich war.](../media/sentiment-response-log1.png)

Herzlichen Glückwunsch! Die [!INCLUDE [func-name-discover](./func-name-discover.md)] funktioniert wie vorgesehen. In diesem Beispiel haben wir eine sehr witzige Nachricht übergeben und eine Bewertung von über 0,98 empfangen. Versuchen Sie die Nachricht in einen weniger optimistisch zu ändern, führen den Test erneut aus, und beachten Sie die Antwort.

## <a name="add-a-message-to-the-queue"></a>Hinzufügen einer Meldung zu einer Warteschlange

Wir wiederholen Sie den Test ein. Dieses Mal anstatt das Fenster "Test" im Portal zu verwenden, wir tatsächlich fügen Sie eine Nachricht in die Eingabewarteschlange und sehen Sie sich, was geschieht.

1. Navigieren Sie zu Ihrer Ressourcengruppe in der **Ressourcengruppen** -Abschnitt des Portals.

1. Wählen Sie die Ressourcengruppe, die in dieser Lektion verwendet.

1. In der **Ressourcengruppe** Bereich, der angezeigt wird, suchen Sie den Storage-Konto-Eintrag, und wählen Sie ihn.

    ![Bildschirmabbildung von Storage-Konto in das Fenster für die Ressourcengruppe ausgewählt.](../media/select-storage-account.png)

1. Wählen Sie **Storage-Explorer (Vorschau)** im linken Menü des Hauptfensters Storage-Konto.  Dadurch wird Azure Storage-Explorer im Portal geöffnet. Ihr Bildschirm sollte zu diesem Zeitpunkt wie im folgenden Screenshot aussehen.

![Screenshot des Storage-Explorer mit unserem Speicherkonto mit derzeit keine Warteschlangen.](../media/sa-no-queue.png)

Wie Sie sehen können, nicht wir noch die Warteschlangen in diesem Speicherkonto haben, korrigieren wir nun, die.

5. Wenn Sie zuvor in dieser Lektion aus vergessen, namens wir die der Trigger zugeordnete Warteschlange **Feedback-Q**. Mit der rechten Maustaste auf die **Warteschlangen** Element in der Storage-Explorer, und wählen Sie *Create Queue*.

1. Geben Sie in dem nun geöffneten Dialogfeld **Feedback-Q** , und klicken Sie auf **OK**. Wir haben jetzt unsere Eingabewarteschlange.

1. Wählen Sie im linken Menü auf der Daten-Explorer für diese Warteschlange finden Sie unter der neuen Warteschlange. Erwartungsgemäß funktioniert, ist die Warteschlange leer. Fügen Sie eine Nachricht an die Warteschlange mithilfe der **Nachricht hinzufügen** -Befehls am oberen Rand des Fensters.

1. In der **Nachricht hinzufügen** Dialogfeld Geben Sie "Diese Nachricht wurde von unseren Eingabewarteschlange, neue-Feedback-Q" in der **Meldungstext** ein, und klicken Sie auf **OK** am unteren Rand des Dialogfelds.

1. Beachten Sie die Nachricht, die die Nachricht im folgenden Screenshot, in dem Daten-Explorer ähnelt.
    ![Screenshot des Storage-Explorer mit unserer Storage-Konto, mit der Meldung, die in die Warteschlange erstellt wurde.](../media/message-in-input-queue.png)

1. Klicken Sie nach einigen Sekunden auf **aktualisieren** zum Aktualisieren der Ansicht der Warteschlange. Beachten Sie, dass die Warteschlange wieder leer ist. Etwas muss die Nachricht aus der Warteschlange gelesen haben.

1. Navigieren Sie zurück zu unserer Funktion im Portal, und öffnen Sie die **Monitor** Registerkarte. Wählen Sie die neueste Nachricht auch in der Liste. Beachten Sie, dass unsere-Funktion die Warteschlangen-Nachricht verarbeitet, die wir auf das neue-Feedback-Q veröffentlicht haben.

![Screenshot der überwachungsdashboard mit einem Eintrag, der mitteilt, dass unsere-Funktion verarbeitet die warteschlangennachricht, die wir veröffentlicht, neue-Feedback-Q.](../media/message-in-monitor.png)

In diesem Test haben wir einen vollständigen Roundtrip etwas in unserer Warteschlange senden, und sehen dann die Funktion, die verarbeitet werden.

Fortschritt machen wir mit unserer Lösung! Unsere Funktion jetzt macht etwas Nützliches. Empfangen von Text aus unserer Eingabewarteschlange und klicken Sie dann Aufrufen der Textanalyse-API-Dienst, um eine stimmungspunktzahl zu erhalten.  Wir haben auch gelernt, die unsere über das Azure-Portal und dem Storage-Explorer-Funktion zu testen. In der nächsten Übung erfahren Sie, wie einfach es ist zum Schreiben in Warteschlangen-ausgabebindungen verwenden.