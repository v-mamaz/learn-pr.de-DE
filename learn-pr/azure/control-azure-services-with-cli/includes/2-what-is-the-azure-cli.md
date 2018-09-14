Die Azure CLI ist ein Befehlszeilenprogramm, über das Sie eine Verbindung mit Azure herstellen und Verwaltungsbefehle für Azure-Ressourcen ausführen können. Die Azure CLI wird unter Linux, macOS und Windows ausgeführt und ermöglicht es Administratoren und Entwicklern, ihre Befehle über ein Terminal oder eine Eingabeaufforderung (oder ein Skript) anstelle eines Webbrowsers auszuführen. Zum Neustarten einer VM würden Sie beispielsweise einen Befehl wie den folgenden verwenden:

 ```azurecli
 az vm restart -g MyResourceGroup -n MyVm
 ```

Die Azure CLI bietet plattformübergreifende Befehlszeilentools zum Verwalten von Azure-Ressourcen. Sie kann lokal auf Linux-, Mac- und Windows-Computern installiert werden. Die Azure CLI kann mit Azure Cloud Shell auch über Browser verwendet werden. In beiden Fällen kann sie interaktiv oder mit Skripts verwendet werden. Bei der interaktiven Nutzung starten Sie zunächst eine Shell wie cmd.exe unter Windows oder Bash unter Linux oder macOS, und geben Sie dann den Befehl bei der Eingabeaufforderung der Shell ein. Um sich wiederholende Aufgaben zu automatisieren, stellen Sie die CLI-Befehle mit der Syntax Ihrer ausgewählten Shell in einem Shellskript zusammen und führen dieses Skript dann aus.

## <a name="how-to-install-azure-cli"></a>Installieren der Azure CLI

Verwenden Sie unter Linux und macOS einen Paket-Manager, um PowerShell Core zu installieren. Der empfohlene Paket-Manager unterscheidet sich je nach Betriebssystem und Distribution:
- Linux: **apt-get** unter Ubuntu, **yum** unter Red Hat und **zypper** unter OpenSUSE
- Mac: **Homebrew**

Die Azure CLI ist im Microsoft-Repository verfügbar, sodass Sie zuerst dieses Repository dem Paket-Manager hinzufügen müssen.

Installieren Sie die Azure CLI unter Windows, indem Sie eine MSI-Datei herunterladen und ausführen.

## <a name="using-the-azure-cli-in-scripts"></a>Verwenden der Azure CLI in Skripts

Wenn Sie Azure CLI-Befehle in Skripts verwenden möchten, müssen Sie die möglichen Probleme in Zusammenhang mit der „Shell“ oder der Ausführungsumgebung kennen. Beispielsweise werden Variablen in einer Bash-Shell mithilfe der folgenden Syntax festgelegt:

 ```azurecli
 variable="value"
 variable=integer
 ```

Wenn Sie eine PowerShell-Umgebung zum Ausführen von Azure CLI-Skripts verwenden, müssen Sie diese Syntax für Variablen verwenden:

 ```powershell
 $variable="value"
 $variable=integer
 ```

## <a name="summary"></a>Zusammenfassung

Sie müssen die Azure CLI installieren, um mit ihr Azure-Ressourcen von einem lokalen Computer aus zu verwalten. Die Installation ist für Windows, Linux und macOS unterschiedlich, allerdings gelten die Befehle nach der Installation plattformübergreifend. 
