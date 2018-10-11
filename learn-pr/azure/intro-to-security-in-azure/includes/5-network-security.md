Der Schutz von Netzwerken vor Angriffen und unbefugtem Zugriff ist ein wichtiger Bestandteil jeder Architektur. Hier betrachten wir die Netzwerksicherheit, wie Sie einen mehrstufigen Ansatz in Ihre Architektur integrieren, und wie Sie mit Azure Netzwerksicherheit für Ihre Umgebung gewährleisten.

## <a name="a-layered-approach-to-network-security"></a>Mehrstufiger Netzwerksicherheitsansatz

Sie haben wahrscheinlich bemerkt, dass ein gemeinsames Thema in diesem Modul der Schwerpunkt eines mehrstufigen Sicherheitsansatzes ist, und das ist auf der Netzwerkebene nicht anders. Es reicht nicht aus, sich nur dem Schutz des Netzwerkumkreises oder der Netzwerksicherheit zwischen Diensten innerhalb eines Netzwerks zu widmen. Ein mehrstufiger Ansatz bietet mehrere Schutzebenen. Das heißt, wenn ein Angriff eine Ebene passiert, sind weitere Schutzmechanismen vorhanden, um weitere Angriffe einzuschränken.

Sehen wir uns an, wie Azure Tools für einen mehrstufigen Ansatz zum Schutz Ihres Netzwerks bereitstellen kann.

:::row:::
  :::column:::
    ![Bild, das ein sicheres Internet darstellt](../media/5-internet-protection.png)
  :::column-end:::
    :::column span="3"::::
**Internetschutz**

Wenn wir im Umkreis des Netzwerks beginnen, konzentrieren wir uns darauf, Angriffe aus dem Internet einzuschränken und zu eliminieren. Es wird empfohlen, zunächst die Ressourcen auszuwerten, die mit dem Internet verbunden sind, und nur bei Bedarf eine eingehende und ausgehende Kommunikation zuzulassen. Stellen Sie sicher, dass Sie alle Ressourcen identifizieren, die eingehenden Netzwerkverkehr jeglicher Art zulassen, und stellen Sie dann sicher, dass diese nur auf die erforderlichen Ports und Protokolle beschränkt sind. Azure Security Center eignet sich hervorragend, um nach diesen Informationen zu suchen, da es Internetressourcen identifiziert, denen keine Netzwerksicherheitsgruppen (NSG) zugeordnet sind, sowie Ressourcen, die nicht hinter einer Firewall geschützt sind.

Es gibt mehrere Möglichkeiten, Schutz für eingehenden Datenverkehr im Umkreis zu gewährleisten:

* Bei Azure Application Gateway handelt es sich um einen Lastenausgleich, der eine Webanwendungsfirewall enthält, die Schutz vor allgemein bekannten Sicherheitslücken bietet.

* Virtuelle Netzwerkgeräte (NVAs) sind geeignete Optionen für Nicht-HTTP-Dienste oder erweiterte Konfigurationen. Sie ähneln Hardwarefirewallgeräten.

Für alle Ressourcen, die im Internet zur Verfügung stehen, besteht die Gefahr eines Denial-of-Service-Angriffs. Bei diesem Angriff wird eine Netzwerkressource überlastet, indem so viele Anforderungen gesendet werden, dass die Ressource langsam oder gar nicht mehr reagiert. Damit diese Angriffe abgewehrt werden können, bietet Azure DDoS Protection einen Basisschutz für alle Azure-Dienste und einen erweiterten Schutz für weitere Anpassungen Ihrer Ressourcen. Azure DDoS Protection sperrt Angriffsdatenverkehr und leitet den verbleibenden Datenverkehr an das vorgesehene Ziel weiter. Innerhalb weniger Minuten nach Angriffserkennung werden Sie mithilfe der Metriken von Azure Monitor benachrichtigt.

In diesem Diagramm wird dargestellt, wie Netzwerkdatenverkehr von beiden Kunden und einem Angreifer bei Azure eingeht. Der Azure DDoS-Schutz identifiziert den Versuch des Angreifers, das Netzwerk zu überlasten, und hindert weiteren Datenverkehr daran, die Azure-Dienste zu erreichen. Legitimer Datenverkehr von Kunden geht noch immer ohne Unterbrechung des Diensts bei Azure ein.

![DDoS](../media/ddos.png)

 :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![Bild, das ein sicheres virtuelles Netzwerk darstellt](../media/5-vnet-security.png)
  :::column-end:::
    :::column span="3"::::
**Sicherheit in virtuellen Netzwerken**

Es ist von entscheidender Bedeutung, in einem virtuellen Netzwerk (VNET) die Kommunikation zwischen den Ressourcen auf das erforderliche Maß zu beschränken.

Bei der Kommunikation zwischen virtuellen Computern spielen Netzwerksicherheitsgruppen eine wichtige Rolle, um unnötige Kommunikation zu verhindern. Sie stellen eine Liste der zulässigen und verweigerten Kommunikation von und zu Netzwerkschnittstellen und Subnetzen bereit und können vollständig angepasst werden.

Sie können den öffentlichen Zugriff durch das Internet auf Ihre Dienste vollständig entfernen, indem Sie den Zugriff auf Dienstendpunkte beschränken. Mit Dienstendpunkten kann der Zugriff von Azure-Diensten auf Ihr virtuelles Netzwerk beschränkt werden.
 :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![Bild, das ein sicheres Netzwerk darstellt](../media/5-network-integration.png)
  :::column-end:::
    :::column span="3"::::
**Netzwerkintegration**

Es ist üblich, dass eine vorhandene Netzwerkinfrastruktur integriert werden soll, um die Kommunikation aus lokalen Netzwerken zu ermöglichen, oder um eine verbesserte Kommunikation zwischen den Diensten in Azure zu ermöglichen. Es gibt einige grundlegende Methoden, diese Integration auszuführen, und die Sicherheit Ihres Netzwerks zu verbessern.

VPN-Verbindungen (virtuelles privates Netzwerk) sind ein gängiger Weg, um sichere Kommunikationskanäle zwischen Netzwerken herzustellen. Die Verbindung zwischen Azure Virtual Network und einem lokalen VPN-Gerät ist eine großartige Möglichkeit, eine sichere Kommunikation zwischen Ihrem Netzwerk und Ihrem VNET in Azure bereitzustellen.

Um eine dedizierte, private Verbindung zwischen Ihrem Netzwerk und Azure herzustellen, können Sie Azure ExpressRoute verwenden. Mit ExpressRoute können Sie Ihre lokalen Netzwerke über eine private Verbindung, die von einem Konnektivitätsanbieter bereitgestellt wird, auf die Microsoft Cloud ausdehnen. Mit ExpressRoute können Sie Verbindungen zu Microsoft-Clouddiensten herstellen, z.B. Microsoft Azure, Office 365 und Dynamics 365. Dies verbessert die Sicherheit Ihrer lokalen Kommunikation, indem dieser Datenverkehr über die private Leitung anstatt über das Internet übertragen wird. Sie müssen Ihren Endbenutzern den Zugriff auf diese Dienste nicht über das Internet gestatten und können diesen Datenverkehr über Appliances zur weiteren Überprüfung des Datenverkehrs senden.
 :::column-end:::
:::row-end:::

## <a name="summary"></a>Zusammenfassung

Mit einem mehrstufigen Ansatz für Netzwerksicherheit können Sie das Gefährdungsrisiko durch netzwerkbasierte Angriffe reduzieren. Azure bietet mehrere Dienste und Funktionen, um Ihre Internetressourcen, interne Ressourcen und die Kommunikation zwischen lokalen Netzwerken zu schützen. Diese Funktionen ermöglichen, sichere Lösungen in Azure zu erstellen.