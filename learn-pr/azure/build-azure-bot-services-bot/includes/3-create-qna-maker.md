
[QnA Maker](https://www.qnamaker.ai/) ist Teil der [Azure Cognitive Services](https://www.microsoft.com/cognitive-services/), einer Sammlung von Diensten und APIs zum Erstellen intelligenter Apps, die durch künstliche Intelligenz (KI) und Machine Learning unterstützt werden. Anstatt einen Bot zu codieren, um alle Fragen vorweg zu nehmen, die ein Benutzer stellen könnte, und eine Antwort bereitzuhalten, können Sie eine Verbindung zwischen ihm und einer Wissensdatenbank herstellen, die mit QnA Maker erstellte Fragen und Antworten enthält. Ein allgemeines Verwendungsszenario ist das Erstellen einer Wissensdatenbank auf Basis eines FAQ, damit der Bot domänenspezifische Fragen beantworten kann, wie z.B.: „Wie finde ich meinen Windows-Produktschlüssel“ oder „Wo kann ich Visual Studio Code herunterladen?“

In dieser Einheit erstellen Sie mit QnA Maker eine Wissensdatenbank mit Fragen wie z.B.: „Welche NFL-Teams haben die meisten Super Bowls gewonnen?“ und „Wie heißt die größte Stadt der Welt?“ Anschließend stellen Sie die Wissensdatenbank in einer Azure-Web-App bereit, damit über einen HTTPS-Endpunkt auf sie zugegriffen werden kann.

1. Öffnen Sie das [QnA Maker-Portal](https://www.qnamaker.ai/) in Ihrem Browser, und melden Sie sich mit Ihrem Microsoft-Konto an, wenn Sie nicht bereits angemeldet sind. Klicken Sie dann in der Menüleiste am oberen Rand der Seite auf **Wissensdatenbank erstellen**.

    ![Erstellen einer Wissensdatenbank](../media-draft/3-qna-new-kb.png)

1. Klicken Sie auf **QnA-Dienst erstellen**.

    ![Erstellen eines QnA-Diensts](../media-draft/3-create-kb-1.png)

1. Geben Sie einen Namen wie „qa-factbot-kb“ in das Feld **Name** ein. Dieser Name muss innerhalb von Azure eindeutig sein, darum stellen Sie sicher, dass daneben *und* im Feld **App-Name** weiter unten auf dem Blatt ein grünes Häkchen angezeigt wird. Wählen Sie **Vorhandene verwenden** unter **Ressourcengruppe** aus, und wählen Sie dann die Ressourcengruppe „factbot-rg“ aus, die Sie beim Bereitstellen des Azure-Web-App-Bots in [Übung 1](#Exercise1) erstellt haben. Wählen Sie **F0** und **F** als Tarife aus. (Beide Tarife sind kostenlos und ideal zum Experimentieren mit Bots.) Wählen Sie in beiden Standort-Dropdownlisten den Ihnen nächstgelegenen Standort aus, und klicken Sie unten auf dem Blatt auf die Schaltfläche **Erstellen**.

    ![Erstellen eines QnA-Diensts](../media-draft/3-new-qna-maker-service.png)

1. Klicken Sie im Menüband auf der linken Seite des Portals auf **Ressourcengruppen**, und öffnen Sie die Ressourcengruppe „factbot-rg“. Warten Sie, bis „Wird bereitgestellt“ am oberen Rand des Blatts sich in „Erfolgreich“ ändert, um anzuzeigen, dass der QnA-Dienst und die zugehörigen Ressourcen erfolgreich bereitgestellt wurden. Klicken Sie zum Aktualisieren des Bereitstellungsstatus noch einmal am oberen Rand des Blatts auf **Aktualisieren**.

    ![Erfolgreiche Bereitstellung](../media-draft/3-resource-group-master-2.png)

1. Wechseln Sie zurück zur Seite [Wissensdatenbank erstellen](https://www.qnamaker.ai/Create) im QnA Maker-Portal. Wählen Sie unter **Azure QnA-Dienst** den QnA-Dienstnamen aus, den Sie in Schritt 3 angegeben haben. Weisen Sie der Wissensdatenbank dann einen Namen wie z.B. „Factbot Knowledge Base“ zu.

    ![Benennen der Wissensdatenbank](../media-draft/3-create-kb-2-3.png)

1. Sie können Fragen und Antworten manuell in eine QnA Maker-Wissensdatenbank eingeben oder sie aus Online-FAQs oder lokalen Dateien importieren. Zu den unterstützten Formaten gehören Textdateien mit Tabstopptrennzeichen, Microsoft Word-Dokumente, Excel-Kalkulationstabellen und PDF-Dateien.

    Klicken Sie zur Veranschaulichung [hier](https://topcs.blob.core.windows.net/public/bots-resources.zip), um eine ZIP-Datei mit einer Textdatei namens **Factbot.tsv** herunterzuladen, und kopieren Sie die Datei auf Ihren Computer. Scrollen Sie dann im QnA Maker-Portal nach unten, klicken Sie auf **+ Datei hinzufügen**, und wählen Sie **Factbot.tsv** aus. Diese Datei enthält 20 Fragen und Antworten im Format mit Tabstopptrennzeichen.

    ![Füllen der Wissensdatenbank](../media-draft/3-create-kb-4.png)

1. Klicken Sie am unteren Rand der Seite auf **Ihre KB erstellen**, und warten Sie darauf, dass die Wissensdatenbank erstellt wird. Dieser Vorgang dauert normalerweise weniger als eine Minute.

    ![Erstellen der Wissensdatenbank](../media-draft/3-create-kb-5.png)

1. Vergewissern Sie sich, dass die aus **Factbot.tsv** importierten Fragen und Antworten in der Wissensdatenbank angezeigt werden. Klicken Sie dann auf **Speichern und Trainieren**, und warten Sie, bis das Training abgeschlossen ist.

    ![Trainieren der Wissensdatenbank](../media-draft/3-save-and-train.png)

1. Klicken Sie auf die Schaltfläche **Testen** rechts neben der Schaltfläche **Speichern und Trainieren**. Geben Sie „Hi“ in das Nachrichtenfeld ein, und drücken Sie die **EINGABETASTE**. Vergewissern Sie sich, dass die Antwort wie unten dargestellt „Welcome to the QnA Factbot“ lautet.

    ![Testen der Wissensdatenbank](../media-draft/3-test-kb.png)

1. Geben Sie „What book has sold the most copies?“ (Von welchem Buch wurden die meisten Exemplare verkauft?) in das Nachrichtenfeld ein, und drücken Sie die **EINGABETASTE**. Wie lautet die Antwort?

1. Klicken Sie erneut auf die Schaltfläche **Testen**, um den Bereich „Testen“ zuzuklappen. Klicken Sie dann im Menü am oberen Rand der Seite auf **Veröffentlichen** und am unteren Seitenrand auf die Schaltfläche **Veröffentlichen**, um die Wissensdatenbank zu veröffentlichen. *Veröffentlichen* macht die Wissensdatenbank an einem HTTPS-Endpunkt verfügbar.

    ![Veröffentlichen der Wissensdatenbank](../media-draft/3-publish-kb.png)

Warten Sie auf den Abschluss des Veröffentlichungsprozesses, und bestätigen Sie, dass Ihnen mitgeteilt wurde, dass der QnA-Dienst bereitgestellt ist. Die Wissensdatenbank wird nun in einer eigenen Azure-Web-App gehostet, und im nächsten Schritt wird ein Bot bereitgestellt, der sie verwenden kann.