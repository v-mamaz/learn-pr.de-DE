## <a name="motivation"></a>Motivation
Angenommen Sie, Ihr Unternehmen Azure-Befehlszeilenschnittstelle als Befehlszeilen-Lösung für die Verwaltung von Azure-Ressourcen ausgewählt hat. Ihre Administratoren und Entwickler bevorzugen die Befehle und Skripts lokal anstatt über einen Browser ausführen. Das Team verwendet, Computer, auf denen Linux, MacOS und Windows ausgeführt wird. In diesem Fall müssen Sie eine Azure-Befehlszeilenschnittstelle funktioniert auf allen ihren Geräten zu erhalten.

## <a name="what-is-the-azure-cli"></a>Was ist der Azure-Befehlszeilenschnittstelle?
Der Azure-Befehlszeilenschnittstelle (Command Line Interface) ist ein Befehlszeilenprogramm zum Verbinden mit Azure und das Ausführen administrativer Befehle für Azure-Ressourcen. Um einen virtuellen Computer (VM) neu zu starten, würden Sie beispielsweise einen Befehl wie den folgenden verwenden:

 ```bash
 az vm restart -g MyResourceGroup -n MyVm
 ```

Der Azure-Befehlszeilenschnittstelle bietet plattformübergreifende Befehlszeilentools zum Verwalten von Azure-Ressourcen und können lokal auf Linux, Mac oder Windows-Computern installiert werden; der Azure-Befehlszeilenschnittstelle kann auch von einem Browser über Azure Cloud Shell verwendet werden. In beiden Fällen können sie interaktiv verwendet oder ein Skript erstellt werden. Für die interaktive Verwendung, wenn Sie eine Shell, wie z. B. cmd.exe unter Windows oder Bash unter Linux oder MacOS zum ersten Mal aufrufen und geben Sie den Befehl an der shelleingabeaufforderung. Um sich wiederholende Aufgaben zu automatisieren, müssen Sie die CLI-Befehle in ein Shell-Skript, das mithilfe der Syntax von Ressourcenskriptdateien Ihrer ausgewählten Shell zusammenstellen und führen Sie das Skript.

## <a name="how-to-install-azure-cli"></a>Vorgehensweise: Installieren der Azure-Befehlszeilenschnittstelle
Unter Linux und MacOS verwenden Sie einen Paket-Manager zum Installieren von PowerShell Core. Das empfohlene Paket-Manager unterscheidet sich von Betriebssystem und die Verteilung:
- Linux: **apt-Get** unter Ubuntu können **Yum** unter Red Hat und **Zypper** opensuse
- Mac: **Homebrew**

Azure-Befehlszeilenschnittstelle ist in der Microsoft-Repository verfügbar, daher Sie zunächst das Repository Ihr Paket-Manager hinzufügen müssen.

Auf Windows installieren Sie Azure CLI, indem herunterladen und Ausführen einer MSI-Datei.

## <a name="using-the-azure-cli-in-scripts"></a>Mithilfe der Azure CLI in Skripts
Wenn Sie Azure CLI-Befehlen in Skripts verwenden möchten, müssen Sie über alle Probleme, um das "Shell" oder die Umgebung, die zum Ausführen des Skripts verwendet werden. Beispielsweise wird in einer Bash-Shell, die folgende Syntax verwendet, wenn Variablen festlegen:

 ```bash
 variable="string"
 variable=integer
 ```

Wenn Sie eine PowerShell-Umgebung für die Ausführung von Azure CLI-Skripts verwenden, müssen Sie für Variablen die folgende Syntax verwenden:

 ```powershell
 $variable="string"
 $variable=integer
 ```

## <a name="summary"></a>Zusammenfassung
Der Azure-Befehlszeilenschnittstelle muss installiert sein, bevor es zum Verwalten von Azure-Ressourcen von einem lokalen Computer verwendet werden kann. Die Installationsschritte für Windows, Linux und MacOS variieren, aber nach der Installation die Befehle werden häufig über Plattformen hinweg. 
