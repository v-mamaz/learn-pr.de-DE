Es gibt Situationen, wenn Sie sicherstellen müssen, dass mehrere Vorgänge zusammen ausgeführt werden. Beispielsweise können in Ihrer instant messaging-Anwendung Benutzer ein einzelnes Bild, eine einzelne Nachricht oder ein Bild und Text-Nachricht zusammen senden. Wenn der Benutzer auswählt, um zusammen eine Bild und Text-Nachricht zu senden, müssen Sie sicherstellen, dass andere Mitglieder der Gruppe zur gleichen Zeit erhalten. Dies ist wichtig, da das empfangen eine Nachricht Bild und Text nicht zusammen, möglich ist, dass eine separate Nachricht zwischen dem Bild und Text-Nachricht gesendet werden konnte. Die gesamte Unterhaltung kann, die auch verwirrend vornehmen.

Hier betrachten wir Gewusst wie: Erstellen einer Transaktion in Azure Redis Cache, um sicherzustellen, dass mehrere Vorgänge zusammen ausgeführt werden.

## <a name="how-to-create-a-transaction"></a>Vorgehensweise: erstellen eine Transaktion

Um Transaktionen zu erstellen, benötigen Sie einen Transaktionsblock. Dies ist eine Warteschlange, die Befehle enthält, die zusammen ausgeführt werden. Die `MULTI` Befehl wird verwendet, um einen Transaktionsblock erstellen, und alle nachfolgenden Befehle werden in die Warteschlange für die unteilbare Ausführung.

## <a name="how-to-execute-a-transaction"></a>Gewusst wie: Ausführen einer Transaktion

Um die Befehle in einem Transaktionsblock auszuführen, verwenden Sie die `EXEC` Befehl. Dadurch werden alle in der Warteschlange Befehle ausführen und den Verbindungsstatus auf Normal wiederherstellen. Wenn Sie sich entscheiden, keine Transaktion ausgeführt werden soll, können Sie mithilfe der `DISCARD` -Befehl, der deaktivieren Sie den Codeblock Transaktion und den Verbindungsstatus auf Normal festgelegt wird.

Wichtig zu verstehen, zu Transaktionen für Azure Redis Cache ist, dass sie keine Wiederherstellung früherer Versionen unterstützen. Dies bedeutet, dass ein Befehl innerhalb einer Transaktion fehlschlägt, die verbleibenden Befehle dennoch ausgeführt werden.

## <a name="what-is-servicestackredis"></a>Was ist ServiceStack.Redis?

**ServiceStack.Redis** ist eine C#-Clientbibliothek für die Interaktion mit Azure Redis Cache. Dies bedeutet, dass anstelle von Low-Level-Azure Redis Cache-Befehle an, wir C#-Klassen und Methoden verwenden können. Z. B. statt der `MULTI` und `EXEC` Befehle aus, um mit eine Transaktion ausgeführt werden, **ServiceStack.Redis** erstellen wir eine `IRedisTransaction` -Objekt unter Verwendung der `CreateTransaction()` Methode.

```csharp
var transaction = redisClient.CreateTransaction();
```

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a>Erstellen Sie eine Transaktion, die mit c# und der Client ServiceStack.Redis

Es folgt ein Beispiel der Verwendung von **ServiceStack.Redis** eine Transaktion erstellt, die eine Nachricht senden kann, die ein Bild und Text enthält.

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
Transaktionen stellen sicher, dass mehrere Vorgänge zusammen ausgeführt werden. Erstellen einer Transaktion mit der `MULTI` Befehl. Bei Verwendung eine Clientbibliothek wie **ServiceStack.Redis**, können Sie die `CreateTransaction()` Methode.