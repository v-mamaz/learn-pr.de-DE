Wir beginnen mit dem Erstellen einer Instanz von Azure Redis Cache, und klicken Sie dann erstellen Sie eine einfache Transaktion, die zwei Datenwerte in den Cache einfügt.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a>Erstellen eines Azure Redis Cache

Wir erstellen zunächst einen Azure Redis Cache mit der Azure CLI. Verwenden Sie für die Interaktion mit Azure Cloud Shell auf der rechten Seite des Browserfensters.

Wir verwenden die `azure rediscache create` Befehl zum Erstellen einer neuen Azure Redis Cache. Es dauert mehrere Parameter. Hier sind die häufigsten (um eine vollständige Liste erhalten in der Dokumentation).

> [!div class="mx-tableFixed"]
> | Parameter | Beschreibung |
> |-----------|-------------|
> | `--name`    | Der Name des Cache - muss dies global eindeutig und besteht aus Buchstaben, Zahlen und Bindestriche enthalten sein. |
> | `--resource-group` | Verwenden Sie vorab erstellte Ressourcengruppe <rgn>[Ressourcengruppennamen Sandkasten]</rgn>, diese ist Teil der Azure-Sandbox. |
> | `--location` | Geben Sie an, wo der Cache gespeichert werden soll. In der Regel sollten Sie einen Speicherort in der Nähe der Datenconsumer auswählen. In diesem Fall sind Sie auf die Speicherorte, die zur Verfügung, in der Azure-Sandbox beschränkt. Wählen Sie dasjenige, das Sie an. |
> | `--size` | Die Größe des Azure Redis Cache. Gültige Werte sind [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]. |
> | `--sku` | Der Azure-Redis-Cache-SKU. Gültige Werte sind ["Basic", "Standard" und "Premium"]. |
> | `--enable-non-ssl-port` | Fügen Sie dieses Flag hinzu, wenn Sie den nicht-SSL-Port für Ihren Cache aktivieren möchten. |

### <a name="selecting-a-location"></a>Auswählen eines Orts
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Erstellen eines Caches mithilfe der folgenden Optionen:
    - Größe: C0
    - SKU: Basic
    - EnableNonSslPort
    
1. Hier ist eine beispielhafte Befehlszeile ein. Achten Sie darauf, ersetzen Sie die **[Name]** und **[Standort]** mit gültigen Werten.

    ```azurecli
    azure rediscache create \
        --name [name] \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location [location] \
        --size C0 --sku Basic
    ```

Es dauert einige Minuten in den Cache zu erstellen.

## <a name="create-a-net-core-console-application"></a>Erstellen einer .NET Core-Konsolenanwendung

Als Nächstes erstellen Sie eine .NET Core c#-basierte Konsolenanwendung, die zum Einfügen von Datenwerten in unserem Azure-Redis-Cache verwendet wird.

1. Erstellen Sie eine neue .NET Core-Anwendung mithilfe der integrierten Cloud-Shell auf der rechten Seite des Fensters. Nennen Sie ihn "RedisData".

    ```bash
    dotnet new console --name RedisData
    ```
    
1. Wechseln Sie in das neue Verzeichnis für Ihre app erstellt haben.

    ```bash
    cd RedisData
    ```
    
1. Sie werden feststellen, eine Projektdatei, und eine einzelne **"Program.cs"** Quelldatei.

1. Erstellen und Ausführen der Anwendung – es sollte "Hello, World!" ausgeben

    ```bash
    dotnet run
    ```
    
## <a name="add-the-servicestackredis-nuget-package"></a>Fügen Sie das ServiceStack.Redis NuGet-Paket hinzu.

Nun, da wir unsere Konsolenanwendung haben, wir müssen die **ServiceStack.Redis** NuGet-Paket. Dadurch können wir mit der Azure Redis Cache und die Befehle in c# verbinden.

1. Fügen Sie das NuGet-Paket **ServiceStack.Redis** mithilfe der terminal-Shell.

    ```bash
    dotnet add package ServiceStack.Redis
    ```
    
1. Erstellen Sie und führen Sie die Anwendung erneut aus, um sicherzustellen, dass alles kompiliert wird. Sie sollten immer noch "Hello, World!" ausgeben.

## <a name="get-your-azure-redis-cache-connection-string"></a>Rufen Sie Ihre Azure Redis Cache-Verbindungszeichenfolge

Um mit Ihren Azure Redis Cache verbinden, benötigen Sie eine Verbindungszeichenfolge, die Ihr Kennwort und die URL enthält. Diese Verbindungszeichenfolge wird nur für **ServiceStack.Redis**, und ist in Form von: `[password]@[host name]:[port]`.

Sie können diesen Schlüssel mit dem Azure-Portal oder über die Befehlszeile abrufen. Die letztere hier verwenden wir da wir das Modul "Optimieren Ihrer Webanwendungen durch das Zwischenspeichern von schreibgeschützten Daten mit Redis" in der Portal-Ansatz verwendet.

Verwenden der `azure rediscache list-keys` Befehl, um die Zugriffsschlüssel abzurufen. Sie benötigen, geben Sie der Gruppe "Namen und die Ressourcengruppe" wie unten dargestellt:

```azurecli
azure rediscache list-keys \
    --name [name] \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

Dadurch wird Folgendes zurückgegeben:

```output
Primary Key   : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
Secondary Key : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
```

1. Kopieren Ihrer **primären** Schlüssel in die Zwischenablage.

1. Der Hostname, werden die Namen, die Sie in den Cache zugewiesen haben, bei der Erstellung, mit dem Suffix `.redis.cache.windows.net`.

1. Der Port muss **6379**.

1. Sie können überprüfen, alle diese Informationen in der Konsole mit der `azure rediscache list` Befehl. Dieser Befehl zeigt alle Instanzen von Azure Redis Cache in Ihr aktives Abonnement (in diesem Fall die Azure-Sandbox).

## <a name="add-the-connection-string-to-your-app"></a>Fügen Sie die Verbindungszeichenfolge zu Ihrer app

1. Stellen Sie sicher, dass Sie in den app-Ordner befinden. Die **"Program.cs"** muss im aktuellen Ordner, wenn Sie eingeben `ls` oder `dir`.

1. Öffnen Sie den integrierten Editor durch Eingabe `code .` in den app-Ordner.

1. Wählen Sie die **"Program.cs"** Quelldatei.

1. Erstellen Sie das folgende Feld in der `Program` Klasse.

    ```csharp
    static string redisConnectionString = "";
    ```

1. Fügen Sie in der Verbindungszeichenfolge in der **RedisConnectionString** Feld, das Sie gerade erstellt haben, und verwenden Sie **6379** als Ihre Portnummer. Beachten Sie, dass Ihre Verbindungszeichenfolge ist in Form von: `[password]@[host name]:[port]`.

Beispiel einer Verbindungszeichenfolge sieht etwa wie folgt:

```output
ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6379
```
    
## <a name="insert-two-data-values-into-your-azure-redis-cache"></a>Legen Sie zwei Datenwerte in Ihren Azure Redis Cache

Abschließend werden wir zum Hinzufügen von Daten in Ihren Azure Redis Cache.

1. Fügen Sie die folgenden `using` Anweisung am Anfang der **"Program.cs"** Datei.

    ```csharp
    using ServiceStack.Redis;
    ```

1. Fügen Sie den folgenden Codeausschnitt in Ihre **Main** Methode. Dadurch werden zwei Werte übergangsweise hinzugefügt.

    ```csharp
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create the transaction
        var transaction = redisClient.CreateTransaction();

        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        var transactionResult = transaction.Commit();

        if(transactionResult)
            Console.WriteLine("Transaction committed");
        else
            Console.WriteLine("Transaction failed to commit");
    }
    ```
1. Führen Sie die Anwendung über die Eingabeaufforderung am unteren Rand im Editor-Fenster, und stellen Sie sicher, dass die Konsole sagt **Transaktionen mit ausgeführtem Commit**. 

    ```bash
    dotnet run
    ```
    
## <a name="verify-your-data"></a>Überprüfen Ihrer Daten

Deaktiviert Abschließend überprüfen wir, dass die Daten, die wir hinzugefügt, in unserem Azure-Redis-Cache.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Suchen Sie Ihren Azure Redis Cache dazu **alle Ressourcen** in der linken Randleiste, und verwenden das Feld "Filter" auf der linken Seite zum Auswählen von Azure Redis Cache-Instanzen. Alternativ können Sie verwenden Sie das Suchfeld oben, und geben Sie den Namen des Caches.

1. Wählen Sie Ihre Azure Redis Cache-Instanz.

1. In der **Übersicht** auf dem Blatt für Ihren Azure Redis Cache, wählen Sie **Konsole**. Dadurch wird eine Azure Redis Cache-Konsole geöffnet, auf niedriger Ebene Azure Redis Cache-Befehle eingeben können.

1. Typ **erhalten MyKey1**. Stellen Sie sicher, dass der zurückgegebene Wert ist **MyValue1**.

1. Typ **erhalten MyKey2**. Stellen Sie sicher, dass der zurückgegebene Wert ist **MyValue2**.

    ![Screenshot der Azure Redis Cache-Konsole, die die Werte von MyKey1 und MyKey2.](../media/4-redis-console.png)