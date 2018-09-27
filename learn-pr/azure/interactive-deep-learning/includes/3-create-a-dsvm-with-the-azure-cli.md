<span data-ttu-id="435ea-101">Als Softwareentwickler in Ihrem Unternehmen haben Sie die Möglichkeit, Ihre Fähigkeiten weiter auszubauen und Teil des internen KI-Teams zu werden.</span><span class="sxs-lookup"><span data-stu-id="435ea-101">As a software developer at your company, you've the opportunity to grow your skills and become part of the in-house AI team.</span></span> <span data-ttu-id="435ea-102">Während Sie sich auf diese spannende neue Rolle vorbereiten, müssen Sie allerdings auch noch Ihre sonstigen Aufgaben erledigen.</span><span class="sxs-lookup"><span data-stu-id="435ea-102">While you ramp-up on this exciting new role, you still have your day job to do.</span></span> <span data-ttu-id="435ea-103">Angenommen, der hauptverantwortliche AI-Engineer in Ihrem Team hat Ihnen von Jupyter Notebooks erzählt. Diese Anwendung umfasst PyTorch-basierte Aufgaben zum Trainieren eines Bildklassifizierungsmodells.</span><span class="sxs-lookup"><span data-stu-id="435ea-103">The senior AI engineer on your team has told you about some useful Jupyter notebooks that have PyTorch-based labs to train an image classification model.</span></span> <span data-ttu-id="435ea-104">Dies ist zwar eine interessante Anwendung, aber es wird nicht empfohlen, mehrere Frameworks auf einem Computer zu installieren.</span><span class="sxs-lookup"><span data-stu-id="435ea-104">Exciting stuff, but you don't want to install a set of frameworks onto your dev rig.</span></span> <span data-ttu-id="435ea-105">Stattdessen sollten Sie einen virtuellen Computer erstellen, der auf dem Data Science Virtual Machine-Image (DSVM) basiert.</span><span class="sxs-lookup"><span data-stu-id="435ea-105">Instead, you decide to create a virtual machine based on the Data Science Virtual Machine (DSVM) image.</span></span> 

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="435ea-106">Was ist die Azure CLI?</span><span class="sxs-lookup"><span data-stu-id="435ea-106">What is the Azure CLI</span></span>

<span data-ttu-id="435ea-107">Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="435ea-107">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources.</span></span> <span data-ttu-id="435ea-108">Sie steht für macOS, Linux und Windows sowie unter Verwendung von [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) im Browser zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="435ea-108">It's available for macOS, Linux, and Windows, or in the browser using [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span> <span data-ttu-id="435ea-109">In dem Modul **Kontrollieren von Azure-Diensten mit der CLI** werden die Funktionen des Tools detailliert erläutert.</span><span class="sxs-lookup"><span data-stu-id="435ea-109">We have complete coverage of using this tool in the **Control Azure services with the CLI** module.</span></span>

## <a name="managing-deployments"></a><span data-ttu-id="435ea-110">Verwalten von Bereitstellungen</span><span class="sxs-lookup"><span data-stu-id="435ea-110">Managing deployments</span></span>

<span data-ttu-id="435ea-111">Die Azure CLI umfasst den `az group deployment`-Befehl zum Verwalten von Azure Resource Manager-Bereitstellungen.</span><span class="sxs-lookup"><span data-stu-id="435ea-111">The Azure CLI includes the `az group deployment` command to manage Azure Resource Manager deployments.</span></span> <span data-ttu-id="435ea-112">Wir können verschiedene Unterbefehle bereitstellen, um bestimmte Aufgaben auszuführen.</span><span class="sxs-lookup"><span data-stu-id="435ea-112">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="435ea-113">Folgende werden am häufigsten verwendeten:</span><span class="sxs-lookup"><span data-stu-id="435ea-113">The most common include:</span></span>

| <span data-ttu-id="435ea-114">Unterbefehl</span><span class="sxs-lookup"><span data-stu-id="435ea-114">Subcommand</span></span> | <span data-ttu-id="435ea-115">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="435ea-115">Description</span></span> |
|-------------|-------------|
| `create` | <span data-ttu-id="435ea-116">Startet eine Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="435ea-116">Start a deployment.</span></span> |
| `list` | <span data-ttu-id="435ea-117">Listet alle Bereitstellungen einer Ressourcengruppe auf.</span><span class="sxs-lookup"><span data-stu-id="435ea-117">Get all the deployments for a resource group.</span></span> |
| `export` | <span data-ttu-id="435ea-118">Exportiert die für die Bereitstellung verwendete Vorlage.</span><span class="sxs-lookup"><span data-stu-id="435ea-118">Export the template used for a deployment.</span></span> |

<span data-ttu-id="435ea-119">Eine vollständige Liste der verfügbaren Bereitstellungsbefehle finden Sie in der [Referenz zu Azure-Befehlen für Gruppenbereitstellungen](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create).</span><span class="sxs-lookup"><span data-stu-id="435ea-119">For a complete list of available deployment commands, see the [az group deployment command reference](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create)</span></span>

<span data-ttu-id="435ea-120">In diesem Beispiel wird `az group deployment create` zum Bereitstellen des virtuellen Computers verwendet.</span><span class="sxs-lookup"><span data-stu-id="435ea-120">We'll use `az group deployment create` to provision our virtual machine.</span></span>

## <a name="create-a-json-deployment-parameters-file"></a><span data-ttu-id="435ea-121">Erstellen einer JSON-Datei mit Bereitstellungsparametern</span><span class="sxs-lookup"><span data-stu-id="435ea-121">Create a JSON deployment parameters file</span></span>

<span data-ttu-id="435ea-122">In diesem Beispiel wird die VM mithilfe einer Azure Resource Manager-Vorlage erstellt.</span><span class="sxs-lookup"><span data-stu-id="435ea-122">We're going to create our VM using an Azure Resource Manager template.</span></span> <span data-ttu-id="435ea-123">Die Vorlage definiert das DSVM-Image für Linux, das bereitgestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="435ea-123">The template defines the Linux DSVM image we want to provision.</span></span> <span data-ttu-id="435ea-124">Sie müssen für die Vorlage einige Parameter angeben, z.B. die Größe der VM, die verwendet werden soll, den Namen des Administratorbenutzers und das zugehörige Kennwort sowie den Hostnamen.</span><span class="sxs-lookup"><span data-stu-id="435ea-124">We need to supply some parameters to the template, such as the VM size we want to use, the admin username and password, and the host name of our machine.</span></span> 

1. <span data-ttu-id="435ea-125">Führen Sie in Azure Cloud Shell für diese Einheit den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="435ea-125">Execute the following command in Azure Cloud Shell to the right of this unit:</span></span>

    ```bash
    code parameter_file.json
    ```
    <span data-ttu-id="435ea-126"><!-- TODO add a link to official doc that explains the built-in editor when it becomes available --> Dieser Befehl öffnet im integrierten Editor eine leere Datei mit dem Namen `parameter_file.json`.</span><span class="sxs-lookup"><span data-stu-id="435ea-126"><!-- TODO add a link to official doc that explains the built-in editor when it becomes available --> This command opens and empty file called `parameter_file.json` in the built-in editor.</span></span> 

1. <span data-ttu-id="435ea-127">Fügen Sie den folgenden JSON-Ausschnitt in die leere Datei im Code-Editor ein.</span><span class="sxs-lookup"><span data-stu-id="435ea-127">Paste the following JSON snippet into the empty file into the code editor.</span></span>

    ```json
    { 
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
         "adminUsername": { "value" : "<USERNAME>"},
         "adminPassword": { "value" : "<PASSWORD>"},
         "vmName": { "value" : "<HOSTNAME>"},
         "vmSize": { "value" : "Standard_DS2_v2"},
      }
    }
    ```

1. <span data-ttu-id="435ea-128">Aktualisieren Sie die folgenden Parameter in der JSON-Datei, die Sie in den Editor eingefügt haben:</span><span class="sxs-lookup"><span data-stu-id="435ea-128">Update the following parameters in the JSON you pasted in the editor:</span></span>

    |<span data-ttu-id="435ea-129">Parameter</span><span class="sxs-lookup"><span data-stu-id="435ea-129">Parameter</span></span>  |<span data-ttu-id="435ea-130">Aktueller Wert</span><span class="sxs-lookup"><span data-stu-id="435ea-130">Current value</span></span>  |<span data-ttu-id="435ea-131">Ihr Wert</span><span class="sxs-lookup"><span data-stu-id="435ea-131">Your value</span></span>  |
    |---------|---------|---------|
    |<span data-ttu-id="435ea-132">adminUsername</span><span class="sxs-lookup"><span data-stu-id="435ea-132">adminUsername</span></span>     |  `<USERNAME>`       |    <span data-ttu-id="435ea-133">Wählen Sie einen Namen für den Administratorbenutzer dieses neuen Computers aus, z.B. *azuser*.</span><span class="sxs-lookup"><span data-stu-id="435ea-133">Choose a name for the admin user of this new machine, such as, *azuser*.</span></span>     |
    |<span data-ttu-id="435ea-134">adminPassword</span><span class="sxs-lookup"><span data-stu-id="435ea-134">adminPassword</span></span>     |  `<PASSWORD>`       |   <span data-ttu-id="435ea-135">Wählen Sie ein Kennwort für dieses Administratorbenutzerkonto aus.</span><span class="sxs-lookup"><span data-stu-id="435ea-135">Choose a password for this admin user account.</span></span> <span data-ttu-id="435ea-136">Weitere Informationen über Kennwortanforderungen finden Sie unter [Häufig gestellte Fragen zu virtuellen Linux-Computern](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="435ea-136">To learn more about password requirements, see [Frequently asked question about Linux Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true)</span></span>     |
    |<span data-ttu-id="435ea-137">vmName</span><span class="sxs-lookup"><span data-stu-id="435ea-137">vmName</span></span>     |   `<HOSTNAME>`      |  <span data-ttu-id="435ea-138">Geben Sie einen Namen für den neuen virtuellen Computer ein.</span><span class="sxs-lookup"><span data-stu-id="435ea-138">Choose a name for the new virtual machine.</span></span> <span data-ttu-id="435ea-139">Der Name muss mit einem Buchstaben beginnen und darf nur Kleinbuchstaben und Zahlen enthalten.</span><span class="sxs-lookup"><span data-stu-id="435ea-139">Your name must begin with a letter and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="435ea-140">Versuchen Sie, einen eindeutigen Namen zu finden, der z.B. Ihre Initialen und Ihr Geburtsjahr enthält.</span><span class="sxs-lookup"><span data-stu-id="435ea-140">Try to choose a unique name, such as one that includes your initials and your birth year.</span></span> |
    |<span data-ttu-id="435ea-141">vmSize</span><span class="sxs-lookup"><span data-stu-id="435ea-141">vmSize</span></span>     |  <span data-ttu-id="435ea-142">Standard_DS2_v2</span><span class="sxs-lookup"><span data-stu-id="435ea-142">Standard_DS2_v2</span></span>       |  <span data-ttu-id="435ea-143">Die VM-Größe eignet sich gut für diese Übung. Sie können sie aber auch ändern.</span><span class="sxs-lookup"><span data-stu-id="435ea-143">This VM size will work fine for this exercise, but you are free to change it.</span></span> <span data-ttu-id="435ea-144">Eine Liste mit verfügbaren VM-Größen finden Sie unter [Größen für virtuelle Linux-Computer in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="435ea-144">A list of available vm sizes can be found here [Sizes for Linux virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true)</span></span>       |

1. <span data-ttu-id="435ea-145">Speichern Sie Ihre Änderungen in `parameter_file.json`, und schließen Sie den Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="435ea-145">Save your changes in `parameter_file.json` and close the text editor.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="435ea-146">Merken Sie sich die Werte, die Sie für adminUsername, adminPassword und vmName angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="435ea-146">Remember the values you chose for adminUsername, adminPassword and vmName.</span></span> <span data-ttu-id="435ea-147">Sie werden Sie im Laufe dieser Übung noch einmal brauchen.</span><span class="sxs-lookup"><span data-stu-id="435ea-147">We'll use them again in this exercise.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="435ea-148">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="435ea-148">Create a resource group</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="435ea-149">In der Regel können Sie Ressourcengruppen in einer Region Ihrer Wahl erstellen.</span><span class="sxs-lookup"><span data-stu-id="435ea-149">Normally you'd create a resource group in a region of your choice.</span></span> <span data-ttu-id="435ea-150">Sie erhalten allerdings über die aktuelle Sandboxsitzung eine Ressourcengruppe, die Sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="435ea-150">However, the sandbox session you are currently in supplies a resource group for you to use.</span></span> <span data-ttu-id="435ea-151">Die Ressourcengruppe für diese Sitzung lautet **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.</span><span class="sxs-lookup"><span data-stu-id="435ea-151">Your resource group for this session is **<rgn>[sandbox resource group name]</rgn>**.</span></span>

## <a name="deploy-the-dsvm-to-your-resource-group"></a><span data-ttu-id="435ea-152">Bereitstellen der DSVM für Ihre Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="435ea-152">Deploy the DSVM to your resource group</span></span>

<span data-ttu-id="435ea-153">Sie verfügen jetzt über eine Ressourcengruppe und über definierte Parameter für die DSVM-Vorlage für den Resource Manager in einer Datei mit dem Namen `parameter_file.json`.</span><span class="sxs-lookup"><span data-stu-id="435ea-153">We now have a resource group and have defined parameters for the DSVM Resource Manager template in a file called `parameter_file.json`.</span></span> <span data-ttu-id="435ea-154">In diesem Beispiel wird als nächstes `az group deployment create` zum Bereitstellen unseres virtuellen Computers ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="435ea-154">We'll run the `az group deployment create` next to provision our virtual machine.</span></span>

1. <span data-ttu-id="435ea-155">Führen Sie in Azure Cloud Shell folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="435ea-155">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    az group deployment create \
    --resource-group  <rgn>[sandbox resource group name]</rgn> \
    --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json \
    --parameters parameter_file.json
    ```

    <span data-ttu-id="435ea-156">Der Befehl verwendet die Resource Manager-Vorlage und unsere Parameter, um den virtuellen Computer in der Ressourcengruppe zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="435ea-156">The command uses the Resource Manager template and our parameters to create the virtual machine in our resource group.</span></span> 

2. <span data-ttu-id="435ea-157">Die Bereitstellung des virtuellen Computers dauert einige Minuten.</span><span class="sxs-lookup"><span data-stu-id="435ea-157">Deploying a virtual machine takes a few minutes to complete.</span></span> <span data-ttu-id="435ea-158">Die Konsole zeigt beinahe ausschließlich ` - Running ..` an, bis der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="435ea-158">The console displays ` - Running ..` and not much else until the operation completes.</span></span> <span data-ttu-id="435ea-159">Wenn der Vorgang abgeschlossen ist, wird eine JSON-Antwortdatei an den Bildschirm ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="435ea-159">When the operation finishes, a JSON response is output to the screen.</span></span> <span data-ttu-id="435ea-160">Scrollen Sie in der JSON-Datei nach unten, und prüfen Sie, ob das Feld **provisioningState** den Wert *Erfolgreich* aufweist.</span><span class="sxs-lookup"><span data-stu-id="435ea-160">Scroll to the bottom of the JSON and check that the field **"provisioningState"** has the value *Succeeded*.</span></span>

    > [!TIP]
    > <span data-ttu-id="435ea-161">Wenn ein Fehler zurückgegeben wird, weil ein DNS-Datensatz bereits von einer weiteren öffentlichen IP verwendet wird, können Sie versuchen, **vmName** in `parameter_file.json` in einen anderen eindeutigen Namen zu ändern.</span><span class="sxs-lookup"><span data-stu-id="435ea-161">If you get an error stating that the DNS record is already used by another public IP, try changing **vmName** in `parameter_file.json` to another name that's unique.</span></span>

3. <span data-ttu-id="435ea-162">Führen Sie den folgenden Befehl aus, um Informationen zu der VM abzurufen. Dabei wird `<HOSTNAME>` durch den Hostnamen ersetzt, den Sie für Ihre VM definiert haben.</span><span class="sxs-lookup"><span data-stu-id="435ea-162">Execute the following command to get information about the VM, replacing `<HOSTNAME>` with the host name you defined for your VM.</span></span>

    ```azurecli
    az vm get-instance-view \
    --name <HOSTNAME> \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query instanceView.statuses[1] \
    --output table
    ```

    <span data-ttu-id="435ea-163">Dieser Befehl zeigt den Status der VM an.</span><span class="sxs-lookup"><span data-stu-id="435ea-163">This command displays the status of the VM.</span></span> <span data-ttu-id="435ea-164">Dieser sollte *Virtueller Computer wird ausgeführt* lauten.</span><span class="sxs-lookup"><span data-stu-id="435ea-164">It should say *VM running*.</span></span>

<span data-ttu-id="435ea-165">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="435ea-165">Congratulations!</span></span> <span data-ttu-id="435ea-166">Sie haben jetzt einen virtuellen Linux-Computer erstellt und bereitgestellt, der auf dem DSVM-Image basiert.</span><span class="sxs-lookup"><span data-stu-id="435ea-166">You've created and deployed a Linux VM based on the DSVM image.</span></span>

## <a name="open-the-vm-to-ssh-traffic-on-port-22"></a><span data-ttu-id="435ea-167">Öffnen der VM für SSH-Datenverkehr auf Port 22</span><span class="sxs-lookup"><span data-stu-id="435ea-167">Open the VM to ssh traffic on port 22</span></span>

<span data-ttu-id="435ea-168">Standardmäßig ist kein Port der VM geöffnet.</span><span class="sxs-lookup"><span data-stu-id="435ea-168">By default, our VM doesn't have any ports open.</span></span> <span data-ttu-id="435ea-169">Ziel ist es, eine Remoteverbindung herzustellen, einen Jupyter Notebook-Server zu starten und andere lokale Befehle auf dem Computer auszuführen.</span><span class="sxs-lookup"><span data-stu-id="435ea-169">Our goal is to connect remotely, start a Jupyter Notebook server and run other local commands on the machine.</span></span> <span data-ttu-id="435ea-170">Damit über das Secure Shell-Protokoll (SSH) eine Remoteverbindung mit der VM hergestellt werden kann, muss ein Port geöffnet werden.</span><span class="sxs-lookup"><span data-stu-id="435ea-170">To remote into the VM using the Secure Shell (SSH) protocol, we need to open a port.</span></span> <span data-ttu-id="435ea-171">Der Standardport für SSH lautet 22.</span><span class="sxs-lookup"><span data-stu-id="435ea-171">Port 22 is the default port for ssh.</span></span>  

1. <span data-ttu-id="435ea-172">Führen Sie den folgenden Befehl in Azure Cloud Shell aus. Dabei wird `<HOSTNAME>` durch den Namen ersetzt, den Sie Ihrem virtuellen Computer unter DSVM beim Einrichten gegeben haben.</span><span class="sxs-lookup"><span data-stu-id="435ea-172">Execute the following command in Azure Cloud Shell, replacing `<HOSTNAME>` wit the name you gave your DSV virtual machine during setup.</span></span> 

    ```azurecli
    az vm open-port \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 22 \
    --priority 900
    ```

<span data-ttu-id="435ea-173">Die Ausführung dieses Befehls kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="435ea-173">This command can take up to a minute to complete.</span></span> <span data-ttu-id="435ea-174">Wenn der letzte Befehl abgeschlossen wird, gibt er eine JSON-Antwort an die Befehlszeile zurück.</span><span class="sxs-lookup"><span data-stu-id="435ea-174">When the command finishes, it returns a JSON response to the command line.</span></span> <span data-ttu-id="435ea-175">Prüfen Sie, ob das Feld **provisioningState** den Wert *Erfolgreich* aufweist.</span><span class="sxs-lookup"><span data-stu-id="435ea-175">Check that the field **"provisioningState"** has the value *Succeeded*.</span></span> <span data-ttu-id="435ea-176">Sie werden in Kürze erfahren, wie Sie testen können, ob SSH funktioniert. Zunächst sollten Sie jedoch noch einen weiteren Port öffnen.</span><span class="sxs-lookup"><span data-stu-id="435ea-176">We'll test that ssh works shortly, but first let's open one more port.</span></span>

## <a name="open-the-vm-to-access-the-jupyter-notebook-server-remotely"></a><span data-ttu-id="435ea-177">Öffnen der VM, um über eine Remoteverbindung auf den Jupyter Notebook-Server zuzugreifen</span><span class="sxs-lookup"><span data-stu-id="435ea-177">Open the VM to access the Jupyter Notebook server remotely</span></span>

<span data-ttu-id="435ea-178">Wie zuvor bereits erwähnt ist das DSVM-Image bei Software, Tools und Beispielen bereits vorinstalliert. Es soll Sie bei Projekten zu Data Science, Machine Learning und Deep Learning unterstützen.</span><span class="sxs-lookup"><span data-stu-id="435ea-178">As mentioned previously, the DSVM image comes pre-installed with software, tools, and samples to help you with your data science, machine learning, and deep learning projects.</span></span> <span data-ttu-id="435ea-179">Jupyter ist zusammen mit mehreren Beispielnotebooks im Image installiert.</span><span class="sxs-lookup"><span data-stu-id="435ea-179">Jupyter is installed in the image, along with sample notebooks.</span></span> <span data-ttu-id="435ea-180">Nun soll erst ein Jupyter Notebook-Server auf der VM gestartet und dann über Ihren lokalen Computer eine Remoteverbindung mit dem Notebook-Server hergestellt werden.</span><span class="sxs-lookup"><span data-stu-id="435ea-180">We want to start a Jupyter notebook server on the VM and then remotely connect to the notebook server from our local machine.</span></span> <span data-ttu-id="435ea-181">Standardmäßig wird der Notebook-Server auf Port 8888 ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="435ea-181">By default, the notebook server runs on port 8888.</span></span> <span data-ttu-id="435ea-182">Wenn Sie über eine Remoteverbindung auf den Server zugreifen möchten, müssen Sie diesen Port auf Ihrem virtuellen Computer öffnen.</span><span class="sxs-lookup"><span data-stu-id="435ea-182">To access the server remotely, we need to open that port on our VM.</span></span> 

1. <span data-ttu-id="435ea-183">Führen Sie den folgenden Befehl in Azure Cloud Shell aus. Dabei wird `<HOSTNAME>` durch den Namen ersetzt, den Sie Ihrem virtuellen Computer unter DSVM beim Einrichten gegeben haben.</span><span class="sxs-lookup"><span data-stu-id="435ea-183">Execute the following command in Azure Cloud Shell, replacing `<HOSTNAME>` with the name you gave your DSVM virtual machine during setup.</span></span>

    ```azurecli
    az vm open-port \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 8888 \
    --priority 901
    ```

<span data-ttu-id="435ea-184">Die Ausführung dieses Befehls kann wieder einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="435ea-184">Again, this command can take up to a minute to complete.</span></span> <span data-ttu-id="435ea-185">Wenn der letzte Befehl abgeschlossen wird, gibt er eine JSON-Antwort an die Befehlszeile zurück.</span><span class="sxs-lookup"><span data-stu-id="435ea-185">When the command finishes, it returns a JSON response to the command line.</span></span> <span data-ttu-id="435ea-186">Prüfen Sie, ob das Feld **provisioningState** den Wert *Erfolgreich* aufweist.</span><span class="sxs-lookup"><span data-stu-id="435ea-186">Check that the field **"provisioningState"** has the value *Succeeded*.</span></span>  

## <a name="connect-to-the-vm-with-secure-shell-ssh"></a><span data-ttu-id="435ea-187">Herstellen einer Verbindung mit dem virtuellen Computer mit Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="435ea-187">Connect to the VM with Secure Shell (ssh)</span></span>

1. <span data-ttu-id="435ea-188">Führen Sie den folgenden Befehl in Azure Cloud Shell aus, um die öffentliche IP-Adresse der VM zu finden.</span><span class="sxs-lookup"><span data-stu-id="435ea-188">Execute the following command in Azure Cloud Shell to find the public IP address of the VM.</span></span> <span data-ttu-id="435ea-189">Ersetzen Sie `<HOSTNAME>` durch den Namen, den Sie Ihrem virtuellen Computer unter DSVM beim Einrichten gegeben haben.</span><span class="sxs-lookup"><span data-stu-id="435ea-189">Replace `<HOSTNAME>` with the name you gave your DSVM virtual machine during setup.</span></span>

    ```azurecli
    az vm list-ip-addresses \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --output table
    ```

1. <span data-ttu-id="435ea-190">Führen Sie in Cloud Shell den folgenden Befehl aus, um sich bei der VM anzumelden.</span><span class="sxs-lookup"><span data-stu-id="435ea-190">Execute the following command in the Cloud Shell to sign into the VM.</span></span> <span data-ttu-id="435ea-191">Ersetzen Sie `<USERNAME>` durch den Benutzernamen, den Sie zu Beginn dieser Übung ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="435ea-191">Replace `<USERNAME>` with the username you chose at the start of this exercise.</span></span> <span data-ttu-id="435ea-192">Ersetzen Sie `<IP>` durch den Wert aus der **PublicIPAddresses**-Spalte, den Sie im Schritt zuvor erhalten haben.</span><span class="sxs-lookup"><span data-stu-id="435ea-192">Replace `<IP>`  with the value from the **PublicIPAddresses** column of the previous step.</span></span>

    <span data-ttu-id="435ea-193">Wenn Sie z.B. den Benutzernamen *azuser* ausgewählt haben und in der Spalte PublicIPAddresses der Wert 33.165.103.23 eingetragen war, würde der Befehl wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="435ea-193">For example, if the username you chose was *azuser* and the PublicIPAddresses had a value of 33.165.103.23, then this command would read:</span></span>
    
    `ssh azuser@33.165.103.23`
    
    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 

1. <span data-ttu-id="435ea-194">Geben Sie das Kennwort des Administratorbenutzers ein, das Sie zu Beginn dieser Übung ausgewählt haben, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="435ea-194">When prompted, enter the password for the admin user you chose at the start of this exercise.</span></span> <span data-ttu-id="435ea-195">Wenn Sie sich erfolgreich angemeldet haben, sollte Ihre Aufforderung in das Format `username@hostname` wechseln, z.B. `azuser@js1982`.</span><span class="sxs-lookup"><span data-stu-id="435ea-195">When you've signed in successfully, your prompt should change to the format `username@hostname`, for example, `azuser@js1982`.</span></span>

<span data-ttu-id="435ea-196">Starten Sie in einem nächsten Schritt den Jupyter Notebook-Server auf Ihrer VM, und öffnen Sie ein Notebook über eine Remoteverbindung.</span><span class="sxs-lookup"><span data-stu-id="435ea-196">The next step is to start the Jupyter notebook server on our VM and open a notebook remotely.</span></span>

## <a name="start-the-jupyter-notebook-server-on-the-vm"></a><span data-ttu-id="435ea-197">Starten des Jupyter Notebook-Servers auf der VM</span><span class="sxs-lookup"><span data-stu-id="435ea-197">Start the Jupyter notebook server on the VM</span></span>

<span data-ttu-id="435ea-198">Sie finden im `~/notebooks`-Ordner Ihrer VM eine Reihe von Notebooks.</span><span class="sxs-lookup"><span data-stu-id="435ea-198">There's a set of notebooks in the `~/notebooks` folder of your VM.</span></span> <span data-ttu-id="435ea-199">Angenommen, Sie sind noch über eine SSH-Sitzung angemeldet. Starten Sie den Notebook-Server, und öffnen Sie eins dieser Notebooks, um zu prüfen, ob alles einwandfrei funktioniert.</span><span class="sxs-lookup"><span data-stu-id="435ea-199">Assuming you are still logged in through an SSH session,  start the notebook server and open one of these notebooks to make sure everything is working.</span></span>


1. <span data-ttu-id="435ea-200">Führen Sie über die Eingabeaufforderung Ihrer VM den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="435ea-200">Run the following command at the command prompt of your VM:</span></span>

    ```bash
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root
    ```

> [!CAUTION]
> <span data-ttu-id="435ea-201">In dieser Übung wird über `http://` auf den Notebook-Server zugegriffen.</span><span class="sxs-lookup"><span data-stu-id="435ea-201">Access to the notebook server in this exercise happens over `http://`.</span></span> <span data-ttu-id="435ea-202">Wenn Sie einen Notebook-Server öffentlich ausführen möchten, sollten Sie ihn sichern.</span><span class="sxs-lookup"><span data-stu-id="435ea-202">If you want to run a notebook server in public, you should secure it.</span></span> <span data-ttu-id="435ea-203">Weitere Informationen zum Sichern eines Notebook-Servers finden Sie in der offiziellen Onlinedokumentation zu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="435ea-203">For more information about securing a notebook server, see the official Jupyter documentation online.</span></span> 

<span data-ttu-id="435ea-204">Im folgenden Befehl wird der Jupyter Notebook-Server mit dem Befehl `jupyter notebook` gestartet.</span><span class="sxs-lookup"><span data-stu-id="435ea-204">In the preceding command, we start the Jupyter Notebook server with the `jupyter notebook` command.</span></span> <span data-ttu-id="435ea-205">Es werden drei wichtige Befehlszeilenargumente bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="435ea-205">We supply three important command-line arguments.</span></span> <span data-ttu-id="435ea-206">Bedenken Sie, dass Sie über eine Remoteverbindung mit einer Konsole bei diesem Computer angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="435ea-206">Remember, we're logged into this machine remotely through a console.</span></span> <span data-ttu-id="435ea-207">Notebooks werden über einen Browser bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="435ea-207">Notebooks are served in a browser.</span></span> 

 - <span data-ttu-id="435ea-208">`--ip=0.0.0.0` Standardmäßig werden Notebook-Server lokal über 127.0.0.1:8888 ausgeführt und sind nur über den Localhost verfügbar.</span><span class="sxs-lookup"><span data-stu-id="435ea-208">`--ip=0.0.0.0` By default, a notebook server runs locally at 127.0.0.1:8888 and is accessible only from localhost.</span></span> <span data-ttu-id="435ea-209">Sie können den Notebook-Server lokal mithilfe von http://127.0.0.1:8888 über den Browser ausführen.</span><span class="sxs-lookup"><span data-stu-id="435ea-209">You can access the notebook server from the browser locally using http://127.0.0.1:8888.</span></span> <span data-ttu-id="435ea-210">Wenn die IP-Adresse auf 0.0.0.0 festgelegt ist, überwacht der Server den Datenverkehr auf allen IPs.</span><span class="sxs-lookup"><span data-stu-id="435ea-210">Setting the IP Address to 0.0.0.0 tells the server to listen for traffic on all IPs.</span></span> <span data-ttu-id="435ea-211">Wenn der Notebook-Server 0.0.0.0 überwacht, kann über die IP-Adresse des Hostcomputers auf ihn zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="435ea-211">If the notebook server listens on 0.0.0.0, it will be reachable through the IP address of the host machine.</span></span>  
 - <span data-ttu-id="435ea-212">`--no-browser` Da Sie über einen anderen Computer über das Internet eine Verbindung zu dem Notebook-Server herstellen möchten, wird der Server so konfiguriert, dass er nicht den Browser öffnet. Dies wäre das Standardverhalten.</span><span class="sxs-lookup"><span data-stu-id="435ea-212">`--no-browser`  Because we want to connect to the notebook from another computer over the internet, we configure the notebook server to not open the browser, which is the default behavior.</span></span> 
 - <span data-ttu-id="435ea-213">`--allow-root` In dieser Übung gibt es nur ein Administratorkonto für die VM. Daher kann kein Notebooks als Stamm verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="435ea-213">`--allow-root`  In this exercise, we only have an admin account on the VM, so  we want to be able to run notebooks as root.</span></span>

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a><span data-ttu-id="435ea-214">Herstellen einer Verbindung mit dem Jupyter Notebook-Server über einen Remotebrowser</span><span class="sxs-lookup"><span data-stu-id="435ea-214">Connect to the Jupyter Notebook server from a remote browser</span></span>

<span data-ttu-id="435ea-215">Wenn der obenstehende Befehl auf der VM ausgeführt wird, startet der Notebook-Server, und die Konsole zeigt eine URL an, die Sie in einem Browser verwenden können.</span><span class="sxs-lookup"><span data-stu-id="435ea-215">When the above command runs on the VM, the notebook server starts and the console displays a URL for you to use in a browser.</span></span> 

![Screenshot: Meldung, die ein Notebook-Server, der gerade ausgeführt wird, in der Konsole anzeigt, inklusive der URL, über die über einen Hostcomputer auf den Server zugegriffen werden kann](../media/notebook-url.png)

1. <span data-ttu-id="435ea-217">Kopieren Sie die URL, die der Notebook-Server in der Adressleiste des von Ihnen bevorzugten Browsers anzeigt.</span><span class="sxs-lookup"><span data-stu-id="435ea-217">Copy the URL the notebook server displays into the address bar of your favorite browser.</span></span> <span data-ttu-id="435ea-218">Sie können auch auf die URL klicken. Dann wird der Server in Ihrem Standardbrowser geöffnet.</span><span class="sxs-lookup"><span data-stu-id="435ea-218">You can also click on the URL to open in your default browser.</span></span> 

    <span data-ttu-id="435ea-219">Sie erhalten dann die Meldung "Site can't be reached" (Website nicht erreichbar.), da die bereitgestellte URL die Verbindung mit dem Notebook-Server über den Hostcomputer darstellt.</span><span class="sxs-lookup"><span data-stu-id="435ea-219">You will receive a "Site can't be reached" message because the URL you were given is the connection to the notebook server from the host machine.</span></span>

1. <span data-ttu-id="435ea-220">Damit Sie über eine Remoteverbindung auf den Server zugreifen können, ersetzen Sie den Hostnamen in der URL durch die IP-Adresse der zuvor gespeicherten VM.</span><span class="sxs-lookup"><span data-stu-id="435ea-220">To access the server remotely,  replace the hostname in the URL with the IP address of the VM you saved earlier.</span></span> 

    <span data-ttu-id="435ea-221">Nachfolgend sehen Sie eine Beispiel-URL eines Notebook-Servers.</span><span class="sxs-lookup"><span data-stu-id="435ea-221">Here's a sample notebook server URL.</span></span>

    <span data-ttu-id="435ea-222">"http://**ab-dsvm-4**:8888/?token={beliebiges Token}"</span><span class="sxs-lookup"><span data-stu-id="435ea-222">"http://**ab-dsvm-4**:8888/?token={some token}"</span></span>

    <span data-ttu-id="435ea-223">In diesem Fall muss **ab-dsvm-4** durch die IP-Adresse des Computers ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="435ea-223">In this case, we would replace **ab-dsvm-4** with IP address of the machine.</span></span> <span data-ttu-id="435ea-224">Wenn die IP-Adresse `52.175.199.43` lautet, lautet die URL wie folgt:</span><span class="sxs-lookup"><span data-stu-id="435ea-224">If our IP address is `52.175.199.43`, then the URL becomes:</span></span>

    <span data-ttu-id="435ea-225">"http://**52.175.199.43**:8888/?token={beliebiges Token}"</span><span class="sxs-lookup"><span data-stu-id="435ea-225">"http://**52.175.199.43**:8888/?token={some token}"</span></span>

    <span data-ttu-id="435ea-226">Vergewissern Sie sich, dass `:8888`, die Portadresse, in der URL bleibt.</span><span class="sxs-lookup"><span data-stu-id="435ea-226">Make sure `:8888`, the port address, is kept in the URL.</span></span>

    > [!TIP]
    > <span data-ttu-id="435ea-227">Wenn Sie nicht die IP-Adresse verwenden möchten, können Sie auch den vollqualifizierten Namen des Servers verwenden, der das Format `<HOST NAME>.<REGION>.cloudapp.azure.com` aufweist.</span><span class="sxs-lookup"><span data-stu-id="435ea-227">If you don't want to use the IP address, you can also use the fully qualified name of your server which is in the form `<HOST NAME>.<REGION>.cloudapp.azure.com`</span></span>

    <span data-ttu-id="435ea-228">Auf dem folgenden Screenshot sehen Sie, wie das Jupyter-Dashboard in Ihrem Browser aussieht.</span><span class="sxs-lookup"><span data-stu-id="435ea-228">The following  screenshot shows what the Jupyter dashboard looks like in your browser.</span></span>

    ![<span data-ttu-id="435ea-229">Screenshot des Jupyter Notebook-Dashboards</span><span class="sxs-lookup"><span data-stu-id="435ea-229">Screenshot showing Jupyter Notebooks dashboard.</span></span> ](../media/jupyter-in-browser.png)

1. <span data-ttu-id="435ea-230">Navigieren Sie zu **notebooks/IntroToJupyterPython.ipynb**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="435ea-230">Navigate to **notebooks/IntroToJupyterPython.ipynb** and select it.</span></span> <span data-ttu-id="435ea-231">Testen Sie dieses Notebook, um zu prüfen, ob alles einwandfrei funktioniert.</span><span class="sxs-lookup"><span data-stu-id="435ea-231">Try out this notebook to verify everythin  works as expected.</span></span>

    <span data-ttu-id="435ea-232">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="435ea-232">Congratulations!</span></span> <span data-ttu-id="435ea-233">Sie verfügen jetzt über einen virtuellen Computer, der auf DSVM basiert, und können über eine Remoteverbindung mit Jupyter arbeiten.</span><span class="sxs-lookup"><span data-stu-id="435ea-233">You now have a running DSVM-based virtual machine running and can work remotely with Jupyter.</span></span> <span data-ttu-id="435ea-234">In dieser Übung wird die Software ausgeführt, die auf der VM installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="435ea-234">In this exercise, we're running the software that was installed on the VM.</span></span> <span data-ttu-id="435ea-235">In der nächsten Übung wird die Software in einem Container auf der VM isoliert, sodass Sie ohne Sorge experimentieren können.</span><span class="sxs-lookup"><span data-stu-id="435ea-235">In the next exercise, we'll isolate the software in a container on the VM so we can experiment with confidence.</span></span>

4. <span data-ttu-id="435ea-236">Wenn Sie das Notebook nicht mehr benötigen, können Sie den Jupyter-Server mit `Control-C` in der Cloud Shell anhalten.</span><span class="sxs-lookup"><span data-stu-id="435ea-236">When you have finished with the notebook, you can stop the Jupyter server with `Control-C` in the Cloud Shell.</span></span>
