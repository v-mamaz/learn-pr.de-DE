
Angenommen, Sie betreiben eine Website zum Teilen von Fotos, bei der Daten auf virtuellen Azure-Maschinen (VMs) mit SQL Server und benutzerdefinierten Anwendungen gespeichert werden. Sie möchten die folgenden Anpassungen vornehmen:

- Sie müssen die Einstellungen für den Datenträgercache auf einer VM ändern.
- Sie möchten einen neuen Datenträger für Daten zur VM mit aktivierter Zwischenspeicherung hinzufügen.

Sie haben sich dafür entschieden, diese Änderungen über das Azure-Portal vorzunehmen.

In dieser Übung wird Schritt für Schritt erklärt, wie Sie die Änderungen an einer VM vornehmen, die oben beschrieben wurde. Zuerst melden Sie sich am Portal an und erstellen eine VM.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-virtual-machine"></a>Erstellen einer virtuellen Maschine

In diesem Schritt erstellen wir eine VM mit den folgenden Eigenschaften:

| Eigenschaft        | Wert   |
|-----------------|---------|
| Image           | **Windows Server 2016 Datacenter** |
| Name            | **fotoshareVM** |
| Ressourcengruppe  |   **<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>** |
| Speicherort        | Siehe unten. |

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

1. Wählen Sie im Menü in der Randleiste **Ressource erstellen** aus.

1. _Windows Server 2016 VM_ befindet sich in der Liste der **beliebten** Marketplace-Elemente. Wenn dies nicht der Fall ist, suchen Sie über das Suchfeld oben nach „Windows Server 2016 DataCenter“.

1. Wählen Sie die Windows-VM, und klicken Sie auf **Erstellen** um den VM-Erstellungsprozesses zu starten.

1. Vergewissern Sie sich im Bereich **Grundlagen**, dass das ausgewählte **Abonnement** _Concierge-Abonnement_ ist.

1. Wählen Sie unter **Ressourcengruppe** die Option **Vorhandene verwenden** aus, und klicken Sie auf _<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>_.

1. Geben Sie in **Name der virtuellen Maschine** _fotoshareVM_ ein.

1. Wählen Sie in der Dropdownliste **Speicherort** die nächstgelegene Region aus der folgenden Liste.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. Der Standard unter **Größe** der VM ist **DS1 v2**. Mit erhalten Sie eine Einzel-CPU und 3,5 GB Speicher. Das reicht für dieses Beispiel.

1. Geben Sie im Abschnitt **ADMINISTRATOR ACCOUNT** einen **Benutzernamen** und **Kennwort** ein, und /**Bestätigen Sie das Kennwort** für ein Administratorkonto auf der neuen VM.

1. Hier ist ein Beispiel für eine ausgefüllte Konfiguration vom Typ **Grundlagen** angegeben. Behalten Sie die Standardwerte für die verbleibenden Registerkarten und Felder bei, und klicken Sie auf **Überprüfen + Erstellen**.

    ![Screenshot des Azure-Portals mit dem Blatt „Erstellen einer virtuellen Maschine“ mit einigen Beispielen für eine ausgefüllte Konfiguration „Grundlagen“.](../media/4-basics-vm.png)

1. Nachdem Sie Ihre neuen VM-Einstellungen überprüft haben, klicken Sie auf **Erstellen**, um die Bereitstellung Ihrer neuen VM zu starten.

Die VM-Erstellung kann einige Minuten dauern, da alle verschiedenen Ressourcen (Speicher, Netzwerkschnittstelle usw.) zur Unterstützung der virtuellen Maschine erstellt werden. Warten Sie, bis die virtuelle Maschine bereitgestellt wurde, bevor Sie mit der Übung fortfahren.

## <a name="view-os-disk-cache-status-in-the-portal"></a>Anzeigen des Betriebssystemdatenträger-Cachestatus im Portal

Nachdem unsere VM bereitgestellt wurde, können wir den Cachestatus des Betriebssystemdatenträgers mit den folgenden Schritten bestätigen:

1. Wählen Sie die **fotoshareVM**-Ressource, um die VM-Details im Portal zu öffnen. Sie können auch in der linken Randleiste auf **Alle Ressourcen** klicken und dann die VM **fotoshareVM** auswählen.

1. Wählen Sie unter **Einstellungen** die Option **Datenträger** aus.

1. Im Bereich **Datenträger** verfügt die virtuelle Maschine über einen Datenträger, nämlich den Betriebssystemdatenträger. Der Cachetyp ist derzeit auf den Standardwert **Lesen/Schreiben** festgelegt.

![Screenshot des Azure-Portals mit dem Abschnitt „Datenträger“ eines VM-Blatts, wobei der BS-Datenträger angezeigt und die schreibgeschützte Zwischenspeicherung aktiviert ist.](../media/4-os-disk-rw.PNG)

## <a name="change-the-cache-settings-of-the-os-disk-in-the-portal"></a>Ändern der Cacheeinstellungen des Betriebssystemdatenträgers im Portal

1. Wählen Sie im Bereich **Datenträger** oben links die Option **Bearbeiten**.

1. Ändern Sie den Wert **HOSTZWISCHENSPEICHERUNG** für den Betriebssystemdatenträger in **Schreibgeschützt**, indem Sie die Dropdownliste verwenden, und wählen Sie dann oben links die Option **Speichern**.

1. Dieses Update kann einige Zeit in Anspruch nehmen. Der Grund hierfür ist, dass der Zieldatenträger durch das Ändern der Cacheeinstellung eines Azure-Datenträgers getrennt und dann erneut angefügt wird. Wenn es sich um den Betriebssystemdatenträger handelt, wird auch die virtuelle Maschine neu gestartet. Wenn der Vorgang abgeschlossen ist, erhalten Sie eine Benachrichtigung, dass die VM-Datenträger aktualisiert wurden.

1. Wenn der Vorgang abgeschlossen ist, ist der Cachetyp des Betriebssystemdatenträgers auf **Schreibgeschützt** festgelegt.

Als Nächstes führen wir die Konfiguration des Caches für den für Daten bestimmten Datenträger durch. Wir müssen zunächst einen Datenträger erstellen, um ihn konfigurieren zu können.

## <a name="add-a-data-disk-to-the-vm-and-set-caching-type"></a>Hinzufügen eines Datenträgers zur virtuellen Maschine und Festlegen des Cachetyps

1. In der Ansicht **Datenträger** unserer VM im Portal können Sie jetzt die auf die Option **Datenträger hinzufügen** klicken. Im Feld **Name** wird sofort ein Fehler mit dem Hinweis angezeigt, dass das Feld nicht leer sein darf. Da wir noch nicht über einen Datenträger für Daten verfügen, erstellen wir ihn jetzt.

1. Klicken Sie in die Liste **Namen** und dann auf **Datenträger erstellen**.

1. Geben Sie im Bereich **Verwalteten Datenträger erstellen** im Feld **Name** den Namen **fotoshareVM-data** ein.

1. Wählen Sie unter **Ressourcengruppe** zuerst **Vorhandene verwenden** und anschließend _<rgn>[Sandbox-Ressourcengruppenname]</rgn>_ aus.

1. Notieren Sie die Standardwerte für die verbleibenden Felder:
    - SSD Premium
    - Größe von 1.023 GB
    - Am gleichen Speicherort wie die VM (kann nicht geändert werden).
    - IOPS-Grenzwert – 5.000
    - Durchsatzbegrenzung (MB/s) – 200

1. Klicken Sie am unteren Rand des Bildschirms auf **Erstellen**. 

    Warten Sie, bis der Datenträger erstellt wurde, bevor Sie fortfahren.

1. Ändern Sie den Wert **HOSTZWISCHENSPEICHERUNG** für den neuen Datenträger in **Schreibgeschützt**, indem Sie die Dropdownliste verwenden (ist ggf schon festgelegt), und klicken Sie dann oben links auf die Option **Speichern**.

    Warten Sie, bis die VM den neuen Datenträger aktualisiert hat. Nach Abschluss des Vorgangs haben Sie einen neuen Datenträger auf Ihrer virtuellen Maschine.

In dieser Übung haben wir das Azure-Portal verwendet, um die Zwischenspeicherung auf einer neuen virtuellen Maschine zu konfigurieren, die Cacheeinstellungen auf einem vorhandenen Datenträger zu ändern und die Zwischenspeicherung auf einem neuen Datenträger zu konfigurieren. Im folgenden Screenshot ist die endgültige Konfiguration dargestellt:

![Screenshot des Azure-Portals mit dem BS-Datenträger und dem neuen Datenträger im Abschnitt „Datenträger“ auf dem Blatt „VM“, wobei für beide Datenträger die schreibgeschützte Zwischenspeicherung aktiviert ist.](../media/disks-final-config-portal.PNG)
