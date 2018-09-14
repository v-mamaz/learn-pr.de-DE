Es wurde bereits erläutert, wie Sie mithilfe von **Azure Load Balancer** Hochverfügbarkeit erreichen und die Downtime minimieren.

Aber auch wenn Ihre E-Commerce-Website über Hochverfügbarkeit verfügt, wird dadurch die Latenz nicht reduziert, und es wird nicht automatisch Resilienz für verschiedene Regionen hergestellt.

Nachfolgend wird erläutert, wie Sie dafür sorgen können, dass eine US-amerikanische Website für Benutzer in Europa oder Asien schneller laden kann.

## <a name="what-is-network-latency"></a>Was ist Netzwerklatenz?

Der Begriff _Latenz_ bezieht sich auf die Zeit, die Daten benötigen, um das Netzwerk zu passieren. Die Latenz wird in der Regel in Millisekunden gemessen.

In welchem Zusammenhang steht die Latenz mit der Bandbreite? Der Begriff „Bandbreite“ bezieht sich auf die Menge an Daten, die innerhalb einer Verbindung verarbeitet werden kann. Der Begriff „Latenz“ bezieht sich hingegen auf die Zeit, die Daten benötigen, um ihr Ziel zu erreichen.

Faktoren wie der von Ihnen verwendete Verbindungstyp und der Aufbau Ihrer Anwendung können Auswirkungen auf die Latenz haben. Den wichtigsten Faktor stellt allerdings die Distanz dar.

Als Beispiel soll Ihre E-Commerce-Website in Azure dienen. Diese befindet sich in der Region „USA, Osten“. In der Regel werden Daten schneller nach Atlanta (Distanz von 400 Meilen) als nach London gesendet (Distanz von 4000 Meilen).

Ihre E-Commerce-Website sendet Standardcode in HTML, CSS und JavaScript sowie Bilder. Wenn mehrere Dateien gesendet werden, ist die Netzwerklatenz entsprechend höher. Wie können Sie also die Latenz für Benutzer reduzieren, die sich weit entfernt befinden?

## <a name="scale-out-to-different-regions"></a>Horizontales Hochskalieren auf verschiedene Regionen

Azure stellt überall auf der Welt in verschiedenen Regionen Rechenzentren zur Verfügung.

Der Bau eines Rechenzentrums ist sehr teuer. Kosten sind nicht der einzige Faktor. Geben Sie die Stromversorgung, Kühlung und Mitarbeiter um behalten Sie Ihre Systeme, die an jedem Standort ausgeführt werden sollen. Daher wäre es viel zu teuer, ein Replikat eines Rechenzentrums an einem anderen Standort zu errichten. Aber auf diese Weise mit Azure kann Kosten wesentlich, da Azure bereits die Ausrüstung und die Mitarbeiter verfügt.

Wenn Sie identische Replikate Ihres Diensts in mehreren Regionen erstellen, ist dies eine Möglichkeit, um die Latenz zu reduzieren. HThe, die folgende Abbildung zeigt ein Beispiel für globale Bereitstellung.

![Eine Abbildung, die eine Weltkarte mit drei Azure-Rechenzentren hervorgehoben angezeigt. Jedes Rechenzentrum wird durch einen eindeutigen Domänennamen gekennzeichnet sind.](../media/4-global-deployment.png)

Auf dem Diagramm sehen Sie Ihre E-Commerce-Website, die in drei Azure-Regionen ausgeführt wird: „USA, Osten“, „Europa, Norden“ und „Asien, Osten“. Beachten Sie die einzelnen DNS-Namen. Nachfolgend wird erläutert, wie Sie Benutzer unter der contoso.com-Domäne mit dem Dienst verbinden können, der diesem am nächsten gelegen ist.

## <a name="use-traffic-manager-to-route-users-to-the-closest-endpoint"></a>Verwenden des Traffic Managers zum Weiterleiten von Benutzern an den nächstgelegenen Endpunkt

Eine Antwort ist **Azure Traffic Manager**. Der Traffic Manager verwendet den DNS-Server, der dem Benutzer am nächsten gelegen ist, um Benutzerdatenverkehr an einen global verteilten Endpunkt weiterzuleiten. Die folgende Abbildung zeigt die von Traffic Manager-Rolle.

![Eine Abbildung, die mit Azure Traffic Manager-routing eine benutzeranforderung an das nächstgelegene Rechenzentrum. ](../media/4-traffic-manager.png)

Der Traffic Manager kann den zwischen Client und Server übergebenen Datenverkehr nicht sehen. Stattdessen leitet es den Webbrowser des Clients an einem bevorzugten Endpunkt. Traffic Manager können Datenverkehr auf verschiedene Weise, wie z. B. an den Endpunkt mit der geringsten Wartezeit weiter.

Obwohl hier nicht gezeigt, kann dieses Setup auch Ihrer lokalen Bereitstellung in Kalifornien unter enthalten. Sie können Traffic Manager auf Ihren eigenen lokalen Netzwerken, verbinden, können Sie Ihre vorhandene Data Center-Investitionen zu verwalten. Alternativ können Sie Ihre Anwendung auch vollständig in die Cloud verschieben. Die Entscheidung liegt bei Ihnen.

## <a name="compare-load-balancer-to-traffic-manager"></a>Vergleichen Sie Load Balancer an Traffic Manager

Azure Load Balancer verteilt den Datenverkehr auf die gesamte Region, damit Ihre Dienste hochverfügbarer und resilienter sind. Traffic Manager arbeitet auf DNS-Ebene und weist den Client an einem bevorzugten Endpunkt. Dieser Endpunkt kann sich in der Region befinden, die dem Benutzer am nächsten gelegen ist.

Load Balancer und Traffic Manager sowohl machen Ihre Dienste stabiler, jedoch etwas anders. Wenn Load Balancer einen nicht reagierenden virtuellen Computer erkennt, leitet er Datenverkehr an andere virtuelle Computer im Pool. Der Traffic Manager überwacht die Integrität der Endpunkte. Wenn der Traffic Manager im Gegensatz dazu einen Endpunkt erkennt, der nicht reagiert, leitet er Datenverkehr an den Endpunkt weiter, der am nächsten gelegen ist und reagiert.

## <a name="summary"></a>Zusammenfassung

Die geografische Distanz ist einer der Hauptfaktoren, die die Latenz beeinflussen. Mithilfe des Traffic Managers können Sie Kopien Ihres Dienst in mehreren geografischen Regionen hosten. Auf diese Weise können Benutzer in den USA sowie in Europa und Asien Ihre E-Commerce-Website ohne Probleme nutzen.
