Der Schutz von Netzwerken vor Angriffen und unbefugtem Zugriff ist ein wichtiger Bestandteil jeder Architektur. Hier betrachten wir die Netzwerksicherheit, wie Sie einen mehrstufigen Ansatz in Ihre Architektur integrieren, und wie Sie mit Azure Netzwerksicherheit für Ihre Umgebung gewährleisten.

## <a name="a-layered-approach-to-network-security"></a>Mehrstufiger Netzwerksicherheitsansatz

Ein roter Faden in diesem Modul ist der mehrstufige Sicherheitsansatz – der auch auf Netzwerkebene gilt. Es reicht nicht aus, sich nur der Sicherung des Netzwerkumkreises oder der Netzwerksicherheit zwischen Diensten innerhalb eines Netzwerks zu widmen. Ein mehrstufiger Ansatz bietet mehrere Schutzebenen. Das heißt, wenn ein Angriff eine Ebene passiert, sind weitere Schutzmechanismen vorhanden, um weitere Angriffe einzuschränken.

Sehen wir uns an, wie Azure Tools für einen mehrstufigen Ansatz zur Sicherung Ihres Netzwerks bereitstellen kann.

### <a name="internet-protection"></a>Internetschutz

Wenn wir im Umkreis des Netzwerks beginnen, konzentrieren wir uns darauf, Angriffe aus dem Internet einzuschränken und zu eliminieren. Eine erste gut, ist die Ressourcen zu bewerten, die Internetverbindung, und nur eingehende und ausgehende Kommunikation ermöglichen, bei Bedarf. Identifizieren Sie alle Ressourcen, die eingehenden Netzwerkdatenverkehr jeglicher Art zulassen, und stellen Sie sicher, dass dieser notwendig und auf die erforderlichen Ports/Protokolle beschränkt ist. Azure Security Center ist ein idealer Ausgangspunkt, um weitere Informationen zu suchen, da es sich bei ihn identifizieren Internetzugriff Ressourcen, die keine netzwerksicherheitsgruppen zugeordnet haben, sowie Ressourcen, die nicht hinter einer Firewall geschützt sind.

Zum Schutz von eingehenden im Umkreis bereitstellen zu können, müssen Sie eine Reihe von Optionen an:

* Azure Application Gateway ist ein Lastenausgleichsmodul mit einer Web Application Firewall, mit die Schutz vor häufig, bekannte Schwachstellen stellt.

* Für nicht-HTTP-Services oder erweiterte Konfigurationen verwenden können virtuelle Netzwerkgeräte (NVAs) verwendet werden. NVAs ähneln Hardware Firewallgeräte.


Gefahr eines Angriffs durch ein Denial-of-Service-Angriff ist eine Ressource mit dem Internet verbunden. Bei diesem Angriff wird eine Netzwerkressource überlastet, indem so viele Anforderungen gesendet werden, dass die Ressource langsam oder gar nicht mehr reagiert. Um solche Angriffe zu verringern, bietet Azure DDoS Protection basic Schutz für alle Azure-Dienste und erweiterten Schutz für die weitere Anpassung für Ihre Ressourcen an. Azure DDoS Protection sperrt angriffsdatenverkehr und leitet den verbleibenden Datenverkehr an das vorgesehene Ziel weiter. Innerhalb weniger Minuten nach Angriffserkennung werden Sie über die Metriken von Azure Monitor benachrichtigt.

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![DDoS](../media-COPIED-FROM-DESIGNFORSECURITY/ddos.png)

### <a name="virtual-network-security"></a>Sicherheit in virtuellen Netzwerken

Es ist wichtig, in einem virtuellen Netzwerk (VNET) die Kommunikation zwischen den Ressourcen auf das erforderliche Maß zu beschränken.

Für die Kommunikation zwischen virtuellen Computern sind netzwerksicherheitsgruppen eine wesentliche Komponente aus, um unnötige Kommunikation zu beschränken. Sie geben eine Liste der zulässigen und verweigerten-Kommunikation zu und von Netzwerkschnittstellen und Subnetze und sind vollständig anpassbar.

Sie können öffentlichen Zugriff auf das Internet auf Ihre Dienste vollständig entfernen, durch Einschränken des Zugriffs auf Dienstendpunkte. Mit Dienstendpunkten kann Azure-Dienst den Zugriff auf Ihr virtuelles Netzwerk beschränkt werden.

### <a name="network-integration"></a>Netzwerkintegration

Es ist üblich, vorhandene Netzwerkinfrastruktur verwenden, der für die Kommunikation vom lokalen Netzwerken oder für die verbesserte Kommunikation zwischen Diensten in Azure integriert werden muss. Es gibt einige grundlegende Methoden, diese Integration auszuführen, und die Sicherheit Ihres Netzwerks zu verbessern.

Virtuelle private Netzwerkverbindungen (VPN) sind eine gängige Methode zum Sichern der Kommunikationskanäle zwischen Netzwerken herstellen. Verbindung zwischen virtuellen Azure-Netzwerk und einem lokalen VPN-Gerät ist eine hervorragende Möglichkeit zum Sichern der Kommunikation zwischen Ihrem Netzwerk und das VNet in Azure bereitstellen.

Um eine dedizierte, private Verbindung zwischen Ihrem Netzwerk und Azure bereitstellen, können Sie Azure ExpressRoute verwenden. Mit ExpressRoute können Sie Ihre lokalen Netzwerke über eine private Verbindung, die von einem Konnektivitätsanbieter bereitgestellt wird, auf die Microsoft Cloud ausdehnen. Mit ExpressRoute können Sie Verbindungen zu Microsoft Cloud Services herstellen, z.B. Microsoft Azure, Office 365 und Dynamics 365. Dies verbessert die Sicherheit Ihrer lokalen Kommunikation, indem dieser Datenverkehr über die private Leitung anstatt über das Internet übertragen wird. Sie müssen nicht den Zugriff auf diese Dienste für Ihre Endbenutzer über das Internet zu ermöglichen, und können diesen Datenverkehr über Geräte für die weiteren datenverkehrsüberprüfung senden.

## <a name="summary"></a>Zusammenfassung

Mit einem mehrstufigen Ansatz für Netzwerksicherheit können Sie das Gefährdungsrisiko durch netzwerkbasierte Angriffe reduzieren. Azure bietet mehrere Dienste und-Funktionen für Ihre Ressource mit Internetzugriff, interne Ressourcen und Kommunikation zwischen lokalen Netzwerken zu schützen. Diese Funktionen ermöglichen es, sichere Lösungen in Azure zu erstellen.