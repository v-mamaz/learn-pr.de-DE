<span data-ttu-id="aeaa8-101">Für den MEAN-Komponentenstapel wird ein Server benötigt.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-101">The MEAN stack of components requires a server.</span></span> <span data-ttu-id="aeaa8-102">Sie können entweder einen Linux-Computer oder einen virtuellen Computer aus Ihrem eigenen Serverbestand verwenden, oder die Konfiguration erfolgt auf einem cloudbasierten virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-102">It could be a Linux machine or virtual machine running in your own server room, or it can be configured on a cloud-based virtual machine.</span></span> <span data-ttu-id="aeaa8-103">In diesem Modul richten wir den Stapel zur Ausführung auf einem virtuellen Ubuntu Linux-Computer ein, der in Azure ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-103">In this module, we will set up the stack to run on an Ubuntu Linux virtual machine running on Azure.</span></span>

<span data-ttu-id="aeaa8-104">In dieser Übung erstellen Sie einen neuen virtuellen Ubuntu Linux-Computer, der in Azure gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-104">In this exercise, you will be creating a new Ubuntu Linux virtual machine hosted on Azure.</span></span> <span data-ttu-id="aeaa8-105">Sie könnten Ihre MEAN-Stapelkomponenten auch auf einer vorhandenen VM oder auf einem physischen Hostcomputer installieren.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-105">You could also install your MEAN stack components on an existing virtual machine or physical host machine.</span></span> <span data-ttu-id="aeaa8-106">Durch das Erstellen eines neuen virtuellen Computers in dieser Übung können Sie alle Komponenten in einer Azure-Ressourcengruppe zusammenfassen. Dies vereinfacht die Verwaltung und die Bereinigung nach Abschluss der Übung.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-106">By creating a new one with this exercise, you can tie together all the components into an Azure resource group for easier management and clean-up after you complete the exercises.</span></span>

<span data-ttu-id="aeaa8-107">Wir verwenden die im Azure-Portal integrierte Cloud Shell-Befehlszeile, um die Linux-VM zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-107">We will use the Cloud Shell command line that's integrated into the Azure portal to create the Linux VM.</span></span>

## <a name="provision-an-ubuntu-linux-vm"></a><span data-ttu-id="aeaa8-108">Bereitstellen eines virtuellen Ubuntu Linux-Computers</span><span class="sxs-lookup"><span data-stu-id="aeaa8-108">Provision an Ubuntu Linux VM</span></span>

1. <span data-ttu-id="aeaa8-109">Öffnen Sie das [Azure-Portal](https://portal.azure.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="aeaa8-109">Go to the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>
1. <span data-ttu-id="aeaa8-110">Öffnen Sie Cloud Shell über das Symbol „>_“ in der Symbolleiste des Azure-Portals.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-110">Open Cloud Shell from the angle bracket (>_) icon in the Azure portal toolbar.</span></span>
1. <span data-ttu-id="aeaa8-111">Führen Sie in Cloud Shell den Befehl zum Erstellen einer Azure-Ressourcengruppe aus, was unseren virtuellen Computer einschließt.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-111">In Cloud Shell, execute the command to create an Azure resource group, which will include our VM.</span></span> <span data-ttu-id="aeaa8-112">Ersetzen Sie `<resource-group-name>` durch den Namen Ihrer eigenen Ressourcengruppe und `<resource-group-location>` durch den gewünschten Azure-Standort (z.B. `westus`).</span><span class="sxs-lookup"><span data-stu-id="aeaa8-112">Substitute your own resource group name for `<resource-group-name>` and your desired Azure location for `<resource-group-location>` (`westus`, for example).</span></span>


    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    <span data-ttu-id="aeaa8-113">Merken Sie sich den Namen Ihrer Ressourcengruppe, weil wir diesen in weiteren Befehlen verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-113">Remember your resource group name as we will use it in other commands.</span></span>

1. <span data-ttu-id="aeaa8-114">Führen Sie in Cloud Shell den folgenden Befehl aus, um einen neuen virtuellen Ubuntu Linux-Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-114">In Cloud Shell, run the following command to create a new Ubuntu Linux VM.</span></span> <span data-ttu-id="aeaa8-115">Ersetzen Sie `<resource-group-name>` durch den Namen Ihrer eigenen Ressourcengruppe und `<vm-admin-username>` und `<vm-admin-password>` durch den bevorzugten Administratornamen sowie das zugehörige Kennwort.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-115">Substitute your own resource group name for `<resource-group-name>` and your preferred admin username and password for `<vm-admin-username>` and `<vm-admin-password>`.</span></span>

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    <span data-ttu-id="aeaa8-116">Notieren Sie sich Ihren Administratornamen und das zugehörige Kennwort, um später eine Verbindung mit diesem virtuellen Computer herstellen zu können.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-116">Take note of your admin username and password to allow you to connect to this VM later.</span></span>

    <span data-ttu-id="aeaa8-117">Die Ausführung dieses Befehls dauert ungefähr zwei Minuten.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-117">This command takes about two minutes to complete.</span></span> <span data-ttu-id="aeaa8-118">Nach Abschluss der Befehlsausführung sieht die resultierende Ausgabe in etwa so aus:</span><span class="sxs-lookup"><span data-stu-id="aeaa8-118">When the command finishes, the resulting output will look similar to this.</span></span>

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<location you chose for the resource group>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<name you chose for thr resource group>",
        "zones": ""
    }
    ```

    <span data-ttu-id="aeaa8-119">Sie sollten sich für die Verbindungsherstellung mit der VM auch die öffentliche IP-Adresse der neu erstellten VM notieren.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-119">You will also want to save the public IP address of the newly created VM in order to connect to the VM.</span></span>

1. <span data-ttu-id="aeaa8-120">Versuchen Sie, eine Verbindung mit Ihrer neuen VM herzustellen.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-120">Try connecting to your new VM.</span></span>

    <span data-ttu-id="aeaa8-121">Öffnen Sie eine Eingabeaufforderung/ein Terminalfenster, und führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-121">Open a command prompt/terminal window and run the following command.</span></span> <span data-ttu-id="aeaa8-122">Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der VM von oben.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-122">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    <span data-ttu-id="aeaa8-123">Bei der ersten Verbindungsherstellung mit dem Computer werden Sie gefragt, ob Sie den Remotecomputer als vertrauenswürdig einstufen.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-123">The first time you connect to the machine, you'll be asked if you trust the remote machine.</span></span> <span data-ttu-id="aeaa8-124">Wenn Sie `yes` eingeben, wird der ECDSA-Fingerabdruck lokal gespeichert, damit nachfolgende Verbindungen als vertrauenswürdig eingestuft werden.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-124">By answering `yes`, the machine's ECDSA key fingerprint will be saved locally, so subsequent connections will be trusted.</span></span>

    <span data-ttu-id="aeaa8-125">Wenn alles gut aussieht, geben Sie `exit` ein, um die SSH-Sitzung zu schließen.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-125">If everything looks fine, type `exit` to close the SSH session.</span></span>

1. <span data-ttu-id="aeaa8-126">Öffnen Sie Port 80, um eingehenden HTTP-Datenverkehr an die neue Webanwendung zuzulassen, die Sie erstellen werden.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-126">Open port 80 to allow incoming HTTP traffic to your new web application that you will create.</span></span>

    <span data-ttu-id="aeaa8-127">Gehen Sie im Azure-Portal zurück zu Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-127">Go back to Cloud Shell on the Azure portal.</span></span> <span data-ttu-id="aeaa8-128">Geben Sie den folgenden Befehl ein, indem Sie Ihren ursprünglichen Ressourcengruppenname für `<resource-group-name>` verwenden.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-128">Issue the following command using your original resource group name for `<resource-group-name>`.</span></span>

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    <span data-ttu-id="aeaa8-129">Durch diesen Befehl wird der HTTP-Port auf Ihrem virtuellen Computer geöffnet, der mit dem Namen „MeanDemo“ erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-129">This command will open up the HTTP port on your VM that was named "MeanDemo" when it was created.</span></span>

## <a name="summary"></a><span data-ttu-id="aeaa8-130">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="aeaa8-130">Summary</span></span>

<span data-ttu-id="aeaa8-131">Mit der neu erstellten Ubuntu Linux-VM ist es jetzt möglich, eine Verbindung herzustellen, um die verschiedenen Komponenten des MEAN-Stapels zu installieren.</span><span class="sxs-lookup"><span data-stu-id="aeaa8-131">With your new Ubuntu Linux VM ready to go, we can now connect to it to start installing the various components of the MEAN stack.</span></span>