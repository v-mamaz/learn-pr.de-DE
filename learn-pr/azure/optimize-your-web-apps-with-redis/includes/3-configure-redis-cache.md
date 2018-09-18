<span data-ttu-id="3b09d-101">Ihr Sportstatistik-Entwicklungsteam hat entschieden, dass Zwischenspeichern die Leistung für zuletzt angeforderte Daten deutlich verbessern könnte.</span><span class="sxs-lookup"><span data-stu-id="3b09d-101">Your sports statistics development team has decided that caching could dramatically improve performance for recently requested data.</span></span> <span data-ttu-id="3b09d-102">Der nächste Schritt ist das Erstellen und Konfigurieren einer Azure Redis Cache-Instanz.</span><span class="sxs-lookup"><span data-stu-id="3b09d-102">Your next step is to create and configure an Azure Redis Cache instance.</span></span>

## <a name="create-and-configure-the-azure-redis-cache-instance"></a><span data-ttu-id="3b09d-103">Erstellen und Konfigurieren der Azure Redis Cache-Instanz</span><span class="sxs-lookup"><span data-stu-id="3b09d-103">Create and configure the Azure Redis Cache instance</span></span>

1. <span data-ttu-id="3b09d-104">Öffnen Sie das [Azure-Portal](https://portal.azure.com/?azure-portal=true) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="3b09d-104">Open the [Azure Portal](https://portal.azure.com/?azure-portal=true) in your browser.</span></span>

1. <span data-ttu-id="3b09d-105">Klicken Sie auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="3b09d-105">Click on **Create a resource**.</span></span>

1. <span data-ttu-id="3b09d-106">Suchen Sie nach **Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="3b09d-106">Search for **Redis Cache**.</span></span>

1. <span data-ttu-id="3b09d-107">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="3b09d-107">Click **Create**.</span></span>

1. <span data-ttu-id="3b09d-108">Sie können eine Azure Redis Cache-Instanz aus den Datenbankressourcen im Azure-Portal hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-108">You can add an Azure Redis Cache instance from the database resources in the Azure portal.</span></span>

1. <span data-ttu-id="3b09d-109">Geben Sie einen global eindeutigen Namen an.</span><span class="sxs-lookup"><span data-stu-id="3b09d-109">Provide a globally unique name.</span></span> <span data-ttu-id="3b09d-110">Der Name muss eine Zeichenfolge mit einer Länge zwischen 1 und 63 Zeichen sein und darf nur Zahlen, Buchstaben und das Zeichen „-“ enthalten.</span><span class="sxs-lookup"><span data-stu-id="3b09d-110">The name must be a string between 1 and 63 characters and include only numbers, letters, and the '-' character.</span></span> <span data-ttu-id="3b09d-111">Der Cachename darf weder mit dem Zeichen „-“ beginnen oder enden, noch mehrere aufeinanderfolgende Zeichen vom Typ „-“ enthalten.</span><span class="sxs-lookup"><span data-stu-id="3b09d-111">The cache name can't start or end with the '-' character, and consecutive '-' characters aren't valid.</span></span>

1. <span data-ttu-id="3b09d-112">Geben Sie das Abonnement an, unter dem diese neue Azure Redis Cache-Instanz erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="3b09d-112">Provide the subscription under which this new Azure Redis Cache instance is created.</span></span>

1. <span data-ttu-id="3b09d-113">Der Name der Ressourcengruppe, in der Ihr Cache erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="3b09d-113">Name the resource group in which to create your cache.</span></span> <span data-ttu-id="3b09d-114">Indem Sie alle Ressourcen für eine App in einer Gruppe zusammenfassen, können Sie diese zusammen verwalten.</span><span class="sxs-lookup"><span data-stu-id="3b09d-114">By putting all the resources for an app in a group, you can manage them together.</span></span>

1. <span data-ttu-id="3b09d-115">Platzieren Sie Ihre Cache-Instanz und Ihre Anwendung immer in der gleichen Region/am gleichen Standort.</span><span class="sxs-lookup"><span data-stu-id="3b09d-115">Always place your cache instance and your application in the same region / location.</span></span> <span data-ttu-id="3b09d-116">Das Herstellen einer Verbindung mit einem Cache in einer anderen Region kann die Wartezeit beträchtlich erhöhen und die Zuverlässigkeit beeinträchtigen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-116">Connecting to a cache in a different region can significantly increase latency and reduce reliability.</span></span> <span data-ttu-id="3b09d-117">Wenn Sie die Verbindung mit dem Cache außerhalb von Azure herstellen, wählen Sie einen Standort in der Nähe des Orts aus, an dem die Anwendung, die die Daten nutzt, ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="3b09d-117">If you are connecting to the cache outside of Azure, then select a location close to where the application consuming the data is running.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3b09d-118">Viel wichtiger als die Nähe des Datenspeichers zum Datennutzer ist die Nähe zum Cache.</span><span class="sxs-lookup"><span data-stu-id="3b09d-118">It's far more important that the cache is close to the data consumer than the data store.</span></span>

1. <span data-ttu-id="3b09d-119">Wählen Sie den Tarif aus.</span><span class="sxs-lookup"><span data-stu-id="3b09d-119">Select the pricing tier.</span></span> 
    - <span data-ttu-id="3b09d-120">Wir empfehlen, für Produktionssysteme immer den Standard- oder Premium-Tarif zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="3b09d-120">We recommend you always use Standard or Premium Tier for production systems.</span></span> <span data-ttu-id="3b09d-121">Der Basic-Tarif ist ein System mit einem einzelnen Knoten ohne Datenreplikation und ohne SLA.</span><span class="sxs-lookup"><span data-stu-id="3b09d-121">The Basic Tier is a single node system with no data replication and no SLA.</span></span> <span data-ttu-id="3b09d-122">Verwenden Sie mindestens einen C1-Cache.</span><span class="sxs-lookup"><span data-stu-id="3b09d-122">Also, use at least a C1 cache.</span></span> <span data-ttu-id="3b09d-123">C0-Caches sind nur für einfache Entwicklungs-/Testszenarien vorgesehen, da sie einen freigegebenen CPU-Kern und nur sehr wenig Arbeitsspeicher haben.</span><span class="sxs-lookup"><span data-stu-id="3b09d-123">C0 caches are really meant for simple dev/test scenarios since they have a shared CPU core and very little memory.</span></span>

    - <span data-ttu-id="3b09d-124">Beim Premium-Tarif stehen Ihnen zwei Methoden zur Auswahl, um Daten bei der Notfallwiederherstellung beizubehalten:</span><span class="sxs-lookup"><span data-stu-id="3b09d-124">The Premium tier allows you to persist data in two ways to provide disaster recovery:</span></span>

        - <span data-ttu-id="3b09d-125">RDB-Persistenz erstellt regelmäßig eine Momentaufnahme und kann den Cache bei einem Ausfall anhand dieser Momentaufnahme wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-125">RDB persistence takes a periodic snapshot and can rebuild the cache using the snapshot in case of failure.</span></span>

            ![Screenshot des Azure-Portals mit den RDB-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-1.png)

        - <span data-ttu-id="3b09d-127">AOF-Persistenz speichert jeden Schreibvorgang in einem Protokoll, das mindestens einmal pro Sekunde gespeichert wird.</span><span class="sxs-lookup"><span data-stu-id="3b09d-127">AOF persistence saves every write operation to a log that is saved at least once per second.</span></span> <span data-ttu-id="3b09d-128">Dabei entstehen größere Dateien als bei RDB, jedoch ist der Datenverlust geringer.</span><span class="sxs-lookup"><span data-stu-id="3b09d-128">This creates bigger files than RDB but has less data loss.</span></span>

            ![Screenshot des Azure-Portals mit den AOF-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-2.png)

    - <span data-ttu-id="3b09d-130">Schützen Sie Ihren Cache mit einem virtuellen Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="3b09d-130">Secure your cache with a virtual network.</span></span>
      <span data-ttu-id="3b09d-131">Wenn Sie über einen Redis-Cache mit Premium-Tarif verfügen, können Sie ihn für ein virtuelles Netzwerk in der Cloud bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-131">If you have a premium tier Redis cache, you can deploy it to a virtual network in the cloud.</span></span> <span data-ttu-id="3b09d-132">Der Cache wird nur für andere virtuelle Computer und Anwendungen in demselben virtuellen Netzwerk verfügbar sein.</span><span class="sxs-lookup"><span data-stu-id="3b09d-132">Your cache will be available to only other virtual machines and applications in the same virtual network.</span></span>

    - <span data-ttu-id="3b09d-133">Verteilen Sie Ihren Cache mit Clustering.</span><span class="sxs-lookup"><span data-stu-id="3b09d-133">Distribute your cache with clustering.</span></span>
      <span data-ttu-id="3b09d-134">Mit Redis-Cache mit Premium-Tarif können Sie Clustering implementieren, um Ihr Dataset automatisch zwischen mehreren Knoten aufzuteilen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-134">With a premium tier Redis cache, you can implement clustering to automatically split your dataset among multiple nodes.</span></span> <span data-ttu-id="3b09d-135">Um Clustering zu implementieren, geben Sie eine maximale Anzahl von zehn Shards an.</span><span class="sxs-lookup"><span data-stu-id="3b09d-135">To implement clustering, you specify the number of shards to a maximum of 10.</span></span> <span data-ttu-id="3b09d-136">Die Kosten entsprechen den Kosten des ursprünglichen Knotens multipliziert mit der Anzahl von Shards.</span><span class="sxs-lookup"><span data-stu-id="3b09d-136">The cost incurred is the cost of the original node, multiplied by the number of shards.</span></span>

    - <span data-ttu-id="3b09d-137">Migrieren Sie von Azure Managed Cache Service.</span><span class="sxs-lookup"><span data-stu-id="3b09d-137">Migrate from Azure Managed Cache Service.</span></span>
      <span data-ttu-id="3b09d-138">Je nach den Features von Managed Cache Service, die Sie verwenden, sind zum Migrieren von Anwendungen, die Azure Managed Cache Service verwenden, zu Azure Redis Cache nur minimale Änderungen an der Anwendung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="3b09d-138">Depending on the Managed Cache Service features you use, migrating applications that use Azure Managed Cache Service to Azure Redis Cache can be accomplished with minimal changes to your application.</span></span> <span data-ttu-id="3b09d-139">Die APIs sind zwar nicht genau gleich, aber ähnlich.</span><span class="sxs-lookup"><span data-stu-id="3b09d-139">While the APIs aren't exactly the same, they're similar.</span></span> <span data-ttu-id="3b09d-140">Ein Großteil des vorhandenen Codes, der mit Managed Cache Service auf den Cache zugreift, kann mit minimalen Änderungen wiederverwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3b09d-140">Much of your existing code that accesses the cache with Managed Cache Service can be reused with minimal changes.</span></span>

## <a name="accessing-the-redis-instance"></a><span data-ttu-id="3b09d-141">Zugreifen auf die Redis-Instanz</span><span class="sxs-lookup"><span data-stu-id="3b09d-141">Accessing the Redis instance</span></span>

<span data-ttu-id="3b09d-142">Redis unterstützt eine Reihe von [bekannten Befehlen](https://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="3b09d-142">Redis supports a set of [known commands](https://redis.io/commands).</span></span> <span data-ttu-id="3b09d-143">Ein Befehl wird in der Regel als `COMMAND parameter1 parameter2 parameter3` ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="3b09d-143">A command is typically issued as `COMMAND parameter1 parameter2 parameter3`.</span></span>

<span data-ttu-id="3b09d-144">Im Folgenden sind einige gängige Befehle aufgeführt, die Sie verwenden können:</span><span class="sxs-lookup"><span data-stu-id="3b09d-144">Here are some common commands you can use:</span></span>

| <span data-ttu-id="3b09d-145">Befehl</span><span class="sxs-lookup"><span data-stu-id="3b09d-145">Command</span></span> | <span data-ttu-id="3b09d-146">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3b09d-146">Description</span></span> |
|---------|-------------|
| `ping` | <span data-ttu-id="3b09d-147">Den Server pingen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-147">Ping the server.</span></span> <span data-ttu-id="3b09d-148">Gibt „PONG“ zurück.</span><span class="sxs-lookup"><span data-stu-id="3b09d-148">Returns "PONG".</span></span> |
| `set [key] [value]` | <span data-ttu-id="3b09d-149">Legt einen Schlüssel/Wert im Cache fest.</span><span class="sxs-lookup"><span data-stu-id="3b09d-149">Sets a key/value in the cache.</span></span> <span data-ttu-id="3b09d-150">Gibt bei erfolgreicher Ausführung „OK“ zurück.</span><span class="sxs-lookup"><span data-stu-id="3b09d-150">Returns "OK" on success.</span></span> |
| `get [key]` | <span data-ttu-id="3b09d-151">Ruft einen Wert aus dem Cache ab.</span><span class="sxs-lookup"><span data-stu-id="3b09d-151">Gets a value from the cache.</span></span> |
| `exists [key]` | <span data-ttu-id="3b09d-152">Gibt „1“ zurück, wenn der **Schlüssel** im Cache vorhanden ist, und andernfalls „0“.</span><span class="sxs-lookup"><span data-stu-id="3b09d-152">Returns '1' if the **key** exists in the cache, '0' if it doesn't.</span></span> |
| `type [key]` | <span data-ttu-id="3b09d-153">Gibt den Typ zurück, der dem Wert für den angegebenen **Schlüssel** zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="3b09d-153">Returns the type associated to the value for the given **key**.</span></span> |
| `incr [key]` | <span data-ttu-id="3b09d-154">Den angegebenen Wert, der dem **Schlüssel** zugeordnet ist, um 1 erhöhen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-154">Increment the given value associated with **key** by \`1'.</span></span> <span data-ttu-id="3b09d-155">Der Wert muss vom Typ „Integer“ oder „Double“ sein.</span><span class="sxs-lookup"><span data-stu-id="3b09d-155">The value must be an integer or double value.</span></span> <span data-ttu-id="3b09d-156">Gibt den neuen Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="3b09d-156">This returns the new value.</span></span> |
| `incrby [key] [amount]` | <span data-ttu-id="3b09d-157">Den angegebenen Wert, der dem **Schlüssel** zugeordnet ist, um den festgelegten Wert erhöhen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-157">Increment the given value associated with **key** by the specified amount.</span></span> <span data-ttu-id="3b09d-158">Der Wert muss vom Typ „Integer“ oder „Double“ sein.</span><span class="sxs-lookup"><span data-stu-id="3b09d-158">The value must be an integer or double value.</span></span> <span data-ttu-id="3b09d-159">Gibt den neuen Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="3b09d-159">This returns the new value.</span></span> |
| `del [key]` | <span data-ttu-id="3b09d-160">Löscht den Wert, der dem **Schlüssel** zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="3b09d-160">Deletes the value associated with the **key**.</span></span> |
| `flushdb` | <span data-ttu-id="3b09d-161">_Alle_ Schlüssel und Werte in der Datenbank löschen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-161">Delete _all_ keys and values in the database.</span></span> |

<span data-ttu-id="3b09d-162">Redis verfügt über ein Befehlszeilentool (**redis-cli**), mit dem Sie direkt mit diesen Befehlen experimentieren können.</span><span class="sxs-lookup"><span data-stu-id="3b09d-162">Redis has a command-line tool (**redis-cli**) you can use to experiment directly with these commands.</span></span> <span data-ttu-id="3b09d-163">Im Folgenden finden Sie einige Beispiele.</span><span class="sxs-lookup"><span data-stu-id="3b09d-163">Here are some examples.</span></span>

```output
> set somekey somevalue
OK
> get somekey
"somevalue"
> exists somekey
(string) 1
> del somekey
(string) 1
> exists somekey
(string) 0
```

<span data-ttu-id="3b09d-164">Hier sehen Sie ein Beispiel zur Verwendung der `INCR`-Befehle.</span><span class="sxs-lookup"><span data-stu-id="3b09d-164">Here's an example of working with the `INCR` commands.</span></span> <span data-ttu-id="3b09d-165">Diese Befehle sind praktisch, da sie unteilbare Inkremente _für mehrere Anwendungen_ bereitstellen, die den Cache verwenden.</span><span class="sxs-lookup"><span data-stu-id="3b09d-165">These are convenient because they provide atomic increments _across multiple applications_ that are using the cache.</span></span>

```output
> set counter 100
OK
> incr counter
(integer) 101
> incrby counter 50
(integer) 151
> type counter
(integer)
```

### <a name="adding-an-expiration-time-to-values"></a><span data-ttu-id="3b09d-166">Hinzufügen einer Ablaufzeit zu Werten</span><span class="sxs-lookup"><span data-stu-id="3b09d-166">Adding an expiration time to values</span></span>

<span data-ttu-id="3b09d-167">Die Zwischenspeicherung ist wichtig, da sie uns das Speichern von häufig verwendeten Werten im Arbeitsspeicher ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="3b09d-167">Caching is important because it allows us to store commonly used values in memory.</span></span> <span data-ttu-id="3b09d-168">Wir müssen jedoch auch in der Lage sein, eine Ablaufzeit für veraltete Werte festzulegen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-168">However, we also need a way to expire values when they are stale.</span></span> <span data-ttu-id="3b09d-169">In Redis wird dazu eine _Gültigkeitsdauer_ (Time To Live, TTL) auf einen Schlüssel angewendet.</span><span class="sxs-lookup"><span data-stu-id="3b09d-169">In Redis this is done by applying a _time to live_ (TTL) to a key.</span></span>

<span data-ttu-id="3b09d-170">Nach Ablauf der TTL wird der Schlüssel genau wie bei der Ausgabe des DEL-Befehls automatisch gelöscht.</span><span class="sxs-lookup"><span data-stu-id="3b09d-170">When the TTL elapses, the key is automatically deleted, exactly as if the DEL command were issued.</span></span> <span data-ttu-id="3b09d-171">Im Folgenden finden Sie einige Hinweise zum TTL-Ablauf.</span><span class="sxs-lookup"><span data-stu-id="3b09d-171">Here are some notes on TTL expirations.</span></span>

- <span data-ttu-id="3b09d-172">Ablaufzeiten können mit Sekunden- oder Millisekundengenauigkeit festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="3b09d-172">Expirations can be set using seconds or milliseconds precision.</span></span>
- <span data-ttu-id="3b09d-173">Die Auflösung der Ablaufzeit ist immer 1 Millisekunde.</span><span class="sxs-lookup"><span data-stu-id="3b09d-173">The expire time resolution is always 1 millisecond.</span></span>
- <span data-ttu-id="3b09d-174">Informationen zum Ablauf werden repliziert und dauerhaft auf dem Datenträger gespeichert. Die Zeit verstreicht gewissermaßen, während Ihr Redis-Server angehalten bleibt (d. h. Redis speichert das Datum, an dem ein Schlüssel abläuft).</span><span class="sxs-lookup"><span data-stu-id="3b09d-174">Information about expires are replicated and persisted on disk, the time virtually passes when your Redis server remains stopped (this means that Redis saves the date at which a key will expire).</span></span>

<span data-ttu-id="3b09d-175">Hier sehen Sie ein Beispiel für einen Ablauf:</span><span class="sxs-lookup"><span data-stu-id="3b09d-175">Here is an example of an expiration:</span></span>

```output
> set counter 100
OK
> expire counter 5
(integer) 1
> get counter
100
... wait ...
> get counter
(nil)
```

## <a name="accessing-a-redis-cache-from-a-client"></a><span data-ttu-id="3b09d-176">Zugreifen auf einen Redis Cache von einem Client</span><span class="sxs-lookup"><span data-stu-id="3b09d-176">Accessing a Redis cache from a client</span></span>

<span data-ttu-id="3b09d-177">Wenn Sie eine Verbindung mit einer Azure Redis Cache-Instanz herstellen, benötigen Clients den Hostnamen, den Port und einen Zugriffsschlüssel für den Cache.</span><span class="sxs-lookup"><span data-stu-id="3b09d-177">When connecting to an Azure Redis Cache instance, clients need the host name, port, and an access key for the cache.</span></span> <span data-ttu-id="3b09d-178">Sie können diese Informationen im Azure-Portal auf der Seite **Einstellungen > Zugriffsschlüssel** abrufen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-178">You can retrieve this information in the Azure portal through the **Settings > Access Keys** page.</span></span> 

- <span data-ttu-id="3b09d-179">Der Hostname ist die öffentliche Internetadresse Ihres Caches, die mit dem Namen des Caches erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="3b09d-179">The host name is the public Internet address of your cache, which was created using the name of the cache.</span></span> <span data-ttu-id="3b09d-180">Beispiel: `sportsresults.redis.cache.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="3b09d-180">For example `sportsresults.redis.cache.windows.net`.</span></span>

- <span data-ttu-id="3b09d-181">Der Zugriffsschlüssel fungiert als Kennwort für Ihren Cache.</span><span class="sxs-lookup"><span data-stu-id="3b09d-181">The access key acts as a password for your cache.</span></span> <span data-ttu-id="3b09d-182">Zwei Schlüssel werden erstellt: ein Primärschlüssel und ein Sekundärschlüssel.</span><span class="sxs-lookup"><span data-stu-id="3b09d-182">There are two keys created: primary and secondary.</span></span> <span data-ttu-id="3b09d-183">Sie können beide Schlüssel verwenden. Zwei Schlüssel werden für den Fall bereitgestellt, dass Sie den Primärschlüssel ändern müssen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-183">You can use either key, two are provided in case you need to change the primary key.</span></span> <span data-ttu-id="3b09d-184">Sie können alle Clients auf den Sekundärschlüssel umstellen und den Primärschlüssel erneut generieren.</span><span class="sxs-lookup"><span data-stu-id="3b09d-184">You can switch all of your clients to the secondary key, and regenerate the primary key.</span></span> <span data-ttu-id="3b09d-185">In diesem Fall werden alle Anwendungen blockiert, die den ursprünglichen Primärschlüssel verwenden.</span><span class="sxs-lookup"><span data-stu-id="3b09d-185">This would block any applications using the original primary key.</span></span> <span data-ttu-id="3b09d-186">Microsoft empfiehlt, die Schlüssel wie persönliche Kennwörter in regelmäßigen Abständen erneut zu generieren.</span><span class="sxs-lookup"><span data-stu-id="3b09d-186">Microsoft recommends periodically regenerating the keys - much like you would your personal passwords.</span></span>

> [!WARNING]
> <span data-ttu-id="3b09d-187">Die Zugriffsschlüssel sollten als vertrauliche Informationen behandelt und wie Kennwörter geschützt werden.</span><span class="sxs-lookup"><span data-stu-id="3b09d-187">Your access keys should be considered confidential information, treat them like you would a password.</span></span> <span data-ttu-id="3b09d-188">Jede Person mit einem Zugriffsschlüssel kann beliebige Vorgänge in Ihrem Cache durchführen.</span><span class="sxs-lookup"><span data-stu-id="3b09d-188">Anyone who has an access key can perform any operation on your cache!</span></span>
