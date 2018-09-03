In dieser Übung installieren Sie **Azure PowerShell** auf Ihrem lokalen Computer. Wählen Sie den entsprechenden Abschnitt für Ihr Betriebssystem.

## <a name="linux-and-mac"></a>Linux und Mac
Unter Linux und macOS besteht der erste Schritt darin, **PowerShell Core** zu installieren.

### <a name="linux"></a>Linux
Wie in der letzten Übungseinheit erläutert, wird PowerShell für Linux über einen Paket-Manager installiert. Wir verwenden für dieses Beispiel **Ubuntu 18.04**. [Detaillierte Anweisungen für andere Versionen und Distributionen finden Sie in unserer Dokumentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).

Sie installieren PowerShell Core unter Ubuntu Linux mit dem Advanced Packaging Tool (**apt**) und der Bash-Befehlszeile. 

1. Importieren Sie den Verschlüsselungsschlüssel für das Microsoft Ubuntu-Repository. So kann der Paket-Manager sicherstellen, dass das PowerShell Core-Paket, das Sie installieren, wirklich von Microsoft stammt.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Registrieren Sie das **Microsoft Ubuntu-Repository**, sodass der Paket-Manager das PowerShell Core-Paket finden kann.

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. Aktualisieren Sie die Liste der Pakete.

    ```bash
    sudo apt-get update
    ```

1. Installieren Sie PowerShell Core.

    ```bash
    sudo apt-get install -y powershell
    ```

1. Starten Sie PowerShell, um sicherzustellen, dass es erfolgreich installiert wurde.

    ```bash
    pwsh
    ```

### <a name="macos"></a>macOS
Installieren Sie als Nächstes **PowerShell Core** mit dem Homebrew-Paket-Manager unter macOS.

> [!IMPORTANT]
> Wenn der Befehl **brew** nicht verfügbar ist, müssen Sie möglicherweise den Homebrew-Paket-Manager installieren. Informationen dazu finden Sie auf der [Website von Homebrew](https://brew.sh/).

1. Installieren Sie „Homebrew-Cask“, um weitere Pakete abzurufen, einschließlich des PowerShell Core-Pakets:

    ```bash
    brew tap caskroom/cask
    ```
1. Installieren von PowerShell Core:

    ```bash
    brew cask installs powershell
    ```

1. Starten Sie PowerShell Core, um sicherzustellen, dass es erfolgreich installiert wurde:

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a>Installieren von Azure PowerShell
Installieren Sie nach dem **PowerShell**-Basisprodukt **Azure PowerShell**, um die Azure-spezifischen Befehle zu installieren.

### <a name="windows"></a>Windows
Installieren Sie Azure PowerShell unter Windows mit dem PowerShell-Befehl „`Install-Module`“.

> [!IMPORTANT]
> Für die Installation von Azure PowerShell benötigen Sie PowerShell Version 5.0 oder höher. Um Ihre PowerShell-Version zu überprüfen, verwenden Sie folgenden Befehl: 
>
> `$PSVersionTable.PSVersion` 
>
>Wenn die Versionsnummer niedriger ist als 5.0, befolgen Sie die Anweisungen zum [Durchführen eines Upgrades einer vorhandenen Windows PowerShell-Version](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).

1. Öffnen Sie das **Startmenü**, und geben Sie **Windows PowerShell** ein.
2. Klicken Sie mit der rechten Maustaste auf das Symbol **Windows PowerShell**, und wählen Sie **Als Administrator ausführen** aus.
3. Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.
4. Geben Sie den folgenden Befehl ein, und drücken Sie die Eingabetaste:

    ```powershell
    Install-Module -Name AzureRM
    ```
5. Wenn Sie gefragt werden, ob Sie Modulen von PSGallery vertrauen, antworten Sie **Ja** oder **Ja, allen**.

> [!NOTE]
> Wenn Sie in einer Fehlermeldung darauf hingewiesen werden, dass bereits eine Version des Azure PowerShell-Moduls installiert ist, können Sie diese mit dem folgenden Befehl auf die _neueste_ Version aktualisieren:
> 
> `Update-Module -Name AzureRM`
> 
> Antworten Sie ebenso wie beim `Install-Module`-Befehl auf die Frage, ob Sie dem Modul vertrauen, mit **Ja** oder **Ja, alle**.

### <a name="linux-or-macos"></a>Linux oder macOS
Zum Installieren von Azure PowerShell unter Linux oder macOS verwenden wir das gleiche grundlegende Verfahren. Das Procedere ist für beide Betriebssysteme gleich. Der Unterschied besteht darin, eine PowerShell Core-Sitzung mit erhöhten Rechten zu starten.

1. Geben Sie auf einem Terminal den folgenden Befehl ein, um PowerShell Core mit erhöhten Rechten zu starten.

    ```bash
    sudo pwsh
    ```

1. Um Azure PowerShell zu installieren, führen Sie an der PowerShell Core-Eingabeaufforderung den folgenden Befehl aus.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. Wenn Sie gefragt werden, ob Sie Modulen von **PSGallery** vertrauen, antworten Sie **Ja** oder **Ja, alle**.

## <a name="summary"></a>Zusammenfassung
Sie haben Ihre(n) lokalen Computer für die Verwaltung von Azure-Ressourcen mithilfe von Azure PowerShell eingerichtet. Sie können Azure PowerShell jetzt lokal zum Eingeben von Befehlen oder Ausführen von Skripts verwenden. Azure PowerShell leitet Ihre Befehle an die Azure-Rechenzentren weiter, wo sie in Ihren Azure-Abonnements ausgeführt werden.
