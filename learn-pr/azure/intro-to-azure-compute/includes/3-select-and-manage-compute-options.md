Nun, dass Sie eingeführt wurden, haben in der Azure compute-Dienste verfügbar sind, näher an jedem helfen Ihnen die Entscheidung, wann jeder Dienst verwendet.

## <a name="azure-virtual-machines"></a>Azure Virtual Machines

Wenn Sie vollständige Kontrolle über das Betriebssystem und die Umgebung benötigen, sind virtuelle Computer eine ideale Option. Sie können die Software auf dem virtuellen Computer genau wie bei einem physischen Computer anpassen. Dies ist vor allem ideal, bei der Ausführung von benutzerdefinierten Software oder benutzerdefinierte Konfigurationen hosten.

Virtuelle Computer sind ebenfalls eine gute Wahl, wenn Sie von physischen Servern auf die Cloud umsteigen möchten. Häufig können Sie ein Image des physischen Servers erstellen und dieses auf einem virtuellen Computer hosten. Dadurch können Sie die Betriebssysteme und die Ausführungsumgebungen von Anwendungen frei wählen. Das bedeutet, dass Sie in fast jeder Sprache entwickeln können, die in den Tools Ihrer Wahl verwendet werden kann.

Sie müssen den virtuellen Computer jedoch verwalten. Das bedeutet, dass Sie das Betriebssystem und die ausgeführte Software aktualisieren müssen. 

Bei einer Skalierung müssen außerdem weitere Überlegungen angestellt werden. Sie können den virtuellen Computer hochskalieren. Das bedeutet, dass Sie weitere Compute- und Arbeitsspeicherressourcen hinzufügen können. Aber wenn Sie mehrere Instanzen Parallel oder horizontales hochskalieren ausgeführt werden müssen, müssen Sie möglicherweise zusätzliche Dienste wie Load balancer hinzufügen.

Also: Angenommen Sie, dass Sie eine Website ausführen, die es ermöglicht datenspezialisten Astronomie Images hochladen, die verarbeitet werden müssen. Wenn Sie den virtuellen Computer dupliziert, müssten Sie einen zusätzlichen Dienst zum Weiterleiten von Anforderungen zwischen mehreren Instanzen der VM-Website.

In Azure sind außerdem erweiterte Dienste für virtuelle Computer verfügbar:

- Verwenden der **Virtual Machine Scale Sets** -Option, wenn Sie durchgängig verfügbar sind, Instanzen der gleichen app oder Mengen von apps, auf ähnliche Weise ausführen möchten, konfiguriert virtuelle Computer. Diese Option generiert automatisch Tausende von identischen virtuellen Computern, die innerhalb weniger Minuten mit Ihrer Anwendung zusammen geladen werden, damit Ihre Benutzer nicht warten müssen. Da für virtuelle Computer keine Vorabbereitstellung erforderlich ist, verwenden Sie immer nur die Computeressourcen, die Ihre Anwendung benötigt.

- Verwenden der **Batch** option cloudebene auftragsplanung und computeverwaltung mit der Möglichkeit, Dutzende, Hunderte oder Tausende von VMs zu skalieren. Es gibt möglicherweise Situationen, in dem Sie unformatierten rechenleistung benötigen, oder Supercomputer-Ebene der computeleistung &mdash; Azure die Bereitstellung dieser Funktionen.

## <a name="azure-containers"></a>Azure-Container

Wenn Sie mehrere Instanzen einer Anwendung auf einem einzelnen virtuellen Computer ausführen möchten, sind Container eine hervorragende Wahl. Der Containerorchestrator kann Anwendungsinstanzen nach Bedarf starten, beenden oder horizontal hochskalieren.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yMhY]

Sie können möglicherweise nicht offensichtlich auf den ersten Was ist der Unterschied zwischen einem virtuellen Computer und Container.  Das folgende Video versucht zur Erläuterung der Unterschiede.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yuaq]

Container dienen jedoch üblicherweise dazu, mithilfe einer Microservicesarchitektur Lösungen zu erstellen. Container werden häufig verwendet, um mithilfe einer microservicearchitektur, Lösungen zu erstellen, wie sie häufig verwendet werden, um Lösungen in kleinere Teile aufteilen. Sie können z. B. eine Website in einem Container hosten Ihre Front-End, eine andere Hosten Ihrer Back-End und eine dritte für den Speicher aufgeteilt. Dadurch können Sie einzelne Bestandteile Ihrer App in logische Abschnitte aufteilen, die unabhängig voneinander verwaltet, skaliert oder aktualisiert werden können.

Versucht, dass im folgende Video wird erläutert, welche ein Microservice ist.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yual]

Angenommen Sie, Ihre Website-Back-End hat die Kapazität erreicht, aber die Front-End und Speicher werden nicht erstellt werden. Können Sie das Back-End getrennt, zur Verbesserung der Leistung skalieren, oder Sie könnten einen anderen Storage-Dienst verwenden. Oder Sie können auch den Storage-Container ersetzen, ohne den Rest der Anwendung.

Wenn Ihr Team mit der Verwendung der Kubernetes-Containerorchestrierung vertraut ist, können Sie die Option **Azure Kubernetes Service (AKS)** verwenden. Diese Option vereinfacht und automatisiert Verwaltung, Bereitstellung und Vorgänge der Kubernetes-Orchestrierung.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEuX]

## <a name="azure-functions"></a>Azure-Funktionen

Azure-Funktionen eignen sich ideal, wenn Sie nur den Code, der mit Ihrem Dienst und nicht die zugrunde liegenden Plattform oder die Infrastruktur Gedanken. Sie werden üblicherweise verwendet, wenn Sie Aufgaben als Reaktion auf ein Ereignis durchführen müssen, das häufig über eine REST-Anforderung, einen Timer oder eine Meldung von einem anderen Azure-Dienst ausgelöst wird, und wenn diese Aufgaben schnell (innerhalb von Sekunden oder noch schneller) ausgeführt werden können.

Azure Functions skalieren automatisch auf, und diese sind eine solide Wahl, wenn Sie bei Bedarf ist Variable aus, und Sie sind nur berechnet, wenn eine Funktion ausgelöst wird. Sie können beispielsweise Meldungen von einer IoT-Lösung erhalten, die verwendet wird, um mehrere Lieferfahrzeuge zu überwachen. Während der Geschäftszeiten gehen wahrscheinlich mehr Daten ein.

Darüber hinaus sind die Azure Functions statusfrei; Sie verhält, als ob sie neu gestartet haben, jedes Mal, wenn sie auf ein Ereignis reagieren. Für das Verarbeiten von eingehenden Daten ist dieses Verhalten optimal. Wenn ein Zustand erforderlich ist, können die Funktionen mit einem Azure Storage-Dienst verbunden werden.
