Im letzten Kapitel wurde beschrieben, dass die Datei `shared/mojis.ts` über eine Liste mit Emojis und die zugehörigen emotionalen Punkte verfügt.

In diesem Kapitel wird der Rest des Codes beschrieben, den wir verwenden, um ein Gesicht einem Emoji zuzuordnen.

Sie lernen Folgendes:

1. Erstellen eines Skripts zum Übergeben einer URL zum Bild eines Gesichts
2. Berechnen des emotionalen Punkts von Gesichtern im Bild
3. Zuordnen der Gesichter im Bild zu den naheliegendsten Emojis

Abschließend implementieren wir dies in Bezug auf die Funktion dann als Slack-Befehl. Jetzt starten wir aber mit einem einfachen Node-Skript, das Sie in der Befehlszeile ausführen können:

```bash
node bin/mojify.js <url-of-image-with-face>
```

## <a name="debugging-typescript"></a>Debuggen von TypeScript

Wir schreiben in TypeScript, aber die Ausführung erfolgt per JavaScript. Dies erschwert das Debuggen, da wir Breakpoints setzen und in den transpilierten JavaScript-Dateien debuggen müssen, die ggf. schwierig zu lesen sind.

Idealerweise sollte das Schreiben _und_ Debuggen in TypeScript erfolgen.

Die gute Nachricht ist, dass dies mit VS Code bei nur geringem Konfigurationsaufwand möglich ist.

Öffnen Sie die Datei `launch.json`, indem Sie die Befehlspalette verwenden: `Ctrl+P > Debug: Open launch.json`.

> TODO: Bild

Fügen Sie wie folgt eine Konfigurationsoption hinzu:

```json
{
  "type": "node",
  "request": "launch",
  "name": "Mojify",
  "env": {
    "DEBUG": "*"
  },
  "args": [
    "https://pbs.twmedia-drafts.com/profile_images/833970306339446784/83MO53R9_400x400.jpg"
  ],
  "sourceMaps": true,
  "stopOnEntry": false,
  "console": "integratedTerminal",
  "cwd": "${workspaceRoot}",
  "program": "${workspaceRoot}/bin/mojify.js",
  "outFiles": ["${workspaceRoot}/bin/mojify.js"]
}
```

Im Menü für das Debuggen wird jetzt die Option `Mojify` angezeigt, mit der das mojify-Skript ausgeführt und eine URL als Argument übergeben wird. Sie können in der TypeScript-Datei Breakpoints setzen und darin direkt Variablen untersuchen.

## <a name="open-up-binmojists"></a>Öffnen Sie `bin/mojis.ts`.

Das Gerüst für die Datei mit allen erforderlichen Importen steht bereits:

```typescript
require("dotenv").config();
import fetch from "node-fetch";
import { EmotivePoint, Face, Rect } from "../shared/models";
```

`dotenv` ist ein Hilfsprogrammpaket, mit dem der Inhalt einer ENV-Datei im Stamm Ihres Projekts in Form von Umgebungsvariablen geladen wird. Dies ist hilfreich für die Entwicklung.

Wir verwenden `node-fetch`, um HTTP-Anforderungen an die Azure-Gesichtserkennungs-API zu senden.

`EmotivePoint` ist eine Hilfsklasse, mit der ein Punkt im _emotionalen Raum_ beschrieben wird. Hierauf gehen wir weiter unten näher ein.

`Rect` ist eine Hilfsklasse zum Beschreiben einer rechteckigen Form. Wir nutzen sie, um die Position eines Gesichts in einem Bild zu beschreiben.

`Face` ist eine Hilfsprogrammklasse, mit der die Informationen zum Rechteck und emotionalen Punkt eines Gesichts in einem Bild kombiniert werden.

Im mittleren Bereich der Datei sollten einige Stub-Funktionen angezeigt werden:

```typescript
async function getFaces(imageUrl) {
  //TODO
}

async function createMojifiedImage(imageUrl, faces) {
  //TODO
}
```

Hierbei handelt es sich um die Funktionen, die Sie in dieser und der nächsten Lektion gestalten.

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

## <a name="add-the-environment-variables"></a>Hinzufügen der Umgebungsvariablen

Da wir die Gesichtserkennungs-API aufrufen, müssen wir die zuvor generierten geheimen Schlüssel und URLs verwenden und oben in der Datei unter den Importen hinzufügen:

```typescript
const API_URL = process.env["FACE_API_URL"];
const API_KEY = process.env["FACE_API_KEY"];
```

## <a name="call-the-face-api-with-the-provided-image-and-get-a-response"></a>Aufrufen der Gesichtserkennungs-API mit dem angegebenen Bild und Erhalten einer Antwort

Wir fügen diesen Code oben in der Funktion `getFaces` hinzu, um eine Anforderung an die Gesichtserkennungs-API zu senden.

```typescript
let response = await fetch(API_URL, {
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

Im obigen Code wird der Befehl `fetch` verwendet, um eine `POST`-Anforderung an die Gesichtserkennungs-API zu senden.

Wir übergeben den `API_KEY` im Header, damit die Gesichtserkennungs-API über unsere Anforderung informiert ist. Andernfalls wird die Anforderung abgelehnt.

Wir übergeben die `imageUrl`, die von der Gesichtserkennungs-API im Text analysiert werden soll.

Anschließend erhalten wir die Antwort von der API-Anforderung und geben sie aus.

Bei Ausführung des Skripts mit:

```bash
node bin/mojify.js <path-to-image>
```

Die JSON-Antwort, die beim Übergeben dieses Bilds an die Gesichtserkennungs-API zurückgegeben wurde, sollte ausgegeben werden.

## <a name="parse-the-responce"></a>Analysieren der Antwort

Zum Berechnen von Emojis müssen Sie jedes Gesicht, das in der Antwort von der API zurückgegeben wird, in eine Instanz einer `Face`-Klasse konvertieren.

Wir fügen diesen Code direkt nach dem Aufrufen der API in der Funktion `getFaces` hinzu:

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

- Wir durchlaufen die einzelnen Gesichter, die in der Antwort zurückgegeben werden.
- Wir generieren aus dem zurückgegebenen JSON-Code die Elemente `EmotivePoint`, `Rect` und `Face`.
- Durch die Erstellung der `Face`-Instanz wird das Gesicht mit einem Emoji abgeglichen.
- Um zu ermitteln, für welches Emoji sich die Übereinstimmung ergeben hat, geben wir das `mojiicon`-Element aus.

## <a name="try-it-out"></a>Testen

Wenn Sie das Skript jetzt ausführen, sollte Folgendes durchgeführt werden:

- Übergeben des bereitgestellten Bilds über die Gesichtserkennungs-API und Berechnen der Emotion
- Abgleichen der Emotionen mit Emojis
- Ausgeben der Emojis im Terminal

Beispiel:

```bash
node bin/mojify.js <path-to-image>
<path-to-image>
😕
```
