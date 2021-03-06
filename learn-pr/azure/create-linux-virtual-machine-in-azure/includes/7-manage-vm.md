In der Regel werden Änderungen an Serverkonfigurationen mithilfe von Geräten in Ihrer lokalen Umgebung vorgenommen. In diesem Zusammenhang stellen Azure-VMs eine Erweiterung zu dieser Umgebung dar. Sie können über das Azure-Portal, die Azure CLI oder Azure PowerShell-Tools die Konfiguration ändern, Netzwerke verwalten, den Datenverkehr öffnen oder blockieren und vieles mehr.

Unser Server wird ausgeführt, und Apache ist installiert und stellt Seiten zur Verfügung. Unser Sicherheitsteam verlangt, dass wir alle unsere Server sperren, und wir haben für diesen virtuellen Computer noch keine derartige Aktion ausgeführt. Der Datenverkehr war geöffnet, und Apache hat an Port 80 gelauscht. Lassen Sie uns die Azure-Netzwerkkonfiguration untersuchen, um zu sehen, wie Sie die integrierte Sicherheitsunterstützung nutzen können, um unseren Server zu schützen.

## <a name="opening-ports-in-azure-vms"></a>Öffnen von Ports auf virtuellen Azure-Computern

Standardmäßig sind neue virtuelle Computer gesperrt. 

Apps können ausgehende Anforderungen vornehmen, aber der einzige zulässige eingehende Datenverkehr stammt aus dem virtuellen Netzwerk (z.B. andere Ressourcen im gleichen lokalen Netzwerk) und aus dem Load Balancer von Azure (Testprüfungen).

Die Anpassung der Konfiguration für die Unterstützung verschiedener Protokolle im Netzwerk erfolgt in zwei Schritten. Wenn Sie einen neuen virtuellen Computer erstellen, können Sie einige häufig verwendete Ports öffnen (RDP, HTTP, HTTPS und SSH). Wenn Sie allerdings andere Änderungen an der Firewall vornehmen müssen, müssen Sie diese manuell anpassen.

Dies umfasst zwei Schritte:

1. Erstellen Sie eine Netzwerksicherheitsgruppe.
2. Erstellen einer Regel für eingehenden Datenverkehr, die Datenverkehr an den benötigten Ports zulässt.

### <a name="what-is-a-network-security-group"></a>Was ist eine Netzwerksicherheitsgruppe?

Virtuelle Netzwerke (VNets) stellen die Grundlage des Azure-Netzwerkmodells dar und stellen Isolation und Schutz bereit. Netzwerksicherheitsgruppen (NSGs) sind das wichtigste Tool zum Erzwingen und Überwachen von Regeln für Netzwerkdatenverkehr auf Netzwerkebene. Sie stellen eine optionale Sicherheitsebene dar, die eine Firewall für Software darstellt, indem sie eingehenden und ausgehenden Datenverkehr auf dem VNet bereitstellt. 

Außerdem können sie einer Netzwerkschnittstelle (für hostspezifische Regeln), einem Subnetz im VNet (das für mehrere Ressourcen verwendbar ist) oder beiden zugeordnet werden. 

#### <a name="security-group-rules"></a>Regeln für Netzwerksicherheitsgruppen

NGS verwenden _Regeln_, um Datenverkehr im Netzwerk zuzulassen oder zu blockieren. Jede Regel erkennt die Quell- und Zieladresse (oder den Bereich), das Protokoll, den Port (oder den Bereich), die Richtung (eingehend oder ausgehend) sowie eine numerische Priorität und stellt fest, ob Datenverkehr, der der Regel entspricht, zugelassen oder blockiert wird.

![Abbildung, die die Architektur von Netzwerksicherheitsgruppen in zwei verschiedenen Subnetzen zeigt. In einem Subnetz sind zwei virtuelle Computer mit jeweils eigenen Netzwerkschnittstellenregeln vorhanden.  Das Subnetz selbst verfügt über einen Satz von Regeln, die für beide virtuellen Computer gelten. ](../media/7-nsg-rules.png)

Jede Sicherheitsgruppe verfügt über mehrere Standardsicherheitsregeln, damit die oben beschriebenen Standardnetzwerkregeln angewendet werden können. Diese Standardregeln können zwar nicht verändert, aber _überschrieben_ werden.

#### <a name="how-azure-uses-network-rules"></a>So verwendet Azure Netzwerkregeln

Für eingehenden Datenverkehr verarbeitet Azure zuerst die Sicherheitsgruppe, die dem Subnetz zugeordnet ist, und anschließend die Sicherheitsgruppe, die der Netzwerkschnittstelle zugeordnet ist. Ausgehender Datenverkehr wird in umgekehrter Reihenfolge verarbeitet (zuerst die Netzwerkschnittstelle, gefolgt vom Subnetz).

> [!WARNING]  
> Beachten Sie, dass Sicherheitsgruppen auf beiden Ebenen optional sind. Wenn keine Sicherheitsgruppe verwendet wird, lässt Azure **sämtlichen Datenverkehr** zu. Wenn der virtuelle Computer über eine öffentliche IP-Adresse verfügt, kann dies ein ernsthaftes Risiko darstellen, insbesondere wenn das Betriebssystem keine integrierte Firewall zur Verfügung stellt.

Die Regeln werden je nach _Priorität_ bewertet, angefangen bei der Regel mit der **niedrigsten Priorität**. Ablehnungsregeln **beenden** die Auswertung immer. Wenn eine Netzwerkschnittstellenregel beispielsweise eine ausgehende Anforderung blockiert, wird keine der auf das Subnetz angewandten Regeln überprüft. Damit die Sicherheitsgruppe Datenverkehr zulässt, muss er _alle_ angewendeten Gruppen durchlaufen.

Die letzte Regel ist immer eine **Alle Ablehnen**-Regel. Es handelt sich dabei um eine Standardregel, die sämtlichen Sicherheitsregeln für eingehenden und ausgehenden Datenverkehr mit einer Priorität von 65500 hinzugefügt wird. Dies bedeutet, dass der Datenverkehr die Sicherheitsgruppe durchlaufen muss, und _Sie müssen über eine Zulassungsregel verfügen_. Andernfalls wird er von der letzten Standardregel blockiert.

> [!NOTE]  
> SMTP (Port 25) ist ein Sonderfall. Abhängig von Ihrer Abonnementebene und dem Erstelldatum Ihres Kontos wird SMTP-Datenverkehr möglicherweise blockiert. Sie können einen Antrag auf Entfernen dieser Einschränkung stellen, wenn Sie dies geschäftlich begründen können.

Nachfolgend erfahren Sie, wie Sie eine Sicherheitsgruppe für diesen virtuellen Computer erstellen.

## <a name="creating-network-security-groups"></a>Erstellen von Netzwerksicherheitsgruppen

Sicherheitsgruppen sind verwaltete Ressourcen, die Sie wie beinahe alle Azure-Elemente im Azure-Portal oder über Tools zur Skripterstellung auf Befehlszeilenebene erstellen können. Die Schwierigkeit besteht darin, die Regeln zu definieren. Sehen wir uns an, wie eine neue Regel definiert wird, die den HTTP-Zugriff erlaubt und alles andere blockiert.