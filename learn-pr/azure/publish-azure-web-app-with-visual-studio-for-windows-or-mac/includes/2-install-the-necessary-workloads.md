Der erste Schritt auf dem Weg zu Ihrer neuen Website ist das Vorbereiten Ihrer Entwicklungsumgebung. Für das Erstellen und Bereitstellen von ASP.NET-Webanwendungen müssen die erforderlichen Tools auf Ihrem lokalen Computer installiert sein. Im Folgenden werden diese Tools und deren Installation beschrieben.

## <a name="prepare-your-development-environment"></a>Vorbereiten Ihrer Entwicklungsumgebung

Visual Studio 2017 enthält zwei Workloads, die Sie für das Erstellen, Veröffentlichen und Bereitstellen Ihrer Website in Azure benötigen. Diese Workloads enthalten alle Vorlagen für Ihre ASP.NET-Website und ermöglichen, Ihre Anwendung mit Azure zu verbinden und dort bereitzustellen.

Stellen Sie sicher, dass Sie folgende Workloads installiert haben:

- ASP.NET und Webentwicklung

Die Workload für die Webentwicklung in Visual Studio 2017 wurde dafür entwickelt, Ihre Produktivität beim Entwickeln von Webanwendungen mithilfe von ASP.NET und standardbasierten Technologien wie HTML und JavaScript zu maximieren.

- Azure-Entwicklung

Durch die Workload „Azure-Entwicklung“ in Visual Studio 2017 werden das neueste Azure SDK für .NET sowie Tools für Visual Studio installiert. Nach der Installation dieser Elemente können Sie Ressourcen im Cloud-Explorer anzeigen, Ressource mithilfe von Azure Resource Manager-Tools erstellen, Anwendungen für Web- und Clouddienste von Azure erstellen und Big Data-Vorgänge mithilfe von Azure Data Lake-Tools durchführen.

## <a name="how-to-install-the-required-workloads"></a>Installieren erforderlicher Workloads

Verwenden Sie den Visual Studio-Installer, um die Komponenten zu bearbeiten, die mit Visual Studio installiert wurden.

- Scrollen Sie im Windows-Startmenü zum Buchstaben **V**, und klicken Sie dann auf **Visual Studio-Installer**, um den Installer zu starten. Alternativ können Sie im Startmenü ```Visual Studio Installer``` eingeben, um den Link zum Installer zu suchen. Drücken Sie anschließend die **EINGABETASTE**.

- Das Fenster des Visual Studio-Installers wird angezeigt. Klicken Sie auf **Ändern**. Wenn diese Schaltfläche nicht angezeigt wird, können Sie **Ändern** im Dropdownmenü **Weitere** auswählen.

    ![Ändern von Visual Studio](../media-draft/3-visual-studio-installer-modify.PNG)

- Stellen Sie sicher, dass die Workloads **ASP.NET und Webentwicklung** und **Azure-Entwicklung** im Abschnitt **Web und Cloud** der Registerkarte **Workloads** ausgewählt sind.   ![Installieren von Workloads](../media-draft/2-select-workloads.png)

Klicken Sie anschließend im unteren rechten Bereich des Installers auf **Ändern**. Der Visual Studio-Installer lädt die erforderlichen Komponenten herunter und installiert diese. Sie können nun eine ASP.NET-Web-App erstellen und diese in Microsoft Azure hochladen.

> [!IMPORTANT]
> In Visual Studio für Mac _sollten_ die erforderlichen Workloads bereits installiert sein. Wenn Sie diese erneut installieren müssen, müssen Sie [Visual Studio für Mac](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio-mac/?sku=communitymac&rel=15_) herunterladen und den Installer ausführen. Im Installer können Sie die Workloads auswählen, die Sie hinzufügen möchten.

## <a name="summary"></a>Zusammenfassung

Sie können eine ASP.NET-Website in Visual Studio 2017 mit den Workloads **ASP.NET und Webentwicklung** und **Azure-Entwicklung** erstellen, verwalten und veröffentlichen.
