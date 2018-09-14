
In dieser Übung verwenden Sie die Azure-Befehlszeilenschnittstelle auf Ihrem lokalen Computer zum Erstellen einer Ressourcengruppe und danach, um in dieser Ressourcengruppe eine Web-App bereitzustellen. 

### <a name="steps-to-create-a-resource-group"></a>Schritte zum Erstellen einer Ressourcengruppe
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
1. Optional können Sie bestätigen, dass die Ressource im Azure-Portal erstellt wurde. Öffnen Sie einen Webbrowser, melden Sie sich beim Portal an, und navigieren Sie zum Abschnitt **Ressourcengruppen** (siehe unten). Die neue Ressourcengruppe sollte in der Liste angezeigt werden.

![Auflisten von Ressourcengruppen über das Portal](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a>Schritte zum Erstellen eines Serviceplans
Beim Ausführen von Web-Apps mithilfe von Azure App Service zahlen Sie für die von der App verwendeten Azure-Computeressourcen, die vom Ihren Web-Apps zugeordneten Service-Plan abhängig sind. Servicepläne bestimmen die Region, die für das Rechenzentrum der App, die Anzahl von verwendeten VMs und Tarife verwendet wird.

1. Erstellen Sie einen App Service-Plan, um die App auszuführen. Der Name der App und des Plans muss eindeutig sein. Ändern Sie deshalb die Zeichenfolge „12345“ in eine zufällige Zahl. Der folgende Befehl gibt keinen Tarif oder Details der VM-Instanzen an, weshalb Sie standardmäßig einen **Basic**-Tarif mit einer **kleinen** VM-Instanz erhalten.

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. Überprüfen Sie, ob der Serviceplan erfolgreich erstellt wurde, indem Sie alle Pläne in einer Tabelle auflisten.

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>Schritte zum Erstellen einer Web-App
Als Nächstes erstellen Sie die Web-App in Ihrem Serviceplan. Sie können den Code zur gleichen Zeit bereitstellen, aber in unserem Beispiel machen wir dies in separaten Schritten.

1. Erstellen Sie die Web-App, und ändern Sie die Zeichenfolge „12345“ in die gleiche Zufallszahl, die Sie zuvor verwendet haben.
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. Überprüfen Sie, ob die App erfolgreich erstellt wurde, indem Sie alle Apps in einer Tabelle auflisten.

    ```bash
    az webapp list --output table
    ```

1. Notieren Sie sich den Wert von **DefaultHostName**, da Sie diesen später erneut benötigen.

### <a name="steps-to-deploy-code-from-github"></a>Schritte zum Bereitstellen von Code über GitHub
1. Im letzten Schritt wird Code über ein GitHub-Repository in der Web-App bereitgestellt, und die Zeichenfolge „12345“ wird erneut in die gleiche zuvor verwendete Zufallszahl geändert.
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. Kopieren Sie die folgende URL in einen Browser, um die Web-App anzuzeigen.
http://popupapp12345.azurewebsites.net

1. Auf der Seite wird die Nachricht „HelloWorld!“ angezeigt.

1. Schließen Sie das Browserfenster.

## <a name="summary"></a>Zusammenfassung
In dieser Übung wurde ein typisches Muster für eine interaktive Azure CLI-Sitzung veranschaulicht. Zuerst haben Sie einen Standardbefehl verwendet, um eine neue Ressourcengruppe zu erstellen. Danach haben Sie eine Reihe von Befehlen verwendet, um eine Ressource (in diesem Beispiel eine Web-App) in dieser Ressourcengruppe bereitzustellen. Diese Befehle können einfach in einem Shellskript zusammengefasst und jederzeit ausgeführt werden, wenn Sie die gleiche Ressource erstellen müssen.
