Viele Anwendungen verwenden Ereignisse, um verteilte Komponenten zu informieren, dass ein Problem aufgetreten ist oder ein Objekt geändert wurde. Sie können Azure Event Grid verwenden, um die Verteilung dieser Ereignisse über Azure zu vereinfachen.

Angenommen, Sie haben eine Anwendung zum Austauschen von Musik mit einer Web-API, die in Azure ausgeführt wird. Wenn ein Benutzer eine neue Audiodatei hochlädt, müssen Sie weltweit alle auf den Endgeräten installierten mobile Apps benachrichtigen.

Sie können Azure Event Grid-Abonnements verwenden, um dies zuverlässig und schnell zu erreichen.

## <a name="what-is-event-grid"></a>Was ist Event Grid?

Event Grid ist ein Dienst, der Ereignisse aus Quellen wie Azure Blob-Speicherkonten oder Azure Media Services an Abonnenten wie Azure Functions oder Webhooks verteilt.

Eine Ereignisquelle ist eine beliebige Komponente, die ein Ereignis generieren kann. Beispielsweise kann ein Benutzer einem Blob-Speicherkonto eine neue Mediendatei hinzufügen. Dies generiert ein Ereignis, das von Event Grid verteilt werden kann.

Ein Ereignisabonnent ist eine beliebige Komponente, die Ereignisse von Event Grid empfangen kann. Azure Functions kann beispielsweise Code ausführen, der auf die neue Mediendatei im Blob-Speicherkonto reagiert.

Event Grid erleichtert das Verbinden von Datenquellen mit mehreren Abonnenten.

![Diagramm mit Event Grid-Quellen und -Abonnenten](../images/6-event-grid.png)

## <a name="event-sources"></a>Ereignisquellen

Ereignisse können von den folgenden Typen von Azure-Ressourcen generiert werden:

- **Azure-Abonnements und -Ressourcengruppen.** Abonnements und Ressourcengruppen generieren Ereignisse im Zusammenhang mit Verwaltungsvorgängen in Azure. Wenn z.B. ein Benutzer einen virtuellen Computer erstellt, generiert diese Quelle ein Ereignis.
- **Speicherkonten.** Speicherkonten können Ereignisse erzeugen, wenn Benutzer Blobs, Dateien, Tabelleneinträge oder Warteschlangennachrichten hinzufügen. Sie können sowohl Blob- als auch allgemeine Konten als Ereignisquellen verwenden.
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

## <a name="how-to-choose"></a>Auswahl

Verwenden Sie Event Grid, wenn Sie diese Features benötigen:

- **Einfachheit.** In Event Grid ist es sehr einfach, Datenquellen mit Abonnenten zu verbinden.
- **Erweiterte Filterung.** Abonnements bieten eine genaue Steuerung der Ereignisse, die sie von einem Thema empfangen.
- **Auffächern nach außen.** Sie können für die gleichen Ereignisse und Themen eine unbegrenzte Anzahl von Endpunkten abonnieren.
- **Zuverlässigkeit.** Event Grid wiederholt die Ereignisübermittlung für jedes Abonnement für bis zu 24 Stunden.
- **Zahlung pro Ereignis.** Sie zahlen nur für die Anzahl der Ereignisse, die Sie übertragen.

## <a name="summary"></a>Zusammenfassung

Event Grid ist ein einfaches, aber vielseitiges Ereignisverteilungssystem. Verwenden Sie es, um Ereignisse für Abonnenten zu veröffentlichen, die diese Ereignisse zuverlässig und schnell empfangen.