Viele Anwendungen verwenden das Veröffentlichen-/Abonnieren-Modell, um verteilte Komponenten zu informieren, dass ein Problem aufgetreten ist oder ein Objekt geändert wurde. Angenommen, Sie verfügen über eine Anwendung für den Austausch von Musik mit einer Web-API, die in Azure ausgeführt wird. Wenn ein Benutzer einen neuen Song hochlädt, müssen Sie weltweit alle auf Endgeräten installierten mobilen Apps benachrichtigen, die Benutzern gehören, die an dem Genre interessiert sind, dem der Song angehört.

In dieser Architektur benötigt der Herausgeber der Audiodatei keine Informationen über die Abonnenten, die an der geteilten Musik interessiert sind. Darüber hinaus soll es eine 1:n-Beziehung mit mehreren Abonnenten geben, die entscheiden können, ob sie an diesem neuen Song interessiert sind. Azure Event Grid eignet sich hervorragend für derartige Architekturen.

## <a name="what-is-azure-event-grid"></a>Was ist Azure Event Grid?
Azure Event Grid ist ein vollständig verwalteter Ereignisroutingdienst, der auf Azure Service Fabric basiert. Der Dienst verteilt _Ereignisse_ aus verschiedenen Quellen wie Azure Blob Storage-Konten oder Azure Media Services an verschiedene Abonnenten wie Azure Functions oder Webhooks. Event Grid wurde erstellt, um das Erstellen von ereignisbasierten und serverlosen Anwendungen in Azure zu vereinfachen.

Event Grid unterstützt die meisten Azure-Dienste und sogar Drittanbieterdienste als Herausgeber oder Abonnent. Event Grid umfasst ein dynamisch skalierbares, kostengünstiges Nachrichtensystem, mit dem Herausgeber Abonnenten über Statusänderungen benachrichtigen können. Die folgende Abbildung zeigt, wie Azure Event Grid Nachrichten von verschiedenen Quellen empfängt und basierend auf dem Abonnement an Ereignishandler verteilt.

Es gibt verschiedene Konzepte in Azure Event Grid, über die eine Verbindung zwischen einer Quelle und einem Abonnenten hergestellt werden kann:

1. **Ereignisse:** Was ist passiert?
1. **Ereignisquellen:** Wo hat das Ereignis stattgefunden?
1. **Themen:** der Endpunkt, an den Herausgeber Ereignisse senden.
1. **Ereignisabonnements**: der Endpunkt oder integrierte Mechanismus zum Weiterleiten von Ereignissen (teilweise an mehrere Handler). Abonnements werden auch von Handlern verwendet, um eingehende Ereignisse intelligent zu filtern.
1. **Ereignishandler:** die App oder der Dienst, der auf das Ereignis reagiert.

![Abbildung eines Azure Event Grid-Elements, das zwischen mehreren Ereignisquellen und mehreren Ereignishandlern positioniert ist Die Ereignisquellen senden Ereignisse an das Event Grid, das die relevanten Ereignisse an die Abonnenten weiterleitet. Event Grid verwendet Themen, um zu entscheiden, welche Ereignisse an welche Handler gesendet werden sollen. Ereignisquellen kennzeichnen jedes Ereignis mit mindestens einem Thema, und Ereignishandler abonnieren die Themen, an denen sie interessiert sind.](../media/4-event-grid.png)

### <a name="what-is-an-event"></a>Was ist ein Ereignis?
**Ereignisse** sind Datennachrichten, die über Event Grid übertragen werden und Informationen über Vorkommnisse enthalten. Jedes Ereignis ist eigenständig, kann bis zu 64 KB umfassen und enthält mehrere Informationen, die auf einem von Event Grid definierten Schema basieren:

```json
[
  {
    "topic": string,
    "subject": string,
    "id": string,
    "eventType": string,
    "eventTime": string,
    "data":{
      object-unique-to-each-publisher
    },
    "dataVersion": string,
    "metadataVersion": string
  }
]
```

| Feld | Beschreibung |
|-------|-------------|
| **topic** | Der vollständige Ressourcenpfad zu der Ereignisquelle. Dieser Wert wird von Event Grid bereitgestellt. |
| **subject** | Vom Herausgeber definierter Pfad zum Ereignisbetreff. |
| **id** | Der eindeutige Bezeichner eines Ereignisses. |
| **eventType** | Einer der für diese Ereignisquelle registrierten Ereignistypen. Für diesen Wert können Sie Filter erstellen, z.B. `CustomerCreated`, `BlobDeleted` oder `HttpRequestReceived`. |
| **eventTime** | Die Zeit, in der das Ereignis generiert wird, basierend auf der UTC-Zeit des Anbieters. |
| **data** | Informationen, die sich auf den Ereignistypen beziehen. Beispielsweise enthält ein Ereignis zu einer neuen Datei, die in Azure Storage erstellt wird, Details über die Datei, z.B. den Wert `lastTimeModified`. Alternativ dazu enthält ein Event Hubs-Ereignis die URL der Erfassungsdatei. Dieses Feld ist optional. |
| **dataVersion** | Die Schemaversion des Datenobjekts. Der Herausgeber definiert die Schemaversion. |
| **metadataVersion** | Die Schemaversion der Ereignismetadaten. Event Grid definiert das Schema der Eigenschaften der obersten Ebene. Dieser Wert wird von Event Grid bereitgestellt. |

> [!TIP]
> Event Grid sendet ein Ereignis, wenn etwas passiert oder Änderungen vorgenommen wurden. Das _eigentliche Objekt_, an dem eine Änderung vorgenommen wurde, ist dabei allerdings nicht Bestandteil der Ereignisdaten. Stattdessen wird häufig eine URL oder ein Bezeichner übergeben, um auf das geänderte Objekt zu verweisen.

### <a name="what-is-an-event-source"></a>Was ist eine Ereignisquelle?
Ereignisquellen sind dafür zuständig, Ereignisse an Event Grid zu senden. Jede Ereignisquelle ist mit mindestens einem Ereignistyp verknüpft. Azure Storage ist z.B. die Ereignisquelle für von Blobs erstellten Ereignissen. IoT Hub ist die Ereignisquelle für Ereignisse, die von Geräten erstellt wurden. Ihre Anwendung ist die Ereignisquelle für benutzerdefinierte Ereignisse, die Sie definieren. Später erhalten Sie noch einen detaillierteren Überblick über Ereignisquellen.

> [!NOTE]
> Außerdem definiert Azure Event Hub das Konzept eines Ereignisherausgebers. Ein Herausgeber für Event Hub ist der Benutzer oder die Organisation, die Ereignisse an Event Grid sendet. Microsoft veröffentlicht beispielsweise Ereignisse für mehrere Azure-Dienste. Sie haben die Möglichkeit, Ereignisse über Ihre eigene Anwendung zu veröffentlichen. Organisationen, die Dienste außerhalb von Azure hosten, können Ereignisse über Event Grid veröffentlichen. Dies wird häufig mit der Ereignisquelle verwechselt. Die vollständig definierte Ereignisquelle ist der Herausgeber und der Dienst, der das Ereignis für diesen Herausgeber erstellt. In diesem Dokument stehen die Begriffe „Herausgeber“ und „Ereignisquelle“ beide für die Entität, die die Nachricht an Event Hub senden.

### <a name="what-is-an-event-topic"></a>Was ist eine Ereignisthema?
Ereignisthemen kategorisieren Ereignisse in Gruppen. Themen werden von einem öffentlichen Endpunkt dargestellt und sind das _Ziel_ von Ereignissen, die von der Ereignisquelle gesendet werden. Sie können beim Entwerfen Ihrer Anwendung entscheiden, wie viele Themen erstellt werden sollen. Größere Lösungen erstellen für jede Kategorie von verknüpften Ereignissen ein benutzerdefiniertes Thema, während kleinere Lösungen ggf. sämtliche Ereignisse an nur ein Thema senden. Denken Sie beispielsweise an eine Anwendung, die Ereignisse im Zusammenhang mit der Änderung von Benutzerkonten und der Verarbeitung von Bestellungen sendet. Es ist unwahrscheinlich, dass ein Ereignishandler beide Ereigniskategorien benötigt. Erstellen Sie zwei benutzerdefinierte Themen, und lassen Sie die Ereignishandler das jeweils für sie relevante Thema abonnieren. Ereignisabonnenten können nach den gewünschten Ereignistypen eines bestimmten Themas filtern.

Themen werden in **Systemthemen** und **benutzerdefinierte** Themen gegliedert.

#### <a name="system-topics"></a>Systemthemen
Systemthemen sind integrierte Themen, die von Azure-Diensten bereitgestellt werden. Es werden keine Systemthemen in Ihrem Azure-Abonnement angezeigt, weil diese dem Herausgeber gehören. Allerdings haben Sie die Möglichkeit, sie zu abonnieren. Stellen Sie dafür Informationen zu der Ressource bereit, deren Ereignisse Sie empfangen möchten. Solange Sie Zugriff auf eine Ressource haben, können Sie auch ihre Ereignisse abonnieren.

#### <a name="custom-topics"></a>Benutzerdefinierte Themen
Benutzerdefinierte Themen sind Anwendungs- und Drittanbieterthemen. Wenn Sie ein benutzerdefiniertes Thema erstellen oder Zugriff darauf erhalten, wird dieses in Ihrem Abonnement angezeigt.

### <a name="what-is-an-event-subscription"></a>Was ist ein Ereignisabonnement?
Ereignisabonnements definieren, welche Ereignisse zu einem Thema der Ereignishandler empfangen soll. Ein Abonnement kann Ereignisse auch anhand ihres Typs oder Betreffs filtern, sodass Sie sicherstellen können, dass ein Ereignishandler nur relevante Ereignisse empfängt.

### <a name="what-is-an-event-handler"></a>Was ist eine Ereignishandler?
Ein Ereignishandler (teilweise auch als „Ereignisabonnent“ bezeichnet) ist eine beliebige Komponente (eine Anwendung oder eine Ressource), die Ereignisse von Event Grid empfangen kann. Azure Functions kann z.B. Code ausführen, wenn dem Blob Storage-Konto ein neuer Song hinzugefügt wird. Abonnenten können sich entscheiden, welche Ereignisse sie verarbeiten möchten, und Event Grid benachrichtigt jeden interessierten Abonnenten, wenn ein neues Ereignis verfügbar ist, ohne dass ein Abruf notwendig ist.

## <a name="types-of-event-sources"></a>Arten von Ereignisquellen
Ereignisse können von den folgenden Azure-Ressourcentypen generiert werden:

- **Azure-Abonnements und -Ressourcengruppen:** Abonnements und Ressourcengruppen generieren Ereignisse, die im Zusammenhang mit Verwaltungsvorgängen in Azure stehen. Wenn z.B. ein Benutzer einen virtuellen Computer erstellt, generiert diese Quelle ein Ereignis.
- **Containerregistrierung:** Azure Container Registry ist ein Dienst, der Ereignisse generiert, wenn Images der Registrierung hinzugefügt, aus ihr entfernt oder geändert werden.
- **Event Hub:** Event Hub kann verwendet werden, um Ereignisse aus verschiedenen Datenquellen zu verarbeiten und zu speichern. Diese Datenquellen stehen in der Regel im Zusammenhang mit der Protokollierung oder Telemetrie. Event Hub kann Ereignisse für Event Grid erstellen, wenn Dateien erfasst werden.
- **Service Bus:** Service Bus kann Ereignisse für Event Grid erzeugen, wenn aktive Nachrichten ohne aktive Listener vorhanden sind.
- **Speicherkonten:** Speicherkonten können Ereignisse erzeugen, wenn Benutzer Blobs, Dateien, Tabelleneinträge oder Warteschlangennachrichten hinzufügen. Sie können sowohl Blobkonten als auch universelle V2-Konten als Ereignisquellen verwenden.
- **Media Services:** Media Services dient dem Hosten von Video- und Audiomedien und bietet erweiterte Verwaltungsfeatures für Mediendateien. Diese Plattform kann Ereignisse generieren, wenn ein Codierungsauftrag für eine Videodatei gestartet oder abgeschlossen wird.
- **Azure IoT Hub:** IoT Hub kommuniziert mit IoT-Geräten und ruft Telemetriedaten von diesen ab. Der Dienst generiert Ereignisse, wenn diese Nachrichten eingehen.
- **Benutzerdefinierte Ereignisse:** Diese können mit der REST-API oder dem Azure SDK für Java, GO, .NET, Node, Python und Ruby generiert werden. Sie können z.B. ein benutzerdefiniertes Ereignis im Web-Apps-Feature von Azure App Service erstellen. Das kann in der Workerrolle passieren, wenn sie eine Nachricht aus einer Speicherwarteschlange abfängt.

Diese umfassende Integration in verschiedene Ereignisquellen innerhalb von Azure stellt sicher, dass Event Grid Ereignisse verteilen kann, die sich auf nahezu alle Azure-Ressourcen beziehen.

## <a name="event-handlers"></a>Ereignishandler
Die folgenden Objekttypen in Azure können Ereignisse von Event Grid empfangen und verarbeiten:

- **Azure Functions:** Eine Azure-Funktion besteht aus benutzerdefiniertem Code, der in Azure ohne virtuellen Hostserver oder Container ausgeführt wird. Verwenden Sie eine Azure-Funktion als Ereignishandler, wenn Sie eine benutzerdefinierte Antwort auf das Ereignis programmieren möchten.
- **Webhooks:** Ein Webhook ist eine Web-API, die eine Pusharchitektur implementiert.
- **Azure Logic Apps:** Eine Azure-Logik-App hostet einen Geschäftsprozess als Workflow.
- **Microsoft Flow:** Flow hostet auch Workflows, kann jedoch von Laien einfacher verwendet werden.

## <a name="should-you-use-event-grid"></a>Gründe für das Verwenden von Event Grid
Verwenden Sie Event Grid, wenn Sie folgende Features benötigen:

- **Einfachheit:** In Event Grid ist es sehr einfach, Quellen mit Abonnenten zu verbinden.
- **Erweitertes Filtern:** Abonnements bieten eine genaue Steuerung der Ereignisse, die sie von einem Thema empfangen.
- **Auffächern:** Sie können für die gleichen Ereignisse und Themen eine unbegrenzte Anzahl von Endpunkten abonnieren.
- **Zuverlässigkeit:** Event Grid wiederholt die Ereignisübermittlung für jedes Abonnement bis zu 24 Stunden.
- **Zahlung pro Ereignis:** Sie zahlen nur für die Anzahl der Ereignisse, die Sie übertragen.

Event Grid ist ein einfaches, aber vielseitiges Ereignisverteilungssystem. Verwenden Sie es, um diskrete Ereignisse für Abonnenten zu versenden, die diese Ereignisse zuverlässig und schnell empfangen. Es gibt noch ein weiteres Nachrichtenmodell, das wir uns hier ansehen: Was müssen wir tun, wenn wir einen großen _Ereignisstream_ versenden möchten? In diesem Szenario eignet sich Event Grid nicht besonders gut, weil es nur ein Ereignis gleichzeitig versenden kann. Aber hier eignet sich ein anderer Azure-Dienst: Event Hubs.