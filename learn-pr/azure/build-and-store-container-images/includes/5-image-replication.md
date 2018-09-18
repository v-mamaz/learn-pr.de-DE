<span data-ttu-id="4e616-101">Ihr Unternehmen stellt Computeworkloads in verschiedenen Regionen bereit, damit Sie lokale Präsenz für Ihren verteilten Kundenstamm zeigen.</span><span class="sxs-lookup"><span data-stu-id="4e616-101">Your company has compute workloads deployed to several regions to make sure you have a local presence to serve your distributed customer base.</span></span> 

<span data-ttu-id="4e616-102">Das Ziel ist, eine Containerregistrierung in jeder Region zu platzieren, in der Images ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="4e616-102">Your aim is to place a container registry in each region where images are run.</span></span> <span data-ttu-id="4e616-103">Durch diese Strategie werden netzwerknahe Vorgänge und dadurch schnelle, zuverlässige Übertragungen auf Imageebene gewährleistet.</span><span class="sxs-lookup"><span data-stu-id="4e616-103">This strategy will allow for network-close operations, enabling fast, reliable image layer transfers.</span></span> 

<span data-ttu-id="4e616-104">Mit der Georeplikation kann eine Azure-Containerregistrierung als zentrale Registrierung verwendet werden, die mehreren Regionen regionale Multimasterregistrierungen zur Verfügung stellt.</span><span class="sxs-lookup"><span data-stu-id="4e616-104">Geo-replication enables an Azure container registry to function as a single registry, serving several regions with multi-master regional registries.</span></span>

<span data-ttu-id="4e616-105">Eine Registrierung mit Georeplikation bietet folgende Vorteile:</span><span class="sxs-lookup"><span data-stu-id="4e616-105">A geo-replicated registry provides the following benefits:</span></span>

- <span data-ttu-id="4e616-106">einzelner Registrierungs-/Image-/Tagname in mehreren Regionen verwendbar</span><span class="sxs-lookup"><span data-stu-id="4e616-106">Single registry/image/tag names can be used across multiple regions</span></span>
- <span data-ttu-id="4e616-107">Netzwerknaher Registrierungszugriff in regionalen Bereitstellungen</span><span class="sxs-lookup"><span data-stu-id="4e616-107">Network-close registry access from regional deployments</span></span>
- <span data-ttu-id="4e616-108">Keine zusätzlichen Ausgangsgebühren, da Images aus einer lokalen, replizierten Registrierung in der gleichen Region wie Ihr Containerhost abgerufen werden</span><span class="sxs-lookup"><span data-stu-id="4e616-108">No additional egress fees, as images are pulled from a local, replicated registry in the same region as your container host</span></span>
- <span data-ttu-id="4e616-109">Zentrale Verwaltung einer Registrierung für mehrere Regionen</span><span class="sxs-lookup"><span data-stu-id="4e616-109">Single management of a registry across multiple regions</span></span>

## <a name="replicate-an-image-to-multiple-locations"></a><span data-ttu-id="4e616-110">Replizieren eines Images für mehrere Standorte</span><span class="sxs-lookup"><span data-stu-id="4e616-110">Replicate an image to multiple locations</span></span>

<span data-ttu-id="4e616-111">Sie verwenden den Azure CLI-Befehl `az acr replication create`, um Ihre Containerimages aus einer Region in eine andere zu replizieren.</span><span class="sxs-lookup"><span data-stu-id="4e616-111">You'll use the `az acr replication create` Azure CLI command to replicate your container images from one region to another.</span></span> <span data-ttu-id="4e616-112">In diesem Beispiel wird eine Replikation für die Region `japaneast` erstellt.</span><span class="sxs-lookup"><span data-stu-id="4e616-112">In this example, you'll create a replication for the `japaneast` region.</span></span> <span data-ttu-id="4e616-113">Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="4e616-113">Update `<acrName>` with the name of your Container Registry.</span></span>

```azurecli
az acr replication create --registry <acrName> --location japaneast
```

<span data-ttu-id="4e616-114">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="4e616-114">The output should look similar to the following:</span></span>

```console
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myACR0007/replications/japaneast",
  "location": "japaneast",
  "name": "japaneast",
  "provisioningState": "Succeeded",
  "resourceGroup": "myresourcegroup",
  "status": {
    "displayStatus": "Syncing",
    "message": null,
    "timestamp": "2018-08-15T20:22:09.275792+00:00"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries/replications"
}
```

<span data-ttu-id="4e616-115">Der letzte Schritt.</span><span class="sxs-lookup"><span data-stu-id="4e616-115">As a final step.</span></span> <span data-ttu-id="4e616-116">Sie können alle erstellten Replikate von Containerimages abrufen.</span><span class="sxs-lookup"><span data-stu-id="4e616-116">You are able to retrieve all container image replicas created.</span></span> <span data-ttu-id="4e616-117">Verwenden Sie den Befehl `az acr replication list` zum Abrufen dieser Liste.</span><span class="sxs-lookup"><span data-stu-id="4e616-117">You'll use the `az acr replication list` command to retrieve this list.</span></span> <span data-ttu-id="4e616-118">Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="4e616-118">Update `<acrName>` with the name of your Container Registry.</span></span>

```azurecli
az acr replication list --registry <acrName> --output table
```

<span data-ttu-id="4e616-119">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="4e616-119">The output should look similar to the following:</span></span>

```console
NAME       LOCATION    PROVISIONING STATE    STATUS
---------  ----------  --------------------  --------
japaneast  japaneast   Succeeded             Ready
eastus     eastus      Succeeded             Ready
```

<span data-ttu-id="4e616-120">Bedenken Sie, dass Sie für das Auflisten der Imagereplikate nicht nur Azure CLI verwenden können.</span><span class="sxs-lookup"><span data-stu-id="4e616-120">Keep in mind that you are not limited to the Azure CLI to list your image replicas.</span></span> <span data-ttu-id="4e616-121">Wenn Sie im Azure-Portal `Replications` für eine Azure-Containerregistrierung auswählen, wird eine Karte mit den aktuellen Replikationen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4e616-121">From within the Azure portal, selecting `Replications` for an Azure Container Registry displays a map that details current replications.</span></span> <span data-ttu-id="4e616-122">Containerimages können in zusätzliche Regionen repliziert werden, indem die Regionen auf der Karte ausgewählt werden.</span><span class="sxs-lookup"><span data-stu-id="4e616-122">Container images can be replicated to additional regions by selecting the regions on the map.</span></span>

![Replikationskarte für Container im Azure-Portal](../media/replication-map.png)

## <a name="clean-up"></a><span data-ttu-id="4e616-124">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="4e616-124">Clean up</span></span>
<!---TODO: Update for sandbox?--->

<span data-ttu-id="4e616-125">Sie können nun die erstellten Ressourcen bereinigen, indem Sie die Ressourcengruppe löschen.</span><span class="sxs-lookup"><span data-stu-id="4e616-125">At this point, you can cleanup the created resources by deleting the resource group.</span></span> <span data-ttu-id="4e616-126">Verwenden Sie hierzu den Befehl `az group delete`.</span><span class="sxs-lookup"><span data-stu-id="4e616-126">To do so, use the `az group delete` command.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a><span data-ttu-id="4e616-127">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="4e616-127">Summary</span></span>

<span data-ttu-id="4e616-128">Sie haben nun mit der Azure CLI erfolgreich ein Containerimage in mehreren Azure-Rechenzentren repliziert.</span><span class="sxs-lookup"><span data-stu-id="4e616-128">You've now successfully replicated a container image to multiple Azure datacenters using the Azure CLI.</span></span> 