<span data-ttu-id="4f24d-101">Die Azure CLI enthält die `vm` Befehl aus, um die Arbeit mit virtuellen Computern in Azure.</span><span class="sxs-lookup"><span data-stu-id="4f24d-101">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="4f24d-102">Wir können mehrere Unterbefehle spezifischer Aufgaben angeben, die am häufigsten verwendeten gehören:</span><span class="sxs-lookup"><span data-stu-id="4f24d-102">We can supply several subcommands to do specific tasks, the most common include:</span></span>

| <span data-ttu-id="4f24d-103">Unterbefehl</span><span class="sxs-lookup"><span data-stu-id="4f24d-103">Sub-Command</span></span> | <span data-ttu-id="4f24d-104">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4f24d-104">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="4f24d-105">Erstellen eines neuen virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="4f24d-105">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="4f24d-106">Aufheben der Zuordnung eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="4f24d-106">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="4f24d-107">Löschen eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="4f24d-107">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="4f24d-108">Auflisten der erstellten virtuellen Computer in Ihrem Abonnement</span><span class="sxs-lookup"><span data-stu-id="4f24d-108">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="4f24d-109">Öffnen Sie einen bestimmten Netzwerkport für eingehenden Datenverkehr</span><span class="sxs-lookup"><span data-stu-id="4f24d-109">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="4f24d-110">Neustarten eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="4f24d-110">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="4f24d-111">Rufen Sie die Details für einen virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="4f24d-111">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="4f24d-112">Starten eines beendeten virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="4f24d-112">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="4f24d-113">Beenden einer ausgeführten virtuellen Maschine</span><span class="sxs-lookup"><span data-stu-id="4f24d-113">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="4f24d-114">Aktualisieren Sie eine Eigenschaft eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="4f24d-114">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="4f24d-115">Eine vollständige Liste der Befehle, sehen Sie sich die [Referenzdokumentation für Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)</span><span class="sxs-lookup"><span data-stu-id="4f24d-115">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)</span></span>

<span data-ttu-id="4f24d-116">Beginnen wir mit der ersten Anweisung: `az vm create`.</span><span class="sxs-lookup"><span data-stu-id="4f24d-116">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="4f24d-117">Mit diesem Befehl wird verwendet, um einen virtuellen Computer in einer Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="4f24d-117">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="4f24d-118">Es gibt mehrere Parameter, die Sie übergeben können, um alle Aspekte von den neuen virtuellen Computer zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="4f24d-118">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="4f24d-119">Die drei Parameter, die angegeben werden müssen, sind:</span><span class="sxs-lookup"><span data-stu-id="4f24d-119">The three parameters that must be supplied are:</span></span>

| <span data-ttu-id="4f24d-120">Parameter</span><span class="sxs-lookup"><span data-stu-id="4f24d-120">Parameter</span></span> | <span data-ttu-id="4f24d-121">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4f24d-121">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="4f24d-122">Die Ressourcengruppe aus, die die virtuelle Maschine besitzt</span><span class="sxs-lookup"><span data-stu-id="4f24d-122">The resource group that will own the virtual machine</span></span> |
| `name` | <span data-ttu-id="4f24d-123">Der Name des virtuellen Computers – muss innerhalb der Ressourcengruppe eindeutig sein</span><span class="sxs-lookup"><span data-stu-id="4f24d-123">The name of the virtual machine - must be unique within the resource group</span></span> |
| `image` | <span data-ttu-id="4f24d-124">Das Betriebssystemabbild zu verwenden, um den virtuellen Computer erstellen</span><span class="sxs-lookup"><span data-stu-id="4f24d-124">The operating system image to use to create the VM</span></span> |

<span data-ttu-id="4f24d-125">Darüber hinaus ist es hilfreich sein, fügen die `--verbose` Flag Fortschritt verfolgen, während die VM erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="4f24d-125">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="4f24d-126">Erstellen einer virtuellen Linux-Maschine</span><span class="sxs-lookup"><span data-stu-id="4f24d-126">Create a Linux virtual machine</span></span>

<span data-ttu-id="4f24d-127">Wir erstellen einen neuen virtuellen Linux-Computer.</span><span class="sxs-lookup"><span data-stu-id="4f24d-127">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="4f24d-128">Führen Sie den folgenden Befehl in Cloud Shell ein:</span><span class="sxs-lookup"><span data-stu-id="4f24d-128">Execute the following command in the Cloud Shell:</span></span>

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

<span data-ttu-id="4f24d-129">Dieser Befehl erstellt ein neues **Debian** virtuellen Linux-Computer mit dem Namen `SampleVM`.</span><span class="sxs-lookup"><span data-stu-id="4f24d-129">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="4f24d-130">Beachten Sie, dass das CLI-Tool blockiert wird, während die VM erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="4f24d-130">Notice that the CLI tool is blocked while the VM is being created.</span></span> <span data-ttu-id="4f24d-131">Wenn Sie nicht warten möchten, können Sie mithilfe der `--no-wait` Option aus, um das Teilen der CLI-Tool sofort zurückkehren, z. B. Wenn Sie den Befehl in einem Skript ausführen.</span><span class="sxs-lookup"><span data-stu-id="4f24d-131">If you would prefer not to wait, you can use the `--no-wait` option to tell the CLI tool to return immediately, for example if you're executing the command in a script.</span></span> <span data-ttu-id="4f24d-132">Verwenden Sie später im Skript, das `azure vm wait --name [vm-name]` Befehl aus, um zu warten, bis der virtuelle Computer beendet, erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="4f24d-132">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="4f24d-133">Wenn Sie die ausführlichen Antworten betrachten, Sie werden auch angezeigt, die `SampleVM` Name wird verwendet, um verschiedene Abhängigkeiten für den virtuellen Computer zu benennen.</span><span class="sxs-lookup"><span data-stu-id="4f24d-133">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="4f24d-134">Sie können diese automatisch generierten Ressourcennamen mithilfe optionaler Parameter zum Überschreiben `vm create` wie z. B. `--vnet-name` und `--public-ip-address-dns-name`.</span><span class="sxs-lookup"><span data-stu-id="4f24d-134">You can override these auto-generated resource names using optional parameters to `vm create` such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="4f24d-135">Beachten Sie, dass wir den Namen des Admin-Konto durch Angeben der `admin-username` Flag "Aldis" sein.</span><span class="sxs-lookup"><span data-stu-id="4f24d-135">Notice that we are specifying the admin account name through the `admin-username` flag to be "aldis".</span></span> <span data-ttu-id="4f24d-136">Wenn Sie nicht angeben, die `vm create` -Befehl Ihrem _aktuellen Benutzernamen_.</span><span class="sxs-lookup"><span data-stu-id="4f24d-136">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="4f24d-137">Da die Regeln für den Kontonamen für jedes Betriebssystem unterschiedlich sind, ist es sicherer, die einen bestimmten Namen zu geben.</span><span class="sxs-lookup"><span data-stu-id="4f24d-137">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> <span data-ttu-id="4f24d-138">Allgemeine Namen, z. B. "Root" und "Admin" sind für die meisten Images nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="4f24d-138">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="4f24d-139">Wir verwenden zudem die `generate-ssh-keys` Flag.</span><span class="sxs-lookup"><span data-stu-id="4f24d-139">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="4f24d-140">Dieser Parameter wird für Linux-Distributionen verwendet und ein Paar von Sicherheitsschlüsseln erstellt, sodass wir nutzen können die `ssh` Tool, um den Remotezugriff auf den virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="4f24d-140">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="4f24d-141">Die beiden Dateien befinden sich in der `.ssh` Ordner auf Ihrem Computer und auf dem virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="4f24d-141">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="4f24d-142">Wenn Sie bereits über einen SSH-Schlüssel mit dem Namen verfügen `id_rsa` im Zielordner, dann wird dieser verwendet statt einen neuen Schlüssel generiert.</span><span class="sxs-lookup"><span data-stu-id="4f24d-142">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="4f24d-143">Nach der Erstellung des virtuellen Computers abgeschlossen wurde, erhalten Sie eine JSON-Antwort, die den aktuellen Status des virtuellen Computers enthält, und es die öffentlichen und privaten IP-Adressen, die von Azure zugewiesen ist:</span><span class="sxs-lookup"><span data-stu-id="4f24d-143">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and it's public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

