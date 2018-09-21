<span data-ttu-id="03c2f-101">Angenommen, Sie möchten jetzt Text aus den vorgefertigten Bildern auslesen, die von Ihren Vertriebspartnern auf Ihrem Server bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="03c2f-101">Suppose you now want to read text from the stock images that your frontline distributors post to your server.</span></span> <span data-ttu-id="03c2f-102">Vor allem möchten Sie die Produkte scannen, um nach Werbeaufklebern mit den Verkaufspreisen zu suchen.</span><span class="sxs-lookup"><span data-stu-id="03c2f-102">In particular, you want to scan product looking for promotional stickers that containing sale prices.</span></span> <span data-ttu-id="03c2f-103">Es ist daher an der Zeit, das OCR-Feature (Optical Character Recognition) der Maschinelles Sehen-API auszuprobieren.</span><span class="sxs-lookup"><span data-stu-id="03c2f-103">It's time to try the optical character recognition (OCR) feature of the Computer Vision API.</span></span> 

## <a name="calling-the-computer-vision-api-to-extract-printed-text"></a><span data-ttu-id="03c2f-104">Aufrufen der Maschinelles Sehen-API zum Extrahieren von handschriftlichem Text</span><span class="sxs-lookup"><span data-stu-id="03c2f-104">Calling the Computer Vision API to extract printed text</span></span>

<span data-ttu-id="03c2f-105">Mit dem Vorgang `ocr` wird Text in einem Bild erkannt, und die erkannten Zeichen werden als computerlesbare Zeichenfolge extrahiert.</span><span class="sxs-lookup"><span data-stu-id="03c2f-105">The `ocr` operation detects text in an image and extracts the recognized characters into a machine-usable character stream.</span></span> <span data-ttu-id="03c2f-106">Die Anforderungs-URL hat folgendes Format:</span><span class="sxs-lookup"><span data-stu-id="03c2f-106">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr?language=<...>&detectOrientation=<...>`

<span data-ttu-id="03c2f-107">Alle Aufrufe müssen wie gewohnt für die Region erfolgen, in der das Konto erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="03c2f-107">As usual, all calls must be made to the region where the account was created.</span></span> <span data-ttu-id="03c2f-108">Für den Aufruf können zwei optionale Parameter verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="03c2f-108">The call accepts two optional parameters:</span></span>

- <span data-ttu-id="03c2f-109">**language**: Der Sprachcode des Texts, der im Bild erkannt werden soll.</span><span class="sxs-lookup"><span data-stu-id="03c2f-109">**language**: The language code of the text to be detected in the image.</span></span> <span data-ttu-id="03c2f-110">Der Standardwert ist `unk` (unknown).</span><span class="sxs-lookup"><span data-stu-id="03c2f-110">The default value is `unk`,or unknown.</span></span> <span data-ttu-id="03c2f-111">Hiermit kann der Dienst die Sprache des Texts im Bild automatisch erkennen.</span><span class="sxs-lookup"><span data-stu-id="03c2f-111">This let's the service auto detect the language of the text in the image.</span></span>
- <span data-ttu-id="03c2f-112">**detectOrientation**: Wenn dieser Parameter „true“ ist, versucht der Dienst, die Bildausrichtung zu erkennen und vor der weiteren Verarbeitung zu korrigieren (z.B. wenn das Bild auf dem Kopf steht).</span><span class="sxs-lookup"><span data-stu-id="03c2f-112">**detectOrientation**: When true, the service  tries to detect the image orientation and correct it before further processing, for example, whether the image is upside-down.</span></span> 

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="extract-printed-text-from-an-image-using-ocr"></a><span data-ttu-id="03c2f-113">Extrahieren von gedrucktem Text aus einem Bild per OCR</span><span class="sxs-lookup"><span data-stu-id="03c2f-113">Extract printed text from an image using OCR</span></span>

<span data-ttu-id="03c2f-114">Das Bild, das wir für die optische Zeichenerkennung (Optical Character Recognition, OCR) verwenden, ist das Cover des Buchs *.NET Microservices: Architecture for Containerized .NET Applications*.</span><span class="sxs-lookup"><span data-stu-id="03c2f-114">The image we're going to be using for Optical Character Recognition (OCR) is the cover from the book *.NET Microservices: Architecture for Containerized .NET Applications*.</span></span>

![Bild vom Cover des eBooks „.NET Microservices: Architecture for containerized .NET Application“](../media/5-ebook.png)

1. <span data-ttu-id="03c2f-116">Führen Sie in Cloud Shell den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="03c2f-116">Execute the following command in Cloud Shell.</span></span> <span data-ttu-id="03c2f-117">Ersetzen Sie im Befehl `<region>` durch die Region Ihres Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="03c2f-117">Replace `<region>` in the command with the region of your cognitive services account.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json"  \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/ebook.png'}" \
 | jq '.'
```

<span data-ttu-id="03c2f-118">Der folgende JSON-Code ist ein Beispiel für die Antwort, die wir für diesen Aufruf erhalten.</span><span class="sxs-lookup"><span data-stu-id="03c2f-118">The following JSON is an example of the response we get from this call.</span></span> <span data-ttu-id="03c2f-119">Einige Zeilen des JSON-Codes wurden entfernt, damit der Codeausschnitt besser auf die Seite passt.</span><span class="sxs-lookup"><span data-stu-id="03c2f-119">Some lines of JSON have been removed to make the snippet fit better on the page.</span></span>

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

<span data-ttu-id="03c2f-120">Wir sehen uns diese Antwort nun genauer an.</span><span class="sxs-lookup"><span data-stu-id="03c2f-120">Let's examine this response in more detail.</span></span> 

- <span data-ttu-id="03c2f-121">Der Dienst identifiziert für den Text die Sprache als Englisch.</span><span class="sxs-lookup"><span data-stu-id="03c2f-121">The service identified the text as being English.</span></span> <span data-ttu-id="03c2f-122">Der Wert des Felds `language` enthält den Sprachcode BCP-47 des Texts, der im Bild erkannt wurde.</span><span class="sxs-lookup"><span data-stu-id="03c2f-122">The value of the `language` field contains the BCP-47 language code of the text detected in the image.</span></span> <span data-ttu-id="03c2f-123">In diesem Beispiel ist dies **en**, also Englisch.</span><span class="sxs-lookup"><span data-stu-id="03c2f-123">In this example it is **en**, or English.</span></span> 
- <span data-ttu-id="03c2f-124">Für `orientation` wurde **up** erkannt.</span><span class="sxs-lookup"><span data-stu-id="03c2f-124">The `orientation` was detected as **up**.</span></span> <span data-ttu-id="03c2f-125">Diese Eigenschaft gibt die Richtung an, in die die Oberseite des erkannten Texts zeigt, nachdem das Bild basierend auf dem erkannten Textwinkel um seinen Mittelpunkt gedreht wurde.</span><span class="sxs-lookup"><span data-stu-id="03c2f-125">This property is the direction that the top of the recognized text is facing, after the image has been rotated around its center according to the detected text angle.</span></span> 
- <span data-ttu-id="03c2f-126">`textAngle` ist der Winkel, um den der Text gedreht werden muss, um horizontal bzw. vertikal ausgerichtet zu sein.</span><span class="sxs-lookup"><span data-stu-id="03c2f-126">The `textAngle` is the angle by which the text must be rotated to become horizontal or vertical.</span></span> <span data-ttu-id="03c2f-127">In diesem Beispiel war der Text bereits richtig horizontal ausgerichtet, sodass der zurückgegebene Wert **0** lautet.</span><span class="sxs-lookup"><span data-stu-id="03c2f-127">In this example, the text was perfectly horizontal, so the value returned is **0**.</span></span>  
- <span data-ttu-id="03c2f-128">Die `regions`-Eigenschaft enthält eine Liste mit Werten, mit denen angezeigt wird, wo sich der Text befindet: Position im Bild und das in diesem Teil des Bilds gefundene Wort.</span><span class="sxs-lookup"><span data-stu-id="03c2f-128">The `regions` property contains a list of values used to show where the text is, its position in the picture, and the word found in that part of the image.</span></span> 
- <span data-ttu-id="03c2f-129">Die vier Integers des Werts `boundingBox` sind:</span><span class="sxs-lookup"><span data-stu-id="03c2f-129">The four integers of the `boundingBox` value are:</span></span> 
    - <span data-ttu-id="03c2f-130">X-Koordinate des linken Rands</span><span class="sxs-lookup"><span data-stu-id="03c2f-130">the x-coordinate of the left edge</span></span> 
    - <span data-ttu-id="03c2f-131">Y-Koordinate des oberen Rands</span><span class="sxs-lookup"><span data-stu-id="03c2f-131">the y-coordinate of the top edge</span></span>
    - <span data-ttu-id="03c2f-132">Breite des Begrenzungsrahmens</span><span class="sxs-lookup"><span data-stu-id="03c2f-132">the width of the bounding box</span></span>
    - <span data-ttu-id="03c2f-133">Höhe des Begrenzungsrahmens</span><span class="sxs-lookup"><span data-stu-id="03c2f-133">the height of the bounding box,</span></span> 
   
    <span data-ttu-id="03c2f-134">Sie können diese Werte verwenden, um Rahmen um die einzelnen Texte zu zeichnen, die im Bild gefunden werden.</span><span class="sxs-lookup"><span data-stu-id="03c2f-134">You can use these values to draw boxes around every piece of text found in the image.</span></span>

<span data-ttu-id="03c2f-135">Wie Sie in dieser Übung sehen, liefert der `ocr`-Dienst ausführliche Informationen zum gedruckten Text eines Bilds.</span><span class="sxs-lookup"><span data-stu-id="03c2f-135">As you can see in this exercise, the `ocr` service gives detailed information about the printed text in an image.</span></span> 

<span data-ttu-id="03c2f-136">Weitere Informationen zum `ocr`-Vorgang finden Sie in der Referenzdokumentation zu [OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc).</span><span class="sxs-lookup"><span data-stu-id="03c2f-136">For more information about the `ocr` operation, see the [OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc) reference documentation.</span></span>