Bevor Sie der Load Balancer ordnungsgemäß funktioniert, müssen Sie Einstellungen konfigurieren, die der Load-Balancer-Verhalten zu steuern. Sie werden hier sehen Sie sich im Netzwerk konfigurieren Integritätstest, Sicherheitsregeln, lastenausgleichsregeln und Serverpool.

## <a name="steps-for-configuring-a-basic-public-load-balancer"></a>Schritte zum Konfigurieren von einem öffentlichen basic Load balancer

Folgendes ist eine Übersicht über die wichtigsten Konfigurationsschritte für einen öffentlichen basic Load Balancer. Die Schritte für die Standard-Lastenausgleich und einer internen Load Balancer werden ähnlich.

### <a name="back-end-servers"></a>Back-End-Server

Zunächst müssen Sie Ihre Back-End-Pool virtueller Computer zu konfigurieren. Die virtuellen Computer in derselben verfügbarkeitsgruppe und ihre eigenen öffentliche IP-Adresse (obwohl dies nicht tatsächlich durch Ihren öffentlichen Endpunkten verwendet wird).

Sie müssen ein neues virtuelles Netzwerk erstellen und definieren ein Subnetz für die VM-Pool verwenden.

 Wenn Sie mehrere virtuelle Computer, der die gleichen Dienste bereitstellt haben, sollten Sie verwenden eine **Netzwerksicherheitsgruppe (NSG)** um sicherzustellen, dass die gleichen Firewallregeln an Stelle innerhalb des VM-Pools (obwohl dies nicht Teil der tatsächliche Prozess für den Lastenausgleich ist) . Beispielsweise für virtuelle Computer hosten von Webanwendungen, müssen Sie Sicherheitsregeln für eingehende an Port 80 für HTTP bzw. Port 8080 für HTTP zu erstellen.

### <a name="public-ip-address"></a>Öffentliche IP-Adresse

Bei der Erstellung eines öffentlichen basic-Lastenausgleichs, die über das Portal oder die **öffentliche IP-Adresse** wird automatisch als Front-End des Lastenausgleichs konfiguriert.

Ist Teil der Konfiguration des Load Balancers den **Back-End-Adresspool**, enthält die IP-Adressen jedes virtuellen Computers virtuelle NICs, die mit dem Load Balancer verbunden sind, und zum Verteilen von Datenverkehr an die virtuellen Computer verwendet. 

### <a name="health-probe"></a>Integritätstest

Abhängig von der Reaktion auf Integritätsüberprüfungen werden der Load Balancer-Rotation durch den Integritätstest dynamisch virtuelle Computer hinzugefügt oder daraus entfernt.
Es werden standardmäßig 15 Sekunden zwischen testversuchen. Nach zwei aufeinander folgender Testfehler wird eine VM als fehlerhaft angesehen.

### <a name="rules"></a>Regeln

Der Load Balancer-Regel gibt an, der Port, dem das Front-End lauscht und den Port zum Senden von Datenverkehr an das Back-End verwendet.
