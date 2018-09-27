<span data-ttu-id="f09c2-101">Wir verfügen über einen Lastenausgleich, mit dem wir eingehenden Internetdatenverkehr weiterleiten. Nun benötigen wir einige Azure-VMs, zu denen der Datenverkehr geleitet werden soll.</span><span class="sxs-lookup"><span data-stu-id="f09c2-101">We have a load balancer to take inbound Internet traffic and route it, now we need some Azure VMs to route traffic to.</span></span> <span data-ttu-id="f09c2-102">In diesem Beispiel wird Linux verwendet, allerdings funktioniert die exakt gleiche Vorgehensweise mit jedem beliebigen VM-Image.</span><span class="sxs-lookup"><span data-stu-id="f09c2-102">We'll use Linux for this example, but the exact same technique would work with any virtual machine image.</span></span>

## <a name="create-a-set-of-vms"></a><span data-ttu-id="f09c2-103">Erstellen einer Gruppe von virtuellen Computern</span><span class="sxs-lookup"><span data-stu-id="f09c2-103">Create a set of VMs</span></span>

<span data-ttu-id="f09c2-104">Im Folgenden erstellen Sie drei virtuelle Computer (VMs) und gruppieren diese über die Azure CLI in einer Verfügbarkeitsgruppe.</span><span class="sxs-lookup"><span data-stu-id="f09c2-104">We're going to create three VMs and group them into an availability set with the Azure CLI.</span></span> <span data-ttu-id="f09c2-105">Für diese Aufgabe hätte auch das Portal verwendet werden können, jedoch ist dieser Vorgang mit einem Tool zur Skripterstellung viel einfacher, da mehrere Ressourcen erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="f09c2-105">We could have used the portal for this task - but because we're creating multiple resources, it's much easier to do this through a scripting tool.</span></span>

<span data-ttu-id="f09c2-106">Wenn Sie die Verwendung des Azure-Portals _wirklich_ bevorzugen, können Sie alternativ eine _Vorlage_ verwenden.</span><span class="sxs-lookup"><span data-stu-id="f09c2-106">An alternative approach if you _really_ prefer to use the Azure portal would be to use a _template_.</span></span> <span data-ttu-id="f09c2-107">Dabei handelt es sich um JSON-Anweisungen, die zum Bereitstellen von Ressourcen verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="f09c2-107">These are JSON instructions which can be used to deploy resources.</span></span> <span data-ttu-id="f09c2-108">Sie können eine Vorlage für die VM definieren und die Vorlage anschließend mehrmals im Azure-Portal bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-108">We could define a template for the virtual machine and then deploy the template multiple times in the Azure portal.</span></span>

### <a name="create-some-azure-cli-defaults"></a><span data-ttu-id="f09c2-109">Erstellen von Standardbefehlen für die Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f09c2-109">Create some Azure CLI defaults</span></span>

1. <span data-ttu-id="f09c2-110">Legen Sie zunächst Standardbefehle in der Azure CLI fest.</span><span class="sxs-lookup"><span data-stu-id="f09c2-110">Start by setting some defaults in the Azure CLI.</span></span> <span data-ttu-id="f09c2-111">Für jeden Befehl ist eine _Ressourcengruppe_ und optional ein _Standort_ erforderlich.</span><span class="sxs-lookup"><span data-stu-id="f09c2-111">Every command we use requires a _resource group_ and an optional _location_.</span></span> <span data-ttu-id="f09c2-112">Anstatt diese jedes Mal einzugeben, können Sie Standardparameter festlegen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-112">Rather than typing that every time, we can set it as a default parameter.</span></span> <span data-ttu-id="f09c2-113">Verwenden Sie die vorab erstellte Azure-Sandboxressourcengruppe und den gleichen Standort, den Sie für Azure Load Balancer ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="f09c2-113">Use the pre-created Azure sandbox resource group, and the same location you selected for the Azure Load Balancer.</span></span> <span data-ttu-id="f09c2-114">Zur Erinnerung werden hier die verfügbaren Standorte aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="f09c2-114">As a reminder, here are the available locations:</span></span>

    [!include[](../../../includes/azure-sandbox-regions-note.md)]

1. <span data-ttu-id="f09c2-115">Geben Sie diesen Befehl rechts in Cloud Shell ein, und ersetzen Sie den Platzhalter `<location>` durch den Standort, den Sie für Azure Load Balancer verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="f09c2-115">Type this command into the Cloud Shell on the right, replacing the `<location>` placeholder with the location you used for your Azure Load Balancer.</span></span>

    ```azurecli
    az configure --defaults group=<rgn>[sandbox Resource Group</rgn> location=<location>
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

### <a name="create-an-availability-set"></a><span data-ttu-id="f09c2-116">Erstellen einer Verfügbarkeitsgruppe</span><span class="sxs-lookup"><span data-stu-id="f09c2-116">Create an availability set</span></span>

<span data-ttu-id="f09c2-117">Beginnen Sie zunächst mit dem Erstellen einer _Verfügbarkeitsgruppe_.</span><span class="sxs-lookup"><span data-stu-id="f09c2-117">Let's start by creating an _availability set_.</span></span>

<span data-ttu-id="f09c2-118">Eine Verfügbarkeitsgruppe muss festgelegt sein, damit die VMs in ihr gruppiert werden können.</span><span class="sxs-lookup"><span data-stu-id="f09c2-118">We will need an availability set to group our virtual machines into.</span></span> <span data-ttu-id="f09c2-119">Mit dem Befehl `vm availability-set` können Sie sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-119">We can use the `vm availability-set` command to create one.</span></span> <span data-ttu-id="f09c2-120">Sie benötigt lediglich einen Namen. Für diese Vorgehensweise wird **woodgrove-avail-set** verwendet.</span><span class="sxs-lookup"><span data-stu-id="f09c2-120">It just needs a name, we'll use **woodgrove-avail-set**.</span></span>

```azurecli
az vm availability-set create --name woodgrove-avail-set
```

### <a name="create-a-configuration-script"></a><span data-ttu-id="f09c2-121">Erstellen eines Konfigurationsskripts</span><span class="sxs-lookup"><span data-stu-id="f09c2-121">Create a configuration script</span></span>

<span data-ttu-id="f09c2-122">Für alle VMs soll die gleiche grundlegende Konfiguration verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="f09c2-122">We want to use the same basic configuration for each of the VMs.</span></span>

    - <span data-ttu-id="f09c2-123">Ubuntu Linux</span><span class="sxs-lookup"><span data-stu-id="f09c2-123">Ubuntu Linux</span></span>
    - <span data-ttu-id="f09c2-124">nginx-Webserver</span><span class="sxs-lookup"><span data-stu-id="f09c2-124">nginx web server</span></span>
    - <span data-ttu-id="f09c2-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="f09c2-125">Node.js</span></span>
    - <span data-ttu-id="f09c2-126">Allgemeine Website mit einer einzigen Seite für Testzwecke</span><span class="sxs-lookup"><span data-stu-id="f09c2-126">Basic website with a single page for testing</span></span>

<span data-ttu-id="f09c2-127">Die Auswahl des Betriebssystem basiert auf dem ausgewählten Image, für andere Konfigurationselemente ist jedoch ein gewisses Maß an Skripterstellung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="f09c2-127">The choice of OS is based on the image we select, but the other configuration elements require some scripting.</span></span> <span data-ttu-id="f09c2-128">Erstellen Sie eine lokale Datei in Cloud Shell, um einen Webserver zu installieren, und konfigurieren Sie diesen mit einer allgemeinen Website.</span><span class="sxs-lookup"><span data-stu-id="f09c2-128">Let's create a local file in the Cloud Shell to install a web server and configure it with a basic site.</span></span>

1. <span data-ttu-id="f09c2-129">Öffnen Sie den Cloud Shell-Editor, indem Sie `code` im Terminal eingeben.</span><span class="sxs-lookup"><span data-stu-id="f09c2-129">Open the Cloud Shell Editor by typing `code` in the terminal.</span></span>

    ```bash
    code
    ```

    <span data-ttu-id="f09c2-130">Dies ist ein integrierter Editor, den Sie zum Erstellen und Bearbeiten von Dateien direkt in der Cloud Shell-Umgebung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="f09c2-130">This is a built-in editor you can use to create and edit files right in the Cloud Shell environment.</span></span> <span data-ttu-id="f09c2-131">Die Dateien werden in einem Speicherkonto in Azure gespeichert, das erstellt wurde, als Sie die Cloud Shell-Umgebung gestartet haben.</span><span class="sxs-lookup"><span data-stu-id="f09c2-131">The files are saved in Azure in a Storage account created when you launched the Cloud Shell environment.</span></span>

1. <span data-ttu-id="f09c2-132">Kopieren Sie das folgende Skript, und fügen Sie es in das Editorfenster ein.</span><span class="sxs-lookup"><span data-stu-id="f09c2-132">Copy the following script and paste it into the editor window.</span></span>

    ```script
    #cloud-config
    package_upgrade: true
    packages:
      - nginx
      - nodejs
      - npm
    write_files:
      - owner: www-data:www-data
      - path: /etc/nginx/sites-available/default
        content: |
          server {
            listen 80;
            location / {
              proxy_pass http://localhost:3000;
              proxy_http_version 1.1;
              proxy_set_header Upgrade $http_upgrade;
              proxy_set_header Connection keep-alive;
              proxy_set_header Host $host;
              proxy_cache_bypass $http_upgrade;
            }
          }
      - owner: azureuser:azureuser
      - path: /home/azureuser/myapp/index.js
        content: |
          var express = require('express')
          var app = express()
          var os = require('os');
          app.get('/', function (req, res) {
            res.send('Hello World from host ' + os.hostname() + '!')
          })
          app.listen(3000, function () {
            console.log('Hello world app listening on port 3000!')
          })
    runcmd:
      - service nginx restart
      - cd "/home/azureuser/myapp"
      - npm init
      - npm install express -y
      - nodejs index.js
    ```

1. <span data-ttu-id="f09c2-133">Speichern Sie die Datei, und nennen Sie sie **cloud-init.txt**.</span><span class="sxs-lookup"><span data-stu-id="f09c2-133">Save the file - give it the name **cloud-init.txt**.</span></span> <span data-ttu-id="f09c2-134">Hierzu können Sie das Kontextmenü „...“ in der oberen rechten Ecke des Editors, <kbd>STRG+S</kbd> unter Windows und Linux oder <kbd>CMD+S</kbd> unter macOS verwenden.</span><span class="sxs-lookup"><span data-stu-id="f09c2-134">You can use the "..." context menu on the top/right corner of the editor, or use <kbd>Ctrl+S</kbd> in Windows and Linux, and <kbd>Cmd+S</kbd> on macOS.</span></span>

1. <span data-ttu-id="f09c2-135">Beenden Sie den Editor. Hierzu können Sie erneut das Kontextmenü „...“ oder eine Tastenkombination (<kbd>STRG+Q</kbd>) verwenden.</span><span class="sxs-lookup"><span data-stu-id="f09c2-135">Exit the editor - again you can use the "..." context menu, or an accelerator key (<kbd>Ctrl+Q</kbd>).</span></span>

1. <span data-ttu-id="f09c2-136">Die Datei sollte sich im Dateisystem befinden.</span><span class="sxs-lookup"><span data-stu-id="f09c2-136">The file should be on the file system.</span></span> <span data-ttu-id="f09c2-137">Versuchen Sie, den Befehl `ls` zum Auflisten der Ordnerinhalte zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="f09c2-137">Try using the `ls` command to list the contents of the folder.</span></span> <span data-ttu-id="f09c2-138">Sie können auch `cat` für die Datei verwenden, um die Inhalte zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-138">You can also `cat` the file to verify the contents.</span></span>

### <a name="create-the-virtual-machines"></a><span data-ttu-id="f09c2-139">Erstellen der virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="f09c2-139">Create the virtual machines</span></span>

<span data-ttu-id="f09c2-140">Als Nächstes erstellen Sie drei Ubuntu Linux-VMs mithilfe der Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f09c2-140">Next, let's create three Ubuntu Linux virtual machines with the Azure CLI.</span></span> <span data-ttu-id="f09c2-141">Die Optionen werden hier nicht erläutert. Sollten Sie jedoch daran interessiert sein, mehr über die Verwaltung von VMs mit der CLI zu lernen, finden Sie weitere Informationen im Modul **Verwalten von virtuellen Computern mit der Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="f09c2-141">We won't cover the options here, but if you are interested in learning more about VM management with the CLI, check out the **Manage virtual machines with the Azure CLI** module.</span></span>

<span data-ttu-id="f09c2-142">Außerdem müssen Sie eine virtuelle Netzwerkschnittstelle für jede VM erstellen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-142">We also need to create a virtual network interface for each VM.</span></span> <span data-ttu-id="f09c2-143">Sie können eine Schleife nutzen, um sie zusammen zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-143">We can use a loop and create them together.</span></span>

1. <span data-ttu-id="f09c2-144">Verwenden Sie den Befehl `vm-create`, um drei VMs in einer Schleife zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-144">Use the `vm-create` command to create three virtual machines in a loop.</span></span> <span data-ttu-id="f09c2-145">Sie können den folgenden Code für Folgendes verwenden:</span><span class="sxs-lookup"><span data-stu-id="f09c2-145">You can use the following code to:</span></span>
    - <span data-ttu-id="f09c2-146">Erstellen Sie eine NIC namens _woodgrove_NicX_, wobei X für [1,2,3] steht.</span><span class="sxs-lookup"><span data-stu-id="f09c2-146">Create a NIC named _woodgrove_NicX_ where X is [1,2,3].</span></span>
    - <span data-ttu-id="f09c2-147">Erstellen Sie eine VM namens _woodgrove-VMX_, wobei X für [1,2,3] steht.</span><span class="sxs-lookup"><span data-stu-id="f09c2-147">Create a VM named _woodgrove-VMX_ where X is [1,2,3].</span></span>
    - <span data-ttu-id="f09c2-148">Ordnen Sie jede NIC dem erstellten virtuellen Netzwerk zu.</span><span class="sxs-lookup"><span data-stu-id="f09c2-148">Associate each NIC to the created VNET</span></span>
    - <span data-ttu-id="f09c2-149">Ordnen Sie jede VM der NIC und der Verfügbarkeitsgruppe zu.</span><span class="sxs-lookup"><span data-stu-id="f09c2-149">Associate each VM to the NIC and availability set.</span></span>

    ```azurecli
    for i in `seq 1 3`; do

        az network nic create --name woodgrove-Nic$i \
            --vnet-name woodgrove-VNET \
            --subnet backendSubnet

        az vm create --name woodgrove-VM$i \
            --availability-set woodgrove-avail-set \
            --nics woodgrove-Nic$i \
            --image UbuntuLTS \
            --admin-username azureuser \
            --generate-ssh-keys \
            --custom-data cloud-init.txt \
            --no-wait
    done
    ```
    > [!TIP]
    > <span data-ttu-id="f09c2-150">Hier legt der Befehl den Namen des Administrators auf „azureuser“ fest, dies können Sie beliebig ändern.</span><span class="sxs-lookup"><span data-stu-id="f09c2-150">The command is setting the administrator name to "azureuser" here, you can change that to anything you like.</span></span> <span data-ttu-id="f09c2-151">Außerdem können Sie ein Kennwort angeben, wenn Sie Benutzernamen mit Kennwort SSH-Schlüsseln vorziehen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-151">You can also supply a password if you prefer username/password over SSH keys.</span></span>

1. <span data-ttu-id="f09c2-152">Die Ausführung dauert eine Weile, und nach Abschluss der Schleife werden die VMs noch nicht verfügbar sein.</span><span class="sxs-lookup"><span data-stu-id="f09c2-152">This will take a while to run - and even when the loop is finished, the VMs won't quite be available.</span></span> <span data-ttu-id="f09c2-153">Sie können zum Azure-Portal wechseln und auf **Alle Ressourcen** klicken, um die erstellten Ressourcen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f09c2-153">You can switch over to the Azure portal and use the **All Resources** display to see the created resources.</span></span>

1. <span data-ttu-id="f09c2-154">Sie können auf den Befehl `vm list` verwenden, um anzuzeigen, wie viele VMs bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="f09c2-154">You can also use the `vm list` command to see how many VMs have been deployed.</span></span>

    ```azurecli
    az vm list -o table
    ```

<span data-ttu-id="f09c2-155">Als Nächstes wird das Konfigurieren des Lastenausgleichs erläutert.</span><span class="sxs-lookup"><span data-stu-id="f09c2-155">Next we'll talk about how to configure the load balancer.</span></span>