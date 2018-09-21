Angenommen, Sie verwenden Azure PowerShell als Automatisierungslösung. Ihre Administratoren führen Skripts lieber lokal als in Azure Cloud Shell aus. Sie verwenden Computer, auf denen Linux, macOS oder Windows ausgeführt wird. Azure PowerShell muss auf all diesen Geräten funktionieren. 

## <a name="what-must-be-installed"></a>Was muss installiert werden?
Die eigentliche Installationsanleitung folgt im nächsten Teil. Betrachten wir jedoch zunächst die beiden Komponenten, aus denen Azure PowerShell besteht.

- **Das PowerShell-Basisprodukt** ist in zwei Varianten verfügbar: PowerShell für Windows und PowerShell Core für macOS und Linux.
- **Das spezielle Azure PowerShell-Modul** muss installiert werden, um PowerShell die Azure-spezifischen Befehle hinzuzufügen.

> [!TIP]
> PowerShell ist im Lieferumfang von Windows enthalten. Allerdings müssen Sie ggf. ein Update ausführen. Installieren Sie für Linux und macOS PowerShell Core.

Sobald das Basisprodukt installiert ist, fügen Sie Ihrer Installation das Azure PowerShell-Modul hinzu.

## <a name="how-to-install-powershell-core"></a>Installieren von PowerShell Core
Verwenden Sie unter Linux und macOS einen Paket-Manager, um PowerShell Core zu installieren. Der empfohlene Paket-Manager unterscheidet sich je nach Betriebssystem und Distribution.

> [!NOTE]
> PowerShell Core ist im Microsoft-Repository verfügbar, sodass Sie zuerst dieses Repository dem Paket-Manager hinzufügen müssen.

### <a name="linux"></a>Linux
Unter Linux unterscheidet sich der Paket-Manager je nach Distribution.

| Distribution(en)  | Paket-Manager |
|------------------|-----------------|
| Ubuntu, Debian   | `apt-get`       |
| Red Hat/CentOS  | `yum`           |
| OpenSUSE         | `zypper`        |
| Fedora           | `dnf`           |

### <a name="mac"></a>Mac
Verwenden Sie unter macOS `Homebrew`, um PowerShell Core zu installieren.

Der nächste Abschnitt behandelt die einzelnen Installationsschritte auf einigen gängigen Plattformen.