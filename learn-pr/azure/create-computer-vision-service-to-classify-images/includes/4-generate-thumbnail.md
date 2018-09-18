<span data-ttu-id="3a5ef-101">In dieser Einheit generieren Sie Miniaturansichten aus einem Quellbild mit dem Maschinelles Sehen-API-Dienst, den wir zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-101">In this unit, you will generate thumbnails from a source image with the Computer Vision API service that we created previously.</span></span>

# <a name="generate-a-thumbnail-from-an-image-with-computer-vision-api"></a><span data-ttu-id="3a5ef-102">Generieren einer Miniaturansicht aus einem Bild mit der Maschinelles Sehen-API</span><span class="sxs-lookup"><span data-stu-id="3a5ef-102">Generate a thumbnail from an image with Computer Vision API</span></span>

<span data-ttu-id="3a5ef-103">Führen Sie den Befehl `az cognitiveservices account keys list` aus, um einen Schlüssel zum Authentifizieren bei der API abzurufen.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-103">Execute the `az cognitiveservices account keys list` command to retrieve a key used to authenticate against the API.</span></span> <span data-ttu-id="3a5ef-104">Speichern Sie die Ausgabe dieses Befehls in der Variablen `key`.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-104">Store the output of that command within the `key` variable.</span></span>

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

<span data-ttu-id="3a5ef-105">Führen Sie einen `curl`-Befehl aus, um eine HTTP-Anforderung an die Maschinelles Sehen-API zu richten und die zuvor deklarierte Variable `key` wiederzuverwenden.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-105">Execute a `curl` command to do an HTTP request against the Computer Vision API and reuse the previously declared variable `key`.</span></span>

<span data-ttu-id="3a5ef-106">Verschiedene Parameter können der API zur Verfügung gestellt werden, um die richtige Miniaturansicht für Ihre Anforderungen zu generieren.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-106">Different parameters can be provided to the API to generate the proper thumbnail for your needs.</span></span> <span data-ttu-id="3a5ef-107">`width` und `height` sind erforderlich und informieren die API, welche Größe für ein bestimmtes Bild benötigt wird.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-107">`width` and `height` are required and will tell the API which size you need for a specific image.</span></span> <span data-ttu-id="3a5ef-108">Schließlich generiert der Parameter `smartCropping` einen intelligenteren Zuschnitt, indem die Region analysiert wird, die für Ihr Bild von Interesse ist, um diese in der Miniaturansichten zu berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-108">Finally, the `smartCropping` parameter generates smarter cropping by analyzing the region of interest in your image to keep it within the thumbnail.</span></span> <span data-ttu-id="3a5ef-109">Wenn intelligentes Zuschneiden aktiviert ist, würde das zugeschnittene Profilbild das Gesicht einer Person beispielsweise im Bildrahmen enthalten, auch wenn das Bild nicht das gleiche Verhältnis wie das von uns gewünschte aufweist.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-109">As an example, with smart cropping enabled, a cropped profile picture would keep someone's face within the picture frame even when the picture isn't in the same ratio as the one that we asked.</span></span>

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail?width=100&height=100&smartCropping=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/mountains.jpg\"}" -o clouddrive/thumbnail.jpg
```

# <a name="downloading-the-thumbnail"></a><span data-ttu-id="3a5ef-110">Herunterladen der Miniaturansicht</span><span class="sxs-lookup"><span data-stu-id="3a5ef-110">Downloading the thumbnail</span></span>

<span data-ttu-id="3a5ef-111">Die generierte Miniaturansicht befindet sich in Ihrem Azure Cloud Shell-Speicherkonto in einer Ressourcengruppe mit dem Namen `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-111">The generated thumbnail will be found in your Azure Cloud Shell storage account within a resource group named `cloud-shell-storage-<region>`.</span></span>

1. <span data-ttu-id="3a5ef-112">Verwenden des automatisch generierten Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="3a5ef-112">Get into the automatically generated storage account.</span></span>

![Bild](../images/storage-account.png)

2. <span data-ttu-id="3a5ef-114">Klicken Sie auf den Abschnitt „Dateien“.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-114">Click on the files section.</span></span>

![Bild](../images/storage-account-click-on-files.png)

3. <span data-ttu-id="3a5ef-116">Die Miniaturansicht finden Sie im Stamm des Containers.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-116">You will find the thumbnail at the root of the container.</span></span>

![Bild](../images/storage-account-thumbnail.png)

4. <span data-ttu-id="3a5ef-118">Klicken auf die Datei, und laden Sie sie anschließend herunter.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-118">Click on the file, and then download it.</span></span>

<span data-ttu-id="3a5ef-119">Sie können das Bild mit `100x100` Pixeln in Ihrem Downloadordner mit einem beliebigen Image-Viewer öffnen.</span><span class="sxs-lookup"><span data-stu-id="3a5ef-119">From within your download folder, you can open the `100x100`-pixels image with any image viewer.</span></span>