Als leitender Entwickler bei Contoso Beverage Distribution sind Sie für den Aufbau und die Pflege einer Branchenanwendung verantwortlich, mit der Ihre Vertriebspartner Bilder von Ladenregalen scannen und hochladen können, in denen sie ihre Bestände auffüllen. 

Sie sollten überprüfen, ob alle von Benutzern geposteten Bilder die von Ihrem Unternehmen festgelegten Regeln für Inhalte einhalten. Das Unternehmen möchte nicht, dass unangemessene Inhalte auf seinen Websites veröffentlicht werden. Angesichts der Fortschritte im Bereich der künstlichen Intelligenz können Sie die Maschinelles Sehen-API in Ihrer App verwenden. 

Erstellen Sie zu Beginn ein Maschinelles Sehen-Konto in Ihrem Azure-Abonnement, und testen Sie das **Analysefeature**.

## <a name="calling-the-computer-vision-api-to-analyze-images"></a>Aufrufen der Maschinelles Sehen-API zum Analysieren von Bildern

Über den `analyze`-Vorgang werden mehrere visuelle Merkmale basierend auf dem Bildinhalt extrahiert. Diese Anforderungs-URL weist das folgende Format auf:

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=<...>&details=<...>&language=<...>`

Die Parameter `visualFeatures`, `details` und `languages` werden an den Dienst gesendet. Legen Sie den Parameter `details` auf `Landmarks` oder `Celebrities` fest, um Sehenswürdigkeiten oder Prominente zu erkennen. Der Parameter `visualFeatures` ermittelt, welche Art von Informationen der Dienst an Sie zurückgeben soll. Die `Categories`-Option kategorisiert den Inhalt der Bilder, z.B. Bäume, Gebäude usw. `Faces` identifiziert die Gesichter von Personen und gibt ihr Geschlecht und Alter an.

Für sämtliche Vorgänge im Zusammenhang mit der Maschinelles Sehen-API gelten die folgenden Einschränkungen im Hinblick auf die Bilder, die verarbeitet werden sollen:

- Unterstützte Bildformate: JPEG, PNG, GIF, BMP 
- Die Bilddateigröße muss weniger als 4 MB betragen.
- Die Bildgröße muss mindestens 50 × 50 Pixel betragen.

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="identify-landmarks-in-an-image"></a>Ermitteln von Sehenswürdigkeiten in einem Bild

Beginnen Sie mit einem Aufruf, über den Sie Sehenswürdigkeiten in einem Bild finden können. In diesem Beispiel wird das folgende Bild verwendet. Sie können aber denselben Befehl auch für URLs zu anderen Bildern verwenden. 

![Bild von einer schneebedeckten Bergkette unter einem blauen Himmel](../media/3-mountains.jpg)

Führen Sie in Azure Cloud Shell folgenden Befehl aus. Ersetzen Sie im Befehl `<region>` durch die Region Ihres Cognitive Services-Kontos.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/mountains.jpg'}" \
| jq '.'
```

- Dieser Aufruf sucht nach Sehenswürdigkeiten in dem von der Bild-URL angegebenen Bild. Das Bild, das analysiert wird, wird für diese Übung in einem GitHub-Repository gespeichert. 
- Außerdem wird über diesen Aufruf der Dienst gebeten, die Kategorieinformationen und eine Bildbeschreibung zurückzugeben. Als Beschreibung wird ein vollständiger Satz in englischer Sprache zurückgegeben. 
- Wie Sie wissen, wird für jeden Aufruf der API ein Zugriffsschlüssel benötigt. Dies wird im `Ocp-Apim-Subscription-Key`-Header der Anforderung festgelegt. 

> [!TIP]
> Das Ergebnis der Anforderung sind JSON-Rohdaten, die das Bild in der `url` beschreiben. In diesem Beispiel wurde ` | jq '.'` dem Ende des Befehls hinzugefügt, um die JSON-Ausgabe zu optimieren.

Die JSON-Antwort auf diesen Aufruf gibt folgende Elemente zurück:

- Ein `categories`-Array, in dem alle Bildkategorien, die ermittelt werden, sowie ein Wert zwischen 0 und 1 aufgelistet werden, der dafür steht, wie sicher der Dienst ist, dass das Bild der festgelegten Kategorie angehört.
- Ein `description`-Eintrag, der ein Array mit Tags oder Wörtern enthält, die im Zusammenhang mit dem Bild stehen.
- Ein `captions`-Eintrag mit einem Textfeld, der in englischer Sprache beschreibt, was auf dem Bild zu sehen ist. Beachten Sie, dass auch der Text einen Zuverlässigkeitswert aufweist. Sie können auf Grundlage dieses Werts entscheiden, wozu Sie diese Analyse als Nächstes verwenden möchten.


## <a name="check-for-inappropriate-content-in-an-image"></a>Suchen nach unangemessenen Bildinhalten

In diesem Beispiel wird ein nicht jugendfreies Bild analysiert. Der Zuverlässigkeitswert steht dafür, wie hoch die Wahrscheinlichkeit ist, dass der Bildinhalt nicht jugendfrei oder anzüglich ist. 

In diesem Beispiel wird das folgende Bild verwendet. Sie können aber denselben Befehl auch für URLs zu anderen Bildern verwenden. 

![Bild einer lächelnden Familie.](../media/3-people.png)

1. Führen Sie in Azure Cloud Shell folgenden Befehl aus. Ersetzen Sie dabei `<region>` in der URL.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Adult,Description" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/people.png'}" \
| jq '.'
```

In diesem Beispiel wurde `visualFeatures` auf `Adult,Description` festgelegt. 

Die Antwort umfasst zwei Zuverlässigkeitswerte, einen für nicht jugendfreie und einen für anzügliche Bildinhalte. Wenn Sie diese Werte, die Bildbeschreibungen und andere visuelle Features verwenden, können Sie Bilder kennzeichnen, die auf Ihrem Server gepostet werden.

Die in dieser Übung erwähnten Beispiele sollen Ihnen aufzeigen, welche Art von Analyse Sie mit dem `analyze`-Vorgang ausführen können. Testen Sie die Analyse mit verschiedene Bildern und verschiedenen Kombinationen aus visualFeatures-, details-, and languages-Parametern.

Weitere Informationen zum `analyze`-Vorgang finden Sie in der Referenzdokumentation zum [Analysieren von Bildern](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa).