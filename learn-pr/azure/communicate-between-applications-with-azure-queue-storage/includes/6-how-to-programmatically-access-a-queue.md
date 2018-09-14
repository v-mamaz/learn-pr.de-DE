<span data-ttu-id="6d1c2-101">Warteschlangen speichern Nachrichten – Datenpakete, deren Form Sender und Empfänger bekannt ist.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-101">Queues hold messages - packets of data whose shape is known to the sender and receiver.</span></span> <span data-ttu-id="6d1c2-102">Der Sender erstellt die Warteschlange und fügt eine Nachricht hinzu.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-102">The sender creates the queue and adds a message.</span></span> <span data-ttu-id="6d1c2-103">Der Empfänger empfängt eine Nachricht, verarbeitet sie und löscht dann die Nachricht aus der Warteschlange.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-103">The receiver retrieves a message, processes it, and then deletes the message from the queue.</span></span> <span data-ttu-id="6d1c2-104">Die folgende Abbildung zeigt einen typischen Fluss dieses Prozesses.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-104">The following illustration shows a typical flow of this process.</span></span>

![Abbildung eines typischen Nachrichtenflusses durch die Azure-Warteschlange.](../media/6-message-flow.png)

<span data-ttu-id="6d1c2-106">Beachten Sie, dass `get` und `delete` separate Vorgänge sind.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-106">Notice that `get` and `delete` are separate operations.</span></span> <span data-ttu-id="6d1c2-107">In dieser Anordnung werden potenzielle Ausfälle im Empfänger behandelt und ein Konzept namens _at-least-once-delivery_ implementiert.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-107">This arrangement handles potential failures in the receiver and implements a concept called _at-least-once delivery_.</span></span> <span data-ttu-id="6d1c2-108">Nachdem der Empfänger eine Nachricht erhalten hat, verbleibt die Nachricht in der Warteschlange, ist jedoch 30 Sekunden lang unsichtbar.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-108">After the receiver gets a message, that message remains in the queue but is invisible for 30 seconds.</span></span> <span data-ttu-id="6d1c2-109">Wenn der Empfänger abstürzt oder dort während der Verarbeitung ein Stromausfall auftritt, wird die Nachricht dadurch niemals aus der Warteschlange entfernt.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-109">If the receiver crashes or experiences a power failure during processing, then it will never delete the message from the queue.</span></span> <span data-ttu-id="6d1c2-110">Nach 30 Sekunden wird die Nachricht erneut in der Warteschlange angezeigt, und eine andere Instanz des Empfängers kann sie abschließend verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-110">After 30 seconds, the message will reappear in the queue and another instance of the receiver can process it to completion.</span></span>

## <a name="the-azure-storage-client-library-for-net"></a><span data-ttu-id="6d1c2-111">Die Azure-Speicherclientbibliothek für .NET</span><span class="sxs-lookup"><span data-stu-id="6d1c2-111">The Azure Storage Client Library for .NET</span></span>

<span data-ttu-id="6d1c2-112">Die **Azure-Speicherclientbibliothek für .NET** bietet Typen zur Darstellung aller Objekte, mit denen Sie interagieren müssen:</span><span class="sxs-lookup"><span data-stu-id="6d1c2-112">The **Azure Storage Client Library for .NET** provides types to represent each of the objects you need to interact with:</span></span>

- <span data-ttu-id="6d1c2-113">`CloudStorageAccount` stellt Ihr Azure-Speicherkonto dar.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-113">`CloudStorageAccount` represents your Azure storage account.</span></span>
- <span data-ttu-id="6d1c2-114">`CloudQueueClient` stellt Ihre Azure-Warteschlange dar.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-114">`CloudQueueClient` represents Azure Queue storage.</span></span>
- <span data-ttu-id="6d1c2-115">`CloudQueue` stellt eine Ihrer Warteschlangeninstanzen dar.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-115">`CloudQueue` represents one of your queue instances.</span></span>
- <span data-ttu-id="6d1c2-116">`CloudQueueMessage` stellt eine Nachricht dar.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-116">`CloudQueueMessage` represents a message.</span></span>

<span data-ttu-id="6d1c2-117">Sie verwenden diese Klassen zum programmgesteuerten Zugriff auf Ihre Warteschlange.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-117">You will use these classes to get programmatic access to your queue.</span></span> <span data-ttu-id="6d1c2-118">Die Bibliothek enthält synchrone und asynchrone Methoden; Sie sollten die asynchronen Versionen verwenden, um ein Blockieren der Client-App zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-118">The library has both synchronous and asynchronous methods; you should prefer to use the asynchronous versions to avoid blocking the client app.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1c2-119">Die Azure-Speicherclientbibliothek für .NET finden Sie im **WindowsAzure.Storage**-NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-119">The Azure Storage Client Library for .NET is available in the **WindowsAzure.Storage** NuGet package.</span></span> <span data-ttu-id="6d1c2-120">Sie können sie über eine IDE, die Azure-Befehlszeilenschnittstelle oder PowerShell `Install-Package WindowsAzure.Storage` installieren.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-120">You can install it through an IDE, Azure CLI, or through PowerShell `Install-Package WindowsAzure.Storage`.</span></span>

## <a name="how-to-connect-to-a-queue"></a><span data-ttu-id="6d1c2-121">Herstellen einer Verbindung mit einer Warteschlange</span><span class="sxs-lookup"><span data-stu-id="6d1c2-121">How to connect to a queue</span></span>

<span data-ttu-id="6d1c2-122">Um eine Verbindung mit einer Warteschlange herzustellen, erstellen Sie zunächst ein `CloudStorageAccount` mit Ihrer Verbindungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-122">To connect to a queue, you first create a `CloudStorageAccount` with your connection string.</span></span> <span data-ttu-id="6d1c2-123">Das resultierende Objekt kann dann einen `CloudQueueClient` erstellen, der wiederum eine `CloudQueue`-Instanz öffnen kann.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-123">The resulting object can then create a `CloudQueueClient`, which in turn can open a `CloudQueue` instance.</span></span> <span data-ttu-id="6d1c2-124">Der grundlegende Codefluss ist unten dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-124">The basic code flow is shown below.</span></span>

```csharp
CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudQueueClient client = account.CreateCloudQueueClient();

CloudQueue queue = client.GetQueueReference("myqueue");
```

<span data-ttu-id="6d1c2-125">Das Erstellen einer `CloudQueue` bedeutet nicht unbedingt, dass die _tatsächliche_ Speicherwarteschlange vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-125">Creating a `CloudQueue` doesn't necessarily mean the _actual_ storage queue exists.</span></span> <span data-ttu-id="6d1c2-126">Allerdings können Sie mit diesem Objekt eine Warteschlange erstellen, löschen und prüfen, ob eine Warteschlange vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-126">However, you can use this object to create, delete, and check for an existing queue.</span></span> <span data-ttu-id="6d1c2-127">Wie oben erwähnt, unterstützen alle Methoden sowohl synchrone als auch asynchrone Versionen, aber wir verwenden nur die `Task`-basierten asynchronen Versionen.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-127">As mentioned above, all methods support both synchronous and asynchronous versions, but we will only be using the `Task`-based asynchronous versions.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="6d1c2-128">Erstellen von Warteschlangen</span><span class="sxs-lookup"><span data-stu-id="6d1c2-128">How to create a queue</span></span>

<span data-ttu-id="6d1c2-129">Sie verwenden ein allgemeines Muster für die Warteschlangenerstellung: Die Senderanwendung sollte immer für das Erstellen der Warteschlange verantwortlich sein.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-129">You will use a common pattern for queue creation: the sender application should always be responsible for creating the queue.</span></span> <span data-ttu-id="6d1c2-130">Auf diese Weise bleibt Ihre Anwendung eigenständiger und ist weniger abhängig vom Administratorsetup.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-130">This keeps your application more self-contained and less dependent on administrative set-up.</span></span> 

<span data-ttu-id="6d1c2-131">Um die Erstellung zu vereinfachen, macht die Clientbibliothek eine `CreateIfNotExistsAsync`-Methode verfügbar, die ggf. die Warteschlange erstellt oder `false` zurückgibt, wenn die Warteschlange bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-131">To make the creation simple, the client library exposes a `CreateIfNotExistsAsync` method that will create the queue if necessary, or return `false` if the queue already exists.</span></span> 

<span data-ttu-id="6d1c2-132">Der typische Code wird im Folgenden gezeigt.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-132">Typical code is shown below.</span></span>

```csharp
CloudQueue queue;
//...

await queue.CreateIfNotExistsAsync();
```

> [!NOTE]
> <span data-ttu-id="6d1c2-133">Sie benötigen `Write`- oder `Create`-Berechtigungen, damit das Speicherkonto diese API verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-133">You must have `Write` or `Create` permissions for the storage account to use this API.</span></span> <span data-ttu-id="6d1c2-134">Dies ist bei Verwendung des **Zugriffsschlüssel**-Sicherheitsmodells immer zutreffend, aber Sie können Berechtigungen für das Konto mit anderen Ansätzen sperren, die nur Lesevorgänge für die Warteschlange zulassen.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-134">This is always true if you use the **Access Key** security model, but you can lock down permissions to the account with other approaches that will only allow read operations against the queue.</span></span>

## <a name="how-to-send-a-message"></a><span data-ttu-id="6d1c2-135">Senden einer Nachricht</span><span class="sxs-lookup"><span data-stu-id="6d1c2-135">How to send a message</span></span>

<span data-ttu-id="6d1c2-136">Um eine Nachricht zu senden, instanziieren Sie ein `CloudQueueMessage`-Objekt.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-136">To send a message, you instantiate a `CloudQueueMessage` object.</span></span> <span data-ttu-id="6d1c2-137">Die Klasse verfügt über einige überladene Konstruktoren, die Ihre Daten in die Nachricht laden.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-137">The class has a few overloaded constructors that load your data into the message.</span></span> <span data-ttu-id="6d1c2-138">Wir verwenden den Konstruktor, der einen `string` entgegennimmt.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-138">We will use the constructor that takes a `string`.</span></span> <span data-ttu-id="6d1c2-139">Nach dem Erstellen der Nachricht senden Sie sie mit einem `CloudQueue`-Objekt.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-139">After creating the message, you use a `CloudQueue` object to send it.</span></span>

<span data-ttu-id="6d1c2-140">Hier sehen Sie ein typisches Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6d1c2-140">Here's a typical example:</span></span>

```csharp
var message = new CloudQueueMessage("your message here");

CloudQueue queue;
//...

await queue.AddMessageAsync(message);
```

> [!NOTE]
> <span data-ttu-id="6d1c2-141">Die gesamte Warteschlangengröße kann bis zu 500TB betragen, die einzelnen Nachrichten darin können nur bis zu 64KB groß sein (48KB bei Base64-Codierung).</span><span class="sxs-lookup"><span data-stu-id="6d1c2-141">While the total queue size can be up to 500 TB, the individual messages in it can only be up to 64 KB in size (48 KB when using Base64 encoding).</span></span> <span data-ttu-id="6d1c2-142">Wenn Sie eine größere Nutzlast benötigen, können Sie Warteschlangen und Blobs kombinieren – übergeben Sie die URL den (als Blob gespeicherten) eigentlichen Daten in der Nachricht.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-142">If you need a larger payload you can combine queues and blobs – passing the URL to the actual data (stored as a Blob) in the message.</span></span> <span data-ttu-id="6d1c2-143">Mit diesem Ansatz könnten Sie bis zu 200GB für ein einzelnes Element in die Warteschlange einreihen.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-143">This approach would allow you to enqueue up to 200 GB for a single item.</span></span>

## <a name="how-to-receive-and-delete-a-message"></a><span data-ttu-id="6d1c2-144">Empfangen und Löschen einer Nachricht</span><span class="sxs-lookup"><span data-stu-id="6d1c2-144">How to receive and delete a message</span></span>

<span data-ttu-id="6d1c2-145">Im Empfänger erhalten Sie die nächste Nachricht, verarbeiten sie und löschen sie nach erfolgreicher Verarbeitung.</span><span class="sxs-lookup"><span data-stu-id="6d1c2-145">In the receiver, you get the next message, process it, and then delete it after processing succeeds.</span></span> <span data-ttu-id="6d1c2-146">Hier ist ein einfaches Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6d1c2-146">Here's a simple example:</span></span>

```C#
CloudQueue queue;
//...

CloudQueueMessage message = await queue.GetMessageAsync();

if (message != null)
{
    // Process the message
    //...

    await queue.DeleteMessageAsync(message);
}
```

<span data-ttu-id="6d1c2-147">Lassen Sie uns jetzt dieses neuen Wissen auf unsere Anwendung anwenden!</span><span class="sxs-lookup"><span data-stu-id="6d1c2-147">Let's now apply this new knowledge to our application!</span></span>