Visual Studio Code ist eine beliebte Wahl für die Entwicklung von Anwendungen für Azure. Die integrierte Entwicklungsumgebung (IDE) ist einfach und erfordert nur einige MB an Speicherplatz im Gegensatz zu einigen GB für einige IDEs. VS Code ist plattformübergreifend und funktioniert unter Windows, Linux und macOS.

## <a name="visual-studio-code"></a>Visual Studio Code

Visual Studio Code (oder einfach VS Code) ist ein leistungsfähiger und zugleich kompakter Editor. Er unterstützt die meisten Programmiersprachen, genau genommen Hunderte, und ist dafür konzipiert, eine Verbindung mit Clouddiensten herzustellen.

Mit einem Schwerpunkt auf plattformübergreifender Unterstützung (die Ausführung ist unter Windows, Linux und macOS möglich) und einer portablen agilen Umgebung enthält die Basisinstallation von VS Code einen Editor, der eine ständig wachsende Abdeckung von Programmiersprachen-Syntaxhervorhebungen erkennt. Es gibt jedoch keinen Compiler. Die Kompilierung muss in der Cloud oder über eine Erweiterung erfolgen.

Sie erhalten eine hervorragende integrierte Unterstützung für die Quellcodeverwaltung über einen Git-Quellcodeverwaltungs-Manager (SCM). Sie müssen allerdings zuerst das Git-Framework installieren.

## <a name="extension-model"></a>Erweiterungsmodell

Eines der leistungsstärksten Features von Visual Studio Code ist das Erweiterungsmodell. Es ermöglicht, Drittanbieterfunktionen als integrierte Bestandteile der VS Code-IDE auszuführen und die Funktionen der IDE auf nahezu jede erdenkliche Weise zu erweitern.

Eine Erweiterung wird in TypeScript oder JavaScript geschrieben. Sie können Yeoman zum Erstellen des Gerüstbaus einer Erweiterung verwenden. Alle Komponenten bieten Unterstützung für IntelliSense, Codenavigation und vollständiges Debuggen.

Es gibt drei allgemeine Kategorien von Erweiterungen für VS Code: Erweiterungen, Sprachserver und Debugger. Die beiden letztgenannten verfügen über zusätzliche Protokolle, die es ihnen ermöglichen, spezielle Funktionen bereitzustellen.

Die verfügbaren Erweiterungen in Marketplace für Erweiterungen umfassen Unterstützung für Python, Go, C++ und viele andere Sprachen. Die Erweiterungen enthalten auch Tools für die Codeformatierung, z.B. Linter, Tools für die Cloudkonnektivität, z.B. Azure, neue Designs, Codeformatierungsprogramme und Bibliotheken mit Codeausschnitten. Diese Erweiterungen sind alle auf dem [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/) verfügbar.

## <a name="azure-extensions"></a>Azure-Erweiterungen

Viele der Erweiterungen sind für Azure-Features und -Produkte vorgesehen, und es werden ständig weitere ergänzt. Sie zielen auf Bereiche wie Docker-Unterstützung, Abonnementverwaltung, Tools für die Azure CLI, Datenbankzugriff, Azure Storage-API-Integration und allgemeine Azure-Erweiterungen ab.

Mit jeder Azure-Erweiterung wird ein Satz von VS Code-Features hinzugefügt, der Ihre Entwicklung mit Azure-Integrationspunkten einfacher und effizienter macht.

## <a name="getting-vs-code-and-preparing-for-azure-development"></a>Abrufen von VS Code und Vorbereiten der Azure-Entwicklung

Es gibt drei verschiedene Plattformen, auf denen VS Code unterstützt wird: Windows, macOS und Linux. Zwar erfolgt die Installation jeweils über eine herunterladbare Datei, beim Setup gibt es jedoch Unterschiede.

Um VS Code unter Windows zu verwenden, laden Sie die Datei für Ihre Version von Windows herunter (32-Bit oder 64-Bit) und installieren sie wie jede andere Windows-Anwendung.

Für macOS laden Sie die Datei herunter und erweitern ihren Inhalt. Es wird empfohlen, VS Code dem Launchpad und dem Dock hinzuzufügen.

Linux ist etwas komplexer, und die Installationsanweisungen hängen von der verwendeten Distribution ab. Debian und Ubuntu erfordern, dass Sie VS Code selbst herunterladen und installieren. Für RHEL, Fedora, CentOS, openSUSE und SLE stellt Microsoft ein Yum-Repository zur Verfügung. Für andere Distributionen sind möglicherweise auch Community-Editionen mit weniger Unterstützung verfügbar.

Um VS Code auf einer Plattform für die Azure-Entwicklung vorzubereiten, installieren Sie über den Marketplace für Erweiterungen die erforderlichen Azure-Erweiterungen. Wenn Sie mit App Service arbeiten, verwenden Sie die App Service-Erweiterung. Wenn Sie mit Node.js arbeiten, benötigen Sie das Node-Paket für Azure.

## <a name="summary"></a>Zusammenfassung

VS Code ist eine perfekte Ergänzung für die Entwicklung und Erstellung von Anwendungen für Azure. Durch die einfache, plattformübergreifende IDE zusammen mit einer Vielzahl von Erweiterungen zur Verbesserung der Effizienz und der Stabilität von Apps eignet sich VS Code hervorragend für die Azure-Entwicklung.
