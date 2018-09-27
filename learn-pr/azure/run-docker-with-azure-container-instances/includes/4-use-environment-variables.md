<span data-ttu-id="69892-101">Mithilfe von Umgebungsvariablen in Ihren Containerinstanzen können Sie eine dynamische Konfiguration der Anwendung oder des Skripts vornehmen, die bzw. das der Container ausführt.</span><span class="sxs-lookup"><span data-stu-id="69892-101">Environment variables in your container instances allow you to provide dynamic configuration of the application or script run by the container.</span></span> <span data-ttu-id="69892-102">Sie können entweder die Azure-Befehlszeilenschnittstelle, PowerShell oder das Azure-Portal verwenden, um Variablen bei der Containererstellung festzulegen.</span><span class="sxs-lookup"><span data-stu-id="69892-102">You can use the Azure CLI, PowerShell, or the Azure portal to set variables when you create the container.</span></span> <span data-ttu-id="69892-103">Abgesicherte Umgebungsvariablen werden zum Schutz vor der Preisgabe sensibler Informationen in der Ausgabe von Containern verwendet.</span><span class="sxs-lookup"><span data-stu-id="69892-103">Secured environment variables are used to prevent sensitive information from being displayed in container output.</span></span>

<span data-ttu-id="69892-104">Hier erstellen Sie eine Azure Cosmos DB-Instanz und verwenden Umgebungsvariablen, um die Verbindungsinformationen an eine Azure-Containerinstanz zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="69892-104">Here, you will create an Azure Cosmos DB instance and use environment variables to pass the connection information to an Azure container instance.</span></span> <span data-ttu-id="69892-105">Eine Anwendung im Container nutzt die Variablen, um Cosmos DB-Daten zu schreiben und zu lesen.</span><span class="sxs-lookup"><span data-stu-id="69892-105">An application in the container uses the variables to write and read data from Cosmos DB.</span></span> <span data-ttu-id="69892-106">Sie erstellen sowohl eine Umgebungsvariable als auch eine abgesicherte Umgebungsvariable.</span><span class="sxs-lookup"><span data-stu-id="69892-106">You will create both an environment variable and a secured environment variable.</span></span>

## <a name="deploy-azure-cosmos-db"></a><span data-ttu-id="69892-107">Bereitstellen von Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="69892-107">Deploy Azure Cosmos DB</span></span>

<span data-ttu-id="69892-108">Erstellen Sie mithilfe des Befehls `az cosmosdb create` die Azure Cosmos DB-Instanz.</span><span class="sxs-lookup"><span data-stu-id="69892-108">Create the Azure Cosmos DB instance with the `az cosmosdb create` command.</span></span> <span data-ttu-id="69892-109">Bei diesem Beispiel wird auch die Azure Cosmos DB-Endpunktadresse in einer Variablen mit dem Namen *COSMOS_DB_ENDPOINT* angegeben.</span><span class="sxs-lookup"><span data-stu-id="69892-109">This example will also place the Azure Cosmos DB endpoint address in a variable named *COSMOS_DB_ENDPOINT*.</span></span> <span data-ttu-id="69892-110">Geben Sie einen eindeutigen Namen für `[cosmos-db-name]` an.</span><span class="sxs-lookup"><span data-stu-id="69892-110">You'll need to supply a unique name for `[cosmos-db-name]`.</span></span>

<span data-ttu-id="69892-111">Die Ausführung dieses Befehls kann einige Minuten dauern:</span><span class="sxs-lookup"><span data-stu-id="69892-111">This command can take a few minutes to complete:</span></span>

```azurecli
COSMOS_DB_ENDPOINT=$(az cosmosdb create --resource-group <rgn>[sandbox resource group name]</rgn> --name [cosmos-db-name] --query documentEndpoint --output tsv)
```

<span data-ttu-id="69892-112">Rufen Sie als Nächstes den Azure Cosmos DB-Verbindungsschlüssel mit dem Befehl `az cosmosdb list-keys` ab, und speichern Sie ihn in einer Variablen namens *COSMOS_DB_DB_MASTERKEY*.</span><span class="sxs-lookup"><span data-stu-id="69892-112">Next, get the Azure Cosmos DB connection key with the `az cosmosdb list-keys` command and store it in a variable named *COSMOS_DB_MASTERKEY*.</span></span> <span data-ttu-id="69892-113">Denken Sie daran, `[cosmos-db-name]` erneut zu ersetzen:</span><span class="sxs-lookup"><span data-stu-id="69892-113">Don't forget to replace `[cosmos-db-name]` again:</span></span>

```azurecli
COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys --resource-group <rgn>[sandbox resource group name]</rgn> --name [cosmos-db-name] --query primaryMasterKey --output tsv)
```

## <a name="deploy-a-container-instance"></a><span data-ttu-id="69892-114">Bereitstellen einer Containerinstanz</span><span class="sxs-lookup"><span data-stu-id="69892-114">Deploy a container instance</span></span>

<span data-ttu-id="69892-115">Führen Sie den Befehl `az container create` aus, um eine Azure-Containerinstanz zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="69892-115">Create an Azure container instance using the `az container create` command.</span></span> <span data-ttu-id="69892-116">Beachten Sie, dass zwei Umgebungsvariablen erstellt werden, `COSMOS_DB_ENDPOINT` und `COSMOS_DB_MASTERKEY`.</span><span class="sxs-lookup"><span data-stu-id="69892-116">Take note that two environment variables are created, `COSMOS_DB_ENDPOINT` and `COSMOS_DB_MASTERKEY`.</span></span> <span data-ttu-id="69892-117">Diese Variablen enthalten die Werte, die für die Verbindung mit der Azure Cosmos DB-Instanz benötigt werden:</span><span class="sxs-lookup"><span data-stu-id="69892-117">These variables hold the values needed to connect to the Azure Cosmos DB instance:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --location eastus \
    --environment-variables COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
```

<span data-ttu-id="69892-118">Rufen Sie nach Abschluss der Containererstellung mithilfe des Befehls `az container show` die IP-Adresse ab:</span><span class="sxs-lookup"><span data-stu-id="69892-118">Once the container has been created, get the IP address with the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo \
    --query ipAddress.ip \
    --output tsv
```

<span data-ttu-id="69892-119">Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers.</span><span class="sxs-lookup"><span data-stu-id="69892-119">Open a browser and navigate to the IP address of the container.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="69892-120">Manchmal brauchen Container ein oder zwei Minuten, um vollständig betriebsbereit zu sein und Verbindungen aufnehmen zu können.</span><span class="sxs-lookup"><span data-stu-id="69892-120">Sometimes containers take a minute or two to fully start up and be able to receive connections.</span></span> <span data-ttu-id="69892-121">Wenn beim Navigieren zur IP-Adresse in Ihrem Browser keine Antwort angezeigt wird, warten Sie einen Moment, und aktualisieren Sie dann die Seite.</span><span class="sxs-lookup"><span data-stu-id="69892-121">If there's no response when you navigate to the IP address in your browser,  wait a few moments and refresh the page.</span></span>

 <span data-ttu-id="69892-122">Sobald die App verfügbar ist, sollte die folgende Anwendung angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="69892-122">Once the app is available, you should see the following application.</span></span> <span data-ttu-id="69892-123">Abgegebene Stimmen werden in der Azure Cosmos DB-Instanz gespeichert.</span><span class="sxs-lookup"><span data-stu-id="69892-123">When casting a vote, the vote is stored in the Azure Cosmos DB instance.</span></span>

![Azure-Abstimmungsanwendung mit zwei Wahlmöglichkeiten: Katzen oder Hunde.](../media/4-azure-vote.png)

## <a name="secured-environment-variables"></a><span data-ttu-id="69892-125">Abgesicherte Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="69892-125">Secured environment variables</span></span>

<span data-ttu-id="69892-126">In der vorherigen Übung wurde ein Container mit Verbindungsinformationen für Azure Cosmos DB erstellt, die in zwei Umgebungsvariablen gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="69892-126">In the previous exercise, a container was created with connection information for Azure Cosmos DB stored in two environment variables.</span></span> <span data-ttu-id="69892-127">Standardmäßig werden Umgebungsvariablen im Azure-Portal und in Befehlszeilentools als Klartext angezeigt.</span><span class="sxs-lookup"><span data-stu-id="69892-127">By default, environment variables are displayed in the Azure portal and command-line tools in plain text.</span></span>

<span data-ttu-id="69892-128">Wenn Sie beispielsweise mit dem Befehl `az container show` Informationen zu dem Container abrufen, der in der vorherigen Übung erstellt wurde, stehen die Umgebungsvariablen als Klartext zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="69892-128">For example, if you get information about the container created in the previous exercise with the `az container show` command, the environment variables are accessible in plain text:</span></span>

```azurecli
az container show --resource-group <rgn>[sandbox resource group name]</rgn> --name aci-demo --query containers[0].environmentVariables
```

<span data-ttu-id="69892-129">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="69892-129">Example output:</span></span>

```json
[
  {
    "name": "COSMOS_DB_ENDPOINT",
    "secureValue": null,
    "value": "https://aci-cosmos.documents.azure.com:443/"
  },
  {
    "name": "COSMOS_DB_MASTERKEY",
    "secureValue": null,
    "value": "Xm5BwdLlCllBvrR26V00000000S2uOusuglhzwkE7dOPMBQ3oA30n3rKd8PKA13700000000095ynys863Ghgw=="
  }
]
```

Abgesicherte Umgebungsvariablen verhindern die Ausgabe als Klartext. <span data-ttu-id="69892-131">Um abgesicherte Umgebungsvariablen zu verwenden, ersetzen Sie das Argument `--environment-variables` durch das Argument `--secure-environment-variables`.</span><span class="sxs-lookup"><span data-stu-id="69892-131">To use secure environment variables, replace the `--environment-variables` argument with the `--secure-environment-variables` argument.</span></span>

<span data-ttu-id="69892-132">Führen Sie das folgende Beispiel aus, um einen Container mit dem Namen *aci-demo-secure* zu erstellen, der abgesicherte Umgebungsvariablen verwendet:</span><span class="sxs-lookup"><span data-stu-id="69892-132">Run the following example to create a container named *aci-demo-secure* that utilizes secured environment variables:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --location eastus \
    --secure-environment-variables COSMOS_DB_ENDPOINT=$COSMOS_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_KEY
```

<span data-ttu-id="69892-133">Wenn der Container nun mit dem Befehl `az container show` zurückgegeben wird, werden die Umgebungsvariablen nicht angezeigt:</span><span class="sxs-lookup"><span data-stu-id="69892-133">Now, when the container is returned with the `az container show` command, the environment variables are not displayed:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --query containers[0].environmentVariables
```

<span data-ttu-id="69892-134">Beispielausgabe:</span><span class="sxs-lookup"><span data-stu-id="69892-134">Example output:</span></span>

```json
[
  {
    "name": "COSMOS_DB_ENDPOINT",
    "secureValue": null,
    "value": null
  },
  {
    "name": "COSMOS_DB_MASTERKEY",
    "secureValue": null,
    "value": null
  }
]
```