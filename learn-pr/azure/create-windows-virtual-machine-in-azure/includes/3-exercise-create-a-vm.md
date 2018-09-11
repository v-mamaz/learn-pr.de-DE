Wie zuvor bereits erwähnt, verarbeitet das Beispielunternehmen Videoinhalte auf virtuellen Windows-Computern. Angenommen, eine neue Stadt hat Sie damit beauftragt, die Aufnahmen ihrer Verkehrsüberwachungskameras zu verarbeiten. Es handelt sich allerdings dabei um ein Modell, mit dem Sie zuvor noch nicht gearbeitet haben. Sie müssen einen neuen virtuellen Windows-Computer erstellen und proprietäre Codecs installieren, damit Sie mit dem Verarbeiten und Analysieren der Bilder beginnen können.

## <a name="create-a-new-windows-virtual-machine"></a>Erstellen eines neuen virtuellen Windows-Computers

Sie können virtuelle Windows-Computer über das Azure-Portal, die Azure CLI oder Azure PowerShell erstellen. Den einfachsten Ansatz stellt das Portal dar, da es Ihnen während des Erstellungsvorgangs sämtliche erforderlichen Informationen, Hinweise und hilfreiche Nachrichten zur Verfügung stellt.

1. Melden Sie sich am [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Klicken Sie im Azure-Portal oben links auf **Ressource erstellen**.

1. Geben Sie **Windows Server 2016 Datacenter** in das Suchfeld ein, und klicken Sie dann in der angezeigten Liste auf den gleichnamigen Link.

1. Klicken Sie auf die Schaltfläche **Erstellen**, um mit dem Konfigurieren des virtuellen Computers zu beginnen.

## <a name="configure-the-vm-settings"></a>Konfigurieren der Einstellungen für den virtuellen Computer

Im Portal steht für die VM-Erstellung ein Assistent zur Verfügung, der Sie durch sämtliche Konfigurationsbereiche für den virtuellen Computer führt. Wenn Sie auf die Schaltfläche „Weiter“ klicken, gelangen Sie jeweils zum nächsten Konfigurationsabschnitt. Sie können allerdings auch über die Registerkarten im oberen Abschnitt beliebig zwischen den einzelnen Abschnitten wechseln.

![Erstellen eines virtuellen Computers im Azure-Portal](../media-drafts/3-azure-portal-create-vm.png)

Sobald Sie alle erforderlichen Optionen (durch rote Sternchen gekennzeichnet) angegeben haben, können Sie die restlichen Schritte des Assistenten überspringen und im unteren Bereich auf die Schaltfläche **Überprüfen und erstellen** klicken, um mit der Erstellung des virtuellen Computers zu beginnen.

Beginnen Sie mit dem Abschnitt **Grundlagen**.

### <a name="configure-basic-vm-settings"></a>Konfigurieren der Grundeinstellungen für den virtuellen Computer

1. Wählen Sie das **Abonnement** aus, über das die VM-Stunden abgerechnet werden sollen.

1. Klicken Sie für **Ressourcengruppe** auf **Neu erstellen**, und geben Sie der Ressourcengruppe den Namen **ExerciseResources**.

> [!NOTE]
> Wenn Sie die Einstellungen ändern und anschließend die TAB-TASTE drücken, prüft Azure den Wert automatisch und versieht ihn mit einem grünen Häkchen, wenn die Änderungen akzeptiert werden. Sie können mit der Maus über Fehlerindikatoren fahren, um weitere Informationen zu den einzelnen gefundenen Problemen abzurufen.

1. Geben im Abschnitt **INSTANZDETAILS** einen Namen für Ihren virtuellen Computer ein, z.B. „test-vp-vm2“ (kurz für „Test Video Processor VM #2).
    - Es gilt als bewährte Methode, Ressourcennamen zu standardisieren, damit deren Zweck einfach ermittelt werden kann. Die Namen für virtuelle Windows-Computer sind eingeschränkt: Sie müssen zwischen 2 und 15 Zeichen lang sein und aus Zahlen, Buchstaben und Bindestrichen bestehen.

1. Wählen Sie eine Region in Ihrer Nähe aus.

1. Behalten Sie die **Verfügbarkeitsoptionen** als „Keine“ bei. Diese Option wird verwendet, um sicherzustellen, dass der virtuelle Computer Hochverfügbarkeit aufweist. Zu diesem Zweck werden mehrere virtuelle Computer in einer Gruppe zusammengefasst, um geplante oder ungeplante Wartungsereignisse oder Ausfälle zu verarbeiten.

1. Stellen Sie sicher, dass das Image auf „Windows Server 2016 Datacenter“ festgelegt ist. Sie können die Dropdownliste öffnen, um alle verfügbaren Optionen anzuzeigen.

1. Klicken Sie im Feld **VM-Datenträgertyp** auf das Dropdownmenü, um alle Optionen anzuzeigen. Stellen Sie sicher, dass **SSD** ausgewählt ist.

1. Das Feld **Größe** kann nicht direkt bearbeitet werden. Es weist die Standardgröße „DS1“ auf. Klicken Sie auf den Link **Größe ändern**, um andere VM-Größen abzurufen. Über das Dialogfeld, das daraufhin angezeigt wird, können Sie anhand der Anzahl von CPUs sowie anhand der Namen und des Datenträgertyps filtern. Kicken Sie abschließend auf „Standard DS1 v2“ (in der Regel die Standardeinstellung). Dadurch erhält der virtuelle Computer eine CPU und 3,5 GB Arbeitsspeicher.

    > [!TIP]
    > Sie können in der Ansicht auch zurück zu den VM-Einstellungen navigieren, wenn ein neues Fenster geöffnet wurde.

1. Legen Sie im Abschnitt **ADMINISTRATORZUGRIFF** das Feld **Benutzername** auf den Benutzernamen fest, den Sie verwenden möchten, um sich beim virtuellen Computer anzumelden.

1. Geben Sie im Feld **Kennwort** ein Kennwort ein, das mindestens 12 Zeichen lang ist. Es muss drei der folgenden Merkmale aufweisen: einen Kleinbuchstaben, einen Großbuchstaben, eine Ziffer bzw. ein Sonderzeichen, das nicht „\'“ oder „-“ ist. Verwenden Sie ein Kennwort, das Sie sich merken können, oder notieren Sie sich das Kennwort. Sie werden es später noch benötigen.

1. Bestätigen Sie das **Kennwort**.

1. Öffnen Sie die Liste im Abschnitt **REGELN FÜR EINGEHENDE PORTS**, und _deaktivieren_ Sie die Option „Keine“. Da es sich dabei um einen virtuellen Windows-Computer handelt, soll die Möglichkeit bestehen, mithilfe von RDP auf den Desktop zuzugreifen. Scrollen Sie ggf. durch die Liste, bis Sie RDP (3389) finden, und wählen Sie diese Option aus. In der Benutzeroberfläche wird der Hinweis angezeigt, dass auch nach dem Erstellen des virtuellen Computers die Netzwerkports geändert werden können.

    ![Öffnen des Ports für RDP-Zugriff auf den virtuellen Windows-Computer](../media-drafts/3-open-ports.png)

## <a name="configure-disks-for-the-vm"></a>Konfigurieren von Datenträgern für den virtuellen Computer

1. Klicken Sie auf **Weiter**, um zum Abschnitt „Datenträger“ zu navigieren.

    ![Konfigurieren von Datenträgern für den virtuellen Computer](../media-drafts/3-configure-disks.png)

1. Wählen Sie „SSD Premium“ als **Betriebssystemdatenträgertyp** aus.

1. Verwenden Sie verwaltete Datenträger, damit Sie nicht mit Speicherkonten arbeiten müssen. Sie können bei Bedarf in der grafischen Benutzeroberfläche die Einstellung ändern, damit Ihnen die Informationen angezeigt werden, die Azure benötigt.

### <a name="create-a-data-disk"></a>Erstellen eines Datenträgers

Rufen Sie sich in Erinnerung, dass wir einen Betriebssystemdatenträger (C:) und einen temporären Datenträger (D:) verwenden. Fügen Sie außerdem einen weiteren Datenträger für Daten hinzu.

1. Klicken Sie im Abschnitt **DATENTRÄGER** auf den Link **Neuen Datenträger erstellen und anfügen**.

    ![Erstellen eines Datenträgers für den virtuellen Computer im Portal](../media-drafts/3-add-data-disk.png)

1. Sie können alle Standardeinstellungen beibehalten: „SSD Premium“, „1.023 GB“ und „Keine“ (leerer Datenträger). Beachten Sie jedoch, dass wir an dieser Stelle eine Momentaufnahme oder ein Speicherblob verwenden könnten, um eine VHD zu erstellen.

1. Klicken Sie auf **OK**, um den Datenträger zu erstellen, und navigieren Sie zurück zum Abschnitt **DATENTRÄGER**.

1. Es sollte nun ein neuer Datenträger in der ersten Zeile angezeigt werden.

    ![Neuer Datenträger im virtuellen Computer](../media-drafts/3-new-disk.png)

## <a name="configure-the-network"></a>Konfigurieren des Netzwerks

1. Klicken Sie auf **Weiter**, um zum Abschnitt „Netzwerk“ zu navigieren.

1. In einem Produktionssystem, in dem bereits andere Komponenten vorhanden sind, sollten Sie ein _vorhandenes_ virtuelles Netzwerk verwenden. So kann Ihr virtueller Computer mit den anderen Clouddiensten in unserer Lösung kommunizieren. Wenn für diesen Speicherort noch kein Netzwerk definiert ist, können Sie es hier erstellen und die folgenden Bestandteile konfigurieren:
    - **Adressraum**: Der IPv4-Bereich, der diesem Netzwerk insgesamt zur Verfügung steht.
    - **Subnetzbereich:** Das erste Subnetz, das der Unterteilung des Adressraums dient. Dieses muss innerhalb des definierten Adressraums liegen. Sobald das VNET erstellt wurde, können Sie weitere Subnetze hinzufügen.

1. Ändern Sie die Standardbereiche, um den IP-Adressraum `172.xxx` zu verwenden.
    - Ändern Sie das Feld **Adressraum** in `172.16.0.0/16`, um diesem den gesamten Adressbereich zuzuweisen.
    - Ändern Sie das Feld **Subnetzbereich** in `172.16.1.0/24`, um ihm 256 IP-Adressen des Adressraums zuzuweisen.

> [!NOTE]
> Azure erstellt standardmäßig ein virtuelles Netzwerk, eine Netzwerkschnittstelle und eine öffentliche IP-Adresse für Ihren virtuellen Computer. Nach der Erstellung des virtuellen Computers können die Netzwerkoptionen nicht mehr problemlos geändert werden. Prüfen Sie daher immer genau die Netzwerkzuweisungen für die von Ihnen in Azure erstellten Dienste.

## <a name="finish-configuring-the-vm-and-create-the-image"></a>Abschließen der Konfiguration des virtuellen Computers und Erstellen des Images

Die restlichen Optionen weisen geeignete Standardeinstellungen auf, die nicht geändert werden müssen. Bei Interesse können sich die anderen Registerkarten genauer ansehen. Neben den einzelnen Optionen befindet sich jeweils ein `(i)`-Symbol, über das Sie eine Erläuterung der jeweiligen Option anzeigen können. Dies ist eine gute Möglichkeit, nähere Informationen über die verschiedenen Optionen zu erhalten, die Sie zum Konfigurieren des virtuellen Computers verwenden können.

1. Klicken Sie im unteren Bereich auf die Schaltfläche **Überprüfen und erstellen**.

1. Das System überprüft Ihre Optionen und zeigt Details zur Erstellung des virtuellen Computers an.

1. Klicken Sie auf **Erstellen**, um den virtuellen Computer zu erstellen und bereitzustellen. Im Azure-Dashboard wird der virtuelle Computer angezeigt, der aktuell bereitgestellt wird. Dieser Vorgang kann einige Minuten in Anspruch nehmen.

Währenddessen erfahren Sie in der nächsten Einheit, wozu Sie diesen virtuellen Computer verwenden können.