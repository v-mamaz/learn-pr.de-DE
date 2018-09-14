Visual Studio ist eine vollständig ausgewählte und umfassende integrierte Entwicklungsumgebung (IDE) zur nahezu jede Art von Software, die professionelle. Visual Studio verfügt über einen vollständigen Satz von Tools und Features, die speziell auf die Entwicklung von Anwendungen mit Microsoft Azure konzipiert sind. Die enge Integration in Visual Studio bedeutet, dass Azure Tools für Bereitstellung, Debuggen und Entwicklung erstklassiger sind. Dies gilt auch für Visual Studio für Mac. Diese Einheit werden beide vorgestellt.

## <a name="visual-studio"></a>Visual Studio

Visual Studio ist eine IDE mit vollem Funktionsumfang zum Entwickeln von Anwendungen für Windows, Android, iOS, das Internet und Azure.

Wenn Sie Visual Studio installieren, sind mehrere Workloads verfügbar. Workloads sind Sammlungen von Bibliotheken und Komponenten, die einen Bereich von Funktionen definieren, der installiert werden kann. Statt einzelne Komponenten zu installieren, bei denen Sie die Abhängigkeiten untereinander kennen müssen, können Sie Workloads verwenden, um „thematische“ Installationen durchzuführen. Dadurch wird sichergestellt, dass alle erforderlichen Komponenten einbezogen werden.

Die Basisinstallation von Visual Studio enthält keine Tools oder Bibliotheken für die Azure-Entwicklung. Dafür müssen Sie die Workload „Azure-Entwicklung“aufnehmen. Diese umfasst die Azure SDKs, Tools und Vorlagenprojekte für die ersten Schritte beim Erstellen von Anwendungen und Umgebungen in Azure.

Um Visual Studio zu installieren, laden Sie den Installer herunter. Dieser Installer fragt, welche Workloads installiert werden sollen. Hier geben Sie die Workload „Azure-Entwicklung“ an. Wenn zusätzliche Funktionen erforderlich sind, stehen diese in den meisten Fällen über NuGet oder eine Visual Studio-Erweiterung zur Verfügung.

## <a name="visual-studio-for-mac"></a>Visual Studio für Mac

Visual Studio für Mac ist eine nativ entworfene und entwickelte IDE für macOS. Es bietet eine erstklassige Entwicklungsumgebung zum Erstellen von Anwendungen für mobile apps für Android und iOS, Web und .NET Core-Lösungen. Sie ist auch hervorragend für die Erstellung von Anwendungen in Azure geeignet.

Die Basisinstallation von Visual Studio für Mac bietet eine kontextbezogene Integration von Azure-Tools. Wenn Sie z.B. eine Xamarin-App für Android erstellen, bietet die Workload „Verbundene Dienste“ einen Link zum Erstellen eines mobilen Back-Ends für Azure App Service. Wenn Sie eine Azure-Funktion erstellen möchten, besteht eine Projektvorlage in der Cloud-Kategorie.

Wenn Sie Tools für Azure-Features und -Funktionen benötigen, die in der Basisinstallation nicht vorhanden sind, ist NuGet die beste Wahl. Der NuGet-Paket-Manager weist zahlreiche Azure-Pakete auf, die die Funktionen und Tools von Visual Studio für Mac erweitern.

Um Visual Studio für Mac zu installieren, laden Sie den Installer herunter. Der Installer prüft Ihr System, um zu bestimmen, welche Komponenten erforderlich sind oder aktualisiert werden müssen. Sie können anhand der Komponenten, die im System fehlen, die zu installierenden Komponenten anpassen. Die Basisinstallation umfasst Azure-Tools. Wenn zusätzliche Funktionen erforderlich sind, stehen diese wahrscheinlich über NuGet oder eine Erweiterung von Visual Studio für Mac zur Verfügung.

> [!NOTE]
> Sie müssen möglicherweise Administratoranmeldeinformationen auf Ihrem Computer angeben, um bestimmte Komponenten zu installieren.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie Visual Studio installiert, entweder auf Windows oder MacOS.

Für Windows, gewählten Azure-entwicklungsworkload in der Installer-Benutzeroberfläche, die installiert alle erforderlichen Tools zum Erstellen von Azure-Anwendungen und Azure-Ressourcen zu generieren.

Im Lieferumfang von Visual Studio für Mac sind einige Azure-Tools die Basisinstallation integriert. Viele weitere Funktionen sind über NuGet verfügbar.
