Nehmen wir an, dass Sie eine Website mit Daten, die auf Azure Virtual Machines (VMs) Ausführen von SQL Server und benutzerdefinierten Anwendungen zum Teilen von Fotos ausführen. Möchten Sie die folgenden Anpassungen vornehmen:

- Sie müssen die Datenträger-cacheeinstellungen auf einem virtuellen Computer zu ändern.
- Einen neuer Datenträger dem virtuellen Computer mit aktivierter Zwischenspeicherung hinzufügen möchten.

Sie haben sich entschieden, diese Änderungen über das Azure-Portal vornehmen.

In dieser Übung behandeln wir die Änderungen an einen virtuellen Computer, die weiter oben beschrieben. Zunächst lassen Sie uns beim Portal anmelden und Erstellen eines virtuellen Computers.

## <a name="sign-in-to-the-azure-portal"></a>Melden Sie sich beim Azure-Portal an.

[!include[](../../../includes/azure-sandbox-activate.md)]

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

## <a name="create-a-virtual-machine"></a>Erstellen eines virtuellen Computers

In diesem Schritt werden wir zum Erstellen einer VM mit den folgenden Eigenschaften:

|Eigenschaft  |Wert  |
|---------|---------|
|Image     |   **Windows Server 2016 Datacenter**      |
|Name     |   **fotoshareVM**     |
|Ressourcengruppe     |   **<rgn>[Sandkasten Resource Group-Name]</rgn>**      |

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Wählen Sie im linken Menü des Portals **VMs**.

1. Wählen Sie jetzt **hinzufügen** in links oben auf der **VMs** Bildschirm. Diese Aktion startet den Erstellungsprozess.

1. Auf der **Compute** Bereich, in dem verfügbaren VM-Images, Typ listet *Windows Server 2016 Datacenter* in das Suchfeld.

1. Wählen Sie **Windows Server 2016 Datacenter** aus der Suchergebnisse, und wählen Sie dann **erstellen** Erstellungsprozesses des virtuellen Computers zu starten.

1. In der **Grundlagen** panel, überprüfen Sie die ausgewählte **Abonnement**.

1. Für **Ressourcengruppe**, klicken Sie auf **neu erstellen** und geben Sie die **Namen** von `fotoshare-rg` , und klicken Sie auf **OK**.

1. in der **Name des virtuellen Computers** geben `fotoshareVM`.

1. Unter **Ressourcengruppe**Option **vorhandene** , und wählen Sie <rgn>[Ressourcengruppennamen Sandkasten]</rgn>.

1. In der **Speicherort** Dropdown-Liste, wählen Sie eine Region aus der Liste oben.

1. Für den virtuellen Computer **Größe**, Sie können der empfohlene Standardwert, oder klicken Sie auf **Ändern der Größe** , wählen Sie eine andere Größe als die **wählen Sie eine Größe** auf dem Blatt.

    > [!NOTE]
    > Es sind keine Optionen zum Konfigurieren der Zwischenspeicherung von Datenträgern zu diesem Zeitpunkt noch in der **Datenträger** auf der Registerkarte das Blatt "erstellen".

    > [!IMPORTANT]
    > Denken Sie daran, dass die Zwischenspeicherung von Datenträgern für virtuelle Computer die L-Serie und B-Serie geändert werden kann. Ich wähle eine andere Größe.

1. In **ADMINISTRATORKONTO** Geben Sie eine **Benutzername** und **Kennwort**/**kennwortbestätigung** für ein Administratorkonto auf dem neuen virtuellen Computer.

1. Die folgende Abbildung zeigt ein Beispiel der **Grundlagen** Konfiguration sieht bei ausgefüllt. Behalten Sie die Standardwerte für die verbleibenden Felder und Registerkarten, und klicken Sie auf **überprüfen + erstellen**.

    ![Screenshot des Azure-Portal mit erstellen Sie ein VM-Blatt mit einigen Grundlagen-Beispielkonfiguration, die ausgefüllt werden soll, wie beschrieben.](../media/4-basics-vm.png)

1. Überprüfen Sie Ihre neuen VM-Einstellungen, und klicken Sie auf **erstellen** die Bereitstellung von den neuen virtuellen Computer zu beginnen.

VM-Erstellung kann eine Weile dauern. Warten Sie die Bereitstellung des virtuellen Computers ab, bevor Sie mit der Übung fortfahren. Sie erhalten eine Meldung im Notification Hub, wenn der Vorgang abgeschlossen ist.

> [!IMPORTANT]
> Wir verwenden diesen virtuellen Computer in der nächsten Lektion, halten Sie es also eine Weile.

## <a name="view-os-disk-cache-status-in-the-portal"></a>Anzeigen des Betriebssystemdatenträgers Cache-Status im portal

Nach der virtuellen Computer bereitgestellt wird, können wir den Status Zwischenspeichern der Betriebssystem-Datenträger, die mit den folgenden Schritten bestätigen:

1. Klicken Sie im linken Menü auf **alle Ressourcen**, und wählen Sie dann auf Ihrem virtuellen Computer **FotoshareVM**.

1. Auf der **VM** Blatt unter **Einstellungen**Option **Datenträger**.

1. Auf der **Datenträger** Bereich, den virtuellen Computer einen Datenträger, den Betriebssystem-Datenträger verfügt. Dessen Cachetyp ist so eingerichtet, der Standardwert von **Lese-/Schreibzugriff**.

![Screenshot des Azure-Portal im Abschnitt Datenträger einer VM auf dem Blatt mit dem Betriebssystem-Datenträger angezeigt, und legen Sie auf die nur-Lese caching mit.](../media/4-os-disk-rw.PNG)

## <a name="change-the-cache-settings-of-the-os-disk-in-the-portal"></a>Ändern der cacheeinstellungen für den Betriebssystem-Datenträger im portal

1. Auf der **Datenträger** wählen Sie im Bereich **bearbeiten** in der oberen linken Ecke des Bildschirms.

1. Ändern der **HOSTZWISCHENSPEICHERN** Wert für den Betriebssystemdatenträger **schreibgeschützte** mithilfe der Dropdownliste aus, und wählen Sie dann **speichern** in der oberen linken Ecke des Bildschirms.

1. Dieses Update kann einige Zeit in Anspruch nehmen. Der Grund ist, dass der Zieldatenträger getrennt und erneut angefügt wird der Zieldatenträger durch Ändern der cacheeinstellung eines Azure-Datenträgers. Wenn es sich um die Betriebssystem-Datenträger handelt, wird der virtuelle Computer ebenfalls neu gestartet. Wenn der Vorgang abgeschlossen ist, erhalten Sie eine Benachrichtigung, die besagt, dass die VM-Datenträger aktualisiert wurden.

1. Nach Abschluss des Vorgangs auf die Betriebssystem-Datenträgertyp Cache festgelegt **schreibgeschützte**.

Betrachten wir nun Daten Datenträger Cachekonfiguration. Um einen Datenträger zu konfigurieren, müssen wir zunächst einen erstellen.

## <a name="add-a-data-disk-to-the-vm-and-set-caching-type"></a>Hinzufügen eines Datenträgers auf dem virtuellen Computer und caching-Typ

1. Auf der **Datenträger** Ansicht der VM im Portal, alles zu wählen **Datenträger**. Ein Fehler sofort angezeigt wird, der **Namen** Feld, das uns mitteilen, dass das Feld darf nicht leer sein. Wir haben einen Datenträger für Daten noch, erstellen wir also einen.

1. Klicken Sie in die Liste **Namen**, und klicken Sie dann auf **Datenträger erstellen**.

1. In der **verwalteten Datenträger erstellen** Bereich, in der **Namen** geben **FotosharesVM-Daten**.

1. Unter **Ressourcengruppe**Option **vorhandene**, und wählen Sie <rgn>[Ressourcengruppennamen Sandkasten]</rgn>.

1. Lassen Sie die verbleibenden Felder Standardwerte, und klicken Sie auf **erstellen** am unteren Rand des Bildschirms.

    Warten Sie, bis der Datenträger erstellt wurde, bevor Sie fortfahren.

1. Ändern der **HOSTZWISCHENSPEICHERN** Wert für unsere neue eines Datenträgers an einen **schreibgeschützte** mithilfe der Dropdownliste aus, und wählen Sie dann **speichern** in der oberen linken Ecke des Bildschirms.

    Warten Sie den virtuellen Computer, um den Vorgang abzuschließen, aktualisieren den neuen Datenträger aus. Nach Abschluss des Vorgangs wird der Datenträger-Cache-Datentyp festgelegt werden, um **schreibgeschützte**.

In dieser Übung verwendet haben wir das Azure-Portal zum Konfigurieren der Zwischenspeicherung auf einen neuen virtuellen Computer, Ändern von cacheeinstellungen für einen vorhandenen Datenträger und konfigurieren die Zwischenspeicherung auf einen neuen Datenträger. Der folgende Screenshot zeigt die endgültige Konfiguration:

![Screenshot des Azure-Portal mit den Betriebssystemdatenträger und einen neuen Datenträger im Abschnitt "Datenträger" auf dem Blatt "VM" Unsere mit beide Datenträger auf schreibgeschützte Zwischenspeicherung festgelegt.](../media/disks-final-config-portal.PNG)
