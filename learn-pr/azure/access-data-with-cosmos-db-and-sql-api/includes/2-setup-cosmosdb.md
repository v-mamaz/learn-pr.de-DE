> [!NOTE]
> Falls Sie zuvor **Erstellen einer skalierbaren Azure Cosmos DB-Datenbank** absolviert und die erstellte Cosmos DB-Datenbank sowie die Sammlung nicht gelöscht haben, können Sie diese Einheit überspringen und mit dem Hinzufügen von Daten mit dem Daten-Explorer fortfahren.

Als Erstes müssen wir eine leere Cosmos DB-Datenbank und eine Sammlung erstellen. Diese sollen der Datenbank und der Sammlung entsprechen, die Sie im letzten Modul dieses Lernpfads erstellt haben. Wir benötigen also eine Datenbank namens **Products** und eine Sammlung namens **Clothing**. Verwenden Sie die folgenden Anweisungen sowie Azure Cloud Shell auf der rechten Bildschirmseite, um die Datenbank neu zu erstellen.

# <a name="create-a-cosmos-db-account--database-with-the-azure-cli"></a>Erstellen eines Cosmos DB-Kontos und einer Datenbank mithilfe der Azure-Befehlszeilenschnittstelle

1. Wählen Sie zunächst das richtige Abonnement aus: Verwenden Sie die Abonnement-ID Ihres Abonnements für kostenlosen Education-Zugriff.

    ```azurecli
    az account list --output table
    ```

1. Vergewissern Sie sich, dass die Abonnementliste „sandbox“ enthält, und legen Sie dieses Element als die zu verwendende Option fest: <!-- TODO: get official name here -->

    ```azurecli
    az account set --subscription "sandbox"
    ```
    
1. Rufen Sie die Ressourcengruppe ab, die für Sie erstellt wurde. Falls Sie Ihr eigenes Abonnement verwenden, überspringen Sie diesen Schritt, und geben Sie in der Umgebungsvariablen `RESOURCE_GROUP` weiter unten lediglich einen eindeutigen Namen an, den Sie verwenden möchten. Notieren Sie sich den Namen der Ressourcengruppe. Dort erstellen wir unsere Datenbank. <!-- Do we get a token for this? -->

    ```azurecli
    az group list --out table
    ```

1. Legen Sie der Einfachheit halber einige Umgebungsvariablen fest, um nicht immer wieder die gleichen Werte eingeben zu müssen. 

    > [!IMPORTANT]
    > Diese Werte müssen auf die entsprechenden Werte für Ihre Sitzung festgelegt werden. Ersetzen Sie also beispielsweise den Wert `<resource group>` durch den Ressourcengruppennamen, den Sie weiter oben angegeben haben.

    ```azurecli
    export RESOURCE_GROUP="<resource group>"
    export NAME="<cosmos db name>"
    export LOCATION="<location>"
    ```
    
1. Legen Sie als Nächstes eine Variable für den Datenbanknamen fest. Nennen Sie sie „Users“, um der Datenbank aus dem letzten Modul zu entsprechen.

    ```azurecli
    export DB_NAME="Products"
    ```
    
1. Falls Sie hierbei Ihr eigenes Abonnement und eine _neue_ Ressourcengruppe verwenden (empfohlen), erstellen Sie die Ressourcengruppe mithilfe des folgenden Befehls. **Wichtig:** Bei Verwendung der kostenlosen Lernressourcen von Microsoft Learn ist dieser Schritt nicht erforderlich. Vergewissern Sie sich stattdessen, dass die obige Variable `RESOURCE_GROUP` auf Ihre zugewiesene Ressourcengruppe festgelegt ist.

    ```azurecli
    az group create --name $RESOURCE_GROUP --location $LOCATION
    ```
    
1. Erstellen Sie als Nächstes ein Azure Cosmos DB-Konto. Der Erstellungsvorgang dauert ein paar Minuten.

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```
    
1. Erstellen Sie unter dem Konto die Datenbank `Products`.

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```
    
1. Erstellen Sie abschließend die Sammlung `Clothing`.

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

Nachdem wir nun über ein Cosmos DB-Konto, eine Datenbank und eine Sammlung verfügen, können wir damit beginnen, Daten hinzuzufügen.