Hier erfahren Sie, wie Sie im Azure-Portal eine Azure-Web-App erstellen.

## <a name="why-use-the-azure-portal"></a>Gründe für das Azure-Portal

Der erste Schritt beim Hosting Ihrer Webanwendung ist die Erstellung einer **Web-App** in Ihrem Azure-Abonnement.

Dazu gibt es verschiedene Möglichkeiten. Sie können das Azure-Portal, die Azure-Befehlszeilenschnittstelle (Azure CLI), ein Skript oder eine IDE verwenden.

Hier nutzen wir das Portal, weil es eine grafische Oberfläche bietet, die es zu einem großartigen Lehrmittel macht. Das Portal hilft Ihnen, verfügbare Funktionen zu ermitteln, zusätzliche Ressourcen hinzuzufügen und vorhandene Ressourcen anzupassen.

## <a name="what-is-web-apps-in-azure"></a>Was sind Web-Apps in Azure?

Web-Apps ist eine vollständig verwaltete IT-Plattform innerhalb der Azure-Umgebung, die für das Hosten von Web-Apps, REST-APIs und mobilen Back-Ends optimiert ist.

Mit diesem PaaS-Angebot (Platform as a Service) von Microsoft Azure können Sie sich auf die Entwicklung konzentrieren, während Azure sich um die Infrastruktur zum Ausführen und Skalieren Ihrer Anwendungen kümmert.

## <a name="how-to-create-an-azure-web-app"></a>Erstellen einer Azure-Web-App

Wenn es an der Zeit ist, Ihre eigene App zu hosten, besuchen Sie das Azure-Portal und erstellen eine neue **Ressource** des Typs **Web-App**. Indem Sie eine solche Ressource im Azure-Portal erstellen, erstellen Sie eigentlich einen **Container** oder eine Vorlage, mit der Sie jede webbasierte Anwendung hosten können, die von Azure unterstützt wird, und zwar ASP.NET Core, Node.js, PHP, usw. Die folgende Abbildung zeigt, wie einfach es ist, das Framework bzw. die Sprache der App zu konfigurieren.

![Web-App-Einstellungen](../media/2-web-app-settings.png)

Das Azure-Portal bietet eine Vorlage zum Erstellen einer neuen Web-App. Diese Vorlage hat die folgenden Pflichtfelder:

- **App-Name** : Der Name der Web-App.
- **Abonnement**: Eine gültiges und aktives Abonnement.
- **Ressourcengruppe**: Eine gültige Ressourcengruppe. In den folgenden Abschnitten wird ausführlich erläutert, was eine Ressourcengruppe ist.
- **Betriebssystem**: Das Betriebssystem. Die Optionen sind: Windows, Linux und Docker-Container. Unter Windows können Sie jede Art von Anwendung mit einer Vielzahl von Technologien hosten. Dasselbe gilt für das Linux-Hosting mit Ausnahme der Tatsache, dass Sie nur ASP.NET Core-Web-Apps erstellen können, die das .NET Core-Framework über Linux verwenden. Bei anderen ASP.NET-Apps, die das gesamte .NET Framework verwenden, muss das Hosting über das Windows-Betriebssystem erfolgen. Die letzte Option sind Docker-Container, bei denen Sie Ihre eigenen lokalen Docker-Container direkt in von Azure gehosteten und verwalteten Containern bereitstellen können. Grundsätzlich kann also jede Web-App, die eine Open-Source-Technologie (PHP, ASP.NET Core, usw.) nutzt, unter einem Linux-Betriebssystem gehostet werden.
- **App Service-Plan/Standort**: Ein gültiger Azure App Service-Plan. In den folgenden Abschnitten wird ausführlich erläutert, was ein App Service-Plan ist.
- **Application Insights**: Sie können die Option Azure Application Insights aktivieren und von den Überwachungs- und Metriktools des Azure-Portals profitieren, die Ihnen helfen, die Leistung Ihrer Apps im Auge zu behalten.

Das Azure-Portal gibt Ihnen durch die vielen verfügbaren Tools die Kontrolle bei der Verwaltung, Überwachung und Steuerung Ihrer Webanwendung.

### <a name="deployment-slots"></a>Bereitstellungsslots

Im Azure-Portal können Sie einer Web-App ganz einfach **Bereitstellungsslots** hinzufügen. Sie können z.B. einen Bereitstellungsslot für das **Staging** erstellen, in dem Sie Ihren zu testenden Code in Azure übertragen. Sobald Sie mit Ihrem Code zufrieden sind, können Sie ganz einfach den Stagingbereitstellungsslot gegen den Produktionsslot **tauschen**. Dies erledigen Sie alles über ein paar einfache Mausklick im Azure-Portal.

![Bereitstellungsslots](../media/2-deployment-slots.png)

### <a name="continuous-integrationdeployment-support"></a>Unterstützung für Continuous Integration/Deployment

Das Azure-Portal bietet standardmäßige Funktionen für Continuous Integration und Continuous Deployment with Visual Studio Team Services, GitHub, Bitbucket, Dropbox, OneDrive oder einem lokalen Git-Repository, das von Azure vollständig verwaltet wird. Sie verbinden Ihre Web-App mit einer der oben genannten Quellen, woraufhin Azure den Rest für Sie erledigt, indem es den Code und alle künftigen Änderungen am Code automatisch mit der Web-App synchronisiert. Darüber hinaus können Sie mit Visual Studio Team Services Ihren eigenen Build- und Release-Prozess definieren, der am Ende dazu führt, dass Ihr Quellcode kompiliert, die Tests ausgeführt, eine Version erstellt und schließlich die Version jedes Mal, wenn Sie für den Code ein Commit durchführen, in eine Web-App übertragen wird. Das alles geschieht implizit, ohne dass Sie eingreifen müssen.

![Konfigurieren von Continuous Integration](../media/2-continuous-integration.PNG)

### <a name="integrated-visual-studio-publishing-and-ftp-publishing"></a>Integrierte Visual Studio- und FTP-Veröffentlichung

Neben der Möglichkeit, Continuous Integration/Deployment für Ihre Web Ap- einzurichten, können Sie jederzeit von der engen Integration mit Visual Studio profitieren, um Ihre Web-App über die Web Deploy-Technologie in Azure zu veröffentlichen. Darüber hinaus unterstützt Azure FTP, obwohl es besser ist, FTP nicht für die Veröffentlichung zu verwenden, da diese Technologie nicht die Möglichkeiten von Web Deploy bietet, nur die Dateien auszuwählen, die geändert oder hinzugefügt wurden, sodass Sie stets alles in Azure veröffentlichen müssen!

### <a name="built-in-auto-scale-support-automatically-scale-updown-based-on-real-world-load"></a>Integrierte Unterstützung der automatischen Skalierung (für automatisches zentrales Hoch- bzw. Herunterskalieren basierend auf der reale Last)

In die Web-App integriert ist die Möglichkeit zum zentrales Hoch- bzw. Herunterskalieren bzw. zum Erweitern. Je nach Nutzung der Web-App können Sie sie horizontal nach oben bzw. unten skalieren, indem Sie die Ressourcen des zu grundeliegenden Computers, der Ihre Web-App hostet soll, erhöhen bzw. verringern. Ressourcen können die Anzahl der Kerne oder die Menge des verfügbaren Arbeitsspeichers sein.

Die Erweiterung ist dagegen die Fähigkeit, die Anzahl der VM-Instanzen zu erhöhen, auf denen Ihre Web-App ausgeführt wird.

## <a name="what-is-a-resource-group"></a>Was ist eine Ressourcengruppe?

Eine Ressourcengruppe ist eine Methode, voneinander abhängige Ressourcen und Dienste wie virtuelle Computer, Web-Apps, Datenbanken und mehr für eine bestimmte Anwendung und Umgebung zu gruppieren. Stellen Sie sie sich als **Ordner** vor, in dem Sie Elemente Ihrer App gruppieren können.

Ressourcengruppen bieten eine einfache Möglichkeit, Ressourcen zu verwalten und zu löschen. Sie bieten auch eine Möglichkeit zur Überwachung, Zugriffssteuerung, Bereitstellung und Verwaltung der Abrechnung von Sammlungen von Ressourcen, die für den Betrieb einer Anwendung erforderlich sind oder von einem Kunden verwendet werden.

## <a name="what-is-an-app-service-plan"></a>Was ist ein App Service-Plan?

Ein App Service-Plan ist eine Zusammenstellung von physischen Ressourcen und Kapazität, die für die Bereitstellung Ihrer App Service-Apps zur Verfügung stehen.

Das Azure-Portal bietet eine Vorlage zum Erstellen eines neuen App Service-Plans. Diese Vorlage fordert die folgenden grundlegenden Informationen an:

- Region (USA, Westen, Europa, Norden usw.)
- Skalierung (Anzahl der Instanzen)
- Instanzgröße (klein, mittel, groß)
- Stock Keeping Unit – SKU (Free, Shared, Basic, Standard, Premium und seit Kurzem Premium v2)

Die Features Web-Apps, Mobile Apps und API-Apps von Azure App Service sowie Azure Functions werden alle in einem App Service-Plan ausgeführt. Während Sie eine unbegrenzte Anzahl von Anwendungen in einem App Service-Plan bereitstellen können, hängt die Anzahl der von Ihnen verwendeten Anwendungen in hohem Maß von der Art der bereitgestellten Anwendungen und ihren erforderlichen Ressourcen bei der CPU-Auslastung ab.

Sie können Ihren App Service-Plan jederzeit im Azure-Portal verwenden, um Ihre CPU- und Speicherauslastung zu visualisieren und Ihren Bedarf an Skalierung oder Verlagerung von Anwendungen in einen anderen App Service-Plan zu ermitteln.
