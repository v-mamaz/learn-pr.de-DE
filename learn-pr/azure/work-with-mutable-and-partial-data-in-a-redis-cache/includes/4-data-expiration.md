<span data-ttu-id="6098f-101">Daten sind nicht immer dauerhaft, und es kann vorkommen, dass Sie sie zu einem bestimmten Zeitpunkt löschen möchten.</span><span class="sxs-lookup"><span data-stu-id="6098f-101">Data is not always permanent and there are times you would like to delete it at a specific time.</span></span> <span data-ttu-id="6098f-102">In Ihrer Instant Messaging-Anwendung können Benutzer beispielsweise den Anzeigenamen des Gruppenchats festlegen. Sie möchten jedoch, dass der Name nach einer Stunde zurückgesetzt wird.</span><span class="sxs-lookup"><span data-stu-id="6098f-102">For example, in your instant messaging application, users can set the display name of the group chat, however, you want the name to reset after one hour.</span></span> <span data-ttu-id="6098f-103">Sie könnten dies erreichen, indem Sie Ihre eigene serverseitige Logik schreiben, die einen Stundentimer festlegt und den Namen löscht.</span><span class="sxs-lookup"><span data-stu-id="6098f-103">You could accomplish this by writing your own server-side logic that set an hour timer and deleted the name.</span></span> <span data-ttu-id="6098f-104">Redis unterstützt jedoch den Ablauf von Daten. Dies ist ein Feature, das dies automatisch und ohne Schreiben zusätzlicher Programmlogik erledigt.</span><span class="sxs-lookup"><span data-stu-id="6098f-104">However, Redis supports data expiration, which is a feature that does this automatically without writing additional logic.</span></span>

<span data-ttu-id="6098f-105">Hier erfahren Sie mehr über die gebräuchlichen Redis-Befehle zur Implementierung des Datenablaufs.</span><span class="sxs-lookup"><span data-stu-id="6098f-105">Here, you'll learn about the common Redis commands to implement data expiration.</span></span>

## <a name="what-is-data-expiration"></a><span data-ttu-id="6098f-106">Was ist Datenablauf?</span><span class="sxs-lookup"><span data-stu-id="6098f-106">What is data expiration?</span></span>

<span data-ttu-id="6098f-107">Datenablauf ist ein Feature, das einen Schlüssel und Wert im Cache nach einem festgelegten Zeitraum automatisch löschen kann.</span><span class="sxs-lookup"><span data-stu-id="6098f-107">Data expiration is a feature that can automatically delete a key and value in the cache after a set amount of time.</span></span>

## <a name="why-use-data-expiration"></a><span data-ttu-id="6098f-108">Warum sollte Datenablauf verwendet werden?</span><span class="sxs-lookup"><span data-stu-id="6098f-108">Why use data expiration?</span></span>

<span data-ttu-id="6098f-109">Datenablauf wird häufig in Situationen verwendet, in denen die Daten, die Sie speichern, kurzlebig sind.</span><span class="sxs-lookup"><span data-stu-id="6098f-109">Data expiration is commonly used in situations where the data you're storing is short-lived.</span></span>  <span data-ttu-id="6098f-110">Dies ist wichtig, da es sich bei Redis um eine In-Memory-Datenbank handelt und nicht so viel Speicher verfügbar ist, wie es bei der Speicherung auf einem Datenträger der Fall wäre.</span><span class="sxs-lookup"><span data-stu-id="6098f-110">This is important because Redis is an in-memory database and you don't have as much memory available to use as you would if you were storing on disk.</span></span> <span data-ttu-id="6098f-111">Da Sie mit Redis nur begrenzt über Speicherplatz verfügen, sollten Sie sicherstellen, dass Sie nur Daten speichern, die wichtig sind.</span><span class="sxs-lookup"><span data-stu-id="6098f-111">Since you have limited storage with Redis, you want to make sure you're only storing data that is important.</span></span> <span data-ttu-id="6098f-112">Wenn die Daten nicht für einen längeren Zeitraum verfügbar sein müssen, stellen Sie sicher, dass Sie eine Ablaufzeit festlegen.</span><span class="sxs-lookup"><span data-stu-id="6098f-112">If the data doesn't need to be around for a long time, make sure you set an expiration.</span></span>

## <a name="how-to-use-data-expiration-in-redis"></a><span data-ttu-id="6098f-113">Verwenden von Datenablauf in Redis</span><span class="sxs-lookup"><span data-stu-id="6098f-113">How to use data expiration in Redis</span></span>

<span data-ttu-id="6098f-114">Es gibt verschiedene Befehle zum Implementieren und Verwalten des Datenablaufs in Redis:</span><span class="sxs-lookup"><span data-stu-id="6098f-114">There are different commands to implement and manage data expiration in Redis:</span></span>

- <span data-ttu-id="6098f-115">`EXPIRE`: Legt das Timeout eines Schlüssels in Sekunden fest.</span><span class="sxs-lookup"><span data-stu-id="6098f-115">`EXPIRE`: Sets the timeout of a key in seconds</span></span>
- <span data-ttu-id="6098f-116">`PEXIRE`: Legt das Timeout eines Schlüssels in Millisekunden fest.</span><span class="sxs-lookup"><span data-stu-id="6098f-116">`PEXIRE`: Sets the timeout of a key in milliseconds</span></span>
- <span data-ttu-id="6098f-117">`EXPIREAT`: Legt das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Sekunden fest.</span><span class="sxs-lookup"><span data-stu-id="6098f-117">`EXPIREAT`: Sets the timeout of a key using an absolute Unix timestamp in seconds</span></span>
- <span data-ttu-id="6098f-118">`PEXPIREAT`: Legt das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Millisekunden fest.</span><span class="sxs-lookup"><span data-stu-id="6098f-118">`PEXPIREAT`: Sets the timeout of a key using an absolute Unix timestamp in milliseconds</span></span>
- <span data-ttu-id="6098f-119">`TTL`: Gibt die verbleibende Zeit in Sekunden zurück, bis ein Schlüssel gelöscht wird.</span><span class="sxs-lookup"><span data-stu-id="6098f-119">`TTL`: Returns the remaining time a key has to live in seconds</span></span>
- <span data-ttu-id="6098f-120">`PTTL`: Gibt die verbleibende Zeit in Millisekunden zurück, bis ein Schlüssel gelöscht wird.</span><span class="sxs-lookup"><span data-stu-id="6098f-120">`PTTL`: Returns the remaining time a key has to live in milliseconds</span></span>
- <span data-ttu-id="6098f-121">`PERSIST`: Bewirkt, dass ein Schlüssel nie abläuft.</span><span class="sxs-lookup"><span data-stu-id="6098f-121">`PERSIST`: Makes a key never expire</span></span>

<span data-ttu-id="6098f-122">Der am häufigsten verwendete Befehl ist `EXPIRE`. Wir verwenden ihn in diesem Modul durchgängig.</span><span class="sxs-lookup"><span data-stu-id="6098f-122">The most common command is `EXPIRE` and we'll use it throughout this module.</span></span>

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a><span data-ttu-id="6098f-123">Beispiel für Datenablauf mit C# und ServiceStack.Redis</span><span class="sxs-lookup"><span data-stu-id="6098f-123">Example of data expiration using C# and ServiceStack.Redis</span></span>

<span data-ttu-id="6098f-124">Denken Sie daran, dass wir uns bei der Verwendung einer Clientbibliothek wie **ServiceStack.Redis** keine Sorgen darüber machen müssen, dass wir uns an die Low-Level Redis-Befehle erinnern.</span><span class="sxs-lookup"><span data-stu-id="6098f-124">Remember, when using a client library like **ServiceStack.Redis**, we don't have to worry about remembering the low-level Redis commands.</span></span> <span data-ttu-id="6098f-125">Stattdessen können wir eine einfache C#-Methoden verwenden.</span><span class="sxs-lookup"><span data-stu-id="6098f-125">Instead, we can use simple C# methods.</span></span>

```csharp
public static void SetGroupChatName(string groupChatID, string chatName)
{
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create a key for group chat display names
        string key = groupChatID + "displayName";

        //Set the group chat display name
        redisClient.Set(key, chatName);

        //Set the expiration for one hour
        redisClient.Expire(key, 3600);
    }
}
```

<span data-ttu-id="6098f-126">Mit Redis können Sie Daten nach einer bestimmten Zeit automatisch mithilfe des Datenablaufs löschen.</span><span class="sxs-lookup"><span data-stu-id="6098f-126">Redis allows you to delete data automatically after a set amount of time using data expiration.</span></span> <span data-ttu-id="6098f-127">Dies ist wichtig, da es sich bei Redis um eine In-Memory-Datenbank handelt und nicht so viel Speicher verfügbar ist, wie es bei der Speicherung auf einem Datenträger der Fall wäre.</span><span class="sxs-lookup"><span data-stu-id="6098f-127">This is important because Redis is an in-memory database, and you don't have as much memory available as you would with storing data on disk.</span></span> <span data-ttu-id="6098f-128">Wenn die Daten, die Sie speichern, nicht für einen längeren Zeitraum verfügbar sein müssen, stellen Sie sicher, dass Sie eine Ablaufzeit festlegen.</span><span class="sxs-lookup"><span data-stu-id="6098f-128">If the data you're storing doesn't need to be around for a long time, make sure you set an expiration.</span></span>