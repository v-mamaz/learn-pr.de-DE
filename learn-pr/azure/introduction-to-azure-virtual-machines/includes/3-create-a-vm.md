Sie haben nun die Netzwerkinfrastruktur geplant und einige virtuelle Computer identifiziert, die zur Cloud migriert werden sollen. Ein virtueller Computer kann auf unterschiedliche Weise erstellt werden. Die Vorgehensweise hängt von Ihrer bevorzugten Umgebung ab. Azure unterstützt zum Erstellen und Verwalten von Ressourcen ein webbasiertes Portal. Des Weiteren können Sie auch Befehlszeilentools nutzen, die unter macOS, Windows und Linux ausgeführt werden können.

> [!TIP]
> Alle Übungen in Microsoft Learn sind kostenlos. Wenn Sie jedoch eigenständig weitere Funktionen nutzen möchten, benötigen Sie ein Azure-Abonnement. Wenn Sie noch nicht über ein Abonnement verfügen, können Sie in wenigen Minuten ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen.

Zunächst werfen Sie einen Blick auf das Azure-Portal, das den einfachsten Einstieg in Azure darstellt.

## <a name="azure-portal"></a>Azure-Portal

Das **Azure-Portal** stellt eine benutzerfreundliche und browserbasierte Benutzeroberfläche bereit, mit dem Sie all Ihre Azure-Ressourcen erstellen und verwalten können. Sie können beispielsweise eine neue Datenbank einrichten, die Rechenleistung Ihrer virtuellen Computer erhöhen und Ihre monatlichen Kosten überwachen. Es ist auch ein großartiges Lerninstrument, da Sie alle verfügbaren Ressourcen auf einen Blick erfassen und Assistenten verwenden können, um benötigte Ressourcen zu erstellen.

Nach der Anmeldung werden zwei Hauptbereiche angezeigt. Der erste ist ein Menü, das Optionen zum Erstellen und Überwachen von Ressourcen sowie zur Abrechnungsverwaltung enthält. Der zweite ist ein anpassbares Dashboard, das eine Momentaufnahme aller grundlegenden Dienste bereitstellt, die Sie in Azure bereitgestellt haben. Wenn Sie vorher noch nicht mit Azure gearbeitet haben, ist das Portal vermutlich die komfortabelste Option für die ersten Schritte.

> [!NOTE]
> Wenn Sie im Portal Optionen auswählen, werden Ansichten angezeigt, die häufig als _Blätter_ bezeichnet werden. Ein Blatt kann sowohl eine Menüstruktur als auch einen Konfigurationsbereich darstellen. Während der Nutzung des Azure-Portals werden neu aufgerufene Benutzeroberflächenelemente immer rechts vom aktuellen Bereich angeordnet. Dabei verschiebt sich der Anzeigebereich, sodass immer das aktuelle Blatt angezeigt wird. Mit dem Schieberegler im unteren Bereich können Sie schnell zu den übergeordneten Ansichten zurückwechseln.

### <a name="create-an-azure-vm-with-the-azure-portal"></a>Erstellen eines virtuellen Azure-Computers über das Azure-Portal

Angenommen, Sie möchten einen virtuellen Computer erstellen, auf dem eine WordPress-Website betrieben wird. Das Einrichten einer Website ist nicht schwierig, doch einige Punkte sind zu bedenken. Sie müssen ein Betriebssystem installieren und konfigurieren, eine Website einrichten, eine Datenbank installieren und sich beispielsweise mit Firewalls befassen. In den nächsten Modulen erhalten Sie ausführliche Informationen zum Erstellen eines virtuellen Computers. Hier erstellen Sie allerdings bereits einen virtuellen Computer, um zu sehen, wie einfach dieser Vorgang ist. Nicht alle Optionen werden an dieser Stelle beschrieben. Eine ausführliche Übersicht zu den einzelnen Optionen finden Sie in den Modulen zum **Erstellen eines virtuellen Computers**.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an. Das Menü zum Erstellen und Verwalten von Azure-Ressourcen wird links angezeigt. Den verbleibenden Bildschirmbereich nimmt das Dashboard ein.

    ![Hauptdashboard des Azure-Portals](../media-draft/3-dashboard-page.png)

1. Klicken Sie oben links auf der Portalseite auf **Ressource erstellen**. Dadurch wird das Blatt „Azure Marketplace“ geöffnet. Wenn die linke Randleiste reduziert ist, wird ein grünes Pluszeichen angezeigt. Sie können die Randleiste erweitern, indem Sie auf das Caretzeichen klicken. Dadurch wird der vollständige Text wie im Bild oben angezeigt.

    ![Der Azure Marketplace](../media-draft/3-create-new-resource.png)

    Wie Sie sehen, werden zahlreiche auswählbare Optionen angezeigt. Zur Erinnerung: Sie möchten einen virtuellen Computer erstellen, auf dem eine WordPress-Website betrieben wird. Virtuelle Computer sind Azure-Computeressourcen. Wählen Sie daher **Compute** aus der Liste der verfügbaren Optionen aus, und suchen Sie anschließend nach Images für virtuelle WordPress-Computer.

1. Geben Sie in der Suchleiste **Marketplace durchsuchen** „WordPress“ ein. Nun sollte eine Liste mit Optionen angezeigt werden. Wählen Sie die Option **WordPress Certified by Bitnami** aus.

    ![Durchsuchen des Azure Marketplace](../media-draft/3-search-vm-image.png)

    Im neu geöffneten Blatt werden nun Lizenzinformationen für das Image angezeigt, das Sie im Folgenden verwenden. Klicken Sie auf **Erstellen**.

    ![Auswählen und Erstellen der WordPress-Website](../media-draft/3-create-vm-image.png)

1. Das Blatt **Virtuellen Computer erstellen** wird angezeigt. Zum Konfigurieren des virtuellen Computers können Sie einen Assistenten verwenden.

    ![Konfigurationsschritt 1](../media-draft/3-create-vm-1.png)

    Zunächst müssen Sie die grundlegenden Parameter des virtuellen Computers für WordPress konfigurieren. Wenn Sie mit einigen Optionen noch nicht vertraut sind, ist das kein Problem. Alle Optionen werden in einem weiteren Modul beschrieben. Sie können die hier verwendeten Werte gerne kopieren.

<!-- TODO: fix subscription + resource group -->
1. Nutzen Sie die folgenden Werte auf der Registerkarte **Basics** (Grundeinstellungen).
    - Wählen Sie das kostenlose Abonnement und eine Ressourcengruppe aus.
    - Geben Sie einen **Namen** für den virtuellen Computer ein. Im Beispiel wurde `test-wp1-eus-vm` verwendet.
    - Wählen Sie eine **Region** in Ihrer Nähe aus. Über die Dropdownliste können Sie einen Ort auswählen.
    - Wählen Sie als Verfügbarkeitsoption **Keine** aus. Diese Option ist für Hochverfügbarkeit relevant, die in einem anderen Modul behandelt wird.
    - Für **Image** sollte die Option **Wordpress by Bitnami** festgelegt werden, die Sie im Marketplace ausgewählt haben.
    - Verwenden Sie für **Größe** den Standardwert. Dadurch können Sie einen Kern und 3,5 GB Speicher nutzen, was für eine einfache Website ausreichend sein sollte.
    - Legen Sie für den Authentifizierungstyp **Kennwort** fest, und geben Sie einen Benutzernamen und ein Kennwort ein.
    - Wählen Sie wie unten gezeigt über die Dropdownliste **Öffentliche Eingangsports hinzufügen** den Eintrag **http** aus.

    ![Öffnen des HTTP-Ports](../media-draft/3-open-http-port.png)

1. Sie können noch weitere Registerkarten mit Einstellungen aufrufen, die Sie während der Erstellung des virtuellen Computers anpassen können. Klicken Sie abschließend auf **Überprüfen + erstellen**, um die Einstellungen zu überprüfen.

    ![Konfigurationsschritt 2](../media-draft/3-review-create-vm.png)

1. Auf dem Überprüfungsbildschirm überprüft Azure Ihre Einstellungen. Stellen Sie sicher, dass alle Einstellungen korrekt sind, und klicken Sie anschließend auf **Erstellen**, um den virtuellen Computer zu erstellen und bereitzustellen.

1. Sie können den Bereitstellungsstatus über den Bereich **Benachrichtigungen** überwachen. Klicken Sie auf das Symbol in der oberen Symbolleiste, um den Bereich anzuzeigen.

    ![Überwachen des Bereitstellungsstatus](../media-draft/3-deploying.png)

1. Der Bereitstellungsprozess für den virtuellen Computer kann einige Minuten in Anspruch nehmen. Nachdem die Bereitstellung erfolgreich abgeschlossen wurde, erhalten Sie eine Benachrichtigung. Klicken Sie auf die Nachricht, um zur Ressourcengruppe mit allen Elementen zu wechseln, die für Ihren virtuellen Computer erstellt wurden.

    ![Virtueller Computer wurde bereitgestellt](../media-draft/3-deployment-succeeded.png)

1. Wählen Sie den Eintrag für den virtuellen Computer aus. Der Eintrag sollte ganz oben mit dem angegebenen Namen angezeigt werden.

    ![Wählen Sie in der Ressourcengruppe den virtuellen Computer aus.](../media-draft/3-open-vm-properties.png)

1. Dadurch wird für den erstellten virtuellen Computer die **Übersicht** aufgerufen. Hier sehen Sie alle Informationen und Konfigurationsoptionen für den neu erstellten virtuellen Computer für WordPress. Dazu gehört auch die Angabe für **Öffentliche IP-Adresse**.

    ![Aufrufen der öffentlichen IP-Adresse zur Nutzung des virtuellen Computers](../media-draft/3-public-ip-address.png)

1. Kopieren Sie die IP-Adresse, öffnen Sie eine neue Registerkarte in Ihrem Browser, und fügen Sie die Adresse ein. Die neue WordPress-Website sollte geöffnet werden.

    ![Neue Wordpress-Website ist aktiv.](../media-draft/3-my-new-blog.png)

Herzlichen Glückwunsch! Sie haben in wenigen Schritten einen virtuellen Linux-Computer bereitgestellt, auf dem eine Datenbank installiert ist und auf dem eine funktionsfähige Website betrieben wird. Im Folgenden erfahren Sie, welche anderen Möglichkeiten Sie nutzen können, um einen virtuellen Computer zu erstellen.