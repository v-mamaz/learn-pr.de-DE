Stellen Sie sich vor, Sie arbeiten für ein Unternehmen, das Videodatenverarbeitung und Musteranalyse betreibt. Sie erstellen eine neue Prototypplattform, um das Videomaterial von Verkehrsüberwachungskameras zu verarbeiten, Trends zu analysieren und verwertbare Daten für Verkehrsfluss- und Straßenverbesserungen bereitzustellen. 

Um Ihre Algorithmen zu verbessern, haben Sie mit mehreren neuen Städten Vereinbarungen getroffen, um die Daten ihrer Verkehrsüberwachungskameras zu erfassen. Allerdings liegen nicht alle Videodaten im gleichen Format vor, und viele der Formate haben nur Windows-Codecs zur Decodierung der Daten. Aus diesem Grund haben Sie sich entschieden, virtuelle Computer (VMs) zu verwenden, um die Erstverarbeitung auszuführen. Anschließend pushen Sie die Daten für die Verarbeitung in einem Standardformat in Azure Functions. Mit dieser Vorgehensweise können Sie neue Datenformate dynamisch einführen, ohne das gesamte System zu beenden.

Azure bietet eine robuste Hostinglösung für virtuelle Computer, die Ihren Anforderungen gerecht wird. Sehen wir uns an, wie Sie virtuelle Windows-Computer in Azure erstellen und mit ihnen arbeiten.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Grundlagen über die Optionen, die für virtuelle Computer in Azure zur Verfügung stehen
- Erstellen eines virtuellen Windows-Computers über das Azure-Portal
- Stellen Sie mithilfe von Remotedesktop eine Verbindung zu einem ausgeführten virtuellen Computer her.
- Installieren Sie die Software, und ändern Sie mithilfe des Azure-Portals die Netzwerkkonfiguration auf einem virtuellen Computer.