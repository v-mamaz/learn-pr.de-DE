<span data-ttu-id="28f3e-101">Daten sind nicht immer dauerhaft, und es kann vorkommen, dass Sie sie zu einem bestimmten Zeitpunkt löschen möchten.</span><span class="sxs-lookup"><span data-stu-id="28f3e-101">Data is not always permanent, and there are times you would like to delete it at a specific time.</span></span> <span data-ttu-id="28f3e-102">In Ihrer Instant Messaging-Anwendung können Benutzer beispielsweise den Anzeigenamen des Gruppenchats festlegen.</span><span class="sxs-lookup"><span data-stu-id="28f3e-102">For example, in your instant messaging application, users can set the display name of the group chat.</span></span> <span data-ttu-id="28f3e-103">Sie möchten jedoch, dass der Name nach einer Stunde zurückgesetzt wird.</span><span class="sxs-lookup"><span data-stu-id="28f3e-103">However, you want the name to reset after one hour.</span></span> <span data-ttu-id="28f3e-104">Dies können Sie erreichen, indem Sie Ihre eigene serverseitige Logik schreiben, die einen Stundentimer festlegt und den Namen löscht.</span><span class="sxs-lookup"><span data-stu-id="28f3e-104">You could accomplish this by writing your own server-side logic that set an hour timer and deleted the name.</span></span> <span data-ttu-id="28f3e-105">Der Azure Redis Cache unterstützt jedoch den Datenablauf. Das Feature erledigt dies automatisch, sodass Sie keine zusätzliche Logik schreiben müssen.</span><span class="sxs-lookup"><span data-stu-id="28f3e-105">However, Azure Redis Cache supports data expiration, which is a feature that does this automatically without writing additional logic.</span></span>

<span data-ttu-id="28f3e-106">Hier erfahren Sie mehr über die gebräuchlichen Redis-Befehle zur Implementierung des Datenablaufs.</span><span class="sxs-lookup"><span data-stu-id="28f3e-106">Here, you'll learn about the common Redis commands to implement data expiration.</span></span>

## <a name="what-is-data-expiration"></a><span data-ttu-id="28f3e-107">Was ist Datenablauf?</span><span class="sxs-lookup"><span data-stu-id="28f3e-107">What is data expiration?</span></span>

<span data-ttu-id="28f3e-108">Datenablauf ist ein Feature, das einen Schlüssel und Wert im Cache nach einem festgelegten Zeitraum automatisch löschen kann.</span><span class="sxs-lookup"><span data-stu-id="28f3e-108">Data expiration is a feature that can automatically delete a key and value in the cache after a set amount of time.</span></span>

## <a name="why-use-data-expiration"></a><span data-ttu-id="28f3e-109">Warum sollte Datenablauf verwendet werden?</span><span class="sxs-lookup"><span data-stu-id="28f3e-109">Why use data expiration?</span></span>

<span data-ttu-id="28f3e-110">Der Datenablauf wird häufig in Situationen verwendet, in denen die gespeicherten Daten kurzlebig sind.</span><span class="sxs-lookup"><span data-stu-id="28f3e-110">Data expiration is commonly used in situations where the data you're storing is short-lived.</span></span>  <span data-ttu-id="28f3e-111">Dies ist wichtig, da es sich beim Azure Redis Cache um eine In-Memory-Datenbank handelt und nicht so viel Speicher verfügbar ist, wie es bei der Speicherung auf einem Datenträger der Fall wäre.</span><span class="sxs-lookup"><span data-stu-id="28f3e-111">This is important because Azure Redis Cache is an in-memory database and you don't have as much memory available to use as you would if you were storing on disk.</span></span> <span data-ttu-id="28f3e-112">Da Sie mit dem Azure Redis Cache nur begrenzt über Speicherplatz verfügen, sollten Sie sicherstellen, dass Sie nur wichtige Daten speichern.</span><span class="sxs-lookup"><span data-stu-id="28f3e-112">Since you have limited storage with Azure Redis Cache, you want to make sure you're only storing data that is important.</span></span> <span data-ttu-id="28f3e-113">Wenn die Daten nicht für einen längeren Zeitraum verfügbar sein müssen, stellen Sie sicher, dass Sie eine Ablaufzeit festlegen.</span><span class="sxs-lookup"><span data-stu-id="28f3e-113">If the data doesn't need to be around for a long time, make sure you set an expiration.</span></span>

## <a name="how-to-use-data-expiration-in-azure-redis-cache"></a><span data-ttu-id="28f3e-114">Verwenden des Datenablaufs im Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="28f3e-114">How to use data expiration in Azure Redis Cache</span></span>

<span data-ttu-id="28f3e-115">Es gibt verschiedene Befehle zum Implementieren und Verwalten des Datenablaufs in Azure Redis Cache:</span><span class="sxs-lookup"><span data-stu-id="28f3e-115">There are different commands to implement and manage data expiration in Azure Redis Cache:</span></span>

- <span data-ttu-id="28f3e-116">`EXPIRE`: Legt das Timeout eines Schlüssels in Sekunden fest.</span><span class="sxs-lookup"><span data-stu-id="28f3e-116">`EXPIRE`: Sets the timeout of a key in seconds</span></span>
- <span data-ttu-id="28f3e-117">`PEXPIRE`: Legt das Timeout eines Schlüssels in Millisekunden fest.</span><span class="sxs-lookup"><span data-stu-id="28f3e-117">`PEXPIRE`: Sets the timeout of a key in milliseconds</span></span>
- <span data-ttu-id="28f3e-118">`EXPIREAT`: Legt das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Sekunden fest.</span><span class="sxs-lookup"><span data-stu-id="28f3e-118">`EXPIREAT`: Sets the timeout of a key using an absolute Unix timestamp in seconds</span></span>
- <span data-ttu-id="28f3e-119">`PEXPIREAT`: Legt das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Millisekunden fest.</span><span class="sxs-lookup"><span data-stu-id="28f3e-119">`PEXPIREAT`: Sets the timeout of a key using an absolute Unix timestamp in milliseconds</span></span>
- <span data-ttu-id="28f3e-120">`TTL`: Gibt die verbleibende Zeit in Sekunden zurück, bis ein Schlüssel gelöscht wird.</span><span class="sxs-lookup"><span data-stu-id="28f3e-120">`TTL`: Returns the remaining time a key has to live in seconds</span></span>
- <span data-ttu-id="28f3e-121">`PTTL`: Gibt die verbleibende Zeit in Millisekunden zurück, bis ein Schlüssel gelöscht wird.</span><span class="sxs-lookup"><span data-stu-id="28f3e-121">`PTTL`: Returns the remaining time a key has to live in milliseconds</span></span>
- <span data-ttu-id="28f3e-122">`PERSIST`: Bewirkt, dass ein Schlüssel nie abläuft.</span><span class="sxs-lookup"><span data-stu-id="28f3e-122">`PERSIST`: Makes a key never expire</span></span>

<span data-ttu-id="28f3e-123">Der am häufigsten verwendete Befehl ist `EXPIRE`. Er wird in diesem Modul durchgängig verwendet.</span><span class="sxs-lookup"><span data-stu-id="28f3e-123">The most common command is `EXPIRE`, and we'll use it throughout this module.</span></span>

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a><span data-ttu-id="28f3e-124">Beispiel für Datenablauf mit C# und ServiceStack.Redis</span><span class="sxs-lookup"><span data-stu-id="28f3e-124">Example of data expiration using C# and ServiceStack.Redis</span></span>

<span data-ttu-id="28f3e-125">Denken Sie daran, dass Sie sich bei der Verwendung einer Clientbibliothek wie **ServiceStack.Redis** keine Sorgen darüber machen müssen, dass Sie sich an spezifische Befehle des Azure Redis Cache erinnern.</span><span class="sxs-lookup"><span data-stu-id="28f3e-125">Remember, when using a client library like **ServiceStack.Redis**, we don't have to worry about remembering the low-level Azure Redis Cache commands.</span></span> <span data-ttu-id="28f3e-126">Stattdessen können Sie einfache C#-Methoden verwenden.</span><span class="sxs-lookup"><span data-stu-id="28f3e-126">Instead, we can use simple C# methods.</span></span>

```csharp
public static void SetGroupChatName(string groupChatID, string chatName)
{
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create a key for group chat display names
        string key = groupChatID + "displayName";

        //Set the group chat display name
        redisClient.SetValue(key, chatName);

        //Set the expiration for one hour
        redisClient.Expire(key, 3600);
    }
}
```

<span data-ttu-id="28f3e-127">Mit dem Azure Redis Cache können Sie Daten nach einer bestimmten Zeit automatisch mithilfe des Datenablaufs löschen.</span><span class="sxs-lookup"><span data-stu-id="28f3e-127">Azure Redis Cache allows you to delete data automatically after a set amount of time using data expiration.</span></span> <span data-ttu-id="28f3e-128">Dies ist wichtig, da es sich beim Azure Redis Cache um eine In-Memory-Datenbank handelt und nicht so viel Speicher verfügbar ist, wie es bei der Speicherung auf einem Datenträger der Fall wäre.</span><span class="sxs-lookup"><span data-stu-id="28f3e-128">This is important because Azure Redis Cache is an in-memory database, and you don't have as much memory available as you would with storing data on disk.</span></span> <span data-ttu-id="28f3e-129">Wenn die gespeicherten Daten nicht für einen längeren Zeitraum verfügbar sein müssen, sollten Sie sicherstellen, dass Sie eine Ablaufzeit festlegen.</span><span class="sxs-lookup"><span data-stu-id="28f3e-129">If the data you're storing doesn't need to be around for a long time, make sure you set an expiration.</span></span>