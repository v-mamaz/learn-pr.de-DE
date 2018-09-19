<span data-ttu-id="b5550-101">Wie bereits erwähnt, handelt es sich bei Redis um eine In-Memory-NoSQL-Datenbank, die auf mehreren Servern repliziert werden kann.</span><span class="sxs-lookup"><span data-stu-id="b5550-101">As mentioned earlier, Redis is an in-memory NoSQL database which can be replicated across multiple servers.</span></span> <span data-ttu-id="b5550-102">Sie wird häufig als Cache verwendet und kann als formale Datenbank oder sogar Nachrichtenbroker verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b5550-102">It is often used as a cache, but can be used as a formal database or even message-broker.</span></span> 

<span data-ttu-id="b5550-103">Sie kann eine Vielzahl von Datentypen und -strukturen speichern und unterstützt eine Vielzahl von Befehlen, mit denen Sie zwischengespeicherte Daten abrufen oder Informationen zum Cache selbst abfragen können.</span><span class="sxs-lookup"><span data-stu-id="b5550-103">It can store a variety of data types and structures and supports a variety of commands you can issue to retrieve cached data or query information about the cache itself.</span></span> <span data-ttu-id="b5550-104">Die Daten, mit denen Sie arbeiten, werden immer als Schlüssel-Wert-Paare gespeichert.</span><span class="sxs-lookup"><span data-stu-id="b5550-104">The data you work with is always stored as key/value pairs.</span></span>

## <a name="executing-commands-on-the-redis-cache"></a><span data-ttu-id="b5550-105">Ausführen von Befehlen in Redis Cache</span><span class="sxs-lookup"><span data-stu-id="b5550-105">Executing commands on the Redis cache</span></span>

<span data-ttu-id="b5550-106">In der Regel verwendet eine Clientanwendung eine _Clientbibliothek_, um Anforderungen zu erstellen und Befehle für eine Redis Cache-Instanz auszuführen.</span><span class="sxs-lookup"><span data-stu-id="b5550-106">Typically, a client application will use a _client library_ to form requests and execute commands on a Redis cache.</span></span> <span data-ttu-id="b5550-107">Eine Liste von Clientbibliotheken finden Sie direkt auf der Seite zu [Redis-Clients](https://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="b5550-107">You can get a list of client libraries directly from the [Redis clients page](https://redis.io/clients).</span></span> <span data-ttu-id="b5550-108">Ein beliebter leistungsstarker Redis-Client für die .NET-Sprache ist **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="b5550-108">A popular high-performance Redis client for the .NET language is **StackExchange.Redis**.</span></span> <span data-ttu-id="b5550-109">Das Paket ist über NuGet verfügbar und kann Ihrem .NET-Code mithilfe der Befehlszeile oder der IDE hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="b5550-109">The package is available through NuGet and can be added to your .NET code using the command line or IDE.</span></span>

### <a name="connecting-to-your-redis-cache-with-stackexchangeredis"></a><span data-ttu-id="b5550-110">Herstellen einer Verbindung mit Redis Cache mit „StackExchange.Redis“</span><span class="sxs-lookup"><span data-stu-id="b5550-110">Connecting to your Redis cache with StackExchange.Redis</span></span>

<span data-ttu-id="b5550-111">Denken Sie daran, dass wir die Hostadresse, die Portnummer und einen Zugriffsschlüssel verwenden, um eine Verbindung mit einem Redis-Server herzustellen.</span><span class="sxs-lookup"><span data-stu-id="b5550-111">Recall that we use the host address, port number, and an access key to connect to a Redis server.</span></span> <span data-ttu-id="b5550-112">Darüber hinaus bietet Azure eine _Verbindungszeichenfolge_ für einige Redis-Clients, die diese Daten zusammen in einer einzelnen Zeichenfolge bündeln.</span><span class="sxs-lookup"><span data-stu-id="b5550-112">Azure also offers a _connection string_ for some Redis clients which bundles this data together into a single string.</span></span>

### <a name="what-is-a-connection-string"></a><span data-ttu-id="b5550-113">Was ist eine Verbindungszeichenfolge?</span><span class="sxs-lookup"><span data-stu-id="b5550-113">What is a connection string?</span></span>

<span data-ttu-id="b5550-114">Eine Verbindungszeichenfolge ist eine einzelne Textzeile, die alle erforderlichen Informationen enthält, um eine Verbindung mit einer Redis Cache-Instanz in Azure herzustellen und sich bei dieser zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="b5550-114">A connection string is a single line of text that includes all the required pieces of information to connect and authenticate to a Redis cache in Azure.</span></span> <span data-ttu-id="b5550-115">Diese sieht etwa wie folgt aus (wobei die Felder **cache-name** und **password-here** mit den tatsächlichen Werten aufgefüllt sind):</span><span class="sxs-lookup"><span data-stu-id="b5550-115">It will look something like the following (with the **cache-name** and **password-here** fields filled in with real values):</span></span>

```
[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False
```

> [!TIP]
> <span data-ttu-id="b5550-116">Die Verbindungszeichenfolge in Ihrer Anwendung sollte geschützt sein.</span><span class="sxs-lookup"><span data-stu-id="b5550-116">The connection string should be protected in your application.</span></span> <span data-ttu-id="b5550-117">Wenn die Anwendung in Azure gehostet wird, sollten Sie den Wert eventuell mit Azure Key Vault speichern.</span><span class="sxs-lookup"><span data-stu-id="b5550-117">If the application is hosted on Azure, consider using an Azure Key Vault to store the value.</span></span>

<span data-ttu-id="b5550-118">Sie können diese Zeichenfolge an **StackExchange.Redis** übergeben, um eine Verbindung mit dem Server herzustellen.</span><span class="sxs-lookup"><span data-stu-id="b5550-118">You can pass this string to **StackExchange.Redis** to create a connection the server.</span></span> 

<span data-ttu-id="b5550-119">Beachten Sie, dass zwei zusätzliche Parameter am Ende angefügt sind:</span><span class="sxs-lookup"><span data-stu-id="b5550-119">Notice that there are two additional parameters at the end:</span></span> 

- <span data-ttu-id="b5550-120">**ssl**: Stellt sicher, dass die Kommunikation verschlüsselt ist.</span><span class="sxs-lookup"><span data-stu-id="b5550-120">**ssl** - ensures that communication is encrypted.</span></span>
- <span data-ttu-id="b5550-121">**abortConnection**: Ermöglicht das Herstellen einer Verbindung, auch wenn der Server zum jeweiligen Zeitpunkt nicht verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="b5550-121">**abortConnection** - allows a connection to be created even if the server is unavailable at that moment.</span></span>

<span data-ttu-id="b5550-122">Es gibt andere [optionale Parameter](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options), die Sie an die Zeichenfolge anfügen können, um die Clientbibliothek zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="b5550-122">There are several other [optional parameters](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options) you can append to the string to configure the client library.</span></span>

### <a name="creating-a-connection"></a><span data-ttu-id="b5550-123">Erstellen einer Verbindung</span><span class="sxs-lookup"><span data-stu-id="b5550-123">Creating a connection</span></span>

<span data-ttu-id="b5550-124">Das wichtigste Verbindungsobjekt in **StackExchange.Redis** ist die Klasse `StackExchange.Redis.ConnectionMultiplexer`.</span><span class="sxs-lookup"><span data-stu-id="b5550-124">The main connection object in **StackExchange.Redis** is the `StackExchange.Redis.ConnectionMultiplexer` class.</span></span> <span data-ttu-id="b5550-125">Dieses Objekt abstrahiert den Prozess beim Herstellen einer Verbindung mit einem Redis-Server (oder einer Gruppe von Servern).</span><span class="sxs-lookup"><span data-stu-id="b5550-125">This object abstracts the process of connecting to a Redis server (or group of servers).</span></span> <span data-ttu-id="b5550-126">Dieses wurde für die effiziente Verwaltung von Verbindungen optimiert und muss bestehen bleiben, solange Sie auf den Cache zugreifen müssen.</span><span class="sxs-lookup"><span data-stu-id="b5550-126">It's optimized to manage connections efficiently and intended to be kept around while you need access to the cache.</span></span>

<span data-ttu-id="b5550-127">Sie erstellen eine `ConnectionMultiplexer`-Instanz mit der statischen `ConnectionMultiplexer.Connect`- oder `ConnectionMultiplexer.ConnectAsync`-Methode, indem Sie eine Verbindungszeichenfolge oder ein `ConfigurationOptions`-Objekt übergeben.</span><span class="sxs-lookup"><span data-stu-id="b5550-127">You create a `ConnectionMultiplexer` instance using the static `ConnectionMultiplexer.Connect` or `ConnectionMultiplexer.ConnectAsync` method, passing in either a connection string or a `ConfigurationOptions` object.</span></span> 

<span data-ttu-id="b5550-128">Im Folgenden finden Sie ein einfaches Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b5550-128">Here's a simple example:</span></span>

```csharp
using StackExchange.Redis;
...
var connectionString = "[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
    // ^^^ store and re-use this!!!
```

<span data-ttu-id="b5550-129">Wenn Sie über `ConnectionMultiplexer` verfügen, gibt es drei primäre Punkte, die Sie tun sollten:</span><span class="sxs-lookup"><span data-stu-id="b5550-129">Once you have a `ConnectionMultiplexer`, there are 3 primary things you might want to do:</span></span>

1. <span data-ttu-id="b5550-130">Zugreifen auf eine Redis-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="b5550-130">Access a Redis Database.</span></span> <span data-ttu-id="b5550-131">Dies ist der Punkt, auf den wir uns im vorliegenden Artikel konzentrieren werden.</span><span class="sxs-lookup"><span data-stu-id="b5550-131">This is what we will focus on here.</span></span>
2. <span data-ttu-id="b5550-132">Verwenden Sie die Features von Redis zum Herausgeben bzw. Anfordern eines Abonnements.</span><span class="sxs-lookup"><span data-stu-id="b5550-132">Make use of the publisher/subscript features of Redis.</span></span> <span data-ttu-id="b5550-133">Diese liegen außerhalb des Bereichs dieses Moduls.</span><span class="sxs-lookup"><span data-stu-id="b5550-133">This is outside the scope of this module.</span></span>
3. <span data-ttu-id="b5550-134">Greifen Sie für Wartungs- oder Überwachungszwecke auf einen einzelnen Server zu.</span><span class="sxs-lookup"><span data-stu-id="b5550-134">Access an individual server for maintenance or monitoring purposes.</span></span>

### <a name="accessing-a-redis-database"></a><span data-ttu-id="b5550-135">Zugreifen auf eine Redis-Datenbank</span><span class="sxs-lookup"><span data-stu-id="b5550-135">Accessing a Redis database</span></span>

<span data-ttu-id="b5550-136">Die Redis-Datenbank wird durch den Typ `IDatabase` dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b5550-136">The Redis database is represented by the `IDatabase` type.</span></span> <span data-ttu-id="b5550-137">Diesen können Sie mithilfe der Methode `GetDatabase()` abrufen:</span><span class="sxs-lookup"><span data-stu-id="b5550-137">You can retrieve one using the `GetDatabase()` method:</span></span>

```csharp
IDatabase db = redisConnection.GetDatabase();
```

> [!TIP]
> <span data-ttu-id="b5550-138">Das von `GetDatabase` zurückgegebene Objekt ist ein einfaches Objekt und muss nicht gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="b5550-138">The object returned from `GetDatabase` is a lightweight object, and does not need to be stored.</span></span> <span data-ttu-id="b5550-139">Nur `ConnectionMultiplexer` muss erhalten werden.</span><span class="sxs-lookup"><span data-stu-id="b5550-139">Only the `ConnectionMultiplexer` needs to be kept alive.</span></span>

<span data-ttu-id="b5550-140">Wenn Sie über das Objekt `IDatabase` verfügen, können Sie Methoden für die Interaktion mit dem Cache ausführen.</span><span class="sxs-lookup"><span data-stu-id="b5550-140">Once you have a `IDatabase` object, you can execute methods to interact with the cache.</span></span> <span data-ttu-id="b5550-141">Alle Methoden weisen synchrone und asynchrone Versionen auf, die `Task`-Objekte zurückgeben, damit sie mit den Schlüsselwörtern `async` und `await` kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="b5550-141">All methods have synchronous and asynchronous versions which return `Task` objects to make them compatible with the `async` and `await` keywords.</span></span>

<span data-ttu-id="b5550-142">Im Folgenden finden Sie ein Beispiel zum Speichern eines Schlüssel-Wert-Paares im Cache:</span><span class="sxs-lookup"><span data-stu-id="b5550-142">Here is an example of storing a key/value in the cache:</span></span>

```csharp
bool wasSet = db.StringSet("favorite:flavor", "i-love-rocky-road");
```

<span data-ttu-id="b5550-143">Die Methode `StringSet` gibt `bool` zurück, was darauf hinweist, dass der Wert festgelegt (`true`) oder nicht festgelegt (`false`) wurde.</span><span class="sxs-lookup"><span data-stu-id="b5550-143">The `StringSet` method returns a `bool` indicating whether the value was set (`true`) or not (`false`).</span></span> <span data-ttu-id="b5550-144">Anschließend kann der Wert mit der Methode `StringGet` abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="b5550-144">We can then retrieve the value with the `StringGet` method:</span></span>

```csharp
string value = db.StringGet("favorite:flavor");
Console.WriteLine(value); // displays: ""i-love-rocky-road""
```

#### <a name="getting-and-setting-binary-values"></a><span data-ttu-id="b5550-145">Abrufen und Festlegen von Binärwerten</span><span class="sxs-lookup"><span data-stu-id="b5550-145">Getting and Setting binary values</span></span>

<span data-ttu-id="b5550-146">Denken Sie daran, dass Redis-Schlüssel und -Werte  _binärsicher_ sind.</span><span class="sxs-lookup"><span data-stu-id="b5550-146">Recall that Redis keys and values are _binary safe_.</span></span> <span data-ttu-id="b5550-147">Diese Methoden können verwendet werden, um Binärdaten zu speichern.</span><span class="sxs-lookup"><span data-stu-id="b5550-147">These same methods can be used to store binary data.</span></span> <span data-ttu-id="b5550-148">Mithilfe impliziter Konvertierungsoperatoren für `byte[]`-Typen können Sie unkompliziert mit den Daten arbeiten:</span><span class="sxs-lookup"><span data-stu-id="b5550-148">There are implicit conversion operators to work with `byte[]` types so you can work with the data naturally:</span></span>

```csharp
byte[] key = ...;
byte[] value = ...;

db.StringSet(key, value);
```

```csharp
byte[] key = ...;
byte[] value = db.StringGet(key);
```

> [!TIP]
> <span data-ttu-id="b5550-149">**StackExchange.Redis** stellt Schlüssel mithilfe des Typs `RedisKey` dar.</span><span class="sxs-lookup"><span data-stu-id="b5550-149">**StackExchange.Redis** represents keys using the `RedisKey` type.</span></span> <span data-ttu-id="b5550-150">Diese Klasse weist implizite Konvertierungen in und von `string` und `byte[]` auf, sodass sowohl Text- als auch Binärschlüssel problemlos verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="b5550-150">This class has implicit conversions to and from both `string` and `byte[]`, allowing both text and binary keys to be used without any complication.</span></span> <span data-ttu-id="b5550-151">Werte werden durch den Typ `RedisValue` dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b5550-151">Values are represented by the `RedisValue` type.</span></span> <span data-ttu-id="b5550-152">Wie bei `RedisKey` stehen Ihnen implizite Konvertierungen zur Verfügung, mit denen Sie `string` oder `byte[]` übergeben können.</span><span class="sxs-lookup"><span data-stu-id="b5550-152">As with `RedisKey`, there are implicit conversions in place to allow you to pass `string` or `byte[]`.</span></span>

#### <a name="other-common-operations"></a><span data-ttu-id="b5550-153">Andere gängige Vorgänge</span><span class="sxs-lookup"><span data-stu-id="b5550-153">Other common operations</span></span>

<span data-ttu-id="b5550-154">Die Schnittstelle `IDatabase` umfasst weitere Methoden für die Arbeit mit Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="b5550-154">The `IDatabase` interface includes several other methods to work with the Redis cache.</span></span> <span data-ttu-id="b5550-155">Es gibt Methoden zum Arbeiten mit Hashes, Listen, Gruppen und sortierten Mengen.</span><span class="sxs-lookup"><span data-stu-id="b5550-155">There are methods to work with hashes, lists, sets, and ordered sets.</span></span>

<span data-ttu-id="b5550-156">Im Folgenden werden gängigere Beispiele vorgestellt, die mit einzelnen Schlüsseln arbeiten. Sie können [den Quellcode](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs) für die Schnittstelle lesen, um die vollständige Liste anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b5550-156">Here are some of the more common ones that work with single keys, you can [read the source code](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs) for the interface to see the full list.</span></span>

| <span data-ttu-id="b5550-157">Methode</span><span class="sxs-lookup"><span data-stu-id="b5550-157">Method</span></span> | <span data-ttu-id="b5550-158">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b5550-158">Description</span></span> |
|--------|-------------|
| `CreateBatch` | <span data-ttu-id="b5550-159">Erstellt eine _Gruppe von Vorgängen_, die an den Server als einzelne Einheit gesendet, jedoch nicht unbedingt als Einheit verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="b5550-159">Creates a _group of operations_ that will be sent to the server as a single unit, but not necessarily processed as a unit.</span></span> |
| `CreateTransaction` | <span data-ttu-id="b5550-160">Erstellt eine Gruppe von Vorgängen, die an den Server als einzelne Einheit gesendet _und_ als einzelne Einheit auf dem Server verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="b5550-160">Creates a group of operations that will be sent to the server as a single unit _and_ processed on the server as a single unit.</span></span> |
| `KeyDelete` | <span data-ttu-id="b5550-161">Löscht das Schlüssel-Wert-Paar.</span><span class="sxs-lookup"><span data-stu-id="b5550-161">Delete the key/value.</span></span> |
| `KeyExists` | <span data-ttu-id="b5550-162">Gibt zurück, ob der angegebene Schlüssel im Cache vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="b5550-162">Returns whether the given key exists in cache.</span></span> |
| `KeyExpire` | <span data-ttu-id="b5550-163">Legt den Ablauf der Gültigkeitsdauer (Time to Live, TTL) eines Schlüssels fest.</span><span class="sxs-lookup"><span data-stu-id="b5550-163">Sets a time-to-live (TTL) expiration on a key.</span></span> |
| `KeyRename` | <span data-ttu-id="b5550-164">Benennt einen Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="b5550-164">Renames a key.</span></span> |
| `KeyTimeToLive` | <span data-ttu-id="b5550-165">Gibt die TTL für einen Schlüssel zurück.</span><span class="sxs-lookup"><span data-stu-id="b5550-165">Returns the TTL for a key.</span></span> |
| `KeyType` | <span data-ttu-id="b5550-166">Gibt die Zeichenfolgendarstellung des Typs des Werts zurück, der im Schlüssel gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="b5550-166">Returns the string representation of the type of the value stored at key.</span></span> <span data-ttu-id="b5550-167">Zu den verschiedenen Typen, die zurückgegeben werden können, zählen Folgende: „string“, „list“, „set“, „zset“ und „hash“.</span><span class="sxs-lookup"><span data-stu-id="b5550-167">The different types that can be returned are: string, list, set, zset and hash.</span></span> |
       
### <a name="executing-other-commands"></a><span data-ttu-id="b5550-168">Ausführen anderer Befehle</span><span class="sxs-lookup"><span data-stu-id="b5550-168">Executing other commands</span></span>

<span data-ttu-id="b5550-169">Das Objekt `IDatabase` weist eine `Execute`- und `ExecuteAsync`-Methode auf, mit der Textbefehle an den Redis-Server übergeben werden können.</span><span class="sxs-lookup"><span data-stu-id="b5550-169">The `IDatabase` object has an `Execute` and `ExecuteAsync` method which can be used to pass textual commands to the Redis server.</span></span> <span data-ttu-id="b5550-170">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="b5550-170">For example:</span></span>

```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString()); // displays: "PONG"
```

<span data-ttu-id="b5550-171">Die Methoden `Execute` und `ExecuteAsync` geben ein `RedisResult`-Objekt zurück, das Daten mit zwei Eigenschaften speichert:</span><span class="sxs-lookup"><span data-stu-id="b5550-171">The `Execute` and `ExecuteAsync` methods return a `RedisResult` object which is a data holder that includes two properties:</span></span>

- <span data-ttu-id="b5550-172">`Type`: Gibt `string` zurück, was auf den Typ des Ergebnisses hinweist, z.B. „STRING“ und „INTEGER“.</span><span class="sxs-lookup"><span data-stu-id="b5550-172">`Type` which returns a `string` indicating the type of the result - "STRING", "INTEGER", etc.</span></span>
- <span data-ttu-id="b5550-173">`IsNull`: Ein True/False-Wert, der erkannt wird, wenn das Ergebnis `null` lautet.</span><span class="sxs-lookup"><span data-stu-id="b5550-173">`IsNull` a true/false value to detect when the result is `null`.</span></span>

<span data-ttu-id="b5550-174">Anschließend können Sie `ToString()` in `RedisResult` verwenden, um den tatsächlichen Rückgabewert zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="b5550-174">You can then use `ToString()` on the `RedisResult` to get the actual return value.</span></span>

<span data-ttu-id="b5550-175">Sie können mit `Execute` beliebige unterstützte Befehle ausführen, beispielsweise können alle mit dem Cache verbundene Clients („CLIENT-LIST“) abgerufen werden:</span><span class="sxs-lookup"><span data-stu-id="b5550-175">You can use `Execute` to perform any supported commands - for example, we can get all the clients connected to the cache ("CLIENT LIST"):</span></span>

```csharp
var result = await db.ExecuteAsync("client", "list");
Console.WriteLine($"Type = {result.Type}\r\nResult = {result}");
```

<span data-ttu-id="b5550-176">Hierdurch würden alle verbundenen Clients ausgegeben werden:</span><span class="sxs-lookup"><span data-stu-id="b5550-176">This would output all the connected clients:</span></span>

```output
Type = BulkString
Result = id=9469 addr=16.183.122.154:54961 fd=18 name=DESKTOP-AAAAAA age=0 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=subscribe numops=5
id=9470 addr=16.183.122.155:54967 fd=13 name=DESKTOP-BBBBBB age=0 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=client numops=17
```

### <a name="storing-more-complex-values"></a><span data-ttu-id="b5550-177">Speichern von komplexeren Werten</span><span class="sxs-lookup"><span data-stu-id="b5550-177">Storing more complex values</span></span>
<span data-ttu-id="b5550-178">Redis ist auf sicheren Binärzeichenfolgen aufgebaut, Sie können jedoch Objektdiagramme zwischenspeichern, indem Sie sie in ein Textformat serialisieren, in der Regel XML oder JSON.</span><span class="sxs-lookup"><span data-stu-id="b5550-178">Redis is oriented around binary safe strings, but you can cache off object graphs by serializing them to a textual format - typically XML or JSON.</span></span> <span data-ttu-id="b5550-179">Nehmen Sie beispielsweise an, das Objekt `GameStats` für unsere Statistiken sieht wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="b5550-179">For example, perhaps for our statistics, we have a `GameStats` object which looks like:</span></span>

```csharp
public class GameStat
{
    public string Id { get; set; }
    public string Sport { get; set; }
    public DateTimeOffset DatePlayed { get; set; }
    public string Game { get; set; }
    public IReadOnlyList<string> Teams { get; set; }
    public IReadOnlyList<(string team, int score)> Results { get; set; }

    public GameStat(string sport, DateTimeOffset datePlayed, string game, string[] teams, IEnumerable<(string team, int score)> results)
    {
        Id = Guid.NewGuid().ToString();
        Sport = sport;
        DatePlayed = datePlayed;
        Game = game;
        Teams = teams.ToList();
        Results = results.ToList();
    }

    public override string ToString()
    {
        return $"{Sport} {Game} played on {DatePlayed.Date.ToShortDateString()} - " +
               $"{String.Join(',', Teams)}\r\n\t" + 
               $"{String.Join('\t', Results.Select(r => $"{r.team } - {r.score}\r\n"))}";
    }
}
```

<span data-ttu-id="b5550-180">Wir könnten die Bibliothek **Newtonsoft.Json** verwenden, um eine Instanz dieses Objekts in eine Zeichenfolge umzuwandeln:</span><span class="sxs-lookup"><span data-stu-id="b5550-180">We could use the **Newtonsoft.Json** library to turn an instance of this object into a string:</span></span>

```csharp
var stat = new GameStat("Soccer", new DateTime(1950, 7, 16), "FIFA World Cup", 
                new[] { "Uruguay", "Brazil" },
                new[] { ("Uruguay", 2), ("Brazil", 1) });

string serializedValue = Newtonsoft.Json.JsonConvert.SerializeObject(stat);
bool added = db.StringSet("event:1950-world-cup", serializedValue);
```

<span data-ttu-id="b5550-181">Wir könnten diese abrufen und anhand des umgekehrten Vorgangs wieder in ein Objekt konvertieren:</span><span class="sxs-lookup"><span data-stu-id="b5550-181">We could retrieve it and turn it back into an object using the reverse process:</span></span>

```csharp
var result = db.StringGet("event:1950-world-cup");
var stat = Newtonsoft.Json.JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine(stat.Sport); // displays "Soccer"
```

## <a name="cleaning-up-the-connection"></a><span data-ttu-id="b5550-182">Bereinigen der Verbindung</span><span class="sxs-lookup"><span data-stu-id="b5550-182">Cleaning up the connection</span></span>
<span data-ttu-id="b5550-183">Sobald die Redis-Verbindung hergestellt ist, können Sie `ConnectionMultiplexer` **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="b5550-183">Once you are done with the Redis connection, you can **Dispose** the `ConnectionMultiplexer`.</span></span> <span data-ttu-id="b5550-184">Dadurch werden alle Verbindungen und die Kommunikation mit dem Server getrennt.</span><span class="sxs-lookup"><span data-stu-id="b5550-184">This will close all connections and shutdown the communication to the server.</span></span>

```csharp
redisConnection.Dispose();
redisConnection = null;
```

<span data-ttu-id="b5550-185">Nun erstellen wir eine Anwendung und führen ein paar einfache Aufgaben mit Redis Cache durch.</span><span class="sxs-lookup"><span data-stu-id="b5550-185">Let's create an application and do some simple work with our Redis cache.</span></span>