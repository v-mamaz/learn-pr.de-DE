Ihr Sportstatistik-Entwicklungsteam hat entschieden, dass Zwischenspeichern die Leistung für zuletzt angeforderte Daten deutlich verbessern könnte. Der nächste Schritt ist das Erstellen und Konfigurieren einer Azure Redis Cache-Instanz.

## <a name="create-and-configure-the-azure-redis-cache-instance"></a>Erstellen und Konfigurieren der Azure Redis Cache-Instanz

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com/?azure-portal=true) in Ihrem Browser.

1. Klicken Sie auf **Ressource erstellen**.

1. Suchen Sie nach **Redis Cache**.

1. Klicken Sie auf **Erstellen**.

1. Sie können eine Azure Redis Cache-Instanz aus den Datenbankressourcen im Azure-Portal hinzufügen.

1. Geben Sie einen global eindeutigen Namen an. Der Name muss eine Zeichenfolge mit einer Länge zwischen 1 und 63 Zeichen sein und darf nur Zahlen, Buchstaben und das Zeichen „-“ enthalten. Der Cachename darf weder mit dem Zeichen „-“ beginnen oder enden, noch mehrere aufeinanderfolgende Zeichen vom Typ „-“ enthalten.

1. Geben Sie das Abonnement an, unter dem diese neue Azure Redis Cache-Instanz erstellt wird.

1. Der Name der Ressourcengruppe, in der Ihr Cache erstellt wird. Indem Sie alle Ressourcen für eine App in einer Gruppe zusammenfassen, können Sie diese zusammen verwalten.

1. Platzieren Sie Ihre Cache-Instanz und Ihre Anwendung immer in der gleichen Region/am gleichen Standort. Das Herstellen einer Verbindung mit einem Cache in einer anderen Region kann die Wartezeit beträchtlich erhöhen und die Zuverlässigkeit beeinträchtigen. Wenn Sie die Verbindung mit dem Cache außerhalb von Azure herstellen, wählen Sie einen Standort in der Nähe des Orts aus, an dem die Anwendung, die die Daten nutzt, ausgeführt wird.

    > [!IMPORTANT]
    > Viel wichtiger als die Nähe des Datenspeichers zum Datennutzer ist die Nähe zum Cache.

1. Wählen Sie den Tarif aus. 
    - Wir empfehlen, für Produktionssysteme immer den Standard- oder Premium-Tarif zu verwenden. Der Basic-Tarif ist ein System mit einem einzelnen Knoten ohne Datenreplikation und ohne SLA. Verwenden Sie mindestens einen C1-Cache. C0-Caches sind nur für einfache Entwicklungs-/Testszenarien vorgesehen, da sie einen freigegebenen CPU-Kern und nur sehr wenig Arbeitsspeicher haben.

    - Beim Premium-Tarif stehen Ihnen zwei Methoden zur Auswahl, um Daten bei der Notfallwiederherstellung beizubehalten:

        - RDB-Persistenz erstellt regelmäßig eine Momentaufnahme und kann den Cache bei einem Ausfall anhand dieser Momentaufnahme wiederherstellen.

            ![Screenshot des Azure-Portals mit den RDB-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-1.png)

        - AOF-Persistenz speichert jeden Schreibvorgang in einem Protokoll, das mindestens einmal pro Sekunde gespeichert wird. Dabei entstehen größere Dateien als bei RDB, jedoch ist der Datenverlust geringer.

            ![Screenshot des Azure-Portals mit den AOF-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-2.png)

    - Schützen Sie Ihren Cache mit einem virtuellen Netzwerk.
      Wenn Sie über einen Redis-Cache mit Premium-Tarif verfügen, können Sie ihn für ein virtuelles Netzwerk in der Cloud bereitstellen. Der Cache wird nur für andere virtuelle Computer und Anwendungen in demselben virtuellen Netzwerk verfügbar sein.

    - Verteilen Sie Ihren Cache mit Clustering.
      Mit Redis-Cache mit Premium-Tarif können Sie Clustering implementieren, um Ihr Dataset automatisch zwischen mehreren Knoten aufzuteilen. Um Clustering zu implementieren, geben Sie eine maximale Anzahl von zehn Shards an. Die Kosten entsprechen den Kosten des ursprünglichen Knotens multipliziert mit der Anzahl von Shards.

    - Migrieren Sie von Azure Managed Cache Service.
      Je nach den Features von Managed Cache Service, die Sie verwenden, sind zum Migrieren von Anwendungen, die Azure Managed Cache Service verwenden, zu Azure Redis Cache nur minimale Änderungen an der Anwendung erforderlich. Die APIs sind zwar nicht genau gleich, aber ähnlich. Ein Großteil des vorhandenen Codes, der mit Managed Cache Service auf den Cache zugreift, kann mit minimalen Änderungen wiederverwendet werden.

## <a name="accessing-the-redis-instance"></a>Zugreifen auf die Redis-Instanz

Redis unterstützt eine Reihe von [bekannten Befehlen](https://redis.io/commands). Ein Befehl wird in der Regel als `COMMAND parameter1 parameter2 parameter3` ausgegeben.

Im Folgenden sind einige gängige Befehle aufgeführt, die Sie verwenden können:

| Befehl | Beschreibung |
|---------|-------------|
| `ping` | Den Server pingen. Gibt „PONG“ zurück. |
| `set [key] [value]` | Legt einen Schlüssel/Wert im Cache fest. Gibt bei erfolgreicher Ausführung „OK“ zurück. |
| `get [key]` | Ruft einen Wert aus dem Cache ab. |
| `exists [key]` | Gibt „1“ zurück, wenn der **Schlüssel** im Cache vorhanden ist, und andernfalls „0“. |
| `type [key]` | Gibt den Typ zurück, der dem Wert für den angegebenen **Schlüssel** zugeordnet ist. |
| `incr [key]` | Den angegebenen Wert, der dem **Schlüssel** zugeordnet ist, um 1 erhöhen. Der Wert muss vom Typ „Integer“ oder „Double“ sein. Gibt den neuen Wert zurück. |
| `incrby [key] [amount]` | Den angegebenen Wert, der dem **Schlüssel** zugeordnet ist, um den festgelegten Wert erhöhen. Der Wert muss vom Typ „Integer“ oder „Double“ sein. Gibt den neuen Wert zurück. |
| `del [key]` | Löscht den Wert, der dem **Schlüssel** zugeordnet ist. |
| `flushdb` | _Alle_ Schlüssel und Werte in der Datenbank löschen. |

Redis verfügt über ein Befehlszeilentool (**redis-cli**), mit dem Sie direkt mit diesen Befehlen experimentieren können. Im Folgenden finden Sie einige Beispiele.

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

Hier sehen Sie ein Beispiel zur Verwendung der `INCR`-Befehle. Diese Befehle sind praktisch, da sie unteilbare Inkremente _für mehrere Anwendungen_ bereitstellen, die den Cache verwenden.

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

### <a name="adding-an-expiration-time-to-values"></a>Hinzufügen einer Ablaufzeit zu Werten

Die Zwischenspeicherung ist wichtig, da sie uns das Speichern von häufig verwendeten Werten im Arbeitsspeicher ermöglicht. Wir müssen jedoch auch in der Lage sein, eine Ablaufzeit für veraltete Werte festzulegen. In Redis wird dazu eine _Gültigkeitsdauer_ (Time To Live, TTL) auf einen Schlüssel angewendet.

Nach Ablauf der TTL wird der Schlüssel genau wie bei der Ausgabe des DEL-Befehls automatisch gelöscht. Im Folgenden finden Sie einige Hinweise zum TTL-Ablauf.

- Ablaufzeiten können mit Sekunden- oder Millisekundengenauigkeit festgelegt werden.
- Die Auflösung der Ablaufzeit ist immer 1 Millisekunde.
- Informationen zum Ablauf werden repliziert und dauerhaft auf dem Datenträger gespeichert. Die Zeit verstreicht gewissermaßen, während Ihr Redis-Server angehalten bleibt (d. h. Redis speichert das Datum, an dem ein Schlüssel abläuft).

Hier sehen Sie ein Beispiel für einen Ablauf:

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

## <a name="accessing-a-redis-cache-from-a-client"></a>Zugreifen auf einen Redis Cache von einem Client

Wenn Sie eine Verbindung mit einer Azure Redis Cache-Instanz herstellen, benötigen Clients den Hostnamen, den Port und einen Zugriffsschlüssel für den Cache. Sie können diese Informationen im Azure-Portal auf der Seite **Einstellungen > Zugriffsschlüssel** abrufen. 

- Der Hostname ist die öffentliche Internetadresse Ihres Caches, die mit dem Namen des Caches erstellt wurde. Beispiel: `sportsresults.redis.cache.windows.net`.

- Der Zugriffsschlüssel fungiert als Kennwort für Ihren Cache. Zwei Schlüssel werden erstellt: ein Primärschlüssel und ein Sekundärschlüssel. Sie können beide Schlüssel verwenden. Zwei Schlüssel werden für den Fall bereitgestellt, dass Sie den Primärschlüssel ändern müssen. Sie können alle Clients auf den Sekundärschlüssel umstellen und den Primärschlüssel erneut generieren. In diesem Fall werden alle Anwendungen blockiert, die den ursprünglichen Primärschlüssel verwenden. Microsoft empfiehlt, die Schlüssel wie persönliche Kennwörter in regelmäßigen Abständen erneut zu generieren.

> [!WARNING]
> Die Zugriffsschlüssel sollten als vertrauliche Informationen behandelt und wie Kennwörter geschützt werden. Jede Person mit einem Zugriffsschlüssel kann beliebige Vorgänge in Ihrem Cache durchführen.
