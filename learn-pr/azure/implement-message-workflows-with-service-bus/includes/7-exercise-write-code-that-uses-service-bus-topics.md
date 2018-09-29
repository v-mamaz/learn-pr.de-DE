<span data-ttu-id="6422f-101">Wir haben uns entschieden, ein Azure Service Bus-Thema zu verwenden, um Nachrichten über die Vertriebsleistung in Ihrer verteilten Sales Force-Anwendung zu verteilen.</span><span class="sxs-lookup"><span data-stu-id="6422f-101">You have chosen to use an Azure Service Bus topic to distribute messages about sales performance in your sales force distributed application.</span></span> <span data-ttu-id="6422f-102">Die von Vertriebsmitarbeitern auf ihren mobilen Geräten verwendete App sendet Nachrichten mit zusammengefassten Umsatzzahlen für die einzelnen Gebiete und Zeiträume.</span><span class="sxs-lookup"><span data-stu-id="6422f-102">The app used by sales personnel on their mobile devices will send messages that summarize sales figures for each area and time period.</span></span> <span data-ttu-id="6422f-103">Diese Nachrichten werden an Webdienste verteilt, die sich in den Geschäftsregionen des Unternehmens befinden, einschließlich Amerika und Europa.</span><span class="sxs-lookup"><span data-stu-id="6422f-103">Those messages will be distributed to web services located in the company's operational regions, including the Americas and Europe.</span></span>

<span data-ttu-id="6422f-104">Sie haben in Ihrem Azure-Abonnement bereits die erforderliche Infrastruktur, darunter auch das Thema und die Abonnements, implementiert.</span><span class="sxs-lookup"><span data-stu-id="6422f-104">You have already implemented the necessary infrastructure in your Azure subscription, including the topic and subscriptions.</span></span> <span data-ttu-id="6422f-105">Jetzt möchten Sie den Code schreiben, der Nachrichten an das Thema sendet und Nachrichten eines Abonnements abruft.</span><span class="sxs-lookup"><span data-stu-id="6422f-105">Now, you want to write the code that sends messages to the topic and retrieves messages from a subscription.</span></span>

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="6422f-106">Konfigurieren einer Verbindungszeichenfolge für einen Service Bus-Namespace</span><span class="sxs-lookup"><span data-stu-id="6422f-106">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="6422f-107">Konfigurieren Sie zunächst Verbindungszeichenfolgen in der sendenden und empfangenden Komponente:</span><span class="sxs-lookup"><span data-stu-id="6422f-107">Start by configuring connection strings both in the sending and receiving components:</span></span>

1. <span data-ttu-id="6422f-108">Öffnen Sie **performancemessagesender/Program.cs** im Editor, und suchen Sie die folgende Codezeile:</span><span class="sxs-lookup"><span data-stu-id="6422f-108">In the editor, open **performancemessagesender/Program.cs** and locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    <span data-ttu-id="6422f-109">Fügen Sie die Verbindungszeichenfolge zwischen den Anführungszeichen ein, und speichern Sie die Datei entweder über das Menü „...“ oder über die entsprechende Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux, <kbd>cmd+S</kbd> unter macOS).</span><span class="sxs-lookup"><span data-stu-id="6422f-109">Paste the connection string between the quotation marks and save the file either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="6422f-110">Wiederholen Sie den vorherigen Schritt in **performancemessagereceiver/Program.cs**. Fügen Sie dabei den gleichen Verbindungszeichenfolgenwert ein, und speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="6422f-110">Repeat the previous step in **performancemessagereceiver/Program.cs**, pasting in the same connection string value and save the file.</span></span>

## <a name="write-code-that-sends-a-message-to-the-topic"></a><span data-ttu-id="6422f-111">Schreiben von Code zum Senden einer Nachricht an das Thema</span><span class="sxs-lookup"><span data-stu-id="6422f-111">Write code that sends a message to the topic</span></span>

<span data-ttu-id="6422f-112">Führen Sie die folgenden Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zur Vertriebsleistung gesendet werden:</span><span class="sxs-lookup"><span data-stu-id="6422f-112">To complete the component that sends messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="6422f-113">Öffnen Sie **performancemessagesender/Program.cs** im Editor.</span><span class="sxs-lookup"><span data-stu-id="6422f-113">Open **performancemessagesender/Program.cs** in the editor.</span></span>

1. <span data-ttu-id="6422f-114">Suchen Sie nach der `SendPerformanceMessageAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="6422f-114">Locate the `SendPerformanceMessageAsync()` method.</span></span>

1. <span data-ttu-id="6422f-115">Suchen Sie in dieser Methode nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="6422f-115">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a Topic Client here
    ```

1. <span data-ttu-id="6422f-116">Ersetzen Sie diese Codezeile durch den folgenden Code, um einen Themenclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="6422f-116">To create a topic client, replace that line of code with the following code:</span></span>

    ```C#
    topicClient = new TopicClient(ServiceBusConnectionString, TopicName);
    ```

1. <span data-ttu-id="6422f-117">Suchen Sie im `try...catch`-Block nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="6422f-117">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="6422f-118">Ersetzen Sie diese Codezeile durch den folgenden Code, um eine Nachricht für die Warteschlange zu erstellen und zu formatieren:</span><span class="sxs-lookup"><span data-stu-id="6422f-118">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"Total sales for Brazil in August: $13m.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="6422f-119">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht in der Konsole anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="6422f-119">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="6422f-120">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht an die Warteschlange zu senden:</span><span class="sxs-lookup"><span data-stu-id="6422f-120">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await topicClient.SendAsync(message);
    ```

1. <span data-ttu-id="6422f-121">Suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="6422f-121">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the topic here
    ```

1. <span data-ttu-id="6422f-122">Ersetzen Sie diese Codezeile durch den folgenden Code, um die Verbindung mit Service Bus zu beenden:</span><span class="sxs-lookup"><span data-stu-id="6422f-122">To close the connection to Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await topicClient.CloseAsync();
    ```

1. <span data-ttu-id="6422f-123">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="6422f-123">Save the file.</span></span>

## <a name="send-a-message-to-the-topic"></a><span data-ttu-id="6422f-124">Senden einer Nachricht an das Thema</span><span class="sxs-lookup"><span data-stu-id="6422f-124">Send a message to the topic</span></span>

<span data-ttu-id="6422f-125">Führen Sie den folgenden Befehl in Cloud Shell aus, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:</span><span class="sxs-lookup"><span data-stu-id="6422f-125">To run the component that sends a message about a sale, run this command in the Cloud Shell:</span></span>

```bash
dotnet run -p performancemessagesender
```

<span data-ttu-id="6422f-126">Während das Programm ausgeführt wird, werden Nachrichten ausgegeben, die darauf hinweisen, dass die Komponente eine Nachricht sendet.</span><span class="sxs-lookup"><span data-stu-id="6422f-126">As the program executes, you'll see messages printed indicating that it's sending a message.</span></span> <span data-ttu-id="6422f-127">Bei jedem Ausführen der App wird dem Thema eine zusätzliche Nachricht hinzugefügt, und jeder Abonnent erhält eine Kopie.</span><span class="sxs-lookup"><span data-stu-id="6422f-127">Each time you run the app, one additional message will be added to the topic, and each subscriber will receive a copy.</span></span>

<span data-ttu-id="6422f-128">Führen Sie nach Abschluss der Ausführung den folgenden Befehl aus, um sich die Anzahl der Nachrichten im Abonnement „Amerika“ anzeigen zu lassen:</span><span class="sxs-lookup"><span data-stu-id="6422f-128">Once it's finished, run the following command to see how many messages are in the Americas subscription:</span></span>

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

<span data-ttu-id="6422f-129">Wenn Sie `EuropeAndAfrica` durch `Americas` ersetzen, sollte für beide Abonnements die gleiche Anzahl von Nachrichten angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="6422f-129">If you substitute `EuropeAndAfrica` for `Americas`, you should see that both subscriptions have the same number of messages.</span></span>

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a><span data-ttu-id="6422f-130">Schreiben von Code zum Empfangen einer Nachricht von einem Themenabonnement</span><span class="sxs-lookup"><span data-stu-id="6422f-130">Write code that receives a message from a topic subscription</span></span>

<span data-ttu-id="6422f-131">Führen Sie die folgenden Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zur Vertriebsleistung abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="6422f-131">To complete the component that retrieves messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="6422f-132">Öffnen Sie **performancemessagereceiver/Program.cs** im Editor.</span><span class="sxs-lookup"><span data-stu-id="6422f-132">Open **performancemessagereceiver/Program.cs** in the editor.</span></span>

1. <span data-ttu-id="6422f-133">Suchen Sie nach der `MainAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="6422f-133">Locate the `MainAsync()` method.</span></span>

1. <span data-ttu-id="6422f-134">Suchen Sie in dieser Methode nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="6422f-134">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a subscription client here
    ```

1. <span data-ttu-id="6422f-135">Ersetzen Sie diese Zeile durch den folgenden Code, um einen Abonnementclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="6422f-135">To create a subscription client, replace that line with the following code:</span></span>

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);
    ```

1. <span data-ttu-id="6422f-136">Suchen Sie nach der `RegisterMessageHandler()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="6422f-136">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="6422f-137">Ersetzen Sie sämtlichen Code innerhalb dieser Methode durch den folgenden Code, um Optionen für die Behandlung von Nachrichten zu konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="6422f-137">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="6422f-138">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um den Nachrichtenhandler zu registrieren:</span><span class="sxs-lookup"><span data-stu-id="6422f-138">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="6422f-139">Suchen Sie nach der `ProcessMessagesAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="6422f-139">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="6422f-140">Sie haben diese Methode als Methode registriert, mit der eingehende Nachrichten behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="6422f-140">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="6422f-141">Ersetzen Sie den gesamten Code dieser Methode durch den folgenden Code, um in der Konsole eingehende Nachrichten anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="6422f-141">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="6422f-142">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die empfangene Nachricht aus dem Abonnement zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="6422f-142">To remove the received message from the subscription, on the next line, add the following code:</span></span>

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="6422f-143">Wechseln Sie zurück zur `MainAsync()`-Methode, und suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="6422f-143">Return to the `MainAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the subscription here
    ```

1. <span data-ttu-id="6422f-144">Ersetzen Sie diesen Code durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:</span><span class="sxs-lookup"><span data-stu-id="6422f-144">To close the connection to Service Bus, replace that code with the following code:</span></span>

    ```C#
    await subscriptionClient.CloseAsync();
    ```

1. <span data-ttu-id="6422f-145">Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.</span><span class="sxs-lookup"><span data-stu-id="6422f-145">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="retrieve-a-message-from-a-topic-subscription"></a><span data-ttu-id="6422f-146">Abrufen einer Nachricht aus einem Themenabonnement</span><span class="sxs-lookup"><span data-stu-id="6422f-146">Retrieve a message from a topic subscription</span></span>

<span data-ttu-id="6422f-147">Führen Sie die folgenden Schritte aus, um die Komponente auszuführen, mit der Nachrichten zur Vertriebsleistung abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="6422f-147">To run the component that retrieves a message about sales performance, follow these steps:</span></span>

```bash
dotnet run -p performancemessagereceiver
```

<span data-ttu-id="6422f-148">Wenn das Programm keine Nachrichten mehr ausgibt, in denen darauf hingewiesen wird, dass Nachrichten empfangen werden,</span><span class="sxs-lookup"><span data-stu-id="6422f-148">When the program stops printing notifications that it is receiving messages.</span></span> <span data-ttu-id="6422f-149">drücken Sie `Enter`, um die App zu beenden.</span><span class="sxs-lookup"><span data-stu-id="6422f-149">press `Enter` to stop the app.</span></span> <span data-ttu-id="6422f-150">Führen Sie anschließend den gleichen Befehl wie zuvor aus, um sicherzustellen, dass im `Americas`-Abonnement keine Nachrichten mehr vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="6422f-150">Then, run the same command as before to confirm that there are zero remaining messages in the `Americas` subscription.</span></span>

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

<span data-ttu-id="6422f-151">Wenn Sie `EuropeAndAfrica` durch `Americas` ersetzen, sehen Sie, dass sich die Anzahl der Nachrichten nicht geändert hat.</span><span class="sxs-lookup"><span data-stu-id="6422f-151">If you substitute `EuropeAndAfrica` for `Americas`, you'll see that the message count has not changed.</span></span> <span data-ttu-id="6422f-152">Die Anwendung hat nur Nachrichten vom `Americas`-Abonnement empfangen.</span><span class="sxs-lookup"><span data-stu-id="6422f-152">The application only received messages from the `Americas` subscription.</span></span>
