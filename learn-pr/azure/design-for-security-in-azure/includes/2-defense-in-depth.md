Die Sicherheitsfrage lässt sich nicht auf Knopfdruck lösen, und es gibt keine Universallösung für alle Sicherheitsprobleme. Angenommen, Lamna Healthcare hat die Sicherheit in seiner Umgebung vernachlässigt. Das Unternehmen hat erkannt, dass es sich unbedingt um diesen Bereich kümmern muss. Lamna weiß aber nicht so recht, wo man anfangen soll – oder ob man nicht einfach eine Lösung kaufen kann, um die Umgebung sicher zu machen. Das Unternehmen ist sich bewusst, dass es einen ganzheitlichen Ansatz benötigt, weiß aber nicht genau, was das bedeutet. Hier werden wir die wichtigsten Konzepte der Verteidigung in der Tiefe identifizieren, Schlüsselsicherheitstechnologien und Ansätze zur Unterstützung einer Strategie zur Verteidigung in der Tiefe ermitteln und erörtern, wie Sie diese Konzepte auf die Architektur Ihrer eigenen Azure-Dienste anwenden können.

#### <a name="defense-in-depth"></a>Verteidigung in der Tiefe

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWjTfZ]

## <a name="a-layered-approach-to-security"></a>Mehrstufiger Sicherheitsansatz

Die *tiefgehende Verteidigung* ist eine Strategie, bei der mithilfe zahlreicher Mechanismen das Ausmaß eines Angriffs gedämpft wird, der darauf abzielt, unberechtigten Zugriff auf Informationen zu erlangen. Jede Ebene bietet Schutz, sodass beim Passieren einer Ebene die nachfolgende Ebene eine weitere Bedrohung verhindert. Microsoft verfolgt einen mehrstufigen Sicherheitsansatz – sowohl in den physischen Rechenzentren als auch für Azure-Dienste. Im Rahmen der Verteidigung in der Tiefe sollen Informationen geschützt und ihr Diebstahl durch Personen verhindert werden, die nicht für den Zugriff berechtigt sind. Die allgemeinen Prinzipien, die zur Definition eines Sicherheitsstatus herangezogen werden, sind Vertraulichkeit, Integrität und Verfügbarkeit.

- __Vertraulichkeit__: Prinzip der geringsten Rechte. Beschränkt den Zugriff auf Informationen auf Personen, denen der Zugriff explizit gewährt wird. Dies dient dem Schutz von Informationen wie Benutzerkennwörtern, Remotezugriffszertifikaten und E-Mail-Inhalten.

- __Integrität__: Verhinderung unbefugter Änderungen an Informationen im Ruhezustand oder bei der Übertragung. Ein gängiger Ansatz bei der Datenübertragung ist, dass der Absender einen eindeutigen Fingerabdruck der Daten mithilfe einer unidirektionalen Hashfunktion erstellt. Der Hash wird zusammen mit den Daten an den Empfänger gesendet. Der Hash der Daten wird vom Empfänger neu berechnet und mit dem Original verglichen, um sicherzustellen, dass die Daten beim Übertragen nicht verloren gegangen sind oder verändert wurden.

- __Verfügbarkeit__: Gewährleisten der Dienstverfügbarkeit für autorisierte Benutzer. Denial-of-Service-Angriffe sind eine weit verbreitete Ursache dafür, dass die Verfügbarkeit für die Benutzer verloren geht. Um für Naturkatastrophen gewappnet zu sein, wird beim Systemdesign darauf geachtet, Single Points of Failure zu vermeiden und mehrere Instanzen einer Anwendung an geografisch verteilten Standorten bereitzustellen.

## <a name="security-layers"></a>Sicherheitsebenen

Die Verteidigung in der Tiefe kann als eine Gruppe konzentrischer Ringe visualisiert werden, wobei die Daten im Zentrum geschützt werden müssen. Jeder Ring stellt eine zusätzliche Sicherheitsebene für die Daten dar. Dieser Ansatz macht die Abhängigkeit von einer einzelnen Schutzebene überflüssig, verlangsamt einen Angriff und bietet Alarmtelemetrie, auf die automatisch oder manuell reagiert werden kann. Sehen wir uns die einzelnen Ebenen einmal genauer an.

![Abbildung der Verteidigung in der Tiefe mit Daten im Mittelpunkt. Die Daten werden durch folgende Sicherheitsringe geschützt: Anwendung, Compute, Netzwerk, Umgebung, Identität und Zugriff sowie physische Sicherheit.](../media/defense_in_depth_layers_small.PNG)

### <a name="data"></a>Daten

In der Regel zielen Angriffe auf folgende Daten ab:

- Daten, die in einer Datenbank gespeichert sind
- Daten, die auf einem Datenträger eines virtuellen Computers gespeichert sind
- Daten, die in einer SaaS-Anwendung wie Office 365 gespeichert sind
- Daten, die im Cloudspeicher gespeichert sind

Es liegt in der Verantwortung derjenigen, die den Zugriff auf Daten steuern und Daten speichern, dafür zu sorgen, dass die Daten ordnungsgemäß geschützt sind. Häufig schreiben gesetzliche Vorgaben die Steuerung und die Prozesse vor, die zur Gewährleistung von Vertraulichkeit, Integrität und Verfügbarkeit von Daten erforderlich sind.

### <a name="applications"></a>Anwendungen

- Stellen Sie sicher, dass Anwendungen sicher vor und frei von Sicherheitsrisiken sind.
- Speichern Sie vertrauliche Anwendungsgeheimnisse auf einem sicheren Speichermedium.
- Machen Sie Sicherheit zu einer Entwurfsanforderung für alle Anwendungsentwicklungen.

Integrieren Sie Sicherheit in den Anwendungsentwicklungszyklus, um die Anzahl von Sicherheitsrisiken im Code zu verringern. Bestärken Sie alle Entwicklungsteams darin, dafür zu sorgen, dass ihre Anwendungen standardmäßig sicher sind. Sicherheitsanforderungen sind nicht verhandelbar.

### <a name="compute"></a>Compute

- Schützen Sie den Zugriff auf VMs.
- Implementieren Sie Endpoint Protection, und halten Sie alle Systeme immer auf dem neuesten Stand.

Schadsoftware sowie nicht gepatchte oder nicht ordnungsgemäß geschützte Systeme machen Ihre Umgebung anfällig für Angriffe. Der Fokus dieser Ebene liegt darin, dafür zu sorgen, dass Ihre Computeressourcen sicher und die notwendigen Kontrollen eingerichtet sind, um Sicherheitsprobleme zu minimieren.

### <a name="networking"></a>Netzwerk

- Schränken Sie die Kommunikation zwischen Ressourcen mittels Segmentierung und Zugriffssteuerung ein.
- Verweigern Sie den Zugriff standardmäßig.
- Schränken Sie eingehenden und ggf. ausgehenden Zugriff auf das Internet ein.
- Implementieren Sie eine sichere Verbindung mit lokalen Netzwerken.

Der Schwerpunkt dieser Ebene liegt darauf, die Netzwerkkonnektivität für alle Ressourcen einzuschränken, um nur das zu ermöglichen, was erforderlich ist. Segmentieren Sie Ihre Ressourcen, und verwenden Sie Steuerungen auf Netzwerkebene, um die Kommunikation auf das erforderliche Maß zu beschränken. Durch die Einschränkung dieser Kommunikation verringern Sie das Lateral Movement-Risiko in Ihrem Netzwerk.

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

Bei der physischen Sicherheit geht es darum, physische Schutzmaßnahmen gegen den Zugriff auf Ressourcen zu treffen. Dadurch wird sichergestellt, dass andere Ebenen nicht umgangen werden, und angemessen auf Verlust oder Diebstahl reagiert wird.

Jede Ebene bezieht sich auf mindestens eines der Schutzziele Vertraulichkeit, Verfügbarkeit oder Integrität.

|#|Ring|Beispiel|Prinzip
|---|---|---|---|
|1|Daten|Verschlüsselung ruhender Daten in Azure Blob Storage|Integrität|
|2|Anwendung|Mit SSL/TLS verschlüsselte Sitzungen|Integrität|
|3|Compute|Regelmäßiges Aufspielen von Betriebssystem- und mehrstufigen Softwarepatches|Verfügbarkeit|
|4|Netzwerk|Netzwerksicherheitsregeln|Vertraulichkeit|
|5|Umkreis|DDoS-Schutz|Verfügbarkeit|
|6|Richtlinien und Zugriff|Azure Active Directory-Benutzerauthentifizierung|Integrität|
|7|Physische Sicherheit|Biometrische Zugriffssteuerung für Azure-Rechenzentren|Vertraulichkeit|

## <a name="shared-responsibilities"></a>Gemeinsame Verantwortung

Mit dem Wandel der Computingumgebungen von vom Kunden gesteuerten Rechenzentren zu Cloudrechenzentren verschiebt sich auch die Verantwortung für die Sicherheit. Sicherheit ist nun ein gemeinsames Anliegen von Cloudanbietern und Kunden.

![Abbildung, die zeigt, wie sich Cloudanbieter und Kunden Sicherheitsaufgaben unter verschiedenen Arten von Computedienstimplementierung teilen: lokal, Infrastructure-as-a-Service, Platform-as-a-Service und Software-as-a-Service. ](../media/shared_responsibilities.png)

## <a name="continuous-improvement"></a>Ständige Verbesserung

Es entstehen sehr schnell und in großem Umfang immer wieder neue Bedrohungen, sodass keine Sicherheitsarchitektur je vollständig ist. Microsoft und seine Kunden müssen auf intelligente, schnelle und umfassende Weise auf diese Bedrohungen reagieren können.

[Azure Security Center](https://azure.microsoft.com/services/security-center/) bietet Kunden eine einheitliche Sicherheitsverwaltung und erweiterten Bedrohungsschutz, um Sicherheitsereignisse – sowohl lokale als auch in Azure – verstehen und darauf reagieren zu können. Im Gegenzug haben Azure-Kunden die Verantwortung, ihre Sicherheitsarchitektur ständig neu zu bewerten und zu entwickeln.

## <a name="defense-in-depth-at-lamna-healthcare"></a>Verteidigung in der Tiefe bei Lamna Healthcare

Lamna Healthcare hat in allen IT-Teams einen starken Fokus auf die Verteidigung in der Tiefe gelegt. Da die Organisation für eine enorme Menge an vertraulichen Gesundheitsdaten verantwortlich ist, hat sie sich für einen umfassenden Ansatz entschieden. 

Ein neu gebildetes virtuelles Team, das aus Vertretern der einzelnen IT-Teams und dem Sicherheitsteam besteht, arbeitet daran, diese Verteidigungsstrategie in der gesamten Organisation durchzusetzen. Entwickler und Architekten werden im Hinblick auf Sicherheitsrisiken geschult, Problemlösungen aufgezeigt und Hilfestellung geboten, wenn Projekte innerhalb der Organisation weitergeleitet werden.

Lamna Healthcare hat erkannt, dass man nie zu 100 Prozent geschützt sein kann, und führt regelmäßig Prüfungen der Richtlinien, Prozesse, Technik und Architektur durch, um die Sicherheit kontinuierlich zu verbessern.

## <a name="summary"></a>Zusammenfassung

Es wurde erläutert, wie ein auf der Verteidigung in der Tiefe basierender Sicherheitsansatz aussieht, was die einzelnen Ebenen ausmacht und worauf jeweils der Fokus liegt. Wenn Sie diesen Sicherheitsansatz für Ihre Architektur verwenden, sind Sie auf dem richtigen Weg, die Sicherheit in Ihrer Umgebung umfassend anzugehen und konzentrieren sich nicht nur auf eine einzige Ebene oder Technologie.