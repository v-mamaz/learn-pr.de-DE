In manchen Fällen müssen Sie sicherstellen, dass mehrere Vorgänge gemeinsam ausgeführt werden. In Ihrer Instant Messaging-Anwendung können Benutzer beispielsweise ein einzelnes Bild, eine individuelle Textnachricht oder ein Bild und eine Textnachricht zusammen senden. Wenn der Benutzer sich dafür entscheidet, ein Bild und eine Textnachricht zusammen zu senden, müssen Sie sicherstellen, dass andere Mitglieder der Gruppe beide Elemente gleichzeitig empfangen. Dies ist wichtig, denn wenn ein Bild und eine Textnachricht nicht zusammen empfangen werden, ist es möglich, dass eine andere Nachricht zwischen dem Bild und der Textnachricht gesendet wird. Dadurch könnte die gesamte Unterhaltung verwirrend werden.

Im Folgenden wird erläutert, wie Sie eine Transaktion in Azure Redis Cache erstellen, um sicherzustellen, dass mehrere Vorgänge gemeinsam ausgeführt werden.

## <a name="creating-and-running-transactions"></a>Erstellen und Ausführen von Transaktionen

Bei Transaktionen werden in Redis mehrere Befehle, die als Gruppe ausgeführt werden sollen, in eine Warteschlange gereiht. Wenn eine Transaktion ausgeführt wird, werden die in der Warteschlange enthaltenen Befehle ausgeführt, ohne dass sich andere Befehle von anderen Clients mit diesen überlappen.

Um einen Transaktionsblock zu starten, geben Sie den Befehl `MULTI` ein. Es werden weitere Befehle in die Warteschlange gereiht, jedoch nicht sofort ausgeführt. Durch Ausführen des Befehls `EXEC` werden alle Befehle in der Warteschlange als Transaktionseinheit ausgeführt. Wenn Sie eine offene Transaktion beim Einfügen von Befehlen in eine Warteschlange abbrechen möchten, wird durch den Befehl `DISCARD` der Transaktionsblock geschlossen, _ohne_ dass die Befehle in der Warteschlange ausgeführt werden.

Redis-Transaktionen unterstützen nicht das Konzept eines Rollbacks. Wenn Sie einen Befehl mit einer falschen Syntax in einen Transaktionsblock in die Warteschlange reihen, bleibt der Block geöffnet, wird jedoch automatisch verworfen, wenn Sie versuchen, ihn mit `EXEC` auszuführen. Wenn bei Befehlen in einer Transaktion, bei denen _während_ der Ausführung (nach Aufruf von `EXEC`) ein Fehler auftritt, wird eine Transaktion weder abgebrochen noch ein Rollback für diese ausgeführt. Redis führt weiterhin alle Befehle aus und betrachtet die Transaktion als erfolgreich abgeschlossen.

## <a name="redis-transactions-with-servicestackredis"></a>Redis-Transaktionen mit ServiceStack.Redis

**ServiceStack.Redis** ist eine C#-Clientbibliothek für die Interaktion mit Azure Redis Cache.

Transaktionen in ServiceStack.Redis werden durch Aufrufen von `IRedisClient.CreateTransaction()` erstellt. Bei dem Objekt `IRedisTransaction`, das zurückgegeben wird, können darin mehrere Befehle mit `QueueCommand()` in der Warteschlange eingereiht sein. Durch Aufrufen von `Commit()` für das Transaktionsobjekt wird es ausgeführt.

`IRedisTransaction`-Objekte können gelöscht werden und stellen automatisch einen `DISCARD`-Befehl aus, wenn diese vor Aufrufen von `Commit()` verworfen werden. Dieses Feature funktioniert gut mit `using`-Blöcken in C#: Wenn Sie eine Transaktion aus irgendeinem Grund nicht committen sollten, wird die Transaktion automatisch verworfen, damit die Redis-Verbindung weiterhin genutzt werden kann.

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a>Erstellen einer Transaktion mit C# und dem ServiceStack.Redis-Client

Das folgende Beispiel zeigt die Verwendung von ServiceStack.Redis zum Erstellen einer Transaktion, die eine Nachricht senden kann, die eine Bild-URL und den Inhalt einer Textnachricht enthält.

```csharp
public bool SendPictureAndText(string groupChatID, string text, string pictureURL)
{
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, pictureURL));
        transaction.QueueCommand(c => c.PublishMessage(groupChatID, text));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    return transactionResult;
}
```

Transaktionen stellen sicher, dass mehrere Vorgänge zusammen ohne Vorgänge von anderen Clients zwischen diesen ausgeführt werden. Sie können eine Transaktion mit dem Befehl `MULTI` erstellen. Bei ServiceStack.Redis verwenden Sie die Methode `CreateTransaction()`.