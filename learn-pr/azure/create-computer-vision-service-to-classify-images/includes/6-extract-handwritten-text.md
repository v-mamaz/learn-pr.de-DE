In dieser Einheit extrahieren Sie handschriftliche Angaben aus einem Bild mit dem Maschinelles Sehen-API-Dienst, den Sie zuvor erstellt haben.

# <a name="extracting-the-handwriting-from-an-image"></a>Extrahieren von handschriftlichen Angaben aus einem Bild

Führen Sie den Befehl `az cognitiveservices account keys list` aus, um einen Schlüssel zum Authentifizieren bei der API abzurufen. Speichern Sie die Ausgabe dieses Befehls in der Variablen `key`.

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

Führen Sie einen `curl`-Befehl aus, um eine HTTP-Anforderung an die Maschinelles Sehen-API zu richten und die zuvor deklarierte Variable `key` wiederzuverwenden.

Das Bild, das wir für die Handschrifterkennung verwenden werden, ist ein Bild dieses Notizblocks.

![Handschrift](../images/handwriting.jpg)

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/recognizeText?handwriting=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/handwriting.jpg\"}" -D -
```

Der Befehl oben gibt die Header aus. Kopieren die `Operation-Location`-Headerwerte in den Befehl unten.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>"
```

Sie erhalten nun eine JSON-Datei, die das Ergebnis der Handschrifterkennungsanforderung enthält.

Experimentieren Sie mit anderen Bildern, um ein anderes Ergebnis zu erhalten, indem Sie die URL ändern, die im Beispiel oben verwendet wird.