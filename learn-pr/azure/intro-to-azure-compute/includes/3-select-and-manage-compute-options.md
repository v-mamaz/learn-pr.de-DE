Nachdem Sie nun in die verfügbaren Azure-Computedienste eingeführt wurden, sollen diese einzeln erläutert werden, damit Sie entscheiden können, wann welcher Dienst verwendet werden soll.

## <a name="azure-virtual-machines"></a>Azure Virtual Machines

Wenn die vollständige Kontrolle über das Betriebssystem und die Umgebung erforderlich ist, sind virtuelle Computer eine optimale Wahl. Sie können die Software auf dem virtuellen Computer genau wie bei einem physischen Computer anpassen. Diese Methode ist optimal, wenn Sie benutzerdefinierte Software oder benutzerdefinierte Hostingkonfigurationen ausführen.

Virtuelle Computer sind ebenfalls eine gute Wahl, wenn Sie Verschiebungen von einem physischen Server in die Cloud vornehmen. Häufig können Sie ein Image des physischen Servers erstellen und dieses auf einem virtuellen Computer hosten. Dadurch können Sie die Betriebssysteme und die Ausführungsumgebungen von Anwendungen frei wählen. Das bedeutet, dass Sie in fast jeder Sprache entwickeln können, die in den Tools Ihrer Wahl verwendet werden kann.

Sie müssen den virtuellen Computer jedoch verwalten. Das bedeutet, dass sie das Betriebssystem und die ausgeführte Software aktualisieren müssen. 

Für die Skalierung müssen außerdem weitere Überlegungen angestellt werden. Sie können den virtuellen Computer hochskalieren. Das bedeutet, dass Sie weitere Compute- und Arbeitsspeicherressourcen hinzufügen können. Wenn Sie jedoch mehrere Instanzen parallel ausführen müssen, müssen Sie ggf. weitere Dienste wie Load Balancer hinzufügen.

Angenommen, Sie betreiben eine Website, die eine Website für den Einzelhandel hostet. Wenn Sie den virtuellen Computer duplizieren würden, wäre ein zusätzlicher Dienst erforderlich, um Anforderungen zwischen mehreren Instanzen des virtuellen Computers für die Website weiterzuleiten.

In Azure sind außerdem erweiterte Dienste für virtuelle Computer verfügbar:

* Verwenden Sie die Option **Virtual Machine Scale Sets**, um durchgängig verfügbare Instanzen derselben App(s) auf ähnlich konfigurierten virtuellen Computern auszuführen. Diese Option generiert automatisch Tausende von identischen virtuellen Computern, die in Minuten mit Ihrer Anwendung zusammen geladen werden, damit Ihre Benutzer nicht warten müssen. Da für virtuelle Computer keine Vorabbereitstellung erforderlich ist, verwenden Sie immer nur die Computeressourcen, die Ihre Anwendung benötigt.

* Es können sich Situationen ergeben, in denen Sie sehr viel Computeleistung bzw. die Computeleistung eines Supercomputers benötigen. Die **Batch**-Option stellt die Skalierung der Auftragsplanung und Computeverwaltung in der Cloud mit der Möglichkeit bereit, sogar Tausende von virtuellen Computern zu skalieren. Sie können sogar virtuelle Computer mit den Funktionen von Supercomputern angeben.

## <a name="azure-containers"></a>Azure-Container

Container sind eine gute Wahl, wenn Sie mehrere Instanzen einer Anwendung auf einem einzelnen virtuellen Computer ausführen möchten. Der Containerorchestrator kann Anwendungsinstanzen nach Bedarf starten, beenden oder hochskalieren.

Container werden jedoch üblicherweise dazu verwendet, Lösungen mithilfe einer Microservicearchitektur zu erstellen. Container werden häufig verwendet, um Lösungen in kleinere Bestandteile aufzuteilen. Sie können eine Website beispielsweise in einen Container aufteilen, der Ihr Front-End hostet, einen weiteren, der Ihr Back-End hostet, und einen dritten für den Speicher. Dadurch können Sie einzelne Bestandteile Ihrer App in logische Abschnitte aufteilen, die unabhängig voneinander verwaltet, skaliert oder aktualisiert werden können.

Angenommen, das Back-End Ihrer Website hat die maximale Kapazität erreicht, aber das Front-End und der Speicher werden nicht beansprucht. Sie könnten das Back-End einzeln skalieren, um die Leistung zu verbessern. Alternativ könnten Sie einen anderen Speicherdienst verwenden. Eine weitere Möglichkeit wäre das Ersetzen des Speichercontainers ohne die restliche Anwendung zu beeinträchtigen.

 Wenn Ihr Team mit der Verwendung der Kubernetes-Containerorchestrierung vertraut ist, können Sie die Option **Azure Kubernetes Service (AKS)** verwenden. Diese Option vereinfacht und automatisiert die Verwaltung, Bereitstellung und Vorgänge der Kubernetes-Orchestrierung.

## <a name="azure-functions"></a>Azure-Funktionen

Azure-Funktionen sind optimal geeignet, wenn Sie nur den Code berücksichtigen müssen, der Ihren Dienst ausführt, nicht aber die zugrunde liegende Plattform oder Infrastruktur. Sie werden üblicherweise verwendet, wenn Sie Aufgaben als Reaktion auf ein Ereignis durchführen müssen, das häufig über eine REST-Anforderung, einen Timer oder eine Meldung von einem anderen Azure-Dienst ausgelöst wird, und wenn diese Aufgaben schnell (innerhalb von Sekunden oder noch schneller) ausgeführt werden können.

Azure-Funktionen werden automatisch skaliert und sind deshalb eine gute Wahl, wenn der Bedarf variiert. Es werden nur Gebühren berechnet, wenn eine Funktion ausgelöst wird. Sie können beispielsweise Meldungen von einer IoT-Lösung erhalten, die verwendet wird, um mehrere Lieferfahrzeuge zu überwachen. Während der Geschäftszeiten gehen wahrscheinlich mehr Daten ein.

Azure-Funktionen sind zustandslos. Sie verhalten Sich bei jeder Reaktion auf ein Ereignis so, als wären sie neu gestartet worden. Für das Verarbeiten von eingehenden Daten ist dieses Verhalten optimal. Wenn ein Zustand erforderlich ist, können die Funktionen mit einem Azure-Speicherdienst verbunden werden.
