<span data-ttu-id="a26a0-101">In manchen Fällen müssen Sie sicherstellen, dass mehrere Vorgänge gemeinsam ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a26a0-101">There are times where you must guarantee that multiple operations execute together.</span></span> <span data-ttu-id="a26a0-102">In Ihrer Instant Messaging-Anwendung können Benutzer beispielsweise ein einzelnes Bild, eine individuelle Textnachricht oder ein Bild und eine Textnachricht zusammen senden.</span><span class="sxs-lookup"><span data-stu-id="a26a0-102">For example, in your instant messaging application, users can send: an individual picture, an individual text message, or a picture and text message together.</span></span> <span data-ttu-id="a26a0-103">Wenn der Benutzer sich dafür entscheidet, ein Bild und eine Textnachricht zusammen zu senden, müssen wir sicherstellen, dass andere Mitglieder der Gruppe beide Elemente gleichzeitig empfangen.</span><span class="sxs-lookup"><span data-stu-id="a26a0-103">When the user chooses to send a picture and text message together, we must ensure that other members of the group receive them at the same time.</span></span> <span data-ttu-id="a26a0-104">Dies ist wichtig, denn wenn ein Bild und eine Textnachricht nicht zusammen empfangen werden, ist es möglich, dass zwischen dem Bild und der Textnachricht eine separate Nachricht gesendet wird, wodurch die gesamte Unterhaltung verwirrend werden könnte.</span><span class="sxs-lookup"><span data-stu-id="a26a0-104">This is important because if a picture and text message are not received together, it’s possible that a separate message could be sent in between the picture and text message, which could make the overall conversation confusing.</span></span>

<span data-ttu-id="a26a0-105">Im Folgenden wird erläutert, wie Sie eine Transaktion in Redis erstellen, um sicherzustellen, dass mehrere Vorgänge gemeinsam ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a26a0-105">Here, we'll look at how to create a transaction in Redis to guarantee multiple operations are executed together.</span></span>

## <a name="how-to-create-a-transaction"></a><span data-ttu-id="a26a0-106">Erstellen einer Transaktion</span><span class="sxs-lookup"><span data-stu-id="a26a0-106">How to create a transaction</span></span>

<span data-ttu-id="a26a0-107">Um eine Transaktion zu erstellen, benötigen Sie einen Transaktionsblock.</span><span class="sxs-lookup"><span data-stu-id="a26a0-107">To create a transaction, you need to have a transaction block.</span></span> <span data-ttu-id="a26a0-108">Dies ist eine Warteschlange, die die Befehle enthält, die zusammen ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a26a0-108">This is a queue that contains the commands that will be executed together.</span></span> <span data-ttu-id="a26a0-109">Der Befehl `MULTI` wird verwendet, um einen Transaktionsblock zu erstellen, und alle nachfolgenden Befehle werden für die atomische Ausführung in der Warteschlange gespeichert.</span><span class="sxs-lookup"><span data-stu-id="a26a0-109">The `MULTI` command is used to create a transaction block and all subsequent commands are queued for atomic execution.</span></span>

## <a name="how-to-execute-a-transaction"></a><span data-ttu-id="a26a0-110">Ausführen einer Transaktion</span><span class="sxs-lookup"><span data-stu-id="a26a0-110">How to execute a transaction</span></span>

<span data-ttu-id="a26a0-111">Um die Befehle in einem Transaktionsblock auszuführen, verwenden Sie den Befehl `EXEC`.</span><span class="sxs-lookup"><span data-stu-id="a26a0-111">To execute the commands in a transaction block, you use the `EXEC` command.</span></span> <span data-ttu-id="a26a0-112">Dadurch werden alle Befehle in der Warteschlange ausgeführt, und der normale Verbindungszustand wird wiederhergestellt.</span><span class="sxs-lookup"><span data-stu-id="a26a0-112">This will execute all queued commands and restore the connection state to normal.</span></span> <span data-ttu-id="a26a0-113">Wenn Sie sich entscheiden, keine Transaktion auszuführen, können Sie den Befehl `DISCARD` verwenden, der den Transaktionsblock löscht und den Verbindungsstatus auf normal festlegt.</span><span class="sxs-lookup"><span data-stu-id="a26a0-113">If you decide you don't want to execute a transaction, you can use the `DISCARD` command, which will clear out the transaction block and set the connection state to normal.</span></span>

<span data-ttu-id="a26a0-114">Ein wichtiger Aspekt, den Sie bei Redis-Transaktionen beachten sollten, ist, dass sie keine Rollbacks unterstützen.</span><span class="sxs-lookup"><span data-stu-id="a26a0-114">One important thing to understand about Redis transactions is that they don't support rollbacks.</span></span> <span data-ttu-id="a26a0-115">Das bedeutet, dass die restlichen Befehle weiterhin ausgeführt werden, wenn ein Befehl innerhalb einer Transaktion fehlschlägt.</span><span class="sxs-lookup"><span data-stu-id="a26a0-115">This means that if a command inside a transaction fails, the remaining commands will still be executed.</span></span>

## <a name="what-is-servicestackredis"></a><span data-ttu-id="a26a0-116">Was ist ServiceStack.Redis?</span><span class="sxs-lookup"><span data-stu-id="a26a0-116">What is ServiceStack.Redis?</span></span>

<span data-ttu-id="a26a0-117">Im vorherigen Modul **Optimieren einer Webanwendung durch Zwischenspeichern von schreibgeschützten Daten mit Redis** haben wir den **StackExchange.Redis**-Client verwendet.</span><span class="sxs-lookup"><span data-stu-id="a26a0-117">In the previous module, **Optimize your web application by caching read-only data with Redis** we used the **StackExchange.Redis** client.</span></span> <span data-ttu-id="a26a0-118">Hier möchten wir einen anderen beliebten Client testen: **ServiceStack.Redis**.</span><span class="sxs-lookup"><span data-stu-id="a26a0-118">Here, we're going to try out another popular client, **ServiceStack.Redis**.</span></span>

<span data-ttu-id="a26a0-119">**ServiceStack.Redis** ist eine C#-Clientbibliothek für die Interaktion mit einem Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="a26a0-119">**ServiceStack.Redis** is a C# client library for interacting with a Redis cache.</span></span> <span data-ttu-id="a26a0-120">Das bedeutet, dass wir anstelle von Low-Level-Redis-Befehlen C#-Klassen und -Methoden verwenden können.</span><span class="sxs-lookup"><span data-stu-id="a26a0-120">This means that instead of using low-level Redis commands, we can use C# classes and methods.</span></span>

<span data-ttu-id="a26a0-121">Um beispielsweise eine Transaktion zu erstellen, müssen wir normalerweise den Redis-Befehl `MULTI` verwenden.</span><span class="sxs-lookup"><span data-stu-id="a26a0-121">For example, to create a transaction, we normally must use the Redis `MULTI` command.</span></span> <span data-ttu-id="a26a0-122">Mit **ServiceStack.Redis** können wir jedoch eine Transaktion mit der `CreateTransaction()`-Methode erstellen.</span><span class="sxs-lookup"><span data-stu-id="a26a0-122">However, using **ServiceStack.Redis** we can create a transaction using the `CreateTransaction()` method.</span></span>

```csharp
var transaction = redisClient.CreateTransaction();
```

## <a name="create-a-transaction-using-c-and-the-servicestackredis-client"></a><span data-ttu-id="a26a0-123">Erstellen einer Transaktion mit C# und dem ServiceStack.Redis-Client</span><span class="sxs-lookup"><span data-stu-id="a26a0-123">Create a transaction using C# and the ServiceStack.Redis client</span></span>

<span data-ttu-id="a26a0-124">Das folgende Beispiel zeigt die Verwendung von **ServiceStack.Redis** zum Erstellen einer Transaktion, die eine Nachricht senden kann, die ein Bild und Text enthält.</span><span class="sxs-lookup"><span data-stu-id="a26a0-124">Here's an example of using **ServiceStack.Redis** to create a transaction that can send a message that includes a picture and text.</span></span>

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
<span data-ttu-id="a26a0-125">Transaktionen stellen sicher, dass mehrere Vorgänge zusammen ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a26a0-125">Transactions ensure that multiple operations are executed together.</span></span> <span data-ttu-id="a26a0-126">Sie erstellen eine Transaktion mit dem Befehl `MULTI`, aber mithilfe einer Client-Bibliothek wie **ServiceStack.Redis** können Sie die `CreateTransaction()`-Methode verwenden.</span><span class="sxs-lookup"><span data-stu-id="a26a0-126">You create a transaction using the `MULTI` command, however, using a client library like **ServiceStack.Redis**, you can use the `CreateTransaction()` method.</span></span>