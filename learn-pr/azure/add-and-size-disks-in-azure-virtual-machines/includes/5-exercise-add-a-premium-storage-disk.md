Wenn Ihre virtuellen Computer (VM) eine Datenträger-Intensive Anwendung hostet, sollten Sie die Verwendung von Storage Premium für die virtuellen Festplatten (VHDs).

Beispielsweise möchten Sie eine virtuelle Festplatte zum Speichern ausgehenden e-Mails auf Ihr SMTP-Server-VM hinzufügen. Um die datenträgerleistung zu optimieren, entscheiden Sie in Storage Premium für ausgehende e-Mails.

Fügen Sie einen Premium-SSD mit dem virtuellen Computer an.

## <a name="sign-in-to-azure"></a>Anmelden bei Azure

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

## <a name="create-a-premium-storage-account"></a>Erstellen eines Premium-Speicherkontos

Alle Premium-Speicher-VHDs muss in einem Premium-Speicherkonto gespeichert werden. Um Premium-Speicherkonto zu erstellen, gehen Sie wie folgt vor.

1. Wählen Sie **Speicherkonten** unter **Favoriten** im linken Menü des Portals.

1. Wählen Sie **+ hinzufügen** am oben links auf die **Speicherkonten** Bildschirm.

1. In der **Storage-Konto erstellen** Bereich, der geöffnet wird, legen Sie die folgenden Eigenschaften.

|Eigenschaft  |Wert  |Hinweise  |
|---------|---------|---------|
|Name     |    *Ein eindeutiger Name (siehe Hinweis)*     |   Dieser Name muss für alle vorhandenen speicherkontonamen in Azure eindeutig sein. Er muss 3 bis 24 Zeichen lang sein und darf nur Kleinbuchstaben und Ziffern enthalten.      |
|Kontoart     |  **Speicher (Allgemein v1)**       |         |
|Standort     |  *Wählen Sie den gleichen Speicherort wie der virtuelle Computer, die Sie zuvor erstellt haben*       |         |
|Replikation     |   **Lokal redundanter Speicher (LRS)**      |  Wählen Sie diesen Wert aus der Dropdownliste aus. Wenn Sie sich erinnern, wir erstellen ein Storage Premium-Konto und Storage Premium unterstützt nur die LRS-Replikation.       |
|Leistung     |  **Premium**       | Storage Premium-Konten werden durch Solid State Drives gesichert und Leistung für konsistente, niedriger Latenz bieten.        |
|Ressourcengruppe     |  *Wählen Sie **vorhandene** und dann <rgn>[Sandkasten Resource Group-Name]</rgn>*      |  Wir möchten alle Ressourcen unter der gleichen Ressourcengruppe beibehalten.       |

Wenn Sie dieses Dialogfeld ausgefüllt haben, sollte es wie im folgenden Screenshot aussehen. 

!["Speicherkonto erstellen" Dialogfeld zeigt alle Eigenschaften festgelegt, wie beschrieben.](../media-draft/create-premium-sa.png)

1. Wählen Sie **erstellen** der Speicher für die kontoerstellung gestartet. Dieser Vorgang kann einige Minuten dauern. 

1. Wenn Sie eine Benachrichtigung erhalten, die Bereitstellung des neuen Speicherkontos, das erfolgreich abgeschlossen haben, wählen Sie **aktualisieren** in Storage-Konten auflisten zum Anzeigen von Storage Premium-Konto erstellt. Notieren Sie den Namen der dieses Konto an, wie er im nächsten Schritt verwendet wird.

## <a name="create-vhd-in-the-premium-storage-account"></a>Virtuelle Festplatte in Storage Premium-Konto erstellen

Jetzt können Sie fügen eine neue virtuelle Festplatte mit dem virtuellen Computer und Storage Premium-Konto als den Speicherort angeben. Führen Sie diese Schritte aus:

1. In der Navigationsleiste auf der linken Seite unter **Favoriten**Option **VMs**.

1. Wählen Sie in der Liste der VMs, **MailSenderVM**.

1. Klicken Sie unter **EINSTELLUNGEN** von der **MailSenderVM** Menü auf der linken Seite auf Konfiguration **Datenträger**.

1. Klicken Sie unter **Datenträger**Option **Datenträger**.

1. In der **nicht verwaltete Datenträger anfügen** Bereich legen Sie die folgenden Eigenschaften.


|Eigenschaft  |Wert  |Hinweise  |
|---------|---------|---------|
|Name     |   **MailSenderVMOutgoing**      |         |
|Quelltyp     |  **Neu (leerer Datenträger)**       |   Wählen Sie diesen Wert aus der Dropdownliste aus.       |
|Kontotyp     |  **Premium-SSD**       |  Wählen Sie diesen Wert aus der Dropdownliste aus.        |

1. Auf der linken Seite von der **Speichercontainer** die Option **Durchsuchen**.

1. Klicken Sie in der Liste der Speicherkonten suchen Sie, und wählen Sie die Storage Premium-Konto, die, das Sie zuvor in dieser Einheit erstellt haben. Der Typ des Eintrags als aufgeführt **Premium-LRS**.

1. Wählen Sie in der Liste der Container, __+ Container__.

1. In der **neuen Container** Bereich, in der **Namen** Geben Sie im Textfeld **Vhds** und wählen Sie dann **OK**.

1. Wählen Sie in der Liste der Container, **Vhds** und wählen Sie dann **wählen**.

1. Auf der **nicht verwalteten Datenträger anfügen** wählen Sie im Bereich **OK**.

1. Auf der **MailSenderVM - Datenträger** wählen Sie im Bereich **speichern**. Azure fügt die neue Storage Premium-Datenträger mit dem virtuellen Computer hinzu.

Der virtuelle Computer verfügt über ein Betriebssystem-Datenträger standard-Datenträger und SSD-basierte Premium-Datenträger.

> [!NOTE]
> Der neue Datenträger muss initialisiert, partitioniert und formatiert, bevor sie Daten speichern kann. Um Wiederholungen zu vermeiden, wurden diese Schritte aus dieser Übung ausgelassen. Wenn Sie diese Aufgaben ausführen möchten, führen Sie die Schritte in der [partitionieren und Formatieren eines Datenträgers](../3-exercise-add-data-disks-to-azure-virtual-machines.yml##partition-and-format-a-data-disk) Teil der vorherigen Übung.
