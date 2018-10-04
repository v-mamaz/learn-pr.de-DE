<span data-ttu-id="5f985-101">Da Ihre Data Science Virtual Machine jetzt betriebsbereit ist und ausgeführt wird, entscheiden Sie sich, Ihr erstes Deep Learning-Modell zu trainieren.</span><span class="sxs-lookup"><span data-stu-id="5f985-101">Now that you have your Data Science Virtual Machine up and running, you decide to train your first deep learning model.</span></span> <span data-ttu-id="5f985-102">Sie möchten Ihre Experimente isoliert von allen anderen Prozessen auf Ihrem Server ausführen.</span><span class="sxs-lookup"><span data-stu-id="5f985-102">You want to run your experiments in isolation from everything else on your server.</span></span> <span data-ttu-id="5f985-103">Zu diesem Zweck führen Sie sie in einem Docker-Container aus.</span><span class="sxs-lookup"><span data-stu-id="5f985-103">To do that, you run them within a Docker container.</span></span>

## <a name="connect-to-the-vm-with-ssh"></a><span data-ttu-id="5f985-104">Herstellen einer Verbindung mit dem virtuellen Computer mit ssh</span><span class="sxs-lookup"><span data-stu-id="5f985-104">Connect to the VM with ssh</span></span>

<span data-ttu-id="5f985-105">Stellen Sie sicher, dass Sie noch immer mit Ihrem virtuellen Computer über ssh verbunden sind.</span><span class="sxs-lookup"><span data-stu-id="5f985-105">Make sure you're still connected to your VM through ssh.</span></span> <span data-ttu-id="5f985-106">Wenn dies nicht der Fall ist, führen Sie diesen Befehl einfach erneut aus, um die Remoteverbindung mit dem virtuellen Computer wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="5f985-106">If not, just run this command again to remote back into the virtual machine.</span></span>

1. <span data-ttu-id="5f985-107">Führen Sie in Azure Cloud Shell den folgenden Befehl aus, um sich beim virtuellen Computer anzumelden.</span><span class="sxs-lookup"><span data-stu-id="5f985-107">Execute the following command in Azure Cloud Shell to sign into the VM.</span></span>

    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 
    
    <span data-ttu-id="5f985-108">Ersetzen Sie `<USERNAME>` durch den Administratorkontonamen, den Sie beim Erstellen des virtuellen Computers definiert haben.</span><span class="sxs-lookup"><span data-stu-id="5f985-108">Replace  `<USERNAME>` with the admin account name you defined when creating the VM.</span></span> <span data-ttu-id="5f985-109">Ersetzen Sie `<IP>` durch die IP-Adresse des virtuellen Computers, die Sie in der vorherigen Übung gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="5f985-109">Replace `<IP>` with the IP address of the VM you saved in the preceding exercise.</span></span>  

1. <span data-ttu-id="5f985-110">Wenn Sie dazu aufgefordert werden, geben Sie Ihr Kennwort für das Administratorkonto ein, um den Anmeldevorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="5f985-110">When prompted, enter your password for the admin account to complete the sign-in process.</span></span>

## <a name="run-a-jupyter-notebook-server-in-a-docker-container-in-the-vm"></a><span data-ttu-id="5f985-111">Ausführen eines Jupyter Notebook-Servers in einem Docker-Container auf dem virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="5f985-111">Run a Jupyter Notebook server in a Docker container in the VM</span></span>

> [!NOTE]
> <span data-ttu-id="5f985-112">Da wir nur über ein Administrator- oder Stammkonto auf dem virtuellen Computer verfügen, müssen wir alle Docker-Befehle als root mit `sudo` ausführen.</span><span class="sxs-lookup"><span data-stu-id="5f985-112">Since we only have an admin, or root, account on our VM, we have to run all Docker commands as root using `sudo`</span></span>

1. <span data-ttu-id="5f985-113">Um zu ermitteln, welche Docker-Container auf dem virtuellen Computer vorhanden sind, führen Sie den folgenden Befehl an der Eingabeaufforderung aus.</span><span class="sxs-lookup"><span data-stu-id="5f985-113">To see what Docker containers exist on the VM, run the following command at the command prompt.</span></span>

    ```azurecli 
    sudo docker ps
    ```

1. <span data-ttu-id="5f985-114">Führen Sie den folgenden Befehl an der Eingabeaufforderung aus, um einen neuen Container für unsere Experimente zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5f985-114">Run the following command at the command prompt to create a new container for our experiments.</span></span>

    ```azurecli 
    sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
    'conda install jupyter matplotlib -y &&\
    curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
    ``` 

    <span data-ttu-id="5f985-115">Die Ausführung dieses Befehls dauert eine ganze Weile.</span><span class="sxs-lookup"><span data-stu-id="5f985-115">This command will run for quite a while.</span></span> <span data-ttu-id="5f985-116">Während wir also etwas Zeit haben, können wir erörtern, was der Befehl bewirkt.</span><span class="sxs-lookup"><span data-stu-id="5f985-116">So, while we have some time, let's discuss what the command does.</span></span> 
    - <span data-ttu-id="5f985-117">`docker run` führt einen Befehl in einem neuen Container aus.</span><span class="sxs-lookup"><span data-stu-id="5f985-117">`docker run` runs a command in a new container.</span></span> <span data-ttu-id="5f985-118">Das Docker-Image, das verwendet wird, ist pytorch/pytorch.</span><span class="sxs-lookup"><span data-stu-id="5f985-118">The Docker image being used is pytorch/pytorch.</span></span> <span data-ttu-id="5f985-119">Es erstellt zunächst eine schreibbare Containerschicht über dem angegebenen Image und startet sie dann mit dem angegebenen Befehl.</span><span class="sxs-lookup"><span data-stu-id="5f985-119">It first creates a writeable container layer over the specified image, and then starts it using the specified command.</span></span>
    - <span data-ttu-id="5f985-120">`--rm` entfernt den Container, sobald dieser vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="5f985-120">`--rm` will remove the container once it exits.</span></span> <span data-ttu-id="5f985-121">Wenn Sie den Container beibehalten möchten, löschen Sie dieses Argument.</span><span class="sxs-lookup"><span data-stu-id="5f985-121">If you want to keep the container around, drop this argument.</span></span> 
    - <span data-ttu-id="5f985-122">`--entrypoint 'bin/sh'` überschreibt den Standardeinstiegspunkt des Images durch die Angabe der Bash-Shell.</span><span class="sxs-lookup"><span data-stu-id="5f985-122">`--entrypoint 'bin/sh'` overwrites the default entry point of the image to be the Bash shell</span></span>
    - <span data-ttu-id="5f985-123">`-c` definiert, welcher Befehl ausgeführt werden soll, wenn der Container gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="5f985-123">`-c` defines what command to run when the container starts.</span></span> <span data-ttu-id="5f985-124">In diesem Fall werden drei Befehle ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="5f985-124">In this case, it's running three commands:</span></span>
        - <span data-ttu-id="5f985-125">Installiert Jupyter und matplotlib.</span><span class="sxs-lookup"><span data-stu-id="5f985-125">Installs Jupyter and matplotlib</span></span>
        - <span data-ttu-id="5f985-126">Kopiert ein Notebook („cifar10_tutorial.ipynb“) aus pytorch.org in eine Datei im Container namens `first_pytorch_classifier.ipynb`.</span><span class="sxs-lookup"><span data-stu-id="5f985-126">Copies a notebook (cifar10_tutorial.ipynb) from pytorch.org to a file in the container called `first_pytorch_classifier.ipynb`</span></span>
        - <span data-ttu-id="5f985-127">Startet den Notebook-Server im Container auf die gleiche Weise wie in der vorherigen Übung.</span><span class="sxs-lookup"><span data-stu-id="5f985-127">Starts the notebook server in the container in the same way as the preceding exercise.</span></span>  <span data-ttu-id="5f985-128">Es wird kein Browser gestartet, auf das Notebook kann über root zugegriffen werden, und es wird an allen Ports gelauscht.</span><span class="sxs-lookup"><span data-stu-id="5f985-128">No browser is started, allow the notebook to be accessed by root and listen on all ports.</span></span> 
    
    <span data-ttu-id="5f985-129">Der Notebook-Server lauscht an allen Ports für den betreffenden Container.</span><span class="sxs-lookup"><span data-stu-id="5f985-129">The notebook server listens on all ports for that container.</span></span> <span data-ttu-id="5f985-130">Aber wie erfolgt Datenverkehr von außerhalb des Containers?</span><span class="sxs-lookup"><span data-stu-id="5f985-130">But, how will traffic come from outside the container?</span></span> <span data-ttu-id="5f985-131">Das `-p 8888:8888`-Argument bindet Port `8888` des Containers an TCP-Port 8888 auf dem Hostcomputer.</span><span class="sxs-lookup"><span data-stu-id="5f985-131">The `-p 8888:8888` argument binds port `8888` of the container to TCP port 8888 on the host machine.</span></span> <span data-ttu-id="5f985-132">Daher wird Datenverkehr, der vom virtuellen Computer stammt, über Port 8888 vom Container aufgenommen.</span><span class="sxs-lookup"><span data-stu-id="5f985-132">So, traffic coming to the VM over port 8888 will be picked up by the container.</span></span> 

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a><span data-ttu-id="5f985-133">Herstellen einer Verbindung mit dem Jupyter Notebook-Server über einen Remotebrowser</span><span class="sxs-lookup"><span data-stu-id="5f985-133">Connect to the Jupyter Notebook server from a remote browser</span></span> 

<span data-ttu-id="5f985-134">Sobald das Jupyter Notebook im Container ausgeführt wird, wird eine Meldung ähnlich der folgenden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5f985-134">Once the Jupyter notebook is running in the container, you'll  see a message similar to the following message.</span></span> 

> <span data-ttu-id="5f985-135">*Kopieren Sie bei der ersten Verbindungsherstellung die folgende URL, und fügen Sie sie in Ihren Browser ein, um sich mit einem Token anzumelden: http://(5b8783e7911d oder 127.0.0.1):8888/?token={sometoken}*</span><span class="sxs-lookup"><span data-stu-id="5f985-135">*Copy/paste this URL into your browser when you connect for the first time, to login with a token: http://(5b8783e7911d or 127.0.0.1):8888/?token={sometoken}*</span></span>

1. <span data-ttu-id="5f985-136">Ersetzen Sie den Teil **http://(5b8783e7911d oder 127.0.0.1)** der URL durch den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) oder die IP-Adresse des virtuellen Computers, und navigieren Sie auf einer neuen Registerkarte in Ihrem Browser zu der Adresse.</span><span class="sxs-lookup"><span data-stu-id="5f985-136">Replace the **http://(5b8783e7911d or 127.0.0.1)** part of the URL with the Fully Qualified Domain Name (FQDN) or the IP address of the VM and navigate to the address in a new a tab of your browser.</span></span>

    ![<span data-ttu-id="5f985-137">Screenshot: Jupyter Notebook-Dashboard</span><span class="sxs-lookup"><span data-stu-id="5f985-137">Screenshot showing Jupyter Notebooks dashboard.</span></span> ](../media/notebook-in-docker.png)

    > [!TIP]
    > <span data-ttu-id="5f985-138">Sie können den FQDN und die IP-Adresse Ihres virtuellen Computers mit folgendem Befehl abrufen:</span><span class="sxs-lookup"><span data-stu-id="5f985-138">You can get the FQDN and IP address of your VM with the following command:</span></span>
    > 
    > `az vm show -d --name <HOSTNAME> --resource-group <rgn>[sandbox resource group name]</rgn> --output table`
    >
    > <span data-ttu-id="5f985-139">Denken Sie daran, `<HOSTNAME>` durch den Namen zu ersetzen, den Sie Ihrem virtuellen Computer zugewiesen haben.</span><span class="sxs-lookup"><span data-stu-id="5f985-139">Remember to replace `<HOSTNAME>` with the name you gave your VM.</span></span> 
    
    <span data-ttu-id="5f985-140">Dieses Mal wird nur ein einzelnes Notebook angezeigt.</span><span class="sxs-lookup"><span data-stu-id="5f985-140">This time we only see a single notebook.</span></span> <span data-ttu-id="5f985-141">Das liegt daran, dass wir uns in einem Container befinden und nur dieses Notebook kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="5f985-141">That's because we're in a container and only copied down this notebook.</span></span> <span data-ttu-id="5f985-142">In der nächsten Übung experimentieren wir mit diesem Notebook.</span><span class="sxs-lookup"><span data-stu-id="5f985-142">In the next exercise, we'll experiment with this notebook.</span></span> 
    
    > [!TIP]
    > <span data-ttu-id="5f985-143">Fahren Sie den Notebook-Server also noch nicht herunter.</span><span class="sxs-lookup"><span data-stu-id="5f985-143">Don't shut down the notebook server just yet.</span></span> <span data-ttu-id="5f985-144">Wir untersuchen das Notebook `first_pytorch_classifier.ipynb` in der nächsten Übung.</span><span class="sxs-lookup"><span data-stu-id="5f985-144">We'll look at the `first_pytorch_classifier.ipynb` notebook in the next exercise.</span></span>