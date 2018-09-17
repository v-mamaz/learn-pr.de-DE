Es gibt viele Kommunikationsplattformen, die zur Verbesserung der Zuverlässigkeit einer verteilten Anwendung beitragen können, darunter auch mehrere innerhalb von Azure. Jedes dieser Tools dient einem anderen Zweck, daher sehen wir uns hier einmal die einzelnen Tools in Azure an, um Sie bei der Wahl des richtigen Tools zu unterstützen.

Die Architektur unserer Bestell- und Nachverfolgungsanwendung für Pizza erfordert mehrere Komponenten: eine Website, Datenspeicherung, einen Back-End-Dienst usw. Wir können die Komponenten unserer Anwendung auf viele verschiedene Arten miteinander verbinden, und eine einzelne Anwendung kann mehrere Techniken nutzen. 

Wir müssen entscheiden, welche Techniken in der Contoso Slices-Anwendung verwendet werden sollen. Der erste Schritt besteht darin, jede Stelle auszuwerten, an der Kommunikation zwischen mehreren Bestandteilen stattfindet. Einige Komponenten _müssen_ zeitnah ausgeführt werden, damit unsere Anwendung überhaupt ihre Arbeit verrichten kann. Andere sind zwar wichtig, aber nicht zeitkritisch. Und wieder andere, wie etwa unsere Benachrichtigungen für mobile Apps, sind etwas optionaler.

Hier erfahren Sie mehr über die in Azure verfügbaren Kommunikationsplattformen, sodass Sie für jede Anforderung in Ihrer Anwendung die richtige auswählen können.

## <a name="decide-between-messages-and-events"></a>Entscheiden zwischen Nachrichten und Ereignissen

Nachrichten und Ereignisse sind beides **Datagramme**: Pakete von Daten, die von einer Komponente an eine andere gesendet werden. Sie unterscheiden sich auf eine Art und Weise, die zunächst subtil erscheint, aber erhebliche Unterschiede dabei bewirken kann, wie Sie Ihre Anwendung gestalten. 

### <a name="messages"></a>Nachrichten

In der Terminologie verteilter Anwendungen ist das bestimmende Merkmal einer Nachricht, dass die allgemeine Integrität der Anwendung davon abhängen kann, dass Nachrichten empfangen werden. Sie können sich das Senden einer Nachricht so vorstellen, dass eine Komponente den Staffelstab eines Workflows an eine andere Komponente übergibt. Der gesamte Workflow kann ein wichtiger Geschäftsprozess sein, und die Nachricht ist der Mörtel, der die Komponenten zusammenhält.

Eine Nachricht enthält im Allgemeinen die Daten selbst, nicht nur einen Verweis auf Daten (etwa eine ID oder URL). Das Senden der Daten als Teil des Datagramms ist weniger fehleranfällig als das Senden eines Verweises. Die Messagingarchitektur garantiert die Zustellung der Nachricht, und da keine zusätzlichen Nachschlagevorgänge erforderlich sind, wird die Nachricht zuverlässig verarbeitet. Die sendende Anwendung muss jedoch genau wissen, welche Daten enthalten sein müssen, um nicht zu viele Daten zu senden, wodurch die empfangende Komponente gezwungen wäre, unnötige Arbeiten auszuführen. In diesem Sinne sind Sender und Empfänger einer Nachricht oft durch einen strengen Datenvertrag verbunden.

In der neuen Architektur von Contoso Slices würden bei der Eingabe einer Pizzabestellung wahrscheinlich Nachrichten verwendet. Das Web-Front-End oder eine mobile App würde eine Nachricht an die Back-End-Verarbeitungskomponenten senden. In den Back-End-Schritten würden beispielsweise die Weiterleitung an eine Filiale in der Nähe des Kunden und die Belastung der Kreditkarte stattfinden.

### <a name="events"></a>Ereignisse

Ein Ereignis löst eine Benachrichtigung darüber aus, dass etwas passiert ist. Ereignisse sind einfacher als Nachrichten und werden am häufigsten für die Broadcastkommunikation verwendet.

Ereignisse weisen folgende Merkmale auf:
* Das Ereignis kann an mehrere Empfänger oder an gar keine Empfänger gesendet werden.
* Ereignisse sollen sich meist „weit verbreiten“ oder weisen eine große Anzahl von Abonnenten für jeden Herausgeber auf.
* Der Herausgeber des Ereignisses hat keine Erwartungen hinsichtlich der Aktion, die eine empfangende Komponente ausführt.

Unsere Pizzakette würde wahrscheinlich Ereignisse verwenden, um Benutzer mittels Benachrichtigungen über Statusänderungen zu informieren. Die Statusänderungsereignisse könnten an Azure Event Grid, dann an Azure Functions und anschließend an Azure Notification Hubs gesendet werden, um eine vollständig _serverlose_ Lösung zu erreichen.

Hierbei handelt es sich um einen wesentlichen Unterschied zwischen Ereignissen und Nachrichten, da Kommunikationsplattformen in der Regel entweder Ereignisse oder Nachrichten verarbeiten. Service Bus wurde für die Verarbeitung von Nachrichten entwickelt. Wenn Sie Ereignisse senden möchten, würden Sie sich wahrscheinlich für Event Grid entscheiden. 

Azure verfügt zwar auch über Azure Event Hubs, diese Lösung wird jedoch am häufigsten für eine bestimmte Art von Kommunikation mit hohem Datenfluss für Analysen verwendet. Wenn unsere Pizzaöfen beispielsweise mit vernetzten Sensoren ausgestattet wären, könnten wir Event Hubs in Verbindung mit Azure Stream Analytics verwenden, um nach Mustern bei Temperaturänderungen zu suchen, die auf einen unerwünschten Brand oder Komponentenverschleiß hindeuten.

## <a name="service-bus-topics-queues-and-relays"></a>Service Bus-Themen, -Warteschlangen und -Relays

Azure Service Bus kann Nachrichten auf drei verschiedene Arten austauschen: über Warteschlangen, Themen und Relays.

### <a name="what-is-a-queue"></a>Was ist eine Warteschlange?

Eine **Warteschlange** ist ein einfacher temporärer Speicherort für Nachrichten. Eine sendende Komponente fügt der Warteschlange eine Nachricht hinzu. Eine Zielkomponente ruft die Nachricht am Anfang der Warteschlange ab. Unter normalen Umständen wird jede Nachricht von nur einem Empfänger empfangen.

![Azure Service Bus-Warteschlange](../media-draft/2-service-bus-queue.png)

Warteschlangen entkoppeln die Quell- und Zielkomponenten, um die Zielkomponenten von hohen Anforderungen zu isolieren. 

In Spitzenzeiten können Nachrichten schneller eintreffen, als die Zielkomponenten sie verarbeiten können. Da Quellkomponenten nicht direkt mit dem Ziel verbunden sind, ist die Quelle nicht betroffen, und die Warteschlange wächst. Zielkomponenten entfernen Nachrichten aus der Warteschlange, sobald sie in der Lage sind, diese zu verarbeiten. Wenn die Anforderungen abnehmen, können die Zielkomponenten aufholen, und die Warteschlange verkürzt sich. 

Eine Warteschlange reagiert auf diese Weise auf hohe Anforderungen, ohne dass dem System Ressourcen hinzugefügt werden müssen. Bei Nachrichten, die relativ schnell verarbeitet werden müssen, kann das Hinzufügen zusätzlicher Instanzen Ihrer Zielkomponente jedoch dazu führen, dass diese die Last teilen können. Jede Nachricht würde nur von einer Instanz verarbeitet. Dies ist eine effiziente Möglichkeit, Ihre gesamte Anwendung zu skalieren und dabei nur Ressourcen für die Komponenten hinzuzufügen, die diese tatsächlich benötigen.

### <a name="what-is-a-topic"></a>Was ist ein Thema?

Ein **Thema** ähnelt einer Warteschlange, kann jedoch über mehrere Abonnements verfügen. Dies bedeutet, dass mehrere Zielkomponenten ein einzelnes Thema abonnieren können, sodass jede Nachricht an mehrere Empfänger übermittelt wird. Abonnements können die Nachrichten im Thema auch filtern, um nur Nachrichten zu empfangen, die relevant sind. Abonnements bieten die gleiche entkoppelten Kommunikation wie Warteschlangen und reagieren auf die gleiche Weise auf hohe Anforderungen. Verwenden Sie ein Thema, wenn jede Nachricht an mehrere Zielkomponenten übermittelt werden soll.

Themen werden für den Basic-Tarif nicht unterstützt.

![Azure Service Bus-Thema](../media-draft/2-service-bus-topic.png)

### <a name="what-is-a-relay"></a>Was ist ein Relay?

Ein **Relay** ist ein Objekt für die synchrone bidirektionale Kommunikation zwischen Anwendungen. Es ist kein temporärer Speicherort für Nachrichten wie Warteschlangen und Themen. Stattdessen stellt es bidirektionale, ungepufferte Verbindungen über Netzwerkgrenzen hinweg bereit. (Ein Beispiel für eine Netzwerkgrenze wäre etwa eine Firewall.) Verwenden Sie ein Relay, wenn Sie eine direkte Kommunikation zwischen Komponenten benötigen, als befänden sie sich im gleichen Netzwerksegment, obwohl sie durch Netzwerksicherheitsgeräte getrennt sind.

> [!NOTE]
> Relays sind zwar Teil von Azure Service Bus, implementieren aber keine lose gekoppelten Messagingworkflows und werden in diesem Modul nicht weiter berücksichtigt.

## <a name="service-bus-queues-and-storage-queues"></a>Service Bus-Warteschlangen und Speicherwarteschlangen

Es gibt zwei Azure-Features, die Nachrichtenwarteschlangen enthalten: Service Bus und Azure Storage-Konten. Im Allgemeinen sind Speicherwarteschlangen einfacher zu verwenden, aber weniger komplex und flexibel als Service Bus-Warteschlangen.

Zu den wichtigsten Vorteilen von Service Bus-Warteschlangen zählen folgende:

* Sie unterstützen größeren Nachrichten (256 KB pro Nachricht im Vergleich zu 64 KB).
* Sie unterstützen die Übermittlungstypen „At-Least-Once“ (mindestens ein Mal) und „At-Most-Once“ (höchstens ein Mal). Sie haben also die Wahl, ob Sie sich bestmöglich gegen den Verlust einer Nachricht oder gegen eine doppelte Verarbeitung einer Nachricht absichern möchten.
* Sie garantieren die **FIFO-Reihenfolge (First-In-First-Out)**: Nachrichten werden in der Reihenfolge verarbeitet, in der sie hinzugefügt wurden. (FIFO ist zwar der normale Betriebsmodus einer Warteschlange, er wird jedoch nicht für jede Nachricht garantiert.)
* Sie können mehrere Nachrichten zu einer Transaktion gruppieren: Wenn eine Nachricht in der Transaktion nicht übermittelt werden kann, wird keine der Nachrichten in der Transaktion übermittelt.
* Sie unterstützen rollenbasierte Sicherheit.
* Sie erfordern nicht, dass Zielkomponenten die Warteschlange kontinuierlich abfragen.

Vorteile von Speicherwarteschlangen:

* Sie unterstützen eine unbegrenzte Warteschlangengröße (im Gegensatz zum Grenzwert von 80 GB bei Service Bus-Warteschlangen).
* Sie pflegen ein Protokoll aller Nachrichten.

## <a name="how-to-choose-a-communications-technology"></a>Auswählen einer Kommunikationstechnologie

Wir haben die verschiedenen Konzepte und Implementierungen kennengelernt, die Azure anbietet. Sehen wir uns nun an, wie unser Entscheidungsprozess für jede unserer Kommunikationsaktivitäten aussehen sollte.

#### <a name="consider-the-following-questions"></a>Stellen Sie sich die folgenden Fragen:

1. Ist die Kommunikation ein Ereignis? Falls ja, sollten Sie Event Grid oder Event Hubs verwenden.

1. Soll eine einzelne Nachricht an mehrere Ziele übermittelt werden? Falls ja, verwenden Sie ein Service Bus-Thema. Falls nicht, verwenden Sie eine Warteschlange.

Für Warteschlangen gilt:

#### <a name="choose-service-bus-queues-if"></a>Verwenden Sie Service Bus-Warteschlangen, wenn Folgendes zutrifft:

- Sie benötigen eine At-Most-Once-Zustellungsgarantie.
- Sie benötigen eine FIFO-Garantie.
- Sie müssen Nachrichten in Transaktionen gruppieren.
- Sie möchten Nachrichten empfangen, ohne die Warteschlange abzufragen.
- Sie benötigen rollenbasierten Warteschlangenzugriff.
- Sie müssen Nachrichten mit einer Größe von 64 bis 256 KB verarbeiten.
- Die Warteschlangengröße liegt unter 80 GB.
- Sie möchten Nachrichtenbatches veröffentlichen und nutzen können.

#### <a name="choose-queue-storage-if"></a>Verwenden Sie Queue Storage, wenn Folgendes zutrifft:
- Sie benötigen eine einfache Warteschlange ohne besondere zusätzliche Anforderungen.
- Sie benötigen serverseitige Protokolle aller Nachrichten, die die Warteschlange passieren.
- Sie gehen davon aus, dass die Größe der Warteschlange 80 GB überschreitet.
- Sie möchten den Verarbeitungsfortschritt einer Nachricht innerhalb der Warteschlange nachverfolgen.

Die Komponenten einer verteilten Anwendung können zwar direkt kommunizieren, durch die Verwendung einer Zwischenkommunikationsplattform wie Azure Service Bus oder Azure Event Grid lässt sich jedoch häufig die Zuverlässigkeit dieser Kommunikation verbessern.

Event Grid ist für Ereignisse konzipiert, die Empfänger nur über ein Ereignis informieren und nicht die diesem Ereignis zugeordneten Rohdaten enthalten. Azure Event Hubs wurde für Analyseereignisse mit hohem Datenfluss entwickelt. Azure Service Bus und Speicherwarteschlangen sind für Nachrichten konzipiert und können zur Bindung der wesentlichen Bestandteile jedes Anwendungsworkflows verwendet werden.

Wenn Sie keine besonders komplexen Anforderungen haben, jede Nachricht nur an ein einzelnes Ziel senden oder möglichst schnell programmieren möchten, ist möglicherweise eine Speicherwarteschlange die beste Option. Andernfalls bieten Service Bus-Warteschlangen viele weitere Optionen und größere Flexibilität.

Wenn Sie Nachrichten an mehrere Abonnenten senden möchten, verwenden Sie ein Service Bus-Thema.
