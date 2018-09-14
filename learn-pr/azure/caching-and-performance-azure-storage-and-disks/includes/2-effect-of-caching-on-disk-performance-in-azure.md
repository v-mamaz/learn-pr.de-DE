Wir werden die Faktoren betrachten, die Auswirkungen auf die datenträgerleistung in Azure und wie caching kann die Leistung optimieren.

### <a name="disk-caching"></a>Nutzung des Datenträgercaches

Ein Cache ist eine spezielle Komponente auf einem Computer, der Daten speichert, sodass es schneller, zugegriffen werden kann in der Regel im Arbeitsspeicher. Die Daten in einem Cache ist häufig die Daten, die zuvor gelesen wurde, oder Daten, die aus einer früheren Berechnungen resultieren. Das Ziel ist, auf Daten zugreifen, schneller, als es vom Datenträger abrufen.

Spezialisierte Zwischenspeicherung verwendet, und manchmal teuer, temporären Speicher, die muss schneller lesen und/oder Schreiben Sie die Leistung als dauerhaften Speicher. Da dieser Cachespeicher häufig beschränkt ist, müssen Entscheidungen vorgenommen werden, was Datenvorgänge am meisten vom caching profitieren. Aber auch, in dem der Cache häufig verfügbar gemacht werden kann wie in Azure, es ist jedoch wichtig die arbeitsauslastungsmuster aufgeführt, für die einzelnen Datenträger zu wissen, bevor Sie entscheiden, auf welche Cachetyp verwenden.

**Zwischenspeichern von Lesevorgängen** versucht, um den Datenabruf zu beschleunigen. Anstatt beim Lesen aus dem dauerhaften Speicher, werden die Daten aus dem Cache schneller gelesen. Daten Cachetreffer der in den folgenden Situationen:

- Die Daten vor der gelesen wurde und im Cache vorhanden ist.
- Und der Cache ist groß genug für alle diese Daten.

Es ist wichtig zu beachten, dass die Zwischenspeicherung für Lesevorgänge unterstützt, bei einigen _Vorhersagbarkeit_ an die lesen Warteschlange, wie z. B. einen Satz von sequenziellen Lesevorgängen. Für zufällige e/a, in denen die Daten, die Sie zugreifen Speicher verteilt ist, caching werden wenig oder keinen Vorteil, und kann sogar in datenträgerleistung.

**Schreibcache** versucht, das Schreiben von Daten in den Speicher zu beschleunigen. Verwenden Sie einen Schreibcache, kann die app die Daten gespeichert werden, in Betracht ziehen. In der Praxis die Daten in einem Cache, in die Warteschlange darauf warten, in einen permanenten Speicher geschrieben werden. Wie Sie sich vorstellen können, dieser Mechanismus kann eine potenzielle Fehlerquelle sein, z. B. wenn das System wird nach unten, bevor diese Daten zwischengespeichert wird geleert, auf dem Datenträger. Einige Systeme, z. B. SQL Server, behandeln das Schreiben von zwischengespeicherten Daten in der permanente Datenträgerspeicher selbst.

### <a name="azure-disk-caching"></a>Azure-Datenträger Zwischenspeichern

Es gibt zwei Arten von Datenträgercache, Datenträgerspeicher relevant:

- Zwischenspeichern von Azure-Speicher
- Zwischenspeicherung von Datenträgern in virtuellen Azure-Computer (VM)

Zwischenspeichern von Azure-Speicher stellt Cachedienste für Azure Blob Storage, Azure Files und andere Inhalte in Azure bereit. Die Konfiguration dieser Art von Cache ist nicht Gegenstand dieses Moduls.

Zwischenspeicherung von Datenträgern in virtuellen Azure-Computer wird zum Optimieren der Lese- und Schreibzugriff auf die virtuelle Festplatte (VHD)-Dateien, die Azure-VMs angefügt. Konzentrieren wir uns auf die Zwischenspeicherung von Datenträgern in diesem Modul.

### <a name="azure-virtual-machine-disk-types"></a>Azure-VM-Datenträgertypen

Es gibt drei Arten von Datenträgern mit Azure-VMs verwendet:

- **Betriebssystem-Datenträger**: Wenn Sie eine Azure-VM erstellen, fügt Azure automatisch eine virtuelle Festplatte für das Betriebssystem (OS). Die virtuelle Festplatte wird als Seitenblob im Azure-Speicher gespeichert.
- **Temporärer Datenträger**: Wenn Sie eine Azure-VM erstellen, fügt Azure auch automatisch einen temporären Datenträger. Dieser Datenträger wird für Daten, z. B. Auslagerungsdateien verwendet. Die Daten auf diesem Datenträger können während der Wartung oder einen virtuellen Computer erneut bereitstellen verloren. Daher verwenden sie nicht zum Speichern von dauerhaften Daten, z. B. die Datenbank- oder Transaktionsprotokoll.
- **Datenträger für Daten**: ein Datenträger ist eine VHD, die an einen virtuellen Computer zum Speichern von Anwendungsdaten oder anderen Daten, die Sie aufbewahren müssen angefügt ist.

Betriebssystem-Datenträger und Datenträger für Daten nutzen Azure-VM-datenträgerzwischenspeicherung. Die Cachegröße für ein VM-Datenträger hängt von der Größe der VM-Instanz und auf der Anzahl der Datenträger, die auf dem virtuellen Computer bereitgestellt. Caching kann nur bis zu vier Datenträger aktiviert werden.

## <a name="cache-options-for-azure-vms"></a>Cacheoptionen für Azure-VMs

Es gibt drei allgemeine Optionen für die Zwischenspeicherung von VM-Datenträgern:

- **Lese-/Schreibzugriff** – zurückschreibcaches. Verwenden Sie diese Option nur, wenn Ihre Anwendung ordnungsgemäß das Schreiben von zwischengespeicherten Daten auf beständige Datenträger verarbeitet bei Bedarf.
- **Nur-Lese** -Lesevorgänge aus dem Cache ausgeführt werden.
- **Keine** -kein Cache. Wählen Sie diese Option für nur-schreiben und mit vielen Schreibvorgängen Datenträger. Protokolldateien sind ein guter Kandidat, weil sie Schreibintensive Vorgänge sind.

Nicht jede Option zum Zwischenspeichern ist für jeden Typ des Datenträgers verfügbar. Die folgende Tabelle zeigt Sie die Optionen für die Zwischenspeicherung für die einzelnen Datenträger:

| |**Read-only**  |**Lese-/Schreibzugriff**  |**Keine**  |
|---------|---------|---------|---------|
|Betriebssystem-Datenträger     |   Ja      |   Ja (Standard)     |   Ja      |
|Datenträger     |   Ja (Standard)      |  Ja       |  Ja       |
|Temporärer Datenträger     |  no       |   no      |   no      |

> [!NOTE]
> Datenträger-cachingoptionen kann nicht für die L-Serie und der virtuelle Computer der B-Serie nicht geändert werden.

## <a name="performance-considerations-for-azure-vm-disk-caching"></a>Überlegungen zur Leistung für Azure-VM-Datenträgerspeicher

Also, wie können die cacheeinstellungen beeinträchtigt die Leistung Ihrer Workloads auf Azure Virtual Machines?

### <a name="os-disk"></a>Betriebssystem-Datenträger

Standardmäßig werden für eine VM-Betriebssystem-Datenträger den Cache im Modus mit Lese-/Schreibzugriff zu verwenden. Wenn Sie Anwendungen, die Datendateien auf dem Betriebssystem-Datenträger zu speichern, und der Anwendungen zahlreiche wahlfreie Lese-/Schreib-Vorgänge für Datendateien bieten, sollten Sie übertragen dieser Dateien auf einen Datenträger, die die Zwischenspeicherung deaktiviert. Warum? Wenn die Lese Warteschlange sequenzielle Lesevorgänge keine enthält, Zwischenspeichern von wenigen oder gar keinen Vorteil werden. Der Mehraufwand für den Cache, als wäre die Daten sequenziell, kann die datenträgerleistung reduzieren.

### <a name="data-disks"></a>Datenträger

Bei leistungsabhängigen Anwendungen sollten Sie den Datenträger anstatt auf Betriebssystem-Datenträger verwenden. Mithilfe von separaten Datenträgern können Sie so konfigurieren Sie die Einstellungen für den entsprechenden Cache für jeden Datenträger.

Beispielsweise Ausführen von SQL Server auf Azure-VMs, sodass **schreibgeschützte** Zwischenspeicherung auf Datenträger (für den regulären und TempDB-Daten) kann dazu führen, erhebliche Leistungssteigerungen. Protokolldateien werden auf der anderen Seite für die Datenträger für Daten ohne Zwischenspeicherung geeignet.

> [!WARNING]
> Durch Ändern der cacheeinstellung eines Azure-Datenträgers wird getrennt, und klicken Sie dann erneut angefügt wird der Zieldatenträger. Wenn es sich um die Betriebssystem-Datenträger handelt, wird der virtuelle Computer neu gestartet. Beenden Sie alle Anwendungen und Dienste, die von dieser Unterbrechung betroffen sein könnten, bevor Sie die Cacheeinstellung des Datenträgers ändern.
