<span data-ttu-id="047e1-101">Unser Ziel ist, einen neuen virtuellen Azure-Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="047e1-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="047e1-102">Wir müssen mehrere Informationen angeben, um den Speicherort der Ressource, das zu verwendende Betriebssystem und die für die VM erforderliche Hardwarekonfiguration zu definieren.</span><span class="sxs-lookup"><span data-stu-id="047e1-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="047e1-103">Lassen Sie uns mit der **Ressourcengruppe** beginnen.</span><span class="sxs-lookup"><span data-stu-id="047e1-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="047e1-104">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="047e1-104">Create a resource group</span></span>

<span data-ttu-id="047e1-105">Azure verwendet _Ressourcengruppen_, um zusammengehörige Ressourcen wie virtuelle Computer und Datenbanken zu gruppieren.</span><span class="sxs-lookup"><span data-stu-id="047e1-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="047e1-106">Die Ressourcengruppe bestimmt auch einen Standort (als „Region“ bezeichnet), der entscheidet, in welchem Rechenzentrum die Ressource platziert wird.</span><span class="sxs-lookup"><span data-stu-id="047e1-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

<span data-ttu-id="047e1-107">Da wir experimentieren, starten Sie mit dem Erstellen einer neuen Ressourcengruppe namens `ExerciseResources`, die Sie in der Region `eastus` platzieren.</span><span class="sxs-lookup"><span data-stu-id="047e1-107">Since we're experimenting, start by creating a new resource group named `ExerciseResources` and place it into the `eastus` region.</span></span>

<!-- TODO: replace with free ed-tier -->

<span data-ttu-id="047e1-108">Geben Sie in Azure Cloud Shell den folgenden Azure CLI-Befehl ein, um die Ressourcengruppe in Ihrem Abonnement zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="047e1-108">Type the following Azure CLI command in Azure Cloud Shell to create the resource group in your subscription.</span></span>

```azurecli
az group create --name ExerciseResources --location eastus
```

<span data-ttu-id="047e1-109">Ein JSON-Block wird zurückgegeben, der angibt, dass die Ressourcengruppe erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="047e1-109">This will return a JSON block indicating the resource group has been created.</span></span> <span data-ttu-id="047e1-110">Dieser sollte ungefähr wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="047e1-110">It should look something like:</span></span>

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources",
  "location": "eastus",
  "managedBy": null,
  "name": "ExerciseResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="047e1-111">Beachten Sie, dass der eindeutige Bezeichner, Standort und Name des Abonnements als Teil der Antwort zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="047e1-111">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="047e1-112">Sie können diese Informationen verwenden, um zu überprüfen, ob sie im richtigen Abonnement und am richtigen Standort erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="047e1-112">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="047e1-113">Nachdem wir nun über eine Ressourcengruppe verfügen, lassen Sie uns einen neuen virtuellen Computer erstellen.</span><span class="sxs-lookup"><span data-stu-id="047e1-113">Now that we have a resource group, let's create a new virtual machine.</span></span>