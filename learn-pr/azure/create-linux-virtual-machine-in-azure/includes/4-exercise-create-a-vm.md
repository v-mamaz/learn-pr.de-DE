Zur Erinnerung: Wir möchten einen vorhandenen Linux-Server, auf dem Apache ausgeführt wird, zu Azure migrieren. Dazu erstellen wir zunächst einen Ubuntu Linux-Server.

## <a name="create-a-new-linux-virtual-machine"></a>Erstellen eines neuen virtuellen Linux-Computers

Virtuelle Linux-Computer können über das Azure-Portal, mithilfe der Azure CLI oder unter Verwendung von Azure PowerShell erstellt werden. Die einfachste Methode für Azure-Neulinge ist das Portal, da es Sie Schritt für Schritt durch die Erstellung führt sowie Hinweise und hilfreiche Meldungen bereithält:

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Klicken Sie im Azure-Portal oben links auf **Ressource erstellen**.

1. Geben Sie **Ubuntu Server** in das Suchfeld ein, um die verfügbaren Versionen anzuzeigen. Wählen Sie in der angezeigten Liste die Option **Ubuntu Server 18.04** aus.

1. Klicken Sie auf die Schaltfläche **Erstellen**, um mit dem Konfigurieren des virtuellen Computers zu beginnen.

## <a name="configure-the-vm-settings"></a>Konfigurieren der Einstellungen für den virtuellen Computer

Im Portal steht für die VM-Erstellung ein **Assistent** zur Verfügung, der Sie durch sämtliche Konfigurationsbereiche für den virtuellen Computer führt. Wenn Sie auf die Schaltfläche **Weiter** klicken, gelangen Sie jeweils zum nächsten Konfigurationsabschnitt. Sie können allerdings auch über die Registerkarten im oberen Bereich zwischen den einzelnen Bereichen wechseln.

![Screenshot des Azure-Portals mit dem anfänglichen Blatt „Virtuellen Computer erstellen“ für einen Ubuntu Server-Computer](../media/3-azure-portal-create-vm.png)

Sobald Sie alle erforderlichen Optionen (durch rote Sternchen gekennzeichnet) angegeben haben, können Sie die verbleibenden Schritte des Assistenten überspringen und im unteren Bereich auf die Schaltfläche **Überprüfen + erstellen** klicken, um mit der Erstellung des virtuellen Computers zu beginnen.

Beginnen Sie mit dem Abschnitt **Grundlagen**.

### <a name="configure-basic-vm-settings"></a>Konfigurieren der Grundeinstellungen für den virtuellen Computer

1. Wählen Sie das **Abonnement** aus, über das die VM-Stunden abgerechnet werden sollen.

1. Klicken Sie für **Ressourcengruppe** auf **Neu erstellen**, und geben Sie der Ressourcengruppe den Namen **ExerciseResources**.

> [!NOTE]  
> Wenn Sie die Einstellungen ändern und anschließend die TAB-TASTE drücken, überprüft Azure den Wert automatisch und versieht ihn mit einem grünen Häkchen, wenn die Änderungen akzeptiert werden. Sie können mit der Maus auf Fehlersymbole zeigen, um weitere Informationen zu gefundenen Problemen zu erhalten.

1. Geben Sie im Abschnitt **INSTANZENDETAILS** einen Namen für Ihre Webserver-VM ein (z.B. **test-web-eus-vm1**). Dieser Name gibt die Umgebung (**test**), die Rolle (**web**), den Standort (**eus; USA, Osten**), den Dienst (**vm**) und die Instanznummer (**1**) an.
    - Als bewährte Methode empfiehlt sich, Ressourcennamen zu standardisieren, um sofort ihren Zweck ermitteln zu können. Namen für Linux-VMs müssen zwischen 1 und 64 Zeichen lang sein und sich aus Zahlen, Buchstaben und Bindestrichen zusammensetzen.

1. Wählen Sie eine Region in Ihrer Nähe aus. Hier haben wir uns für **USA, Osten** entschieden.

1. Behalten Sie für die **Verfügbarkeitsoptionen** die Einstellung **Keine** bei. Diese Option wird verwendet, um sicherzustellen, dass der virtuelle Computer hochverfügbar ist. Zu diesem Zweck werden mehrere virtuelle Computer in einer Gruppe zusammengefasst, um geplante oder ungeplante Wartungsereignisse oder Ausfälle zu verarbeiten.

1. Vergewissern Sie sich, dass das Image auf **Ubuntu Server 18.04 LTS** festgelegt ist. Sie können die Dropdownliste öffnen, um alle verfügbaren Optionen anzuzeigen.

1. Das Feld **Größe** kann nicht direkt bearbeitet werden und enthält standardmäßig die Größe **DS2_v3** (eine der universellen Computingoptionen). Diese Option ist für einen öffentlichen Webserver optimal. Klicken Sie aber trotzdem auf den Link **Größe ändern**, um sich die anderen VM-Größen anzusehen. Im daraufhin angezeigten Dialogfeld können Sie nach der **Anzahl von CPUs**, nach **Name** und nach **Datenträgertyp** filtern. Wählen Sie die Option **DS2_v3** aus, um zwei vCPUs mit 8 GB RAM zu erhalten.

    > [!TIP]
    > Da auf der rechten Seite ein neues Fenster geöffnet und über das vorherige Fenster geschoben wurde, um es anzuzeigen, können Sie die Ansicht auch nach links verschieben, um wieder zu den VM-Einstellungen zu gelangen.

1. Wählen Sie im Abschnitt **ADMINISTRATORZUGRIFF** für **Authentifizierungstyp** die Option „Öffentlicher SSH-Schlüssel“ aus.

1. Geben Sie unter **Benutzername** einen Benutzernamen für die SSH-Anmeldung ein.

1. Kopieren Sie den SSH-Schlüssel aus Ihrer Datei mit dem öffentlichen Schlüssel, und fügen Sie ihn in das Feld **Öffentlicher SSH-Schlüssel** ein.

> [!IMPORTANT]
> Achten Sie beim Kopieren des öffentlichen Schlüssels in das Azure-Portal darauf, keine zusätzlichen Leerräume oder Zeilenvorschubzeichen hinzuzufügen.

1. Öffnen Sie die Liste im Abschnitt **REGELN FÜR EINGEHENDE PORTS**, und deaktivieren Sie die Option **Keine**. Da es sich hier um eine Linux-VM handelt, soll die Möglichkeit bestehen, per SSH-Remoteverbindung auf die VM zuzugreifen. Wählen Sie in der Liste die Option **ssh (22)** aus. Unter Umständen müssen Sie dazu scrollen. Auf der Benutzeroberfläche wird der Hinweis angezeigt, dass auch nach dem Erstellen des virtuellen Computers die Netzwerkports geändert werden können.

    ![Screenshot des Azure-Portals mit dem Administratorkonto und den Einstellungen für Eingangsports zum Herstellen einer SSH-Verbindung mit einer Linux-VM](../media/3-open-ports.png) 

## <a name="configure-disks-for-the-vm"></a>Konfigurieren von Datenträgern für den virtuellen Computer

1. Klicken Sie auf **Weiter**, um zum Abschnitt **Datenträger** zu navigieren.

    ![Screenshot, auf dem das Azure-Portal und der Abschnitt „Datenträger“ auf dem Blatt „Virtuellen Computer erstellen“ zu sehen sind](../media/3-configure-disks.png) 

1. Wählen Sie **SSD Premium** als **Typ des Betriebssystemdatenträgers** aus.

1. Verwenden Sie verwaltete Datenträger, um nicht mit Speicherkonten arbeiten zu müssen. Wenn Sie wissen möchten, welche unterschiedlichen Informationen Azure jeweils benötigt, können Sie die Einstellung über die grafische Benutzeroberfläche ändern.

### <a name="create-a-data-disk"></a>Erstellen eines Datenträgers

Zur Erinnerung: Wir erhalten einen Betriebssystem-Datenträger (/dev/sda) und einen temporären Datenträger (/dev/sdb). Hier fügen wir auch noch einen Datenträger hinzu:

1. Klicken Sie auf den Link **Create and attach a new disk** (Neuen Datenträger erstellen und anfügen) im Abschnitt **DATENTRÄGER**.

    ![Screenshot des Azure-Portals mit dem Blatt „Neuen Datenträger erstellen“](../media/3-add-data-disk.png) 

1. Sie können alle Standardeinstellungen beibehalten: „SSD Premium“, „1023 GB“ und **Keine** (leerer Datenträger). Beachten Sie jedoch, dass wir an dieser Stelle eine Momentaufnahme oder einen Azure-Blobspeicher verwenden könnten, um eine VHD zu erstellen.

1. Klicken Sie auf **OK**, um den Datenträger zu erstellen, und navigieren Sie zurück zum Abschnitt **DATENTRÄGER**.

1. Es sollte nun ein neuer Datenträger in der ersten Zeile angezeigt werden.

    ![Screenshot des Azure-Portals mit dem neu erstellten Datenträger für den VM-Erstellungsprozess](../media/3-new-disk.png) 

## <a name="configure-the-network"></a>Konfigurieren des Netzwerks

1. Klicken Sie auf **Weiter**, um zum Abschnitt **Netzwerk** zu navigieren.

1. In einem Produktionssystem, in dem bereits andere Komponenten vorhanden sind, sollten Sie ein _vorhandenes_ virtuelles Netzwerk verwenden. So kann Ihr virtueller Computer mit den anderen Clouddiensten in unserer Lösung kommunizieren. Wenn für diesen Standort noch kein Netzwerk definiert ist, können Sie es hier erstellen und die folgenden Bestandteile konfigurieren:
    - **Adressbereich:** der IPv4-Bereich, der dem Netzwerk insgesamt zur Verfügung steht.
    - **Subnetzbereich:** das erste Subnetz, das der Unterteilung des Adressraums dient. Dieses muss innerhalb des definierten Adressraums liegen. Nach der Erstellung des VNet können Sie weitere Subnetze hinzufügen.

> [!NOTE]  
> Azure erstellt standardmäßig ein virtuelles Netzwerk, eine Netzwerkschnittstelle und eine öffentliche IP-Adresse für Ihren virtuellen Computer. Nach der Erstellung des virtuellen Computers können die Netzwerkoptionen nicht mehr problemlos geändert werden. Überprüfen Sie daher immer genau die Netzwerkzuweisungen für die von Ihnen in Azure erstellten Dienste.

## <a name="finish-configuring-the-vm-and-create-the-image"></a>Abschließen der Konfiguration des virtuellen Computers und Erstellen des Images

Die restlichen Optionen verfügen über passende Standardeinstellungen, die nicht geändert werden müssen. Bei Interesse können Sie sich die anderen Registerkarten genauer ansehen. Neben den einzelnen Optionen befindet sich jeweils ein `(i)`-Symbol, über das Sie eine Erläuterung der jeweiligen Option anzeigen können. Dies ist eine gute Möglichkeit, nähere Informationen über die verschiedenen Optionen zu erhalten, die Sie zum Konfigurieren des virtuellen Computers verwenden können:

1. Klicken Sie im unteren Bereich auf die Schaltfläche **Überprüfen + erstellen**.

1. Das System überprüft Ihre Optionen und zeigt Details zur Erstellung des virtuellen Computers an.

1. Klicken Sie auf **Erstellen**, um den virtuellen Computer zu erstellen und bereitzustellen. Im Azure-Dashboard wird der virtuelle Computer angezeigt, der aktuell bereitgestellt wird. Dieser Vorgang kann einige Minuten in Anspruch nehmen.

Währenddessen erfahren Sie in der nächsten Einheit, wozu Sie diesen virtuellen Computer verwenden können.