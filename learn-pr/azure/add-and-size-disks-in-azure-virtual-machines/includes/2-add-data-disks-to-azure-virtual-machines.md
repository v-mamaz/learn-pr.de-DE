Virtuelle Computer in Azure verwenden wie alle anderen Computer auch einen Datenträger, auf dem das Betriebssystem, Anwendungen und Daten gespeichert sind. Diese Datenträger werden als virtuelle Festplatten (VHDs) bezeichnet.

Angenommen, Sie haben in Azure einen virtuellen Computer (VM) erstellt, mit dem die Datenbank mit den Fallverläufen gehostet wird, die für Ihre Anwaltskanzlei wichtig sind. Eine gut entworfene Datenträgerkonfiguration ist für eine hohe Leistung und Stabilität in Bezug auf SQL Server von grundlegender Bedeutung.

In dieser Einheit wird beschrieben, wie Sie die richtigen Konfigurationswerte für Ihre Datenträger auswählen und diese Datenträger an eine VM anfügen.

## <a name="how-disks-are-used-by-vms"></a>Verwendung von Datenträgern durch virtuelle Computer

Für VMs werden Datenträger zu drei unterschiedlichen Zwecken genutzt:

- **Speicher für Betriebssystem**: Jede VM enthält einen Datenträger, auf dem das Betriebssystem gespeichert ist. Dieses Laufwerk ist als SATA-Laufwerk registriert und wird in Windows als Laufwerk „C:“ bezeichnet und für Unix-Betriebssysteme unter „/“ bereitgestellt. Es hat eine maximale Kapazität von 2.048 GB, und sein Inhalt stammt aus dem VM-Image, das Sie für die Erstellung der VM verwendet haben.
- **Temporärer Speicher**: Jede VM enthält auch eine temporäre VHD, die für Auslagerungsdateien genutzt wird. Es kann sein, dass die Daten auf diesem Laufwerk bei der Wartung oder erneuten Bereitstellung verloren gehen. Das Laufwerk hat auf einer Windows-VM standardmäßig die Bezeichnung „D:“. Verwenden Sie dieses Laufwerk nicht zum Speichern von wichtigen Daten, die nicht verloren gehen dürfen.
- **Datenspeicher**: Ein Datenträger ist ein beliebiger anderer Datenträger, der an eine VM angefügt ist. Sie verwenden Datenträger zum Speichern von Dateien, Datenbanken und beliebigen anderen Daten, die Sie über Neustarts hinweg beibehalten müssen. Einige VM-Images enthalten standardmäßig bereits Datenträger für Daten. Sie können bis zur maximalen Anzahl, die durch die Größe der VM vorgegeben ist, auch eigene Datenträger hinzufügen. Jeder Datenträger wird als SCSI-Laufwerk registriert und verfügt über eine maximale Kapazität von 4.095 GB. Sie können Laufwerkbuchstaben oder Bereitstellungspunkte für Ihre Datenlaufwerke wählen.

## <a name="storing-vhd-files"></a>Speichern von VHD-Dateien

In Azure werden VHDs unter einem Azure-Speicherkonto als **Seitenblobs** gespeichert.

Die folgende Tabelle enthält die verschiedenen Arten von Speicherkonten sowie die Objekte, die jeweils mit den Konten verwendet werden können.

|**Speicherkontotyp**|**Standard (allgemein)**|**Premium (allgemein)**|**Blobspeicher, Zugriffsebenen „Heiß“ und „Kalt“**|
|-----|-----|-----|-----|
|**Unterstützte Dienste**| Azure Blob Storage, Azure Files, Azure Queue Storage | Blobspeicher | Blobspeicher|
|**Unterstützte Blobtypen**|Blockblobs, Seitenblobs und Anfügeblobs | Seitenblobs | Blockblobs und Anfügeblobs|

Da VHDs als Seitenblobs gespeichert werden und nur Standardspeicher Seitenblobs unterstützt, benötigen Sie zum Speichern von VHDs ein Standardspeicherkonto.

## <a name="attach-data-disks-to-vms"></a>Anfügen von Datenträgern an VMs

Sie können einem virtuellen Computer jederzeit Datenträger hinzufügen, indem Sie diese an die VM anfügen. Beim Anfügen eines Datenträgers wird die VHD-Datei der VM zugeordnet. 

Die virtuelle Festplatte kann nicht aus dem Speicher gelöscht werden, solange sie angefügt ist.

### <a name="attach-an-existing-data-disk-to-an-azure-vm"></a>Anfügen eines vorhandenen Datenträgers an eine Azure-VM

Unter Umständen verfügen Sie bereits über eine VHD zum Speichern der Daten, die Sie auf Ihrer Azure-VM verwenden möchten. Im Szenario mit der Anwaltskanzlei kann es beispielsweise sein, dass Sie Ihre physischen Datenträger bereits lokal in VHDs konvertiert haben. In diesem Fall können Sie das PowerShell-Cmdlet `Add-AzureRmVhd` verwenden, um den Upload in das Speicherkonto durchzuführen. Dieses Cmdlet ist für das Übertragen von VHD-Dateien optimiert und kann bewirken, dass der Upload schneller als mit anderen Methoden durchgeführt wird. Die Übertragung wird mit mehreren Threads durchgeführt, um eine optimale Leistung zu erzielen. Nachdem die VHD hochgeladen wurde, können Sie sie als Datenträger an eine vorhandene VM anfügen. Dieser Ansatz ist eine hervorragende Möglichkeit, um Daten jedes Typs auf Azure-VMs bereitzustellen. Die Daten sind automatisch auf der VM vorhanden, und es ist nicht erforderlich, den neuen Datenträger zu partitionieren oder zu formatieren.

### <a name="attach-a-new-data-disk-to-an-azure-vm"></a>Anfügen eines neuen Datenträgers an eine Azure-VM

Sie können das Azure-Portal nutzen, um einer VM einen neuen, leeren Datenträger hinzuzufügen. 

Im von Ihnen angegebenen Speicherkonto wird eine **VHD**-Datei als Seitenblob erstellt, und die VHD-Datei wird als Datenträger für Daten an die VM angefügt. 

Bevor Sie die neue VHD zum Speichern von Daten nutzen können, müssen Sie den neuen Datenträger initialisieren, partitionieren und formatieren. Die Ausführung dieser Schritte wird in der nächsten Übung beschrieben.

Auf lokalen physischen Servern speichern Sie Daten auf physischen Festplatten. Sie speichern die Daten eines virtuellen Azure-Computers (VM) auf virtuellen Festplatten (VHDs). Diese VHDs werden als Seitenblobs in Azure-Speicherkonten gespeichert. Wenn Sie beispielsweise die Datenbank mit den Fallverläufen für Ihre Anwaltskanzlei zu Azure migrieren, müssen Sie VHDs erstellen, auf denen die Datenbankdateien gespeichert werden können.
