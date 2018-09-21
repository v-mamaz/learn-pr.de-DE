Es gibt bestimmte Anwendungen, die eine riesige Anzahl von Ereignissen aus fast ebenso vielen Quellen erzeugen. Für diese Szenarios, für deren Bewältigung eine einzigartige Infrastruktur erforderlich ist, wird häufig der Begriff „Big Data“ verwendet.

Angenommen, Sie arbeiten bei Contoso Aircraft Engines. Die Triebwerke, die Ihr Arbeitgeber herstellt, haben Hunderte von Sensoren. Bevor ein Flugzeug morgens geflogen werden kann, werden seine Triebwerke mit einem Prüfkabel verbunden und auf Herz und Nieren geprüft. Zusätzlich werden während des Flugs zwischengespeicherte Daten gestreamt, wenn das Flugzeug mit der Bodenausrüstung verbunden wird.

Sie möchten bislang erfasste Sensordaten verwenden, um Muster in den Sensormesswerten zu finden, die darauf hinweisen, dass ein Triebwerksausfall wahrscheinlich schon bald eintreten wird. Sie möchten die Echtzeit-Sensorwerte mit diesen Störungsmustern vergleichen. Sie können dann Benutzer nahezu in Echtzeit warnen, wenn ein Triebwerk besorgniserregende Werte meldet.

## <a name="what-is-azure-event-hubs"></a>Was ist Azure Event Hubs?
Bei Event Hubs handelt es sich um einen Zwischendienst für Kommunikationsmuster zum Veröffentlichen bzw. Abonnieren. Im Gegensatz zu Event Grid ist dieser Dienst auf sehr hohe Durchsätze, viele Herausgeber, Sicherheit und Resilienz ausgerichtet.

#### <a name="what-is-an-event-hub"></a>Was ist ein Event Hub?

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yuat]

Event Grid eignet sich sehr gut für das Veröffentlichen-Abonnieren-Muster, da es Abonnements verwaltet und Kommunikation an die Abonnenten weiterleitet. Event Hubs bietet hingegen noch weitere Dienste. Diese zusätzlichen Aufgaben verleihen Event Hub den Charakter einer Service Bus-Warteschlange oder einer Nachrichtenwarteschlange. Daher kann man nicht von einem einfachen Ereignisbroadcaster sprechen.

#### <a name="partitions"></a>Partitionen
Die von Event Hubs empfangenen Nachrichten werden in Partitionen aufgeteilt. Partitionen sind Puffer, in denen die Nachrichten gespeichert werden. Aufgrund der Ereignispuffer sind Ereignisse nicht ausschließlich von kurzfristiger Bedeutung, und ein Ereignis wird nicht verpasst, nur weil ein Abonnent gerade beschäftigt oder sogar offline ist. Der Abonnent kann den Puffer jederzeit nutzen, um sich zu informieren. Standardmäßig bleiben Ereignisse 24 Stunden im Puffer und verfallen dann automatisch.

Die Puffer werden Partitionen genannt, da die Daten unter ihnen aufgeteilt sind. Jede Event Hubs-Instanz verfügt über mindestens zwei Partitionen, und jede Partition verfügt über eine eigene Gruppe von Abonnenten.

#### <a name="capture"></a>Capture
Event Hubs kann alle Ihre Ereignisse sofort an Azure Data Lake oder Azure Blob Storage senden, um sie dauerhaft und kostengünstig zu speichern.

#### <a name="authentication"></a>Authentifizierung
Allen Herausgebern wird nach ihrer Authentifizierung ein Token ausgestellt. Das bedeutet, dass Event Hubs Ereignisse von externen Geräten und mobilen Anwendungen akzeptieren kann, ohne dass Sie sich Sorgen darüber machen müssten, ob gefälschte Daten von Betrügern Ihre Analyse beeinträchtigen könnten. 

## <a name="using-event-hubs"></a>Verwenden von Event Hubs
Event Hubs bietet Unterstützung für das Übertragen von Ereignisdatenströmen an andere Azure-Dienste. Seine Verwendung mit Azure Stream Analytics ermöglicht beispielsweise die komplexe Analyse von Daten nahezu in Echtzeit mit der Möglichkeit, mehrere Ereignisse zu korrelieren und nach Mustern zu suchen. In diesem Fall würde Stream Analytics als Abonnent betrachtet werden.

Bei unseren Flugzeugtriebwerken richten wir unsere Architektur so ein, dass Event Hubs die Nachrichten von unseren Triebwerken authentifiziert. Anschließend soll Capture verwendet werden, um sämtliche Daten in Data Lake zu speichern. Später können Sie sämtliche Daten verwenden, um Machine Learning-Modelle erneut zu trainieren und zu verbessern. Schließlich werden unsere Ereignisdatenströme von Stream Analytics-Abonnenten empfangen. Stream Analytics verwendet unser Machine Learning-Modell zum Suchen nach Mustern in den Sensordaten, die auf Probleme hinweisen könnten.

Da mehrere Partitionen vorhanden sind und jedes Triebwerk alle seine Daten an nur eine Partition sendet, muss sich jede Instanz unseres Stream Analytics-Abonnenten nur mit einer Teilmenge unserer Gesamtdaten befassen. Sie müssen weder gefiltert noch korreliert werden.

## <a name="which-service-should-i-choose"></a>Welcher Dienst eignet sich für mich?
Genauso wie bei der Wahl der richtigen Warteschlange, scheint die Wahl zwischen diesen beiden Diensten zur Zustellung von Ereignissen zunächst schwierig. Beide unterstützen *At-Least-Once*-Semantiken.

#### <a name="choose-event-hubs-if"></a>Verwenden Sie Event Hubs, wenn Folgendes zutrifft:  

- Sie müssen die Authentifizierung einer großen Anzahl von Herausgebern unterstützen.
- Sie einen Datenstrom von Ereignissen in Data Lake oder Blob Storage speichern müssen.
- Sie eine Aggregation oder Analyse für Ihren Ereignisdatenstrom benötigen.
- Sie benötigen zuverlässiges Messaging oder Resilienz.  

Wenn Sie stattdessen für Ereignisse eine einfache Infrastruktur zum Veröffentlichen bzw. Abonnieren mit vertrauenswürdigen Herausgebern (z.B. Ihrem eigenen Webserver) benötigen, sollten Sie sich für Event Grid entscheiden.

Mithilfe von Event Hub können Sie eine Pipeline für Big Data erstellen, die mit geringer Latenz Millionen von Ereignissen pro Sekunde verarbeiten kann. Der Dienst kann gleichzeitige Quellen verarbeiten und an verschiedene Infrastrukturen zum Verarbeiten von Streams und an Analysedienste senden. Er ermöglicht die Verarbeitung in Echtzeit und unterstützt das wiederholte Abrufen von gespeicherten Rohdaten. 