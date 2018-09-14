Wir haben unsere benutzerdefinierte Software installiert, einen FTP-Server eingerichtet und den virtuellen Computer für den Empfang von Videodateien konfiguriert. Allerdings können wir keine FTP-Verbindung mit unserer öffentlichen IP-Adresse herstellen, da sie blockiert wird. 

In der Regel werden Änderungen an der Serverkonfiguration über Geräte in Ihrer lokalen Umgebung vorgenommen. In diesem Sinne können virtuelle Azure-Computer als Erweiterung dieser Umgebung betrachtet werden. Sie können mithilfe des Azure-Portals, der Azure CLI oder der Azure PowerShell-Tools Änderungen an Konfigurationen vornehmen, Netzwerke verwalten und Datenverkehr zulassen oder blockieren.

Sie haben bereits einige der grundlegenden Informationen und Verwaltungsoptionen des Bereichs **Übersicht** für den virtuellen Computer gesehen. Hier gehen wir etwas ausführlicher auf die Netzwerkkonfiguration ein.

## <a name="opening-ports-in-azure-vms"></a>Öffnen von Ports auf virtuellen Azure-Computern

<!-- TODO: Azure portal is inconsistent here in applying the NSG.
By default, new VMs are locked down. 

Apps can make outgoing requests, but the only inbound traffic allowed is from the virtual network (e.g. other resources on the same local network), and from Azure's Load Balancer (probe checks). -->

Sie können die Konfiguration in zwei Schritten ändern, sodass FTP unterstützt wird. Bei der Erstellung eines neuen virtuellen Computers können Sie einige gängige Ports öffnen (RDP, HTTP, HTTPS und SSH). Weitere Änderungen an der Firewall müssen Sie allerdings manuell vornehmen.

Der Prozess umfasst zwei Schritte:

1. Erstellen einer Netzwerksicherheitsgruppe
2. Erstellen einer Eingangsregel für eine aktive FTP-Unterstützung, die Datenverkehr an den Ports 20 und 21 zulässt

### <a name="what-is-a-network-security-group"></a>Was ist eine Netzwerksicherheitsgruppe?

Virtuelle Netzwerke (VNETs) stellen die Grundlage des Azure-Netzwerkmodells dar und sorgen für Isolation und Schutz. Netzwerksicherheitsgruppen (NSGs) sind das wichtigste Tool zur Erzwingung und Steuerung von Regeln für Netzwerkdatenverkehr auf Netzwerkebene. NSGs sind eine optionale Sicherheitsebene mit einer Softwarefirewall zur Filterung von eingehendem und ausgehendem Datenverkehr für das VNET. 

Außerdem können sie einer Netzwerkschnittstelle (für hostspezifische Regeln), einem Subnetz im VNet (das für mehrere Ressourcen verwendbar ist) oder beiden zugeordnet werden. 

#### <a name="security-group-rules"></a>Regeln für Sicherheitsgruppen

NGS verwenden _Regeln_, um Datenverkehr im Netzwerk zuzulassen oder zu blockieren. Jede Regel gibt die Quell- und Zieladresse (oder den entsprechenden Adressbereich), das Protokoll, den Port (oder den Portbereich), die Richtung (eingehend oder ausgehend) sowie eine numerische Priorität an und legt fest, ob der entsprechende Datenverkehr zugelassen oder blockiert werden soll. Die folgende Abbildung zeigt NSG-Regeln, die auf Subnetz- und Netzwerkschnittstellenebene angewendet wurden.

![Abbildung, die die Architektur von Netzwerksicherheitsgruppen in zwei verschiedenen Subnetzen zeigt. In einem Subnetz sind zwei virtuelle Computer mit jeweils eigenen Netzwerkschnittstellenregeln vorhanden.  Das Subnetz selbst verfügt über einen Satz von Regeln, die für beide virtuellen Computer gelten.](../media/7-nsg-rules.png)

Jede Sicherheitsgruppe verfügt über einen Satz von Standardsicherheitsregeln, um die oben beschriebenen Standardnetzwerkregeln anzuwenden. Diese Standardregeln können zwar nicht verändert, aber sie können _überschrieben_ werden.

#### <a name="how-azure-uses-network-rules"></a>Verwendung von Netzwerkregeln durch Azure

Für eingehenden Datenverkehr verarbeitet Azure zuerst die Sicherheitsgruppe, die dem Subnetz zugeordnet ist, und anschließend die Sicherheitsgruppe, die der Netzwerkschnittstelle zugeordnet ist. Ausgehender Datenverkehr wird in umgekehrter Reihenfolge verarbeitet (also erst die Netzwerkschnittstelle, dann das Subnetz).

> [!WARNING]
> Beachten Sie, dass Sicherheitsgruppen auf beiden Ebenen optional sind. Wenn keine Sicherheitsgruppe verwendet wird, lässt Azure **sämtlichen Datenverkehr** zu. Wenn der virtuelle Computer über eine öffentliche IP-Adresse verfügt, kann dies ein ernsthaftes Risiko darstellen – insbesondere, wenn das Betriebssystem keine Firewall bereitstellt.

Die Regeln werden je nach _Priorität_ bewertet, angefangen bei der Regel mit der **niedrigsten Priorität**. Ablehnungsregeln führen immer zur **Beendigung** der Auswertung. Wenn also beispielsweise eine ausgehende Anforderung durch eine Netzwerkschnittstellenregel blockiert wird, werden sämtliche Regeln, die auf das Subnetz angewendet werden, nicht mehr überprüft. Damit die Sicherheitsgruppe Datenverkehr zulässt, muss dieser _alle_ angewendeten Gruppen durchlaufen.

Die letzte Regel ist immer eine Regel vom Typ **Alle ablehnen**. Diese Standardregel wird jeder Sicherheitsgruppe für eingehenden und ausgehenden Datenverkehr mit der Priorität 65.500 hinzugefügt. D.h., der Datenverkehr muss die Sicherheitsgruppe durchlaufen, und _Sie müssen über eine Zulassungsregel verfügen_, damit dieser nicht von der letzten Standardregel blockiert wird.

> [!NOTE]
> SMTP (Port 25) ist ein Sonderfall. Abhängig von Ihrer Abonnementstufe und dem Erstelldatum Ihres Kontos wird ausgehender SMTP-Datenverkehr möglicherweise blockiert. Sie können einen Antrag auf Entfernen dieser Einschränkung stellen, wenn Sie dies geschäftlich begründen können.

Nachfolgend erfahren Sie, wie Sie eine Sicherheitsgruppe für diese VM erstellen.

## <a name="creating-network-security-groups"></a>Erstellen von Netzwerksicherheitsgruppen

Sicherheitsgruppen sind verwaltete Ressourcen, die Sie wie beinahe alle Azure-Elemente über das Azure-Portal oder mithilfe von Skripterstellungstools auf Befehlszeilenebene erstellen können. Die Schwierigkeit besteht darin, die Regeln zu definieren. Im nächsten Teil erfahren Sie, wie Sie eine neue Regel erstellen, um FTP-Zugriff zu ermöglichen.