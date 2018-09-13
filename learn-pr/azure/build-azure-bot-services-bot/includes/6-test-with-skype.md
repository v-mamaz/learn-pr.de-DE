Nach der Bereitstellung können Bots mit Kanälen wie Skype, Slack, Microsoft Teams und Facebook Messenger verbunden werden, mit denen Sie auf die gleiche Weise interagieren können wie mit einer Person. In dieser Übung fügen Sie den Bot Ihren Skype-Kontakten hinzu und führen eine Konversation mit diesem in Skype.

1. Wenn Skype noch nicht auf Ihrem Computer installiert ist, installieren Sie es jetzt. Sie können Skype für Windows, macOS oder Linux unter https://www.skype.com/en/download-skype/skype-for-computer/ herunterladen.

1. Kehren Sie zu Ihrem Web-App-Bot im Azure-Portal zurück, und klicken Sie links im Menü auf **Kanäle**. Klicken Sie auf das **Skype**-Symbol. Klicken Sie dann ganz unten auf dem Blatt auf **Abbrechen**.

    ![Bearbeiten des Skype-Kanals](../images/portal-edit-skype.png)

    _Bearbeiten des Skype-Kanals_
 
1. Klicken Sie auf **Skype**. Klicken Sie anschließend auf **Zu Kontakten hinzufügen**, um den Bot als Skype-Kontakt hinzuzufügen, und starten Sie Skype.

    ![Herstellen einer Verbindung mit Skype](../images/portal-click-skype.png)
    
    _Herstellen einer Verbindung mit Skype_
 
1. Starten Sie ein Gespräch, indem Sie „hi“ in das Skype-Fenster eingeben. Unterhalten Sie sich dann mit dem Bot, indem Sie Fragen stellen und sich ansehen, wie er antwortet. Halten Sie sich dabei an den Inhalt der Datei **Factbot.tsv**, die Sie in [Übung 2](#Exercise2) zum Auffüllen der Wissensdatenbank mit Beispielfragen verwendet haben.
 
    ![Chatten mit dem Bot in Skype](../images/skype-responses.png)

    _Chatten mit dem Bot in Skype_

Hiermit haben Sie einen voll funktionsfähigen Bot mit Azure Bot Service erstellt, in diesen haben Sie Intelligenz von Microsoft QnA Maker eingefügt, und Sie haben ihn weltweit zur Interaktion zur Verfügung gestellt. Sie können Ihren Bot in andere Kanäle einfügen und in verschiedenen Szenarios testen. Wenn der Bot intelligenter werden soll, können Sie die Wissensdatenbank mit weiteren Fragen und Antworten erweitern. Sie können beispielsweise das [Online-FAQ](https://docs.microsoft.com/azure/bot-service/bot-service-resources-bot-framework-faq?view=azure-bot-service-3.0) für das Bot-Framework verwenden, um den Bot auf das Antworten von Fragen zum Framework selbst zu trainieren.