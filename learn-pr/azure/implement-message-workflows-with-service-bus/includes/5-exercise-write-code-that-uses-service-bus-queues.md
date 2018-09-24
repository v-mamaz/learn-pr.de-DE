<span data-ttu-id="e6974-101">Sie haben sich für die Verwendung einer Service Bus-Warteschlange entschieden, um Nachrichten zu den einzelnen Verkäufen zwischen der mobilen App, die von Ihren Vertriebsmitarbeitern genutzt wird, und dem in Azure gehosteten Webdienst auszutauschen. Über den Webdienst werden Details zu den einzelnen Verkäufen in einer Azure SQL-Datenbank-Instanz gespeichert.</span><span class="sxs-lookup"><span data-stu-id="e6974-101">You've chosen to use a Service Bus queue to exchange messages about individual sales between the mobile app that your sales personnel use and the web service, hosted in Azure, that will store details about each sale in an Azure SQL Database instance.</span></span>

<span data-ttu-id="e6974-102">Sie haben die erforderlichen Objekte in Ihrem Azure-Abonnement implementiert.</span><span class="sxs-lookup"><span data-stu-id="e6974-102">You've already implemented the necessary objects in your Azure subscription.</span></span> <span data-ttu-id="e6974-103">Nun möchten Sie Code schreiben, mit dem Nachrichten an diese Warteschlange gesendet und daraus abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="e6974-103">Now, you want to write code that sends messages to that queue and retrieves messages.</span></span>

## <a name="clone-and-open-the-starter-application"></a><span data-ttu-id="e6974-104">Klonen und Öffnen der Startanwendung</span><span class="sxs-lookup"><span data-stu-id="e6974-104">Clone and open the starter application</span></span>

<span data-ttu-id="e6974-105">In dieser Einheit erstellen Sie zwei Konsolenanwendungen.</span><span class="sxs-lookup"><span data-stu-id="e6974-105">In this unit, you'll build two console applications.</span></span> <span data-ttu-id="e6974-106">Mit der ersten Anwendung werden Nachrichten in einer Service Bus-Warteschlange angeordnet, und mit der zweiten werden diese Nachrichten abgerufen.</span><span class="sxs-lookup"><span data-stu-id="e6974-106">The first application places messages into a Service Bus queue and the second retrieves them.</span></span> <span data-ttu-id="e6974-107">Die Anwendungen sind Teil einer einzelnen .NET Core-Lösung.</span><span class="sxs-lookup"><span data-stu-id="e6974-107">The applications are part of a single .NET Core solution.</span></span>

1. <span data-ttu-id="e6974-108">Beginnen Sie, indem Sie die Lösung klonen: Führen Sie die folgenden Befehle in Cloud Shell aus:</span><span class="sxs-lookup"><span data-stu-id="e6974-108">Start by cloning the solution: run the following commands in the Cloud Shell:</span></span>

```bash
cd ~
git clone https://github.com/MicrosoftDocs/mslearn-connect-services-together.git
```

2. <span data-ttu-id="e6974-109">Wechseln Sie als Nächstes in den Startordner, und öffnen Sie den Cloud Shell-Editor.</span><span class="sxs-lookup"><span data-stu-id="e6974-109">Next, change directories into the starter folder and open the Cloud Shell editor.</span></span>

```bash
cd mslearn-connect-services-together/implement-message-workflows-with-service-bus/src/start
code .
```

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="e6974-110">Konfigurieren einer Verbindungszeichenfolge für einen Service Bus-Namespace</span><span class="sxs-lookup"><span data-stu-id="e6974-110">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="e6974-111">Sie müssen in Ihren Konsolen-Apps zwei Informationselemente konfigurieren, um auf einen Service Bus-Namespace zuzugreifen und eine Warteschlange zu verwenden:</span><span class="sxs-lookup"><span data-stu-id="e6974-111">In order to access a Service Bus namespace and use a queue, you must configure two pieces of information in your console apps:</span></span>

* <span data-ttu-id="e6974-112">Endpunkt für Ihren Namespace</span><span class="sxs-lookup"><span data-stu-id="e6974-112">The endpoint for your namespace</span></span>
* <span data-ttu-id="e6974-113">Freigegebener Zugriffsschlüssel für die Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="e6974-113">The shared access key for authentication</span></span>

<span data-ttu-id="e6974-114">Beide Werte können im Azure-Portal in Form einer vollständigen Verbindungszeichenfolge abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="e6974-114">Both of these values can be obtained from the Azure portal in the form of a complete connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="e6974-115">Der Einfachheit halber führen Sie für die Verbindungszeichenfolge in der Datei **Program.cs** beider Konsolenanwendungen das Hartcodieren durch.</span><span class="sxs-lookup"><span data-stu-id="e6974-115">For simplicity, you will hard-code the connection string in the **Program.cs** file of both console applications.</span></span> <span data-ttu-id="e6974-116">In einer Produktionsanwendung können Sie eine Konfigurationsdatei oder auch Azure Key Vault nutzen, um die Verbindungszeichenfolge zu speichern.</span><span class="sxs-lookup"><span data-stu-id="e6974-116">In a production application, you might use a configuration file or even Azure Key Vault to store the connection string.</span></span>

1. <span data-ttu-id="e6974-117">Führen Sie in Cloud Shell den folgenden Befehl aus, um die primäre Verbindungszeichenfolge für Ihren Service Bus-Namespace anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="e6974-117">In the Cloud Shell, run the following command to display the primary connection string for your Service Bus namespace.</span></span> <span data-ttu-id="e6974-118">Ersetzen Sie `<namespace-name>` durch den Namen Ihres Service Bus-Namespace.</span><span class="sxs-lookup"><span data-stu-id="e6974-118">Replace `<namespace-name>` with the name of your Service Bus namespace.</span></span>

    ```azurecli
    az servicebus namespace authorization-rule keys list \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --namespace-name <namespace-name> \
        --name RootManageSharedAccessKey \
        --query primaryConnectionString \
        --output tsv
    ```

    <span data-ttu-id="e6974-119">Da Sie diese Verbindungszeichenfolge in diesem Modul mehrfach benötigen, sollten Sie sie schnell zugänglich aufbewahren.</span><span class="sxs-lookup"><span data-stu-id="e6974-119">You'll be needing this connection string multiple times throughout this module, so you might want to paste it somewhere handy.</span></span>

1. <span data-ttu-id="e6974-120">Kopieren Sie den Schlüssel aus Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e6974-120">Copy the key from Cloud Shell.</span></span> <span data-ttu-id="e6974-121">Öffnen Sie im Editor **performancemessagesender/Program.cs**, und suchen Sie die folgende Codezeile:</span><span class="sxs-lookup"><span data-stu-id="e6974-121">In the editor, open **privatemessagesender/Program.cs** and locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    <span data-ttu-id="e6974-122">Fügen Sie die Verbindungszeichenfolge zwischen den Anführungszeichen ein.</span><span class="sxs-lookup"><span data-stu-id="e6974-122">Paste the connection string between the quotation marks.</span></span> <span data-ttu-id="e6974-123">Speichern Sie die Datei mit <kbd>STRG+S</kbd>.</span><span class="sxs-lookup"><span data-stu-id="e6974-123">Save the file with <kbd>Ctrl+S</kbd>.</span></span>

1. <span data-ttu-id="e6974-124">Wiederholen Sie den vorherigen Schritt in **privatemessagereceiver/Program.cs**. Fügen Sie dabei den gleichen Verbindungszeichenfolgenwert ein.</span><span class="sxs-lookup"><span data-stu-id="e6974-124">Repeat the previous step in **privatemessagereceiver/Program.cs**, pasting in the same connection string value.</span></span> <span data-ttu-id="e6974-125">Speichern Sie die Datei entweder über das Menü unter „...“ oder über die entsprechende Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux bzw. <kbd>CMD+S</kbd> unter macOS).</span><span class="sxs-lookup"><span data-stu-id="e6974-125">Save the file either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

## <a name="write-code-that-sends-a-message-to-the-queue"></a><span data-ttu-id="e6974-126">Schreiben von Code zum Senden einer Nachricht an die Warteschlange</span><span class="sxs-lookup"><span data-stu-id="e6974-126">Write code that sends a message to the queue</span></span>

<span data-ttu-id="e6974-127">Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zu Verkäufen gesendet werden:</span><span class="sxs-lookup"><span data-stu-id="e6974-127">To complete the component that sends messages about sales, follow these steps:</span></span>

1. <span data-ttu-id="e6974-128">Öffnen Sie **privatemessagesender/Program.cs** im Editor.</span><span class="sxs-lookup"><span data-stu-id="e6974-128">Open **privatemessagesender/Program.cs** in the editor</span></span>

1. <span data-ttu-id="e6974-129">Suchen Sie nach der `SendSalesMessageAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="e6974-129">Locate the `SendSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="e6974-130">Suchen Sie in dieser Methode nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="e6974-130">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a queue client here
    ```

1. <span data-ttu-id="e6974-131">Ersetzen Sie diese Codezeile durch den folgenden Code, um einen Warteschlangenclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="e6974-131">To create a queue client, replace that line of code with the following code:</span></span>

    ```C#
    var queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="e6974-132">Suchen Sie im `try...catch`-Block nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="e6974-132">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="e6974-133">Ersetzen Sie diese Codezeile durch den folgenden Code, um eine Nachricht für die Warteschlange zu erstellen und zu formatieren:</span><span class="sxs-lookup"><span data-stu-id="e6974-133">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"$10,000 order for bicycle parts from retailer Adventure Works.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="e6974-134">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht in der Konsole anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="e6974-134">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="e6974-135">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht an die Warteschlange zu senden:</span><span class="sxs-lookup"><span data-stu-id="e6974-135">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.SendAsync(message);
    ```

1. <span data-ttu-id="e6974-136">Suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="e6974-136">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the queue here
    ```

1. <span data-ttu-id="e6974-137">Ersetzen Sie diese Codezeile durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:</span><span class="sxs-lookup"><span data-stu-id="e6974-137">To close the connection the Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="e6974-138">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="e6974-138">Save the file.</span></span>

## <a name="send-a-message-to-the-queue"></a><span data-ttu-id="e6974-139">Senden einer Nachricht an die Warteschlange</span><span class="sxs-lookup"><span data-stu-id="e6974-139">Send a message to the queue</span></span>

<span data-ttu-id="e6974-140">Führen Sie den folgenden Befehl in Cloud Shell aus, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:</span><span class="sxs-lookup"><span data-stu-id="e6974-140">To run the component that sends a message about a sale, run this command in the Cloud Shell:</span></span>

```bash
dotnet run -p privatemessagesender
```

> [!NOTE]
> <span data-ttu-id="e6974-141">Das Starten der Apps, die Sie während dieser Übung ausführen, kann einen Moment dauern. Über `dotnet` müssen Pakete von Remotequellen wiederhergestellt werden, und für die Apps muss für die erste Ausführung ein Buildvorgang durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="e6974-141">The apps you run during this exercise may take a moment to start up, as `dotnet` has to restore packages from remote sources and build the apps the first time they are run.</span></span>

<span data-ttu-id="e6974-142">Während das Programm ausgeführt wird, werden Nachrichten ausgegeben, die darauf hinweisen, dass die Komponente eine Nachricht sendet.</span><span class="sxs-lookup"><span data-stu-id="e6974-142">As the program executes, you'll see messages printed indicating that it's sending a message.</span></span> <span data-ttu-id="e6974-143">Bei jeder Ausführung der App wird der Warteschlange eine zusätzliche Nachricht hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="e6974-143">Each time you run the app, one additional message will be added to the queue.</span></span>

<span data-ttu-id="e6974-144">Führen Sie nach Abschluss des Vorgangs den folgenden Befehl aus, um die Anzahl von Nachrichten in der Warteschlange anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="e6974-144">Once it's finished, run the following command to see how many messages are in the queue:</span></span>

```azurecli
az servicebus queue show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --name salesmessages \
    --query messageCount
```

## <a name="write-code-that-receives-a-message-from-the-queue"></a><span data-ttu-id="e6974-145">Schreiben von Code für den Empfang einer Nachricht aus der Warteschlange</span><span class="sxs-lookup"><span data-stu-id="e6974-145">Write code that receives a message from the queue</span></span>

1. <span data-ttu-id="e6974-146">Öffnen Sie **privatemessagereceiver/Program.cs** im Editor.</span><span class="sxs-lookup"><span data-stu-id="e6974-146">Open **privatemessagereceiver/Program.cs** in the editor</span></span>

1. <span data-ttu-id="e6974-147">Suchen Sie nach der `ReceiveSalesMessageAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="e6974-147">Locate the `ReceiveSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="e6974-148">Suchen Sie in dieser Methode nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="e6974-148">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a queue client here
    ```

1. <span data-ttu-id="e6974-149">Ersetzen Sie diese Zeile durch den folgenden Code, um einen Warteschlangenclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="e6974-149">To create a queue client, replace that line with the following code:</span></span>

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="e6974-150">Suchen Sie nach der `RegisterMessageHandler()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="e6974-150">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="e6974-151">Ersetzen Sie sämtlichen Code innerhalb dieser Methode durch den folgenden Code, um Optionen für die Behandlung von Nachrichten zu konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="e6974-151">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="e6974-152">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um den Nachrichtenhandler zu registrieren:</span><span class="sxs-lookup"><span data-stu-id="e6974-152">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="e6974-153">Suchen Sie nach der `ProcessMessagesAsync()`-Methode.</span><span class="sxs-lookup"><span data-stu-id="e6974-153">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="e6974-154">Sie haben diese Methode als Methode registriert, mit der eingehende Nachrichten behandelt werden.</span><span class="sxs-lookup"><span data-stu-id="e6974-154">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="e6974-155">Ersetzen Sie den gesamten Code dieser Methode durch den folgenden Code, um in der Konsole eingehende Nachrichten anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="e6974-155">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="e6974-156">Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die empfangene Nachricht aus der Warteschlange zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="e6974-156">To remove the received message from the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="e6974-157">Wechseln Sie zurück zur `ReceiveSalesMessageAsync()`-Methode, und suchen Sie nach der folgenden Codezeile:</span><span class="sxs-lookup"><span data-stu-id="e6974-157">Return to the `ReceiveSalesMessageAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the queue here
    ```

1. <span data-ttu-id="e6974-158">Ersetzen Sie diese Zeile durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:</span><span class="sxs-lookup"><span data-stu-id="e6974-158">To close the connection to Service Bus, replace that line with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="e6974-159">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="e6974-159">Save the file.</span></span>

## <a name="retrieve-a-message-from-the-queue"></a><span data-ttu-id="e6974-160">Abrufen einer Nachricht aus der Warteschlange</span><span class="sxs-lookup"><span data-stu-id="e6974-160">Retrieve a message from the queue</span></span>

<span data-ttu-id="e6974-161">Führen Sie den folgenden Befehl in Cloud Shell aus, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:</span><span class="sxs-lookup"><span data-stu-id="e6974-161">To run the component that sends a message about a sale, run this command in the Cloud Shell:</span></span>

```bash
dotnet run -p privatemessagereceiver
```

<span data-ttu-id="e6974-162">Wenn Sie sehen, dass die Nachricht empfangen wurde und in der Konsole angezeigt wird, können Sie `Enter` drücken, um die App zu beenden.</span><span class="sxs-lookup"><span data-stu-id="e6974-162">When you see that the message has been received and displayed in the console, press `Enter` to stop the app.</span></span> <span data-ttu-id="e6974-163">Führen Sie dann den gleichen Befehl wie zuvor aus, um sich zu vergewissern, dass alle Nachrichten aus der Warteschlange entfernt wurden:</span><span class="sxs-lookup"><span data-stu-id="e6974-163">Then, run the same command as before to confirm that all of the messages have been removed from the queue:</span></span>

```azurecli
az servicebus queue show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --name salesmessages \
    --query messageCount
```

<span data-ttu-id="e6974-164">Es wird `0` angezeigt, wenn alle Nachrichten entfernt wurden.</span><span class="sxs-lookup"><span data-stu-id="e6974-164">This will show `0` if all the messages have been removed.</span></span>

<span data-ttu-id="e6974-165">Sie haben Code geschrieben, mit dem eine Nachricht zu einem einzelnen Verkauf an eine Service Bus-Warteschlange gesendet wird.</span><span class="sxs-lookup"><span data-stu-id="e6974-165">You have written code that sends a message about individual sales to a Service Bus queue.</span></span> <span data-ttu-id="e6974-166">In der verteilten Vertriebsanwendung sollten Sie diesen Code in der mobilen App schreiben, die von den Vertriebsmitarbeitern auf den Geräten genutzt wird.</span><span class="sxs-lookup"><span data-stu-id="e6974-166">In the sales force distributed application, you should write this code in the mobile app that sales personnel use on devices.</span></span>

<span data-ttu-id="e6974-167">Sie haben auch Code geschrieben, mit dem eine Nachricht von der Service Bus-Warteschlange empfangen wird.</span><span class="sxs-lookup"><span data-stu-id="e6974-167">You have also written code that receives a message from the Service Bus queue.</span></span> <span data-ttu-id="e6974-168">In der verteilten Vertriebsanwendung sollten Sie diesen Code in dem Webdienst schreiben, der in Azure ausgeführt wird und mit dem empfangene Nachrichten verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="e6974-168">In the sales force distributed application, you should write this code in the web service that runs in Azure and processes received messages.</span></span>
