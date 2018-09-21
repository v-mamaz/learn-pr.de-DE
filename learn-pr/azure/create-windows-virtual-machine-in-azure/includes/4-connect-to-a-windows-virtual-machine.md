Nachdem Sie nun über einen virtuellen Windows-Computer in Azure verfügen, platzieren Sie als Nächstes Ihre Anwendungen und Daten für die Verarbeitung von Verkehrsvideos auf den virtuellen Computern. 

Ohne Site-to-Site-VPN mit Azure kann allerdings nicht über Ihr lokales Netzwerk auf Ihre virtuellen Azure-Computer zugegriffen werden. Wenn Sie sich gerade erst mit Azure vertraut machen, haben Sie wahrscheinlich noch kein Site-to-Site-VPN eingerichtet. Wie können Sie also Dateien auf virtuelle Azure-Computer übertragen? Eine einfache Möglichkeit besteht darin, Ihre lokalen Laufwerke über das Remotedesktopverbindungs-Feature von Azure für Ihre neuen virtuellen Azure-Computer freizugeben.

Nachdem wir nun über einen neuen virtuellen Windows-Computer verfügen, müssen wir darauf unsere benutzerdefinierte Software installieren. Dazu gibt es verschiedene Möglichkeiten.

- Remotedesktopprotokoll (RDP)
- Benutzerdefinierte Skripts
- Benutzerdefinierte VM-Images (mit vorinstallierter Software)

Sehen wir uns den einfachsten Ansatz für virtuelle Windows-Computer an: das Remotedesktopprotokoll.

## <a name="what-is-the-remote-desktop-protocol"></a>Was ist das Remotedesktopprotokoll (RDP)?

Das Remotedesktopprotokoll (RDP) bietet Remotekonnektivität mit der Benutzeroberfläche Windows-basierter Computer. RDP ermöglicht es Ihnen, sich remote bei einem physischen oder virtuellen Windows-Computer anzumelden und diesen Computer so zu steuern, als ob Sie an der Konsole sitzen würden. Eine RDP-Verbindung ermöglicht es Ihnen, die meisten Vorgänge auszuführen, die Sie über die Konsole eines physischen Computers durchführen können. Ausgenommen hiervon sind einige Funktionen in Bezug auf den Betriebszustand und die Hardware.

Für eine RDP-Verbindung wird ein RDP-Client benötigt. Microsoft bietet RDP-Clients für die folgenden Betriebssysteme:

- Windows (integriert)
- macOS
- iOS
- Android

Der folgende Screenshot zeigt den Remotedesktopprotokoll-Client unter Windows 10.

![Screenshot der Benutzeroberfläche des Remotedesktopprotokoll-Clients](../media/4-rdp-client.png)

Es gibt auch Open-Source-Linux-Clients (etwa Remmina), mit denen Sie von einer Ubuntu-Distribution aus eine Verbindung mit einem Windows-PC herstellen können.

## <a name="connecting-to-an-azure-vm"></a>Herstellen einer Verbindung mit einem virtuellen Azure-Computer

Wie Sie bereits gesehen haben, kommunizieren virtuelle Azure-Computer über ein virtuelles Netzwerk. Ihnen kann auch eine optionale öffentliche IP-Adresse zugewiesen werden. Eine öffentliche IP-Adresse ermöglicht die Kommunikation mit dem virtuellen Computer über das Internet. Alternativ können wir ein virtuelles privates Netzwerk (VPN) einrichten, das unser lokales Netzwerk mit Azure verbindet. So können wir eine sichere Verbindung mit dem virtuellen Computer herstellen, ohne eine öffentliche IP-Adresse verfügbar zu machen. Dieser Ansatz wird in einem anderen Modul behandelt und ist vollständig dokumentiert, sollten Sie sich für diese Option interessieren.

Noch ein Hinweis: Öffentliche IP-Adressen werden in Azure häufig dynamisch zugewiesen. Das bedeutet, dass sich die IP-Adresse im Laufe der Zeit ändern kann. Bei virtuellen Computern geschieht das, wenn der virtuelle Computer neu gestartet wird. Sie können gegen Aufpreis statische Adressen zuweisen, wenn Sie eine direkte Verbindung mit einer IP-Adresse anstatt mit einem Namen herstellen möchten und sicherstellen müssen, dass sich die IP-Adresse nicht ändert.

### <a name="how-do-you-connect-to-a-vm-in-azure-using-rdp"></a>Wie stelle ich über RDP eine Verbindung mit einer VM in Azure her?

Die Verbindungsherstellung mit einer VM in Azure über RDP ist ein einfacher Vorgang. Wechseln Sie im Azure-Portal zu den Eigenschaften Ihrer VM, und klicken Sie oben auf **Verbinden**. Dort werden die dem virtuellen Computer zugewiesenen IP-Adressen angezeigt, und Sie können eine vorkonfigurierte **RDP-Datei** herunterladen, die Windows dann im RDP-Client öffnet. Sie können die Verbindung über die öffentliche IP-Adresse der VM in der RDP-Datei herstellen. Wenn Sie die Verbindung per VPN oder ExpressRoute herstellen, können Sie alternativ die interne IP-Adresse auswählen. Sie können außerdem die Portnummer für die Verbindung festlegen.

Wenn Sie für den virtuellen Computer eine statische öffentliche IP-Adresse verwenden, können Sie die **RDP-Datei** auf Ihrem Desktop speichern. Bei Verwendung der dynamischen IP-Adressierung ist die **RDP-Datei** nur gültig, solange der virtuelle Computer aktiv ist. Wenn Sie den virtuellen Computer beenden und neu starten, müssen Sie eine weitere **RDP-Datei** herunterladen.

> [!TIP]
> Sie können die öffentliche IP-Adresse der VM auch im Windows RDP-Client eingeben und auf **Verbinden** klicken.

Bei der Verbindungsherstellung werden typischerweise zwei Warnungen angezeigt. Dies sind:

-**Herausgeberwarnung:** Diese Warnung wird angezeigt, weil die **RDP-Datei** nicht öffentlich signiert ist.
- **Zertifikatwarnung:** Diese Warnung wird angezeigt, weil das Computerzertifikat nicht als vertrauenswürdig eingestuft wird.

In Testumgebungen können diese Warnungen ignoriert werden. In Produktionsumgebungen kann die **RDP-Datei** mithilfe von **RDPSIGN.EXE** signiert und das Computerzertifikat im Speicher **Vertrauenswürdige Stammzertifizierungsstellen** platziert werden.

Als Nächstes stellen wir eine RDP-Verbindung mit dem virtuellen Computer her.