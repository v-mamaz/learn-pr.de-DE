Nachdem Sie sich nun mit den verfügbaren Azure-Computediensten vertraut gemacht haben, sollen diese einzeln näher erläutert werden, damit Sie entscheiden können, wann welcher Dienst verwendet werden soll.

## <a name="azure-virtual-machines"></a>Virtuelle Azure-Computer

:::row:::
  :::column:::
    ![Bild eines virtuellen Azure-Computers](../media/3-azure-vms.png)
  :::column-end:::
  :::column span="3"::: Wenn die vollständige Kontrolle über das Betriebssystem und die Umgebung erforderlich ist, sind virtuelle Computer eine optimale Wahl. Sie können die Software auf dem virtuellen Computer genau wie bei einem physischen Computer anpassen. Diese Methode ist optimal, wenn Sie benutzerdefinierte Software oder benutzerdefinierte Hostingkonfigurationen ausführen.
  :::column-end:::
:::row-end:::

Virtuelle Computer sind ebenfalls eine gute Wahl, wenn Sie Verschiebungen von einem physischen Server in die Cloud vornehmen. Häufig können Sie ein Image des physischen Servers erstellen und dieses auf einem virtuellen Computer hosten. Dadurch können Sie die Betriebssysteme und die Ausführungsumgebungen von Anwendungen frei wählen. Das bedeutet, dass Sie in fast jeder Sprache entwickeln können, die in den Tools Ihrer Wahl verwendet werden kann.

Sie müssen den virtuellen Computer jedoch verwalten. Das bedeutet, dass sie das Betriebssystem und die ausgeführte Software aktualisieren müssen. 

Für die Skalierung müssen außerdem weitere Überlegungen angestellt werden. Sie können den virtuellen Computer hochskalieren. Dies bedeutet, dass Sie weitere Compute- und Arbeitsspeicherressourcen hinzufügen können. Wenn Sie aber mehrere Instanzen parallel ausführen oder horizontal hochskalieren möchten, müssen Sie ggf. weitere Dienste hinzufügen, z.B. einen Lastenausgleich.

Angenommen, Sie führen eine Website aus, mit der Wissenschaftler astronomische Bilder hochladen können, die verarbeitet werden müssen. Wenn Sie den virtuellen Computer duplizieren, ist ein zusätzlicher Dienst erforderlich, um Anforderungen zwischen mehreren Instanzen des virtuellen Computers für die Website weiterzuleiten.

In Azure sind außerdem erweiterte Dienste für virtuelle Computer verfügbar:

- Verwenden Sie die Option **Virtual Machine Scale Sets**, wenn Sie durchgängig verfügbare Instanzen derselben App(s) auf ähnlich konfigurierten virtuellen Computern ausführen müssen. Diese Option generiert automatisch Tausende von identischen virtuellen Computern, die innerhalb weniger Minuten mit Ihrer Anwendung zusammen geladen werden, damit Ihre Benutzer nicht warten müssen. Da für virtuelle Computer keine Vorabbereitstellung erforderlich ist, verwenden Sie immer nur die Computeressourcen, die Ihre Anwendung benötigt.

- Verwenden Sie die Option **Batch**, wenn Sie die Skalierung der Auftragsplanung und Computeverwaltung in der Cloud mit der Möglichkeit benötigen, eine Skalierung auf Dutzende, Hunderte oder Tausende von virtuellen Computern durchzuführen. Es können sich Situationen ergeben, in denen Sie sehr viel Computeleistung bzw. die Computeleistung eines Supercomputers benötigen. Diese Funktionen können über Azure bereitgestellt werden.

## <a name="azure-containers"></a>Azure-Container

:::row:::
  :::column:::
    ![Bild von Azure-Containern](../media/3-azure-containers.png)
  :::column-end:::
  :::column span="3"::: Container eignen sich ausgezeichnet, wenn Sie mehrere Instanzen einer Anwendung auf einem einzelnen virtuellen Computer ausführen möchten. Der Containerorchestrator kann Anwendungsinstanzen nach Bedarf starten, beenden oder horizontal hochskalieren.
  :::column-end:::
:::row-end:::

#### <a name="what-are-containers"></a>Was sind Container?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yMhY]

#### <a name="vms-versus-containers"></a>Vergleich von virtuellen Computern und Containern

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yuaq]

Container dienen aber üblicherweise dazu, Lösungen mithilfe einer Microservicearchitektur zu erstellen. Container werden häufig verwendet, um mithilfe einer Microservicearchitektur Lösungen zu erstellen, da sie das Unterteilen von Lösungen in kleinere Teile ermöglichen. Sie können eine Website beispielsweise in einen Container aufteilen, der Ihr Front-End hostet, einen weiteren, der Ihr Back-End hostet, und einen dritten für den Speicher. Dadurch können Sie einzelne Bestandteile Ihrer App in logische Abschnitte aufteilen, die unabhängig voneinander verwaltet, skaliert oder aktualisiert werden können.

#### <a name="what-is-a-microservice"></a>Was ist ein Microservice?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yual]

Angenommen, das Back-End Ihrer Website hat die maximale Kapazität erreicht, aber das Front-End und der Speicher werden nicht beansprucht. Sie sollten das Back-End dann separat skalieren, um die Leistung zu verbessern, oder Sie können sich für die Nutzung eines anderen Speicherdiensts entscheiden. Eine weitere Möglichkeit wäre sogar das Ersetzen des Speichercontainers ohne Beeinträchtigung der restlichen Anwendung.

Wenn Ihr Team mit der Verwendung der Kubernetes-Containerorchestrierung vertraut ist, können Sie die Option **Azure Kubernetes Service (AKS)** verwenden. Diese Option vereinfacht und automatisiert die Verwaltung, Bereitstellung und Vorgänge der Kubernetes-Orchestrierung.

#### <a name="what-is-kubernetes"></a>Was ist Kubernetes?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEuX]

## <a name="azure-functions"></a>Azure-Funktionen

:::row:::
  :::column:::
    ![Bild von Azure-Funktionen](../media/3-azure-functions.png)
  :::column-end:::
  :::column span="3"::: Azure-Funktionen sind optimal geeignet, wenn Sie nur den Code berücksichtigen müssen, der Ihren Dienst ausführt, nicht aber die zugrunde liegende Plattform oder Infrastruktur. Sie werden in der Regel verwendet, wenn Aufgaben als Reaktion auf ein Ereignis durchgeführt werden müssen, das häufig über eine REST-Anforderung, einen Timer oder eine Meldung von einem anderen Azure-Dienst ausgelöst wird, und wenn diese Aufgaben schnell (innerhalb von Sekunden oder noch schneller) ausgeführt werden können.
  :::column-end:::
:::row-end:::

Azure-Funktionen werden automatisch skaliert und sind deshalb eine gute Wahl, wenn der Bedarf variiert. Es werden nur Gebühren berechnet, wenn eine Funktion ausgelöst wird. Sie können beispielsweise Meldungen von einer IoT-Lösung erhalten, die verwendet wird, um mehrere Lieferfahrzeuge zu überwachen. Während der Geschäftszeiten gehen wahrscheinlich mehr Daten ein.

Darüber hinaus sind Azure-Funktionen zustandslos. Sie verhalten sich bei jeder Reaktion auf ein Ereignis so, als wären sie neu gestartet worden. Für das Verarbeiten von eingehenden Daten ist dieses Verhalten optimal. Wenn ein Zustand erforderlich ist, können die Funktionen mit einem Azure-Speicherdienst verbunden werden.
