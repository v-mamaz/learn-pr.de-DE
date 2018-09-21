<span data-ttu-id="524d1-101">In dieser Einheit erstellen Sie eine Azure Container Registry-Instanz über die Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="524d1-101">In this unit, you will create an Azure container registry using the Azure CLI.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]
 
## <a name="create-an-azure-container-registry"></a><span data-ttu-id="524d1-102">Erstellen einer Azure-Containerregistrierung</span><span class="sxs-lookup"><span data-stu-id="524d1-102">Create an Azure container registry</span></span>

<span data-ttu-id="524d1-103">Wir arbeiten in einer kostenlosen Sandbox, sodass Sie keine eigene Ressourcengruppe erstellen müssen.</span><span class="sxs-lookup"><span data-stu-id="524d1-103">We'll be working in a free Sandbox, so there's no need to create your own Resource Group.</span></span> <span data-ttu-id="524d1-104">Führen Sie den Befehl `az acr create` aus, um eine Azure-Containerregistrierung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="524d1-104">Create an Azure container registry with the `az acr create` command.</span></span> <span data-ttu-id="524d1-105">Der Name der Containerregistrierung muss innerhalb von Azure eindeutig sein und 5 bis 50 alphanumerische Zeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="524d1-105">The container registry name must be unique within Azure and contain between 5 and 50 alphanumeric characters.</span></span> <span data-ttu-id="524d1-106">Ersetzen Sie `<acrName>` durch einen eindeutigen Namen für die Registrierung.</span><span class="sxs-lookup"><span data-stu-id="524d1-106">Replace `<acrName>` with a unique name for your registry.</span></span>

<span data-ttu-id="524d1-107">In diesem Beispiel wird eine Premium-Registrierungs-SKU bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="524d1-107">In this example, a premium registry SKU is deployed.</span></span> <span data-ttu-id="524d1-108">Die Premium-SKU ist für die Georeplikation erforderlich.</span><span class="sxs-lookup"><span data-stu-id="524d1-108">The premium SKU is required for geo-replication.</span></span> <span data-ttu-id="524d1-109">Geben Sie den folgenden Befehl in den Cloud Shell-Editor ein.</span><span class="sxs-lookup"><span data-stu-id="524d1-109">Enter the following command into the cloud shell editor.</span></span>

```azurecli
az acr create --resource-group <rgn>[Sandbox resource group name]</rgn> --name <acrName> --sku Premium
```

<span data-ttu-id="524d1-110">Im Folgenden sehen Sie eine Beispielausgabe für eine neue Azure-Containerregistrierung:</span><span class="sxs-lookup"><span data-stu-id="524d1-110">Here's an example output for a new Azure container registry:</span></span>

```output
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

<span data-ttu-id="524d1-111">Im verbleibenden Teil dieses Moduls wird `<acrName>` als Platzhalter für den Namen der Containerregistrierung verwendet, den Sie in diesem Schritt angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="524d1-111">The rest of this module refers to `<acrName>` as a placeholder for the container registry name that you chose in this step.</span></span>

<span data-ttu-id="524d1-112">In dieser Einheit haben Sie eine Azure Container Registry-Instanz über die Azure CLI erstellt.</span><span class="sxs-lookup"><span data-stu-id="524d1-112">In this unit, you created an Azure container registry using the Azure CLI.</span></span>