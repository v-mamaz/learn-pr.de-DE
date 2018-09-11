In dieser Einheit laden Sie Ihre ASP.NET Core-Anwendung in eine Azure-Web-App hoch.

## <a name="create-a-staging-deployment-slot"></a>Erstellen eines Stagingbereitstellungsslots

1. Öffnen Sie die zuvor erstellte Web-App-Ressource. Wenn Sie ihr Ressourcenblatt geschlossen haben, können Sie es wiederfinden, indem Sie unter **Alle Ressourcen** oder in der enthaltenden Ressourcengruppe unter **Ressourcengruppen** nach der App suchen.

1. Klicken Sie im linken Navigationsbereich auf das Menüelement **Bereitstellungsslots**.

1. Klicken Sie auf dem Blatt **Bereitstellungsslots** in der oberen Navigationsleiste des Blatts auf die Schaltfläche **Slot hinzufügen**.

1. Im Azure-Portal wird das Blatt **Slot hinzufügen** geöffnet, wie unten gezeigt.

    1. Geben Sie einen Namen für Ihren Bereitstellungsslot ein. Verwenden Sie in diesem Fall `staging`.

    2. Sie haben zwei Möglichkeiten, eine **Konfigurationsquelle** auszuwählen.

        * Sie können sich entscheiden, die Konfigurationselemente eines beliebigen vorhandenen Bereitstellungsslots oder einer in Azure erstellten Web-App zu klonen.
        * Oder Sie können sich gegen das Klonen von Konfigurationselementen entscheiden. Wählen Sie die Option **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen) aus.

        Wählen Sie für diesen Bereitstellungsslot die zweite Option aus, **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen). Sie werden ihn direkt konfigurieren.

    ![Screenshot des Azure-Portals mit der Konfiguration für einen neuen Stagingbereitstellungsslot.](../media/7-new-deployment-slot-blade.png)

1. Klicken Sie unten auf dem Blatt auf die Schaltfläche **OK**, um Ihren neuen Bereitstellungsslot zu erstellen.

1. Nachdem der Bereitstellungsslot erfolgreich erstellt wurde, wird im Azure-Portal wieder das Blatt **Bereitstellungsslots** Ihrer Web-App angezeigt.

    Sie sehen nun den neuen Bereitstellungsslot, den Sie gerade erstellt haben.

    ![Screenshot des Azure-Portals mit dem Blatt „Slots“ und dem neu erstellten Slot.](../media/7-deployment-slot-created.png)

1. Wählen Sie den neuen Bereitstellungsslot aus.

1. Im Azure-Portal wird die Seite **Übersicht** des neu erstellten Bereitstellungsslots angezeigt.

    ![Stagingbereitstellungsslot](../media/7-deployment-slot-staging.png)

    Beachten Sie die **URL** des Stagingbereitstellungsslots. Die URL unterscheidet sich von der zuvor angezeigten, sie enthält den angefügten Slotnamen.

    Ein Bereitstellungsslot wird Azure-intern als vollständige Web-App behandelt. Allerdings handelt es sich um einen speziellen Typ, der ein untergeordnetes Element der ursprünglichen Web-App ist und nicht gegen die ursprüngliche Web-App ausgetauscht werden kann.

    Wenn Sie auf die **URL** klicken, sehen Sie dieselbe Standardseite, die Azure für die Web-App erstellt hat, als wir die App erstmals im Azure-Portal erstellt haben.

Nachdem der Stagingbereitstellungsslot erfolgreich erstellt wurde, müssen Sie nun **Anmeldeinformationen für die Bereitstellung** konfigurieren.

## <a name="create-deployment-credentials"></a>Erstellen von Anmeldeinformationen für die Bereitstellung

In Azure müssen Anmeldeinformationen für die Bereitstellung eingerichtet werden, bevor Sie mit dem eigentlichen Bereitstellungsvorgang beginnen können. Aus diesem Grund lernen Sie, wie Sie Ihre eigenen Anmeldeinformationen für die Bereitstellung erstellen.

1. Klicken Sie im linken Navigationsbereich auf das Menüelement **Anmeldeinformationen für Bereitstellung**.

1. Das Azure-Portal navigiert wie unten gezeigt zum Blatt **Anmeldeinformationen für Bereitstellung**.

    Geben Sie einen **Benutzernamen** und ein **Kennwort** Ihrer Wahl ein, und bestätigen Sie nochmals Ihr Kennwort.

    > [!NOTE]
    > Notieren Sie sich unbedingt Ihren Benutzernamen und das Kennwort, damit Sie beides nicht vergessen! Sie werden diese Informationen später benötigen, wenn wir beginnen, Ihren Code in Azure hochzuladen und bereitzustellen.

    ![Screenshot des Azure-Portals mit dem Blatt „Anmeldeinformationen für die Bereitstellung“ mit Beispielanmeldeinformationen in den erforderlichen Feldern.](../media/7-deployment-credentials.png)

1. Klicken Sie oben auf dem Blatt **Anmeldeinformationen für die Bereitstellung** auf **Speichern**.

Nachdem die Anmeldeinformationen für die Bereitstellung erfolgreich erstellt wurden, müssen Sie nun weitere Bereitstellungsoptionen konfigurieren.

## <a name="use-a-local-git-repository-as-your-deployment-option"></a>Verwenden eines lokalen Git-Repositorys als Ihre Bereitstellungsoption

Als Nächstes erstellen wir ein lokales Git-Repository in Azure, damit Sie mit dem Hochladen Ihres Codes beginnen können.

1. Klicken Sie in der Bereitstellungsslot-Web-App **staging** im linken Navigationsbereich auf das Menüelement **Bereitstellungsoptionen**.

1. Das Azure-Portal navigiert zum Blatt **Bereitstellungsoptionen**.

1. Klicken Sie auf **Quelle auswählen**, um die erforderlichen Einstellungen zu konfigurieren.

1. Im Azure-Portal werden die verfügbaren Optionen angezeigt, die Sie konfigurieren und verwenden können. Wählen Sie in unserem Fall die Option **Lokales Git-Repository** aus.

1. Sie gelangen wieder zum Blatt **Bereitstellungsoption** zurück. Klicken Sie unten auf dem Blatt auf die Schaltfläche **OK**, um die Bereitstellungsquelle zu erstellen.

1. Navigieren Sie jetzt zum Abschnitt **Deployment Center (Preview)** (Bereitstellungscenter (Vorschau)) im linken Navigationsbereich, um die neuen Bereitstellungsdetails anzuzeigen.

    ![Screenshot des Azure-Portals mit dem Blatt „Bereitstellungscenter“ mit dem Git Clone-URI für den hervorgehobenen Slot.](../media/7-staging-after-setting-git.png)

    Die wichtige Information hier, die zu beachten ist, ist der **Git Clone-URI**, bei dem es sich um die URL des lokalen Git-Repositorys handelt, die Sie als **Remote** für Ihr Lokales Webanwendungsrepository verwenden werden.

Nun wird es Zeit, mit dem Hochladen Ihres Codes in den Stagingbereitstellungsslot zu beginnen.

## <a name="install-git-on-your-machine"></a>Installieren von Git auf Ihrem Computer

Installieren Sie Git auf Ihrem Linux-Computer, wenn dies noch nicht geschehen ist.

> [!NOTE]
> Diese Anweisungen beziehen sich auf Ubuntu 18.04, daher können die Schritte zum Installieren von Git für Ihre Distribution und Version abweichen. Suchen Sie in den [Installationsanweisungen für Git unter Linux](https://git-scm.com/download/linux) nach den passenden Schritten.

1. Öffnen Sie ein neues **Terminal**fenster.

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

1. Um zu überprüfen, ob Ihre Daten von Git erfasst wurden, geben Sie den folgenden Befehl ein:

    ```console
    cat ~/.gitconfig
    ```

   Sie sollten Folgendes sehen, einschließlich Ihres Namens und Ihrer E-Mail-Adresse:

    ```console
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-web-app"></a>Initialisieren eines lokalen Git-Repositorys für Ihre Web-App

Um mit der Verwendung von Git zu beginnen, müssen Sie ein lokales Git-Repository für die Web-App initialisieren.

1. Öffnen Sie ein neues **Terminal**fenster.

1. Navigieren Sie zum Inhaltsstammordner der Web-App, die Sie zuvor erstellt hatten. Sie können Folgendes eingeben:

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

1. Stellen Sie alle Web-App-Dateien für Git bereit.

   Der nächste Schritt besteht darin, Git die Existenz Ihrer Web-App-Dateien mitzuteilen. Hierzu fügen Sie alle Dateien des Arbeitsverzeichnisses hinzu, sodass sie von Git **bereitgestellt** werden. Geben Sie den folgenden Befehl ein:

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

Sie haben nun erfolgreich ein neues lokales Git-Repository initialisiert. Außerdem haben Sie alle Ihre Web-App-Dateien an Git committet. Nun müssen Sie lediglich noch ein **Remote**repository hinzufügen, um Ihr lokales Git-Repository mit dem auf Azure gehosteten Repository zu verbinden.

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

Nachdem Ihr lokales Git-Repository nun mit dem Remote-Git-Repository in Azure verbunden ist, werden Sie die App entwickeln und erstellen und anschließend Ihre Web-App mithilfe von Push an Azure übertragen.

1. Geben Sie den folgenden Git-Befehl ein, um Ihren **Haupt**branch mithilfe von Push an das Remote-Git-Repository in Azure zu übertragen:

    ```console
    git push origin master
    ```

1. Sie werden aufgefordert, das Kennwort einzugeben, das Sie im Abschnitt **Anmeldeinformationen für die Bereitstellung** weiter oben konfiguriert haben. Geben Sie Ihr Kennwort ein, und drücken Sie die Eingabetaste. Git beginnt, Ihre Commit-Dateien in das Remote-Git-Repository von Azure hochzuladen, das unter dem Stagingbereitstellungsslot konfiguriert wurde.

## <a name="verify-the-web-app-is-uploaded-to-azure"></a>Überprüfen, ob die Web-App in Azure hochgeladen wird

1. Melden Sie sich beim Azure-Portal an.

1. Klicken Sie im linken Navigationsbereich auf das Menüelement **Alle Ressourcen**.

1. Sie gelangen im Azure-Portal zur Liste aller Ressourcen, die bisher in Azure erstellt wurden.

1. Klicken Sie auf den oben erstellten Stagingslot. Beachten Sie, dass ein Bereitstellungsslot als Web-App angesehen wird. Daher wird er unter **Alle Ressourcen** als Web-App-Ressource angezeigt.

1. Wenn das Blatt „Stagingbereitstellungsslot“ angezeigt wird, wechseln Sie zu **Bereitstellungsoptionen**.

    Sie sehen, dass Ihr erster Commit, der sich lokal auf Ihrem Computer befindet, jetzt in das Azure-Portal hochgeladen wurde.

    Indem Ihr Code lokal mithilfe von Push an das in Azure gehostete Remote-Git-Repository übertragen wurde, hat Azure diesen Vorgang aufgezeichnet.

    Jedes Mal, wenn Sie Ihren Code an Azure übertragen, wird ein neuer Datensatz zusammen mit der Nachricht angezeigt, die Sie eingeben, wenn Sie Ihre Änderungen lokal auf Ihrem Computer committen.

    ![Screenshot des Azure-Portals mit einer kürzlich erfolgten Bereitstellung im Git-Repository auf dem Blatt „Entwicklungsoptionen“.](../media/7-staging-deployment-slot-after-uploading-files.png)

1. Sehen wir uns nun die **Stagingslot**-URL an. Auf die URL wurde bereits oben eingegangen. Sollten Sie jedoch Ihre URL vergessen haben, können Sie stets zur Seite **Übersicht** des Stagingbereitstellungsslots wechseln und von dort die URL übernehmen.

1. Geben Sie die folgende URL in die Adressleiste Ihres Browsers ein: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).

    ![Screenshot einer Webbrowseransicht der Website des Stagingbereitstellungsslots.](../media/7-staging-slot-hosted-online.png)

Sie haben Ihre lokalen Web-App-Dateien erfolgreich in den Stagingbereitstellungsslot in Azure hochgeladen.

## <a name="swapping-the-staging-and-production-deployment-slots"></a>Austauschen von Staging- und Produktionsbereitstellungsslots

Nachdem die Anwendung nun in dem Stagingbereitstellungsslot ausgeführt wird, der in Azure gehostet wird, ist es Zeit, diesen Slot gegen den Produktionsbereitstellungsslot austauschen. Gehen Sie dazu folgendermaßen vor:

1. Navigieren Sie zum Blatt der ursprünglichen Web-App, die Sie früher erstellt haben. Sie finden die ursprüngliche Web-App auf dem Blatt **Alle Ressourcen**.

1. Klicken Sie im linken Navigationsbereich auf das Menüelement **Bereitstellungsslots**.

1. Klicken Sie oben auf dem Blatt auf die Schaltfläche **Austauschen**.

1. Sie gelangen im Azure-Portal zum Blatt **Austauschen**.

1. Wählen Sie für das Feld **Austauschen** die Option **Austauschen** aus.

1. Wählen Sie für das Feld **Quelle** die Option **Staging** aus.

1. Wählen Sie für das Feld **Ziel** die Option **Produktion** aus.

    ![Screenshot des Azure-Portals mit dem Blatt „Austauschen“ des Bereitstellungsslots.](../media/7-swap-blade.png)

1. Klicken Sie am unteren Blattrand auf die Schaltfläche **OK**.

1. Azure beginnt mit dem Austauschprozess. Dieser Vorgang dauert in der Regel einige Sekunden, je nach der Größe der ausgetauschten Web-App.

1. Wechseln Sie nach Abschluss des Vorgangs zur Web-App-URL: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).

    ![Screenshot mit einer Webbrowseransicht des früheren Stagingbereitstellungsslots, der jetzt als primäre Web-App gehostet ist.](../media/7-web-app-page.png)

    Der Austauschvorgang war erfolgreich! Sie sehen nun, dass der Code, den Sie in den Stagingbereitstellungsslot hochgeladen haben, auch im Produktionsslot gehostet wird.

1. Wechseln Sie nun zur URL des Stagingslots: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).

    ![Screenshot mit einer Webbrowseransicht des zuvor primären Bereitstellungsslots, der jetzt als Stagingbereitstellungsslot-Web-App gehostet ist.](../media/7-staging-after-swapping.png)

    Der Stagingbereitstellungsslot enthält jetzt die ursprünglichen Standard-Webanwendungsdateien, die zuvor unter dem Produktionsslot gehostet wurden.

Herzlichen Glückwunsch! Sie haben Ihre Web-App erfolgreich in Azure hochgeladen und die Bereitstellungsslots getauscht.
