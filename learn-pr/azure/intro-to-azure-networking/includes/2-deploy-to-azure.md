Der erste Schritt besteht mit hoher Wahrscheinlichkeit darin, Ihre lokale Konfiguration in der Cloud neu zu erstellen.

Mit der folgenden grundlegenden Konfiguration erhalten Sie einen Überblick darüber, wie Netzwerke konfiguriert werden und Netzwerkdatenverkehr an bzw. von Azure gesendet wird.

## <a name="your-e-commerce-site-at-a-glance"></a>Ihre E-Commerce-Website auf einen Blick

Größere Unternehmenssysteme bestehen häufig aus miteinander verbundenen Anwendungen und Diensten, die interagieren. Möglicherweise verfügen Sie über ein Front-End-System, das den Bestand anzeigt und Kunden die Möglichkeit bietet, eine Bestellung aufzugeben. Dieses System kommuniziert unter Umständen mit einer Vielzahl von Webdiensten, um Bestandsdaten bereitzustellen, Benutzerprofile zu verwalten, Kreditkartendaten zu verarbeiten und die Bestellabwicklung anzufordern.

Es gibt verschiedene Strategien und Muster, die von Softwarearchitekten und Entwicklern eingesetzt werden, um diese komplexen Systeme einfacher zu entwerfen, zu erstellen, zu verwalten und zu warten. Wir werfen nun einen Blick auf einige dieser Ansätze und beginnen mit _lose gekoppelten Architekturen_.

#### <a name="benefits-of-loosely-coupled-architectures"></a>Vorteile lose gekoppelter Architekturen

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yHrc]

### <a name="using-an-n-tier-architecture"></a>Verwenden einer n-schichtigen Architektur

Zur Erstellung lose gekoppelter Systeme kann ein _n-schichtiges_ Architekturmuster verwendet werden.

In einer [n-schichtigen Architektur](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) wird eine Anwendung in mindestens zwei logische Schichten aufgeteilt. Höhere Schichten können dabei auf Dienste niedrigerer Schichten zugreifen. Umgekehrt sollte dies jedoch nicht möglich sein.

Schichten sind im Idealfall wiederverwendbar und werden dazu verwendet, unterschiedliche Aufgaben voneinander zu trennen. Eine Schichtenarchitektur verringert auch den Wartungsaufwand. Schichten können unabhängig voneinander geändert oder ersetzt werden können. Zusätzlich können neue Schichten bei Bedarf eingefügt werden.

Unter einer _dreischichtigen_ Anwendung wird eine n-schichtige Anwendung mit drei Schichten verstanden. Auch für Ihre E-Commerce-Webanwendung wird eine dreischichtige Architektur verwendet:

* Die **Webschicht** stellt über einen Browser die Webschnittstelle für Ihre Benutzer bereit.
* In der **Logikschicht** wird die Geschäftslogik ausgeführt.
* Die **Datenschicht** enthält Datenbanken und andere Speicher, die Produktinformationen und Kundenbestellungen enthalten.

Auf der folgenden Abbildung wird der Weg der Benutzeranforderung vom Benutzer bis zur Datenschicht dargestellt.

![Abbildung mit dreischichtiger Architektur, in der jede Schicht auf einem dedizierten virtuellen Computer gehostet wird](../media/2-three-tier.png)

Wenn der Benutzer auf die Schaltfläche zum Aufgeben der Bestellung klickt, wird die Anforderung zusammen mit der Adresse des Benutzers und den Zahlungsinformationen an die Webschicht gesendet. Die Webschicht übergibt diese Informationen der Logikschicht, in der die Zahlungsinformationen überprüft werden und eine Bestandsprüfung durchgeführt wird. Mithilfe der Logikschicht kann die Bestellung anschließend in der Datenschicht gespeichert werden, damit später die Bestellabwicklung eingeleitet werden kann.

## <a name="your-e-commerce-site-running-on-azure"></a>Ihre E-Commerce-Website in Azure

Azure bietet mehrere Möglichkeiten zum Hosten Ihrer Webanwendungen, die von vollständig vorkonfigurierten Umgebungen, in denen Ihr Code gehostet wird, bis hin zu virtuellen Computern reichen, die Sie selbst konfigurieren, anpassen und verwalten.

Angenommen, Sie möchten Ihre E-Commerce-Website auf virtuellen Computern betreiben. In Ihrer Testumgebung in Azure könnte dies etwa wie folgt aussehen. Auf der folgenden Abbildung wird eine Architektur mit drei Schichten dargestellt, die auf virtuellen Computern ausgeführt werden. Zusätzlich sind Sicherheitsfeatures aktiviert, durch die eingehende Anforderungen eingeschränkt werden. 

![Abbildung mit dreischichtiger Architektur, in der jede Schicht auf einem eigenständigen virtuellen Computer gehostet wird Jeder virtuelle Computer befindet sich in einem eigenständigen virtuellen Netzwerk und verfügt über eine eigene IP-Adresse. Jedes virtuelle Netzwerk verfügt über eine Netzwerksicherheitsgruppe, in der offene Ports aufgeführt sind.](../media/2-test-deployment.png)

Im Folgenden erhalten Sie einen Überblick über die einzelnen Komponenten.

:::row:::
  :::column:::
    ![Mit Stecknadel gekennzeichneter Standort, der eine Azure-Region darstellt](../media/2-azure-region.png)
  :::column-end:::
    :::column span="3"::: **Was ist eine Azure-Region?**

Eine _Region_ ist ein Azure-Rechenzentrum an einem bestimmten geografischen Standort. Beispiele für Regionen sind „USA, Osten“, „USA, Westen“ und „Europa, Norden“. Wie Sie sehen, wird in diesem Fall die Anwendung in der Region „USA, Osten“ ausgeführt.

  :::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Zwei virtuelle Computer, die in einem virtuellen Netzwerk ausgeführt werden](../media/2-azure-vnet.png)
  :::column-end:::
    :::column span="3"::: **Was ist ein virtuelles Netzwerk?**

Ein _virtuelles Netzwerk_ ist ein logisch isoliertes Netzwerk in Azure. Wenn Sie bereits Netzwerke in Hyper-V, VMware oder in anderen öffentlichen Clouds eingerichtet haben, sind Sie sicherlich mit virtuellen Azure-Netzwerken vertraut.

Die Web-, Logik- und Datenschichten verfügen jeweils über einen eigenen virtuellen Computer. Jeder virtuelle Computer gehört zu einem virtuellen Netzwerk.

Benutzer interagieren direkt mit der Webschicht, weshalb der virtuelle Computer in dieser Schicht über eine öffentliche IP-Adresse verfügt. Mit der Logik- und Datenschicht interagieren die Benutzer hingegen nicht. Diese virtuellen Computer verfügen dementsprechend über jeweils eine private IP-Adresse.

Die physische Hardware wird von Azure-Rechenzentren für Sie verwaltet. Die virtuellen Netzwerke konfigurieren Sie mithilfe von Software, wodurch Sie virtuelle Netzwerke wie eigene Netzwerke behandeln können. Beispielsweise haben Sie die Möglichkeit, ein virtuelles Netzwerk in Subnetze zu unterteilen, um besser steuern zu können, wie das Netzwerk IP-Adressen zuweist. Außerdem können Sie andere Netzwerke – beispielsweise das öffentliche Internet oder Netzwerke innerhalb des privaten IP-Adressraums – festlegen, die über das virtuelle Netzwerk erreichbar sind.

  :::column-end:::
:::row-end:::
:::row:::
  :::column:::
    ![Zwei virtuelle Computer mit einer gemeinsamen Netzwerksicherheitsgruppe](../media/2-azure-nsg.png)
  :::column-end:::
    :::column span="3"::: **Was ist eine Netzwerksicherheitsgruppe?**

Eine _Netzwerksicherheitsgruppe_ (NSG) lässt eingehenden Netzwerkdatenverkehr für Ihre Azure-Ressourcen zu oder blockiert diesen. Eine Netzwerksicherheitsgruppe ist mit einer Firewall auf Cloudebene für Ihr Netzwerk vergleichbar.

Der virtuelle Computer in der Webschicht lässt beispielsweise eingehenden Datenverkehr für die Ports 22 (SSH) und 80 (HTTP) zu. Die Netzwerksicherheitsgruppe dieses virtuellen Computers lässt über diese Ports eingehenden Datenverkehr aus allen Quellen zu. Sie können die Netzwerksicherheitsgruppe so konfigurieren, dass nur Datenverkehr aus bekannten Quellen, z.B. von vertrauenswürdigen IP-Adressen, akzeptiert wird.

> [!NOTE]
> Über Port 22 können Sie eine SSH-Verbindung mit Linux-Systemen herstellen. In unserem Szenario ist Port 22 aus didaktischen Gründen offen. In der Praxis können Sie den VPN-Zugriff auf Ihr virtuelles Netzwerk konfigurieren und so die Sicherheit erhöhen.

  :::column-end:::
:::row-end:::

## <a name="summary"></a>Zusammenfassung

Ihre dreischichtige Anwendung wird nun in Azure in der Region „USA, Osten“ ausgeführt. Eine _Region_ ist ein Azure-Rechenzentrum an einem bestimmten geografischen Standort.

Jede Schicht kann nur auf Dienste untergeordneter Schichten zugreifen. Der virtuelle Computer in der Webschicht verfügt über eine öffentliche IP-Adresse, da Datenverkehr über das Internet empfangen wird. Die virtuellen Computer in der niedrigeren Logik- und Datenschicht verfügen jeweils über private IP-Adressen, da sie nicht direkt über das Internet kommunizieren.

Mit _virtuellen Netzwerken_ können Sie zugehörige Systeme gruppieren und isolieren. Über _Netzwerksicherheitsgruppen_ steuern Sie, welcher Datenverkehr über ein virtuelles Netzwerk übertragen wird.

Die hier beschriebene Konfiguration erleichtert Ihnen die ersten Schritte. Wenn Sie jedoch Ihre E-Commerce-Website für die Produktionsphase in der Cloud bereitstellen, werden vermutlich die gleichen Probleme wie bei Ihrer lokalen Bereitstellung auftreten.
