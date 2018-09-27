Als Nächstes verwenden wir die Azure-Befehlszeilenschnittstelle, um eine Ressourcengruppe zu erstellen und anschließend eine Web-App in dieser Ressourcengruppe bereitzustellen.

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="using-a-resource-group"></a>Verwenden einer Ressourcengruppe

Wenn Sie Ihren eigenen Computer und Ihr eigenes Azure-Abonnement verwenden, müssen Sie sich zuerst mithilfe des `az login`-Befehls bei Azure anmelden. Mit der Cloud Shell-Umgebung ist dies nicht erforderlich.

Als Nächstes würden Sie normalerweise mit einem Befehl vom Typ `az group create` eine Ressourcengruppe für alle Ihre verwandten Azure-Ressourcen erstellen. Für diese Übungen wurde aber bereits eine Ressourcengruppe für Sie erstellt. Verwenden Sie **<rgn>[Name der Sandboxressourcengruppe]</rgn>** für Ihre Ressourcengruppe.

1. Mithilfe der Azure-Befehlszeilenschnittstelle können Sie alle Ihre Ressourcengruppen in einer Tabelle auflisten. Es sollte eine Ressourcengruppe vorhanden sein, wenn Sie die kostenlose Azure-Sandbox verwenden.

    ```azurecli
    az group list --output table
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. Im Zuge der Azure-Entwicklung können nach und nach mehrere Ressourcengruppen zusammenkommen. Falls die Gruppenliste mehrere Elemente enthält, können Sie die Rückgabewerte filtern, indem Sie eine Option vom Typ `--query` hinzufügen. Verwenden Sie den folgenden Befehl:

    ```azurecli
    az group list --query "[?name == '<rgn>[sandbox resource group name]</rgn>']"
    ```

    Die Abfrage wird mit **JMESPath** (einer Standardabfragesprache für JSON-Abfragen) formatiert. Weitere Informationen zu dieser leistungsstarken Filtersprache finden Sie unter <http://jmespath.org/>. Im Modul **Verwalten von virtuellen Computern mit Azure CLI** werden Abfragen ausführlicher behandelt.

### <a name="steps-to-create-a-service-plan"></a>Schritte zum Erstellen eines Serviceplans

Beim Ausführen von Web-Apps mithilfe von Azure App Service zahlen Sie für die von der App verwendeten Azure-Computeressourcen, die vom Ihren Web-Apps zugeordneten Service-Plan abhängig sind. Servicepläne bestimmen die Region, die für das Rechenzentrum der App, die Anzahl von verwendeten VMs und Tarife verwendet wird.

1. Erstellen Sie einen App Service-Plan, um die App auszuführen. Der folgende Befehl gibt weder Tarif noch Details der VM-Instanzen an, weshalb Sie standardmäßig einen **Basic**-Tarif mit einer **kleinen** VM-Instanz erhalten.

    > [!WARNING]
    > Der Name der App und des Plans muss _eindeutig_ sein. Fügen Sie dem Namen also ein Suffix hinzu, und ersetzen Sie den Text `<unique>` im folgenden Befehl durch eine Reihe von Zahlen, Ihre Initialen oder anderen Text, um sicherzustellen, dass der Name in Azure eindeutig ist.

    Verwenden Sie für den `--location`-Parameter einen der folgenden Standortwerte.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    az appservice plan create --name popupappplan-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --location <location>
    ```

    Die Ausführung dieses Befehls kann mehrere Minuten dauern.

1. Überprüfen Sie, ob der Serviceplan erfolgreich erstellt wurde, indem Sie alle Pläne in einer Tabelle auflisten.

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>Schritte zum Erstellen einer Web-App

Als Nächstes erstellen Sie die Web-App in Ihrem Serviceplan. Sie können den Code zur gleichen Zeit bereitstellen, in diesem Beispiel wird dies jedoch in separaten Schritten durchgeführt.

1. Erstellen Sie die Web-App, und geben Sie den Namen des zuvor erstellten Plans an. **Der Name der App muss wie der des Plans eindeutig sein.** Ersetzen Sie den `<unique>`-Marker durch Text, damit der Name global eindeutig ist.

    ```azurecli
    az webapp create --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --plan popupappplan-<unique>
    ```

1. Überprüfen Sie, ob die App erfolgreich erstellt wurde, indem Sie alle Apps in einer Tabelle auflisten.

    ```azurecli
    az webapp list --output table
    ```

1. Notieren Sie sich den Wert von **DefaultHostName** in der Tabelle. Dies ist die erreichbare Webadresse der neuen Website. Ihre Website wird von Azure über den eindeutigen App-Namen in der `azurewebsites.net`-Domäne zur Verfügung gestellt. Wenn der Name beispielsweise „popupwebapp-mslearn123“ wäre, würde die Website-URL wie folgt aussehen: `http://popupwebapp-mslearn123.azurewebsites.net`.

1. Ihre Website verfügt über die Seite "QuickStart", die von Azure erstellt wurde und die Sie entweder in einem Browser oder mit cURL anzeigen können, indem Sie **DefaultHostName** verwenden.

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
### <a name="steps-to-deploy-code-from-github"></a>Schritte zum Bereitstellen von Code über GitHub

1. Der letzte Schritt besteht im Bereitstellen von Code über ein GitHub-Repository in die Web-App. Sie verwenden hierzu eine einfache PHP-Seite, die im GitHub-Repository „Azure Samples“ verfügbar ist und „HelloWorld!“ anzeigt, wenn sie ausgeführt wird. Stellen Sie sicher, dass Sie den Namen der Web-App verwenden, die Sie erstellt haben.

    ```azurecli
    az webapp deployment source config --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. Besuchen Sie Ihre Website nach der Bereitstellung erneut über einen Browser oder cURL.

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
    Auf der Seite wird die Nachricht „Hello World!“ angezeigt.

    ```output
    Hello World!
    ```

In dieser Übung wurde ein typisches Muster für eine interaktive Azure CLI-Sitzung gezeigt. Zuerst haben Sie einen Standardbefehl verwendet, um eine neue Ressourcengruppe zu erstellen. Danach haben Sie eine Reihe von Befehlen verwendet, um eine Ressource (in diesem Beispiel eine Web-App) in dieser Ressourcengruppe bereitzustellen. Diese Befehle können einfach in einem Shellskript zusammengefasst und jederzeit ausgeführt werden, wenn Sie die gleiche Ressource erstellen müssen.