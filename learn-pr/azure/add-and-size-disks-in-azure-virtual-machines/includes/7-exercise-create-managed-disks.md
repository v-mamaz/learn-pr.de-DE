In dieser kurzen Übung erfahren wir, Migrieren von einer virtuellen Festplatte mit vorhandenen, nicht verwalteten zu verwalteten einer virtuellen Festplatte. 

## <a name="sign-in-to-azure"></a>Anmelden bei Azure

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

## <a name="migrate-our-disks-to-managed-disks"></a>Datenträger zu managed Disks migrieren

1. Wählen Sie im Azure-Portal im Navigationsbereich auf der linken Seite **VMs**.

1. Wählen Sie in der Liste der virtuellen Maschinen, unsere virtuellen Computer **MailSenderVM**.

1. In der **MailSenderVM** Bereich unter **EINSTELLUNGEN**Option **Datenträger**.

1. In der **MailSenderVM - Datenträger** Seite **Migrieren zu managed Disks**.

1. In der **Migrieren zu managed Disks** Seite **migrieren**. Azure den virtuellen Computer beendet, migriert die Datenträger und startet dann den virtuellen Computer neu. Dieser Vorgang kann mehrere Minuten dauern.

Datenträger migriert in verwaltete Datenträger in dieser Übung. Mithilfe von verwalteten Datenträgern müssen Sie Storage-Konten für diese Datenträger nicht konfigurieren, weil Azure für Sie verwaltet.
