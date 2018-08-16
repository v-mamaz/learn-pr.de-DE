<span data-ttu-id="603d3-101">Der letzte Schritt soll nun versuchen Sie es auf dem virtuellen Computer ist auf einen Webserver zu installieren.</span><span class="sxs-lookup"><span data-stu-id="603d3-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="603d3-102">Eine der einfachsten Pakete zu installieren ist `nginx`.</span><span class="sxs-lookup"><span data-stu-id="603d3-102">One of the easiest packages to install is `nginx`.</span></span>

1. <span data-ttu-id="603d3-103">Suchen Sie die öffentliche IP-Adresse des virtuellen Linux-Computer.</span><span class="sxs-lookup"><span data-stu-id="603d3-103">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="603d3-104">Denken Sie daran, Sie können die `vm list-ip-addresses` Befehls zu suchen.</span><span class="sxs-lookup"><span data-stu-id="603d3-104">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

2. <span data-ttu-id="603d3-105">Öffnen Sie als Nächstes eine `ssh` Verbindung mit dem Computer, wie bei der testen.</span><span class="sxs-lookup"><span data-stu-id="603d3-105">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="603d3-106">Denken Sie daran, Sie müssen den Administratornamen zu übergeben ("**Aldis**").</span><span class="sxs-lookup"><span data-stu-id="603d3-106">Remember you will need to pass in the admin name ("**aldis**").</span></span>

3. <span data-ttu-id="603d3-107">Führen Sie in der dargestellten Shell den folgenden Befehl zum Installieren der `nginx` Webserver.</span><span class="sxs-lookup"><span data-stu-id="603d3-107">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. <span data-ttu-id="603d3-108">Verwenden Sie in der Cloud Shell `curl` die Standardseite von Ihrem Linux-Web-Server zu lesen.</span><span class="sxs-lookup"><span data-stu-id="603d3-108">In the Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="603d3-109">Alternativ können Sie eine neue Browserregisterkarte zu öffnen, und navigieren Sie zu die öffentliche IP-Adresse.</span><span class="sxs-lookup"><span data-stu-id="603d3-109">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 168.61.54.62
```

<span data-ttu-id="603d3-110">Es schlägt fehl, da es sich bei virtuellen Linux-Computer auf Port 80 verfügbar macht (`http`) über die integrierte Firewall.</span><span class="sxs-lookup"><span data-stu-id="603d3-110">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="603d3-111">Glücklicherweise wurde der Azure-Befehlszeilenschnittstelle einen Befehl für diese: `vm open-port`.</span><span class="sxs-lookup"><span data-stu-id="603d3-111">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

5. <span data-ttu-id="603d3-112">Geben Sie Folgendes in die Cloud Shell, öffnen Sie Port 80:</span><span class="sxs-lookup"><span data-stu-id="603d3-112">Type the following into the Cloud Shell to open port 80:</span></span>

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="603d3-113">Letztendlich sollten Sie `curl` erneut aus.</span><span class="sxs-lookup"><span data-stu-id="603d3-113">Finally, try `curl` again.</span></span> <span data-ttu-id="603d3-114">Dieses Mal sollte Rückgabe von Daten – sehen Sie die Seite in einem Browser auch.</span><span class="sxs-lookup"><span data-stu-id="603d3-114">This time it should return data - you can see the page in a browser as well.</span></span>



