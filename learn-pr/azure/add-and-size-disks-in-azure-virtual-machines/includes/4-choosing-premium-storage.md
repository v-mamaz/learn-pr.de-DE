Einige Anwendungen setzen größere Ansprüche auf die datenspeicherung als andere. Beispielsweise benötigen in Microsoft Exchange-Server und SharePoint-Servern äußerst leistungsfähige Datenträger optimal ausgeführt.

Sehen wir uns erneut das Szenario die fallverläufen-Datenbank für Ihre Anwaltskanzlei hingegen in Azure zu migrieren. Sie möchten sicherstellen, dass Ihre Rechtsanwälte und andere Mitarbeiter so schnell wie möglich Details zur Anfrage zugreifen können. Das Unternehmen wächst, und Ihrer Datenbank, um höhere Nachfrage behandelt werden sollen.

Eine Möglichkeit, die Sie die Leistung von virtuellen Computern (VMs) in Azure optimal nutzen können, ist zur Verwendung von Storage Premium für virtuelle Festplatten (VHDs). Storage Premium bietet schnellere Eingabe und Ausgabe (e/a) als Standardspeicher. Schnellere Datenträger-e/a führt eine bessere Leistung für Datenträger-Intensive Anwendungen.

Wir vergleichen die Leistungsstufen für den Speicher, und erfahren Sie mehr über Storage Premium-Konten.

## <a name="how-premium-storage-differs-from-standard-storage"></a>Wie unterscheidet sich Premium-Speicher aus dem Standardspeicher

In Azure wird die Premium-Speicher auf SSD-Laufwerken (SSDs) implementiert. SSDs haben höhere e/a-Leistung als Festplattenlaufwerke (HDDs) und zuverlässiger werden können, da sie keine beweglichen Teile aufweisen. Ein Lese- oder Schreibvorgang Head nicht am richtigen Speicherort auf einem Datenträger verschieben, um die angeforderten Daten zu finden. 

Standardspeicher ist für HDDs implementiert. Standardspeicher mit einer niedrigeren Rate abgerechnet. Wählen Sie zur Kontrolle der Kosten Standardspeicher und Storage Premium Wenn schnelle e/a-Leistung erforderlich ist.

Sie können auch eine Kombination aus Standard- und Premium-Speicher pro Datenträger in einem einzelnen virtuellen Computer zu verwenden.

> [!NOTE]
> Wenn Sie verwaltete Datenträger verwenden, Sie haben eine dritte option: standard, SSDs. Standard-SSDs sind sowohl die Leistung als auch die Preis zwischen standard HDDs und Premium SSDs in intermediate sind jedoch nicht verfügbar für nicht verwaltete Datenträger. Erfahren Sie mehr über die standardmäßigen SSDs weiter unten in diesem Modul.

## <a name="premium-storage-accounts"></a>Storage Premium-Konten

VHDs werden als Seitenblobs in allgemeinen Azure-Speicherkonten gespeichert. Um Storage Premium für Ihre VHDs verwenden zu können, müssen Sie virtuelle Festplatten in speichern eine **Storage Premium-Konto**. Wenn Sie ihn erstellen, und Sie können diese Einstellung später nicht ändern, wählen Sie die Leistungsstufe für ein Speicherkonto.

> [!IMPORTANT]
> Storage Premium ist in allen Azure-Regionen möglicherweise nicht zur Verfügung. Um die Verfügbarkeit in Ihrer Region überprüfen zu können, finden Sie unter [verfügbare Produkte nach Region](https://azure.microsoft.com/en-us/global-infrastructure/services/).

### <a name="data-replication-and-premium-storage-accounts"></a>Daten, Replikation und Premium-Speicherkonten

Die Daten in Ihrem Microsoft Azure-Speicherkonto werden stets repliziert, um Beständigkeit und Hochverfügbarkeit sicherzustellen. Azure Storage-Replikation-Kopien, die Ihre Daten, damit er von geschützt ist geplant und ungeplanten Ereignissen wie vorübergehenden Hardwareausfällen kommt, Netzwerk oder Stromausfälle, schweren Naturkatastrophen und So weiter. Sie können Ihre Daten wahlweise im selben Rechenzentrum, Rechenzentren in derselben Zone und sogar Regionen übergreifend replizieren. Es gibt vier Arten der Replikation:

- **Lokal redundanter Speicher (LRS)** -repliziert Azure die Daten in der gleichen Azure-Rechenzentrum. Die Daten bleiben verfügbar, wenn ein Knoten ausfällt. Wenn ein gesamtes Rechenzentrum ausfällt, können Daten jedoch nicht verfügbar sein.
- **Georedundanter Speicher (GRS)** -Azure repliziert Ihre Daten in eine sekundäre Region, die Hunderte von Meilen von der primären Region ist. Wenn Ihr Speicherkonto GRS aktiviert ist, sind Ihre Daten dauerhaft, selbst wenn einem regionalen Komplettausfall oder einem Notfall, in dem die primäre Region wiederhergestellt wird, nicht, vorhanden ist.
- **Read-Access Geo-redundant Storage (RA-GRS)** – Azure bietet schreibgeschützten Zugriff auf die Daten in den sekundären Standort und Geo-Replikation zwischen zwei Regionen. Wenn ein Rechenzentrum ausfällt, werden die Daten lesbar bleibt jedoch nicht geändert werden.
- **Zonenredundanter Speicher (ZRS)** -Azure repliziert Ihre Daten synchron in drei speichercluster in einer einzelnen Region. Jeder Speichercluster ist physisch unabhängig von den anderen und befindet sich in einer eigenen Verfügbarkeitszone. Mit dieser Art von Replikation können Sie weiterhin zugreifen und verwalten Sie Ihre Daten, die eine Zone nicht verfügbar ist.

Standard-Speicherkonten unterstützt, für alle Replikationstypen dagegen Storage Premium-Konten unterstützen nur lokal redundanten Speicher (LRS). Da virtuelle Computer selbst in einer einzelnen Region ausgeführt wird ist diese Beschränkung normalerweise kein Problem für VHD-Speicher.

## <a name="migrating-from-standard-storage-to-premium-storage"></a>Migrieren aus dem Standardspeicher zu Storage premium

Es wird empfohlen, zum Erstellen von VHDs in den richtigen Typ des Speicherkontos, das in erster Linie. Jedoch manchmal Anforderungen ändern, Anforderungen steigen, oder Sie feststellen, dass Sie den falschen Typ ausgewählt haben. Erwägen Sie einen Wechsel zu Storage Premium in diesen Situationen.

Beachten Sie, dass es eine Ausfallzeit umfasst, die der virtuellen Computer nicht für Benutzer verfügbar sein soll, bevor Sie mit einer Migration beginnen.

> [!NOTE]
> Ausführliche Informationen von der Migration von Standard zu Storage Premium finden Sie unter [Migrieren zu Azure Storage Premium (nicht verwaltete Datenträger)](https://docs.microsoft.com/azure/storage/common/storage-migration-to-premium-storage).

Wenn Sie einen virtuellen Computer in Azure erstellen, müssen Sie das richtige Gleichgewicht zwischen Kosten und Leistung zu finden. Storage Premium ist eine gute Wahl für Datenträger-Intensive Anwendungen wie Datenbanken, da es ein schnelleres e/a als Standardspeicher unterstützt.
