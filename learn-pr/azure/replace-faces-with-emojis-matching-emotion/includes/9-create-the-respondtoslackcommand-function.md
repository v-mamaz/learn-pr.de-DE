Wir erstellt haben die `MojifyImage` Azure-Funktion ein Mojified Image zurückgegeben, die wir benötigen einen zweiten Endpunkt die Slack aufruft, jedes Mal, wenn ein Benutzer führt die `\mojify` Befehl.

Dieser zweite Endpunkt muss die URL zum Zurückgeben der `MojifyImage` Azure-Funktion.

Wenn Sie einen slack-Befehl wie ausführen `\mojify [some-image-url]` erleichtert eine POST-Anforderung an den Endpunkt, die Sie konfiguriert haben, und übergeben Sie `[some-image-url]` als eine `text` Abfrage Parameter im Text der Nachricht eingebettet.

Das Ziel dieser Vorlesung ist diese Funktion zu erstellen, koordiniert und reagiert auf die slack-Befehle; Wir bezeichnen diese zweite Azure-Funktion `RespondToSlackCommand`.

Am Ende dieser Vorlesung lernen Sie Folgendes:

- Gewusst wie: erstellen ein HTTP-Endpunkts auf Slack antwortet-Befehle verstehen Sie das Format, das erwartet Slack für die Anforderung und wie Sie mit einem Bild zu reagieren.

## <a name="create-the-function-trigger-and-convert-to-typescript"></a>Erstellen Sie den Trigger-Funktion, und Konvertieren in TypeScript

Wir müssen einen anderen HTTP-ausgelöste Azure-Funktion zu erstellen. Diese Anweisungen sind identisch mit der vorherigen Vorlesung; der einzige Unterschied besteht darin, dass wir diese Funktion aufrufen `RespondToSlackCommand` anstelle von `MojifyImage`.

1. Typ <kbd>STRG</kbd>+<kbd>P</kbd> , öffnen Sie die befehlspalette, und klicken Sie dann zu suchen und auswählen `Azure Functions: Create Function...`

   ![Erstellen Sie neue Funktion](/media-drafts/7.create-function.png)

2. Wählen Sie den Ordner, in dem Sie zuvor erstellt haben die Functions-Projekt (die erste Option ist für den aktuellen Ordner)

   ![Ordner auswählen](/media-drafts/7.select-current-project.png)

3. Wir erstellen eine _HTTP-Trigger_, also wählen Sie diese Option.

   ![Ordner auswählen](/media-drafts/7.select-trigger.png)

4. Geben Sie in `RespondToSlackCommand` als Namen für die Funktion, die Sie erstellen möchten

   ![Wählen Sie Namen](/media-drafts/7.choose-function-name.png)

5. Wählen Sie die anonyme Authentifizierung als die Authentifizierungsebene

   ![Wählen Sie Namen](/media-drafts/7.choose-auth-level.png)

Wenn sie dann einen Ordner namens erfolgreich `RespondToSlackCommand` sollte in das Stammverzeichnis vorhanden sein.

Identisch mit dem letzten Vortrag lassen Sie uns jetzt konvertieren diese `JavaScript` zu `TypeScript`.

6. Erstellen Sie eine Datei namens `index.ts` in die `RespondToSlackCommand` Ordner.

   Sicherstellen, dass die `TypeScript` Build-Prozess weiterhin ausgeführt wird, und, die automatisch kompiliert ihn in `index.js` und `index.map` Dateien.

7. Fügen Sie diesen Code in `index.ts`

```typescript
export async function index(context, req) {
  context.log("RespondToSlackCommand HTTP trigger");
  context.res.body = "Hello!";
  context.done();
}
```

## <a name="try-it-out"></a>Ausprobieren

Stellen Sie sicher, dass alles finden Sie unter funktioniert http://localhost:7171/api/RespondToSlackCommand in einem Browser drucken sollte unser `Hello!`.

## <a name="flesh-out-the-index-function"></a>Ausarbeitung der `index` Funktion

Dies `index` -Funktion ist viel schneller als die vorherige Funktion schreiben.

Lassen Sie uns zunächst einrichten unsere `context.res` Objekt

```typescript
context.res = {
  headers: {
    "Content-Type": "application/json"
  },
  body: null
};
```

Einfacher, als zuvor, legen wir nicht die `isRaw` Eigenschaft, da hier der Standardwert `false`, aber wir legen Sie den Inhalt Typ sein `application/json`.

Wie zuvor in Slack sendet die Bild-URL, die wir mit dem Schlüssel des als Abfragezeichenfolge verarbeiten möchten `text`, aber Sicherheitsgründen sie dies im Hauptteil der Anforderung, bettet, daher müssen wir ein bisschen härter arbeiten, um die Informationen zu erhalten, wir müssen, , nicht zu schwierig Obwohl!

Um unser Leben leichter importieren wir auf den Knoten `querystring` Paket, dies wird als Bestandteil des NodeJS brauchen Sie also nicht etwas zusätzliche installieren.

```typescript
import * as querystring from "querystring";
```

Klicken Sie dann in unsere `index` Funktion wir konvertieren die `req.body` in ein Objekt, von dem wir extrahieren, den `text` -Eigenschaft, wie folgt:

```typescript
const { text } = querystring.parse(req.body);
```

Wenn der Benutzer den Befehl ordnungsgemäß haben, und klicken Sie dann der Text sollte die URL eines Bilds enthalten können wir eine grundlegende Validierung hinzufügen wie folgt:

```typescript
let message = "Your mojified image my liege...";
if (!text) {
  message = "You must provide an image to mojify";
}
```

Denken Sie daran, die slack-Befehl ist der Aufruf https://somedomain.com/api/RespondToSlackCommand, und wir müssen mit der URL MojifyImage reagieren, die vermutlich wahrscheinlich auf der gleichen Domäne sein. https://somedomain.com/api/MojifyImage

Anstatt die Domäne in der Datei, lassen Sie uns stattdessen die gleiche Domäne wie die Anforderung der Domäne des Te `MojifyImage` -Url wie folgt:

```typescript
const mojifyUrl = req.url.substr(0, req.url.lastIndexOf("/")) + "/MojifyImage";
```

Schließlich legen wir der Text der Antwort an, der slack-Befehl erwartet, dass ein bestimmtes Format in der Antwort wie folgt:

```typescript
context.res.body = {
  response_type: "in_channel",
  text: message,
  attachments: [
    {
      image_url: `${mojifyUrl}?imageUrl=${text}`
    }
  ]
};

context.done();
```

Ist entscheidend, beachten Sie oben die `image_url` in die `attachments` Eigenschaft; wir legen Sie diese auf die Rückgabe der `mojifyUrl` und den Benutzer in den Befehl wie angegeben in der URL übergeben die `imageUrl` Param Abfragen.

## <a name="try-it-out"></a>Ausprobieren

Stellen Sie sicher, dass alles finden Sie unter funktioniert http://localhost:7171/api/RespondToSlackCommand in einem Browser sollte nun ausdrucken veranschaulicht einige `json` wie die folgenden:

```json
{
  "response_type": "in_channel",
  "text": "You must provide an image to mojify",
  "attachments": [
    {
      "image_url": "http://localhost:7071/api/MojifyImage?imageUrl=undefined"
    }
  ]
}
```
