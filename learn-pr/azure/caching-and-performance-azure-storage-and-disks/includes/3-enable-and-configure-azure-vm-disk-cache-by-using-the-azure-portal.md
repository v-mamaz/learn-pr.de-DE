Wir haben Einstellungen und Eigenschaften kennengelernt, die Sie auswählen können, um die Leistung des Datenträgers vorherzusagen. Nun schauen wir uns Möglichkeiten an, diese durch _Zwischenspeichern_ zu verbessern.

## <a name="disk-caching"></a>Datenträgerzwischenspeicherung

Ein Cache ist eine spezielle Komponente, in der Regel im Arbeitsspeicher, die Daten speichert, damit schneller darauf zugegriffen werden kann. Die Daten in einem Cache sind oft Daten, die zuvor gelesen wurden oder aus einer früheren Berechnung resultieren. Ziel ist, schneller auf Daten zuzugreifen, als wenn sie vom Datenträger abgerufen würden.

Zum Zwischenspeichern wird spezialisierter und manchmal teurer, temporärer Speicher verwendet, der eine höhere Lese- und Schreibleistung als dauerhafter Speicher aufweist. Da dieser Cachespeicher häufig begrenzt ist, muss entschieden werden, welchen Datenvorgängen das Zwischenspeichern am meisten nutzt. Aber auch wenn der Cache in hohem Maße verfügbar gemacht werden kann wie in Azure, ist es dennoch wichtig, die Workloadmuster der einzelnen Datenträger zu kennen, bevor Sie entscheiden, welcher Cachetyp verwendet werden soll.

Das **Zwischenspeichern von Lesevorgängen** soll den _Abruf_ von Daten beschleunigen. Anstatt aus dem dauerhaften Speicher werden die Daten aus dem schnelleren Cache gelesen. Beim Lesen von Daten wird der Cache unter den folgenden Bedingungen genutzt:

- Die Daten wurden zuvor gelesen und sind im Cache vorhanden.
- Außerdem ist der Cache groß genug, um alle diese Daten aufzunehmen.

Beachten Sie unbedingt, dass das Zwischenspeichern von Lesevorgängen hilfreich ist, wenn eine gewisse _Vorhersagbarkeit_ der Lesewarteschlange gegeben ist, wie z.B. bei einem Satz sequenzieller Lesevorgänge. Bei zufälligen E/A-Vorgängen, bei denen die Daten, auf die Sie zugreifen, über den ganzen Speicher verteilt sind, bietet das Zwischenspeichern wenige oder gar keine Vorteile und kann sogar die Datenträgerleistung reduzieren.

Durch **Zwischenspeichern von Schreibvorgängen** wird versucht, das _Schreiben von Daten_ in den dauerhaften Speicher zu beschleunigen. Bei Verwendung eines Schreibcaches kann die App die zu speichernden Daten in Betracht ziehen. In der Praxis werden die Daten im Cache in eine Warteschlange eingereiht, um auf Datenträger geschrieben zu werden. Wie Sie sich vorstellen können, kann dieser Mechanismus eine potenzielle Fehlerquelle sein, wenn das System heruntergefahren wird, bevor diese zwischengespeicherten Daten geschrieben werden. Einige Systeme, z.B. SQL Server, regeln das Schreiben zwischengespeicherter Daten in den permanenten Datenträgerspeicher selbst.

### <a name="azure-disk-caching"></a>Azure-Datenträgerzwischenspeichern

Es gibt zwei Arten des Datenträgerzwischenspeicherns, die Datenträgerspeicher betreffen:

- Azure-Datenträgerzwischenspeicherung
- Azure-VM-Datenträgerzwischenspeicherung

Die Azure Storage-Zwischenspeicherung stellt Cachedienste für Azure Blob Storage, Azure Files und andere Inhalte in Azure bereit. Die Konfiguration dieser Arten von Cache ist nicht Gegenstand dieses Moduls.

Azure-VM-Datenträgerzwischenspeichern dient zum Optimieren der Lese- und Schreibzugriffe auf die Dateien der virtuellen Festplatte (Virtual Hard Disk, VHD), die Azure-VMs angefügt sind. Wir konzentrieren uns in diesem Modul auf das Datenträgerzwischenspeichern.

### <a name="azure-virtual-machine-disk-types"></a>Azure-VM-Datenträgertypen

Mit Azure-VMs werden drei Typen von Datenträgern verwendet:

- **Betriebssystem-Datenträger**: Wenn Sie eine Azure-VM erstellen, fügt Azure automatisch eine virtuelle Festplatte (VHD) für das Betriebssystem an.

- **Temporärer Datenträger**: Wenn Sie eine Azure-VM erstellen, fügt Azure auch automatisch einen temporären Datenträger hinzu. Dieser Datenträger wird für Daten verwendet, z.B. Auslagerungsdateien. Die Daten auf diesem Datenträger können während der Wartung oder erneuten Bereitstellung eines virtuellen Computers verloren gehen. Verwenden Sie diesen Datenträger nicht zum Speichern dauerhafter Daten, z.B. Datenbankdateien oder Transaktionsprotokolle.

- **Datenträger für Daten**: Ein Datenträger für Daten ist eine VHD, die zum Speichern von Anwendungsdaten oder anderen Daten, die Sie aufbewahren müssen, an einen virtuellen Computer angefügt ist.

Betriebssystem-Datenträger und Datenträger für Daten nutzen die Azure-VM-Datenträgerzwischenspeicherung. Die Cachegröße für einen VM-Datenträger hängt von der Größe der VM-Instanz und der Anzahl der Datenträger ab, die auf dem virtuellen Computer bereitgestellt werden. Das Zwischenspeichern kann nur für bis zu vier Datenträger für Daten aktiviert werden.

## <a name="cache-options-for-azure-vms"></a>Cacheoptionen für Azure-VMs

Es gibt drei allgemeine Optionen für die VM-Datenträgerzwischenspeicherung:

- **Lese-/Schreibzugriff**: Zurückschreibcache. Verwenden Sie diese Option nur, wenn Ihre Anwendung das Schreiben zwischengespeicherter Daten auf dauerhafte Datenträger bei Bedarf ordnungsgemäß ausführt.
- **Schreibgeschützt**: Lesevorgänge werden aus dem Cache ausgeführt.
- **Kein**: Kein Cache. Wählen Sie diese Option für lesegeschützte und schreibintensive Datenträger. Protokolldateien sind gut geeignet, da sie mit schreibintensiven Vorgängen verbunden sind.

Nicht jede Option zum Zwischenspeichern ist für jeden Datenträgertyp verfügbar. Die folgende Tabelle zeigt die Optionen zum Zwischenspeichern für die einzelnen Datenträgertypen:

|               | **Schreibgeschützt**  | **Lesen/Schreiben** | **Keine** |
|---------------|----------------|----------------|----------|
| Betriebssystem-Datenträger       | Ja            | Ja (Standard)  | Ja      |
| Datenträger     | Ja (Standard)  | Ja            | Ja      |
| Temporärer Datenträger     | Nein             | Nein             | Nein       |

> [!NOTE]
> Optionen für die Datenträgerzwischenspeicherung können für virtuelle Computer der **L-** und **B-Serie** nicht geändert werden.

## <a name="performance-considerations-for-azure-vm-disk-caching"></a>Überlegungen zur Leistung der Azure-VM-Datenträgerzwischenspeicherung

Wie können Ihre Cacheeinstellungen die Leistung Ihrer auf Azure-VMs ausgeführten Workloads beeinträchtigen?

### <a name="os-disk"></a>Betriebssystem-Datenträger

Standardmäßig wird der Cache für einen VM-Betriebssystem-Datenträger im Lese-/Schreibzugriffsmodus verwendet. Wenn Ihre Anwendungen Datendateien auf dem Betriebssystem-Datenträger speichern und die Apps zahlreiche zufällige Lese-/Schreib-Vorgänge in Datendateien ausführen, sollten Sie in Betracht ziehen, diese Dateien auf einen Datenträger für Daten zu verschieben, für den das Zwischenspeichern deaktiviert ist. Warum? Wenn die Lesewarteschlange keine sequenziellen Lesevorgänge enthält, hat das Zwischenspeichern wenig oder keinen Nutzen. Der Mehraufwand für die Verwaltung des Caches, als wären die Daten sequenziell, kann die Datenträgerleistung reduzieren.

### <a name="data-disks"></a>Datenträger für Daten

Für leistungsabhängige Anwendungen sollten Sie Datenträger für Daten anstelle des Betriebssystem-Datenträgers verwenden. Mithilfe von separaten Datenträgern können Sie die entsprechenden Cacheeinstellungen für jeden Datenträger konfigurieren.

Beispielsweise kann auf Azure-VMs, die SQL Server ausführen, das Aktivieren des **schreibgeschützten** Zwischenspeicherns auf den Datenträgern für Daten (für reguläre und TempDB-Daten) zu erheblichen Leistungsverbesserungen führen. Protokolldateien sind auf der anderen Seite gute Kandidaten für Datenträger für Daten ohne Zwischenspeichern.

> [!WARNING]
> Durch Ändern der Cacheeinstellung eines Azure-Datenträgers wird der Zieldatenträger getrennt und erneut angefügt. Wenn es sich um den Betriebssystem-Datenträger handelt, wird der virtuelle Computer neu gestartet. Beenden Sie alle Anwendungen und Dienste, die von dieser Unterbrechung betroffen sein könnten, bevor Sie die Cacheeinstellung des Datenträgers ändern.

Sie können die Cacheeinstellungen für virtuelle Computer mit einem der folgenden Tools konfigurieren:

- Azure-Portal
- Azure CLI
- Azure PowerShell
- Resource Manager-Vorlagen

## <a name="using-the-azure-portal-to-configure-caching"></a>Konfigurieren der Zwischenspeicherung im Azure-Portal

Wenn Sie einen neuen virtuellen Computer über das Azure-Portal bereitstellen, können Sie die standardmäßige Zwischenspeicherkonfiguration für den Betriebssystem-Datenträger vom Lese-/Schreibzugriff nicht ändern, bis der virtuelle Computer bereitgestellt wird.

Wenn Sie einem vorhandenen virtuellen Computer einen Datenträger für Daten hinzufügen, können Sie die Cacheoption konfigurieren, bevor der Datenträger für den virtuellen Computer bereitgestellt wird.

Durch Ändern der Cacheeinstellung eines Azure-Datenträgers wird der Zieldatenträger getrennt und erneut angefügt. Wenn es sich um den Betriebssystemdatenträger handelt, wird der virtuelle Computer neu gestartet. Beenden Sie alle Anwendungen und Dienste, die von dieser Unterbrechung betroffen sein könnten, bevor Sie die Cacheeinstellung des Datenträgers ändern.

Wir erstellen einen virtuellen Computer und ändern die Cacheeinstellungen über das Azure-Portal.
