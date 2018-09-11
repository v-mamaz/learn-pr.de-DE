In dieser Einheit extrahieren Sie Text aus einem Bild mit dem Maschinelles Sehen-API-Dienst, den Sie zuvor erstellt haben.

# <a name="extracting-the-text-from-an-image"></a>Extrahieren von Text aus einem Bild

Führen Sie den Befehl `az cognitiveservices account keys list` aus, um einen Schlüssel zum Authentifizieren der API abzurufen. Speichern Sie die Ausgabe dieses Befehls in der Variablen `key`.

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

Führen Sie einen Befehl `curl` aus, um eine HTTP-Anforderung an die Maschinelles Sehen-API auszuführen und die zuvor deklarierte Variable `key` wiederzuverwenden.

Das Bild, das wir für die optische Zeichenerkennung (Optical Character Recognition, OCR) verwenden, ist das Umschlagbild aus dem Buch [.NET Microservices: Architecture for Containerized .NET Applications](/dotnet/standard/microservices-architecture/).

![E-Book-Umschlagbild](../images/ebook.png)

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/ocr" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/ebook.png\"}" | jq '.'
```

Die ersten drei Eigenschaften sind die Sprache, die Ausrichtung sowie der Textwinkel. Dann enthalten die `regions`-Eigenschaften eine Liste von Werten, die anzeigen, wo sich der Text befindet, welche Position er im Bild hat und welche Wörter tatsächlich enthalten sind.

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

Experimentieren Sie mit anderen Bildern, um ein anderes Ergebnis zu erhalten, indem Sie die URL ändern, die im Beispiel oben verwendet wird.