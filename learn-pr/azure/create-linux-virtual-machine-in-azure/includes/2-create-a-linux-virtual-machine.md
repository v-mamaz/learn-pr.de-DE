Wir verfügen über eine vorhandene Website, die auf einem lokalen Ubuntu Linux-Server ausgeführt wird. Unser Ziel ist das Erstellen eines virtuellen Azure-Computers (VM), das Verwenden des neuesten Ubuntu-Images und das Migrieren der Website in die Cloud. In diesem Abschnitt erfahren Sie mehr über die Optionen, über die Sie beim Erstellen eines virtuellen Computers in Azure entscheiden müssen.

## <a name="introduction-to-azure-virtual-machines"></a>Einführung in Azure Virtual Machines

Virtuelle Azure-Computer sind skalierbare, bedarfsgesteuerte Cloud Computing-Ressourcen. Sie umfassen einen Prozessor, den Arbeitsspeicher, den Speicher und Netzwerkressourcen. Sie können virtuelle Computer beliebig starten und beenden und über das Azure-Portal oder die Azure CLI verwalten. Sie können auch eine SSH (Remote Secure Shell) verwenden, um direkt eine Verbindung mit dem ausgeführten virtuellen Computer herzustellen und Befehle auszuführen, als würden Sie auf einem lokalen Computer arbeiten.

### <a name="running-linux-in-azure"></a>Ausführen von Linux in Azure

Das Erstellen von auf Linux basierenden virtuellen Computern in Azure ist einfach. Microsoft arbeitet mit herausragenden Linux-Anbietern zusammen, um sicherzustellen, dass deren Distributionen für die Azure-Plattform optimiert sind. Sie können virtuelle Computer aus vordefinierten Images für eine Vielzahl gängiger Linux-Distributionen wie SUSE, Red Hat und Ubuntu erstellen oder Ihre eigene Linux-Distribution für die Ausführung in der Cloud erstellen.

## <a name="creating-an-azure-vm"></a>Erstellen eines virtuellen Azure-Computers

Es gibt verschiedene Möglichkeiten, virtuelle Computer in Azure zu definieren und bereitzustellen: das Azure-Portal, ein Skript (über die Azure CLI oder PowerShell) oder eine Azure Resource Manager-Vorlage. In allen Fällen müssen Sie verschiedene Arten von Informationen bereitstellen, auf die wir später noch eingehen.

Außerdem stellt Azure Marketplace vorkonfigurierte Images zur Verfügung, die sowohl ein Betriebssystem als auch beliebte Softwaretools umfassen, die für bestimmte Szenarien installiert sind.

![Azure Marketplace Virtual Machines](../media-drafts/2-marketplace-vm-choices.png)

## <a name="resources-used-in-a-linux-vm"></a>Auf einem virtuellen Linux-Computer verwendete Ressourcen

Wenn Sie einen virtuellen Linux-Computer in Azure erstellen, erstellen Sie gleichzeitig auch Ressourcen, um diesen zu hosten. Diese Ressourcen arbeiten zusammen, um einen virtuellen Computer zu erstellen und das Linux-Betriebssystem auszuführen. Sie sind entweder bereits vorhanden (und werden während der Erstellung des virtuellen Computers ausgewählt), oder Sie werden gemeinsam mit dem virtuellen Computer erstellt. Folgende Ressourcen müssen vorhanden sein:

- Ein virtueller Computer, der CPU und Speicherressourcen bereitstellt.
- Ein Azure Storage-Konto, in dem die virtuellen Festplatten gespeichert werden.
- Virtuelle Datenträger, auf denen das Betriebssystem, die Anwendungen und Daten gespeichert werden.
- Ein virtuelles Netzwerk (VNET), über das der virtuelle Computer mit anderen Azure-Diensten oder Ihrer lokalen Hardware verbunden wird.
- Eine Netzwerkschnittstelle für die Kommunikation mit dem VNET.
- Eine optionale öffentliche IP-Adresse, damit Sie auf den virtuellen Computer zugreifen können.

Wie bei anderen Azure-Diensten auch benötigen Sie eine **Ressourcengruppe**, in der der virtuelle Computer gespeichert wird. Sie sollten diese Ressourcen zu Verwaltungszwecken optional in einer Gruppe zusammenfassen. Bei der Erstellung eines neuen virtuellen Computers können Sie eine vorhandene Ressourcengruppe verwenden oder eine neue Ressourcengruppe erstellen.

## <a name="choose-the-vm-image"></a>Auswählen des VM-Image

Das Auswählen eines Images ist eine der wichtigsten Entscheidungen, die Sie beim Erstellen einer VM berücksichtigen müssen. Ein Image ist eine Vorlage, die zum Erstellen einer VM verwendet wird. Diese Vorlagen enthalten ein Betriebssystem und häufig auch weitere Software, z.B. Entwicklungstools oder Webhostingumgebungen.

Alle Komponenten, die auf einem Computer installiert werden können, können auch in einem Image enthalten sein. Sie können einen virtuellen Computer über ein Image erstellen, das genau für die Aufgaben vorkonfiguriert ist, die Sie benötigen, beispielsweise zum Hosten einer Web-App auf einem Apache-Server.

> [!TIP]
> Sie können außerdem auch Ihre eigenen Datenträgerimages erstellen und hochladen. Weitere Informationen dazu finden Sie in der Dokumentation.

## <a name="sizing-your-vm"></a>Auswählen der Größe Ihres virtuellen Computers
Ein virtueller Computer weist wie ein physischer Computer eine bestimmte Menge an Arbeitsspeicher und CPU-Leistung auf. Azure bietet eine Reihe von virtuellen Computern mit unterschiedlichen Größen zu unterschiedlichen Preisen an. Die Größe, die Sie auswählen, bestimmt die Verarbeitungsleistung, den Arbeitsspeicher und die maximale Speicherkapazität Ihres virtuellen Computers.

> [!WARNING]
> Es gelten Kontingentgrenzwerte für die einzelnen Abonnements, die Einfluss auf die Erstellung des virtuellen Computers haben können. Standardmäßig dürfen Ihre virtuellen Computer innerhalb einer Region insgesamt nicht mehr als 20 virtuelle _Kerne_ aufweisen. Sie können die virtuellen Computer entweder auf mehrere Regionen aufteilen oder einen [Onlineantrag](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) stellen, damit die Grenzwerte erhöht werden.

Die VM-Größen werden in Kategorien unterteilt, angefangen bei der B-Serie für grundlegende Tests bis hin zur H-Serie für große Computingtasks. Wählen Sie die Größe des virtuellen Computers anhand der Workload aus, die Sie ausführen möchten. Sie können die Größe eines virtuellen Computers zwar ändern, nachdem Sie ihn erstellt haben, aber Sie müssen ihn zu diesem Zweck beenden. Daher ist es besser, wenn Sie direkt zu Beginn die richtige Größe auswählen.

#### <a name="here-are-some-guidelines-based-on-the-scenario-you-are-targeting"></a>Nachfolgend werden einige Richtlinien für verschiedene Szenarien aufgeführt.

| Vorgehensweise | Prüfen Sie die folgenden Größen:
|-------|------------------|
| **Allgemeine Verwendung für das Computing bzw. Internet:** für Test- und Entwicklungsaufgaben, für kleine bis mittlere Datenbanken oder für Webserver mit geringer bis mittlerer Auslastung. | B, Dsv3, Dv3, DSv2, Dv2 |
| **Schwierige Rechenaufgaben:** für Webserver, Network Appliances, Batchverarbeitungsvorgänge und Anwendungsserver mit mittlerer Auslastung. | Fsv2, Fs, F |
| **Hohe Speicherauslastung:** für relationale Datenbankserver, mittlere bis große Caches und In-Memory-Analysen. | Esv3, Ev3, M, GS, G, DSv2, Dv2 |
| **Speichern und Verarbeiten von Daten:** Datenbanken für Big Data, SQL und NoSQL, für die ein hoher Datenträgerdurchsatz und E/A erforderlich sind. | Ls |
| **Aufwendiges Grafikrendering** oder Videobearbeitung sowie für Modelltraining und Rückschlüsse (ND) mit Deep Learning. | NV, NC, NCv2, NCv3, ND |
| **High Performance Computing (HPC):** wenn Sie die schnellsten und leistungsfähigsten CPUs benötigen, die optional über Netzwerkschnittstellen mit hohem Durchsatz (RDMA) verfügen. | H |

## <a name="choosing-storage-options"></a>Auswählen von Speicheroptionen

Die nächsten Entscheidungen drehen sich um den Speicher. Zunächst können Sie die Datenträgertechnologie auswählen. Zu den Optionen zählt ein konventionelles Festplattenlaufwerk (HDD) oder ein modernerer SSD-Datenträger (Solid State Drive). Genau wie die Hardware, die Sie erwerben, kostet SSD-Speicher mehr, bietet aber eine bessere Leistung.

> [!TIP]
> Es sind zwei Ebenen von SSD-Speicher verfügbar: Standard und Premium. Wählen Sie SSD Standard-Datenträger aus, wenn Sie normale Workloads verwenden, aber eine bessere Leistung wünschen. Wählen Sie SSD Premium-Datenträger aus, wenn Sie über E/A-intensive Workloads oder unternehmenskritische Systeme verfügen, die Daten sehr schnell verarbeiten müssen.

### <a name="mapping-storage-to-disks"></a>Zuordnen von Speicher zu Datenträgern

Azure verwendet virtuelle Festplatten (VHDs), um physische Datenträger für den virtuellen Computer darzustellen. VHDs replizieren das logische Format und die Daten eines Festplattenlaufwerks, werden aber als Seitenblobs in einem Azure Storage-Konto gespeichert. Sie können pro Datenträger auswählen, welche Art von Speicher verwendet werden soll (SSD oder HDD). Dies ermöglicht es Ihnen, die Leistung jedes Datenträgers zu steuern, wahrscheinlich basierend auf der E/A, die Sie auf ihm ausführen möchten.

Standardmäßig werden zwei virtuelle Festplatten (VHDs) für Ihren virtuellen Linux-Computer erstellt:

1. Der **Betriebssystemdatenträger**. Dies ist das primäre Laufwerk. Es besitzt eine maximale Kapazität von 2.048 GB. Es wird standardmäßig mit der Bezeichnung `/dev/sda` versehen.

1. Ein **temporärer Datenträger**. Dieser dient als temporärer Speicher für das Betriebssystem oder Apps. Auf virtuellen Linux-Computern trägt der Datenträger den Namen `/dev/sdb`. Er wird vom Azure Linux-Agent formatiert und in `/mnt` eingebunden. Er wird basierend auf der Größe des virtuellen Computers dimensioniert und dient zum Speichern der Auslagerungsdatei. 

> [!WARNING]
> Der temporäre Datenträger ist nicht persistent. Sie sollten nur Daten auf diesen Datenträger schreiben, die für das System nicht wichtig sind.

#### <a name="what-about-data"></a>Wie sieht es mit Daten aus?

Sie können Daten auf dem primären Laufwerk zusammen mit dem Betriebssystem speichern, aber ein besserer Ansatz ist es, dedizierte _Datenträger für Daten_ zu erstellen. Sie können weitere Datenträger erstellen und an den virtuellen Computer anfügen. Jeder Datenträger kann bis zu 4.095 GB Daten enthalten. Die Höchstmenge des Speichers wird durch die Größe des virtuellen Computers bestimmt, die Sie auswählen.

> [!NOTE]
> Eine interessante Möglichkeit ist die Erstellung eines VHD-Images von einem echten Datenträger. Dies ermöglicht die einfache Migration _vorhandener_ Informationen von einem lokalen Computer in die Cloud.

### <a name="unmanaged-vs-managed-disks"></a>Nicht verwaltete und verwaltete Datenträger im Vergleich

Die letzte Speicherentscheidung, die Sie treffen müssen, bezieht sich darauf, ob Sie **nicht verwaltete** oder **verwaltete** Datenträger verwenden möchten.

Mit nicht verwalteten Datenträgern sind Sie für die Speicherkonten verantwortlich, die verwendet werden, um die VHDs zu speichern, die den Datenträgern Ihrer virtuellen Computer entsprechen. Sie zahlen die Speicherkontogebühren für die Menge an Speicherplatz, die Sie verwenden. Ein einzelnes Speicherkonto verfügt über ein festes Ratenlimit von 20.000 E/A-Vorgängen/Sek. Dies bedeutet, dass ein einzelnes Speicherkonto 40 virtuelle Standardfestplatten mit voller Arbeitsauslastungskontrolle unterstützen kann. Wenn Sie horizontal hochskalieren müssen, benötigen Sie mehrere Speicherkonten. Dies kann kompliziert sein.

Verwaltete Datenträger stellen das neuere und empfohlene Datenträgerspeichermodell dar. Sie lösen diese Komplexität elegant, indem sie die Last der Verwaltung der Speicherkonten an Azure übertragen. Sie geben den Datenträgertyp (Premium oder Standard) und die Größe des Datenträgers an, und Azure erstellt und verwaltet den Datenträger _und_ den verwendeten Speicher. Sie müssen sich keine Sorgen um die Limits für Speicherkonten machen, was deren horizontale Hochskalierung erleichtert. Sie bieten auch einige weitere Vorteile:

- **Erhöhte Zuverlässigkeit**: Azure stellt sicher, dass VHDs, die hochzuverlässigen virtuellen Computern zugeordnet sind, in verschiedenen Teilen des Azure-Speichers platziert werden, um ein ähnliches Maß an Ausfallsicherheit zu gewährleisten.
- **Größere Sicherheit**: Verwaltete Datenträger sind echte verwaltete Ressourcen in der Ressourcengruppe. Dies bedeutet, dass sie rollenbasierte Zugriffssteuerung verwenden können, um einzuschränken, wer mit den VHD-Daten arbeiten kann.
- **Unterstützung von Momentaufnahmen**: Momentaufnahmen können verwendet werden, um eine schreibgeschützte Kopie einer VHD zu erstellen. Sie müssen den übergeordneten virtuellen Computer herunterfahren, aber das Erstellen der Momentaufnahme dauert nur wenige Sekunden. Wenn dieser Vorgang abgeschlossen ist, können Sie den virtuellen Computer aktivieren und die Momentaufnahme verwenden, um den virtuellen Computer zu duplizieren, damit Sie die Problembehandlung eines Produktionsproblems ausführen oder ein Rollback des virtuellen Computers zum Zeitpunkt erstellen können, zu dem die Momentaufnahme erstellt wurde.
- **Sicherungsunterstützung**: Verwaltete Datenträger können ohne Auswirkungen auf den Dienst des virtuellen Computers automatisch in verschiedenen Regionen für die Notfallwiederherstellung mit Azure Backup gesichert werden.

## <a name="network-communication"></a>Netzwerkkommunikation

Virtuelle Computer kommunizieren mit externen Ressourcen über ein virtuelles Netzwerk (VNET). Das VNET stellt ein privates Netzwerk in einer einzelnen Region dar, in der Ihre Ressourcen kommunizieren. Ein virtuelles Netzwerk verhält sich wie die Netzwerke, die Sie lokal verwalten. Sie können es in Subnetze zum Isolieren von Ressourcen unterteilen, eine Verbindung mit anderen Netzwerken (einschließlich Ihrer lokalen Netzwerke) herstellen und Regeln für den Datenverkehr zum Steuern von eingehenden und ausgehenden Verbindungen anwenden.

### <a name="planning-your-network"></a>Planen des Netzwerks

Wenn Sie einen neuen virtuellen Computer erstellen, besteht die Option, ein neues virtuelles Netzwerk zu erstellen oder ein vorhandenes VNET in Ihrer Region zu verwenden.

Es ist einfach, Azure das Netzwerk zusammen mit dem virtuellen Computer erstellen zu lassen, aber es ist wahrscheinlich für die meisten Szenarien nicht ideal. Es ist besser, Ihre Netzwerkanforderungen _im Voraus_  für alle Komponenten Ihrer Architektur zu planen und die VNET-Struktur separat zu erstellen. Erstellen Sie dann die virtuellen Computer, und platzieren Sie sie in den bereits erstellten VNETs. Wir werden uns später in diesem Modul ausführlicher mit virtuellen Netzwerken befassen.

Bevor wir einen virtuellen Computer erstellen, müssen wir entscheiden, wie wir den virtuellen Computer verwalten möchten. Sehen wir uns die verfügbaren Optionen an.