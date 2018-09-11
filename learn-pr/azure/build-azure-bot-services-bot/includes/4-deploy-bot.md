Als Sie in [Übung 1](#Exercise1) einen Azure-Web-App-Bot erstellt haben, wurde eine Azure-Web-App bereitgestellt, um ihn zu hosten. Der Bot erfordert jedoch etwas Code und muss immer noch für die Azure-Web-App bereitgestellt werden. Glücklicherweise wurde der Code für Sie vom Azure Bot Service generiert. In dieser Einheit verwenden Sie Visual Studio Code, um den Code in einem lokalen Git-Repository zu platzieren und den Bot durch Pushen von Änderungen aus dem lokalen Repository in ein mit der Azure-Web-App verbundenes Remoterepository, das den Bot hostet, in Azure zu veröffentlichen – ein als [Continuous Integration](https://en.wikipedia.org/wiki/Continuous_integration) bekannter Prozess.

1. Wenn [Git](https://git-scm.com/) nicht auf Ihrem PC installiert ist, wechseln Sie zu https://git-scm.com/downloads, und installieren Sie den Git-Client für Ihr Betriebssystem. Git ist ein kostenloses, verteiltes und nahtlos in Visual Studio Code integriertes Open-Source-Versionskontrollsystem. Wenn Sie nicht sicher sind, ob Git installiert ist, öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, und führen Sie den folgenden Befehl aus:

    ``` 
    git --version
    ```

    Wenn eine Versionsnummer angezeigt wird, ist der Git-Client installiert.

1. Wenn Node.js nicht auf Ihrem PC installiert ist, fahren Sie mit https://nodejs.org/ fort, und installieren Sie die neueste LTS-Version. Sie können ermitteln, ob Node.js installiert ist, indem Sie eine Eingabeaufforderung oder ein Terminalfenster öffnen und den folgenden Befehl eingeben:

    ```
    node --version
    ```

    Wenn Node installiert ist, wird die Versionsnummer angezeigt.

1. Wenn Visual Studio Code nicht auf Ihrem PC installiert ist, fahren Sie mit https://code.visualstudio.com/ fort, und installieren Sie es jetzt.

1. Erstellen Sie auf Ihrer Festplatte einen Ordner namens „Factbot“ am Speicherort Ihrer Wahl, der den Quellcode des Bots enthalten soll.

1. Kehren Sie zum Azure-Portal zurück, und öffnen Sie die Ressourcengruppe „factbot-rg“. Klicken Sie dann auf den Web-App-Bot, den Sie in [Übung 1](#Exercise1) erstellt haben.

    ![Öffnen des Web-App-Bots](../media-draft/4-open-web-app-bot.png)

1. Klicken Sie im Menü auf der linken Seite auf **Erstellen** und dann auf **ZIP-Datei herunterladen**, um eine ZIP-Datei vorzubereiten, die den Quellcode des Bots enthält. Sobald die ZIP-Datei vorbereitet ist, klicken Sie auf die Schaltfläche **ZIP-Datei herunterladen**, um sie herunterzuladen. Wenn der Download abgeschlossen ist, kopieren Sie den Inhalt der ZIP-Datei in den Ordner „Factbot“, den Sie in Schritt 4 erstellt haben.

    ![Herunterladen des Quellcodes](../media-draft/4-download-source.png)

1. Klicken Sie – immer noch auf dem Blatt „Erstellen“ – auf **Konfigurieren von Continuous Deployment**. Klicken Sie am oberen Rand des folgenden Blatts auf **Setup**, gefolgt von **Quelle auswählen**. Wählen Sie dann **Lokales Git-Repository** als Bereitstellungsquelle aus, und klicken Sie auf **OK**. 

    ![Angeben eines lokalen Git-Repositorys als Bereitstellungsquelle](../media-draft/4-portal-set-local-git.png)

1. Schließen Sie das Blatt „Bereitstellungen“, und klicken Sie im Menü auf der linken Seite auf **Alle App Service-Einstellungen**.

1. Klicken Sie auf **Anmeldeinformationen für die Bereitstellung**, und geben Sie einen Benutzernamen und ein Kennwort ein. Wahrscheinlich müssen Sie einen anderen Benutzernamen als „FactbotAdministrator“ eingeben, da der Name innerhalb von Azure eindeutig sein muss. Klicken Sie dann auf **Speichern**, und schließen Sie das Blatt.

    ![Eingeben von Anmeldeinformationen für die Bereitstellung](../media-draft/4-portal-enter-ci-creds.png)

1. Starten Sie Visual Studio Code, und öffnen Sie mit dem Befehl **Datei** > **Ordner öffnen...** den Ordner „Factbot“, in den Sie in Schritt 6 den Quellcode des Bots kopiert haben.

1. Klicken Sie in der Aktivitätsleiste auf der linken Seite von Visual Studio Code auf die Schaltfläche **Quellcodeverwaltung** und dann oben auf das Symbol **Repository initialisieren**. Klicken Sie dann im folgenden Dialogfeld auf die Schaltfläche **Repository initialisieren**.

    ![Initialisieren eines lokalen Git-Repositorys](../media-draft/4-vs-init-git-repo.png)

1. Geben Sie „First commit“ (Erster Commit) in das Nachrichtenfeld ein, und klicken Sie dann auf das Häkchen, um Ihre Änderungen zu übernehmen.

    ![Committen von Änderungen an das lokale Repository](../media-draft/4-vs-first-git-commit.png)

1. Wählen Sie **Integriertes Terminal** im Menü **Ansicht** von Visual Studio Code aus, um ein integriertes Terminal zu öffnen. Führen Sie dann den folgenden Befehl im integrierten Terminal aus, wobei Sie BOT_NAME an zwei Stellen durch den Bot-Namen ersetzen, den Sie in Übung 1, Schritt 3 eingegeben haben.

    ```
    git remote add qna-factbot https://BOT_NAME.scm.azurewebsites.net:443/BOT_NAME.git
    ```

1. Klicken Sie auf die Auslassungspunkte (drei Punkte) am oberen Rand der QUELLCODEVERWALTUNG, und wählen Sie **Branch veröffentlichen** im Menü aus, um den Botcode aus dem lokalen Repository nach Azure zu pushen. Wenn Sie zur Eingabe von Anmeldeinformationen aufgefordert werden, geben Sie den Benutzernamen und das Kennwort ein, die Sie in Schritt 9 dieser Übung angegeben haben.

Ihr Bot wurde in Azure veröffentlicht. Aber bevor Sie ihn dort testen, lassen Sie uns ihn lokal ausführen, und erfahren Sie, wie Sie ihn in Visual Studio Code debuggen können.