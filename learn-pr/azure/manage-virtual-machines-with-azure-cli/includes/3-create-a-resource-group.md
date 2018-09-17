<span data-ttu-id="bd307-101">Unser Ziel ist, einen neuen virtuellen Azure-Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="bd307-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="bd307-102">Wir müssen mehrere Informationen angeben, um den Speicherort der Ressource, das zu verwendende Betriebssystem und die für die VM erforderliche Hardwarekonfiguration zu definieren.</span><span class="sxs-lookup"><span data-stu-id="bd307-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="bd307-103">Lassen Sie uns mit der **Ressourcengruppe** beginnen.</span><span class="sxs-lookup"><span data-stu-id="bd307-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="bd307-104">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="bd307-104">Create a resource group</span></span>

<span data-ttu-id="bd307-105">Azure verwendet _Ressourcengruppen_, um zusammengehörige Ressourcen wie virtuelle Computer und Datenbanken zu gruppieren.</span><span class="sxs-lookup"><span data-stu-id="bd307-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="bd307-106">Die Ressourcengruppe bestimmt auch einen Standort (als „Region“ bezeichnet), der entscheidet, in welchem Rechenzentrum die Ressource platziert wird.</span><span class="sxs-lookup"><span data-stu-id="bd307-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

> [!NOTE]
> <span data-ttu-id="bd307-107">Die Azure-Sandbox stellt eine vorab erstellte Ressourcengruppe mit dem Namen <rgn>[Sandbox resource group name]</rgn> (Sandbox Ressourcengruppenname) bereit.</span><span class="sxs-lookup"><span data-stu-id="bd307-107">The Azure sandbox provides a pre-created resource group named <rgn>[Sandbox resource group name]</rgn>.</span></span> <span data-ttu-id="bd307-108">Die Ausführung der folgenden Schritte ist optional.</span><span class="sxs-lookup"><span data-stu-id="bd307-108">You do not need to execute these steps.</span></span> <span data-ttu-id="bd307-109">Wenn Sie allerdings Ihre _eigenen_ Ressourcen für echte Projekte erstellen, werden Sie die aufgeführten Befehle nutzen müssen.</span><span class="sxs-lookup"><span data-stu-id="bd307-109">However, when you are creating your _own_ resources for real projects, these will be the commands you will need to perform.</span></span> <span data-ttu-id="bd307-110">Sie können mit der Azure-Sandbox Ressourcengruppen nicht direkt erstellen.</span><span class="sxs-lookup"><span data-stu-id="bd307-110">The Azure sandbox does not allow you to create resource groups directly.</span></span>

<span data-ttu-id="bd307-111">Geben Sie in Azure Cloud Shell beispielsweise den folgenden Azure CLI-Befehl ein, um eine Ressourcengruppe in der Region **USA, Osten** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="bd307-111">As an example, you could type the following Azure CLI command in Azure Cloud Shell to create a resource group in the **East US** region.</span></span> <span data-ttu-id="bd307-112">**[resource-group]** ersetzen Sie durch einen gültigen Namen, der im aktiven Abonnement eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="bd307-112">You would replace **[resource-group]** with a valid name that is unique within the active subscription.</span></span>

```azurecli
az group create --name [resource-group] --location eastus
```

<span data-ttu-id="bd307-113">Dadurch wird ein JSON-Block zurückgegeben, der angibt, dass die Ressourcengruppe erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="bd307-113">This would return a JSON block indicating the resource group has been created.</span></span>

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/<resourcegroup>",
  "location": "eastus",
  "managedBy": null,
  "name": "<resourcegroup>",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="bd307-114">Beachten Sie, dass der eindeutige Bezeichner, Standort und Name des Abonnements als Teil der Antwort zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="bd307-114">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="bd307-115">Sie können diese Informationen verwenden, um zu überprüfen, ob die Ressourcengruppe im richtigen Abonnement und am richtigen Standort erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="bd307-115">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="bd307-116">Da wir nun wissen, wie eine Ressourcengruppe erstellt wird, können wir einen neuen virtuellen Computer erstellen.</span><span class="sxs-lookup"><span data-stu-id="bd307-116">Now that we know how to create a resource group, let's create a new virtual machine.</span></span>