Sie sind ein Lösungsarchitekt. Ihre Organisation, Lamna Healthcare, hat ihre Workloads in die Cloud verschoben. Vor Kurzem sind die Kosten für Ressourcen und Workflows stärker angestiegen als von Lamna erwartet. Sie wurden gebeten zu prüfen, ob es sich um natürliches, effizientes Wachstum handelt oder ob die Kosten reduziert werden können, wenn der Umgang mit den Cloudressourcen der Organisation effizienter gestaltet wird.

## <a name="how-the-cloud-changes-your-expenses"></a>Kostenänderungen durch die Cloud

Ein Unterschied zwischen einer öffentlichen Cloud und der lokalen Infrastruktur besteht darin, wie Sie für die von Ihnen verwendeten Dienste bezahlen. In lokalen Rechenzentren dauert es lange, Hardware zu beschaffen. Außerdem ist die Hardware auf maximale Kapazitäten ausgelegt und ein Teil der Kosten, z.B. für Strom und Lagerfläche, bleibt der Unternehmenseinheit vorenthalten, die die Ressourcen verbraucht. Der Erwerb von physischer Infrastruktur ist mit Investitionen in langfristig verwendbare Objekte verknüpft, wodurch Sie weniger flexibel im Hinblick auf Ressourcen sind.

Wenn Sie zur Cloud wechseln, zahlen Sie nur für das, was Sie tatsächlich verwenden. Sie müssen keine langfristigen Investitionen mehr in Hardware tätigen, und wenn sich Ihre Anforderungen an Ressourcen ändern, können Sie darauf reagieren, indem Sie Ressourcen hinzufügen, verschieben oder entfernen. Workloads in Diensten unterscheiden sich voneinander (nicht nur innerhalb eines Diensts, sondern auch im Bezug auf andere Dienste), der Bedarf ist unter Umständen nicht vorhersehbar und Ihre Wachstumsmuster ändern sich mit der Zeit. Da Sie in der Cloud nur für das zahlen, was Sie verwenden, ändert sich Ihre Kostenstruktur im Einklang mit Ihren Ressourcen.

Die Cloudinfrastruktur ist für Szenarien mit fluktuierender Ressourcennutzung geeignet. Ressourcen, die für längere Zeit nicht verwendet werden, können heruntergefahren werden und verursachen so keine Kosten. Wenn ein erfolgreicher Dienst wächst, können auch die Ressourcen mitwachsen. Es muss nicht auf den nächsten Beschaffungszyklus gewartet werden. Weitere Ressourcen können hinzugefügt und entfernt werden, um auf vorhersagbare und nicht vorhersagbare Bedarfsschwankungen zu reagieren. Die folgende Abbildung zeigt, warum die lokale Infrastruktur nicht für all diese Schwankungen geeignet ist.

![Abbildung, die die Nachteile der Verwendung einer lokalen Infrastruktur zeigt.](../media/cloudcomputingpatterns.png)

In einer effizienten Architektur sind die bereitgestellten Ressourcen auf den jeweiligen Bedarf abgestimmt. Wenn ein virtueller Computer weniger als 10 % ausgelastet ist, verschwenden Sie Ressourcen – sowohl im Hinblick auf Computeressourcen als auch auf Kosten. Wenn im Gegensatz dazu ein virtueller Computer 90 % ausgelastet ist und die meisten der verfügbaren Ressourcen verwendet, ist er effizient. Wenn ein System zu 100 % ausgelastet ist, kann dies die Leistung beeinträchtigen. Es ist wichtig, dass Sie sicherstellen, dass die Leistung des Systems nicht beeinflusst wird, wenn Sie die Effizienz steigern. Sie können nur selten von konstantem Bedarf ausgehen. Daher ist es wichtig, dass Sie Ihre Ressourcen so konstruieren, dass sie stets an den tatsächlichen Bedarf angepasst werden können, um Effizienz zu gewährleisten.

## <a name="track-your-cloud-spend"></a>Nachverfolgen von Cloudausgaben

Sie benötigen Daten, um intelligente Entscheidungen treffen zu können. Wenn Sie Ihre Ausgaben prüfen, können Sie diese mit der jeweiligen Auslastung vergleichen und so ermitteln, wo in Ihrer Umgebung Einsparungen möglich sind.

Sie können Ihre Abrechnungsdaten jederzeit exportieren. Wenn Sie Ihre Abrechnungsdaten verwenden, können Sie Ihre Ausgaben nachverfolgen und feststellen, wie diese auf Ihre Ressourcen verteilt sind. Das Problem dabei ist, dass in den Abrechnungsdaten nur die Kosten und nicht die Auslastung aufgeführt sind. Sie können also sehen, dass Sie für eine große VM bezahlen, aber nicht, inwieweit diese auch verwendet wird.

Mithilfe von Azure Cost Management können Sie nicht nur Ihre Ausgaben nachverfolgen, sondern Sie erfahren auch, welche Ressourcen nicht effizient genutzt werden. Azure Cost Management erfasst Ihre Gesamtausgaben, die Kosten pro Dienst sowie langfristige Kosten. Sie können Detailinformationen zu Ressourcentypen und Instanzen anzeigen. Außerdem können Sie Ihre Kosten nach Organisation oder Kostenstelle aufteilen, indem Sie Ressourcen entsprechende Kategorien zuordnen.

Auch der Azure Advisor verfügt über eine Kostenkomponente. Er empfiehlt bei Bedarf die Größenanpassung von VMs und den Kauf von reservierten Instanzen, wenn diese weniger Kosten verursachen als Instanzen mit nutzungsbasierter Bezahlung. Er erkennt nicht verwendete ExpressRoute-Verbindungen und virtuelle Netzwerkgateways, die sich im Leerlauf befinden. Zudem stellt der Advisor Empfehlungen im Hinblick auf Leistung, Hochverfügbarkeit und Sicherheit zur Verfügung.

Dabei ist es wichtig, dass Sie sich die Zeit nehmen, Ihre Ausgaben zu prüfen. Finden Sie heraus, welche Bereiche ineffizient sind, damit Sie so effizient wie möglich arbeiten können.

## <a name="organize-to-optimize"></a>Optimierung durch Organisation

Wenn Sie Ihre Ressourcen besser organisieren, hilft Ihnen das dabei, Ihre Ausgaben einfacher nachzuverfolgen. Sie können Ihre Ressourcen dafür in Gruppen zusammenfassen und in Beziehung zueinander stellen, um zu prüfen, inwieweit die jeweiligen Kosten miteinander verknüpft sind. Sie können Ressourcen im Hinblick auf die jeweiligen Ausgaben wie folgt gruppieren:

- Sie können Ressourcen verschiedenen Abonnements zuweisen.
- Sie können Ressourcen verschiedenen Ressourcengruppen zuweisen.
- Sie können Ressourcen Tags zuordnen.

Wenn Sie Abonnements und Ressourcengruppen verwenden, um Ressourcen zu organisieren, stellt dies eine einfache Möglichkeit dar, Ressourcen auf logische Weise zu gruppieren. Sie müssen dafür nur Ihre Abrechnungsdaten prüfen. Tags eignen sich, wenn Ressourcenbeziehungen die Grenzen zwischen Abonnements und Ressourcengruppen umfassen. Tags sind Schlüssel-Wert-Paare, die zu jeder beliebigen Ressource hinzugefügt werden können. Sie sind in dem Abrechnungsdaten enthalten. So können Sie jede Ressource einer Abteilung oder Kostenstelle zuordnen. Mithilfe von Tags können Sie Berichte zu Kosten verbessern und jeder Abteilung innerhalb Ihrer Organisation die Kosten zuordnen, die diese verursacht. Die folgende Abbildung zeigt, wie Sie das gleiche Tag auf Ressourcen in verschiedenen Ressourcengruppen und sogar in verschiedenen Abonnements anwenden können.

![Abbildung mit Ressourcen, die mithilfe von Tags, Ressourcengruppen und Abonnements organisiert wurden.](../media/tagging.png)

Wenn Sie Ihre Ressourcen organisieren, hilft Ihnen das in vielerlei Hinsicht, und Sie können Ihre Ausgaben besser nachverfolgen. Nachfolgend wird erläutert, wie Sie Ihre Kosten optimieren können.

## <a name="optimizing-iaas-costs"></a>Optimieren von IaaS-Kosten

In Organisationen, die virtuelle Computer verwenden, stellen die Kosten für diese Computer einen Großteil der Gesamtausgaben dar. Die Computekosten verursachen dabei in der Regel einen Großteil der Gesamtkosten, gefolgt vom Speicher. Wenn Sie sich die Zeit nehmen, um die Ressourcen so zu optimieren, dass Sie nur für das bezahlen, was Sie auch verwenden, kann Ihre monatliche Rechnung bedeutend geringer ausfallen.

Im Folgenden werden einige Best Practices zum Senken der Compute- und Speicherkosten erläutert.

### <a name="compute"></a>Compute

Es gibt verschiedene Möglichkeiten, Kosten für virtuelle Computer zu sparen.

- Sie können die Größe der VM-Instanz reduzieren.
- Sie können die Anzahl der Stunden reduzieren, in denen ein virtueller Computer ausgeführt wird.
- Sie können Rabatte für die Computekosten nutzen.

#### <a name="right-size-virtual-machines"></a>Bestimmen der richtigen Größe von virtuellen Computern

Eine VM hat die richtige Größe, wenn diese an den jeweiligen Ressourcenbedarf angepasst ist. Wenn sich eine VM 25 % der Zeit im Leerlauf befindet, werden Ihre Kosten automatisch verringert, sobald Sie deren Größe verringern. Innerhalb einer Instanzenfamilie sind die Kosten eines virtuellen Computers linear. Durch die Verwendung einer höheren Instanz werden die Kosten jeweils verdoppelt. Wenn Sie im Gegensatz dazu einen virtuellen Computer um eine einzelne Instanz verringern, halbieren sich Ihre Kosten. Die folgende Abbildung zeigt Einsparungen in Höhe von 50 Prozent, die durch die Umstellung auf die nächstniedrigere Größe innerhalb der Serie erzielt wurden.

![Abbildung zur Veranschaulichung der Einsparungen, die für einen nicht ausgelasteten virtuellen Computer durch die Umstellung auf die nächstniedrigere Größe erzielt wurden.](../media/vm-resize.png)

Der Azure Advisor ermittelt, welche virtuellen Computer zu wenig ausgelastet sind. Advisor überwacht die Verwendung Ihrer virtuellen Computer 14 Tage lang und ermittelt virtuelle Computer mit geringer Auslastung. Virtuelle Computer, deren CPU-Auslastung über einen Zeitraum von mindestens vier Tagen höchstens 5 % und deren Netzwerkauslastung höchstens 7 MB beträgt, gelten als nicht ausgelastete virtuelle Computer.

#### <a name="implement-shutdown-schedules-for-virtual-machines"></a>Implementieren von Zeitplänen zum Abschalten virtueller Computer

Wenn Sie über VM-Workloads verfügen, die nur gelegentlich verwendet, aber dauerhaft ausgeführt werden, verschwenden Sie Geld. Diese VMs können bei Nichtbenutzung abgeschaltet und gemäß einem Zeitplan wiedereingeschaltet werden. So sparen Sie Computekosten, wenn die Zuordnung der VMs aufgehoben wird. Dies gilt insbesondere für Entwicklungsumgebungen, da häufig nur während der offiziellen Geschäftszeiten entwickelt wird. Sie können die Zuordnung für diese Systeme außerhalb der Geschäftszeiten aufheben und so Computekosten vermeiden.

Verwenden Sie Azure Automation, um festzulegen, dass Ihre VMs nur dann ausgeführt werden, wenn dies für Ihre Workloads erforderlich ist.

Sie können auch das Feature zum automatischen Herunterfahren einer VM verwenden, um eine einmalige automatisierte Abschaltung zu planen.

#### <a name="apply-compute-cost-discounts"></a>Inanspruchnehmen von Rabatten für Computekosten

Mithilfe des Azure-Hybridvorteils können Sie Ihre Kosten für Windows Server und SQL Server optimieren, da Sie Ihre lokalen Lizenzen für Windows Server oder SQL Server zusammen mit Software Assurance verwenden können. Dadurch erhalten Sie einen Rabatt auf die Computekosten für diese VMs, da so keine Kosten für Windows Server und SQL Server auf aktivierten Instanzen entstehen.

Einige virtuelle Computer müssen permanent ausgeführt werden. Dies ist z.B. bei einer Serverfarm für eine Webanwendung, die von einer Produktionsworkload benötigt wird, oder einen Domänencontroller der Fall, der verschiedene Server auf einem virtuellen Netzwerk unterstützt. Wenn Sie sicher sind, dass diese virtuellen Computer mindestens ein Jahr lang ausgeführt werden, können Sie die Kosten weiter reduzieren, indem Sie auf reservierte Instanzen zurückgreifen. Azure Reserved Virtual Machine Instances können entweder für ein Jahr oder für drei Jahre an Computekapazität verwendet werden. Dabei reduzieren sich die Kosten im Vergleich zu Computeressourcen mit nutzungsbasierter Bezahlung Azure Reserved Virtual Machine Instances können die Kosten für virtuelle Computer mit einer Vorauszahlung für ein Jahr oder für drei Jahre erheblich reduzieren – im Vergleich zu den Preisen bei nutzungsbasierter Bezahlung um bis zu 72 Prozent. Die folgende Abbildung zeigt die Einsparungen, die erzielt werden, wenn Sie Ihre lokale Lizenz mit dem Azure-Hybridvorteil kombinieren und wenn Sie Ihre lokale Lizenz sowohl mit Azure-RI als auch mit dem Azure-Hybridvorteil kombinieren.

![Abbildung mit den Einsparungen für Azure-Produkte, wenn Sie über lokale Lizenzen mit Software Assurance verfügen.](../media/ahub-save.png)

### <a name="virtual-machine-disk-storage-cost-optimization"></a>Optimieren der Kosten für VM-Datenträgerspeicher

Sie können bei Workloads, für die keine hohe Zuverlässigkeit und Leistung von Datenträgern benötigt wird, den kostengünstigen Standardspeicher verwenden. Möglicherweise entscheiden Sie sich dafür, den Standardspeicher für Dev-/Testumgebungen zu verwenden, die nicht eindeutig der Produktionsworkload entsprechen.

Vergewissern Sie sich, dass in Ihrer Umgebung keine Datenträger vorhanden sind, die nicht mehr verwendet werden. Auch Datenträger, die keiner VM zugewiesen sind, verursachen Speicherkosten. Wenn Sie zwar eine VM, aber nicht die Datenträger entfernt haben, können Sie die nicht verwendeten Datenträger entfernen, um Ihre Speicherkosten zu reduzieren.

Wenn Sie neben nicht verwendeten Datenträgern auch über Momentaufnahmen verfügen, die niemand mehr verwendet, nehmen Sie sich die Zeit, diese auszusortieren. Zwar sind die Kosten für diese Momentaufnahmen geringer als für die Datenträger, aber es empfiehlt sich immer, Kosten für nicht benötigte Ressourcen zu reduzieren.

## <a name="optimizing-paas-costs"></a>Optimieren der PaaS-Kosten

PaaS-Dienste werden in der Regel anhand der Kosten für IaaS-Dienste optimiert. Allerdings gibt es Möglichkeiten, unnötige Kosten zu ermitteln und diese auf ein Minimum zu reduzieren. Nachfolgend werden Möglichkeiten zum Reduzieren von Speicherkosten für Azure SQL-Datenbank und Azure Blob aufgeführt.

### <a name="optimizing-azure-sql-database-costs"></a>Optimieren der Kosten für Azure SQL-Datenbank

Wenn Sie eine Datenbank mit Azure SQL-Datenbank erstellen, müssen Sie einen Server mit Azure SQL Server und eine Leistungsstufe auswählen. Jede Stufe steht für eine Leistungsebene in Datenbanktransaktionseinheiten oder virtuellen Kernen. Bei stabiler Datenbankauslastung können Sie die Kosten ganz einfach optimieren, indem Sie eine Stufe auswählen, die der benötigten Leistung entspricht. Sie fragen sich sicher, was geschieht, wenn die Aktivität für Ihre Datenbank unerwartete Schwankungen verzeichnet. Sie können mithilfe von Pools für elastische Datenbanken Kosten für unvorhersehbare Workloads reduzieren.

Pools für elastische Datenbanken mit SQL-Datenbank stellen eine einfache, kostengünstige Lösung zum Verwalten und Skalieren mehrerer Datenbanken mit variierenden und unvorhersehbaren Anforderungen dar. Die Datenbanken in einem Pool für elastische Datenbanken befinden sich auf einem einzelnen Server in Azure SQL-Datenbank und nutzen gemeinsam mehrere Ressourcen zu einem festen Preis. Pools eignen sich hervorragend für eine große Anzahl an Datenbanken mit spezifischen Nutzungsmustern. Im Hinblick auf eine einzelne Datenbank wird dieses Muster durch eine geringe durchschnittliche Auslastung mit relativ wenigen Nutzungslastspitzen gekennzeichnet.
Je mehr Datenbanken Sie einem Pool hinzufügen können, desto mehr sparen Sie. Die folgende Abbildung zeigt die Funktionen von drei Arten von Pools für elastische Datenbanken: Basic, Standard und Premium.  Basic bietet eine automatische Hochskalierung auf bis zu 5 eDTUs pro Datenbank, Standard bietet eine automatische Hochskalierung auf bis zu 100 eDTUs pro Datenbank, und Premium bietet eine automatische Hochskalierung auf bis zu 1.000 eDTUs pro Datenbank.

![Abbildung der Kapazität der automatischen Skalierung für verschiedene Arten von Pools für elastische Datenbanken.](../media/sqldb-elastic-pools.png)

Pools für elastische Datenbanken sind eine gute Möglichkeit, um Kosten auf mehrere Datenbanken aufzuteilen. Sie können dazu beitragen, Ihre Kosten für Azure SQL-Datenbank zu reduzieren.

### <a name="optimizing-blob-storage-costs"></a>Optimieren der Kosten für Blob Storage

Blob Storage ist zwar eine kostensparende Möglichkeit, um Daten zu speichern, aber je mehr Daten gespeichert werden, desto größer ist der Kostenvorteil, wenn Sie den Datenspeicher optimieren.

Im Folgenden wird nochmal auf Lamna Healthcare eingegangen. Es geht um eine Anwendung für medizinische Bildgebung, die Bilder in Blob Storage speichert. Da aber eine große Menge an Bildern gespeichert werden muss, die viel Speicherplatz in Anspruch nehmen, hat die Verwendung dieses Speicherdiensts zur Folge, dass die Anwendung sehr teuer wird. Wenn für einen Patienten ein Bild aufgenommen wird, ist es wahrscheinlich, dass dieses in der ersten Woche nach der Aufnahme mehrmals angesehen wird. Daher wird erwartet, dass die Leistung für Bildabrufe hoch ist. Im Gegensatz dazu wird ein Bild, das vor zwei Jahren aufgenommen wurde, möglicherweise nur selten aufgerufen, und es wird eine geringere Abrufleistung erwartet. Sie können in diesem Zusammenhang mit Speicherebenen arbeiten, um die Kosten für Bildabrufe zu optimieren, da immer weniger Leistung erforderlich ist, je älter die Bilder sind.

Azure Storage bietet drei Speicherebenen für Blob-Objektspeicher. Die heiße Speicherebene von Azure ist für das Speichern von Daten optimiert, auf die häufig zugegriffen wird. Die kalte Speicherebene von Azure ist für das Speichern von Daten optimiert, auf die selten zugegriffen wird, und die mindestens 30 Tage lang gespeichert werden. Die Archivzugriffsebene von Azure ist für das Speichern von Daten optimiert, auf die selten zugegriffen wird und die bei flexiblen Latenzanforderungen mindestens 180 Tage lang gespeichert werden.

- **Heiße Speicherebene:** die höchsten Speicherkosten, aber die geringsten Zugriffskosten.
- **Kalte Speicherebene:** niedrigere Speicherkosten, aber höhere Zugriffskosten im Vergleich zur heißen Speicherebene. Diese Ebene ist für Daten bestimmt, die mindestens 30 Tage lang auf der kalten Ebene verbleiben.
- **Archivspeicherebene:** die niedrigsten Speicherkosten, aber die höchsten Datenabrufkosten im Vergleich zur kalten und heißen Speicherebene. Diese Ebene ist für Daten bestimmt, die mehrere Stunden Abrufwartezeit tolerieren und mindestens 180 Tage lang auf der Archivebene verbleiben.

Für Lamna Healthcare bietet es sich also an, neue Bilder einen Monat lang der heißen Speicherebene zuzuordnen, damit die neusten Bilder schnellstmöglich abgerufen werden können. Bilder, die älter als ein Jahr sind, könnten auf die Archivspeicherebene verschoben werden, da es wahrscheinlich ist, dass diese Bilder nicht abgerufen werden. Dadurch fallen weniger Kosten für das Speichern dieser Bilder an.

## <a name="cost-optimization-at-lamna-healthcare"></a>Kostenoptimierung bei Lamna Healthcare

Lamna Healthcare macht Fortschritte beim Reduzieren der Unternehmenskosten. Das Unternehmen prüft seine Ausgaben monatlich und jede Abteilung hat Zugriff auf Azure Cost Management und kann im Laufe des Monats prüfen, welche Kosten durch sie angefallen sind. Es wurden einige Möglichkeiten gefunden, reservierte Instanzen einzusetzen. Mehrere dieser Instanzen wurden erworben, um diesen Rabatt nutzen zu können. Automatisierte Prozesse wurden implementiert, um Entwicklungsumgebungen außerhalb der offiziellen Geschäftszeiten auszuschalten. Dadurch werden zu Zeiten, zu denen diese Ressourcen nicht verwendet werden, Kosten gespart. 

Außerdem hat das Optimieren von Blob Storage für das Speichern von Bildern dazu beigetragen, dass die Kosten im Laufe der letzten Monate gesenkt werden konnten.

## <a name="summary"></a>Zusammenfassung

Wenn Sie die Kosten für Ihre Cloudinfrastruktur optimieren, müssen Sie Ihre Ausgaben nachverfolgen und sicherstellen, dass die Auslastung Ihrer Ressourcen dem Bedarf Ihrer Workloads entspricht. Wenn Sie die richtige Qualität und Leistungsstufe für Ihre Ressourcen verwenden, können Ihre Cloudkosten weiter optimiert werden.