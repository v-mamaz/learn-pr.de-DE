Ihr Unternehmen ist für streng vertrauliche Daten und verfügt über große Mengen von Informationen, die sie in Azure gespeichert werden sollen, gibt es Bedenken hinsichtlich Sicherheit und Zuverlässigkeit von Verbindungen über das öffentliche Internet. Das Unternehmen nicht bereit, die global zu Azure migrieren, es sei denn, es höheres Maß an Zuverlässigkeit, Sicherheit und Konnektivität gezeigt werden kann.

Wir werden hier Verbindungen hinausgehen, die über das Internet auf dedizierten Zeilen direkt in der Azure-Rechenzentren ausgeführt.

## <a name="azure-expressroute"></a>Azure ExpressRoute

Mit Microsoft Azure ExpressRoute können Organisationen ihre lokalen Netzwerke über eine private Verbindung, die von einem Konnektivitätsanbieter implementiert wird, auf die Microsoft Cloud erweitern. Diese Anordnung bedeutet, dass die Verbindung mit der Azure-Rechenzentren über das Internet, aber über eine dedizierte Verbindung verläuft nicht. ExpressRoute ermöglicht auch effizientere Verbindungen mit anderen cloudbasierten Microsoft-Diensten wie Office 365 und Dynamics 365.

ExpressRoute bietet unter anderem folgende Vorteile:

- Höhere Geschwindigkeit (zwischen 50 MBit/s und 10 GBit/s) mit dynamischer Bandbreitenskalierung

- Geringere Wartezeit

- Peering integrierte Zuverlässigkeit

- Hohe Sicherheit

Weitere Vorteile von ExpressRoute:

- Konnektivität mit allen unterstützten Azure-Diensten

- Globale Konnektivität mit allen Regionen (Premium-Add-On erforderlich)

- Dynamisches Routing über Border Gateway Protocol

- Vereinbarungen zum Servicelevel (Service Level Agreements, SLAs) für Verbindungsverfügbarkeit

- Servicequalität (Quality of Service, QoS) für Skype for Business

Darüber hinaus ist das ExpressRoute Premium-Add-On, das Vorteile wie z. B. die Erhöhung der routengrenzwerte, globalen dienstkonnektivität und erhöhte vnet-Links pro Verbindung bietet.

## <a name="expressroute-connectivity-models"></a>ExpressRoute-Konnektivitätsmodelle

Für ExpressRoute-Verbindungen stehen folgende Mechanismen zur Verfügung:

- IP-basiertes VPN (Any-to-Any-Netzwerk)

- Virtuelle Querverbindung über einen Ethernet-Exchange

- Point-to-Point-Ethernet-Verbindung

 Die ExpressRoute-Funktionen und -Features sind für alle oben genannten Konnektivitätsmodelle identisch.

### <a name="what-is-layer-3-connectivity"></a>Was ist Layer 3-Konnektivität?

Microsoft nutzt ein Branchenstandardprotokoll für dynamisches Routing (BGP), um Routen zwischen Ihrem lokalen Netzwerk, Ihren Instanzen in Azure und öffentlichen Microsoft-Adressen auszutauschen. Wir richten für Ihr Netzwerk mehrere BGP-Sitzungen für unterschiedliche Datenverkehrsprofile ein.

### <a name="any-to-any-ipvpn-networks"></a>Any-to-Any-Netzwerke (IPVPN)

IPVPN-Anbieter stellen die Konnektivität zwischen Zweigstellen und dem Rechenzentrum Ihres Unternehmens in der Regel über verwaltete Layer 3-Verbindungen bereit. Mit ExpressRoute können die Azure-Rechenzentren wie eine weitere Zweigstelle verwendet werden.

### <a name="virtual-cross-connection-through-an-ethernet-exchange"></a>Virtuelle Querverbindung über einen Ethernet-Exchange

Wenn sich Ihre Organisation am gleichen Ort befindet wie eine Cloud Exchange-Einrichtung, fordern Sie Querverbindungen mit der Microsoft Cloud über den Ethernet-Exchange Ihres Anbieters an. Diese Querverbindungen mit der Microsoft Cloud können wie im OSI-Netzwerkmodell als Layer 2- oder verwaltete Layer 3-Verbindungen verwendet werden.

### <a name="point-to-point-ethernet-connection"></a>Point-to-Point-Ethernet-Verbindung

Point-to-Point-Ethernet-Verbindungen können Layer 2- oder verwaltete Layer 3-Verbindungen zwischen Ihren lokalen Rechenzentren oder Filialen und der Microsoft Cloud bereitstellen.

## <a name="how-expressroute-works"></a>Funktionsweise von ExpressRoute

Azure ExpressRoute verwendet eine Kombination von ExpressRoute-Verbindungen und Routingdomänen, um Konnektivität mit hoher Bandbreite mit der Microsoft Cloud bereitzustellen.

### <a name="what-are-expressroute-circuits"></a>Was sind ExpressRoute-Verbindungen?

Eine ExpressRoute-Verbindung ist die logische Verbindung zwischen Ihrer lokalen Infrastruktur und der Microsoft Cloud. Diese Verbindung wird von einem Konnektivitätsanbieter implementiert. Aus Redundanzgründen verwenden einige Organisationen mehrere Konnektivitätsanbieter. Jede Verbindung verfügt über eine feste Bandbreite entweder 50, 100, 200 Mbit/s oder 500 Mbit/s oder 1 Gbit/s oder 10 Gbit/s, und mit diesen Verbindungen ordnen Sie einem konnektivitätsanbieter und einem peeringstandort. Darüber hinaus gelten für jede ExpressRoute-Verbindung Standardkontingente und -grenzwerte.

Eine ExpressRoute-Verbindung nicht gleichbedeutend mit einer Netzwerkverbindung oder ein Netzwerkgerät. Jede Verbindung wird durch eine GUID (_Dienstschlüssel___) definiert. Dieser Dienstschlüssel stellt den Link der Konnektivität zwischen Microsoft, Ihr konnektivitätsanbieter und Ihrer Organisation – es ist eine kryptografische Schlüssel nicht bereit. Für jeden Dienstschlüssel besteht eine 1: 1-Zuordnung zu einer Azure ExpressRoute-Verbindung.

Jede Verbindung kann über bis zu drei Peerings (aus Redundanzgründen konfiguriertes BGP-Sitzungspaar) verfügen. Sie lauten wie folgt:

- Privates Azure-Peering
- Öffentliches Azure-Peering
- Microsoft

### <a name="routing-domains"></a>Routingdomänen

ExpressRoute-Verbindungen werden anschließend Routingdomänen zugeordnet. Die einzelnen ExpressRoute-Verbindungen verfügen dabei jeweils über mehrere Routingdomänen. Diese Domänen sind identisch mit den oben aufgeführten drei Peerings. In einer Aktiv-Aktiv-Konfiguration ist jede Routingdomäne für jedes Routerpaar identisch konfiguriert, was für hohe Verfügbarkeit sorgt. Die Namen für öffentliches und privates Azure-Peering stellen die IP-Adressierungsschemas dar.

#### <a name="azure-private-peering"></a>Privates Azure-Peering

Beim privaten Azure-Peering wird eine Verbindung mit Azure-Computediensten (etwa mit virtuellen Computern und Clouddiensten) hergestellt, die mit einem virtuellen Netzwerk bereitgestellt wurden. In puncto Sicherheit ist die private Peeringdomäne einfach eine Erweiterung Ihres lokalen Netzwerks in Azure. Sie aktivieren dann die bidirektionale Konnektivität zwischen diesem Netzwerk und virtuellen Azure-Netzwerken, wodurch die IP-Adressen des virtuellen Azure-Computers in Ihrem internen Netzwerk sichtbar werden.

> [!NOTE]
> Sie können nur ein virtuelles Netzwerk mit der privaten Peeringdomäne verbinden.

#### <a name="azure-public-peering"></a>Öffentliches Azure-Peering

Öffentliches Azure-Peering ermöglicht private Verbindungen mit Diensten, die über öffentliche IP-Adressen verfügbar sind. Hierzu zählen beispielsweise Azure Storage, Azure SQL-Datenbanken und Azure-Webdienste. Für die öffentliches peering, können Sie ohne Ihr Datenverkehr, die über das Internet weitergeleitet werden diese öffentlichen IP-Adressen von Dienst verbinden. Die Konnektivität verläuft immer von Ihrem WAN zu Azure, nicht umgekehrt. Dies ist auch ein nichts-Ansatz, wie Sie die Dienste auswählen, können nicht für die öffentliches peering aktiviert.

> [!NOTE]
> Bei Azure-PaaS-Diensten ist das Microsoft-Peering dem öffentlichen Peering vorzuziehen.

#### <a name="microsoft-peering"></a>Microsoft-Peering

Microsoft-Peering unterstützt Verbindungen mit cloudbasierten SaaS-Angeboten wie Office 365 und Dynamics 365. Diese Peering-Option bietet bidirektionale Konnektivität zwischen dem WAN Ihres Unternehmens und den Clouddiensten von Microsoft.

### <a name="expressroute-health"></a>ExpressRoute-Integrität

Wie bei den meisten Features in Microsoft Azure können Sie die ExpressRoute-Verbindungen überwachen, um sich zu vergewissern, dass sie zufriedenstellend funktionieren. Die Überwachung umfasst folgende Aspekte:

- Verfügbarkeit
- Konnektivität mit virtuellen Netzwerken
- Bandbreitennutzung

Das zentrale Tool für diese Überwachung ist der Netzwerkleistungsmonitor (Network Performance Monitor, NPM) für ExpressRoute.

## <a name="summary"></a>Zusammenfassung

Mit Azure ExpressRoute können Sie private Verbindungen zwischen Azure-Datencentern und einer Infrastruktur in Ihrer lokalen Umgebung oder in einer Housingumgebung erstellen. ExpressRoute-Verbindungen nicht über das öffentliche Internet geleitet und bieten mehr Zuverlässigkeit, schnellere Geschwindigkeiten und geringere Latenz als herkömmliche internetverbindungen.
