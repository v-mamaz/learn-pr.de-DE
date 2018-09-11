<span data-ttu-id="f37f7-101">In dieser Einheit extrahieren Sie handschriftliche Angaben aus einem Bild mit dem Maschinelles Sehen-API-Dienst, den Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="f37f7-101">In this unit, you will extract hand writing from an image with the Computer Vision API service that we created previously.</span></span>

# <a name="extracting-the-hand-writing--from-an-image"></a><span data-ttu-id="f37f7-102">Extrahieren von handschriftlichen Angaben aus einem Bild</span><span class="sxs-lookup"><span data-stu-id="f37f7-102">Extracting the hand writing  from an image</span></span>

<span data-ttu-id="f37f7-103">Führen Sie den Befehl `az cognitiveservices account keys list` aus, um einen Schlüssel zum Authentifizieren der API abzurufen.</span><span class="sxs-lookup"><span data-stu-id="f37f7-103">Execute the `az cognitiveservices account keys list` command to retrieve a key used to authenticate against the API.</span></span> <span data-ttu-id="f37f7-104">Speichern Sie die Ausgabe dieses Befehls in der Variablen `key`.</span><span class="sxs-lookup"><span data-stu-id="f37f7-104">Store the output of that command within the `key` variable.</span></span>

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

<span data-ttu-id="f37f7-105">Führen Sie einen Befehl `curl` aus, um eine HTTP-Anforderung an die Maschinelles Sehen-API auszuführen und die zuvor deklarierte Variable `key` wiederzuverwenden.</span><span class="sxs-lookup"><span data-stu-id="f37f7-105">Execute a `curl` command to do an HTTP request against the Computer Vision API and reusing the previously declared variable `key`.</span></span>

<span data-ttu-id="f37f7-106">Das Bild, das wir für die Handschrifterkennung verwenden werden, ist ein Bild dieses Notizblocks.</span><span class="sxs-lookup"><span data-stu-id="f37f7-106">The image we're going to be using for hand writing recognition is a picture of this note board.</span></span>

![Handschriftliche Eingaben](../images/handwriting.jpg)

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/recognizeText?handwriting=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/handwriting.jpg\"}" -D -
```

<span data-ttu-id="f37f7-108">Der Befehl oben gibt die Header aus.</span><span class="sxs-lookup"><span data-stu-id="f37f7-108">The command above will output the headers.</span></span> <span data-ttu-id="f37f7-109">Kopieren die `Operation-Location`-Headerwerte in den Befehl unten.</span><span class="sxs-lookup"><span data-stu-id="f37f7-109">Copy the `Operation-Location` header value into the command below.</span></span>

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>"
```

<span data-ttu-id="f37f7-110">Sie erhalten nun eine JSON-Datei, die das Ergebnis der Handschrifterkennungsanforderung enthält.</span><span class="sxs-lookup"><span data-stu-id="f37f7-110">You will now receive a JSON file containing the result of the handwriting recognition request.</span></span>

<span data-ttu-id="f37f7-111">Experimentieren Sie mit anderen Bildern, um ein anderes Ergebnis zu erhalten, indem Sie die URL ändern, die im Beispiel oben verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f37f7-111">Experiment with other images to get different result by changing the URL used in the sample above.</span></span>