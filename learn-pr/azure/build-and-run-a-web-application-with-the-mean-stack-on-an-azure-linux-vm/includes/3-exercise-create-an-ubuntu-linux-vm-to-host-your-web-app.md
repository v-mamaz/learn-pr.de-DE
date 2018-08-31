<span data-ttu-id="cd24e-101">Für den MEAN-Komponentenstapel wird ein Server benötigt.</span><span class="sxs-lookup"><span data-stu-id="cd24e-101">The MEAN stack of components requires a server.</span></span> <span data-ttu-id="cd24e-102">Sie können entweder einen Linux-Computer oder einen virtuellen Computer aus Ihrem eigenen Serverbestand verwenden, oder die Konfiguration erfolgt auf einer cloudbasierten VM.</span><span class="sxs-lookup"><span data-stu-id="cd24e-102">It could be a Linux machine or virtual machine running in your own server room, or it can be configured on a cloud-based virtual machine.</span></span> <span data-ttu-id="cd24e-103">In diesem Modul richten wir den Stapel zur Ausführung auf einer Ubuntu Linux-VM ein, die in Azure ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="cd24e-103">In this module, we will be setting up the stack to run on an Ubuntu Linux virtual machine running on Azure.</span></span>

<span data-ttu-id="cd24e-104">In dieser Übung erstellen Sie eine neue Ubuntu Linux-VM, die in Azure gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="cd24e-104">In this exercise, you will be creating a new Ubuntu Linux virtual machine hosted on Azure.</span></span> <span data-ttu-id="cd24e-105">Sie könnten Ihre MEAN-Stapelkomponenten auch auf einer vorhandenen VM oder auf einem physischen Hostcomputer installieren.</span><span class="sxs-lookup"><span data-stu-id="cd24e-105">You could also install your MEAN stack components on an existing virtual machine or physical host machine.</span></span> <span data-ttu-id="cd24e-106">Durch das Erstellen einer neuen VM in dieser Übung können Sie alle Komponenten in einer Azure-Ressourcengruppe zusammenfassen. Dies vereinfacht die Verwaltung und die Bereinigung nach Abschluss der Übung.</span><span class="sxs-lookup"><span data-stu-id="cd24e-106">By creating a new one with this exercise, you can tie together all the components into an Azure resource group for easier management and clean-up after you complete the exercises.</span></span>

<span data-ttu-id="cd24e-107">Wir verwenden die im Azure-Portal integrierte Cloud Shell-Befehlszeile, um die Linux-VM zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cd24e-107">We will use the Cloud Shell command-line integrated into the Azure portal to create the Linux VM.</span></span>

## <a name="provision-an-ubuntu-linux-vm"></a><span data-ttu-id="cd24e-108">Bereitstellen einer Ubuntu Linux-VM</span><span class="sxs-lookup"><span data-stu-id="cd24e-108">Provision an Ubuntu Linux VM</span></span>

1. <span data-ttu-id="cd24e-109">Wechseln Sie zum [Azure-Portal](https://portal.azure.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="cd24e-109">Go to the [Azure Portal](https://portal.azure.com?azure-portal=true).</span></span>
1. <span data-ttu-id="cd24e-110">Öffnen Sie die Cloud Shell-Befehlszeile über das Symbol `>_` in der Symbolleiste des Azure-Portals.</span><span class="sxs-lookup"><span data-stu-id="cd24e-110">Open the Cloud Shell from the `>_` icon in the Azure portal toolbar.</span></span>
1. <span data-ttu-id="cd24e-111">Führen Sie in der Cloud Shell-Befehlszeile den Befehl zum Erstellen einer Azure-Ressourcengruppe aus, dies schließt unsere VM ein.</span><span class="sxs-lookup"><span data-stu-id="cd24e-111">Within the Cloud Shell, execute the command to create an Azure resource group, which will include our VM.</span></span> <span data-ttu-id="cd24e-112">Ersetzen Sie `<resource-group-name>` durch den Namen Ihrer eigenen Ressourcengruppe und `<resource-group-location>` durch den gewünschten Azure-Standort (z.B. `westus`).</span><span class="sxs-lookup"><span data-stu-id="cd24e-112">Substitute your own resource group name for `<resource-group-name>` and your desired Azure location for `<resource-group-location>` (`westus`, for example).</span></span>

    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    <span data-ttu-id="cd24e-113">Merken Sie sich den Namen Ihrer Ressourcengruppe, weil wir diesen in weiteren Befehlen verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="cd24e-113">Remember your resource group name as we will use it in other commands.</span></span>

1. <span data-ttu-id="cd24e-114">Führen Sie in der Cloud Shell-Befehlszeile den folgenden Befehl aus, um eine neue Ubuntu Linux-VM zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="cd24e-114">In the Cloud Shell, run the following command to create a new Ubuntu Linux VM.</span></span> <span data-ttu-id="cd24e-115">Ersetzen Sie `<resource-group-name>` durch den Namen Ihrer eigenen Ressourcengruppe und `<vm-admin-username>` und `<vm-admin-password>` durch den bevorzugten Administratornamen sowie das zugehörige Kennwort.</span><span class="sxs-lookup"><span data-stu-id="cd24e-115">Substitute your own resource group name for `<resource-group-name>` and your preferred admin username and password for `<vm-admin-username>` and `<vm-admin-password>`.</span></span>

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    <span data-ttu-id="cd24e-116">Notieren Sie sich Ihren Administratornamen und das zugehörige Kennwort, um später eine Verbindung mit dieser VM herstellen zu können.</span><span class="sxs-lookup"><span data-stu-id="cd24e-116">Take note of your admin username and password to allow you to connect to this VM later.</span></span>

    <span data-ttu-id="cd24e-117">Die Ausführung dieses Befehls dauert ungefähr 2 Minuten.</span><span class="sxs-lookup"><span data-stu-id="cd24e-117">This command takes about 2 minutes to complete.</span></span> <span data-ttu-id="cd24e-118">Nach Abschluss der Befehlsausführung sieht die resultierende Ausgabe in etwa so aus:</span><span class="sxs-lookup"><span data-stu-id="cd24e-118">When the command finishes, the resulting output will look similar to this.</span></span>

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

    <span data-ttu-id="cd24e-119">Sie sollten sich für die Verbindungsherstellung mit der VM auch die öffentliche IP-Adresse der neu erstellten VM notieren.</span><span class="sxs-lookup"><span data-stu-id="cd24e-119">You will also want to save the public IP address of the newly created VM in order to connect to the VM.</span></span>

1. <span data-ttu-id="cd24e-120">Versuchen Sie, eine Verbindung mit Ihrer neuen VM herzustellen.</span><span class="sxs-lookup"><span data-stu-id="cd24e-120">Try connecting to your new VM.</span></span>

    <span data-ttu-id="cd24e-121">Öffnen Sie eine Eingabeaufforderung/ein Terminalfenster, und führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="cd24e-121">Open a command prompt/terminal window and run the following command.</span></span> <span data-ttu-id="cd24e-122">Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der VM von oben.</span><span class="sxs-lookup"><span data-stu-id="cd24e-122">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    <span data-ttu-id="cd24e-123">Bei der ersten Verbindungsherstellung mit der VM werden Sie gefragt, ob Sie den Remotecomputer als vertrauenswürdig einstufen.</span><span class="sxs-lookup"><span data-stu-id="cd24e-123">The first time you connect to the machine, you'll be asked if you trust the remote machine.</span></span> <span data-ttu-id="cd24e-124">Wenn Sie `yes` eingeben, wird der ECDSA-Fingerabdruck lokal gespeichert, damit nachfolgende Verbindungen als vertrauenswürdig eingestuft werden.</span><span class="sxs-lookup"><span data-stu-id="cd24e-124">By answering `yes`, the machine's ECDSA key fingerprint will be saved locally so subsequent connections will be trusted.</span></span>

    <span data-ttu-id="cd24e-125">Wenn alles gut aussieht, geben Sie `exit` ein, um die SSH-Sitzung zu schließen.</span><span class="sxs-lookup"><span data-stu-id="cd24e-125">If everything looks fine, type `exit` to close the SSH session.</span></span>

1. <span data-ttu-id="cd24e-126">Öffnen Sie Port 80, um eingehenden HTTP-Datenverkehr an die neue Webanwendung zuzulassen, die Sie erstellen werden.</span><span class="sxs-lookup"><span data-stu-id="cd24e-126">Open port 80 to allow incoming HTTP traffic to your new web application you will create.</span></span>

    <span data-ttu-id="cd24e-127">Wechseln Sie zurück zur Cloud Shell-Befehlszeile im Azure-Portal, und führen Sie den folgenden Befehl aus. Verwenden Sie hierbei Ihren ursprünglichen Ressourcengruppennamen für `<resource-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="cd24e-127">Go back to the Cloud Shell on the Azure portal and issue the following command, using your original resource group name for `<resource-group-name>`.</span></span>

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    <span data-ttu-id="cd24e-128">Hierdurch wird der HTTP-Port auf Ihrer VM geöffnet, die mit dem Namen „MeanDemo“ erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="cd24e-128">This will open up the HTTP port on your VM that was named "MeanDemo" when it was created.</span></span>

## <a name="summary"></a><span data-ttu-id="cd24e-129">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="cd24e-129">Summary</span></span>

<span data-ttu-id="cd24e-130">Mit der neu erstellten Ubuntu Linux-VM ist es jetzt möglich, eine Verbindung herzustellen, um die verschiedenen Komponenten des MEAN-Stapels zu installieren.</span><span class="sxs-lookup"><span data-stu-id="cd24e-130">With your new Ubuntu Linux VM ready to go, we can now connect to it to start installing the various components of the MEAN stack.</span></span>
