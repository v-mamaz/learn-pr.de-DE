Um Visual Studio Code für die Azure-Entwicklung verwenden zu können, müssen Sie Visual Studio Code lokal und mindestens eine weitere Azure-Erweiterung installieren. In dieser Übung fügen wir die **Azure App Service**-Erweiterung hinzu.

## <a name="install-visual-studio-code"></a>Installieren von Visual Studio Code

::: zone pivot="windows"

### <a name="windows"></a>Windows

1. [Laden Sie den Visual Studio Code-Installer für Windows herunter.](https://code.visualstudio.com/)

1. Führen Sie das Installationsprogramm aus.

1. Öffnen Sie Visual Studio Code, indem Sie die Windows-Taste drücken oder auf das Windows-Symbol auf der Taskleiste klicken, „Visual Studio Code“ eingeben und auf das Ergebnis **Visual Studio Code** klicken.

::: zone-end

::: zone pivot="macos"

### <a name="macos"></a>macOS

1. [Laden Sie Visual Studio Code für macOS herunter.](https://code.visualstudio.com/)

1. Doppelklicken Sie auf das heruntergeladene Archiv, um den Inhalt zu erweitern.

1. Ziehen Sie „Visual Studio Code.app“ in den Ordner „Programme“.

1. Öffnen Sie Visual Studio Code, indem Sie auf das Symbol im Abschnitt „Apps“ klicken oder nach Visual Studio Code in Spotlight suchen.

::: zone-end

::: zone pivot="linux"

### <a name="linux"></a>Linux 

#### <a name="debian-and-ubuntu"></a>Debian und Ubuntu

1. Laden Sie das [DEB-Paket (64-Bit)](https://go.microsoft.com/fwlink/?LinkID=760868) herunter, und installieren Sie es über das grafische Softwarecenter (falls verfügbar) oder über die Befehlszeile (ersetzen Sie `<file>` durch den Namen der heruntergeladenen DEB-Datei):

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

#### <a name="rhel-fedora-and-centos"></a>RHEL, Fedora und CentOS

1. Verwenden Sie folgendes Skript, um Schlüssel und Repository zu installieren:

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    ```

1. Aktualisieren Sie den Paketcache, und installieren Sie das Paket mithilfe von „dnf“ (Fedora 22 und höher):

    ```bash
    dnf check-update
    sudo dnf install code
    ```

#### <a name="opensuse-and-sle"></a>openSUSE und SLE

1. Das yum-Repository funktioniert ebenfalls für openSUSE- und SLE-basierte Systeme. Mit folgendem Skript werden der Schlüssel und das Repository installiert:

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
    ```

1. Aktualisieren Sie den Paketcache, und installieren Sie das Paket folgendermaßen:

    ```bash
    sudo zypper refresh
    sudo zypper install code
    ```

> [!NOTE]
> Weitere Informationen zum Installieren oder Aktualisieren von Visual Studio Code auf den verschiedenen Linux-Distributionen finden Sie in der Dokumentation [Running Visual Studio Code on Linux (Ausführen von Visual Studio Code unter Linux)](https://code.visualstudio.com/docs/setup/linux).

::: zone-end

## <a name="install-azure-app-service-extension"></a>Installieren der Azure App Service-Erweiterung

1. Öffnen Sie Visual Studio Code, wenn Sie dies noch nicht getan haben.

1. Öffnen Sie den Browser „Erweiterungen“, auf den über das Menü auf der linken Seite zugegriffen werden kann.

1. Suchen Sie nach **Azure App Service**.

1. Wählen Sie das Ergebnis **Azure App Service** aus, und klicken Sie auf **Installieren**.

    Der folgende Screenshot stellt die Azure App Service-Erweiterung dar, die in den Suchergebnissen für Visual Studio Code-Erweiterungen ausgewählt ist.

    ![Screenshot von Visual Studio Code, der die Registerkarte „Erweiterungen“ mit der in den Suchergebnissen hervorgehobenen Azure App Service-Erweiterung darstellt.](../media/3-install-azure-extension.png)

Dadurch wird die Erweiterung installiert. Sie sind nun bereit, eine Verbindung mit Ihrem Azure-Abonnement herzustellen und Web-Apps, mobile Apps oder API-Apps in Azure App Service bereitzustellen.
