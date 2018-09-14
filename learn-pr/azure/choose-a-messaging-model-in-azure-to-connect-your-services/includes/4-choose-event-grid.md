Viele Anwendungen verwenden eine Veröffentlichen-Abonnieren-Modell, um verteilte Komponenten zu benachrichtigen, das ist ein Problem aufgetreten, oder, die ein Objekt geändert. Angenommen, Sie haben eine Anwendung zum Austauschen von Musik mit einer Web-API, die in Azure ausgeführt wird. Wenn ein Benutzer eine neue "Song" hochgeladen wird, müssen Sie benachrichtigen von allen mobilen apps auf benutzergeräten auf der ganzen Welt, die dieses Genres interessiert sind installiert.

In dieser Architektur muss der Herausgeber der Datei nicht kennen, einer der Abonnenten, die die freigegebene Musik interessiert. Darüber hinaus möchten wir haben eine 1: n Beziehung, in dem wir mehrere Abonnenten haben, die optional entscheiden können, ob sie diese neue "Song" interessiert sind. Azure Event Grid eignet sich hervorragend für derartige Architekturen.

## <a name="what-is-azure-event-grid"></a>Was ist Azure Event Grid?
Azure Event Grid ist ein vollständig verwalteter ereignisroutingdienst auf Azure Service Fabric ausgeführt wird. Event Grid verteilt _Ereignisse_ aus verschiedenen Quellen, z. B. Azure Blob Storage-Konten oder Azure Media Services an andere Handler, wie Azure Functions oder Webhooks. Event Grid wurde erstellt, um es einfacher, die das ereignisbasierte erstellen und serverlose Anwendungen in Azure zu machen.

Event Grid unterstützt die meisten Azure-Dienste als Verleger oder Abonnenten und mit Diensten von Drittanbietern verwendet werden kann. Event Grid umfasst ein dynamisch skalierbares, kostengünstiges Nachrichtensystem, mit dem Herausgeber Abonnenten benachrichtigen können, wenn der Status sich ändert. Die folgende Abbildung zeigt die Azure Event Grid empfangen von Nachrichten aus mehreren Quellen und Ereignis-Handlern, die basierend auf Abonnements verteilen.

Es gibt verschiedene Konzepte in Azure Event Grid, die eine Quelle an einen Abonnenten zu verbinden:

1. **Ereignisse**: Was ist passiert?
1. **Ereignisquellen**: Wo das Ereignis stattgefunden hat
1. **Themen**: Der Endpunkt, an den Herausgeber Ereignisse senden.
1. **Ereignisabonnements**: Der Endpunkt oder integrierte Mechanismus zum Weiterleiten von Ereignissen, und zwar mitunter zu mehreren Handlern. Abonnements werden auch von Handlern verwendet, um eingehende Ereignisse Intelligent zu filtern.
1. **Ereignishandler**: Die App oder der Dienst, die/der auf das Ereignis reagiert.

![Eine Abbildung, zeigt ein Azure Event Grid zwischen mehreren Ereignisquellen und mehrere Ereignishandler positioniert. Die Ereignisquellen senden Ereignisse an Event Grid und Event Grid relevante Ereignisse an die Abonnenten weitergeleitet. Event Grid verwenden Themen um zu entscheiden, welche Ereignisse an die Handler zu senden. Ereignisquellen tag jedes Ereignis mit einem oder mehreren Themen und -Ereignishandler abonnieren, in den Themen, die, denen Sie interessieren.](../media-draft/5-event-grid.png)

### <a name="what-is-an-event"></a>Was ist ein Ereignis?
**Ereignisse** sind die Datennachrichten über Event Grid übergeben, die beschreiben, was stattgefunden hat. Jedes Ereignis kann ist in sich geschlossen, bis zu 64 KB, und enthält verschiedene Informationen, die anhand eines Schemas, die von Event Grid definiert:

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
| **topic** | Der vollständige Ressourcenpfad für die Ereignisquelle. Dieser Wert wird von Event Grid bereitgestellt. |
| **subject** | Vom Herausgeber definierter Pfad zum Ereignisbetreff |
| **id** | Der eindeutige Bezeichner für das Ereignis. |
| **eventType** | Einer der registrierten Ereignistypen für die Ereignisquelle. Dies ist ein Wert, Sie Filter, z. B. erstellen können `CustomerCreated`, `BlobDeleted`, `HttpRequestReceived`usw. |
| **eventTime** | Die Zeit, die das Ereignis generiert wurde basierend auf UTC-Zeit des Anbieters. |
| **Daten** | Spezielle Informationen, die für den Typ des Ereignisses relevant ist. Beispielsweise enthält ein Ereignis zu einer neuen Datei, die in Azure Storage erstellt wird, Details über die Datei, z.B. den Wert von `lastTimeModified`. Alternativ dazu enthält ein Event Hubs-Ereignis die URL der Erfassungsdatei. Dieses Feld ist optional. |
| **dataVersion** | Die Schemaversion des Datenobjekts. Der Herausgeber definiert die Schemaversion. |
| **metadataVersion** | Die Schemaversion der Ereignismetadaten. Event Grid definiert das Schema der Eigenschaften der obersten Ebene. Dieser Wert wird von Event Grid bereitgestellt. |

> [!TIP]
> Event Grid sendet ein Ereignis an, dass etwas passiert ist oder geändert werden. Allerdings die _eigentliche Objekt_ , das geändert wurde ist nicht Teil der Ereignisdaten. Stattdessen wird eine URL oder einen Bezeichner oft übergeben das geänderte Objekt verweisen.

### <a name="what-is-an-event-source"></a>Was ist eine Ereignisquelle?
Ereignisquellen sind dafür zuständig, Ereignisse an Event Grid zu senden. Jede Ereignisquelle ist mit mindestens einem Ereignistyp verknüpft. Azure Storage ist z.B. die Ereignisquelle für durch Blobs erstellte Ereignisse. IoT Hub ist die Ereignisquelle für Ereignisse, die von Geräten erstellt wurden. Ihre Anwendung ist die Ereignisquelle für benutzerdefinierte Ereignisse, die Sie definieren. Wir werden sogleich Ereignisquellen ausführlicher betrachten.

> [!NOTE]
> Azure Event Hub wird außerdem das Konzept eines Ereignisverlegers definiert. Ein Herausgeber an Event Hub ist der Benutzer oder eine Organisation, die entscheidet, die zum Senden von Ereignissen an Event Grid. Microsoft veröffentlicht beispielsweise Ereignisse für mehrere Azure-Dienste. Sie haben die Möglichkeit, Ereignisse über Ihre eigene Anwendung zu veröffentlichen. Organisationen, die Dienst außerhalb von Azure hosten, können Ereignisse über Event Grid veröffentlichen. Dies ruft häufig mit der Ereignisquelle kombiniert. Die Ereignisquelle, die vollständig definiert ist, dem Verleger und den jeweiligen Dienst, der das Ereignis für diesen Verleger generiert. Hier verwenden wir "Publisher" und "Ereignisquelle" sind austauschbar, um die Entität mit dem Senden der Nachricht an den Event Hub darstellen.

### <a name="what-is-an-event-topic"></a>Was ist ein Ereignisthema?
Event-Themen werden Ereignisse in Gruppen kategorisieren. Themen werden durch einen öffentlichen Endpunkt dargestellt und sind, an die Ereignisquelle Ereignisse sendet _zu_. Wenn Ihre Anwendung entwerfen, können Sie wie viele Themen zu erstellen. Größere Projektmappen erstellt ein benutzerdefiniertes Thema für jede Kategorie von verwandten Ereignissen, während kleinere Projektmappen alle Ereignisse an ein Thema senden können. Denken Sie beispielsweise an eine Anwendung, die Ereignisse im Zusammenhang mit der Änderung von Benutzerkonten und der Verarbeitung von Bestellungen sendet. Es ist unwahrscheinlich, dass ein Ereignishandler beide Ereigniskategorien benötigt. Erstellen Sie zwei benutzerdefinierte Themen, und lassen Sie Ereignishandler das jeweils relevante Thema abonnieren. Ereignisabonnenten können für die Ereignistypen filtern, die sie aus einem bestimmten Thema werden soll.

Themen sind in unterteilt **System** Themen und **benutzerdefinierte** Themen.

#### <a name="system-topics"></a>Systemthemen
Systemthemen sind integrierte Themen, die von Azure-Diensten bereitgestellt werden. Sie können keine Systemthemen in Ihrem Azure-Abonnement ansehen, weil diese dem Herausgeber gehören. Allerdings haben Sie die Möglichkeit, diese zu abonnieren. Dafür stellen Sie Informationen zu der Ressource bereit, deren Ereignisse Sie empfangen möchten. Solange Sie Zugriff auf die Ressource haben, können Sie deren Ereignis abonnieren.

#### <a name="custom-topics"></a>Benutzerdefinierte Themen
Benutzerdefinierte Themen sind Anwendungs- und Drittanbieterthemen. Wenn Sie ein benutzerdefiniertes Thema erstellen oder Zugriff darauf erhalten, wird das benutzerdefinierte Thema in Ihrem Abonnement angezeigt.

### <a name="what-is-an-event-subscription"></a>Was ist ein Ereignisabonnement aus?
Event-Abonnements definieren, welche Ereignisse zu einem Thema, auf die ein Ereignishandler empfangen möchte. Ein Abonnement kann auch Ereignisse nach Typ oder Betreff, filtern, so können Sie sicherstellen, dass ein Ereignishandler nur relevante Ereignisse empfängt.

### <a name="what-is-an-event-handler"></a>Was ist ein Ereignishandler?
Ein Ereignishandler (manchmal auch ein Ereignis "Abonnent" genannt) ist jede Komponente (Anwendung oder Ressource), die Ereignisse von Event Grid empfangen kann. Azure Functions kann z.B. Code ausführen, wenn dem Blob Storage-Konto ein neuer Song hinzugefügt wird. Abonnenten können sich entscheiden, welche Ereignisse sie verarbeiten möchten, und Event Grid benachrichtigt jeden interessierten Abonnenten, wenn ein neues Ereignis verfügbar ist, ohne das ein Abruf notwendig ist.

## <a name="types-of-event-sources"></a>Arten von Ereignisquellen
Ereignisse können von den folgenden Typen von Azure-Ressourcen generiert werden:

- **Azure-Abonnements und -Ressourcengruppen.** Abonnements und Ressourcengruppen generieren Ereignisse im Zusammenhang mit Verwaltungsvorgängen in Azure. Wenn z.B. ein Benutzer einen virtuellen Computer erstellt, generiert diese Quelle ein Ereignis.
- **Container Registry-Instanz.** Der Azure Container Registry-Dienst generiert Ereignisse aus, wenn die Images in der Registrierung hinzugefügt, entfernt oder geändert werden.
- **Event Hub.** Event Hubs kann verwendet werden, zum Verarbeiten und Speichern von Ereignissen aus einer Vielzahl von Datenquellen - Protokollierung in der Regel oder Telemetriedaten, die im Zusammenhang. Event Hubs kann Ereignisse an Event Grid generieren, wenn die Dateien erfasst werden.
- **Servicebus.** Servicebus kann Ereignisse an Event Grid generieren, wenn aktive Nachrichten mit keine aktive Listener vorhanden sind.
- **Speicherkonten.** Speicherkonten können Ereignisse erzeugen, wenn Benutzer Blobs, Dateien, Tabelleneinträge oder Warteschlangennachrichten hinzufügen. Sie können sowohl für Blob-Konten als auch für allgemeine Zwecke V2-Konten als Ereignisquellen verwenden.
- **Media Services.** Media Services dienen zum Hosten von Video- und Audiomedien und bieten erweiterte Verwaltungsfunktionen für Mediendateien. Media Services können Ereignisse generieren, wenn ein Codierungsauftrag in einer Videodatei gestartet oder abgeschlossen wird.
- **Azure IoT Hub.** IoT Hub kommuniziert mit IoT-Geräten und ruft Telemetriedaten von diesen ab. Er kann Ereignisse generieren, wenn diese Nachrichten eingehen.
- **Benutzerdefinierte Ereignisse.** Benutzerdefinierte Ereignisse können mit der REST-API oder dem Azure SDK für Java, GO, .NET, Node, Python und Ruby generiert werden. Sie können z.B. ein benutzerdefiniertes Ereignis im Web-Apps-Feature von Azure App Service erstellen. Dies kann in der workerrolle passieren, wenn sie eine Nachricht von einer Storage-Warteschlange aufnimmt.

Diese enge Integration in unterschiedlichen Ereignisquellen in Azure wird sichergestellt, dass es sich bei Event Grid Ereignisse verteilen kann, die im Zusammenhang mit fast allen Azure-Ressource.

## <a name="event-handlers"></a>Ereignishandler
Die folgenden Objekttypen in Azure können Ereignisse von Event Grid empfangen und verarbeiten:

- **Azure Functions.** Eine Azure-Funktion besteht aus benutzerdefiniertem Code, der in Azure ohne virtuellen Hostserver oder Container ausgeführt wird. Verwenden Sie eine Azure-Funktion als Ereignishandler, wenn Sie eine benutzerdefinierte Antwort auf das Ereignis programmieren möchten.
- **Webhooks.** Ein Webhook ist eine Web-API, die eine Push-Architektur implementiert.
- **Azure Logic Apps.** Eine Azure-Logik-App hostet einen Geschäftsprozess als Workflow.
- **Microsoft Flow.** Flow hostet auch Workflows, ist jedoch von nicht technischen Mitarbeitern einfacher zu verwenden.

## <a name="should-you-use-event-grid"></a>Gründe für das Verwenden von Event Grid
Verwenden Sie Event Grid, wenn Sie folgende Features benötigen:

- **Einfachheit.** Es ist einfach, Abonnenten im Event Grid Quellen herstellen.
- **Erweiterte Filterung.** Abonnements bieten eine genaue Steuerung der Ereignisse, die sie von einem Thema empfangen.
- **Auffächern nach außen.** Sie können eine unbegrenzte Anzahl von Endpunkten für dieselben Ereignisse und Themen abonnieren.
- **Zuverlässigkeit.** Event Grid wiederholt die Ereignisübermittlung für jedes Abonnement für bis zu 24 Stunden.
- **Zahlung pro Ereignis.** Sie zahlen nur für die Anzahl der Ereignisse, die Sie übertragen.

## <a name="summary"></a>Zusammenfassung
Event Grid ist ein einfaches, aber vielseitiges Ereignisverteilungssystem. Verwenden Sie es, um diskrete Ereignisse für Abonnenten zu versenden, die diese Ereignisse zuverlässig und schnell empfangen. Es gibt noch ein weiteres Nachrichtenmodell, das wir uns hier ansehen: Was müssen wir tun, wenn wir einen großen _Ereignisstream_ versenden möchten? In diesem Szenario eignet sich Event Grid nicht besonders gut, weil es nur ein Ereignis gleichzeitig versenden kann. Aber hier eignet sich ein anderer Azure-Dienst: Event Hubs.