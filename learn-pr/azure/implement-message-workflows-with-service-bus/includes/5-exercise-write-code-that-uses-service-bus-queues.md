<span data-ttu-id="dd950-101">Sie haben sich für die Verwendung einer Service Bus-Warteschlange entschieden, um Nachrichten zu den einzelnen Verkäufen zwischen der mobilen App, die von Ihren Vertriebsmitarbeitern genutzt wird, und dem in Azure gehosteten Webdienst auszutauschen. Über den Webdienst werden Details zu den einzelnen Verkäufen in einer Azure SQL-Datenbank-Instanz gespeichert.</span><span class="sxs-lookup"><span data-stu-id="dd950-101">You've chosen to use a Service Bus queue to exchange messages about individual sales between the mobile app that your sales personnel use and the web service, hosted in Azure, that will store details about each sale in an Azure SQL Database instance.</span></span>

<span data-ttu-id="dd950-102">Sie haben die erforderlichen Objekte in Ihrem Azure-Abonnement implementiert.</span><span class="sxs-lookup"><span data-stu-id="dd950-102">You've already implemented the necessary objects in your Azure subscription.</span></span> <span data-ttu-id="dd950-103">Nun möchten Sie Code schreiben, mit dem Nachrichten an diese Warteschlange gesendet und daraus abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="dd950-103">Now, you want to write code that sends messages to that queue and retrieves messages.</span></span>

## <a name="clone-and-open-the-starter-application"></a><span data-ttu-id="dd950-104">Klonen und Öffnen der Startanwendung</span><span class="sxs-lookup"><span data-stu-id="dd950-104">Clone and open the starter application</span></span>

<span data-ttu-id="dd950-105">In dieser Einheit erstellen Sie zwei Konsolenanwendungen in **Visual Studio Code**.</span><span class="sxs-lookup"><span data-stu-id="dd950-105">In this unit, you'll build two console applications in **Visual Studio Code**.</span></span> <span data-ttu-id="dd950-106">Mit der ersten Anwendung werden Nachrichten in einer Service Bus-Warteschlange angeordnet, und mit der zweiten werden diese Nachrichten abgerufen.</span><span class="sxs-lookup"><span data-stu-id="dd950-106">The first application places messages into a Service Bus queue and the second retrieves them.</span></span> <span data-ttu-id="dd950-107">Die Anwendungen sind Teil einer einzelnen .NET Core-Lösung.</span><span class="sxs-lookup"><span data-stu-id="dd950-107">The applications are part of a single .NET Core solution.</span></span> 

<span data-ttu-id="dd950-108">Führen Sie zuerst das Klonen der Lösung durch:</span><span class="sxs-lookup"><span data-stu-id="dd950-108">Start by cloning the solution:</span></span>

1. <span data-ttu-id="dd950-109">Starten Sie eine Eingabeaufforderung, und wechseln Sie in das Verzeichnis, in dem Sie den Quellcode für die Anwendung hosten möchten.</span><span class="sxs-lookup"><span data-stu-id="dd950-109">Start a command prompt and change to the directory where you want to host the source code for the application.</span></span>

1. <span data-ttu-id="dd950-110">Geben Sie den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="dd950-110">Type the following command, and then press **Enter**:</span></span>

    ```powershell
    git clone https:\\ <!-- TODO: (add git URL) -->
    ```

1. <span data-ttu-id="dd950-111">Nachdem der Klonvorgang abgeschlossen ist, können Sie in den Startordner wechseln.</span><span class="sxs-lookup"><span data-stu-id="dd950-111">When the clone operation is complete, change to the starter folder.</span></span>

1. <span data-ttu-id="dd950-112">Geben Sie den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:</span><span class="sxs-lookup"><span data-stu-id="dd950-112">Type the following command, and then press **Enter**.</span></span>

    ```powershell
    code .
    ```

1. <span data-ttu-id="dd950-113">Klicken Sie auf **Ja**, wenn eine Meldung mit der Abfrage zur Wiederherstellung von Abhängigkeiten angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="dd950-113">If a message appears asking if you want to restore dependencies, click **Yes**.</span></span>

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="dd950-114">Konfigurieren einer Verbindungszeichenfolge für einen Service Bus-Namespace</span><span class="sxs-lookup"><span data-stu-id="dd950-114">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="dd950-115">Sie müssen in Ihren Konsolen-Apps zwei Informationselemente konfigurieren, um auf einen Service Bus-Namespace zuzugreifen und eine Warteschlange zu verwenden:</span><span class="sxs-lookup"><span data-stu-id="dd950-115">In order to access a Service Bus namespace and use a queue, you must configure two pieces of information in your console apps:</span></span>

* <span data-ttu-id="dd950-116">Endpunkt für Ihren Namespace</span><span class="sxs-lookup"><span data-stu-id="dd950-116">The endpoint for your namespace</span></span>
* <span data-ttu-id="dd950-117">Freigegebener Zugriffsschlüssel für die Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="dd950-117">The shared access key for authentication</span></span>

<span data-ttu-id="dd950-118">Beide Werte können im Azure-Portal in Form einer vollständigen Verbindungszeichenfolge abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="dd950-118">Both of these values can be obtained from the Azure portal in the form of a complete connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="dd950-119">Der Einfachheit halber führen Sie für die Verbindungszeichenfolge in der Datei **Program.cs** beider Konsolenanwendungen das Hartcodieren durch.</span><span class="sxs-lookup"><span data-stu-id="dd950-119">For simplicity, you will hard-code the connection string in the **Program.cs** file of both console applications.</span></span> <span data-ttu-id="dd950-120">In einer Produktionsanwendung können Sie eine Konfigurationsdatei oder auch Azure Key Vault nutzen, um die Verbindungszeichenfolge zu speichern.</span><span class="sxs-lookup"><span data-stu-id="dd950-120">In a production application, you might use a configuration file or even Azure Key Vault to store the connection string.</span></span>

1. <span data-ttu-id="dd950-121">Wechseln Sie zum Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="dd950-121">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="dd950-122">Klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="dd950-122">In the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="dd950-123">Klicken Sie unter **EINSTELLUNGEN** auf **Freigegebene Zugriffsrichtlinien**.</span><span class="sxs-lookup"><span data-stu-id="dd950-123">Under **SETTINGS**, click **Shared Access Policies**.</span></span>

1. <span data-ttu-id="dd950-124">Klicken Sie in der Liste mit den Richtlinien auf **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="dd950-124">In the list of policies, click **RootManageSharedAccessKey**.</span></span>

1. <span data-ttu-id="dd950-125">Klicken Sie rechts vom Textfeld **Primäre Verbindungszeichenfolge** auf die Schaltfläche **Click to copy** \(Zum Kopieren klicken).</span><span class="sxs-lookup"><span data-stu-id="dd950-125">To the right of the **Primary Connection string** text box, click the **Click to copy** button.</span></span>

1. <span data-ttu-id="dd950-126">Wechseln Sie zu **Visual Studio Code**.</span><span class="sxs-lookup"><span data-stu-id="dd950-126">Switch to **Visual Studio Code**.</span></span>

1. <span data-ttu-id="dd950-127">Klicken Sie im Bereich **Explorer** im Ordner **privatemessagesender** auf die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="dd950-127">In the **Explorer** pane, in the **privatemessagesender** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="dd950-128">Suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="dd950-128">Locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. <span data-ttu-id="dd950-129">Platzieren Sie den Cursor zwischen den Anführungszeichen, und drücken Sie dann **STRG+V**.</span><span class="sxs-lookup"><span data-stu-id="dd950-129">Place the cursor between the quotation marks, and then press **Ctrl+V**.</span></span>

1. <span data-ttu-id="dd950-130">Klicken Sie im Bereich **Explorer** im Ordner **privatemessagereceiver** auf die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="dd950-130">In the **Explorer** pane, in the **privatemessagereceiver** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="dd950-131">Suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="dd950-131">Locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. <span data-ttu-id="dd950-132">Platzieren Sie den Cursor zwischen den Anführungszeichen, und drücken Sie dann **STRG+V**.</span><span class="sxs-lookup"><span data-stu-id="dd950-132">Place the cursor between the quotation marks, and then press **Ctrl+V**.</span></span>

1. <span data-ttu-id="dd950-133">Klicken Sie auf **Datei** und anschließend auf **Alles speichern**.</span><span class="sxs-lookup"><span data-stu-id="dd950-133">Click **File**, and then click **Save All**.</span></span>

1. <span data-ttu-id="dd950-134">Schließen Sie alle geöffneten Editor-Fenster.</span><span class="sxs-lookup"><span data-stu-id="dd950-134">Close all open editor windows.</span></span>

## <a name="write-code-that-sends-a-message-to-the-queue"></a><span data-ttu-id="dd950-135">Schreiben von Code zum Senden einer Nachricht an die Warteschlange</span><span class="sxs-lookup"><span data-stu-id="dd950-135">Write code that sends a message to the queue</span></span>

<span data-ttu-id="dd950-136">Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zu Verkäufen gesendet werden:</span><span class="sxs-lookup"><span data-stu-id="dd950-136">To complete the component that sends messages about sales, follow these steps:</span></span>

1. <span data-ttu-id="dd950-137">Klicken Sie in Visual Studio Code im Bereich **Explorer** im Ordner **privatemessagesender** auf die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="dd950-137">In Visual Studio Code, in the **Explorer** pane, in the **privatemessagesender** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="dd950-138">Suchen Sie nach der `SendSalesMessageAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="dd950-138">Locate the `SendSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="dd950-139">Suchen Sie in dieser Methode nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="dd950-139">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a queue client here
    ```

1. <span data-ttu-id="dd950-140">Ersetzen Sie diese Codezeile durch den folgenden Code, um einen Warteschlangenclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="dd950-140">To create a queue client, replace that line of code with the following code:</span></span>

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="dd950-141">Suchen Sie im `try...catch`-Block nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="dd950-141">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="dd950-142">Ersetzen Sie diese Codezeile durch den folgenden Code, um eine Nachricht für die Warteschlange zu erstellen und zu formatieren:</span><span class="sxs-lookup"><span data-stu-id="dd950-142">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"$10,000 order for bicycle parts from retailer Adventure Works.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="dd950-143">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht in der Konsole anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="dd950-143">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="dd950-144">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht an die Warteschlange zu senden:</span><span class="sxs-lookup"><span data-stu-id="dd950-144">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.SendAsync(message);
    ```

1. <span data-ttu-id="dd950-145">Suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="dd950-145">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the queue here
    ```

1. <span data-ttu-id="dd950-146">Ersetzen Sie diese Codezeile durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:</span><span class="sxs-lookup"><span data-stu-id="dd950-146">To close the connection the Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="dd950-147">Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.</span><span class="sxs-lookup"><span data-stu-id="dd950-147">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="send-a-message-to-the-queue"></a><span data-ttu-id="dd950-148">Senden einer Nachricht an die Warteschlange</span><span class="sxs-lookup"><span data-stu-id="dd950-148">Send a message to the queue</span></span>

<span data-ttu-id="dd950-149">Verwenden Sie diese Schritte, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:</span><span class="sxs-lookup"><span data-stu-id="dd950-149">To run the component that sends a message about a sale, follow these steps:</span></span>

1. <span data-ttu-id="dd950-150">Klicken Sie in Visual Studio Code im Menü **Ansicht** auf **Debuggen**.</span><span class="sxs-lookup"><span data-stu-id="dd950-150">In Visual Studio Code, on the **View** menu, click **Debug**.</span></span>

1. <span data-ttu-id="dd950-151">Wählen Sie im Bereich **Debuggen** in der Dropdownliste die Option **Senden privater Nachrichten starten**, und drücken Sie anschließend **F5**.</span><span class="sxs-lookup"><span data-stu-id="dd950-151">In the **Debug** pane, in the drop-down list, select **Launch Private Message Sender**, and then press **F5**.</span></span> <span data-ttu-id="dd950-152">Visual Studio Code führt das Erstellen und Ausführen der Konsolenanwendung im Debugmodus durch.</span><span class="sxs-lookup"><span data-stu-id="dd950-152">Visual Studio Code builds and runs the console application in debugging mode.</span></span>

1. <span data-ttu-id="dd950-153">Sehen Sie sich die Nachrichten in der **Debugging-Konsole** an, während das Programm ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="dd950-153">As the program executes, examine the messages in the **Debug Console**.</span></span>

1. <span data-ttu-id="dd950-154">Wechseln Sie zum Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="dd950-154">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="dd950-155">Falls der Service Bus-Namespace nicht angezeigt wird, klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="dd950-155">If the Service Bus namespace is not displayed, in the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="dd950-156">Klicken Sie auf dem Blatt **Service Bus-Namespace** unter **ENTITÄTEN** auf **Warteschlangen** und dann auf die Warteschlange **salesmessages**.</span><span class="sxs-lookup"><span data-stu-id="dd950-156">In the **Service Bus Namespace** blade, under **ENTITIES**, click **Queues**, and then click the **salesmessages** queue.</span></span> <span data-ttu-id="dd950-157">Unter **ANZAHL AKTIVER NACHRICHTEN** sollte angezeigt werden, dass der Warteschlange eine Nachricht hinzugefügt wurde.</span><span class="sxs-lookup"><span data-stu-id="dd950-157">The **ACTIVE MESSAGE COUNT** should indicate that one message has been added to the queue.</span></span>

## <a name="write-code-that-receives-a-message-from-the-queue"></a><span data-ttu-id="dd950-158">Schreiben von Code für den Empfang einer Nachricht von der Warteschlange</span><span class="sxs-lookup"><span data-stu-id="dd950-158">Write code that receives a message from the queue</span></span>

<span data-ttu-id="dd950-159">Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zu Verkäufen abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="dd950-159">To complete the component that retrieves messages about sales, follow these steps:</span></span>

1. <span data-ttu-id="dd950-160">Klicken Sie in Visual Studio Code im Bereich **Explorer** im Ordner **privatemessagereceiver** auf die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="dd950-160">In Visual Studio Code, in the **Explorer** pane, in the **privatemessagereceiver** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="dd950-161">Suchen Sie nach der `ReceiveSalesMessageAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="dd950-161">Locate the `ReceiveSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="dd950-162">Suchen Sie in dieser Methode nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="dd950-162">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a queue client here
    ```

1. <span data-ttu-id="dd950-163">Ersetzen Sie diese Zeile durch den folgenden Code, um einen Warteschlangenclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="dd950-163">To create a queue client, replace that line with the following code:</span></span>

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="dd950-164">Suchen Sie nach der `RegisterMessageHandler()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="dd950-164">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="dd950-165">Ersetzen Sie sämtlichen Code innerhalb dieser Methode durch den folgenden Code, um Optionen für die Behandlung von Nachrichten zu konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="dd950-165">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="dd950-166">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um den Nachrichtenhandler zu registrieren:</span><span class="sxs-lookup"><span data-stu-id="dd950-166">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="dd950-167">Suchen Sie nach der `ProcessMessagesAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="dd950-167">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="dd950-168">Sie haben diese Methode als Methode registriert, mit der eingehende Nachrichten behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="dd950-168">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="dd950-169">Ersetzen Sie den gesamten Code dieser Methode durch den folgenden Code, um in der Konsole eingehende Nachrichten anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="dd950-169">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="dd950-170">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die empfangene Nachricht aus der Warteschlange zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="dd950-170">To remove the received message from the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="dd950-171">Wechseln Sie zurück zur `ReceiveSalesMessageAsync()`-Methode, und suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="dd950-171">Return to the `ReceiveSalesMessageAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the queue here
    ```

1. <span data-ttu-id="dd950-172">Ersetzen Sie diese Zeile durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:</span><span class="sxs-lookup"><span data-stu-id="dd950-172">To close the connection to Service Bus, replace that line with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="dd950-173">Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.</span><span class="sxs-lookup"><span data-stu-id="dd950-173">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="retrieve-a-message-from-the-queue"></a><span data-ttu-id="dd950-174">Abrufen einer Nachricht aus der Warteschlange</span><span class="sxs-lookup"><span data-stu-id="dd950-174">Retrieve a message from the queue</span></span>

<span data-ttu-id="dd950-175">Verwenden Sie diese Schritte, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf empfangen wird:</span><span class="sxs-lookup"><span data-stu-id="dd950-175">To run the component that retrieves a message about a sale, follow these steps:</span></span>

1. <span data-ttu-id="dd950-176">Klicken Sie in Visual Studio Code im Menü **Ansicht** auf **Debuggen**.</span><span class="sxs-lookup"><span data-stu-id="dd950-176">In Visual Studio Code, on the **View** menu, click **Debug**.</span></span>

1. <span data-ttu-id="dd950-177">Wählen Sie im Bereich **Debuggen** in der Dropdownliste die Option **Empfangen privater Nachrichten starten**, und drücken Sie anschließend **F5**.</span><span class="sxs-lookup"><span data-stu-id="dd950-177">In the **Debug** pane, in the drop-down list, select **Launch Private Message Receiver**, and then press **F5**.</span></span> <span data-ttu-id="dd950-178">Visual Studio Code führt das Erstellen und Ausführen der Konsolenanwendung im Debugmodus durch.</span><span class="sxs-lookup"><span data-stu-id="dd950-178">Visual Studio Code builds and runs the console application in debugging mode.</span></span>

1. <span data-ttu-id="dd950-179">Sehen Sie sich die Nachrichten in der **Debugging-Konsole** an, während das Programm ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="dd950-179">As the program executes, examine the messages in the **Debug Console**.</span></span>

1. <span data-ttu-id="dd950-180">Klicken Sie im Menü **Debuggen** auf **Debugging beenden**, wenn Sie sehen, dass die Nachricht empfangen wurde und in der Konsole angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="dd950-180">When you see that the message has been received and displayed in the console, on the **Debug** menu, click **Stop Debugging**.</span></span>

1. <span data-ttu-id="dd950-181">Wechseln Sie zum Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="dd950-181">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="dd950-182">Falls der Service Bus-Namespace nicht angezeigt wird, klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="dd950-182">If the Service Bus namespace is not displayed, in the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="dd950-183">Klicken Sie auf dem Blatt **Service Bus-Namespace** unter **ENTITÄTEN** auf **Warteschlangen** und dann auf die Warteschlange **salesmessages**.</span><span class="sxs-lookup"><span data-stu-id="dd950-183">In the **Service Bus Namespace** blade, under **ENTITIES**, click **Queues**, and then click the **salesmessages** queue.</span></span> <span data-ttu-id="dd950-184">Unter **ANZAHL AKTIVER NACHRICHTEN** sollte angezeigt werden, dass die Nachricht aus der Warteschlange entfernt wurde.</span><span class="sxs-lookup"><span data-stu-id="dd950-184">The **ACTIVE MESSAGE COUNT** should indicate that the message has been removed from the queue.</span></span>

<span data-ttu-id="dd950-185">Sie haben Code geschrieben, mit dem eine Nachricht zu einem einzelnen Verkauf an eine Service Bus-Warteschlange gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="dd950-185">You have written code that sends a message about individual sales to a Service Bus queue.</span></span> <span data-ttu-id="dd950-186">In der verteilten Vertriebsanwendung sollten Sie diesen Code in der mobilen App schreiben, die von den Vertriebsmitarbeitern auf den Geräten genutzt wird.</span><span class="sxs-lookup"><span data-stu-id="dd950-186">In the sales force distributed application, you should write this code in the mobile app that sales personnel use on devices.</span></span>

<span data-ttu-id="dd950-187">Sie haben auch Code geschrieben, mit dem eine Nachricht von der Service Bus-Warteschlange empfangen wird.</span><span class="sxs-lookup"><span data-stu-id="dd950-187">You have also written code that receives a message from the Service Bus queue.</span></span> <span data-ttu-id="dd950-188">In der verteilten Vertriebsanwendung sollten Sie diesen Code in dem Webdienst schreiben, der in Azure ausgeführt wird und mit dem empfangene Nachrichten verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="dd950-188">In the sales force distributed application, you should write this code in the web service that runs in Azure and processes received messages.</span></span>
