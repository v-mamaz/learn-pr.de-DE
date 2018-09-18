Damit der Lastenausgleich korrekt funktioniert, müssen Sie vorab Einstellungen konfigurieren, die das Verhalten des Lastenausgleichs steuern. In diesem Artikel werden wir uns mit der Konfiguration des Netzwerks, des Integritätstests, der Sicherheits- und Lastenausgleichsregeln sowie des Serverpools befassen.

## <a name="steps-to-configure-a-basic-public-load-balancer"></a>Schritte zum Konfigurieren eines öffentlichen Load Balancer Basic

Im Folgenden finden Sie eine Übersicht über die wichtigsten Konfigurationsschritte für einen öffentlichen Load Balancer Basic. Die Vorgehensweise für einen Load Balancer Standard und einen internen Load Balancer ist ähnlich.

### <a name="backend-servers"></a>Back-End-Server

Zunächst müssen Sie Ihren Back-End-VM-Pool konfigurieren. Die VMs sollten in derselben Verfügbarkeitsgruppe enthalten sein und über eine eigene öffentliche IP-Adresse verfügen (obwohl diese nicht wirklich von Ihren öffentlichen Endpunkten verwendet wird).

Sie müssen ein neues virtuelles Netzwerk (VNET) erstellen und ein Subnetz für den zu verwendenden VM-Pool definieren.

Falls mehrere VMs die gleichen Dienste bereitstellen, sollten Sie – obwohl dies nicht direkt zum Lastenausgleich gehört – eine **Netzwerksicherheitsgruppe (NSG)** verwenden, um sicherzustellen, dass im gesamten VM-Pool die gleichen Firewallregeln angewendet werden. Für VMs, die Webanwendungen hosten, müssen Sie beispielsweise Eingangssicherheitsregeln am Port 80 für HTTP bzw. Port 8080 für HTTPS erstellen.

### <a name="public-ip-address"></a>Öffentliche IP-Adresse

Wenn Sie einen öffentlichen Load Balancer Basic im Portal erstellen, wird die **öffentliche IP-Adresse** automatisch als Front-End des Lastenausgleichs konfiguriert.

Teil der Konfiguration des Lastenausgleichs ist der **Back-End-Adresspool**. Dieser enthält die IP-Adressen der virtuellen Netzwerkkarten aller VMs, die mit dem Lastenausgleich verbunden sind und zum Verteilen des Datenverkehrs auf die VMs verwendet werden. 

### <a name="health-probe"></a>Integritätstest

Basierend auf der Antwort der VMs auf Integritätsüberprüfungen werden die VMs beim Integritätstest dynamisch zur Lastenausgleichsrotation hinzugefügt oder aus ihr entfernt.
Das Standardintervall zwischen Testversuchen beträgt 15 Sekunden. Nach zwei aufeinander folgenden Testfehlern wird eine VM als fehlerhaft eingestuft.

### <a name="rules"></a>Regeln

Die Lastenausgleichsregel gibt den Port an, an dem das Front-End lauscht, und den Port, der zum Senden von Datenverkehr an das Back-End verwendet wird.