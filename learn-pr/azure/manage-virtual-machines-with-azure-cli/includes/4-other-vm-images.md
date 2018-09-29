<span data-ttu-id="6f61e-101">Wir haben `Debian` für das Image verwendet, um den virtuellen Computer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6f61e-101">We used `Debian` for the image to create the virtual machine.</span></span> <span data-ttu-id="6f61e-102">Azure bietet verschiedene VM-Standardimages, mit denen Sie einen virtuellen Computer erstellen können.</span><span class="sxs-lookup"><span data-stu-id="6f61e-102">Azure has several standard VM images you can use to create a virtual machine.</span></span> 

## <a name="listing-images"></a><span data-ttu-id="6f61e-103">Auflisten von Images</span><span class="sxs-lookup"><span data-stu-id="6f61e-103">Listing images</span></span>

<span data-ttu-id="6f61e-104">Mit dem folgenden Befehl können Sie eine Liste der verfügbaren Images virtueller Computer abrufen.</span><span class="sxs-lookup"><span data-stu-id="6f61e-104">You can get a list of the available VM images using the following command.</span></span> 

```azurecli
az vm image list --output table
```

<span data-ttu-id="6f61e-105">Dieser Befehl gibt die am häufigsten verwendeten Images aus, die zu einer in die Azure CLI integrierten Offlineliste gehören.</span><span class="sxs-lookup"><span data-stu-id="6f61e-105">This will output the most popular images that are part of an offline list built into the Azure CLI.</span></span> <span data-ttu-id="6f61e-106">Im Azure Marketplace sind jedoch _Hunderte_ von Imageoptionen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="6f61e-106">However, there are _hundreds_ of image options available in the Azure Marketplace.</span></span> 

## <a name="getting-all-images"></a><span data-ttu-id="6f61e-107">Abrufen aller Images</span><span class="sxs-lookup"><span data-stu-id="6f61e-107">Getting all images</span></span>

<span data-ttu-id="6f61e-108">Sie können eine vollständige Liste abrufen, indem Sie dem Befehl das `--all`-Flag hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="6f61e-108">You can get a full list by adding the `--all` flag to the command.</span></span> <span data-ttu-id="6f61e-109">Da die Liste der Images im Marketplace sehr umfangreich ist, ist es hilfreich, die Liste mit den Optionen „`--publisher`“, „`--sku`“ oder „`–-offer`“ zu filtern.</span><span class="sxs-lookup"><span data-stu-id="6f61e-109">Since the list of images in the Marketplace is very large, it is helpful to filter the list with the `--publisher`, `--sku` or `–-offer` options.</span></span>

<span data-ttu-id="6f61e-110">Verwenden Sie beispielsweise den folgenden Befehl, um _alle_ verfügbaren Wordpress-Images anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="6f61e-110">For example, try the following command to see _all_ Wordpress images available:</span></span>

```azurecli
az vm image list --sku Wordpress --output table --all
```

<span data-ttu-id="6f61e-111">Oder diesen Befehl, um alle von Microsoft bereitgestellten Images anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="6f61e-111">Or this command to see all images provided by Microsoft:</span></span>

```azurecli
az vm image list --publisher Microsoft --output table --all
```

## <a name="location-specific-images"></a><span data-ttu-id="6f61e-112">Standortspezifische Images</span><span class="sxs-lookup"><span data-stu-id="6f61e-112">Location-specific images</span></span>

<span data-ttu-id="6f61e-113">Einige Images sind nur in bestimmten Regionen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="6f61e-113">Some images are only available in certain locations.</span></span> <span data-ttu-id="6f61e-114">Fügen Sie das `--location [location]`-Flag zum Befehl hinzu, um die Ergebnisse auf diejenigen einzugrenzen, die in der Region verfügbar sind, in der Sie den virtuellen Computer erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="6f61e-114">Try adding the `--location [location]` flag to the command to scope the results to ones available in the region where you want to create the virtual machine.</span></span> <span data-ttu-id="6f61e-115">Geben Sie z.B. in Azure Cloud Shell Folgendes ein, um eine Liste der in der Region `eastus` verfügbaren Images abzurufen.</span><span class="sxs-lookup"><span data-stu-id="6f61e-115">For example, type the following into Azure Cloud Shell to get a list of images available in the `eastus` region.</span></span>

```azurecli
az vm image list --location eastus --output table
```

<span data-ttu-id="6f61e-116">Versuchen Sie, einige der Images an den anderen verfügbaren Azure-Sandboxstandorten zu überprüfen:</span><span class="sxs-lookup"><span data-stu-id="6f61e-116">Try checking some of the images in the other Azure sandbox available locations:</span></span>

[!include[](../../../includes/azure-sandbox-regions-note.md)]

> [!TIP]
> <span data-ttu-id="6f61e-117">Dies sind die Standardimages, die von Azure bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="6f61e-117">These are the standard images that are provided by Azure.</span></span> <span data-ttu-id="6f61e-118">Denken Sie daran, dass Sie auch [eigene benutzerdefinierte Images erstellen und hochladen](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images) können, um virtuelle Computer basierend auf eindeutigen Konfigurationen oder weniger häufigen Versionen oder Distributionen eines Betriebssystems zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6f61e-118">Keep in mind that you can also [create and upload your own custom images](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images) to create VMs based on unique configurations or less common versions or distributions of an operating system.</span></span>

<span data-ttu-id="6f61e-119">Ihr Befehlsfenster ist jetzt wahrscheinlich voll. Sie können `clear` eingeben, um den Bildschirm zu löschen, wenn Sie möchten.</span><span class="sxs-lookup"><span data-stu-id="6f61e-119">Your command window is probably full now, you can type `clear` to clear the screen if you like.</span></span>