Angenommen, Sie betreiben eine Website zum Teilen von Fotos, bei der Daten auf virtuellen Azure-Computern (VMs) mit SQL Server und benutzerdefinierten Anwendungen gespeichert werden. Sie möchten die folgenden Anpassungen vornehmen.

- Ändern der Einstellungen für den Datenträgercache auf einer VM
- Hinzufügen eines neuen Datenträgers für Daten zur VM mit aktivierter Zwischenspeicherung

Sie haben sich dafür entschieden, diese Änderungen über das Azure-Portal vorzunehmen.

In dieser Übung wird Schritt für Schritt erklärt, wie Sie die Änderungen an einer VM vornehmen, die oben beschrieben wurde. Zuerst melden Sie sich am Portal an und erstellen eine VM.

## <a name="sign-in-to-the-azure-portal"></a>Anmelden am Azure-Portal
<!---TODO: Update for sandbox?--->

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

## <a name="create-a-virtual-machine"></a>Erstellen eines virtuellen Computers

In diesem Schritt erstellen wir eine VM mit den folgenden Eigenschaften.

|Eigenschaft  |Wert  |
|---------|---------|
|Image     |   **Windows Server 2016 Datacenter**      |
|Name     |   **fotoshareVM**     |
|Ressourcengruppe     |   **fotoshare-rg**      |


1. Wählen Sie im linken Menü des Portals die Option **Virtuelle Computer**.

1. Wählen Sie anschließend oben links auf dem Bildschirm **Virtuelle Computer** die Option **+ Hinzufügen**. Mit dieser Aktion wird der Erstellungsvorgang gestartet.

1. Geben Sie im Panel „Compute“, in dem die verfügbaren VM-Images aufgeführt sind, im Suchfeld *Windows Server 2016 Datacenter* ein.

1. Wählen Sie in den Suchergebnissen den Eintrag **Windows Server 2016 Datacenter** und dann die Option **Erstellen**, um den Prozess für die VM-Erstellung zu starten.

1. Geben Sie im Panel **Grundlagen** im Feld **Name** den Namen **fotoshareVM** ein.

1. Geben Sie in den Feldern **Benutzername** und **Kennwort** einen Namen und ein Kennwort für ein Administratorkonto auf diesem Server ein.

1. Wählen Sie in der Dropdownliste **Abonnement** Ihr Azure-Abonnement aus.

1. Wählen Sie unter **Ressourcengruppe** die Option **Neu erstellen**, und geben Sie im Feld den Namen **fotoshare-rg** ein.

1. Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.

Hier ist ein Beispiel für eine ausgefüllte Konfiguration vom Typ **Grundlagen** angegeben.

![Screenshot: Ausgefüllte Konfiguration „Grundlagen“](../media-draft/vm-basics-settings.PNG)

1. Wählen Sie **OK**, um mit dem nächsten Schritt fortzufahren.

Als Nächstes wählen Sie eine Größe für die VM aus und starten die Bereitstellung:

> [!IMPORTANT]
> Beachten Sie hierbei, dass die Datenträgerzwischenspeicherung für virtuelle Computer der L- und B-Serie nicht geändert werden kann. Wir wählen eine andere Größe.

1. Wählen Sie im Abschnitt **Größe auswählen** die SKU vom Typ **Standard** aus, z.B. **F1s**, und wählen Sie anschließend die Option **Auswählen**.

1. Scrollen Sie im Bereich **Einstellungen** nach unten. Sie sehen, dass keine Option zum Konfigurieren der Datenträgerzwischenspeicherung vorhanden ist. Akzeptieren Sie in diesem Schritt die Standardeinstellungen, und wählen Sie unten im Bereich **OK**.

1. Sehen Sie sich im Panel **Erstellen** die Übersicht an, und wählen Sie anschließend die Option **Erstellen**.

1. Die VM-Erstellung kann ein Weile dauern. Warten Sie die Bereitstellung des virtuellen Computers ab, bevor Sie mit der Übung fortfahren. Sie erhalten im Notification Hub eine Nachricht, wenn der Vorgang abgeschlossen ist.

> [!IMPORTANT]
> Da wir diesen virtuellen Computer in der nächsten Lektion verwenden, sollten Sie ihn vorerst beibehalten.

## <a name="view-os-disk-cache-status-in-the-portal"></a>Anzeigen des Betriebssystemdatenträger-Cachestatus im Portal

Nachdem unsere VM bereitgestellt wurde, können wir den Cachestatus des Betriebssystemdatenträgers mit den folgenden Schritten bestätigen.

1. Klicken Sie im linken Menü auf **Alle Ressourcen**, und wählen Sie dann die VM **fotoshareVM** aus.

1. Wählen Sie auf dem Bildschirm **Virtueller Computer** unter **EINSTELLUNGEN** die Option **Datenträger**.

1. Im Bereich **Datenträger** verfügt der virtuelle Computer über einen Datenträger, nämlich den Betriebssystemdatenträger. Der Cachetyp ist derzeit auf den Standardwert **Lesen/Schreiben** festgelegt.

![Screenshot: Betriebssystemdatenträger und Datenträger, jeweils mit schreibgeschütztem Caching](../media-draft/os-disk-rw.PNG)

## <a name="change-the-cache-settings-of-the-os-disk-in-the-portal"></a>Ändern der Cacheeinstellungen des Betriebssystemdatenträgers im Portal

1. Wählen Sie im Bereich **Datenträger** oben links die Option **Bearbeiten**.

1. Ändern Sie den Wert **HOSTZWISCHENSPEICHERUNG** für den Betriebssystemdatenträger in **Schreibgeschützt**, indem Sie die Dropdownliste verwenden, und wählen Sie dann oben links die Option **Speichern**.

1. Dieses Update dauert eine Weile. Der Grund hierfür ist, dass der Zieldatenträger durch das Ändern der Cacheeinstellung eines Azure-Datenträgers getrennt und dann erneut angefügt wird. Wenn es sich um den Betriebssystemdatenträger handelt, wird auch der virtuelle Computer neu gestartet. Wenn das Update abgeschlossen ist, erhalten Sie eine Benachrichtigung, die dem folgenden Beispiel ähnelt.

![Beispiel für eine Benachrichtigung nach Abschluss des Updatevorgangs für die Cacheeinstellung](../media-draft/vm-disk-update-complete.PNG)

4. Wenn der Vorgang abgeschlossen ist, ist der Cachetyp des Betriebssystemdatenträgers auf **Schreibgeschützt** festgelegt.

Als Nächstes führen wir die Konfiguration des Caches für den für Daten bestimmten Datenträger durch. Wir müssen zunächst einen Datenträger erstellen, um ihn konfigurieren zu können.

## <a name="add-a-data-disk-to-the-vm-and-set-caching-type"></a>Hinzufügen eines Datenträgers zum virtuellen Computer und Festlegen des Cachetyps

1. In der Ansicht **Datenträger** unserer VM im Portal können Sie jetzt die Option **Datenträger hinzufügen** wählen. Im Feld **Name** wird sofort ein Fehler mit dem Hinweis angezeigt, dass das Feld nicht leer sein darf. Da wir noch nicht über einen Datenträger für Daten verfügen, erstellen wir ihn jetzt.

1. Klicken Sie in die Liste **Namen** und dann auf **Datenträger erstellen**.

1. Geben Sie im Bereich **Verwalteten Datenträger erstellen** im Feld **Name** den Namen **fotosharesVM-data** ein.

1. Wählen Sie unter **Ressourcengruppe** die Option **Vorhandene verwenden** und dann im Dropdownmenü die Option **fotoshare-rg**.

1. Wählen Sie unten auf dem Bildschirm die Option **Erstellen**.

1. Warten Sie, bis der Datenträger erstellt wurde, bevor Sie fortfahren.

1. Ändern Sie den Wert **HOSTZWISCHENSPEICHERUNG** für den neuen Datenträger in **Schreibgeschützt**, indem Sie die Dropdownliste verwenden, und wählen Sie dann oben links die Option **Speichern**.

1. Warten Sie, bis der virtuelle Computer aktualisiert wurde. Die Aktualisierung dauert eine Weile, weil Azure die Zuordnung des Datenträgers aufhebt und ihn dann neu zuordnet, um diese Einstellung zu ändern.

1. Wenn der Vorgang abgeschlossen ist, ist der Cachetyp des Datenträgers auf **Schreibgeschützt** festgelegt.

In dieser Übung haben wir das Azure-Portal verwendet, um die Zwischenspeicherung auf einem neuen virtuellen Computer zu konfigurieren, die Cacheeinstellungen auf einem vorhandenen Datenträger zu ändern und die Zwischenspeicherung auf einem neuen Datenträger zu konfigurieren. Im folgenden Screenshot ist die endgültige Konfiguration dargestellt. 

![Screenshot: Betriebssystemdatenträger und Datenträger, jeweils mit schreibgeschütztem Caching](../media-draft/disks-final-config-portal.PNG)