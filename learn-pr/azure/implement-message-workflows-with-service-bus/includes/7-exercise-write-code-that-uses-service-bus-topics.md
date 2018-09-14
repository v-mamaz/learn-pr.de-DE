Sie möchten eine Azure Service Bus-Thema zu verwenden, um Nachrichten zu vertriebsleistung in Ihrer Anwendung verteilte Außendienstmitarbeiter zu verteilen. Die app ein, die Vertriebsmitarbeiter im Hinblick auf ihren mobilen Geräten senden Nachrichten, die Umsatzzahlen für jeden Bereich und Zeitraum zusammenzufassen. Diese Nachrichten werden an Webdienste verteilt, die sich in den Geschäftsregionen des Unternehmens befinden, einschließlich Amerika und Europa.

Sie haben in Ihrem Azure-Abonnement bereits die erforderliche Infrastruktur implementiert, einschließlich des Themas und der Abonnements. Nun möchten den Code zu schreiben, der Nachrichten an das Thema gesendet und ruft Nachrichten aus jedem Abonnement ab.

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>Konfigurieren einer Verbindungszeichenfolge für einen Service Bus-Namespace

Konfigurieren von Verbindungszeichenfolgen, die sowohl in den sendenden und empfangenden Komponenten starten:

1. Wechseln Sie zum Azure-Portal.

1. Klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.

1. Klicken Sie unter **EINSTELLUNGEN** auf **Freigegebene Zugriffsrichtlinien**.

1. Klicken Sie in der Liste mit den Richtlinien auf **RootManageSharedAccessKey**.

1. Klicken Sie rechts vom Textfeld **Primäre Verbindungszeichenfolge** auf die Schaltfläche **Click to copy** \(Zum Kopieren klicken).

1. Wechseln Sie zu **Visual Studio Code**.

1. Klicken Sie im Bereich **Explorer** im Ordner **performancemessagesender** auf die Datei **Program.cs**.

1. Suchen Sie nach der folgenden Codezeile:

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. Platzieren Sie den Cursor zwischen den Anführungszeichen, und drücken Sie dann **STRG+V**.

1. Klicken Sie im Bereich **Explorer** im Ordner **performancemessagereceiver** auf die Datei **Program.cs**.

1. Suchen Sie nach der folgenden Codezeile:

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. Platzieren Sie den Cursor zwischen den Anführungszeichen, und drücken Sie dann **STRG+V**.

1. Klicken Sie auf **Datei** und anschließend auf **Alles speichern**.

1. Schließen Sie alle geöffneten Editor-Fenster.

## <a name="write-code-that-sends-a-message-to-the-topic"></a>Schreiben von Code zum Senden einer Nachricht an das Thema

Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zur Vertriebsleistung gesendet werden:

1. Klicken Sie in Visual Studio Code im Bereich **Explorer** im Ordner **performancemessagesender** auf die Datei **Program.cs**.

1. Wechseln Sie zur `SendPerformanceMessageAsync()`-Methode.

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

1. Ersetzen Sie diese Codezeile zum Schließen der Verbindung mit Service Bus mit dem folgenden Code:

    ```C#
    await topicClient.CloseAsync();
    ```

1. Schließen Sie in Visual Studio Code alle Editor-Fenster, und speichern Sie alle geänderten Dateien.

## <a name="send-a-message-to-the-topic"></a>Senden einer Nachricht an das Thema

Führen Sie diese Schritte aus, um die Komponente auszuführen, mit der eine Nachricht zu einem Verkauf gesendet wird:

1. Klicken Sie in Visual Studio Code im Menü **Ansicht** auf **Debuggen**.

1. In der **Debuggen** Bereich in der Dropdown-Liste **Leistung Nachrichtenabsender starten**, und drücken Sie dann die **F5**. Visual Studio Code führt das Erstellen und Ausführen der Konsolenanwendung im Debugmodus durch.

1. Sehen Sie sich die Nachrichten in der **Debugging-Konsole** an, während das Programm ausgeführt wird.

1. Wechseln Sie zum Azure-Portal.

1. Falls der Service Bus-Namespace nicht angezeigt wird, klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.

1. Klicken Sie auf dem Blatt **Service Bus-Namespace** unter **ENTITÄTEN** auf **Themen** und dann auf das Thema **salesperformancemessages**. In der Liste der Abonnements sollte sowohl im **Amerika**- als auch im **Europa**-Abonnement eine Nachricht angezeigt werden.

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a>Schreiben von Code zum Empfangen einer Nachricht von einem Themenabonnement

Führen Sie diese Schritte aus, um die Komponente fertigzustellen, mit der Nachrichten zur Vertriebsleistung empfangen werden:

1. Klicken Sie in Visual Studio Code im Bereich **Explorer** im Ordner **performancemessagereceiver** auf die Datei **Program.cs**.

1. Wechseln Sie zur `MainAsync()`-Methode.

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

Führen Sie diese Schritte aus, um die Komponente auszuführen, mit der Nachrichten zur Vertriebsleistung empfangen werden:

1. Klicken Sie in Visual Studio Code im Menü **Ansicht** auf **Debuggen**.

1. In der **Debuggen** Bereich in der Dropdown-Liste **Leistung Nachrichtenempfänger starten**, und drücken Sie dann die **F5**. Visual Studio Code führt das Erstellen und Ausführen der Konsolenanwendung im Debugmodus durch.

1. Sehen Sie sich die Nachrichten in der **Debugging-Konsole** an, während das Programm ausgeführt wird.

1. Klicken Sie im Menü **Debuggen** auf **Debugging beenden**, wenn Sie sehen, dass die Nachricht empfangen wurde und in der Konsole angezeigt wird.

1. Wechseln Sie zum Azure-Portal.

1. Falls der Service Bus-Namespace nicht angezeigt wird, klicken Sie auf der Startseite auf **Alle Ressourcen** und dann auf den zuvor erstellten Service Bus-Namespace.

1. Klicken Sie auf dem Blatt **Service Bus-Namespace** unter **ENTITÄTEN** auf **Themen** und dann auf das Thema **salesperformancemessages**. In der Liste der Abonnements sollten im **Amerika**-Abonnement null Nachrichten angezeigt werden, da Ihre Anwendung die einzige Nachricht verarbeitet und entfernt hat. Beachten Sie, dass die Nachricht im **Europa**-Abonnement noch vorhanden ist.
