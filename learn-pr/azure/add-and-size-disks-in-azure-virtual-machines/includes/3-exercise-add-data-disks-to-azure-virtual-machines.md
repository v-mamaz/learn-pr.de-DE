In dieser Übung wird angenommen, dass Ihr Unternehmen einen Simple Mail Transfer Protocol (SMTP) e-Mail-Server ausgeführt wird. Möchten Sie diesen Server in Azure zu migrieren. Sie möchten den SMTP-Server, um eingehende Nachrichten für Ihre eigene Domäne in einem Ordner namens "Löschen" aus, auf einer dedizierten virtuellen Festplatte zu speichern.

Das Ziel dieser Übung ist auf der Windows virtuellen Computer (VM) erstellen, und fügen Sie eine neue virtuelle Festplatte (VHD) wird aufgerufen, um das Verzeichnis "Drop" Speichern "eingehenden".

## <a name="sign-in-to-azure"></a>Anmelden bei Azure

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

## <a name="create-a-windows-vm-in-the-azure-portal"></a>Erstellen einer Windows-VM im Azure-portal

Um einen virtuellen Computer zum Hosten des SMTP-Servers mit der Datenträger für Daten zu erstellen, gehen Sie folgendermaßen vor:

1. Wählen Sie **erstellen Sie eine Ressource** in der oberen linken Ecke des Azure-Portals.

1. Suchen Sie in das Suchfeld oberhalb der Liste der Azure Marketplace-Ressourcen, und wählen Sie **Windows Server 2016 Datacenter**, und wählen Sie dann **erstellen**.

1. In der **Grundlagen** Bereich, der mit der rechten Seite geöffnet wird, geben die folgenden Eigenschaftenwerte fest. 


|Eigenschaft  |Wert  |Hinweise  |
|---------|---------|---------|
|Name     |   **MailSenderVM**      |         |
|VM-Datenträgertyp     |  **Standard HDD**       |   Wählen Sie diesen Wert aus der Dropdownliste aus.      |
|Benutzername     |  **mailmaster**       |         |
|Password     |  Das Kennwort muss mindestens zwölf Zeichen lang sein und die [definierten Anforderungen an die Komplexität](https://docs.microsoft.com/azure/virtual-machines/windows/faq#what-are-the-password-requirements-when-creating-a-vm) erfüllen.       | Stellen Sie sicher, dass diese Benutzernamen und ein Kennwort merken werden, da wir diese in das Modul verwendet werden.         |
|Abonnement     |  Wählen Sie Ihr Abonnement aus.       |  Wählen Sie diesen Wert aus der Dropdownliste aus.       |
|Ressourcengruppe     |  Wählen Sie **vorhandene** , und wählen Sie <rgn>[Ressourcengruppennamen Sandkasten]</rgn>.       |  Sammeln wir alle Ressourcen, die in diesem Modul verwendet werden, in einer Ressourcengruppe.       |
|Standort     |   Ein Speicherort in Ihrer Nähe.      | Wählen Sie diesen Wert aus der Dropdownliste aus.        |

4. Wählen Sie **OK** am unteren Rand der **Grundlagen** Seite, um weiterhin die **Größe** Konfigurationsbereich.

1. In der **Größe** Konfigurationsbereich, suchen Sie nach, und wählen **B1ms**, und klicken Sie dann auf **wählen**.

1. In der **Einstellungen** Bereich verlassen die meisten Werte die Standardwerte. Klicken Sie unter **verwaltete Datenträger verwenden**, klicken Sie auf **keine**. Verwaltete Datenträger später in diesem Modul ist werden gleich erörtert.

1. In der **öffentliche Eingangsports hinzufügen** Dropdown-Liste wählen **RDP (3389)**. Wir verwenden diesen Port auf den Remotecomputer in den virtuellen Computer nach der Erstellung.

1. Behalten Sie Standardwerte für alle anderen Einstellungen, und klicken Sie dann auf **OK**.

1. In der **erstellen** Bereich, überprüfen Sie die Konfiguration.

1. Wenn Sie die Konfiguration überprüft haben, wählen Sie **erstellen**. Azure erstellt und startet die neue VM.

> [!TIP]
> Erstellen Ihres virtuellen Computers und die Bereitstellung in Azure können einige Minuten dauern. Sie können verfolgen, wie in der **Benachrichtigungen** Hub. Azure wird ein Benachrichtigungsdialogfeld angezeigt, wenn er abgeschlossen ist.

## <a name="add-an-empty-data-disk-to-our-vm"></a>Fügen Sie einen leeren Datenträger an den virtuellen Computer hinzu.

Wir sind auf den Datenträger zu benennen, speichert das Verzeichnis "Drop" für den SMTP-Server "Eingehend". Fügen Sie einen neuen leeren Datenträger an den Server mithilfe der folgenden Schritte aus:

1. In der Navigationsleiste auf der linken Seite unter **Favorits**Option **VMs**.

1. Wählen Sie in der Liste der VMs, **MailSenderVM**.

1. Klicken Sie unter **Einstellungen** von der **MailSenderVM** Menü auf der linken Seite auf Konfiguration **Datenträger**.

1. Klicken Sie unter **Datenträger**Option **Datenträger**.

1. In der **nicht verwaltete Datenträger anfügen** Bereich legen Sie die folgenden Eigenschaften.

|Eigenschaft  |Wert  |Hinweise  |
|---------|---------|---------|
|Name     |   **MailSenderVMIncoming**      |         |
|Quelltyp     |  **Neu (leerer Datenträger)**       |   Wählen Sie diesen Wert aus der Dropdownliste aus.       |
|Kontotyp     |  **Standard HDD**       |  Wählen Sie diesen Wert aus der Dropdownliste aus.        |

6. Auf der linken Seite von der **Speichercontainer** die Option **Durchsuchen**.

1. Suchen Sie in der Liste der Speicherkonten, für das Speicherkonto, deren Name mit beginnt **Mailinfrastructure** und wählen Sie ihn.

1. Klicken Sie in der Liste der Container, auf **Vhds** und wählen Sie dann **wählen**.

1. Auf der **nicht verwalteten Datenträger anfügen** auf **OK**.

1. Auf der **MailSenderVM - Datenträger** auf **speichern**.

Wir haben jetzt einen Datenträger namens definiert **MainSenderVMIncoming**. Um den Datenträger zu verwenden, müssen wir zunächst zum Partitionieren und formatieren Sie ihn, wenn wir auf dem virtuellen Computer anmelden.

## <a name="partition-and-format-a-data-disk"></a>Partitionieren und Formatieren eines Datenträgers

Wie bei physischen Datenträgern zu initiieren Sie, und formatieren Sie eine Partition auf einer virtuellen Festplatte zu, bevor sie verwendet werden kann.

### <a name="log-into-our-windows-vm-using-rdp"></a>Melden Sie sich unsere Windows-VM über RDP

1. In der **MailSenderVM** VM Hauptbildschirm auf **Übersicht**.

1. Wählen Sie **Connect** von links oben auf dem Übersichtsbildschirm.

1. In der **Herstellen einer Verbindung mit dem virtuellen Computer** Dialogfeld, das geöffnet wird, auf der rechten Seite wählen **RDP-Datei herunterladen**.

   ![Screenshot des Dialogfelds "Verbinden mit dem virtuellen Computer" mit hervorgehobener Schaltfläche "Herunterladen der RDP-Datei".](../media-draft/download-rdp.png)

4. Eine Datei namens **MailSenderVM.rdp** auf Ihrem lokalen heruntergeladen `Downloads` Ordner. Diese Datei ist die remotedesktopkonfiguration-Datei für die VM MailSenderVM. Öffnen Sie die Datei, um die Verbindung herzustellen.

1. In der **Remotedesktopverbindung** Dialogfeld klicken Sie auf **Connect**.

1. Klicken Sie im Dialogfeld **Windows-Sicherheit** auf **Anderes Konto verwenden**.

1. In der **Benutzername** Geben Sie im Textfeld **Mailmaster**.

1. In der **Kennwort** Textbox, geben Sie das Kennwort, das Sie für diesen Benutzer in dieser Übung eingegeben haben. 

1. In der **Remotedesktopverbindung** Dialogfeld klicken Sie auf **Ja**.

Eine Remotedesktopsitzung mit dem virtuellen Computer wird nun gestartet. Dauert möglicherweise einige Minuten, bis Sie zum ersten Mal anmelden. Wenn die Anmeldung abgeschlossen ist, die **Server-Manager** Tool wird auf dem Bildschirm angezeigt werden.

### <a name="partition-and-format-our-data-disk-using-server-manager"></a>Partitionieren Sie und formatieren Sie unsere Datenträger für Daten mit dem Server-Manager

1. Wenn **Server-Manager** angezeigt, wählen **Datei- und Speicherdienste** im Navigationsbereich auf der linken Seite.

1. Klicken Sie unter **Volumes**Option **Datenträger**.

1. Die Liste der Datenträger, auf den Datenträger **0** ist das Betriebssystem-Datenträger und Datenträger **1** ist der temporäre Datenträger. Select Disk **2**, d.h., dass die neue virtuelle Festplatte, die Sie gerade hinzugefügt haben.

1. Am oberen Rand der **VOLUMES** wählen Sie im Bereich **Aufgaben** gefolgt von **neues Volume...** . Klicken Sie im Menü wird in der oberen rechten Rand des Bildschirms wie folgt.

   ![Screenshot von "Aufgaben" im Menü Erweitert, um drei Menüelemente anzuzeigen. Sie sind "Neue Volume...", "Rescan Storage" und "Aktualisieren".](../media-draft/tasks-menu.png)


1. In der **neues Volume** -Assistenten klicken Sie auf **Weiter**.

1. In der **Server und Datenträger auswählen** Seite **MailSenderVM** und **Disk 2**, und klicken Sie dann auf **Weiter**.

1. In der **"Offline" oder uninitialisiert Datenträger** Dialogfeld klicken Sie auf **OK**.

1. In der **Geben Sie die Größe des Volumes** auf **Weiter**.

1. In der **Ihr einen Laufwerkbuchstaben zuweisen** Seite **F:** gefolgt von **Weiter**.

1. In der **Dateisystemeinstellungen auswählen** auf der Seite die **Volumebezeichnung** Geben Sie im Textfeld **eingehende** und wählen Sie dann **Weiter**.

1. In der **Auswahl bestätigen** Seite **erstellen**. Windows startet den Datenträger und formatiert die neue Partition.

1. In der **Abschluss** Seite **schließen**.

Werfen wir einen Blick auf unser neues Datenträgervolume im Datei-Explorer.

1. Open **Datei-Explorer**.

1. Klicken Sie im Navigationsbereich links auf **diesem PC** und doppelklicken Sie dann auf **eingehenden (f:))**.

1. Wählen Sie **Startseite**, und klicken Sie dann **neuer Ordner**.

1. Typ **löschen** und drücken Sie dann die EINGABETASTE.

Wir haben jetzt ein neues Volume erstellt, die auf unserem virtuellen Festplatte wird aufgerufen, **eingehende**, und wir haben einen Ordner namens erstellt **löschen** auf diesem Volume.  

1. Schließen Sie Windows Explorer.

1. Auf der **Taskleiste**, klicken Sie auf die **starten** , zeigen Sie auf die **Power** Schaltfläche, und klicken Sie dann auf **trennen**.

Herzlichen Glückwunsch! Sie haben erfolgreich eine Windows-VM erstellt, eine neue virtuelle Festplatte angefügt, einen Ordner auf diesem Volume hinzugefügt und ein Volume auf dieser VHD erstellt. Wenn Sie sich erinnern, wurde der Datenträgertyp für die neue VHD verwendet eine **Standard HDD**. In der nächsten Einheit erfahren wir, die Unterschiede zwischen Standard- und Storage Premium. 
