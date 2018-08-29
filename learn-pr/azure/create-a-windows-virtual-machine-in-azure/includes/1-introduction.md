Angenommen, Sie arbeiten in einem Unternehmen, das die Daten von Verkehrskameras verarbeitet. Die Videodatenströme werden analysiert, kategorisiert und verarbeitet, um Gesichter und Kfz-Kennzeichen zu bestimmten Zeiten zu identifizieren. Diese Informationen werden anschließend in Azure Data Lake hochgeladen, und es wird ein durchsuchbarer Index generiert.

Diese Videodatenströme verwenden verschiedene Codecs und Auflösungen. Für die anfängliche Verarbeitung und die Codierung in einem gängigen Videoformat müssen Sie verschiedene Windows-basierte proprietäre Softwarepakete ausführen. Weil regelmäßig neue Formate veröffentlicht werden, ist es vorteilhaft, die Videoverarbeitung auf virtuellen Computern (VMs) durchzuführen. Die proprietären Pakete können so hinzugefügt und aktualisiert werden, ohne das gesamte System anzuhalten.

Um die Codierungssoftware auf Ihren Windows-VMs zu verwalten, müssen Sie eine Verbindung mit der Benutzeroberfläche herstellen.

In diesem Modul lernen Sie, wie Sie eine Windows-VM erstellen und mit dem Remotedesktopprotokoll (RDP) eine Verbindung mit der VM herstellen.

## <a name="learning-objectives"></a>Lernziele
> [!div class="checklist"]
> * Erstellen einer Windows-VM über das Azure-Portal
> * Kenntnis der Optionen, die für virtuelle Computer in Azure zur Verfügung stehen
> * Verbindungsherstellung mit einer ausgeführten Windows-VM über eine Windows RDP-Verbindung

## <a name="prerequisites"></a>Voraussetzungen

- Kenntnis der Azure Cloud Services-Umgebung
- Kenntnisse im Umgang mit virtuellen Computern
