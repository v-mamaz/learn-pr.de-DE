<span data-ttu-id="e6b74-101">Während des Buildprozesses erstellt Packer temporäre Azure-Ressourcen, für die Basis-VM.</span><span class="sxs-lookup"><span data-stu-id="e6b74-101">During the build process, Packer creates temporary Azure resources for the base VM.</span></span> <span data-ttu-id="e6b74-102">Wenn diese Basis-VM für die Verwendung als Image erfassen möchten, müssen Sie eine Ressourcengruppe definieren.</span><span class="sxs-lookup"><span data-stu-id="e6b74-102">To capture that base VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="e6b74-103">Eine Azure-Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen bereitgestellt und verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="e6b74-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="e6b74-104">Erstellen Sie zuerst eine Ressourcengruppe in Azure Cloud Shell mit [az-Gruppe erstellen](/cli/azure/group#az_group_create).</span><span class="sxs-lookup"><span data-stu-id="e6b74-104">First, create a resource group in the Azure Cloud Shell with [az group create](/cli/azure/group#az_group_create).</span></span> <span data-ttu-id="e6b74-105">Im folgenden Beispiel wird eine Ressourcengruppe mit dem Namen *myResourceGroup* am Standort *eastus* erstellt:</span><span class="sxs-lookup"><span data-stu-id="e6b74-105">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```

<span data-ttu-id="e6b74-106">Packer authentifiziert sich bei Azure mithilfe eines Dienstprinzipals.</span><span class="sxs-lookup"><span data-stu-id="e6b74-106">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="e6b74-107">Ein Azure-Dienstprinzipal ist eine Sicherheitsidentität, die Sie mit Apps, Diensten und Automatisierungstools wie Packer verwenden können.</span><span class="sxs-lookup"><span data-stu-id="e6b74-107">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="e6b74-108">Sie steuern und definieren die Berechtigungen hinsichtlich der Vorgänge, die der Dienstprinzipal in Azure ausführen können soll.</span><span class="sxs-lookup"><span data-stu-id="e6b74-108">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="e6b74-109">Erstellen eines dienstprinzipals in Azure Cloud Shell mit [az Ad sp create-for-Rbac](/cli/azure/ad/sp#create-for-rbac) und geben Sie die Anmeldeinformationen, die Packer benötigt:</span><span class="sxs-lookup"><span data-stu-id="e6b74-109">Create a service principal in the Azure Cloud Shell with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query "{ client_id: appId, client_secret: password, tenant_id: tenant }"
```

<span data-ttu-id="e6b74-110">Ein Beispiel der Ausgabe der vorherigen Befehle lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="e6b74-110">An example of the output from the preceding commands is as follows:</span></span>

```azurecli
{
    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
}
```

<span data-ttu-id="e6b74-111">Kopieren Sie Ihre eigenen Ausgabe für die Verwendung im nächsten Schritt ein.</span><span class="sxs-lookup"><span data-stu-id="e6b74-111">Copy your own output for use in the next step.</span></span>

<span data-ttu-id="e6b74-112">Zur Authentifizierung bei Azure müssen Sie auch Ihre Azure-Abonnement-ID mit [az account show](/cli/azure/account#az_account_show) abrufen:</span><span class="sxs-lookup"><span data-stu-id="e6b74-112">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#az_account_show):</span></span>

```azurecli
az account show --query '{ "subscription_id": "id" }'
```

<span data-ttu-id="e6b74-113">Die Ausgabe dieser beiden Befehle verwenden Sie im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="e6b74-113">You use the output from these two commands in the next step.</span></span>