<span data-ttu-id="fdf8c-101">Als Erstes müssen wir eine leere Azure Cosmos DB-Datenbank und eine Sammlung erstellen, mit der wir arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-101">The first thing we need to do is create an empty Azure Cosmos DB database and collection to work with.</span></span> <span data-ttu-id="fdf8c-102">Diese sollen der Datenbank und der Sammlung entsprechen, die Sie im letzten Modul dieses Lernpfads erstellt haben. Wir benötigen also eine Datenbank namens **Products** und eine Sammlung namens **Clothing**.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-102">We want them to match the ones you created in the last module in this Learning Path: a database named **"Products"** and a collection named **"Clothing"**.</span></span> <span data-ttu-id="fdf8c-103">Verwenden Sie die folgenden Anweisungen sowie Azure Cloud Shell auf der rechten Bildschirmseite, um die Datenbank neu zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-103">Use the following instructions and the Azure Cloud Shell on the right side of the screen to recreate the database.</span></span>

## <a name="create-an-azure-cosmos-db-account--database-with-the-azure-cli"></a><span data-ttu-id="fdf8c-104">Erstellen eines Azure Cosmos DB-Kontos und einer -Datenbank mithilfe der Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="fdf8c-104">Create an Azure Cosmos DB account + database with the Azure CLI</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="select-a-subscription"></a><span data-ttu-id="fdf8c-105">Auswählen eines Abonnements</span><span class="sxs-lookup"><span data-stu-id="fdf8c-105">Select a subscription</span></span>

<span data-ttu-id="fdf8c-106">Wenn Sie Azure schon eine Weile verwenden, stehen Ihnen möglicherweise mehrere Abonnements zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-106">If you've been using Azure for a while, you might have multiple subscriptions available to you.</span></span> <span data-ttu-id="fdf8c-107">Dies ist häufig bei Entwicklern der Fall, die ein Abonnement für Visual Studio und weitere Unternehmensressourcen haben.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-107">This is often the case for developers who might have a subscription for Visual Studio, and another for corporate resources.</span></span>

<span data-ttu-id="fdf8c-108">Die Azure Sandbox hat in Cloud Shell bereits das Concierge-Abonnement für Sie ausgewählt, und Sie können mithilfe dieser Schritte die Abonnementeinstellung überprüfen.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-108">The Azure Sandbox has already selected the Concierge Subscription for you in the Cloud Shell, and you can validate the subscription setting using these steps.</span></span> <span data-ttu-id="fdf8c-109">Wenn Sie Ihr eigenes Abonnement verwenden, können Sie zum Wechseln von Abonnements mit der Azure-Befehlszeilenschnittstelle die folgenden Schritte ausführen.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-109">Or, when you are working with your own subscription, you can use the following steps to switch subscriptions with the Azure CLI.</span></span>

1. <span data-ttu-id="fdf8c-110">Beginnen Sie, indem Sie die verfügbaren Abonnements auflisten.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-110">Start by listing the available subscriptions.</span></span>

    ```azurecli
    az account list --output table
    ```

   <span data-ttu-id="fdf8c-111">Wenn Sie ein Concierge-Abonnement verwenden, sollte nur dieses aufgeführt sein.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-111">If you're working with a Concierge Subscription, it should be the only one listed.</span></span>

1. <span data-ttu-id="fdf8c-112">Wenn das Standardabonnement nicht das ist, das Sie verwenden möchten, können Sie dieses mithilfe des `account set`-Befehls ändern:</span><span class="sxs-lookup"><span data-stu-id="fdf8c-112">Next, if the default subscription isn't the one you want to use, you can change it with the `account set` command:</span></span>

    ```azurecli
    az account set --subscription "<subscription name>"
    ```
    
1. <span data-ttu-id="fdf8c-113">Rufen Sie die Ressourcengruppe ab, die von der Sandbox für Sie erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-113">Get the Resource Group that has been created for you by the sandbox.</span></span> <span data-ttu-id="fdf8c-114">Falls Sie Ihr eigenes Abonnement verwenden, überspringen Sie diesen Schritt, und geben Sie in der Umgebungsvariablen `RESOURCE_GROUP` weiter unten lediglich einen eindeutigen Namen an, den Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-114">If you are using your own subscription, skip this step and just supply a unique name you want to use in the `RESOURCE_GROUP` environment variable below.</span></span> <span data-ttu-id="fdf8c-115">Notieren Sie sich den Namen der Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-115">Take note of the Resource Group name.</span></span> <span data-ttu-id="fdf8c-116">Dort erstellen wir unsere Datenbank.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-116">This is where we will create our database.</span></span>

    ```azurecli
    az group list --out table
    ```
### <a name="setup-environment-variables"></a><span data-ttu-id="fdf8c-117">Einrichten von Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="fdf8c-117">Setup environment variables</span></span>

1. <span data-ttu-id="fdf8c-118">Legen Sie einige Umgebungsvariablen fest, um nicht immer wieder die gleichen Werte eingeben zu müssen.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-118">Set a few environment variables so you don't have to type the common values each time.</span></span> <span data-ttu-id="fdf8c-119">Legen Sie zunächst einen Namen für das Azure Cosmos DB-Konto fest (beispielsweise `export NAME="mycosmosdbaccount"`).</span><span class="sxs-lookup"><span data-stu-id="fdf8c-119">Start by setting a name for the Azure Cosmos DB account, for example `export NAME="mycosmosdbaccount"`.</span></span> <span data-ttu-id="fdf8c-120">Das Feld darf nur Kleinbuchstaben, Ziffern und Bindestriche enthalten und muss zwischen 3 und 31 Zeichen lang sein.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-120">The field can contain only lowercase letters, numbers and the '-' character, and must be between 3 and 31 characters.</span></span>

    ```azurecli
    export NAME="<Azure Cosmos DB account name>"
    ```

1. <span data-ttu-id="fdf8c-121">Legen Sie für die Ressourcengruppe die Verwendung der bereits vorhandenen Sandbox-Ressourcengruppe fest.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-121">Set the resource group to use the existing Sandbox resource group.</span></span>

    ```azurecli
    export RESOURCE_GROUP="<rgn>[Sandbox resource group name]</rgn>"
    ```

1. <span data-ttu-id="fdf8c-122">Wählen Sie die Region aus, die Ihnen am nächsten ist, und legen Sie die Umgebungsvariable entsprechen fest (Beispiel: `export LOCATION="EastUS"`).</span><span class="sxs-lookup"><span data-stu-id="fdf8c-122">Select the region closest to you, and set the environment variable, such as `export LOCATION="EastUS"`.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    export LOCATION="<location>"
    ```

1. <span data-ttu-id="fdf8c-123">Legen Sie eine Variable für den Datenbanknamen fest.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-123">Set a variable for the database name.</span></span> <span data-ttu-id="fdf8c-124">Nennen Sie sie „Products“, damit sie mit der Datenbank aus dem letzten Modul übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-124">Name it "Products" so it matches the database we created in the last module.</span></span>

    ```azurecli
    export DB_NAME="Products"
    ```

### <a name="create-a-resource-group-in-your-subscription"></a><span data-ttu-id="fdf8c-125">Erstellen einer Ressourcengruppe in Ihrem Abonnement</span><span class="sxs-lookup"><span data-stu-id="fdf8c-125">Create a resource group in your subscription</span></span>

<span data-ttu-id="fdf8c-126">Wenn Sie unter Verwendung Ihres eigenen Abonnements eine Cosmos DB-Datenbank erstellen, sollten Sie eine neue Ressourcengruppe erstellen, die alle zugehörigen Ressourcen enthält.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-126">When you are creating a Cosmos DB on your own subscription you will want to create a new resource group to hold all the related resources.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdf8c-127">Sie müssen diesen Schritt nicht ausführen, wenn Sie die von Microsoft Learn bereitgestellte Azure Sandbox verwenden.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-127">If you are using the Azure Sandbox provided by Microsoft Learn, then you do not need to execute this step.</span></span> <span data-ttu-id="fdf8c-128">Vergewissern Sie sich stattdessen, dass die obige Variable `RESOURCE_GROUP` auf **<rgn>[Sandbox-Ressourcengruppenname]</rgn>** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-128">Instead, make sure the `RESOURCE_GROUP` variable above is set to **<rgn>[Sandbox Resource Group Name</rgn>**.</span></span>

<span data-ttu-id="fdf8c-129">In Ihrem eigenen Abonnement verwenden Sie den folgenden Befehl, um die Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-129">In your own subscription you would use the following command to create the Resource Group.</span></span> 

```azurecli
az group create --name <name> --location <location>
```

### <a name="create-the-azure-cosmos-db-account"></a><span data-ttu-id="fdf8c-130">Erstellen des Azure Cosmos DB-Kontos</span><span class="sxs-lookup"><span data-stu-id="fdf8c-130">Create the Azure Cosmos DB account</span></span>

1. <span data-ttu-id="fdf8c-131">Erstellen Sie mithilfe des Befehls `cosmosdb create` das Azure Cosmos DB-Konto.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-131">Create the Azure Cosmos DB account with the `cosmosdb create` command.</span></span> <span data-ttu-id="fdf8c-132">Der Befehl verwendet die folgenden Parameter und kann ohne Änderungen ausgeführt werden, wenn Sie die Umgebungsvariablen wie empfohlen festgelegt haben.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-132">The command uses the following parameters and can be run with no modifications if you set the environment variables as recommended.</span></span>
    - <span data-ttu-id="fdf8c-133">`--name`: Eindeutiger Name für die Ressource</span><span class="sxs-lookup"><span data-stu-id="fdf8c-133">`--name`: Unique name for the resource.</span></span>
    - <span data-ttu-id="fdf8c-134">`--kind`: Datenbankart, verwenden Sie _GlobalDocumentDB_.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-134">`--kind`: Kind of database, use _GlobalDocumentDB_.</span></span>
    - <span data-ttu-id="fdf8c-135">`--resource-group`: Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="fdf8c-135">`--resource-group`: The resource group.</span></span> <span data-ttu-id="fdf8c-136">Verwenden Sie **<rgn>[Sandbox-Ressourcengruppe]</rgn>**.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-136">Use **<rgn>[Sandbox Resource Group]</rgn>**.</span></span> <span data-ttu-id="fdf8c-137">Diese sollte der `RESOURCE_GROUP`-Variable zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-137">It should be assigned to the `RESOURCE_GROUP` variable.</span></span>

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

    <span data-ttu-id="fdf8c-138">Die Ausführung des Befehls kann einige Minuten dauern und Cloud Shell zeigt die Einstellungen für das neue Konto an, sobald dieses bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-138">The command takes a few minutes to complete and the cloud shell displays the settings for the new account once it's deployed.</span></span>

1. <span data-ttu-id="fdf8c-139">Erstellen Sie unter dem Konto die Datenbank `Products`.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-139">Create the `Products` database in the account.</span></span>

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

1. <span data-ttu-id="fdf8c-140">Erstellen Sie abschließend die Sammlung `Clothing`.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-140">Finally, create the `Clothing` collection.</span></span>

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

<span data-ttu-id="fdf8c-141">Nachdem Sie nun über ein Azure Cosmos DB-Konto, eine Datenbank und eine Sammlung verfügen, können wir damit beginnen, Daten hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="fdf8c-141">Now that you have your Azure Cosmos DB account, database, and collection, let's go add some data!</span></span>