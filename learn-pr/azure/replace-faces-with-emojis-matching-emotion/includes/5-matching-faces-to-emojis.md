Im letzten Kapitel, Daten, die `shared/mojis.ts` Datei enthält eine Liste von Emojis und ihre emotionalen Punkten.

In diesem Kapitel erfahren Sie, den Rest des Codes, den wir verwenden, um ein Gesicht eine Emoji zuzuordnen.

Folgendes wird vermittelt:

1. Erstellen Sie ein Skript, das dort Sie übergeben in einer URL eines Bilds mit einem Gesicht.
2. Berechnen Sie den emotionalen Punkt alle Gesichter im Bild.
3. Zuordnen der Gesichter im Bild auf die nächste emojis

Schließlich implementieren wir diese Funktionen als ein Slack-Befehl, aber jetzt befassen wir uns zunächst ein einfacher-Skript, das Sie in der Befehlszeile ausführen können wie folgt:

```bash
node bin/mojify.js <url-of-image-with-face>
```

## <a name="debugging-typescript-in-vs-code"></a>Debuggen von TypeScript in Visual Studio Code

Schreiben wir `TypeScript` aber ausgeführten `JavaScript`; Dies ermöglicht, das Debuggen kompliziert, wie wir hätten, legen Sie Haltepunkte fest und Debuggen in der transpilierten JavaScript-Dateien die schwer zu lesen sein können.

Wir möchten im Idealfall ist das Schreiben _und_ in TypeScript Debuggen.

Die gute Nachricht ist, dass es mit Visual Studio Code mit ganz wenig Konfiguration möglich ist.

Öffnen Sie die `launch.json` -Datei mit dem Befehl Palete <kbd>STRG</kbd>+<kbd>P</kbd> und Eingabe `Debug: Open launch.json`

![Öffnen starten Json](/media-drafts/5.open-debug-launch.json.png)

Daraufhin öffnet sich die `launch.json` Konfigurationsdatei. Zum Hinzufügen und Entfernen von Debugkonfigurationen bearbeiten wir diese Datei.

Hinzufügen der folgenden Option der Debug-Konfiguration in das Array der Einstellungen:

```json
{
  "type": "node",
  "request": "launch",
  "name": "Mojify",
  "env": {
    "DEBUG": "*"
  },
  "args": [
    "https://pbs.twimg.com/profile_images/833970306339446784/83MO53R9_400x400.jpg"
  ],
  "sourceMaps": true,
  "stopOnEntry": false,
  "console": "integratedTerminal",
  "cwd": "${workspaceRoot}",
  "program": "${workspaceRoot}/bin/mojify.js",
  "outFiles": ["${workspaceRoot}/bin/mojify.js"]
}
```

Nachdem Sie im Menü Debuggen Sie eine Option Namens finden Sie unter `Mojify` Dies führt, dass das Mojify-Skript, das in einer URL als Argument übergeben. Sie können Haltepunkte festlegen, in der `TypeScript` Datei, und untersuchen Sie Variablen direkt von dort aus.

## <a name="open-up-binmojists"></a>Öffnen Sie `bin/mojis.ts`

Die Datei ist bereits erstellt haben, mit der alle erforderlichen Importe, etwa so:

```typescript
require("dotenv").config();
import fetch from "node-fetch";
import { EmotivePoint, Face, Rect } from "../shared/models";
```

`dotenv` ist ein Hilfsprogramm-Paket lädt den Inhalt einer env-Datei im Stammverzeichnis des Projekts als Umgebungsvariablen, die für die Entwicklung nützlich.

`node-fetch` In diesem Fall verwenden wir eine HTTP-Anforderungen an die Gesichtserkennungs-API von Azure vornehmen.

`EmotivePoint` ist eine Hilfsklasse, die beschreibt, einen Punkt im _emotionaler Speicherplatz_ -wir dies unten ausführlicher erläutert.

`Rect` ist eine Hilfsklasse, um eine rechteckige Form, zu beschreiben. wir verwenden dies zum Beschreiben der Position von einem Gesicht in einem Bild.

`Face` ist eine Hilfsklasse für das Hilfsprogramm das Rechteck und emotive zeigen Informationen über ein Gesicht in einem Bild kombiniert.

In der Mitte der Datei sollte einige Stubfunktionen, wie folgt:

```typescript
async function getFaces(imageUrl) {
  //TODO
}

async function createMojifiedImage(imageUrl, faces) {
  //TODO
}
```

Dies sind die Funktionen, die Sie sich in diesem Vortrag und die nächste ausarbeitete werden werden.

Am Ende der Datei sollte dieser Code angezeigt werden:

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

## <a name="add-the-environment-variables"></a>Fügen Sie der Umgebungsvariablen hinzu.

Es wird zunächst der Gesichtserkennungs-API aufrufen, daher müssen wir zur Verwendung dieser geheimen Schlüssel und die URLs, die vor dem generierten am Anfang der Datei unter die Importe Folgendes hinzu:

```typescript
const API_URL = process.env["FACE_API_URL"];
const API_KEY = process.env["FACE_API_KEY"];
```

## <a name="call-the-face-api-with-the-provided-image-and-get-a-response"></a>Rufen Sie die Gesichtserkennungs-API mit dem angegebenen Bild und erhalten eine Antwort

Um eine Anforderung für die Gesichtserkennungs-API zu machen, wir fügen Sie folgenden Code am Anfang der `getFaces` Funktion

```typescript
const fullUrl =
  API_URL +
  "/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion";

let response = await fetch(fullUrl, {
  headers: {
    "Ocp-Apim-Subscription-Key": API_KEY,
    "Content-Type": "application/json"
  },
  method: "POST",
  body: JSON.stringify({ url: imageUrl })
});
let resp = await response.json();
console.log(resp);
```

Der Code oben verwendet die `fetch` zu sendenden Befehl eine `POST` Anforderung der Gesichtserkennungs-API.

> **HINWEIS**
>
> Wir müssen Anfügen `/detect` und einige Abfrage-Parameter, um die API_URL um abzurufen, erkennen Sie Gesichter und Emotionen auch zurückgeben.

Wir übergeben den `API_KEY` in der Kopfzeile, sodass der Gesichtserkennungs-API kann die Anforderung stammt von uns; andernfalls wird die Anforderung zurückgewiesen.

Wir übergeben den `imageUrl` der Gesichtserkennungs-API, die im Text analysieren soll.

Wir klicken Sie dann die Antwort von der API-Anforderung erhalten und drucken Sie ihn aus.

Wenn Sie nun das Skript mit ausführen.

```bash
node bin/mojify.js <path-to-image>
```

Es sollte die JSON-Antwort zurückgegeben wird, an der gesichtserkennungs-API übergeben wird dieses Image auszugeben.

## <a name="parse-the-response"></a>Analyse der Antwort

Zum Berechnen der Emojis Ee müssen jedes Gesicht in der Antwort der API mit einer Instanz von zurückgegeben konvertieren eine `Face` Klasse.

Wir fügen Sie folgenden Code unmittelbar nach dem Code zum Aufrufen der API in der `getFaces` Funktion:

```typescript
let faces = [];
for (let f of resp) {
  let scores = new EmotivePoint(f.faceAttributes.emotion);
  let faceRectangle = new Rect(f.faceRectangle);
  let face = new Face(scores, faceRectangle);
  console.log(face.mojiIcon);
  faces.push(face);
}
return faces;
```

- Wir durchlaufen Jedes Gesicht in der Antwort zurückgegeben.
- Generiert eine `EmotivePoint`, `Rect` und `Face` aus den zurückgegebenen JSON-Code.
- Erstellen der `Face` -Instanz übereinstimmt, das Gesicht, ein Emoji
- Wir sehen, welche Emoji übereinstimmte ausgeben der `mojiicon`.

## <a name="try-it-out"></a>Ausprobieren

Nun, wenn Sie das Skript ausführen, wie, das Sie sollte:

1. Übergeben Sie das bereitgestellte Image mithilfe der Gesichtserkennungs-API, und berechnen Sie die Emotionen.
2. Übereinstimmung mit Emotionen, Emojis.
3. Drucken Sie die Emojis auf das Terminal ein.

Wie folgt:

```bash
node bin/mojify.js <path-to-image>
<path-to-image>
😕
```
