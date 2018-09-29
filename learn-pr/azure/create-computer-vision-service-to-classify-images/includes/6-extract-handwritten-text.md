<span data-ttu-id="57df3-101">Wir haben gesehen, wie die Maschinelles Sehen-API gedruckten Text aus Bildern extrahiert.</span><span class="sxs-lookup"><span data-stu-id="57df3-101">We saw how the Computer Vision API can extract printed text from images.</span></span> <span data-ttu-id="57df3-102">In dieser Übung verwenden wir den Dienst, um handschriftlichen Text zu erkennen.</span><span class="sxs-lookup"><span data-stu-id="57df3-102">In this exercise, we'll use the service to detect handwritten text.</span></span>

## <a name="calling-the-computer-vision-api-to-extract-handwritten-text"></a><span data-ttu-id="57df3-103">Aufrufen der Maschinelles Sehen-API, um handschriftlichen Text zu extrahieren</span><span class="sxs-lookup"><span data-stu-id="57df3-103">Calling the Computer Vision API to extract handwritten text</span></span>

<span data-ttu-id="57df3-104">Der Vorgang `recognizeText` erkennt und extrahiert handschriftlichen Text in Notizen, Briefen, Abhandlungen, Tafelbildern, Formularen und anderen Quellen.</span><span class="sxs-lookup"><span data-stu-id="57df3-104">The `recognizeText` operation detects and extracts handwritten text from notes, letters, essays, whiteboards, forms, and other sources.</span></span> <span data-ttu-id="57df3-105">Die Anforderungs-URL hat folgendes Format:</span><span class="sxs-lookup"><span data-stu-id="57df3-105">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=<...>`

<span data-ttu-id="57df3-106">Alle Aufrufe müssen an den Standort gerichtet werden, an dem das Konto erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="57df3-106">All calls must be made to the region where the account was created.</span></span>

<span data-ttu-id="57df3-107">Der Parameter `mode` muss, sofern vorhanden, auf `Handwritten` oder `Printed` festgelegt werden (Beachten Sie die Groß-/Kleinschreibung).</span><span class="sxs-lookup"><span data-stu-id="57df3-107">If present, the `mode` parameter must be set to `Handwritten` or `Printed` and is case-sensitive.</span></span> <span data-ttu-id="57df3-108">Ist der Parameter auf `Handwritten` festgelegt oder nicht vorhanden, wird eine Handschrifterkennung durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="57df3-108">If the parameter is set to `Handwritten` or is not specified, handwriting recognition is performed.</span></span> <span data-ttu-id="57df3-109">Ist der Parameter auf `Printed` festgelegt, wird eine Erkennung von gedrucktem Text durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="57df3-109">If the parameter is set to `Printed`, then printed text recognition is performed.</span></span> <span data-ttu-id="57df3-110">Die Dauer bis zur Rückgabe eines Ergebnisses für diesen Aufruf hängt von der Textmenge auf dem Bild ab.</span><span class="sxs-lookup"><span data-stu-id="57df3-110">The time it takes to get a result from this call depends on the amount of writing in the image.</span></span>

<span data-ttu-id="57df3-111">Dieses Beispiel umfasst Folgendes:</span><span class="sxs-lookup"><span data-stu-id="57df3-111">In this example, we'll:</span></span>

- <span data-ttu-id="57df3-112">Ausgeben der Antwortheader an die Konsole mithilfe der cURL-Option `-D`</span><span class="sxs-lookup"><span data-stu-id="57df3-112">Print the response headers to the console using cUrl's `-D` option</span></span>
- <span data-ttu-id="57df3-113">Kopieren des Werts des Headers `Operation-Location` aus den in der Antwort zurückgegebenen Headern</span><span class="sxs-lookup"><span data-stu-id="57df3-113">Copy the `Operation-Location` header value from the headers we receive in the response</span></span>
- <span data-ttu-id="57df3-114">Überprüfen der URL, die von `Operation-Location` für die Ergebnisse angegeben wird (nach einer Wartezeit von einigen Sekunden)</span><span class="sxs-lookup"><span data-stu-id="57df3-114">After a few seconds, check the URL specified by the `Operation-Location` for the results</span></span>

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="detect-and-extract-handwritten-text-from-an-image"></a><span data-ttu-id="57df3-115">Erkennen und Extrahieren von handschriftlichem Text in einem Bild</span><span class="sxs-lookup"><span data-stu-id="57df3-115">Detect and extract handwritten text from an image</span></span>

<span data-ttu-id="57df3-116">In diesem Beispiel wird das folgende Bild verwendet. Sie können den Befehl aber auch mit URLs zu anderen Bildern verwenden.</span><span class="sxs-lookup"><span data-stu-id="57df3-116">We'll use the following image in this example, but you're free to try the same command with URLs to other images.</span></span>

![Bild mit handschriftlichem Text auf einem Notizzettel](../media/6-handwriting.jpg)

1. <span data-ttu-id="57df3-118">Führen Sie in Azure Cloud Shell die folgenden Befehle aus:</span><span class="sxs-lookup"><span data-stu-id="57df3-118">Execute the following commands in Azure Cloud Shell.</span></span> <span data-ttu-id="57df3-119">Ersetzen Sie im Befehl `<region>` durch die Region Ihres Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="57df3-119">Replace `<region>` in the command with the region of your cognitive services account.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=Handwritten" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/handwriting.jpg'}" \
-D - 
```

<span data-ttu-id="57df3-120">Dadurch werden die Header dieses Vorgangs an die Konsole übergeben.</span><span class="sxs-lookup"><span data-stu-id="57df3-120">The above dumps the headers of this operation to the console.</span></span> <span data-ttu-id="57df3-121">Ein Beispiel:</span><span class="sxs-lookup"><span data-stu-id="57df3-121">Here's an example:</span></span>

```azurecli
HTTP/1.1 202 Accepted
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Expires: -1
Operation-Location: https://westus2.api.cognitive.microsoft.com/vision/v2.0/textOperations/d0e9b397-4072-471c-ae61-7490bec8f077
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
apim-request-id: f5663487-03c6-4760-9be7-c9157fac10a1
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
x-content-type-options: nosniff
Date: Wed, 12 Sep 2018 19:22:00 GMT
```

<span data-ttu-id="57df3-122">Im Header `Operation-Location` werden nach Abschluss des Vorgangs die Ergebnisse veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="57df3-122">The `Operation-Location` header is where the results will be posted once complete.</span></span>

2. <span data-ttu-id="57df3-123">Kopieren Sie den Wert des Headers `Operation-Location`.</span><span class="sxs-lookup"><span data-stu-id="57df3-123">Copy the `Operation-Location` header value.</span></span>
1. <span data-ttu-id="57df3-124">Führen Sie in Azure Cloud Shell den folgenden Befehl aus, und ersetzen Sie dabei `"<Operation-Location>"` durch den Wert des Headers **Operation-Location**, den Sie im vorherigen Schritt kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="57df3-124">Execute the following command in Azure Cloud Shell replacing `"<Operation-Location>"` with the value for the **Operation-Location** header you copied from the preceding step.</span></span>

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>" | jq '.'
```

<span data-ttu-id="57df3-125">Nach Abschluss des Vorgangs erhalten Sie eine JSON-Datei, die das Ergebnis der Handschrifterkennungsanforderung enthält.</span><span class="sxs-lookup"><span data-stu-id="57df3-125">If the operation has completed, you'll receive a JSON file containing the result of the handwriting recognition request.</span></span>

<span data-ttu-id="57df3-126">Weitere Informationen zum Vorgang `recognizeText` finden Sie in der Referenzdokumentation zum [Analysieren von handschriftlichem Text](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200).</span><span class="sxs-lookup"><span data-stu-id="57df3-126">For more information about the `recognizeText` operation, see the [Recognize Handwritten Text](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) reference documentation.</span></span>