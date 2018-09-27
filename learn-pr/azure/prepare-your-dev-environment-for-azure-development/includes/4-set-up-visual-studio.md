Visual Studio ist eine vollständige integrierte Entwicklungsumgebung (IDE), die für das Programmieren von vielen verschiedenen Anwendungstypen mit unterschiedlichen Programmiersprachen verwendet wird. Visual Studio verfügt über eine Vielzahl von Tools und Features, die speziell für die Entwicklung von Anwendungen mit Microsoft Azure konzipiert sind. Das bedeutet, dass Tools für die Entwicklung, das Debuggen und die Bereitstellung in Azure eng in die IDE integriert sind.

## <a name="visual-studio-2017"></a>Visual Studio 2017

Visual Studio 2017 ist eine vollständige IDE, die zum Entwickeln von vielen verschiedenen Anwendungstypen verwendet wird, unter anderem für Windows, Android, iOS, Webanwendungen und Azure.

Beim Installieren von Visual Studio sind mehrere *Workloads* verfügbar. Workloads sind installierbare Sammlungen von Bibliotheken und Komponenten, die bestimmte Funktionen ermöglichen. Statt einzelne Komponenten zu installieren, bei denen Sie die Abhängigkeiten untereinander kennen müssen, können Sie Workloads verwenden, um Installationen für spezifische Entwicklungsanforderungen durchzuführen. Dadurch wird sichergestellt, dass alle erforderlichen Komponenten einbezogen werden.

Die Basisinstallation von Visual Studio enthält keine Tools oder Bibliotheken für die Azure-Entwicklung. Hierfür müssen Sie die Workload „Azure-Entwicklung“ hinzufügen, die die Azure SDKs, Azure-Tools und entsprechende Projektvorlagen enthält.

[Laden Sie den Installer herunter](https://visualstudio.microsoft.com/), um Visual Studio zu installieren. Wählen Sie im Installer an der entsprechenden Stelle die Workload „Azure-Entwicklung“ aus. Falls zusätzliche Funktionen erforderlich sind, werden diese üblicherweise über NuGet-Pakete oder Erweiterungen für Visual Studio hinzugefügt.

## <a name="visual-studio-for-mac"></a>Visual Studio für Mac

Visual Studio für Mac ist eine nativ entworfene und entwickelte IDE für macOS. Mit dieser IDE können Sie Projektmappen für mobile Apps unter Android und iOS, für Webanwendungen und für .NET Core-Anwendungen erstellen.

Die Basisinstallation von Visual Studio für Mac bietet eine kontextbezogene Integration von Azure-Tools. Wenn Sie z.B. eine Xamarin-App für Android erstellen, enthält die integrierte Vorlage „Verbundene Dienste“ einen Link zum Erstellen eines mobilen Back-Ends mit Azure App Service. Für die Erstellung einer Azure-Funktion wird eine Projektvorlage aus der Kategorie „Cloud“ verwendet.

Wenn Sie Tools für Azure-Features und -Funktionen benötigen, die in der Basisinstallation nicht enthalten sind, müssen Sie in der Regel NuGet-Pakete oder eine Erweiterung für Visual Studio für Mac hinzufügen.

[Laden Sie den Installer herunter](https://visualstudio.microsoft.com/), um Visual Studio für Mac zu installieren. Der Installer prüft Ihr System, um zu bestimmen, welche Komponenten erforderlich sind oder aktualisiert werden müssen.

> [!NOTE]
> Sie müssen möglicherweise Administratoranmeldeinformationen auf Ihrem Computer eingeben, um bestimmte Komponenten zu installieren.