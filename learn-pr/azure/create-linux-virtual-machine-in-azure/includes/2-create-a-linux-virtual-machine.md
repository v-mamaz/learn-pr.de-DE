Wir verfügen über eine Website, die auf einem lokalen Ubuntu Linux-Server ausgeführt wird. Wir möchten einen virtuellen Azure-Computer (Virtual Machine, VM) mit dem neuesten Ubuntu-Image erstellen und die Website in die Cloud migrieren. In diesem Abschnitt erfahren Sie mehr über die Optionen, zwischen denen Sie sich beim Erstellen eines virtuellen Computers in Azure entscheiden müssen.

## <a name="introduction-to-azure-virtual-machines"></a>Einführung in Azure Virtual Machines

Bei Azure Virtual Machines handelt es sich um eine skalierbare bedarfsgesteuerte Cloud Computing-Ressource. Sie umfasst einen Prozessor, Arbeitsspeicher, Speicherplatz und Netzwerkressourcen. Sie können virtuelle Computer nach Belieben starten und beenden und über das Azure-Portal oder mithilfe der Azure-Befehlszeilenschnittstelle verwalten. Sie können auch eine Remote-SSH (Secure Shell) verwenden, um direkt eine Verbindung mit dem ausgeführten virtuellen Computer herzustellen und Befehle wie auf einem lokalen Computer auszuführen.

### <a name="running-linux-in-azure"></a>Ausführen von Linux in Azure

Das Erstellen von auf Linux basierenden virtuellen Computern in Azure ist einfach. Microsoft arbeitet mit bekannten Linux-Anbietern zusammen, um sicherzustellen, dass deren Distributionen für die Azure-Plattform optimiert sind. Sie können virtuelle Computer aus vordefinierten Images für eine Vielzahl gängiger Linux-Distributionen wie SUSE Linux Enterprise Server, Red Hat Enterprise Linux und Ubuntu erstellen oder Ihre eigene Linux-Distribution für die Ausführung in der Cloud erstellen.

## <a name="creating-an-azure-vm"></a>Erstellen eines virtuellen Azure-Computers

Es gibt verschiedene Möglichkeiten, virtuelle Computer in Azure zu definieren und bereitzustellen: das Azure-Portal, ein Skript (unter Verwendung von PowerShell oder der Azure-Befehlszeilenschnittstelle) oder eine Azure Resource Manager-Vorlage. In allen Fällen müssen Sie verschiedene Arten von Informationen angeben, auf die wir später noch eingehen.

Außerdem stellt der Azure Marketplace vorkonfigurierte Images mit Betriebssystem und Installationen beliebter Softwaretools für bestimmte Szenarien zur Verfügung.

![Screenshot des Azure-Portals mit verschiedenen VM-Optionen im Azure Marketplace.](../media/2-marketplace-vm-choices.png)

## <a name="resources-used-in-a-linux-vm"></a>Auf einem virtuellen Linux-Computer verwendete Ressourcen

Wenn Sie einen virtuellen Linux-Computer in Azure erstellen, erstellen Sie gleichzeitig auch Ressourcen, um diesen zu hosten. Diese Ressourcen bilden die Grundlage für die Virtualisierung eines Computers und die Ausführung des Linux-Betriebssystems. Sie müssen entweder bereits vorhanden sein (und im Rahmen der VM-Erstellung ausgewählt werden) oder werden zusammen mit dem virtuellen Computer erstellt:

- Ein virtueller Computer, der CPU- und Arbeitsspeicherressourcen bereitstellt.
- Ein Azure Storage-Konto, in dem die virtuellen Festplatten gespeichert werden.
- Virtuelle Datenträger, auf denen das Betriebssystem, die Anwendungen und Daten gespeichert werden.
- Ein virtuelles Netzwerk (VNET), über das der virtuelle Computer mit anderen Azure-Diensten oder Ihrer lokalen Hardware verbunden wird.
- Eine Netzwerkschnittstelle für die Kommunikation mit dem VNET.
- Eine optionale öffentliche IP-Adresse, damit Sie auf den virtuellen Computer zugreifen können.

Wie bei anderen Azure-Diensten auch benötigen Sie eine **Ressourcengruppe**, in der der virtuelle Computer gespeichert wird. Sie sollten diese Ressourcen zu Verwaltungszwecken optional in einer Gruppe zusammenfassen. Bei der Erstellung eines neuen virtuellen Computers können Sie eine vorhandene Ressourcengruppe verwenden oder eine neue Ressourcengruppe erstellen.

## <a name="choose-the-vm-image"></a>Auswählen des VM-Image

Das Auswählen eines Images ist eine der wichtigsten Entscheidungen, die Sie beim Erstellen einer VM berücksichtigen müssen. Ein Image ist eine Vorlage, die zum Erstellen einer VM verwendet wird. Diese Vorlagen enthalten ein Betriebssystem und häufig auch weitere Software, z.B. Entwicklungstools oder Webhostingumgebungen.

Alle Komponenten, die auf einem Computer installiert werden können, können auch in einem Image enthalten sein. Sie können einen virtuellen Computer über ein Image erstellen, das genau für die Aufgaben vorkonfiguriert ist, die Sie benötigen (beispielsweise, um eine Web-App in einer Apache HTTP Server-Instanz zu hosten).

> [!TIP]  
> Sie können auch benutzerdefinierte Datenträgerimages erstellen und hochladen. Weitere Informationen finden Sie in der Dokumentation.

## <a name="sizing-your-vm"></a>Auswählen der Größe Ihres virtuellen Computers

Ein virtueller Computer weist wie ein physischer Computer eine bestimmte Menge an Arbeitsspeicher und CPU-Leistung auf. Azure bietet eine Reihe von virtuellen Computern mit unterschiedlichen Größen zu unterschiedlichen Preisen an. Die gewählte Größe bestimmt die Verarbeitungsleistung, den Arbeitsspeicher und die maximale Speicherkapazität des virtuellen Computers.

> [!WARNING]
> Es gelten Kontingentgrenzwerte für die einzelnen Abonnements, die Einfluss auf die Erstellung des virtuellen Computers haben können. Standardmäßig dürfen Ihre virtuellen Computer innerhalb einer Region insgesamt nicht mehr als 20 virtuelle _Kerne_ aufweisen. Sie können die virtuellen Computer entweder auf mehrere Regionen aufteilen oder einen [Onlineantrag](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) stellen, damit die Grenzwerte erhöht werden.

Die VM-Größen werden in Kategorien unterteilt, angefangen bei der B-Serie für grundlegende Tests, bis hin zur H-Serie für große Computingtasks. Wählen Sie die Größe des virtuellen Computers anhand der Workload aus, die Sie ausführen möchten. Sie können die Größe eines virtuellen Computers zwar ändern, nachdem Sie ihn erstellt haben, dazu müssen Sie ihn jedoch beenden. Daher ist es besser, wenn Sie direkt zu Beginn die richtige Größe auswählen.

#### <a name="here-are-some-guidelines-based-on-the-scenario-you-are-targeting"></a>Im Anschluss werden einige Richtlinien für verschiedene Szenarien aufgeführt.

| Vorgehensweise | Geeignete Größen
|-------|------------------|
| **Allgemeine Verwendung für Computing/Web:** Für Test- und Entwicklungsaufgaben, für kleine bis mittelgroße Datenbanken oder für Webserver mit geringer bis mittlerer Auslastung. | B, Dsv3, Dv3, DSv2, Dv2 |
| **Rechenintensive Aufgaben:** Für Webserver, Netzwerkappliances, Batchverarbeitungsvorgänge und Anwendungsserver mit mittlerer Auslastung. | Fsv2, Fs, F |
| **Hohe Speicherauslastung:** Für relationale Datenbankserver, mittelgroße bis große Caches und In-Memory-Analysen. | Esv3, Ev3, M, GS, G, DSv2, Dv2 |
| **Datenspeicherung und -verarbeitung:** Für Big Data-, SQL- und NoSQL-Datenbanken, für die ein hoher Datenträgerdurchsatz und E/A erforderlich sind. | Ls |
| **Aufwendiges Grafikrendering** oder Videobearbeitung sowie Modelltraining und Rückschlüsse (ND) mit Deep Learning. | NV, NC, NCv2, NCv3, ND |
| **High Performance Computing (HPC):** Für Szenarien, in denen Sie virtuelle Computer mit den schnellsten und leistungsstärksten CPUs benötigen (optional mit Netzwerkschnittstellen mit hohem Durchsatz). | H |

## <a name="choosing-storage-options"></a>Auswählen von Speicheroptionen

Die nächsten Entscheidungen beziehen sich auf den Speicher. Zunächst können Sie die Datenträgertechnologie auswählen. Zu den Optionen zählt ein konventionelles Festplattenlaufwerk (HDD) oder ein moderneres Solid State Drive (SSD). Genau wie die Hardware, die Sie erwerben, kostet SSD-Speicher mehr, bietet aber eine bessere Leistung.

> [!TIP]
> Es sind zwei SSD-Speicher-Ebenen verfügbar: Standard und Premium. Wählen Sie SSD Standard-Datenträger aus, wenn Sie normale Workloads verwenden, aber eine bessere Leistung wünschen. Wählen Sie SSD Premium-Datenträger aus, wenn Sie über E/A-intensive Workloads oder unternehmenskritische Systeme verfügen, die Daten sehr schnell verarbeiten müssen.

### <a name="mapping-storage-to-disks"></a>Zuordnen von Speicher zu Datenträgern

Azure verwendet virtuelle Festplatten (VHDs), um physische Datenträger für den virtuellen Computer darzustellen. VHDs replizieren das logische Format und die Daten eines Festplattenlaufwerks, werden aber als Seitenblobs in einem Azure Storage-Konto gespeichert. Sie können für jeden Datenträger auswählen, welche Art von Speicher verwendet werden soll (SSD oder HDD). Dies ermöglicht es Ihnen, die Leistung der einzelnen Datenträger zu steuern, – wahrscheinlich auf der Grundlage der für den Datenträger geplanten E/A-Vorgänge.

Standardmäßig werden zwei virtuelle Festplatten (VHDs) für Ihren virtuellen Linux-Computer erstellt:

1. Der **Betriebssystemdatenträger**: Dies ist das primäre Laufwerk. Es besitzt eine maximale Kapazität von 2.048 GB. Es wird standardmäßig mit der Bezeichnung `/dev/sda` versehen.

1. Ein **temporärer Datenträger**: Dieser dient als temporärer Speicher für das Betriebssystem oder für Apps. Auf virtuellen Linux-Computern hat der Datenträger den Namen `/dev/sdb`. Er wird vom Azure Linux-Agent formatiert und in `/mnt` eingebunden. Er wird basierend auf der Größe des virtuellen Computers dimensioniert und dient zum Speichern der Auslagerungsdatei. 

> [!WARNING]
> Der temporäre Datenträger ist nicht persistent. Sie sollten nur Daten auf diesen Datenträger schreiben, die für das System nicht wichtig sind.

#### <a name="what-about-data"></a>Wie sieht es mit Daten aus?

Sie können Daten auf dem primären Laufwerk zusammen mit dem Betriebssystem speichern, aber ein besserer Ansatz ist es, dedizierte _Datenträger für Daten_ zu erstellen. Sie können weitere Datenträger erstellen und an den virtuellen Computer anfügen. Jeder Datenträger kann bis zu 4.095 GB Daten enthalten. Die maximale Speicherkapazität wird durch die Größe des virtuellen Computers bestimmt, den Sie auswählen.

> [!NOTE]  
> Eine interessante Möglichkeit stellt die Erstellung eines VHD-Images auf der Grundlage eines echten Datenträgers dar. Dies ermöglicht die einfache Migration _vorhandener_ Informationen von einem lokalen Computer in die Cloud.

### <a name="unmanaged-vs-managed-disks"></a>Nicht verwaltete und verwaltete Datenträger im Vergleich

Die letzte Speicherentscheidung, die Sie treffen müssen, bezieht sich darauf, ob Sie **nicht verwaltete** oder **verwaltete** Datenträger verwenden möchten.

Mit nicht verwalteten Datenträgern sind Sie für die Speicherkonten verantwortlich, die verwendet werden, um die VHDs zu speichern, die den Datenträgern Ihrer virtuellen Computer entsprechen. Sie zahlen die Speicherkontogebühren für die Menge an Speicherplatz, die Sie verwenden. Ein einzelnes Speicherkonto verfügt über ein festes Ratenlimit von 20.000 E/A-Vorgängen/Sek. Dies bedeutet, dass ein einzelnes Speicherkonto 40 virtuelle Standardfestplatten mit voller Arbeitsauslastungskontrolle unterstützen kann. Wenn Sie horizontal hochskalieren müssen, benötigen Sie mehrere Speicherkonten. Dies kann kompliziert sein.

Die Verwendung von verwalteten Datenträgern stellt das neuere Datenträgerspeichermodell dar und wird empfohlen. Sie lösen dieses komplexe Problem elegant, indem sie die Last der Verwaltung der Speicherkonten auf Azure übertragen. Sie geben den Datenträgertyp (Premium oder Standard) und die Größe des Datenträgers an, und Azure erstellt und verwaltet den Datenträger _und_ den verwendeten Speicher. Sie müssen sich keine Gedanken um die Grenzwerte für Speicherkonten machen. Dies erleichtert deren horizontale Hochskalierung. Sie bieten auch einige weitere Vorteile:

- **Höhere Zuverlässigkeit:** Azure stellt sicher, dass VHDs, die virtuellen Computern mit hoher Zuverlässigkeit zugeordnet sind, in verschiedenen Teilen des Azure-Speichers platziert werden, um ein ähnliches Maß an Ausfallsicherheit zu gewährleisten.
- **Höhere Sicherheit:** Verwaltete Datenträger sind echte verwaltete Ressourcen in der Ressourcengruppe. Dies bedeutet, dass sie rollenbasierte Zugriffssteuerung verwenden können, um einzuschränken, wer mit den VHD-Daten arbeiten kann.
- **Unterstützung von Momentaufnahmen:** Momentaufnahmen können verwendet werden, um eine schreibgeschützte Kopie einer VHD zu erstellen. Der übergeordnete virtuelle Computer muss zwar heruntergefahren werden, das Erstellen der Momentaufnahme dauert jedoch nur wenige Sekunden. Anschließend können Sie den virtuellen Computer aktivieren und mithilfe der Momentaufnahme einen duplizierten virtuellen Computer erstellen, um ein Produktionsproblem zu behandeln, oder den virtuellen Computer mittels Rollback auf den Zeitpunkt der Momentaufnahmenerstellung zurücksetzen.
- **Sicherungsunterstützung:** Verwaltete Datenträger können für die Notfallwiederherstellung mit Azure Backup ohne Auswirkungen auf den VM-Dienst automatisch in verschiedenen Regionen gesichert werden.

## <a name="network-communication"></a>Netzwerkkommunikation

Virtuelle Computer kommunizieren mit externen Ressourcen über ein virtuelles Netzwerk (VNet). Das VNET stellt ein privates Netzwerk in einer einzelnen Region dar, in der Ihre Ressourcen kommunizieren. Ein virtuelles Netzwerk verhält sich wie die Netzwerke, die Sie lokal verwalten. Sie können es in Subnetze zum Isolieren von Ressourcen unterteilen, eine Verbindung mit anderen Netzwerken (einschließlich Ihrer lokalen Netzwerke) herstellen und Regeln für den Datenverkehr zum Steuern von eingehenden und ausgehenden Verbindungen anwenden.

### <a name="planning-your-network"></a>Planen des Netzwerks

Wenn Sie einen neuen virtuellen Computer erstellen, besteht die Option, ein neues virtuelles Netzwerk zu erstellen oder ein vorhandenes VNET in Ihrer Region zu verwenden.

Es ist zwar einfach, Azure das Netzwerk zusammen mit dem virtuellen Computer erstellen zu lassen, aber es ist wahrscheinlich für die meisten Szenarien nicht ideal. Es ist besser, Ihre Netzwerkanforderungen _im Voraus_ für alle Komponenten Ihrer Architektur zu planen und die VNET-Struktur separat zu erstellen. Erstellen Sie dann die virtuellen Computer, und platzieren Sie sie in den bereits erstellten VNETs. Wir werden uns später in diesem Modul ausführlicher mit virtuellen Netzwerken befassen.

Bevor wir einen virtuellen Computer erstellen, müssen wir entscheiden, wie wir den virtuellen Computer verwalten möchten. Sehen wir uns die verfügbaren Optionen an.