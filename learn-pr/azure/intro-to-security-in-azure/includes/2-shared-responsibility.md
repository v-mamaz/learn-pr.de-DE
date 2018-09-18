Mit dem Wandel der Computingumgebungen von vom Kunden gesteuerten Rechenzentren zu Cloudrechenzentren verschiebt sich auch die Verantwortung für die Sicherheit. Sicherheit ist nun ein gemeinsames Anliegen von Cloudanbietern und Kunden. Es ist wichtig, dass Sie für jede Anwendung und Lösung verstehen, wofür Sie selbst verantwortlich sind und welche Aufgaben von Azure für Sie übernommen werden. 

## <a name="share-security-responsibility-with-azure"></a>Gemeinsame Verantwortung für die Sicherheit bei der Zusammenarbeit mit Azure

Die erste Verschiebung erfolgt von lokalen Rechenzentren zu Infrastructure-as-a-Service (IaaS). Mit IaaS nutzen Sie den Dienst der niedrigsten Ebene und fordern von Azure die Erstellung von virtuellen Computern (VMs) und virtuellen Netzwerken an. Auf dieser Ebene sind Sie weiterhin dafür verantwortlich, Ihre Betriebssysteme und Software zu patchen und zu schützen sowie Ihr Netzwerk so zu konfigurieren, dass es sicher ist. Die Mitarbeiter von Contoso Shipping nutzen IaaS, wenn sie damit beginnen, anstelle der lokalen physischen Server die virtuellen Azure-VMs zu nutzen. Zusätzlich zu den betriebsbezogenen Vorteilen kommen sie in den Genuss des sicherheitsbezogenen Vorteils, dass Sie sich nicht mehr um den Schutz der physischen Teile des Netzwerks kümmern müssen.

Mit der Umstellung auf Platform-as-a-Service (PaaS) wird ein Großteil der Sicherheitsrisiken outgesourct. Auf dieser Ebene kümmert sich Azure um das Betriebssystem und die meisten grundlegenden Softwarekomponenten, z.B. Datenbankverwaltungssysteme. Alle Updates mit den aktuellen Sicherheitspatches werden durchgeführt und können für die Zugriffssteuerung in Active Directory integriert werden. Bei PaaS ergeben sich außerdem viele betriebsbezogene Vorteile. Anstatt für Ihre Umgebungen gesamte Infrastrukturen und Subnetze manuell zu erstellen, können Sie im Azure-Portal per Mausklick vorgehen oder automatisierte Skripts ausführen, um komplexe geschützte Systeme hoch- und herunterzufahren und wie gewünscht zu skalieren. Contoso verwendet Event Hubs zum Erfassen von Telemetriedaten für die LKW. Außerdem wird als mobile App eine Web-App mit einem CosmosDb-Back-End eingesetzt. Diese Dienste sind Beispiele für PaaS.

Bei Software-as-a-Service (SaaS) wird nahezu alles outgesourct. SaaS ist eine Software, die über Internetinfrastruktur ausgeführt wird, und der Code wird vom Anbieter gesteuert, aber für die Nutzung durch den Kunden konfiguriert. Wie viele andere Unternehmen auch, nutzt Contoso Office 365. Dies ist ein gutes Beispiel für SaaS!

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![shared_responsibility.png](../media-COPIED-FROM-DESIGNFORSECURITY/shared_responsibilities.png)

## <a name="a-layered-approach-to-security"></a>Mehrstufiger Sicherheitsansatz

Die *tiefgehende Verteidigung* ist eine Strategie, bei der mithilfe zahlreicher Mechanismen das Ausmaß eines Angriffs gedämpft wird, der darauf abzielt, unberechtigten Zugriff auf Informationen zu erlangen. Jede Ebene bietet Schutz, sodass bei einer Sicherheitsverletzung auf einer Ebene die nachfolgende Ebene eine weitere Bedrohung verhindert. Microsoft verfolgt einen mehrstufigen Sicherheitsansatz – sowohl in den physischen Rechenzentren als auch für Azure-Dienste. Im Rahmen der tiefgehenden Verteidigung sollen Informationen geschützt und ihr Diebstahl durch Personen verhindert werden, die keine Zugriffsberechtigung besitzen.

Sie können sich die tiefgehende Verteidigung wie einen Satz mit konzentrischen Ringen vorstellen, wobei die Daten im Zentrum geschützt werden müssen. Jeder Ring stellt eine zusätzliche Sicherheitsebene für die Daten dar. Dieser Ansatz macht die Abhängigkeit von einer einzelnen Schutzebene überflüssig, verlangsamt einen Angriff und bietet Alarmtelemetrie, auf die automatisch oder manuell reagiert werden kann. Sehen wir uns jede Ebene genauer an.

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![Tiefgehende Verteidigung](../media-COPIED-FROM-DESIGNFORSECURITY/defense_in_depth_layers_small.PNG)

### <a name="data"></a>Daten

In der Regel zielen Angriffe auf folgende Daten ab:

- Daten, die in einer Datenbank gespeichert sind
- Daten, die auf einem Datenträger einer VM gespeichert sind
- Daten, die in einer SaaS-Anwendung wie Office 365 gespeichert sind
- Daten, die im Cloudspeicher gespeichert sind

Es liegt in der Verantwortung derjenigen, die den Zugriff auf Daten steuern und Daten speichern, sicherzustellen, dass die Daten ordnungsgemäß geschützt sind. Häufig schreiben gesetzliche Vorgaben die Steuerung und die Prozesse vor, die zur Gewährleistung von Vertraulichkeit, Integrität und Verfügbarkeit von Daten erforderlich sind.

### <a name="applications"></a>Anwendungen

- Stellen Sie sicher, dass Anwendungen sicher vor und frei von Sicherheitsrisiken sind.
- Speichern Sie vertrauliche Anwendungsgeheimnisse auf einem sicheren Speichermedium.
- Machen Sie Sicherheit zu einer Entwurfsanforderung für alle Anwendungsentwicklungen.

Integrieren Sie Sicherheit in den Anwendungsentwicklungszyklus, um die Anzahl der im Code eingeführten Sicherheitsrisiken zu reduzieren. Bestärken Sie alle Entwicklungsteams darin, dafür zu sorgen, dass ihre Anwendungen standardmäßig sicher sind, und dass Sicherheitsanforderungen nicht verhandelbar sind.

### <a name="compute"></a>Compute

- Schützen Sie den Zugriff auf VMs.
- Implementieren Sie Endpoint Protection, und halten Sie alle Systeme immer auf dem neuesten Stand.

Durch Malware, nicht gepatchte und nicht ordnungsgemäß geschützte Systeme ist Ihre Umgebung offen für Angriffe. Der Fokus dieser Ebene liegt darin, dafür zu sorgen, dass Ihre Computeressourcen sicher sind, und die notwendigen Kontrollen eingerichtet sind, um Sicherheitsprobleme zu minimieren.

### <a name="networking"></a>Netzwerk

- Schränken Sie die Kommunikation zwischen Ressourcen ein.
- Verweigern Sie Aktionen standardmäßig.
- Schränken Sie eingehenden und ggf. ausgehenden Zugriff auf das Internet ein.
- Implementieren Sie eine sichere Verbindung mit lokalen Netzwerken.

Der Schwerpunkt dieser Ebene liegt darauf, die Netzwerkkonnektivität für alle Ressourcen einzuschränken, um nur das zu ermöglichen, was erforderlich ist. Durch die Einschränkung dieser Kommunikation reduzieren Sie das Lateral Movement-Risiko in Ihrem Netzwerk.

### <a name="perimeter"></a>Umkreis

- Aktivieren Sie einen Schutz vor verteilten Denial-of-Service-Angriffen (DDoS), um umfangreiche Angriffe zu filtern, bevor es zu einem Denial-of-Service bei Endbenutzern kommt.
- Verwenden Sie Umkreisfirewalls, um böswillige Angriffe auf Ihr Netzwerk zu erkennen und zu melden.

Beim Netzwerkumkreis geht es um den Schutz vor Angriffen auf das Netzwerk und somit auf Ihre Ressourcen. Es ist wichtig, diese Angriffe zu erkennen, zu melden und ihre Folgen zu beseitigen, um Ihr Netzwerk sicher zu halten.

### <a name="policies--access"></a>Richtlinien und Zugriff

- Steuern Sie den Zugriff auf die Infrastruktur, und ändern Sie ggf. Kontrollen.
- Verwenden Sie einmaliges Anmelden und mehrstufige Authentifizierung.
- Überwachen Sie Ereignisse und Änderungen.

Bei der Ebene „Richtlinien und Zugriff“ geht es darum, die Sicherheit von Identitäten zu gewährleisten, nur erforderlichen Zugriff zu gewähren, und Änderungen zu protokollieren.

### <a name="physical-security"></a>Physische Sicherheit

- Die physische Gebäudesicherheit und die Steuerung des Zugriffs auf Computerhardware im Rechenzentrum ist die erste Verteidigungslinie.

Bei der physischen Sicherheit geht es darum, physische Schutzmaßnahmen gegen den Zugriff auf Ressourcen zu treffen. Dadurch wird sichergestellt, dass andere Ebenen nicht umgangen werden und angemessen auf Verlust oder Diebstahl reagiert wird.

Wir haben gesehen, dass Azure eine Hilfe für viele Ihrer Sicherheitsprobleme darstellt. Die Sicherheit ist aber weiterhin eine **gemeinsame Aufgabe**, für die beide Seiten verantwortlich sind. Wie hoch hierbei unser Anteil an der Verantwortung ist, hängt davon ab, welches Modell wir in Bezug auf Azure verwenden.

Wir nutzen die *Tiefgehende Verteidigung* als Richtlinie, um zu ermitteln, welche Schutzmaßnahmen für unsere Daten und Umgebungen geeignet sind.