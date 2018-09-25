Wir haben uns entschieden, ein Azure Service Bus-Thema zu verwenden, um Nachrichten über die Vertriebsleistung in Ihrer verteilten Sales Force-Anwendung zu verteilen. Die von Vertriebsmitarbeitern auf ihren mobilen Geräten verwendete App sendet Nachrichten mit zusammengefassten Umsatzzahlen für die einzelnen Gebiete und Zeiträume. Diese Nachrichten werden an Webdienste verteilt, die sich in den Geschäftsregionen des Unternehmens befinden, einschließlich Amerika und Europa.

Sie haben in Ihrem Azure-Abonnement bereits die erforderliche Infrastruktur, darunter auch das Thema und die Abonnements, implementiert. Jetzt möchten Sie den Code schreiben, der Nachrichten an das Thema sendet und Nachrichten eines Abonnements abruft.

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>Konfigurieren einer Verbindungszeichenfolge für einen Service Bus-Namespace

Konfigurieren Sie zunächst Verbindungszeichenfolgen in der sendenden und empfangenden Komponente:

1. Öffnen Sie **performancemessagesender/Program.cs** im Editor, und suchen Sie die folgende Codezeile:

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    Fügen Sie die Verbindungszeichenfolge zwischen den Anführungszeichen ein, und speichern Sie die Datei entweder über das Menü „...“ oder über die entsprechende Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux, <kbd>cmd+S</kbd> unter macOS).

1. Wiederholen Sie den vorherigen Schritt in **performancemessagereceiver/Program.cs**. Fügen Sie dabei den gleichen Verbindungszeichenfolgenwert ein, und speichern Sie die Datei.

## <a name="write-code-that-sends-a-message-to-the-topic"></a>Schreiben von Code zum Senden einer Nachricht an das Thema

Führen Sie die folgenden Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zur Vertriebsleistung gesendet werden:

1. Öffnen Sie **performancemessagesender/Program.cs** im Editor.

1. Suchen Sie nach der `SendPerformanceMessageAsync()`-Methode.

1. Suchen Sie in dieser Methode nach der folgenden Codezeile:

    ```C#
    // Create a Topic Client here
    ```

1. Ersetzen Sie diese Codezeile durch den folgenden Code, um einen Themenclient zu erstellen:

    ```C#
    topicClient = new TopicClient(ServiceBusConnectionString, TopicName);
    ```

1. Suchen Sie im `try...catch`-Block nach der folgenden Codezeile:

    ```C#
    // Create and send a message here
    ```

1. Ersetzen Sie diese Codezeile durch den folgenden Code, um eine Nachricht für die Warteschlange zu erstellen und zu formatieren:

    ```C#
    string messageBody = $"Total sales for Brazil in August: $13m.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht in der Konsole anzuzeigen:

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht an die Warteschlange zu senden:

    ```C#
    await topicClient.SendAsync(message);
    ```

1. Suchen Sie nach der folgenden Codezeile:

    ```C#
    // Close the connection to the topic here
    ```

1. Ersetzen Sie diese Codezeile durch den folgenden Code, um die Verbindung mit Service Bus zu beenden:

    ```C#
    await topicClient.CloseAsync();
    ```

1. Speichern Sie die Datei.

## <a name="send-a-message-to-the-topic"></a>Senden einer Nachricht an das Thema

Führen Sie den folgenden Befehl in Cloud Shell aus, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:

```bash
dotnet run -p performancemessagesender
```

Während das Programm ausgeführt wird, werden Nachrichten ausgegeben, die darauf hinweisen, dass die Komponente eine Nachricht sendet. Bei jedem Ausführen der App wird dem Thema eine zusätzliche Nachricht hinzugefügt, und jeder Abonnent erhält eine Kopie.

Führen Sie nach Abschluss der Ausführung den folgenden Befehl aus, um sich die Anzahl der Nachrichten im Abonnement „Amerika“ anzeigen zu lassen:

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

Wenn Sie `EuropeAndAfrica` durch `Americas` ersetzen, sollte für beide Abonnements die gleiche Anzahl von Nachrichten angezeigt werden.

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a>Schreiben von Code zum Empfangen einer Nachricht von einem Themenabonnement

Führen Sie die folgenden Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zur Vertriebsleistung abgerufen werden:

1. Öffnen Sie **performancemessagereceiver/Program.cs** im Editor.

1. Suchen Sie nach der `MainAsync()`-Methode.

1. Suchen Sie in dieser Methode nach der folgenden Codezeile:

    ```C#
    // Create a subscription client here
    ```

1. Ersetzen Sie diese Zeile durch den folgenden Code, um einen Abonnementclient zu erstellen:

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);
    ```

1. Suchen Sie nach der `RegisterMessageHandler()`-Methode.

1. Ersetzen Sie sämtlichen Code innerhalb dieser Methode durch den folgenden Code, um Optionen für die Behandlung von Nachrichten zu konfigurieren:

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um den Nachrichtenhandler zu registrieren:

    ```C#
    subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. Suchen Sie nach der `ProcessMessagesAsync()`-Methode. Sie haben diese Methode als Methode registriert, mit der eingehende Nachrichten behandelt werden.

1. Ersetzen Sie den gesamten Code dieser Methode durch den folgenden Code, um in der Konsole eingehende Nachrichten anzuzeigen:

    ```C#
    Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die empfangene Nachricht aus dem Abonnement zu entfernen:

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. Wechseln Sie zurück zur `MainAsync()`-Methode, und suchen Sie nach der folgenden Codezeile:

    ```C#
    // Close the subscription here
    ```

1. Ersetzen Sie diesen Code durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:

    ```C#
    await subscriptionClient.CloseAsync();
    ```

1. Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.

## <a name="retrieve-a-message-from-a-topic-subscription"></a>Abrufen einer Nachricht aus einem Themenabonnement

Führen Sie die folgenden Schritte aus, um die Komponente auszuführen, mit der Nachrichten zur Vertriebsleistung abgerufen werden:

```bash
dotnet run -p performancemessagereceiver
```

Wenn das Programm keine Nachrichten mehr ausgibt, in denen darauf hingewiesen wird, dass Nachrichten empfangen werden, drücken Sie `Enter`, um die App zu beenden. Führen Sie anschließend den gleichen Befehl wie zuvor aus, um sicherzustellen, dass im `Americas`-Abonnement keine Nachrichten mehr vorhanden sind.

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

Wenn Sie `EuropeAndAfrica` durch `Americas` ersetzen, sehen Sie, dass sich die Anzahl der Nachrichten nicht geändert hat. Die Anwendung hat nur Nachrichten vom `Americas`-Abonnement empfangen.
