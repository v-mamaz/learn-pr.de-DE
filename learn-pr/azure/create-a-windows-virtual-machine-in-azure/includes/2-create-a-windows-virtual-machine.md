Ihr Unternehmen hat sich dazu entschlossen, die Videodaten seiner Verkehrskameras in Azure mithilfe von VMs zu verwalten. Um die verschiedenen Codecs auszuführen, müssen zuerst die VMs erstellt werden. Außerdem muss eine Verbindung mit den VMs hergestellt und mit diesen interagiert werden. In dieser Einheit erfahren Sie, wie Sie eine VM über das Azure-Portal erstellen. Sie konfigurieren die VM für das RDP, wählen ein VM-Image aus, und wählen die entsprechende Speicheroption.

## <a name="introduction-to-windows-virtual-machines-in-azure"></a>Einführung in virtuelle Windows-Computer in Azure

Azure-VMs sind skalierbare bedarfsgesteuerte Cloud Computing-Ressourcen. Diese sind mit virtuellen Computern vergleichbar, die in Windows Hyper-V gehostet werden. Sie umfassen einen Prozessor, den Arbeitsspeicher, den Speicher und Netzwerkressourcen. Sie können virtuelle Computer wie bei Hyper-V beliebig starten und beenden und über das Portal oder mit der Azure CLI verwalten. Sie können auch einen RDP-Client verwenden, um direkt eine Verbindung mit der Windows-Desktopbenutzeroberfläche (UI) herzustellen und die VM so verwenden, als ob Sie bei einem lokalen Windows-Computer angemeldet wären.

## <a name="create-resources-for-a-windows-vm"></a>Erstellen von Ressourcen für eine Windows-VM

Beim Erstellen einer Windows-VM in Azure können Sie auch Ressourcen zum Hosten der VM erstellen. Wie bei anderen Azure-Diensten benötigen Sie eine **Ressourcengruppe**. In der Regel werden andere Dienste eingeschlossen, die im Zusammenhang mit der VM in der gleichen Ressourcengruppe stehen, einschließlich die Folgenden:

* Der virtuelle Computer
* Speicher
* Virtuelle Netzwerke 
* Netzwerkschnittstellen
* Subnetz
* Öffentliche IP-Adresse

Bei der Erstellung einer neuen VM können Sie entweder eine vorhandene Ressourcengruppe verwenden oder eine neue erstellen.

## <a name="choose-the-vm-image"></a>Auswählen des VM-Image

Das Auswählen eines Images ist eine der wichtigsten Entscheidungen, die Sie beim Erstellen einer VM berücksichtigen müssen. Ein Image ist eine Vorlage, die zum Erstellen einer VM verwendet wird. Diese Vorlagen enthalten ein Betriebssystem und häufig auch andere Software, z.B. Entwicklungstools oder Webhostingumgebungen.

Alle Komponenten, die auf einem Computer installiert werden können, können in einem Image enthalten sein, was ein leistungsstarkes Feature darstellt. Sie können eine VM über ein Image erstellen, das genau für die Aufgaben vorkonfiguriert ist, die Sie benötigen, beispielsweise zum Hosten einer ASP.NET Core-App.

Sie können optional eigene Images erstellen und hochladen, dies würde jedoch den Rahmen dieses Modul sprengen.

> [!Note] 
> Eventuell wird Ihnen ein Feature mit dem Namen „Virtueller Computer (klassisch)“ auffallen. Hierbei handelt es sich um ein Legacyfeature, das für Kunden unterstützt wird, die bereits Instanzen erstellt haben. Bei neuen Workloads benötigen Sie das Feature „Virtueller Azure-Computer“ oder kurz „Virtuelle Computer“.

## <a name="sizing-your-vm"></a>Ändern der Größe Ihrer VM

Ein virtueller Computer weist wie ein physischer Computer eine bestimmte Menge an Arbeitsspeicher und CPU-Leistung auf. Azure bietet eine Reihe von VMs mit unterschiedlichen Größen zu unterschiedlichen Preisen an. Diese VMs reichen von Entwicklungs- und Testimages der A-Serie für den Einstieg bis hin zur D-Serie für allgemeines Computing. Dazu gehören die H-Serie für leistungsstarke Computeanforderungen und die N-Serie für GPU-optimierte Rollen (Grafikprozessor) optimiert.

Wie Sie später im Modul sehen werden, können wir die Größe einer VM nach ihrer Erstellung ändern, wofür diese jedoch heruntergefahren werden muss, was zu Ausfallzeiten bei unseren Workloads führen könnte.

## <a name="choosing-storage-options"></a>Auswählen von Speicheroptionen

Die nächste Auswahl bei der Angabe einer VM ist die Festplattentechnologie. Zu den Optionen zählt ein konventionelles Festplattenlaufwerk (HDD) oder ein moderneres Solid State Drive (SSD). SSD-Speicher sind in ihrer Verwendung kostspieliger, bieten jedoch eine bessere Leistung, insbesondere in Umgebungen, die eine hohe Datenübertragung oder eine hohe E/A-Frequenz unterstützen.

> [!Note] 
> Anwendungen in Azure Virtual Machines können zudem eine Verbindung mit anderen Formen von Persistenz in Azure wie Azure Cosmos DB und Azure Blob Storage herstellen.
