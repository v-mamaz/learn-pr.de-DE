Als Erstes müssen wir eine leere Azure Cosmos DB-Datenbank und eine Sammlung erstellen, mit der wir arbeiten können. Diese sollen der Datenbank und der Sammlung entsprechen, die Sie im letzten Modul dieses Lernpfads erstellt haben. Wir benötigen also eine Datenbank namens **Products** und eine Sammlung namens **Clothing**. Verwenden Sie die folgenden Anweisungen sowie Azure Cloud Shell auf der rechten Bildschirmseite, um die Datenbank neu zu erstellen.

## <a name="create-an-azure-cosmos-db-account--database-with-the-azure-cli"></a>Erstellen eines Azure Cosmos DB-Kontos und einer -Datenbank mithilfe der Azure-Befehlszeilenschnittstelle

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="select-a-subscription"></a>Auswählen eines Abonnements

Wenn Sie Azure schon eine Weile verwenden, stehen Ihnen möglicherweise mehrere Abonnements zur Verfügung. Dies ist häufig bei Entwicklern der Fall, die ein Abonnement für Visual Studio und weitere Unternehmensressourcen haben.

Die Azure-Sandbox hat in Cloud Shell bereits das Concierge-Abonnement für Sie ausgewählt, und Sie können mithilfe dieser Schritte die Abonnementeinstellung überprüfen. Wenn Sie Ihr eigenes Abonnement verwenden, können Sie zum Wechseln von Abonnements mit der Azure-Befehlszeilenschnittstelle die folgenden Schritte ausführen.

1. Beginnen Sie, indem Sie die verfügbaren Abonnements auflisten.

    ```azurecli
    az account list --output table
    ```

   Wenn Sie ein Concierge-Abonnement verwenden, sollte nur dieses aufgeführt sein.

1. Wenn das Standardabonnement nicht das ist, das Sie verwenden möchten, können Sie dieses mithilfe des `account set`-Befehls ändern:

    ```azurecli
    az account set --subscription "<subscription name>"
    ```
    
1. Rufen Sie die Ressourcengruppe ab, die von der Sandbox für Sie erstellt wurde. Falls Sie Ihr eigenes Abonnement verwenden, überspringen Sie diesen Schritt, und geben Sie in der Umgebungsvariablen `RESOURCE_GROUP` weiter unten lediglich einen eindeutigen Namen an, den Sie verwenden möchten. Notieren Sie sich den Namen der Ressourcengruppe. Dort erstellen wir unsere Datenbank.

    ```azurecli
    az group list --out table
    ```
### <a name="setup-environment-variables"></a>Einrichten von Umgebungsvariablen

1. Legen Sie einige Umgebungsvariablen fest, um nicht immer wieder die gleichen Werte eingeben zu müssen. Legen Sie zunächst einen Namen für das Azure Cosmos DB-Konto fest (beispielsweise `export NAME="mycosmosdbaccount"`). Das Feld darf nur Kleinbuchstaben, Ziffern und Bindestriche enthalten und muss zwischen 3 und 31 Zeichen lang sein.

    ```azurecli
    export NAME="<Azure Cosmos DB account name>"
    ```

1. Legen Sie die Ressourcengruppe darauf fest, die bereits vorhandene Sandboxressourcengruppe zu verwenden.

    ```azurecli
    export RESOURCE_GROUP="<rgn>[sandbox resource group name]</rgn>"
    ```

1. Wählen Sie die Region aus, die Ihnen am nächsten ist, und legen Sie die Umgebungsvariable entsprechend fest (Beispiel: `export LOCATION="EastUS"`).

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    export LOCATION="<location>"
    ```

1. Legen Sie eine Variable für den Datenbanknamen fest. Nennen Sie sie „Products“, damit sie mit der Datenbank aus dem letzten Modul übereinstimmt.

    ```azurecli
    export DB_NAME="Products"
    ```

### <a name="create-a-resource-group-in-your-subscription"></a>Erstellen einer Ressourcengruppe in Ihrem Abonnement

Wenn Sie unter Verwendung Ihres eigenen Abonnements eine Cosmos DB-Datenbank erstellen, sollten Sie eine neue Ressourcengruppe erstellen, die alle zugehörigen Ressourcen enthält.

> [!IMPORTANT]
> Sie müssen diesen Schritt nicht ausführen, wenn Sie die von Microsoft Learn bereitgestellte Azure-Sandbox verwenden. Vergewissern Sie sich stattdessen, dass die obige Variable `RESOURCE_GROUP` auf **<rgn>[Name der Sandboxressourcengruppe]</rgn>** festgelegt ist.

In Ihrem eigenen Abonnement verwenden Sie den folgenden Befehl, um die Ressourcengruppe zu erstellen. 

```azurecli
az group create --name <name> --location <location>
```

### <a name="create-the-azure-cosmos-db-account"></a>Erstellen des Azure Cosmos DB-Kontos

1. Erstellen Sie mithilfe des Befehls `cosmosdb create` das Azure Cosmos DB-Konto. Der Befehl verwendet die folgenden Parameter und kann ohne Änderungen ausgeführt werden, wenn Sie die Umgebungsvariablen wie empfohlen festgelegt haben.
    - `--name`: Eindeutiger Name für die Ressource
    - `--kind`: Datenbankart, verwenden Sie _GlobalDocumentDB_.
    - `--resource-group`: Ressourcengruppe Verwenden Sie **<rgn>[Sandboxressourcengruppe]</rgn>**. Diese sollte der `RESOURCE_GROUP`-Variable zugewiesen sein.

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

    Die Ausführung des Befehls kann einige Minuten dauern und Cloud Shell zeigt die Einstellungen für das neue Konto an, sobald dieses bereitgestellt wird.

1. Erstellen Sie unter dem Konto die Datenbank `Products`.

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

1. Erstellen Sie abschließend die Sammlung `Clothing`.

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

Nachdem Sie nun über ein Azure Cosmos DB-Konto, eine Datenbank und eine Sammlung verfügen, können wir damit beginnen, Daten hinzuzufügen.