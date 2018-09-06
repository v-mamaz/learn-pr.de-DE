Nur selten können wir die Last auf unserem System genau vorhersagen: Öffentliche Anwendungen können schnell wachsen, oder eine interne Anwendung muss möglicherweise eine größere Benutzerbasis unterstützen, da das Unternehmen wächst. Und selbst wenn wir die Last vorhersagen können, ist diese nur selten gleichbleibend hoch: Einzelhändler haben vor den Feiertagen einen höheren Bedarf, während es bei Sportwebseiten bei Spitzenspielen zu Spitzenlasten kommt. In dieser Einheit werden wir uns eingehend mit dem _zentralen Hochskalieren/Herunterskalieren_ und dem _horizontalen Hochskalieren/Herunterskalieren_ befassen. Außerdem werden wir einige Methoden kennenlernen, wie Azure Ihre Skalierfunktionen verbessern kann und wie serverlose Technologien und Containertechnologien die Skalierfähigkeit Ihrer Architektur steigern können.

## <a name="what-is-scaling"></a>Was versteht man unter Skalierung?

_Skalierung_ bezeichnet den Prozess zum Verwalten Ihrer Ressourcen, damit Ihre Anwendung eine Reihe von Leistungsanforderungen erfüllt.  Wenn zu viele Ressourcen für die Benutzer vorhanden sind, werden diese Ressourcen nicht effizient eingesetzt und wir verschwenden Geld. Nicht genügend verfügbare Ressourcen bedeuten hingegen, dass die Leistung unserer Anwendung beeinträchtigt werden könnte. Ziel ist es, unsere definierten Leistungsanforderungen zu erfüllen und gleichzeitig die Kosten zu optimieren. 

„_Ressourcen_“ kann sich auf alles beziehen, was wir verwalten müssen, damit unsere Anwendungen ausgeführt werden können. Arbeitsspeicher und CPU für virtuelle Computer (VM) sind die offensichtlichsten Ressourcen, für einige Azure-Dienste müssen Sie aber möglicherweise auch die Bandbreite oder Abstraktionen wie Cosmos DB-Anforderungseinheiten berücksichtigen.

In einer Welt mit einem konstanten Anwendungsbedarf lässt sich der erforderliche Ressourcenbedarf gut vorhersagen. In der realen Welt ändern sich die Anforderungen unserer Anwendungen im Laufe der Zeit, was Vorhersagen erschweren kann. Wenn Sie Glück haben, sind diese Änderungen vorhersehbar oder saisonal, aber dies trifft nicht auf alle Anwendungen zu. Im Idealfall möchten Sie die richtige Menge an Ressourcen bereitstellen, um die Nachfrage zu erfüllen, und bei Bedarfsänderungen Anpassungen vornehmen.

Eine Skalierung ist bei einem lokalen Szenario, in dem Sie Ihre eigenen Server erwerben und verwalten, schwierig. Das Hinzufügen von Ressourcen kann kostspielig sein, und häufig dauert es zu lange, bis diese online gehen – manchmal sogar länger, als der tatsächliche Bedarf an der erhöhten Kapazität besteht. Anschließend ist es unter Umständen ähnlich schwierig, in Zeiten mit geringem Bedarf im System die Kapazität zu verringern, sodass Sie möglicherweise auf den höheren Kosten sitzen bleiben.

Ein zentraler Vorteil von Azure ist die einfache Skalierung. Die meisten Azure-Ressourcen können Sie problemlos mit dem sich verändernden Bedarf hinzufügen oder entfernen, und viele Dienste verfügen über automatische Optionen, die den Bedarf für Sie überwachen und anpassen. Diese Funktion der automatischen Skalierung ermöglicht es Ihnen, Schwellenwerte für die Mindest- und Höchstverfügbarkeit von Instanzen festzulegen, und übernimmt das Hinzufügen bzw. Entfernen von Instanzen auf Grundlage einer Leistungsmetrik (beispielsweise der CPU-Auslastung).

## <a name="what-is-scaling-up-and-down"></a>Was bedeutet Hoch- oder Herunterskalieren?

Hochskalieren bezeichnet den Prozess, mit dem wir die Kapazität einer bestimmten Instanz erhöhen. Ein virtueller Computer könnte von 1 vCPU und 3,5 GB RAM auf 2 vCPUs und 7 GB RAM hochgestuft werden, um mehr Verarbeitungskapazität zu bieten. Herunterskalieren bezeichnet im Umkehrschluss den Prozess, bei dem die Kapazität einer bestimmten Instanz reduziert wird. Dies bedeutet beispielsweise, die Kapazität eines virtuellen Computers von 2 vCPUs und 7 GB RAM auf 1 vCPU und 3,5 GB RAM zu verringern, was neben der Kapazität auch die Kosten reduziert.

![Hoch-/Herunterskalieren](../media/ScaleUpDown.png)

Sehen wir uns nun einmal an, was Hoch- bzw. Herunterskalieren im Kontext von Azure-Ressourcen bedeutet:

* Bei virtuellen Azure-Computern erfolgt die Skalierung anhand der Größe eines virtuellen Computers. Zu dieser Größe gehören eine bestimmte Menge von zugeordneten vCPUs sowie eine bestimmte Menge von RAM und lokalem Speicher. Wir könnten beispielsweise einen virtuellen Computer mit Standard_DS1_v2 (1 vCPU und 3,5 GB RAM) auf einen virtuellen Computer mit Standard_DS2_v2 (2 vCPUs und 7 GB RAM) hochskalieren.
* Azure SQL-Datenbank ist eine Paas-Implementierung (Platform-as-a-Service) von Microsoft SQL Server.  Sie können eine Datenbank anhand der Zahl der Datenbanktransaktionseinheiten (DTUs) oder vCPUs hochskalieren. DTUs sind eine Abstraktion der zugrunde liegenden Ressourcen und eine Mischung aus CPU, E/A und Arbeitsspeicher. Sie könnten Ihre Datenbankinstanz von 500 DTUs auf 250 DTUs skalieren.
* Azure App Service ist ein PaaS-Websitehostingdienst in Azure. Websites werden auf einer virtuellen Serverfarm ausgeführt, die auch als App Service-Plan bezeichnet wird. Sie können den App Service-Plan zwischen Tarifen hoch- und herunterskalieren und verfügen innerhalb der Tarife über verschiedene Kapazitätsoptionen. Ein S1-App Service-Plan verfügt beispielsweise über 1 vCPU und 1,75 GB RAM pro Instanz. Wir könnten ihn auf einen S2-App Service-Plan hochskalieren, der 2 vCPUs und 3 GB RAM pro Instanz bietet.

Um in einer lokalen Umgebung über diese Fähigkeit zu verfügen, müssten Sie üblicherweise auf die Beschaffung der erforderlichen Hardware und deren Installation warten, bevor Sie die neue Skalierungsstufe verwenden könnten. In Azure sind die physischen Ressourcen bereits bereitgestellt und für Sie verfügbar. Sie müssen lediglich die neue Skalierungsstufe auswählen, die Sie verwenden möchten.

Möglicherweise müssen Sie die Auswirkungen der Hochskalierung in Ihrer Lösung berücksichtigen, die von den Clouddiensten abhängen, die Sie ausgewählt haben.

Wenn Sie beispielsweise in einer Azure SQL-Datenbank hochskalieren möchten, skaliert der Dienst einzelne Knoten hoch und setzt den Betrieb Ihres Dienstes fort. Wenn Sie die Dienst- und/oder Leistungsstufe einer Datenbank ändern, wird ein Replikat der ursprünglichen Datenbank auf der neuen Leistungsebene erstellt, und anschließend werden die Verbindungen auf dieses Replikat umgeschaltet. Während dieses Vorgangs gehen keine Daten verloren, und es kommt nur zu einer kurzen Unterbrechung (in der Regel von weniger als vier Sekunden), wenn der Dienst auf das Replikat umgeschaltet wird.

Wenn Sie hingegen auswählen, einen virtuellen Computer hoch- oder herunterzuskalieren, wählen Sie dazu eine andere Instanzgröße aus. In den meisten Fällen erfordert dies einen Neustart des virtuellen Computers. Rechnen Sie also sicherheitshalber damit, dass ein Neustart erforderlich ist und Sie diesen bei der Durchführung dieser Aktivität berücksichtigen müssen.

Und schließlich sollten Sie stets prüfen, ob stellenweise auch Herunterskalieren eine Option darstellt. Wenn Ihre Anwendung eine angemessene Leistung auf einer niedrigeren Tarifstufe bereitstellen kann, könnte Ihre Azure-Rechnung erheblich günstiger ausfallen.

## <a name="what-is-scaling-out-and-in"></a>Was ist horizontales Hoch- und Herunterskalieren?

Während beim Hoch- und Herunterskalieren die Menge der verfügbaren Ressourcen einer einzelnen Instanz angepasst wird, wird beim horizontalen Hoch- und Herunterskalieren die Gesamtzahl der Instanzen angepasst.

_Horizontales Hochskalieren_ bezeichnet den Prozess, mit dem weitere Instanzen hinzugefügt werden, um die Last Ihrer Lösung aufzufangen. Wenn beispielsweise Ihr Website-Front-End auf virtuellen Computern gehostet wurde, ließe sich die Zahl der virtuellen Computer erhöhen, wenn die Last zunimmt.

_Horizontales Herunterskalieren_ bezeichnet den Prozess, mit dem Instanzen entfernt werden, die nicht mehr benötigt werden, um die Last Ihrer Lösung aufzufangen. Wenn die Website-Front-Ends nur wenig genutzt werden, ist es unter Umständen sinnvoll, die Zahl der Instanzen zu verringern, um Kosten zu sparen.


![Horizontales Hoch-/Herunterskalieren](../media/ScaleInOut.png)

Nachfolgend werden einige Beispiele für horizontales Hoch- und Herunterskalieren im Kontext von Azure-Ressourcen aufgeführt:

* Für die Infrastrukturebene würden wahrscheinlich VM-Skalierungsgruppen verwendet, um das Hinzufügen und Entfernen zusätzlicher Instanzen zu automatisieren.
  * Mit VM-Skalierungsgruppen können Sie eine Gruppe von identischen virtuellen Computern mit Lastenausgleich erstellen und verwalten.
  * Die Anzahl der VM-Instanzen kann automatisch erhöht oder verringert werden, wenn sich der Bedarf ändert, oder es kann ein Zeitplan festgelegt werden.
* In einer Azure SQL-Datenbankimplementierung können Sie die Last für Datenbankinstanzen durch horizontales Partitionieren teilen. Mit _Sharding_ (horizontales Partitionieren) werden große Mengen identisch strukturierter Daten auf mehrere unabhängige Datenbanken verteilt.
* In Azure App Service handelt es sich beim App Service-Plan um die virtuelle Webserverfarm, die Ihren Inhalt hostet. Ein solches horizontales Hochskalieren bedeutet, dass Sie die Zahl der virtuellen Computer in der Farm erhöhen. Wie bei VM-Skalierungsgruppen kann die Zahl der Instanzen automatisch anhand bestimmter Metriken oder eines Zeitplans erhöht oder gesenkt werden.

Horizontales Hochskalieren erfolgt in der Regel ganz einfach im Azure-Portal, in Befehlszeilentools oder Resource Manager-Vorlagen, und in den meisten Fällen erfolgt dieses Hochskalieren für den Endbenutzer nahtlos.

### <a name="autoscale"></a>Automatische Skalierung

Sie können einige dieser Dienste so konfigurieren, dass sie eine Funktion namens automatische Skalierung verwenden. Bei der automatischen Skalierung müssen Sie sich nicht mehr um das manuelle Skalieren von Diensten kümmern. Stattdessen können Sie einen minimalen und maximalen Schwellenwert von Instanzen und eine Skalierung basierend auf bestimmten Metriken (Länge der Warteschlange, CPU-Auslastung) oder Zeitplänen (Mo-Fr 17:00 Uhr bis 19:00 Uhr) festlegen.

![Automatische Skalierung](../media/autoscale.png)

### <a name="considerations-when-scaling-in-and-out"></a>Überlegungen zum horizontalen Hoch- und Herunterskalieren

Beim horizontalen Hochskalieren kann sich die Startzeit Ihrer Anwendung darauf auswirken, wie schnell Ihre Anwendung skaliert werden kann. Wenn Ihre Web-App zwei Minuten benötigt, um gestartet zu werden und für Benutzer zur Verfügung zu stehen, bedeutet dies, dass jede Ihrer Instanzen zwei Minuten benötigt, bis sie Ihren Benutzern zur Verfügung steht. Sie sollten diese Startzeit berücksichtigen, wenn Sie festlegen, wie schnell Sie skalieren möchten.

Sie müssen ferner überlegen, wie Ihre Anwendung Status behandelt. Wenn die Anwendung horizontal herunterskaliert wird, sind auf einem Computer gespeicherte Status nicht mehr verfügbar. Wenn ein Benutzer eine Verbindung zu einer Instanz herstellt, die seinen Status nicht kennt, könnte er gezwungen werden, sich anzumelden oder erneut Daten auszuwählen, was die Benutzerfreundlichkeit beeinträchtigen würde. Ein gängiges Muster besteht darin, Status an einen anderen Dienst wie Redis Cache oder SQL-Datenbank auszulagern, wodurch Ihre Webserver statusfrei werden. Wenn Ihre Web-Front-Ends nun statusfrei sind, ist es nicht mehr relevant, welche individuellen Instanzen verfügbar sind. Alle Instanzen führen denselben Auftrag aus und werden auf die gleiche Weise bereitgestellt.

## <a name="throttling"></a>Drosselung

Wir haben bereits festgestellt, dass die Last einer Anwendung im Laufe der Zeit variieren kann. Dies kann auf die Zahl der aktiven oder gleichzeitigen Benutzer und die ausgeführten Aktivitäten zurückzuführen sein. Wir könnten die automatische Skalierung verwenden, um Kapazität hinzuzufügen. Wir können jedoch auch einen Drosselungsmechanismus verwenden, um die Zahl der Anforderungen von einer Quelle zu beschränken. Sie können die Leistungsgrenzwerte schützen, indem Sie bekannte Einschränkungen auf Anwendungsebene festlegen, die die Anwendung vor Ausfällen bewahrt. Die Drosselung wird hauptsächlich bei Anwendungen verwendet, die API-Endpunkte verfügbar zu machen.

Nachdem die Anwendung festgestellt hat, dass sie einen Grenzwert überschreiten würde, kann mit der Drosselung begonnen werden, und es wird sichergestellt, dass nicht gegen die Gesamtsystem-SLA verstoßen wird. Wenn wir eine API für Kunden zum Abrufen von Daten verfügbar machen, könnten wir beispielsweise die Anzahl der Anforderungen auf 100 pro Minute begrenzen. Sobald ein einzelner Kunde diese Grenze überschritten hat, könnten wir mit einem HTTP 429-Statuscode antworten und dabei die Wartezeit angeben, bis eine weitere Anforderung erfolgreich übermittelt werden kann.

## <a name="serverless"></a>Serverlos

Serverloses Computing stellt eine in der Cloud gehostete Ausführungsumgebung bereit, die Ihre Apps ausführt, die zugrunde liegende Umgebung jedoch vollständig abstrahiert. Sie erstellen eine Instanz des Dienstes und fügen Ihren Code hinzu. Die Verwaltung oder Wartung der Infrastruktur ist weder erforderlich noch zulässig.

Sie konfigurieren Ihre serverlosen Apps, um auf Ereignisse zu reagieren. Dabei kann es sich um einen REST-Endpunkt, einen Timer oder eine von einem anderen Azure-Dienst empfangene Nachricht handeln. Die serverlose App wird nur ausgeführt, wenn sie durch ein Ereignis ausgelöst wird.

Für die Infrastruktur sind Sie nicht verantwortlich. Die Skalierung und Leistung wird automatisch verarbeitet. Es werden nur genau die Ressourcen in Rechnung gestellt, die Sie verwenden. Das Reservieren von Kapazität ist nicht notwendig. Azure Functions, Azure Container Instances und Logic Apps sind Beispiele für in Azure verfügbares serverloses Computing.

Sehen wir uns nochmals das Beispiel von Lamna Healthcare an. Dort gibt es möglicherweise ein gewisses Potenzial für Kosteneinsparungen und die Vereinfachung der Verwaltung. Betrachten wir einen API-Endpunkt. Anstatt die API in Azure App Service zu hosten, wo für reservierte Kapazität gezahlt werden muss, könnte der Kunde stattdessen eine Azure-Funktionen-App verwenden, die durch eine HTTP-Anforderung ausgelöst wird. Azure-Funktionen würden es dem Team erlauben, nur für die Ressourcen zu zahlen, die für die Verarbeitung der einzelnen Transaktionen benötigt werden. Die Kosten und die Skalierung würden genau der Zahl der Transaktionen im System entsprechen.

## <a name="containers"></a>Container

Ein Container ist eine Methode, um Anwendungen in einer virtualisierten Umgebung auszuführen. Ein virtueller Computer wird auf Hardwareebene virtualisiert, wo es ein Hypervisor erlaubt, mehrere virtualisierte Betriebssysteme auf einem einzelnen physischen Server auszuführen. Container verbessern die Virtualisierung, denn sie erfolgt auf der Betriebssystemebene, wodurch es möglich wird, mehrere identische Anwendungsinstanzen in demselben Betriebssystem auszuführen.

Container eignen sich gut für Skalierungsszenarios. Sie sind kompakt und dafür konzipiert, dynamisch erstellt, hochskaliert und beendet zu werden, wenn sich die Umgebung oder der Bedarf verändert.

Die Verwendung von Containern hat den Vorteil, dass auf jedem einzelnen virtuellen Computer mehrere isolierte Anwendungen ausgeführt werden können. Da Container selbst gesichert und auf Kernelebene isoliert sind, benötigen Sie nicht unbedingt separate VMs für separate Workloads.

Zwar können Sie Container auf virtuellen Computern ausführen, es gibt jedoch eine Reihe von Azure-Diensten, die die Verwaltung und Skalierung von Containern vereinfachen:

* **Azure Kubernetes Service (AKS)**

  Mit Azure Kubernetes Service können Sie virtuelle Computer einrichten, die als Ihre Knoten fungieren. Azure hostet die Kubernetes-Verwaltungsebene und berechnet nur die ausgeführten Workerknoten, die Ihre Container hosten.

  Um die Zahl Ihrer Workerknoten in Azure zu erhöhen, könnten Sie die Azure CLI verwenden, um diese Erhöhung manuell vorzunehmen. Zum Redaktionszeitpunkt ist eine Vorschau von Cluster Autoscaler auf AKS verfügbar, welcher die automatische Skalierung Ihrer Workerknoten ermöglicht. In Ihrem Kubernetes-Cluster können Sie den Horizontal Pod Autoscaler verwenden, um die Zahl der Instanzen des bereitzustellenden Containers horizontal hochzuskalieren.

  AKS können auch mit dem unten beschriebenen Virtual Kubelet skaliert werden.

* **Azure Container Instances (ACI)**
  
  Azure Container Instances ist ein serverloser Ansatz, mit dem Sie Container bei Bedarf erstellen und ausführen können. Nur die Ausführungszeit pro Sekunde wird Ihnen in Rechnung gestellt.

  Sie können Virtual Kubelet verwenden, um Azure Container Instances mit Ihrer Kubernetes-Umgebung zu verbinden, einschließlich AKS. Wenn bei Virtual Kubelet Ihr Kubernetes-Cluster zusätzliche Containerinstanzen anfordert, kann dieser Bedarf von ACI erfüllt werden. Da ACI serverlos sind, muss keine Kapazität reserviert werden. Sie können somit die Kontrolle und Flexibilität der Kubernetes-Skalierung mit der sekundenbasierten Abrechnung des serverlosen Konzepts nutzen. Zum Redaktionszeitpunkt fällt das Virtual Kubelet unter die experimentelle Software und sollte daher nicht in Produktionsszenarios verwendet werden.

## <a name="scaling-at-lamna-healthcare"></a>Skalierung bei Lamna Healthcare

Lamna Healthcare betreibt ein Patientenverwaltungs- und -buchungssystem. Das Verwaltungssystem wird für Terminbuchungen und Patientendatensätze in Dutzenden von Krankenhäusern und medizinischen Einrichtungen verwendet. Der lokale Gesundheitsdienst arbeitet mit voller Kapazität, und gegenwärtig wird mit keinem Wachstum gerechnet. Das System wird auf einer PHP-Website ausgeführt, die in Azure App Service gehostet wird.

Das Auslastungsmuster der Anwendung ist vorhersehbar, da sie hauptsächlich von Montag bis Freitag zwischen 9 Uhr und 17 Uhr verwendet wird.  Von Dienstag bis Freitag führt das System durchschnittlich im gesamten System 1.200 Transaktionen pro Stunde aus. Am Wochenende verarbeitet es 500 Transaktionen pro Stunde. Nach dem ruhigen Wochenende fallen an Montagen hingegen durchschnittlich 2.000 Transaktionen pro Stunde an.

Die Anwendung wird auf einem S1-App Service-Plan gehostet, aber das Betriebsteam hat eine hohe CPU-Auslastung (über 95 %) bei allen Instanzen festgestellt. Die hohe Auslastung hat Auswirkungen auf die Verarbeitungs- und Ladezeiten der Anwendung. In einer Cloudumgebung ist eine hohe Auslastung von Ressourcen nicht unbedingt etwas Schlechtes. Es bedeutet vielmehr, dass die bereitgestellten Ressourcen ihr Geld wert sind, da sie gut genutzt werden. 

Das Team entscheidet sich, den App Service-Plan für die bereitgestellten Instanzen von S1 (1 vCPU und 1,75 GB RAM) auf S2 (2 vCPUs und 3 GB RAM) _hochzuskalieren_. Dies lässt sich mit dem Azure-Portal problemlos realisieren. Dasselbe Ergebnis ließe sich jedoch auch mit einem einzigen Befehl in der Azure CLI, Azure PowerShell oder mithilfe von Resource Manager-Vorlagen erzielen.

Das Team beschließt, dass es die Zahl der bereitgestellten Instanzen basierend auf einem Zeitplan automatisieren möchte, da das Auslastungsprofil vorhersagbar ist. Es konfiguriert den Zeitplan für die automatische Skalierung des App Service-Plans. Nehmen wir einmal an, dass zwei Instanzen 500 Transaktionen pro Stunde angemessen verarbeiten können. Das Team könnte dann eine Skalierung auf sechs Instanzen von Dienstag bis Freitag und auf acht Instanzen an Montagen vornehmen, um die Anforderungen (basierend auf den Erfahrungen und einer Überwachung in Form von Auslastungstests) zu erfüllen.

Die automatische Skalierung bietet dem Team außerdem einen zusätzlichen Vorteil, da Vorsorge für unvorhergesehene Szenarios getroffen wird. Auf der Site könnte es plötzlich am Wochenende zu einer Auslastung kommen, die höher ist als erwartet (mehr Termine im Winter aufgrund von Erkältungen und Grippeerkrankungen). Das Team kann die automatische Skalierung so einrichten, dass eine Erhöhung um eine Instanz erfolgt, wenn die CPU-Auslastung mehr als 90 % beträgt, und eine Reduzierung um eine Instanz erfolgt, wenn die Auslastung unter 15 % beträgt.

Das Team hat somit das Drosselungsmuster in der API für Patientenbuchungen verwendet, das es hinter einer Azure API Management-Instanz verfügbar gemacht hat. So wird eine schwache Systemleistung verhindert, indem nur ein bestimmtes Durchsatzvolumen im System erlaubt wird.

## <a name="summary"></a>Zusammenfassung

Wir haben das zentrale und das horizontale Hoch- und Herunterskalieren behandelt und gelernt, wie Sie diese Optionen in Ihrer Architektur nutzen können. Wir haben ferner erfahren, wie serverlose Technologien und Container Ihre Skalierungsmöglichkeiten weiter verbessern können. Als Nächstes werden wir sehen, wie sich die Leistung des Netzwerks auf Ihre Anwendung auswirken kann, und verschiedene Möglichkeiten der Netzwerkoptimierung kennenlernen.