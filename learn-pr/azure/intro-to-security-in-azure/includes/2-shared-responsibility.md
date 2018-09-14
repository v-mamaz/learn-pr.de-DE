Mit dem Wandel der Computingumgebungen von kundengesteuerten Rechenzentren zu Cloudrechenzentren verschiebt sich auch die Verantwortung für die Sicherheit. Sicherheit ist jetzt freigegeben werden, sowohl von Cloud-Anbietern und Kunden relevant. Für jede Anwendung und die Projektmappe ist es wichtig zu verstehen, was Ihre Aufgabe ist und was mit Azure für Sie übernimmt. 

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEvj]

## <a name="share-security-responsibility-with-azure"></a>Azure Security Zuständigkeit freigeben

Die erste Schicht liegt zwischen lokalen Datencentern und Infrastruktur als a-Service (IaaS). Bei IaaS, die Sie nutzen den Dienst der untersten Ebene sind und stellen Azure zum Erstellen von virtuellen Computern (VMs) und virtuelle Netzwerke. Auf dieser Ebene ist es immer noch Ihre Aufgabe, Patchen und schützen Ihre Betriebssysteme und Software, sowie konfigurieren Sie Ihr Netzwerk schützen. Versand von Contoso ist nutzen IaaS beim start anstelle von ihren lokalen physischen Servern in Azure-VMs. Zusätzlich zu den Vorteilen operational erhalten sie den Sicherheitsvorteil, dass Problem ausgelagert, über den Schutz der physischen Teile des Netzwerks.

Umstellung auf die Plattform als Dienst lagert (PaaS) viele Sicherheitsrisiken. Auf dieser Ebene ist Azure des Betriebssystems und die meisten grundlegenden Software, z.B. Datenbank-Managementsystemen zuständig. Alles, was mit den neuesten Sicherheitspatches aktualisiert wird und für die Zugriffssteuerung in Azure Active Directory integriert werden kann. PaaS gehört außerdem zahlreiche Vorteile, operational. Anstatt zu ganzen Infrastrukturen und Subnetze für Ihre Umgebungen manuell, Sie "zeigen und klicken Sie auf können" erstellen, das Azure-Portal, oder führen die automatisierte Skripts komplexe, sichere Systeme nach oben oder unten, und diese nach Bedarf skalieren. Versand von Contoso verwendet Azure Event Hubs für die Erfassung von Telemetriedaten aus ihrer Trucks. Sie verwenden außerdem eine Web-app mit einer Azure Cosmos DB-Back-End mit ihren mobilen apps. Diese Dienste sind Beispiele für PaaS.

Mit Software-as-a-Service (SaaS) Lagern Sie nahezu jede Aktion aus. SaaS handelt es sich um Software, die mit einer Internetinfrastruktur ausgeführt wird. Der Code wird gesteuert, die vom Anbieter jedoch so konfiguriert, dass der Kunde verwendet werden. Wie so viele Unternehmen verwendet das Versenden von Contoso Office 365, die ist ein gutes Beispiel SaaS!

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![shared_responsibility.png](../media-COPIED-FROM-DESIGNFORSECURITY/shared_responsibilities.png)

## <a name="a-layered-approach-to-security"></a>Mehrstufiger Sicherheitsansatz

Die *tiefgehende Verteidigung* ist eine Strategie, bei der mithilfe zahlreicher Mechanismen das Ausmaß eines Angriffs gedämpft wird, der darauf abzielt, unberechtigten Zugriff auf Informationen zu erlangen. Jede Ebene bietet Schutz, sodass beim Passieren einer Ebene die nachfolgende Ebene eine weitere Bedrohung verhindert. Microsoft verfolgt einen mehrstufigen Sicherheitsansatz – sowohl in den physischen Rechenzentren als auch für Azure-Dienste. Mehrstufige Verteidigung wird zum Schützen und zu verhindern, dass Informationen aus den Diebstahl von Personen nicht berechtigt sind, darauf zuzugreifen.

Die tiefgehende Verteidigung kann als ein Satz konzentrischer Ringe visualisiert werden, wobei die Daten im Zentrum gesichert werden müssen. Jeder Ring stellt eine zusätzliche Sicherheitsebene für die Daten dar. Dieser Ansatz macht die Abhängigkeit von einer einzelnen Schutzebene überflüssig, verlangsamt einen Angriff und bietet Alarmtelemetrie, auf die automatisch oder manuell reagiert werden kann. Sehen wir uns jede Ebene genauer an.

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![Mehrstufige Verteidigung](../media-COPIED-FROM-DESIGNFORSECURITY/defense_in_depth_layers_small.PNG)

### <a name="data"></a>Daten

In der Regel zielen Angriffe auf folgende Daten ab:

- Daten, die in einer Datenbank gespeichert sind
- Daten, die auf einem Datenträger auf einer VM gespeichert sind
- Klicken Sie auf eine SaaS-Anwendung, z. B. Office 365 gespeicherten Daten
- Daten, die im Cloudspeicher gespeichert sind

Es liegt in der Verantwortung derjenigen, die den Zugriff auf Daten steuern und Daten speichern, sicherzustellen, dass die Daten ordnungsgemäß gesichert sind. Es sind häufig gesetzliche Anforderungen, die vorgeben, die Steuerelemente und Prozesse, die vorhanden, um die Vertraulichkeit, Integrität und Verfügbarkeit der Daten sicherzustellen, dass sein müssen.

### <a name="application"></a>Anwendung

- Stellen Sie sicher, dass Anwendungen sicher und frei von Sicherheitsrisiken sind.
- Store geheime Schlüssel für sensible Anwendungen in einem sicheren Speichermedium.
- Stellen Sie Sicherheit eine Anforderung für die Entwicklung für alle Anwendungen.

Integrieren Sie Sicherheit in den Anwendungsentwicklungszyklus, um die Anzahl der im Code eingeführten Sicherheitsrisiken zu reduzieren. Empfehlen Sie alle Entwicklungsteams sicherstellen, dass ihre Anwendungen standardmäßig sicher sind, und, dass diese sicherheitsanforderungen nicht verhandelbar vornehmen.

### <a name="compute"></a>Compute

- Sichern des Zugriffs auf virtuelle Computer.
- Implementieren von endpointprotection und Systeme geändert wurde und aktuell zu halten.

Durch Malware, nicht gepatchte und nicht ordnungsgemäß gesicherte Systeme kann Ihre Umgebung angegriffen werden. Der Schwerpunkt auf dieser Ebene liegt daran, Sie sicher, dass Ihre Compute-Ressourcen sicher sind, und dass Sie die richtigen Steuerelemente einrichten, um Sicherheitsprobleme zu minimieren.

### <a name="networking"></a>Netzwerk

- Kommunikation zwischen Ressourcen zu beschränken.
- Standardmäßig verweigert.
- Beschränken Sie eingehenden Zugriff auf das Internet und begrenzen, die ausgehende, gegebenenfalls.
- Implementieren Sie sichere Verbindungen mit lokalen Netzwerken.

In dieser Ebene liegt der Schwerpunkt auf, auf die Beschränken der Netzwerkkonnektivität für all Ihre Ressourcen zu ermöglichen, erforderlich sind. Durch die Einschränkung dieser Kommunikation reduzieren Sie das Lateral Movement-Risiko in Ihrem Netzwerk.

### <a name="perimeter"></a>Umkreis

- Verwenden Sie verteilte Denial--Schutz (DDoS), um groß angelegten Angriffen zu filtern, bevor sie einen Denial of Service für Endbenutzer verursachen können.
- Verwenden Sie Umkreisfirewalls zu identifizieren und Warnung für böswillige Angriffe gegen Ihr Netzwerk.

Beim Netzwerkumkreis geht es um den Schutz vor Angriffen auf das Netzwerk und somit auf Ihre Ressourcen. Es ist wichtig, diese Angriffe zu erkennen, zu melden und ihre Folgen zu beseitigen, um Ihr Netzwerk sicher zu halten.

### <a name="policies--access"></a>Richtlinien und Zugriff

- Steuern Sie des Zugriffs auf die Infrastruktur und ändern Sie Steuerelement.
- Einmaliges Anmelden und Multi-Factor-Authentifizierung verwenden.
- Überwachen Sie Ereignisse und Änderungen an.

Die Standardrichtlinien und -Ebene ist alles über Identitäten sichergestellt sind sicher und Zugriff gewährt wird nur die erforderlichen Änderungen werden protokolliert.

### <a name="physical-security"></a>Physische Sicherheit

- Physische Sicherheit erstellen und Steuern des Zugriffs auf die Anforderungen an die Computerhardware innerhalb des Rechenzentrums ist die erste Verteidigungslinie.

Bei der physischen Sicherheit geht es darum, physische Schutzmaßnahmen gegen den Zugriff auf Ressourcen zu treffen. Dadurch wird sichergestellt, dass andere Ebenen nicht umgangen werden, und angemessen mit Verlust oder Diebstahl umgegangen wird.

Wir haben hier zu sehen, dass es sich bei Azure viel mit Ihre Sicherheitsprobleme können. Sicherheit ist immer noch eine **gemeinsame Verantwortung**. Wie viel von diese Verantwortung auf uns fällt, hängt davon ab, welches Modell wir mit Azure verwenden.

Wir verwenden die *Tiefenverteidigung* Ringe als Richtlinie für die in Betracht ziehen, welche Schutzfunktionen für unsere Daten und Umgebungen angemessen sind.