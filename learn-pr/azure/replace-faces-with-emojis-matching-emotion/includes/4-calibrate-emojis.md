Wir können an die Gesichtserkennungs-API kein Bild des Emojis übergeben, um dessen Emotion zu ermitteln, da es sich dabei nicht um ein menschliches Gesicht handelt. Für jedes Emoji war also ein menschlicher Ersatz (ich) erforderlich.

Ich habe daher Bilder von mir aufgenommen, auf denen ich jedes Emoji _exakt_ nachstelle, und habe den _emotionalen Punkt_ für dieses Bild als Ersatz für das Emoji verwendet. Darüber hinaus habe ich Mitglieder meines Teams ausgewählt und sie ebenfalls Emojis zugeordnet:

![Emoji-Team](/media-drafts/team.jpg)

Für das Emoji mit den Herzaugen (😍) habe ich ein Bild von meiner Frau verwendet (❤️). Zur Darstellung von 🤔 habe ich im Gedenken an [Stephen Hawking](https://en.wikipedia.org/wiki/Stephen_Hawking) ein Bild von ihm gewählt.

Die Liste mit den Ersatzbildern für die einzelnen Emojis finden Sie im Beispielcode zu diesem Tutorial im Ordner `bin/proxy-images`.

In diesem Kapitel generieren Sie einen Schlüssel, um die Gesichtserkennungs-API verwenden zu können, und verwenden anschließend die Gesichtserkennungs-API, um alle Emojis mit Ersatzbildern von mir zu kalibrieren.

## <a name="generate-an-azure-face-api-key"></a>Generieren eines Schlüssels für die Gesichtserkennungs-API von Azure

<!-- To make calls to the Azure Face API we will need a special authorization key.

We are going to create one using the `az` CLI. -->

Um die Gesichtserkennungs-API von Azure verwenden zu können, benötigen wir einen speziellen Authentifizierungsschlüssel. Navigieren Sie daher zu https://azure.microsoft.com/try/cognitive-services/, und registrieren Sie sich für eine Testversion der Gesichtserkennungs-API.

![Emoji-Team](/media-drafts/4.calibrating-emojis.get-face-api.png)

> TODO: Ermitteln von az-Befehlen zum Erstellen der Gesichtserkennungs-API und Abrufen von Schlüsseln

<!-- > NOTE the Azure Face API doesn't return the emotion information by default, we need to switch on this behavior by setting some query parameters, like so:
> https://westeurope.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion -->

## <a name="setup-the-environment-variables"></a>Einrichten der Umgebungsvariablen

Für das Kalibrierungsskript müssen die URL und der Schlüssel der Gesichtserkennungs-API angegeben werden, um die korrekten Aufrufe ausführen zu können. Anstelle einer Hartcodierung im Skript verwenden wir Umgebungsvariablen. Führen Sie die folgenden Befehle in dem Terminal aus, in dem Sie voraussichtlich die Anwendung ausführen:

```bash
FACE_API_URL=<the-face-api-url>
FACE_API_KEY=<your-face-api-key>
```

<!-- > NOTE
> Don't forget to add the query param returnFaceAttributes=emotion to ensure the Face API returns emotion as well -->

## <a name="create-some-proxy-images-for-emojis"></a>Erstellen einiger Ersatzbilder für Emojis

Ich habe alle Ersatzbilder bereitgestellt – Sie können aber gerne eigene erstellen.

Nehmen Sie für jedes Emoji im Ordner `bin/proxy-images` ein Foto von sich selbst auf, auf dem Sie das Emoji nachstellen, und ersetzen Sie das Bild durch Ihr eigenes.

## <a name="try-it-out"></a>Ausprobieren

Nun kommt der spaßige Teil! Wir schicken jedes der Bilder aus `bin/proxy-images` durch die Gesichtserkennungs-API, um einen emotionalen Punkt für das Emoji im _emotionalen Raum_ zu berechnen:

```bash
node bin/calibrate.js
```

Die Ausgabe dieses Befehls sollte in etwa wie folgt aussehen:

```json
...
Processing 🤓
Processing 🤔
Processing 🦄
Processing 😃
Processing 😆
...
{
    emotiveValues: new EmotivePoint({
        anger: 0,
        contempt: 0.005,
        disgust: 0.001,
        fear: 0,
        happiness: 0,
        neutral: 0.922,
        sadness: 0.071,
        surprise: 0
    }),
    emojiIcon: "😴"
}
```

Als Erstes werden die verarbeiteten Emojis ausgegeben. Danach folgt ein Array, das `EmotivePoint` für alle Emojis definiert. Das Format entspricht dabei dem Format des Arrays in `shared/mojis.ts`.

Falls Sie Ersatzbilder geändert haben, kopieren Sie die Ausgabe dieses Skripts in den entsprechenden Abschnitt von `mojis.ts`.
