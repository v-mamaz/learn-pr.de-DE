Virtuelle Computer in Azure verwenden wie alle anderen Computer auch einen Datenträger, auf dem das Betriebssystem, Anwendungen und Daten gespeichert sind. Diese Datenträger werden als virtuellen Festplatten (VHDs) bezeichnet.

Nehmen wir an, dass Sie einen virtuellen Computer (VM) erstellt haben, in dem die Datenbank des fallverläufen gehostet werden, denen Ihre Anwaltskanzlei verwendet Azure. Eine gut entworfene Datenträgerkonfiguration ist elementar für eine gute Leistung und Stabilität für SQL Server.

In dieser Einheit erfahren Sie, wie Sie die richtigen Konfigurationswerte für Ihre Datenträger auswählen und diese Datenträger an einen virtuellen Computer anfügen.

## <a name="how-disks-are-used-by-vms"></a>Wie Datenträger von virtuellen Computern verwendet werden.

VMs werden Datenträger für drei verschiedene Zwecke verwenden:

- **Betriebssystemspeicher**. Jeder virtuelle Computer enthält einen Datenträger, die das Betriebssystem speichert. Dieses Laufwerk ist als SATA-Laufwerk registriert und mit der Bezeichnung Laufwerk in Windows und bereitgestellt werden, unter "/" in Unix-ähnlichen Betriebssystemen. Es hat eine maximale Kapazität von 2048 Gigabyte (GB), und dessen Inhalt stammt aus dem VM-Image, die, das Sie zum Erstellen des virtuellen Computers verwendet.
- **Temporäre Speicherung**. Jeder virtuelle Computer enthält eine temporäre virtuelle Festplatte, die für Auslagerungsdateien verwendet wird. Daten auf diesem Laufwerk möglicherweise während einer Wartung oder erneute Bereitstellung verloren. Das Laufwerk ist standardmäßig als "d:" auf einer Windows-VM bezeichnet. Verwenden Sie dieses Laufwerk nicht, um wichtige Daten speichern, die Sie nicht verlieren möchten.
- **Datenspeicher**. Ein Datenträger ist eine beliebige andere Datenträger an eine VM angefügt. Sie verwenden Datenträger zum Speichern von Dateien, Datenbanken und alle anderen Daten, die Sie bei Neustarts beibehalten müssen. Einige VM-Images werden standardmäßig Datenträger für Daten enthalten. Sie können auch eigene Datenträger für Daten bis zur maximalen Anzahl, angegeben durch die Größe des virtuellen Computers hinzufügen. Jeder Datenträger als SCSI-Laufwerk registriert und hat eine maximale Kapazität von 4095 GB. Wählen Sie Laufwerkbuchstaben oder Bereitstellungspunkte für Ihre Datenträger für Daten.

## <a name="storing-vhd-files"></a>Das Speichern von VHD-Dateien

In Azure-VHDs werden gespeichert, in Azure Storage-Konto als **Seitenblobs**.

Die folgende Tabelle enthält die verschiedenen Arten von Speicherkonten sowie die Objekte, die jeweils mit den Konten verwendet werden können.

|**Speicherkontotyp**|**Standard (Allgemein)**|**Premium (Allgemein)**|**Blobspeicher, Zugriffsebenen „Heiß“ und „Kalt“**|
|-----|-----|-----|-----|
|**Unterstützte Dienste**| Azure Blob Storage, Azure Files, Azure Queue storage | Blob-Speicher | Blob-Speicher|
|**Unterstützte Blobtypen**|Blockblobs, Seitenblobs und Anfügeblobs | Seitenblobs | Blockblobs und Anfügeblobs|

Beide Seiten-Blobs allgemeinen Standard- und Storage Premium-Support. Wählen Sie ein standardmäßiges Speicherkonto aus, wenn die Kosten auf Ihr primäres Ziel ist. Storage Premium ist teurer, aber es liefert auch viel höheren e/a-Vorgänge/Sekunde (IOPS). Wenn Data-Leistung für Ihren virtuellen Computer erforderlich ist, bevorzugen Sie Storage Premium.

## <a name="attach-data-disks-to-vms"></a>Anfügen von Datenträgern an virtuelle Computer

Sie können Datenträger an einen virtuellen Computer zu einem beliebigen Zeitpunkt hinzufügen, von dem virtuellen Computer anfügen. Anfügen eines Datenträgers wird die VHD-Datei mit dem virtuellen Computer verknüpft. 

Die virtuelle Festplatte kann nicht aus dem Speicher gelöscht werden, solange sie angefügt ist.

### <a name="attach-an-existing-data-disk-to-an-azure-vm"></a>Fügen Sie einen vorhandenen Datenträger an eine Azure-VM

Möglicherweise verfügen Sie bereits über eine virtuelle Festplatte, die Daten speichert, die Sie in Ihrer Azure-VM verwenden möchten. In diesem Szenario recht gute haben z. B. möglicherweise Sie bereits physischen Datenträger in virtuelle Festplatten lokal konvertiert. In diesem Fall können Sie die PowerShell `Add-AzureRmVhd` Cmdlet, um ihn in das Speicherkonto hochzuladen. Dieses Cmdlet ist optimiert für die Übertragung von VHD-Dateien und möglicherweise schneller als die anderen Methoden den Upload abgeschlossen. Die Übertragung abgeschlossen ist, indem mithilfe mehrerer Threads für eine optimale Leistung. Sobald die VHD hochgeladen wurde, fügen Sie sie als Datenträger für Daten einem vorhandenen virtuellen Computer. Dieser Ansatz eine hervorragende Möglichkeit, die Daten aller Typen auf virtuellen Azure-Computern bereitstellen. Die Daten automatisch auf dem virtuellen Computer vorhanden sind, und besteht keine Notwendigkeit zum Partitionieren oder den neuen Datenträger formatieren.

### <a name="attach-a-new-data-disk-to-an-azure-vm"></a>Fügen Sie einen neuen Datenträger an eine Azure-VM

Sie können im Azure-Portal verwenden, um einen neuen, leeren Datenträger an einen virtuellen Computer hinzufügen. 

Dieser Vorgang erstellt eine **VHD** Datei als Seiten-Blob im Speicherkonto, dass Sie angeben, und die VHD-Datei als Datenträger für Daten mit dem virtuellen Computer anfügen.

Bevor Sie die neue virtuelle Festplatte zum Speichern von Daten verwenden können, müssen Sie initialisieren, Partition und formatieren den neuen Datenträger ein. Wir werden diese Schritte in der nächsten Übung üben.

In lokalen physischen Servern speichern Sie Daten auf physische Festplatten. Sie können Daten auf einer Azure-VM (VM) auf virtuellen Festplatten (VHDs) speichern. Diese VHDs werden als Seitenblobs in Azure Storage-Konten gespeichert. Z. B. Wenn Sie Ihre Anwaltskanzlei Datenbank fallverläufen in Azure migrieren, müssen Sie VHDs erstellen, in dem die Datenbankdateien gespeichert wird.
