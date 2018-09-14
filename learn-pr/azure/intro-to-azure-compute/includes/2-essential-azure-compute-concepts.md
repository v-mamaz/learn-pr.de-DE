Ihre Forschungsteam große Mengen von Image-Daten gesammelt, die eine Ermittlung auf dem Mars führen können. Sie müssen die Datenverarbeitung auf Rechenaufwand, aber die Geräte aus, um die Arbeit haben. Sehen wir uns an, warum Azure eine gute Wahl, die Data-Analyse durchzuführen ist.

## <a name="what-is-azure-compute"></a>Was ist Azure Compute?
Azure Compute ist eine bei Bedarf-computing-Dienst zum Ausführen von Cloud-basierte Anwendungen. Er stellt Rechenressourcen wie Multi-Core-Prozessoren und Supercomputer über virtuelle Computer und Container bereit. Darüber hinaus bietet das serverlose computing zum Ausführen von apps ohne Infrastruktur einrichten oder konfigurieren. Die Ressourcen sind bei Bedarf verfügbar und können in der Regel innerhalb von Minuten oder sogar Sekunden erstellt werden. Sie zahlen nur für die Ressourcen, die Sie verwenden, und nur solange Sie sie verwenden.

Es gibt drei gängige Vorgehensweise zum Ausführen von Compute in Azure:

- Virtuelle Computer
- Container
- Serverloses Computing

## <a name="what-are-virtual-machines"></a>Was sind virtuelle Computer?

**Virtuelle Computer**, oder virtuellen Computern, Software-Emulationen physischer Computer. Dies umfasst einen virtuellen Prozessor, den Arbeitsspeicher, den Speicher und die Netzwerkressourcen. Sie hosten ein Betriebssystem, und Sie können Software wie auf einem physischen Computer installieren und ausführen. Und mit einem Remotedesktopclient, können Sie verwenden und den virtuellen Computer zu steuern, als säßen Sie am Anfang es.

### <a name="virtual-machines-in-azure"></a>Virtuelle Computer in Azure

Virtuelle Computer (VMs) können in Azure erstellt und gehostet werden. In der Regel können neuer virtuelle Computer erstellt und in wenigen Minuten durch Auswählen eines Images von vorkonfigurierten virtuellen Computer bereitgestellt werden.

Wählen ein Image ist eine der wichtigsten Entscheidungen, die Sie beim Erstellen eines virtuellen Computers vornehmen müssen. Ein Image ist eine Vorlage, die zum Erstellen einer VM verwendet wird. Diese Vorlagen enthalten bereits ein Betriebssystem und häufig auch andere Software, z.B. Entwicklungstools oder Webhostingumgebungen.

## <a name="what-are-containers"></a>Was sind Container?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yMhY]

Container sind eine Virtualisierungsumgebung, die im Gegensatz zu VMs kein Betriebssystem beinhaltet. Stattdessen verweisen sie auf das Betriebssystem der Hostumgebung, in der der Container ausführt wird. Wenn zum Beispiel fünf Container auf einem Server mit einem spezifischen Linux-Kernel ausgeführt werden, werden alle fünf Container auf demselben Kernel ausgeführt.

Die folgende Abbildung zeigt einen Vergleich zwischen Anwendungen, die direkt auf einem virtuellen Computer und Anwendungen, die innerhalb von Containern auf einem virtuellen Computer ausgeführt wird.

![Eine Abbildung zeigt, wie das Betriebssystem einem der virtuellen Maschine und nicht Teil des Containers ist](../media/2-vm-versus-containers.png)

Container enthalten in der Regel eine Anwendung, die Sie schreiben &mdash; zusammen mit alle Bibliotheken, die für Ihre Anwendung zur Ausführung in der hostumgebung Kernel erforderlich sind.

Container sind kompakt und dafür konzipiert, dynamisch erstellt, hochskaliert und beendet zu werden. Dadurch können Sie zu reagieren auf Änderungen bei Bedarf schnell neu starten, im Falle einer Unterbrechung Absturz oder die Hardwarekonfiguration.

Ein weiterer Vorteil der Verwendung von Containern ist die Möglichkeit, mehrere isolierte Anwendung auf einem virtuellen Computer auszuführen. Da Container selbst gesichert und isoliert sind, benötigen Sie nicht unbedingt separate VMs für separate Workloads.

Azure unterstützt Docker-Container und mehrere Methoden zum Verwalten dieser Container. Container können manuell oder mit Azure-Diensten wie Azure Kubernetes Service verwaltet werden.

### <a name="what-is-serverless-computing"></a>Was ist serverloses Computing?

Serverloses Computing ist eine in der Cloud gehostete Ausführungsumgebung, die Ihren Code ausführt, die zugrunde liegende Hostumgebung jedoch vollständig abstrahiert. Sie erstellen eine Instanz des Diensts und fügen Ihren Code hinzu. Eine Konfiguration oder Wartung der Infrastruktur ist weder erforderlich noch zulässig.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yzjL]

Sie konfigurieren Ihre serverlosen Apps, um auf _Ereignisse_ zu reagieren. Dabei kann es sich um einen REST-Endpunkt, einen Timer oder eine von einem anderen Azure-Dienst empfangene Nachricht handeln. Die serverlose App wird nur ausgeführt, wenn sie durch ein Ereignis ausgelöst wird.

Im Wesentlichen keine Infrastruktur Ihrer Verantwortung. Die Skalierung und Leistungsanpassung erfolgt automatisch. Es werden nur die Ressourcen in Rechnung gestellt, die Sie verwenden. Das Reservieren von Kapazität ist nicht notwendig.

Azure verfügt über zwei Implementierungen von serverlosem Computing:

- **Azure Functions** kann der Code in fast jeder modernen Sprache ausführen.
- Mit **Azure Logic Apps** erstellte Apps werden in einem webbasierten Designer erstellt und können Logik ausführen, die von Azure-Diensten ausgelöst wird – und zwar ganz ohne Schreiben von Code.
