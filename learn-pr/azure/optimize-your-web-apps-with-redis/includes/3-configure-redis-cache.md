Ihr Sportstatistik-Entwicklungsteam hat entschieden, dass Zwischenspeichern die Leistung für zuletzt angeforderte Daten deutlich verbessern könnte. Der nächste Schritt ist das Erstellen und Konfigurieren einer Azure Redis Cache-Instanz.

## <a name="create-and-configure-the-azure-redis-cache-instance"></a>Erstellen und Konfigurieren der Azure Redis Cache-Instanz

Sie können einen Redis Cache über das Azure-Portal, die Azure-Befehlszeilenschnittstelle oder Azure PowerShell erstellen. Es gibt mehrere Parameter, die Sie benötigen, um zu entscheiden, um den Cache ordnungsgemäß für Ihre Zwecke zu konfigurieren.

### <a name="name"></a>Name

Der Redis-Cache benötigen einen global eindeutigen Namen. Der Name muss innerhalb von Azure eindeutig sein, da er verwendet wird, um eine öffentliche URL für die Verbindung und kommunizieren mit dem Dienst zu generieren.

Der Name muss zwischen 1 und 63 Zeichen lang sein, aus Zahlen, Buchstaben, sein und die '-' Zeichen. Der Cachename darf weder mit dem Zeichen „-“ beginnen oder enden, noch mehrere aufeinanderfolgende Zeichen vom Typ „-“ enthalten.

### <a name="resource-group"></a>Ressourcengruppe

Azure Redis Cache ist eine verwaltete Ressource und muss eine _Ressourcengruppe_ Besitzer. Sie können entweder eine neue Ressourcengruppe erstellen oder verwenden Sie eine vorhandene Ressourcengruppe in eine Susbcription, die Sie angehören.

### <a name="location"></a>Standort

Sie müssen entscheiden, in denen der Redis-Cache physisch wird durch Auswählen einer Azure-Region. Sie sollten Ihre Cache-Instanz und Ihrer Anwendung immer in derselben Region platzieren. Herstellen einer Verbindung mit einem Cache in einer anderen Region kann beträchtlich Latenz erhöhen und reduzieren die Zuverlässigkeit. Wenn Sie in den Cache außerhalb von Azure herstellen, wählen Sie einen Speicherort in der Nähe, in dem die Anwendung, die die Daten ausgeführt wird.

> [!IMPORTANT]
> Fügen den Redis-Cache wie in der Nähe der Daten _Consumer_ wie möglich.

### <a name="pricing-tier"></a>Tarif

Wie in der letzten Einheit erwähnt, sind gibt es drei Tarife für einen Azure Redis Cache verfügbar.

- **Grundlegende**: Basic-Cache ideal zu Entwicklungs-und Testzwecken. Ist auf einem einzelnen Server, 53 GB Arbeitsspeicher und 20.000 Verbindungen beschränkt. Es gibt keine SLA für diese Dienstebene.
- **Standard**: produktionscache unterstützt die Replikation und eine SLA von 99,99 % enthält. Es unterstützt zwei-Server (Master/Slave) und den gleichen Speicher/Anzahl der Verbindungen begrenzt als Tarif "Basic".
- **Premium**: Enterprise-Tarifs baut auf den Tarif "Standard" und bietet Unterstützung für Persistenz, clustering und horizontale Skalierung Cache. Dies ist die höchste Leistung Ebene mit bis zu 530 GB an Arbeitsspeicher und 40.000 gleichzeitige Verbindungen.

Sie können die Menge des verfügbaren Cachespeichers auf jeder Ebene steuern – diese Option wählen Sie eine Ebene des Caches aus C0-C6, für Basic/Standard "und" P0-P4 für Premium aktiviert ist. Überprüfen Sie die [Preisseite](https://azure.microsoft.com/en-us/pricing/details/cache/) Weitere Details.

> [!TIP]
> Microsoft empfiehlt, dass Sie immer Standard- oder Premium-Tarif für Produktionssysteme verwenden. Der Basic-Tarif ist ein System mit einem einzelnen Knoten, ohne Datenreplikation und ohne SLA. Verwenden Sie mindestens einen C1-Cache. C0-Caches sind wirklich für einfache Entwicklungs-/Testszenarien vorgesehen, da sie einen freigegebenen CPU-Kern und nur sehr wenig Arbeitsspeicher aufweisen.

Tarif "Premium" können Sie Daten auf zwei Arten Wiederherstellung im Notfall zu dauerhaft zu speichern:

1. RDB-Persistenz erstellt regelmäßig eine Momentaufnahme und kann den Cache mit dieser Momentaufnahme bei einem Ausfall wiederherstellen.

    ![Screenshot des Azure-Portals mit den RDB-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-1.png)

2. AOF-Persistenz speichert jeden Schreibvorgang in einem Protokoll, das mindestens einmal pro Sekunde gespeichert wird. Dabei entstehen größere Dateien als bei RDB, jedoch ist der Datenverlust geringer.

    ![Screenshot des Azure-Portals mit den AOF-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-2.png)

Es gibt verschiedene andere Einstellungen, die nur zur Verfügung stehen die **Premium** Ebene.

### <a name="virtual-network-support"></a>Unterstützung für virtuelle Netzwerke

Wenn Sie einen Tarif "Premium" Redis-Cache erstellen, können Sie es mit einem virtuellen Netzwerk in der Cloud bereitstellen. Der Cache wird nur für andere virtuelle Computer und Anwendungen in demselben virtuellen Netzwerk verfügbar sein. Dies bietet eine höhere Sicherheit, wenn der Dienst und der Cache sowohl in Azure gehostet werden, oder über ein Azure virtual Network VPN verbunden sind.

### <a name="clustering-support"></a>Unterstützung für Clustering

Mit Redis-Cache mit Premium-Tarif können Sie Clustering implementieren, um Ihr Dataset automatisch zwischen mehreren Knoten aufzuteilen. Um Clustering zu implementieren, geben Sie eine maximale Anzahl von 10 Shards an. Die Kosten ist die Kosten für den ursprünglichen Knoten, multipliziert mit der Anzahl von Shards.

## <a name="accessing-the-redis-instance"></a>Zugreifen auf die Redis-Instanz

Redis unterstützt eine Reihe von [bekannte Befehle](https://redis.io/commands). Ein Befehl in der Regel als ausgegeben `COMMAND parameter1 parameter2 parameter3`.

Hier sind einige häufig verwendete Befehle, die Sie verwenden können:

| Get-Help | Beschreibung |
|---------|-------------|
| `ping` | Pingen Sie den Server. Gibt "PINGPONG". |
| `set [key] [value]` | Legt einen Schlüssel-Wert in den Cache fest. Gibt "OK" bei Erfolg zurück. |
| `get [key]` | Ruft einen Wert aus dem Cache ab. |
| `exists [key]` | Gibt "1" zurück, wenn die **Schlüssel** im Cache, "0" ist vorhanden, wenn dies nicht der Fall. |
| `type [key]` | Gibt den Typ zugeordnet ist, auf den Wert für den angegebenen **Schlüssel**. |
| `incr [key]` | Erhöhen Sie den angegebenen Wert zugeordnet **Schlüssel** durch '1'. Der Wert muss eine ganze Zahl oder double-Wert sein. Dies gibt den neuen Wert zurück. |
| `incrby [key] [amount]` | Erhöhen Sie den angegebenen Wert zugeordnet **Schlüssel** den angegebenen Betrag. Der Wert muss eine ganze Zahl oder double-Wert sein. Dies gibt den neuen Wert zurück. |
| `del [key]` | Löscht den Wert der **Schlüssel**. |
| `flushdb` | Löschen Sie _alle_ Schlüssel und Werte in der Datenbank. |

Redis ist ein Befehlszeilentool (**Redis-Cli**) können Sie direkt mit diesen Befehlen zu experimentieren. Hier einige Beispiele.

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

Es folgt ein Beispiel der Arbeit mit der `INCR` Befehle. Diese sind praktisch, da sie atomische Schritten bereitstellen _für mehrere Anwendungen_ , die den Cache verwenden.

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

### <a name="adding-an-expiration-time-to-values"></a>Eine Ablaufzeit hinzufügen zu Werten

Es ist wichtig, zwischenspeichern, da es, häufig verwendete Werte im Arbeitsspeicher ermöglicht. Wir benötigen jedoch auch die Möglichkeit, Werte ablaufen, wenn sie veraltet sind. In Redis Dies erfolgt durch Anwenden einer _Gültigkeitsdauer_ (TTL), der einem Schlüssel.

Nach Ablauf der Gültigkeitsdauer (TTL) wird der Schlüssel automatisch gelöscht, genau so, als ob der Befehl DEL ausgegeben wurden. Hier sind einige Hinweise auf TTL-Ablauf.

- Ablaufzeiten können mit Sekunden oder Millisekunden-Genauigkeit festgelegt werden.
- Die zeitauflösung Ablauf ist immer 1 Millisekunde.
- Informationen zum Ablauf repliziert und dauerhaft gespeichert werden auf dem Datenträger, die Zeit praktisch übergibt, wenn Ihre Redis-Server bleibt (Dies bedeutet, der Redis das Datum speichert angehalten, an dem ein Schlüssel läuft ab).

Hier ist ein Beispiel für ein Ablaufdatum:

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

## <a name="accessing-a-redis-cache-from-a-client"></a>Zugreifen auf einen Redis-Cache von einem client

Um eine Verbindung mit einer Azure Redis Cache-Instanz herzustellen, benötigen Sie verschiedene Arten von Informationen. Clients benötigen den Hostnamen, Port und einen Zugriffsschlüssel für den Cache. Sie können diese Informationen im Azure-Portal durch Abrufen der **Einstellungen > Zugriffsschlüssel** Seite. 

- Der Hostname ist die öffentliche Internet-Adresse des Caches, die mit dem Namen des dem Cache erstellt wurde. Beispiel: `sportsresults.redis.cache.windows.net`.

- Der Zugriffsschlüssel fungiert als Kennwort für Ihren Cache. Es gibt zwei Schlüssel erstellt haben: primäre und sekundäre. Sie beide Schlüssel verwenden können, sind zwei bereitgestellt, falls Sie den Primärschlüssel ändern möchten. Sie können Ihre Clients auf den sekundären Schlüssel umschalten und den Primärschlüssel erneut generieren. Dadurch würden alle Anwendungen, die mit dem ursprünglichen primären Schlüssel blockiert. Es empfiehlt sich in regelmäßigen Abständen Neugenerieren von Schlüssel - ähnlich, wie Sie Ihre persönlichen Kennwörter tun würden.

> [!WARNING]
> Zugriffsschlüssel für Ihr sollten die vertraulichen Informationen, behandeln sie, wie Sie ein Kennwort würde berücksichtigt werden. Jede Person mit einer Zugriffstaste kann alle Vorgänge für Ihren Cache durchführen.
