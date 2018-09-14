Hier fügen Sie eine Ablaufzeit auf unsere Daten in Azure Redis Cache.

## <a name="add-an-expiration-time"></a>Fügen Sie eine Ablaufzeit

In der letzten Übung aufgehört mit den folgenden Code in **"Program.cs"**.

```csharp
using (RedisClient redisClient = new RedisClient(redisConnectionString))
{
    //Create the transaction
    var transaction = redisClient.CreateTransaction();

    //Add multiple operations to the transaction
    transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
    transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

    //Commit and get result of transaction
    var transactionResult = transaction.Commit();

    if(transactionResult)
        Console.WriteLine("Transaction committed");
    else
        Console.WriteLine("Transaction failed to commit");
}
```

Fügen Sie ein Ablaufdatum von 15 Sekunden sowohl **MyKey1** und **MyKey2**.

Fügen Sie den folgenden Code aus, bevor Sie die Transaktion ausführen:

    ```csharp
    //Add an expiration time
    transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
    transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
    ```

In diesem Code wird die **ablaufen** Methode ist ein Teil der **RedisNativeClient**. Um die Methode zugreifen zu können, müssen wir zunächst das-Objekt umwandeln.

## <a name="verify-the-expiration"></a>Überprüfen Sie das Ablaufdatum

Nun, da wir den Code, um die Daten ablaufen hinzugefügt haben, lassen Sie uns das Programm auszuführen, und überprüfen Sie, dass die Daten aus Azure Redis Cache entfernt werden.

1. Führen Sie das Programm aus.

    ```bash
    dotnet run
    ```
    
1. Wechseln Sie zurück in die Azure Redis Cache-Konsole im Azure-Portal.

1. Um sicherzustellen, dass die Daten immer noch vorhanden sind, geben Sie den folgenden Befehl aus:

    ```
    get MyKey1
    ```

1. Geben Sie den Befehl erneut aus, nach 15 Sekunden. Sollte angezeigt werden, dass die Daten nicht mehr vorhanden ist.

    ![Screenshot der Azure Redis Cache-Konsole mit dem Wert des MyKey1, wird NULL](../media/6-redis-console-data-expiration.png)