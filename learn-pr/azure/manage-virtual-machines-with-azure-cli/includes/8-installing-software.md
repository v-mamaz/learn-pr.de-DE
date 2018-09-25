<span data-ttu-id="3dae3-101">Das Letzte, was wir in unserer VM ausprobieren möchten, ist die Installation eines Webservers.</span><span class="sxs-lookup"><span data-stu-id="3dae3-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="3dae3-102">Eines der am einfachsten zu installierenden Pakete ist `nginx`.</span><span class="sxs-lookup"><span data-stu-id="3dae3-102">One of the easiest packages to install is `nginx`.</span></span>

## <a name="install-nginx-web-server"></a><span data-ttu-id="3dae3-103">Installieren eines NGINX-Webservers</span><span class="sxs-lookup"><span data-stu-id="3dae3-103">Install NGINX web server</span></span>

1. <span data-ttu-id="3dae3-104">Bestimmen Sie die öffentliche IP-Adresse Ihres virtuellen Linux-Computers.</span><span class="sxs-lookup"><span data-stu-id="3dae3-104">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="3dae3-105">Denken Sie daran, dass Sie den Befehl `vm list-ip-addresses` verwenden können, um ihn nachzuschlagen.</span><span class="sxs-lookup"><span data-stu-id="3dae3-105">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

1. <span data-ttu-id="3dae3-106">Öffnen Sie als Nächstes wie beim Test eine `ssh`-Verbindung mit dem Computer.</span><span class="sxs-lookup"><span data-stu-id="3dae3-106">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="3dae3-107">Sie müssen hierbei den Administratornamen übergeben („**aldis**“).</span><span class="sxs-lookup"><span data-stu-id="3dae3-107">Remember you will need to pass in the admin name ("**aldis**").</span></span>

1. <span data-ttu-id="3dae3-108">Führen Sie in der dargestellten Shell den folgenden Befehl zum Installieren des Webservers `nginx` aus.</span><span class="sxs-lookup"><span data-stu-id="3dae3-108">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```bash
sudo apt-get -y update && sudo apt-get -y install nginx
```

1. <span data-ttu-id="3dae3-109">Beenden Sie die Secure Shell.</span><span class="sxs-lookup"><span data-stu-id="3dae3-109">Exit the Secure Shell.</span></span>

```bash
exit
```

## <a name="retrieve-our-default-page"></a><span data-ttu-id="3dae3-110">Abrufen unserer Standardseite</span><span class="sxs-lookup"><span data-stu-id="3dae3-110">Retrieve our default page</span></span>

1. <span data-ttu-id="3dae3-111">Verwenden Sie in Azure Cloud Shell `curl`, um die Standardseite von Ihrem Linux-Webserver einzulesen.</span><span class="sxs-lookup"><span data-stu-id="3dae3-111">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="3dae3-112">Alternativ können Sie eine neue Browserregisterkarte öffnen und zur öffentlichen IP-Adresse navigieren.</span><span class="sxs-lookup"><span data-stu-id="3dae3-112">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 40.83.165.85
```

<span data-ttu-id="3dae3-113">Er wird fehlschlagen, weil der virtuelle Linux-Computer den Port 80 (`http`) durch die integrierte Firewall nicht verfügbar macht.</span><span class="sxs-lookup"><span data-stu-id="3dae3-113">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="3dae3-114">Glücklicherweise bietet die Azure CLI einen Befehl hierfür: `vm open-port`.</span><span class="sxs-lookup"><span data-stu-id="3dae3-114">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

1. <span data-ttu-id="3dae3-115">Geben Sie Folgendes in Cloud Shell ein, um Port 80 zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="3dae3-115">Type the following into Cloud Shell to open port 80:</span></span>

```azurecli
az vm open-port --port 80 --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM
```

<span data-ttu-id="3dae3-116">Es dauert einen Moment, die Netzwerkregel hinzuzufügen und den Port über die Firewall zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="3dae3-116">It will take a moment to add the network rule and open the port through the firewall.</span></span> <span data-ttu-id="3dae3-117">Versuchen Sie `curl` erneut.</span><span class="sxs-lookup"><span data-stu-id="3dae3-117">Try `curl` again.</span></span> <span data-ttu-id="3dae3-118">Dieses Mal sollten Daten zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="3dae3-118">This time it should return data.</span></span> <span data-ttu-id="3dae3-119">Sie können die Seite auch in einem Browser anzeigen.</span><span class="sxs-lookup"><span data-stu-id="3dae3-119">You can see the page in a browser as well.</span></span>

```output
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx on Debian!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx on Debian!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working on Debian. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a></p>

<p>
      Please use the <tt>reportbug</tt> tool to report bugs in the
      nginx package with Debian. However, check <a
      href="http://bugs.debian.org/cgi-bin/pkgreport.cgi?ordering=normal;archive=0;src=nginx;repeatmerged=0">existing
      bug reports</a> before reporting a new bug.
</p>

<p><em>Thank you for using debian and nginx.</em></p>


</body>
</html>
```
