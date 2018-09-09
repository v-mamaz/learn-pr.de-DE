### <a name="exercise-1-create-a-custom-vision-service-project"></a>Übung 1: Erstellen eines Custom Vision Service-Projekts

Wenn Sie mithilfe von Custom Vision Service ein Modell zur Bildklassifizierung erstellen möchten, müssen Sie in einem ersten Schritt ein Projekt erstellen. In dieser Übung erfahren Sie, wie Sie das Custom Vision Service-Portal verwenden, um ein Custom Vision Service-Projekt zu erstellen.

1. Öffnen Sie das [Custom Vision Service-Portal](https://www.customvision.ai/) in Ihrem Browser. Klicken Sie anschließend auf **Anmelden**. 
 
    ![Anmelden im Custom Vision Service-Portal](../images/portal-sign-in.png)

    _Anmelden im Custom Vision Service-Portal_

1. Wenn Sie aufgefordert werden, sich anzumelden, geben Sie die Anmeldeinformationen für Ihr Microsoft-Konto ein. Wenn Sie zustimmen sollen, dass diese App auf Ihre Daten zugreifen kann, klicken Sie auf **Ja**, und stimmen Sie den Vertragsbedingungen zu, wenn Sie dazu aufgefordert werden.

1. Klicken Sie auf **Neues Projekt**, um ein neues Projekt zu erstellen.
  
    ![Erstellen eines Custom Vision Service-Projekts](../images/portal-click-new-project.png)

    _Erstellen eines Custom Vision Service-Projekts_

1. Geben Sie dem Projekt im Dialogfeld „Neues Projekt“ den Namen „Kunstwerke“, prüfen Sie, ob **Allgemein** als Domäne ausgewählt ist, und klicken Sie auf **Projekt erstellen**.

    > Domänen optimieren Modelle für bestimmte Bildtypen. Wenn Sie z.B. Bilder von Essen nach dargestellter Essensart oder nach Landesküche klassifizieren möchten, sollten Sie die Domäne „Essen“ auswählen. In Szenarios, die nicht im Zusammenhang mit einer der angebotenen Domänen stehen, oder wenn Sie unsicher sind, welche Domäne die Richtige ist, wählen Sie die Domäne „Allgemein“ aus.

    ![Erstellen eines Custom Vision Service-Projekts](../images/portal-create-project.png)

    _Erstellen eines Custom Vision Service-Projekts_

Laden Sie in einem nächsten Schritt Bilder in das Projekt, und weisen Sie diesen zur Klassifizierung Markierungen zu.