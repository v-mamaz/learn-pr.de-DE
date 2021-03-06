Hier erfahren Sie, wie eine Web-App in Azure App Service über das Azure-Portal erstellt wird.

## <a name="why-use-the-azure-portal"></a>Gründe für das Azure-Portal

Der erste Schritt beim Hosting Ihrer Webanwendung ist das Erstellen einer Web-App (einer App Service-App) in Ihrem Azure-Abonnement.

Es gibt mehrere Möglichkeiten, wie Sie eine Web-App erstellen können. Sie können das Azure-Portal, die Azure-Befehlszeilenschnittstelle (Azure CLI), ein Skript oder eine IDE (integrierte Entwicklungsumgebung) verwenden.

Hier nutzen wir das Portal, weil es eine grafische Oberfläche bietet, die es zu einem großartigen Lehrmittel macht. Das Portal hilft Ihnen, verfügbare Funktionen zu ermitteln, zusätzliche Ressourcen hinzuzufügen und vorhandene Ressourcen anzupassen.

## <a name="what-is-azure-app-service"></a>Was ist Azure App Service?

Azure App Service ist eine vollständig verwaltete IT-Plattform in der Azure-Umgebung, die für das Hosten von Web-Apps, REST-APIs und mobilen Back-Ends optimiert ist.

Mit diesem PaaS-Angebot (Platform-as-a-Service) von Microsoft Azure können Sie sich auf die Entwicklung konzentrieren, während Azure sich um die Infrastruktur zum Ausführen und Skalieren Ihrer Anwendungen kümmert.

## <a name="how-to-create-a-web-app"></a>Schritte zum Erstellen einer Web-App

Wenn es an der Zeit ist, Ihre eigene App zu hosten, besuchen Sie das Azure-Portal und erstellen eine neue **Web-App**. Durch das Erstellen einer **Web App** im Azure-Portal erstellen Sie tatsächlich eine Reihe von Hostingressourcen in App Service, mit denen Sie jede webbasierte Anwendung hosten können, die von Azure unterstützt wird, unabhängig davon, ob es sich um ASP.NET Core, Node.js, PHP usw. handelt. Die folgende Abbildung zeigt, wie einfach es ist, das Framework bzw. die Sprache der App zu konfigurieren.

![Screenshot: Anwendungseinstellungen für die Konfiguration der Web-App](../media/2-web-app-settings.png)

Das Azure-Portal bietet eine Vorlage zum Erstellen einer Web-App. Diese Vorlage weist die folgenden Pflichtfelder auf:

- **App-Name** : Der Name der Web-App.
- **Abonnement**: Eine gültiges und aktives Abonnement.
- **Ressourcengruppe**: Eine gültige Ressourcengruppe. In den folgenden Abschnitten wird ausführlich erläutert, was eine Ressourcengruppe ist.
- **Betriebssystem**: Das Betriebssystem. Die Optionen sind: Windows, Linux und Docker-Container. Unter Windows können Sie jede Art von Anwendung mit einer Vielzahl von Technologien hosten. Das gleiche gilt für das Hosten unter Linux. Allerdings müssen alle ASP.NET-Apps unter Linux ASP.NET Core-Apps im .NET Core-Framework sein. Die letzte Option sind Docker-Container, bei denen Sie Ihre Container direkt in von Azure gehosteten und verwalteten Containern bereitstellen können. 
- **App Service-Plan/-Speicherort**: Ein gültiger Azure App Service-Plan. In den folgenden Abschnitten wird ausführlich erläutert, was ein App Service-Plan ist.
- **Application Insights**: Sie können Azure Application Insights aktivieren und von den Überwachungs- und Metriktools des Azure-Portals profitieren, die Ihnen helfen, die Leistung Ihrer Apps im Auge zu behalten.

Das Azure-Portal gibt Ihnen durch die vielen verfügbaren Tools die Kontrolle über die Verwaltung, Überwachung und Steuerung Ihrer Webanwendung.

### <a name="deployment-slots"></a>Bereitstellungsslots

Im Azure-Portal können Sie einer App Service-Web-App ganz einfach **Bereitstellungsslots** hinzufügen. Sie können z.B. einen Bereitstellungsslot für das **Staging** erstellen, in dem Sie Ihren zu testenden Code in Azure pushen können. Sobald Sie mit Ihrem Code zufrieden sind, können Sie ganz einfach den Bereitstellungsslot „Staging“ gegen den Bereitstellungsslot „Produktion“ **tauschen**. Dies erledigen Sie alles mit ein paar einfachen Mausklicks im Azure-Portal.

![Screenshot: Staging-Bereitstellungsslot zum Testen der Bereitstellungen](../media/2-deployment-slots.png)

### <a name="continuous-integrationdeployment-support"></a>Unterstützung für Continuous Integration/Continuous Deployment

Das Azure-Portal bietet standardmäßige Funktionen für Continuous Integration und Continuous Deployment mit Visual Studio Team Services, GitHub, Bitbucket, Dropbox, OneDrive oder einem lokalen Git-Repository auf Ihrem Entwicklungscomputer. Sie verbinden Ihre Web-App mit einer der oben genannten Quellen. App Service erledigt den Rest für Sie, indem der Code und alle künftigen Änderungen am Code automatisch mit der Web-App synchronisiert werden. Darüber hinaus können Sie mit Visual Studio Team Services Ihren eigenen Build- und Releaseprozess definieren, der am Ende dazu führt, dass Ihr Quellcode kompiliert, die Tests ausgeführt, ein Release erstellt und schließlich das Release jedes Mal, wenn Sie den Code committen, mithilfe von Push an eine Web-App übertragen wird. Das alles geschieht implizit, ohne dass Sie eingreifen müssen.

![Screenshot: Einrichten der Bereitstellungsoptionen und Auswählen der Quelle für den Bereitstellungsquellcode](../media/2-continuous-integration.PNG)

### <a name="integrated-visual-studio-publishing-and-ftp-publishing"></a>Integrierte Visual Studio- und FTP-Veröffentlichung

Neben der Möglichkeit, Continuous Integration/Continuous Deployment für Ihre Web-App einzurichten, können Sie jederzeit von der engen Integration mit Visual Studio profitieren, um Ihre Web-App über die Web Deploy-Technologie in Azure zu veröffentlichen. Darüber hinaus unterstützt Azure FTP, obwohl es besser ist, FTP nicht für die Veröffentlichung zu verwenden, da diese Technologie nicht die Möglichkeiten von Web Deploy bietet, nur die Dateien auszuwählen, die geändert oder hinzugefügt wurden, sodass Sie stets alles in Azure veröffentlichen müssen!

### <a name="built-in-auto-scale-support-automatic-scale-out-based-on-real-world-load"></a>Integrierte Unterstützung für automatische Skalierung (automatische zentrale Hochskalierung basierend auf der realen Last)

In die Web-App integriert ist die Möglichkeit zum zentralen Hoch- bzw. Herunterskalieren bzw. zum horizontalen Skalieren. Je nach Nutzung der Web-App können Sie sie zentral hoch- bzw. herunterskalieren, indem Sie die Ressourcen des zugrunde liegenden Computers, der Ihre Web-App hostet soll, erhöhen bzw. verringern. Ressourcen können die Anzahl der Kerne oder die Menge des verfügbaren Arbeitsspeichers sein.

Die Erweiterung ist dagegen die Fähigkeit, die Anzahl der VM-Instanzen zu erhöhen, auf denen Ihre Web-App ausgeführt wird.

## <a name="what-is-a-resource-group"></a>Was ist eine Ressourcengruppe?

Eine Ressourcengruppe ist eine Methode, voneinander abhängige Ressourcen und Dienste wie virtuelle Computer, Web-Apps, Datenbanken und mehr für eine bestimmte Anwendung und Umgebung zu gruppieren. Stellen Sie sie sich als **Ordner** vor, in dem Sie Elemente Ihrer App gruppieren können.

Ressourcengruppen bieten eine einfache Möglichkeit, Ressourcen zu verwalten und zu löschen. Sie bieten auch eine Möglichkeit zur Überwachung, Zugriffssteuerung, Bereitstellung und Verwaltung der Abrechnung von Sammlungen von Ressourcen, die für den Betrieb einer Anwendung erforderlich sind oder von einem Kunden verwendet werden.

## <a name="what-is-an-app-service-plan"></a>Was ist ein App Service-Plan?

Ein App Service-Plan ist eine Zusammenstellung von physischen Ressourcen und Kapazität, die für die Bereitstellung Ihrer App Service-Apps zur Verfügung stehen.

Das Azure-Portal bietet eine Vorlage zum Erstellen eines neuen App Service-Plans. Diese Vorlage fordert die folgenden grundlegenden Informationen an:

- Region (USA, Westen, Europa, Norden usw.)
- Skalierung (Anzahl der Instanzen)
- Instanzgröße (klein, mittel oder groß)
- SKU oder Tarif (Free, Shared, Basic, Standard, Premium, PremiumV2 und Isolated)

Web-Apps, mobile Apps und API-Apps, die in Azure App Service gehostet werden, sowie Azure Functions, die alle in einem App Service-Plan ausgeführt werden. Während Sie eine unbegrenzte Anzahl von Anwendungen in einem App Service-Plan bereitstellen können, hängt die Anzahl der von Ihnen verwendeten Anwendungen in hohem Maß von der Art der bereitgestellten Anwendungen und ihren erforderlichen Ressourcen bei der CPU-Auslastung ab.

Sie können Ihren App Service-Plan jederzeit im Azure-Portal verwenden, um Ihre CPU- und Speicherauslastung zu visualisieren und Ihren Bedarf an Skalierung oder Verlagerung von Anwendungen in einen anderen App Service-Plan zu ermitteln.
