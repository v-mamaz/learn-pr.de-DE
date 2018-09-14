Der erste Schritt werden Sie wahrscheinlich zum Neuerstellen Ihrer lokalen Konfigurations in der Cloud.

Diese Basiskonfiguration bietet Ihnen einen Eindruck davon, wie Netzwerke konfiguriert sind und wie Netzwerkverkehr aus Azure verschiebt.

## <a name="your-e-commerce-site-at-a-glance"></a>Ihre E-Commerce-Website auf einen Blick

Größere Unternehmenssysteme bestehen häufig mehrere miteinander verbundene Anwendungen und Dienste, die reibungslos zusammenarbeiten. Sie möglicherweise ein Front-End-System, das zeigt erfasst und ermöglicht es Kunden, die einen Auftrag zu erstellen. Die möglicherweise mit einer Vielzahl von Web Services bieten die Inventurdaten, Verwalten von Benutzerprofilen, Prozess-Kreditkarten und Request-Fulfillment verarbeiteten Bestellungen kommunizieren.

Es gibt verschiedene Strategien und Muster, die von Softwarearchitekten und Entwicklern eingesetzt werden, um diese komplexe Systeme einfacher zu entwerfen, erstellen, verwalten und warten. Sehen wir uns einige davon, beginnend mit _lose gekoppelter Architekturen_.

### <a name="benefits-of-a-loosely-coupled-architecture"></a>Vorteile einer lose gekoppelten Architektur

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yHrc]

### <a name="using-an-n-tier-architecture"></a>Verwenden eine Architektur mit N Ebenen

Ein Architekturmuster, die verwendet werden kann, um lose gekoppelte Systeme zu erstellen ist _N-schichtige_.

Ein [N-schichtige Architektur](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) unterteilt eine Anwendung in zwei oder mehrere logische Ebenen. Aus Sicht der Systemarchitektur ein höherer Tarif auf Dienste zugreifen, von einem niedrigen Tarif, aber eine niedrigere Ebene sollten nie auf einen höheren Tarif zugreifen.

Ebenen können Belange abzutrennen und im Idealfall einfacher wiederverwendet werden sollen. Verwenden eine geschichtete Architektur vereinfacht auch den Verwaltungsaufwand. Ebenen unabhängig ersetzt oder aktualisiert werden können, und die neuen Tarife eingefügt werden können, falls erforderlich.

Unter einer _dreischichtigen_ Architektur wird eine n-schichtige Anwendung mit drei Schichten verstanden. Auch für Ihre E-Commerce-Webanwendung wird eine dreischichtige Architektur verwendet:

* Die **Webebene** die Weboberfläche für Ihre Benutzer über einen Browser bietet.
* Die **Anwendungsebene** Geschäftslogik ausgeführt.
* Die **Datenebene** enthält Datenbanken und anderen Speicher, die Product Informationen und Kunde Bestellungen enthalten.

Die folgende Abbildung zeigt den Fluss der Anforderung des Benutzers, für die Datenebene.

![Eine Abbildung, zeigt eine Architektur mit drei Ebenen, in dem jede Ebene in einem dedizierten virtuellen Computer gehostet wird.](../media/2-three-tier.png)

Wenn der Benutzer auf die Schaltfläche zum Aufgeben der Bestellung klickt, wird die Anforderung zusammen mit der Adresse des Benutzers und den Zahlungsinformationen an die Webschicht gesendet. Die Webschicht übergibt diese Informationen der Logikschicht, in der die Zahlungsinformationen überprüft werden und eine Bestandsprüfung durchgeführt wird. Die Anwendungsebene kann dann die Reihenfolge in der Datenebene, später für die Erfüllung übernommen werden speichern.

## <a name="your-e-commerce-site-running-on-azure"></a>Ihre E-Commerce-Website in Azure

Azure bietet viele verschiedene Arten von Umgebungen, die vollständig vorkonfiguriert, dass Ihre Webanwendungen zu hosten, die Ihren Code, um virtuelle Computer, die Sie konfigurieren hosten, anpassen und verwalten.

Angenommen, Sie möchten Ihre E-Commerce-Website auf virtuellen Computern betreiben. In Ihrer Testumgebung in Azure könnte dies etwa wie folgt aussehen. Die folgende Abbildung zeigt eine Architektur mit drei Ebenen auf virtuellen Computern ausgeführt werden, mit den Sicherheitsfunktionen aktiviert, um eingehende Anforderungen zu beschränken. 

![Eine Abbildung, zeigt eine Architektur mit drei Ebenen, in dem jede Ebene auf einem separaten virtuellen Computer ausgeführt wird. Jeder virtuelle Computer wird mit der Bezeichnung mit der IP-Adresse und befindet sich in einem eigenen virtuellen Netzwerk. Jedes virtuelles Netzwerk verfügt über eine Netzwerksicherheitsgruppe, die die geöffneten Ports aufgeführt.](../media/2-test-deployment.png)

Im Folgenden erhalten Sie einen Überblick über die einzelnen Komponenten.

### <a name="what-is-an-azure-region"></a>Was ist eine Azure-Region?

Eine _Region_ ist ein Azure-Rechenzentrum an einem bestimmten geografischen Standort. Beispiele für Regionen sind „USA, Osten“, „USA, Westen“ und „Europa, Norden“. Wie Sie sehen, wird die Anwendung in der Region „USA, Osten“ ausgeführt.

### <a name="what-is-a-virtual-network"></a>Was ist ein virtuelles Netzwerk?

Ein _virtuelles Netzwerk_ ist ein logisch isoliertes Netzwerk in Azure. Wenn Sie bereits Netzwerke in Hyper-V, VMware oder in anderen öffentlichen Clouds eingerichtet haben, sind Sie sicherlich mit virtuellen Azure-Netzwerken vertraut.

Die Web-, Logik- und Datenschichten verfügen jeweils über einen eigenen virtuellen Computer. Jeder virtuelle Computer gehört zu einem virtuellen Netzwerk.

Benutzer interagieren direkt mit der Webschicht, weshalb der virtuelle Computer in dieser Schicht über eine öffentliche IP-Adresse verfügt. Mit der Logik- und Datenschicht interagieren die Benutzer hingegen nicht. Diese virtuellen Computer verfügen dementsprechend über jeweils eine private IP-Adresse.

Die physische Hardware wird von Azure-Rechenzentren für Sie verwaltet. Die virtuellen Netzwerke konfigurieren Sie mithilfe von Software, wodurch Sie virtuelle Netzwerke wie eigene Netzwerke behandeln können. Beispielsweise haben Sie die Möglichkeit, ein virtuelles Netzwerk in Subnetze zu unterteilen, um besser steuern zu können, wie das Netzwerk IP-Adressen zuweist. Welche anderen Netzwerken, die Ihrem virtuelle Netzwerk erreichen kann, wählen Sie auch, ob dies das öffentliche Internet oder anderen Netzwerken in der privaten IP-Adressbereich ist ein.

### <a name="whats-a-network-security-group"></a>Was ist eine Netzwerksicherheitsgruppe?

Eine _Netzwerksicherheitsgruppe_ (NSG) lässt eingehenden Netzwerkdatenverkehr für Ihre Azure-Ressourcen zu oder blockiert diesen. Eine Netzwerksicherheitsgruppe ist mit einer Firewall auf Cloudebene für Ihr Netzwerk vergleichbar.

Der virtuelle Computer in der Webschicht lässt beispielsweise eingehenden Datenverkehr für die Ports 22 (SSH) und 80 (HTTP) zu. Hierbei lässt jede Netzwerksicherheitsgruppe Datenverkehr aus allen Quellen zu. Sie können nun die Netzwerksicherheitsgruppe so konfigurieren, dass nur Datenverkehr aus bekannten Quellen, z.B. von vertrauenswürdigen IP-Adressen, akzeptiert wird.

> [!NOTE]
> Über Port 22 können Sie eine SSH-Verbindung mit Linux-Systemen herstellen. In unserem Szenario ist Port 22 aus didaktischen Gründen offen. In der Praxis können Sie den VPN-Zugriff auf Ihr virtuelles Netzwerk konfigurieren und so die Sicherheit erhöhen.

## <a name="summary"></a>Zusammenfassung

Ihre dreischichtige Anwendung wird nun in Azure in der Region „USA, Osten“ ausgeführt. Eine _Region_ ist ein Azure-Rechenzentrum an einem bestimmten geografischen Standort.

Jede Schicht kann nur auf Dienste untergeordneter Schichten zugreifen. Der virtuellen Computer auf der Webebene ausgeführt verfügt über eine öffentliche IP-Adresse aus, da sie aus dem Internet Datenverkehr empfängt. Die virtuellen Computer in den niedrigeren Tarifen, die Anwendungs- und Datenebenen, jede haben private IP-Adressen, da sie nicht direkt über das Internet kommunizieren.

Mit _virtuellen Netzwerken_ können Sie zugehörige Systeme gruppieren und isolieren. Über _Netzwerksicherheitsgruppen_ steuern Sie, welcher Datenverkehr über ein virtuelles Netzwerk übertragen wird.

Die Konfiguration, die Sie hier gesehen haben, ist ein guter Anfang. Aber wenn Sie Ihre e-Commerce-Website für die Produktion in der Cloud bereitstellen, wahrscheinlich führen Sie in den gleichen Problemen wie in der lokalen Bereitstellung.
