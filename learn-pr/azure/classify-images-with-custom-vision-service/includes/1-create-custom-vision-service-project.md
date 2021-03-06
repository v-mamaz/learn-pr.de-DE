Wenn Sie mithilfe von Custom Vision Service ein Modell zur Bildklassifizierung erstellen möchten, müssen Sie in einem ersten Schritt ein Projekt erstellen. In dieser Einheit erfahren Sie, wie Sie das Custom Vision Service-Portal verwenden, um ein Custom Vision Service-Projekt zu erstellen.

1. Öffnen Sie das [Custom Vision Service-Portal](https://www.customvision.ai/?azure-portal=true) in Ihrem Browser. Wählen Sie anschließend **Anmelden** aus.

1. Wenn Sie aufgefordert werden, sich anzumelden, geben Sie die Anmeldeinformationen für Ihr Microsoft-Konto ein. Wenn Sie zustimmen sollen, dass diese App auf Ihre Daten zugreifen kann, klicken Sie auf **Ja**, und stimmen Sie den Vertragsbedingungen zu, wenn Sie dazu aufgefordert werden.

1. Klicken Sie auf **Neues Projekt**, um ein neues Projekt zu erstellen.

    ![Erstellen eines Custom Vision Service-Projekts](../media/1-portal-click-new-project.png)

1. Geben Sie dem Projekt im Dialogfeld **Create new project** (Neues Projekt erstellen) den Namen *Kunstwerke*, und prüfen Sie, ob **Allgemein** in der Liste **Domänen** ausgewählt ist. Sie können für **Projekttypen** und **Klassifizierungstypen** die Standardeinstellungen beibehalten. Wählen Sie **Create project** (Projekt erstellen) aus, um das Projekt zu erstellen.

    > Domänen optimieren Modelle für bestimmte Bildtypen. Wenn Sie z.B. Bilder von Essen nach dargestellter Essensart oder nach Landesküche klassifizieren möchten, sollten Sie die Domäne „Essen“ auswählen. In Szenarios, die nicht im Zusammenhang mit einer der angebotenen Domänen stehen, oder wenn Sie unsicher sind, welche Domäne die Richtige ist, wählen Sie die Domäne „Allgemein“ aus.

   ![Erstellen eines Custom Vision Service-Projekts](../media/1-portal-create-project.png)

Laden Sie in einem nächsten Schritt Bilder in das Projekt, und weisen Sie diesen zur Klassifizierung Tags zu.