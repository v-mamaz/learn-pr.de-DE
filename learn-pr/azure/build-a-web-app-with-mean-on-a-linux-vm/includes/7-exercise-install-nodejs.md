<span data-ttu-id="592c5-101">In dieser Einheit installieren Sie Node.js (das **N** im Akronym MEAN) auf einem virtuellen Ubuntu Linux-Computer, der in Azure gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="592c5-101">In this unit, you will install Node.js - the **N** in the MEAN acronym - on an Azure-hosted Ubuntu Linux virtual machine.</span></span> <span data-ttu-id="592c5-102">Node.js wird als Laufzeit verwendet, über die der HTTP-Datenverkehr verarbeitet und unsere Webanwendung gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="592c5-102">Node.js will serve as our runtime for handling our HTTP traffic and hosting our web application.</span></span>

## <a name="install-nodejs"></a><span data-ttu-id="592c5-103">Installieren von Node.js</span><span class="sxs-lookup"><span data-stu-id="592c5-103">Install Node.js</span></span>

1. <span data-ttu-id="592c5-104">**Wenn Sie immer noch nicht über SSH mit Ihrem virtuellen Computer aus der vorherigen Übung verbunden sind**, stellen Sie die SSH-Verbindung her.</span><span class="sxs-lookup"><span data-stu-id="592c5-104">**If you aren't still SSHed into your VM from the previous exercise**, SSH in.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

1. <span data-ttu-id="592c5-105">Registrieren Sie das Node.js-Paketrepository, damit **apt-get** das richtige Paket zur Installation auf Ihrem virtuellen Computer finden kann.</span><span class="sxs-lookup"><span data-stu-id="592c5-105">Register the Node.js package repository so **apt-get** can find the right package to install on your virtual machine.</span></span>

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. <span data-ttu-id="592c5-106">Installieren Sie das Node.js-Paket auf Ihrem Linux-System.</span><span class="sxs-lookup"><span data-stu-id="592c5-106">Install the Node.js package on your Linux system.</span></span>

    ```bash
    sudo apt-get install -y Node.js
    ```

1. <span data-ttu-id="592c5-107">Überprüfen Sie mit dem folgenden Befehl, ob die Installation von Node.js erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="592c5-107">Verify the Node.js installation succeeded by running the following simple Node.js command.</span></span>

    ```bash
    node -v
    ```

    <span data-ttu-id="592c5-108">Die Ausgabe sollte etwa so wie in `v8.11.4` aussehen und die aktuelle Version von Node.js enthalten, die Sie bei der Installation angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="592c5-108">The output should be something like `v8.11.4`, with the version reflecting the latest Node.js version that's available when you install the package.</span></span>

## <a name="summary"></a><span data-ttu-id="592c5-109">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="592c5-109">Summary</span></span>

<span data-ttu-id="592c5-110">Sie haben Node.js auf Ihrem virtuellen Computer installiert. Nun können Sie eine Webanwendung erstellen, die vom virtueller Computer ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="592c5-110">With Node.js installed on your virtual machine, we can start building a web application that it will be responsible for running.</span></span>