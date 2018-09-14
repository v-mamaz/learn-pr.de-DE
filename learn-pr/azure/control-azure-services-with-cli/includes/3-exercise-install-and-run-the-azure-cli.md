Installieren Sie die Azure CLI auf Ihrem lokalen Computer, und führen Sie dann einen einfachen Befehl aus, um die Installation zu überprüfen. Mit welcher Methode Sie die Azure CLI installieren, hängt vom Betriebssystem Ihres Computers ab. Wählen Sie die entsprechenden Schritte für Ihr Betriebssystem aus.

> [!NOTE]
> In dieser Übung lernen Sie die lokale Installation des Azure CLI-Tools kennen. Im restlichen Teil des Moduls verwenden Sie die Azure Cloud Shell, sodass Sie die kostenlose Abonnementsupport in Microsoft Learn nutzen können. Sie können diese Übung als optionale Aktivität betrachten und ggf. nur die Anweisungen lesen.

::: zone pivot="linux"

### <a name="linux"></a>Linux

Hier installieren Sie die Azure CLI unter **Ubuntu Linux** mit dem Advanced Packaging Tool (**apt**) und der Bash-Befehlszeile.

> [!TIP]
> Die unten aufgeführten Befehle gelten für Ubuntu-Version 18.04. Für andere Versionen und Distributionen von Linux gelten andere Anweisungen. Falls Sie eine andere Linux-Version verwenden, finden Sie entsprechende Informationen in der [offiziellen Dokumentation](https://docs.microsoft.com/cli/azure/install-azure-cli).

1. Bearbeiten Sie Ihre Quellenliste, sodass das Microsoft-Repository registriert wird und der Paket-Manager das Azure CLI-Paket ermitteln kann.

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

1. Importieren Sie den Verschlüsselungsschlüssel für das Microsoft Ubuntu-Repository. So kann der Paket-Manager sicherstellen, dass das Azure CLI-Paket, das Sie installieren, wirklich von Microsoft stammt.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. Installieren Sie die Azure CLI.

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

::: zone-end

::: zone pivot="macos"

### <a name="macos"></a>macOS

Hier installieren Sie die Azure CLI mit dem Homebrew-Paket-Manager unter macOS.

> [!IMPORTANT]
> Wenn der Befehl **brew** nicht verfügbar ist, müssen Sie möglicherweise den Homebrew-Paket-Manager installieren. Informationen dazu finden Sie auf der [Website von Homebrew](https://brew.sh/).

1. Aktualisieren Sie Ihr brew-Repository, um sicherzustellen, dass Sie das neueste Azure CLI-Paket abrufen.

    ```bash
    brew update
    ```

1. Installieren Sie die Azure CLI.

    ```bash
    brew install azure-cli
    ```

::: zone-end

::: zone pivot="windows"

### <a name="windows"></a>Windows

Hier installieren Sie die Azure CLI mit dem Microsoft Installer (MSI) unter Windows.

1. Wechseln Sie zu „[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)“, und klicken Sie im Sicherheitsdialogfeld des Browsers auf **Ausführen**.
1. Akzeptieren Sie die Lizenzbedingungen im Installer, und klicken Sie dann auf **Installieren**.
1. Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.

::: zone-end

## <a name="running-the-azure-cli"></a>Ausführen der Azure CLI

Unter Linux und macOS führen Sie die Azure CLI aus, indem Sie eine Bash-Shell öffnen. Unter Windows führen Sie die CLI von der Eingabeaufforderung oder über PowerShell aus.

1. Starten Sie die Azure CLI, und überprüfen Sie Ihre Installation, indem Sie die Versionsprüfung ausführen.

    ```azurecli
    az --version
    ```

::: zone pivot="windows"

> [!TIP]
> Die Ausführung der Azure CLI über PowerShell bietet im Vergleich zur Ausführung der Azure CLI über die Windows-Eingabeaufforderung einige Vorteile. Zusätzlich zu den in der Eingabeaufforderung verfügbaren Features stellt PowerShell weitere Features zur Vervollständigung mit der TAB-Taste zur Verfügung. 

::: zone-end

## <a name="summary"></a>Zusammenfassung

Sie richten Ihre lokalen Computer für die Verwaltung von Azure-Ressourcen mithilfe der Azure CLI ein. Sie können die Azure CLI jetzt lokal verwenden, um Befehle einzugeben oder Skripts auszuführen. Die Azure CLI leitet Ihre Befehle an die Azure-Rechenzentren weiter, wo sie in Ihren Azure-Abonnements ausgeführt werden.