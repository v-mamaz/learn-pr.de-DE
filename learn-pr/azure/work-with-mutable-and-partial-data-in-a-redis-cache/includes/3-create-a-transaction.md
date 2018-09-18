Zunächst erstellen Sie einen Redis Cache in Azure und dann eine einfache Transaktion, die zwei Datenwerte in den Cache einfügt.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a>Erstellen eines Azure Redis Cache

Sie beginnen mit der Erstellung eines Azure Redis Cache über die Azure CLI. Verwenden Sie Cloud Shell auf der rechten Seite des Browserfensters, um mit Azure zu interagieren.

Verwenden Sie den Befehl `azure rediscache create`, um einen neuen Azure Redis Cache zu erstellen. Es werden mehrere Parameter benötigt. An dieser Stelle sind die gängigsten aufgeführt (eine vollständige Liste finden Sie in der Dokumentation).

> [!div class="mx-tableFixed"]
> | Parameter | Beschreibung |
> |-----------|-------------|
> | `--name`    | Der Name des Cache: muss global eindeutig sein und sich aus Buchstaben, Zahlen und Bindestrichen zusammensetzen. |
> | `--resource-group` | Verwenden Sie die vorab erstellte Ressourcengruppe <rgn>[Name der Sandbox-Ressourcengruppe]</rgn>, die zur Azure-Sandbox gehört. |
> | `--location` | Geben Sie den Ort an, an dem sich der Cache befinden soll. Normalerweise würden Sie wahrscheinlich einen Standort in der Nähe der Datenconsumer wählen. In diesem Fall sind Sie auf die in der Azure-Sandbox verfügbaren Standorte beschränkt. Wählen Sie den Standort aus, der Ihnen am nächsten liegt. |
> | `--size` | Die Größe des Redis Cache. Gültige Werte sind [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]. |
> | `--sku` | Redis-SKU. Gültige Werte sind [Basic, Standard, Premium]. |
> | `--enable-non-ssl-port` | Fügen Sie dieses Flag hinzu, wenn Sie den Nicht-SSL-Port für Ihren Cache aktivieren möchten. |

### <a name="selecting-a-location"></a>Auswahl eines Standorts
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Erstellen Sie einen Cache mit den folgenden Optionen:
    - Größe: C0
    - SKU: Basic
    - EnableNonSslPort
    
1. Hier ist eine exemplarische Befehlszeile, stellen Sie sicher, dass Sie **[name]** und **[location]** durch gültige Werte ersetzen.

    ```azurecli
    azure rediscache create \
        --name [name] \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location [location] \
        --size C0 --sku Basic
    ```

1. Das Erstellen des Cache dauert einige Minuten.

## <a name="create-a-net-core-console-application"></a>Erstellen einer .NET Core-Konsolenanwendung

Als Nächstes erstellen Sie eine C#-basierte .NET Core-Konsolenanwendung, mit der Sie Datenwerte in den Azure Redis Cache einfügen können.

1. Erstellen Sie mithilfe der integrierten Cloud Shell auf der rechten Fensterseite eine neue .NET Core-Anwendung. Nennen Sie sie „RedisData“.

    ```bash
    dotnet new console --name RedisData
    ```
    
1. Wechseln Sie in das neue Verzeichnis, das für Ihre App erstellt wurde.

    ```bash
    cd RedisData
    ```
    
1. Darin sollten sich eine Projektdatei und eine einzelne Quelldatei namens **Program.cs** befinden.

1. Erstellen Sie die Anwendung, und führen Sie sie aus. Sie sollten „Hello, World!“ als Ausgabe erhalten.

    ```bash
    dotnet run
    ```
    
## <a name="add-the-servicestackredis-nuget-package"></a>Hinzufügen des NuGet-Pakets „ServiceStack.Redis“

Nachdem nun die Konsolenanwendung fertig erstellt ist, können Sie das NuGet-Paket **ServiceStack.Redis** hinzufügen. Dies ermöglicht es Ihnen, eine Verbindung zum Redis Cache herzustellen und Befehle in C# auszugeben.

1. Fügen Sie das NuGet-Paket **ServiceStack.Redis** mithilfe der Terminalshell hinzu.

    ```bash
    dotnet add package ServiceStack.Redis
    ```
    
1. Kompilieren und starten Sie die Anwendung erneut, um sicherzustellen, dass alles vollständig kompiliert ist. Wie zuvor, sollte die Ausgabe „Hello, World!“ lauten.

## <a name="get-your-azure-redis-cache-connection-string"></a>Abrufen Ihrer Azure Redis Cache-Verbindungszeichenfolge

Für die Verbindung mit Ihrem Azure Redis Cache benötigen Sie eine Verbindungszeichenfolge, die Ihr Kennwort und die URL enthält. Diese Verbindungszeichenfolge ist für **ServiceStack.Redis** eindeutig und wie folgt aufgebaut: `[password]@[host name]:[port]`

Sie können diesen Schlüssel über das Azure-Portal oder über die Befehlszeile abrufen. Verwenden Sie hier die Befehlszeile, da Sie dem Ansatz mit dem Portal bereits im Modul **Optimieren Ihrer Webanwendungen durch das Zwischenspeichern von schreibgeschützten Daten mit Redis** gefolgt sind.

Rufen Sie die Zugriffsschlüssel über den Befehl `azure rediscache list-keys` ab. Sie müssen den Namen und die Ressourcengruppe angeben, wie unten dargestellt:

```azurecli
azure rediscache list-keys \
    --name [name] \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

Die Rückgabe sollte dem folgenden Beispiel ähneln:

```output
Primary Key   : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
Secondary Key : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
```

1. Kopieren Sie Ihren **Primärschlüssel** in die Zwischenablage.

1. Der Hostname ist der Name, den Sie dem Cache beim Erstellen mit dem Suffix `.redis.cache.windows.net` gegeben haben.

1. Der Port muss **6379** sein.

1. Alle diese Informationen können Sie in der Konsole mit dem Befehl `azure rediscache list` überprüfen, der Ihnen alle Redis Cache-Instanzen in Ihrem aktiven Abonnement (in diesem Fall die Azure-Sandbox) anzeigt.

## <a name="add-the-connection-string-to-your-app"></a>Hinzufügen der Verbindungszeichenfolge zu Ihrer App

1. Stellen Sie sicher, dass Sie sich im App-Ordner befinden. Die Datei **Program.cs** sollte sich im aktuellen Ordner befinden, wenn Sie `ls` oder `dir` eingeben.

1. Öffnen Sie den integrierten Editor, indem Sie `code .` in den App-Ordner eingeben.

1. Wählen Sie die Quelldatei **Program.cs** aus.

1. Erstellen Sie in der `Program`-Klasse das folgende Feld.

    ```csharp
    static string redisConnectionString = "";
    ```

1. Fügen Sie Ihre Verbindungszeichenfolge in das Feld **redisConnectionString** ein, das Sie gerade erstellt haben, und verwenden Sie **6379** als Portnummer. Denken Sie daran, Ihre Verbindungszeichenfolge in folgendem Format einzugeben: `[password]@[host name]:[port]`

Die Verbindungszeichenfolge sollte in etwa wie folgt aussehen:

```output
ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6379
```
    
## <a name="insert-two-data-values-into-your-azure-redis-cache"></a>Hinzufügen von zwei Datenwerten in Ihrem Azure Redis Cache

Abschließend werden Sie nun Daten in Ihrem Azure Redis Cache hinzufügen.

1. Fügen Sie oben in der Datei **Program.cs** die folgende using-Anweisung ein.

    ```csharp
    using ServiceStack.Redis;
    ```

1. In der **Main**-Methode fügen Sie dann den folgenden Codeausschnitt hinzu. Dadurch werden zwei Werte übergangsweise hinzugefügt.

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
1. Führen Sie die Anwendung über die Eingabeaufforderung unten im Editor-Fenster aus, und vergewissern Sie sich, dass in der Konsole **Commit für Transaktion ausgeführt** steht. 

    ```bash
    dotnet run
    ```
    
## <a name="verify-your-data"></a>Überprüfen Ihrer Daten

Als letzten Schritt überprüfen Sie, ob sich die von Ihnen hinzugefügten Daten im Azure Redis Cache befinden.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Suchen Sie Ihren Redis Cache, indem Sie in der linken Randleiste **Alle Ressourcen** auswählen und auf der linken Seite über das Feld zum Filtern Redis Cache-Instanzen auswählen. Alternativ können Sie auch oben das Suchfeld verwenden und den Namen des Cache eingeben.

1. Wählen Sie Ihre Redis Cache-Instanz aus.

1. Wählen Sie im Blatt **Übersicht** für Ihren Redis Cache die Option **Konsole** aus. Dadurch wird eine Redis-Konsole geöffnet, in der Sie Low-Level-Redis-Befehle eingeben können.

1. Geben Sie **get MyKey1** ein. Vergewissern Sie sich, dass der zurückgegebene Wert **MyValue1** ist.

1. Geben Sie **get MyKey2** ein. Vergewissern Sie sich, dass der zurückgegebene Wert **MyValue2** ist.

    ![Screenshot der Azure Redis-Konsole mit den Werten von „MyKey1“ und „MyKey2“.](../media/4-redis-console.png)