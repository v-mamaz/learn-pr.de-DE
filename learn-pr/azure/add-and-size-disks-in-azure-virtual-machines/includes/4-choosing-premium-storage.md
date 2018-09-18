Für einige Anwendungen gelten höhere Anforderungen an die Datenspeicherung als für andere. Beispielsweise benötigen Microsoft Exchange-Server und SharePoint-Server Hochleistungsdatenträger, um bestmöglich ausgeführt zu werden.

Wir kehren noch einmal zum Szenario für die Migration der Datenbank mit den Fallverläufen für Ihre Anwaltskanzlei zu Azure zurück. Sie möchten sicherstellen, dass Ihre Rechtsanwälte und anderen Mitarbeiter so schnell wie möglich auf die Falldetails zugreifen können. Die Kanzlei wächst, und Sie möchten erreichen, dass Sie mit Ihrer Datenbank die steigenden Anforderungen erfüllen können.

Eine Möglichkeit, wie Sie die Leistung der virtuellen Computer (VMs) in Azure maximieren können, ist die Verwendung von Storage Premium für virtuelle Festplatten (VHDs). Storage Premium ermöglicht schnellere Ein- und Ausgaben (E/A) als Standardspeicher. Eine höhere E/A-Geschwindigkeit für Datenträger führt zu einer besseren Leistung für Anwendungen mit hohem Datenträgeraufwand.

Wir vergleichen die Leistungsstufen für Speicher und geben Ihnen weitere Informationen zu Storage Premium-Konten.

## <a name="how-premium-storage-differs-from-standard-storage"></a>Vergleich: Storage Premium und Standardspeicher

In Azure wird Storage Premium auf Solid State Drives (SSDs) implementiert. SSDs verfügen über eine höhere E/A-Leistung als Festplattenlaufwerke (HDDs) und eine höhere Zuverlässigkeit, da sie keine beweglichen Teile haben. Für einen Datenträger muss kein Lese-/Schreibkopf an die richtige Position bewegt werden, um auf die angeforderten Daten zuzugreifen. 

Standardspeicher wird auf HDDs implementiert. Für Standardspeicher wird eine niedrigere Rate berechnet. Wählen Sie Standardspeicher, um die Kosten niedrig zu halten, wenn eine schnelle E/A-Leistung benötigt wird.

Sie können auch eine Mischung aus Standardspeicher und Storage Premium pro Datenträger einer einzelnen VM wählen.

> [!NOTE]
> Bei der Verwendung von verwalteten Datenträgern haben Sie noch eine dritte Option: Standard-SSDs. Standard-SSDs liegen sowohl bei der Leistung als auch beim Preis zwischen Standard-HDDs und Premium-SSDs, sind für nicht verwaltete Datenträger aber nicht verfügbar. Weitere Informationen zu Standard-SSDs finden Sie im weiteren Verlauf dieses Moduls.

## <a name="premium-storage-accounts"></a>Storage Premium-Konten

VHDs werden in allgemeinen Azure-Speicherkonten als Seitenblobs gespeichert. Zur Verwendung von Storage Premium für Ihre VHDs müssen Sie die VHDs in einem **Storage Premium-Konto** speichern. Sie wählen die Leistungsstufe eines Speicherkontos während der Erstellung aus und können diese Einstellung später nicht mehr ändern.

> [!IMPORTANT]
> Storage Premium ist unter Umständen nicht in allen Azure-Regionen verfügbar. Sie können die Verfügbarkeit für Ihre Region unter [Verfügbare Produkte nach Region](https://azure.microsoft.com/en-us/global-infrastructure/services/) überprüfen.

### <a name="data-replication-and-premium-storage-accounts"></a>Datenreplikation und Storage Premium-Konten

Die Daten in Ihrem Microsoft Azure-Speicherkonto werden stets repliziert, um Beständigkeit und Hochverfügbarkeit sicherzustellen. Die Azure Storage-Replikation kopiert Ihre Daten so, dass sie vor geplanten und ungeplanten Ereignissen geschützt sind, z.B. vorübergehend auftretende Hardwarefehler, Netzwerk- oder Stromausfälle, schwere Naturkatastrophen usw. Sie können Ihre Daten wahlweise in demselben Rechenzentrum, in Rechenzentren in derselben Zone und sogar regionsübergreifend replizieren. Es gibt vier Arten der Replikation:

- **Lokal redundanter Speicher (LRS)**: Azure repliziert die Daten in demselben Azure-Rechenzentrum. Die Daten bleiben auch verfügbar, wenn ein Knoten ausfällt. Wenn ein gesamtes Rechenzentrum ausfällt, sind die Daten ggf. nicht mehr verfügbar.
- **Georedundanter Speicher (GRS)**: Azure repliziert Ihre Daten in eine sekundäre Region, die Hunderte von Kilometern von der primären Region entfernt ist. Wenn für Ihr Speicherkonto GRS aktiviert ist, sind Ihre Daten beständig gespeichert – selbst bei einem regionalen Komplettausfall oder einer Katastrophe, nach der die primäre Region nicht mehr wiederherstellbar ist.
- **Georedundanter Speicher mit Lesezugriff (RA-GRS)**: Azure stellt den schreibgeschützten Zugriff auf die Daten am sekundären Standort und die Georeplikation über zwei Regionen hinweg bereit. Wenn ein Rechenzentrum ausfällt, bleiben die Daten lesbar, können aber nicht geändert werden.
- **Zonenredundanter Speicher (ZRS)**: Azure repliziert Ihre Daten synchron über drei Speichercluster in einer Region. Jeder Speichercluster ist physisch unabhängig von den anderen und befindet sich in einer eigenen Verfügbarkeitszone. Bei dieser Art der Replikation können Sie weiterhin auf Ihre Daten zugreifen und diese verwalten, wenn eine Zone nicht mehr verfügbar ist.

Für Standardspeicherkonten werden alle Replikationstypen unterstützt, aber für Storage Premium-Konten wird nur lokal redundanter Speicher (LRS) unterstützt. Da VMs selbst nur in einer einzelnen Region ausgeführt werden, ist diese Einschränkung normalerweise kein Problem für die VHD-Speicherung.

## <a name="migrating-from-standard-storage-to-premium-storage"></a>Migrieren von Standardspeicher zu Storage Premium

Es ist am besten, VHDs gleich mit dem richtigen Typ von Speicherkonto zu erstellen. Manchmal ändern oder erhöhen sich aber ggf. die Anforderungen, oder Sie merken, dass Sie den falschen Typ gewählt haben. In diesen Fällen können Sie eine Umstellung auf Storage Premium erwägen.

Vor Beginn einer Migration sollten Sie sich darüber im Klaren sein, dass es zu Ausfallzeit kommen kann, in der die VM für Benutzer nicht verfügbar ist.

> [!NOTE]
> Ausführliche Details zur Migration von Standardspeicher zu Storage Premium finden Sie unter [Migrieren zu Azure Storage Premium (Nicht verwaltete Datenträger)](https://docs.microsoft.com/azure/storage/common/storage-migration-to-premium-storage).

Wenn Sie eine VM in Azure erstellen, müssen Sie die richtige Balance zwischen Kosten und Leistung finden. Storage Premium ist eine gute Wahl für Anwendungen mit hohem Datenträgeraufwand, z.B. Datenbanken, da eine höhere E/A-Geschwindigkeit als bei Standardspeicher unterstützt wird.
