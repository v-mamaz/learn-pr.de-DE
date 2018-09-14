Sie haben erfolgreich eine plattformübergreifende mobile App mit Xamarin und eine Azure-Funktion mit einer Twilio-Bindung erstellt.

## <a name="clean-up"></a>Bereinigen

<!---TODO: Update for sandbox?--->

Nachdem Sie die Arbeit an dieser Azure Functions-Anwendung abgeschlossen haben, können Sie alle Ressourcen löschen, die während des Tutorials im Azure-Portal erstellt wurden.

1. Klicken Sie in Visual Studio auf *Ansicht > Cloud-Explorer*.

1. Wählen Sie oben im Panel aus der Dropdownliste *Ressourcengruppen* aus.

1. Erweitern Sie das Abonnement, das Sie zum Erstellen der Ressourcengruppe verwendet haben. Klicken Sie mit der rechten Maustaste auf die Ressourcengruppe „ImHere“ und anschließend auf *Im Portal öffnen*.

    ![Öffnen Sie im Portal die Ressourcengruppe über das Cloud-Explorer-Fenster.](../media/9-open-resource-group-in-portal.png)

1. Melden Sie sich falls erforderlich in Ihrem Browser beim Azure-Portal an.

1. Im geöffneten Portal wird die Ressourcengruppe „ImHere“ angezeigt. Klicken Sie auf **Ressourcengruppe löschen**.

1. Geben Sie zur Bestätigung des Löschvorgangs den Namen der Ressourcengruppe ein, und klicken Sie auf **Löschen**.

## <a name="summary"></a>Zusammenfassung

In diesem Artikel haben Sie Folgendes gelernt:

- Erstellen einer plattformübergreifenden Xamarin.Forms-App, die Xamarin.Essentials nutzt
- Erstellen einer plattformübergreifenden Benutzeroberfläche mit XAML zusammen mit Anwendungslogik in einem ViewModel sowie Binden der ViewModel-Eigenschaften an die Benutzeroberfläche
- Erfassen des Benutzerstandorts
- Erstellen einer Azure-Funktion mit einem HTTP-Trigger und lokales Ausführen der Funktion
- Aufrufen einer Azure-Funktion über eine mobile App und Übergeben von Daten im JSON-Format
- Binden einer Azure-Funktion an Twilio und Senden einer SMS
- Veröffentlichen einer Azure-Funktion in Azure