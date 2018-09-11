Wie zuvor bereits erwähnt, verarbeitet das Beispielunternehmen Videoinhalte auf Windows-VMs. Angenommen, eine neue Stadt hat Sie damit beauftragt, die Aufnahmen ihrer Verkehrskameras zu verarbeiten. Es handelt sich allerdings dabei um ein Modell, mit dem Sie zuvor noch nicht gearbeitet haben. Sie müssen eine neue Windows-VM erstellen und proprietäre Codecs installieren, damit Sie mit dem Verarbeiten und Analysieren der Images beginnen können.

## <a name="create-a-new-windows-virtual-machine"></a>Erstellen eines neuen virtuellen Windows-Computers

Sie können Windows-VMs über das Azure-Portal, die Azure CLI oder Azure PowerShell erstellen. Den einfachsten Ansatz stellt das Portal dar, da es Ihnen während des Erstellvorgangs sämtliche erforderlichen Informationen, Hinweise und hilfreiche Nachrichten zur Verfügung stellt.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Klicken Sie im Azure-Portal oben links auf **Ressource erstellen**.

1. Geben Sie **Windows Server 2016 Datacenter** in das Suchfeld ein, und klicken Sie in der anschließend dargestellten Liste auf den gleichnamigen Link.

1. Klicken Sie auf die Schaltfläche **Erstellen**, um mit dem Konfigurieren der VM zu beginnen.

## <a name="configure-the-vm-settings"></a>Konfigurieren der Einstellungen für den virtuellen Computer

Das Portal verfügt über eine Art Assistenten, der Sie während der Erstellung der VM durch sämtliche Konfigurationsbereiche leitet. Wenn Sie auf die Schaltfläche „Weiter“ klicken, gelangen Sie jeweils zum nächsten Konfigurationsabschnitt. Sie können allerdings auch über die Registerkarten im oberen Abschnitt beliebig zwischen den einzelnen Abschnitten wechseln. Für jeden Abschnitt öffnet sich eine eigene Registerkarte.

![Erstellen eines neuen virtuellen Computers im Azure-Portal](../media-drafts/3-azure-portal-create-vm.png)

Sobald Sie alle erforderlichen Optionen (mit roten Sternen kenntlich gemacht) angegeben haben, können Sie die restlichen vom Assistenten beschriebenen Schritte überspringen und mit dem Erstellen der VM über die Schaltfläche **Überprüfen und erstellen** im unteren Bereich beginnen.

Beginnen Sie mit dem Abschnitt **Grundlagen**.

### <a name="configure-basic-vm-settings"></a>Konfigurieren der Grundeinstellungen für den virtuellen Computer

1. Wählen Sie das **Abonnement** aus, über das die VM-Stunden abgerechnet werden sollen.

1. Klicken Sie für **Ressourcengruppe** auf **Neu erstellen**, und geben Sie der Ressourcengruppe den Namen **ExerciseResources**.

> [!NOTE]
> Wenn Sie die Einstellungen ändern und anschließend die TAB-TASTE drücken, prüft Azure den Wert automatisch und platziert einen grünen Haken daneben, wenn die Änderungen akzeptiert werden. Sie können mit der Maus auf Fehlerindikatoren zeigen, um mehr Informationen zu den einzelnen gefundenen Problemen abzurufen.

1. Geben in den Abschnitt **INSTANCE DETAILS** einen Namen für Ihre VM ein, z.B. „test-vp-vm2“ (für die zweite Testprozessor-VM für Videos).
    - Es gilt als bewährte Methode, Ressourcennamen zu standardisieren, damit deren Zweck einfach ermittelt werden kann. Die Namen für Windows-VMs sind eingeschränkt: Sie müssen zwischen 2 und 15 Zeichen umfassen und Zahlen, Buchstaben und Bindestriche aufweisen.

1. Wählen Sie eine Region in Ihrer Nähe aus.

1. Ändern Sie für **Verfügbarkeitsoptionen** nicht die Einstellung „Keine“. Diese Option wird verwendet, um sicherzustellen, dass die VM Hochverfügbarkeit aufweist. Dafür werden mehrere VMs in einer Gruppe zusammengefasst, um geplante oder ungeplante Wartungsereignisse oder Ausfälle zu verarbeiten.

1. Stellen Sie sicher, dass das Image auf „Windows Server 2016 Datacenter“ festgelegt ist. Sie können die Dropdownliste öffnen, um alle verfügbaren Optionen abzurufen.

1. Klicken Sie im Feld **VM-Datenträgertyp** auf das Dropdownmenü, um sich alle Optionen anzeigen zu lassen. Stellen Sie sicher, dass **SSD** ausgewählt ist.

1. Das Feld **Größe** kann nicht direkt bearbeitet werden. Die Standardgröße lautet „DS1“. Klicken Sie auf den Link **Größe ändern**, um andere VM-Größen abzurufen. Über das Dialogfeld, das daraufhin angezeigt wird, können Sie anhand der Anzahl von CPUs sowie anhand der Namen und des Datenträgertyps filtern. Kicken Sie abschließend auf „Standard DS1 v2“ (in der Regel die Standardeinstellung). Dadurch erhält die VM eine CPU und 3,5 GB Arbeitsspeicher.

    > [!TIP]
    > Da auf der rechten Seite ein neues Fenster geöffnet und über das vorherige Fenster geschoben wurde, um es anzuzeigen, können Sie die Ansicht auch nach links verschieben, um wieder zu den VM-Einstellungen zu gelangen.

1. Legen Sie im Abschnitt **ADMINISTRATOR ACCESS** (ADMINISTRATORZUGRIFF) das Feld **Username** (Benutzername) auf den Benutzernamen fest, den Sie verwenden möchten, um sich bei der VM anzumelden.

1. Geben Sie in das Feld **Kennwort** ein Kennwort ein, das mindestens zwölf Zeichen lang ist. Das Kennwort muss drei der folgenden Anforderungen umfassen: ein Kleinbuchstabe, ein Großbuchstabe, eine Ziffer und ein Sonderzeichen (weder „\'“ noch „-“). Verwenden Sie ein Kennwort, das Sie sich merken können, oder schreiben Sie es sich auf. Sie werden es später noch brauchen.

1. Bestätigen Sie das **Kennwort**.

1. Öffnen Sie die Liste im Abschnitt **INBOUND PORT RULES** (REGELN FÜR EINGEHENDE PORTS), und _deaktivieren_ Sie die Option „Keine“. Da es sich dabei um eine Windows-VM handelt, soll die Möglichkeit bestehen, mithilfe eines Remotedesktopprotokolls (RDP) auf den Desktop zuzugreifen. Scrollen Sie wenn nötig durch die Liste, bis Sie das RDP (3389) finden, und wählen Sie es aus. Auf der Benutzeroberfläche wird der Hinweis angezeigt, dass auch nach dem Erstellen der VM die Netzwerkports geändert werden können.

    ![Öffnen des Ports, um auf der Windows-VM Zugriff auf das RDP zu erhalten](../media-drafts/3-open-ports.png)

## <a name="configure-disks-for-the-vm"></a>Konfigurieren von Datenträgern für die VM

1. Klicken Sie auf **Weiter**, um zum Abschnitt „Datenträger“ zu wechseln.

    ![Konfigurieren von Datenträgern für die VM](../media-drafts/3-configure-disks.png)

1. Wählen Sie „SSD Premium“ als **Betriebssystemdatenträgertyp** aus.

1. Verwenden Sie verwaltete Datenträger, damit Sie keine Speicherkonten verwenden müssen. Sie können bei Bedarf in der grafischen Benutzeroberfläche die Einstellung ändern, damit Ihnen die Informationen angezeigt werden, die Azure benötigt.

### <a name="create-a-data-disk"></a>Erstellen eines Datenträgers

Sie erhalten einen Betriebssystemdatenträger (C:) und einen temporären Datenträger (D:). Fügen Sie außerdem einen weiteren Datenträger hinzu.

1. Klicken Sie auf den Link **Create and attach a new disk** (Neuen Datenträger erstellen und anfügen) im Abschnitt **DATA DISKS** (DATENTRÄGER).

    ![Erstellen eines Datenträgers auf der VM im Portal](../media-drafts/3-add-data-disk.png)

1. Sie können sämtliche Standardeinstellungen verwenden: „SSD Premium“, „1023 GB“ und „Keine“ (leerer Datenträger). Beachten Sie allerdings, dass an dieser Stelle eine Momentaufnahme oder Storage Blob hilfreich wären, um eine virtuelle Festplatte zu erstellen.

1. Klicken Sie auf **OK**, um den Datenträger zu erstellen, und navigieren Sie zurück zum Abschnitt **DATA DISKS** (DATENTRÄGER).

1. Es sollte nun ein neuer Datenträger in der ersten Zeile angezeigt werden.

    ![Neuer Datenträger in der VM](../media-drafts/3-new-disk.png)

## <a name="configure-the-network"></a>Konfigurieren des Netzwerks

1. Klicken Sie auf **Weiter**, um zum Abschnitt „Netzwerk“ zu wechseln.

1. In einem Produktionssystem, in dem bereits andere Komponenten vorhanden sind, sollten Sie ein _bereits_ vorhandenes virtuelles Netzwerk verwenden. Auf diese Weise kann Ihre VM mit anderen Clouddiensten in Ihrer Lösung kommunizieren. Wenn für diesen Speicherort noch kein Netzwerk definiert ist, können Sie eins erstellen und folgende Bestandteile konfigurieren:
    - **Den Adressbereich:** der IPv4-Bereich, der dem Netzwerk insgesamt zur Verfügung steht.
    - **Den Subnetzbereich:** das erste Subnetz, das der Unterteilung des Adressbereichs dient. Dieser muss innerhalb des definierten Adressbereichs liegen. Sobald das VNet erstellt ist, können Sie zusätzliche Subnetze hinzufügen.

1. Ändern Sie die Standardbereiche, um den IP-Adressbereich `172.xxx` zu verwenden.
    - Ändern Sie das Feld **Adressbereich** in `172.16.0.0/16`, um diesem den gesamten Adressbereich zuzuweisen.
    - Ändern Sie das Feld **Subnetzbereich** in `172.16.1.0/24`, um ihm 256 IP-Adressen dieses Bereichs zuzuweisen.

> [!NOTE]
> Standardmäßig erstellt Azure ein virtuelles Netzwerk, eine Netzwerkschnittstelle und eine öffentliche IP-Adresse für Ihre VM. Es ist kompliziert, die Netzwerkoptionen zu ändern, nachdem die VM erstellt wurde. Prüfen Sie daher die Netzwerkzuweisungen für die von Ihnen in Azure erstellten Dienste immer genau.

## <a name="finish-configuring-the-vm-and-create-the-image"></a>Abschließen der Konfiguration des virtuellen Computers und Erstellen des Images

Die restlichen Optionen verfügen über passende Standardeinstellungen, die nicht geändert werden müssen. Bei Interesse können sich die anderen Registerkarten genauer ansehen. Die einzelnen Optionen sind mit einem `(i)`-Symbol ausgestattet. Wenn Sie darauf klicken, wird ein Hilfetext angezeigt, in dem die jeweilige Option erläutert wird. Dies ist eine gute Möglichkeit, nähere Informationen über die verschiedenen Optionen zu erhalten, die Sie zum Konfigurieren der VM verwenden können.

1. Klicken Sie im unteren Bereich auf die Schaltfläche **Überprüfen und erstellen**.

1. Dann überprüft das System Ihre Optionen und stellt Ihnen Details zu der VM zur Verfügung, die gerade erstellt wird.

1. Klicken Sie auf **Erstellen**, um die VM zu erstellen und bereitzustellen. Im Azure-Dashboard wird der virtuelle Computer angezeigt, der aktuell bereitgestellt wird. Dieser Vorgang kann einige Minuten dauern.

Währenddessen erfahren Sie in der nächsten Einheit, wozu Sie diese VM verwenden können.