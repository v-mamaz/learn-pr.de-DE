Der Schutz von Netzwerken vor Angriffen und unbefugtem Zugriff ist ein wichtiger Bestandteil jeder Architektur. Im Rahmen der Planung für die cloudmigration dauerte Lamna Healthcare die Zeit zum Planen ihrer Netzwerkinfrastruktur, um sicherzustellen, dass hatten die richtige Netzwerk Sicherheitskontrollen direkt auf ihrer Netzwerkinfrastruktur vor Angriffen zu schützen. Hier betrachten wir die Netzwerksicherheit, wie Sie einen mehrstufigen Ansatz in Ihre Architektur integrieren, und wie Sie mit Azure Netzwerksicherheit für Ihre Umgebung gewährleisten.

## <a name="what-is-network-security"></a>Was ist Netzwerksicherheit?

Netzwerksicherheit schützt die Kommunikation von Ressourcen innerhalb und außerhalb Ihres Netzwerks. Ziel ist es, das Risiko für Ihre Dienste und Systeme auf Netzwerkebene einzuschränken. Indem Sie das Risiko einschränken, verringern Sie die Wahrscheinlichkeit für einen Angriff auf Ihre Ressourcen. Die Netzwerksicherheit konzentriert sich vor allem auf folgende Bereiche:

- Sichern des Datenverkehrs zwischen Anwendungen und dem Internet
- Sichern des Datenverkehrs zwischen Anwendungen
- Sichern den Datenverkehrs zwischen Benutzern und Anwendungen

Die Sicherung des Datenverkehrs zwischen Anwendungen und dem Internet konzentriert sich darauf, das Risiko außerhalb Ihres Netzwerks einzuschränken. Netzwerkangriffe beginnen meist außerhalb Ihres Netzwerks, sodass durch die Begrenzung des Internetrisikos und die Sicherung des Umkreises die Gefahr eines Angriffs reduziert werden kann.

Die Sicherung des Datenverkehrs zwischen Anwendungen konzentriert sich auf Daten, die zwischen Anwendungen, deren Schichten, verschiedenen Umgebungen und anderen Diensten in Ihrem Netzwerk übertragen werden. Durch die Einschränkung der Gefährdung zwischen diesen Ressourcen verringern Sie die Auswirkungen einer möglicherweise beschädigten Ressource. Dies kann dazu beitragen, die weitere Verbreitung innerhalb eines Netzwerks zu einzudämmen.

Die Sicherung des Datenverkehrs zwischen Benutzern und Anwendungen konzentriert sich auf die Sicherung des Netzwerkflusses Ihrer Endbenutzer. Dadurch wird die Gefährdung Ihrer Ressourcen durch Angriffe von außen begrenzt und ein sicherer Mechanismus für Benutzer geschaffen, um Ihre Ressourcen zu nutzen. 

## <a name="a-layered-approach-to-network-security"></a>Mehrstufiger Netzwerksicherheitsansatz

Ein roter Faden in diesem Modul ist der mehrstufige Sicherheitsansatz – der auch auf Netzwerkebene gilt. Es reicht nicht aus, sich nur der Sicherung des Netzwerkumkreises oder der Netzwerksicherheit zwischen Diensten innerhalb eines Netzwerks zu widmen. Ein mehrstufiger Ansatz bietet mehrere Schutzebenen. Das heißt, wenn ein Angriff eine Ebene passiert, sind weitere Schutzmechanismen vorhanden, um weitere Angriffe einzuschränken.

Sehen wir uns an, wie Azure Tools für einen mehrstufigen Ansatz zur Sicherung Ihres Netzwerks bereitstellen kann.

### <a name="internet-protection"></a>Internetschutz

Wenn wir im Umkreis des Netzwerks beginnen, konzentrieren wir uns darauf, Angriffe aus dem Internet einzuschränken und zu eliminieren. Ein guter Ausgangspunkt ist es, die Ressourcen zu bewerten, mit denen das Internet konfrontiert ist, und ein- und ausgehende Kommunikation nur dann zu erlauben, wenn sie erforderlich ist. Identifizieren Sie alle Ressourcen, die eingehenden Netzwerkdatenverkehr jeglicher Art zulassen, und stellen Sie sicher, dass dieser notwendig und auf die erforderlichen Ports/Protokolle beschränkt ist. Das Azure Security Center eignet sich hervorragend, um nach diesen Informationen zu suchen, da es Internetressourcen identifiziert, denen keine Netzwerksicherheitsgruppen (NSG) zugeordnet sind, sowie Ressourcen, die nicht hinter einer Firewall gesichert sind.

Es gibt mehrere Möglichkeiten, Schutz für eingehenden Datenverkehr im Umkreis zu gewährleisten. Application Gateway ist ein Layer 7-Lastenausgleich, der auch eine Web Application Firewall (WAF) beinhaltet, um erweiterte Sicherheit für Ihre HTTP-basierten Dienste zu bieten. Die WAF basiert auf den Kernregeln von OWASP 3.0 bzw. 2.2.9 und bietet Schutz vor bekannten Sicherheitsrisiken wie Cross-Site-Scripting und Einschleusung von SQL-Befehlen.

![Application Gateway mit WAF](../media-draft/appgw-waf.png)

Zum Schutz von Diensten, die nicht auf HTTP basieren, oder zur besseren Anpassung können virtuelle Netzwerkappliances zur Sicherung Ihrer Netzwerkressourcen eingesetzt werden. Virtuelle Netzwerkappliances sind ähnlich wie Firewallappliances auf lokalen Netzwerken und über viele gängige Anbieter von Netzwerksicherheit erhältlich. Sie können eine bessere Anpassung der Sicherheitsmaßnahmen bieten, die Anwendungen benötigen. Allerdings sind sie ggf. komplexer, sodass eine sorgfältige Berücksichtigung der Anforderungen empfohlen wird.

Für alle Ressourcen, die im Internet zur Verfügung stehen, besteht die Gefahr eines Denial-of-Service-Angriffs. Bei diesem Angriff wird eine Netzwerkressource überlastet, indem so viele Anforderungen gesendet werden, dass die Ressource langsam oder gar nicht mehr reagiert. Damit diese Angriffe abgewehrt werden können, bietet Azure DDoS einen Basisschutz für alle Azure-Dienste und einen erweiterten Schutz für weitere Anpassungen Ihrer Ressourcen. Der DDoS-Schutz blockiert Angriffsdatenverkehr und leitet den verbleibenden Datenverkehr an das vorgesehene Ziel weiter. Innerhalb weniger Minuten nach Angriffserkennung werden Sie über die Metriken von Azure Monitor benachrichtigt.

![DDoS](../media-draft/ddos.png)

### <a name="virtual-network-security"></a>Sicherheit in virtuellen Netzwerken

Es ist wichtig, in einem virtuellen Netzwerk (VNET) die Kommunikation zwischen den Ressourcen auf das erforderliche Maß zu beschränken.

Bei der Kommunikation zwischen VMs spielen Netzwerksicherheitsgruppen eine wichtige Rolle, um unnötige Kommunikation zu verhindern. NSGs werden auf den Ebenen 3 und 4 ausgeführt und stellen eine Liste der zulässigen und verweigerten Kommunikation von und zu Netzwerkschnittstellen und Subnetzen bereit. NSGs sind vollständig anpassbar und bieten Ihnen die Möglichkeit, die Netzwerkkommunikation zu und von Ihren VMs vollständig zu sperren. Mit NSGs können Sie Anwendungen zwischen Umgebungen, Ebenen und Diensten isolieren.

![Azure-Netzwerksicherheitsgruppen](../media-draft/azure-network-security.png)

Verwenden Sie VNET-Dienstendpunkte, um Azure-Dienste zu isolieren, damit nur die Kommunikation aus virtuellen Netzwerken zugelassen wird. Mit Dienstendpunkten können Ressourcen von Azure-Diensten auf Ihr virtuelles Netzwerk beschränkt und so geschützt werden. Das Sichern von Dienstressourcen in einem virtuellen Netzwerk erhöht die Sicherheit, da der Zugriff über das öffentliche Internet auf Ressourcen vollständig verhindert, und nur Datenverkehr aus Ihrem virtuellen Netzwerk zugelassen wird. Dies verringert die Angriffsfläche Ihrer Umgebung, reduziert den Verwaltungsaufwand, um die Kommunikation zwischen Ihren VNet- und Azure-Diensten einzuschränken, und bietet ein optimales Routing für diese Kommunikation.

### <a name="network-integration"></a>Netzwerkintegration

Es ist üblich, dass eine vorhandene Netzwerkinfrastruktur integriert werden soll, um die Kommunikation aus lokalen Netzwerken zu ermöglichen, oder um eine verbesserte Kommunikation zwischen den Diensten in Azure zu ermöglichen. Es gibt einige grundlegende Methoden, diese Integration auszuführen, und die Sicherheit Ihres Netzwerks zu verbessern.

VPN-Verbindungen (virtuelles privates Netzwerk) sind ein gängiger Weg, um sichere Kommunikationskanäle zwischen Netzwerken herzustellen – das ist auch bei virtuellen Netzwerken in Azure nicht anders. Die Verbindung zwischen Azure-VNETs und einem lokalen VPN-Gerät ist eine großartige Möglichkeit, eine sichere Kommunikation zwischen Ihrem Netzwerk und Ihren VMs in Azure bereitzustellen.

Um eine dedizierte, private Verbindung zwischen Ihrem Netzwerk und Azure herzustellen, lässt sich ExpressRoute verwenden. Mit ExpressRoute können Sie Ihre lokalen Netzwerke über eine private Verbindung, die von einem Konnektivitätsanbieter bereitgestellt wird, auf die Microsoft Cloud ausdehnen. Mit ExpressRoute können Sie Verbindungen zu Microsoft Cloud Services herstellen, z.B. Microsoft Azure, Office 365 und Dynamics 365. Dies verbessert die Sicherheit Ihrer lokalen Kommunikation, indem dieser Datenverkehr über die private Leitung anstatt über das Internet übertragen wird. Sie müssen Ihren Endbenutzern den Zugriff auf diese Dienste nicht über das Internet gestatten und können diesen Datenverkehr über Appliances zur weiteren Überprüfung des Datenverkehrs senden.

![ExpressRoute](../media-draft/expressroute-connection-overview.png)

Um mehrere VNETs einfach in Azure zu integrieren, stellt das VNET-Peering eine direkte Verbindung zwischen bestimmten VNETs her. Sobald die Verbindung hergestellt ist, können Sie mit NSGs die Isolierung zwischen den Ressourcen genauso einrichten, wie Sie Ressourcen in einem VNET sichern. Diese Integration gibt Ihnen die Möglichkeit, die gleiche grundlegende Sicherheitsebene für alle VNETs mit Peering bereitzustellen. Die Kommunikation ist nur zwischen direkt verbundenen VNETs zulässig.

## <a name="network-security-at-lamna-healthcare"></a>Netzwerksicherheit bei Lamna Healthcare

Lamna Healthcare hat viele dieser Dienste zum Aufbau einer sicheren Netzwerkinfrastruktur genutzt. Die Kommunikation zwischen den Ressourcen wird standardmäßig verweigert und nur bei Bedarf zugelassen. Eingehende Verbindungen über das Internet sind nur für Dienste aktiviert, die diese benötigen. RDP und SSH werden nicht von Internetendpunkten aus zugelassen, sondern nur von vertrauenswürdigen internen Ressourcen.

Zum Sichern von internetbasierten Webdiensten platziert Lamna Healthcare sie hinter Application Gateways mit aktivierter WAF. Dies gilt sowohl für Dienste, die auf VMs als auch in App Service ausgeführt werden. Application Gateways schützen die Organisation vor den meisten häufigsten Sicherheitsrisiken.

Der DDoS-Standardschutz ist aktiviert, um die Internetendpunkte vor Denial-of-Service-Angriffen zu schützen.

Durch die Verwendung von NSGs ist Lamna Healthcare in der Lage, die Kommunikation zwischen Anwendungsdiensten und Umgebungen vollständig zu isolieren. Die Organisation lässt nur die notwendige Kommunikation zwischen Diensten innerhalb einer Umgebung zu, und erlaubt keinen Zugriff zwischen Produktions- und Nicht-Produktionsumgebungen.

Um eine dedizierte Konnektivität zwischen Endbenutzern und Anwendungen in Azure zu bieten, hat Lamna Healthcare eine ExpressRoute-Leitung mit Konnektivität zum lokalen Netzwerk bereitgestellt. So wird der Datenverkehr zu Azure nicht über das Internet übertragen, und es wird eine private Verbindung für die Dienste in Azure geschaffen, um mit lokalen Systemen zu kommunizieren.

Mit diesem Ansatz hat Lamna Healthcare mithilfe der Azure-Dienste Sicherheit auf mehreren Ebenen in der Netzwerkinfrastruktur des Unternehmens gewährleistet.

## <a name="summary"></a>Zusammenfassung

Mit einem mehrstufigen Ansatz für Netzwerksicherheit können Sie das Gefährdungsrisiko durch netzwerkbasierte Angriffe reduzieren. Azure bietet mehrere Dienste und Funktionen, um Ihre Internetressourcen, interne Ressourcen und die Kommunikation zwischen lokalen Netzwerken zu schützen. Diese Funktionen ermöglichen es, sichere Lösungen in Azure zu erstellen.