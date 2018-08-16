<span data-ttu-id="cf870-101">Unser Ziel ist die Erstellung einer neuen Azure-VM.</span><span class="sxs-lookup"><span data-stu-id="cf870-101">Our goal is to create a new Azure Virtual Machine.</span></span> <span data-ttu-id="cf870-102">Wir benötigen, geben Sie die verschiedenen informationsbestandteilen um den Speicherort der Ressource, Betriebssystem verwenden und die Hardwarekonfiguration, die erforderlich sind, für den virtuellen Computer zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="cf870-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="cf870-103">Beginnen wir mit der **Ressourcengruppe**.</span><span class="sxs-lookup"><span data-stu-id="cf870-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="cf870-104">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="cf870-104">Create a resource group</span></span>

<span data-ttu-id="cf870-105">Azure verwendet _Ressourcengruppen_ um zusammengehörige Ressourcen wie virtuelle Computer und Datenbanken zu gruppieren.</span><span class="sxs-lookup"><span data-stu-id="cf870-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="cf870-106">Die Ressourcengruppe identifiziert auch einen bestimmten Standort (eine "Region" bezeichnet), der entscheiden, welche Datencenter wird in die Ressource platziert wird.</span><span class="sxs-lookup"><span data-stu-id="cf870-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

<span data-ttu-id="cf870-107">Da wir experimentieren können, starten Sie durch das Erstellen einer neuen Ressourcengruppe mit dem Namen `ExerciseResources` und platzieren Sie sie in der `eastus` Region.</span><span class="sxs-lookup"><span data-stu-id="cf870-107">Since we're experimenting, start by creating a new resource group named `ExerciseResources` and place it into the `eastus` region.</span></span>

> [!NOTE]
> <span data-ttu-id="cf870-108">Achten Sie darauf, die exakt diesem Namen für die neue Ressourcengruppe zu verwenden, das Microsoft-Learn-System wird, und sehen uns für diese Ressourcennamen später noch mal.</span><span class="sxs-lookup"><span data-stu-id="cf870-108">Make sure to use this exact name for your new resource group, the Microsoft Learn system will be looking for this resource name later.</span></span> 

<span data-ttu-id="cf870-109">Geben Sie den folgenden Azure CLI-Befehl in der Cloud Shell, um die Ressourcengruppe in Ihrem Abonnement zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cf870-109">Type the following Azure CLI command in the Cloud Shell to create the resource group in your subscription.</span></span>

```azurecli
az group create --name ExerciseResources --location eastus
```

<span data-ttu-id="cf870-110">Dadurch wird zurückgegeben, eine JSON-Block, der angibt, ob die Ressourcengruppe erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="cf870-110">This will return a JSON block indicating the resource group has been created.</span></span> <span data-ttu-id="cf870-111">Es sollte etwa so aussehen:</span><span class="sxs-lookup"><span data-stu-id="cf870-111">It should look something like:</span></span>

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

<span data-ttu-id="cf870-112">Beachten Sie, dass die eindeutige Abonnement-ID, den Speicherort und Namen als Teil der Antwort zurückgegeben: Sie können diese verwenden, um sicherzustellen, dass es in die richtige Abonnement und den Standort erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="cf870-112">Notice that it returns the subscription unique identifier, location, and name as part of the response - you can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="cf870-113">Nun, da wir eine Ressourcengruppe erstellt haben, erstellen wir einen neuen virtuellen Computer an.</span><span class="sxs-lookup"><span data-stu-id="cf870-113">Now that we have a resource group, let's create a new virtual machine.</span></span>