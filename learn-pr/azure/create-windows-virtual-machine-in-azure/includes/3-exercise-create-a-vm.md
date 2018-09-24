Wie zuvor bereits erwähnt, verarbeitet das Beispielunternehmen Videoinhalte auf virtuellen Windows-Computern. Angenommen, eine neue Stadt hat Sie damit beauftragt, die Aufnahmen ihrer Verkehrskameras zu verarbeiten. Es handelt sich allerdings dabei um ein Modell, mit dem Sie zuvor noch nicht gearbeitet haben. Sie müssen eine neue Windows-VM erstellen und proprietäre Codecs installieren, damit Sie mit dem Verarbeiten und Analysieren der Images beginnen können.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-new-windows-virtual-machine"></a>Erstellen eines neuen virtuellen Windows-Computers

Sie können virtuelle Windows-Computer über das Azure-Portal, die Azure CLI oder Azure PowerShell erstellen. Am einfachsten ist es im Portal, da es Ihnen während der Erstellung der VM alle erforderlichen Informationen, Hinweise und hilfreiche Meldungen zur Verfügung stellt.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.

1. Klicken Sie im Azure-Portal oben links auf **Ressource erstellen**.

1. Geben Sie **Windows Server 2016 Datacenter** in das Suchfeld ein, und klicken Sie dann in der angezeigten Liste auf den gleichnamigen Link.

1. Klicken Sie auf die Schaltfläche **Erstellen**, um mit dem Konfigurieren des virtuellen Computers zu beginnen.

## <a name="configure-the-vm-settings"></a>Konfigurieren der Einstellungen für den virtuellen Computer

Im Portal steht für die VM-Erstellung ein Assistent zur Verfügung, der Sie durch sämtliche Konfigurationsbereiche für den virtuellen Computer führt. Wenn Sie auf die Schaltfläche „Weiter“ klicken, gelangen Sie jeweils zum nächsten Konfigurationsabschnitt. Sie können allerdings auch über die Registerkarten im oberen Abschnitt nach Belieben zwischen den einzelnen Abschnitten wechseln.

![Screenshot der Umgebung zum Erstellen eines virtuellen Computers im Azure-Portal.](../media/3-azure-portal-create-vm.png)

Sobald Sie alle erforderlichen Optionen (durch rote Sternchen gekennzeichnet) angegeben haben, können Sie die verbleibenden Schritte des Assistenten überspringen und im unteren Bereich auf die Schaltfläche **Überprüfen + erstellen** klicken, um mit der Erstellung des virtuellen Computers zu beginnen.

Beginnen Sie mit dem Abschnitt **Grundlagen**.

### <a name="configure-basic-vm-settings"></a>Konfigurieren der Grundeinstellungen für den virtuellen Computer

> [!NOTE]  
> Wenn Sie die Einstellungen ändern und anschließend in jedem Freitextfeld die TAB-TASTE drücken, überprüft Azure den Wert automatisch und versieht ihn mit einem grünen Häkchen, wenn die Änderungen akzeptiert werden. Sie können mit der Maus auf Fehlerindikatoren zeigen, um weitere Informationen zu gefundenen Problemen zu erhalten.

1. Wählen Sie das **Abonnement** aus, über das die VM-Stunden abgerechnet werden sollen.

1. Wählen Sie für **Ressourcengruppe** **<rgn>[Sandbox- Ressourcengruppenname]</rgn>** aus.

1. Geben Sie im Abschnitt **INSTANZENDETAILS** einen Namen für Ihren virtuellen Computer ein (beispielsweise **test-vp-vm2** für „zweiter virtueller Computer zum Testen des Videoprozessors“).
    - Es empfiehlt sich, Ressourcennamen zu standardisieren, um ihren Zweck einfach ermitteln zu können. Die Namen für virtuelle Windows-Computer sind eingeschränkt: Sie müssen zwischen 1 und 15 Zeichen lang sein, dürfen keine Sonderzeichen bzw. Zeichen enthalten, die nicht den ASCII-Richtlinien entsprechen, und müssen in der aktuellen Ressourcengruppe eindeutig sein.

1. Wählen Sie von den folgenden Standorten eine Region aus, die in Ihrer Nähe liegt.

   [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. Behalten Sie die **Verfügbarkeitsoptionen** als „Keine“ bei. Diese Option wird verwendet, um sicherzustellen, dass der virtuelle Computer Hochverfügbarkeit aufweist. Zu diesem Zweck werden mehrere virtuelle Computer in einer Gruppe zusammengefasst, um geplante oder ungeplante Wartungsereignisse oder Ausfälle zu verarbeiten.

1. Stellen Sie sicher, dass das Image auf „Windows Server 2016 Datacenter“ festgelegt ist. Sie können die Dropdownliste öffnen, um alle verfügbaren Optionen anzuzeigen.

1. Das Feld **Größe** enthält die Standardgröße „DS1“ und kann nicht direkt bearbeitet werden. Klicken Sie auf den Link **Größe ändern**, um andere VM-Größen abzurufen. Über das Dialogfeld, das daraufhin angezeigt wird, können Sie anhand der Anzahl von CPUs sowie anhand der Namen und des Datenträgertyps filtern. Klicken Sie abschließend auf „Standard DS1 v2“ (in der Regel die Standardeinstellung). Dadurch erhält der virtuelle Computer eine CPU und 3,5 GB Arbeitsspeicher.

    > [!TIP]
    > Da auf der rechten Seite ein neues Fenster geöffnet und über das vorherige Fenster geschoben wurde, um es anzuzeigen, können Sie die Ansicht auch nach links verschieben, um wieder zu den VM-Einstellungen zu gelangen.

1. Legen Sie im Abschnitt **ADMINISTRATORKONTO** das Feld **Benutzername** auf den Benutzernamen fest, den Sie verwenden möchten, um sich bei dem virtuellen Computer anzumelden.

1. Geben Sie im Feld **Kennwort** ein Kennwort mit mindestens 12 Zeichen ein. Es muss drei der folgenden Zeichen aufweisen: einen Kleinbuchstaben, einen Großbuchstaben, eine Ziffer bzw. ein Sonderzeichen, das nicht „\\“ oder „-“ ist. Verwenden Sie ein Kennwort, das Sie sich merken können, oder notieren Sie sich das Kennwort. Sie werden es später noch benötigen.

1. Bestätigen Sie das **Kennwort**.

1. Öffnen Sie die Liste im Abschnitt **REGELN FÜR EINGEHENDE PORTS**, und wählen Sie _Allow selected ports_ (Ausgewählte Ports zulassen) aus. Da es sich hier um einen virtuellen Windows-Computer handelt, möchten wir per RDP auf den Desktop zugreifen können. Scrollen Sie ggf. durch die Liste, bis Sie RDP (3389) finden, und wählen Sie diese Option aus. Auf der Benutzeroberfläche wird der Hinweis angezeigt, dass die Netzwerkports auch nach dem Erstellen des virtuellen Computers geändert werden können.

    ![Screenshot der Dropdownliste zum Öffnen des Ports für RDP-Zugriff auf dem virtuellen Windows-Computer.](../media/3-open-ports.png)

## <a name="configure-disks-for-the-vm"></a>Konfigurieren von Datenträgern für den virtuellen Computer

1. Klicken Sie auf **Weiter**, um zum Abschnitt „Datenträger“ zu gelangen.

    ![Screenshot des Abschnitts zum Konfigurieren von Datenträgern für den virtuellen Computer.](../media/3-configure-disks.png)

1. Wählen Sie „SSD Premium“ als **Betriebssystemdatenträgertyp** aus.

1. Verwenden Sie verwaltete Datenträger, damit Sie nicht mit Speicherkonten arbeiten müssen. Sie können bei Bedarf in der grafischen Benutzeroberfläche die Einstellung ändern, damit Ihnen die Informationen angezeigt werden, die Azure benötigt.

### <a name="create-a-data-disk"></a>Erstellen eines Datenträgers

Rufen Sie sich in Erinnerung, dass wir einen Betriebssystemdatenträger (C:) und einen temporären Datenträger (D:) verwenden. Fügen Sie außerdem einen weiteren Datenträger hinzu.

1. Klicken Sie im Abschnitt **DATENTRÄGER** auf den Link **Create and attach a new disk** (Neuen Datenträger erstellen und anfügen).

    ![Screenshot des Dialogfelds zum Erstellen eines neuen VM-Datenträgers im Portal.](../media/3-add-data-disk.png)

1. Sie können alle Standardeinstellungen beibehalten: „SSD Premium“, „1.023 GB“ und „Keine“ (leerer Datenträger). Beachten Sie jedoch, dass wir an dieser Stelle eine Momentaufnahme oder ein Speicherblob verwenden könnten, um eine VHD zu erstellen.

1. Klicken Sie auf **OK**, um den Datenträger zu erstellen, und navigieren Sie zurück zum Abschnitt **DATA DISKS** (DATENTRÄGER).

1. Es sollte nun ein neuer Datenträger in der ersten Zeile angezeigt werden.

    ![Screenshot des neu hinzugefügten Datenträgers für den virtuellen Computer.](../media/3-new-disk.png)

## <a name="configure-the-network"></a>Konfigurieren des Netzwerks

1. Klicken Sie auf **Weiter**, um zum Abschnitt „Netzwerk“ zu navigieren.

1. In einem Produktionssystem, in dem bereits andere Komponenten vorhanden sind, sollten Sie ein _vorhandenes_ virtuelles Netzwerk verwenden. So kann Ihr virtueller Computer mit den anderen Clouddiensten in unserer Lösung kommunizieren. Wenn für diesen Speicherort noch kein Netzwerk definiert ist, können Sie es hier erstellen und die folgenden Bestandteile konfigurieren:
    - **Den Adressbereich:** der IPv4-Bereich, der dem Netzwerk insgesamt zur Verfügung steht.
    - **Subnetzbereich:** Das erste Subnetz, das der Unterteilung des Adressraums dient. Dieses muss innerhalb des definierten Adressraums liegen. Sobald das VNET erstellt wurde, können Sie weitere Subnetze hinzufügen.

1. Als Nächstes ändern wir die Standardbereiche, um den IP-Adressraum `172.xxx` zu verwenden. Klicken Sie unter „Virtuelles Netzwerk“ auf **Neu erstellen**.
    - Ändern Sie das Feld **Adressraum** in `172.16.0.0/16`, um ihm den gesamten Adressbereich zuzuweisen.
    - Ändern Sie das Feld **Subnetzbereich** in `172.16.1.0/24`, um ihm 256 IP-Adressen des Adressraums zuzuweisen.

1. Klicken Sie auf **OK**.

> [!NOTE]
> Azure erstellt standardmäßig ein virtuelles Netzwerk, eine Netzwerkschnittstelle und eine öffentliche IP-Adresse für Ihren virtuellen Computer. Nach der Erstellung des virtuellen Computers können die Netzwerkoptionen nicht mehr problemlos geändert werden. Prüfen Sie daher immer genau die Netzwerkzuweisungen für die von Ihnen in Azure erstellten Dienste.

## <a name="finish-configuring-the-vm-and-create-the-image"></a>Abschließen der Konfiguration des virtuellen Computers und Erstellen des Images

Die restlichen Optionen weisen geeignete Standardeinstellungen auf, die nicht geändert werden müssen. Bei Interesse können sich die anderen Registerkarten genauer ansehen. Neben den einzelnen Optionen befindet sich jeweils ein `(i)`-Symbol, über das Sie eine Erläuterung der jeweiligen Option anzeigen können. Dies ist eine gute Möglichkeit, nähere Informationen über die verschiedenen Optionen zu erhalten, die Sie zum Konfigurieren des virtuellen Computers verwenden können.

1. Klicken Sie im unteren Bereich auf die Schaltfläche **Überprüfen und erstellen**.

1. Das System überprüft Ihre Optionen und zeigt Details zur Erstellung des virtuellen Computers an.

1. Klicken Sie auf **Erstellen**, um den virtuellen Computer zu erstellen und bereitzustellen. Im Azure-Dashboard wird der virtuelle Computer angezeigt, der aktuell bereitgestellt wird. Dieser Vorgang kann einige Minuten in Anspruch nehmen.

Währenddessen erfahren Sie in der nächsten Einheit, wozu Sie diesen virtuellen Computer verwenden können.