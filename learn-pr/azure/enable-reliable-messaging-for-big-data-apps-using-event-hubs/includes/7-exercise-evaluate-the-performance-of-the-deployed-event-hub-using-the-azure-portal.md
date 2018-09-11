<span data-ttu-id="dd238-101">In dieser Einheit verwenden Sie das Azure-Portal, um zu überprüfen, ob Ihr Event Hub gemäß den gewünschten Anforderungen funktioniert.</span><span class="sxs-lookup"><span data-stu-id="dd238-101">In this unit, you'll use the Azure portal to verify your event hub is working and performing according to the desired expectations.</span></span> <span data-ttu-id="dd238-102">Sie testen auch, wie das Event Hub-Messaging arbeitet, wenn es zeitweise nicht verfügbar ist. Des Weiteren testen Sie Event Hubs-Metriken, um die Leistung Ihres Event Hubs zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="dd238-102">You'll also test how event hub messaging works when it's temporarily unavailable and use Event Hubs metrics to check the performance of your event hub.</span></span>

## <a name="view-event-hub-activity"></a><span data-ttu-id="dd238-103">Anzeigen der Event Hub-Aktivität</span><span class="sxs-lookup"><span data-stu-id="dd238-103">View event hub activity</span></span>

1. <span data-ttu-id="dd238-104">Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="dd238-104">Sing in to your [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="dd238-105">Suchen Sie über die Suchleiste nach Ihrem Event Hub, und öffnen Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="dd238-105">Find your event hub, using the Search bar, and open it.</span></span>

1. <span data-ttu-id="dd238-106">Zeigen Sie auf der Übersichtsseite die Nachrichtenanzahl an.</span><span class="sxs-lookup"><span data-stu-id="dd238-106">On the Overview page, view the message counts.</span></span>

    ![Anzeigen von Event Hub-Nachrichten](../media-draft/6-view-messages.png)

1. <span data-ttu-id="dd238-108">Die Anwendungen „SimpleSend“ und „EventProcessorSample“ werden zum Senden bzw. Empfangen von 100 Nachrichten konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="dd238-108">The SimpleSend and EventProcessorSample applications are configured to send/receive 100 messages.</span></span> <span data-ttu-id="dd238-109">Sie sehen, dass der Event Hub 100 Nachrichten der SimpleSend-Anwendung verarbeitet und 100 Nachrichten an die EventProcessorSample-Anwendung übertragen hat.</span><span class="sxs-lookup"><span data-stu-id="dd238-109">You'll see that the event hub has processed 100 messages from the SimpleSend application, and has transmitted 100 messages to the EventProcessorSample application.</span></span>

## <a name="test-event-hub-resilience"></a><span data-ttu-id="dd238-110">Testen der Event Hub-Resilienz</span><span class="sxs-lookup"><span data-stu-id="dd238-110">Test event hub resilience</span></span>

<span data-ttu-id="dd238-111">Wenn Sie folgende Schritte befolgen, sehen Sie, was passiert, wenn eine Anwendung Nachrichten an einen Event Hub sendet, während dieser vorübergehend nicht verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="dd238-111">Use the following steps to see what happens when an application sends messages to an event hub while it's temporarily unavailable.</span></span>

1. <span data-ttu-id="dd238-112">Senden Sie Nachrichten mithilfe der SimpleSend-Anwendung erneut an den Event Hub.</span><span class="sxs-lookup"><span data-stu-id="dd238-112">Resend messages to the event hub using the SimpleSend application.</span></span> <span data-ttu-id="dd238-113">Verwenden Sie den folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="dd238-113">Use the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. <span data-ttu-id="dd238-114">Wenn Sie **Send Complete...** (Sendevorgang abgeschlossen) sehen, drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="dd238-114">When you see **Send Complete...**, press ENTER.</span></span>

1. <span data-ttu-id="dd238-115">Klicken Sie im Azure-Portal auf **Event Hubs-Instanz** > **EINSTELLUNGEN** > **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="dd238-115">In the Azure portal, click **Event Hubs Instance** > **SETTINGS** > **Properties**.</span></span>

1. <span data-ttu-id="dd238-116">Klicken Sie unter dem Event Hub-Zustand auf **Deaktiviert**.</span><span class="sxs-lookup"><span data-stu-id="dd238-116">Under Event Hub state, click **Disabled**.</span></span>

    ![Deaktivieren des Event Hubs](../media-draft/7-disable-event-hub.png)

<span data-ttu-id="dd238-118">Warten Sie mindestens fünf Minuten.</span><span class="sxs-lookup"><span data-stu-id="dd238-118">Wait for a minimum of five minutes.</span></span>

1. <span data-ttu-id="dd238-119">Klicken Sie unter dem Event Hub-Zustand auf **Aktiv**, um Ihren Event Hub erneut zu aktivieren und Ihre Änderungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="dd238-119">Click **Active** under Event Hub state to re-enable your event hub and save your changes.</span></span>

1. <span data-ttu-id="dd238-120">Ausführen der EventProcessorSample-Anwendung zum Empfangen von Nachrichten</span><span class="sxs-lookup"><span data-stu-id="dd238-120">Rerun the EventProcessorSample application to receive messages.</span></span> <span data-ttu-id="dd238-121">Verwenden Sie den folgenden Befehl.</span><span class="sxs-lookup"><span data-stu-id="dd238-121">Use the following command.</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. <span data-ttu-id="dd238-122">Wenn in der Konsole keine Nachrichten mehr angezeigt werden, drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="dd238-122">When messages stop being displayed to the console, press ENTER.</span></span>

1. <span data-ttu-id="dd238-123">Suchen Sie im Azure-Portal Ihren Event Hub **_namespace_**, und öffnen Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="dd238-123">In the Azure portal, find your event hub **_namespace_** and open it.</span></span> 

1. <span data-ttu-id="dd238-124">Klicken Sie auf **Event Hubs-Namespace** > **ÜBERWACHUNG** > **Metrik (Vorschau)**.</span><span class="sxs-lookup"><span data-stu-id="dd238-124">Click **Event Hubs Namespace** > **MONITORING** > **Metrics (preview)**.</span></span>

    ![Verwenden von Event Hub-Metrik](../media-draft/7-event-hub-metrics.png)

1. <span data-ttu-id="dd238-126">Wählen Sie aus der **Metrik**-Liste die Option **Eingehende Nachricht** aus, und klicken Sie auf **Metrik hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="dd238-126">From the **Metric** list, select **Incoming Messages** and click **Add Metric**.</span></span>

1. <span data-ttu-id="dd238-127">Wählen Sie aus der **Metrik**-Liste die Option **Ausgehende Nachricht** aus, und klicken Sie auf **Metrik hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="dd238-127">From the **Metric** list, select **Outgoing Messages** and click **Add Metric**.</span></span>

1. <span data-ttu-id="dd238-128">Klicken Sie am oberen Rand des Diagramms auf **Letzte 24 Stunden (automatisch)**, um den Zeitraum in **Letzte 30 Minuten** zu ändern.</span><span class="sxs-lookup"><span data-stu-id="dd238-128">At the top of the chart, click **Last 24 hours (Automatic)** to change the time period to **Last 30 minutes**.</span></span>

1. <span data-ttu-id="dd238-129">Klicken Sie auf **Anwenden**.</span><span class="sxs-lookup"><span data-stu-id="dd238-129">Click **Apply**.</span></span>

<span data-ttu-id="dd238-130">Sie sehen nun, dass alle 100 Nachrichten erfolgreich übermittelt wurden, obwohl diese gesendet wurden, bevor der Event Hub für einen Zeitraum offline war.</span><span class="sxs-lookup"><span data-stu-id="dd238-130">You'll see that though the messages were sent before the event hub was taken offline for a period, all 100 messages were successfully transmitted.</span></span>

## <a name="summary"></a><span data-ttu-id="dd238-131">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="dd238-131">Summary</span></span>

<span data-ttu-id="dd238-132">In dieser Einheit haben Sie die Event Hubs-Metrik verwenden, um zu testen, ob Ihr Event Hub den Sende- und Empfangsprozess von Nachrichten erfolgreich verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="dd238-132">In this unit, you used the Event Hubs metrics to test that your event hub is successfully processing the sending and receiving messages.</span></span>
