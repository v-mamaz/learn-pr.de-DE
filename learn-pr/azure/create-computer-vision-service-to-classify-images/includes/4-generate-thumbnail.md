An vorderster Front Verteiler an Ihren Produkten überprüfen und Hochladen von Bildern von Regalen, die sie aufgefüllt werden. Da Entwickler in Ihrem Unternehmen führen zu können, erstellen Sie die Miniaturansichten der Bilder. Miniaturansichten werden in den online-Berichten, die Sie erstellen für das Vertriebsteam verwendet. Vor kurzem, sagte der Vertriebsleiter, dass die Bilder im Bericht Webvideos werden verwischt und häufig nicht haben, das Produkt und in den Mittelpunkt, wodurch es schwierig ist, überprüfen Sie die umfangreichen Bericht. Es liegt an Ihnen, die Situation verbessern.

Möchten Sie die Generierung von Miniaturansichten-Funktion von der maschinelles sehen-API zu testen. Möglicherweise kann besser als die Größenänderung-Funktion werden, die Sie geschrieben haben.

Maschinelles sehen zuerst eine hochwertige vorschauminiatur generiert und dann analysiert die Objekte in das Bild, das den Bereich von Interesse sind (ROI) zu ermitteln. Anschließend wird das Bild auf den relevanten Bereich zugeschnitten. Das Seitenverhältnis der generierten Miniaturansicht kann sich bei Bedarf vom Seitenverhältnis des ursprünglichen Bilds unterscheiden. Sehen Sie sich die Anwendung in Aktion an.

## <a name="calling-the-computer-vision-api-to-generate-a-thumbnail"></a>Aufrufen der maschinelles sehen-API um eine Miniaturansicht zu generieren.

Die `generateThumbnail` Vorgang wird eine Miniaturansicht erstellt, mit der Benutzer angegebenen Breite und Höhe. Der Dienst standardmäßig analysiert das Bild, identifiziert die Region von Interesse sind (ROI) und intelligente Zuschneiden Koordinaten, die basierend auf den ROI generiert. Intelligentes Zuschneiden kann, wenn Sie ein Seitenverhältnis angeben, das Seitenverhältnis des Bildes unterscheidet. Die Anforderungs-URL weist das folgende Format:

`https://[location].api.cognitive.microsoft.com/vision/v2.0/generateThumbnail[?width][&height][&smartCropping]`

Verschiedene Parameter können der API zur Verfügung gestellt werden, um die richtige Miniaturansicht für Ihre Anforderungen zu generieren. Die `width` und `height` Parameter sind erforderlich. Sie informieren der API, welche Größe Sie für ein bestimmtes Image benötigen. Die `smartCropping` Parameter generiert intelligenter zuschneiden, durch die Analyse der Region von Interesse in Ihrem Image in die Miniaturansicht aufbewahrt. Beispielsweise würden mit intelligentes Zuschneiden aktiviert ist, ein zugeschnittenes Profilbild halten ein Gesicht im Bild-Frame selbst, wenn das Bild auf einem anderen Seitenverhältnis hat.

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="generate-a-thumbnail"></a>Generieren von Miniaturansichten

Wir verwenden die folgende Abbildung in diesem Beispiel, aber Sie können den gleichen Befehl mit URLs zu anderen Images versuchen Sie es. 

![Überblick über die ein niedliches weißer Hund im grünen Gras.](../media/4-dog.png)

1. Führen Sie die folgenden Befehle in Azure Cloud Shell ein:

```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=100&height=100&smartCropping=true" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/dog.png'}" \
-o  thumbnail.jpg
```

In diesem Beispiel fordern wir den Dienst, eine Miniaturansicht zu erstellen, die 100 x 100 ist. Intelligentes Zuschneiden ist aktiviert. Eine erfolgreiche Antwort enthält die Miniaturansicht Binärdatei, die wir in eine Datei namens thumbnail.jpg schreiben.  

> [!CAUTION]
> Die `-o` Parameter wird die Ausgabe in eine Datei. Die Datei immer überschrieben, daher sollten Sie um mehr als eine Miniaturansicht zu halten, während Sie mit diesem Befehl versucht, den Dateinamen ändern.

## <a name="downloading-the-thumbnail"></a>Herunterladen der Miniaturansicht

Die generierte Miniaturansicht wird in Ihrem Azure Cloud Shell-Storage-Konto gefunden. Wir mit dem Namen der das **thumbnail.jpg**. 

1. Führen Sie die folgenden Befehle in Azure Cloud Shell aus, um zu bestätigen, dass die Datei **thumbnail.jg** in Ihrem Ordner "home" vorhanden ist.

```azurecli
cd ~
ls -l
```
2. Wählen Sie im Menü Cloud Shell **hoch-und Herunterladen von Dateien**, und wählen Sie dann **herunterladen** aus dem Dropdownmenü aus.

3. In der **Herunterladen einer Datei** Dialogfeld, das angezeigt wird, geben Sie **thumbnail.jpg** in das Pflichtfeld und wählen **herunterladen**. Der Download des Bilds auf Ihrem lokalen Computer wird gestartet.

4. Suchen Sie das heruntergeladene Bild **thumbnail.jpg** in Ihrem Ordner "Downloads". Öffnen Sie das Image in Ihrer bevorzugten Image-Viewer, um die Miniaturansicht anzuzeigen, die erstellt wurde.

Die `generateThumbnail` Vorgang ist ein leistungsfähiges Miniaturansicht-Generator, der die Region von Interesse sind (ROI) eines Bilds in der Miniaturansicht beibehalten kann. 

Weitere Informationen zu den `generateThumbnails` Vorgang finden Sie unter den [Miniaturansicht zu erhalten](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb) Referenzdokumentation.