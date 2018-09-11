Wenn beim Entwerfen die Hochverfügbarkeit berücksichtigt wird, kann eine Anwendung oder ein Prozess auch dann weiter ausgeführt werden, wenn negative Ereignisse eintreten oder widrige Bedingungen herrschen. Aber was können Sie tun, wenn das Ereignis so schwerwiegend ist, dass Daten verloren gehen, und Sie nicht verhindern können, dass Ihre Apps und Prozesse ausfallen? Sie müssen über einen Plan für Notfälle verfügen. Ihnen sollte bewusst sein, welche Ziele und Erwartungen für die Wiederherstellung gelten, welche Kosten und Einschränkungen mit Ihrem Plan verbunden sind und wie Sie vorgehen müssen.

## <a name="what-is-disaster-recovery"></a>Was ist die Notfallwiederherstellung?

Bei der Notfallwiederherstellung geht es um *die Wiederherstellung nach schwerwiegenden Ereignissen*, die zu Ausfallzeiten und Datenverlust führen. Ein Notfall ist ein einzelnes größeres Ereignis mit sehr starken und länger andauernden Auswirkungen, denen über die Hochverfügbarkeitsfunktionen der Anwendung nicht begegnet werden kann.

Beim Begriff „Notfall“ (bzw. „Katastrophe“) wird häufig an *Naturkatastrophen* (Erdbeben, Überschwemmungen, Tropenstürme usw.) gedacht, aber es gibt noch viele andere Arten von Notfällen. Eine Bereitstellung oder ein Upgrade, bei der bzw. dem schwere Fehler auftreten, kann dazu führen, dass sich eine App in einem nicht erkennbaren Zustand befindet. Leichte Fehler bei der Implementierung oder Konfiguration können das Schreiben von fehlerhaften Daten oder das Löschen von Daten, die als beständig angesehen werden, nach sich ziehen. Böswillige Hacker können Daten beschädigen oder löschen und andere Arten von Schäden verursachen, sodass eine App in den Offlinezustand versetzt wird oder einen Teil ihrer Funktionalität verliert.

Unabhängig von der Ursache sind die einzigen Gegenmittel nach einem Notfall ein gut definierter, getesteter Plan für die Notfallwiederherstellung und eine Anwendung, die so entworfen wurde, dass Maßnahmen für die Notfallwiederherstellung aktiv unterstützt werden.

## <a name="how-to-create-a-disaster-recovery-plan"></a>Erstellen eines Plans für die Notfallwiederherstellung

Ein Plan für die Notfallwiederherstellung ist ein einzelnes Dokument mit den Details zu den Verfahren, die für die Wiederherstellung nach einem Datenverlust und Ausfallzeiten aufgrund eines Notfalls erforderlich sind. Außerdem ist darin angegeben, wer die Leitung bei der Durchführung dieser Maßnahmen innehat. Bediener sollten den Plan als Anleitung zum Wiederherstellen der Anwendungskonnektivität und der Daten nach einem Notfall verwenden können. Ein ausführlicher Plan für die Notfallwiederherstellung in Schriftform ist von entscheidender Bedeutung, um sicherzustellen, dass ein akzeptables Ergebnis erzielt wird: Der Prozess zum Erstellen des Plans trägt zur Erstellung eines vollständigen Bilds der Anwendung bei, und die sich ergebenden niedergeschriebenen Schritte fördern das Treffen von guten Entscheidungen und sind die Grundlage für die weitere Bearbeitung in der von Panik erfüllten und chaotischen Zeit nach einem Notfallereignis.

Zum Erstellen eines Plans für die Notfallwiederherstellung ist Expertenwissen in Bezug auf die Workflows, Daten, Infrastruktur und Abhängigkeiten einer Anwendung erforderlich.

### <a name="risk-assessment-and-process-inventory"></a>Risikobewertung und Prozessbestandsdaten

Der erste Schritt beim Erstellen eines Plans für die Notfallwiederherstellung ist die Durchführung einer Risikoanalyse, mit der die Auswirkungen unterschiedlicher Arten von Notfällen auf die Anwendung untersucht werden. Die genaue Art eines Notfalls ist für die Risikoanalyse nicht so wichtig wie die potenziellen Auswirkungen aufgrund von Datenverlust und Ausfallzeiten der Anwendung. Untersuchen Sie verschiedene Arten von hypothetischen Notfällen, und versuchen Sie, sich die spezifischen Auswirkungen vorzustellen: Bei einem zielgerichteten schädlichen Angriff können beispielsweise Code oder Daten verändert werden, woraus sich andere Auswirkungen als bei einem Erdbeben ergeben, bei dem die Netzwerkkonnektivität und die Datacenterverfügbarkeit gestört werden.

Bei der Risikobewertung müssen *alle* Prozesse berücksichtigt werden, für die es nicht zu unbegrenzten Ausfallzeiten kommen kann, sowie alle Datenkategorien, für die keine unbegrenzten Datenverluste auftreten können. Wenn ein Notfall eintritt, der sich auf mehrere Anwendungskomponenten bezieht, ist es wichtig, dass die Besitzer des Plans diesen für folgende Zwecke verwenden können: Erstellung eines vollständigen Bestands der Punkte, die behandelt werden müssen, und die Priorisierung der einzelnen Elemente.

Einige Apps können unter Umständen nur einen einzelnen Prozess oder eine Klassifizierung von Daten darstellen. Dies sollte trotzdem beachtet werden, da die Anwendung wahrscheinlich eine Komponente eines größeren Plans für die Notfallwiederherstellung ist, der mehrere Anwendungen innerhalb der Organisation umfasst.

### <a name="recovery-objectives"></a>Ziele der Wiederherstellung

Für einen vollständigen Plan müssen für jeden Prozess, der von der Anwendung implementiert wird, zwei wichtige Geschäftsanforderungen angegeben werden:

* **Recovery Point Objective (RPO)**: Die maximale Dauer des akzeptablen Datenverlusts. Der RPO-Wert wird in Zeiteinheiten gemessen, nicht anhand des Umfangs: „30 Minuten an Daten“, „vier Stunden an Daten“ usw. Beim RPO-Wert geht es um das Einschränken und Wiederherstellen des *Verlusts* von Daten, nicht um den *Diebstahl* von Daten.
* **Recovery Time Objective (RTO)**: Die maximale Dauer der akzeptablen Ausfallzeit, wobei „Ausfallzeit“ gemäß Ihrer Spezifikation definiert werden muss.

![RTO und RPO](../media-draft/rto-rpo.png)

Jeder größere Prozess bzw. jede Workload, der bzw. die von einer App implementiert wird, sollte über separate RPO- und RTO-Werte verfügen. Auch wenn Sie für unterschiedliche Prozesse zu den gleichen Werten gelangen, sollten diese jeweils anhand einer separaten Analyse generiert werden, mit der Risiken von Notfallszenarien und potenzielle Wiederherstellungsstrategien für jeden Prozess untersucht werden.

Das Angeben eines RPO- und RTO-Werts entspricht praktisch der Erstellung der Anforderungen an die Notfallwiederherstellung für Ihre Anwendung. Es müssen die Priorität jeder Workload und die Datenkategorie angegeben werden. Darüber hinaus muss eine Kosten-Nutzen-Analyse durchgeführt werden, mit der Bereiche wie Implementierungs- und Wartungskosten, Betriebskosten, Verarbeitungsaufwand, Auswirkungen auf die Leistung und die Auswirkungen von Ausfallzeiten und Datenverlust abgedeckt werden. Sie müssen genau definieren, was „Ausfallzeit“ für Ihre Anwendung bedeutet, und in einigen Fällen müssen Sie unter Umständen separate RPO- und RTO-Werte für unterschiedliche Funktionalitätsebenen angeben. Das Angeben der RPO- und RTO-Werte sollte mehr als das einfache Auswählen von willkürlichen Werten sein. Ein Großteil des Nutzens eines Plans für die Notfallwiederherstellung ergibt sich aus den Recherche- und Analyseschritten, die beim Ermitteln der potenziellen Auswirkungen eines Notfalls und der Kosten für die Risikoeindämmung ausgeführt werden.

Bei RPO und RTO handelt es sich um *Ziele* (Objectives). Notfälle und Katastrophen sind unvorhersehbar, und es kann sein, dass Sie für ein bestimmtes Ereignis Ihre vorgegebenen RPO- und RTO-Werte nicht erreichen können. Wenn sich ein Unternehmen bereiterklärt, die Kosten für die Erreichung der vereinbarten RPO- und RTO-Werte zu übernehmen, sollten als Gegenleistung diese Ziele für ein Notfallwiederherstellungsszenario im Allgemeinen erreicht werden. Alle Notfallereignisse sollten nach der Wiederherstellung eine Prüfung umfassen, bei der die Stärken und Schwächen untersucht werden. Aber Notfälle, die dazu führen, dass der RPO- oder RTO-Wert nicht erreicht wird, bedürfen besonderer Aufmerksamkeit.

### <a name="detailing-recovery-steps"></a>Detailliertes Angeben von Schritten zur Wiederherstellung

Im endgültigen Plan sollte ausführlich angegeben sein, welche Schritte ausgeführt werden sollten, um verloren gegangene Daten und die Anwendungskonnektivität wiederherzustellen. Schritte enthalten häufig Informationen zu folgenden Punkten:

* **Sicherungen**: Häufigkeit der Erstellung, Ort der Sicherungen und Vorgehensweise bei der Wiederherstellung.
* **Datenreplikate**: Anzahl und Ort der Replikate, Art und Konsistenzmerkmale der replizierten Daten und Wechsel zu einem anderen Replikat.
* **Bereitstellungen**: Durchführung von Bereitstellungen und Rollbacks und Fehlerszenarien für Bereitstellungen.
* **Infrastruktur**: Lokale Ressourcen und Cloudressourcen, Netzwerkinfrastruktur und Hardwarebestand.
* **Abhängigkeiten**: Externe Dienste, die von der Anwendung verwendet werden, z.B. SLAs und Kontaktinformationen.
* **Konfiguration und Benachrichtigung**: Flags oder Optionen, die festgelegt werden können, um die Anwendung korrekt herabzustufen, und Dienste, die zum Benachrichtigen von Benutzern über die Auswirkungen der Anwendung verwendet werden.

Da die genauen erforderlichen Schritte stark von den Implementierungsdetails der App abhängen, ist es wichtig, den Plan immer auf dem aktuellen Stand zu halten. Bei routinemäßigen Tests des Plans können Lücken und veraltete Abschnitte identifiziert werden.

## <a name="designing-for-disaster-recovery"></a>Entwerfen für die Notfallwiederherstellung

Die Notfallwiederherstellung ist kein automatisches Feature. Sie muss entworfen, erstellt und getestet werden. Eine App, für die eine robuste Strategie für die Notfallwiederherstellung unterstützt werden soll, muss im Hinblick auf die Notfallwiederherstellung von Grund auf neu erstellt werden. Azure verfügt über Dienste, Features und Anleitungen, damit Sie Apps erstellen können, die die Notfallwiederherstellung unterstützen. Es liegt aber an Ihnen, diese in Ihren Entwurf einzubauen.

Beim Entwerfen für die Notfallwiederherstellung geht es um diese beiden Hauptaspekte:

* **Datenwiederherstellung**: Sicherungen und die Replikation werden verwendet, um verlorene Daten wiederherzustellen.
* **Prozesswiederherstellung**: Die Wiederherstellung von Diensten und Bereitstellung von Code für die Wiederherstellung nach Ausfällen.

### <a name="data-recovery-and-replication"></a>Datenwiederherstellung und -replikation

Bei der Replikation werden gespeicherte Daten in mehreren Datenspeicherreplikaten dupliziert. Im Gegensatz zu *Sicherungen*, bei denen langlebige, schreibgeschützte Momentaufnahmen von Daten zur Verwendung bei der Wiederherstellung erstellt werden, werden bei der Replikation Echtzeitkopien (bzw. nahezu in Echtzeit) von Livedaten erstellt. Das Ziel der Replikation besteht darin, Replikate mit möglichst geringer Latenz synchron zu halten, während gleichzeitig die Reaktionsfähigkeit der Anwendung aufrechterhalten wird. Die Replikation ist eine wichtige Komponente des Entwurfs im Hinblick auf Hochverfügbarkeit und Notfallwiederherstellung und ein häufiges Feature von Anwendungen für die Produktion.

Die Replikation wird genutzt, um eine Lösung für einen ausgefallenen oder nicht erreichbaren Datenspeicher zu erzielen, indem ein *Failover* ausgeführt wird: Die Anwendungskonfiguration wird geändert, um Datenanforderungen an ein funktionierendes Replikat zu leiten. Das Failover ist häufig automatisiert und wird durch eine Fehlererkennung ausgelöst, die in ein Datenspeicherprodukt integriert ist, oder durch eine Erkennung, die Sie über Ihre Überwachungslösung implementieren. Je nach Implementierung und Szenario muss das Failover ggf. von Systembedienern manuell ausgeführt werden.

Die Replikation ist kein Vorgang, den Sie von Grund auf neu implementieren. Die meisten Datenbanksysteme mit vollem Funktionsumfang und andere Datenspeicherprodukte und -dienste enthalten im Rahmen der Funktions- und Leistungsanforderungen eine Art der Replikation als fest integriertes Feature. Es liegt aber an Ihnen, diese Features in Ihren Anwendungsentwurf zu integrieren und entsprechend einzusetzen.

Unterschiedliche Azure-Dienste unterstützen verschiedene Ebenen und Konzepte der Replikation. Beispiel:

* Die **Azure Storage**-Replikation erfolgt praktisch automatisch. Weder Ihre Anwendung noch Ihre Bediener interagieren direkt damit. Failover sind automatisch und transparent, und Sie müssen lediglich eine Replikationsebene auswählen, mit der die gewünschte Balance zwischen Kosten und Risiko erzielt wird.
* Die Replikation per **Azure SQL-Datenbank** erfolgt in geringerem Umfang automatisch, aber für die Wiederherstellung nach einem vollständigen Ausfall eines Azure-Datencenters oder einer Azure-Region ist die Georeplikation erforderlich. Die Einrichtung der Georeplikation erfolgt manuell, aber es handelt sich um ein hervorragendes Feature des Diensts, das über eine gute Unterstützung durch Dokumentation verfügt.
* **Cosmos DB** ist ein global verteiltes Datenbanksystem, und die Replikation ist ein zentraler Punkt der Implementierung. Bei Cosmos DB konfigurieren Sie die Replikation nicht direkt, sondern Sie konfigurieren Optionen in Bezug auf die Partitionierung und Datenkonsistenz.

Es gibt viele verschiedene Replikationsentwürfe, bei denen die Datenkonsistenz, Leistung und Kosten unterschiedliche Prioritäten aufweisen. Für die Replikation vom Typ *Aktiv* müssen Updates gleichzeitig auf mehreren Replikaten durchgeführt werden, um die Konsistenz auf Kosten des Durchsatzes zu gewährleisten. Im Gegensatz hierzu wird die Synchronisierung bei der *passiven* Replikation im Hintergrund durchgeführt, sodass die Replikation als Einschränkung der Anwendungsleistung wegfällt. Es ergibt sich aber ein höherer RPO-Wert. Bei der Replikation vom Typ *Aktiv/Aktiv* oder *Multimaster* können mehrere Replikate gleichzeitig genutzt werden, sodass ein Lastenausgleich auf Kosten einer komplizierteren Datenkonsistenz durchgeführt werden kann. Bei der Replikation vom Typ *Aktiv/Passiv* werden Replikate für die Livenutzung nur während des Failovers reserviert.

![Azure SQL-Datenbank-Georeplikation](../media-draft/geo-replication.png)

> [!IMPORTANT]
> **Weder bei der Replikation noch bei Sicherungen handelt es sich um vollständige eigenständige Lösungen für die Notfallwiederherstellung**. Die Datenwiederherstellung ist nur eine Komponente der Notfallwiederherstellung, und mit der Replikation können nicht für viele Arten von Notfallwiederherstellungsszenarien alle Anforderungen erfüllt werden. Bei einem Szenario mit Datenbeschädigung kann es aufgrund der Art der Beschädigung beispielsweise dazu kommen, dass sich der Fehler vom primären Datenspeicher auf die Replikate verteilt, sodass alle Replikate nutzlos werden und eine Sicherung für die Wiederherstellung verwendet werden muss.

### <a name="process-recovery"></a>Prozesswiederherstellung

Nach einer Notfallsituation müssen nicht nur die Geschäftsdaten wiederhergestellt werden. Häufig führen Notfallszenarien auch zu Ausfallzeiten, z.B. aufgrund von Problemen mit der Netzwerkverbindung, Datencenterausfällen oder beschädigten VM-Instanzen oder Softwarebereitstellungen. Ihre Anwendung muss so entworfen worden sein, dass Sie dafür die Funktionsfähigkeit wiederherstellen können.

In den meisten Fällen umfasst die Prozesswiederherstellung auch ein Failover auf eine separate funktionierende Bereitstellung. Je nach Szenario kann der geografische Standort ein kritischer Aspekt sein: Bei einer größeren Naturkatastrophe, bei der eine gesamte Azure-Region ausfällt und in den Offlinezustand versetzt wird, muss der Dienst beispielsweise in einer anderen Region wiederhergestellt werden. Die Anforderungen an die Notfallwiederherstellung für Ihre Anwendung, vor allem der RTO-Wert, sollten die Grundlage für Ihren Entwurf sein und Ihnen bei den folgenden Entscheidungen behilflich sein: wie viele replizierte Umgebungen vorhanden sein sollten, wo sich diese befinden sollten und ob sie sich in einem ausführungsbereiten Zustand befinden oder bei einem Notfall eine Bereitstellung akzeptieren sollten.

Je nach Entwurf Ihrer Anwendung gibt es einige unterschiedliche Strategien und Azure-Dienste und -Features, die Sie nutzen können, um die Unterstützung der Prozesswiederherstellung nach einem Notfall für Ihre App zu verbessern.

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery ist ein dedizierter Dienst zum Verwalten der Prozesswiederherstellung für Workloads auf in Azure bereitgestellten VMs oder VMs auf physischen Servern und für direkt auf physischen Servern ausgeführte Workloads. Site Recovery repliziert Workloads an anderen Orten und unterstützt Sie bei der Ausführung des Failovers, wenn ein Ausfall eintritt, und beim Testen eines Plans für die Notfallwiederherstellung.

![Azure Site Recovery](../media-draft/asr.png)

Site Recovery unterstützt das Replizieren von gesamten VMs und Images physischer Server sowie einzelner *Workloads*. Hierbei kann eine Workload eine einzelne Anwendung oder ein vollständiger virtueller Computer oder ein Betriebssystem mit den entsprechenden Anwendungen sein. Jede Anwendungsworkload kann repliziert werden, aber Site Recovery verfügt über erstklassige integrierte Unterstützung für viele Microsoft-Serveranwendungen, z.B. SQL Server und SharePoint, sowie für einige Drittanbieteranwendungen, z.B. von SAP.

Für jede App, die auf virtuellen Computern oder physischen Servern ausgeführt wird, sollte zumindest die Nutzung von Azure Site Recovery geprüft werden. Dies ist eine gute Möglichkeit, um Szenarien und Möglichkeiten für die Prozesswiederherstellung zu ermitteln und zu untersuchen.

#### <a name="service-specific-features"></a>Dienstspezifische Features

Für Apps, die auf Azure PaaS-Angeboten wie App Service ausgeführt werden, verfügen die meisten dieser Dienste über Features und eine Anleitung zur Unterstützung der Notfallwiederherstellung. In vielen Fällen erfolgt die Notfallwiederherstellung automatisch und wird von Azure transparent durchgeführt. Für bestimmte Szenarien können Sie dienstspezifische Features nutzen, um eine schnelle Wiederherstellung zu unterstützen. Beispielsweise wird für Azure SQL Server die Georeplikation unterstützt, um einen Dienst schnell in einer anderen Region wiederherstellen zu können. Azure App Service verfügt über ein Feature für die Sicherung und Wiederherstellung, und die Dokumentation enthält eine Anleitung zur Verwendung von Azure Traffic Manager, um das Leiten von Datenverkehr in eine sekundäre Region zu unterstützen.

![Regionspaare](../media-draft/AzRegionPairs.png)

## <a name="testing-a-disaster-recovery-plan"></a>Testen eines Plans für die Notfallwiederherstellung

Die Planung der Notfallwiederherstellung endet nicht damit, dass Sie einen abgeschlossenen Plan in der Hand halten. Das Testen des Plans ist ein entscheidender Aspekt der Notfallwiederherstellung, um sicherzustellen, dass die Anleitungen und Erläuterungen klar verständlich und aktuell sind.

Wählen Sie Intervalle für die Durchführung unterschiedlicher Testtypen und -bereiche, z.B. monatliches Testen von Sicherungen und Failovermechanismen, und einer umfassenden Simulation der Notfallwiederherstellung alle sechs Monate. Halten Sie sich immer genau an die Schritte und Details, die im Plan dokumentiert sind. Sie können auch erwägen, eine Person, die nicht mit dem Plan vertraut ist, Hinweise zu den Punkten geben zu lassen, die verständlicher formuliert werden können.

Stellen Sie sicher, dass Sie auch Ihr Überwachungssystem in die Tests einbeziehen. Wenn Ihre Anwendung beispielsweise automatische Failover unterstützt, können Fehler in eine Abhängigkeit oder eine andere kritische Komponente eingebaut werden. So können Sie sich vergewissern, dass sich die Anwendung während des gesamten Prozesses richtig verhält, z.B. bei der Erkennung des Fehlers und beim Auslösen des automatisierten Failovers.

 Indem Ihre Anforderungen sorgfältig identifiziert werden und ein Plan aufgestellt wird, können Sie ermitteln, welche Arten von Diensten Sie verwenden müssen, um Ihre Wiederherstellungsziele zu erreichen. In Azure werden mehrere Dienste und Features für die Erreichung dieser Ziele bereitgestellt.
