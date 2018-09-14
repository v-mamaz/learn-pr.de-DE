Wir haben gesehen, wie das Computer Vision-API gedruckten Text aus Bildern extrahiert werden können. In dieser Übung verwenden wir den Dienst handschriftlichen Text zu erkennen.

## <a name="calling-the-computer-vision-api-to-extract-handwritten-text"></a>Aufrufen der maschinelles sehen-API zum Extrahieren von handschriftlichen text

Die `recognizeText` Vorgang erkennt und extrahiert Sie handschriftlichen Text aus den Anmerkungen zu dieser Version, Buchstaben, Abhandlungen, tafelbildern, Formularen und anderen Quellen. Die Anforderungs-URL weist das folgende Format:

`https://[location].api.cognitive.microsoft.com/vision/v2.0/recognizeText[?mode] `

Wie üblich, müssen alle Aufrufe an den Speicherort ausgeführt werden, in dem das Konto erstellt wurde. Wenn die `mode` Parameter Ust festgelegt werden, um `Handwritten` oder `Printed` und Groß-/Kleinschreibung beachtet wird. Wenn der Parameter, um festgelegt ist `Handwritten` oder ist nicht angegeben ist, ist handschrifterkennung erfolgt. Andernfalls legen Sie den Parameter auf `Printed` gedruckte texterkennung wird durch Aufrufen von OCR-Vorgang ausgeführt.

Der Zeitaufwand für das um ein Ergebnis dieses Aufrufs zu erhalten, hängt von den Betrag der Handschrift in der Abbildung ab. Wir müssen also möglicherweise einige Sekunden warten. In diesem Beispiel werden wir daher:

- Sichern Sie die Header der Antwort an die Konsole, die mithilfe von cUrl die `-D` Option
- Kopieren der `Operation-Location` Headerwert aus den Headern, die wir, in der Antwort erhalten
- Überprüfen Sie nach wenigen Sekunden wird die URL, die gemäß der `Operation-Location` für die Ergebnisse

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="detect-and-extract-handwritten-text-from-an-image"></a>Erkennen und Extrahieren von handschriftlichem Text aus einem Bild

Wir verwenden die folgende Abbildung in diesem Beispiel, aber Sie können den gleichen Befehl mit URLs zu anderen Images versuchen Sie es.

![Bild einer Handschrift-Beispiel für eine Anmerkung](../media/6-handwriting.jpg)

1. Führen Sie die folgenden Befehle in Azure Cloud Shell ein:

```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=Handwritten" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/handwriting.jpg'}" \
-D - 
```

Die oben genannten sichert die Header für diesen Vorgang an die Konsole. Hier sehen Sie ein Beispiel:

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

Die `Operation-Location` -Header ist, in dem die Ergebnisse nach Abschluss des Vorgangs ausgegeben wird.

2. Kopieren der `Operation-Location` Headerwert.
1. Führen Sie den folgenden Befehl in Azure Cloud Shell ersetzen `"<Operation-Location>"` mit dem Wert für die **Operation-Location** Header, die Sie aus dem vorherigen Schritt kopiert haben.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>" | jq '.'
```

Wenn der Vorgang abgeschlossen wurde, erhalten Sie eine JSON-Datei, die das Ergebnis der Erkennung Handschrift-Anforderung.

Weitere Informationen zu den `recognizeText` Vorgang finden Sie unter der [Erkennung von handschriftlichem Text](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) Referenzdokumentation.