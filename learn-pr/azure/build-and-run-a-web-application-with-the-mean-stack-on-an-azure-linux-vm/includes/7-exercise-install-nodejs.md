<span data-ttu-id="1e7e5-101">In dieser Einheit installieren Sie Node.js (das **N** im Akronym MEAN) auf einem virtuellen Ubuntu Linux-Computer, der in Azure gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-101">In this unit, you will install Node.js - the **N** in the MEAN acronym - on an Azure-hosted Ubuntu Linux virtual machine.</span></span> <span data-ttu-id="1e7e5-102">Node.js wird als Runtime verwendet, über die der HTTP-Datenverkehr verarbeitet und unsere Webanwendung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-102">Node.js will serve as our runtime for handling our HTTP traffic and hosting our web application.</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="1e7e5-103">Herstellen der Verbindung zum virtueller Computer</span><span class="sxs-lookup"><span data-stu-id="1e7e5-103">Connect to the VM</span></span>

<span data-ttu-id="1e7e5-104">Stellen Sie mit **ssh** eine Verbindung mit dem virtuellen Computer her, um Node.js zu installieren.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-104">In order to install Node.js, you have to connect to the VM using **ssh**.</span></span> <span data-ttu-id="1e7e5-105">Wenn diese Verbindung noch nicht besteht, müssen Sie den folgenden Befehl ausführen.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-105">If you aren't still connected to your VM, run the following command.</span></span> <span data-ttu-id="1e7e5-106">Ersetzen Sie die Platzhalter `<vm-admin-username>` und `<vm-public-ip>` durch Ihren Administratorbenutzernamen und die öffentliche IP-Adresse des virtuellen Computers von oben.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-106">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="install-nodejs"></a><span data-ttu-id="1e7e5-107">Installieren von Node.js</span><span class="sxs-lookup"><span data-stu-id="1e7e5-107">Install Node.js</span></span>

> [!Important]
> <span data-ttu-id="1e7e5-108">Ubuntu stellt ein inoffizielles Paket namens **Node.js-legacy** bereit.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-108">Ubuntu provides an unofficial package called **Node.js-legacy**.</span></span> <span data-ttu-id="1e7e5-109">Dieses Paket wird nicht von Node.js gewartet und ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-109">This package is not maintained by Node.js and is outdated.</span></span>

1. <span data-ttu-id="1e7e5-110">Registrieren Sie das Node.js-Paketrepository, damit **apt-get** das richtige Paket zur Installation auf Ihrem virtuellen Computer finden kann.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-110">Register the Node.js package repository, so **apt-get** can find the right package to install on your virtual machine.</span></span>

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. <span data-ttu-id="1e7e5-111">Installieren Sie das Node.js-Paket auf Ihrem Linux-System.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-111">Install the Node.js package on your Linux system.</span></span>

    ```bash
    sudo apt-get install -y Node.js
    ```

1. <span data-ttu-id="1e7e5-112">Überprüfen Sie mit dem folgenden Befehl, ob die Installation von Node.js erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-112">Verify the Node.js installation succeeded by running the following simple Node.js command.</span></span>

    ```bash
    node -v
    ```

    <span data-ttu-id="1e7e5-113">Die Ausgabe sollte etwa so wie in `v8.11.4` aussehen und die aktuelle Version von Node.js enthalten, die Sie bei der Installation angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-113">The output should be something like `v8.11.4`, with the version reflecting the latest Node.js version that's available when you install the package.</span></span>

## <a name="summary"></a><span data-ttu-id="1e7e5-114">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="1e7e5-114">Summary</span></span>

<span data-ttu-id="1e7e5-115">Sie haben Node.js auf Ihrem virtuellen Computer installiert. Nun können Sie eine Webanwendung erstellen, die vom virtueller Computer ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="1e7e5-115">With Node.js installed on your virtual machine, we can start building a web application that it will be responsible for running.</span></span>