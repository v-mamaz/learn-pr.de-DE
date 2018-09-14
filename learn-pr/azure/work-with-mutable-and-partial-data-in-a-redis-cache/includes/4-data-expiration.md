Daten sind nicht immer dauerhaft, und es gibt Situationen, die Sie zu einem bestimmten Zeitpunkt löschen möchten. Beispielsweise können Benutzer in Ihrer instant messaging-Anwendung, den Anzeigenamen des der Gruppenchat festlegen. Allerdings möchten Sie den Namen nach einer Stunde zurückgesetzt. Sie können dies erreichen, indem Schreiben Ihrer eigenen serverseitige Logik, die den Timer für eine Stunde festlegen und den Namen gelöscht. Azure Redis Cache unterstützt jedoch Ablauf von Daten, also eine Funktion, die dies automatisch vornimmt, ohne zusätzlichen Logik schreiben zu müssen.

Hier erfahren Sie, über die gängiger Redis-Befehle zum Ablauf von Daten zu implementieren.

## <a name="what-is-data-expiration"></a>Was ist der Ablauf von Daten?

Ablauf von Daten ist ein Feature, das automatisch einen Schlüssel und Wert im Cache nach einem festgelegten Zeitraum löschen kann.

## <a name="why-use-data-expiration"></a>Gründe für die Verwendung der Ablauf von Daten

Ablauf von Daten wird häufig in Situationen verwendet, in denen die Daten, die Sie speichern kurzlebiger ist.  Dies ist wichtig, da Azure Redis Cache eine in-Memory-Datenbank ist, und Sie müssen nicht so viel Arbeitsspeicher verwendet wird, als würden Sie auf dem Datenträger gespeichert haben. Da Sie Speicher mit Azure Redis Cache begrenzt ist, sollten Sie sicherstellen, dass Sie nur Daten speichern, die wichtig sind. Wenn die Daten nicht für einen längeren Zeitraum sein müssen, stellen Sie sicher, dass Sie eine Ablaufzeit festlegen.

## <a name="how-to-use-data-expiration-in-azure-redis-cache"></a>Gewusst wie: Verwenden Sie den Ablauf von Daten in Azure Redis Cache

Es gibt verschiedene Befehle zum Implementieren und Verwalten des datenablaufs in Azure Redis Cache:

- `EXPIRE`: Legt fest, das Timeout eines Schlüssels in Sekunden
- `PEXIRE`: Legt fest, das Timeout eines Schlüssels in Millisekunden
- `EXPIREAT`: Legt fest, das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Sekunden
- `PEXPIREAT`: Legt fest, das Timeout eines Schlüssels mit einem absoluten Unix-Zeitstempel in Millisekunden
- `TTL`: Gibt die verbleibende Zeit, die einen Schlüssel aufweist, die Gültigkeitsdauer in Sekunden
- `PTTL`: Gibt die verbleibende Zeit, die einen Schlüssel aufweist, die Gültigkeitsdauer in Millisekunden
- `PERSIST`: Bewirkt, dass einen Schlüssel läuft nie ab

Der am häufigsten verwendete Befehl ist `EXPIRE`, und wir verwenden sie in diesem Modul.

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a>Beispiel der Ablauf von Daten mithilfe von C#- und ServiceStack.Redis

Beachten Sie, dass bei Verwendung eine Clientbibliothek wie **ServiceStack.Redis**, wir keine Gedanken um die Low-Level-Azure Redis Cache-Befehle zu speichern. Stattdessen können wir eine einfache C#-Methoden verwenden.

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

Azure Redis Cache können Sie zum automatischen Löschen von Daten nach einem festgelegten Zeitraum Ablauf von Daten verwenden. Dies ist wichtig, da es sich bei Azure Redis Cache ist eine in-Memory-Datenbank, und Sie müssen nicht so viel Arbeitsspeicher zur Verfügung wie bei der Speicherung von Daten auf dem Datenträger. Wenn die Daten, die Sie speichern nicht um einen längeren Zeitraum sein müssen, stellen Sie sicher, dass Sie eine Ablaufzeit festlegen.