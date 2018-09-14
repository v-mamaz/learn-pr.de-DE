<span data-ttu-id="60210-101">Das Letzte, was wir in unserer VM ausprobieren möchten, ist die Installation eines Webservers.</span><span class="sxs-lookup"><span data-stu-id="60210-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="60210-102">Eines der am einfachsten zu installierenden Pakete ist `nginx`.</span><span class="sxs-lookup"><span data-stu-id="60210-102">One of the easiest packages to install is `nginx`.</span></span>

1. <span data-ttu-id="60210-103">Bestimmen Sie die öffentliche IP-Adresse Ihres virtuellen Linux-Computers.</span><span class="sxs-lookup"><span data-stu-id="60210-103">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="60210-104">Denken Sie daran, dass Sie den Befehl `vm list-ip-addresses` verwenden können, um ihn nachzuschlagen.</span><span class="sxs-lookup"><span data-stu-id="60210-104">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

1. <span data-ttu-id="60210-105">Öffnen Sie als Nächstes wie beim Test eine `ssh`-Verbindung mit dem Computer.</span><span class="sxs-lookup"><span data-stu-id="60210-105">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="60210-106">Sie müssen hierbei den Administratornamen übergeben („**aldis**“).</span><span class="sxs-lookup"><span data-stu-id="60210-106">Remember you will need to pass in the admin name ("**aldis**").</span></span>

1. <span data-ttu-id="60210-107">Führen Sie in der dargestellten Shell den folgenden Befehl zum Installieren des Webservers `nginx` aus.</span><span class="sxs-lookup"><span data-stu-id="60210-107">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

1. <span data-ttu-id="60210-108">Verwenden Sie in Azure Cloud Shell `curl`, um die Standardseite von Ihrem Linux-Webserver einzulesen.</span><span class="sxs-lookup"><span data-stu-id="60210-108">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="60210-109">Alternativ können Sie eine neue Browserregisterkarte öffnen und zur öffentlichen IP-Adresse navigieren.</span><span class="sxs-lookup"><span data-stu-id="60210-109">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 168.61.54.62
```

<span data-ttu-id="60210-110">Er wird fehlschlagen, weil der virtuelle Linux-Computer den Port 80 (`http`) durch die integrierte Firewall nicht verfügbar macht.</span><span class="sxs-lookup"><span data-stu-id="60210-110">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="60210-111">Glücklicherweise bietet die Azure CLI einen Befehl hierfür: `vm open-port`.</span><span class="sxs-lookup"><span data-stu-id="60210-111">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

1. <span data-ttu-id="60210-112">Geben Sie Folgendes in Cloud Shell ein, um Port 80 zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="60210-112">Type the following into Cloud Shell to open port 80:</span></span>

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="60210-113">Wiederholen Sie schließlich `curl`.</span><span class="sxs-lookup"><span data-stu-id="60210-113">Finally, try `curl` again.</span></span> <span data-ttu-id="60210-114">Dieses Mal sollten Daten zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="60210-114">This time it should return data.</span></span> <span data-ttu-id="60210-115">Sie können die Seite auch in einem Browser anzeigen.</span><span class="sxs-lookup"><span data-stu-id="60210-115">You can see the page in a browser as well.</span></span>
