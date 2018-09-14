Wir verfügen über eine Website, die auf einem lokalen Ubuntu Linux-Server ausgeführt wird. Unser Ziel ist es zum Erstellen eines Azure virtuellen Computers (VM), das mit dem neuesten Ubuntu-Image, und klicken Sie dann den Standort in die Cloud migrieren. In dieser Einheit erfahren Sie zu den Optionen, die Sie benötigen, um auszuwerten, wenn Sie einen virtuellen Computer in Azure zu erstellen.

## <a name="introduction-to-azure-virtual-machines"></a>Einführung in virtuelle Azure-Computer

Azure Virtual Machines eignet es sich um eine bedarfsgesteuerte, skalierbare Cloud computing-Ressource. Sie enthalten, Prozessoren, Arbeitsspeicher, Speicher und Netzwerkressourcen. Sie können starten und Beenden von virtuellen Computern auf und Verwalten von Azure-Portal oder mit der Azure CLI. Sie können auch einen Remoteserver Secure Shell (SSH) direkt mit dem ausgeführten virtuellen Computer verbinden, und führen Befehle aus, als wären Sie auf einem lokalen Computer.

### <a name="running-linux-in-azure"></a>Ausführen von Linux in Azure

Das Erstellen von auf Linux basierenden VMs in Azure ist einfach. Microsoft arbeitet mit herausragenden Linux-Anbietern zusammen, um sicherzustellen, dass deren Distributionen für die Azure-Plattform optimiert sind. Sie können Erstellen virtueller Computer aus vorgefertigten Images für eine Vielzahl von beliebten Linux-Distributionen wie Ubuntu, SUSE und Red Hat oder erstellen Ihre eigenen Linux-Distribution, in der Cloud auszuführen.

## <a name="creating-an-azure-vm"></a>Erstellen einer Azure-VM

Virtuelle Computer definiert und auf verschiedene Weise in Azure bereitgestellt werden können: das Azure-Portal, ein Skript (mit dem Azure-Befehlszeilenschnittstelle oder Azure PowerShell) oder einer Azure Resource Manager-Vorlage. In allen Fällen müssen Sie verschiedene Arten von Informationen bereitstellen, die wir bald eingehe.

Azure Marketplace enthält auch vorkonfigurierte Images, die ein Betriebssystem und bevorzugten Softwaretools, die für bestimmte Szenarien installiert enthalten.

![Screenshot des Azure-Portal mit mehreren VM-Optionen im Azure Marketplace.](../media/2-marketplace-vm-choices.png)

## <a name="resources-used-in-a-linux-vm"></a>Auf einer Linux-VM verwendete Ressourcen

Wenn Sie eine Linux-VM in Azure erstellen, erstellen Sie gleichzeitig auch Ressourcen, um diese zu hosten. Diese Ressourcen arbeiten zusammen, um einen virtuellen Computer zu erstellen und das Linux-Betriebssystem auszuführen. Diese müssen vorhanden sein (und bei der Erstellung des virtuellen Computers ausgewählt werden) oder mit dem virtuellen Computer erstellt werden:

- Ein virtueller Computer, der CPU und Speicherressourcen bereitstellt.
- Ein Azure Storage-Konto, in dem die virtuellen Festplatten gespeichert werden.
- Virtuelle Datenträger, auf denen das Betriebssystem, die Anwendungen und Daten gespeichert werden.
- Ein virtuelles Netzwerk (VNET), über das der virtuelle Computer mit anderen Azure-Diensten oder Ihrer lokalen Hardware verbunden wird.
- Eine Netzwerkschnittstelle für die Kommunikation mit dem VNET.
- Eine optionale öffentliche IP-Adresse, damit Sie auf den virtuellen Computer zugreifen können.

Wie bei anderen Azure-Diensten auch benötigen Sie eine **Ressourcengruppe**, in der der virtuelle Computer gespeichert wird. Sie sollten diese Ressourcen zu Verwaltungszwecken optional in einer Gruppe zusammenfassen. Bei der Erstellung einer neuen VM können Sie entweder eine vorhandene Ressourcengruppe verwenden oder eine neue erstellen.

## <a name="choose-the-vm-image"></a>Auswählen des VM-Image

Das Auswählen eines Images ist eine der wichtigsten Entscheidungen, die Sie beim Erstellen einer VM berücksichtigen müssen. Ein Image ist eine Vorlage, die zum Erstellen einer VM verwendet wird. Diese Vorlagen enthalten ein Betriebssystem und häufig auch andere Software, z.B. Entwicklungstools oder Webhostingumgebungen.

Alle Komponenten, die auf einem Computer installiert werden können, können auch in einem Image enthalten sein. Sie können einen virtuellen Computer aus einem Image erstellen, die auf genau die Aufgaben, die Sie benötigen vorkonfiguriert ist beispielsweise zum Hosten von Web-app unter der Apache-HTTP-Server.

> [!TIP]
> Sie können auch benutzerdefinierten Datenträgerimages hochladen.

## <a name="sizing-your-vm"></a>Ändern der Größe Ihrer VM

Ein virtueller Computer weist wie ein physischer Computer eine bestimmte Menge an Arbeitsspeicher und CPU-Leistung auf. Azure bietet eine Reihe von VMs mit unterschiedlichen Größen zu unterschiedlichen Preisen an. Verarbeitungsleistung, Arbeitsspeicher und maximale Speicherkapazität des virtuellen Computers bestimmt die Größe, die Sie auswählen.

> [!WARNING]
> Es gelten Kontingentgrenzen für die einzelnen Abonnements, die sich auf die Erstellung der VM auswirken können. Standardmäßig dürfen Ihre VMs innerhalb einer Region insgesamt nicht mehr als 20 virtuelle _Kerne_ aufweisen. Sie können die VMs entweder auf mehrere Regionen aufteilen oder einen [Onlineantrag](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) stellen, damit die Grenzen erhöht werden.

Die VM-Größen werden in Kategorien unterteilt, angefangen bei der B-Serie für grundlegende Tests, bis hin zur H-Serie für große Computingtasks. Wählen Sie die Größe der VM anhand der Workload aus, die Sie ausführen möchten. Es ist möglich, die Größe eines virtuellen Computers ändern, nachdem dieses erstellt wurde, aber der virtuelle Computer zuerst beendet werden muss. Daher empfiehlt es sich entsprechend ausgehend nach Möglichkeit Größe zu.

#### <a name="here-are-some-guidelines-based-on-the-scenario-you-are-targeting"></a>Es folgen einige Richtlinien, die anhand des Szenarios, die Sie verwenden möchten

| Vorgehensweise | Prüfen Sie die folgenden Größen:
|-------|------------------|
| **Allgemeine Verwendung computing/Web**: Tests und Entwicklung, kleine bis mittlere Datenbanken oder mit geringer bis mittlerer Auslastung-Webserver. | B, Dsv3, Dv3, DSv2, Dv2 |
| **Hohe berechnungstasks**: mittlere Webserver, Network Appliances, Batchprozesse und Anwendungsserver. | Fsv2, Fs, F |
| **Hohen speicherauslastung**: relationale Datenbankserver, mittlere bis große Caches und in-Memory-Analysen. | Esv3, Ev3, M, GS, G, DSv2, Dv2 |
| **Die datenspeicherung und-Verarbeitung**: Big Data, SQL- und NoSQL-Datenbanken, die Notwendigkeit hoher Durchsatz und e/a. | Ls |
| **Aufwendiges Grafikrendering** oder Videobearbeitung sowie Modelltraining und Rückschlüsse (ND) mit Deep Learning. | NV, NC, NCv2, NCv3, ND |
| **High Performance computing (HPC)**: Ihre Workloads benötigen die schnellsten und leistungsfähigsten CPU-VMs mit hohem Durchsatz. über optionale Schnittstellen. | H |

## <a name="choosing-storage-options"></a>Auswählen von Speicheroptionen

Der nächste Satz von Entscheidungen dreht sich um Speicher. Zunächst können Sie die Datenträgertechnologie auswählen. Zu den Optionen zählt ein konventionelles Festplattenlaufwerk (HDD) oder ein moderneres Solid State Drive (SSD). Genau wie die Hardware, die Sie erwerben, kostet SSD-Speicher mehr, bietet aber eine bessere Leistung.

> [!TIP]
> Es sind zwei SSD-Speicherebenen verfügbar: Standard und Premium. Wählen Sie SSD Standard-Datenträger aus, wenn Sie normale Workloads verwenden, aber eine bessere Leistung wünschen. Wählen Sie SSD Premium-Datenträger aus, wenn Sie über E/A-intensive Workloads oder unternehmenskritische Systeme verfügen, die Daten sehr schnell verarbeiten müssen.

### <a name="mapping-storage-to-disks"></a>Zuordnen von Speicher zu Datenträgern

Azure verwendet virtuellen Festplatten (VHDs), um physische Datenträger für den virtuellen Computer darstellen. VHDs replizieren das logische Format und die Daten eines Festplattenlaufwerks, werden aber als Seitenblobs in einem Azure Storage-Konto gespeichert. Sie können pro Datenträger welche Art von Speicher (SSD oder HDD) verwenden soll. Dies ermöglicht es Ihnen, die Leistung jedes Datenträgers zu steuern, wahrscheinlich basierend auf der E/A, die Sie auf ihm ausführen möchten.

Standardmäßig werden zwei virtuelle Festplatten (VHDs) für Ihre Linux-VM erstellt:

1. Die **Betriebssystem-Datenträger**: Dies ist das primäre Laufwerk, und es hat eine maximale Kapazität von 2048 GB. Es wird standardmäßig mit der Bezeichnung `/dev/sda` versehen.

1. Ein **temporären Datenträger**: Dies dient als temporärer Speicher für das Betriebssystem oder andere apps. Auf virtuellen Linux-Computern trägt der Datenträger den Namen `/dev/sdb`. Er wird vom Azure Linux-Agent formatiert und in `/mnt` eingebunden. Er wird basierend auf der Größe der VM dimensioniert und dient zum Speichern der Auslagerungsdatei.

> [!WARNING]
> Der temporäre Datenträger ist nicht persistent. Sie sollten nur Daten auf diesen Datenträger schreiben, die für das System nicht wichtig sind.

#### <a name="what-about-data"></a>Wie sieht es mit Daten aus?

Sie können Daten auf dem primären Laufwerk zusammen mit dem Betriebssystem speichern, aber ein besserer Ansatz ist es, dedizierte _Datenträger_ zu erstellen. Sie können weitere Datenträger erstellen und an die VM anfügen. Jeder Datenträger kann bis zu 4.095 GB Daten enthalten. Die maximale Speicherkapazität wird durch die Größe der VM bestimmt, die Sie auswählen.

> [!NOTE]
> Eine interessante Möglichkeit stellt die Erstellung eines VHD-Images über einen echten Datenträger dar. Dadurch können Sie die einfache Migration zu _vorhandenen_ Informationen von einem lokalen Computer in der Cloud.

### <a name="unmanaged-vs-managed-disks"></a>Nicht verwaltete und verwaltete Datenträger im Vergleich

Die letzte Speicherentscheidung, die Sie treffen müssen, bezieht sich darauf, ob Sie **nicht verwaltete** oder **verwaltete** Datenträger verwenden möchten.

Mit nicht verwalteten Datenträgern sind Sie für die Speicherkonten verantwortlich, die verwendet werden, um die VHDs zu speichern, die den Datenträgern Ihrer VM entsprechen. Sie zahlen die Speicherkontogebühren für die Menge an Speicherplatz, die Sie verwenden. Ein einzelnes Speicherkonto verfügt über ein festes Ratenlimit von 20.000 E/A-Vorgängen pro Sekunde. Dies bedeutet, dass ein einzelnes Speicherkonto 40 virtuelle Standardfestplatten mit voller Auslastung unterstützen kann. Wenn Sie horizontal hochskalieren müssen, benötigen Sie mehrere Speicherkonten. Dies kann kompliziert sein.

Die Verwendung von verwalteten Datenträgern stellt das neuere Datenträgerspeichermodell dar und wird empfohlen. Sie lösen diese Komplexität elegant, indem sie die Last der Verwaltung der Speicherkonten an Azure übertragen. Sie geben den Datenträgertyp (Premium oder Standard) und die Größe des Datenträgers, und Azure erstellt und verwaltet sowohl den Datenträger _und_ den Speicher verwendet. Sie müssen sich keine Sorgen um die Limits für Speicherkonten machen, was deren horizontale Hochskalierung vereinfacht. Sie bieten auch einige weitere Vorteile:

- **Verbesserte Zuverlässigkeit**: Azure stellt sicher, dass VHDs, die hohe Zuverlässigkeit virtuellen Computern in verschiedenen Teilen der Azure-Speicher zu ähnlichen Maß an Stabilität platziert werden.
- **Größere Sicherheit**: Verwaltete Datenträger sind echte verwaltete Ressourcen in der Ressourcengruppe. Dies bedeutet, dass sie die rollenbasierte Zugriffssteuerung verwenden können, um einzuschränken, wer mit den VHD-Daten arbeiten kann.
- **Unterstützung von Momentaufnahmen**: Momentaufnahmen können verwendet werden, um eine schreibgeschützte Kopie einer VHD zu erstellen. Müssen Sie den übergeordneten virtuellen Computer herunterfahren, aber erstellen die Momentaufnahme nur dauert ein paar Sekunden. Sobald dies abgeschlossen ist, können Sie den virtuellen Computer einschalten und verwenden die Momentaufnahme einen doppelten virtueller Computer, um ein Produktionsproblem zu beheben oder Rollback für den virtuellen Computer zu dem Punkt in der Zeit, die die Momentaufnahme erstellt wurde erstellt.
- **Sichern Sie die Unterstützung**: verwaltete Datenträger können automatisch gesichert werden in verschiedenen Regionen für die notfallwiederherstellung mit Azure Backup ohne Auswirkungen auf den Dienst des virtuellen Computers.

## <a name="network-communication"></a>Netzwerkkommunikation

Virtuelle Computer kommunizieren mit externen Ressourcen über ein virtuelles Netzwerk (VNET). Das VNET stellt ein privates Netzwerk in einer einzelnen Region dar, in der Ihre Ressourcen kommunizieren. Ein virtuelles Netzwerk verhält sich wie die Netzwerke, die Sie lokal verwalten. Sie können es in Subnetze zum Isolieren von Ressourcen unterteilen, eine Verbindung mit anderen Netzwerken (einschließlich Ihrer lokalen Netzwerke) herstellen und Regeln für den Datenverkehr zum Steuern von eingehenden und ausgehenden Verbindungen anwenden.

### <a name="planning-your-network"></a>Planen des Netzwerks

Wenn Sie eine neue VM erstellen, besteht die Option, ein neues virtuelles Netzwerk zu erstellen oder ein vorhandenes VNET in Ihrer Region zu verwenden.

Es ist einfach, Azure das Netzwerk zusammen mit der VM erstellen zu lassen, aber es ist wahrscheinlich für die meisten Szenarien nicht ideal. Es ist besser, Planen Sie Ihren netzwerkanforderungen _voraus_ für alle Komponenten in Ihrer Architektur und VNet-Struktur separat erstellen. Anschließend erstellen Sie die virtuellen Computer aus, und platzieren Sie sie in den VNets bereits erstellt. Wir werden uns später in diesem Modul ausführlicher mit virtuellen Netzwerken befassen.

Bevor wir einen virtuellen Computer erstellen, müssen wir entscheiden, wie wir den virtuellen Computer verwalten möchten. Sehen wir uns die verfügbaren Optionen an.