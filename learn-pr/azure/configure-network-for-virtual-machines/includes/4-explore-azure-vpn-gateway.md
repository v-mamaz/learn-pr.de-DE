Wenn Sie Ihre lokale Umgebung in Azure integrieren möchten, müssen Sie eine verschlüsselte Verbindung erstellen können. Die Verbindung kann entweder über das öffentliche Internet oder über einen dedizierten Link hergestellt werden. Hier beschäftigen wir uns mit dem Azure-VPN-Gateway, das einen Endpunkt für eingehende Verbindungen aus lokalen Umgebungen bereitstellt.

Sie haben ein virtuelles Azure-Netzwerk eingerichtet und müssen sicherstellen, dass sämtliche Datenübertragungen von Azure sowie zwischen virtuellen Azure-Netzwerken verschlüsselt werden. Außerdem müssen Sie wissen, wie Sie virtuelle Netzwerke zwischen Regionen und Abonnements verbinden.

## <a name="describe-a-vpn-gateway"></a>Beschreiben eines VPN-Gateways

Ein Azure-VPN-Gateway stellt einen Endpunkt für eingehende verschlüsselte Verbindungen bereit, die von lokalen Standorten aus über das Internet mit Azure hergestellt werden. Es kann auch verschlüsselten Datenverkehr zwischen virtuellen Azure-Netzwerken über das dedizierte Netzwerk von Microsoft senden, das Azure-Rechenzentren in verschiedenen Regionen miteinander verbindet. Mit dieser Konfiguration können Sie virtuelle Computer und Dienste in unterschiedlichen Regionen sicher miteinander verknüpfen.

Ein virtuelles Netzwerk kann jeweils nur über ein einzelnes VPN-Gateway verfügen. Alle Verbindungen mit diesem VPN-Gateway teilen sich die verfügbare Netzwerkbandbreite.

Innerhalb jedes Gateways für virtuelle Netzwerke befinden sich mindestens zwei virtuelle Computer. Diese virtuellen Computer wurden in einem speziellen, von Ihnen angegebenen Subnetz bereitgestellt – dem sogenannten _Gatewaysubnetz_. Sie enthalten Routingtabellen für Verbindungen mit anderen Netzwerken sowie spezifische Gatewaydienste. Diese virtuellen Computer und das Gatewaysubnetz ähneln einem gehärteten Netzwerkgerät. Sie müssen diese virtuellen Computer nicht direkt konfigurieren und sollten im Gatewaysubnetz keine zusätzlichen Ressourcen bereitstellen.

Die Erstellung eines Gateways für virtuelle Netzwerke kann eine Weile dauern. Berücksichtigen Sie dies bei Ihrer Planung. Wenn Sie ein Gateway für virtuelle Netzwerke erstellen, werden im Rahmen des Bereitstellungsprozesses die virtuellen Gatewaycomputer generiert und im Gatewaysubnetz bereitgestellt. Diese virtuellen Computer verfügen über die Einstellungen, die Sie für das Gateway konfigurieren.

Eine wichtige Einstellung ist der **_Gatewaytyp_**. Bei einem VPN-Gateway muss diese Einstellung auf „vpn“ festgelegt werden. Für VPN-Gateways stehen unter anderem folgende Optionen zur Verfügung:

- Netzwerk-zu-Netzwerk-Verbindungen über IPsec/IKE-VPN-Tunneling, um VPN-Gateways mit anderen VPN-Gateways zu verknüpfen.

- Standortübergreifendes IPsec/IKE-VPN-Tunneling, um lokale Netzwerke über dedizierte VPN-Geräte mit Azure zu verbinden und Site-to-Site-Verbindungen zu erstellen.

- Point-to-Site-Verbindungen über IKEv2 oder SSTP, um Clientcomputer mit Ressourcen in Azure zu verknüpfen.

Kommen wir zu den Faktoren, die bei der Planung Ihres VPN-Gateways zu berücksichtigen sind.

## <a name="plan-a-vpn-gateway"></a>Planen eines VPN-Gateways

Bei der Planung eines VPN-Gateways sind drei Architekturen zu berücksichtigen:

- Point-to-Site über das Internet
- Site-to-Site über das Internet
- Site-to-Site über ein dediziertes Netzwerk (beispielsweise Azure ExpressRoute)

### <a name="planning-factors"></a>Planungsfaktoren

Berücksichtigen Sie bei Ihrem Planungsprozess unter anderem folgende Faktoren:

- Durchsatz (MBit/s oder GBit/s)
- Backbone: Internet oder privat?
- Verfügbarkeit einer öffentlichen (statischen) IP-Adresse
- VPN-Gerätekompatibilität
- Mehrere Clientverbindungen oder Site-to-Site-Verbindung?
- VPN-Gatewaytyp
- SKU des Azure-VPN-Gateways

Die folgende Tabelle enthält eine Zusammenfassung für einige dieser Aspekte. Die übrigen Aspekte werden weiter unten behandelt.

|                           |  Point-to-Site            | Site-to-Site                          |  ExpressRoute                 |
| -------------             | -------------             | -------------                         | ---------                     |
| Von Azure unterstützte Dienste  | Clouddienste und virtuelle Computer    | Clouddienste und virtuelle Computer                | Alle unterstützten Dienste        |
| Typische Bandbreite         | Abhängig von der VPN-Gateway-SKU    | Bis zu 1 GBit/s mit Aggregation         | Zwischen 50 MBit/s und 10 GBit/s       |
| Unterstützte Protokolle       | SSTP und IPsec            | IPsec                                 | Direkte Verbindung, VLANs      |
| Routing                   | RouteBased (dynamisch)      | PolicyBased (statisch) und RouteBased   | BGP                           |
| Verbindungsresilienz     | Aktiv-passiv            | Aktiv-passiv oder aktiv-aktiv       | Aktiv-aktiv                 |
| Anwendungsfall                  | Tests und Prototypenerstellung   | Entwicklung, Test und Produktion im kleinen Stil  | Unternehmens-/geschäftskritisch   |

### <a name="gateway-skus"></a>Gateway-SKUs

Azure bietet folgenden SKUs für Gatewaydienste:

| SKU              |  S2S/Netzwerk-zu-Netzwerk-Tunnel | P2S-Verbindungen  |  Benchmark für den aggregierten Durchsatz   | Verwendung                         |
| -------------    | -------------             | -------------    | ---------                         | ---------                       |
| Basic            | Max. 10                    | Max. 128          | 100 MBit/s                          | Entwicklung/Tests/Proof of Concept                    |
| VpnGw1           | Max. 30                    | Max. 128          | 650 MBit/s                          | Produktion/kritische Workloads   |
| VpnGw2           | Max. 30                    | Max. 128          | 1 GBit/s                            | Produktion/kritische Workloads   |
| VpnGw3           | Max. 30                    | Max. 128          | 1,25 GBit/s                          | Produktion/kritische Workloads   |

> [!Note]
> Es ist wichtig, sich für die passende SKU zu entscheiden. Wenn Sie Ihr VPN-Gateway mit der falschen SKU einrichten, müssen Sie es entfernen und neu erstellen, was zeitaufwändig sein kann.

## <a name="workflow"></a>Workflow

Wenn Sie eine Cloudkonnektivitätsstrategie mit VPN für Azure entwerfen, sollten Sie wie folgt vorgehen:

1. Entwerfen Sie Ihre Netzwerktopologie, und listen Sie die Adressräume für alle verbundenen Netzwerke auf.

1. Erstellen Sie ein virtuelles Azure-Netzwerk.

1. Erstellen Sie ein VPN-Gateway für das virtuelle Netzwerk.

1. Erstellen und konfigurieren Sie Verbindungen mit lokalen Netzwerken oder anderen virtuellen Netzwerken nach Bedarf.

1. Erstellen und konfigurieren Sie ggf. eine Point-to-Site-Verbindung für Ihr Azure-VPN-Gateway.

### <a name="design-considerations"></a>Überlegungen zum Entwurf

Berücksichtigen Sie die folgenden Faktoren, wenn Sie Ihre VPN-Gateways entwerfen, um virtuelle Netzwerke zu verbinden:

- Subnetze dürfen nicht überlappen

    Ein Subnetz darf nicht den gleichen Adressraum enthalten wie ein Subnetz an einem anderen Standort.

- IP-Adressen müssen eindeutig sein

    Es dürfen nicht zwei Hosts mit der gleichen IP-Adresse an unterschiedlichen Standorten vorhanden sein, da es in diesem Fall nicht möglich ist, Datenverkehr zwischen diesen beiden Hosts weiterzuleiten und eine Netzwerk-zu-Netzwerk-Verbindung herzustellen.

- VPN-Gateways benötigen ein Gatewaysubnetz namens **GatewaySubnet**

    Das Gateway muss diesen Namen besitzen, da es sonst nicht funktioniert. Außerdem darf es keine anderen Ressourcen enthalten.

### <a name="create-an-azure-virtual-network"></a>Erstellen eines virtuellen Azure-Netzwerks

Bevor Sie ein VPN-Gateway erstellen, müssen Sie das virtuelle Azure-Netzwerk erstellen.

### <a name="create-a-vpn-gateway"></a>Erstellen eines VPN-Gateways

Die Art des VPN-Gateways, das Sie erstellen, hängt von Ihrer Architektur ab. Folgende Optionen stehen zur Verfügung:

- RouteBased

    Für routenbasierte VPN-Geräte werden Any-to-Any-Datenverkehrsselektoren (mit Platzhalter) verwendet, und mit Routing-/Weiterleitungstabellen wird das Leiten von Datenverkehr an verschiedene IPsec-Tunnel ermöglicht. Routenbasierte Verbindungen basieren in der Regel auf Routerplattformen, auf denen jeder IPsec-Tunnel als Netzwerkschnittstelle oder virtuelle Tunnelschnittstelle (Virtual Tunnel Interface, VTI) modelliert ist.

- PolicyBased

    Für richtlinienbasierte VPN-Geräte werden die Kombinationen aus Präfixen beider Netzwerke verwendet, um zu definieren, wie Datenverkehr mithilfe von IPsec-Tunneln verschlüsselt bzw. entschlüsselt wird. Eine richtlinienbasierte Verbindung basiert in der Regel auf Firewallgeräten für die Paketfilterung. Die Ver- und Entschlüsselung von IPsec-Tunneln wird der Engine für die Paketfilterung und -verarbeitung hinzugefügt.

## <a name="set-up-a-vpn-gateway"></a>Einrichten eines VPN-Gateways

Die auszuführenden Schritte hängen von der Art des VPN-Gateways ab, das Sie installieren. Wenn Sie also beispielsweise über das Azure-Portal ein Point-to-Site-VPN-Gateway erstellen, sind folgende Schritte erforderlich:

1. Erstellen eines virtuellen Netzwerks

2. Hinzufügen eines Gatewaysubnetzes

3. Angeben eines DNS-Servers (optional)

4. Erstellen eines Gateways für virtuelle Netzwerke

5. Generieren von Zertifikaten

6. Hinzufügen des Clientadresspools

7. Konfigurieren des Tunneltyps

8. Konfigurieren des Authentifizierungstyps

9. Hochladen der Daten des öffentlichen Zertifikats für das Stammzertifikat

10. Installieren eines exportierten Clientzertifikats

11. Generieren und Installieren des Konfigurationspakets für VPN-Clients

12. Herstellen einer Verbindung mit Azure

Aufgrund der vielfältigen Konfigurationspfade und Optionen für Azure-VPN-Gateways können in diesem Kurs nicht alle Kombinationen behandelt werden. Weitere Informationen finden Sie im Abschnitt mit den zusätzlichen Ressourcen.

## <a name="configure-the-gateway"></a>Konfigurieren des Gateways

Das erstellte Gateway muss noch konfiguriert werden.  Dabei müssen verschiedene Konfigurationseinstellungen wie Name, Standort, DNS-Server usw. angegeben werden. Auf diese gehen wir in der Übung noch näher ein.

## <a name="summary"></a>Zusammenfassung

Azure-VPN-Gateways sind eine Komponente in virtuellen Azure-Netzwerken, die Point-to-Site-, Site-to-Site- und Netzwerk-zu-Netzwerk-Verbindungen ermöglichen. Mit Azure-VPN-Gateways können einzelne Clientcomputer eine Verbindung mit Ressourcen in Azure herstellen, lokale Netzwerke auf Azure ausdehnen sowie Verbindungen zwischen virtuellen Netzwerken in unterschiedlichen Regionen und Abonnements vereinfachen.
