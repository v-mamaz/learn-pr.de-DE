
In dieser Übung installieren Sie **Azure PowerShell** auf Ihrem lokalen Computer. Wählen Sie die Schritte für Ihr Betriebssystem aus.

## <a name="install-powershell-core"></a>Installieren von PowerShell Core
Unter Linux und MacOS wird der erste Schritt zum Installieren **PowerShell Core**.

### <a name="linux"></a>Linux
Installieren Sie PowerShell Core auf Ubuntu Linux über das Advanced Packaging Tool (**apt**) und die Bash-Befehlszeile. 

> [!NOTE] Die unten aufgeführten Befehle sind für Ubuntu-Version 18.04. Wenn Sie eine andere Version von Ubuntu verwenden, müssen Sie ein anderes Repository hinzufügen. Weitere Informationen finden Sie [Installieren von PowerShell Core unter Linux](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-powershell-core-on-linux).

1. Importieren Sie den Verschlüsselungsschlüssel für das Microsoft-Ubuntu-Repository. Das Paket dadurch Manager, um sicherzustellen, dass das PowerShell Core-Paket, die, das Sie installieren, von Microsoft stammt.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```
1. Registrieren Sie das Microsoft-Ubuntu-Repository aus, damit das PowerShell Core-Paket mit der Paket-Manager gefunden werden kann.

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

1. Starten Sie PowerShell, um sicherzustellen, dass die It wurde erfolgreich installiert.

    ```bash
    pwsh
    ```

### <a name="macos"></a>macOS
Installieren Sie als Nächstes **PowerShell Core** unter MacOS unter Verwendung der Homebrew-Paket-Manager.

> [!IMPORTANT] Wenn die **brew** Befehl nicht verfügbar ist, müssen Sie möglicherweise die Homebrew-Paket-Manager zu installieren. Weitere Informationen finden Sie die [Homebrew-Website](https://brew.sh/).

1. Installieren Sie Homebrew-Cask, um weitere Pakete, sowie das PowerShell Core-Paket zu erhalten:

    ```bash
    brew tap caskroom/cask
    ```
1. Installieren Sie PowerShell Core:

    ```bash
    brew cask install powershell
    ```

1. Starten Sie PowerShell Core, um sicherzustellen, dass die It wurde erfolgreich installiert:

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a>Installieren von Azure Powershell
Nach der Installation der Basis **PowerShell** Produkt installieren **Azure PowerShell** , die Azure-spezifischen Befehle hinzuzufügen.

### <a name="windows"></a>Windows
Installieren Sie Azure PowerShell zur Verwendung von Windows die **Install-Module** PowerShell-Befehl.

> [!IMPORTANT] Sie müssen PowerShell, Version 5.0 oder höher zum Installieren von Azure PowerShell verfügen. Um Ihre Version von PowerShell zu überprüfen, verwenden Sie den folgenden Befehl aus: 
>
> `$PSVersionTable.PSVersion` 
>
>Wenn die Versionsnummer niedriger als 5.0 ist, finden Sie unter [Aktualisieren von vorhandenen Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).

1. Öffnen der **starten** integrierten **Windows PowerShell**.
1. Mit der rechten Maustaste die **Windows PowerShell** Symbol, und wählen **als Administrator ausführen**.
1. In der **User Account Control** wählen Sie im Dialogfeld **Ja**.
1. Geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE:

    ```powershell
    Install-Module -Name AzureRM
    ```
1. Wenn Sie aufgefordert werden, ob Sie Module aus PSGallery vertrauen, beantworten **Ja** oder **Ja, alle**.

### <a name="linux-or-macos"></a>Linux oder macOS
Installieren Sie Azure PowerShell unter Linux oder MacOS verwenden, die **Install-Module** PowerShell-Befehl. Das Verfahren ist für beide Betriebssysteme gleich.

1. Geben Sie in einem Terminal den folgenden Befehl zum Starten von PowerShell Core mit erhöhten Rechten aus.

    ```bash
    sudo pwsh
    ```

1. Führen Sie den folgenden Befehl an der Eingabeaufforderung PowerShell Core, Azure PowerShell installieren.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. Wenn Sie aufgefordert werden, ob Sie Module aus vertrauen **PSGallery**, Antwort **Ja** oder **Ja, alle**.

## <a name="summary"></a>Zusammenfassung
Sie richten Sie Ihre lokalen Computer zum Azure-Ressourcen mit Azure PowerShell verwalten. Sie können nun Azure PowerShell lokal verwenden, geben Befehle oder Skripts ausführen. Azure PowerShell wird Ihre Befehle aus, um den Azure-Rechenzentren weitergeleitet, wo sie in Ihrem Azure-Abonnement ausgeführt werden sollen.