<span data-ttu-id="bb311-101">Das Festlegen von Umgebungsvariablen in Ihren Containerinstanzen ermöglicht Ihnen, eine dynamische Konfiguration der Anwendung oder des Skripts bereitzustellen, die bzw. das vom Container ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="bb311-101">Setting environment variables in your container instances allows you to provide dynamic configuration of the application or script run by the container.</span></span> <span data-ttu-id="bb311-102">Umgebungsvariablen werden bei der Containererstellung über die Azure CLI, PowerShell oder das Azure-Portal festgelegt.</span><span class="sxs-lookup"><span data-stu-id="bb311-102">Environment variables are set using the Azure CLI, PowerShell, or the Azure portal at container creation time.</span></span> <span data-ttu-id="bb311-103">Abgesicherte Umgebungsvariablen werden zum Schutz vor der Preisgabe sensibler Informationen in der Ausgabe von Containervorgängen verwendet.</span><span class="sxs-lookup"><span data-stu-id="bb311-103">Secured environment variables are used to prevent sensitive information from being displayed in container operations output.</span></span>

<span data-ttu-id="bb311-104">In dieser Einheit wird eine Azure Cosmos DB-Instanz erstellt. Dann wird eine Azure-Containerinstanz mit den Verbindungsinformationen der Azure Cosmos DB-Instanz ausgeführt, die als Umgebungsvariablen gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="bb311-104">In this unit, an Azure Azure Cosmos DB instance is created and then an Azure Container Instance run with the connection information of the Azure Cosmos DB stored as environment variables.</span></span> <span data-ttu-id="bb311-105">Eine Anwendung im Container nutzt die Variablen, um Azure Cosmos DB-Daten zu schreiben und zu lesen.</span><span class="sxs-lookup"><span data-stu-id="bb311-105">An application in the container uses the variables to write and read data from Azure Azure Cosmos DB.</span></span> <span data-ttu-id="bb311-106">In dieser Einheit erstellen Sie sowohl eine Umgebungsvariable als auch eine abgesicherte Umgebungsvariable.</span><span class="sxs-lookup"><span data-stu-id="bb311-106">During this unit, you will create both an environment variable and a secured environment variable.</span></span>

## <a name="deploy-cosmose-db"></a><span data-ttu-id="bb311-107">Bereitstellen von Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bb311-107">Deploy Cosmose DB</span></span>

<span data-ttu-id="bb311-108">Erstellen Sie mithilfe des Befehls `az Azure Cosmos DB create` die Azure Cosmos DB-Instanz.</span><span class="sxs-lookup"><span data-stu-id="bb311-108">Create the Azure Cosmos DB instance with the `az Azure Cosmos DB create` command.</span></span> <span data-ttu-id="bb311-109">Bei diesem Beispiel wird auch die Azure Cosmos DB-Endpunktadresse in einer Variablen mit dem Namen *COSMOS_DB_ENDPOINT* angegeben.</span><span class="sxs-lookup"><span data-stu-id="bb311-109">This example will also place the Azure Cosmos DB endpoint address in a variable named *COSMOS_DB_ENDPOINT*.</span></span>

<span data-ttu-id="bb311-110">Die Ausführung dieses Befehls kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="bb311-110">This command can take a few minutes to complete</span></span>

```azurecli
COSMOS_DB_ENDPOINT=$(az cosmosdb create --resource-group myResourceGroup --name aci-cosmos --query documentEndpoint -o tsv)
```

<span data-ttu-id="bb311-111">Rufen Sie als Nächstes den Azure Cosmos DB-Verbindungsschlüssel mit dem Befehl `az cosmosdb list-keys` ab, und speichern Sie ihn in einer Variablen namens *COSMOS_DB_DB_MASTERKEY*.</span><span class="sxs-lookup"><span data-stu-id="bb311-111">Next, get the Azure Cosmos DB connection key with the `az cosmosdb list-keys` command and store it in a variable named *COSMOS_DB_MASTERKEY*.</span></span>

```azurecli
COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys --resource-group myResourceGroup --name aci-cosmos --query primaryMasterKey -o tsv)
```

## <a name="deploy-container-instance"></a><span data-ttu-id="bb311-112">Bereitstellen einer Containerinstanz</span><span class="sxs-lookup"><span data-stu-id="bb311-112">Deploy container instance</span></span>

<span data-ttu-id="bb311-113">Führen Sie den Befehl `az container create` aus, um eine Azure-Containerinstanz zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="bb311-113">Create an Azure Container instance using the `az container create` command.</span></span> <span data-ttu-id="bb311-114">Beachten Sie, dass zwei Umgebungsvariablen erstellt werden, `COSMOS_DB_ENDPOINT` und `COSMOS_DB_ENDPOINT`.</span><span class="sxs-lookup"><span data-stu-id="bb311-114">Take note that two environment variables are created, `COSMOS_DB_ENDPOINT` and `COSMOS_DB_ENDPOINT`.</span></span> <span data-ttu-id="bb311-115">Diese Variablen enthalten die Werte, die für die Verbindung mit der Azure Cosmos DB-Instanz benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="bb311-115">These variables hold the values needed to connect to the Azure Cosmos DB instance.</span></span>

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name aci-demo \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --environment-variables COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
```

<span data-ttu-id="bb311-116">Nachdem der Container erstellt wurde, rufen Sie mit dem Befehl `az container show` die öffentliche IP-Adresse ab.</span><span class="sxs-lookup"><span data-stu-id="bb311-116">Once the container has been created, get the IP address with the `az container show` command.</span></span>

```azurecli
az container show --resource-group myResourceGroup --name aci-demo --query ipAddress.ip --output tsv
```

<span data-ttu-id="bb311-117">Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers.</span><span class="sxs-lookup"><span data-stu-id="bb311-117">Open up a browser and navigate to the IP address of the container.</span></span> <span data-ttu-id="bb311-118">Die folgende Anwendung sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="bb311-118">You should see the following application.</span></span> <span data-ttu-id="bb311-119">Bei der Abgabe einer Stimme wird die Stimme in der Azure Cosmos DB-Instanz gespeichert.</span><span class="sxs-lookup"><span data-stu-id="bb311-119">When casing a vote, the vote is stored in the Azure Cosmos DB.</span></span>

![Azure-Abstimmungsanwendung mit zwei Wahlmöglichkeiten: Katzen oder Hunde.](../media-draft/azure-vote.png)

## <a name="secured-environment-variables"></a><span data-ttu-id="bb311-121">Abgesicherte Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="bb311-121">Secured environment variables</span></span>

<span data-ttu-id="bb311-122">In der vorherigen Übung wurde ein Container mit Verbindungsinformationen für Azure Cosmos DB erstellt, die in zwei Umgebungsvariablen gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="bb311-122">In the previous exercise, a container was created with connection information for Azure Cosmos DB stored in two environment variables.</span></span> <span data-ttu-id="bb311-123">Standardmäßig werden Umgebungsvariablen im Azure-Portal und in Befehlszeilentools als Klartext angezeigt.</span><span class="sxs-lookup"><span data-stu-id="bb311-123">By default, environment variables are displayed in the Azure portal and command-line tools in plan text.</span></span>

<span data-ttu-id="bb311-124">Wenn Sie beispielsweise mit dem Befehl `az container show` Informationen über den Container abrufen, der in der vorherigen Übung erstellt wurde, können die Umgebungsvariablen im Klartext angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="bb311-124">For example, if you get information about the container created in the previous exercise with the `az container show` command, the environment variables are accusable in plan text.</span></span>

```azurecli
az container show --resource-group myResourceGroup --name aci-demo --query containers[0].environmentVariables
```

<span data-ttu-id="bb311-125">Beispielausgabe</span><span class="sxs-lookup"><span data-stu-id="bb311-125">Example output.</span></span>

```bash
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

Abgesicherte Umgebungsvariablen verhindern die Ausgabe als Klartext. <span data-ttu-id="bb311-127">Um abgesicherte Umgebungsvariablen zu verwenden, ersetzen Sie das Argument `--environment-variables` durch das Argument `--secure-environment-variables`.</span><span class="sxs-lookup"><span data-stu-id="bb311-127">To use secure environment variables, replace the `--environment-variables` argument with the `--secure-environment-variables` argument.</span></span>

<span data-ttu-id="bb311-128">Führen Sie das folgende Beispiel aus, um einen Container mit dem Namen *aci-demo-secure* zu erstellen, der abgesicherte Umgebungsvariablen verwendet.</span><span class="sxs-lookup"><span data-stu-id="bb311-128">Run the following example to create a container named *aci-demo-secure* that utilizes secured environment variables.</span></span>

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name aci-demo-secure \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --secure-environment-variables COSMOS_DB_ENDPOINT=$COSMOS_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_KEY
```

<span data-ttu-id="bb311-129">Wenn der Container nun mit dem Befehl `az container show` zurückgegeben wird, werden die Umgebungsvariablen nicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="bb311-129">Now, when the container is returned with the `az container show` command, the environment variables are not displayed.</span></span>

```azurecli
az container show --resource-group myResourceGroup --name aci-demo-secure --query containers[0].environmentVariables
```

<span data-ttu-id="bb311-130">Beispielausgabe</span><span class="sxs-lookup"><span data-stu-id="bb311-130">Example output.</span></span>

```bash
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

## <a name="summary"></a><span data-ttu-id="bb311-131">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="bb311-131">Summary</span></span>

<span data-ttu-id="bb311-132">In dieser Einheit haben Sie eine Azure Cosmos DB-Instanz und eine Azur- Containerinstanz erstellt.</span><span class="sxs-lookup"><span data-stu-id="bb311-132">In this unit, you created an Azure Azure Cosmos DB instance and an Azure Container Instance.</span></span> <span data-ttu-id="bb311-133">Umgebungsvariablen wurden in der Containerinstanz so festgelegt, dass die im Container ausgeführte Anwendung die Verbindung mit Azure Cosmos DB herstellen konnte.</span><span class="sxs-lookup"><span data-stu-id="bb311-133">Environment variables were set in the container instance such that the application running inside of the container was able to connect to the Azure Cosmos DB.</span></span>

<span data-ttu-id="bb311-134">In der nächsten Lektion binden Sie Datenvolumes in eine Azure-Containerinstanz ein, um Daten dauerhaft zu speichern.</span><span class="sxs-lookup"><span data-stu-id="bb311-134">In the next unit, you will mount data volumes to an Azure Container Instance for date persistence.</span></span>
