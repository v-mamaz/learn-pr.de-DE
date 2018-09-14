In der Regel werden Änderungen an Serverkonfigurationen mithilfe von Geräten in Ihrer lokalen Umgebung vorgenommen. In diesem Zusammenhang stellen Azure-VMs eine Erweiterung zu dieser Umgebung dar. Sie können die Konfiguration ändern, verwalten, Netzwerke, Open oder Datenverkehr blockiert und mehr über das Azure-Portal, Azure-Befehlszeilenschnittstelle oder Azure PowerShell-Tools.

Unser Server wird ausgeführt, und Apache ist installiert und stellt Seiten zur Verfügung. Unser Sicherheitsteam ist es erforderlich, dass wir alle unsere Server sperren, und wir noch nicht nichts an diesen virtuellen Computer fertig haben. Der Datenverkehr war geöffnet, und Apache hat an Port 80 gelauscht. Lassen Sie uns die Azure-Netzwerkkonfiguration untersuchen, um zu sehen, wie Sie die integrierte Sicherheitsunterstützung nutzen können, um unseren Server zu schützen.

## <a name="opening-ports-in-azure-vms"></a>Öffnen von Ports in Azure-VMs

Standardmäßig sind neue virtuelle Computer gesperrt. 

Apps können ausgehende Anforderungen, aber nur eingehende Datenverkehr zulässig ist, aus dem virtuellen Netzwerk (z. B. andere Ressourcen im selben lokalen Netzwerk) und von Azure Load Balancer (Überprüfungen).

Die Anpassung der Konfiguration für die Unterstützung verschiedener Protokolle im Netzwerk erfolgt in zwei Schritten. Wenn Sie einen neuen virtuellen Computer erstellen, können Sie einige häufig verwendete Ports öffnen (RDP, HTTP, HTTPS und SSH). Wenn Sie allerdings andere Änderungen an der Firewall vornehmen müssen, müssen Sie diese manuell anpassen.

Dies umfasst zwei Schritte:

1. Erstellen Sie eine Netzwerksicherheitsgruppe.
2. Erstellen einer Regel für eingehenden Datenverkehr, die Datenverkehr an den benötigten Ports zulässt.

### <a name="what-is-a-network-security-group"></a>Was ist eine Netzwerksicherheitsgruppe?

Virtuelle Netzwerke (VNets) stellen die Grundlage des Azure-Netzwerkmodells dar und stellen Isolation und Schutz bereit. Netzwerksicherheitsgruppen (NSGs) sind das wichtigste Tool, die, das Sie verwenden, um zu erzwingen und die Regeln für den Netzwerkdatenverkehr auf Netzwerkbetrieb Ebene steuern. Sie stellen eine optionale Sicherheitsebene dar, die eine Firewall für Software darstellt, indem sie eingehenden und ausgehenden Datenverkehr auf dem VNet bereitstellt. 

Sicherheitsgruppen können eine Netzwerkschnittstelle zugeordnet werden (für pro Host Regeln), ein Subnetz im virtuellen Netzwerk (um mehrere Ressourcen zuweisen), oder auf beiden Ebenen. 

#### <a name="security-group-rules"></a>Regeln für Sicherheitsgruppen

Netzwerksicherheitsgruppen verwenden _Regeln_, um Datenverkehr im Netzwerk zuzulassen oder zu blockieren. Jede Regel gibt die Quell- und Zieladresse (oder den entsprechenden Adressbereich), das Protokoll, den Port (oder den Portbereich), die Richtung (eingehend oder ausgehend) sowie eine numerische Priorität an und legt fest, ob der entsprechende Datenverkehr zugelassen oder blockiert werden soll.

![Abbildung, die die Architektur von Netzwerksicherheitsgruppen in zwei verschiedenen Subnetzen zeigt. In einem Subnetz sind zwei virtuelle Computer mit jeweils eigenen Netzwerkschnittstellenregeln vorhanden.  Das Subnetz selbst verfügt über einen Satz von Regeln, die für beide virtuellen Computer gelten. ](../media/7-nsg-rules.png)

Jede Sicherheitsgruppe verfügt über einen Satz von Standardsicherheitsregeln, um die oben beschriebenen Standardnetzwerkregeln anzuwenden. Diese Standardregeln können nicht geändert werden, aber _können_ außer Kraft gesetzt werden.

#### <a name="how-azure-uses-network-rules"></a>So verwendet Azure Netzwerkregeln

Für eingehenden Datenverkehr müssen Sie die Sicherheitsgruppe mit dem Subnetz, und klicken Sie dann die Sicherheitsgruppe verknüpft Azure-Prozessen auf die Netzwerkschnittstelle angewendet. Ausgehender Datenverkehr wird in umgekehrter Reihenfolge verarbeitet (zuerst die Netzwerkschnittstelle, gefolgt vom Subnetz).

> [!WARNING]  
> Beachten Sie, dass Sicherheitsgruppen auf beiden Ebenen optional sind. Wenn keine Sicherheitsgruppe, klicken Sie dann angewendet wird **alle Datenverkehr wird zugelassen.** von Azure. Wenn der virtuelle Computer eine öffentliche IP-Adresse verfügt, könnte dies ein großes Sicherheitsrisiko, sein, insbesondere, wenn das Betriebssystem nicht zu eine integrierten Firewall bereitstellt.

Die Regeln werden ausgewertet, _Prioritätsreihenfolge_, beginnend mit der **niedrigste Priorität** Regel. Ablehnungsregeln **beenden** die Auswertung immer. Wenn eine Netzwerkschnittstellenregel beispielsweise eine ausgehende Anforderung blockiert, wird keine der auf das Subnetz angewandten Regeln überprüft. Damit die Sicherheitsgruppe Datenverkehr zulässt, muss er _alle_ angewendeten Gruppen durchlaufen.

Die letzte Regel ist immer eine **Alle Ablehnen**-Regel. Es handelt sich dabei um eine Standardregel, die sämtlichen Sicherheitsregeln für eingehenden und ausgehenden Datenverkehr mit einer Priorität von 65500 hinzugefügt wird. Das bedeutet, dass Datenverkehr durchlaufen die Sicherheitsgruppe _benötigen Sie eine Zulassungsregel_, oder die endgültige Standardregel wird blockiert werden.

> [!NOTE]  
> SMTP (Port 25) ist ein besonderer Fall. Abhängig von Ihrer Abonnementstufe entspricht, und wenn Ihr Konto erstellt wurde kann ausgehende SMTP-Datenverkehr blockiert werden. Sie können einen Antrag auf Entfernen dieser Einschränkung stellen, wenn Sie dies geschäftlich begründen können.

Nachfolgend erfahren Sie, wie Sie eine Sicherheitsgruppe für diese VM erstellen.

## <a name="creating-network-security-groups"></a>Erstellen von Netzwerk-Sicherheitsgruppen

Sicherheitsgruppen sind verwaltete Ressourcen, die Sie wie beinahe alle Azure-Elemente im Azure-Portal oder über Tools zur Skripterstellung auf Befehlszeilenebene erstellen können. Die Schwierigkeit besteht darin, die Regeln zu definieren. Sehen wir uns an, wie eine neue Regel definiert wird, die den HTTP-Zugriff erlaubt und alles andere blockiert.