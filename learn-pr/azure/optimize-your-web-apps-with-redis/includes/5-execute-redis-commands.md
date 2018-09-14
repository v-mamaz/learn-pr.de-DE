Wie bereits erwähnt, ist Redis eine in-Memory-NoSQL-Datenbank, die auf mehreren Servern repliziert werden kann. Es wird häufig als Zwischenspeicher verwendet und kann als eine formale Datenbank oder sogar nachrichtenbroker verwendet werden. 

Sie können eine Vielzahl von Datentypen und-Strukturen speichern und unterstützt eine Vielzahl von Befehlen, dass Sie zum Abrufen von zwischengespeicherten Daten oder Abfrage Informationen zu der Cache selbst ausgeben können. Die Daten, mit denen Sie zusammenarbeiten, ist immer als Schlüssel/Wert-Paare gespeichert.

## <a name="executing-commands-on-the-redis-cache"></a>Ausführen von Befehlen auf dem Redis cache

In der Regel eine Clientanwendung verwendet einen _Clientbibliothek_ bilden von Anforderungen, und führen Sie Befehle für einen Redis-Cache. Sie erhalten eine Liste von Clientbibliotheken direkt unter der [Redis-Clients Seite](https://redis.io/clients). Ein beliebter Hochleistungs-Redis-Client für die .NET-Sprache ist **StackExchange.Redis**. Das Paket ist über NuGet verfügbar und kann Ihrem .NET Code mithilfe der Befehlszeile oder IDE hinzugefügt werden.

### <a name="connecting-to-your-redis-cache-with-stackexchangeredis"></a>Herstellen einer Verbindung mit dem Redis-Cache mit "stackexchange.redis"

Denken Sie daran, dass wir die Hostadresse, Portnummer und einen Zugriffsschlüssel verwenden, für die Verbindung mit einem Redis-Server. Darüber hinaus bietet Azure eine _Verbindungszeichenfolge_ für einige Redis-Clients, die diese Daten zusammen in einer einzelnen Zeichenfolge gebündelt.

### <a name="what-is-a-connection-string"></a>Was ist eine Verbindungszeichenfolge?

Eine Verbindungszeichenfolge ist eine einzelne Textzeile, die enthält alle erforderlichen Teile der Informationen, die eine Verbindung herzustellen und auf einen Redis-Cache in Azure zu authentifizieren. Es sieht etwa wie folgt (mit der **Cachename** und **Kennwort-Here** Felder mit echten Werten gefüllt):

```
[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False
```

> [!TIP]
> Die Verbindungszeichenfolge sollte in Ihrer Anwendung geschützt werden. Wenn die Anwendung in Azure gehostet wird, erwägen Sie, die Azure Key Vault zum Speichern des Werts.

Sie können diese Zeichenfolge übergeben **"stackexchange.redis"** um eine Verbindung mit dem Server herzustellen. 

Beachten Sie, dass es zwei zusätzliche Parameter am Ende: 

- **SSL** – stellt sicher, dass die Kommunikation verschlüsselt wird.
- **AbortConnection** – Dadurch wird eine Verbindung erstellt werden, auch wenn der Server, die zu diesem Zeitpunkt nicht verfügbar ist.

Es gibt mehrere andere [optionale Parameter](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options) können Sie auf die Zeichenfolge so konfigurieren Sie die Clientbibliothek anfügen.

### <a name="creating-a-connection"></a>Erstellen einer Verbindung

Das wichtigste Verbindungsobjekt in **"stackexchange.redis"** ist die `StackExchange.Redis.ConnectionMultiplexer` Klasse. Dieses Objekts abstrahiert den Prozess der verbindungsherstellung mit einem Redis-Server (oder eine Gruppe von Servern). Es wurde optimiert, um Verbindungen effizient zu verwalten und soll, ist es jedoch Zugriff auf den Cache bleiben muss.

Sie erstellen eine `ConnectionMultiplexer` -Instanz mit der statischen `ConnectionMultiplexer.Connect` oder `ConnectionMultiplexer.ConnectAsync` Methode und übergeben entweder eine Verbindungszeichenfolge oder ein `ConfigurationOptions` Objekt. 

Hier ist ein einfaches Beispiel:

```csharp
using StackExchange.Redis;
...
var connectionString = "[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
    // ^^^ store and re-use this!!!
```

Nachdem Sie haben eine `ConnectionMultiplexer`, es gibt 3 Hauptmerkmale, die Sie tun möchten:

1. Zugriff auf einen Redis-Datenbank. Dies ist, was konzentrieren wir uns hier.
2. Stellen Sie mithilfe der Verleger/Subscript-Features von Redis. Dies ist außerhalb des Bereichs dieses Moduls.
3. Zugriff auf einen einzelnen Server für die Wartung oder Überwachungszwecken.

### <a name="accessing-a-redis-database"></a>Zugreifen auf eine Redis-Datenbank

Die Redis-Datenbank wird dargestellt, durch die `IDatabase` Typ. Können Sie abrufen, mithilfe der `GetDatabase()` Methode:

```csharp
IDatabase db = redisConnection.GetDatabase();
```

> [!TIP]
> Das von zurückgegebene Objekt `GetDatabase` ist ein einfaches Objekt, und muss nicht gespeichert werden. Nur die `ConnectionMultiplexer` aktiv gehalten werden muss.

Nachdem Sie haben eine `IDatabase` Objekt ist, können Sie Methoden für die Interaktion mit dem Cache ausführen. Alle Methoden besitzen synchrone und asynchrone Versionen der zurückgibt `Task` Objekte, damit sie kompatibel mit der `async` und `await` Schlüsselwörter.

Hier ist ein Beispiel für ein Schlüssel-Wert im Cache zu speichern:

```csharp
bool wasSet = db.StringSet("favorite:flavor", "i-love-rocky-road");
```

Die `StringSet` Methode gibt eine `bool` , der angibt, ob der Wert festgelegt wurde (`true`) oder nicht (`false`). Wir können dann abrufen, den Wert mit dem `StringGet` Methode:

```csharp
string value = db.StringGet("favorite:flavor");
Console.WriteLine(value); // displays: ""i-love-rocky-road""
```

#### <a name="getting-and-setting-binary-values"></a>Abrufen und Festlegen von Binärwerten

Denken Sie daran, dass die Redis-Schlüssel und Werte sind _Binärdatei sicher_. Die gleichen Methoden können verwendet werden, um binäre Daten zu speichern. Es sind implizite Konvertierungsoperatoren zum Arbeiten mit `byte[]` Typen, sodass Sie auf natürliche Weise mit den Daten arbeiten können:

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
> **"Stackexchange.redis"** stellt die Schlüssel mithilfe der `RedisKey` Typ. Diese Klasse verfügt über implizite Konvertierungen in und aus beiden `string` und `byte[]`, sodass sowohl Text- und Schlüssel, ohne alle Komplikation verwendet werden soll. Werte werden durch dargestellt die `RedisValue` Typ. Wie bei `RedisKey`, es sind implizite Konvertierungen in an Sie übergeben können `string` oder `byte[]`.

#### <a name="other-common-operations"></a>Andere gängige Vorgänge

Die `IDatabase` Schnittstelle umfasst mehrere andere Methoden zum Arbeiten mit den Redis-Cache. Es gibt Methoden zum Arbeiten mit Hashes, Listen, Sätze und sortierte Sätze.

Hier sind einige der häufigeren, die mit den einzelnen Schlüsseln arbeiten, können Sie [lesen den Quellcode](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs) für die Schnittstelle für die vollständige Liste anzuzeigen.

| Methode | Beschreibung |
|--------|-------------|
| `CreateBatch` | Erstellt eine _Gruppe von Vorgängen_ , werden an den Server als einzelne Einheit gesendet, aber nicht unbedingt als eine Einheit verarbeitet. |
| `CreateTransaction` | Erstellt eine Gruppe von Vorgängen, die als einzelne Einheit an den Server gesendet werden _und_ auf dem Server als eine Einheit verarbeitet. |
| `KeyDelete` | Löschen Sie die Schlüssel-Wert. |
| `KeyExists` | Gibt zurück, ob der angegebene Schlüssel im Cache vorhanden ist. |
| `KeyExpire` | Legt ein Ablauf für die Time-to-live (TTL) für einen Schlüssel fest. |
| `KeyRename` | Benennt einen Schlüssel an. |
| `KeyTimeToLive` | Gibt die Gültigkeitsdauer (TTL) für einen Schlüssel zurück. |
| `KeyType` | Gibt die Zeichenfolgendarstellung des Typs von den gespeicherten Schlüssel-Wert zurück. Die verschiedenen Typen, die zurückgegeben werden können, sind: eine Zeichenfolge, list, festlegen, Zset und Hash. |
       
### <a name="executing-other-commands"></a>Ausführen anderer Befehle

Die `IDatabase` Objekt verfügt über eine `Execute` und `ExecuteAsync` Methode, mit Textbefehlen an den Redis-Server übergeben werden kann. Beispiel:

```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString()); // displays: "PONG"
```

Die `Execute` und `ExecuteAsync` Methoden zurückgeben einer `RedisResult` Objekt, das eine Daten besitzt, die zwei Eigenschaften enthält:

- `Type` Gibt eine `string` , der angibt, der des Typs des Ergebnisses: "STRING", "INTEGER" usw.
- `IsNull` Ein True/False-Wert zu erkennen, wenn das Ergebnis ist `null`.

Anschließend können Sie `ToString()` auf die `RedisResult` zum Abrufen der tatsächliche Wert zurückgeben.

Sie können `Execute` unterstützt Sie Befehle ausführen: Beispielsweise können wir alle verbundenen Clients an den Cache ("CLIENT-LIST") abrufen:

```csharp
var result = await db.ExecuteAsync("client", "list");
Console.WriteLine($"Type = {result.Type}\r\nResult = {result}");
```

Dadurch würden alle verbundenen Clients ausgeben:

```output
Type = BulkString
Result = id=9469 addr=16.183.122.154:54961 fd=18 name=DESKTOP-AAAAAA age=0 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=subscribe numops=5
id=9470 addr=16.183.122.155:54967 fd=13 name=DESKTOP-BBBBBB age=0 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=client numops=17
```

### <a name="storing-more-complex-values"></a>Speichern von komplexen Werten
Redis ist für sichere Binärzeichenfolgen orientiert, jedoch können Sie Zwischenspeichern deaktiviert Objektdiagramme durch Serialisierung ein Textformat – in der Regel XML oder JSON. Angenommen, z. B. für unsere Statistiken, wir haben eine `GameStats` Objekt die wie folgt aussieht:

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

Wir können die **"newtonsoft.JSON"** Bibliothek, um eine Instanz dieses Objekts in eine Zeichenfolge zu aktivieren:

```csharp
var stat = new GameStat("Soccer", new DateTime(1950, 7, 16), "FIFA World Cup", 
                new[] { "Uruguay", "Brazil" },
                new[] { ("Uruguay", 2), ("Brazil", 1) });

string serializedValue = Newtonsoft.Json.JsonConvert.SerializeObject(stat);
bool added = db.StringSet("event:1950-world-cup", serializedValue);
```

Wir könnten abzurufen, und schalten Sie ihn wieder in ein Objekt mit der umgekehrte Vorgang:

```csharp
var result = db.StringGet("event:1950-world-cup");
var stat = Newtonsoft.Json.JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine(stat.Sport); // displays "Soccer"
```

## <a name="cleaning-up-the-connection"></a>Bereinigen die Verbindung
Sobald Sie mit der Redis-Verbindung haben, können Sie **Dispose** der `ConnectionMultiplexer`. Dadurch werden alle Verbindungen und Herunterfahren der Kommunikation mit dem Server geschlossen.

```csharp
redisConnection.Dispose();
redisConnection = null;
```

Erstellen Sie eine Anwendung, und einige einfache Aufgaben mit der Redis-Cache.