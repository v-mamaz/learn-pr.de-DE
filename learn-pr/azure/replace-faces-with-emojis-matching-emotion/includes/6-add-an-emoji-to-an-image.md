An diesem Punkt im Anwendungsfluss ist uns Folgendes bekannt:

1.  Die Liste der Gesichter im Bild (sofern vorhanden)
2.  Das gewünschte Emoji für jedes Gesicht
3.  Der Begrenzungsrahmen für jedes Gesicht im Bild

Für jedes im Bild erkannte Gesicht müssen wir also ein Emoji über das Gesicht legen und die Größe des Emojis entsprechend der Größe des Gesichts ändern.

Zum Implementieren dieser Funktion verwenden wir die Open Source-Bildbearbeitungsbibliothek [Jimp](https://www.npmjs.com/package/jimp).

In dieser Lektion erfahren Sie, wie Sie mit der `Jimp`-Bibliothek Bilder bearbeiten und insbesondere ein Emoji über ein Gesicht legen und das Bild wieder auf dem Datenträger speichern.

Hierzu erweitern wir das `bin/mojify.ts`-Skript, mit dem wir in der vorherigen Lektion begonnen haben, indem wir die `createMojifiedImage`-Funktion erstellen.

> HINWEIS: Wir werden den gesamten Code aus diesem Skript wiederverwenden, wenn wir in späteren Lektionen den Slack-Befehl und die Azure-Funktion erstellen. Diese Schritte sind also keine vergeudete Mühe.

## <a name="steps"></a>Schritte

### <a name="required-imports"></a>Erforderliche Importe

Um mit Jimp experimentieren und Dateien in unserem Dateisystem bearbeiten zu können, müssen wir zunächst einige Pakete importieren.

```typescript
import * as Jimp from "jimp";
import * as path from "path";
```

> HINWEIS: `path` ist erforderlich, weil wir Dateien vom Datenträger laden möchten.

### <a name="basic-use-case"></a>Einfacher Anwendungsfall

Vereinfachen wir das Ganze, indem wir uns fragen, was wir zum Ausführen der folgenden Aufgaben benötigen:

1. Ein Bild hochladen
2. Das Emoji 😕 in der oberen rechten Ecke platzieren (nach der Größenänderung auf 50 x 50 Pixel)
3. Das Bild speichern

All diese Funktionen können wir wie folgt in sechs Codezeilen implementieren:

```typescript
async function createMojifiedImage(imageUrl) {
  let sourceImage = await Jimp.read(imageUrl);

  let mojiPath = path.resolve(__dirname, "../shared/emojis/😕.png");
  let emojiImage = await Jimp.read(mojiPath);

  emojiImage.resize(50, 50);

  sourceImage = sourceImage.composite(emojiImage, 0, 0);
  sourceImage.write(path.join(__dirname, "..", "mojified.jpg"));
}
```

Wir unterteilen den Code Schritt für Schritt.

Um ein Bild mit `Jimp` zu laden, verwenden wir die `Jimp.read`-Funktion wie folgt:

```typescript
let sourceImage = await Jimp.read(imageUrl);
```

Wir haben ein Verzeichnis mit PNG‑Dateien für jedes Emoji in `shared/emojis`. Jede Emoji-PNG-Datei ist als „<emoji>.png“ benannt. `😕.png` ist folglich eine Datei, die eine PNG-Datei des Emojis 😕 enthält.

Wir laden `😕.png` wie folgt hoch:

```typescript
let mojiPath = path.resolve(__dirname, "../shared/emojis/😕.png");
let emojiImage = await Jimp.read(mojiPath);
```

Als Nächstes müssen wir die Größe des „emojiImage“ in 50 Pixel (Breite) x 50 Pixel (Höhe) ändern. Diese Anpassung können wir mit der Größenänderungsfunktion wie folgt vornehmen:

```typescript
emojiImage.resize(50, 50);
```

Die Größe von `emojiImage` wurde nun so geändert, dass das Bild in einen 50 x 50 Pixel großen Bereich passt.

Jetzt müssen wir das „emojiImage“ wie folgt in der oberen linken Ecke auf dem „sourceImage“ _platzieren_:

```typescript
sourceImage = sourceImage.composite(emojiImage, 0, 0);
```

Wir verwenden die `composite`-Funktion, die `emojiImage` 0 Pixel vom oberen Rand und 0 Pixel vom unteren Rand auf `sourceImage` platziert. Die `composite`-Funktion ändert `sourceImage` nicht direkt, sondern gibt eine Kopie von `sourceImage` mit darüber platziertem `emojiImage` zurück.

Zum Schluss speichern wir das Ausgabebild wie folgt auf dem Datenträger:

```typescript
sourceImage.write(path.join(__dirname, "..", "mojified.jpg"));
```

### <a name="full-use-case"></a>Vollständiger Anwendungsfall

Jetzt wissen Sie, wie `Jimp` funktioniert und wie Sie damit Bilder zusammensetzen können. Wenn wir nun den vollständigen Code für die `createMojifiedImage`-Funktion durchgehen, werden Sie das Prinzip noch besser verstehen.

Kopieren Sie den unten stehenden Code, und fügen Sie ihn in Ihre `createMojifiedImage`-Funktion in `bin/mojify.ts` ein.

```typescript
async function createMojifiedImage(imageUrl) {
  // Create a composite image, we will "append" to this composite an emoji image for each face found
  let compositeImage = sourceImage;

  for (let face of faces) {
    const mojiIcon = face.mojiIcon;
    const faceHeight = face.faceRectangle.height;
    const faceWidth = face.faceRectangle.width;
    const faceTop = face.faceRectangle.top;
    const faceLeft = face.faceRectangle.left;

    // Load the emoji from disk
    let mojiPath = path.resolve(
      __dirname,
      "../shared/emojis/" + mojiIcon + ".png"
    );
    let emojiImage = await Jimp.read(mojiPath);

    // Resize the emoji to fit the face
    emojiImage.resize(faceWidth, faceHeight);

    // Compose the emoji on the image
    compositeImage = compositeImage.composite(emojiImage, faceLeft, faceTop);
  }
  compositeImage.write(path.join(__dirname, "..", "mojified.jpg"));
}
```

Der obige Code ist dem Code für den einfachen Anwendungsfall sehr ähnlich. Anstatt ein Emoji und seine Position hartzucodieren, entscheiden wir jedoch basierend auf einem übergebenen Array von Gesichtern, welches Emoji zusammengesetzt und wo es platziert werden soll.

Das Array von Gesichtern stammt aus der `getFaces`-Funktion, die wir in der letzten Lektion erstellt haben. Alle Elemente sind hier wie folgt in der Main-Funktion verbunden:

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

Wir rufen `getFaces` mit dem übergebenen `imageUrl` auf, um das Array von `Face`-Instanzen abzurufen.
Dieses Array übergeben wir zusammen mit dem Originalbild an die `createMojifiedImage`-Funktion, die Emojis auf den Gesichtern von Personen zusammensetzt und die resultierende Datei als `mojified.jpg` im Stammordner des Projekts speichert.

### <a name="try-it-out"></a>Ausprobieren

Probieren Sie diesen Code selbst aus:

```bash
node bin/mojify.js <url>
```

Wenn es funktioniert hat, sollte eine Version der Quelldatei mit Emojis im Stammordner des Projekts `mojified.jpg` gespeichert worden sein.

Probieren Sie es mit anderen Bildern aus.
