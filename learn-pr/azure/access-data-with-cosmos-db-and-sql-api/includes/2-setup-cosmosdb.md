> [!NOTE]
> <span data-ttu-id="19aa6-101">Falls Sie zuvor **Erstellen einer skalierbaren Azure Cosmos DB-Datenbank** absolviert und die erstellte Cosmos DB-Datenbank sowie die Sammlung nicht gelöscht haben, können Sie diese Einheit überspringen und mit dem Hinzufügen von Daten mit dem Daten-Explorer fortfahren.</span><span class="sxs-lookup"><span data-stu-id="19aa6-101">If you are continuing on from **Create an Azure Cosmos DB database built to scale** and you did not delete the Cosmos DB database + collection that you created, then you can skip this unit and move on to adding data with the Data Explorer.</span></span>

<span data-ttu-id="19aa6-102">Als Erstes müssen wir eine leere Cosmos DB-Datenbank und eine Sammlung erstellen.</span><span class="sxs-lookup"><span data-stu-id="19aa6-102">The first thing we need to do is create an empty Cosmos DB database and collection to work with.</span></span> <span data-ttu-id="19aa6-103">Diese sollen der Datenbank und der Sammlung entsprechen, die Sie im letzten Modul dieses Lernpfads erstellt haben. Wir benötigen also eine Datenbank namens **Products** und eine Sammlung namens **Clothing**.</span><span class="sxs-lookup"><span data-stu-id="19aa6-103">We want it to match the one you created in the last module in this Learning Path: a database named **"Products"** and a collection named **"Clothing"**.</span></span> <span data-ttu-id="19aa6-104">Verwenden Sie die folgenden Anweisungen sowie Azure Cloud Shell auf der rechten Bildschirmseite, um die Datenbank neu zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="19aa6-104">Use the following instructions and the Azure Cloud Shell on the right side of the screen to recreate the database.</span></span>

# <a name="create-a-cosmos-db-account--database-with-the-azure-cli"></a><span data-ttu-id="19aa6-105">Erstellen eines Cosmos DB-Kontos und einer Datenbank mithilfe der Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="19aa6-105">Create a Cosmos DB account + database with the Azure CLI</span></span>

1. <span data-ttu-id="19aa6-106">Wählen Sie zunächst das richtige Abonnement aus: Verwenden Sie die Abonnement-ID Ihres Abonnements für kostenlosen Education-Zugriff.</span><span class="sxs-lookup"><span data-stu-id="19aa6-106">Start by selecting the correct subscription - you want to select the subscription ID associated with your free education access subscription.</span></span>

    ```azurecli
    az account list --output table
    ```

1. <span data-ttu-id="19aa6-107">Vergewissern Sie sich, dass die Abonnementliste „sandbox“ enthält, und legen Sie dieses Element als die zu verwendende Option fest: <!-- TODO: get official name here --></span><span class="sxs-lookup"><span data-stu-id="19aa6-107">Make sure you see "sandbox" in the subscription list and set it as the current one to use: <!-- TODO: get official name here --></span></span>

    ```azurecli
    az account set --subscription "sandbox"
    ```
    
1. <span data-ttu-id="19aa6-108">Rufen Sie die Ressourcengruppe ab, die für Sie erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="19aa6-108">Get the Resource Group that has been created for you.</span></span> <span data-ttu-id="19aa6-109">Falls Sie Ihr eigenes Abonnement verwenden, überspringen Sie diesen Schritt, und geben Sie in der Umgebungsvariablen `RESOURCE_GROUP` weiter unten lediglich einen eindeutigen Namen an, den Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="19aa6-109">If you are using your own subscription, skip this step and just supply a unique name you want to use in the `RESOURCE_GROUP` environment variable below.</span></span> <span data-ttu-id="19aa6-110">Notieren Sie sich den Namen der Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="19aa6-110">Take note of the Resource Group name.</span></span> <span data-ttu-id="19aa6-111">Dort erstellen wir unsere Datenbank.</span><span class="sxs-lookup"><span data-stu-id="19aa6-111">This is where we will create our database.</span></span> <!-- Do we get a token for this? -->

    ```azurecli
    az group list --out table
    ```

1. <span data-ttu-id="19aa6-112">Legen Sie der Einfachheit halber einige Umgebungsvariablen fest, um nicht immer wieder die gleichen Werte eingeben zu müssen.</span><span class="sxs-lookup"><span data-stu-id="19aa6-112">To make this a bit easier, set a few environment variables so you don't have to type the common values each time.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="19aa6-113">Diese Werte müssen auf die entsprechenden Werte für Ihre Sitzung festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="19aa6-113">Make sure to change these values to ones appropriate for your session.</span></span> <span data-ttu-id="19aa6-114">Ersetzen Sie also beispielsweise den Wert `<resource group>` durch den Ressourcengruppennamen, den Sie weiter oben angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="19aa6-114">For example, replace the `<resource group>` value with the Resource Group name you identified above.</span></span>

    ```azurecli
    export RESOURCE_GROUP="<resource group>"
    export NAME="<cosmos db name>"
    export LOCATION="<location>"
    ```
    
1. <span data-ttu-id="19aa6-115">Legen Sie als Nächstes eine Variable für den Datenbanknamen fest.</span><span class="sxs-lookup"><span data-stu-id="19aa6-115">Next, set a variable for the database name.</span></span> <span data-ttu-id="19aa6-116">Nennen Sie sie „Users“, um der Datenbank aus dem letzten Modul zu entsprechen.</span><span class="sxs-lookup"><span data-stu-id="19aa6-116">Name it "Users" so it matches the database we created in the last module.</span></span>

    ```azurecli
    export DB_NAME="Products"
    ```
    
1. <span data-ttu-id="19aa6-117">Falls Sie hierbei Ihr eigenes Abonnement und eine _neue_ Ressourcengruppe verwenden (empfohlen), erstellen Sie die Ressourcengruppe mithilfe des folgenden Befehls.</span><span class="sxs-lookup"><span data-stu-id="19aa6-117">If you are doing this on your own subscription, and you are using a _new_ Resource Group (recommended), then use the following command to create the Resource Group.</span></span> <span data-ttu-id="19aa6-118">**Wichtig:** Bei Verwendung der kostenlosen Lernressourcen von Microsoft Learn ist dieser Schritt nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="19aa6-118">**Important:** If you are using the free education resources provided by Microsoft Learn, then you do not need to execute this step.</span></span> <span data-ttu-id="19aa6-119">Vergewissern Sie sich stattdessen, dass die obige Variable `RESOURCE_GROUP` auf Ihre zugewiesene Ressourcengruppe festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="19aa6-119">Instead, make sure the `RESOURCE_GROUP` variable above is set to your assigned resource group.</span></span>

    ```azurecli
    az group create --name $RESOURCE_GROUP --location $LOCATION
    ```
    
1. <span data-ttu-id="19aa6-120">Erstellen Sie als Nächstes ein Azure Cosmos DB-Konto.</span><span class="sxs-lookup"><span data-stu-id="19aa6-120">Next, create the Cosmos DB account.</span></span> <span data-ttu-id="19aa6-121">Der Erstellungsvorgang dauert ein paar Minuten.</span><span class="sxs-lookup"><span data-stu-id="19aa6-121">This will take a few minutes to complete.</span></span>

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```
    
1. <span data-ttu-id="19aa6-122">Erstellen Sie unter dem Konto die Datenbank `Products`.</span><span class="sxs-lookup"><span data-stu-id="19aa6-122">Create the `Products` database in the account.</span></span>

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```
    
1. <span data-ttu-id="19aa6-123">Erstellen Sie abschließend die Sammlung `Clothing`.</span><span class="sxs-lookup"><span data-stu-id="19aa6-123">Finally, create the `Clothing` collection.</span></span>

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

<span data-ttu-id="19aa6-124">Nachdem wir nun über ein Cosmos DB-Konto, eine Datenbank und eine Sammlung verfügen, können wir damit beginnen, Daten hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="19aa6-124">Now that we have our Cosmos DB account, database, and collection, let's go add some data!</span></span>