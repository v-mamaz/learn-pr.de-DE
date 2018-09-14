In dieser Einheit müssen Sie Ihre ASP.NET Core-Anwendung in Azure App Service hochladen.

## <a name="create-a-staging-deployment-slot"></a>Erstellen eines Stagingbereitstellungsslots

1. Öffnen Sie die App Service-Ressource (der Web-app), die Sie zuvor erstellt haben. Wenn Sie die Ressourcenseite geschlossen haben, finden Sie es erneut durch Suchen nach der app im **alle Ressourcen** oder die enthaltende Ressourcengruppe in **Ressourcengruppen**.

1. Klicken Sie im linken Navigationsbereich auf das Menüelement **Bereitstellungsslots**.

1. In der **bereitstellungsslots** klicken Sie auf die **Slot hinzufügen** Schaltfläche auf der oberen Navigationsleiste, der die Steckplätze Bereitstellungsseite.

1. Das Azure-Portal wird geöffnet. die **Slot hinzufügen** Seite wie unten dargestellt.

    1. Geben Sie einen Namen für Ihren Bereitstellungsslot ein. Verwenden Sie in diesem Fall `staging`.

    2. Sie haben zwei Möglichkeiten, eine **Konfigurationsquelle** auszuwählen.

        * Sie können auch die Konfigurationselemente von App Service-app oder vorhandenen bereitstellungsslot klonen.
        * Oder Sie können sich gegen das Klonen von Konfigurationselementen entscheiden. Wählen Sie die Option **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen) aus.

        Wählen Sie für diesen Bereitstellungsslot die zweite Option aus, **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen). Sie werden ihn direkt konfigurieren.

    ![Screenshot des Azure-Portals mit der Konfiguration für einen neuen Stagingbereitstellungsslot.](../media/7-new-deployment-slot-blade.png)

1. Klicken Sie auf die **OK** Schaltfläche am unteren Rand der Seite, um Ihren neuen bereitstellungsslot zu erstellen.

1. Nachdem der bereitstellungsslot erfolgreich erstellt wurde, gelangen Sie über den Azure-Portal an die **bereitstellungsslots** auf der Seite Ihrer Web-app.

    Sie sehen nun den neuen Bereitstellungsslot, den Sie gerade erstellt haben.

    ![Screenshot des Azure-Portal mit die Steckplätze Bereitstellungsseite mit den neuen Steckplatz erstellt.](../media/7-deployment-slot-created.png)

1. Wählen Sie den neuen Bereitstellungsslot aus.

1. Im Azure-Portal wird die Seite **Übersicht** des neu erstellten Bereitstellungsslots angezeigt.

    ![Stagingbereitstellungsslot](../media/7-deployment-slot-staging.png)

    Beachten Sie die **URL** des Stagingbereitstellungsslots. Die URL unterscheidet sich von der zuvor angezeigten, sie enthält den angefügten Slotnamen.

    Ein bereitstellungsslot wird als eine vollständige App Service-app in Azure behandelt. Es ist jedoch ein spezieller Typ, der ist ein untergeordnetes Element der ursprünglichen app, und kann mit der ursprünglichen app ausgetauscht werden.

    Wenn Sie auf die **URL**, sehen Sie die gleichen Standardseite, die beim ersten wir ihn im Azure-Portal erstellt Azure für den bereitstellungsslot "app" erstellt.

Nachdem der Stagingbereitstellungsslot erfolgreich erstellt wurde, müssen Sie nun **Anmeldeinformationen für die Bereitstellung** konfigurieren.

## <a name="create-deployment-credentials"></a>Erstellen von Anmeldeinformationen für die Bereitstellung

In Azure müssen Anmeldeinformationen für die Bereitstellung eingerichtet werden, bevor Sie mit dem eigentlichen Bereitstellungsvorgang beginnen können. Aus diesem Grund lernen Sie, wie Sie Ihre eigenen Anmeldeinformationen für die Bereitstellung erstellen.

1. Klicken Sie im linken Navigationsbereich auf das Menüelement **Anmeldeinformationen für Bereitstellung**.

1. Das Azure-Portal navigiert zu der **Anmeldeinformationen für die Bereitstellung** Seite wie unten dargestellt.

    Geben Sie einen **Benutzernamen** und ein **Kennwort** Ihrer Wahl ein, und bestätigen Sie nochmals Ihr Kennwort.

    > [!NOTE]
    > Notieren Sie sich unbedingt Ihren Benutzernamen und das Kennwort, damit Sie beides nicht vergessen! Sie werden diese Informationen später benötigen, wenn wir beginnen, Ihren Code in Azure hochzuladen und bereitzustellen.

    ![Screenshot des Azure-Portal mit der Seite Anmeldeinformationen für die Bereitstellung im stagingslot mit Beispiel-Anmeldeinformationen die erforderlichen Felder.](../media/7-deployment-credentials.png)

1. Klicken Sie auf die **speichern** Schaltfläche am oberen Rand der **bereitstellungsanmeldeinformationen** Seite.

Nachdem die Anmeldeinformationen für die Bereitstellung erfolgreich erstellt wurden, müssen Sie nun weitere Bereitstellungsoptionen konfigurieren.

## <a name="use-a-local-git-repository-as-your-deployment-option"></a>Verwenden eines lokalen Git-Repositorys als Bereitstellungsoption

Als Nächstes erstellen wir ein lokales Git-Repository in Azure, sodass Sie Ihren Code hochladen beginnen können.

1. In der **staging** bereitstellungsslot "app", klicken Sie auf die **Bereitstellungsoptionen** Menüelement im linken Navigationsbereich auf.

1. Das Azure-Portal navigiert zu der **Bereitstellungsoptionen** Seite.

1. Klicken Sie auf **Quelle auswählen**, um die erforderlichen Einstellungen zu konfigurieren.

1. Im Azure-Portal werden die verfügbaren Optionen angezeigt, die Sie konfigurieren und verwenden können. Wählen Sie in unserem Fall die Option **Lokales Git-Repository** aus.

1. Sie kehren zu den **Bereitstellungsoption** Seite. Klicken Sie auf die **OK** Schaltfläche am unteren Rand der Seite zum Einrichten der bereitstellungsquelle.

1. Navigieren Sie jetzt zum Abschnitt **Deployment Center (Preview)** (Bereitstellungscenter (Vorschau)) im linken Navigationsbereich, um die neuen Bereitstellungsdetails anzuzeigen.

    ![Screenshot des Azure-Portal mit dem bereitstellungsslot Deployment-Center-Seite mit dem Git-Klon-Uri für den Slot hervorgehoben.](../media/7-staging-after-setting-git.png)

    Die wichtigen Informationen hier zu beachten ist die **Git-Klon-Uri**, d.h., dass die lokale Git-Repository-URL, die Sie als verwenden eine **remote** für Ihr lokales Repository für Anwendungscode.

Nun wird es Zeit, mit dem Hochladen Ihres Codes in den Stagingbereitstellungsslot zu beginnen.

## <a name="install-git-on-your-machine"></a>Installieren von Git auf Ihrem Computer

Installieren Sie Git auf Ihrem Linux-Computer, wenn dies noch nicht geschehen ist.

> [!NOTE]
> Diese Anweisungen beziehen sich auf Ubuntu 18.04, daher können die Schritte zum Installieren von Git für Ihre Distribution und Version abweichen. Suchen Sie in den [Installationsanweisungen für Git unter Linux](https://git-scm.com/download/linux) nach den passenden Schritten.

1. Öffnen Sie ein neues **Terminalfenster**.

1. Geben Sie den folgenden Befehl ein. Sie werden aufgefordert, Ihr Ubuntu-Benutzerkennort einzugeben.

    ```console
    sudo apt-get update
    ```

1. Sobald das Update erfolgreich abgeschlossen wurde, geben Sie den folgenden Befehl ein, um Git lokal zu installieren. Sie werden aufgefordert, die Installation von Git auf Ihrem Computer zu akzeptieren.

    ```console
    sudo apt-get install git-core
    ```

1. Um sicherzustellen, dass Git jetzt installiert ist, geben Sie den folgenden Befehl ein:

    ```console
    git --version
    ```

   Wenn die Installation erfolgreich war, wird die folgende Ausgabe angezeigt:

    ```console
    git version 2.17.1
    ```

1. Es empfiehlt sich stets, Git-Einstellungen zu konfigurieren, indem Sie Ihren Namen und Ihre E-Mail-Adresse bereitstellen. Hierzu müssen Sie die folgenden Befehle verwenden. Ersetzen Sie dabei die Platzhalter für `{your name}` und `{your email}` durch Ihren eigenen Namen und Ihre E-Mail-Adresse, jedoch ohne die geschweiften Klammern `{}`:

    ```console
    git config --global user.name "{your name}"
    git config --global user.email "{your email}"
    ```

1. Um sicherzustellen, dass Ihre Daten von Git erfasst wurden, geben Sie den folgenden Befehl ein:

    ```console
    cat ~/.gitconfig
    ```

   Sie sollten Folgendes sehen, einschließlich Ihres Namens und Ihrer E-Mail-Adresse:

    ```console
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-code"></a>Initialisieren Sie ein lokales Git-Repository für Ihren code

Nutzen Sie Git, müssen Sie ein lokales Git-Repository für Ihren Code der .NET Core-Anwendung zu initialisieren.

1. Öffnen Sie ein neues **Terminalfenster**.

1. Navigieren Sie zum Stammordner Inhaltsbereichs der .NET Core-app, die Sie zuvor erstellt haben. Sie können Folgendes eingeben:

    ```console
    cd ~/Documents/BestBikeApp/
    ```

1. Verwenden Sie den folgenden Befehl, um ein neues Git-Repository zu initialisieren:

    ```console
    git init
    ```

    Wenn der Befehl erfolgreich ist, erhalten Sie sinngemäß die folgende Meldung:

    ```console
    Initialized empty Git repository in /home/{your-user}/Documents/BestBikeApp/.git/
    ```

1. Stellen Sie die Anwendungsdateien in Git an.

   Der nächste Schritt ist auf Git, kennen Ihre Anwendungsdateien zu ermöglichen. Hierzu fügen Sie alle Dateien des Arbeitsverzeichnisses hinzu, sodass sie von Git **bereitgestellt** werden. Geben Sie den folgenden Befehl ein:

    ```console
    git add .
    ```

    Der obige Befehl fügt alle durch „.“ dargestellten Dateien zum Stagingstatus von Git hinzu.

1. Nun müssen Sie Ihre Änderungen an Git committen.

   Nachdem Sie die Dateien mit Git bereitgestellt haben, müssen Sie Ihre Dateien an den **Git-Commitverlauf** auf Ihrem lokalen Computer committen. Hierzu geben Sie den folgenden Befehl ein:

    ```console
   git commit -m "Initial create"
    ```

   Der `commit`-Befehl akzeptiert das `-m`-Argument, um eine Nachricht mit dem von Ihnen erstellten Commit einzuschließen. Wenn Sie später Ihren Code an Azure übertragen, sehen Sie diese Nachricht, die mit diesem konkreten Commit gespeichert wurde.

## <a name="add-a-remote-for-the-local-git-repository"></a>Hinzufügen eines Remoterepositorys für das lokale Git-Repository

Sie haben nun erfolgreich ein neues lokales Git-Repository initialisiert. Darüber hinaus haben Sie alle Ihre Anwendungsdateien zu Git ein Commit ausgeführt. Nun müssen Sie lediglich noch ein **Remote**repository hinzufügen, um Ihr lokales Git-Repository mit dem auf Azure gehosteten Repository zu verbinden.

Hierzu müssen Sie Folgendes durchführen:

1. Kopieren Sie die **GIT-Klon-URL**, die Sie weiter oben gesehen haben.

1. Nach dem Kopieren kehren Sie zum **Terminal**fenster zurück und verwenden den folgenden Git-Befehl:

    ```console
    git remote add origin https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    Mit dem obigen Git-Befehl wird Ihr lokales Git-Repository mit dem in Azure gehosteten Repository verbunden. Nun ist Push und Pull zwischen dem lokalen Git-Repository und dem Remote-Git-Repository möglich.

1. Geben Sie zum Überprüfen des obigen Befehls den folgenden Git-Befehl ein:

    ```console
    git remote -v
    ```

    Mit dem obigen Befehl wird die folgende Ausgabe generiert:

    ```console
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a>Übertragen Ihres Codes an Azure mithilfe von Push

Nun, da Sie Ihr lokale Git-Repository verknüpft, die remote-Git-Repository in Azure verfügen, Sie entwickeln und erstellen Sie die app, und klicken Sie dann den Anwendungscode in Azure übertragen.

1. Geben Sie den folgenden Git-Befehl ein, um Ihren **Haupt**branch mithilfe von Push an das Remote-Git-Repository in Azure zu übertragen:

    ```console
    git push origin master
    ```

1. Sie werden aufgefordert, das Kennwort einzugeben, das Sie im Abschnitt **Anmeldeinformationen für die Bereitstellung** weiter oben konfiguriert haben. Geben Sie Ihr Kennwort ein, und drücken Sie die Eingabetaste. Git beginnt, Ihre Commit-Dateien in das Remote-Git-Repository von Azure hochzuladen, das unter dem Stagingbereitstellungsslot konfiguriert wurde.

## <a name="verify-the-code-is-uploaded-to-azure"></a>Stellen Sie sicher, dass der Code in Azure hochgeladen wird

1. Melden Sie sich beim Azure-Portal an.

1. Klicken Sie im linken Navigationsbereich auf das Menüelement **Alle Ressourcen**.

1. Sie gelangen im Azure-Portal zur Liste aller Ressourcen, die bisher in Azure erstellt wurden.

1. Klicken Sie auf den oben erstellten Stagingslot. Beachten Sie, dass ein bereitstellungsslot ist, gilt als eine app, und daher erscheint als App Service-Ressource unter **alle Ressourcen**.

1. Nachdem Sie auf die staging-Slot Bereitstellungsseite eingehen, wechseln Sie zur **Bereitstellungsoptionen**.

    Sie sehen, dass Ihr erster Commit, der sich lokal auf Ihrem Computer befindet, jetzt in das Azure-Portal hochgeladen wurde.

    Wenn Sie Ihren Code lokal in Git-remoterepositorys in App Service übertragen, zeichnet es sich bei Azure um diesen Vorgang.

    Jedes Mal, wenn Sie Ihren Code an Azure übertragen, wird ein neuer Datensatz zusammen mit der Nachricht angezeigt, die Sie eingeben, wenn Sie Ihre Änderungen lokal auf Ihrem Computer committen.

    ![Screenshot des Azure-Portal eine kürzliche Bereitstellung des Git-Repository auf der Optionsseite für die Entwicklung mit.](../media/7-staging-deployment-slot-after-uploading-files.png)

1. Sehen wir uns nun die **Stagingslot**-URL an. Auf die URL wurde bereits oben eingegangen. Sollten Sie jedoch Ihre URL vergessen haben, können Sie stets zur Seite **Übersicht** des Stagingbereitstellungsslots wechseln und von dort die URL übernehmen.

1. Geben Sie die folgende URL in die Adressleiste Ihres Browsers ein: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).

    ![Screenshot einer Webbrowseransicht der Website des Stagingbereitstellungsslots.](../media/7-staging-slot-hosted-online.png)

Sie haben erfolgreich Ihre lokalen Anwendungsdateien auf den staging-bereitstellungsslot in Azure hochgeladen werden.

## <a name="swapping-the-staging-and-production-deployment-slots"></a>Austauschen von Staging- und Produktionsbereitstellungsslots

Nachdem die Anwendung nun in dem Stagingbereitstellungsslot ausgeführt wird, der in Azure gehostet wird, ist es Zeit, diesen Slot gegen den Produktionsbereitstellungsslot austauschen. Gehen Sie dazu folgendermaßen vor:

1. Navigieren Sie zu der ursprünglichen app-Seite, die zuvor erstellt haben. Sie finden die ursprüngliche Web-app aus dem **alle Ressourcen** Seite.

1. Klicken Sie im linken Navigationsbereich auf das Menüelement **Bereitstellungsslots**.

1. Klicken Sie auf die **austauschen** Schaltfläche am oberen Rand der Seite.

1. Das Azure-Portal zu gelangen Sie zu der **austauschen** Seite.

1. Wählen Sie für das Feld **Austauschen** die Option **Austauschen** aus.

1. Wählen Sie für das Feld **Quelle** die Option **Staging** aus.

1. Wählen Sie für das Feld **Ziel** die Option **Produktion** aus.

    ![Screenshot des Azure-Portal mit die Bereitstellungsseite des Slots austauschen.](../media/7-swap-blade.png)

1. Klicken Sie auf die **OK** am unteren Rand der Seite.

1. Azure beginnt mit dem Austauschprozess. Dieser Vorgang dauert in der Regel einige Sekunden, je nach der Größe der ausgetauschten Web-App.

1. Wechseln Sie nach Abschluss des Vorgangs zur Web-App-URL: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).

    ![Screenshot mit einer Webbrowseransicht des früheren Stagingbereitstellungsslots, der jetzt als primäre Web-App gehostet ist.](../media/7-web-app-page.png)

    Der Austauschvorgang war erfolgreich! Sie sehen nun, dass der Code, den Sie in den Stagingbereitstellungsslot hochgeladen haben, auch im Produktionsslot gehostet wird.

1. Wechseln Sie nun zur URL des Stagingslots: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).

    ![Screenshot mit einer Webbrowseransicht des zuvor primären Bereitstellungsslots, der jetzt als Stagingbereitstellungsslot-Web-App gehostet ist.](../media/7-staging-after-swapping.png)

    Der staging-bereitstellungsslot hat die ursprüngliche, Standardeinstellung jetzt HTML-Dateien, die zuvor in den produktionsslot bereitgestellt wurden.

Herzlichen Glückwunsch! Sie haben erfolgreich Ihr Anwendungscode in Azure hochgeladen und bereitstellungsslots ausgetauscht.
