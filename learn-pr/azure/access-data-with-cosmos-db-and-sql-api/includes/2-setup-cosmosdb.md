> [!NOTE]
> Falls Sie zuvor **Erstellen einer skalierbaren Azure Cosmos DB-Datenbank** absolviert und die erstellte Cosmos DB-Datenbank sowie die Sammlung nicht gelöscht haben, können Sie diese Einheit überspringen und mit dem Hinzufügen von Daten mit dem Daten-Explorer fortfahren.

Als Erstes müssen wir eine leere Cosmos DB-Datenbank und eine Sammlung erstellen. Diese sollen der Datenbank und der Sammlung entsprechen, die Sie im letzten Modul dieses Lernpfads erstellt haben. Wir benötigen also eine Datenbank namens **Products** und eine Sammlung namens **Clothing**. Verwenden Sie die folgenden Anweisungen sowie Azure Cloud Shell auf der rechten Bildschirmseite, um die Datenbank neu zu erstellen.

# <a name="create-a-cosmos-db-account--database-with-the-azure-cli"></a>Erstellen eines Cosmos DB-Kontos und einer Datenbank mithilfe der Azure-Befehlszeilenschnittstelle

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<!--
TODO: This is original text prior to updates to use the sandbox. These can be worked back in as instructions for people using their own subscriptions. There is one more block like this below. Note that the assignment of RESOURCE_GROUP below would need to be different as well.

1. Start by selecting the correct subscription - you want to select the subscription ID associated with your free education access subscription.

    ```azurecli
    az account list --output table
    ```

1. Make sure you see "sandbox" in the subscription list and set it as the current one to use:

    ```azurecli
    az account set --subscription "sandbox"
    ```
    
1. Get the Resource Group that has been created for you. If you are using your own subscription, skip this step and just supply a unique name you want to use in the `RESOURCE_GROUP` environment variable below. Take note of the Resource Group name. This is where we will create our database.

    ```azurecli
    az group list --out table
    ```
-->

1. Legen Sie einige Umgebungsvariablen, sodass Sie keine häufig verwendeten Werte jedes Mal erneut eingeben.

    > [!IMPORTANT]
    > Diese Werte müssen auf die entsprechenden Werte für Ihre Sitzung festgelegt werden. Ersetzen Sie z. B. die `<comsos db name>` Wert mit dem Namen Ihrer Cosmos DB haben möchten.

    ```azurecli
    export RESOURCE_GROUP="<rgn>[Sandbox resource group name]</rgn>"
    export NAME="<cosmos db name>"
    export LOCATION="<location>"
    ```

2. Legen Sie als Nächstes eine Variable für den Datenbanknamen fest. Nennen Sie sie „Users“, um der Datenbank aus dem letzten Modul zu entsprechen.

    ```azurecli
    export DB_NAME="Products"
    ```

<!-- 

TODO: Pre-sandbox text to be worked back in.

1. If you are doing this on your own subscription, and you are using a _new_ Resource Group (recommended), then use the following command to create the Resource Group. **Important:** If you are using the free education resources provided by Microsoft Learn, then you do not need to execute this step. Instead, make sure the `RESOURCE_GROUP` variable above is set to your assigned resource group.

    ```azurecli
    az group create --name $RESOURCE_GROUP --location $LOCATION
    ```
-->

3. Erstellen Sie als Nächstes ein Azure Cosmos DB-Konto. Der Erstellungsvorgang dauert ein paar Minuten.

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

4. Erstellen Sie unter dem Konto die Datenbank `Products`.

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

5. Erstellen Sie abschließend die Sammlung `Clothing`.

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

Nachdem wir nun über ein Cosmos DB-Konto, eine Datenbank und eine Sammlung verfügen, können wir damit beginnen, Daten hinzuzufügen.