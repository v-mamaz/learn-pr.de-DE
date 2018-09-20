Ihr Sportstatistik-Entwicklungsteam hat entschieden, dass Zwischenspeichern die Leistung für zuletzt angeforderte Daten deutlich verbessern könnte. Der nächste Schritt ist das Erstellen und Konfigurieren einer Azure Redis Cache-Instanz.

## <a name="create-and-configure-the-azure-redis-cache-instance"></a>Erstellen und Konfigurieren der Azure Redis Cache-Instanz

Sie können einen Redis Cache über das Azure-Portal, mithilfe der Azure CLI oder unter Verwendung von Azure PowerShell erstellen. Es gibt mehrere Parameter, für die Sie sich entscheiden müssen, um den Cache für Ihre Zwecke ordnungsgemäß zu konfigurieren.

### <a name="name"></a>Name

Der Redis Cache benötigen einen global eindeutigen Namen. Der Name muss innerhalb von Azure eindeutig sein, da er verwendet wird, um eine öffentlich zugängliche URL zu generieren, um eine Verbindung herzustellen und mit dem Dienst zu kommunizieren.

Der Name muss zwischen 1 und 63 Zeichen lang sein und aus Ziffern, Buchstaben und dem Zeichen „-“ bestehen. Der Cachename darf weder mit dem Zeichen „-“ beginnen oder enden, noch mehrere aufeinanderfolgende Zeichen vom Typ „-“ enthalten.

### <a name="resource-group"></a>Ressourcengruppe

Azure Redis Cache ist eine verwaltete Ressource und benötigt eine _Ressourcengruppe_ als Besitzer. Sie können eine neue Ressourcengruppe erstellen oder eine vorhandene Ressourcengruppe in einem Abonnement verwenden, in dem Sie Mitglied sind.

### <a name="location"></a>Standort

Sie müssen entscheiden, wo sich der Redis Cache physisch befinden soll, indem Sie eine Azure-Region auswählen. Sie sollten Ihre Cacheinstanz und Ihre Anwendung immer in der gleichen Region platzieren. Das Herstellen einer Verbindung mit einem Cache in einer anderen Region kann die Wartezeit beträchtlich erhöhen und die Zuverlässigkeit beeinträchtigen. Wenn Sie die Verbindung mit dem Cache außerhalb von Azure herstellen, wählen Sie einen Standort in der Nähe des Orts aus, an dem die Anwendung, die die Daten nutzt, ausgeführt wird.

> [!IMPORTANT]
> Platzieren Sie den Redis Cache so nah wie möglich am Daten_consumer_.

### <a name="pricing-tier"></a>Tarif

Wie bereits in der letzten Einheit erwähnt wurde, sind drei Tarife für einen Azure Redis Cache verfügbar.

- **Basic**: Basiscache, der sich ideal zu Entwicklungs-/Testzwecken eignet. Ist auf einen einzelnen Server, 53 GB Arbeitsspeicher und 20.000 Verbindungen beschränkt. Es gibt keine SLA für diesen Diensttarif.
- **Standard**: Produktionscache, der Replikation und eine SLA von 99,99 % unterstützt. Der Tarif unterstützt zwei Server (Master/Slave) und weist die gleichen Einschränkungen für den Arbeitsspeicher bzw. die Anzahl der Verbindungen wie der Tarif „Basic“ auf.
- **Premium**: Enterprise-Tarif, der auf dem Tarif „Standard“ aufbaut und Unterstützung für Persistenz, Clustering und horizontale Skalierung bietet. Dies ist der leistungsstärkste Tarif mit bis zu 530 GB Arbeitsspeicher und 40.000 gleichzeitigen Verbindungen.

Sie können die Kapazität des verfügbaren Cachespeichers für jeden Tarif steuern, indem Sie eine Cacheebene von C0-C6 für Basic/Standard und P0-P4 für Premium auswählen. Ausführliche Informationen finden Sie in der [Preisübersicht](https://azure.microsoft.com/pricing/details/cache/).

> [!TIP]
> Microsoft empfiehlt, für Produktionssysteme immer den Standard- oder Premium-Tarif zu verwenden. Der Basic-Tarif ist ein System mit einem einzelnen Knoten ohne Datenreplikation und ohne SLA. Verwenden Sie mindestens einen C1-Cache. C0-Caches sind nur für einfache Entwicklungs-/Testszenarien vorgesehen, da sie einen freigegebenen CPU-Kern und nur sehr wenig Arbeitsspeicher haben.

Beim Premium-Tarif stehen Ihnen zwei Methoden zur Auswahl, um Daten bei der Notfallwiederherstellung beizubehalten:

1. RDB-Persistenz erstellt regelmäßig eine Momentaufnahme und kann den Cache bei einem Ausfall anhand dieser Momentaufnahme wiederherstellen.

    ![Screenshot des Azure-Portals mit den RDB-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-1.png)

2. AOF-Persistenz speichert jeden Schreibvorgang in einem Protokoll, das mindestens einmal pro Sekunde gespeichert wird. Dabei entstehen größere Dateien als bei RDB, jedoch ist der Datenverlust geringer.

    ![Screenshot des Azure-Portals mit den AOF-Persistenzoptionen für eine neue Redis-Cacheinstanz.](../media/3-redis-persistence-2.png)

Es gibt verschiedene weitere Einstellungen, die nur für den Tarif **Premium** zur Verfügung stehen.

### <a name="virtual-network-support"></a>Unterstützung für virtuelle Netzwerke

Wenn Sie einen Redis Cache mit dem Premium-Tarif erstellen, können Sie ihn für ein virtuelles Netzwerk in der Cloud bereitstellen. Der Cache ist nur für andere virtuelle Computer und Anwendungen im gleichen virtuellen Netzwerk verfügbar. Dies bietet ein höheres Maß an Sicherheit, wenn Ihr Dienst und Ihr Cache beide in Azure gehostet werden oder über ein VPN des virtuellen Azure-Netzwerks verbunden sind.

### <a name="clustering-support"></a>Unterstützung für Clustering

Mit einem Redis Cache mit Premium-Tarif können Sie Clustering implementieren, um Ihr Dataset automatisch auf mehrere Knoten aufzuteilen. Um Clustering zu implementieren, geben Sie eine maximale Anzahl von zehn Shards an. Die Kosten entsprechen den Kosten des ursprünglichen Knotens multipliziert mit der Anzahl von Shards.

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
| `incr [key]` | Inkrementiert den angegebenen Wert, der dem **Schlüssel** zugeordnet ist, um 1. Der Wert muss vom Typ „Integer“ oder „Double“ sein. Gibt den neuen Wert zurück. |
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

Um eine Verbindung mit einer Azure Redis Cache-Instanz herzustellen, benötigen Sie verschiedene Arten von Informationen. Clients benötigen den Hostnamen, den Port und einen Zugriffsschlüssel für den Cache. Sie können diese Informationen im Azure-Portal auf der Seite **Einstellungen > Zugriffsschlüssel** abrufen. 

- Der Hostname ist die öffentliche Internetadresse Ihres Caches, die mit dem Namen des Caches erstellt wurde. Beispiel: `sportsresults.redis.cache.windows.net`.

- Der Zugriffsschlüssel fungiert als Kennwort für Ihren Cache. Zwei Schlüssel werden erstellt: ein Primärschlüssel und ein Sekundärschlüssel. Sie können beide Schlüssel verwenden. Zwei Schlüssel werden für den Fall bereitgestellt, dass Sie den Primärschlüssel ändern müssen. Sie können alle Clients auf den Sekundärschlüssel umstellen und den Primärschlüssel erneut generieren. In diesem Fall werden alle Anwendungen blockiert, die den ursprünglichen Primärschlüssel verwenden. Microsoft empfiehlt, die Schlüssel wie persönliche Kennwörter in regelmäßigen Abständen erneut zu generieren.

> [!WARNING]
> Die Zugriffsschlüssel sollten als vertrauliche Informationen behandelt und wie Kennwörter geschützt werden. Jede Person mit einem Zugriffsschlüssel kann beliebige Vorgänge in Ihrem Cache durchführen.
