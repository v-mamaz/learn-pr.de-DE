Als leitender Entwickler bei Contoso trinken Verteilung Sie sind verantwortlich für die Erstellung und Wartung einer Line-of-Business-Apps, mit dem Ihre an vorderster Front Verteiler überprüfen und Hochladen von Bildern der Store-Fächer, in dem sie aufgefüllt werden. 

Überprüfen, dass die Regeln fest, die Ihrem Unternehmen, keine Bilder, die von Benutzern bereitgestellt berücksichtigen werden sollen. Das Unternehmen soll nicht mehr unerwünschten Inhalten, die an Standorten des Unternehmens gesendet. Wenn die Fortschritten, künstliche Intelligenz, möchten Sie das Computer Vision-API in Ihrer app zu verwenden. 

Zunächst erstellen Sie ein maschinelles sehen-Konto im Azure-Abonnement, und Testen der **analysieren** Feature.

## <a name="calling-the-computer-vision-api-to-analyze-images"></a>Aufrufen der maschinelles sehen-API um Images zu analysieren

Die `analyze` Vorgang extrahiert eine Vielzahl von visuellen basierend auf den Inhalt des Features.  Die Anforderungs-URL weist das folgende Format:

`https://[location].api.cognitive.microsoft.com/vision/v2.0/analyze[?visualFeatures][&details][&language] `

Die Parameter `visualFeatures`, `details` und `languages` werden an den Dienst gesendet. Legen Sie die `details` Parameter `Landmarks` oder `Celebrities` zum Orientierungspunkte oder berühmte Personen erkennen. `visualFeatures` identifizieren, welche Art von Informationen der Dienst an Sie zurückgeben soll. Die `Categories` Option wird den Inhalt der Images wie Strukturen, Gebäude und vieles mehr zu kategorisieren. `Faces` identifiziert die Gesichter von Personen und gibt ihr Geschlecht und Alter an.

Alle Vorgänge auf dem Computer Vision-API gelten die folgenden Einschränkungen auf, wenn es sich um die Images geht, die Sie zu stellen:

- Unterstützte Bildformate: JPEG, PNG, GIF, BMP 
- Image-Dateigröße muss weniger als 4 MB sein.
- Bildmaße muss über mindestens 50 x 50.

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="identify-landmarks-in-an-image"></a>Identifizieren Sie Orientierungspunkte in einem Bild

Beginnen wir mit einem Aufruf von Orientierungspunkte in einem Image suchen. Wir verwenden die folgende Abbildung in diesem Beispiel, aber Sie können den gleichen Befehl mit URLs zu anderen Images versuchen Sie es. 

![Bild eines Mountain-Bereichs mit blauen Wetter über den snow-capped bergen.](../media/3-mountains.jpg)

1. Führen Sie in Azure Cloud Shell folgenden Befehl aus:

<!-- TODO Replace image URL with one that points to an image in the sample repo -->
```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/mountains.jpg'}" \
| jq '.'
```

Dieser Aufruf sucht nach Orientierungspunkte in der Abbildung, die durch die Bild-URL angegeben. Der Aufruf gebeten, den Dienst an Informationen zu Auftragskategorien und eine Beschreibung des Images zurückzugeben. Die Beschreibung wird als vollständiger englische Satz zurückgegeben. Wie Sie wissen, benötigt jeder Aufruf an die API einen Zugriffsschlüssel. Diese Einstellung für jeden Aufruf mit der `Ocp-Apim-Subscription-Key` Header. 

> [!TIP]
> Das Ergebnis der Anforderung sind JSON-Rohdaten, die das Bild in der `url` beschreiben. Wir haben hinzugefügt ` | jq '.'` am Ende des Befehls, der Datei optimieren, den JSON-Code ausgegeben.

Die JSON-Antwort in diesem Beispiel wird zurückgegeben:

- Ein `categories` Array alle Image-Kategorien, die erkannt wurden, sowie eine Bewertung zwischen 0 und 1 des Falls Ja: wie der Dienst ist, dass das Bild in der angegebenen Kategorie gehört, auflistet.
- Ein `description` Eintrag mit einem Array von Tags oder Wörter, die auf das Bild beziehen.
- Ein `captions` Eintrag mit einem Textfeld, das in englischer Sprache Informationen zu Neuheiten in der Abbildung. Beachten Sie, dass der Text auch eine Bewertung der Sicherheit verfügt. Diese Bewertung können Sie entscheiden, was Sie tun, diese Analyse.


## <a name="check-for-inappropriate-content-in-an-image"></a>Überprüfung auf anstößige Inhalte in einem Bild

In diesem Beispiel werden wir ein Bild für nicht jugendfreie Inhalte analysieren. Das vertrauensergebnis bewertet die Wahrscheinlichkeit, dass das Image entweder nicht jugendfreie oder rassistische Inhalte enthält. 

Wir verwenden die folgende Abbildung in diesem Beispiel, aber Sie können den gleichen Befehl mit URLs zu anderen Images versuchen Sie es. 

![Bild einer lächelnden Familie.](../media/3-people.png)

1. Führen Sie in Azure Cloud Shell folgenden Befehl aus:

```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Adult,Description" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/people.png'}" \
| jq '.'
```

In diesem Beispiel legen wir die `visualFeatures` zu `Adult,Description`. Die Antwort erhalten wir zwei vertrauensergebnisse, eine für rassistische Inhalte und eine für nicht jugendfreie Inhalte. Verwenden diese Bewertungen plus der Beschreibung des Images und andere visuelle Features, können Sie beginnen, kennzeichnen von Images, die an den Server gesendet.

Die Beispiele, die wir in dieser Übung versucht vermitteln Ihnen einen Eindruck von den Typ der Analyse, die Verwendungsmöglichkeiten der `analyze` Vorgang. Testen Sie die Analyse mit anderen Bildern, und versuchen Sie es verschiedene Kombinationen von Parametern für VisualFeatures, Details und Sprachen.

Weitere Informationen zu den `analyze` -Vorgang finden Sie unter der [analysieren Image](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) Referenzdokumentation.