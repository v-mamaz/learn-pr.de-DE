<span data-ttu-id="daacd-101">In dieser Einheit installieren Sie MongoDB als Datenspeicher für Beispielwebanwendungen auf ihrem virtuellen Ubuntu Linux-Computer (Virtual Machine, VM).</span><span class="sxs-lookup"><span data-stu-id="daacd-101">In this unit, you will install MongoDB on your Ubuntu Linux virtual machine to act as a data store for your upcoming sample web application.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="daacd-102">Installieren von MongoDB</span><span class="sxs-lookup"><span data-stu-id="daacd-102">Install MongoDB</span></span>

1. <span data-ttu-id="daacd-103">Stellen Sie über Cloud Shell eine SSH-Verbindung mit Ihrem virtuellen Computer her.</span><span class="sxs-lookup"><span data-stu-id="daacd-103">From Cloud Shell, SSH into your VM.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

1. <span data-ttu-id="daacd-104">Importieren Sie den Verschlüsselungsschlüssel für das MongoDB-Repository.</span><span class="sxs-lookup"><span data-stu-id="daacd-104">Import the encryption key for the MongoDB repository.</span></span> <span data-ttu-id="daacd-105">So kann der Paket-Manager prüfen, ob die mongodb-Pakete, die Sie installieren, wirklich von MongoDB Inc. stammen.</span><span class="sxs-lookup"><span data-stu-id="daacd-105">This will allow the package manager to verify that the mongodb packages you install are coming from MongoDB Inc.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    <span data-ttu-id="daacd-106">Der Befehl **sudo** impliziert, dass der angegebene Befehl mit Administratorberechtigungen ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="daacd-106">The **sudo** command means that we want to run the specified command with administrative privileges.</span></span>

1. <span data-ttu-id="daacd-107">Registrieren Sie das Ubuntu-Repository für MongoDB, damit der Paket-Manager die mongodb-Pakete finden kann.</span><span class="sxs-lookup"><span data-stu-id="daacd-107">Register the MongoDB Ubuntu repository so the package manager can locate the mongodb packages.</span></span>

    > [!NOTE]
    > <span data-ttu-id="daacd-108">Dieser Befehl unterscheidet sich je nach Ubuntu-Version.</span><span class="sxs-lookup"><span data-stu-id="daacd-108">This command is different for different versions of Ubuntu.</span></span> <span data-ttu-id="daacd-109">Führen Sie `uname -v` aus, um zu prüfen, welche Ubuntu-Version Sie verwenden.</span><span class="sxs-lookup"><span data-stu-id="daacd-109">To find out which version of Ubuntu you're using, run: `uname -v`.</span></span>
    > <span data-ttu-id="daacd-110">Die Ausgabe dieses Befehls sieht in etwa wie folgt aus: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.</span><span class="sxs-lookup"><span data-stu-id="daacd-110">This command will output something like this: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.</span></span>
    >
    > <span data-ttu-id="daacd-111">Diese Ausgabe lässt darauf schließen, dass Sie Version 16.04.1 von Ubuntu ausführen.</span><span class="sxs-lookup"><span data-stu-id="daacd-111">This output indicates that we're running Ubuntu version 16.04.1.</span></span>
    > <span data-ttu-id="daacd-112">Den genauen Befehl für die jeweiligen Versionen finden Sie in der Dokumentation zum Installieren von MongoDB Community unter Ubuntu: [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="daacd-112">Refer to the [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) documentation to get the exact command for your version.</span></span>

    <span data-ttu-id="daacd-113">Führen Sie unter Ubuntu 16.04 diesen Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="daacd-113">On Ubuntu 16.04, we run this command:</span></span>

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. <span data-ttu-id="daacd-114">Aktualisieren Sie die Paketdatenbank, damit Sie über aktuelle Paketinformationen verfügen.</span><span class="sxs-lookup"><span data-stu-id="daacd-114">Update the package database so we have the latest package information.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="daacd-115">Installieren Sie das MongoDB-Paket auf der VM.</span><span class="sxs-lookup"><span data-stu-id="daacd-115">Install the MongoDB package onto our VM.</span></span>

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. <span data-ttu-id="daacd-116">Starten Sie den MongoDB-Dienst, damit Sie später eine Verbindung mit diesem herstellen können.</span><span class="sxs-lookup"><span data-stu-id="daacd-116">Start the MongoDB service so you can connect to it later.</span></span>

    ```bash
    sudo service mongod start
    ```

## <a name="summary"></a><span data-ttu-id="daacd-117">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="daacd-117">Summary</span></span>

<span data-ttu-id="daacd-118">MongoDB ist jetzt auf Ihrer Ubuntu Linux-VM installiert.</span><span class="sxs-lookup"><span data-stu-id="daacd-118">We now have MongoDB installed on our Ubuntu Linux VM.</span></span> <span data-ttu-id="daacd-119">MongoDB dient als Sicherungsdatenspeicher für die Informationen, die Sie in Ihrer Webanwendung speichern und aus dieser abrufen.</span><span class="sxs-lookup"><span data-stu-id="daacd-119">MongoDB will serve as your backing data store for the information you save and retrieve in your web application.</span></span>