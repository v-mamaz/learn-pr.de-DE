In dieser Einheit analysieren Sie Bilder mit dem Maschinelles Sehen-API-Dienst, den wir im vorherigen Schritt erstellt haben.

# <a name="analyzing-an-image-with-computer-vision-api"></a>Analysieren eines Bilds mit der Maschinelles Sehen-API

Führen Sie den Befehl `az cognitiveservices account keys list` aus, um einen Schlüssel zum Authentifizieren der API abzurufen. Speichern Sie die Ausgabe dieses Befehls in der Variablen `key`.

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

Führen Sie einen Befehl `curl` aus, um eine HTTP-Anforderung an die Maschinelles Sehen-API auszuführen und die zuvor deklarierte Variable `key` wiederzuverwenden.

Die Parameter `visualFeatures`, `details` und `languages` werden an den Dienst gesendet. Während der Dienst ohne sie weiterhin funktioniert, geben sie Hinweise zum Inhalt der Bilder. Als Beispiel kann `details` auf `Landmarks` oder `Celebrities` festgelegt werden, um Sehenswürdigkeiten oder Prominente zu erkennen. `visualFeatures` identifizieren, welche Art von Informationen der Dienst an Sie zurückgeben soll. Die `Categories`-Option kategorisiert den Inhalt der Bilder, z.B. Bäume, Gebäude usw. `Faces` identifiziert die Gesichter von Personen und gibt ihr Geschlecht und Alter an.

Weitere Informationen finden Sie in [der Dokumentation](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).

Lassen Sie uns vorerst Sehenswürdigkeiten identifizieren, indem der Dienst `Categories` und `Description` zurückgibt.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Categories,Description&details=Landmarks" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/mountains.jpg\"}"
```

Das Ergebnis der Anforderung sind JSON-Rohdaten, die das Bild in der `url` beschreiben. Wir können auch ` | jq '.'` am Ende hinzufügen, um die JSON-Ausgabe zu optimieren.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Categories,Description&details=Landmarks&language=en" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/mountains.jpg\"}" | jq '.'
```

Kopieren Sie den Link zu anderen online gefundenen Bildern, und testen Sie den Dienst, indem Sie die URL in den oben aufgeführten Befehlen ersetzen.