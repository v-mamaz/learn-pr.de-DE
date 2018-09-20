<span data-ttu-id="eadd9-101">Ihr Sportstatistik-Entwicklungsteam hat entschieden, dass Zwischenspeichern die Leistung für zuletzt angeforderte Daten deutlich verbessern könnte.</span><span class="sxs-lookup"><span data-stu-id="eadd9-101">Your sports statistics development team has decided that caching could dramatically improve performance for recently requested data.</span></span> <span data-ttu-id="eadd9-102">Der nächste Schritt ist das Erstellen und Konfigurieren einer Azure Redis Cache-Instanz.</span><span class="sxs-lookup"><span data-stu-id="eadd9-102">Your next step is to create and configure an Azure Redis Cache instance.</span></span>

## <a name="create-and-configure-the-azure-redis-cache-instance"></a><span data-ttu-id="eadd9-103">Erstellen und Konfigurieren der Azure Redis Cache-Instanz</span><span class="sxs-lookup"><span data-stu-id="eadd9-103">Create and configure the Azure Redis Cache instance</span></span>

<span data-ttu-id="eadd9-104">Sie können einen Redis Cache über das Azure-Portal, mithilfe der Azure CLI oder unter Verwendung von Azure PowerShell erstellen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-104">You can create a Redis cache using the Azure portal, the Azure CLI, or Azure PowerShell.</span></span> <span data-ttu-id="eadd9-105">Es gibt mehrere Parameter, für die Sie sich entscheiden müssen, um den Cache für Ihre Zwecke ordnungsgemäß zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="eadd9-105">There are several parameters you will need to decide in order to configure the cache properly for your purposes.</span></span>

### <a name="name"></a><span data-ttu-id="eadd9-106">Name</span><span class="sxs-lookup"><span data-stu-id="eadd9-106">Name</span></span>

<span data-ttu-id="eadd9-107">Der Redis Cache benötigen einen global eindeutigen Namen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-107">The Redis cache will need a globally unique name.</span></span> <span data-ttu-id="eadd9-108">Der Name muss innerhalb von Azure eindeutig sein, da er verwendet wird, um eine öffentlich zugängliche URL zu generieren, um eine Verbindung herzustellen und mit dem Dienst zu kommunizieren.</span><span class="sxs-lookup"><span data-stu-id="eadd9-108">The name has to be unique within Azure because it is used to generate a public-facing URL to connect and communicate with the service.</span></span>

<span data-ttu-id="eadd9-109">Der Name muss zwischen 1 und 63 Zeichen lang sein und aus Ziffern, Buchstaben und dem Zeichen „-“ bestehen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-109">The name must be between 1 and 63 characters, composed of numbers, letters, and the '-' character.</span></span> <span data-ttu-id="eadd9-110">Der Cachename darf weder mit dem Zeichen „-“ beginnen oder enden, noch mehrere aufeinanderfolgende Zeichen vom Typ „-“ enthalten.</span><span class="sxs-lookup"><span data-stu-id="eadd9-110">The cache name can't start or end with the '-' character, and consecutive '-' characters aren't valid.</span></span>

### <a name="resource-group"></a><span data-ttu-id="eadd9-111">Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="eadd9-111">Resource Group</span></span>

<span data-ttu-id="eadd9-112">Azure Redis Cache ist eine verwaltete Ressource und benötigt eine _Ressourcengruppe_ als Besitzer.</span><span class="sxs-lookup"><span data-stu-id="eadd9-112">The Azure Redis Cache is a managed resource and needs a _resource group_ owner.</span></span> <span data-ttu-id="eadd9-113">Sie können eine neue Ressourcengruppe erstellen oder eine vorhandene Ressourcengruppe in einem Abonnement verwenden, in dem Sie Mitglied sind.</span><span class="sxs-lookup"><span data-stu-id="eadd9-113">You can either create a new resource group, or use an existing one in a subscription you are part of.</span></span>

### <a name="location"></a><span data-ttu-id="eadd9-114">Standort</span><span class="sxs-lookup"><span data-stu-id="eadd9-114">Location</span></span>

<span data-ttu-id="eadd9-115">Sie müssen entscheiden, wo sich der Redis Cache physisch befinden soll, indem Sie eine Azure-Region auswählen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-115">You will need to decide where the Redis cache will be physically located by selecting an Azure region.</span></span> <span data-ttu-id="eadd9-116">Sie sollten Ihre Cacheinstanz und Ihre Anwendung immer in der gleichen Region platzieren.</span><span class="sxs-lookup"><span data-stu-id="eadd9-116">You should always place your cache instance and your application in the same region.</span></span> <span data-ttu-id="eadd9-117">Das Herstellen einer Verbindung mit einem Cache in einer anderen Region kann die Wartezeit beträchtlich erhöhen und die Zuverlässigkeit beeinträchtigen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-117">Connecting to a cache in a different region can significantly increase latency and reduce reliability.</span></span> <span data-ttu-id="eadd9-118">Wenn Sie die Verbindung mit dem Cache außerhalb von Azure herstellen, wählen Sie einen Standort in der Nähe des Orts aus, an dem die Anwendung, die die Daten nutzt, ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="eadd9-118">If you are connecting to the cache outside of Azure, then select a location close to where the application consuming the data is running.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eadd9-119">Platzieren Sie den Redis Cache so nah wie möglich am Daten_consumer_.</span><span class="sxs-lookup"><span data-stu-id="eadd9-119">Put the Redis cache as close to the data _consumer_ as you can.</span></span>

### <a name="pricing-tier"></a><span data-ttu-id="eadd9-120">Tarif</span><span class="sxs-lookup"><span data-stu-id="eadd9-120">Pricing tier</span></span>

<span data-ttu-id="eadd9-121">Wie bereits in der letzten Einheit erwähnt wurde, sind drei Tarife für einen Azure Redis Cache verfügbar.</span><span class="sxs-lookup"><span data-stu-id="eadd9-121">As mentioned in the last unit, there are three pricing tiers available for an Azure Redis Cache.</span></span>

- <span data-ttu-id="eadd9-122">**Basic**: Basiscache, der sich ideal zu Entwicklungs-/Testzwecken eignet.</span><span class="sxs-lookup"><span data-stu-id="eadd9-122">**Basic**: Basic cache ideal for development/testing.</span></span> <span data-ttu-id="eadd9-123">Ist auf einen einzelnen Server, 53 GB Arbeitsspeicher und 20.000 Verbindungen beschränkt.</span><span class="sxs-lookup"><span data-stu-id="eadd9-123">Is limited to a single server, 53 GB of memory, and 20,000 connections.</span></span> <span data-ttu-id="eadd9-124">Es gibt keine SLA für diesen Diensttarif.</span><span class="sxs-lookup"><span data-stu-id="eadd9-124">There is no SLA for this service tier.</span></span>
- <span data-ttu-id="eadd9-125">**Standard**: Produktionscache, der Replikation und eine SLA von 99,99 % unterstützt.</span><span class="sxs-lookup"><span data-stu-id="eadd9-125">**Standard**: Production cache which supports replication and includes an 99.99% SLA.</span></span> <span data-ttu-id="eadd9-126">Der Tarif unterstützt zwei Server (Master/Slave) und weist die gleichen Einschränkungen für den Arbeitsspeicher bzw. die Anzahl der Verbindungen wie der Tarif „Basic“ auf.</span><span class="sxs-lookup"><span data-stu-id="eadd9-126">It supports two servers (master/slave), and has the same memory/connection limits as the Basic tier.</span></span>
- <span data-ttu-id="eadd9-127">**Premium**: Enterprise-Tarif, der auf dem Tarif „Standard“ aufbaut und Unterstützung für Persistenz, Clustering und horizontale Skalierung bietet.</span><span class="sxs-lookup"><span data-stu-id="eadd9-127">**Premium**: Enterprise tier which builds on the Standard tier and includes persistence, clustering, and scale-out cache support.</span></span> <span data-ttu-id="eadd9-128">Dies ist der leistungsstärkste Tarif mit bis zu 530 GB Arbeitsspeicher und 40.000 gleichzeitigen Verbindungen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-128">This is the highest performing tier with up to 530 GB of memory and 40,000 simultaneous connections.</span></span>

<span data-ttu-id="eadd9-129">Sie können die Kapazität des verfügbaren Cachespeichers für jeden Tarif steuern, indem Sie eine Cacheebene von C0-C6 für Basic/Standard und P0-P4 für Premium auswählen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-129">You can control the amount of cache memory available on each tier - this is selected by choosing a cache level from C0-C6 for Basic/Standard and P0-P4 for Premium.</span></span> <span data-ttu-id="eadd9-130">Ausführliche Informationen finden Sie in der [Preisübersicht](https://azure.microsoft.com/pricing/details/cache/).</span><span class="sxs-lookup"><span data-stu-id="eadd9-130">Check the [pricing page](https://azure.microsoft.com/pricing/details/cache/) for full details.</span></span>

> [!TIP]
> <span data-ttu-id="eadd9-131">Microsoft empfiehlt, für Produktionssysteme immer den Standard- oder Premium-Tarif zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="eadd9-131">Microsoft recommends you always use Standard or Premium Tier for production systems.</span></span> <span data-ttu-id="eadd9-132">Der Basic-Tarif ist ein System mit einem einzelnen Knoten ohne Datenreplikation und ohne SLA.</span><span class="sxs-lookup"><span data-stu-id="eadd9-132">The Basic Tier is a single node system with no data replication and no SLA.</span></span> <span data-ttu-id="eadd9-133">Verwenden Sie mindestens einen C1-Cache.</span><span class="sxs-lookup"><span data-stu-id="eadd9-133">Also, use at least a C1 cache.</span></span> <span data-ttu-id="eadd9-134">C0-Caches sind nur für einfache Entwicklungs-/Testszenarien vorgesehen, da sie einen freigegebenen CPU-Kern und nur sehr wenig Arbeitsspeicher haben.</span><span class="sxs-lookup"><span data-stu-id="eadd9-134">C0 caches are really meant for simple dev/test scenarios since they have a shared CPU core and very little memory.</span></span>

<span data-ttu-id="eadd9-135">Beim Premium-Tarif stehen Ihnen zwei Methoden zur Auswahl, um Daten bei der Notfallwiederherstellung beizubehalten:</span><span class="sxs-lookup"><span data-stu-id="eadd9-135">The Premium tier allows you to persist data in two ways to provide disaster recovery:</span></span>

1. <span data-ttu-id="eadd9-136">RDB-Persistenz erstellt regelmäßig eine Momentaufnahme und kann den Cache bei einem Ausfall anhand dieser Momentaufnahme wiederherstellen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-136">RDB persistence takes a periodic snapshot and can rebuild the cache using the snapshot in case of failure.</span></span>

    ![Screenshot des Azure-Portals mit den RDB-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-1.png)

2. <span data-ttu-id="eadd9-138">AOF-Persistenz speichert jeden Schreibvorgang in einem Protokoll, das mindestens einmal pro Sekunde gespeichert wird.</span><span class="sxs-lookup"><span data-stu-id="eadd9-138">AOF persistence saves every write operation to a log that is saved at least once per second.</span></span> <span data-ttu-id="eadd9-139">Dabei entstehen größere Dateien als bei RDB, jedoch ist der Datenverlust geringer.</span><span class="sxs-lookup"><span data-stu-id="eadd9-139">This creates bigger files than RDB but has less data loss.</span></span>

    ![Screenshot des Azure-Portals mit den AOF-Persistenzoptionen für eine neue Redis-Cacheinstanz.](../media/3-redis-persistence-2.png)

<span data-ttu-id="eadd9-141">Es gibt verschiedene weitere Einstellungen, die nur für den Tarif **Premium** zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-141">There are several other settings which are only available to the **Premium** tier.</span></span>

### <a name="virtual-network-support"></a><span data-ttu-id="eadd9-142">Unterstützung für virtuelle Netzwerke</span><span class="sxs-lookup"><span data-stu-id="eadd9-142">Virtual Network support</span></span>

<span data-ttu-id="eadd9-143">Wenn Sie einen Redis Cache mit dem Premium-Tarif erstellen, können Sie ihn für ein virtuelles Netzwerk in der Cloud bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-143">If you create a premium tier Redis cache, you can deploy it to a virtual network in the cloud.</span></span> <span data-ttu-id="eadd9-144">Der Cache ist nur für andere virtuelle Computer und Anwendungen im gleichen virtuellen Netzwerk verfügbar.</span><span class="sxs-lookup"><span data-stu-id="eadd9-144">Your cache will be available to only other virtual machines and applications in the same virtual network.</span></span> <span data-ttu-id="eadd9-145">Dies bietet ein höheres Maß an Sicherheit, wenn Ihr Dienst und Ihr Cache beide in Azure gehostet werden oder über ein VPN des virtuellen Azure-Netzwerks verbunden sind.</span><span class="sxs-lookup"><span data-stu-id="eadd9-145">This provides a higher level of security when your service and cache are both hosted in Azure, or are connected through an Azure virtual network VPN.</span></span>

### <a name="clustering-support"></a><span data-ttu-id="eadd9-146">Unterstützung für Clustering</span><span class="sxs-lookup"><span data-stu-id="eadd9-146">Clustering support</span></span>

<span data-ttu-id="eadd9-147">Mit einem Redis Cache mit Premium-Tarif können Sie Clustering implementieren, um Ihr Dataset automatisch auf mehrere Knoten aufzuteilen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-147">With a premium tier Redis cache, you can implement clustering to automatically split your dataset among multiple nodes.</span></span> <span data-ttu-id="eadd9-148">Um Clustering zu implementieren, geben Sie eine maximale Anzahl von zehn Shards an.</span><span class="sxs-lookup"><span data-stu-id="eadd9-148">To implement clustering, you specify the number of shards to a maximum of 10.</span></span> <span data-ttu-id="eadd9-149">Die Kosten entsprechen den Kosten des ursprünglichen Knotens multipliziert mit der Anzahl von Shards.</span><span class="sxs-lookup"><span data-stu-id="eadd9-149">The cost incurred is the cost of the original node, multiplied by the number of shards.</span></span>

## <a name="accessing-the-redis-instance"></a><span data-ttu-id="eadd9-150">Zugreifen auf die Redis-Instanz</span><span class="sxs-lookup"><span data-stu-id="eadd9-150">Accessing the Redis instance</span></span>

<span data-ttu-id="eadd9-151">Redis unterstützt eine Reihe von [bekannten Befehlen](https://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="eadd9-151">Redis supports a set of [known commands](https://redis.io/commands).</span></span> <span data-ttu-id="eadd9-152">Ein Befehl wird in der Regel als `COMMAND parameter1 parameter2 parameter3` ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="eadd9-152">A command is typically issued as `COMMAND parameter1 parameter2 parameter3`.</span></span>

<span data-ttu-id="eadd9-153">Im Folgenden sind einige gängige Befehle aufgeführt, die Sie verwenden können:</span><span class="sxs-lookup"><span data-stu-id="eadd9-153">Here are some common commands you can use:</span></span>

| <span data-ttu-id="eadd9-154">Befehl</span><span class="sxs-lookup"><span data-stu-id="eadd9-154">Command</span></span> | <span data-ttu-id="eadd9-155">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="eadd9-155">Description</span></span> |
|---------|-------------|
| `ping` | <span data-ttu-id="eadd9-156">Den Server pingen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-156">Ping the server.</span></span> <span data-ttu-id="eadd9-157">Gibt „PONG“ zurück.</span><span class="sxs-lookup"><span data-stu-id="eadd9-157">Returns "PONG".</span></span> |
| `set [key] [value]` | <span data-ttu-id="eadd9-158">Legt einen Schlüssel/Wert im Cache fest.</span><span class="sxs-lookup"><span data-stu-id="eadd9-158">Sets a key/value in the cache.</span></span> <span data-ttu-id="eadd9-159">Gibt bei erfolgreicher Ausführung „OK“ zurück.</span><span class="sxs-lookup"><span data-stu-id="eadd9-159">Returns "OK" on success.</span></span> |
| `get [key]` | <span data-ttu-id="eadd9-160">Ruft einen Wert aus dem Cache ab.</span><span class="sxs-lookup"><span data-stu-id="eadd9-160">Gets a value from the cache.</span></span> |
| `exists [key]` | <span data-ttu-id="eadd9-161">Gibt „1“ zurück, wenn der **Schlüssel** im Cache vorhanden ist, und andernfalls „0“.</span><span class="sxs-lookup"><span data-stu-id="eadd9-161">Returns '1' if the **key** exists in the cache, '0' if it doesn't.</span></span> |
| `type [key]` | <span data-ttu-id="eadd9-162">Gibt den Typ zurück, der dem Wert für den angegebenen **Schlüssel** zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="eadd9-162">Returns the type associated to the value for the given **key**.</span></span> |
| `incr [key]` | <span data-ttu-id="eadd9-163">Inkrementiert den angegebenen Wert, der dem **Schlüssel** zugeordnet ist, um 1.</span><span class="sxs-lookup"><span data-stu-id="eadd9-163">Increment the given value associated with **key** by '1'.</span></span> <span data-ttu-id="eadd9-164">Der Wert muss vom Typ „Integer“ oder „Double“ sein.</span><span class="sxs-lookup"><span data-stu-id="eadd9-164">The value must be an integer or double value.</span></span> <span data-ttu-id="eadd9-165">Gibt den neuen Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="eadd9-165">This returns the new value.</span></span> |
| `incrby [key] [amount]` | <span data-ttu-id="eadd9-166">Den angegebenen Wert, der dem **Schlüssel** zugeordnet ist, um den festgelegten Wert erhöhen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-166">Increment the given value associated with **key** by the specified amount.</span></span> <span data-ttu-id="eadd9-167">Der Wert muss vom Typ „Integer“ oder „Double“ sein.</span><span class="sxs-lookup"><span data-stu-id="eadd9-167">The value must be an integer or double value.</span></span> <span data-ttu-id="eadd9-168">Gibt den neuen Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="eadd9-168">This returns the new value.</span></span> |
| `del [key]` | <span data-ttu-id="eadd9-169">Löscht den Wert, der dem **Schlüssel** zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="eadd9-169">Deletes the value associated with the **key**.</span></span> |
| `flushdb` | <span data-ttu-id="eadd9-170">_Alle_ Schlüssel und Werte in der Datenbank löschen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-170">Delete _all_ keys and values in the database.</span></span> |

<span data-ttu-id="eadd9-171">Redis verfügt über ein Befehlszeilentool (**redis-cli**), mit dem Sie direkt mit diesen Befehlen experimentieren können.</span><span class="sxs-lookup"><span data-stu-id="eadd9-171">Redis has a command-line tool (**redis-cli**) you can use to experiment directly with these commands.</span></span> <span data-ttu-id="eadd9-172">Im Folgenden finden Sie einige Beispiele.</span><span class="sxs-lookup"><span data-stu-id="eadd9-172">Here are some examples.</span></span>

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

<span data-ttu-id="eadd9-173">Hier sehen Sie ein Beispiel zur Verwendung der `INCR`-Befehle.</span><span class="sxs-lookup"><span data-stu-id="eadd9-173">Here's an example of working with the `INCR` commands.</span></span> <span data-ttu-id="eadd9-174">Diese Befehle sind praktisch, da sie unteilbare Inkremente _für mehrere Anwendungen_ bereitstellen, die den Cache verwenden.</span><span class="sxs-lookup"><span data-stu-id="eadd9-174">These are convenient because they provide atomic increments _across multiple applications_ that are using the cache.</span></span>

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

### <a name="adding-an-expiration-time-to-values"></a><span data-ttu-id="eadd9-175">Hinzufügen einer Ablaufzeit zu Werten</span><span class="sxs-lookup"><span data-stu-id="eadd9-175">Adding an expiration time to values</span></span>

<span data-ttu-id="eadd9-176">Die Zwischenspeicherung ist wichtig, da sie uns das Speichern von häufig verwendeten Werten im Arbeitsspeicher ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="eadd9-176">Caching is important because it allows us to store commonly used values in memory.</span></span> <span data-ttu-id="eadd9-177">Wir müssen jedoch auch in der Lage sein, eine Ablaufzeit für veraltete Werte festzulegen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-177">However, we also need a way to expire values when they are stale.</span></span> <span data-ttu-id="eadd9-178">In Redis wird dazu eine _Gültigkeitsdauer_ (Time To Live, TTL) auf einen Schlüssel angewendet.</span><span class="sxs-lookup"><span data-stu-id="eadd9-178">In Redis this is done by applying a _time to live_ (TTL) to a key.</span></span>

<span data-ttu-id="eadd9-179">Nach Ablauf der TTL wird der Schlüssel genau wie bei der Ausgabe des DEL-Befehls automatisch gelöscht.</span><span class="sxs-lookup"><span data-stu-id="eadd9-179">When the TTL elapses, the key is automatically deleted, exactly as if the DEL command were issued.</span></span> <span data-ttu-id="eadd9-180">Im Folgenden finden Sie einige Hinweise zum TTL-Ablauf.</span><span class="sxs-lookup"><span data-stu-id="eadd9-180">Here are some notes on TTL expirations.</span></span>

- <span data-ttu-id="eadd9-181">Ablaufzeiten können mit Sekunden- oder Millisekundengenauigkeit festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="eadd9-181">Expirations can be set using seconds or milliseconds precision.</span></span>
- <span data-ttu-id="eadd9-182">Die Auflösung der Ablaufzeit ist immer 1 Millisekunde.</span><span class="sxs-lookup"><span data-stu-id="eadd9-182">The expire time resolution is always 1 millisecond.</span></span>
- <span data-ttu-id="eadd9-183">Informationen zum Ablauf werden repliziert und dauerhaft auf dem Datenträger gespeichert. Die Zeit verstreicht gewissermaßen, während Ihr Redis-Server angehalten bleibt (d. h. Redis speichert das Datum, an dem ein Schlüssel abläuft).</span><span class="sxs-lookup"><span data-stu-id="eadd9-183">Information about expires are replicated and persisted on disk, the time virtually passes when your Redis server remains stopped (this means that Redis saves the date at which a key will expire).</span></span>

<span data-ttu-id="eadd9-184">Hier sehen Sie ein Beispiel für einen Ablauf:</span><span class="sxs-lookup"><span data-stu-id="eadd9-184">Here is an example of an expiration:</span></span>

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

## <a name="accessing-a-redis-cache-from-a-client"></a><span data-ttu-id="eadd9-185">Zugreifen auf einen Redis Cache von einem Client</span><span class="sxs-lookup"><span data-stu-id="eadd9-185">Accessing a Redis cache from a client</span></span>

<span data-ttu-id="eadd9-186">Um eine Verbindung mit einer Azure Redis Cache-Instanz herzustellen, benötigen Sie verschiedene Arten von Informationen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-186">To connect to an Azure Redis Cache instance, you'll need several pieces of information.</span></span> <span data-ttu-id="eadd9-187">Clients benötigen den Hostnamen, den Port und einen Zugriffsschlüssel für den Cache.</span><span class="sxs-lookup"><span data-stu-id="eadd9-187">Clients need the host name, port, and an access key for the cache.</span></span> <span data-ttu-id="eadd9-188">Sie können diese Informationen im Azure-Portal auf der Seite **Einstellungen > Zugriffsschlüssel** abrufen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-188">You can retrieve this information in the Azure portal through the **Settings > Access Keys** page.</span></span> 

- <span data-ttu-id="eadd9-189">Der Hostname ist die öffentliche Internetadresse Ihres Caches, die mit dem Namen des Caches erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="eadd9-189">The host name is the public Internet address of your cache, which was created using the name of the cache.</span></span> <span data-ttu-id="eadd9-190">Beispiel: `sportsresults.redis.cache.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="eadd9-190">For example `sportsresults.redis.cache.windows.net`.</span></span>

- <span data-ttu-id="eadd9-191">Der Zugriffsschlüssel fungiert als Kennwort für Ihren Cache.</span><span class="sxs-lookup"><span data-stu-id="eadd9-191">The access key acts as a password for your cache.</span></span> <span data-ttu-id="eadd9-192">Zwei Schlüssel werden erstellt: ein Primärschlüssel und ein Sekundärschlüssel.</span><span class="sxs-lookup"><span data-stu-id="eadd9-192">There are two keys created: primary and secondary.</span></span> <span data-ttu-id="eadd9-193">Sie können beide Schlüssel verwenden. Zwei Schlüssel werden für den Fall bereitgestellt, dass Sie den Primärschlüssel ändern müssen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-193">You can use either key, two are provided in case you need to change the primary key.</span></span> <span data-ttu-id="eadd9-194">Sie können alle Clients auf den Sekundärschlüssel umstellen und den Primärschlüssel erneut generieren.</span><span class="sxs-lookup"><span data-stu-id="eadd9-194">You can switch all of your clients to the secondary key, and regenerate the primary key.</span></span> <span data-ttu-id="eadd9-195">In diesem Fall werden alle Anwendungen blockiert, die den ursprünglichen Primärschlüssel verwenden.</span><span class="sxs-lookup"><span data-stu-id="eadd9-195">This would block any applications using the original primary key.</span></span> <span data-ttu-id="eadd9-196">Microsoft empfiehlt, die Schlüssel wie persönliche Kennwörter in regelmäßigen Abständen erneut zu generieren.</span><span class="sxs-lookup"><span data-stu-id="eadd9-196">Microsoft recommends periodically regenerating the keys - much like you would your personal passwords.</span></span>

> [!WARNING]
> <span data-ttu-id="eadd9-197">Die Zugriffsschlüssel sollten als vertrauliche Informationen behandelt und wie Kennwörter geschützt werden.</span><span class="sxs-lookup"><span data-stu-id="eadd9-197">Your access keys should be considered confidential information, treat them like you would a password.</span></span> <span data-ttu-id="eadd9-198">Jede Person mit einem Zugriffsschlüssel kann beliebige Vorgänge in Ihrem Cache durchführen.</span><span class="sxs-lookup"><span data-stu-id="eadd9-198">Anyone who has an access key can perform any operation on your cache!</span></span>
