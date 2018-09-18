Wir werden die Faktoren betrachten, die Auswirkungen auf die Datenträgerleistung in Azure haben, und wie Zwischenspeichern die Leistung optimieren kann. 

### <a name="disk-caching"></a>Datenträgerzwischenspeichern

Ein Cache ist eine spezielle Komponente in einem Computer, die Daten speichert, damit schneller darauf zugegriffen werden kann, in der Regel im Arbeitsspeicher. Die Daten in einem Cache wurden häufig zuvor gelesen, oder es sind Daten, die aus einer früheren Berechnung stammen. Das Ziel ist, schneller auf Daten zuzugreifen, als wenn sie vom Datenträger abgerufen würden.

Zum Zwischenspeichern wird spezialisierter und manchmal teurer, temporärer Speicher verwendet, der eine höhere Lese- und/oder Schreibleistung als dauerhafter Speicher aufweist. Da dieser Cachespeicher häufig beschränkt ist, muss entschieden werden, welchen Datenvorgängen das Zwischenspeichern am meisten nutzt. Aber auch wenn der Cache in hohem Maße verfügbar gemacht werden kann wie in Azure, ist es dennoch wichtig, die Workloadmuster der einzelnen Datenträger zu kennen, bevor Sie entscheiden, welcher Cachetyp verwendet werden soll.

**Zwischenspeichern von Lesevorgängen** soll den Datenabruf beschleunigen. Anstatt aus dem dauerhaften Speicher werden die Daten aus dem schnelleren Cache gelesen. Beim Datenlesen wird der Cache unter den folgenden Bedingungen genutzt.

- Die Daten wurden zuvor gelesen und sind im Cache vorhanden.
- Außerdem ist der Cache groß genug, um alle diese Daten aufzunehmen.

Beachten Sie unbedingt, dass das Zwischenspeichern Lesevorgänge unterstützt, wenn eine gewisse _Vorhersagbarkeit_ der Lesewarteschlange gegeben ist, wie z.B. bei einem Satz sequenzieller Lesevorgänge. Bei zufälliger E/A, wo die Daten, auf die Sie zugreifen, über den ganzen Speicher verteilt sind, bietet das Zwischenspeichern wenige oder gar keine Vorteile und kann sogar die Datenträgerleistung reduzieren.

**Zwischenspeichern von Schreibvorgängen** versucht, das Schreiben von Daten in den Speicher zu beschleunigen. Bei Verwendung eines Schreibcaches kann die App die zu speichernden Daten in Betracht ziehen. In der Praxis werden die Daten im Cache in eine Warteschlange eingereiht, um in den permanenten Speicher geschrieben zu werden. Wie Sie sich vorstellen können, kann dieser Mechanismus eine potenzielle Fehlerquelle sein, wenn das System heruntergefahren wird, bevor diese zwischengespeicherten Daten auf den Datenträger geschrieben werden. Einige Systeme, z.B. SQL Server, regeln das Schreiben zwischengespeicherter Daten in den permanenten Datenträgerspeicher selbst.  

### <a name="azure-disk-caching"></a>Azure-Datenträgerzwischenspeichern

Es gibt zwei Arten des Datenträgerzwischenspeicherns, die Datenträgerspeicher betreffen:

- Azure-Datenträgerzwischenspeichern
- Azure-VM-Datenträgerzwischenspeichern

Azure-Datenträgerzwischenspeichern stellt Cachedienste für Azure Blob Storage, Azure Files und andere Inhalte in Azure bereit. Die Konfiguration dieser Arten von Cache ist nicht Gegenstand dieses Moduls.

Azure-VM-Datenträgerzwischenspeichern dient zum Optimieren der Lese- und Schreibzugriffe auf die Dateien der virtuellen Festplatte (Virtual Hard Disk, VHD), die Azure-VMs angefügt sind. Wir konzentrieren uns in diesem Modul auf das Datenträgerzwischenspeichern.

### <a name="azure-virtual-machine-disk-types"></a>Azure-VM-Datenträgertypen

Mit virtuellen Azure-Computern (VMs) werden drei Typen von Datenträgern verwendet.

- **Betriebssystem-Datenträger**: Wenn Sie eine Azure-VM erstellen, fügt Azure automatisch eine virtuelle Festplatte für das Betriebssystem (Operating System, OS) an. Die virtuelle Festplatte wird als Seitenblob im Azure-Speicher gespeichert.
- **Temporärer Datenträger**: Wenn Sie eine Azure-VM erstellen, fügt Azure auch automatisch einen temporären Datenträger hinzu. Dieser Datenträger wird für Daten verwendet, z.B. Auslagerungsdateien. Die Daten auf diesem Datenträger können während der Wartung oder erneuten Bereitstellung eines virtuellen Computers verloren gehen. Verwenden Sie diesen Datenträger nicht zum Speichern dauerhafter Daten, z.B. Datenbankdateien oder Transaktionsprotokolle.
- **Datenträger**: Ein Datenträger ist eine VHD, die zum Speichern von Anwendungsdaten oder anderen Daten, die Sie aufbewahren müssen, an einen virtuellen Computer angebunden ist.

Betriebssystem-Datenträger und Datenträger für Daten nutzen Azure-VM-Datenträgerzwischenspeichern. Die Cachegröße für einen VM-Datenträger hängt von der Größe der VM-Instanz und der Anzahl der Datenträger ab, die auf dem virtuellen Computer bereitgestellt werden. Das Zwischenspeichern kann nur für bis zu vier Datenträger für Daten aktiviert werden.

## <a name="cache-options-for-azure-vms"></a>Cacheoptionen für Azure-VMs

Es gibt drei allgemeine Optionen für das VM-Datenträgerzwischenspeichern.

- **Lese-/Schreibzugriff** – Zurückschreibcache.  Verwenden Sie diese Option nur, wenn Ihre Anwendung das Schreiben von zwischengespeicherten Daten auf persistente Datenträger bei Bedarf ordnungsgemäß verarbeitet.
- **Schreibgeschützt** – Lesevorgänge aus dem Cache werden ausgeführt.
- **Keine** – kein Cache. Wählen Sie diese Option für lesegeschützte und schreibintensive Datenträger. Protokolldateien sind gute Kandidaten, da sie mit schreibintensiven Vorgängen verbunden sind.

Nicht jede Option zum Zwischenspeichern ist für jeden Datenträgertyp verfügbar. Die folgende Tabelle zeigt die Optionen zum Zwischenspeichern für die einzelnen Datenträgertypen:

| |**Schreibgeschützt**  |**Lesen/Schreiben**  |**Keine**  |
|---------|---------|---------|---------|
|Betriebssystem-Datenträger     |   Ja      |   Ja (Standard)     |   Ja      |
|Datenträger     |   Ja (Standard)      |  Ja       |  Ja       |
|Temporärer Datenträger     |  Nein       |   Nein      |   Nein      |

> [!NOTE]
> Datenträgerzwischenspeicher-Optionen können für virtuelle Computer der L- und B-Serie nicht geändert werden.

## <a name="performance-considerations-for-azure-vm-disk-caching"></a>Überlegungen zur Leistung für das Azure-VM-Datenträgerzwischenspeichern

Wie können Ihre Cacheeinstellungen die Leistung Ihrer auf Azure-VMs ausgeführten Workloads beeinträchtigen?

### <a name="os-disk"></a>Betriebssystem-Datenträger

Standardmäßig wird der Cache für einen VM-Betriebssystem-Datenträger im Lese-/Schreibzugriffsmodus verwendet. Wenn Ihre Anwendungen Datendateien auf dem Betriebssystem-Datenträger speichern, und die Anwendungen zahlreiche wahlfreie Lese-/Schreib-Vorgänge in Datendateien ausführen, sollten Sie in Betracht ziehen, diese Dateien auf einen Datenträger für Daten zu verschieben, für den das Zwischenspeichern deaktiviert ist. Warum? Wenn die Lesewarteschlange keine sequenziellen Lesevorgänge enthält, hat das Zwischenspeichern wenig oder keinen Vorteil. Der Mehraufwand für die Verwaltung des Caches, als wären die Daten sequenziell, kann die Datenträgerleistung reduzieren.

### <a name="data-disks"></a>Datenträger für Daten

Für leistungsabhängige Anwendungen sollten Sie Datenträger für Daten statt des Betriebssystem-Datenträgers verwenden. Mithilfe von separaten Datenträgern können Sie die entsprechenden Cacheeinstellungen für jeden Datenträger konfigurieren.

Beispielsweise kann auf Azure-VMs, die SQL Server ausführen, das Aktivieren des **schreibgeschützten** Zwischenspeicherns auf den Datenträgern für Daten (für reguläre und TempDB-Daten) zu erheblichen Leistungsverbesserungen führen. Protokolldateien sind auf der anderen Seite gute Kandidaten für Datenträger für Daten ohne Zwischenspeichern.

> [!WARNING]
> Durch Ändern der Cacheeinstellung eines Azure-Datenträgers wird der Zieldatenträger getrennt und erneut angefügt. Wenn es sich um den Betriebssystemdatenträger handelt, wird der virtuelle Computer neu gestartet. Beenden Sie alle Anwendungen und Dienste, die von dieser Unterbrechung betroffen sein könnten, bevor Sie die Cacheeinstellung des Datenträgers ändern.
>
>