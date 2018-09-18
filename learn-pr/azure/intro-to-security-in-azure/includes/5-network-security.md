Der Schutz von Netzwerken vor Angriffen und unbefugtem Zugriff ist ein wichtiger Bestandteil jeder Architektur. Hier betrachten wir die Netzwerksicherheit, wie Sie einen mehrstufigen Ansatz in Ihre Architektur integrieren, und wie Sie mit Azure Netzwerksicherheit für Ihre Umgebung gewährleisten.

## <a name="a-layered-approach-to-network-security"></a>Mehrstufiger Netzwerksicherheitsansatz

Ein roter Faden in diesem Modul ist der mehrstufige Sicherheitsansatz – der auch auf Netzwerkebene gilt. Es reicht nicht aus, sich nur der Sicherung des Netzwerkumkreises oder der Netzwerksicherheit zwischen Diensten innerhalb eines Netzwerks zu widmen. Ein mehrstufiger Ansatz bietet mehrere Schutzebenen. Das heißt, wenn ein Angriff eine Ebene passiert, sind weitere Schutzmechanismen vorhanden, um weitere Angriffe einzuschränken.

Sehen wir uns an, wie Azure Tools für einen mehrstufigen Ansatz zur Sicherung Ihres Netzwerks bereitstellen kann.

### <a name="internet-protection"></a>Internetschutz

Wenn wir im Umkreis des Netzwerks beginnen, konzentrieren wir uns darauf, Angriffe aus dem Internet einzuschränken und zu eliminieren. Ein guter Ausgangspunkt ist, die Ressourcen zu bewerten, mit denen das Internet konfrontiert ist, und ein- und ausgehende Kommunikation nur dann zu erlauben, wenn sie erforderlich ist. Identifizieren Sie alle Ressourcen, die eingehenden Netzwerkdatenverkehr jeglicher Art zulassen, und stellen Sie sicher, dass dieser notwendig und auf die erforderlichen Ports/Protokolle beschränkt ist. Das Azure Security Center eignet sich hervorragend, um nach diesen Informationen zu suchen, da es Internetressourcen identifiziert, denen keine Netzwerksicherheitsgruppen (NSG) zugeordnet sind, sowie Ressourcen, die nicht hinter einer Firewall gesichert sind.

Es gibt mehrere Möglichkeiten, Schutz für eingehenden Datenverkehr im Umkreis zu gewährleisten:

* Bei Application Gateway handelt es sich um einen Lastenausgleich, der eine Webanwendungsfirewall enthält, die Schutz vor allgemein bekannten Sicherheitslücken bietet.

* Für Nicht-HTTP-Dienste oder erweiterte Konfigurationen können virtuelle Netzwerkgeräte (Network Virtual Appliances, NVAs) verwendet werden. NVAs ähneln Hardwarefirewallgeräten.


Für alle Ressourcen, die im Internet zur Verfügung stehen, besteht die Gefahr eines Denial-of-Service-Angriffs. Bei diesem Angriff wird eine Netzwerkressource überlastet, indem so viele Anforderungen gesendet werden, dass die Ressource langsam oder gar nicht mehr reagiert. Damit diese Angriffe abgewehrt werden können, bietet Azure DDoS einen Basisschutz für alle Azure-Dienste und einen erweiterten Schutz für weitere Anpassungen Ihrer Ressourcen. DDoS Protection sperrt Angriffsdatenverkehr und leitet den verbleibenden Datenverkehr an das vorgesehene Ziel weiter. Innerhalb weniger Minuten nach Angriffserkennung werden Sie mithilfe der Metriken von Azure Monitor benachrichtigt.

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![DDoS](../media-COPIED-FROM-DESIGNFORSECURITY/ddos.png)

### <a name="virtual-network-security"></a>Sicherheit in virtuellen Netzwerken

Es ist wichtig, in einem virtuellen Netzwerk (VNET) die Kommunikation zwischen den Ressourcen auf das erforderliche Maß zu beschränken.

Bei der Kommunikation zwischen VMs spielen Netzwerksicherheitsgruppen (NSGs) eine wichtige Rolle, um unnötige Kommunikation zu verhindern. Sie stellen eine Liste der zulässigen und verweigerten Kommunikation von und zu Netzwerkschnittstellen und Subnetzen bereit und können vollständig angepasst.

Sie können den öffentlichen Zugriff durch das Internet auf Ihre Dienste vollständig entfernen, indem Sie den Zugriff auf Dienstendpunkte beschränken. Mit Dienstendpunkten kann der Zugriff von Azure-Diensten auf Ihr virtuelles Netzwerk beschränkt werden.

### <a name="network-integration"></a>Netzwerkintegration

Es ist üblich, dass eine vorhandene Netzwerkinfrastruktur integriert werden soll, um die Kommunikation aus lokalen Netzwerken zu ermöglichen, oder um eine verbesserte Kommunikation zwischen den Diensten in Azure zu ermöglichen. Es gibt einige grundlegende Methoden, diese Integration auszuführen, und die Sicherheit Ihres Netzwerks zu verbessern.

VPN-Verbindungen (virtuelles privates Netzwerk) sind ein gängiger Weg, um sichere Kommunikationskanäle zwischen Netzwerken herzustellen. Die Verbindung zwischen Azure-VNETs und einem lokalen VPN-Gerät ist eine großartige Möglichkeit, eine sichere Kommunikation zwischen Ihrem Netzwerk und Ihrem VNET in Azure bereitzustellen.

Um eine dedizierte, private Verbindung zwischen Ihrem Netzwerk und Azure herzustellen, können Sie ExpressRoute verwenden. Mit ExpressRoute können Sie Ihre lokalen Netzwerke über eine private Verbindung, die von einem Konnektivitätsanbieter bereitgestellt wird, auf die Microsoft Cloud ausdehnen. Mit ExpressRoute können Sie Verbindungen zu Microsoft-Clouddiensten herstellen, z.B. Microsoft Azure, Office 365 und Dynamics 365. Dies verbessert die Sicherheit Ihrer lokalen Kommunikation, indem dieser Datenverkehr über die private Leitung anstatt über das Internet übertragen wird. Sie müssen Ihren Endbenutzern den Zugriff auf diese Dienste nicht über das Internet gestatten und können diesen Datenverkehr über Appliances zur weiteren Überprüfung des Datenverkehrs senden.

## <a name="summary"></a>Zusammenfassung

Mit einem mehrstufigen Ansatz für Netzwerksicherheit können Sie das Gefährdungsrisiko durch netzwerkbasierte Angriffe reduzieren. Azure bietet mehrere Dienste und Funktionen, um Ihre Internetressourcen, interne Ressourcen und die Kommunikation zwischen lokalen Netzwerken zu schützen. Diese Funktionen ermöglichen, sichere Lösungen in Azure zu erstellen.