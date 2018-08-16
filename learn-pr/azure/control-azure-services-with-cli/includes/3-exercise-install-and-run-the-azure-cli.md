
Sie werden in dieser Übung installieren Azure-Befehlszeilenschnittstelle auf Ihrem lokalen Computer und führen Sie dann einen einfachen Befehl für Ihre Installation zu überprüfen. 

## <a name="installing-the-azure-cli"></a>Installieren der Azure-Befehlszeilenschnittstelle
Die Methode, die Sie für die Installation der Azure-Befehlszeilenschnittstelle verwenden, hängt von das Betriebssystem des Computers ab. Wählen Sie die Schritte für Ihr Betriebssystem aus.

### <a name="linux"></a> Linux
Hier installieren Sie Azure-Befehlszeilenschnittstelle unter Ubuntu Linux über das Advanced Packaging Tool (**apt**) und die Bash-Befehlszeile.

> [!NOTE] Die unten aufgeführten Befehle sind für Ubuntu-Version 18.04. Wenn Sie eine andere Version von Ubuntu verwenden, müssen Sie ein anderes Repository hinzufügen. Weitere Informationen finden Sie [Installieren der Azure CLI 2.0 mit apt](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt).

1. Ändern Sie die Quellenliste, sodass das Microsoft-Repository registriert ist und der Paket-Manager kann das Azure-CLI-Paket suchen.

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```
1. Importieren Sie den Verschlüsselungsschlüssel für das Microsoft-Ubuntu-Repository. Das Paket dadurch Manager, um sicherzustellen, dass das Azure-CLI-Paket, die, das Sie installieren, von Microsoft stammt.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Installieren der Azure CLI.

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

### <a name="macos"></a>macOS
Hier installieren Sie Azure CLI unter MacOS unter Verwendung der Homebrew-Paket-Manager.

> [!IMPORTANT] Wenn die **brew** Befehl nicht verfügbar ist, müssen Sie möglicherweise die Homebrew-Paket-Manager zu installieren. Weitere Informationen finden Sie die [Homebrew-Website](https://brew.sh/).

1. Aktualisieren Sie Ihre Brew-Repository, um sicherzustellen, dass Sie das neueste Azure CLI-Paket erhalten.

    ```bash
    brew update
    ```
1. Installieren der Azure CLI.

    ```bash
    brew install azure-cli
    ```

### <a name="windows"></a> Windows
Hier installieren Sie Azure-Befehlszeilenschnittstelle für Windows, die mit dem MSI-Installer.

1. Wechseln Sie zu [ https://aka.ms/installazurecliwindows ](https://aka.ms/installazurecliwindows), und klicken Sie in das Dialogfeld Sicherheit Browser auf **ausführen**.
1. Im Installationsprogramm akzeptiere die Lizenzbedingungen, und klicken Sie dann auf **installieren**.
1. In der **User Account Control** wählen Sie im Dialogfeld **Ja**.

## <a name="running-the-azure-cli"></a>Der Azure CLI
Sie haben die Azure CLI ausführen, durch Öffnen einer Bash-Shell (Linux und MacOS) oder über die Eingabeaufforderung oder PowerShell (Windows).

1. Starten Sie die Azure-Befehlszeilenschnittstelle, und überprüfen Sie die Installation, indem Sie die Überprüfung der Version ausführen.

    ```bash
    az --version
    ```

> [!NOTE] In Windows hat das Ausführen der Azure-Befehlszeilenschnittstelle über PowerShell einige Vorteile gegenüber der Azure-Befehlszeilenschnittstelle ausführen, an der Eingabeaufforderung aus; Beispielsweise bietet PowerShell zusätzliche Registerkarte Abschluss Features im Vergleich zu, von der Befehlszeile aus. 

## <a name="summary"></a>Zusammenfassung
Sie richten Sie Ihre lokalen Computer zum Verwalten von Azure-Ressourcen mit Azure-Befehlszeilenschnittstelle. Sie können jetzt Azure CLI lokal verwenden, geben Befehle oder Skripts ausführen. Azure-Befehlszeilenschnittstelle wird Ihre Befehle aus, um den Azure-Rechenzentren weitergeleitet, wo sie in Ihrem Azure-Abonnement ausgeführt werden sollen.
