Hier fügen Sie unseren Daten im Azure Redis Cache eine Ablaufzeit hinzu.

## <a name="add-an-expiration-time"></a>Hinzufügen einer Ablaufzeit

Die letzte Übung haben wir mit dem folgenden Code in **Program.cs** abgeschlossen.

```csharp
bool transactionResult = false;

using (RedisClient redisClient = new RedisClient(redisConnectionString))
using (var transaction = redisClient.CreateTransaction())
{
    //Add multiple operations to the transaction
    transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
    transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

    //Commit and get result of transaction
    transactionResult = transaction.Commit();
}

if(transactionResult)
{
    Console.WriteLine("Transaction committed");
}
else
{
    Console.WriteLine("Transaction failed to commit");
}
```

Fügen Sie nun eine Gültigkeitsdauer von 15 Sekunden zu **MyKey1** und **MyKey2** hinzu.

Fügen Sie den folgenden Code hinzu, bevor Sie die Transaktion committen:

```csharp
//Add an expiration time
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
```

In diesem Code ist die **Expire**-Methode ein Teil von **RedisNativeClient**. Um auf die Methode zugreifen zu können, müssen wir zunächst das-Objekt umwandeln.

## <a name="verify-the-expiration"></a>Überprüfen der Ablaufzeit

Nachdem Sie den Code hinzugefügt haben, der für den Ablauf unserer Daten zuständig ist, führen sie das Programm aus und überprüfen, ob die Daten aus dem Azure Redis Cache entfernt wurden.

1. Führen Sie das Programm aus.

    ```bash
    dotnet run
    ```

1. Wechseln Sie im Azure-Portal zurück zur Azure Redis Cache-Konsole.

1. Um sicherzustellen, dass die Daten noch immer vorhanden sind, geben Sie den folgenden Befehl ein:

    ```console
    get MyKey1
    ```

1. Geben Sie den Befehl nach 15 Sekunden erneut aus. Sie sollten sehen, dass die Daten nicht mehr vorhanden sind.

    ![Screenshot der Azure Redis Cache-Konsole, „MyKey1“ ist NULL.](../media/6-redis-console-data-expiration.png)