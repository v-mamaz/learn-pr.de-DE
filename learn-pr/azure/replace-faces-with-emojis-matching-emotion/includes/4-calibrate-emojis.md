Wir können kein Abbild von das gewünschte Emoji übergeben, der Gesichtserkennungs-API abgerufen werden, da sie die Emotionen, gut, da es keine menschliche ist. Damit für jede Emoji, ich einen Proxy für den Menschen erforderlich mir.

Habe ich mich Bilder _genau_ jedes Emoji imitiert, und verwendet die _emotionaler Punkt_ für das Bild als Proxy für das gewünschte Emoji. Damit bleibt die Dinge interessante ich auch ausgewählt haben Benutzer in Mein Team und Emojis auch zugeordnet, wie folgt:

![Team Moji](/media-drafts/team.jpg)

Sehen Sie die Liste der Proxy-Images für jede Emoji in die `bin/proxy-images` Ordner, in dem Beispielcode in diesem Tutorial.

## <a name="goal"></a>Zielsetzung

In diesem Kapitel generieren Sie die Schlüssel für die erforderliche Authentifizierung, damit Sie der Gesichtserkennungs-API von Azure mithilfe und klicken Sie dann die Gesichtserkennungs-API alle für die Verwendung über einen Proxy Images von mir Emojis kalibrieren verwenden können.

## <a name="learning-objectives"></a>Lernziele

- Gewusst wie: Generieren von API-Schlüsseln für die Verwendung mit Cognitive Services.
- So führen Sie die Images mithilfe der Gesichtserkennungs-API und Emotionen-Informationen zu extrahieren.

## <a name="generate-an-azure-face-api-key"></a>Generieren Sie einen Azure Gesichtserkennungs-API-Schlüssel

Um die Gesichtserkennungs-API von Azure verwenden zu können, benötigen wir einen Authentifizierungsschlüssel.

Die schnellste Möglichkeit zum Abrufen eines Schlüssels besteht darin, Head über https://azure.microsoft.com/try/cognitive-services/?api=face-api und melden Sie sich an die Testversion der Gesichtserkennungs-API.

Sobald Sie Registrierung wenige Informationen erhalten Sie, die Sie für später speichern müssen.

1. Ziehen Sie die _Endpunkt_. Es sollte etwa so aussehen https://westcentralus.api.cognitive.microsoft.com/face/v1.0

2. Hier erfahren Sie, zwei API-Schlüssel, Speichern eines davon für die spätere Verwendung (es keine Rolle spielt, welches)

## <a name="setup-the-environment-variables"></a>Die Umgebungsvariablen

Das Skript Kalibrierung muss Ihre Gesichtserkennungs-API-URL und den Schlüssel für die richtige Aufrufe bekannt sind, und nicht als fest zu Programmieren in das Skript mit der hier verwendeten Umgebungsvariablen verwenden, führen die folgenden Befehle im Terminal zum Ausführen der Anwendung im erwartet:

```bash
export FACE_API_URL=<the-face-api-url>
export FACE_API_KEY=<your-face-api-key>
```

Wir verwenden zudem ein Paket namens `dotenv` in unserer Node-Anwendung. Dieses Paket wir verwenden die Umgebungsvariablen lokal speichern in einer Datei namens `.env`. Die `dotenv` Paket lädt alle Variablen in dieser Datei und präsentiert diese als Umgebungsvariablen für Ihre Anwendung.

> **HINWEIS**
>
> Nicht Einchecken `.env` Dateien in die quellcodeverwaltung.

Azure-Funktionen haben eine andere Methode zur Handhabung der Umgebungsvariablen über ihre `local.settings.json` -Datei mehr dazu später.

## <a name="create-some-proxy-images-for-emojis"></a>Erstellen Sie eine Proxy-Images für emojis

Ich habe alle Proxy-Images bereitgestellt, selbst, aber gerne eigene generieren!

Für jede Emoji in die `bin/proxy-images` Ordner, ein Foto selbst imitiert, Emoji, und Ersetzen Sie das Image mit Ihrem Image.

## <a name="try-it-out"></a>Ausprobieren

Nun kommen wir zum interessanten Teil! Sind die Bilder auf führen wir die `bin/proxy-images` mithilfe der Gesichtserkennungs-API zum Berechnen dieser Emoji in eines emotionalen Zeitpunkt _emotionaler Speicherplatz_führen:

```bash
node bin/calibrate.js
```

Die Ausgabe dieses Befehls sieht etwa wie folgt:

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

Gibt er zuerst des gewünschte Emoji des dabei handelt es sich verarbeitet dann schließlich ausgeben an die Konsole ein Array, das definiert die `EmotivePoint` der das gewünschte Emoji. Dies ist das gleiche Format wie das Array in `shared/mojis.ts`.

Wenn Sie einige der über einen Proxy Bilder geändert haben, kopieren Sie die Ausgabe des Skripts zum relevanten Abschnitt des `mojis.ts`
