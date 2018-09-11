Sie verfügen über ein lokales Rechenzentrum, das erhalten bleiben soll, und möchten Datenverkehrsspitzen an in Azure gehostete virtuelle Computer (Virtual Machines, VMs) auslagern. Sie möchten wissen, ob Sie Ihr bisheriges IP-Adressierungsschema und Ihre Netzwerkgeräte behalten und gleichzeitig die Sicherheit sämtlicher Datenübertragungen sicherstellen können.

## <a name="what-is-azure-virtual-networking"></a>Was ist Azure Virtual Network?

Mit **virtuellen Azure-Netzwerken** können Azure-Ressourcen wie etwa virtuelle Computer, Web-Apps und Datenbanken untereinander, mit Benutzern im Internet sowie mit lokalen Clientcomputern kommunizieren. Ein Azure-Netzwerk können Sie sich als eine Gruppe von Ressourcen vorstellen, die andere Azure-Ressourcen miteinander verbindet.

Virtuelle Azure-Netzwerke bieten wichtige Netzwerkfunktionen. Hierzu zählen beispielsweise folgende:

- Isolation und Segmentierung
- Internetkommunikation
- Kommunikation zwischen Azure-Ressourcen
- Kommunikation mit lokalen Ressourcen
- Weiterleitung von Netzwerkdatenverkehr
- Filterung von Netzwerkdatenverkehr
- Verbindung virtueller Netzwerke

### <a name="isolation-and-segmentation"></a>Isolation und Segmentierung

Azure ermöglicht die Erstellung mehrerer isolierter virtueller Netzwerke. Wenn Sie ein virtuelles Netzwerk einrichten, definieren Sie einen privaten IP-Adressraum (Internetprotokoll) mit öffentlichen oder privaten IP-Adressbereichen. Diesen IP-Adressraum können Sie dann in Subnetze unterteilen und den einzelnen benannten Subnetzen jeweils einen Teil des definierten Adressraums zuordnen.

Für die Namensauflösung können Sie entweder den integrierten Namensauflösungsdienst von Azure verwenden oder das virtuelle Netzwerk für die Verwendung eines internen oder externen DNS-Servers (Domain Name System) konfigurieren.

### <a name="internet-communications"></a>Internetkommunikation

Ein virtueller Computer in Azure kann standardmäßig eine Internetverbindung herstellen. Sie müssen jedoch eine Verbindung mit diesem virtuellen Computer herstellen und ihn steuern. Hierzu können Sie entweder die Azure-Befehlszeilenschnittstelle (Command Line Interface, CLI), das Remotedesktopprotokoll (RDP) oder Secure Shell (SSH) verwenden. Sie können eingehende Kommunikation ermöglichen, indem Sie eine öffentliche IP-Adresse oder einen öffentlichen Load Balancer definieren.

### <a name="communicate-between-azure-resources"></a>Kommunikation zwischen Azure-Ressourcen

Es empfiehlt sich, eine sichere Kommunikation zwischen Azure-Ressourcen zu ermöglichen. Dazu haben Sie zwei Möglichkeiten:

- **Virtuelle Netzwerke:** Virtuelle Netzwerke können nicht nur eine Verbindung mit virtuellen Computern herstellen, sondern auch mit anderen Ressourcen. Hierzu zählen beispielsweise App Service-Umgebungen, Azure Kubernetes Service und VM-Skalierungsgruppen.

- **Dienstendpunkte:** Mithilfe von Dienstendpunkten können Sie eine Verbindung mit anderen Azure-Ressourcentypen (wie etwa Azure SQL-Datenbanken und Speicherkonten) herstellen. Bei diesem Ansatz können Sie mehrere Azure-Ressourcen mit virtuellen Netzwerken verknüpfen und so die Sicherheit erhöhen und ein optimales Routing zwischen Ressourcen sicherstellen.

### <a name="communicate-with-on-premises-resources"></a>Kommunikation mit lokalen Ressourcen

Virtuelle Azure-Netzwerke ermöglichen es Ihnen, Ressourcen in Ihrer lokalen Umgebung und in Ihrem Azure-Abonnement miteinander zu verknüpfen und so ein Netzwerk zu erstellen, das sowohl Ihre lokale Umgebung als auch Ihre Cloudumgebung abdeckt. Für diese Konnektivität stehen drei Mechanismen zur Verfügung:

- **Point-to-Site-VPNs:** Dieser Ansatz gleicht einer VPN-Verbindung, die ein Computer außerhalb Ihrer Organisation mit Ihrem Unternehmensnetzwerk herstellt – allerdings in entgegengesetzter Richtung. In diesem Fall initiiert der Clientcomputer eine verschlüsselte VPN-Verbindung mit Azure, um den Computer mit dem virtuellen Azure-Netzwerk zu verbinden.

- **Site-to-Site-VPNs:** Ein Site-to-Site-VPN verknüpft Ihr lokales VPN-Gerät oder -Gateway mit dem Azure VPN Gateway in einem virtuellen Netzwerk. Dadurch entsteht bisweilen der Eindruck, die Geräte in Azure befänden sich tatsächlich im lokalen Netzwerk. Die Verbindung ist verschlüsselt und internetbasiert.

- **Azure ExpressRoute:** Für Umgebungen, in denen Sie eine höhere Bandbreite und ein noch höheres Maß an Sicherheit benötigen, ist Azure ExpressRoute die beste Lösung. Azure ExpressRoute bietet dedizierte private Konnektivität mit Azure ohne internetbasierte Datenübertragung.

### <a name="route-network-traffic"></a>Weiterleitung von Netzwerkdatenverkehr

Azure leitet standardmäßig Datenverkehr zwischen Subnetzen in beliebigen verbundenen virtuellen Netzwerken, lokalen Netzwerken und dem Internet weiter. Sie können das Routing jedoch steuern und die Einstellungen mit folgen Methoden überschreiben:

- **Routingtabellen:** Mit einer Routingtabelle können Sie Regeln für die Weiterleitung von Datenverkehr definieren. Sie können benutzerdefinierte Routingtabellen erstellen, die steuern, wie Pakete zwischen Subnetzen weitergeleitet werden.

- **Border Gateway Protocol:** Border Gateway Protocol (BGP) kann für Azure-VPN-Gateways oder ExpressRoute verwendet werden, um lokale BGP-Routen zu virtuellen Azure-Netzwerken zu verteilen.

### <a name="filter-network-traffic"></a>Filterung von Netzwerkdatenverkehr

Mit virtuellen Azure-Netzwerken können Sie Datenverkehr zwischen Subnetzen wie folgt filtern:

- **Netzwerksicherheitsgruppen:** Eine Netzwerksicherheitsgruppe ist eine Azure-Ressource, die mehrere Eingangs- und Ausgangssicherheitsregeln enthalten kann. Sie können diese Regeln definieren, um Datenverkehr auf der Grundlage von Faktoren wie Quell- und Ziel-IP-Adresse, Port und Protokoll zuzulassen oder zu blockieren.

- **Virtuelle Netzwerkgeräte:** Ein virtuelles Netzwerkgerät ist ein spezieller virtueller Computer, der mit einem gehärteten Netzwerkgerät vergleichbar ist. Ein virtuelles Netzwerkgerät führt eine bestimmte Netzwerkfunktion aus (beispielsweise eine Firewall oder eine WAN-Optimierung).

## <a name="connect-virtual-networks"></a>Verbindung virtueller Netzwerke

Virtuelle Netzwerke können mittels _Peering_ miteinander verknüpft werden. Peering ermöglicht es Ressourcen in den einzelnen virtuellen Netzwerken, miteinander zu kommunizieren. Da sich diese virtuellen Netzwerke in unterschiedlichen Regionen befinden können, können Sie so über Azure ein globales, miteinander verbundenes Netzwerk erstellen.

## <a name="azure-virtual-network-settings"></a>Einstellungen für virtuelle Azure-Netzwerke

Virtuelle Azure-Netzwerke können über das Azure-Portal, unter Verwendung von Azure PowerShell auf Ihrem lokalen Computer oder mithilfe von Azure Cloud Shell erstellt und konfiguriert werden.

### <a name="create-a-virtual-network"></a>Erstellen eines virtuellen Netzwerks

Bei der Erstellung eines virtuellen Azure-Netzwerks muss eine Reihe von grundlegenden Einstellungen konfiguriert werden. Sie haben auch die Möglichkeit, erweiterte Einstellungen wie mehrere Subnetze, DDoS-Schutz (Distributed Denial of Service) und Dienstendpunkte zu konfigurieren.

![Erstellen des virtuellen Netzwerks](../media-draft/2-create-virtual-network.PNG)

Für ein einfaches virtuelles Netzwerk müssen folgende Einstellungen konfiguriert werden:

- **Netzwerkname:** Dieser Name muss in Ihrem Abonnement (aber nicht global) eindeutig sein. Verwenden Sie einen aussagekräftigen, einprägsamen Namen, der einfach von anderen virtuellen Netzwerken zu unterscheiden ist.

- **Adressraum:** Beim Einrichten eines virtuellen Netzwerks definieren Sie den internen Adressbereich im CIDR-Format (Classless Interdomain Routing). Dieser Adressraum muss innerhalb Ihres Abonnements eindeutig sein. Es ist also beispielsweise nicht möglich, für ein virtuelles Netzwerk den Adressraum 10.0.0.0/24 und für ein anderes den Adressraum 10.1.0.0/8 festzulegen, da sich das Netzwerk 10.1.0.0/8 mit 10.0.0.0/24 überschneidet. Sie können jedoch beispielsweise 10.0.0.0/16 und 10.1.0.0/16 verwenden. 
    > [!NOTE] 
    > Adressräume können nach der Erstellung des virtuellen Netzwerks hinzugefügt werden.

- **Abonnement:** Gilt nur, wenn Sie über mehrere Abonnements verfügen.

- **Ressourcengruppe:** Ein virtuelles Netzwerk muss sich genau wie jede andere Azure-Ressource in einer Ressourcengruppe befinden. Sie können entweder eine vorhandene Ressourcengruppe auswählen oder eine neue Ressourcengruppe erstellen.
- **Standort:** Wählen Sie den gewünschten Standort für das virtuelle Netzwerk aus.

- **Subnetz:** Innerhalb der einzelnen VNet-Adressbereiche können Sie einzelne oder mehrere Subnetze erstellen, um den Adressraum des virtuellen Netzwerks zu partitionieren. Das Routing zwischen den Subnetzen basiert dann auf den standardmäßigen Datenverkehrsrouten. Sie können aber auch benutzerdefinierte Routen definieren. Alternativ können Sie ein Subnetz definieren, das den gesamten Adressbereich des virtuellen Netzwerks umfasst.

    > [!NOTE]
    >Subnetznamen müssen mit einem Buchstaben oder einer Zahl beginnen, mit einem Buchstaben, einer Zahl oder einem Unterstrich enden und dürfen nur Buchstaben, Zahlen, Unterstriche, Punkte oder Bindestriche enthalten.

- **DDoS-Schutz:** Sie haben die Wahl zwischen zwei Optionen: „Basic“ und "Standard“. Der DDoS-Schutz „Standard“ ist ein Premium-Dienst. Weitere Informationen zum DDoS-Schutz „Standard“.

- **Dienstendpunkte:** Hier können Sie Dienstendpunkte aktivieren und in einer Liste auswählen, welche Azure-Dienstendpunkte Sie aktivieren möchten. Mögliche Optionen sind beispielsweise Azure Cosmos DB, Azure Service Bus, Key Vault und Ähnliches.

Klicken Sie nach dem Konfigurieren dieser Einstellungen auf die Schaltfläche **Erstellen**.

### <a name="define-additional-settings"></a>Definieren zusätzlicher Einstellungen

Nach dem Erstellen eines virtuellen Netzwerks können Sie weitere Einstellungen definieren. Dazu zählen unter anderem folgende:

- **Netzwerksicherheitsgruppen:** Netzwerksicherheitsgruppen enthalten Sicherheitsregeln, mit denen Sie die Art des ein- und ausgehenden Netzwerkdatenverkehrs der Subnetze von virtuellen Netzwerken und Netzwerkschnittstellen filtern können. Die Netzwerksicherheitsgruppe muss separat erstellt und anschließend dem virtuellen Netzwerk zugeordnet werden.

- **Routingtabelle:** Azure erstellt automatisch eine Routingtabelle für jedes Subnetz in einem virtuellen Azure-Netzwerk und fügt der Tabelle Systemstandardrouten hinzu. Sie können jedoch benutzerdefinierte Routingtabellen hinzufügen, um den Datenverkehr zwischen virtuellen Netzwerken zu ändern.

Außerdem können Sie die Dienstendpunkte ändern.

![Einstellungen für das virtuelle Netzwerk](../media-draft/2-virtual-network-additional-settings.PNG)

### <a name="configure-virtual-networks"></a>Konfigurieren virtueller Netzwerke

Wenn Sie ein virtuelles Netzwerk erstellt haben, können Sie alle weiteren Einstellungsänderungen im Azure-Portal auf dem Blatt „Virtuelle Netzwerke“ vornehmen. Alternativ können Sie die Änderungen mithilfe von PowerShell-Befehlen oder mithilfe von CLI-Befehlen in Cloud Shell vornehmen.

![Konfigurieren des virtuellen Netzwerks](../media-draft/2-configure-virtual-network.PNG)

Anschließend können Sie Einstellungen auf weiteren untergeordneten Blättern überprüfen und ändern. Zu diesen Einstellungen zählen:

- Adressräume: Sie können der ursprünglichen Definition weitere Adressräume hinzufügen.

- Verbundene Geräte: Verbinden Sie Computer über das virtuelle Netzwerk.

- Subnetze: Fügen Sie weitere Subnetze hinzu.

- Peerings: Verknüpfen Sie virtuelle Netzwerke mittels Peering.

Sie können auch virtuelle Netzwerke überwachen und Probleme mit virtuellen Netzwerken behandeln oder ein Automatisierungsskript für die Generierung des aktuellen virtuellen Netzwerks erstellen.

## <a name="summary"></a>Zusammenfassung

Virtuelle Netzwerke sind leistungsstarke und präzise konfigurierbare Mechanismen für die Verbindungsherstellung zwischen Entitäten in Azure. Sie können Azure-Ressourcen untereinander oder mit lokalen Ressourcen verbinden. Außerdem können Sie Netzwerkdatenverkehr isolieren, filtern und weiterleiten und mithilfe von Azure bei Bedarf die Sicherheit erhöhen.