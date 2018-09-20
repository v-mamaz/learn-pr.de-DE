<span data-ttu-id="44bce-101">Wir beginnen mit der offensichtlichsten Aufgabe: der Erstellung eines virtuellen Azure-Computers.</span><span class="sxs-lookup"><span data-stu-id="44bce-101">Let's start with the most obvious task: creating an Azure Virtual Machine.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="logins-subscriptions-and-resource-groups"></a><span data-ttu-id="44bce-102">Anmeldungen, Abonnements und Ressourcengruppen</span><span class="sxs-lookup"><span data-stu-id="44bce-102">Logins, subscriptions, and resource groups</span></span>

<span data-ttu-id="44bce-103">Sie arbeiten in Azure Cloud Shell auf der rechten Seite.</span><span class="sxs-lookup"><span data-stu-id="44bce-103">You'll be working in the Azure Cloud Shell on the right.</span></span> <span data-ttu-id="44bce-104">Nachdem Sie die Sandbox aktiviert haben, werden Sie mit einem kostenlosen Abonnement, das von Microsoft Learn verwaltet wird, bei Azure angemeldet.</span><span class="sxs-lookup"><span data-stu-id="44bce-104">Once you activate the sandbox, you'll be logged into Azure with a free subscription managed by Microsoft Learn.</span></span> <span data-ttu-id="44bce-105">Sie müssen sich nicht selbst bei Azure anmelden oder ein Abonnement auswählen. Dies wird für Sie durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="44bce-105">You don't have to log into Azure on your own, or select a subscription - this will be done for you.</span></span> <span data-ttu-id="44bce-106">Außerdem erstellen Sie normalerweise eine _Ressourcengruppe_ für neue Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="44bce-106">In addition, normally you would create a _resource group_ to hold new resources.</span></span> <span data-ttu-id="44bce-107">In diesem Modul erstellt die Azure-Sandbox für Sie eine Ressourcengruppe, die verwendet wird, um alle Befehle auszuführen.</span><span class="sxs-lookup"><span data-stu-id="44bce-107">In this module, the Azure Sandbox will create a resource group for you which will be used to execute all the commands.</span></span>

## <a name="create-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="44bce-108">Erstellen eines virtuellen Linux-Computers mit der Azure CLI</span><span class="sxs-lookup"><span data-stu-id="44bce-108">Create a Linux VM with the Azure CLI</span></span>

<span data-ttu-id="44bce-109">Die Azure CLI enthält den Befehl „`vm`“ für die Arbeit mit virtuellen Computern in Azure.</span><span class="sxs-lookup"><span data-stu-id="44bce-109">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="44bce-110">Wir können verschiedene Unterbefehle bereitstellen, um bestimmte Aufgaben auszuführen.</span><span class="sxs-lookup"><span data-stu-id="44bce-110">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="44bce-111">Dies sind die am häufigsten verwendeten:</span><span class="sxs-lookup"><span data-stu-id="44bce-111">The most common include:</span></span>

| <span data-ttu-id="44bce-112">Unterbefehl</span><span class="sxs-lookup"><span data-stu-id="44bce-112">Sub-command</span></span> | <span data-ttu-id="44bce-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="44bce-113">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="44bce-114">Erstellen eines neuen virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="44bce-114">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="44bce-115">Aufheben der Zuordnung eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="44bce-115">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="44bce-116">Löschen eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="44bce-116">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="44bce-117">Auflisten der erstellten virtuellen Computer in Ihrem Abonnement</span><span class="sxs-lookup"><span data-stu-id="44bce-117">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="44bce-118">Öffnen eines bestimmten Netzwerkports für eingehenden Datenverkehr</span><span class="sxs-lookup"><span data-stu-id="44bce-118">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="44bce-119">Neustarten eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="44bce-119">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="44bce-120">Abrufen der Details für einen virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="44bce-120">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="44bce-121">Starten eines angehaltenen virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="44bce-121">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="44bce-122">Anhalten eines ausgeführten virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="44bce-122">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="44bce-123">Aktualisieren der Eigenschaft eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="44bce-123">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="44bce-124">Eine vollständige Liste der Befehle finden Sie in der [Dokumentation der Azure CLI-Referenz](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="44bce-124">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="44bce-125">Beginnen wir mit dem ersten: `az vm create`.</span><span class="sxs-lookup"><span data-stu-id="44bce-125">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="44bce-126">Mit diesem Befehl wird ein virtueller Computer in einer Ressourcengruppe erstellt.</span><span class="sxs-lookup"><span data-stu-id="44bce-126">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="44bce-127">Es gibt verschiedene Parameter, die Sie übergeben können, um alle Aspekte des neuen virtuellen Computers zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="44bce-127">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="44bce-128">Diese drei Parameter müssen angegeben werden:</span><span class="sxs-lookup"><span data-stu-id="44bce-128">The three parameters that must be supplied are:</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="44bce-129">Parameter</span><span class="sxs-lookup"><span data-stu-id="44bce-129">Parameter</span></span> | <span data-ttu-id="44bce-130">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="44bce-130">Description</span></span> |
> |-----------|-------------|
> | `resource-group` | <span data-ttu-id="44bce-131">Die Ressourcengruppe, die als Besitzer des virtuellen Computers fungiert. Verwenden Sie **<rgn>[Sandbox Resource Group]</rgn>** (Sandbox-Ressourcengruppe).</span><span class="sxs-lookup"><span data-stu-id="44bce-131">The resource group that will own the virtual machine, use **<rgn>[Sandbox Resource Group]</rgn>**.</span></span> |
> | `name` | <span data-ttu-id="44bce-132">Der Name des virtuellen Computers – muss innerhalb der Ressourcengruppe eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="44bce-132">The name of the virtual machine - must be unique within the resource group.</span></span> |
> | `image` | <span data-ttu-id="44bce-133">Das Betriebssystemimage, das zum Erstellen des virtuellen Computers verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="44bce-133">The operating system image to use to create the VM.</span></span> |
> | `location` | <span data-ttu-id="44bce-134">Die Region, in der die VM angeordnet wird.</span><span class="sxs-lookup"><span data-stu-id="44bce-134">The region to place the VM in.</span></span> <span data-ttu-id="44bce-135">Normalerweise liegt die Region in der Nähe des VM-Benutzers.</span><span class="sxs-lookup"><span data-stu-id="44bce-135">Typically this would be close to the consumer of the VM.</span></span> <span data-ttu-id="44bce-136">Wählen Sie in dieser Übung in der folgenden Liste einen Standort in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="44bce-136">In this exercise, choose a location nearby from the following list.</span></span> |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="44bce-137">Darüber hinaus ist es hilfreich, das `--verbose`-Flag hinzuzufügen, um den Fortschritt der Erstellung des virtuellen Computers zu beobachten.</span><span class="sxs-lookup"><span data-stu-id="44bce-137">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="44bce-138">Erstellen eines virtuellen Linux-Computers</span><span class="sxs-lookup"><span data-stu-id="44bce-138">Create a Linux virtual machine</span></span>

<span data-ttu-id="44bce-139">Wir erstellen nun einen neuen virtuellen Linux-Computer.</span><span class="sxs-lookup"><span data-stu-id="44bce-139">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="44bce-140">Führen Sie den folgenden Befehl in Azure Cloud Shell aus, um am Standort „USA, Westen“ einen Debian Linux-Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="44bce-140">Execute the following command in Azure Cloud Shell to create a Debian Linux machine in the "West US" location.</span></span> <span data-ttu-id="44bce-141">Ändern Sie den Standort, wenn dieser nicht in Ihrer Nähe liegt.</span><span class="sxs-lookup"><span data-stu-id="44bce-141">Change the location if that one isn't nearby.</span></span>

```azurecli
az vm create --resource-group <rgn>[Sandbox resource group name]</rgn> --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --location westus --verbose 
```

[!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


<span data-ttu-id="44bce-142">Dieser Befehl erstellt einen neuen virtuellen Linux-Computer unter **Debian** mit dem Namen „`SampleVM`“.</span><span class="sxs-lookup"><span data-stu-id="44bce-142">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="44bce-143">Beachten Sie, dass sich das Azure CLI-Tool während der Erstellung des virtuellen Computers im Wartezustand befindet.</span><span class="sxs-lookup"><span data-stu-id="44bce-143">Notice that the Azure CLI tool waits while the VM is being created.</span></span> <span data-ttu-id="44bce-144">Sie können die Option `--no-wait` hinzufügen, um das Azure CLI-Tool anzuweisen, die Rückgabe sofort durchzuführen, und zu erreichen, dass Azure mit der Erstellung der VM im Hintergrund fortfährt.</span><span class="sxs-lookup"><span data-stu-id="44bce-144">You can add the `--no-wait` option to tell the Azure CLI tool to return immediately and have Azure continue creating the VM in the background.</span></span> <span data-ttu-id="44bce-145">Dies ist hilfreich, wenn Sie den Befehl in einem Skript ausführen.</span><span class="sxs-lookup"><span data-stu-id="44bce-145">This is useful if you're executing the command in a script.</span></span> <span data-ttu-id="44bce-146">Verwenden Sie später im Skript den Befehl „`azure vm wait --name [vm-name]`“, um zu warten, bis der virtuelle Computer vollständig erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="44bce-146">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="44bce-147">Wenn Sie sich die ausführlichen Antworten ansehen, werden Sie auch feststellen, dass der Name „`SampleVM`“ in verschiedenen Abhängigkeiten für den virtuellen Computer verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="44bce-147">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```output
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="44bce-148">Sie können diese automatisch generierten Ressourcennamen mithilfe von optionalen Parametern für „`vm create`“ überschreiben, z.B. `--vnet-name` und `--public-ip-address-dns-name`.</span><span class="sxs-lookup"><span data-stu-id="44bce-148">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="44bce-149">Wir ändern den Namen des Administratorkontos mit dem `admin-username`-Flag in **„aldis“**.</span><span class="sxs-lookup"><span data-stu-id="44bce-149">We are specifying the administrator account name through the `admin-username` flag to be **"aldis"**.</span></span> <span data-ttu-id="44bce-150">Wenn Sie dies auslassen, verwendet der `vm create`-Befehl Ihren _aktuellen Benutzernamen_.</span><span class="sxs-lookup"><span data-stu-id="44bce-150">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="44bce-151">Da die Regeln für Kontonamen in jedem Betriebssystem anders sind, ist es sicherer, einen bestimmten Namen anzugeben.</span><span class="sxs-lookup"><span data-stu-id="44bce-151">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> 

> [!NOTE]
> <span data-ttu-id="44bce-152">Allgemeine Namen wie „root“ und „admin“ sind für die meisten Images nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="44bce-152">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="44bce-153">Wir verwenden auch das `generate-ssh-keys`-Flag.</span><span class="sxs-lookup"><span data-stu-id="44bce-153">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="44bce-154">Dieser Parameter wird für Linux-Distributionen verwendet und erstellt ein Sicherheitsschlüsselpaar, sodass wir das `ssh`-Tool verwenden können, um remote auf den virtuellen Computer zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="44bce-154">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="44bce-155">Die beiden Dateien werden in den Ordner „`.ssh`“ auf Ihrem Computer und auf dem virtuellen Computer platziert.</span><span class="sxs-lookup"><span data-stu-id="44bce-155">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="44bce-156">Wenn Sie bereits über einen SSH-Schlüssel namens „`id_rsa`“ im Zielordner verfügen, wird dieser verwendet, anstatt einen neuen Schlüssel zu generieren.</span><span class="sxs-lookup"><span data-stu-id="44bce-156">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="44bce-157">Sobald der virtuelle Computer erstellt wurde, erhalten Sie eine JSON-Antwort, die den aktuellen Zustand des virtuellen Computers und seine von Azure zugewiesenen öffentlichen und privaten IP-Adressen enthält:</span><span class="sxs-lookup"><span data-stu-id="44bce-157">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "westus",
  "macAddress": "00-0D-3A-58-F8-45",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
  "resourceGroup": "2568d0d0-efe3-4d04-a08f-df7f009f822a",
  "zones": ""
}
```
