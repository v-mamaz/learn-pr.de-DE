<span data-ttu-id="08350-101">In dieser Einheit erstellen Sie eine Azure Container Registry-Instanz über die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="08350-101">In this unit, you will create an Azure container registry using the Azure CLI.</span></span>

## <a name="create-an-azure-container-registry"></a><span data-ttu-id="08350-102">Erstellen einer Azure-Containerregistrierung</span><span class="sxs-lookup"><span data-stu-id="08350-102">Create an Azure container registry</span></span>

<span data-ttu-id="08350-103">Zum Erstellen einer Azure Container Registry-Instanz benötigen Sie eine *Ressourcengruppe*, in der die Instanz bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="08350-103">Before you create your Azure container registry, you need a *resource group* to deploy it to.</span></span> <span data-ttu-id="08350-104">Eine Azure-Ressourcengruppe ist eine logische Sammlung, in der alle Azure-Ressourcen bereitgestellt und verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="08350-104">A resource group is a logical collection into which all Azure resources are deployed and managed.</span></span>

<span data-ttu-id="08350-105">Erstellen Sie mit dem Befehl `az group create` eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="08350-105">Create a resource group with the `az group create` command.</span></span> <span data-ttu-id="08350-106">Im folgenden Beispiel wird eine Ressourcengruppe mit dem Namen *myResourceGroup* in der Region *eastus* erstellt:</span><span class="sxs-lookup"><span data-stu-id="08350-106">In the following example, a resource group named *myResourceGroup* is created in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="08350-107">Erstellen Sie nach der Erstellung der Ressourcengruppe mit dem Befehl `az acr create` eine Azure-Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="08350-107">Once you've created the resource group, create an Azure container registry with the `az acr create` command.</span></span> <span data-ttu-id="08350-108">Der Containerregistrierungsname muss innerhalb von Azure eindeutig sein und 5 bis 50 alphanumerische Zeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="08350-108">The container registry name must be unique within Azure, and contain between 5 and 50 alphanumeric characters.</span></span> <span data-ttu-id="08350-109">Ersetzen Sie `<acrName>` durch einen eindeutigen Namen für die Registrierung.</span><span class="sxs-lookup"><span data-stu-id="08350-109">Replace `<acrName>` with a unique name for your registry.</span></span>

<span data-ttu-id="08350-110">In diesem Beispiel wird eine Premium-Registrierungs-SKU bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="08350-110">For this example, a premium registry SKU is deployed.</span></span> <span data-ttu-id="08350-111">Die Premium-SKU ist für die Georeplikation erforderlich.</span><span class="sxs-lookup"><span data-stu-id="08350-111">The premium SKU is required for geo-replication.</span></span> <span data-ttu-id="08350-112">Weitere Informationen zu Container Registry-SKUs finden Sie unter [Azure Container Registry-SKUs](https://docs.microsoft.com/azure/container-registry/container-registry-skus).</span><span class="sxs-lookup"><span data-stu-id="08350-112">For more information on Container Registry SKUs, see, [Azure Container Registry SKUs](https://docs.microsoft.com/azure/container-registry/container-registry-skus)</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Premium
```

<span data-ttu-id="08350-113">Im Folgenden sehen Sie eine Beispielausgabe für eine neue Azure-Containerregistrierung:</span><span class="sxs-lookup"><span data-stu-id="08350-113">Here's example output for a new Azure container registry:</span></span>

```console
{
  "adminUserEnabled": false,
  "creationDate": "2018-08-15T19:19:07.042178+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myACR0007",
  "location": "eastus",
  "loginServer": "myacr.azurecr.io",
  "name": "myACR",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Premium",
    "tier": "Premium"
  },
  "status": null,
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="08350-114">Im verbleibenden Teil dieses Moduls wird `<acrName>` als Platzhalter für den Namen der Containerregistrierung verwendet, den Sie in diesem Schritt angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="08350-114">The rest of this module refers to `<acrName>` as a placeholder for the container registry name that you chose in this step.</span></span>

## <a name="summary"></a><span data-ttu-id="08350-115">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="08350-115">Summary</span></span>

<span data-ttu-id="08350-116">In dieser Einheit haben Sie eine Azure Container Registry-Instanz über die Azure CLI erstellt.</span><span class="sxs-lookup"><span data-stu-id="08350-116">In this unit, you created an Azure container registry using the Azure CLI.</span></span>