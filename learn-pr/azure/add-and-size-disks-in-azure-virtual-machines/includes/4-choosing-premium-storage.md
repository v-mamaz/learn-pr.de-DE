Für einige Anwendungen gelten höhere Anforderungen an die Datenspeicherung als für andere. Apps wie Dynamics CRM, Exchange Server, SAP Business Suite, SQL Server, Oracle und SharePoint erfordern konstant hohe Leistung und geringe Latenz, um optimal ausgeführt zu werden.

Wenn Sie Ihre virtuellen Computer erstellen oder neue Datenträger hinzufügen, stehen Ihnen einige Optionen zur Auswahl, die dramatische Auswirkungen auf die Datenträgerleistung haben werden, beginnend mit dem _Typ_ des Speichers, den Sie auswählen.

## <a name="types-of-disks"></a>Datenträgertypen 
Azure-Datenträger sind auf eine Verfügbarkeit von 99,999% ausgelegt. 

Es gibt drei Leistungsstufen, zwischen denen Sie beim Erstellen Ihrer Datenträger wählen können: SSD Premium-Datenträger, HDD Standard-Speicher und SSD Standard. Abhängig von der VM-Größe können Sie diese Datenträgertypen mischen und aufeinander abstimmen.

### <a name="premium-ssd-disks"></a>SSD Premium-Datenträger 

SSD Premium-Datenträger basieren auf Festkörperlaufwerken (Solid-State Drives, SSDs) und verfügen über eine hohe Leistung und geringe Latenz für virtuelle Computer mit E/A-intensiven Workloads. Diese Laufwerke sind tendenziell zuverlässiger, da sie keine beweglichen Teile aufweisen. Es muss kein Lese-/Schreibkopf an die richtige Position eines Datenträgers bewegt werden, um auf die angeforderten Daten zuzugreifen. 

Sie können SSD Premium-Datenträger mit VM-Größen verwenden, deren Serienname ein „s“ enthält. Es gibt beispielsweise die **Dv3-Serie** und die **Dsv3-Serie**. Die **Dsv3-Serie** kann mit SSD Premium-Datenträgern verwendet werden.

### <a name="standard-hdd-storage"></a>HDD Standard-Datenträger

HDD Standard-Datenträger werden durch herkömmliche Festplattenlaufwerke (HDDs) unterstützt. Für HDD Standard-Datenträger wird ein niedrigerer Satz als für Premium-Datenträger in Rechnung gestellt. HDD Standard-Datenträger können mit jeder VM-Größe verwendet werden.

### <a name="standard-ssd"></a>SSD Standard

Storage Premium ist auf bestimmte VM-Größen beschränkt, d.h. der VM-Typ, den Sie erstellen, wirkt sich auf die Speicherfunktionen aus: Größe, maximale Kapazität und Speichertyp. Was geschieht, wenn Sie eine Low-End-VM einsetzen, aber Sie für die E/A-Leistung SSD-Speicher benötigen? Hierfür gibt es SSD Standard-Datenträger. SSD Standard-Datenträger liegen unter Leistungs- und Kostenaspekten zwischen HDD Standard und SSD Premium.

Datenträger der Leistungsstufe „SSD Standard“ können mit jeder VM-Größe verwendet werden, einschließlich der VM-Größen, die Storage Premium nicht unterstützen. Die Verwendung von SSD Standard-Datenträgern ist die einzige Möglichkeit, um SSDs mit diesen VMs einzusetzen. Dieser Datenträgertyp ist nur in bestimmten Regionen und nur mit _verwalteten Datenträgern_ verfügbar.

### <a name="unmanaged-vs-managed-disks"></a>Nicht verwaltete Datenträger und verwaltete Datenträger

Wenn Sie VMs oder VHDs erstellen, können Sie zwischen **nicht verwalteten** oder **verwalteten** Datenträgern wählen.

Mit nicht verwalteten Datenträgern sind Sie für die Speicherkonten verantwortlich, die verwendet werden, um die VHDs zu speichern, die den Datenträgern Ihrer VM entsprechen. Sie zahlen die Speicherkontogebühren für die Menge an Speicherplatz, die Sie verwenden. Ein einzelnes Speicherkonto verfügt über ein festes Ratenlimit von 20.000 E/A-Vorgängen pro Sekunde. Dies bedeutet, dass ein einzelnes Speicherkonto 40 virtuelle Standardfestplatten mit voller Auslastung unterstützen kann. Wenn Sie horizontal hochskalieren müssen, benötigen Sie mehrere Speicherkonten. Dies kann kompliziert sein.

Die Verwendung von verwalteten Datenträgern stellt das neuere und **empfohlene Datenträgerspeichermodell** dar. Sie lösen dieses komplexe Problem elegant, indem sie die Last der Verwaltung der Speicherkonten auf Azure übertragen. Sie geben den Datenträgertyp und die Größe des Datenträgers an, und Azure erstellt und verwaltet den Datenträger _und_ den verwendeten Speicher. Sie müssen sich keine Gedanken um die Grenzwerte für Speicherkonten machen. Dies erleichtert deren horizontale Hochskalierung. Einige der Vorteile gegenüber den älteren, nicht verwalteten Datenträgern sind:

- **Höhere Zuverlässigkeit**: Azure stellt sicher, dass VHDs, die VMs mit hoher Zuverlässigkeit zugeordnet sind, in verschiedenen Teilen des Azure-Speichers platziert werden, um ein ähnliches Maß an Ausfallsicherheit zu gewährleisten.
- **Höhere Sicherheit:** Verwaltete Datenträger sind verwaltete Ressourcen in der Ressourcengruppe. Dies bedeutet, dass sie die rollenbasierte Zugriffssteuerung verwenden können, um einzuschränken, wer mit den VHD-Daten arbeiten kann.
- **Unterstützung von Momentaufnahmen**: Momentaufnahmen können verwendet werden, um eine schreibgeschützte Kopie einer VHD zu erstellen. Sie müssen die übergeordnete VM herunterfahren, aber das Erstellen der Momentaufnahme dauert nur wenige Sekunden. Wenn dieser Vorgang abgeschlossen ist, können Sie die VM aktivieren und die Momentaufnahme verwenden, um die VM zu duplizieren, damit Sie die Problembehandlung eines Produktionsproblems ausführen oder ein Rollback der VM zum Zeitpunkt erstellen können, zu dem die Momentaufnahme erstellt wurde.
- **Sicherungsunterstützung**: Verwaltete Datenträger können ohne Auswirkungen auf den Dienst der VM automatisch in verschiedenen Regionen für die Notfallwiederherstellung mit Azure Backup gesichert werden.

Mit allen zusätzlichen Vorteilen einschließlich der garantierten Leistungsmerkmale sollten Sie für neue virtuelle Computer immer verwaltete Datenträger auswählen.

### <a name="disk-comparison"></a>Datenträgervergleich
Die folgende Tabelle ermöglicht einen Vergleich von HDD Standard, SSD Standard und SSD Premium, um Ihnen die Entscheidung zu erleichtern.

|    | Azure-Premium-Datenträger |Azure-SSD Standard-Datenträger (Vorschau)| Azure-HDD Standard-Datenträger 
|--- | ------------------ | ------------------------------- | ----------------------- 
| **Datenträgertyp** | Festkörperlaufwerke (SSD) | Festkörperlaufwerke (SSD) | Festplattenlaufwerke (HDD)  
| **Übersicht**  | SSD-basierte Datenträgerunterstützung mit hoher Leistung und geringer Wartezeit für virtuelle Computer mit E/A-intensiven Workloads oder zum Hosten unternehmenskritischer Produktionsumgebungen |Konsistentere und höhere Zuverlässigkeit als HDD. Für Workloads mit niedrigem IOPS-Wert optimiert| HDD-basierter kosteneffizienter Datenträger für sporadischen Zugriff
| **Szenario**  | Produktionsworkloads und leistungsabhängige Workloads |Webserver, wenig genutzte Unternehmensanwendungen und Dev/Test| Sicherung, nicht kritisch, sporadischer Zugriff 
| **Datenträgergröße** | 32-4.095GiB | 128-4.095GiB | 32-4.095GiB 
| **Max. Durchsatz pro Datenträger** | 250MiB/s | Bis zu 60MiB/s | Bis zu 60MiB/s 
| **Max. IOPS pro Datenträger** | 7.500IOPS | Bis zu 500IOPS | Bis zu 500IOPS 

Weitere Details zur Datenträgerleistung im Folgenden.

## <a name="data-replication"></a>Datenreplikation

Die Daten in Ihrem Microsoft Azure-Speicherkonto werden stets repliziert, um Beständigkeit und Hochverfügbarkeit sicherzustellen. Die Azure Storage-Replikation kopiert Ihre Daten so, dass sie vor geplanten und ungeplanten Ereignissen geschützt sind, z.B. vorübergehend auftretende Hardwarefehler, Netzwerk- oder Stromausfälle, schwere Naturkatastrophen usw. Sie können Ihre Daten wahlweise in demselben Rechenzentrum, in Rechenzentren in derselben Zone und sogar regionsübergreifend replizieren. Es gibt vier Arten der Replikation:

- **Lokal redundanter Speicher (LRS)**: Azure repliziert die Daten in demselben Azure-Rechenzentrum. Die Daten bleiben auch verfügbar, wenn ein Knoten ausfällt. Wenn ein gesamtes Rechenzentrum ausfällt, sind die Daten ggf. nicht mehr verfügbar.
- **Georedundanter Speicher (GRS)**: Azure repliziert Ihre Daten in eine zweite Region, die Hunderte von Kilometern von der primären Region entfernt ist. Wenn für Ihr Speicherkonto GRS aktiviert ist, sind Ihre Daten beständig gespeichert – selbst bei einem regionalen Komplettausfall oder einer Katastrophe, nach der die primäre Region nicht mehr wiederherstellbar ist.
- **Georedundanter Speicher mit Lesezugriff (RA-GRS)**: Azure stellt den schreibgeschützten Zugriff auf die Daten am sekundären Standort und die Georeplikation über zwei Regionen hinweg bereit. Wenn ein Rechenzentrum ausfällt, bleiben die Daten lesbar, können aber nicht geändert werden.
- **Zonenredundanter Speicher (ZRS)**: Azure repliziert Ihre Daten synchron über drei Speichercluster in einer Region. Jeder Speichercluster ist physisch unabhängig von den anderen und befindet sich in einer eigenen Verfügbarkeitszone. Bei dieser Art der Replikation können Sie weiterhin auf Ihre Daten zugreifen und diese verwalten, wenn eine Zone nicht mehr verfügbar ist.

Für Standardspeicherkonten werden alle Replikationstypen unterstützt, aber für Storage Premium-Konten wird nur lokal redundanter Speicher (LRS) unterstützt. Da VMs selbst nur in einer einzelnen Region ausgeführt werden, ist diese Einschränkung normalerweise kein Problem für die VHD-Speicherung.

## <a name="disk-performance"></a>Datenträgerleistung

Die Leistung Ihrer Datenträger hängt vom Datenträgertyp ab, den Sie ausgewählt haben. Jeder Datenträger ist für eine bestimmte Anzahl von E/A-Vorgängen pro Sekunde bzw. IOPS („Ei-Ops“ ausgesprochen) ausgelegt. Darüber hinaus hat jedes Laufwerk eine Durchsatzrate – davon hängt ab, wie viele Daten Sie in einer Sekunde lesen oder schreiben können. Die Kombination beider Größen bestimmt, wie schnell der Datenträger ist.

Bei Verwendung von Standardspeicher erhalten Sie einen maximalen Durchsatz von **500 IOPS und 60MB/Sekunde** pro Datenträger (gilt auch für SSDs). Der IOPS-Wert hängt bei Storage Premium von den ausgewählten Premium-Datenträgern und der VM-Größe ab.

|  | P4 | P6 | P10 | P20 | P30 | P40 | P50 |
|--|----|----|-----|-----|-----|-----|-----|
| **Datenträgergröße** | 32GiB | 64GiB | 128GiB | 512GiB | 1TiB | 2TiB | 4TiB |
| **Max. IOPS pro Datenträger** | 120 | 240 | 500 | 2.300 | 5.000 | 7.500 | 7.500 |
| **Max. Durchsatz pro Datenträger** | 25MB/s | 50 MB/s | 100MB/s | 200MB/s | 250MB/s | 250MB/s |

Wie Sie sehen, reicht das Spektrum von **25MB/s** und **120IOPS** bis zu **250MB/s** und **7.500IOPS**.