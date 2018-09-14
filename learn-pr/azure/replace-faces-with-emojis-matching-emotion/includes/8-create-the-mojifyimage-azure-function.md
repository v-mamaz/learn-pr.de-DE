Das Ziel dieser Vortrag ist, erstellen Sie einen Azure-Funktion-HTTP-Endpunkt, die Mojify ein übergebenen Images und zurück klicken Sie dann das Mojified-Image aus, damit es auf dem Bildschirm angezeigt.

Am Ende lernen Sie Folgendes:

- Gewusst wie: Konvertieren einer `JavaScript` Azure Functions-Projekts zu `TypeScript`.
- Gewusst wie: zurückgeben `raw` imagedaten aus einem Funktionsendpunkt.

## <a name="convert-to-typescript"></a>Konvertieren in TypeScript

Werden wir eine Codierung in `TypeScript` , aber die Funktionen-app erstellt ein `JavaScript` -Datei müssen wir, die über in konvertieren `TypeScript`.

1. Benennen Sie die `index.js` Datei `index.ts`

> **HINWEIS**
>
> Wenn Sie ausgeführt werden `npm run build` und in den dazugehörigen `tsc -w` Befehl wird das `index.ts` Datei sofort kompiliert wird, um `index.js` und sollte auch ein `index.map` erstellte Datei.
>
> Wenn die `index.js` und `index.map` Dateien werden nicht automatisch erstellt, klicken Sie dann überprüfen Sie die `npm run build` Befehl ausgeführt wird und keine Fehler in der Ausgabe angezeigt.

2. Fügen Sie diesen Code in `index.ts`

```typescript
export async function index(context, req) {
  context.log("ReplyWithMojifiedImage HTTP trigger");
  context.res.body = "Hello!";
  context.done();
}
```

3. Führen Sie die Funktions-app

Stellen Sie sicher, dass die Funktion, die app ausgeführt wird, verwenden eine der Methoden bisher entweder oben angeführt wurde die `func host start` Befehl aus, oder führen Sie die Anwendung über das Menü "Debuggen".

Besuchen Sie anschließend http://localhost:7171/api/MojifyImage in einem Browser.

Wenn alles ordnungsgemäß funktioniert, sollte dies ausdrucken `Hello!` an den Browser.

Ihre Funktionstrigger, um TypeScript statt in JavaScript werden jetzt wurden konvertiert 👏.

## <a name="environment-variables-in-azure-functions"></a>Umgebungsvariablen im Azure-Funktionen

Um sicher zu sein, nicht wir hartcodieren private Daten in unserem Code; Stattdessen haben wir Umgebungsvariablen verwendet.

Insbesondere zum Einsatz – Umgebungsvariablen zum Speichern der Gesichtserkennungs-API-URL und Schlüssel wie folgt:

```bash
export FACE_API_URL=[face-api-url]
export FACE_API_KEY=[face-api-key]
```

Wenn Sie ein Azure Functions-Projekt erstellen, erstellt er auch eine Datei namens `local.settings.json`. Diese Datei befindet sich auch in der `.gitignore` Datei so _Isnot in quellcodeverwaltung eingecheckt_.

Es ist eine direkte Konfiguration vertrauliche oder nur lokal zu speichern, die nicht veröffentlicht werden sollen.

Standardmäßig sieht dies wie folgt:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "node"
  }
}
```

Komponenten in der `Values` Objekt ist für Ihren Node.js-Code als Umgebungsvariable verfügbar gemacht.

Wenn Sie die Variablen für die gesichtserkennungs-API hinzugefügt und wie auch damit:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "node",
    "FACE_API_URL": "[face-api-url]",
    "FACE_API_KEY": "[face-api-key]"
  }
}
```

Die `FACE_API_URL` und `FACE_API_KEY` Variablen werden für Knoten verfügbar sein, wie Umgebungsvariablen wie folgt:

```typescript
const API_URL = process.env["FACE_API_URL"];
const API_KEY = process.env["FACE_API_KEY"];
```

## <a name="copy-existing-code-from-the-mojifyts-script"></a>Kopieren Sie vorhandenen Code aus der `mojify.ts` Skript

Die Arbeit, die wir im vorherigen vorlesungen erstellen haben unsere `bin\mojify.ts` Code ist nicht verschwendet, die meisten dieser Code können jetzt in diese Funktion kopiert werden.

Kopieren Sie das gesamte **außer** der `main` -Funktion über die `index.ts` Datei.

Es spielt keine Rolle, aber ich persönlich nutze jede alle Importe und abhängige Funktionen am Anfang der Datei und die `index` -Funktion am unteren Rand.

> **WICHTIGE**
>
> Überschreiben Sie nicht die `index` -Funktion, dieser Schritt muss für die Azure-Funktion funktioniert vorhanden sind.

Wir touch wird nicht die `getFaces` funktioniert; er bleibt völlig unverändert.

Allerdings die `createMojifiedImage` Funktion führt müssen eine Änderung in der ursprünglichen Version dieser Funktion wurden Speichern des Bildes auf dem Datenträger mit einer Zeile wie folgt am Ende des Codes:

```typescript
compositeImage.write(path.join(__dirname, "..", "mojified.jpg"));
```

In der neuen Version von Azure-Funktion des Codes möchten wir nicht die Datei auf den Datenträger zu speichern; Wir möchten _zurückgeben_ das Bild, das der Benutzer und stattdessen im Browserfenster anzuzeigen.

Ausführen, die so genannte benötigen wir eine `buffer`, bitten wir `Jimp` an uns zu den Puffer für das Abbild, aber wir müssen den Code in umschließen einer `Promise` da die `Jimp.getBuffer` Funktion ist asynchron.

So ersetzen Sie den oben genannten `compositeImage.write` Zeile mit diesem:

```typescript
return new Promise((resolve, reject) => {
  compositeImage.getBuffer(Jimp.MIME_JPEG, (error, buffer) => {
    // get a buffer of the composed image
    if (error) {
      let message = "There was an error adding the emoji to the image";
      context.log.error(error);
      reject(message);
    } else {
      // put the image into the context body
      resolve(buffer);
    }
  });
});
```

Dadurch wird den Puffer des Images, die unformatierten binären Daten zurückgegeben.

Sie können an diesem Punkt Beachten Sie, dass TypeScript beschweren ist, dass es nicht bekannt ist die `context` Variable.

Zum Beheben dieses Problems fügen `context` als das erste Argument für die `createMojifiedImage` -Funktion wie folgt:

```typescript
async function createMojifiedImage(context, imageUrl, faces) {
  ...
}
```

## <a name="connect-it-all-in-the-index-function"></a>Verbinden Sie es alle in der `index` Funktion

Wenn jemand dieses Endpunkts besucht sollten:

1. Abrufen der `imageUrl` sie anfordern
2. Mojify der `imageUrl` und den unformatierten Puffer zu erhalten.
3. Reagieren Sie auf die HTTP-Anforderung so, dass ein Bild im Browser angezeigt wird.

Beginnen wir also die Index-Funktion gibt.

Die `context.res` Eigenschaft beschreibt die Antwort dieser Funktion wird hier legen wir, was an den Browser zurückgegeben wird.

Wir konfigurieren `context.res` wie folgt:

```typescript
context.res = {
  status: 200,
  headers: {
    "Content-Type": "image/jpeg"
  },
  isRaw: true
};
```

Fügen Sie den oben genannten am Anfang Ihrer `index` -Funktion, dadurch wird die Antwort auf einen Statuscode von 200 zurückzugeben legt den Rückgabetyp JPEG-Format sein Inhalt und die `isRaw` Flag auf "true" an, damit wir binäre zurückgeben kann _Image_ Daten.

Als Nächstes extrahiert werden sollen die `imageUrl` aus der Abfrage Params damit wir, welches Bild wissen sollte werden Mojifying. Wir möchten auch einige gute Fehlermeldung zurückgegeben, wenn vom Benutzer nicht bereitgestellt.

```typescript
const { imageUrl } = req.query;
if (!imageUrl) {
  let message = `imageUrl is required`;
  context.log.error(message);
  return context.done(message, { status: 400, body: message });
} else {
  context.log(`Called with imageUrl: "${imageUrl}"`);
}
```

Schließlich soll die `getFaces` und `createMojifiedImage` Funktionen, die wir am Anfang der Datei hinzugefügt.

```typescript
// Get the response from the faceAPI
try {
  let faces = await getFaces(imageUrl);
  let buffer = await createMojifiedImage(context, imageUrl, faces);
  context.res.body = buffer;
  context.log(`Posted reply with mojified image`);
  context.done();
} catch (err) {
  let message =
    "There was an error processing this image: " + JSON.stringify(err);
  context.log.error(message);
  context.done(null, {
    status: 400,
    body: message
  });
}
```

Die oben genannten wichtigen zwei Zeilen sind:

```typescript
context.res.body = buffer;
context.done();
```

Hiermit wird die binäre Rohdaten als Textkörper, um unsere Response-Objekt, und klicken Sie dann rufen wir `context.done()` damit die Funktionen-app weiß, dass wir fertig sind und sie können die Aufgabe, die Antwort zurückzugeben.

Die vollständige Auflistung für die index.ts-Funktion ist wie folgt:

```typescript
export async function index(context, req) {
  context.log("ReplyWithMojifiedImage HTTP trigger");

  context.res = {
    status: 200,
    headers: {
      "Content-Type": "image/jpeg"
    },
    isRaw: true
  };

  const { imageUrl } = req.query;
  if (!imageUrl) {
    let message = `imageUrl is required`;
    context.log.error(message);
    return context.done(message, { status: 400, body: message });
  } else {
    context.log(`Called with imageUrl: "${imageUrl}"`);
  }

  // Get the response from the faceAPI
  try {
    let faces = await getFaces(imageUrl);
    let buffer = await createMojifiedImage(context, imageUrl, faces);
    context.res.body = buffer;
    context.log(`Posted reply with mojified image`);
    context.done();
  } catch (err) {
    let message =
      "There was an error processing this image: " + JSON.stringify(err);
    context.log.error(message);
    context.done(null, {
      status: 400,
      body: message
    });
  }
}
```

## <a name="try-it-out"></a>Ausprobieren

Stellen Sie sicher, die Funktionen-app aus dem Debugmenü den Ausnahmebefehl gestartet oder über das Terminal ausführen ausgeführt wird wie folgt:

```bash
func host start
```

Wenn die Funktions-app ordnungsgemäß gestartet werden soll, und klicken Sie dann das Fenster "Ausgabe" etwa wie folgt angezeigt werden sollen:

```
Http Functions:
        MojifyImage: http://localhost:7071/api/MojifyImage
```

Wenn die Funktions-app ordnungsgemäß gestartet wurde und besuchen dann die URL, die Denken Sie daran, übergeben Sie in der URL zu einem Bild über den `imageUrl` Param, Abfragen wie folgt:

http://localhost:7171/api/MojifyImage?imageUrl=[Url-an-ein-Image]

Wenn alle arbeitet, wird eine Mojified-Version des Images zurückgegeben, sollte wie folgt:

![Mojified-Bild](/media-drafts/7.mojified-image.png)
