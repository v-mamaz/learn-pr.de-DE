In dieser Übung wird angenommen, dass Ihr Unternehmen einen SMTP-E-Mail-Server (Simple Mail Transfer Protocol) verwendet. Sie möchten diesen Server zu Azure migrieren. Sie möchten eingehende Nachrichten für Ihre eigene Domäne auf dem SMTP-Server in einem Ordner namens „Drop“ auf einer dedizierten VHD speichern.

Das Ziel dieser Übung ist, einen virtuellen Windows-Computer (VM) zu erstellen und eine neue virtuelle Festplatte (VHD) namens „Incoming“ für das Verzeichnis „Drop“ anzufügen.

## <a name="sign-in-to-azure"></a>Anmelden bei Azure
<!---TODO: Need update for sanbox?--->

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

## <a name="create-a-windows-vm-in-the-azure-portal"></a>Erstellen einer Windows-VM im Azure-Portal

Um eine VM zum Hosten des SMTP-Servers mit den Datenlaufwerken zu erstellen, gehen Sie folgendermaßen vor:

1. Wählen Sie im Azure-Portal oben links **Ressource erstellen** aus.

1. Suchen Sie im Suchfeld oberhalb der Liste der Azure Marketplace-Ressourcen nach **Windows Server 2016 Datacenter**, und wählen Sie dann **Erstellen** aus.

1. Geben Sie im Bereich **Grundlagen**, der auf der rechten Seite geöffnet wird, die folgenden Eigenschaftswerte ein. 


|Eigenschaft  |Wert  |Hinweise  |
|---------|---------|---------|
|Name     |   **MailSenderVM**      |         |
|VM-Datenträgertyp     |  **HDD Standard**       |   Wählen Sie diesen Wert aus der Dropdownliste aus.      |
|Benutzername     |  **mailmaster**       |         |
|Kennwort     |  Das Kennwort muss mindestens zwölf Zeichen lang sein und die [definierten Anforderungen an die Komplexität](https://docs.microsoft.com/azure/virtual-machines/windows/faq#what-are-the-password-requirements-when-creating-a-vm) erfüllen.       | Sie müssen sich diesen Benutzernamen und das Kennwort merken, da beides im gesamten Modul verwendet wird.         |
|Abonnement     |  Wählen Sie Ihr Abonnement aus.       |  Wählen Sie diesen Wert aus der Dropdownliste aus.       |
|Ressourcengruppe     |  Klicken Sie auf **Neu erstellen**, und geben Sie dann **MailInfrastructure** ein.       |  Wir sammeln alle Ressourcen, die in diesem Modul verwendet werden, in einer Ressourcengruppe.       |
|Standort     |   Ein Standort in Ihrer Nähe.      | Wählen Sie diesen Wert aus der Dropdownliste aus.        |

4. Wählen Sie unten auf der Seite **Grundlagen** die Option **OK** aus, um mit dem Konfigurationsbereich **Größe** fortzufahren.

1. Suchen Sie im Konfigurationsbereich **Größe** nach **B1ms**, und wählen Sie sie aus, und klicken Sie dann auf **Auswählen**.

1. Klicken Sie im Bereich **Einstellungen** unter **Verwaltete Datenträger verwenden** auf **Nein**. Verwaltete Datenträger werden später in diesem Modul erörtert.

1. Wählen Sie in der Dropdownliste **Öffentliche Eingangsports hinzufügen** den Port **RDP (3389)** aus. Wir verwenden diesen Port für den Remotezugriff auf die VM, nachdem sie erstellt wurde.

1. Behalten Sie für alle anderen Einstellungen die Standardwerte bei, und klicken Sie dann auf **OK**.

1. Prüfen Sie im Bereich **Erstellen** die Konfiguration.

1. Wenn Sie die Konfiguration geprüft haben, wählen Sie **Erstellen** aus. Azure erstellt und startet die neue VM.

> [!TIP]
> Das Erstellen Ihrer VM und deren Bereitstellung in Azure kann einige Minuten dauern. Sie können den Fortschritt im Hub **Benachrichtigungen** überwachen. Beim Abschluss zeigt Azure ein Benachrichtigungsdialogfeld an.

## <a name="add-an-empty-data-disk-to-our-vm"></a>Hinzufügen eines leeren Datenträgers zur VM

Wir nennen den Datenträger, auf dem das Verzeichnis „Drop“ für den SMTP-Server gespeichert wird, „Incoming“. Fügen Sie mit den folgenden Schritten dem Server einen neuen leeren Datenträger hinzu:

1. Wählen Sie im Navigationsbereich auf der linken Seite unter **FAVORITEN** die Option **Virtuelle Computer** aus.

1. Wählen Sie in der Liste der VMs **MailSenderVM** aus.

1. Wählen Sie auf der linken Seite im Konfigurationsmenü von **MailSenderVM** unter **EINSTELLUNGEN** die Option **Datenträger** aus.

1. Wählen Sie unter **Datenträger** die Option **Datenträger hinzufügen** aus.

1. Legen Sie im Bereich **Nicht verwaltete Datenträger anfügen** die folgenden Eigenschaften fest.


|Eigenschaft  |Wert  |Hinweise  |
|---------|---------|---------|
|Name     |   **MailSenderVMIncoming**      |         |
|Quelltyp     |  **Neu (leerer Datenträger)**       |   Wählen Sie diesen Wert aus der Dropdownliste aus.       |
|Kontotyp     |  **HDD Standard**       |  Wählen Sie diesen Wert aus der Dropdownliste aus.        |


6. Wählen Sie links neben dem Feld **Speichercontainer** die Option **Durchsuchen** aus.

1. Suchen Sie in der Liste der Speicherkonten nach dem Speicherkonto, dessen Name mit **mailinfrastructure** beginnt, und wählen Sie es aus.

1. Klicken Sie in der Liste der Container auf **VHDs**, und wählen Sie dann **Auswählen** aus.

1. Wählen Sie auf dem Bildschirm **Nicht verwalteten Datenträger anfügen** die Option **OK** aus.

1. Wählen Sie auf dem Bildschirm **MailSenderVM – Datenträger** die Option **Speichern** aus.

Wir haben jetzt einen Datenträger namens **MainSenderVMIncoming** definiert. Um den Datenträger zu verwenden, müssen wir ihn zunächst partitionieren und formatieren, wenn wir uns bei der VM anmelden. 

## <a name="partition-and-format-a-data-disk"></a>Partitionieren und Formatieren eines Datenträgers

Wie bei physischen Datenträgern müssen Sie auf einer VHD eine Partition initialisieren und formatieren, bevor sie verwendet werden kann.

### <a name="log-into-our-windows-vm-using-rdp"></a>Anmelden bei der Windows-VM über RDP

1. Wählen Sie auf dem Hauptbildschirm des virtuellen Computers **MailSenderVM** die Option **Übersicht** aus.

1. Wählen Sie auf dem Übersichtsbildschirm oben links **Verbinden** aus.

1. Wählen Sie im Dialogfeld **Herstellen einer Verbindung mit dem virtuellen Computer** auf der rechten Seite **RDP-Datei herunterladen** aus.

   ![Screenshot des Dialogfelds „Herstellen einer Verbindung mit dem virtuellen Computer“ mit hervorgehobener Schaltfläche „RDP-Datei herunterladen“.](../media-draft/download-rdp.png)

4. Eine Datei namens **MailSenderVM.rdp** wird in Ihren lokalen Ordner `Downloads` heruntergeladen. Diese Datei ist die Datei mit der Remotedesktopkonfiguration für den virtuellen Computer „MailSenderVM“. Öffnen Sie die Datei, um die Verbindung herzustellen.

1. Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **Verbinden**.

1. Klicken Sie im Dialogfeld **Windows-Sicherheit** auf **Anderes Konto verwenden**.

1. Geben Sie im Textfeld **Benutzername** den Text **mailmaster** ein.

1. Geben Sie im Textfeld **Kennwort** das Kennwort ein, das Sie in dieser Übung für diesen Benutzernamen eingegeben haben. 

1. Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **Ja**.

Eine Remotedesktopsitzung mit dem virtuellen Computer wird gestartet. Die erste Anmeldung kann einige Minuten dauern. Wenn die Anmeldung abgeschlossen ist, wird das Tool **Server-Manager** auf dem Bildschirm angezeigt.

### <a name="partition-and-format-our-data-disk-using-server-manager"></a>Partitionieren und Formatieren des Datenträgers mit dem Server-Manager

1. Wenn **Server-Manager** angezeigt wird, wählen im Navigationsbereich auf der linken Seite **Datei- und Speicherdienste** aus.

1. Wählen Sie unter **Volumes** die Option **Datenträger** aus.

1. In der Liste der Datenträger ist der Datenträger **0** der Betriebssystemdatenträger, und der Datenträger **1** ist der temporäre Datenträger. Wählen Sie den Datenträger **2** aus. Dies ist die VHD, die Sie gerade hinzugefügt haben.

1. Wählen Sie oben im Bereich **VOLUMES** die Option **AUFGABEN** und dann **Neues Volume** aus. Das Menü befindet sich oben rechts auf dem Bildschirm.

   ![Screenshot des erweiterten Menüs „AUFGABEN“ mit drei Menüelementen. Es sind: „Neues Volume“, „Speicher neu einlesen“ und „Aktualisieren“.](../media-draft/tasks-menu.png)


1. Klicken Sie im Assistenten **Neues Volume** auf **Weiter**.

1. Wählen Sie auf der Seite **Server und Datenträger auswählen** die Einträge **MailSenderVM** und **Datenträger 2** aus, und klicken Sie dann auf **Weiter**.

1. Klicken Sie im Dialogfeld **Datenträger offline oder nicht initialisiert** auf **OK**.

1. Klicken Sie auf der Seite **Geben Sie die Größe des Volumes an** auf **Weiter**.

1. Wählen Sie auf der Seite **Einen Laufwerkbuchstaben zuweisen** den Buchstaben **F:** und dann **Weiter** aus.

1. Geben Sie auf der Seite **Dateisystemeinstellungen auswählen** im Textfeld **Volumebezeichnung** den Namen **Incoming** ein, und wählen Sie dann **Weiter** aus.

1. Wählen Sie auf der Seite **Auswahl bestätigen** die Option **Erstellen** aus. Windows initialisiert den Datenträger und formatiert die neue Partition.

1. Wählen Sie auf der Seite **Abschluss** die Option **Schließen** aus.

Sehen wir uns das neue Datenträgervolume im Datei-Explorer an. 
1. Öffnen Sie den **Datei-Explorer**.

1. Klicken Sie im Navigationsbereich auf der linken Seite auf **Dieser PC**, und doppelklicken Sie dann auf **Incoming (F:)**.

1. Wählen Sie **Start** und dann **Neuer Ordner** aus.

1. Geben Sie **Drop** ein, und drücken Sie dann die EINGABETASTE.

Wir haben jetzt auf der VHD ein neues Volume namens **Incoming** und auf dem Volume einen Ordner namens **Drop** erstellt.  

1. Schließen Sie Windows-Explorer.

1. Klicken Sie auf der **Taskleiste** auf die Schaltfläche **Start**, klicken Sie auf die Schaltfläche **Ein/Aus**, und klicken Sie dann auf **Trennen**.

Herzlichen Glückwunsch! Sie haben erfolgreich eine Windows-VM erstellt, eine neue VHD angefügt, auf der VHD ein Volume erstellt und dem Volume einen Ordner hinzugefügt. Der Datenträgertyp, den wir für die neue VHD verwendet haben, war **HDD Standard**. In der nächsten Einheit lernen Sie die Unterschiede zwischen Standardspeicher und Storage Premium kennen. 
