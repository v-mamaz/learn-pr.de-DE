Es ist wichtig, dass Sie in Ihrer Architektur Überlegungen zur Speicherleistung berücksichtigen. Genau wie die Netzwerklatenz kann eine schlechte Leistung auf Speicherebene die Endbenutzererfahrung beeinträchtigen. Wie würden Sie Ihren Datenspeicher optimieren? Welche Aspekte müssen Sie berücksichtigen, um sicherzustellen, dass Sie in der Architektur keine Speicherengpässe verursachen? Hier sehen wir uns an, wie Sie die Speicherleistung in Ihrer Architektur optimieren können.

## <a name="optimize-virtual-machine-storage-performance"></a>Optimieren der Speicherleistung für virtuelle Computer

Zuerst untersuchen wir das Optimieren von Speicher für virtuelle Computer. Datenträgerspeicher spielt eine wichtige Rolle in Bezug auf die Leistung Ihrer virtuellen Computer, und die Auswahl des richtigen Datenträgertyps für Ihre Anwendung ist eine wichtige Entscheidung.

Unterschiedliche Anwendungen haben unterschiedliche Speicheranforderungen. Ihre Anwendung reagiert möglicherweise empfindlich auf die Latenz von Lese- und Schreibvorgängen auf dem Datenträger, oder sie erfordert die Fähigkeit, eine große Anzahl von Eingabe-/Ausgabevorgänge pro Sekunde (IOPS) oder einen größeren Datenträger-Gesamtdurchsatz verarbeiten zu können.

Welchen Typ von Datenträger sollten Sie beim Erstellen einer IaaS-Workload verwenden? Es gibt vier Optionen:

- **Lokaler SSD-Speicher**: Jede VM verfügt über einen temporären Datenträger, der vom lokalen SSD-Speicher gestützt wird. Die Größe dieses Datenträgers hängt von der Größe des virtuellen Computers ab. Da dies ein lokaler SSD-Datenträger ist, ist die Leistung hoch, steht aber möglicherweise während einer Wartung oder einer erneuten Bereitstellung der VM nicht zur Verfügung. Dieser Datenträger ist nur für die temporäre Speicherung von Daten geeignet, die Sie nicht dauerhaft benötigen. Dieser Datenträger eignet sich hervorragend für Auslagerungsdateien und z.B. für „tempdb“ in SQL Server. Für diesen Speicher fallen keine Gebühren an. Er ist in den Kosten für den virtuellen Computer enthalten.

- **HDD-Standardspeicher**: Dies ist ein Spindel-Datenträgerspeicher, und er ist möglicherweise gut geeignet, wenn inkonsistente Latenz oder ein geringerer Durchsatz keinen Einfluss auf Ihre Anwendung haben. Eine Dev/Test-Workload, für die keine garantierte Leistung benötigt wird, ist ein hervorragender Anwendungsfall für diesen Datenträgertyp.

- **SSD-Standardspeicher**: Dies ist ein SSD-gestützter Speicher mit der niedrigen Latenz von SSD, aber geringerem Durchsatz. Ein nicht für die Produktion verwendeter Webserver wäre ein guter Anwendungsfall für diesen Datenträgertyp.

- **Storage Premium-SSD**: Dieser SSD-gestützte Speicher eignet sich gut für Workloads, die in die Produktion übergehen, die höchste Zuverlässigkeit, konsistent niedrige Latenz oder hohen Durchsatz und hohe IOPS-Werte erfordern. Da diese Datenträger höhere Leistung und Zuverlässigkeit bieten, werden sie für alle Produktionsworkloads empfohlen.

Storage Premium kann nur virtuellen Computern (VM) bestimmter Größe angefügt werden. Premium-Speicher-fähige Größen festgelegt sind, mit "s" im Namen, z. B. D2**s**_v3 oder VM Standard_F2**s**_v2. Jedem Typ von virtuellem Computer (mit oder ohne „s“ im Namen) können HDD- oder SSD-Laufwerke als Standardspeicher angefügt werden.

Auf alle Datenträger können Stripingtechnologien (wie „Direkte Speicherplätze“ unter Windows oder „mdadm“ unter Linux) angewendet werden, um den Durchsatz und die IOPS-Werte zu erhöhen, indem die Datenträgeraktivität auf mehrere Datenträger verteilt wird. Über Datenträgerstriping können Sie die Leistung für Datenträger enorm steigern. Es wird häufig in Hochleistungs-Datenbanksystemen und anderen Systemen mit hohen Speicheranforderungen verwendet.

Wenn Sie auf die Workloads virtueller Computer angewiesen sind, müssen Sie die Leistungsanforderungen Ihrer Anwendung bewerten, um den zugrunde liegenden Speicher zu bestimmen, den Sie für Ihre virtuellen Computer bereitstellen müssen.

## <a name="optimize-storage-performance-for-your-application"></a>Optimieren der Speicherleistung für Ihre Anwendung

Sie können unterschiedliche Speichertechnologien zum Verbessern der Leistung der RAW-Datenträger verwenden, Sie können aber auch die Leistung beim Zugriff auf Daten auf Anwendungsebene beeinflussen. Sehen wir uns einige dafür geeignete Möglichkeiten an.

### <a name="caching"></a>Caching

Eine gängige Methode zum Verbessern der Anwendungsleistung ist, eine Cachingebene zwischen Ihrer Anwendung und Ihrem Datenspeicher zu integrieren. Ein Cache speichert Daten in der Regel im Arbeitsspeicher und ermöglicht schnelles Abrufen. Bei diesen Daten kann es sich um häufig verwendete Daten, Daten, die Sie aus einer Datenbank angeben, oder temporäre Daten wie z.B. den Benutzerstatus handeln. Sie steuern, welcher Typ von Daten gespeichert wird, wie oft die Daten aktualisiert werden und wann sie ablaufen. Wenn Sie diesen Cache in derselben Region wie die Anwendung und die Datenbank implementieren, verringern Sie die Gesamtlatenz zwischen den beiden. Das Abrufen von Daten aus dem Cache ist fast immer schneller als das Abrufen der gleichen Daten aus einer Datenbank. Mit einer Cachingebene können Sie also die Gesamtleistung der Anwendung erheblich verbessern. Die folgende Abbildung zeigt, wie eine Anwendung ruft Daten aus einer Datenbank ab, speichert es in einem Cache, und verwendet den zwischengespeicherten Wert nach Bedarf.

![Eine Abbildung zeigt, dass das Abrufen von Daten aus dem Cache schneller als das Abrufen aus einer Datenbank ist.](../media/4-cache.png)

Azure Redis Cache ist ein Cachedienst in Azure. Er basiert auf dem Open-Source-Redis-Cache. Azure Redis Cache ist ein vollständig verwaltetes Dienstangebot von Microsoft. Sie wählen die Leistungsstufe aus, die Sie benötigen, und konfigurieren Ihre Anwendung zur Verwendung des Diensts.

### <a name="polyglot-persistence"></a>Mehrsprachige Persistenz

Mehrsprachige Persistenz ist die Verwendung unterschiedlicher Technologien für die Datenspeicherung zur Verarbeitung Ihrer Speicheranforderungen.

Betrachten Sie ein E-Commerce-Beispiel. Sie können die Anwendungsressourcen in einem Blobspeicher, Produktbewertungen und Empfehlungen in einem NoSQL-Speicher und Benutzerprofil- bzw. Kontodaten in einer SQL-­Datenbank speichern. Die folgende Abbildung zeigt, wie eine Anwendung mehrere Data-Speicher-Techniken zum Speichern unterschiedlicher Datentypen der Daten.

![Eine Abbildung, zeigt die Verwendung von anderen datenspeichermethoden innerhalb derselben Anwendung auf die Leistung verbessern und Kosten reduzieren.](../media/4-polyglotpersistence.png)

Dies ist wichtig, da verschiedene Datenspeicher für bestimmte Anwendungsfälle vorgesehen sind oder aufgrund der Kosten besser zugänglich sein können. Der Zugriff auf in einer SQL-Datenbank gespeicherte Blobs kann beispielsweise teurer und langsamer sein als der Zugriff direkt über einen Blobspeicher.

Durch die Verwendung vieler unterstützender Speicher wird die Komplexität der Lösung vergrößert. Bedenken Sie, wie Sie die nicht funktionsbezogenen Anforderungen für solche Datenspeicher erfüllen können und welche Auswirkungen eine Dienstbeeinträchtigung auf die Anwendung insgesamt hat. Berücksichtigen Sie auch, wie Daten zwischen diesen Datenspeichern konsistent bleiben. 

**Letztliche Konsistenz** bietet häufig einen guten Ausgleich, allerdings sind abhängig vom Dienst mehrere verschiedene Modelle verfügbar.

Letztliche Konsistenz bedeutet, dass Replikatdatenspeicher letztendlich konvergieren, wenn keine weiteren Schreibvorgänge auftreten. Wenn ein Schreibvorgang an einem der Datenspeicher vorgenommen wird, können Lesevorgänge aus einem anderen zu leicht veralteten Daten führen. Letztliche Konsistenz ermöglicht eine höhere Skalierung, da die Latenz für Lese- und Schreibvorgänge gering ist. Es muss nicht überprüft werden, ob Informationen in allen Speichern konsistent sind.

## <a name="lamna-healthcare-example"></a>Lamna Healthcare-Beispiel

Das Patientenbuchungssystem von Lamna Healthcare wird in zwei Azure-Regionen gehostet: „Europa, Westen“ und „Australien, Osten“. Sie verwenden virtuelle Computer als Front-End-Knoten, um ihre Website bereitzustellen, und haben Azure SQL-Datenbank in „Europa, Westen“ als primäres und in „Australien, Osten“ als lesbares sekundäres Replikat bereitgestellt. Für ihre Front-End-Knoten ist kein großer Datenträgerdurchsatz erforderlich, jedoch eine konsistente Latenz und Zuverlässigkeit für die Produktion. Dafür wird SSD Premium-gestützter Speicher verwendet.

Sie hosten einen lokalen Azure Redis Cache in jeder Azure-Region, um die allgemeinen Benutzeranforderungen und die Verfügbarkeit der Ärzte zu speichern. Caching wurde implementiert, um die Leistung der am häufigsten auftretenden Datenleseaktivitäten, die in der Anwendung ermittelt wurden, zu optimieren.

## <a name="summary"></a>Zusammenfassung

In diesem Artikel wurden einige Beispiele dazu behandelt, wie Sie die Speicherleistung in Ihrer Infrastrukturebene durch die Auswahl der richtigen Datenträgerarchitektur und auf Anwendungsebene durch die Verwendung von Caching und die Auswahl der richtigen Datenplattform für Ihre Daten verbessern können. Durch eine Lösung mit geeigneter Architektur wird sichergestellt, dass die Leistung beim Zugriff auf Daten möglichst hoch ist. Nun betrachten wir, wie Leistungsprobleme in einer Architektur identifiziert werden können.
