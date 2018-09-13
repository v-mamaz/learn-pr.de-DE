Als Nächstes verwenden Sie Azure CLI zum Erstellen einer Ressourcengruppe und anschließend zum Bereitstellen einer Web-App in dieser Ressourcengruppe. 

### <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

1. Öffnen Sie eine Bash-Shell unter Linux oder macOS, oder öffnen Sie das Fenster „Eingabeaufforderung“ oder PowerShell, wenn Sie unter Windows arbeiten.

1. Starten Sie die Azure-Befehlszeilenschnittstelle, und führen Sie den Anmeldebefehl aus.

    ```bash
    az login
    ```
    Wenn sich in Ihrem Webbrowser keine Azure-Anmeldeseite öffnet, befolgen Sie die Befehlszeilenanweisungen, und geben Sie unter [https://aka.ms/devicelogin](https://aka.ms/devicelogin) einen Autorisierungscode ein.

1. Erstellen Sie eine Ressourcengruppe.

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. Überprüfen Sie, ob die Ressourcengruppe erfolgreich erstellt wurde, indem Sie alle Ressourcengruppen in einer Tabelle auflisten.

    ```bash
    az group list --output table
    ```

> [!TIP]
> Sie können auch im Azure-Portal überprüfen, ob die Ressource erstellt wurde. Öffnen Sie einen Webbrowser, melden Sie sich beim Portal an, und navigieren Sie zum Abschnitt **Ressourcengruppen**. Die neue Ressourcengruppe sollte in der Liste angezeigt werden.

1. Wenn Sie über viele Elemente in der Gruppe verfügen, können Sie nach den Rückgabewerten filtern, indem Sie eine `--query`-Option hinzufügen. Testen Sie den folgenden Befehl:

    ```bash
    az group list --query '[?name == popupResGroup]'
    ```

    Die Abfrage wird mit **JMESPath** formatiert, was eine standardmäßige Abfragesprache für JSON-Abfragen ist. Weitere Informationen über diese leistungsstarke Filtersprache finden Sie unter <http://jmespath.org/>. Im Modul **Verwalten von virtuellen Computern mit Azure CLI** werden Abfragen ausführlicher behandelt.

### <a name="steps-to-create-a-service-plan"></a>Schritte zum Erstellen eines Serviceplans

Beim Ausführen von Web-Apps mithilfe von Azure App Service zahlen Sie für die von der App verwendeten Azure-Computeressourcen, die vom Ihren Web-Apps zugeordneten Service-Plan abhängig sind. Servicepläne bestimmen die Region, die für das Rechenzentrum der App, die Anzahl von verwendeten VMs und Tarife verwendet wird.

1. Erstellen Sie einen App Service-Plan, um die App auszuführen. Der folgende Befehl gibt weder Tarif noch Details der VM-Instanzen an, weshalb Sie standardmäßig einen **Basic**-Tarif mit einer **kleinen** VM-Instanz erhalten.

    > [!WARNING]
    > Die Namen der App und des Plans müssen _eindeutig_ sein, fügen Sie den Namen also ein Suffix hinzu, und ersetzen Sie den `<unique>`-Text im folgenden Befehl mit einer Reihe von Zahlen, Ihren Initialen oder einem anderen Text, um sicherzustellen, dass der Name im gesamten Umfang von Azure eindeutig ist. 

    ```bash
    az appservice plan create --name popupapp-<unique> --resource-group popupResGroup --location westeurope
    ```

1. Überprüfen Sie, ob der Serviceplan erfolgreich erstellt wurde, indem Sie alle Pläne in einer Tabelle auflisten.

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>Schritte zum Erstellen einer Web-App

Als Nächstes erstellen Sie die Web-App in Ihrem Serviceplan. Sie können den Code zur gleichen Zeit bereitstellen, in diesem Beispiel wird dies jedoch in separaten Schritten durchgeführt.

1. Erstellen Sie die Web-App, und geben Sie den Namen des zuvor erstellten Plans an. **Der Name der App muss wie der des Plans eindeutig sein. Ersetzen Sie den Marker `<unique>` durch Text, damit der Name global eindeutig ist.**
    ```bash
    az webapp create --name popupapp-<unique> --resource-group popupResGroup --plan popupapp-<unique>
    ```

1. Überprüfen Sie, ob die App erfolgreich erstellt wurde, indem Sie alle Apps in einer Tabelle auflisten.

    ```bash
    az webapp list --output table
    ```

1. Notieren Sie sich den Wert von **DefaultHostName**, da Sie diesen später erneut benötigen.

### <a name="steps-to-deploy-code-from-github"></a>Schritte zum Bereitstellen von Code über GitHub

1. Der letzte Schritt besteht im Bereitstellen von Code über ein GitHub-Repository in die Web-App. Sie verwenden hierzu eine einfache PHP-Seite, die im GitHub-Repository „Azure Samples“ verfügbar ist und „HelloWorld!“ anzeigt, wenn sie ausgeführt wird. Stellen Sie sicher, dass Sie den Namen der Web-App verwenden, die Sie erstellt haben.

    ```bash
    az webapp deployment source config --name popupapp-<unique> --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. Nach der Bereitstellung wird Ihre Website von Azure über den eindeutigen App-Namen in der `azurewebsites.net`-Domäne zur Verfügung gestellt. Wenn der Name beispielsweise „popupapp-mslearn123“ wäre, würde die Adresse der Website wie folgt aussehen: <http://popupapp-mslearn123.azurewebsites.net>. Sie müssen die richtige URL eingeben, um die spezifische Instanz zu erreichen.

1. Auf der Seite wird die Nachricht „HelloWorld!“ angezeigt.

1. Schließen Sie das Browserfenster.

## <a name="summary"></a>Zusammenfassung

In dieser Übung wurde ein typisches Muster für eine interaktive Azure CLI-Sitzung veranschaulicht. Zuerst haben Sie einen Standardbefehl verwendet, um eine neue Ressourcengruppe zu erstellen. Danach haben Sie eine Reihe von Befehlen verwendet, um eine Ressource (in diesem Beispiel eine Web-App) in dieser Ressourcengruppe bereitzustellen. Diese Befehle können einfach in einem Shellskript zusammengefasst und jederzeit ausgeführt werden, wenn Sie die gleiche Ressource erstellen müssen.
