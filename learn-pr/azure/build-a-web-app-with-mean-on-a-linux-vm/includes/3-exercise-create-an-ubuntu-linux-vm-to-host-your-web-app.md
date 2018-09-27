<span data-ttu-id="12032-101">Für den MEAN-Komponentenstapel wird ein Server benötigt.</span><span class="sxs-lookup"><span data-stu-id="12032-101">The MEAN stack of components requires a server.</span></span> <span data-ttu-id="12032-102">Sie können entweder einen Linux-Computer oder einen virtuellen Computer aus Ihrem eigenen Serverbestand verwenden, oder die Konfiguration erfolgt auf einem cloudbasierten virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="12032-102">It could be a Linux machine or virtual machine running in your own server room, or it can be configured on a cloud-based virtual machine.</span></span> <span data-ttu-id="12032-103">In diesem Modul richten wir den Stapel zur Ausführung auf einem virtuellen Ubuntu Linux-Computer ein, der in Azure ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="12032-103">In this module, we will set up the stack to run on an Ubuntu Linux virtual machine running on Azure.</span></span>

<span data-ttu-id="12032-104">In dieser Einheit erstellen Sie einen neuen virtuellen Ubuntu Linux-Computer, der in Azure gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="12032-104">In this unit, you will be creating a new Ubuntu Linux virtual machine hosted on Azure.</span></span> <span data-ttu-id="12032-105">Sie könnten Ihre MEAN-Stapelkomponenten auch auf einer vorhandenen VM oder auf einem physischen Hostcomputer installieren.</span><span class="sxs-lookup"><span data-stu-id="12032-105">You could also install your MEAN stack components on an existing virtual machine or physical host machine.</span></span> <span data-ttu-id="12032-106">Durch das Erstellen eines neuen virtuellen Computers in dieser Übung können Sie alle Komponenten in einer Azure-Ressourcengruppe zusammenfassen. Dies vereinfacht die Verwaltung und die Bereinigung nach Abschluss der Übung.</span><span class="sxs-lookup"><span data-stu-id="12032-106">By creating a new one with this exercise, you can tie together all the components into an Azure resource group for easier management and clean-up after you complete the exercises.</span></span>

## <a name="provision-an-ubuntu-linux-vm"></a><span data-ttu-id="12032-107">Bereitstellen eines virtuellen Ubuntu Linux-Computers</span><span class="sxs-lookup"><span data-stu-id="12032-107">Provision an Ubuntu Linux VM</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="creating-a-resource-group"></a><span data-ttu-id="12032-108">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="12032-108">Creating a resource group</span></span>

<span data-ttu-id="12032-109">Wenn Sie neue Ressourcen erstellen, erstellen Sie in der Regel zuerst eine _Ressourcengruppe_, um alle Ressourcen zu besitzen.</span><span class="sxs-lookup"><span data-stu-id="12032-109">Normally, the first thing you'll do when creating a new set of resources is create a _resource group_ to own them all.</span></span> <span data-ttu-id="12032-110">Dieser Schritt ist in der Azure-Sandbox überflüssig, aber wenn Sie in Ihrem eigenen Abonnement arbeiten, erstellen Sie mit dem folgenden Befehl eine Ressourcengruppe an einem Standort in Ihrer Nähe.</span><span class="sxs-lookup"><span data-stu-id="12032-110">This is an unnecessary step in the Azure sandbox, but when you are working in your own subscription use the following command to create a resource group in a location near you.</span></span>

```azurecli
az group create --name <resource-group-name> --location <resource-group-location>
```

> [!IMPORTANT]
> <span data-ttu-id="12032-111">In der Azure-Sandbox müssen Sie keine Ressourcengruppe erstellen.</span><span class="sxs-lookup"><span data-stu-id="12032-111">You do not need to create a resource group with the Azure sandbox.</span></span> <span data-ttu-id="12032-112">Verwenden Sie stattdessen die vorab erstellte Ressourcengruppe mit dem Namen **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.</span><span class="sxs-lookup"><span data-stu-id="12032-112">Instead use the pre-created resource group named **<rgn>[sandbox Resource Group]</rgn>**.</span></span>

1. <span data-ttu-id="12032-113">Führen Sie in der Cloud Shell rechts den folgenden Befehl aus, um eine neue Ubuntu Linux-VM zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="12032-113">In the Cloud Shell on the right, type the following command to create a new Ubuntu Linux VM.</span></span> <span data-ttu-id="12032-114">Ersetzen Sie `<vm-admin-username>` und `<vm-admin-password>` durch Ihren bevorzugten Administratornamen sowie das zugehörige Kennwort.</span><span class="sxs-lookup"><span data-stu-id="12032-114">Substitute your preferred admin username and password for `<vm-admin-username>` and `<vm-admin-password>`.</span></span>

    ```azurecli
    az vm create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    <span data-ttu-id="12032-115">Notieren Sie sich Ihren Administratornamen und das zugehörige Kennwort, um später eine Verbindung mit diesem virtuellen Computer herstellen zu können.</span><span class="sxs-lookup"><span data-stu-id="12032-115">Take note of your admin username and password to allow you to connect to this VM later.</span></span>

    <span data-ttu-id="12032-116">Die Ausführung dieses Befehls dauert ungefähr zwei Minuten.</span><span class="sxs-lookup"><span data-stu-id="12032-116">This command takes about two minutes to complete.</span></span> <span data-ttu-id="12032-117">Nach Abschluss der Befehlsausführung sieht die resultierende Ausgabe in etwa so aus:</span><span class="sxs-lookup"><span data-stu-id="12032-117">When the command finishes, the resulting output will look similar to this.</span></span>

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<resource group location>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<rgn>[sandbox resource group name]</rgn>",
        "zones": ""
    }
    ```

    <span data-ttu-id="12032-118">Sie sollten sich für die Verbindungsherstellung mit der VM auch die öffentliche IP-Adresse der neu erstellten VM notieren.</span><span class="sxs-lookup"><span data-stu-id="12032-118">You will also want to save the public IP address of the newly created VM in order to connect to the VM.</span></span>

1. <span data-ttu-id="12032-119">Versuchen Sie, eine Verbindung mit Ihrer neuen VM herzustellen.</span><span class="sxs-lookup"><span data-stu-id="12032-119">Try connecting to your new VM.</span></span>

    <span data-ttu-id="12032-120">Führen Sie in der Cloud Shell den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="12032-120">From the Cloud Shell, run the following command.</span></span> <span data-ttu-id="12032-121">Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der zuvor erwähnten VM.</span><span class="sxs-lookup"><span data-stu-id="12032-121">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    <span data-ttu-id="12032-122">Bei der ersten Verbindungsherstellung mit dem Computer werden Sie gefragt, ob Sie den Remotecomputer als vertrauenswürdig einstufen.</span><span class="sxs-lookup"><span data-stu-id="12032-122">The first time you connect to the machine, you'll be asked if you trust the remote machine.</span></span> <span data-ttu-id="12032-123">Wenn Sie `yes` eingeben, wird der ECDSA-Fingerabdruck lokal gespeichert, damit nachfolgende Verbindungen als vertrauenswürdig eingestuft werden.</span><span class="sxs-lookup"><span data-stu-id="12032-123">By answering `yes`, the machine's ECDSA key fingerprint will be saved locally, so subsequent connections will be trusted.</span></span> <span data-ttu-id="12032-124">Sie werden dann zur Eingabe Ihres Kennworts aufgefordert. Diese Eingabeaufforderung wird jedes Mal angezeigt, wenn Sie eine Verbindung herstellen.</span><span class="sxs-lookup"><span data-stu-id="12032-124">You'll then be prompted for your password, which you'll see every time you connect.</span></span>

    <span data-ttu-id="12032-125">Wenn alles gut aussieht, geben Sie `exit` ein, um die SSH-Sitzung zu schließen.</span><span class="sxs-lookup"><span data-stu-id="12032-125">If everything looks fine, type `exit` to close the SSH session.</span></span>

1. <span data-ttu-id="12032-126">Öffnen Sie Port 80 auf der VM, um bei der neuen Webanwendung, die Sie erstellen werden, eingehenden HTTP-Datenverkehr zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="12032-126">Open port 80 on the VM to allow incoming HTTP traffic to the new web application that you will create.</span></span>

    ```azurecli
    az vm open-port --port 80 --resource-group <rgn>[sandbox resource group name]</rgn> --name MeanDemo
    ```

    <span data-ttu-id="12032-127">Durch diesen Befehl wird der HTTP-Port auf Ihrem virtuellen Computer geöffnet, der mit dem Namen „MeanDemo“ erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="12032-127">This command will open up the HTTP port on your VM that was named "MeanDemo" when it was created.</span></span>

## <a name="summary"></a><span data-ttu-id="12032-128">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="12032-128">Summary</span></span>

<span data-ttu-id="12032-129">Mit der neu erstellten Ubuntu Linux-VM ist es jetzt möglich, eine Verbindung herzustellen, um die verschiedenen Komponenten des MEAN-Stapels zu installieren.</span><span class="sxs-lookup"><span data-stu-id="12032-129">With your new Ubuntu Linux VM ready to go, we can now connect to it to start installing the various components of the MEAN stack.</span></span>