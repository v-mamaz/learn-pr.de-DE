<span data-ttu-id="7d832-101">In dieser Einheit installieren Sie MongoDB als Datenspeicher für Beispielwebanwendungen auf ihrem virtuellen Ubuntu Linux-Computer (virtual machine, VM).</span><span class="sxs-lookup"><span data-stu-id="7d832-101">In this unit, you will install MongoDB on your Ubuntu Linux virtual machine to act as a data store for your upcoming sample web application.</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="7d832-102">Herstellen der Verbindung mit der VM</span><span class="sxs-lookup"><span data-stu-id="7d832-102">Connect to the VM</span></span>

<span data-ttu-id="7d832-103">Sie müssen mithilfe von **ssh** eine Verbindung mit der VM herstellen, um MongoDB zu installieren.</span><span class="sxs-lookup"><span data-stu-id="7d832-103">In order to install MongoDB, you have to connect to the VM using **ssh**.</span></span> <span data-ttu-id="7d832-104">Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratornamen und die öffentliche IP-Adresse der zuvor erwähnten VM.</span><span class="sxs-lookup"><span data-stu-id="7d832-104">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="install-mongodb"></a><span data-ttu-id="7d832-105">Installieren von MongoDB</span><span class="sxs-lookup"><span data-stu-id="7d832-105">Install MongoDB</span></span>

> [!Important]
> <span data-ttu-id="7d832-106">Ubuntu stellt ein inoffizielles Paket namens **mongodb** bereit.</span><span class="sxs-lookup"><span data-stu-id="7d832-106">Ubuntu provides an unofficial package called **mongodb**.</span></span> <span data-ttu-id="7d832-107">Dieses Paket wird nicht von MongoDB Inc. verwaltet.</span><span class="sxs-lookup"><span data-stu-id="7d832-107">This package is not maintained by MongoDB Inc.</span></span>

1. <span data-ttu-id="7d832-108">Importieren Sie den Verschlüsselungsschlüssel für das MongoDB-Repository.</span><span class="sxs-lookup"><span data-stu-id="7d832-108">Import the encryption key for the MongoDB repository.</span></span> <span data-ttu-id="7d832-109">So kann der Paket-Manager prüfen, ob die mongodb-Pakete, die Sie installieren, wirklich von MongoDB Inc. stammen.</span><span class="sxs-lookup"><span data-stu-id="7d832-109">This will allow the package manager to verify that the mongodb packages you install are coming from MongoDB Inc.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    <span data-ttu-id="7d832-110">Der Befehl **sudo** impliziert, dass der angegebene Befehl mit Administratorberechtigungen ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="7d832-110">The **sudo** command means that we want to run the specified command with administrative privileges.</span></span>

1. <span data-ttu-id="7d832-111">Registrieren Sie das Ubuntu-Repository für MongoDB, damit der Paket-Manager die mongodb-Pakete finden kann.</span><span class="sxs-lookup"><span data-stu-id="7d832-111">Register the MongoDB Ubuntu repository so the package manager can locate the mongodb packages.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7d832-112">Dieser Befehl unterscheidet sich je nach Ubuntu-Version.</span><span class="sxs-lookup"><span data-stu-id="7d832-112">This command is different for different versions of Ubuntu.</span></span> <span data-ttu-id="7d832-113">Führen Sie `uname -v` aus, um zu prüfen, welche Ubuntu-Version Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="7d832-113">To find out which version of Ubuntu you're using, run: `uname -v`.</span></span>
    > <span data-ttu-id="7d832-114">Die Ausgabe dieses Befehls sieht in etwa wie folgt aus: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.</span><span class="sxs-lookup"><span data-stu-id="7d832-114">This command will output something like this: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.</span></span>
    >
    > <span data-ttu-id="7d832-115">Diese Ausgabe lässt darauf schließen, dass Sie Version 16.04.1 von Ubuntu ausführen.</span><span class="sxs-lookup"><span data-stu-id="7d832-115">This output indicates that we're running Ubuntu version 16.04.1.</span></span>
    > <span data-ttu-id="7d832-116">Den genauen Befehl für die jeweiligen Versionen finden Sie in der Dokumentation zum Installieren von MongoDB Community unter Ubuntu: [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="7d832-116">Refer to the [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) documentation to get the exact command for your version.</span></span>

    <span data-ttu-id="7d832-117">Führen Sie unter Ubuntu 16.04 diesen Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="7d832-117">On Ubuntu 16.04, we run this command:</span></span>

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. <span data-ttu-id="7d832-118">Laden Sie die Paketdatenbank neu, damit Sie über aktuelle Paketinformationen verfügen.</span><span class="sxs-lookup"><span data-stu-id="7d832-118">Reload the package database so we have the latest package information.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="7d832-119">Installieren Sie das MongoDB-Paket auf der VM.</span><span class="sxs-lookup"><span data-stu-id="7d832-119">Install the MongoDB package onto our VM.</span></span>

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. <span data-ttu-id="7d832-120">Starten Sie den MongoDB-Dienst, damit Sie später eine Verbindung mit diesem herstellen können.</span><span class="sxs-lookup"><span data-stu-id="7d832-120">Start the MongoDB service so you can connect to it later.</span></span>

    ```bash
    sudo service mongod start
    ```

## <a name="summary"></a><span data-ttu-id="7d832-121">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="7d832-121">Summary</span></span>

<span data-ttu-id="7d832-122">MongoDB ist jetzt auf Ihrer Ubuntu Linux-VM installiert.</span><span class="sxs-lookup"><span data-stu-id="7d832-122">We now have MongoDB installed on our Ubuntu Linux VM.</span></span> <span data-ttu-id="7d832-123">MongoDB dient als Sicherungsdatenspeicher für die Informationen, die Sie in Ihrer Webanwendung speichern und aus dieser abrufen.</span><span class="sxs-lookup"><span data-stu-id="7d832-123">MongoDB will serve as your backing data store for the information you save and retrieve in your web application.</span></span>