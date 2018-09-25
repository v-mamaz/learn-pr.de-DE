Vor-Ort-Vertriebspartner Ihrer Produkte scannen und laden Bilder von Ladenregalen hoch, die sie gerade auffüllen. Als leitender Entwickler in Ihrem Unternehmen sind Sie für die Erstellung von Miniaturansichten der Bilder verantwortlich. Die Miniaturansichten werden in Onlineberichten verwendet, die Sie für das Vertriebsteam erstellen. Vor kurzem hat der Vertriebsleiter mitgeteilt, dass die Bilder im Bericht verschwommen sind und oft nicht die Produktvorderseite und -mitte zeigen, was es schwierig macht, den großen Bericht zu durchsuchen. Es liegt nun an Ihnen, die Situation verbessern.

Sie entscheiden sich, die Miniaturansicht-Generierungsfunktion der Maschinelles Sehen-API auszuprobieren. Vielleicht kann sie die Aufgabe besser erledigen als die Größenänderungsfunktion, die Sie geschrieben haben.

Maschinelles Sehen generiert zunächst eine hochwertige Miniaturansicht und analysiert dann die Objekte im Bild, um den relevanten Bereich (Region Of Interest, ROI) zu bestimmen. Anschließend wird das Bild auf den relevanten Bereich zugeschnitten. Das Seitenverhältnis der generierten Miniaturansicht kann sich bei Bedarf vom Seitenverhältnis des ursprünglichen Bilds unterscheiden. Sehen Sie sich die Anwendung in Aktion an.

## <a name="calling-the-computer-vision-api-to-generate-a-thumbnail"></a>Aufrufen der Maschinelles Sehen-API zum Generieren von Miniaturansichten

Der `generateThumbnail`-Vorgang erstellt eine Miniaturansicht mit der vom Benutzer angegebenen Breite und Höhe. Der Dienst analysiert das Bild standardmäßig, identifiziert den relevanten Bereich (Region of Interest, ROI) und generiert intelligente Zuschneidekoordinaten basierend auf dem relevanten Bereich. Intelligentes Zuschneiden ist hilfreich, wenn Sie ein Seitenverhältnis angeben, das sich vom Seitenverhältnis des Eingabebilds unterscheidet. Die Anforderungs-URL weist das folgende Format auf:

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=<...>&height=<...>&smartCropping=<...>`

Verschiedene Parameter können der API zur Verfügung gestellt werden, um die richtige Miniaturansicht für Ihre Bedürfnisse zu generieren. Die `width`- und `height`-Parameter sind erforderlich. Sie informieren die API, welche Größe für ein bestimmtes Bild benötigt wird. Der Parameter `smartCropping` generiert einen intelligenteren Zuschnitt, indem der Bereich analysiert wird, der für Ihr Bild relevant ist, um diesen in der Miniaturansichten zu berücksichtigen. Wenn intelligentes Zuschneiden aktiviert ist, würde das zugeschnittene Profilbild das Gesicht einer Person beispielsweise im Bildrahmen enthalten, auch wenn das Bild ein anderes Seitenverhältnis aufweist.

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="generate-a-thumbnail"></a>Generieren von Miniaturansichten

In diesem Beispiel wird das folgende Bild verwendet. Sie können den Befehl aber auch mit URLs zu anderen Bildern verwenden.

![Bild eines weißen Hunds, der in grünem Gras sitzt.](../media/4-dog.png)

1. Führen Sie in Azure Cloud Shell die folgenden Befehle aus. Ersetzen Sie `<region>` im Befehl durch die Region Ihres Cognitive Services-Kontos.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=100&height=100&smartCropping=true" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/dog.png'}" \
-o  thumbnail.jpg
```

In diesem Beispiel fordern wir den Dienst auf, eine Miniaturansicht zu erstellen, die 100 x 100 groß ist. Intelligentes Zuschneiden ist aktiviert. Eine erfolgreiche Antwort enthält die Miniaturansicht-Binärdatei, die wir in eine Datei namens „thumbnail.jpg“ schreiben.

> [!CAUTION]
> Der `-o`-Parameter leitet die Ausgabe in eine Datei um. Die Datei wird immer überschrieben. Wenn Sie also während des Ausprobierens dieses Befehls mehrere Miniaturansichten beibehalten möchten, ändern Sie den Dateinamen.

## <a name="view-the-generated-thumbnail"></a>Anzeigen der generierten Miniaturansicht

Die generierte Miniaturansicht befindet sich in Ihrem Azure Cloud Shell-Speicherkonto. Wir haben die Datei **thumbnail.jpg** genannt.

Die Cloud Shell in Microsoft Learn bietet keine Möglichkeit, Dateien herunterzuladen, aber Sie können diese Anweisungen befolgen, um die Miniaturansicht über das Azure-Portal herunterzuladen.

1. Führen Sie die folgenden Befehle in Azure Cloud Shell aus, um zu bestätigen, dass die Datei **thumbnail.jpg** in Ihrem Basisordner vorhanden ist.

    ```azurecli
    cd ~
    ls -l
    ```



1. Führen Sie den folgenden Befehl zum Verschieben von `thumbnail.jpg` in den Ordner „clouddrive“ aus.

    ```azurecli
    mv ~/thumbnail.jpg ~/clouddrive
    ```
1. Melden Sie sich am [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit demselben Konto an, über das Sie die Sandbox aktiviert haben.
1. Wählen Sie im Bereich **Alle Ressourcen** des Portaldashboards das Speicherkonto aus, dessen Namen mit `cloudshell` beginnt.
1. Wählen Sie im Speicherkontobereich **Storage-Explorer**, **DATEIFREIGABEN** und dann die Dateifreigabe in dieser Sammlung mit dem Namen aus, der mit **cloudshellfiles*** beginnt.
1. Wählen Sie die Datei *thunbnail.jpg* und dann **Herunterladen** im oberen Menü aus, um das Bild anzuzeigen.

Der `generateThumbnail`-Vorgang ist ein leistungsstarker Miniaturansichtengenerator, der in der Lage ist, den relevanten Bereich (Region Of Interest, ROI) eines Bildes in der Miniaturansicht beizubehalten.

Weitere Informationen zum `generateThumbnails`-Vorgang finden Sie in der Referenzdokumentation zu [Abrufen der Miniaturansicht](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb).