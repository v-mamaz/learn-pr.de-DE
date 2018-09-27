Damit der Lastenausgleich korrekt funktioniert, müssen Sie vorab Einstellungen konfigurieren, die das Verhalten des Lastenausgleichs steuern. Im Folgenden befassen Sie sich mit der Konfiguration des Netzwerks, des Integritätstests, der Sicherheits- und Lastenausgleichsregeln sowie des Serverpools.

## <a name="steps-for-configuring-a-basic-public-load-balancer"></a>Schritte zum Konfigurieren eines öffentlichen Lastenausgleichs im Tarif „Basic“

In der folgenden Übersicht sind die wichtigsten Schritte zur Konfiguration eines öffentlichen Lastenausgleichs im Tarif „Basic“ aufgeführt. Die Schritte für einen Lastenausgleich im Tarif „Standard“ und für einen internen Lastenausgleich sehen ähnlich aus. Die folgenden vier Punkte müssen bei der Einrichtung berücksichtigt werden:

- Back-End-Server zum Verarbeiten von Anforderungen
- Öffentliche IP-Adresse
- Integritätstest
- Lastenausgleichsregeln

### <a name="backend-servers"></a>Back-End-Server

Zunächst müssen Sie Ihren Back-End-VM-Pool konfigurieren. Die VMs sollten in derselben Verfügbarkeitsgruppe enthalten sein und über eine eigene öffentliche IP-Adresse verfügen (obwohl diese nicht von Ihren öffentlichen Endpunkten verwendet wird).

Sie müssen ein neues virtuelles Netzwerk erstellen und ein Subnetz für den zu verwendenden VM-Pool definieren.

 Falls mehrere VMs die gleichen Dienste bereitstellen, sollten Sie – obwohl dies nicht direkt zum Lastenausgleichsvorgang gehört – eine **Netzwerksicherheitsgruppe (NSG)** verwenden, um sicherzustellen, dass im gesamten VM-Pool die gleichen Firewallregeln angewendet werden. Für VMs, die Webanwendungen hosten, müssen Sie beispielsweise Eingangssicherheitsregeln am Port 80 für HTTP bzw. Port 8080 für HTTPS erstellen.

### <a name="public-ip-address"></a>Öffentliche IP-Adresse

Wenn Sie einen öffentlichen Lastenausgleich im Tarif „Basic“ über das Portal erstellen, wird die **öffentliche IP-Adresse** automatisch als Front-End des Lastenausgleichs konfiguriert.

Teil der Konfiguration des Lastenausgleichs ist der **Back-End-Adresspool**. Dieser enthält die IP-Adressen der virtuellen Netzwerkadapter aller VMs, die mit dem Lastenausgleich verbunden sind und zum Verteilen des Datenverkehrs auf die VMs verwendet werden.

### <a name="health-probe"></a>Integritätstest

Basierend auf der Antwort der VMs auf Integritätsüberprüfungen werden die VMs beim Integritätstest dynamisch zur Lastenausgleichsrotation hinzugefügt oder aus ihr entfernt. Zwischen den Testversuchen liegen standardmäßig 15 Sekunden. Nach zwei aufeinanderfolgenden Testfehlern wird ein virtueller Computer als fehlerhaft eingestuft, und der Datenverkehr wird nicht weitergeleitet, bis der Server wieder online ist.

### <a name="rules"></a>Regeln

Mit den Lastenausgleichsregeln werden die Ports festgelegt, auf denen der Lastenausgleich lauscht und über die der Datenverkehr an die Back-End-VMs weitergeleitet wird. Sie benötigen mindestens eine Regel zum Weiterleiten von Datenverkehr.
