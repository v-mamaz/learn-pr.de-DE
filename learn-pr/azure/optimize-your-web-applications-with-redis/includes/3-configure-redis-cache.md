Ihr Sportstatistik-Entwicklungsteam hat entschieden, dass Zwischenspeichern die Leistung für zuletzt angeforderte Daten deutlich verbessern könnte. Der nächste Schritt ist das Erstellen und Konfigurieren einer Azure Redis Cache-Instanz.

### <a name="create-and-configure-the-azure-redis-cache-instance"></a>Erstellen und Konfigurieren der Azure Redis Cache-Instanz

1. Sie können eine Azure Redis Cache-Instanz aus den Datenbankressourcen im Azure-Portal hinzufügen.

1. Geben Sie einen global eindeutigen Namen an. Der Name muss eine Zeichenfolge mit einer Länge zwischen 1 und 63 Zeichen sein und darf nur Zahlen, Buchstaben und das Zeichen „-“ enthalten. Der Cachename darf weder mit dem Zeichen „-“ beginnen oder enden, noch mehrere aufeinanderfolgende Zeichen vom Typ „-“ enthalten.

1. Geben Sie das Abonnement an, unter dem diese neue Azure Redis Cache-Instanz erstellt wird.

1. Der Name der Ressourcengruppe, in der Ihr Cache erstellt wird. Indem Sie alle Ressourcen für eine App in einer Gruppe zusammenfassen, können Sie sie zusammen verwalten.

1. Wählen Sie einen Speicherort aus, der sich in der Nähe des Datennutzers befindet.

    > [!NOTE]
    > Es ist viel wichtiger, dass der Cache sich in der Nähe des Datennutzers befindet, als der Datenspeicher.

1. Wählen Sie den Tarif aus. Beachten Sie: Um den Vorteil der Datenpersistenz zu nutzen, müssen Sie einen Premium-Tarif auswählen.

    - Mit dem Premium-Tarif können Sie eine von zwei Möglichkeiten nutzen, Daten bei der Wiederherstellung im Notfall beizubehalten:

        - RDB-Persistenz erstellt regelmäßig eine Momentaufnahme und kann den Cache mit dieser Momentaufnahme bei einem Ausfall wiederherstellen.

            ![Screenshot des Azure-Portals mit den RDB-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-1.png)

        - AOF-Persistenz speichert jeden Schreibvorgang in einem Protokoll, das mindestens einmal pro Sekunde gespeichert wird. Dabei entstehen größere Dateien als bei RDB, jedoch ist der Datenverlust geringer.

            ![Screenshot des Azure-Portals mit den AOF-Persistenzoptionen auf einer neuen Redis Cache-Instanz.](../media/3-redis-persistence-2.png)

    - Schützen Sie Ihren Cache mit einem virtuellen Netzwerk.
      Wenn Sie über einen Redis-Cache mit Premium-Tarif verfügen, können Sie ihn für ein virtuelles Netzwerk in der Cloud bereitstellen. Der Cache wird nur für andere virtuelle Computer und Anwendungen in demselben virtuellen Netzwerk verfügbar sein.

    - Verteilen Sie Ihren Cache mit Clustering.
      Mit Redis-Cache mit Premium-Tarif können Sie Clustering implementieren, um Ihr Dataset automatisch zwischen mehreren Knoten aufzuteilen. Um Clustering zu implementieren, geben Sie eine maximale Anzahl von 10 Shards an. Die Kosten entsprechen den Kosten der ursprünglichen Knoten multipliziert mit der Anzahl von Shards.

    - Migrieren Sie von Azure Managed Cache Service.
      Je nach den Features von Managed Cache Service, die Sie verwenden, sind zum Migrieren von Anwendungen, die Azure Managed Cache Service verwenden, zu Azure Redis Cache nur minimale Änderungen an der Anwendung erforderlich. Die APIs sind zwar nicht genau gleich, aber ähnlich. Ein Großteil des vorhandenem Codes, der mit Managed Cache Service auf den Cache zugreift, kann mit minimalen Änderungen wiederverwendet werden.

### <a name="configure-your-client"></a>Konfigurieren Ihres Clients

Clientanwendungen müssen konfiguriert werden, um Redis-Cache zu verwenden. Ein beliebter Hochleistungs-Redis-Client für die .NET-Sprache ist **StackExchange.Redis**. Sie fügen den Redis-Client mit dem **NuGet-Paket-Manager** in Visual Studio mithilfe des **Install-Package**-Befehls hinzu.

Sie müssen Ihren Client dann konfigurieren, um die Verbindung mit Ihrem Cache herzustellen. Erstellen Sie eine Textdatei mit einer **CONFIG**-Dateierweiterung, die die Einstellungen für den Hostnamen und den primären oder sekundären Schlüssel enthält. Die Datei sollte die folgende Struktur aufweisen:

```XML
    <appSettings>
        <add key="CacheConnection" value="HOST-NAME.redis.cache.windows.net,abortConnect=false,ssl=true,password=PRIMARY-KEY"/>
    </appSettings>
```

Bearbeiten Sie dann Ihre **App.config**-Datei, und aktualisieren Sie sie, sodass sie ein **appSettings**-Dateiattribut einschließt, das auf die Konfigurationsdatei verweist, die Sie gerade erstellt haben.

### <a name="what-are-access-keys"></a>Was sind Zugriffsschlüssel?

Wenn Sie eine Verbindung mit einer Azure Redis Cache-Instanz herstellen, benötigen Cacheclients den Hostnamen, die Ports und einen Schlüssel für den Cache. Diese Informationen können Sie im Azure-Portal abrufen.

### <a name="connection-settings"></a>Verbindungseinstellungen

Um eine Verbindung mit Ihrem Azure Redis Cache herzustellen, benötigen Sie den Hostnamen und den Zugriffsschlüssel. Der Hostname ist die Internetadresse Ihres Caches, z.B. *sportsresults.redis.cache.windows.net*. Der Zugriffsschlüssel fungiert als Kennwort für Ihren Cache. Es gibt primäre und sekundäre Zugriffsschlüssel. Sie können beide Schlüssel verwenden, aber zwei werden bereitgestellt für den Fall, dass Sie den Primärschlüssel ändern müssen. Sie können den Wechsel aller Clients zum sekundären Schlüssel vornehmen und dann die Änderung des Primärschlüssels durchführen, was einen Verlust des Diensts verhindern würde.
