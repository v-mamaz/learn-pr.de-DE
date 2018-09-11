Viele Anwendungen verwenden das Herausgeben-Abonnieren-Modell, um verteilte Komponenten zu informieren, dass ein Problem aufgetreten ist oder ein Objekt geändert wurde. Angenommen, Sie haben eine Anwendung zum Austauschen von Musik mit einer Web-API, die in Azure ausgeführt wird. Wenn ein Benutzer einen Song hochlädt, müssen Sie alle auf Endgeräten installierten mobilen Apps weltweit benachrichtigen, die Benutzern gehören, die an dem Genre des Songs interessiert sind, der gerade hochgeladen wurde.

In dieser Architektur muss der Herausgeber der Audiodatei nichts von den Abonnenten wissen, die an der veröffentlichten Musik interessiert sind. Darüber hinaus soll es eine 1:n-Beziehung mit mehreren Abonnenten geben, die entscheiden können, ob sie an diesem neuen Song interessiert sind. Azure Event Grid eignet sich hervorragend für derartige Architekturen.

## <a name="what-is-event-grid"></a>Was ist Event Grid?
Event Grid ist ein Dienst, der _Ereignisse_ aus verschiedenen Quellen wie Azure Blob Storage-Konten oder Azure Media Services an verschiedene Abonnenten wie Azure Functions oder Webhooks verteilt.

### <a name="what-is-an-event-source"></a>Was ist eine Ereignisquelle?
Eine Ereignisquelle ist eine Komponente, die ein Ereignis generieren kann (auch als „Herausgeber“ bezeichnet). Beispielsweise kann ein Benutzer einem Blob Storage-Konto über unsere Web-API einen neuen Song hinzufügen. Dies generiert ein Ereignis, das von Event Grid an interessierte Abonnenten verteilt werden kann. Herausgeber senden Ereignisse, haben aber keine bestimmten Erwartungen, wer oder was diese empfängt oder verarbeitet.

### <a name="what-is-an-event-subscriber"></a>Was ist ein Ereignisabonnent?
Ein Ereignisabonnent ist jede Komponente, die Ereignisse von Event Grid empfangen kann. Azure Functions kann z.B. Code ausführen, wenn dem Blob Storage-Konto ein neuer Song hinzugefügt wird. Abonnenten können sich entscheiden, welche Ereignisse sie verarbeiten möchten, und Event Grid benachrichtigt jeden interessierten Abonnenten, wenn ein neues Ereignis verfügbar ist, ohne das ein Abruf notwendig ist.

Event Grid unterstützt die meisten Azure-Dienste und sogar Drittanbieterdienste als Herausgeber oder Abonnent. Event Grid umfasst ein dynamisch skalierbares, kostengünstiges Nachrichtensystem, mit dem Herausgeber Abonnenten benachrichtigen können, wenn der Status sich ändert.

![Diagramm mit Event Grid-Quellen und -Abonnenten](../media-draft/5-event-grid.png)

> [!NOTE]
> Event Grid sendet Ereignisse, um Abonnenten über Änderungen zu informieren. In der Ereignisbereitstellung ist allerdings nicht das _geänderte Objekt_ enthalten.

## <a name="types-of-event-sources"></a>Arten von Ereignisquellen
Ereignisse können von den folgenden Typen von Azure-Ressourcen generiert werden:

- **Azure-Abonnements und -Ressourcengruppen.** Abonnements und Ressourcengruppen generieren Ereignisse im Zusammenhang mit Verwaltungsvorgängen in Azure. Wenn z.B. ein Benutzer einen virtuellen Computer erstellt, generiert diese Quelle ein Ereignis.
- **Speicherkonten.** Speicherkonten können Ereignisse erzeugen, wenn Benutzer Blobs, Dateien, Tabelleneinträge oder Warteschlangennachrichten hinzufügen. Sie können sowohl Blobkonten als auch allgemeine Konten als Ereignisquellen verwenden.
- **Media Services.** Media Services dienen zum Hosten von Video- und Audiomedien und bieten erweiterte Verwaltungsfeatures für Mediendateien. Media Services können Ereignisse generieren, wenn ein Codierungsauftrag in einer Videodatei gestartet oder abgeschlossen wird.
- **Azure IoT Hub.** IoT Hub kommuniziert mit IoT-Geräten und ruft Telemetriedaten von diesen ab. Er kann Ereignisse generieren, wenn diese Nachrichten eingehen.
- **Benutzerdefinierte Ereignisse.** Benutzerdefinierte Ereignisse können mit der REST-API oder dem Azure SDK für Java, GO, .NET, Node, Python und Ruby generiert werden. Sie können z.B. ein benutzerdefiniertes Ereignis im Web-Apps-Feature von Azure App Service erstellen. Das kann in der Workerrolle passieren, wenn sie eine Nachricht aus einer Speicherwarteschlange abfängt.

Diese weitgehende Integration in verschiedene Ereignisquellen innerhalb von Azure stellt sicher, dass Event Grid Ereignisse verteilen kann, die sich auf nahezu alle Azure-Ressourcen beziehen.

## <a name="topics"></a>Themen
Ein Event Grid-Thema ist eine Sammlung ähnlicher Ereignisse. Wenn Sie Ereignisse aus einer Quelle veröffentlichen, entscheiden Sie, ob diese Ereignisse nur ein einziges Thema benötigen oder in mehrere Themen aufgeteilt werden sollen. Komponenten, die Ereignisse empfangen und verarbeiten, abonnieren Themen, um die Ereignisse zu bestimmen, die sie empfangen.

## <a name="subscriptions"></a>Abonnements
Ereignishandler verwenden Abonnements, um Event Grid mitzuteilen, welche Ereignisse in einem Thema sie empfangen möchten. Das Abonnement bestimmt auch den Endpunkt, d.h. den Ort, an den Event Grid Ereignisbenachrichtigungen sendet. Ein Abonnement kann Ereignisse auch anhand ihres Typs oder Betreffs filtern, sodass Sie sicherstellen können, dass ein Ereignishandler nur relevante Ereignisse empfängt.

## <a name="event-handlers"></a>Ereignishandler
Die folgenden Objekttypen in Azure können Ereignisse von Event Grid empfangen und verarbeiten:

- **Azure Functions.** Eine Azure-Funktion besteht aus benutzerdefiniertem Code, der in Azure ohne virtuellen Hostserver oder Container ausgeführt wird. Verwenden Sie eine Azure-Funktion als Ereignishandler, wenn Sie eine benutzerdefinierte Antwort auf das Ereignis programmieren möchten.
- **Webhooks.** Ein Webhook ist eine Web-API, die eine Push-Architektur implementiert.
- **Azure Logic Apps.** Eine Azure-Logik-App hostet einen Geschäftsprozess als Workflow.
- **Microsoft Flow.** Flow hostet auch Workflows, ist jedoch von nicht technischen Mitarbeitern einfacher zu verwenden.

## <a name="should-you-use-event-grid"></a>Gründe für das Verwenden von Event Grid
Verwenden Sie Event Grid, wenn Sie folgende Features benötigen:

- **Einfachheit.** In Event Grid ist es sehr einfach, Datenquellen mit Abonnenten zu verbinden.
- **Erweiterte Filterung.** Abonnements bieten eine genaue Steuerung der Ereignisse, die sie von einem Thema empfangen.
- **Auffächern nach außen.** Sie können für die gleichen Ereignisse und Themen eine unbegrenzte Anzahl von Endpunkten abonnieren.
- **Zuverlässigkeit.** Event Grid wiederholt die Ereignisübermittlung für jedes Abonnement für bis zu 24 Stunden.
- **Zahlung pro Ereignis.** Sie zahlen nur für die Anzahl der Ereignisse, die Sie übertragen.

## <a name="summary"></a>Zusammenfassung
Event Grid ist ein einfaches, aber vielseitiges Ereignisverteilungssystem. Verwenden Sie es, um diskrete Ereignisse für Abonnenten zu versenden, die diese Ereignisse zuverlässig und schnell empfangen. Es gibt noch ein weiteres Nachrichtenmodell, das wir uns hier ansehen: Was müssen wir tun, wenn wir einen großen _Ereignisstream_ versenden möchten? In diesem Szenario eignet sich Event Grid nicht besonders gut, weil es nur ein Ereignis gleichzeitig versenden kann. Aber hier eignet sich ein anderer Azure-Dienst: Event Hubs.