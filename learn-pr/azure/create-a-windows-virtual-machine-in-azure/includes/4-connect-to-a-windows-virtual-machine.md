Als Netzwerkadministrator bei einem Unternehmen für Datenanalyse sind Sie für die Verbindungsherstellung mit virtuellen Computern in Azure verantwortlich und müssen überprüfen, ob diese ordnungsgemäß konfiguriert sind. Sie verwenden hierbei einen RDP-Client, um eine Verbindung mit der Windows-Desktopoberfläche der VMs herzustellen.

## <a name="what-is-the-remote-desktop-protocol"></a>Was ist das Remotedesktopprotokoll (RDP)?

Das Remotedesktopprotokoll (RDP) bietet Remotekonnektivität mit der Benutzeroberfläche Windows-basierter Computer. RDP ermöglicht es Ihnen, sich remote bei einem physischen oder virtuellen Windows-Computer anzumelden und diesen Computer so zu steuern, als ob Sie an der Konsole sitzen würden.

> [!Note]
> Windows Hyper-V in Windows Server 2016 und Windows 10 nutzen RDP, um eine Verbindung mit VMs herzustellen, die auf dem Hypervisor ausgeführt werden.

Eine RDP-Verbindung ermöglicht es Ihnen, die meisten Vorgänge auszuführen, die Sie über die Konsole eines physischen Computers durchführen können. Ausgenommen hiervon sind einige Funktionen in Bezug auf den Betriebszustand und die Hardware.

Für eine RDP-Verbindung wird ein RDP-Client benötigt. Microsoft bietet RDP-Clients für die folgenden Betriebssysteme:

* Windows
* iOS
* MacOS
* Android

Es gibt auch Open Source-Linux-Clients, z.B. Remmina, mit denen Sie von einer Ubuntu-Distribution aus eine Verbindung mit einem Windows-PC herstellen können.

Windows 10 umfasst einen RDP-Client.

![Windows-RDP-Client](../media-drafts/4-rdp-client.PNG)

## <a name="what-functionality-does-an-rdp-connection-support"></a>Welche Funktionalität unterstützt eine RDP-Verbindung?

Mithilfe einer RDP-Verbindung können Sie mit der Benutzeroberfläche interagieren. Sie können aber auch eine Verbindung mit anderen Diensten auf dem Remotecomputer herstellen. Zu diesen Diensten gehören:

* Druckerverbindungen: Sie ermöglichen dem Remotecomputer das Drucken auf Ihrem lokalen Druckgerät.
* Audiowiedergabe: Die Wiedergabe kann entweder auf dem lokalen Computer oder auf dem Remotegerät erfolgen.
* Audioaufzeichnung: Sie können eine Audioaufzeichnung auf dem lokalen Computer durchführen und die Ausgabe an das Remotegerät umleiten.
* Ports: Sie können Ports an die Ports auf dem lokalen Computer umleiten.
* Laufwerke (zugeordnete Netzlaufwerke eingeschlossen): Laufwerke werden auf dem Remotecomputer als verbundene Laufwerke angezeigt.
* Geräte für die Videoaufzeichnung: z. B. integrierte Webcams.
* Andere unterstützte Plug&Play-Geräte.

Nicht alle dieser Features werden in Azure unterstützt, weil für diese Plattform Einschränkungen in Bezug auf die verfügbaren physischen Assets gelten. Beispielsweise können über eine RDP-Verbindung von einer durch Azure gehosteten VM zu den Druckgeräten des verbundenen Clients nur Softwaredrucker umgeleitet werden.

## <a name="configure-network-settings-for-rdp-access-to-virtual-machines"></a>Konfigurieren von Netzwerkeinstellungen für den RDP-Zugriff auf virtuelle Computer

Verbindungen mit Azure-VMs können auf drei Arten erfolgen:

1. Direkt über die öffentliche IP-Adresse der VM
2. Über eine VPN-Verbindung (Virtual Private Network, virtuelles privates Netzwerk)
3. Über eine ExpressRoute-Verbindung

Eine öffentliche IP-Adresse kann entweder dauerhaft oder dynamisch zugewiesen werden. Sie müssen außerdem sicherstellen, dass Sie Zugriff auf die öffentliche IP-Adresse der VM auf Port 3389 (RDP) besitzen. Für diese Bereitstellung müssen Sie sich möglicherweise an das Team für die Verwaltung der Firewallsicherheit Ihrer Organisation wenden, um eine Regel für die öffentliche IP-Adresse der VM auf Port 3389 einzurichten.

Dynamische öffentliche IP-Adressen werden bei jedem Neustart der VM neu zugewiesen. Statische Adressen sind dauerhaft, aber teurer.

Um die Verbindung über ein VPN herzustellen, muss Ihr lokales Netzwerk über eine aktive VPN-Verbindung mit Microsoft Azure verfügen.

Bei Verwendung einer ExpressRoute-Leitung wird die Konnektivität zur VM verwaltet. Dieser Ansatz bietet gleichzeitig die niedrigste Latenz und die Verbindung mit der höchsten Bandbreite.

> [!Note]
> Unabhängig davon, welche Option Sie für die Verbindungsherstellung mit Azure verwenden, muss die VM über RDP verfügbar sein – typischerweise auf dem Standardport 3389. Sie können die VM so konfigurieren, dass nur von Ihrer eigenen Client-IP-Adresse darauf zugegriffen werden kann. Die Verbindungsherstellung mit einer VM über Port 3389 für eine öffentliche IP-Adresse wird nur für Testumgebungen empfohlen. Verwenden Sie in Produktionsumgebungen Option 2 oder 3.

## <a name="how-do-you-connect-to-a-vm-in-azure-using-rdp"></a>Wie stelle ich über RDP eine Verbindung mit einer VM in Azure her?

Die Verbindungsherstellung mit einer VM in Azure über RDP ist ein einfacher Vorgang. Wechseln Sie im Azure-Portal zu den Eigenschaften Ihrer VM, und klicken Sie oben auf **Verbinden**. Durch diese Aktion wird eine vorkonfigurierte RDP-Datei heruntergeladen, die Windows dann im RDP-Client öffnet. Sie können die Verbindung über die öffentliche IP-Adresse der VM in der RDP-Datei herstellen. Wenn Sie die Verbindung per VPN oder ExpressRoute herstellen, können Sie alternativ die interne IP-Adresse auswählen. Sie können außerdem die Portnummer für die Verbindung festlegen.

Wenn Sie für die VM eine statische öffentliche IP-Adresse verwenden, können Sie die RDP-Datei auf Ihrem Desktop speichern. Wenn Sie eine dynamische IP-Adressierung verwenden, ist die RDP-Datei nur während der Ausführung der VM gültig. Wenn Sie die VM beenden und neu starten, müssen Sie eine weitere RDP-Datei herunterladen.

> [!Note]
> Sie können die öffentliche IP-Adresse der VM auch im Windows RDP-Client eingeben und auf **Verbinden** klicken.

Bei der Verbindungsherstellung werden typischerweise zwei Warnungen angezeigt. Dies sind:

* Herausgeberwarnung: Diese Warnung wird verursacht, weil die RDP-Datei nicht öffentlich signiert ist.
* Zertifikatwarnung: Diese Warnung wird verursacht, weil das Computerzertifikat nicht als vertrauenswürdig eingestuft wird.

In Testumgebungen können diese Warnungen ignoriert werden. In Produktionsumgebungen kann die RDP-Datei mithilfe von RDPSIGN.EXE signiert und das Computerzertifikat im Speicher **Vertrauenswürdige Stammzertifizierungsstellen** platziert werden.

## <a name="summary"></a>Zusammenfassung

Sie können jetzt über RDP eine Verbindung mit einer Windows-VM herstellen. In der folgenden Übung verwenden Sie RDP zur Verbindungsherstellung mit einer VM und installieren dann eine Serverrolle auf diesem Computer.
