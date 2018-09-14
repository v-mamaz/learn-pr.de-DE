Sie haben nun die Netzwerkinfrastruktur geplant und einige virtuelle Computer identifiziert, die zur Cloud migriert werden sollen. Ein virtueller Computer kann auf unterschiedliche Weise erstellt werden. Die Vorgehensweise hängt von Ihrer bevorzugten Umgebung ab. Azure unterstützt zum Erstellen und Verwalten von Ressourcen ein webbasiertes Portal. Des Weiteren können Sie auch Befehlszeilentools nutzen, die unter macOS, Windows und Linux ausgeführt werden können.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

Zunächst werfen Sie einen Blick auf das Azure-Portal, das den einfachsten Einstieg in Azure darstellt.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="azure-portal"></a>Azure-Portal

Die **Azure-Portal** bietet eine einfache zu bedienende browserbasierte Benutzeroberfläche, mit dem Sie zum Erstellen und Verwalten Ihrer Azure-Ressourcen. Sie können beispielsweise eine neue Datenbank einrichten, die Rechenleistung Ihrer virtuellen Computer erhöhen und Ihre monatlichen Kosten überwachen. Es ist auch ein großartiges Tool, da Sie geführte Assistenten verwenden, um diejenigen zu erstellen, die Sie benötigen und befragen alle verfügbare Ressourcen können.

Nach der Anmeldung werden zwei Hauptbereiche angezeigt. Die erste ist ein Menü mit den Optionen können Sie das Erstellen von Ressourcen, Ressourcen zu überwachen und Verwalten der Abrechnung. Der zweite ist ein anpassbares Dashboard, das eine Momentaufnahme aller grundlegenden Dienste bereitstellt, die Sie in Azure bereitgestellt haben. Wenn Sie vorher noch nicht mit Azure gearbeitet haben, ist das Portal vermutlich die komfortabelste Option für die ersten Schritte.

> [!TIP]
> Wenn Sie im Portal Optionen auswählen, werden Ansichten angezeigt, die häufig als _Blätter_ bezeichnet werden. Ein Blatt kann sowohl eine Menüstruktur als auch einen Konfigurationsbereich darstellen. Wie Sie in der gesamten Azure-Portal navigieren, Benutzeroberfläche wird von links nach rechts gestapelt werden, und Web Viewport wird über schieben Sie das aktuelle Blatt angezeigt. Mit dem Schieberegler im unteren Bereich können Sie schnell zu den übergeordneten Ansichten zurückwechseln.

### <a name="create-an-azure-vm-with-the-azure-portal"></a>Erstellen eines virtuellen Azure-Computers über das Azure-Portal

Angenommen, Sie möchten einen virtuellen Computer erstellen, auf dem eine WordPress-Website betrieben wird. Das Einrichten einer Website ist nicht schwierig, doch einige Punkte sind zu bedenken. Sie müssen ein Betriebssystem installieren und konfigurieren, eine Website einrichten, eine Datenbank installieren und sich beispielsweise mit Firewalls befassen. In den nächsten Modulen erhalten Sie ausführliche Informationen zum Erstellen eines virtuellen Computers. Hier erstellen Sie allerdings bereits einen virtuellen Computer, um zu sehen, wie einfach dieser Vorgang ist. Nicht alle Optionen werden an dieser Stelle beschrieben. Eine ausführliche Übersicht zu den einzelnen Optionen finden Sie in den Modulen zum **Erstellen eines virtuellen Computers**.

#### <a name="select-a-location"></a>Standort auswählen

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an. Sie sehen im Azure-Ressourcen erstellen und Verwalten von-Menü auf der linken und das Dashboard, füllen den Rest des Bildschirms.

    ![Hauptdashboard des Azure-Portals](../media-draft/3-dashboard-page.png)

1. Klicken Sie oben links auf der Portalseite auf **Ressource erstellen**. Dadurch wird das Blatt „Azure Marketplace“ geöffnet. Wenn die linke Randleiste reduziert ist, wird ein grünes Pluszeichen angezeigt. Sie können die Randleiste erweitern, indem Sie auf das Caretzeichen klicken. Dadurch wird der vollständige Text wie im Bild oben angezeigt.

    ![Der Azure Marketplace](../media-draft/3-create-new-resource.png)

    Wie Sie sehen, werden zahlreiche auswählbare Optionen angezeigt. Beachten Sie, dass einen virtueller Computer mit einer WordPress-Website erstellt werden soll. Virtuelle Computer sind Azure-Computeressourcen. Wählen Sie daher **Compute** aus der Liste der verfügbaren Optionen aus, und suchen Sie anschließend nach Images für virtuelle WordPress-Computer. Klicken Sie auf **alle** um die vollständige Liste zu erhalten.

1. Verwenden der **suchen Sie im Marketplace** Suchleiste, und suchen Sie nach "WordPress". Nun sollte eine Liste mit Optionen angezeigt werden. Wählen Sie die Option **WordPress Certified by Bitnami** aus.

    ![Durchsuchen des Azure Marketplace](../media-draft/3-search-vm-image.png)

    Im neu geöffneten Blatt werden nun Lizenzinformationen für das Image angezeigt, das Sie im Folgenden verwenden. Klicken Sie auf **Erstellen**.

    ![Wählen Sie aus, und erstellen Sie die WordPress-Website](../media-draft/3-create-vm-image.png)

1. Daraufhin die **erstellen virtuellen Computer** Blatt. Zum Konfigurieren des virtuellen Computers können Sie einen Assistenten verwenden.

    ![Konfigurationsschritt 1](../media-draft/3-create-vm-1.png)

    Zunächst müssen Sie die grundlegenden Parameter des virtuellen Computers für WordPress konfigurieren. Wenn einige der Optionen für Sie an diesem Punkt auskennen, ist, das in Ordnung. Alle Optionen werden in einem weiteren Modul beschrieben. Sie können die hier verwendeten Werte gerne kopieren.

1. Nutzen Sie die folgenden Werte auf der Registerkarte **Basics** (Grundeinstellungen).
    - Wählen Sie das kostenlose Abonnement und die <rgn>[Ressourcengruppennamen Sandkasten]</rgn> Ressourcengruppe aus.
    - Geben Sie einen **Namen** für den virtuellen Computer ein. Im Beispiel wurde `test-wp1-eus-vm` verwendet.
    - Wählen Sie eine **Region** in Ihrer Nähe aus. Stellen Sie sicher, dass Sie einen Speicherort aus der Liste oben aus der Dropdown-Liste angegebenen auswählen.
    - Wählen Sie als Verfügbarkeitsoption **Keine** aus. Dies ist für hohe Verfügbarkeit, die wir in einem anderen Modul zu behandeln.
    - Die **Image** muss die **WordPress von Bitnami** Option, die wir aus dem Marketplace ausgewählt.
    - Lassen Sie die **Größe** als Standard - haben Sie einen einzelnen Kern und 3,5 GB Arbeitsspeicher, der für eine einfache Website ausreichend sein soll.
    - Wechseln Sie zur **Kennwort** für die Authentifizierung geben Sie an, und geben Sie Benutzername und Kennwort.
    - Wählen Sie **lassen Sie die ausgewählten Ports**, wählen Sie dann in der Dropdown-Liste **http**.

    ![Öffnen des HTTP-Ports](../media-draft/3-open-http-port.png)

1. Sie können noch weitere Registerkarten mit Einstellungen aufrufen, die Sie während der Erstellung des virtuellen Computers anpassen können. Klicken Sie abschließend auf **Überprüfen + erstellen**, um die Einstellungen zu überprüfen.

    ![Konfigurationsschritt 2](../media-draft/3-review-create-vm.png)

1. Auf dem Überprüfungsbildschirm überprüft Azure Ihre Einstellungen. Überprüfen Sie alle Einstellungen sind legen Sie die Möglichkeit, Sie möchten, und klicken Sie dann auf **erstellen** bereitstellen und den virtuellen Computer erstellen.

1. Sie können den Bereitstellungsstatus über den Bereich **Benachrichtigungen** überwachen. Klicken Sie auf das Symbol in der oberen Symbolleiste, um den Bereich anzuzeigen.

    ![Überwachen des Bereitstellungsstatus](../media-draft/3-deploying.png)

1. Der Bereitstellungsprozess für den virtuellen Computer kann einige Minuten in Anspruch nehmen. Nachdem die Bereitstellung erfolgreich abgeschlossen wurde, erhalten Sie eine Benachrichtigung. Klicken Sie auf die Nachricht, um zur Ressourcengruppe mit allen Elementen zu wechseln, die für Ihren virtuellen Computer erstellt wurden.

    ![Virtueller Computer wurde bereitgestellt](../media-draft/3-deployment-succeeded.png)

1. Wählen den VM-Eintrag – wird die erste Bedingung, und muss den Namen, die, den Sie angegeben haben.

    ![Wählen Sie in der Ressourcengruppe den virtuellen Computer aus.](../media-draft/3-open-vm-properties.png)

1. Dadurch wird für den erstellten virtuellen Computer die **Übersicht** aufgerufen. Hier sehen Sie alle Informationen und Konfigurationsoptionen für den neu erstellten virtuellen Computer für WordPress. Dazu gehört auch die Angabe für **Öffentliche IP-Adresse**.

    ![Aufrufen der öffentlichen IP-Adresse zur Nutzung des virtuellen Computers](../media-draft/3-public-ip-address.png)

11. Kopieren Sie die IP-Adresse, öffnen Sie eine neue Registerkarte in Ihrem Browser, und fügen Sie die Adresse ein. Sie sollten in einer ganz neuen WordPress-Website zu durchsuchen.

    ![Neue WordPress-Website ist aktiv.](../media-draft/3-my-new-blog.png)

Herzlichen Glückwunsch! Mit wenigen Schritten haben Sie einen virtuellen Computer, die Linux ausführt, verfügt über eine Datenbank, die installiert und verfügt über eine funktionsfähige Website bereitgestellt. Im Folgenden erfahren Sie, welche anderen Möglichkeiten Sie nutzen können, um einen virtuellen Computer zu erstellen.
