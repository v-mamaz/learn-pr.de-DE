Stellen Sie sich vor, Sie arbeiten für ein Unternehmen, das Datenverarbeitung und -speicherung für Verkehrsüberwachungskameras betreibt. Die Videodatenströme werden analysiert, kategorisiert und verarbeitet, um Gesichter und Kfz-Kennzeichen zu bestimmten Zeiten zu identifizieren. Die Informationen werden in Azure Data Lake hochgeladen, und es wird ein durchsuchbarer Index für die Strafverfolgung generiert.

Diese Videodatenströme verwenden verschiedene Codecs und Auflösungen. Für die anfängliche Verarbeitung und die Codierung in einem gängigen Videoformat müssen Sie verschiedene Windows-basierte proprietäre Softwarepakete ausführen. Weil regelmäßig neue Formate veröffentlicht werden, ist es vorteilhaft, die Videoverarbeitung auf virtuellen Computern (VMs) durchzuführen. Die proprietären Pakete können so hinzugefügt und aktualisiert werden, ohne das gesamte System anzuhalten.

Azure bietet eine robuste Hostinglösung für virtuelle Computer, die Ihren Anforderungen gerecht wird. Sehen wir uns an, wie Sie virtuelle Windows-Computer in Azure erstellen und mit ihnen arbeiten.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Grundlagen über die Optionen, die für virtuelle Computer in Azure zur Verfügung stehen
- Erstellen eines virtuellen Windows-Computers über das Azure-Portal
- Stellen Sie mithilfe von Remotedesktop eine Verbindung zu einem ausgeführten virtuellen Computer her.
- Installieren Sie die Software, und ändern Sie mithilfe des Azure-Portals die Netzwerkkonfiguration auf einem virtuellen Computer.