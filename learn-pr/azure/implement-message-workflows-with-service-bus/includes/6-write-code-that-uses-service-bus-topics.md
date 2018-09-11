In einer verteilten Anwendung müssen einige Nachrichten nur an eine Empfängerkomponente gesendet werden. Andere Nachrichten sind für mehr als ein Ziel bestimmt.

Hier wird beschrieben, was passiert, wenn ein Benutzer die Bestellung einer Pizza storniert. Dieser Vorgang weicht etwas vom Aufgeben der ursprünglichen Bestellung ab. In diesem Fall wollten wir warten, bis für die Bestellung die Verarbeitung der Zahlung abgeschlossen ist, bevor die Bestellung an die weiteren Schritte gesendet wird (z.B. den Zubereitungs-/Kochvorgang im Geschäft). Für den Stornierungsvorgang benachrichtigen wir dagegen gleichzeitig das Geschäft *und* die Stelle, von der die Zahlung verarbeitet wird. Mit diesem Ansatz wird die Wahrscheinlichkeit verringert, dass wir Zutaten oder Lieferzeitaufwand vergeuden.

Wir verwenden ein Azure Service Bus-Thema, um es zu ermöglichen, dass mehrere Komponenten die gleiche Nachricht erhalten.

## <a name="how-code-that-uses-topics-differs-from-queues"></a>Code mit Verwendung von Themen – Unterscheidung von Warteschlangen

Sie verwenden Themen, wenn Sie möchten, dass alle an das Thema gesendeten Nachrichten für alle am Abonnement beteiligten Komponenten zugestellt wird. Das Schreiben von Code mit Verwendung von Themen unterscheidet sich von Warteschlangen. Sie verwenden das gleiche **Microsoft.Azure.ServiceBus**-NuGet-Paket, konfigurieren Verbindungszeichenfolgen und nutzen asynchrone Programmierungsmuster.

Anstelle der `QueueClient`-Klasse verwenden Sie aber die `TopicClient`-Klasse, um Nachrichten zu senden, und die `SubscriptionClient`-Klasse, um Nachrichten zu empfangen.

## <a name="setting-filters-on-subscriptions"></a>Festlegen von Filtern für Abonnements

Wenn Sie steuern möchten, welche an das Thema gesendeten Nachrichten an die jeweiligen Abonnements gesendet werden, können Sie für jedes Abonnement im Thema Filter festlegen. In der Pizza-Anwendung werden in den Geschäften beispielsweise UWP-Anwendungen ausgeführt. Jedes Geschäft kann das Thema „OrderCancellation“ abonnieren, aber nach seiner eigenen „StoreId“ filtern. Wir sparen Internetbandbreite, da keine unnötigen Nachrichten an weit entfernte Geschäftsstandorte gesendet werden. In der Zwischenzeit abonniert die Komponente für die Zahlungsverarbeitung unsere gesamten Stornierungsnachrichten.

Drei Arten von Filtern sind möglich:

- **Boolesche Filter:** Mit `TrueFilter` wird sichergestellt, dass alle an das Thema gesendeten Nachrichten für das aktuelle Abonnement zugestellt werden. Mit `FalseFilter` wird sichergestellt, dass keine Nachricht für das aktuelle Abonnement zugestellt wird. (Hierdurch wird das Abonnement praktisch blockiert bzw. ausgeschaltet.)
- **SQL-Filter:** Mit einem SQL-Filter wird eine Bedingung angegeben, indem die gleiche Syntax wie in der `WHERE`-Klausel einer SQL-Abfrage verwendet wird. Nur Nachrichten, für die beim Auswerten für dieses Abonnement `True` zurückgegeben wird, werden für die Abonnenten zugestellt.
- **Korrelationsfilter:** Ein Korrelationsfilter enthält einen Satz mit Bedingungen, die mit den Eigenschaften jeder Nachricht abgeglichen werden. Wenn die Eigenschaft im Filter und die Eigenschaft der Nachricht über den gleichen Wert verfügen, ergibt sich eine Übereinstimmung.

Für unseren StoreId-Filter *können* wir einen SQL-Filter verwenden. Dies sind die flexibelsten Filter, die aber auch mit dem höchsten Rechenaufwand verbunden sind und zu einer Verlangsamung des Service Bus-Durchsatzes führen können. In diesem Fall wählen wir stattdessen einen Korrelationsfilter. 

## <a name="topicclient-example"></a>TopicClient-Beispiel

Für alle Sende- oder Empfangskomponenten sollten Sie die folgenden using-Anweisungen allen Codedateien hinzufügen, mit denen ein Service Bus-Thema aufgerufen wird:

    ```C#
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.ServiceBus;
    ```

Beginnen Sie das Senden einer Nachricht, indem Sie ein neues `TopicClient`-Objekt erstellen und dafür die Verbindungszeichenfolge und den Namen des Themas übergeben:

    ```C#
    topicClient = new TopicClient(TextAppConnectionString, "GroupMessageTopic");
    ```

Sie können eine Nachricht an das Thema senden, indem Sie die `TopicClient.SendAsync()`-Methode aufrufen und die Nachricht übergeben. Wie bei Warteschlangen auch, muss die Nachricht das Format einer Zeichenfolge mit UTF-8-Codierung aufweisen:

    ```C#
    string message = "Cancel! I can't believe you use canned mushrooms!";
    var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
    await topicClient.SendAsync(encodedMessage);
    ```

Um Nachrichten zu erhalten, müssen Sie ein `SubscriptionClient`-Objekt erstellen (kein `TopicClient`-Objekt) und dafür die Verbindungszeichenfolge, den Namen des Themas **und** den Namen des Abonnements übergeben:

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, "GroupMessageTopic", "NorthAmerica");
    ```

Registrieren Sie anschließend einen Nachrichtenhandler. Dies ist die asynchrone Methode in Ihrem Code, mit der die abgerufene Nachricht verarbeitet wird.

    ```C#
    subscriptionClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
    ```

Rufen Sie im Nachrichtenhandler die `SubscriptionClient.CompleteAsync()`-Methode auf, um die Nachricht aus der Warteschlange zu entfernen:

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```