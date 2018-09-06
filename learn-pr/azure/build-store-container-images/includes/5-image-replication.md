<span data-ttu-id="d652a-101">Als bewährte Methode ermöglicht die Platzierung einer Containerregistrierung in jeder Region, in der Images ausgeführt werden, netzwerknahe Vorgänge, die schnelle und zuverlässige Übertragungen auf Imageebene gestatten.</span><span class="sxs-lookup"><span data-stu-id="d652a-101">As a best practice, placing a container registry in each region where images are run allows network-close operations, enabling fast, reliable image layer transfers.</span></span> <span data-ttu-id="d652a-102">Mit der Georeplikation kann eine Azure-Containerregistrierung als zentrale Registrierung verwendet werden, die mehreren Regionen regionale Multimasterregistrierungen zur Verfügung stellt.</span><span class="sxs-lookup"><span data-stu-id="d652a-102">Geo-replication enables an Azure container registry to function as a single registry, serving multiple regions with multi-master regional registries.</span></span>

<span data-ttu-id="d652a-103">Eine Registrierung mit Georeplikation bietet folgende Vorteile:</span><span class="sxs-lookup"><span data-stu-id="d652a-103">A geo-replicated registry provides the following benefits:</span></span>

* <span data-ttu-id="d652a-104">einzelner Registrierungs-/Image-/Tagname in mehreren Regionen verwendbar</span><span class="sxs-lookup"><span data-stu-id="d652a-104">Single registry/image/tag names can be used across multiple regions</span></span>
* <span data-ttu-id="d652a-105">netzwerknaher Registrierungszugriff über regionale Bereitstellungen</span><span class="sxs-lookup"><span data-stu-id="d652a-105">Network-close registry access from regional deployments</span></span>
* <span data-ttu-id="d652a-106">keine zusätzlichen Ausgangsgebühren, da Images aus einer lokalen, replizierten Registrierung in derselben Region wie Ihr Containerhost mithilfe von Pull übertragen werden</span><span class="sxs-lookup"><span data-stu-id="d652a-106">No additional egress fees because images are pulled from a local, replicated registry in the same region as your container host</span></span>
* <span data-ttu-id="d652a-107">zentrale Verwaltung einer Registrierung für mehrere Regionen</span><span class="sxs-lookup"><span data-stu-id="d652a-107">Single management of a registry across multiple regions</span></span>

## <a name="replicate-image-to-multiple-locations"></a><span data-ttu-id="d652a-108">Replizieren eines Images für mehrere Standorte</span><span class="sxs-lookup"><span data-stu-id="d652a-108">Replicate image to multiple locations</span></span>

<span data-ttu-id="d652a-109">Verwenden Sie den `az acr replication create`-Befehl, um Ihre Containerimages für eine andere Region zu replizieren.</span><span class="sxs-lookup"><span data-stu-id="d652a-109">Use the `az acr replication create` command to replicate your container images to another region.</span></span> <span data-ttu-id="d652a-110">In diesem Beispiel wird eine Replikation für die Region `japaneast` erstellt.</span><span class="sxs-lookup"><span data-stu-id="d652a-110">In this example, a replication is created for the `japaneast` region.</span></span> <span data-ttu-id="d652a-111">Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="d652a-111">Update `<acrName>` with the name of your container registry.</span></span>

```azurecli
az acr replication create --registry <acrName> --location japaneast
```

<span data-ttu-id="d652a-112">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="d652a-112">The output should look similar to the following:</span></span>

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

<span data-ttu-id="d652a-113">Verwenden Sie den Befehl `az acr replication list`, um sich eine Liste mit allen Replikaten des Containerimages anzeigen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="d652a-113">To see a list of all container image replicas, use the `az acr replication list` command.</span></span> <span data-ttu-id="d652a-114">Ersetzen Sie `<acrName>` durch den Namen Ihrer Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="d652a-114">Update `<acrName>` with the name of your container registry.</span></span>

```azurecli
az acr replication list --registry <acrName> --output table
```

<span data-ttu-id="d652a-115">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="d652a-115">The output should look similar to the following:</span></span>

```console
NAME       LOCATION    PROVISIONING STATE    STATUS
---------  ----------  --------------------  --------
japaneast  japaneast   Succeeded             Ready
eastus     eastus      Succeeded             Ready
```

<span data-ttu-id="d652a-116">Obwohl das Azure-Portal in dieser Übung nicht genutzt wurde, bietet es sich an, dessen Benutzeroberfläche aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="d652a-116">While the Azure portal was not used in this exercise, it is neat to see the portal experience.</span></span>

<span data-ttu-id="d652a-117">Wenn Sie im Azure-Portal `Replications` für eine Azure-Containerregistrierung auswählen, wird eine Karte mit den aktuellen Replikationen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d652a-117">From within the Azure portal, selecting `Replications` for an Azure container registry displays a map that details current replications.</span></span> <span data-ttu-id="d652a-118">Containerimages können für zusätzliche Regionen repliziert werden, indem letztere auf der Karte ausgewählt werden.</span><span class="sxs-lookup"><span data-stu-id="d652a-118">Container images can be replicated to additional regions by selecting the regions on the map.</span></span>

![Replikationskarte für Container im Azure-Portal](../media/replication-map.png)

## <a name="clean-up"></a><span data-ttu-id="d652a-120">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="d652a-120">Clean up</span></span>

<span data-ttu-id="d652a-121">Dies ist die letzte Einheit des Azure Container Registry-Lernmoduls.</span><span class="sxs-lookup"><span data-stu-id="d652a-121">This is the last unit of the Azure Container Registry learning module.</span></span> <span data-ttu-id="d652a-122">Sie können nun die erstellten Ressourcen bereinigen, indem Sie die Ressourcengruppe löschen.</span><span class="sxs-lookup"><span data-stu-id="d652a-122">At this point, you can clean up the created resources by deleting the resource group.</span></span> <span data-ttu-id="d652a-123">Verwenden Sie hierzu den `az group delete`-Befehl.</span><span class="sxs-lookup"><span data-stu-id="d652a-123">To do so, use the `az group delete` command.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a><span data-ttu-id="d652a-124">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="d652a-124">Summary</span></span>

<span data-ttu-id="d652a-125">In diesem Modul haben Sie ein Containerimage für mehrere Azure-Regionen mithilfe der Azure CLI repliziert.</span><span class="sxs-lookup"><span data-stu-id="d652a-125">In this module, you replicated a container image to multiple Azure regions using the Azure CLI.</span></span>