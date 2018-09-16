Daten sind nicht immer dauerhaft, und es kann vorkommen, dass Sie sie zu einem bestimmten Zeitpunkt löschen möchten. In Ihrer Instant Messaging-Anwendung können Benutzer beispielsweise den Anzeigenamen des Gruppenchats festlegen. Sie möchten jedoch, dass der Name nach einer Stunde zurückgesetzt wird. Sie könnten dies erreichen, indem Sie Ihre eigene serverseitige Logik schreiben, die einen Stundentimer festlegt und den Namen löscht. Redis unterstützt jedoch den Ablauf von Daten. Dies ist ein Feature, das dies automatisch und ohne Schreiben zusätzlicher Programmlogik erledigt.

Hier erfahren Sie mehr über die gebräuchlichen Redis-Befehle zur Implementierung des Datenablaufs.

## <a name="what-is-data-expiration"></a>Was ist Datenablauf?

Datenablauf ist ein Feature, das einen Schlüssel und Wert im Cache nach einem festgelegten Zeitraum automatisch löschen kann.

## <a name="why-use-data-expiration"></a>Warum sollte Datenablauf verwendet werden?

Datenablauf wird häufig in Situationen verwendet, in denen die Daten, die Sie speichern, kurzlebig sind.  Dies ist wichtig, da es sich bei Redis um eine In-Memory-Datenbank handelt und nicht so viel Speicher verfügbar ist, wie es bei der Speicherung auf einem Datenträger der Fall wäre. Da Sie mit Redis nur begrenzt über Speicherplatz verfügen, sollten Sie sicherstellen, dass Sie nur Daten speichern, die wichtig sind. Wenn die Daten nicht für einen längeren Zeitraum verfügbar sein müssen, stellen Sie sicher, dass Sie eine Ablaufzeit festlegen.

## <a name="how-to-use-data-expiration-in-redis"></a>Verwenden von Datenablauf in Redis

Es gibt verschiedene Befehle zum Implementieren und Verwalten des Datenablaufs in Redis:

- `EXPIRE`: Legt das Timeout eines Schlüssels in Sekunden fest.
- `PEXIRE`: Legt das Timeout eines Schlüssels in Millisekunden fest.
- `EXPIREAT`: Legt das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Sekunden fest.
- `PEXPIREAT`: Legt das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Millisekunden fest.
- `TTL`: Gibt die verbleibende Zeit in Sekunden zurück, bis ein Schlüssel gelöscht wird.
- `PTTL`: Gibt die verbleibende Zeit in Millisekunden zurück, bis ein Schlüssel gelöscht wird.
- `PERSIST`: Bewirkt, dass ein Schlüssel nie abläuft.

Der am häufigsten verwendete Befehl ist `EXPIRE`. Wir verwenden ihn in diesem Modul durchgängig.

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a>Beispiel für Datenablauf mit C# und ServiceStack.Redis

Denken Sie daran, dass wir uns bei der Verwendung einer Clientbibliothek wie **ServiceStack.Redis** keine Sorgen darüber machen müssen, dass wir uns an die Low-Level Redis-Befehle erinnern. Stattdessen können wir eine einfache C#-Methoden verwenden.

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

Mit Redis können Sie Daten nach einer bestimmten Zeit automatisch mithilfe des Datenablaufs löschen. Dies ist wichtig, da es sich bei Redis um eine In-Memory-Datenbank handelt und nicht so viel Speicher verfügbar ist, wie es bei der Speicherung auf einem Datenträger der Fall wäre. Wenn die Daten, die Sie speichern, nicht für einen längeren Zeitraum verfügbar sein müssen, stellen Sie sicher, dass Sie eine Ablaufzeit festlegen.