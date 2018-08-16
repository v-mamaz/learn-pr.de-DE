## <a name="motivation"></a>Motivation
Nehmen wir an, dass Sie Azure PowerShell als Ihr Automation-Lösung ausgewählt haben. Ihre Administratoren möchten ihre Skripts lokal statt in der Azure Cloud Shell ausführen. Das Team verwendet, Computer, auf denen Linux, MacOS und Windows ausgeführt wird. Sie müssen Azure PowerShell arbeiten, die auf allen ihren Geräten zu erhalten. 

## <a name="what-must-be-installed"></a>Was installiert werden müssen?
Es gibt zwei Komponenten von Azure PowerShell aus:
- die grundlegende PowerShell-Produkt
- Das Azure PowerShell-Modul, das die Azure-Befehle hinzugefügt

Das Basisprodukt weist zwei Varianten: PowerShell unter Windows und PowerShell Core unter Linux und Mac. PowerShell ist in Windows enthalten. Sie müssen zum Installieren von PowerShell Core für Linux und Mac-Geräten. 

Sobald das Basisprodukt installiert ist, fügen Sie dann Azure PowerShell-Moduls zu Ihrer Installation hinzu.

## <a name="how-to-install-powershell-core"></a>Vorgehensweise: Installieren von PowerShell Core
Unter Linux und MacOS verwenden Sie einen Paket-Manager zum Installieren von PowerShell Core. Das empfohlene Paket-Manager unterscheidet sich von Betriebssystem und die Verteilung:
- Linux: **apt-Get** unter Ubuntu können **Yum** unter Red Hat und **Zypper** opensuse
- Mac: **Homebrew**

PowerShell Core ist in der Microsoft-Repository verfügbar, daher Sie zunächst das Repository Ihr Paket-Manager hinzufügen müssen.

## <a name="how-to-install-azure-powershell"></a>Gewusst wie: Installieren von Azure PowerShell
Die bevorzugte Methode für das Azure PowerShell-Modul ist die Verwendung der **Install-Module** in PowerShell den Befehl.

Sie benötigen erhöhte Rechte, um Module zu installieren:
- Auf Windows müssen Sie PowerShell als Administrator ausführen.
- Unter Linux und MacOS verwenden Sie die **"sudo"** Befehl aus, um erhöhte Rechte zu erhalten.

## <a name="summary"></a>Zusammenfassung
Auf Windows PowerShell ist eine integrierte Funktion, aber Sie müssen Azure PowerShell-Modul installieren. Unter Linux und MacOS müssen Sie sowohl PowerShell Core und Azure PowerShell-Modul installieren. Im nächsten Abschnitt gelangen Sie über die Ausführliche Installationsschritte für einige gängige Plattformen.