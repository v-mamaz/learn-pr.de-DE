Es gibt viele Kommunikationsplattformen, die zur Verbesserung der Zuverlässigkeit einer verteilten Anwendung beitragen können, darunter auch mehrere innerhalb von Azure. Jedes dieser Tools dient einem anderen Zweck. Lassen Sie uns jedes Tool in Azure untersuchen, um Sie bei der Auswahl des richtigen Tools zu unterstützen.

Die Architektur unserer Pizzabestell- und -nachverfolgungsanwendung erfordert mehrere Komponenten: eine Website, Datenspeicherung, einen Back-End-Dienst usw. Wir können die Komponenten unserer Anwendung auf viele verschiedene Arten miteinander verbinden, und eine einzige Anwendung kann mehrere Techniken nutzen. 

Wir müssen entscheiden, welche Techniken in der Contoso Slices-Anwendung verwendet werden sollen. Der erste Schritt besteht darin, jede Stelle auszuwerten, an der Kommunikation zwischen mehreren Bestandteilen stattfindet. Einige Komponenten _müssen_ zeitgerecht ausgeführt werden, damit unsere Anwendung überhaupt ihre Arbeit verrichten kann. Einige mögen wichtig sein, aber nicht zeitkritisch. Schließlich sind andere Komponenten, wie unsere Benachrichtigungen für mobile Apps, etwas optionaler.

Hier erfahren Sie mehr über die in Azure verfügbaren Kommunikationsplattformen, sodass Sie für jede Anforderung in Ihrer Anwendung die richtige auswählen können.

## <a name="decide-between-messages-and-events"></a>Entscheiden zwischen Nachrichten und Ereignissen

Nachrichten und Ereignisse sind beides **Datagramme**: Pakete von Daten, die von einer Komponente an eine andere gesendet werden. Sie unterscheiden sich auf eine Art und Weise, die zunächst subtil erscheint, aber erhebliche Unterschiede dabei bewirken kann, wie Sie Ihre Anwendung gestalten. 

### <a name="messages"></a>Nachrichten

In der Terminologie verteilter Anwendungen ist das bestimmende Merkmal einer Nachricht, dass die allgemeine Integrität der Anwendung davon abhängen kann, dass Nachrichten empfangen werden. Sie können sich das Senden einer Nachricht so vorstellen, dass eine Komponente den Staffelstab eines Workflows an eine andere Komponente übergibt. Der gesamte Workflow kann ein wichtiger Geschäftsprozess sein, und die Nachricht ist der Mörtel, der die Komponenten zusammenhält.

Eine Nachricht enthält im Allgemeinen die Daten selbst, nicht nur einen Verweis (wie eine ID oder URL) auf Daten. Das Senden der Daten als Teil des Datagramms ist weniger fehleranfällig als das Senden eines Verweises. Die Messagingarchitektur garantiert die Zustellung der Nachricht, und da keine zusätzlichen Nachschlagevorgänge erforderlich sind, wird die Nachricht zuverlässig verarbeitet. Die sendende Anwendung muss jedoch genau wissen, welche Daten enthalten sein müssen, um nicht zu viele Daten zu senden, wodurch die empfangende Komponente gezwungen wäre, unnötige Verarbeitung auszuführen. In diesem Sinne sind Sender und Empfänger einer Nachricht oft durch einen strengen Datenvertrag verbunden.

In der neuen Architektur von Contoso Slice würden bei der Eingabe einer Pizzabestellung wahrscheinlich Nachrichten verwendet. Das Web-Front-End oder eine mobile App würde eine Nachricht an die Back-End-Verarbeitungskomponenten senden. In den Back-End-Schritten würden z.B. die Weiterleitung an eine Filiale in der Nähe des Kunden und die Belastung der Kreditkarte stattfinden.

### <a name="events"></a>Ereignisse

Ein Ereignis benachrichtigt darüber, dass etwas geschehen ist. Ereignisse sind „leichter“ als Nachrichten und werden am häufigsten für die Broadcastkommunikation verwendet.
Ereignisse weisen die folgenden Merkmale auf:
* Das Ereignis kann an mehrere Empfänger oder an gar keine Empfänger gesendet werden.
* Ereignisse sollen sich meist „weit verbreiten“ oder weisen eine große Anzahl von Abonnenten für jeden Herausgeber auf.
* Der Herausgeber des Ereignisses hat keine Erwartungen hinsichtlich der Aktion, die eine empfangende Komponente ausführt.

Unsere Pizzakette würde wahrscheinlich Ereignisse für Benachrichtigungen verwenden, die Benutzer über Statusänderungen informieren. Das Statusänderungsereignis könnte an Azure Event Grid, dann an eine Azure Function-Funktion und an den Notification Hub für eine vollständig _serverlose_ Lösung gesendet werden.

Dieser Unterschied zwischen Ereignissen und Nachrichten ist grundlegend, da Kommunikationsplattformen im Allgemeinen so konzipiert sind, dass sie das eine oder das andere verarbeiten. Service Bus wurde für die Verarbeitung von Nachrichten entwickelt. Wenn Sie Ereignisse senden möchten, würden Sie wahrscheinlich Event Grid auswählen. 

Außerdem verfügt Azure über Azure Event Hub. Dieser wird aber am häufigsten für eine bestimmte Art von hohem Kommunikationsdatenstrom für Analysen verwendet. Wenn wir beispielsweise vernetzte Sensoren an unseren Pizzaöfen hätten, könnten wir Event Hub in Verbindung mit Azure Stream Analytics verwenden, um nach Mustern in den Temperaturänderungen zu suchen, die auf einen unerwünschten Brand oder Komponentenverschleiß hinweisen könnten.

## <a name="service-bus-topics-queues-and-relays"></a>Service Bus-Themen, -Warteschlangen und -Relays

Azure Service Bus kann Nachrichten auf drei verschiedene Arten austauschen: über Warteschlangen, Themen und Relays.

### <a name="what-is-a-queue"></a>Was ist eine Warteschlange?

Ein **Warteschlange** ist ein einfacher temporärer Speicherort für Nachrichten. Eine sendende Komponente fügt der Warteschlange eine Nachricht hinzu. Eine Zielkomponente ruft die Nachricht am Anfang der Warteschlange ab. Unter normalen Umständen wird jede Nachricht von nur einem Empfänger empfangen.

![Azure Service Bus-Warteschlange](../media-draft/2-service-bus-queue.png)

Warteschlangen entkoppeln die Quell- und Zielkomponenten, um die Zielkomponenten von hohen Anforderungen zu isolieren. 

In Spitzenzeiten können Nachrichten schneller eintreffen, als die Zielkomponente sie verarbeiten kann. Da Quellkomponenten keine direkte Verbindung mit dem Ziel aufweisen, ist die Quelle nicht betroffen, und die Warteschlange wächst. Zielkomponenten entfernen Nachrichten aus der Warteschlange, sobald sie in der Lage sind, diese zu verarbeiten. Wenn die Anforderungen abnehmen, können die Zielkomponenten aufholen, und die Warteschlange verkürzt sich. 

Eine Warteschlange reagiert auf diese Weise auf hohe Anforderungen, ohne dass dem System Ressourcen hinzugefügt werden müssen. Bei Nachrichten, die relativ schnell verarbeitet werden müssen, kann das Hinzufügen zusätzlicher Instanzen Ihrer Zielkomponente jedoch dazu führen, dass diese die Last teilen können. Jede Nachricht würde nur von einer Instanz verarbeitet. Dies ist eine effiziente Möglichkeit, Ihre gesamte Anwendung zu skalieren und dabei Ressourcen nur für die Komponenten hinzuzufügen, die diese tatsächlich benötigen.

### <a name="what-is-a-topic"></a>Was ist ein Thema?

Ein **Thema** ähnelt einer Warteschlange, kann jedoch über mehrere Abonnements verfügen. Dies bedeutet, dass mehrere Zielkomponenten ein einzelnes Thema abonnieren können, sodass jede Nachricht an mehrere Empfänger übermittelt wird. Abonnements können die Nachrichten im Thema auch filtern, um nur Nachrichten zu empfangen, die relevant sind. Abonnements bieten die gleiche entkoppelten Kommunikation wie Warteschlangen und reagieren auf die gleiche Weise auf hohe Anforderungen. Verwenden Sie ein Thema, wenn jede Nachricht an mehrere Zielkomponenten übermittelt werden soll.

Themen werden für den Basic-Tarif nicht unterstützt.

![Azure Service Bus-Thema](../media-draft/2-service-bus-topic.png)

### <a name="what-is-a-relay"></a>Was ist ein Relay?

Ein **Relay** ist ein Objekt, das synchrone bidirektionale Kommunikation zwischen Anwendungen ausführt. Es ist kein temporärer Speicherort für Nachrichten wie Warteschlangen und Themen. Stattdessen bietet es eine bidirektionale, ungepufferte Verbindung über Netzwerkgrenzen (z.B. Firewalls) hinweg. Verwenden Sie ein Relay, wenn Sie direkte Kommunikation zwischen Komponenten wünschen, als ob sie sich im gleichen Netzwerksegment befinden, aber durch Netzwerksicherheitsgeräte getrennt sind.

> [!NOTE]
> Obwohl Relays Teil von Azure Service Bus sind, implementieren sie keine lose gekoppelten Messagingworkflows und werden in diesem Modul nicht weiter berücksichtigt.

## <a name="service-bus-queues-and-storage-queues"></a>Service Bus-Warteschlangen und Speicherwarteschlangen

Es gibt zwei Azure-Features, die Nachrichtenwarteschlangen enthalten: Service Bus und Speicherkonten. Im Allgemeinen sind Speicherwarteschlangen einfacher zu verwenden, aber weniger anspruchsvoll und flexibel als Service Bus-Warteschlangen.

Die wichtigsten Vorteile von Service Bus-Warteschlangen:

* Sie unterstützen größeren Nachrichten (256 KB pro Nachricht im Vergleich zu 64 KB).
* Sie unterstützen die Übermittlungstypen „At-Least-Once“ (mindestens ein Mal) und „At-Most-Once“ (höchstens ein Mal). Wählen Sie zwischen der sehr geringen Möglichkeit aus, dass eine Nachricht verloren geht, und der sehr geringen Möglichkeit, dass sie zwei Mal verarbeitet wird.
* Sie garantieren die **FIFO-Reihenfolge (First-In-First-Out)**: Nachrichten werden in der gleichen Reihenfolge verarbeitet wie sie hinzugefügt werden (obwohl FIFO der normale Betrieb einer Warteschlange ist, ist diese Reihenfolge nicht für jede Nachricht garantiert).
* Sie können mehrere Nachrichten in einer Transaktion gruppieren: Wenn eine Nachricht in der Transaktion nicht übermittelt werden kann, werden alle Nachrichten in der Transaktion nicht übermittelt.
* Sie unterstützen rollenbasierte Sicherheit.
* Sie erfordern nicht, dass Zielkomponenten die Warteschlange kontinuierlich abfragen.

Vorteile von Speicherwarteschlangen:

* Sie unterstützen eine unbegrenzte Warteschlangengröße (im Gegensatz zum Grenzwert von 80 GB für Service Bus-Warteschlangen).
* Sie verwalten ein Protokoll aller Nachrichten.

## <a name="how-to-choose-a-communications-technology"></a>Auswählen einer Kommunikationstechnologie

Wir haben die verschiedenen Konzepte und Implementierungen kennengelernt, die Azure anbietet. Sehen wir uns nun an, wie unser Entscheidungsprozess für jede unserer Kommunikationsaktivitäten aussehen sollte.

#### <a name="consider-the-following-questions"></a>Stellen Sie sich die folgenden Fragen:

1. Ist die Kommunikation ein Ereignis? Wenn dies der Fall ist, sollten Sie Event Grid oder Event Hub verwenden.

1. Sollte eine einzelne Nachricht an mehrere Ziele übermittelt werden? Wenn dies der Fall ist, verwenden Sie ein Service Bus-Thema. Verwenden Sie andernfalls eine Warteschlange.

Wenn Sie sich dafür entscheiden, dass Sie eine Warteschlange benötigen:

#### <a name="choose-service-bus-queues-if"></a>Verwenden Sie Service Bus-Warteschlangen, wenn Folgendes zutrifft:

- Sie benötigen eine At-Most-Once-Zustellungsgarantie.
- Sie benötigen eine FIFO-Garantie.
- Sie müssen Nachrichten in Transaktionen gruppieren.
- Sie möchten Nachrichten empfangen, ohne die Warteschlange abzufragen.
- Sie müssen ein rollenbasiertes Zugriffsmodell für die Warteschlange bereitstellen.
- Sie müssen Nachrichten mit einer Größe von 64 bis 256 KB verarbeiten.
- Die Warteschlangengröße liegt unter 80 GB.
- Sie möchten Nachrichtenbatches veröffentlichen und nutzen können.

#### <a name="choose-queue-storage-if"></a>Verwenden Sie Queue Storage, wenn Folgendes zutrifft:
- Sie benötigen eine einfache Warteschlange ohne besondere zusätzliche Anforderungen.
- Sie benötigen serverseitige Protokolle aller Nachrichten, die die Warteschlange passieren.
- Sie gehen davon aus, dass die Größe der Warteschlange 80 GB überschreitet.
- Sie möchten den Verarbeitungsfortschritt einer Nachricht innerhalb der Warteschlange nachverfolgen.

Obwohl die Komponenten einer verteilten Anwendung direkt kommunizieren können, können Sie die Zuverlässigkeit dieser Kommunikation oft erhöhen, indem Sie eine Zwischenkommunikationsplattform wie Azure Service Bus oder Event Grid verwenden.

Event Grid ist für Ereignisse konzipiert, die nur Empfänger über ein Ereignis informieren und nicht die diesem Ereignis zugeordneten Rohdaten enthalten. Event Hub wurde für hohe Datenflussanalyseereignisse entwickelt. Azure Service Bus und Speicherwarteschlangen sind für Nachrichten konzipiert und können für die Bindung der wesentlichen Bestandteile jedes Anwendungsworkflows verwendet werden.

Wenn Ihre Anforderungen einfach sind, wenn Sie jede Nachricht nur an ein Ziel senden oder so schnell wie möglich Code schreiben möchten, kann eine Speicherwarteschlange die beste Option sein. Andernfalls bieten Service Bus-Warteschlangen viele weitere Optionen und größere Flexibilität.

Wenn Sie Nachrichten an mehrere Abonnenten senden möchten, verwenden Sie ein Service Bus-Thema.
