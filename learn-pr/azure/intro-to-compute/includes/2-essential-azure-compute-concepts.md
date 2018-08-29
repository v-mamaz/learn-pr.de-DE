Ihr Forschungsteam muss rechnerisch aufwändige Datenverarbeitung durchführen und verfügt nicht über die erforderlichen Mittel. Sie haben sich dazu entschieden, Azure für die Datenanalyse zu verwenden.

## <a name="what-is-azure-compute"></a>Was ist Azure Compute?
Azure Compute ist ein bei Bedarf abrufbarer Dienst für Rechenressourcen zum Ausführen von cloudbasierten Anwendungen. Er stellt Rechenressourcen wie Multi-Core-Prozessoren und Supercomputer über virtuelle Computer und Container bereit. Darüber hinaus bietet der Dienst serverloses Computing, damit Apps ausgeführt werden können, ohne dass Infrastruktur eingerichtet oder konfiguriert werden muss. Die Ressourcen sind bei Bedarf verfügbar und können in der Regel innerhalb von Minuten oder sogar Sekunden erstellt werden. Sie zahlen nur für die Ressourcen, die Sie verwenden, und nur solange Sie sie verwenden.

Es gibt drei gängige Vorgehensweise zum Ausführen von Compute in Azure:
1. Virtuelle Computer
1. Container
1. Serverloses Computing

## <a name="what-are-virtual-machines"></a>Was sind virtuelle Computer?

Ein **virtueller Computer (VM)** ist eine Softwareemulation eines physischen Computers. Dies umfasst einen virtuellen Prozessor, den Arbeitsspeicher, den Speicher und die Netzwerkressourcen. Sie hosten ein Betriebssystem, und Sie können Software wie auf einem physischen Computer installieren und ausführen. Mithilfe eines Remotedesktopclients können Sie die VM verwenden und steuern, als würden Sie vor einem physischen Computer sitzen.

### <a name="virtual-machines-in-azure"></a>Virtuelle Computer in Azure

Virtuelle Computer (VMs) können in Azure erstellt und gehostet werden. Neue VMs können in der Regel innerhalb von Minuten erstellt und bereitgestellt werden, indem ein Image eines vorkonfigurierten virtuellen Computers ausgewählt wird.

Das Auswählen eines Images ist eine der wichtigsten Entscheidungen, die Sie beim Erstellen einer VM berücksichtigen müssen. Ein Image ist eine Vorlage, die zum Erstellen einer VM verwendet wird. Diese Vorlagen enthalten bereits ein Betriebssystem und häufig auch andere Software, z.B. Entwicklungstools oder Webhostingumgebungen.

## <a name="what-are-containers"></a>Was sind Container?

Container sind eine Virtualisierungsumgebung, die im Gegensatz zu VMs kein Betriebssystem beinhaltet. Stattdessen verweisen sie auf das Betriebssystem der Hostumgebung, in der der Container ausführt wird. Wenn zum Beispiel fünf Container auf einem Server mit einem spezifischen Linux-Kernel ausgeführt werden, werden alle fünf Container auf demselben Kernel ausgeführt. 

Container enthalten in der Regel eine von Ihnen geschriebene Anwendung sowie alle Bibliotheken, die für die Ausführung Ihrer Anwendung auf dem Kernel der Hostumgebung erforderlich sind. 

Container sind kompakt und dafür konzipiert, dynamisch erstellt, hochskaliert und beendet zu werden, damit jede Änderung der Umgebung oder des Bedarfs abgedeckt werden kann.

Die Verwendung von Containern hat den Vorteil, dass mehrere isolierte Anwendungen auf einem virtuellen Computer ausgeführt werden können. Da Container selbst gesichert und isoliert sind, benötigen Sie nicht unbedingt separate VMs für separate Workloads.

Azure unterstützt Docker-Container und mehrere Methoden zum Verwalten dieser Container. Container können manuell oder mit Azure-Diensten wie Azure Kubernetes Service verwaltet werden.

### <a name="what-is-serverless-computing"></a>Was ist serverloses Computing?

Serverloses Computing ist eine in der Cloud gehostete Ausführungsumgebung, die Ihren Code ausführt, die zugrunde liegende Hostumgebung jedoch vollständig abstrahiert. Sie erstellen eine Instanz des Diensts und fügen Ihren Code hinzu. Die Konfiguration oder Wartung der Infrastruktur ist weder erforderlich noch zulässig.

Sie konfigurieren Ihre serverlosen Apps, um auf Ereignisse zu reagieren. Dabei kann es sich um einen REST-Endpunkt, einen Timer oder eine von einem anderen Azure-Dienst empfangene Nachricht handeln. Die serverlose App wird nur ausgeführt, wenn sie durch ein Ereignis ausgelöst wird. 

Für die Infrastruktur sind Sie nicht verantwortlich. Die Skalierung und Leistung wird automatisch verarbeitet. Es werden nur genau die Ressourcen in Rechnung gestellt, die Sie verwenden. Das Reservieren von Kapazität ist nicht notwendig.

Azure verfügt über zwei Implementierungen von serverlosem Computing: **Azure Functions**, womit Code in den meisten modernen Programmiersprachen ausführbar ist, und **Azure Logic Apps**, womit Sie von Azure-Diensten ausgelöste Logik ausführen können, ohne Code schreiben zu müssen.
