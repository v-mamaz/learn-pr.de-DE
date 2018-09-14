Sie haben sich für die Verwendung einer Service Bus-Warteschlange entschieden, um Nachrichten zu den einzelnen Verkäufen zwischen der mobilen App, die von Ihren Vertriebsmitarbeitern genutzt wird, und dem in Azure gehosteten Webdienst auszutauschen. Über den Webdienst werden Details zu den einzelnen Verkäufen in einer Azure SQL-Datenbank-Instanz gespeichert.

Sie haben die erforderlichen Objekte in Ihrem Azure-Abonnement implementiert. Nun möchten Sie Code schreiben, mit dem Nachrichten an diese Warteschlange gesendet und daraus abgerufen werden.

## <a name="clone-and-open-the-starter-application"></a>Klonen und Öffnen der Startanwendung

In dieser Einheit erstellen Sie zwei Konsolenanwendungen in **Visual Studio Code**. Mit der ersten Anwendung werden Nachrichten in einer Service Bus-Warteschlange angeordnet, und mit der zweiten werden diese Nachrichten abgerufen. Die Anwendungen sind Teil einer einzelnen .NET Core-Lösung. 

Führen Sie zuerst das Klonen der Lösung durch:

1. Starten Sie eine Eingabeaufforderung, und wechseln Sie in das Verzeichnis, in dem Sie den Quellcode für die Anwendung hosten möchten.

1. Geben Sie den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:

    ```powershell
    git clone https:\\ <!-- TODO: (add git URL) -->
    ```

1. Nachdem der Klonvorgang abgeschlossen ist, können Sie in den Startordner wechseln.

1. Geben Sie den folgenden Befehl ein, und drücken Sie die **EINGABETASTE**:

    ```powershell
    code .
    ```

1. Klicken Sie auf **Ja**, wenn eine Meldung mit der Abfrage zur Wiederherstellung von Abhängigkeiten angezeigt wird.

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>Konfigurieren einer Verbindungszeichenfolge für einen Service Bus-Namespace

Sie müssen in Ihren Konsolen-Apps zwei Informationselemente konfigurieren, um auf einen Service Bus-Namespace zuzugreifen und eine Warteschlange zu verwenden:

* Endpunkt für Ihren Namespace
* Freigegebener Zugriffsschlüssel für die Authentifizierung

Beide Werte können im Azure-Portal in Form einer vollständigen Verbindungszeichenfolge abgerufen werden.

> [!NOTE]
> Der Einfachheit halber führen Sie für die Verbindungszeichenfolge in der Datei **Program.cs** beider Konsolenanwendungen das Hartcodieren durch. In einer Produktionsanwendung können Sie eine Konfigurationsdatei oder auch Azure Key Vault nutzen, um die Verbindungszeichenfolge zu speichern.

1. Wechseln Sie zum Azure-Portal.

1. Klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.

1. Klicken Sie unter **EINSTELLUNGEN** auf **Freigegebene Zugriffsrichtlinien**.

1. Klicken Sie in der Liste mit den Richtlinien auf **RootManageSharedAccessKey**.

1. Klicken Sie rechts vom Textfeld **Primäre Verbindungszeichenfolge** auf die Schaltfläche **Click to copy** \(Zum Kopieren klicken).

1. Wechseln Sie zu **Visual Studio Code**.

1. Klicken Sie im Bereich **Explorer** im Ordner **privatemessagesender** auf die Datei **Program.cs**.

1. Suchen Sie nach der folgenden Codezeile:

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. Platzieren Sie den Cursor zwischen den Anführungszeichen, und drücken Sie dann **STRG+V**.

1. Klicken Sie im Bereich **Explorer** im Ordner **privatemessagereceiver** auf die Datei **Program.cs**.

1. Suchen Sie nach der folgenden Codezeile:

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. Platzieren Sie den Cursor zwischen den Anführungszeichen, und drücken Sie dann **STRG+V**.

1. Klicken Sie auf **Datei** und anschließend auf **Alles speichern**.

1. Schließen Sie alle geöffneten Editor-Fenster.

## <a name="write-code-that-sends-a-message-to-the-queue"></a>Schreiben von Code zum Senden einer Nachricht an die Warteschlange

Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zu Verkäufen gesendet werden:

1. Klicken Sie in Visual Studio Code im Bereich **Explorer** im Ordner **privatemessagesender** auf die Datei **Program.cs**.

1. Suchen Sie nach der `SendSalesMessageAsync()`-Methode.

1. Suchen Sie in dieser Methode nach der folgenden Codezeile:

    ```C#
    // Create a queue client here
    ```

1. Ersetzen Sie diese Codezeile durch den folgenden Code, um einen Warteschlangenclient zu erstellen:

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
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

1. Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.

## <a name="send-a-message-to-the-queue"></a>Senden einer Nachricht an die Warteschlange

Verwenden Sie diese Schritte, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:

1. Klicken Sie in Visual Studio Code im Menü **Ansicht** auf **Debuggen**.

1. Wählen Sie im Bereich **Debuggen** in der Dropdownliste die Option **Senden privater Nachrichten starten**, und drücken Sie anschließend **F5**. Visual Studio Code führt das Erstellen und Ausführen der Konsolenanwendung im Debugmodus durch.

1. Sehen Sie sich die Nachrichten in der **Debugging-Konsole** an, während das Programm ausgeführt wird.

1. Wechseln Sie zum Azure-Portal.

1. Falls der Service Bus-Namespace nicht angezeigt wird, klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.

1. Klicken Sie auf dem Blatt **Service Bus-Namespace** unter **ENTITÄTEN** auf **Warteschlangen** und dann auf die Warteschlange **salesmessages**. Unter **ANZAHL AKTIVER NACHRICHTEN** sollte angezeigt werden, dass der Warteschlange eine Nachricht hinzugefügt wurde.

## <a name="write-code-that-receives-a-message-from-the-queue"></a>Schreiben von Code für den Empfang einer Nachricht von der Warteschlange

Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zu Verkäufen abgerufen werden:

1. Klicken Sie in Visual Studio Code im Bereich **Explorer** im Ordner **privatemessagereceiver** auf die Datei **Program.cs**.

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

1. Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.

## <a name="retrieve-a-message-from-the-queue"></a>Abrufen einer Nachricht aus der Warteschlange

Verwenden Sie diese Schritte, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf empfangen wird:

1. Klicken Sie in Visual Studio Code im Menü **Ansicht** auf **Debuggen**.

1. Wählen Sie im Bereich **Debuggen** in der Dropdownliste die Option **Empfangen privater Nachrichten starten**, und drücken Sie anschließend **F5**. Visual Studio Code führt das Erstellen und Ausführen der Konsolenanwendung im Debugmodus durch.

1. Sehen Sie sich die Nachrichten in der **Debugging-Konsole** an, während das Programm ausgeführt wird.

1. Klicken Sie im Menü **Debuggen** auf **Debugging beenden**, wenn Sie sehen, dass die Nachricht empfangen wurde und in der Konsole angezeigt wird.

1. Wechseln Sie zum Azure-Portal.

1. Falls der Service Bus-Namespace nicht angezeigt wird, klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.

1. Klicken Sie auf dem Blatt **Service Bus-Namespace** unter **ENTITÄTEN** auf **Warteschlangen** und dann auf die Warteschlange **salesmessages**. Unter **ANZAHL AKTIVER NACHRICHTEN** sollte angezeigt werden, dass die Nachricht aus der Warteschlange entfernt wurde.

Sie haben Code geschrieben, mit dem eine Nachricht zu einem einzelnen Verkauf an eine Service Bus-Warteschlange gesendet wird. In der verteilten Vertriebsanwendung sollten Sie diesen Code in der mobilen App schreiben, die von den Vertriebsmitarbeitern auf den Geräten genutzt wird.

Sie haben auch Code geschrieben, mit dem eine Nachricht von der Service Bus-Warteschlange empfangen wird. In der verteilten Vertriebsanwendung sollten Sie diesen Code in dem Webdienst schreiben, der in Azure ausgeführt wird und mit dem empfangene Nachrichten verarbeitet werden.
