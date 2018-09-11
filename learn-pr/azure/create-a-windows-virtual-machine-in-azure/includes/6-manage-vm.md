Es wurde bereits erläutert, wie Sie benutzerdefinierte Software installieren, einen FTP-Server einrichten und die VM so konfigurieren, dass sie Videodateien empfängt. Sie können allerding nicht über einen FTP-Server eine Verbindung mit einer öffentlichen IP-Adresse herstellen. 

In der Regel werden Änderungen an Serverkonfigurationen mithilfe von Geräten in Ihrer lokalen Umgebung vorgenommen. In diesem Zusammenhang stellen Azure-VMs eine Erweiterung zu dieser Umgebung dar. Sie können mithilfe des Azure-Portals, der Azure CLI oder der Azure PowerShell-Tools Änderungen an Konfigurationen vornehmen, Netzwerke verwalten und Datenverkehr zulassen oder blockieren.

Einige der grundlegenden Informationen und die Verwaltungsoptionen im Bereich **Übersicht** der VM wurden bereits erläutert. Nachfolgend wird ausführlicher auf Netzwerkkonfigurationen eingegangen.

## <a name="opening-ports-in-azure-vms"></a>Öffnen von Ports in Azure-VMs

<!-- TODO: Azure portal is inconsistent here in applying the NSG.
By default, new VMs are locked down. 

Apps can make outgoing requests, but the only inbound traffic allowed is from the virtual network (e.g. other resources on the same local network), and from Azure's Load Balancer (probe checks). -->

Sie können die Konfiguration in zwei Schritten ändern, sodass FTP unterstützt wird. Wenn Sie eine neue VM erstellen, können Sie einige häufig verwendete Ports öffnen (RDP, HTTP, HTTPS und SSH). Weitere Änderungen an der Firewall müssen Sie allerdings manuell vornehmen.

Dies umfasst zwei Schritte:

1. Erstellen Sie eine Netzwerksicherheitsgruppe.
2. Erstellen Sie eine eingehende Regel, die Datenverkehr für eine aktive FTP-Unterstützung auf den Ports 20 und 21 zulässt.

### <a name="what-is-a-network-security-group"></a>Was ist eine Netzwerksicherheitsgruppe?

Virtuelle Netzwerke (VNets) stellen die Grundlage des Azure-Netzwerkmodells dar und stellen Isolation und Schutz bereit. Netzwerksicherheitsgruppen werden in erster Linie dazu verwendet, Regeln zum Netzwerkdatenverkehr auf Netzwerkebene zu erzwingen und zu überwachen. Sie stellen eine optionale Sicherheitsebene dar, die eine Firewall für Software darstellt, indem sie eingehenden und ausgehenden Datenverkehr auf dem VNet bereitstellt. 

Außerdem können sie einer Netzwerkschnittstelle (für hostspezifische Regeln), einem Subnetz im VNet (das für mehrere Ressourcen verwendbar ist) oder beiden zugeordnet werden. 

#### <a name="security-group-rules"></a>Regeln für Sicherheitsgruppen

Netzwerksicherheitsgruppen verwenden _Regeln_, um Datenverkehr im Netzwerk zuzulassen oder zu blockieren. Jede Regel erkennt die Quell- und Zieladresse (oder den Bereich), das Protokoll, den Port (oder den Bereich), die Richtung (eingehend oder ausgehend) sowie eine numerische Priorität und stellt fest, ob Datenverkehr, der der Regel entspricht, zugelassen oder blockiert wird.

![Regeln für Netzwerksicherheitsgruppen](../media/7-nsg-rules.png)

Jede Sicherheitsgruppe verfügt über mehrere Standardsicherheitsregeln, damit die oben beschriebenen Standardnetzwerkregeln angewendet werden können. Diese Standardregeln können zwar nicht verändert, aber dafür _überschrieben_ werden.

#### <a name="how-azure-uses-network-rules"></a>So verwendet Azure Netzwerkregeln

Für eingehenden Datenverkehr verarbeitet Azure erst die Sicherheitsgruppen, die dem Subnetz zugeordnet sind, und anschließend die Sicherheitsgruppen, die der Netzwerkschnittstelle zugeordnet sind. Ausgehender Datenverkehr wird in umgekehrter Reihenfolge verarbeitet (zuerst die Netzwerkschnittstelle, gefolgt vom Subnetz).

> [!WARNING]
> Beachten Sie, dass Sicherheitsgruppen auf beiden Ebenen optional sind. Wenn keine Sicherheitsgruppe verwendet wird, lässt Azure **sämtlichen Datenverkehr** zu. Wenn die VM über eine öffentliche IP-Adresse verfügt, kann dies ein ernsthaftes Risiko darstellen, insbesondere wenn das Betriebssystem keine Firewall zur Verfügung stellt.

Die Regeln werden je nach _Priorität_ bewertet, angefangen bei der Regel mit der **niedrigsten Priorität**. Ablehnungsregeln **beenden** die Auswertung immer. Wenn beispielsweise eine ausgehende Anforderung von einer Netzwerkschnittstellenregel blockiert wird, werden sämtliche Regeln, die auf das Subnetz angewendet werden, nicht mehr überprüft. Damit die Sicherheitsgruppe Datenverkehr zulässt, muss dieser _alle_ angewendeten Gruppen durchlaufen.

Die letzte Regel ist immer eine **Alle Ablehnen**-Regel. Es handelt sich dabei um eine Standardregel, die sämtlichen Sicherheitsregeln für eingehenden und ausgehenden Datenverkehr mit einer Priorität von 65500 hinzugefügt wird. D.h., der Datenverkehr muss die Sicherheitsgruppe durchlaufen, und _Sie müssen über eine Zulassungsregel verfügen_, damit dieser nicht von der letzten Standardregel blockiert wird.

> [!NOTE]
> Bei SMTP (Port 25) handelt es sich um einen Sonderfall. Abhängig von Ihrer Abonnementstufe und dem Erstelldatum Ihres Kontos, wird SMTP-Datenverkehr möglicherweise blockiert. Sie können einen Antrag auf Entfernen dieser Beschränkung stellen, wenn Sie dies geschäftlich begründen können.

Nachfolgend erfahren Sie, wie Sie eine Sicherheitsgruppe für diese VM erstellen.

## <a name="creating-network-security-groups"></a>Erstellen von Netzwerksicherheitsgruppen

Sicherheitsgruppen sind verwaltete Ressourcen, die Sie wie beinahe alle Azure-Elemente im Azure-Portal oder über Tools zur Skripterstellung auf Befehlszeilenebene erstellen können. Die Schwierigkeit besteht darin, die Regeln zu definieren. Nachfolgend wird erläutert, wie Sie neue Regeln erstellen können, um den Zugriff auf FTP zuzulassen.