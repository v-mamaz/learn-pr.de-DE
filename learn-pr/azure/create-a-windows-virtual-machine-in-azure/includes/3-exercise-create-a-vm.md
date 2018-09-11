Betrachten wir ein alternatives Szenario. Angenommen, Ihre Organisation ist eine Schule, in der mithilfe von Windows-VMs Testumgebungen bereitgestellt werden. Schüler können in diesen Testumgebungen Web-Apps installieren, Domänen konfigurieren und Windows-Dienste und -Features ausprobieren, ohne die Funktionalität der Schulcomputer zu beeinflussen. Lehrer können mithilfe von RDP eine Verbindung mit diesen VMs herstellen und den Arbeitsfortschritt der Schüler überprüfen. Sehen wir uns an, wie ein solches Szenario mit Azure umgesetzt werden kann.

## <a name="create-a-windows-vm"></a>Erstellen einer Windows-VM

Gehen Sie zum Erstellen eines virtuellen Windows-Computers wie folgt vor:

1. Melden Sie sich über das [Azure-Portal](https://portal.azure.com?azure-portal=true) bei Azure an.

1. Klicken Sie im Azure-Portal oben links auf **Ressource erstellen**.

1. Geben Sie **Windows Server 2016 Datacenter** in der **Suchleiste** ein, und klicken Sie anschließend auf den gleichnamigen Link.

### <a name="configure-the-vm-settings"></a>Konfigurieren der Einstellungen für den virtuellen Computer

1. Geben Sie unter **Grundeinstellungen** im Feld **Name** einen Namen für Ihren virtuellen Computer ein, z.B. „SchülerVM“.

1. Klicken Sie im Feld **VM-Datenträgertyp** auf das Dropdownmenü, um sich alle Optionen anzeigen zu lassen. Stellen Sie sicher, dass **SSD** ausgewählt ist.

1. Geben Sie im Feld **Benutzername** einen geeigneten Benutzernamen ein, der zur Anmeldung beim virtuellen Computer verwendet wird.

1. Geben Sie im Feld **Kennwort** ein Kennwort ein, das mindestens zwölf Zeichen lang ist. Es muss Groß- und Kleinbuchstaben, Ziffern und Sonderzeichen enthalten.

1. Klicken Sie unter **Ressourcengruppe** auf **Erstellen**. Geben Sie für die Ressourcengruppe einen Namen ein, z.B. „MeineTestRG“.

1. Wählen Sie einen geeigneten Speicherort für den virtuellen Computer aus, der erstellt werden soll, und klicken Sie anschließend auf **OK**.

### <a name="select-the-vm-image-size-and-options"></a>Auswählen der Größe und der Optionen des virtuellen Computers

1. Klicken Sie auf der Seite **Größe auswählen** zuerst auf das Image **B1s** und anschließend auf **Auswählen**.

   > [!Note] 
   > Das B1-Image verfügt nur über 1 GB RAM. Dies führt bei der erstmaligen Anmeldung zu Speicherfehlern. Sie können die Größe des Images jedoch später über eine Registerkarte anpassen.

1. Klicken Sie auf der Seite **Einstellungen** unter **Öffentliche Eingangsports hinzufügen** auf **No public inbound ports** (Keine öffentlichen Eingangsports). Den RDP-Zugriff konfigurieren Sie später.

### <a name="finish-configuring-the-vm-and-create-the-image"></a>Abschließen der Konfiguration des virtuellen Computers und Erstellen des Images

1. Scrollen Sie nach unten, und klicken Sie auf **OK**.

1. Überprüfen Sie unter **Erstellen** die konfigurierten Einstellungen. Klicken Sie unten auf **Erstellen**. Im Azure-Dashboard wird der virtuelle Computer angezeigt, der aktuell bereitgestellt wird. Dieser Vorgang kann einige Minuten dauern.

## <a name="summary"></a>Zusammenfassung

In dieser Übung haben Sie einen virtuellen Windows Server-Computer erstellt, der von Schülern genutzt werden kann und über das Schulnetzwerk erreichbar ist. In der nächsten Lektion erfahren Sie, wie Sie mithilfe von RDP eine Verbindung mit dem virtuellen Computer herstellen und diesen verwalten.
