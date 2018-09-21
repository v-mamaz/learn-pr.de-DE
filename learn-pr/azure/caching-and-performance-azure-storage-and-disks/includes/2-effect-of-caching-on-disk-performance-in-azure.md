Ähnlich wie bei Ihren lokalen Computern ist die Leistung von virtuellen Computern häufig direkt davon abhängig, wie schnell Daten gelesen und geschrieben werden können. Damit Sie verstehen, wie wir diese Leistung verbessern, müssen wir zuerst beschreiben, wie die Leistung gemessen wird und welche Einstellungen und Auswahloptionen sich darauf auswirken.

Wir sehen uns vor allem die zugrunde liegenden Datenträger und den Speicher für VMs an. Beachten Sie in Bezug auf die Leistung, dass Sie auch die Anwendungsschicht berücksichtigen sollten. Wenn Sie beispielsweise eine Datenbank auf einer VM ausführen, sollten Sie sich die spezifischen Leistungseinstellungen der Datenbank ansehen. So können Sie sicherstellen, dass diese für die VM und den zugehörigen Speicher für die Ausführung optimiert sind.

Zunächst definieren wir einige Bedingungen und die Garantien, die in Azure dafür gelten.

## <a name="io-operations-per-second"></a>E/A-Vorgänge pro Sekunde

Der von Ihnen gewählte Speichertyp (Standard oder Premium) bestimmt, wie schnell Ihre Datenträger sind. Wir messen diese Leistung in E/A-Vorgängen pro Sekunde (IOPS; englische Aussprache „eye-ops“).

IOPS steht für die Anzahl von Anforderungen, die vom Datenträger innerhalb einer Sekunde verarbeitet werden können. Eine einzelne Anforderung umfasst einen Lese- oder Schreibvorgang. Diese Messung wird direkt auf den Speicher angewendet. Wenn Sie beispielsweise über einen Datenträger verfügen, für den **5.000 IOPS** möglich sind, bedeutet dies, dass theoretisch 5.000 Lese- und Schreibvorgänge pro Sekunde verarbeitet werden können.

IOPS wirkt sich direkt auf Ihre Anwendungsleistung aus. Für einige Anwendungen, z.B. Einzelhandelswebsites, ist ein hoher IOPS-Wert für alle kleineren und zufälligen E/A-Anforderungen erforderlich, die schnell verarbeitet werden müssen, damit die Website reaktionsfähig bleibt.

### <a name="iops-in-azure"></a>IOPS in Azure

Wenn Sie einen Storage Premium-Datenträger an Ihre Hochleistungs-VM anfügen, stellt Azure für Sie gemäß der Datenträgerspezifikation eine garantierte IOPS-Anzahl bereit. Beispielsweise stellt ein Datenträger vom Typ **P50** **7.500 IOPS** bereit. Jeder Typ von Hochleistungs-VM weist außerdem ein bestimmtes IOPS-Limit auf. Für eine VM vom Typ **Standard GS5** gilt beispielsweise ein Limit von **80.000 IOPS**.

IOPS ist ein Messwert für Speicherdatenträger, aber es handelt sich hierbei um einen _theoretischen_ Grenzwert. Zwei weitere Faktoren können sich ebenfalls auf die Anwendungsleistung auswirken: **Durchsatz** und **Latenz**.

### <a name="what-is-throughput"></a>Was ist der Durchsatz?
Durchsatz (auch als „Bandbreite“ bezeichnet) ist die Menge der Daten, die Ihre Anwendung in einem angegebenen Intervall an die Speicherdatenträger überträgt (normalerweise pro Sekunde). Wenn Ihre Anwendung einen E/A-Vorgang mit großen Datenblöcken durchführt, wird ein hoher Durchsatz benötigt.

Azure stellt Durchsatz für Storage Premium-Datenträger basierend auf der Spezifikation des Datenträgers bereit. Für einen **P50**-Datenträger wird beispielsweise ein Datenträgerdurchsatz von **250 MB pro Sekunde** bereitgestellt. Jeder Typ von Hochleistungs-VM weist außerdem ein bestimmtes _Durchsatzlimit_ auf. Für eine VM vom Typ **Standard GS5** gilt beispielsweise ein maximaler Durchsatz von **2.000 MB pro Sekunde**.

#### <a name="iops-vs-throughput"></a>Vergleich von IOPS und Durchsatz

Durchsatz und IOPS stehen in direkter Beziehung zueinander. Wenn Sie einen Wert ändern, wirkt sich dies direkt auf den anderen aus. Sie können die folgende Formel verwenden, um einen theoretischen Grenzwert für den Durchsatz zu erhalten: `IOPS x I/O size = throughput`. Es ist wichtig, diese beiden Werte zu berücksichtigen, wenn Sie Ihre Anwendung planen.

### <a name="what-is-latency"></a>Was ist die Latenz?

Das Lesen und Schreiben von Daten benötigt Zeit. Hier kommt die _Latenz_ ins Spiel. Die Latenz ist die Zeit, die Ihre App zum Senden einer Anforderung an den Datenträger und zum Erhalten einer Antwort benötigt. Im Wesentlichen können wir anhand der Latenz ablesen, wie lange es dauert, eine einzelne E/A-Anforderung für einen Lese- oder Schreibvorgang zu _verarbeiten_.

Mit der Latenz wird der IOPS-Wert beschränkt. Wenn der Datenträger beispielsweise 5.000 IOPS verarbeiten kann, aber die Verarbeitung jedes Vorgangs 10 ms dauert, ergibt für die App aufgrund der Verarbeitungsdauer ein Limit von 100 Vorgängen pro Sekunde. Dies ist nur ein einfaches Beispiel. Die meiste Zeit ist die Latenz deutlich geringer. Letztendlich wird anhand der Latenz und des Durchsatzes bestimmt, wie schnell Ihre App Daten aus dem Speicher verarbeiten kann. 

Storage Premium ermöglicht einheitlich niedrige Latenzen, und per _Zwischenspeicherung_ können Sie eine noch bessere Latenz erzielen. 

## <a name="testing-your-disk-performance"></a>Testen der Datenträgerleistung

Sie können IOPS, Durchsatz und Latenz Ihrer VM-Datenträger anpassen und ausgleichen, indem Sie die richtige VM-Größe und den passenden Speichertyp auswählen. Normalerweise verfügen die höheren bzw. teureren VM-Größen über umfassendere Garantien für die maximalen IOPS- und Durchsatzwerte. Da Sie dann noch die Wahl zwischen Standard- und Premium-Speicher bzw. HDD und SSD haben, verfügen Sie über mehrere Parameter, um Ihre Anforderungen zu erfüllen.

Damit Sie die richtige Kombination wählen können, müssen Sie Ihre Anwendungsanforderungen kennen. Für Anwendungen mit hohem E/A-Aufwand, z.B. Datenbankserver oder OLTP-Systeme (Online Transactional Processing, Onlinetransaktionsverarbeitung), sind höhere IOPS-Werte erforderlich. Für Anwendungen, die eher computebasiert sind, reichen dagegen unter Umständen geringere Anforderungen aus. Außerdem wirken sich die _Typen_ von Vorgängen, die von Anwendungen durchgeführt werden, auf den Durchsatz aus. Vorgänge mit hohem Random-Access-E/A-Aufwand sind in der Regel langsamer als lange sequenzielle Lesevorgänge.

Nachdem Sie Ihre Konfiguration ausgewählt haben, können Sie Tools wie [Iometer](http://iometer.org/) nutzen, um Ihre Datenträgerleistung auf Linux- und Windows-VMs zu testen. Sie erhalten dann einen praxisbezogeneren Eindruck davon, welche Leistung zu erwarten ist. Außerdem können Sie so besser Möglichkeiten ermitteln, wie Sie die Speichernutzung für Ihre App verbessern. Für eine Anwendung mit Single-Thread-E/A ergibt sich aufgrund von Latenz beispielsweise eher eine niedrigere E/A-Leistung.

Wir sehen uns noch einige andere Optionen zur Verbesserung der Datenträgerleistung an.

