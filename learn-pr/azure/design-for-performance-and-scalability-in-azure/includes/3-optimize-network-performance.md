Die Netzwerkleistung kann erhebliche Auswirkungen auf die Benutzerfreundlichkeit haben. In komplexen Architekturen mit vielen verschiedenen Diensten kann die Minimierung der Wartezeit bzw. Latenz an den einzelnen Hops enorme Auswirkungen auf die Leistung insgesamt haben. In dieser Einheit wird die Bedeutung der Netzwerklatenz erläutert und erklärt, wie Sie diese in Ihrer Architektur reduzieren können. Ferner wird beschrieben, wie bei Lamna Healthcare Strategien zur Minimierung der Netzwerklatenz zwischen den Azure-Ressourcen sowie zwischen den Benutzern und Azure eingeführt wurden.

## <a name="the-importance-of-network-latency"></a>Die Bedeutung der Netzwerklatenz

Latenz ist ein Maß für die Verzögerung. Die Netzwerklatenz ist die Zeit, die benötigt wird, um von einer Quelle über eine Netzwerkinfrastruktur an ein Ziel zu gelangen. Dieser Zeitraum wird allgemein als Roundtripverzögerung bezeichnet oder als die erforderliche Zeit für die Route von der Quelle zum Ziel und wieder zurück.

In einer herkömmlichen Datencenterumgebung kann die Wartezeit minimal sein, da sich Ressourcen häufig am selben Standort befinden und eine gemeinsame Infrastruktur nutzen. Die Zeit von der Quelle zum Ziel ist kürzer, wenn der physische Abstand zwischen Ressourcen gering ist.

Eine Cloudumgebung ist im Gegensatz dazu für Skalierung konzipiert. In der Cloud gehostete Ressourcen befinden sich möglicherweise nicht im selben Rack oder im selben Datencenter oder nicht einmal in derselben Region. Dieses Konzept der Verteilung kann sich bei der Netzwerkkommunikation auf die Roundtripzeit auswirken. Zwar sind alle Azure-Regionen über ein schnelles Glasfaserbackbone miteinander verbunden, doch stellt die Lichtgeschwindigkeit nach wie vor eine physikalische Beschränkung dar. Bei Aufrufen zwischen Diensten an unterschiedlichen physischen Standorten tritt nach wie vor eine Netzwerklatenz auf, die in direktem Zusammenhang mit dem Abstand zwischen den Diensten steht.

Hinzu kommt, dass umso mehr Roundtrips benötigt werden, je aktiver eine Anwendung ist. Jeder Roundtrip erzeugt eine Wartezeit und trägt somit zur Gesamtwartezeit bei. Die folgende Abbildung zeigt, dass es sich bei der vom Benutzer wahrgenommenen Wartezeit um die Kombination der Roundtrips handelt, die zum Verarbeiten der Anforderung erforderlich sind.

![Eine Abbildung der Netzwerklatenz zwischen Ressourcen an verschiedenen geografischen Standorten in der Cloud.](../media/3-networkLatency.png)

Betrachten wir nun, wie die Leistung zwischen den einzelnen Azure-Ressourcen und zwischen Endbenutzern und Azure-Ressourcen verbessert werden kann.

## <a name="latency-among-multiple-azure-resources"></a>Wartezeit zwischen verschiedenen Azure-Ressourcen

Angenommen, bei Lamna Healthcare wird für ein neues Patientenbuchungssystem mit einem Webserver und einer Datenbank in der Azure-Region „Europa, Westen“ ein Pilottest durchgeführt. Die Website ruft statische Medienobjekte (Bilder, JavaScript, Stylesheets) aus Azure Blob Storage in derselben Region ab. Bei dieser Architektur sind die Daten nur kurze Zeit unterwegs, da sich die Ressourcen innerhalb einer Region befinden.

Angenommen, der Pilottest verläuft gut und wird auf Benutzer in Australien ausgeweitet. Für diese Benutzer macht sich die Roundtripzeit von Irland nach Australien bemerkbar, wenn sie eine Website anzeigen möchten, und die Benutzerfreundlichkeit lässt aufgrund der Netzwerklatenz zu wünschen übrig.

Das Lamna Healthcare-Team beschließt, eine weitere Front-End-Instanz und ein weiteres Speicherkonto in der Region „Australien, Osten“ zu hosten, um die Wartezeit für Benutzer zu reduzieren. Mit diesem Design wird zwar die Zeit verkürzt, die der Webserver benötigt, um Inhalte für Endbenutzer zurückzugeben, die Benutzerfreundlichkeit ist jedoch weiterhin unzureichend, da bei der Kommunikation zwischen dem Front-End-Webserver in der Region „Australien, Osten“ und der Datenbank in der Region „Europa, Westen“ eine erhebliche Wartezeit auftritt.

Es gibt mehrere Möglichkeiten, wie wir die übrige Wartezeit reduzieren können:

- Erstellen eines Lesereplikats der Datenbank in der Region „Australien, Osten“. Dadurch funktionieren Lesevorgänge gut, bei Schreibvorgängen tritt jedoch nach wie vor eine Latenz auf. Die Georeplikation einer Azure SQL-Datenbank ermöglicht Lesereplikate.
- Synchronisieren der Daten zwischen den einzelnen Regionen mit Azure SQL-Datensynchronisierung.
- Verwenden einer global verteilten Datenbank wie Azure Cosmos DB. Damit können Lese- und Schreibvorgänge ortsunabhängig durchgeführt werden.

Das Ziel hierbei ist es, die Netzwerklatenz zwischen den einzelnen Ebenen der Anwendung zu minimieren. Wie diese Aufgabe gelöst wird, hängt von der Anwendung und der Datenarchitektur ab. Azure stellt jedoch Mechanismen zur Bewältigung dieser Aufgabe bei verschiedenen Diensten bereit.

## <a name="latency-in-the-context-of-users-to-azure"></a>Latenz im Kontext zwischen Benutzern und Azure

Bisher haben wir die Latenz zwischen den Azure-Ressourcen betrachtet. Wir sollten jedoch auch die Latenz zwischen Benutzern und der Cloudanwendung berücksichtigen. Ziel ist es, die Bereitstellung der Front-End-Benutzeroberfläche für die Benutzer zu optimieren. Betrachten wir einige Möglichkeiten zur Verbesserung der Netzwerkleistung zwischen Endbenutzern und der Anwendung.

### <a name="use-a-dns-load-balancer-for-endpoint-path-optimization"></a>Verwenden eines DNS-Lastenausgleichs zur Optimierung des Endpunktpfads

Bei dem Lamna Healthcare-Beispiel haben wir gesehen, dass das Team einen zusätzlichen Front-End-Webknoten in der Region „Australien, Osten“ erstellt hat. Endbenutzer müssen jedoch explizit angeben, welchen Front-End-Endpunkt sie verwenden möchten. Als Entwickler einer Lösung möchte Lamna Healthcare das System für seine Benutzer so angenehm wie möglich gestalten.

Hier könnte Microsoft Azure Traffic Manager helfen. Traffic Manager ist ein DNS-basierter Lastenausgleich, mit dessen Hilfe Sie Datenverkehr innerhalb und zwischen Azure-Regionen verteilen können. Benutzer müssen bei der Verwendung dieses Diensts nicht mehr zu einer bestimmten Instanz des Web-Front-Ends navigieren, sondern werden von Traffic Manager anhand einer Reihe von Merkmalen weitergeleitet:

- **Priorität**: Sie geben eine sortierte Liste von Front-End-Servern an. Wenn der Server mit der höchsten Priorität nicht verfügbar ist, wird der Benutzer von Traffic Manager zur nächsten verfügbaren Instanz weitergeleitet.
- **Gewichtet**: Sie legen für jede Front-End-Instanz eine Gewichtung fest. Traffic Manager verteilt den Datenverkehr entsprechend diesen definierten Verhältnissen.
- **Leistung**: Benutzer werden basierend auf der Netzwerklatenz von Traffic Manager an die nächstgelegene Front-End-Instanz weitergeleitet.
- **Geografisch**: Sie können für Front-End-Bereitstellungen geografische Regionen einrichten und Benutzer basierend auf Datenhoheitsmandaten oder auf der Lokalisierung von Inhalten weiterleiten.

Traffic Manager-Profile können auch geschachtelt werden. Sie könnten Benutzer zunächst mit geografischem Routing durch verschiedene geografische Regionen (beispielsweise Europa und Australien) und anschließend mithilfe der leistungsorientierten Routingmethode an lokale Front-End-Bereitstellungen weiterleiten.

Beachten Sie, dass Lamna Healthcare einen Web-Front-End in Westeuropa und Australien bereitgestellt hat. Gehen wir davon aus, dass mit der primären Bereitstellung in „Europa, Westen“ eine Azure SQL-Datenbank und in „Australien, Osten“ ein Lesereplikat bereitgestellt wurde. Gehen wir ferner davon aus, dass die Anwendung für Leseabfragen eine Verbindung mit der lokalen SQL-Instanz herstellen kann.

Das Team stellt eine Traffic Manager-Instanz im Leistungsmodus bereit und fügt die beiden Front-End-Instanzen als Traffic Manager-Profile hinzu. Als Endbenutzer navigieren Sie zu einem benutzerdefinierten Domänennamen (z. B. „lamnahealthcare.com“), und von dort aus werden Sie zu Traffic Manager weitergeleitet. Traffic Manager gibt den DNS-Namen der Front-Ends in „Europa, Westen“ oder „Australien, Osten“ basierend auf der besten Netzwerklatenzleistung zurück.

Dabei ist zu beachten, dass dieser Lastenausgleich nur über DNS gesteuert wird und weder ein Inline-Lastenausgleich noch eine Zwischenspeicherung stattfindet. Traffic Manager gibt einfach den DNS-Namen des nächsten Front-Ends an den Benutzer zurück.

### <a name="use-cdn-to-cache-content-close-to-users"></a>Verwenden von CDN zum Zwischenspeichern von Inhalten in der Nähe von Benutzern

Auf der Website wird wahrscheinlich irgendeine Art von statischem Inhalt verwendet (entweder ganze Seiten oder Objekte wie Bilder und Videos). Dieser Inhalt könnte Benutzern bei Verwendung eines Inhaltsübermittlungsnetzwerks (CDN, Content Delivery Network) wie Azure CDN schneller bereitgestellt werden. 

Wenn Lamna Inhalte in Azure CDN bereitstellt, werden die jeweiligen Elemente auf mehrere Server weltweit kopiert. Angenommen, eines dieser Elemente ist ein aus Blob-Speicher bereitgestelltes Video: `HowToCompleteYourBillingForms.MP4`. Das Team konfiguriert die Website anschließend so, dass jeder Benutzerzugriff auf das Video nicht auf den Blob-Speicher verweist, sondern auf den nächstgelegenen CDN-Edgeserver. Bei diesem Ansatz befinden sich Inhalte näher am Ziel, wodurch die Wartezeit reduziert und die Benutzerfreundlichkeit verbessert wird. Die folgende Abbildung zeigt, wie Inhalte durch die Verwendung von Azure CDN näher am Ziel platziert und dadurch die Wartezeit reduziert sowie die Benutzerfreundlichkeit verbessert werden.

![Abbildung, die die Verwendung von Azure CDN zum Reduzieren der Wartezeit veranschaulicht.](../media/3-cdnSketch.png)

Content Delivery Networks _können_ auch zum Hosten von zwischengespeicherten dynamischen Inhalten verwendet werden. Hier ist jedoch besondere Aufmerksamkeit gefordert, da zwischengespeicherte Inhalte im Vergleich zur Quelle veraltet sein können. Der Kontextablauf kann durch Festlegen einer Gültigkeitsdauer (Time To Live, TTL) gesteuert werden. Wenn für die Gültigkeitsdauer ein zu hoher Wert festgelegt wird, werden möglicherweise veraltete Inhalte angezeigt, und der Cache muss bereinigt werden.

Eine Möglichkeit zur Verarbeitung zwischengespeicherter Inhalte ist die Funktion **Beschleunigung dynamischer Websites**, mit der die Leistung von Webseiten mit dynamischen Inhalten verbessert werden kann. Mit der Funktion „Beschleunigung dynamischer Websites“ kann außerdem ein Pfad mit geringer Wartezeit zu weiteren Diensten in der Lösung (z. B. zu einem API-Endpunkt) bereitgestellt werden.

### <a name="use-expressroute-for-connectivity-from-on-premises-to-azure"></a>Verwenden von ExpressRoute für die Konnektivität zwischen lokalen Umgebungen und Azure

Darüber hinaus sollte auch die Netzwerkkonnektivität zwischen der lokalen Umgebung und Azure optimiert werden. Für Benutzer, die eine Verbindung mit Anwendungen herstellen, die auf VMs oder in PaaS-Angeboten wie Azure App Service gehostet werden, sollten Sie eine optimale Verbindung mit Ihren Anwendungen sicherstellen. 

Sie können immer das öffentliche Internet verwenden, um Benutzer mit Ihren Diensten zu verbinden. Die Leistung des Internets kann jedoch schwanken und durch äußere Faktoren beeinträchtigt werden. Zudem werden Sie nicht all Ihre Dienste über das Internet verfügbar machen und eine private Verbindung mit Ihren Azure-Ressourcen nutzen wollen.

Site-to-Site-VPN über das Internet ist ebenfalls eine Option. Bei Architekturen mit hohem Durchsatz kann sich die Wartezeit aufgrund des Mehraufwands durch das VPN und der Schwankungen bei der Internetverbindung jedoch erheblich erhöhen.

Hier kann Azure ExpressRoute Abhilfe schaffen. ExpressRoute ist eine private, dedizierte Verbindung zwischen Ihrem Netzwerk und Azure, die eine garantierte Leistung bietet und sicherstellt, dass Endbenutzer den besten Pfad zu all Ihren Azure-Ressourcen nutzen. Die folgende Abbildung zeigt, wie eine ExpressRoute-Verbindung Konnektivität zwischen lokalen Anwendungen und Azure-Ressourcen bereitstellt.

![Ein Architekturdiagramm, das die ExpressRoute-Verbindung zwischen dem Kundennetzwerk und Azure-Ressourcen veranschaulicht.](../media/3-expressroute-connection-overview.png)

Betrachten wir noch einmal das Lamna-Szenario. Bei Lamna wurde beschlossen, die Endbenutzererfahrung für Benutzer in den Einrichtungen des Unternehmens durch die Bereitstellung einer ExpressRoute-Verbindung in „Australien, Osten“ und „Europa, Westen“ weiter zu verbessern. So kann für die Endbenutzer eine direkte Verbindung mit dem Buchungssystem bereitgestellt und die geringstmögliche Wartezeit für die Anwendung sichergestellt werden.

## <a name="summary"></a>Zusammenfassung

Um Endbenutzern die bestmögliche Leistung gewährleisten zu können, muss bei der Architektur die Netzwerklatenz berücksichtigt werden. Vor diesem Hintergrund haben wir einige Möglichkeiten zur Verringerung der Netzwerklatenz zwischen Endbenutzern und Azure sowie zwischen den einzelnen Azure-Ressourcen betrachtet. Als Nächstes befassen wir uns mit der Optimierung der Speicherleistung.