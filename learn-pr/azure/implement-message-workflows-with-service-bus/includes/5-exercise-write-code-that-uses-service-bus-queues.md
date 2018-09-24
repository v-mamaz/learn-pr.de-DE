Sie haben sich für die Verwendung einer Service Bus-Warteschlange entschieden, um Nachrichten zu den einzelnen Verkäufen zwischen der mobilen App, die von Ihren Vertriebsmitarbeitern genutzt wird, und dem in Azure gehosteten Webdienst auszutauschen. Über den Webdienst werden Details zu den einzelnen Verkäufen in einer Azure SQL-Datenbank-Instanz gespeichert.

Sie haben die erforderlichen Objekte in Ihrem Azure-Abonnement implementiert. Nun möchten Sie Code schreiben, mit dem Nachrichten an diese Warteschlange gesendet und daraus abgerufen werden.

## <a name="clone-and-open-the-starter-application"></a>Klonen und Öffnen der Startanwendung

In dieser Einheit erstellen Sie zwei Konsolenanwendungen. Mit der ersten Anwendung werden Nachrichten in einer Service Bus-Warteschlange angeordnet, und mit der zweiten werden diese Nachrichten abgerufen. Die Anwendungen sind Teil einer einzelnen .NET Core-Lösung.

1. Beginnen Sie, indem Sie die Lösung klonen: Führen Sie die folgenden Befehle in Cloud Shell aus:

```bash
cd ~
git clone https://github.com/MicrosoftDocs/mslearn-connect-services-together.git
```

2. Wechseln Sie als Nächstes in den Startordner, und öffnen Sie den Cloud Shell-Editor.

```bash
cd mslearn-connect-services-together/implement-message-workflows-with-service-bus/src/start
code .
```

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>Konfigurieren einer Verbindungszeichenfolge für einen Service Bus-Namespace

Sie müssen in Ihren Konsolen-Apps zwei Informationselemente konfigurieren, um auf einen Service Bus-Namespace zuzugreifen und eine Warteschlange zu verwenden:

* Endpunkt für Ihren Namespace
* Freigegebener Zugriffsschlüssel für die Authentifizierung

Beide Werte können im Azure-Portal in Form einer vollständigen Verbindungszeichenfolge abgerufen werden.

> [!NOTE]
> Der Einfachheit halber führen Sie für die Verbindungszeichenfolge in der Datei **Program.cs** beider Konsolenanwendungen das Hartcodieren durch. In einer Produktionsanwendung können Sie eine Konfigurationsdatei oder auch Azure Key Vault nutzen, um die Verbindungszeichenfolge zu speichern.

1. Führen Sie in Cloud Shell den folgenden Befehl aus, um die primäre Verbindungszeichenfolge für Ihren Service Bus-Namespace anzuzeigen. Ersetzen Sie `<namespace-name>` durch den Namen Ihres Service Bus-Namespace.

    ```azurecli
    az servicebus namespace authorization-rule keys list \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --namespace-name <namespace-name> \
        --name RootManageSharedAccessKey \
        --query primaryConnectionString \
        --output tsv
    ```

    Da Sie diese Verbindungszeichenfolge in diesem Modul mehrfach benötigen, sollten Sie sie schnell zugänglich aufbewahren.

1. Kopieren Sie den Schlüssel aus Cloud Shell. Öffnen Sie im Editor **performancemessagesender/Program.cs**, und suchen Sie die folgende Codezeile:

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    Fügen Sie die Verbindungszeichenfolge zwischen den Anführungszeichen ein. Speichern Sie die Datei mit <kbd>STRG+S</kbd>.

1. Wiederholen Sie den vorherigen Schritt in **privatemessagereceiver/Program.cs**. Fügen Sie dabei den gleichen Verbindungszeichenfolgenwert ein. Speichern Sie die Datei entweder über das Menü unter „...“ oder über die entsprechende Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux bzw. <kbd>CMD+S</kbd> unter macOS).

## <a name="write-code-that-sends-a-message-to-the-queue"></a>Schreiben von Code zum Senden einer Nachricht an die Warteschlange

Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zu Verkäufen gesendet werden:

1. Öffnen Sie **privatemessagesender/Program.cs** im Editor.

1. Suchen Sie nach der `SendSalesMessageAsync()`-Methode.

1. Suchen Sie in dieser Methode nach der folgenden Codezeile:

    ```C#
    // Create a queue client here
    ```

1. Ersetzen Sie diese Codezeile durch den folgenden Code, um einen Warteschlangenclient zu erstellen:

    ```C#
    var queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. Suchen Sie im `try...catch`-Block nach der folgenden Codezeile:

    ```C#
    // Create and send a message here
    ```

1. Ersetzen Sie diese Codezeile durch den folgenden Code, um eine Nachricht für die Warteschlange zu erstellen und zu formatieren:

    ```C#
    string messageBody = $"$10,000 order for bicycle parts from retailer Adventure Works.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht in der Konsole anzuzeigen:

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die Nachricht an die Warteschlange zu senden:

    ```C#
    await queueClient.SendAsync(message);
    ```

1. Suchen Sie nach der folgenden Codezeile:

    ```C#
    // Close the connection to the queue here
    ```

1. Ersetzen Sie diese Codezeile durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:

    ```C#
    await queueClient.CloseAsync();
    ```

1. Speichern Sie die Datei.

## <a name="send-a-message-to-the-queue"></a>Senden einer Nachricht an die Warteschlange

Führen Sie den folgenden Befehl in Cloud Shell aus, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:

```bash
dotnet run -p privatemessagesender
```

> [!NOTE]
> Das Starten der Apps, die Sie während dieser Übung ausführen, kann einen Moment dauern. Über `dotnet` müssen Pakete von Remotequellen wiederhergestellt werden, und für die Apps muss für die erste Ausführung ein Buildvorgang durchgeführt werden.

Während das Programm ausgeführt wird, werden Nachrichten ausgegeben, die darauf hinweisen, dass die Komponente eine Nachricht sendet. Bei jeder Ausführung der App wird der Warteschlange eine zusätzliche Nachricht hinzugefügt.

Führen Sie nach Abschluss des Vorgangs den folgenden Befehl aus, um die Anzahl von Nachrichten in der Warteschlange anzuzeigen:

```azurecli
az servicebus queue show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --name salesmessages \
    --query messageCount
```

## <a name="write-code-that-receives-a-message-from-the-queue"></a>Schreiben von Code für den Empfang einer Nachricht aus der Warteschlange

1. Öffnen Sie **privatemessagereceiver/Program.cs** im Editor.

1. Suchen Sie nach der `ReceiveSalesMessageAsync()`-Methode.

1. Suchen Sie in dieser Methode nach der folgenden Codezeile:

    ```C#
    // Create a queue client here
    ```

1. Ersetzen Sie diese Zeile durch den folgenden Code, um einen Warteschlangenclient zu erstellen:

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
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
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. Suchen Sie nach der `ProcessMessagesAsync()`-Methode. Sie haben diese Methode als Methode registriert, mit der eingehende Nachrichten behandelt werden.

1. Ersetzen Sie den gesamten Code dieser Methode durch den folgenden Code, um in der Konsole eingehende Nachrichten anzuzeigen:

    ```C#
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. Fügen Sie in der nächsten Zeile den folgenden Code hinzu, um die empfangene Nachricht aus der Warteschlange zu entfernen:

    ```C#
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. Wechseln Sie zurück zur `ReceiveSalesMessageAsync()`-Methode, und suchen Sie nach der folgenden Codezeile:

    ```C#
    // Close the queue here
    ```

1. Ersetzen Sie diese Zeile durch den folgenden Code, um die Verbindung mit Service Bus zu schließen:

    ```C#
    await queueClient.CloseAsync();
    ```

1. Speichern Sie die Datei.

## <a name="retrieve-a-message-from-the-queue"></a>Abrufen einer Nachricht aus der Warteschlange

Führen Sie den folgenden Befehl in Cloud Shell aus, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:

```bash
dotnet run -p privatemessagereceiver
```

Wenn Sie sehen, dass die Nachricht empfangen wurde und in der Konsole angezeigt wird, können Sie `Enter` drücken, um die App zu beenden. Führen Sie dann den gleichen Befehl wie zuvor aus, um sich zu vergewissern, dass alle Nachrichten aus der Warteschlange entfernt wurden:

```azurecli
az servicebus queue show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --name salesmessages \
    --query messageCount
```

Es wird `0` angezeigt, wenn alle Nachrichten entfernt wurden.

Sie haben Code geschrieben, mit dem eine Nachricht zu einem einzelnen Verkauf an eine Service Bus-Warteschlange gesendet wird. In der verteilten Vertriebsanwendung sollten Sie diesen Code in der mobilen App schreiben, die von den Vertriebsmitarbeitern auf den Geräten genutzt wird.

Sie haben auch Code geschrieben, mit dem eine Nachricht von der Service Bus-Warteschlange empfangen wird. In der verteilten Vertriebsanwendung sollten Sie diesen Code in dem Webdienst schreiben, der in Azure ausgeführt wird und mit dem empfangene Nachrichten verarbeitet werden.
