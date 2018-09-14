<span data-ttu-id="93c59-101">Die Azure CLI enthält den Befehl „`vm`“ für die Arbeit mit virtuellen Computern in Azure.</span><span class="sxs-lookup"><span data-stu-id="93c59-101">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="93c59-102">Wir können verschiedene Unterbefehle bereitstellen, um bestimmte Aufgaben auszuführen.</span><span class="sxs-lookup"><span data-stu-id="93c59-102">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="93c59-103">Dies sind die am häufigsten verwendeten:</span><span class="sxs-lookup"><span data-stu-id="93c59-103">The most common include:</span></span>

| <span data-ttu-id="93c59-104">Unterbefehl</span><span class="sxs-lookup"><span data-stu-id="93c59-104">Sub-command</span></span> | <span data-ttu-id="93c59-105">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93c59-105">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="93c59-106">Erstellen eines neuen virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="93c59-106">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="93c59-107">Aufheben der Zuordnung eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="93c59-107">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="93c59-108">Löschen eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="93c59-108">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="93c59-109">Auflisten der erstellten virtuellen Computer in Ihrem Abonnement</span><span class="sxs-lookup"><span data-stu-id="93c59-109">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="93c59-110">Öffnen eines bestimmten Netzwerkports für eingehenden Datenverkehr</span><span class="sxs-lookup"><span data-stu-id="93c59-110">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="93c59-111">Neustarten eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="93c59-111">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="93c59-112">Abrufen der Details für einen virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="93c59-112">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="93c59-113">Starten eines angehaltenen virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="93c59-113">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="93c59-114">Anhalten eines ausgeführten virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="93c59-114">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="93c59-115">Aktualisieren der Eigenschaft eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="93c59-115">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="93c59-116">Eine vollständige Liste der Befehle finden Sie in der [Dokumentation der Azure CLI-Referenz](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="93c59-116">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="93c59-117">Beginnen wir mit dem ersten: `az vm create`.</span><span class="sxs-lookup"><span data-stu-id="93c59-117">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="93c59-118">Mit diesem Befehl wird ein virtueller Computer in einer Ressourcengruppe erstellt.</span><span class="sxs-lookup"><span data-stu-id="93c59-118">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="93c59-119">Es gibt verschiedene Parameter, die Sie übergeben können, um alle Aspekte des neuen virtuellen Computers zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="93c59-119">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="93c59-120">Diese drei Parameter müssen angegeben werden:</span><span class="sxs-lookup"><span data-stu-id="93c59-120">The three parameters that must be supplied are:</span></span>

| <span data-ttu-id="93c59-121">Parameter</span><span class="sxs-lookup"><span data-stu-id="93c59-121">Parameter</span></span> | <span data-ttu-id="93c59-122">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="93c59-122">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="93c59-123">Die Ressourcengruppe, die Besitzer des virtuellen Computers sein soll.</span><span class="sxs-lookup"><span data-stu-id="93c59-123">The resource group that will own the virtual machine</span></span> |
| `name` | <span data-ttu-id="93c59-124">Der Name des virtuellen Computers – muss innerhalb der Ressourcengruppe eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="93c59-124">The name of the virtual machine - must be unique within the resource group</span></span> |
| `image` | <span data-ttu-id="93c59-125">Das Betriebssystemimage, das zum Erstellen des virtuellen Computers verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="93c59-125">The operating system image to use to create the VM</span></span> |

<span data-ttu-id="93c59-126">Darüber hinaus ist es hilfreich, das `--verbose`-Flag hinzuzufügen, um den Fortschritt der Erstellung des virtuellen Computers zu beobachten.</span><span class="sxs-lookup"><span data-stu-id="93c59-126">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="93c59-127">Erstellen eines virtuellen Linux-Computers</span><span class="sxs-lookup"><span data-stu-id="93c59-127">Create a Linux virtual machine</span></span>

<span data-ttu-id="93c59-128">Erstellen wir jetzt einen neuen virtuellen Linux-Computer.</span><span class="sxs-lookup"><span data-stu-id="93c59-128">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="93c59-129">Führen Sie in Azure Cloud Shell folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="93c59-129">Execute the following command in Azure Cloud Shell:</span></span>

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

<span data-ttu-id="93c59-130">Dieser Befehl erstellt einen neuen virtuellen Linux-Computer unter **Debian** mit dem Namen „`SampleVM`“.</span><span class="sxs-lookup"><span data-stu-id="93c59-130">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="93c59-131">Beachten Sie, dass das Azure CLI-Tool während der Erstellung des virtuellen Computers gesperrt ist.</span><span class="sxs-lookup"><span data-stu-id="93c59-131">Notice that the Azure CLI tool is blocked while the VM is being created.</span></span> <span data-ttu-id="93c59-132">Wenn Sie nicht warten möchten, können Sie die Option „`--no-wait`“ verwenden, damit das Azure CLI-Tool sofort wieder verfügbar ist, wenn Sie den Befehl beispielsweise in einem Skript ausführen.</span><span class="sxs-lookup"><span data-stu-id="93c59-132">If you would prefer not to wait, you can use the `--no-wait` option to tell the Azure CLI tool to return immediately, for example if you're executing the command in a script.</span></span> <span data-ttu-id="93c59-133">Verwenden Sie später im Skript den Befehl „`azure vm wait --name [vm-name]`“, um zu warten, bis der virtuelle Computer vollständig erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="93c59-133">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="93c59-134">Wenn Sie sich die ausführlichen Antworten ansehen, werden Sie auch feststellen, dass der Name „`SampleVM`“ in verschiedenen Abhängigkeiten für den virtuellen Computer verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="93c59-134">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="93c59-135">Sie können diese automatisch generierten Ressourcennamen mithilfe von optionalen Parametern für „`vm create`“ überschreiben, z.B.: `--vnet-name` und `--public-ip-address-dns-name`.</span><span class="sxs-lookup"><span data-stu-id="93c59-135">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="93c59-136">Beachten Sie, dass wir den Namen des Administratorkontos mit dem `admin-username`-Flag zu „aldis“ ändern.</span><span class="sxs-lookup"><span data-stu-id="93c59-136">Notice that we are specifying the admin account name through the `admin-username` flag to be "aldis".</span></span> <span data-ttu-id="93c59-137">Wenn Sie dies auslassen, verwendet der `vm create`-Befehl Ihren _aktuellen Benutzernamen_.</span><span class="sxs-lookup"><span data-stu-id="93c59-137">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="93c59-138">Da die Regeln für Kontonamen in jedem Betriebssystem anders sind, ist es sicherer, einen bestimmten Namen anzugeben.</span><span class="sxs-lookup"><span data-stu-id="93c59-138">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> <span data-ttu-id="93c59-139">Allgemeine Namen wie „root“ und „admin“ sind für die meisten Images nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="93c59-139">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="93c59-140">Wir verwenden auch das `generate-ssh-keys`-Flag.</span><span class="sxs-lookup"><span data-stu-id="93c59-140">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="93c59-141">Dieser Parameter wird für Linux-Distributionen verwendet und erstellt ein Sicherheitsschlüsselpaar, sodass wir das `ssh`-Tool verwenden können, um remote auf den virtuellen Computer zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="93c59-141">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="93c59-142">Die beiden Dateien werden in den Ordner „`.ssh`“ auf Ihrem Computer und auf dem virtuellen Computer platziert.</span><span class="sxs-lookup"><span data-stu-id="93c59-142">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="93c59-143">Wenn Sie bereits über einen SSH-Schlüssel namens „`id_rsa`“ im Zielordner verfügen, wird dieser verwendet, anstatt einen neuen Schlüssel zu generieren.</span><span class="sxs-lookup"><span data-stu-id="93c59-143">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="93c59-144">Sobald der virtuelle Computer erstellt wurde, erhalten Sie eine JSON-Antwort, die den aktuellen Zustand des virtuellen Computers und seine von Azure zugewiesenen öffentlichen und privaten IP-Adressen enthält:</span><span class="sxs-lookup"><span data-stu-id="93c59-144">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

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

> [!NOTE]
> <span data-ttu-id="93c59-145">Beachten Sie, dass der virtuelle Computer am Speicherort **eastus** erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="93c59-145">Notice that the VM was created in the **eastus** location.</span></span> <span data-ttu-id="93c59-146">Standardmäßig wird der virtuelle Computer am von der besitzenden Region identifizierten Speicherort erstellt.</span><span class="sxs-lookup"><span data-stu-id="93c59-146">By default, the virtual machine is created in the location identified by the owning region.</span></span> <span data-ttu-id="93c59-147">Wenn Sie den virtuellen Computer einer vorhandenen Region zuordnen möchten, kann es allerdings vorkommen, dass dieser einer beliebigen Region irgendwo anders zugeordnet wird.</span><span class="sxs-lookup"><span data-stu-id="93c59-147">However, sometimes you might want to associate the VM with an existing region, but actually have it spin up somewhere else in the world.</span></span> <span data-ttu-id="93c59-148">Dies ist möglich, indem Sie den `--location`-Parameter als Teil des `az vm create`-Befehls angeben.</span><span class="sxs-lookup"><span data-stu-id="93c59-148">You can do this by specifying the option `--location` parameter as part of the `az vm create` command.</span></span>