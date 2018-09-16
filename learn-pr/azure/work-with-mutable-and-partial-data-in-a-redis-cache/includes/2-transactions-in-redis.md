In manchen Fällen müssen Sie sicherstellen, dass mehrere Vorgänge gemeinsam ausgeführt werden. In Ihrer Instant Messaging-Anwendung können Benutzer beispielsweise ein einzelnes Bild, eine individuelle Textnachricht oder ein Bild und eine Textnachricht zusammen senden. Wenn der Benutzer sich dafür entscheidet, ein Bild und eine Textnachricht zusammen zu senden, müssen wir sicherstellen, dass andere Mitglieder der Gruppe beide Elemente gleichzeitig empfangen. Dies ist wichtig, denn wenn ein Bild und eine Textnachricht nicht zusammen empfangen werden, ist es möglich, dass zwischen dem Bild und der Textnachricht eine separate Nachricht gesendet wird, wodurch die gesamte Unterhaltung verwirrend werden könnte.

Im Folgenden wird erläutert, wie Sie eine Transaktion in Redis erstellen, um sicherzustellen, dass mehrere Vorgänge gemeinsam ausgeführt werden.

## <a name="how-to-create-a-transaction"></a>Erstellen einer Transaktion

Um eine Transaktion zu erstellen, benötigen Sie einen Transaktionsblock. Dies ist eine Warteschlange, die die Befehle enthält, die zusammen ausgeführt werden. Der Befehl `MULTI` wird verwendet, um einen Transaktionsblock zu erstellen, und alle nachfolgenden Befehle werden für die atomische Ausführung in der Warteschlange gespeichert.

## <a name="how-to-execute-a-transaction"></a>Ausführen einer Transaktion

Um die Befehle in einem Transaktionsblock auszuführen, verwenden Sie den Befehl `EXEC`. Dadurch werden alle Befehle in der Warteschlange ausgeführt, und der normale Verbindungszustand wird wiederhergestellt. Wenn Sie sich entscheiden, keine Transaktion auszuführen, können Sie den Befehl `DISCARD` verwenden, der den Transaktionsblock löscht und den Verbindungsstatus auf normal festlegt.

Ein wichtiger Aspekt, den Sie bei Redis-Transaktionen beachten sollten, ist, dass sie keine Rollbacks unterstützen. Das bedeutet, dass die restlichen Befehle weiterhin ausgeführt werden, wenn ein Befehl innerhalb einer Transaktion fehlschlägt.

## <a name="what-is-servicestackredis"></a>Was ist ServiceStack.Redis?

Im vorherigen Modul **Optimieren einer Webanwendung durch Zwischenspeichern von schreibgeschützten Daten mit Redis** haben wir den **StackExchange.Redis**-Client verwendet. Hier möchten wir einen anderen beliebten Client testen: **ServiceStack.Redis**.

**ServiceStack.Redis** ist eine C#-Clientbibliothek für die Interaktion mit einem Redis-Cache. Das bedeutet, dass wir anstelle von Low-Level-Redis-Befehlen C#-Klassen und -Methoden verwenden können.

Um beispielsweise eine Transaktion zu erstellen, müssen wir normalerweise den Redis-Befehl `MULTI` verwenden. Mit **ServiceStack.Redis** können wir jedoch eine Transaktion mit der `CreateTransaction()`-Methode erstellen.

```csharp
var transaction = redisClient.CreateTransaction();
```

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a>Erstellen einer Transaktion mit C# und dem ServiceStack.Redis-Client

Das folgende Beispiel zeigt die Verwendung von **ServiceStack.Redis** zum Erstellen einer Transaktion, die eine Nachricht senden kann, die ein Bild und Text enthält.

```csharp
public bool SendPictureAndText(string groupChatID, string text, string pictureURL)
{
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create the transaction
        var transaction = redisClient.CreateTransaction();

        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, pictureURL));
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, text));

        //Commit and get result of transaction
        var transactionResult = transaction.Commit();

        return transactionResult;
    }
}
```
Transaktionen stellen sicher, dass mehrere Vorgänge zusammen ausgeführt werden. Sie erstellen eine Transaktion mit dem Befehl `MULTI`, aber mithilfe einer Client-Bibliothek wie **ServiceStack.Redis** können Sie die `CreateTransaction()`-Methode verwenden.