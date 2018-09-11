<span data-ttu-id="77f68-101">Unser Ziel ist, einen neuen virtuellen Azure-Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="77f68-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="77f68-102">Wir müssen mehrere Informationen angeben, um den Speicherort der Ressource, das zu verwendende Betriebssystem und die für die VM erforderliche Hardwarekonfiguration zu definieren.</span><span class="sxs-lookup"><span data-stu-id="77f68-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="77f68-103">Lassen Sie uns mit der **Ressourcengruppe** beginnen.</span><span class="sxs-lookup"><span data-stu-id="77f68-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="77f68-104">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="77f68-104">Create a resource group</span></span>

<span data-ttu-id="77f68-105">Azure verwendet _Ressourcengruppen_, um zusammengehörige Ressourcen wie virtuelle Computer und Datenbanken zu gruppieren.</span><span class="sxs-lookup"><span data-stu-id="77f68-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="77f68-106">Die Ressourcengruppe bestimmt auch einen Standort (als „Region“ bezeichnet), der entscheidet, in welchem Rechenzentrum die Ressource platziert wird.</span><span class="sxs-lookup"><span data-stu-id="77f68-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

<span data-ttu-id="77f68-107">Da wir experimentieren, starten Sie mit dem Erstellen einer neuen Ressourcengruppe namens `ExerciseResources`, die Sie in der Region `eastus` platzieren.</span><span class="sxs-lookup"><span data-stu-id="77f68-107">Since we're experimenting, start by creating a new resource group named `ExerciseResources` and place it into the `eastus` region.</span></span>

> [!NOTE]
> <span data-ttu-id="77f68-108">Vergewissern Sie sich, dass Sie genau diesen Namen für Ihre neue Ressourcengruppe verwenden, da das Microsoft-Lernsystem später diesen Ressourcennamen suchen wird.</span><span class="sxs-lookup"><span data-stu-id="77f68-108">Make sure to use this exact name for your new resource group, because the Microsoft Learn system will be looking for this resource name later.</span></span> 

<span data-ttu-id="77f68-109">Geben Sie in Azure Cloud Shell den folgenden Azure CLI-Befehl ein, um die Ressourcengruppe in Ihrem Abonnement zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="77f68-109">Type the following Azure CLI command in Azure Cloud Shell to create the resource group in your subscription.</span></span>

```azurecli
az group create --name ExerciseResources --location eastus
```

<span data-ttu-id="77f68-110">Ein JSON-Block wird zurückgegeben, der angibt, dass die Ressourcengruppe erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="77f68-110">This will return a JSON block indicating the resource group has been created.</span></span> <span data-ttu-id="77f68-111">Dieser sollte ungefähr wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="77f68-111">It should look something like:</span></span>

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

<span data-ttu-id="77f68-112">Beachten Sie, dass der eindeutige Bezeichner, Standort und Name des Abonnements als Teil der Antwort zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="77f68-112">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="77f68-113">Sie können diese Informationen verwenden, um zu überprüfen, ob sie im richtigen Abonnement und am richtigen Standort erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="77f68-113">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="77f68-114">Nachdem wir nun über eine Ressourcengruppe verfügen, lassen Sie uns einen neuen virtuellen Computer erstellen.</span><span class="sxs-lookup"><span data-stu-id="77f68-114">Now that we have a resource group, let's create a new virtual machine.</span></span>