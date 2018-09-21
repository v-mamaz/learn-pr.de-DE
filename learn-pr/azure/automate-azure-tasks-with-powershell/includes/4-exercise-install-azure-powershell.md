In dieser Einheit installieren Sie **Azure PowerShell** auf Ihrem lokalen Computer.

> [!NOTE]
> Diese Übung führt Sie durch die lokale Installation der PowerShell-Tools. Im restlichen Teil des Moduls verwenden Sie Azure Cloud Shell, um den kostenlosen Abonnementsupport in Microsoft Learn nutzen zu können. Sie können diese Übung als optionale Aktivität betrachten und ggf. nur die Anweisungen lesen.

::: zone pivot="linux"

## <a name="linux"></a>Linux

PowerShell für Linux wird über einen Paket-Manager installiert. Wir verwenden für dieses Beispiel **Ubuntu 18.04**. [Detaillierte Anweisungen für andere Versionen und Distributionen finden Sie in unserer Dokumentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).

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

1. Starten Sie PowerShell, um sich zu vergewissern, dass es erfolgreich installiert wurde.

    ```bash
    pwsh
    ```
::: zone-end

::: zone pivot="macos"

## <a name="macos"></a>macOS

Unter macOS muss zunächst **PowerShell Core** installiert werden. Hierzu wird der Homebrew-Paket-Manager verwendet.

> [!IMPORTANT]
> Sollte der Befehl **brew** nicht verfügbar sein, müssen Sie möglicherweise den Homebrew-Paket-Manager installieren. Informationen dazu finden Sie auf der [Website von Homebrew](https://brew.sh/).

1. Installieren Sie „Homebrew-Cask“, um weitere Pakete abzurufen, einschließlich des PowerShell Core-Pakets:

    ```bash
    brew tap caskroom/cask
    ```

1. Installieren von PowerShell Core:

    ```bash
    brew cask install powershell
    ```

1. Starten Sie PowerShell Core, um sich zu vergewissern, dass es erfolgreich installiert wurde:

    ```bash
    pwsh
    ```

::: zone-end

::: zone pivot="windows"

## <a name="windows"></a>Windows
PowerShell ist in Windows enthalten. Es ist jedoch möglicherweise ein Update für Ihren Computer verfügbar. Für den Azure-Support, den wir verwenden möchten, benötigen wir mindestens PowerShell 5.0. Die installierte Version können Sie wie folgt ermitteln:

1. Öffnen Sie das **Startmenü**, und geben Sie **Windows PowerShell** ein. Unter Umständen stehen mehrere Verknüpfungslinks zur Verfügung:
    - Windows PowerShell: Dies ist die 64-Bit-Version und in der Regel die Option, die Sie auswählen sollten.
    - Windows PowerShell (x86): Dies ist eine 32-Bit-Version, die unter Windows mit 64 Bit installiert ist.
    - Windows PowerShell ISE: Integrated Scripting Environment (ISE) dient zum Schreiben von Skripts in PowerShell. 
    - Windows PowerShell ISE (x86): Eine 32-Bit-Version von ISE.

1. Klicken Sie auf das Windows PowerShell-Symbol.

1. Geben Sie den folgenden Befehl ein, um die installierte PowerShell-Version zu ermitteln.

    ```powershell
    $PSVersionTable.PSVersion
    ```
    
Ist die Versionsnummer niedriger als 5.0, führen Sie die Schritte zum [Upgraden einer vorhandenen Windows PowerShell-Instanz](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell) aus.

::: zone-end

Sie haben die Unterstützung von PowerShell für Ihre lokalen Computer eingerichtet. Als Nächstes beschäftigen wir uns mit zusätzlichen Befehlen, die Sie hinzufügen können (einschließlich des Azure-Moduls).