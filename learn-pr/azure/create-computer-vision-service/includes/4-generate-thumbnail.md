In dieser Einheit generieren Sie Miniaturansichten aus einem Quellbild mit dem Maschinelles Sehen-API-Dienst, den wir zuvor erstellt haben.

# <a name="generate-a-thumbnail-from-an-image-with-computer-vision-api"></a>Generieren einer Miniaturansicht aus einem Bild mit der Maschinelles Sehen-API

Führen Sie den Befehl `az cognitiveservices account keys list` aus, um einen Schlüssel zum Authentifizieren der API abzurufen. Speichern Sie die Ausgabe dieses Befehls in der Variablen `key`.

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

Führen Sie einen Befehl `curl` aus, um eine HTTP-Anforderung an die Maschinelles Sehen-API auszuführen und die zuvor deklarierte Variable `key` wiederzuverwenden.

Verschiedene Parameter können der API zur Verfügung gestellt werden, um die richtige Miniaturansicht für Ihre Anforderungen zu generieren. `width` und `height` sind erforderlich und informieren die API, welche Größe für ein bestimmtes Bild benötigt wird. Schließlich generiert der Parameter `smartCropping` einen intelligenteren Zuschnitt, indem die Region analysiert wird, die für Ihr Bild von Interesse ist, um diese in der Miniaturansichten zu berücksichtigen. Wenn intelligentes Zuschneiden aktiviert ist, würde das zugeschnittene Profilbild das Gesicht einer Person beispielsweise im Bildrahmen enthalten, auch wenn das Bild nicht das gleiche Verhältnis wie das von uns gewünschte aufweist.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail?width=100&height=100&smartCropping=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/mountains.jpg\"}" -o clouddrive/thumbnail.jpg
```

# <a name="downloading-the-thumbnail"></a>Herunterladen der Miniaturansicht

Die generierte Miniaturansicht befindet sich in Ihrem Cloud Shell-Speicherkonto in einer Ressourcengruppe mit dem Namen `cloud-shell-storage-<region>`.

1. Verwenden des automatisch generierten Speicherkontos

![Bild](../images/storage-account.png)

2. Klicken im Abschnitt „Dateien“

![Bild](../images/storage-account-click-on-files.png)

3. Die Miniaturansicht finden Sie im Stamm des Containers.

![Bild](../images/storage-account-thumbnail.png)

4. Klicken auf die Datei und anschließendes Herunterladen

Sie können das Bild mit `100x100` Pixeln mit einem beliebigen Image-Viewer aus Ihrem Downloadordner öffnen.