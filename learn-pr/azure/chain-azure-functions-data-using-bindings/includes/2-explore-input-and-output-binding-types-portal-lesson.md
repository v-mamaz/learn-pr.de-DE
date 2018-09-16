<span data-ttu-id="7c543-101">Das Zugreifen auf und Verarbeiten von Daten sind wichtige Aufgaben in vielen Softwarelösungen.</span><span class="sxs-lookup"><span data-stu-id="7c543-101">Accessing and processing data are key tasks in many software solutions.</span></span> <span data-ttu-id="7c543-102">Betrachten Sie einige dieser Szenarien:</span><span class="sxs-lookup"><span data-stu-id="7c543-102">Consider some of these scenarios:</span></span>

* <span data-ttu-id="7c543-103">Sie wurden gebeten, eine Möglichkeit zu implementieren, eingehende Daten aus dem Blobspeicher in Azure Cosmos DB zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="7c543-103">You've been asked to implement a way to move incoming data from blob storage to Azure Cosmos DB.</span></span>
* <span data-ttu-id="7c543-104">Sie möchten eingehende Nachrichten in einer Warteschlange zur Verarbeitung durch eine andere Komponente in Ihrem Unternehmen speichern.</span><span class="sxs-lookup"><span data-stu-id="7c543-104">You want to post incoming messages to a queue for processing by another component in your enterprise.</span></span>
* <span data-ttu-id="7c543-105">Der Dienst muss Spielergebnisse aus einer Warteschlange abrufen und eine Onlineanzeigetafel aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="7c543-105">Your service needs to grab gamer scores from a queue and update an online scoreboard.</span></span>

<span data-ttu-id="7c543-106">Alle diese Beispiele beschäftigen sich mit dem Verschieben von Daten.</span><span class="sxs-lookup"><span data-stu-id="7c543-106">All of these examples are about moving data.</span></span> <span data-ttu-id="7c543-107">Die Datenquelle und die Ziele unterscheiden sich von Szenario zu Szenario, aber das Muster ist ähnlich.</span><span class="sxs-lookup"><span data-stu-id="7c543-107">The data source and destinations differ from scenario to scenario, but the pattern is similar.</span></span> <span data-ttu-id="7c543-108">Sie stellen eine Verbindung mit einer Datenquelle her, Sie lesen und schreiben Daten.</span><span class="sxs-lookup"><span data-stu-id="7c543-108">You connect to a data source, you read and write data.</span></span> <span data-ttu-id="7c543-109">Azure Functions unterstützt Sie bei der Integration von Daten und Diensten über Bindungen.</span><span class="sxs-lookup"><span data-stu-id="7c543-109">Azure Functions helps you integrate with data and services using bindings.</span></span> 

## <a name="what-is-a-binding"></a><span data-ttu-id="7c543-110">Was ist eine Bindung?</span><span class="sxs-lookup"><span data-stu-id="7c543-110">What is a binding?</span></span>

<span data-ttu-id="7c543-111">In Funktionen bieten Bindungen eine deklarative Möglichkeit, eine Verbindung mit Daten über Ihren Code herzustellen.</span><span class="sxs-lookup"><span data-stu-id="7c543-111">In functions, bindings provide a declarative way to connect to data from within your code.</span></span> <span data-ttu-id="7c543-112">Sie erleichtern die konsistente Integration von Datenströmen in eine Funktion.</span><span class="sxs-lookup"><span data-stu-id="7c543-112">They make it easier to integrate with data streams consistently in a function.</span></span> <span data-ttu-id="7c543-113">Ein Trigger definiert, wie eine Funktion aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="7c543-113">A trigger defines how a function is invoked.</span></span> <span data-ttu-id="7c543-114">Sie können nur einen Trigger verwenden, aber Sie können mehrere Bindungen in einer Funktion haben.</span><span class="sxs-lookup"><span data-stu-id="7c543-114">You can only have one trigger, but you can have multiple bindings in a function.</span></span> <span data-ttu-id="7c543-115">Dies ist leistungsfähig, da Sie sich mit Ihren Datenquellen verbinden können, ohne die Werte hartcodieren zu müssen, z.B. die *Verbindungszeichenfolge*.</span><span class="sxs-lookup"><span data-stu-id="7c543-115">This is powerful because you can connect to your data sources without having to hard code the values, like for instance, the *connection string*.</span></span>

### <a name="two-kinds-of-bindings"></a><span data-ttu-id="7c543-116">Zwei Arten von Bindungen</span><span class="sxs-lookup"><span data-stu-id="7c543-116">Two kinds of bindings</span></span>

<span data-ttu-id="7c543-117">Es gibt zwei Arten von Bindungen, die Sie für Ihre Funktionen verwenden können:</span><span class="sxs-lookup"><span data-stu-id="7c543-117">There are two kinds of bindings you can use for your functions:</span></span>

1. <span data-ttu-id="7c543-118">**Eingabebindung**: Eine Eingabebindung ist eine Verbindung mit einer **Datenquelle**.</span><span class="sxs-lookup"><span data-stu-id="7c543-118">**Input binding** An input binding is a connection to a data **source**.</span></span> <span data-ttu-id="7c543-119">Unsere Funktion liest Daten aus dieser Quelle.</span><span class="sxs-lookup"><span data-stu-id="7c543-119">Our function reads data from this source.</span></span>

1. <span data-ttu-id="7c543-120">**Ausgabebindung**: Eine Ausgabebindung ist eine Verbindung mit einem **Datenziel**.</span><span class="sxs-lookup"><span data-stu-id="7c543-120">**Output binding** An output binding is a connection to a data **destination**.</span></span> <span data-ttu-id="7c543-121">Unsere Funktion schreibt Daten in dieses Ziel.</span><span class="sxs-lookup"><span data-stu-id="7c543-121">Our function writes data to this destination.</span></span>

### <a name="types-of-supported-bindings"></a><span data-ttu-id="7c543-122">Typen von unterstützten Bindungen</span><span class="sxs-lookup"><span data-stu-id="7c543-122">Types of supported bindings</span></span>

<span data-ttu-id="7c543-123">Der *Typ* der Bindung definiert, woraus wir Daten lesen oder wohin wir Daten senden.</span><span class="sxs-lookup"><span data-stu-id="7c543-123">The *type* of binding defines where we are reading or sending data.</span></span> <span data-ttu-id="7c543-124">Es gibt eine Bindung zur Beantwortung von Webanforderungen und eine große Auswahl an Bindungen für die Interaktion mit dem Speicher.</span><span class="sxs-lookup"><span data-stu-id="7c543-124">There is a binding to respond to web requests and a large selection of bindings to interact with storage.</span></span>

<span data-ttu-id="7c543-125">Die folgende Liste führt häufig verwendete Bindungen auf:</span><span class="sxs-lookup"><span data-stu-id="7c543-125">Here's a list of commonly used bindings:</span></span>
- <span data-ttu-id="7c543-126">Blob</span><span class="sxs-lookup"><span data-stu-id="7c543-126">Blob</span></span>
- <span data-ttu-id="7c543-127">Warteschlange</span><span class="sxs-lookup"><span data-stu-id="7c543-127">Queue</span></span>
- <span data-ttu-id="7c543-128">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7c543-128">CosmosDB</span></span>
- <span data-ttu-id="7c543-129">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7c543-129">Event Hubs</span></span>
- <span data-ttu-id="7c543-130">Externe Dateien</span><span class="sxs-lookup"><span data-stu-id="7c543-130">External Files</span></span>
- <span data-ttu-id="7c543-131">Externe Tabellen</span><span class="sxs-lookup"><span data-stu-id="7c543-131">External Tables</span></span>
- <span data-ttu-id="7c543-132">HTTP</span><span class="sxs-lookup"><span data-stu-id="7c543-132">HTTP</span></span>

### <a name="binding-properties"></a><span data-ttu-id="7c543-133">Bindungseigenschaften</span><span class="sxs-lookup"><span data-stu-id="7c543-133">Binding properties</span></span>

<span data-ttu-id="7c543-134">Es gibt vier Eigenschaften, die in allen Bindungen erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="7c543-134">There are four properties that are required in all bindings.</span></span> <span data-ttu-id="7c543-135">Sie müssen möglicherweise zusätzliche Eigenschaften basierend auf dem Typ der verwendeten Bindung und/oder des Speichers angeben.</span><span class="sxs-lookup"><span data-stu-id="7c543-135">You may have to supply additional properties based on the type of binding and/or storage you are using.</span></span>

- <span data-ttu-id="7c543-136">**Name**: Die `name`-Eigenschaft definiert den Funktionsparameter, über den Sie auf die Daten zugreifen.</span><span class="sxs-lookup"><span data-stu-id="7c543-136">**Name** The `name` property defines the function parameter through which you access the data.</span></span> <span data-ttu-id="7c543-137">In einer Warteschlangen-Eingabebindung ist dies z.B. der Name des Funktionsparameters, der den Inhalt der Warteschlangennachricht empfängt.</span><span class="sxs-lookup"><span data-stu-id="7c543-137">For example, in a queue input binding, this is the name of the function parameter that receives the queue message content.</span></span> 

- <span data-ttu-id="7c543-138">**Typ**: Die `type`-Eigenschaft identifiziert den Typ der Bindung, d.h. den Typ der Daten oder des Diensts, mit denen bzw. dem die Interaktion erfolgen soll.</span><span class="sxs-lookup"><span data-stu-id="7c543-138">**Type** The `type` property identifies the type of binding, i.e., the type of data or service we want to interact with.</span></span>

- <span data-ttu-id="7c543-139">**Richtung**: Die `direction`-Eigenschaft identifiziert die Richtung, in die Daten fließen. Sie gibt also an, ob es sich um eine Eingabe- oder Ausgabebindung handelt.</span><span class="sxs-lookup"><span data-stu-id="7c543-139">**Direction** The `direction` property identifies the direction data is flowing ie. is it an input or output binding?</span></span>

- <span data-ttu-id="7c543-140">**Verbindung**: Bei der `connection`-Eigenschaft handelt es sich nicht um die Verbindungszeichenfolge selbst, sondern um den Namen einer App-Einstellung, die die Verbindungszeichenfolge enthält.</span><span class="sxs-lookup"><span data-stu-id="7c543-140">**Connection** The `connection` property is the name of an app setting that contains the connection string, not the connection string itself.</span></span> <span data-ttu-id="7c543-141">Bindungen verwenden Verbindungszeichenfolgen, die in den App-Einstellungen gespeichert sind, um die bewährte Methode durchzusetzen, dass „function.json“ keine Dienstgeheimnisse enthält.</span><span class="sxs-lookup"><span data-stu-id="7c543-141">Bindings use connection strings stored in app settings to enforce the best practice that function.json does not contain service secrets.</span></span>

## <a name="create-a-binding"></a><span data-ttu-id="7c543-142">Erstellen einer Bindung</span><span class="sxs-lookup"><span data-stu-id="7c543-142">Create a binding</span></span>

<span data-ttu-id="7c543-143">Bindungen werden in JSON definiert.</span><span class="sxs-lookup"><span data-stu-id="7c543-143">Bindings are defined in JSON.</span></span> <span data-ttu-id="7c543-144">Eine Bindung wird in der Konfigurationsdatei Ihrer Funktion konfiguriert, die den Namen `function.json` trägt und sich im gleichen Ordner wie Ihr Funktionscode befindet.</span><span class="sxs-lookup"><span data-stu-id="7c543-144">A binding is configured in your function's configuration file, which is named `function.json` and lives in the same folder as your function code.</span></span>

 <span data-ttu-id="7c543-145">Sehen wir uns ein Beispiel für eine *Eingabebindung* an:</span><span class="sxs-lookup"><span data-stu-id="7c543-145">Let's examine a sample of an *input binding*:</span></span>

```json
    ...
    {
      "name": "headshotBlob",
      "type": "blob",
      "path": "thumbnail-images/{filename}",
      "connection": "HeadshotStorageConnection",
      "direction": "in"
    },
    ...
```

<span data-ttu-id="7c543-146">Zum Erstellen dieser Bindung gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="7c543-146">To create this binding we:</span></span>

1. <span data-ttu-id="7c543-147">Erstellen Sie eine Bindung in der Datei `function.json`.</span><span class="sxs-lookup"><span data-stu-id="7c543-147">Create a binding in our `function.json` file.</span></span>

1. <span data-ttu-id="7c543-148">Geben Sie den Wert für die Variable `name` an.</span><span class="sxs-lookup"><span data-stu-id="7c543-148">Provide the value for the `name` variable.</span></span> <span data-ttu-id="7c543-149">In diesem Beispiel enthält die Variable die Blobdaten.</span><span class="sxs-lookup"><span data-stu-id="7c543-149">In this example, the variable will hold the blob data.</span></span>

1. <span data-ttu-id="7c543-150">Geben Sie den Speicher `type` an. Im vorherigen Beispiel verwenden wir Blobspeicher.</span><span class="sxs-lookup"><span data-stu-id="7c543-150">Provide the storage `type`, in the preceding example, we are using Blob storage.</span></span>

1. <span data-ttu-id="7c543-151">Geben Sie den `path` an, der den Container und den Elementnamen angibt, der in ihm gespeichert wird.</span><span class="sxs-lookup"><span data-stu-id="7c543-151">Provide the `path`, which specifies the container and the item name which goes in it.</span></span> <span data-ttu-id="7c543-152">Die `path`-Eigenschaft ist für Blobs erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7c543-152">The `path` property is required for Blobs.</span></span>

1. <span data-ttu-id="7c543-153">Geben Sie den Namen der `connection`-Zeichenfolgeneinstellung an, der in der Datei mit den Einstellungen der Anwendung definiert wurde.</span><span class="sxs-lookup"><span data-stu-id="7c543-153">Provide the `connection` string setting name defined in the application's settings file.</span></span> <span data-ttu-id="7c543-154">Er wird als Suche verwendet, um die Verbindungszeichenfolge für die Verbindung mit Ihrem Speicher zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="7c543-154">It's used as a lookup to find the connection string to connect to your storage.</span></span>

1. <span data-ttu-id="7c543-155">Definieren Sie die `direction` als `in`, damit Daten aus dem Blob gelesen werden.</span><span class="sxs-lookup"><span data-stu-id="7c543-155">Define the `direction` as `in`, it will read data from the Blob.</span></span>

<span data-ttu-id="7c543-156">Bindungen werden verwendet, um Daten mit Ihrer Funktion zu verbinden.</span><span class="sxs-lookup"><span data-stu-id="7c543-156">Bindings are used to connect to data into your function.</span></span> <span data-ttu-id="7c543-157">In dem Beispiel, das wir uns angesehen haben, haben wir eine Eingabebindung verwendet, um Benutzerbilder zu verbinden, die von unserer Funktion als Miniaturansichten verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="7c543-157">In the example we looked at, we used an input binding to connect user images to be processed by our function as thumbnails.</span></span>