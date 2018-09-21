Wir haben gesehen, wie die Maschinelles Sehen-API gedruckten Text aus Bildern extrahiert. In dieser Übung verwenden wir den Dienst, um handschriftlichen Text zu erkennen.

## <a name="calling-the-computer-vision-api-to-extract-handwritten-text"></a>Aufrufen der Maschinelles Sehen-API, um handschriftlichen Text zu extrahieren

Der Vorgang `recognizeText` erkennt und extrahiert handschriftlichen Text in Notizen, Briefen, Abhandlungen, Tafelbildern, Formularen und anderen Quellen. Die Anforderungs-URL hat folgendes Format:

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=<...>`

Alle Aufrufe müssen an den Standort gerichtet werden, an dem das Konto erstellt wurde.

Der Parameter `mode` muss, sofern vorhanden, auf `Handwritten` oder `Printed` festgelegt werden (Beachten Sie die Groß-/Kleinschreibung). Ist der Parameter auf `Handwritten` festgelegt oder nicht vorhanden, wird eine Handschrifterkennung durchgeführt. Ist der Parameter auf `Printed` festgelegt, wird eine Erkennung von gedrucktem Text durchgeführt. Die Dauer bis zur Rückgabe eines Ergebnisses für diesen Aufruf hängt von der Textmenge auf dem Bild ab.

Dieses Beispiel umfasst Folgendes:

- Ausgeben der Antwortheader an die Konsole mithilfe der cURL-Option `-D`
- Kopieren des Werts des Headers `Operation-Location` aus den in der Antwort zurückgegebenen Headern
- Überprüfen der URL, die von `Operation-Location` für die Ergebnisse angegeben wird (nach einer Wartezeit von einigen Sekunden)

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="detect-and-extract-handwritten-text-from-an-image"></a>Erkennen und Extrahieren von handschriftlichem Text in einem Bild

In diesem Beispiel wird das folgende Bild verwendet. Sie können den Befehl aber auch mit URLs zu anderen Bildern verwenden.

![Bild mit handschriftlichem Text auf einem Notizzettel](../media/6-handwriting.jpg)

1. Führen Sie in Azure Cloud Shell die folgenden Befehle aus: Ersetzen Sie im Befehl `<region>` durch die Region Ihres Cognitive Services-Kontos.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=Handwritten" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/handwriting.jpg'}" \
-D - 
```

Dadurch werden die Header dieses Vorgangs an die Konsole übergeben. Ein Beispiel:

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

Im Header `Operation-Location` werden nach Abschluss des Vorgangs die Ergebnisse veröffentlicht.

2. Kopieren Sie den Wert des Headers `Operation-Location`.
1. Führen Sie in Azure Cloud Shell den folgenden Befehl aus, und ersetzen Sie dabei `"<Operation-Location>"` durch den Wert des Headers **Operation-Location**, den Sie im vorherigen Schritt kopiert haben.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>" | jq '.'
```

Nach Abschluss des Vorgangs erhalten Sie eine JSON-Datei, die das Ergebnis der Handschrifterkennungsanforderung enthält.

Weitere Informationen zum Vorgang `recognizeText` finden Sie in der Referenzdokumentation zum [Analysieren von handschriftlichem Text](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200).