In dieser Einheit installieren Sie Visual Studio Code und die Azure App Service-Erweiterung. Dadurch können Sie für Microsoft Azure entwickeln und eine Web-App bereitstellen.

## <a name="exercise-steps"></a>Schritte

Finden Sie zunächst heraus, welches Betriebssystem Sie verwenden, und befolgen Sie die Schritte in den entsprechenden Abschnitten, um Visual Studio Code zu installieren.

### <a name="windows"></a>Windows

1. Laden Sie den Visual Studio Code-Installer für Windows herunter.

1. Führen Sie das Installationsprogramm aus. Die Ausführung wird nicht lange dauern.

1. Öffnen Sie Visual Studio Code, indem Sie zum Installationsordner navigieren (Standardpfad auf einem 64-Bit-Computer: C:\Programme\Microsoft VS Code).

### <a name="macos"></a>macOS

1. Laden Sie Visual Studio Code für macOS herunter.

1. Doppelklicken Sie auf das heruntergeladene Archiv, um den Inhalt zu erweitern.

1. Ziehen Sie „Visual Studio Code.app“ in den Ordner „Programme“. Dadurch wird die Datei im Launchpad verfügbar.

1. Visual Studio Code mit der rechten Maustaste auf das Symbol und die Auswahl der Option Ihrer Dock hinzufügen > im Dock beibehalten.

### <a name="linux--debian-and-ubuntu"></a>Linux – Debian und Ubuntu

1. Herunterladen und Installieren der [Deb-Paket (64-Bit)](https://go.microsoft.com/fwlink/?LinkID=760868) über die grafische Softwarecenter, sofern diese verfügbar ist oder über die Befehlszeile ausführen (ersetzen `<file>` mit dem Deb-Dateinamen, die Sie heruntergeladen haben):

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

### <a name="linux--rhel-fedora-and-centos"></a>Linux – RHEL, Fedora und CentOS

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

### <a name="linux--opensuse-and-sle"></a>Linux – openSUSE und SLE

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
> Weitere Informationen zum Installieren oder Updaten von Visual Studio Code auf den verschiedenen Linux-Distributionen finden Sie in der Dokumentation [Running VS Code on Linux (Ausführen von Visual Studio Code unter Linux)](https://code.visualstudio.com/docs/setup/linux).

## <a name="install-azure-app-service-extension"></a>Installieren der Azure App Service-Erweiterung

Öffnen Sie Visual Studio Code, sobald die Installation abgeschlossen ist.

1. Navigieren Sie zur Registerkarte „Extensions“ (Erweiterungen)

1. Suchen Sie nach „Azure App Service“.

1. Klicken Sie auf „Installieren“.

    Der folgende Screenshot stellt die Azure App Service-Erweiterung dar, die in den Suchergebnissen für Visual Studio Code-Erweiterungen ausgewählt ist.

    ![Screenshot von Visual Studio Code, der die Registerkarte „Erweiterungen“ mit der in den Suchergebnissen hervorgehobenen Azure App Service-Erweiterung darstellt.](../media/3-install-azure-extension.png)

Dadurch wird die Erweiterung installiert. Sie nun können eine Verbindung mit Ihrem Azure-Abonnement, und eine Web-, Mobile oder API-app für Azure App Service bereitstellen.