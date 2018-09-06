## <a name="exercise-install-mongodb"></a><span data-ttu-id="5f5ff-101">Übung: Installieren von MongoDB</span><span class="sxs-lookup"><span data-stu-id="5f5ff-101">Exercise: Install MongoDB</span></span>

<span data-ttu-id="5f5ff-102">Im Rahmen dieser Übung installieren Sie MongoDB als Datenspeicher für Beispielwebanwendungen auf ihrer Ubuntu Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-102">In this exercise, you will install MongoDB on your Ubuntu Linux virtual machine to act as a data store for your upcoming sample web application.</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="5f5ff-103">Herstellen einer Verbindung mit der VM</span><span class="sxs-lookup"><span data-stu-id="5f5ff-103">Connect to the VM</span></span>

<span data-ttu-id="5f5ff-104">Sie müssen mithilfe von **ssh** eine Verbindung mit der VM herstellen, um MongoDB zu installieren.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-104">In order to install MongoDB, you have to connect to the VM using **ssh**.</span></span> <span data-ttu-id="5f5ff-105">Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der zuvor erwähnten VM.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-105">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="install-mongodb"></a><span data-ttu-id="5f5ff-106">Installieren von MongoDB</span><span class="sxs-lookup"><span data-stu-id="5f5ff-106">Install MongoDB</span></span>

> [!Important]
> <span data-ttu-id="5f5ff-107">Ubuntu stellt ein inoffizielles Paket mit dem Namen **mongodb** zur Verfügung, das allerdings nicht von MongoDB Inc. gewartet wird.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-107">Ubuntu provides an unofficial package called **mongodb**, but this package is not maintained by MongoDB Inc.</span></span>

1. <span data-ttu-id="5f5ff-108">Importieren Sie den Verschlüsselungsschlüssel für das MongoDB-Repository.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-108">Import the encryption key for the MongoDB repository.</span></span> <span data-ttu-id="5f5ff-109">So kann der Paket-Manager prüfen, ob die mongodb-Pakete, die Sie installieren, wirklich von MongoDB Inc. stammen.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-109">This will allow the package manager to verify that the mongodb packages you install are coming from MongoDB Inc.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    <span data-ttu-id="5f5ff-110">Der Befehl **sudo** impliziert, dass der angegebene Befehl mit Administratorberechtigungen ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-110">The **sudo** command means that we want to run the specified command with administrative privileges.</span></span>

1. <span data-ttu-id="5f5ff-111">Registrieren Sie das Ubuntu-Repository für MongoDB, damit der Paket-Manager die mongodb-Pakete finden kann.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-111">Register the MongoDB Ubuntu repository so the package manager can locate the mongodb packages.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f5ff-112">Dieser Befehl unterscheidet sich je nach Ubuntu-Version.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-112">This command is different for different versions of Ubuntu.</span></span> <span data-ttu-id="5f5ff-113">Führen Sie `uname -v` aus, um zu prüfen, welche Ubuntu-Version Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-113">To find out which version of Ubuntu you are running please run: `uname -v`.</span></span>
    > <span data-ttu-id="5f5ff-114">Die Ausgabe sieht in etwa wie folgt aus: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-114">This will output something like this: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.</span></span>
    >
    > <span data-ttu-id="5f5ff-115">Dies lässt darauf schließen, dass Sie Version 16.04.1 von Ubuntu ausführen.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-115">This indicates that we are running Ubuntu version 16.04.1.</span></span>
    > <span data-ttu-id="5f5ff-116">Den genauen Befehl für die jeweiligen Versionen finden Sie in der Dokumentation zum [Installieren von MongoDB Community unter Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="5f5ff-116">Please refer to [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) documentation to get the exact command for your version</span></span>

    <span data-ttu-id="5f5ff-117">Gehen Sie unter Ubuntu 16.04 wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="5f5ff-117">On Ubuntu 16.04 we run this:</span></span>

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. <span data-ttu-id="5f5ff-118">Laden Sie die Paketdatenbank neu, damit Sie über aktuelle Paketinformationen verfügen.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-118">Reload the package database so we have the latest package information.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="5f5ff-119">Installieren Sie das MongoDB-Paket auf der VM.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-119">Install the MongoDB package onto our VM.</span></span>

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. <span data-ttu-id="5f5ff-120">Starten Sie den MongoDB-Dienst, damit Sie später eine Verbindung mit diesem herstellen können.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-120">Start the MongoDB service so you can connect to it later.</span></span>

    ```bash
    sudo service mongod start
    ```

## <a name="summary"></a><span data-ttu-id="5f5ff-121">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="5f5ff-121">Summary</span></span>

<span data-ttu-id="5f5ff-122">MongoDB ist jetzt auf Ihrer Ubuntu Linux-VM installiert.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-122">We now have MongoDB installed on our Ubuntu Linux VM.</span></span> <span data-ttu-id="5f5ff-123">MongoDB dient als Sicherungsdatenspeicher für die Informationen, die Sie in Ihrer Webanwendung speichern und aus dieser abrufen.</span><span class="sxs-lookup"><span data-stu-id="5f5ff-123">MongoDB will serve as your backing data store for the information you save and retrieve in your web application.</span></span>
