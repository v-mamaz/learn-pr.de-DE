<span data-ttu-id="f5c79-101">Wir haben uns entschieden, ein Azure Service Bus-Thema zu verwenden, um Nachrichten über die Vertriebsleistung in Ihrer verteilten Sales Force-Anwendung zu verteilen.</span><span class="sxs-lookup"><span data-stu-id="f5c79-101">You have chosen to use an Azure Service Bus topic to distribute messages about sales performance in your sales force distributed application.</span></span> <span data-ttu-id="f5c79-102">Die von Vertriebsmitarbeitern auf ihren mobilen Geräten verwendete App sendet Nachrichten mit zusammengefassten Umsatzzahlen für die einzelnen Gebiete und Zeiträume.</span><span class="sxs-lookup"><span data-stu-id="f5c79-102">The app used by sales personnel on their mobile devices will send messages that summarize sales figures for each area and time period.</span></span> <span data-ttu-id="f5c79-103">Diese Nachrichten werden an Webdienste verteilt, die sich in den Geschäftsregionen des Unternehmens befinden, einschließlich Amerika und Europa.</span><span class="sxs-lookup"><span data-stu-id="f5c79-103">Those messages will be distributed to web services located in the company's operational regions, including the Americas and Europe.</span></span>

<span data-ttu-id="f5c79-104">Sie haben in Ihrem Azure-Abonnement bereits die erforderliche Infrastruktur implementiert, einschließlich des Themas und der Abonnements.</span><span class="sxs-lookup"><span data-stu-id="f5c79-104">You have already implemented the necessary infrastructure in your Azure subscription, including the topic and subscriptions.</span></span> <span data-ttu-id="f5c79-105">Jetzt möchten Sie den Code schreiben, der Nachrichten an das Thema sendet und Nachrichten von den einzelnen Abonnements abruft.</span><span class="sxs-lookup"><span data-stu-id="f5c79-105">Now, you want to write the code that sends messages to the topic and retrieves messages from each subscription.</span></span>

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="f5c79-106">Konfigurieren einer Verbindungszeichenfolge für einen Service Bus-Namespace</span><span class="sxs-lookup"><span data-stu-id="f5c79-106">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="f5c79-107">Konfigurieren Sie zunächst Verbindungszeichenfolgen in der sendenden und empfangenden Komponente:</span><span class="sxs-lookup"><span data-stu-id="f5c79-107">Start by configuring connection strings both in the sending and receiving components:</span></span>

1. <span data-ttu-id="f5c79-108">Wechseln Sie zum Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="f5c79-108">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="f5c79-109">Klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="f5c79-109">In the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="f5c79-110">Klicken Sie unter **EINSTELLUNGEN** auf **Freigegebene Zugriffsrichtlinien**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-110">Under **SETTINGS**, click **Shared Access Policies**.</span></span>

1. <span data-ttu-id="f5c79-111">Klicken Sie in der Liste mit den Richtlinien auf **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-111">In the list of policies, click **RootManageSharedAccessKey**.</span></span>

1. <span data-ttu-id="f5c79-112">Klicken Sie rechts vom Textfeld **Primäre Verbindungszeichenfolge** auf die Schaltfläche **Klicken Sie zum Kopieren**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-112">To the right of the **Primary Connection string** text box, click the **Click to copy** button.</span></span>

1. <span data-ttu-id="f5c79-113">Wechseln Sie zu **Visual Studio Code**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-113">Switch to **Visual Studio Code**.</span></span>

1. <span data-ttu-id="f5c79-114">Klicken Sie im Bereich **Explorer** im Ordner **performancemessagesender** auf die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-114">In the **Explorer** pane, in the **performancemessagesender** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="f5c79-115">Suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="f5c79-115">Locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. <span data-ttu-id="f5c79-116">Platzieren Sie den Cursor zwischen den Anführungszeichen, und drücken Sie dann **STRG+V**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-116">Place the cursor between the quotation marks, and then press **Ctrl+V**.</span></span>

1. <span data-ttu-id="f5c79-117">Klicken Sie im Bereich **Explorer** im Ordner **performancemessagereceiver** auf die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-117">In the **Explorer** pane, in the **performancemessagereceiver** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="f5c79-118">Suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="f5c79-118">Locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. <span data-ttu-id="f5c79-119">Platzieren Sie den Cursor zwischen den Anführungszeichen, und drücken Sie dann **STRG+V**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-119">Place the cursor between the quotation marks, and then press **Ctrl+V**.</span></span>

1. <span data-ttu-id="f5c79-120">Klicken Sie auf **Datei** und anschließend auf **Alles speichern**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-120">Click **File**, and then click **Save All**.</span></span>

1. <span data-ttu-id="f5c79-121">Schließen Sie alle geöffneten Editor-Fenster.</span><span class="sxs-lookup"><span data-stu-id="f5c79-121">Close all open editor windows.</span></span>

## <a name="write-code-that-sends-a-message-to-the-topic"></a><span data-ttu-id="f5c79-122">Schreiben von Code zum Senden einer Nachricht an das Thema</span><span class="sxs-lookup"><span data-stu-id="f5c79-122">Write code that sends a message to the topic</span></span>

<span data-ttu-id="f5c79-123">Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zur Vertriebsleistung gesendet werden:</span><span class="sxs-lookup"><span data-stu-id="f5c79-123">To complete the component that sends messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="f5c79-124">Klicken Sie in Visual Studio Code im Bereich **Explorer** im Ordner **performancemessagesender** auf die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-124">In Visual Studio Code, in the **Explorer** pane, in the **performancemessagesender** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="f5c79-125">Wechseln Sie zur `SendPerformanceMessageAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="f5c79-125">Locate the `SendPerformanceMessageAsync()` method.</span></span>

1. <span data-ttu-id="f5c79-126">Suchen Sie in dieser Methode nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="f5c79-126">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a Topic Client here
    ```

1. <span data-ttu-id="f5c79-127">Ersetzen Sie diese Codezeile durch den folgenden Code, um einen Themenclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="f5c79-127">To create a topic client, replace that line of code with the following code:</span></span>

    ```C#
    topicClient = new TopicClient(ServiceBusConnectionString, TopicName);
    ```

1. <span data-ttu-id="f5c79-128">Suchen Sie im `try...catch`-Block nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="f5c79-128">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="f5c79-129">Ersetzen Sie diese Codezeile durch den folgenden Code, um eine Nachricht für die Warteschlange zu erstellen und zu formatieren:</span><span class="sxs-lookup"><span data-stu-id="f5c79-129">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"Total sales for Brazil in August: $13m.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="f5c79-130">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht in der Konsole anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="f5c79-130">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="f5c79-131">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht an die Warteschlange zu senden:</span><span class="sxs-lookup"><span data-stu-id="f5c79-131">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await topicClient.SendAsync(message);
    ```

1. <span data-ttu-id="f5c79-132">Suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="f5c79-132">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the topic here
    ```

1. <span data-ttu-id="f5c79-133">Ersetzen Sie diese Codezeile durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:</span><span class="sxs-lookup"><span data-stu-id="f5c79-133">To close the connection to Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await topicClient.CloseAsync();
    ```

1. <span data-ttu-id="f5c79-134">Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.</span><span class="sxs-lookup"><span data-stu-id="f5c79-134">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="send-a-message-to-the-topic"></a><span data-ttu-id="f5c79-135">Senden einer Nachricht an das Thema</span><span class="sxs-lookup"><span data-stu-id="f5c79-135">Send a message to the topic</span></span>

<span data-ttu-id="f5c79-136">Führen Sie diese Schritte aus, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:</span><span class="sxs-lookup"><span data-stu-id="f5c79-136">To run the component that sends a message about a sale, follow these steps:</span></span>

1. <span data-ttu-id="f5c79-137">Klicken Sie in Visual Studio Code im Menü **Ansicht** auf **Debuggen**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-137">In Visual Studio Code, on the **View** menu, click **Debug**.</span></span>

1. <span data-ttu-id="f5c79-138">Wählen Sie im Bereich **Debuggen** in der Dropdownliste die Option **Launch Performance Message Sender** (Senden von Leistungsnachrichten starten) aus, und drücken Sie anschließend **F5**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-138">In the **Debug** pane, in the drop-down list, select **Launch Performance Message Sender**, and then press **F5**.</span></span> <span data-ttu-id="f5c79-139">Visual Studio Code führt das Erstellen und Ausführen der Konsolenanwendung im Debugmodus durch.</span><span class="sxs-lookup"><span data-stu-id="f5c79-139">Visual Studio Code builds and runs the console application in debugging mode.</span></span>

1. <span data-ttu-id="f5c79-140">Sehen Sie sich die Nachrichten in der **Debugging-Konsole** an, während das Programm ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f5c79-140">As the program executes, examine the messages in the **Debug Console**.</span></span>

1. <span data-ttu-id="f5c79-141">Wechseln Sie zum Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="f5c79-141">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="f5c79-142">Klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace, falls dieser nicht angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="f5c79-142">If the Service Bus namespace is not displayed, in the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="f5c79-143">Klicken Sie auf dem Blatt **Service Bus-Namespace** unter **ENTITÄTEN** auf **Themen** und dann auf das Thema **salesperformancemessages**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-143">In the **Service Bus Namespace** blade, under **ENTITIES**, click **Topics**, and then click the **salesperformancemessages** topic.</span></span> <span data-ttu-id="f5c79-144">In der Liste der Abonnements sollte sowohl im **Amerika**- als auch im **Europa**-Abonnement eine Nachricht angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="f5c79-144">In the list of subscriptions, there should be one message displayed in both the **Americas** and **Europe** subscriptions.</span></span>

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a><span data-ttu-id="f5c79-145">Schreiben von Code zum Empfangen einer Nachricht von einem Themenabonnement</span><span class="sxs-lookup"><span data-stu-id="f5c79-145">Write code that receives a message from a topic subscription</span></span>

<span data-ttu-id="f5c79-146">Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zur Vertriebsleistung empfangen werden:</span><span class="sxs-lookup"><span data-stu-id="f5c79-146">To complete the component that retrieves messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="f5c79-147">Klicken Sie in Visual Studio Code im Bereich **Explorer** im Ordner **performancemessagereceiver** auf die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-147">In Visual Studio Code, in the **Explorer** pane, in the **performancemessagereceiver** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="f5c79-148">Wechseln Sie zur `MainAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="f5c79-148">Locate the `MainAsync()` method.</span></span>

1. <span data-ttu-id="f5c79-149">Suchen Sie in dieser Methode nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="f5c79-149">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a subscription client here
    ```

1. <span data-ttu-id="f5c79-150">Ersetzen Sie diese Zeile durch den folgenden Code, um einen Abonnementclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="f5c79-150">To create a subscription client, replace that line with the following code:</span></span>

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);
    ```

1. <span data-ttu-id="f5c79-151">Suchen Sie nach der `RegisterMessageHandler()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="f5c79-151">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="f5c79-152">Ersetzen Sie sämtlichen Code innerhalb dieser Methode durch den folgenden Code, um Optionen für die Behandlung von Nachrichten zu konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="f5c79-152">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="f5c79-153">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um den Nachrichtenhandler zu registrieren:</span><span class="sxs-lookup"><span data-stu-id="f5c79-153">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="f5c79-154">Suchen Sie nach der `ProcessMessagesAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="f5c79-154">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="f5c79-155">Sie haben diese Methode als Methode registriert, mit der eingehende Nachrichten behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="f5c79-155">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="f5c79-156">Ersetzen Sie den gesamten Code dieser Methode durch den folgenden Code, um in der Konsole eingehende Nachrichten anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="f5c79-156">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="f5c79-157">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die empfangene Nachricht aus dem Abonnement zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="f5c79-157">To remove the received message from the subscription, on the next line, add the following code:</span></span>

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="f5c79-158">Wechseln Sie zurück zur `MainAsync()`-Methode, und suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="f5c79-158">Return to the `MainAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the subscription here
    ```

1. <span data-ttu-id="f5c79-159">Ersetzen Sie diesen Code durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:</span><span class="sxs-lookup"><span data-stu-id="f5c79-159">To close the connection to Service Bus, replace that code with the following code:</span></span>

    ```C#
    await subscriptionClient.CloseAsync();
    ```

1. <span data-ttu-id="f5c79-160">Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.</span><span class="sxs-lookup"><span data-stu-id="f5c79-160">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="retrieve-a-message-from-a-topic-subscription"></a><span data-ttu-id="f5c79-161">Abrufen einer Nachricht aus einem Themenabonnement</span><span class="sxs-lookup"><span data-stu-id="f5c79-161">Retrieve a message from a topic subscription</span></span>

<span data-ttu-id="f5c79-162">Führen Sie diese Schritte aus, um die Komponente auszuführen, mit der Nachrichten zur Vertriebsleistung empfangen werden:</span><span class="sxs-lookup"><span data-stu-id="f5c79-162">To run the component that retrieves a message about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="f5c79-163">Klicken Sie in Visual Studio Code im Menü **Ansicht** auf **Debuggen**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-163">In Visual Studio Code, on the **View** menu, click **Debug**.</span></span>

1. <span data-ttu-id="f5c79-164">Wählen Sie im Bereich **Debuggen** in der Dropdownliste die Option **Launch Performance Message Receiver** (Empfangen von Leistungsnachrichten starten) aus, und drücken Sie anschließend **F5**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-164">In the **Debug** pane, in the drop-down list, select **Launch Performance Message Receiver**, and then press **F5**.</span></span> <span data-ttu-id="f5c79-165">Visual Studio Code führt das Erstellen und Ausführen der Konsolenanwendung im Debugmodus durch.</span><span class="sxs-lookup"><span data-stu-id="f5c79-165">Visual Studio Code builds and runs the console application in debugging mode.</span></span>

1. <span data-ttu-id="f5c79-166">Sehen Sie sich die Nachrichten in der **Debugging-Konsole** an, während das Programm ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="f5c79-166">As the program executes, examine the messages in the **Debug Console**.</span></span>

1. <span data-ttu-id="f5c79-167">Klicken Sie im Menü **Debuggen** auf **Debugging beenden**, wenn Sie sehen, dass die Nachricht empfangen wurde und in der Konsole angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="f5c79-167">When you see that the message has been received and displayed in the console, on the **Debug** menu, click **Stop Debugging**.</span></span>

1. <span data-ttu-id="f5c79-168">Wechseln Sie zum Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="f5c79-168">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="f5c79-169">Klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace, falls dieser nicht angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="f5c79-169">If the Service Bus namespace is not displayed, in the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="f5c79-170">Klicken Sie auf dem Blatt **Service Bus-Namespace** unter **ENTITÄTEN** auf **Themen** und dann auf das Thema **salesperformancemessages**.</span><span class="sxs-lookup"><span data-stu-id="f5c79-170">In the **Service Bus Namespace** blade, under **ENTITIES**, click **Topics**, and then click the **salesperformancemessages** topic.</span></span> <span data-ttu-id="f5c79-171">In der Liste der Abonnements sollten im **Amerika**-Abonnement null Nachrichten angezeigt werden, da Ihre Anwendung die einzige Nachricht verarbeitet und entfernt hat.</span><span class="sxs-lookup"><span data-stu-id="f5c79-171">In the list of subscriptions, there should be zero messages displayed in the **Americas** subscription because your application has processed and removed the only message.</span></span> <span data-ttu-id="f5c79-172">Beachten Sie, dass die Nachricht im **Europa**-Abonnement noch vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="f5c79-172">Notice that the message is still present in the **Europe** subscription.</span></span>
