
In dieser Übung verwenden Sie einen der Azure-Befehlszeilenschnittstelle auf Ihrem lokalen Computer zum Erstellen einer Ressourcengruppe aus, und klicken Sie dann auf, um eine Web-App in dieser Ressourcengruppe bereitzustellen. 

### <a name="steps-to-create-a-resource-group"></a>Schritte zum Erstellen einer Ressourcengruppe
1. Öffnen Sie eine Bash-Shell unter Linux oder MacOS, oder öffnen Sie die Eingabeaufforderung oder PowerShell ein, wenn von Windows zu arbeiten.

1. Starten Sie die Azure-Befehlszeilenschnittstelle, und führen Sie den Login-Befehl.

    ```bash
    az login
    ```
    Wenn Sie ein Azure-Registrierung nicht erhalten Seite in Ihrem Webbrowser, folgen Sie den Anweisungen über die Befehlszeile, und geben Sie einen Autorisierungscode an [ https://aka.ms/devicelogin ](https://aka.ms/devicelogin).

1. Erstellen Sie eine Ressourcengruppe.

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. Stellen Sie sicher, dass die Ressourcengruppe erfolgreich erstellt wurde, indem Sie alle Ressourcengruppen in einer Tabelle auflisten.

    ```bash
    az group list --output table
    ```
1. Optional: Überprüfen Sie, dass die Ressource im Azure-Portal erstellt wurde. Öffnen Sie einen Webbrowser, melden Sie sich im Portal, und navigieren Sie zu der **Ressourcengruppen** Abschnitt (siehe unten). Die neue Ressourcengruppe sollte in der Liste angezeigt werden.

![Verwenden des Portals zum Auflisten von Ressourcengruppen](../images/listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a>Schritte zum Erstellen eines Service-Plans
Beim Ausführen von Web-Apps mithilfe des Azure-Apps-Diensts, Zahlen Sie für die Azure Compute-Ressourcen, die von der app verwendet, und dies hängt von der App Service-Plans, der Ihre Web-Apps zugeordnet. Service-Pläne bestimmen Sie die Region für die app-Datencenter, die Anzahl von virtuellen Computern verwendet und Tarif.

1. Erstellen Sie einen App Service-Plan, um die Anwendung auszuführen. Der Name der app und den Plan muss eindeutig sein, so ändern Sie die Zeichenfolge "12345", um eine zufällige Zahl ist. Der folgende Befehl gibt keinen Tarif oder die Details der VM-Instanzen, von Standard, erhalten Sie eine **grundlegende** Plan mit 1 **kleine** VM-Instanz.

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. Stellen Sie sicher, dass der Service-Plan erfolgreich erstellt wurde, indem Sie die Pläne in einer Tabelle auflisten.

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>Schritte zum Erstellen einer Web-app
Als Nächstes erstellen Sie die Web-app in Ihrem Service-Plan. Sie können den Code bereitstellen, zur gleichen Zeit, aber in unserem Beispiel machen wir dies als separater Schritt.

1. Denken Sie daran, die die Zeichenfolge "12345" in der gleichen Zufallszahl zu ändern, die Sie zuvor die Web-app zu erstellen.
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. Stellen Sie sicher, dass die app erfolgreich erstellt wurde, indem Sie alle Ihre apps in einer Tabelle auflisten.

    ```bash
    az webapp list --output table
    ```

1. Notieren Sie sich die **DefaultHostName**, Sie benötigen diesen später noch mal.

### <a name="steps-to-deploy-code-from-github"></a>Schritte zum Bereitstellen von Code über GitHub
1. Der letzte Schritt ist zum Bereitstellen von Code über ein GitHub-Repository in der Web-App erneut Denken Sie daran, die die Zeichenfolge "12345" in der gleichen Zufallszahl zu ändern, die Sie zuvor.
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. Kopieren Sie die folgende Url in einem Browser, um die Web-app finden Sie unter.
http://popupapp12345.azurewebsites.net

1. Die angezeigte Seite "Hello World!"

1. Schließen Sie das Browserfenster.

## <a name="summary"></a>Zusammenfassung
In dieser Übung veranschaulicht ein typisches Muster für eine interaktive Azure CLI-Sitzung. Zuerst verwendet Sie einen standard-Befehl, um eine neue Ressourcengruppe zu erstellen. Danach haben Sie verwendet eine Reihe von Befehlen zum Bereitstellen einer Ressource (in diesem Beispiel eine Web-app) in dieser Ressourcengruppe. Dieser Satz von Befehlen werden einfach in einem Shell-Skript zusammengefasst, und jedes Mal ausgeführt, müssen Sie die gleiche Ressource zu erstellen.
