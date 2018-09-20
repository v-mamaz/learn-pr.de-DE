Daten sind nicht immer dauerhaft, und es kann vorkommen, dass Sie sie zu einem bestimmten Zeitpunkt löschen möchten. In Ihrer Instant Messaging-Anwendung können Benutzer beispielsweise den Anzeigenamen des Gruppenchats festlegen. Sie möchten jedoch, dass der Name nach einer Stunde zurückgesetzt wird. Dies können Sie erreichen, indem Sie Ihre eigene serverseitige Logik schreiben, die einen Stundentimer festlegt und den Namen löscht. Der Azure Redis Cache unterstützt jedoch den Datenablauf. Das Feature erledigt dies automatisch, sodass Sie keine zusätzliche Logik schreiben müssen.

Hier erfahren Sie mehr über die gebräuchlichen Redis-Befehle zur Implementierung des Datenablaufs.

## <a name="what-is-data-expiration"></a>Was ist Datenablauf?

Datenablauf ist ein Feature, das einen Schlüssel und Wert im Cache nach einem festgelegten Zeitraum automatisch löschen kann.

## <a name="why-use-data-expiration"></a>Warum sollte Datenablauf verwendet werden?

Der Datenablauf wird häufig in Situationen verwendet, in denen die gespeicherten Daten kurzlebig sind.  Dies ist wichtig, da es sich beim Azure Redis Cache um eine In-Memory-Datenbank handelt und nicht so viel Speicher verfügbar ist, wie es bei der Speicherung auf einem Datenträger der Fall wäre. Da Sie mit dem Azure Redis Cache nur begrenzt über Speicherplatz verfügen, sollten Sie sicherstellen, dass Sie nur wichtige Daten speichern. Wenn die Daten nicht für einen längeren Zeitraum verfügbar sein müssen, stellen Sie sicher, dass Sie eine Ablaufzeit festlegen.

## <a name="how-to-use-data-expiration-in-azure-redis-cache"></a>Verwenden des Datenablaufs im Azure Redis Cache

Es gibt verschiedene Befehle zum Implementieren und Verwalten des Datenablaufs in Azure Redis Cache:

- `EXPIRE`: Legt das Timeout eines Schlüssels in Sekunden fest.
- `PEXPIRE`: Legt das Timeout eines Schlüssels in Millisekunden fest.
- `EXPIREAT`: Legt das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Sekunden fest.
- `PEXPIREAT`: Legt das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Millisekunden fest.
- `TTL`: Gibt die verbleibende Zeit in Sekunden zurück, bis ein Schlüssel gelöscht wird.
- `PTTL`: Gibt die verbleibende Zeit in Millisekunden zurück, bis ein Schlüssel gelöscht wird.
- `PERSIST`: Bewirkt, dass ein Schlüssel nie abläuft.

Der am häufigsten verwendete Befehl ist `EXPIRE`. Er wird in diesem Modul durchgängig verwendet.

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a>Beispiel für Datenablauf mit C# und ServiceStack.Redis

Denken Sie daran, dass Sie sich bei der Verwendung einer Clientbibliothek wie **ServiceStack.Redis** keine Sorgen darüber machen müssen, dass Sie sich an spezifische Befehle des Azure Redis Cache erinnern. Stattdessen können Sie einfache C#-Methoden verwenden.

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

Mit dem Azure Redis Cache können Sie Daten nach einer bestimmten Zeit automatisch mithilfe des Datenablaufs löschen. Dies ist wichtig, da es sich beim Azure Redis Cache um eine In-Memory-Datenbank handelt und nicht so viel Speicher verfügbar ist, wie es bei der Speicherung auf einem Datenträger der Fall wäre. Wenn die gespeicherten Daten nicht für einen längeren Zeitraum verfügbar sein müssen, sollten Sie sicherstellen, dass Sie eine Ablaufzeit festlegen.