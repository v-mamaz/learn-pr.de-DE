Es wurde gezeigt, wie Sie Kostenschätzungen für geplante Umgebungen erstellen können, wir haben einige Tools untersucht, um genauere Informationen darüber zu erhalten, wo Kosten entstehen, und es wurden zukünftige Ausgaben geplant. Die nächste Herausforderung besteht darin, zu ermitteln, wie diese Infrastrukturkosten gesenkt werden können.

## <a name="use-reserved-instances"></a>Verwenden reservierter Instanzen

Wenn Ihre VM-Workloads – insbesondere diejenigen, die rund um die Uhr und das ganze Jahr ausgeführt werden – statisch und vorhersagbar sind, ist die Verwendung reservierter Instanzen eine gute Möglichkeit, je nach VM-Größe Einsparungen zwischen 70 und 80 % Prozent zu erzielen. Die folgende Abbildung zeigt, dass Sie mithilfe von reservierten Azure-Instanzen bis zu 72 % und mithilfe von reservierten Instanzen inklusive des Azure-Hybridvorteils bis zu 80 % Ihrer Kosten einsparen können.

![Illustration mit Kostenvorteilen bei der Verwendung von reservierten Azure-Instanzen und der Azure-Hybridvorteile im Vergleich zur nutzungsbasierten Zahlung.](../media-drafts/4-savings-coins.png)

Reservierte Instanzen werden für eine Laufzeit von ein oder drei Jahren erworben. Hierbei müssen die Gebühren für die gesamte Laufzeit vorab entrichtet werden. Nach dem Erwerb gleicht Microsoft die Reservierung mit den ausgeführten Instanzen ab und zieht die Betriebsstunden von Ihrer Reservierung ab. Reservierungen können über das Azure-Portal erworben werden. Da reservierte Instanzen einen Rabatt auf Computeressourcen bieten, sind sie sowohl für Windows- als auch für Linux-VMs verfügbar.

## <a name="right-size-underutilized-virtual-machines"></a>Ändern der Größe von wenig genutzten virtuellen Computern

Zuvor wurde besprochen, dass Azure Cost Management und Azure Advisor möglicherweise empfehlen, die Größe von VMs zu ändern oder VMs herunterzufahren. Bei der richtigen Dimensionierung einer VM wird deren Größe entsprechend angepasst. Angenommen, Sie führen einen Server als Domänencontroller aus, der auf die Größe **Standard_D4sv3** festgelegt ist, aber Ihre VM befindet sich fast immer zu 90 % im Leerlauf. Indem Sie die Größe dieser VM in **Standard_D2sv3** ändern, verringern Sie Ihre Computekosten um 50 %. Die Kosten sind linear und verdoppeln sich für jede nächsthöhere Größe innerhalb derselben Serie. In diesem Fall ist es möglicherweise sogar vorteilhaft, die Instanzserie zu ändern und auf eine kostengünstigere VM-Serie umzustellen. Die folgende Abbildung zeigt Einsparungen in Höhe von 50 %, die durch die Umstellung auf die nächstniedrigere Größe innerhalb der Serie erzielt wurden.

![Illustration zur Veranschaulichung der Einsparungen, die für eine unterdurchschnittlich ausgelastete VM durch die Umstellung auf die nächstniedrigere Größe erzielt wurden.](../media-drafts/4-vm-resize.png)

Überdimensionierte VMs sind eine häufige Ursache für unnötige Kosten in Azure, die aber schnell behoben werden kann. Sie können die Größe einer VM über das Azure-Portal, Azure PowerShell oder die Azure CLI ändern.

> [!NOTE]
> Um die Größe einer VM zu ändern, müssen Sie sie beenden, ihre Größe ändern und die VM dann neu starten. Dieser Vorgang kann abhängig davon, wie umfassend die Größenänderung ist, einige Minuten in Anspruch nehmen. Planen Sie eine Downtime, oder leiten Sie Ihren Datenverkehr auf eine andere Instanz um, während Sie diese Aufgabe ausführen.

## <a name="deallocate-virtual-machines-in-off-hours"></a>Aufheben der Zuordnung virtueller Computer außerhalb der Geschäftszeiten

Wenn Sie über VM-Workloads verfügen, die nur zu bestimmten Zeiten verwendet werden, aber den ganzen Tag ausgeführt werden, erzeugt dies unnötig Kosten. Diese VMs sind hervorragende Kandidaten für das Herunterfahren bei Nichtbenutzung und das Wiedereinschalten nach einem Zeitplan. So sparen Sie Computekosten, während die Zuordnung der VMs aufgehoben ist.

Dieser Ansatz ist besonders für Entwicklungsumgebungen geeignet. Häufig erfolgt die Entwicklung nur während der Geschäftszeiten, sodass Sie die Zuordnung dieser Systeme außerhalb der Geschäftszeiten aufheben können, um unnötige Computekosten zu vermeiden. Azure bietet ab sofort eine [Automatisierungslösung](https://docs.microsoft.com/azure/automation/automation-solution-vm-management), die Sie in Ihrer Umgebung nutzen können.

Sie können auch das Feature zum automatischen Herunterfahren einer VM verwenden, um eine automatisierte Abschaltung zu planen.

![Automatisches Herunterfahren](../media-drafts/4-vm-auto-shutdown.png)

## <a name="delete-unused-virtual-machines"></a>Löschen nicht verwendeter virtueller Computer 

 Diese Empfehlung mag offensichtlich klingen, aber wenn Sie einen Dienst nicht verwenden, sollten Sie ihn ausschalten. Es ist nicht ungewöhnlich, dass im Anschluss an ein Projekt Nicht-Produktionssysteme oder Proof of Concept-Systeme beibehalten werden, obwohl diese nicht mehr benötigt werden. Überprüfen Sie Ihre Umgebung regelmäßig, und identifizieren Sie diese Systeme. Das Herunterfahren dieser Systeme kann in vielfältiger Weise zu Einsparungen beitragen – nicht nur in Bezug auf die Infrastrukturkosten, sondern auch bei den Kosten für Lizenzierung und Betrieb.

## <a name="migrate-to-paas-or-saas-services"></a>Migration zu PaaS- oder SaaS-Diensten 

Wenn Sie schließlich Ihre Workloads in die Cloud verlagern, beginnen Sie üblicherweise mit IaaS-Diensten (Infrastructure-as-a-Service) und wechseln in einem iterativen Prozess zu PaaS (Platform-as-a-Service).

PaaS-Dienste bieten typischerweise erhebliche Einsparungen im Hinblick auf die Ressourcen- und die Betriebskosten. Die Herausforderung besteht darin, dass die Umstellung auf diese Dienste je nach Diensttyp mit einem unterschiedlichen Zeit- und Ressourcenaufwand einhergeht. Die Umstellung einer SQL Server-Datenbank auf Azure SQL-Datenbank ist möglicherweise einfach, der Aufwand für das Verlagern einer mehrstufigen Anwendung in eine Container- oder serverlose Architektur kann hingegen erheblich sein. Es hat sich bewährt, durch eine fortlaufende Auswertung der Architektur Ihrer Anwendungen zu ermitteln, ob über PaaS-Dienste eine positive Wirkung erzielt werden kann.  

Dank Azure ist es einfach, diese Dienste mit geringem Risiko zu testen, sodass Sie neue Architekturmuster relativ einfach ausprobieren können. Gleichwohl ist dies in der Regel ein längerer Prozess, der möglicherweise keine sofortigen Vorteile bietet, wenn Sie schnelle Kosteneinsparungen erzielen möchten. Das Azure Architecture Center ist der ideale Ort, um Ideen für die Transformation Ihrer Anwendung sowie Best Practices für eine große Auswahl von Architekturen und Azure-Diensten zu erhalten. 