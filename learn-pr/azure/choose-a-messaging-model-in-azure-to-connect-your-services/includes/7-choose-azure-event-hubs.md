Es gibt bestimmte Anwendungen, die eine riesige Anzahl von Ereignissen aus fast ebenso vielen Quellen erzeugen. Wir hören oft den Begriff „Big Data“ für diese Szenarien, für deren Bewältigung eine einzigartige Infrastruktur erforderlich ist.

Angenommen, Sie arbeiten bei Contoso Aircraft Engines. Die Triebwerke, die Ihr Arbeitgeber herstellt, haben Hunderte von Sensoren. Bevor ein Flugzeug morgens geflogen werden kann, werden seine Triebwerke mit einem Prüfkabel verbunden und auf Herz und Nieren geprüft. Zusätzlich werden während des Flugs zwischengespeicherte Daten gestreamt, wenn das Flugzeug mit der Bodenausrüstung verbunden wird.

Sie möchten bislang erfasste Sensordaten verwenden, um Muster in den Sensormesswerten zu finden, die darauf hinweisen, dass ein Triebwerksausfall wahrscheinlich schon bald eintreten wird. Sie möchten die Echtzeit-Sensorwerte mit diesen Störungsmustern vergleichen. Sie können dann Benutzer nahezu in Echtzeit warnen, wenn ein Triebwerk besorgniserregende Werte meldet.

## <a name="what-is-azure-event-hubs"></a>Was sind Azure Event Hubs?

Azure Event Hub ist ein Vermittler für das Kommunikationsmuster „Veröffentlichen-Abonnieren“. Doch im Gegensatz zu Event Grid ist diese Produkt für extrem hohen Durchsatz, eine große Anzahl von Herausgebern, Sicherheit und Resilienz optimiert.

Event Grid fügt sich mehr oder weniger perfekt in das Muster „Veröffentlichen-Abonnieren“ ein, indem es einfach Abonnements verwaltet und Nachrichten an diese Abonnenten weiterleitet. Auf der anderen Seite führt Event Hub einige zusätzliche Dienste aus, wodurch die Lösung in gewisser Weise eher einem Servicebus oder einer Nachrichtenwarteschlange ähnelt als einem einfachen Ereignisbroadcaster.

#### <a name="partitions"></a>Partitionen ####
Die von Event Hub empfangenen Nachrichten werden in Partitionen aufgeteilt. Partitionen sind Puffer, in denen die Nachrichten gespeichert werden. Aufgrund der Ereignispuffer sind Ereignisse nicht völlig flüchtig, und ein Ereignis wird nicht verpasst, nur weil ein Abonnent gerade beschäftigt oder sogar offline ist. Der Abonnent kann den Puffer jederzeit zum „Aufholen“ nutzen. Standardmäßig bleiben Ereignisse 24 Stunden im Puffer und verfallen dann automatisch.

Die Puffer werden Partitionen genannt, da die Daten unter ihnen aufgeteilt sind. Jede Event Hub-Instanz verfügt über mindestens zwei Partitionen, und jede Partition verfügt über eine eigene Gruppe von Abonnenten.

#### <a name="capture"></a>Erfassung ####
Event Hub kann alle Ihre Ereignisse sofort an Azure Data Lake oder Blob Storage senden, um sie dauerhaft und kostengünstig zu speichern.

#### <a name="authentication"></a>Authentifizierung ####
Allen Herausgebern wird nach ihrer Authentifizierung ein Token ausgestellt. Dies bedeutet, dass Event Hub Ereignisse von externen Geräten und mobilen Anwendungen akzeptieren kann, ohne sich Sorgen darüber machen zu müssen, ob gefälschte Daten von Betrügern unsere Analyse ruinieren könnten. 

## <a name="using-azure-event-hub"></a>Verwenden von Azure Event Hubs

Event Hubs bietet Unterstützung für das Übertragen von Ereignisdatenströmen an andere Azure-Dienste. Seine Verwendung mit Stream Analytics ermöglicht beispielsweise die komplexe Analyse von Daten in nahezu Echtzeit mit der Möglichkeit, mehrere Ereignisse zu korrelieren und nach Mustern zu suchen. In diesem Fall würde Stream Analytics als Abonnent betrachtet werden.

Bei unseren Flugzeugtriebwerken richten wir unsere Architektur so ein, dass Event Hubs die Nachrichten von unseren Triebwerken authentifiziert. Wir lassen die Lösung dann Capture von Event Hubs verwenden, um alle Daten in Azure Data Lake zu speichern. Später können wir alle diese Daten verwenden, um unsere Machine Learning-Modelle weiter zu trainieren und zu verbessern. Schließlich werden unsere Ereignisdatenströme von Azure Stream Analytics-Abonnenten empfangen. Stream Analytics verwendet unser Machine Learning-Modell zum Suchen nach Mustern in den Sensordaten, die auf Probleme hinweisen könnten.

Da wir mehrere Partitionen haben und jedes Triebwerk alle seine Daten an nur eine Partition sendet, muss sich jede Instanz unseres Stream Analytics-Abonnenten nur mit einer Teilmenge unserer Gesamtdaten befassen, anstatt sie zu filtern und zu korrelieren.

## <a name="choose-event-grid-or-event-hub"></a>Wahl zwischen Event Grid oder Event Hub

Beide unterstützen Semantik des Typs *Mindestens einmal*.

Wenn Sie für Ereignisse eine einfache „Veröffentlichen-Abonnieren“-Infrastruktur mit vertrauenswürdigen Herausgebern (z.B. Ihrem eigenen Webserver) benötigen, sollten Sie sich für Azure Event Grid entscheiden.

### <a name="consider-event-hub-if"></a>Erwägen Sie Event Hubs, wenn
* Sie die Authentifizierung einer großen Anzahl von Herausgebern unterstützen müssen.
* Sie einen Datenstrom von Ereignissen in Azure Data Lake oder Blob Storage speichern müssen.
* Sie eine Aggregation oder Analyse für Ihren Ereignisdatenstrom benötigen.
* Sie zuverlässiges Messaging oder Resilienz benötigen. 