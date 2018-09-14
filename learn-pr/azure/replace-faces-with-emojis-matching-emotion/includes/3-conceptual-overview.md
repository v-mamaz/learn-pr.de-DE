Bevor wir zu weit in die Implementierungen beschäftigen, lassen Sie uns zunächst einige Fragen zu beantworten höheren Ebene.

## <a name="how-to-calculate-the-emotion-of-a-face"></a>Wie die Emotionen einer Fläche berechnen?

Die Berechnung Emotion ist einer der Teile der Anwendung am häufigsten zugegriffen werden kann. Wir verwenden die [FaceAPI](https://azure.microsoft.com/services/cognitive-services/face/), der Teil des Angebots von Azure Cognitive Services.

Das FaceAPI nimmt als Eingabe eine Bild und gibt Informationen über das Image besteht, einschließlich, wenn es Gesichter, die Positionen der Gesichter im Bild erkannt, und wenn diese angefordert berechnet und Zurückgeben der Emotionen der Flächen aus, wie folgt:

```json
{
  "anger": 0.572,
  "contempt": 0.025,
  "disgust": 0.242,
  "fear": 0.001,
  "happiness": 0.014,
  "neutral": 0.111,
  "sadness": 0.033,
  "surprise": 0.003
}
```

Führen Sie beispielsweise dieser Abbildung:

![Beispiel für Gesichtserkennung](/media-drafts/example-face.jpg)

Um dieses Image zu verarbeiten, sollten Sie eine POST-Anforderung an die API-Endpunkt wie folgt vornehmen:

https://xxxxxxxxx.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion

Wir bieten das Bild im Text wie folgt:

```json
{
  "url": "<path-to-image>"
}
```

> **Hinweis**
>
> Die API wird standardmäßig der Emotionen zurückgegeben wird, müssen Sie explizit die Query-Parameter angeben `returnFaceAttributes=emotion`

Die Verwendung eines geheimen Schlüssels authentifiziert die API; Wir müssen diesen Schlüssel mit dem Header zu senden.

```
Ocp-Apim-Subscription-Key: <your-subscription-key>
```

Die API mit der obigen Abfrage Params würde eine JSON-Code zurück, die wie folgt:

```json
[
  {
    "faceRectangle": {
      "top": 207,
      "left": 198,
      "width": 229,
      "height": 229
    },
    "faceAttributes": {
      "emotion": {
        "anger": 0.001,
        "contempt": 0.014,
        "disgust": 0,
        "fear": 0,
        "happiness": 0.306,
        "neutral": 0.675,
        "sadness": 0.003,
        "surprise": 0.001
      }
    }
  }
]
```

Es gibt ein Array von Ergebnissen, eine pro Gesicht im Bild erkannt. Für jedes Gesicht, gibt es zurück, der Größe bzw. an einem Standort das Gesicht als `faceRectangle` und die Emotionen, ausgedrückt als Zahl von 0 auf 1 als `faceAttributes`.

> **Tipp**
>
> Sie können beginnen, ein wenig Herumspielen mit Cognitive Services auch _ohne_ müssen ein Azure-Konto an, wechseln Sie zu [auf dieser Seite](https://azure.microsoft.com/try/cognitive-services/?api=face-api&WT.mc_id=mojifier-sandbox-ashussai) , und geben Sie Ihre e-Mail-Adresse um Testversion zu erhalten.

## <a name="how-to-map-an-emotion-to-an-emoji"></a>Wie Sie eine Emotion ein Emoji zuordnen?

Angenommen Sie, gab es nur zwei Emotionen "," Angst "und" Fröhlich, mit Werten zwischen 0 und 1. Und dann jedes Gesicht in einer 2D-Texturmap. darstellbare _emotionaler Speicherplatz_ basierend auf der Emotionen des Benutzers wie folgt:

![Euklidische Distanz 1](/media-drafts/graph-1.jpg)

Angenommen Sie, klicken Sie dann, dass wir auch der emotionaler Punkt für die einzelnen Emoji herausgefunden, und auf das emotionale 2D-Bereich ebenfalls dargestellt. Wenn wir berechnen den Abstand zwischen dem Zifferblatt Ihrer und die andere Emojis in einem dieser emotionaler 2D-Bereich wir, bis die nächste Emoji, das Ihre Emotionen herausfinden können, dann wie folgt:

![Euklidische Distanz 2](/media-drafts/graph-2.png)

Diese Berechnung wird aufgerufen, die `euclidian distance`, und dies wird von uns verwendet, aber nicht in 2D emotionaler Speicherplatz in einem emotionaler 8d-Raum mit (Wut, verachtung, ekel, Angst, fröhlich, Neutral, traurig, überrascht).

> **Tipp**
>
> Um sicherzustellen, wie einfacher das Npm-Paket namens euklidischen Abstand verwendet <https://www.npmjs.com/package/euclidean-distance>.

## <a name="shared-code"></a>Freigegebener Code

Das Beispiel-Starter-Projekt enthält einen freigegebenen Ordner mit Code, der bereits einen Großteil der oben genannten Fällen behandelt.

### <a name="emotivepoint"></a>EmotivePoint

Bei genauer Betrachtung der `EmotivePoint` -Klasse im `shared/emmotive-point.ts` sehen Sie einige Dinge.

Der Konstruktor akzeptiert als Eingabe ein Objekt mit emotive Informationen aus und speichert Sie als Mitglied der lokalen Variablen wie folgt:

```typescript
 constructor({
    anger,
    contempt,
    disgust,
    fear,
    happiness,
    neutral,
    sadness,
    surprise
  }) {
    this.anger = anger;
    this.contempt = contempt;
    this.disgust = disgust;
    this.fear = fear;
    this.happiness = happiness;
    this.neutral = neutral;
    this.sadness = sadness;
    this.surprise = surprise;
  }
```

Es verfügt auch über eine Funktion namens Abstand berechnet den euklidischen Abstand zwischen zwei Punkten emotive verwenden wie folgt:

```typescript
  distance(other) {
    let myPoint = this.toArray();
    let otherPoint = other.toArray();
    return distance(myPoint, otherPoint);
  }
```

Wir daher erstellen Sie zwei emotive Punkten und berechnen, wie nah können wie folgt:

```typescript
let a = new EmotivePoint({
  /* ... */
});
let b = new EmotivePoint({
  /* ... */
});
let distance = a.distance(b);
```

### <a name="face"></a>Gesicht

Einer weiteren Hilfsklasse ist die `Face` Klasse; dabei werden einige andere Eigenschaften, einschließlich kombiniert die `EmotivePoint` einer Fläche und auch das Rechteck definieren das Gesicht im Bild; wir verwenden die `Rect` Klasse.

Bei genauer Betrachtung der `Face` Klassenkonstruktor im `shared/face.ts` sehen Sie diese Codezeile:

```typescript
this.moji = this.chooseMoji(this.emotivePoint);
```

`emotivePoint` ist der emotive Punkt der Oberfläche selbst.
`chooseMoji` Gibt eine entsprechende Emoji basierend auf den EmotivePoint, der das Gesicht zurück.

```typescript
  chooseMoji(point) {
    let closestMoji = null;
    let closestDistance = Number.MAX_VALUE;
    for (let moji of MOJIS) {
      let emoPoint = moji.emotiveValues;
      let distance = emoPoint.distance(point);
      if (distance < closestDistance) {
        closestMoji = moji;
        closestDistance = distance;
      }
    }
    return closestMoji;
  }
```

`MOJIS` die Liste der emotive Punkte für alle ist die Emojis, werden gleich erörtert wie diese in der nächsten Vorlesung generiert.

Die `chooseMoji` -Funktion berechnet den Abstand zwischen diesem Gesichts- und die Emojis dasjenige zurückgeben.

# <a name="summary"></a>Zusammenfassung

Für jede Emoji berechnen wir die zeitpunktwiederherstellung _emotionaler_ Leerzeichen, dies wird als bezeichnet _Kalibrierung_ dies im nächsten Kapitel behandelt.

Verwenden der Azure-Gesichtserkennungs-API, wir rufen Sie eine Liste der Gesichter in Bildern mit dem emotionaler Punkt jeder einzelnen Fläche. Klicken Sie dann mithilfe der euklidischen Distanz-Algorithmus finden Sie die nächsten Emoji, das jedes Gesicht ein.
