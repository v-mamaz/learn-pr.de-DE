<span data-ttu-id="a739b-101">In dieser Einheit extrahieren Sie Text aus einem Bild mit dem Maschinelles Sehen-API-Dienst, den Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="a739b-101">In this unit, you will extract text from an image with the Computer Vision API service that we created previously.</span></span>

# <a name="extracting-the-text-from-an-image"></a><span data-ttu-id="a739b-102">Extrahieren von Text aus einem Bild</span><span class="sxs-lookup"><span data-stu-id="a739b-102">Extracting the text from an image</span></span>

<span data-ttu-id="a739b-103">Führen Sie den Befehl `az cognitiveservices account keys list` aus, um einen Schlüssel zum Authentifizieren bei der API abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a739b-103">Execute the `az cognitiveservices account keys list` command to retrieve a key used to authenticate against the API.</span></span> <span data-ttu-id="a739b-104">Speichern Sie die Ausgabe dieses Befehls in der Variablen `key`.</span><span class="sxs-lookup"><span data-stu-id="a739b-104">Store the output of that command within the `key` variable.</span></span>

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

<span data-ttu-id="a739b-105">Führen Sie einen `curl`-Befehl aus, um eine HTTP-Anforderung an die Maschinelles Sehen-API zu richten und die zuvor deklarierte Variable `key` wiederzuverwenden.</span><span class="sxs-lookup"><span data-stu-id="a739b-105">Execute a `curl` command to do an HTTP request against the Computer Vision API and reuse the previously declared variable `key`.</span></span>

<span data-ttu-id="a739b-106">Das Bild, das wir für die optische Zeichenerkennung (Optical Character Recognition, OCR) verwenden, ist das Cover des Buchs [.NET Microservices: Architecture for Containerized .NET Applications](/dotnet/standard/microservices-architecture/).</span><span class="sxs-lookup"><span data-stu-id="a739b-106">The image we're going to be using for Optical Character Recognition (OCR) is the cover from the book [.NET Microservices: Architecture for Containerized .NET Applications](/dotnet/standard/microservices-architecture/).</span></span>

![E-Book-Cover](../images/ebook.png)

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/ocr" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/ebook.png\"}" | jq '.'
```

<span data-ttu-id="a739b-108">Die ersten drei Eigenschaften sind Sprache, Ausrichtung und Textwinkel.</span><span class="sxs-lookup"><span data-stu-id="a739b-108">The first three properties are the language, the orientation, and the text angle.</span></span> <span data-ttu-id="a739b-109">Dann enthalten die `regions`-Eigenschaften eine Liste von Werten, die anzeigen, wo sich der Text befindet, welche Position er im Bild hat und welche Wörter tatsächlich enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="a739b-109">Then, the `regions` properties will contain a list of values used to show where the text is, its position in the picture, and the actual words it contains.</span></span>

```json
{
  "language": "en",
  "orientation": "Up",
  "textAngle": 0,
  "regions" : [
        /*... snipped*/
        {
          "boundingBox": "766,1419,302,33",
          "words": [
            {
              "boundingBox": "766,1419,126,25",
              "text": "Microsoft"
            },
            {
              "boundingBox": "903,1420,165,32",
              "text": "Corporation"
            }
          ]
        }]
}
```

<span data-ttu-id="a739b-110">Experimentieren Sie mit anderen Bildern, um ein anderes Ergebnis zu erhalten, indem Sie die URL ändern, die im Beispiel oben verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a739b-110">Experiment with other images to get different results by changing the URL used in the sample above.</span></span>