Angenommen, Sie möchten jetzt Text aus den vorgefertigten Bildern auslesen, die von Ihren Vertriebspartnern auf Ihrem Server bereitgestellt werden. Vor allem möchten Sie die Produkte scannen, um nach Werbeaufklebern mit den Verkaufspreisen zu suchen. Es ist daher an der Zeit, das OCR-Feature (Optical Character Recognition) der Maschinelles Sehen-API auszuprobieren. 

## <a name="calling-the-computer-vision-api-to-extract-printed-text"></a>Aufrufen der Maschinelles Sehen-API zum Extrahieren von handschriftlichem Text

Mit dem Vorgang `ocr` wird Text in einem Bild erkannt, und die erkannten Zeichen werden als computerlesbare Zeichenfolge extrahiert. Die Anforderungs-URL hat folgendes Format:

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr?language=<...>&detectOrientation=<...>`

Alle Aufrufe müssen wie gewohnt für die Region erfolgen, in der das Konto erstellt wurde. Für den Aufruf können zwei optionale Parameter verwendet werden:

- **language**: Der Sprachcode des Texts, der im Bild erkannt werden soll. Der Standardwert ist `unk` (unknown). Hiermit kann der Dienst die Sprache des Texts im Bild automatisch erkennen.
- **detectOrientation**: Wenn dieser Parameter „true“ ist, versucht der Dienst, die Bildausrichtung zu erkennen und vor der weiteren Verarbeitung zu korrigieren (z.B. wenn das Bild auf dem Kopf steht). 

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="extract-printed-text-from-an-image-using-ocr"></a>Extrahieren von gedrucktem Text aus einem Bild per OCR

Das Bild, das wir für die optische Zeichenerkennung (Optical Character Recognition, OCR) verwenden, ist das Cover des Buchs *.NET Microservices: Architecture for Containerized .NET Applications*.

![Bild vom Cover des eBooks „.NET Microservices: Architecture for containerized .NET Application“](../media/5-ebook.png)

1. Führen Sie in Cloud Shell den folgenden Befehl aus. Ersetzen Sie im Befehl `<region>` durch die Region Ihres Cognitive Services-Kontos.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json"  \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/ebook.png'}" \
 | jq '.'
```

Der folgende JSON-Code ist ein Beispiel für die Antwort, die wir für diesen Aufruf erhalten. Einige Zeilen des JSON-Codes wurden entfernt, damit der Codeausschnitt besser auf die Seite passt.

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

Wir sehen uns diese Antwort nun genauer an. 

- Der Dienst identifiziert für den Text die Sprache als Englisch. Der Wert des Felds `language` enthält den Sprachcode BCP-47 des Texts, der im Bild erkannt wurde. In diesem Beispiel ist dies **en**, also Englisch. 
- Für `orientation` wurde **up** erkannt. Diese Eigenschaft gibt die Richtung an, in die die Oberseite des erkannten Texts zeigt, nachdem das Bild basierend auf dem erkannten Textwinkel um seinen Mittelpunkt gedreht wurde. 
- `textAngle` ist der Winkel, um den der Text gedreht werden muss, um horizontal bzw. vertikal ausgerichtet zu sein. In diesem Beispiel war der Text bereits richtig horizontal ausgerichtet, sodass der zurückgegebene Wert **0** lautet.  
- Die `regions`-Eigenschaft enthält eine Liste mit Werten, mit denen angezeigt wird, wo sich der Text befindet: Position im Bild und das in diesem Teil des Bilds gefundene Wort. 
- Die vier Integers des Werts `boundingBox` sind: 
    - X-Koordinate des linken Rands 
    - Y-Koordinate des oberen Rands
    - Breite des Begrenzungsrahmens
    - Höhe des Begrenzungsrahmens 
   
    Sie können diese Werte verwenden, um Rahmen um die einzelnen Texte zu zeichnen, die im Bild gefunden werden.

Wie Sie in dieser Übung sehen, liefert der `ocr`-Dienst ausführliche Informationen zum gedruckten Text eines Bilds. 

Weitere Informationen zum `ocr`-Vorgang finden Sie in der Referenzdokumentation zu [OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc).