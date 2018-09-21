Zunächst erstellen Sie eine Instanz von Azure Redis Cache und dann eine einfache Transaktion, die zwei Datenwerte in den Cache einfügt.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a>Erstellen einer Azure Redis Cache-Instanz

Sie beginnen mit der Erstellung eines Azure Redis Cache über die Azure CLI. Verwenden Sie Cloud Shell auf der rechten Seite des Browserfensters, um mit Azure zu interagieren.

Verwenden Sie den Befehl `az redis create`, um einen neuen Azure Redis Cache zu erstellen. Es werden mehrere Parameter benötigt. An dieser Stelle sind die gängigsten aufgeführt (eine vollständige Liste finden Sie in der Dokumentation).

> [!div class="mx-tableFixed"]
> | Parameter | Beschreibung |
> |-----------|-------------|
> | `--name`    | Der Cachename muss global eindeutig sein und aus Buchstaben, Zahlen und Bindestrichen bestehen. |
> | `--resource-group` | Verwenden Sie die vorab erstellte Ressourcengruppe **<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>**, die zur Azure-Sandbox gehört. |
> | `--location` | Geben Sie den Ort an, an dem sich der Cache befinden soll. Normalerweise würden Sie wahrscheinlich einen Standort in der Nähe der Datenconsumer wählen. In diesem Fall sind Sie auf die in der Azure-Sandbox verfügbaren Standorte beschränkt. Wählen Sie den Standort aus, der Ihnen am nächsten liegt. |
> | `--size` | Die Größe der Azure Redis Cache-Instanz. Gültige Werte sind [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]. |
> | `--sku` | Die Azure Redis Cache SKU. Gültige Werte sind [Basic, Standard, Premium]. |

### <a name="select-a-location"></a>Auswählen eines Standorts
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Erstellen Sie einen Cache mit den folgenden Optionen:
    - Größe: C0
    - SKU: Basic

1. Hier ein Beispiel einer Befehlszeile. Ersetzen Sie unbedingt den Parameter `[name]` durch einen eindeutigen Namen. Sie können den Standort ersetzen, wenn Sie eine andere Region als USA, Osten wünschen.

    ```azurecli
    REDIS_NAME=[name]

    az redis create \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location eastus \
        --vm-size C0 \
        --sku Basic \
    ```

## <a name="create-a-net-core-console-application"></a>Erstellen einer .NET Core-Konsolenanwendung

Als Nächstes erstellen Sie eine .NET Core-Konsolenanwendung, mit der Sie Datenwerte in Ihre Azure Redis Cache-Instanz einfügen können.

1. Erstellen Sie mithilfe der integrierten Cloud Shell auf der rechten Fensterseite eine neue .NET Core-Anwendung. Nennen Sie sie „RedisData“.

    ```bash
    cd ~
    dotnet new console --name RedisData
    ```

1. Wechseln Sie in das neue Verzeichnis, das für Ihre App erstellt wurde.

    ```bash
    cd RedisData
    ```

1. Kompilieren Sie die Anwendung, und führen Sie sie aus. Sie sollten „Hello, World!“ als Ausgabe erhalten.

    ```bash
    dotnet run
    ```

## <a name="add-the-servicestackredis-nuget-package"></a>Hinzufügen des NuGet-Pakets „ServiceStack.Redis“

Nachdem nun die Konsolenanwendung fertig erstellt ist, können Sie das NuGet-Paket **ServiceStack.Redis** hinzufügen. Dies ermöglicht Ihnen, eine Verbindung mit der Azure Redis Cache-Instanz herzustellen und Befehle in C# aufzurufen.

1. Fügen Sie das NuGet-Paket **ServiceStack.Redis** mithilfe der Terminalshell hinzu.

    ```bash
    dotnet add package ServiceStack.Redis
    ```

1. Kompilieren und starten Sie die Anwendung erneut, um sicherzustellen, dass alles vollständig kompiliert ist. Wie zuvor sollte die Ausgabe „Hello, World!“ lauten.

## <a name="get-your-azure-redis-cache-connection-string"></a>Abrufen Ihrer Azure Redis Cache-Verbindungszeichenfolge

Für die Verbindung mit Ihrer Azure Redis Cache-Instanz benötigen Sie eine Verbindungszeichenfolge, die Ihr Kennwort und die URL enthält. **ServiceStack.Redis** hat ein eigenes Format für Verbindungszeichenfolgen: `[password]@[hostname]:[sslport]?ssl=true`.

Sie können Ihr Kennwort über das Azure-Portal oder die Befehlszeile abrufen. Verwenden Sie hier die Befehlszeile, da Sie dem Ansatz mit dem Portal bereits im Modul „Optimieren Ihrer Webanwendungen durch das Zwischenspeichern von schreibgeschützten Daten mit Redis“ gefolgt sind.

Rufen Sie die Zugriffsschlüssel über den Befehl `az redis list-keys` ab. Führen Sie diese Befehle aus, um den Primärschlüssel abzurufen, ihn in einer Variablen namens `REDIS_KEY` zu speichern und anzuzeigen:

```azurecli
REDIS_KEY=$(az redis list-keys \
    --name "$REDIS_NAME" \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --query primaryKey \
    --output tsv)

echo $REDIS_KEY
```

Führen Sie anschließend diesen Befehl aus, um die Verbindungszeichenfolge zusammenzusetzen und in der Befehlszeile anzuzeigen. Beachten Sie, dass der Hostname der Name des Cache ist, gefolgt von `.redis.cache.windows.net`. Der Port ist **6380**, der Standard-SSL-Port von Redis.

```bash
echo "$REDIS_KEY"@"$REDIS_NAME".redis.cache.windows.net:6380?ssl=true
```

Kopieren Sie die Verbindungszeichenfolge in die Zwischenablage. Sie verwenden sie im nächsten Schritt.

## <a name="add-the-connection-string-to-your-app"></a>Hinzufügen der Verbindungszeichenfolge zu Ihrer App

1. Öffnen Sie den Cloud Shell-Editor im Anwendungsordner.

    ```bash
    cd ~/RedisData
    code .
    ```

1. Wählen Sie die Quelldatei **Program.cs** aus.

1. Erstellen Sie das folgende Feld in der `Program`-Klasse, und fügen Sie Ihre Verbindungszeichenfolge als Wert ein.

    ```csharp
    static string redisConnectionString = "<connection string>";
    ```

    Ein Beispiel:

    ```csharp
    static string redisConnectionString = "ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6380?ssl=true";
    ```

## <a name="insert-two-data-values-into-your-azure-redis-cache"></a>Einfügen von zwei Datenwerten in Ihre Azure Redis Cache-Instanz

Abschließend werden Sie Ihrer Azure Redis Cache-Instanz nun Daten hinzufügen.

1. Fügen Sie am Anfang der Datei **Program.cs** die folgende `using`-Anweisung hinzu.

    ```csharp
    using ServiceStack.Redis;
    ```

1. Ersetzen Sie den Inhalt der `Main`-Methode durch den nachstehenden Code. Hierbei wird eine Transaktion verwendet, um zwei Werte hinzuzufügen.

    ```csharp
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    if (transactionResult)
    {
        Console.WriteLine("Transaction committed");
    }
    else
    {
        Console.WriteLine("Transaction failed to commit");
    }
    ```

1. Bevor Sie die Anwendung kompilieren und ausführen, stellen Sie sicher, dass der Redis-Cache vollständig bereitgestellt wurde. Nach Abschluss von `az redis create` kann dies manchmal einige Minuten dauern. Führen Sie den folgenden Befehl aus, um den Status zu überprüfen.

    ```azcli
    az redis show \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --query provisioningState
    ```

    Wenn der Status `Creating` ist, versuchen Sie es in ein paar Minuten noch einmal. Nach Abschluss wird `Succeeded` angezeigt.

1. Führen Sie die Anwendung aus, und bestätigen Sie, dass in der Konsole **Commit für Transaktion ausgeführt** ausgegeben wird.

    ```bash
    dotnet run
    ```

## <a name="verify-your-data"></a>Überprüfen Ihrer Daten

Als letzten Schritt überprüfen Sie, ob sich die von Ihnen hinzugefügten Daten in Ihrer Azure Redis Cache-Instanz befinden.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.

1. Suchen Sie Ihre Azure Redis Cache-Instanz, indem Sie auf der linken Randleiste auf **Alle Ressourcen** klicken und über das Filterfeld auf der linken Seite Azure Redis Cache-Instanzen auswählen. Alternativ können Sie auch oben das Suchfeld verwenden und den Namen des Cache eingeben.

1. Wählen Sie Ihre Azure Redis Cache-Instanz aus.

1. Wählen Sie im Blatt **Übersicht** für Ihre Azure Redis Cache-Instanz die Option **Konsole** aus. Dadurch wird eine Azure Redis Cache-Konsole geöffnet, in der Sie detaillierte Azure Redis Cache-Befehle eingeben können.

1. Geben Sie **get MyKey1** ein. Vergewissern Sie sich, dass der zurückgegebene Wert **MyValue1** ist.

1. Geben Sie **get MyKey2** ein. Vergewissern Sie sich, dass der zurückgegebene Wert **MyValue2** ist.

    ![Screenshot der Azure Redis Cache-Konsole mit den Werten von „MyKey1“ und „MyKey2“.](../media/4-redis-console.png)