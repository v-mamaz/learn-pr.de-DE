Nehmen wir an, dass Sie nun Text aus der vorhandenen Images zu lesen, die Ihre an vorderster Front Verteiler auf Ihrem Server bereitstellen möchten. Insbesondere Produkt nach Aktionspreise Aufkleber, enthält, die überprüft werden sollen Verkaufspreise. Es ist Zeit, die optische zeichenerkennung (OCR)-Funktion von der maschinelles sehen-API zu testen. 

## <a name="calling-the-computer-vision-api-to-extract-printed-text"></a>Aufrufen der maschinelles sehen-API um gedruckten Text zu extrahieren

Die `ocr` Vorgang erkennt Text in einem Bild und extrahiert die erkannten Zeichen in eine computerlesbare Zeichenfolge. Die Anforderungs-URL weist das folgende Format:

`https://[location].api.cognitive.microsoft.com/vision/v2.0/ocr[?language][&detectOrientation ] `

Wie üblich, müssen alle Aufrufe an den Speicherort ausgeführt werden, in dem das Konto erstellt wurde. Der Aufruf lässt zwei optionale Parameter:

- **Sprache**: der Sprachcode des Texts in der Abbildung erkannt wird. Der Standardwert ist `unk`, oder unbekannt. Dieser Dienst automatisch erkennen lassen Sie uns die Sprache des Texts, in der Abbildung.
- **DetectOrientation**: bei "true", der Dienst versucht, die Ausrichtung des Bilds zu erkennen und korrigieren Sie dies vor der weiteren Verarbeitung, z. B., ob das Bild ist Kopf. 

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="extract-printed-text-from-an-image-using-ocr"></a>Extrahieren Sie gedruckten Text aus einem Image mithilfe von OCR

Das Bild, das wir für die optische Zeichenerkennung (Optical Character Recognition, OCR) verwenden, ist das Umschlagbild aus dem Buch *.NET Microservices: Architecture for Containerized .NET Applications*.

![Überblick über die Abdeckung des e-Book .NET Microservices: Architektur für .NET-Containeranwendung](../media/5-ebook.png)

1. Führen Sie die folgenden Befehle in Azure Cloud Shell ein:

```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/ocr" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json"  \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/ebook.png'}" \
 | jq '.'
```

Die folgende JSON-Code ist ein Beispiel für die Antwort, die wir aus diesen Aufruf zu erhalten. Einige Zeilen der JSON-wurden entfernt, um der Ausschnitt besser auf der Seite angepasst zu machen.

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

Wir sehen uns diese Antwort noch ausführlicher. 

- Der Dienst identifiziert den Text als Englisch. Der Wert des der `language` Feld enthält den BCP-47-Sprachcode des Texts in der Abbildung. In diesem Beispiel ist dies **En**, oder als Englisch. 
- Die `orientation` wurde erkannt, als **einrichten**. Diese Eigenschaft ist die Richtung, bei der am Anfang der erkannte Text wird nach dem das Bild um seine Mitte gemäß den Textwinkel der erkannte gedreht wurde, an. 
- Die `textAngle` ist der Winkel mit dem der Text zu horizontal oder vertikal gedreht werden muss. In diesem Beispiel ist der Text, damit der zurückgegebene Wert ist perfekt horizontale wurde **0**.  
- Die `regions` Eigenschaft enthält eine Liste der Werte verwendet, um anzuzeigen, in dem der Text, seine Position in der Abbildung ist und das Wort gefunden. in diesem Teil des Bilds. 
- Die vier ganzen Zahlen, von der `boundingBox` Wert sind: 
    - die X-Koordinate des linken Rands 
    - die y-Koordinate des oberen Rands
    - die Breite des umgebenden Felds
    - die Höhe des umgebenden Felds 
   
    Sie können diese Werte verwenden, um Felder für jedes Datenelement im Abbild gefundenen Text zu zeichnen.

Wie Sie in dieser Übung sehen die `ocr` -Dienst bietet ausführliche Informationen über den gedruckten Text in einem Bild. 

Weitere Informationen zu den `ocr` Vorgang finden Sie unter den [OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc) Referenzdokumentation.