Wie bereits erwähnt, handelt es sich bei Redis um eine In-Memory-NoSQL-Datenbank, die auf mehreren Servern repliziert werden kann. Sie wird häufig als Cache verwendet und kann als formale Datenbank oder sogar Nachrichtenbroker verwendet werden. 

Sie kann eine Vielzahl von Datentypen und -strukturen speichern und unterstützt eine Vielzahl von Befehlen, mit denen Sie zwischengespeicherte Daten abrufen oder Informationen zum Cache selbst abfragen können. Die Daten, mit denen Sie arbeiten, werden immer als Schlüssel-Wert-Paare gespeichert.

## <a name="executing-commands-on-the-redis-cache"></a>Ausführen von Befehlen in Redis Cache

In der Regel verwendet eine Clientanwendung eine _Clientbibliothek_, um Anforderungen zu erstellen und Befehle für eine Redis Cache-Instanz auszuführen. Eine Liste von Clientbibliotheken finden Sie direkt auf der Seite zu [Redis-Clients](https://redis.io/clients). Ein beliebter leistungsstarker Redis-Client für die .NET-Sprache ist **StackExchange.Redis**. Das Paket ist über NuGet verfügbar und kann Ihrem .NET-Code mithilfe der Befehlszeile oder der IDE hinzugefügt werden.

### <a name="connecting-to-your-redis-cache-with-stackexchangeredis"></a>Herstellen einer Verbindung mit Redis Cache mit „StackExchange.Redis“

Denken Sie daran, dass wir die Hostadresse, die Portnummer und einen Zugriffsschlüssel verwenden, um eine Verbindung mit einem Redis-Server herzustellen. Darüber hinaus bietet Azure eine _Verbindungszeichenfolge_ für einige Redis-Clients, die diese Daten zusammen in einer einzelnen Zeichenfolge bündeln.

### <a name="what-is-a-connection-string"></a>Was ist eine Verbindungszeichenfolge?

Eine Verbindungszeichenfolge ist eine einzelne Textzeile, die alle erforderlichen Informationen enthält, um eine Verbindung mit einer Redis Cache-Instanz in Azure herzustellen und sich bei dieser zu authentifizieren. Diese sieht etwa wie folgt aus (wobei die Felder **cache-name** und **password-here** mit den tatsächlichen Werten aufgefüllt sind):

```
[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False
```

> [!TIP]
> Die Verbindungszeichenfolge in Ihrer Anwendung sollte geschützt sein. Wenn die Anwendung in Azure gehostet wird, sollten Sie den Wert eventuell mit Azure Key Vault speichern.

Sie können diese Zeichenfolge an **StackExchange.Redis** übergeben, um eine Verbindung mit dem Server herzustellen. 

Beachten Sie, dass zwei zusätzliche Parameter am Ende angefügt sind: 

- **ssl**: Stellt sicher, dass die Kommunikation verschlüsselt ist.
- **abortConnection**: Ermöglicht das Herstellen einer Verbindung, auch wenn der Server zum jeweiligen Zeitpunkt nicht verfügbar ist.

Es gibt andere [optionale Parameter](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options), die Sie an die Zeichenfolge anfügen können, um die Clientbibliothek zu konfigurieren.

### <a name="creating-a-connection"></a>Erstellen einer Verbindung

Das wichtigste Verbindungsobjekt in **StackExchange.Redis** ist die Klasse `StackExchange.Redis.ConnectionMultiplexer`. Dieses Objekt abstrahiert den Prozess beim Herstellen einer Verbindung mit einem Redis-Server (oder einer Gruppe von Servern). Dieses wurde für die effiziente Verwaltung von Verbindungen optimiert und muss bestehen bleiben, solange Sie auf den Cache zugreifen müssen.

Sie erstellen eine `ConnectionMultiplexer`-Instanz mit der statischen `ConnectionMultiplexer.Connect`- oder `ConnectionMultiplexer.ConnectAsync`-Methode, indem Sie eine Verbindungszeichenfolge oder ein `ConfigurationOptions`-Objekt übergeben. 

Im Folgenden finden Sie ein einfaches Beispiel:

```csharp
using StackExchange.Redis;
...
var connectionString = "[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
    // ^^^ store and re-use this!!!
```

Wenn Sie über `ConnectionMultiplexer` verfügen, gibt es drei primäre Punkte, die Sie tun sollten:

1. Zugreifen auf eine Redis-Datenbank. Dies ist der Punkt, auf den wir uns im vorliegenden Artikel konzentrieren werden.
2. Verwenden Sie die Features von Redis zum Herausgeben bzw. Anfordern eines Abonnements. Diese liegen außerhalb des Bereichs dieses Moduls.
3. Greifen Sie für Wartungs- oder Überwachungszwecke auf einen einzelnen Server zu.

### <a name="accessing-a-redis-database"></a>Zugreifen auf eine Redis-Datenbank

Die Redis-Datenbank wird durch den Typ `IDatabase` dargestellt. Diesen können Sie mithilfe der Methode `GetDatabase()` abrufen:

```csharp
IDatabase db = redisConnection.GetDatabase();
```

> [!TIP]
> Das von `GetDatabase` zurückgegebene Objekt ist ein einfaches Objekt und muss nicht gespeichert werden. Nur `ConnectionMultiplexer` muss erhalten werden.

Wenn Sie über das Objekt `IDatabase` verfügen, können Sie Methoden für die Interaktion mit dem Cache ausführen. Alle Methoden weisen synchrone und asynchrone Versionen auf, die `Task`-Objekte zurückgeben, damit sie mit den Schlüsselwörtern `async` und `await` kompatibel sind.

Im Folgenden finden Sie ein Beispiel zum Speichern eines Schlüssel-Wert-Paares im Cache:

```csharp
bool wasSet = db.StringSet("favorite:flavor", "i-love-rocky-road");
```

Die Methode `StringSet` gibt `bool` zurück, was darauf hinweist, dass der Wert festgelegt (`true`) oder nicht festgelegt (`false`) wurde. Anschließend kann der Wert mit der Methode `StringGet` abgerufen werden:

```csharp
string value = db.StringGet("favorite:flavor");
Console.WriteLine(value); // displays: ""i-love-rocky-road""
```

#### <a name="getting-and-setting-binary-values"></a>Abrufen und Festlegen von Binärwerten

Denken Sie daran, dass Redis-Schlüssel und -Werte  _binärsicher_ sind. Diese Methoden können verwendet werden, um Binärdaten zu speichern. Mithilfe impliziter Konvertierungsoperatoren für `byte[]`-Typen können Sie unkompliziert mit den Daten arbeiten:

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
> **StackExchange.Redis** stellt Schlüssel mithilfe des Typs `RedisKey` dar. Diese Klasse weist implizite Konvertierungen in und von `string` und `byte[]` auf, sodass sowohl Text- als auch Binärschlüssel problemlos verwendet werden können. Werte werden durch den Typ `RedisValue` dargestellt. Wie bei `RedisKey` stehen Ihnen implizite Konvertierungen zur Verfügung, mit denen Sie `string` oder `byte[]` übergeben können.

#### <a name="other-common-operations"></a>Andere gängige Vorgänge

Die Schnittstelle `IDatabase` umfasst weitere Methoden für die Arbeit mit Redis Cache. Es gibt Methoden zum Arbeiten mit Hashes, Listen, Gruppen und sortierten Mengen.

Im Folgenden werden gängigere Beispiele vorgestellt, die mit einzelnen Schlüsseln arbeiten. Sie können [den Quellcode](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs) für die Schnittstelle lesen, um die vollständige Liste anzuzeigen.

| Methode | Beschreibung |
|--------|-------------|
| `CreateBatch` | Erstellt eine _Gruppe von Vorgängen_, die an den Server als einzelne Einheit gesendet, jedoch nicht unbedingt als Einheit verarbeitet werden. |
| `CreateTransaction` | Erstellt eine Gruppe von Vorgängen, die an den Server als einzelne Einheit gesendet _und_ als einzelne Einheit auf dem Server verarbeitet werden. |
| `KeyDelete` | Löscht das Schlüssel-Wert-Paar. |
| `KeyExists` | Gibt zurück, ob der angegebene Schlüssel im Cache vorhanden ist. |
| `KeyExpire` | Legt den Ablauf der Gültigkeitsdauer (Time to Live, TTL) eines Schlüssels fest. |
| `KeyRename` | Benennt einen Schlüssel. |
| `KeyTimeToLive` | Gibt die TTL für einen Schlüssel zurück. |
| `KeyType` | Gibt die Zeichenfolgendarstellung des Typs des Werts zurück, der im Schlüssel gespeichert ist. Zu den verschiedenen Typen, die zurückgegeben werden können, zählen Folgende: „string“, „list“, „set“, „zset“ und „hash“. |
       
### <a name="executing-other-commands"></a>Ausführen anderer Befehle

Das Objekt `IDatabase` weist eine `Execute`- und `ExecuteAsync`-Methode auf, mit der Textbefehle an den Redis-Server übergeben werden können. Beispiel:

```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString()); // displays: "PONG"
```

Die Methoden `Execute` und `ExecuteAsync` geben ein `RedisResult`-Objekt zurück, das Daten mit zwei Eigenschaften speichert:

- `Type`: Gibt `string` zurück, was auf den Typ des Ergebnisses hinweist, z.B. „STRING“ und „INTEGER“.
- `IsNull`: Ein True/False-Wert, der erkannt wird, wenn das Ergebnis `null` lautet.

Anschließend können Sie `ToString()` in `RedisResult` verwenden, um den tatsächlichen Rückgabewert zu erhalten.

Sie können mit `Execute` beliebige unterstützte Befehle ausführen, beispielsweise können alle mit dem Cache verbundene Clients („CLIENT-LIST“) abgerufen werden:

```csharp
var result = await db.ExecuteAsync("client", "list");
Console.WriteLine($"Type = {result.Type}\r\nResult = {result}");
```

Hierdurch würden alle verbundenen Clients ausgegeben werden:

```output
Type = BulkString
Result = id=9469 addr=16.183.122.154:54961 fd=18 name=DESKTOP-AAAAAA age=0 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=subscribe numops=5
id=9470 addr=16.183.122.155:54967 fd=13 name=DESKTOP-BBBBBB age=0 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=client numops=17
```

### <a name="storing-more-complex-values"></a>Speichern von komplexeren Werten
Redis ist auf sicheren Binärzeichenfolgen aufgebaut, Sie können jedoch Objektdiagramme zwischenspeichern, indem Sie sie in ein Textformat serialisieren, in der Regel XML oder JSON. Nehmen Sie beispielsweise an, das Objekt `GameStats` für unsere Statistiken sieht wie folgt aus:

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

Wir könnten die Bibliothek **Newtonsoft.Json** verwenden, um eine Instanz dieses Objekts in eine Zeichenfolge umzuwandeln:

```csharp
var stat = new GameStat("Soccer", new DateTime(1950, 7, 16), "FIFA World Cup", 
                new[] { "Uruguay", "Brazil" },
                new[] { ("Uruguay", 2), ("Brazil", 1) });

string serializedValue = Newtonsoft.Json.JsonConvert.SerializeObject(stat);
bool added = db.StringSet("event:1950-world-cup", serializedValue);
```

Wir könnten diese abrufen und anhand des umgekehrten Vorgangs wieder in ein Objekt konvertieren:

```csharp
var result = db.StringGet("event:1950-world-cup");
var stat = Newtonsoft.Json.JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine(stat.Sport); // displays "Soccer"
```

## <a name="cleaning-up-the-connection"></a>Bereinigen der Verbindung
Sobald die Redis-Verbindung hergestellt ist, können Sie `ConnectionMultiplexer` **Löschen**. Dadurch werden alle Verbindungen und die Kommunikation mit dem Server getrennt.

```csharp
redisConnection.Dispose();
redisConnection = null;
```

Nun erstellen wir eine Anwendung und führen ein paar einfache Aufgaben mit Redis Cache durch.