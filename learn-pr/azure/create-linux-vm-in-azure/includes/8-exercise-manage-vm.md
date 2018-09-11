Wenden wir eine Netzwerksicherheitsgruppe auf unser Netzwerk an, um ausschließlich HTTP-Datenverkehr über unsere Server zuzulassen.

## <a name="create-a-network-security-group"></a>Erstellen einer Netzwerksicherheitsgruppe

Aufgrund der Angabe, dass wir SSH-Zugriff benötigen, sollte Azure eine Sicherheitsgruppe für uns erstellt haben. Wir erstellen hier jedoch eine neue Sicherheitsgruppe, damit Sie sich mit dem gesamten Prozess vertraut machen können. Das ist besonders wichtig, wenn Sie Ihr virtuelles Netzwerk _vor_ Ihren virtuellen Computern erstellen möchten. Zur Erinnerung: Sicherheitsgruppen sind _optional_ und werden nicht unbedingt zusammen mit dem Netzwerk erstellt.

1. Klicken Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) auf der linken Randleiste auf die Schaltfläche **Ressource erstellen**, um die Ressourcenerstellung zu starten.

1. Geben Sie „Netzwerksicherheitsgruppe“ in das Filterfeld ein, und wählen Sie das entsprechende Element in der Liste aus.

1. Vergewissern Sie sich, dass das Bereitstellungsmodell **Resource Manager** ausgewählt ist, und klicken Sie auf **Erstellen**.

1. Geben Sie unter **Name** einen Namen für Ihre Sicherheitsgruppe an. Auch hier empfiehlt sich die Verwendung einer Namenskonvention. Wir verwenden also „test-web-eus-nsg1“ für die erste Web-Netzwerksicherheitsgruppe zu Testzwecken in der Region „USA, Osten“. Ändern Sie bei Bedarf den Standortteil, um den Standort Ihrer Sicherheitsgruppe anzugeben.

1. Wählen Sie das richtige **Abonnement** aus, und verwenden Sie Ihre bereits vorhandene **Ressourcengruppe**.

1. Platzieren Sie sie abschließend am gleichen **Standort** wie den virtuellen Computer bzw. das virtuelle Netzwerk. Dies ist wichtig, da Sie diese Ressource andernfalls nicht anwenden können.

1. Klicken Sie auf **Erstellen**, um die Gruppe zu erstellen.

## <a name="add-a-new-inbound-rule-to-our-network-security-group"></a>Hinzufügen einer neuen Regel für eingehenden Datenverkehr zur Netzwerksicherheitsgruppe

Die Bereitstellung sollte schnell abgeschlossen sein.

1. Suchen Sie im Azure-Portal nach der neuen Sicherheitsgruppenressource, und wählen Sie sie aus.

1. Auf der Übersichtsseite sehen Sie, dass einige Standardregeln zum Sperren des Netzwerks erstellt wurden.

    Eingangsseite:

    - Sämtlicher eingehender Datenverkehr zwischen zwei VNETs wird zugelassen. So können Ressourcen im VNET miteinander kommunizieren.
    - Azure Load Balancer sendet Testanforderungen, um zu überprüfen, ob die VM aktiv ist.
    - Anderer eingehender Datenverkehr wird vollständig unterbunden.
    Ausgangsseite:
    - Der gesamte eingehende Netzwerkdatenverkehr im VNET wird zugelassen.
    - Sämtlicher ausgehender Datenverkehr ins Internet wird zugelassen.
    - Jeglicher andere ausgehende Datenverkehr wird unterbunden.

> [!NOTE]
> Da diese Standardregeln mit hohen Prioritätswerten festgelegt sind, werden sie _zuletzt_ ausgewertet. Diese Regeln können weder geändert noch gelöscht werden. Sie können die Regeln aber _überschreiben_, indem Sie spezifischere Regeln für Ihren Datenverkehr mit einem niedrigeren Prioritätswert erstellen.

1. Klicken Sie im Bereich **Einstellungen** für die Sicherheitsgruppe auf den Abschnitt **Eingangssicherheitsregeln**.

1. Klicken Sie auf **+ Hinzufügen**, um eine neue Sicherheitsregel hinzuzufügen.

    ![Hinzufügen einer Sicherheitsregel](../media-drafts/8-add-rule.png)

    Es gibt zwei Optionen für die Eingabe der Informationen für eine Sicherheitsregel: im einfachen oder im erweiterten Modus. Zwischen diesen beiden Modi kann mithilfe der Schaltfläche im oberen Bereich des Bereichs „Hinzufügen“ gewechselt werden.

    ![Regeleingabe: einfacher vs.   erweiterter Modus](../media-drafts/8-advanced-create-rule.png)

    Im erweiterten Modus kann die Regel vollständig angepasst werden. Wenn Sie allerdings ein bekanntes Protokoll konfigurieren möchten, ist der einfache Modus benutzerfreundlicher.

1. Wechseln Sie in den einfachen Modus.

1. Fügen Sie die Informationen für die HTTP-Regel hinzu.

    - Legen Sie den **Dienst** auf „HTTP“ fest. Dadurch wird der Portbereich automatisch eingerichtet.
    - Legen Sie die **Priorität** auf „1.000“ fest. Der Wert muss niedriger sein als der Wert der Regel **Verweigern**. Der Bereich kann bei einem beliebigen Wert beginnen. Allerdings wird empfohlen, einen gewissen Puffer einzubauen, falls später eine Ausnahme erstellt werden muss.
    - Benennen Sie die Regel. Wir verwenden hier den Namen „allow-http-traffic“.
    - Geben Sie eine Beschreibung für die Regel ein.

1. Kehren Sie zum Modus **Erweitert** zurück. Wie Sie sehen, sind unsere Einstellungen immer noch vorhanden. In diesem Bereich können Sie differenziertere Einstellungen erstellen. Sie können beispielsweise die **Quelle** auf eine bestimmte IP-Adresse oder auf einen bestimmten IP-Adressbereich für die Kameras beschränken. Wenn Sie die aktuelle IP-Adresse Ihres lokalen Computers kennen, können Sie das ausprobieren. Behalten Sie andernfalls die Einstellung „Beliebig“ bei, um die Regel zu testen.

1. Klicken Sie auf **Hinzufügen**, um die Regel zu erstellen. Dadurch wird die Eingangsregelliste aktualisiert. Die Regeln werden nach Priorität sortiert und in der angezeigten Reihenfolge ausgewertet.
    
## <a name="apply-the-security-group"></a>Anwenden der Sicherheitsgruppe

Zur Erinnerung: Eine Sicherheitsgruppe lässt sich auf eine Netzwerkschnittstelle anwenden, um einen einzelnen virtuellen Computer zu schützen, oder auf ein Subnetz, um alle Ressourcen dieses Subnetzes zu schützen. Der zweite Fall ist gängiger, daher verwenden wir ihn hier. Zu der Ressource in Azure gelangen wir entweder über die Ressource des virtuellen Netzwerks oder indirekt über den virtuellen Computer, der das virtuelle Netzwerk verwendet.

1. Wechseln Sie zum Bereich **Übersicht** für den virtuellen Computer. Den virtuellen Computer finden Sie unter **Alle Ressourcen**.

1. Klicken Sie im Abschnitt **Einstellungen** auf das Element **Netzwerk**.

    ![Element „Netzwerk“ in den VM-Einstellungen](../media-drafts/8-network-settings.png)

1. In den Netzwerkeigenschaften finden Sie Informationen zum Netzwerk des virtuellen Computers – einschließlich **Virtuelles Netzwerk/Subnetz**. Hierbei handelt es sich um einen klickbaren Link, über den Sie zu der Ressource gelangen. Klicken Sie auf den Link, um das virtuelle Netzwerk zu öffnen. Dieser Link steht _auch_ im Bereich **Übersicht** des virtuellen Computers zur Verfügung. Beide Links öffnen die **Übersicht** des virtuellen Netzwerks.

1. Klicken Sie im Abschnitt **Einstellungen** auf das Element **Subnetze**.

1. Hier sollte ein einzelnes Subnetz (Standard) definiert sein, das zuvor zusammen mit dem virtuellen Computer und dem virtuellen Netzwerk erstellt wurde. Klicken Sie auf das Listenelement, um die Details zu öffnen.

1. Klicken Sie auf den Eintrag **Netzwerksicherheitsgruppe**.

1. Wählen Sie Ihre neue Sicherheitsgruppe (**test-web-eus-nsg1**) aus. Hier sollte sich noch eine weitere Gruppe befinden, die zusammen mit dem virtuellen Computer erstellt wurde.

1. Klicken Sie auf **Speichern**, um die Änderung zu speichern. Die Anwendung auf das Netzwerk nimmt etwas Zeit in Anspruch.

## <a name="verify-the-rules"></a>Überprüfen der Regeln

Im nächsten Schritt überprüfen wir die Änderung.

1. Kehren Sie zum Bereich **Übersicht** für den virtuellen Computer zurück. Den virtuellen Computer finden Sie unter **Alle Ressourcen**.

1. Klicken Sie im Abschnitt **Einstellungen** auf das Element **Netzwerk**.

1. Über den Link **Effektive Sicherheitsregeln** im Bereich **Übersicht** für das Netzwerk können Sie schnell überprüfen, wie Regeln ausgewertet werden. Klicken Sie auf den Link, um die Analyse zu öffnen, und überprüfen Sie, ob die neue Regel vorhanden ist.

    ![Effektive Sicherheitsregeln für das Netzwerk](../media-drafts/8-effective-rules.png)

1. Ob alles funktioniert, lässt sich natürlich am besten überprüfen, indem eine HTTP-Anforderung an den Server gesendet wird. Dies sollte weiterhin funktionieren. Sie können sogar die Regel **HTTP** löschen, um zu überprüfen, ob die Sicherheitsgruppenregeln nun angewendet werden.

## <a name="one-more-thing"></a>Anmerkung:

Die richtige Implementierung von Sicherheitsregeln ist nicht immer ganz einfach. Beim Anwenden dieser neuen Sicherheitsgruppe ist uns ein Fehler unterlaufen: Wir haben den SSH-Zugriff verloren. Zur Behebung dieses Problems können Sie der Sicherheitsgruppe eine weitere Regel hinzufügen, um den SSH-Zugriff zu unterstützen. Achten Sie darauf, die eingehenden TCP/IP-Adressen für die Regel auf Ihre eigenen Adressen zu beschränken.

> [!WARNING]
> Denken Sie immer daran, für den Administratorzugriff verwendete Ports zu sperren. Noch besser: Erstellen Sie ein VPN, um das virtuelle Netzwerk mit Ihrem privaten Netzwerk zu verbinden, und lassen Sie nur RDP- oder SSH-Anforderungen aus diesem Adressbereich zu. Sie können auch die Standardeinstellung für den von SSH verwendeten Port ändern. Denken Sie aber daran, dass eine Portänderung noch keine ausreichende Angriffsabwehr darstellt, sondern lediglich die Portermittlung erschwert.