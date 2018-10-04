[!INCLUDE [0-vm-note](0-vm-note.md)]

[QnA Maker](https://www.qnamaker.ai/) ist Teil der [Azure Cognitive Services](https://www.microsoft.com/cognitive-services/), einer Sammlung von Diensten und APIs zum Erstellen intelligenter Apps, die durch künstliche Intelligenz (KI) und Machine Learning unterstützt werden. Anstatt einen Bot zu codieren, um alle Fragen vorwegzunehmen, die ein Benutzer stellen könnte, und eine Antwort bereitzuhalten, können Sie eine Verbindung zwischen dem Bot und einer Wissensdatenbank herstellen, die mit QnA Maker erstellte Fragen und Antworten enthält. Ein allgemeines Verwendungsszenario ist das Erstellen einer Wissensdatenbank über die URL einer FAQ-Seite, damit der Bot domänenspezifische Fragen beantworten kann, z.B.: „Wie finde ich meinen Windows-Produktschlüssel“ oder „Wo kann ich Visual Studio Code herunterladen?“

In dieser Einheit erstellen Sie mit QnA Maker eine Wissensdatenbank, z.B. mit folgenden Fragen: „Welche NFL-Teams haben die meisten Super Bowls gewonnen?“ und „Wie heißt die größte Stadt der Welt?“ Anschließend stellen Sie die Wissensdatenbank in einer Azure-Web-App bereit, damit über einen HTTPS-Endpunkt darauf zugegriffen werden kann.

1. Öffnen Sie das QnA Maker-Portal, indem Sie https://www.qnamaker.ai im VM-Browser öffnen und auf **Anmelden** klicken, um sich mit dem gleichen Lab-Konto anzumelden, mit dem Sie sich beim Azure-Portal angemeldet haben. 

1. Klicken Sie auf das Hamburger-Menü und dann auf **Create a knowledge base** (Wissensdatenbank erstellen). 

1. Klicken Sie auf **Create a QnA service** (QnA-Dienst erstellen).

1. Geben Sie in der neu geöffneten Registerkarte des Azure-Portals einen Namen in das Feld **Name** ein. Dieser Name muss innerhalb von Azure eindeutig sein. Stellen Sie deshalb sicher, dass daneben *und* im Feld **App-Name** weiter unten auf dem Blatt ein grünes Häkchen angezeigt wird.

1. Klicken Sie unter **Ressourcengruppe** auf **Vorhandene verwenden**, und wählen Sie anschließend auf die Übungsressourcengruppe aus, die zuvor für diese Übung erstellt wurde.

1. Wählen Sie einen **Standort** aus der Dropdownliste aus. 

1. Wählen Sie **F0** als **Tarif für Verwaltung** aus. 

1. Wählen Sie **F** als **Tarif für Suche** aus. 

1. Stellen Sie sicher, dass der **App-Name** in Azure eindeutig ist.

1. Wählen Sie in beiden Dropdownlisten für den Standort den Ihnen nächstgelegenen aus, und klicken Sie unten auf dem Blatt auf die Schaltfläche **Erstellen**.

    ![Screenshot: Azure-Portal mit dem Blatt „Erstellen“ von QnA Maker mit den beschriebenen Konfigurationswerten](../media/3-new-qna-maker-service.png)

1. Klicken Sie im Menüband auf der linken Seite im Portal auf **Ressourcengruppen**, und öffnen Sie die zuvor erstellte Übungsressourcengruppe. Warten Sie, bis sich „Wird bereitgestellt“ am oberen Rand des Blatts in „Erfolgreich“ ändert, um anzuzeigen, dass der QnA-Dienst und die zugehörigen Ressourcen erfolgreich bereitgestellt wurden. Wenn die Meldung nicht mehr angezeigt wird, können Sie in der Menüleiste auf das Glockensymbol klicken, um den Status anzuzeigen. Sie können auch oben auf dem Blatt auf **Aktualisieren** klicken, um den Bereitstellungsstatus zu aktualisieren.

1. Kehren Sie zu **Create a knowledge base** (Wissensdatenbank erstellen) zurück, indem Sie https://www.qnamaker.ai/Create im VM-Browser öffnen und zu **Schritt 2** scrollen, um eine Verbindung mit dem QnA-Dienst herzustellen.

1. Wählen Sie unter **Microsoft Azure Directory ID** **Microsoft Learn Hosting** aus.

1. Wählen Sie **Microsoft Learn Hosting** aus der Dropdownliste **Azure-Abonnementnamen** aus.

1. Wählen Sie unter **Azure QnA-Dienst** den QnA-Dienstnamen aus, den Sie zuvor angegeben haben. Wenn keine Dienste aufgeführt sind, müssen Sie die Seite möglicherweise aktualisieren.

1. Weisen Sie der Wissensdatenbank dann einen Namen wie „Factbot Knowledge Base“ zu.

1. Sie können Fragen und Antworten manuell in eine QnA Maker-Wissensdatenbank eingeben oder sie aus Online-FAQs oder lokalen Dateien importieren. Zu den unterstützten Formaten gehören Textdateien mit Tabstopptrennzeichen, Microsoft Word-Dokumente, Excel-Kalkulationstabellen und PDF-Dateien.

    Öffnen Sie https://github.com/MicrosoftDocs/mslearn-build-chat-bot-with-azure-bot-service/blob/master/Factbot.tsv.zip zur Veranschaulichung im VM-Browser, und laden Sie dann die Datei **Factbot.tsv.zip** herunter. Dieser ZIP-Ordner enthält eine Textdatei namens **Factbot.tsv**. Extrahieren und kopieren Sie die Datei auf Ihren Computer. Scrollen Sie dann im QnA Maker-Portal im VM-Browser nach unten, klicken Sie auf **+ Datei hinzufügen**, und wählen Sie dann die Datei **Factbot.tsv** aus. Diese Datei enthält 20 Fragen und Antworten im Format mit Tabstopptrennzeichen.

1. Klicken Sie am unteren Rand der Seite auf **Create your KB** (Ihre Wissensdatenbank erstellen), und warten Sie darauf, dass die Wissensdatenbank erstellt wird. Dieser Vorgang dauert normalerweise weniger als eine Minute.

1. Vergewissern Sie sich, dass die aus **Factbot.tsv** importierten Fragen und Antworten in der Wissensdatenbank angezeigt werden. Klicken Sie dann auf **Speichern und trainieren**, und warten Sie, bis das Training abgeschlossen ist.

    ![Screenshot der Factbot Knowledge Base-Website mit den geladenen Daten der Wissensdatenbank.](../media/3-save-and-train.png)

1. Klicken Sie rechts neben der Schaltfläche **Speichern und trainieren** auf **Testen**. Geben Sie „Hi“ in das Nachrichtenfeld ein, und drücken Sie die **EINGABETASTE**. Vergewissern Sie sich, dass die Antwort wie unten dargestellt „Welcome to the QnA Factbot“ lautet.

    ![Screenshot einer Testinteraktion mit dem erstellten Chatbot.](../media/3-test-kb.png)

1. Geben Sie „What book has sold the most copies?“ (Von welchem Buch wurden die meisten Exemplare verkauft?) in das Nachrichtenfeld ein, und drücken Sie die **EINGABETASTE**. Wie lautet die Antwort?

1. Klicken Sie erneut auf **Testen**, um den Testbereich auszublenden. 
1. Klicken Sie im Menü am oberen Rand der Seite auf **Veröffentlichen** und am unteren Seitenrand auf die Schaltfläche **Veröffentlichen**, um die Wissensdatenbank zu veröffentlichen. Mit *Veröffentlichen* wird die Wissensdatenbank an einem HTTPS-Endpunkt zur Verfügung gestellt.

Warten Sie auf den Abschluss des Veröffentlichungsprozesses, und bestätigen Sie, dass der QnA-Dienst bereitgestellt wurde. Die Wissensdatenbank wird nun in einer eigenen Azure-Web-App gehostet, und im nächsten Schritt wird ein Bot bereitgestellt, der sie verwenden kann.
