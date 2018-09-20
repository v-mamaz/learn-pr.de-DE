<span data-ttu-id="235cf-101">Hier fügen Sie unseren Daten im Azure Redis Cache eine Ablaufzeit hinzu.</span><span class="sxs-lookup"><span data-stu-id="235cf-101">Here, you'll add an expiration time to our data in the Azure Redis Cache.</span></span>

## <a name="add-an-expiration-time"></a><span data-ttu-id="235cf-102">Hinzufügen einer Ablaufzeit</span><span class="sxs-lookup"><span data-stu-id="235cf-102">Add an expiration time</span></span>

<span data-ttu-id="235cf-103">Die letzte Übung haben wir mit dem folgenden Code in **Program.cs** abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="235cf-103">In the last exercise, we left off with the following code in **Program.cs**.</span></span>

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

<span data-ttu-id="235cf-104">Fügen Sie nun eine Gültigkeitsdauer von 15 Sekunden zu **MyKey1** und **MyKey2** hinzu.</span><span class="sxs-lookup"><span data-stu-id="235cf-104">Let’s add an expiration of 15 seconds to both **MyKey1** and **MyKey2**.</span></span>

<span data-ttu-id="235cf-105">Fügen Sie den folgenden Code hinzu, bevor Sie die Transaktion committen:</span><span class="sxs-lookup"><span data-stu-id="235cf-105">Add the following code before you commit the transaction:</span></span>

```csharp
//Add an expiration time
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey1", 15));
transaction.QueueCommand(c => ((RedisNativeClient)c).Expire("MyKey2", 15));
```

<span data-ttu-id="235cf-106">In diesem Code ist die **Expire**-Methode ein Teil von **RedisNativeClient**.</span><span class="sxs-lookup"><span data-stu-id="235cf-106">In this code, the **Expire** method is a part of the **RedisNativeClient**.</span></span> <span data-ttu-id="235cf-107">Um auf die Methode zugreifen zu können, müssen wir zunächst das-Objekt umwandeln.</span><span class="sxs-lookup"><span data-stu-id="235cf-107">To access the method, we must first cast our object.</span></span>

## <a name="verify-the-expiration"></a><span data-ttu-id="235cf-108">Überprüfen der Ablaufzeit</span><span class="sxs-lookup"><span data-stu-id="235cf-108">Verify the expiration</span></span>

<span data-ttu-id="235cf-109">Nachdem Sie den Code hinzugefügt haben, der für den Ablauf unserer Daten zuständig ist, führen sie das Programm aus und überprüfen, ob die Daten aus dem Azure Redis Cache entfernt wurden.</span><span class="sxs-lookup"><span data-stu-id="235cf-109">Now that we added the code to expire our data, let's run the program and check that the data is removed from Azure Redis Cache.</span></span>

1. <span data-ttu-id="235cf-110">Führen Sie das Programm aus.</span><span class="sxs-lookup"><span data-stu-id="235cf-110">Run the program.</span></span>

    ```bash
    dotnet run
    ```

1. <span data-ttu-id="235cf-111">Wechseln Sie im Azure-Portal zurück zur Azure Redis Cache-Konsole.</span><span class="sxs-lookup"><span data-stu-id="235cf-111">Switch back to the Azure Redis Cache console in the Azure portal.</span></span>

1. <span data-ttu-id="235cf-112">Um sicherzustellen, dass die Daten noch immer vorhanden sind, geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="235cf-112">To verify that the data is still there, issue the following command:</span></span>

    ```console
    get MyKey1
    ```

1. <span data-ttu-id="235cf-113">Geben Sie den Befehl nach 15 Sekunden erneut aus.</span><span class="sxs-lookup"><span data-stu-id="235cf-113">After 15 seconds, issue the command again.</span></span> <span data-ttu-id="235cf-114">Sie sollten sehen, dass die Daten nicht mehr vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="235cf-114">You should see that the data is no longer there.</span></span>

    ![Screenshot der Azure Redis Cache-Konsole, „MyKey1“ ist NULL.](../media/6-redis-console-data-expiration.png)