[!INCLUDE [0-vm-note](0-vm-note.md)]

Als Sie einen Azure-Web-App-Bot erstellt haben, wurde eine Azure-Web-App bereitgestellt, um diesen zu hosten. Der Bot erfordert jedoch etwas Code und muss immer noch für die Azure-Web-App bereitgestellt werden. Glücklicherweise wurde der Code für Sie vom Azure Bot Service generiert. In dieser Einheit verwenden Sie Visual Studio Code, um den Code in einem lokalen Git-Repository zu platzieren und den Bot durch Pushen von Änderungen aus dem lokalen Repository in ein mit der Azure-Web-App verbundenes Remoterepository, das den Bot hostet, in Azure zu veröffentlichen – ein als [Continuous Integration](https://wikipedia.org/wiki/Continuous_integration) bekannter Prozess.

1. Erstellen Sie auf Ihrer Festplatte am Speicherort Ihrer Wahl einen Ordner namens „Factbot“, der den Quellcode des Bots enthalten soll.

1. Kehren Sie im Browser des virtuellen Computers zum Azure-Portal zurück, und öffnen Sie Ressourcengruppe, die in der vorherigen Übung erstellt wurde. Wählen Sie anschließend den Web-App-Bot aus, den Sie in der vorherigen Übung erstellt haben.

1. Wählen Sie links im Menü den Eintrag **Erstellen** und anschließend **Download Bot source code** (Botquellcode herunterladen) aus, um eine ZIP-Datei vorzubereiten, die den Quellcode des Bots enthält. Sobald die ZIP-Datei vorbereitet wurde, klicken Sie auf die Schaltfläche **Download Bot source code** (Botquellcode herunterladen), um diesen herunterzuladen. Wenn der Download abgeschlossen ist, extrahieren Sie den Inhalt der ZIP-Datei in den zuvor erstellten Ordner „Factbot“.

1. Wählen Sie den Eintrag **Konfigurieren von Continuous Deployment** aus, wenn Sie sich im Azure-Portal wieder auf dem Blatt „Erstellen“ des Web-App-Bots befinden.

1. Wählen Sie oben auf dem Blatt **Bereitstellungen** den Eintrag **Einrichtung** aus, gefolgt von **Quelle auswählen**.

1. Wählen Sie anschließend **Lokales Git-Repository** als Bereitstellungsquelle aus.

1. Wählen Sie als Nächstes **Setup connection** (Verbindung einrichten) aus, und geben Sie einen Benutzernamen und ein Kennwort ein. Wahrscheinlich müssen Sie einen anderen Benutzernamen als „FactbotAdministrator“ eingeben, da der Name innerhalb von Azure eindeutig sein muss. Wählen Sie anschließend **OK** aus, um zum Blatt **Bereitstellungsoption** zurückzukehren. Wählen Sie erneut **OK** aus, um zum Blatt **Bereitstellungen** zurückzukehren.

    ![Screenshot: Azure-Portal mit dem neuen Bot-App Service-Blatt mit der Anzeige „Anmeldeinformationen für die Bereitstellung“, in der das Menüelement „Anmeldeinformationen für die Bereitstellung“ und die Schaltfläche „Speichern“ hervorgehoben sind.](../media/4-portal-enter-ci-creds.png)

1. Während das Bereitstellungssystem eine Bereitstellung durchführt, können Sie das Blatt **Bereitstellungen** schließen und links im Menü auf **Alle App-Diensteinstellungen** klicken.

1. Starten Sie **Visual Studio Code**, und öffnen Sie mit dem Befehl **Datei** > **Ordner öffnen...** den Ordner „Factbot“, in den Sie den Quellcode des Bots kopiert haben.

1. Klicken Sie in Visual Studio Code links in der Aktivitätsleiste auf die Schaltfläche **Quellcodeverwaltung**.

1. Klicken Sie oben auf das Symbol **Repository initialisieren**.

1. Wählen Sie im Dialogfeld die Schaltfläche **Repository initialisieren** aus.

1. Geben Sie „First commit“ (Erster Commit) in das Nachrichtenfeld ein.

1. Aktivieren Sie das Kontrollkästchen, um Ihre Änderungen zu committen und dabei alle Dateien bereitzustellen, wenn Sie dazu aufgefordert werden.

    > [!NOTE]
    > Falls ein Git-Fehler auftritt, der darauf hindeutet, dass Ihre Identität in Git nicht festgelegt wurde, starten Sie eine Eingabeaufforderung, und führen Sie die folgenden Befehle aus. Ersetzen Sie dabei bei Bedarf die Platzhalter für die Werte „E-Mail-Adresse“ und „Name“. Versuchen Sie anschließend erneut, auf die Schaltfläche „Commit“ zu klicken.
    >
    > ```bash
    > git config --global user.email "Lab User"
    > git config --global user.name "LabUser#######@learn"
    > ```

1. Wählen Sie im Menü **Ansicht** von Visual Studio Code **Terminal** aus, um ein integriertes Terminal zu öffnen.

1. Führen Sie im integrierten Terminal den folgenden Befehl aus, wobei Sie BOT_NAME an zwei Stellen durch den Botnamen ersetzen, den Sie in Übung 1 eingegeben haben.

    > [!NOTE]
    > Die vollständige Remote-URL von Git ist auch im Abschnitt **Übersicht** der App Service-Ressource unter **Git Clone-URL** zu finden.

    ```bash
    git remote add qna-factbot https://BOT_NAME.scm.azurewebsites.net:443/BOT_NAME.git
    ```

1. Kehren Sie zum Bereich **Quellcodeverwaltung** zurück, und wählen Sie oben im Bereich „Quellcodeverwaltung“ die Auslassungspunkte (drei Punkte) aus. Wählen Sie anschließend **Branch veröffentlichen** aus dem Menü aus, um den Botcode aus dem lokalen Repository nach Azure zu pushen. Wenn Sie zur Eingabe von Anmeldeinformationen aufgefordert werden, geben Sie den Benutzernamen und das Kennwort ein, die Sie in Schritt 9 dieser Übung angegeben haben.

Ihr Bot wurde in Azure veröffentlicht. Aber bevor Sie ihn dort testen, lassen Sie uns ihn lokal ausführen, und erfahren Sie, wie Sie ihn in Visual Studio Code debuggen können.
