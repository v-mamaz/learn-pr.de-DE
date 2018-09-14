An diesem Punkt im Fluss der Anwendung wissen wir:

1.  Die Liste der Gesichter im Bild (sofern vorhanden).
2.  Das gewünschte Emoji, die für jedes Gesicht verwendet werden soll.
3.  Das umschließende Rechteck des jedes Gesicht im Bild.

Für jedes Gesicht im Bild erkannt wird müssen wir eine Emoji über das Gesicht layer Ändern der Größe der Emoji das Gesicht angepasst.

Um diese Funktionalität zu implementieren, verwenden wir die open-Source-Bildbibliothek Manipulation [Jimp](https://www.npmjs.com/package/jimp).

Das Ziel dieser Vortrag ist, erfahren, wie Sie mit der `Jimp` -Bibliothek zum Bearbeiten von Bildern und speziell für erfahren, wie ein Emoji eine Ebene über den ein Gesicht, und speichern Sie das Image auf den Datenträger zurück.

Werden wir zur Erweiterung der `bin/mojify.ts` Skripts, die wir zunächst in der vorherigen Vorlesung Ausarbeiten der `createMojifiedImage` Funktion.

> **Hinweis**
>
> Wir verwenden alle den Code mit folgendem Skript erneut, beim Erstellen der Slack-Befehl und die Azure-Funktion in späteren vorlesungen. Es ist nicht verschwendet, Aufwand!

## <a name="add-the-required-imports"></a>Fügen Sie die erforderlichen Importe

Zum Experimentieren Sie mit Jimp und Bearbeiten von Dateien auf unsere Filesystem, müssen wir einige Pakete am Anfang der Datei zu importieren wie folgt:

```typescript
import * as Jimp from "jimp";
import * as path from "path";
```

> **Hinweis**
>
> `path` ist erforderlich, da die Dateien vom Datenträger geladen werden soll

## <a name="simplified-use-case"></a>Vereinfachte Anwendungsfall

Wir entfernen, entfernt einen Großteil der Komplexität und Fragen, was es dauern würde, einfach:

1. Laden eines Bilds
2. Ort der 😕 Emoji in der oberen rechten Ecke (nach der Größenänderung auf 50x50px)
3. Speichern Sie das Bild

Wir können alle Funktionen über 6 Codezeilen implementieren wie folgt:

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

Wir werden sie Schritt für Schritt unterteilen.

Beim Laden ein Bild mit `Jimp` verwenden wir die `Jimp.read` -Funktion wie folgt:

```typescript
let sourceImage = await Jimp.read(imageUrl);
```

Wir haben es sich um ein Verzeichnis mit PNG‑Dateien für jede Emoji in `shared/emojis`. Jede Png Emoji heißt als <emoji>PNG, sodass `😕.png` ist eine Datei mit PNG-Datei mit den 😕 Emoji.

Wir laden `😕.png` wie folgt:

```typescript
let mojiPath = path.resolve(__dirname, "../shared/emojis/😕.png");
let emojiImage = await Jimp.read(mojiPath);
```

Als Nächstes bis wir müssen zum Ändern der Größe der `emojiImage` 50 Pixel Breite X 50 Pixel Höhe, wir können dies mithilfe der Funktion für die bildgrößenänderung wie folgt:

```typescript
emojiImage.resize(50, 50);
```

Die `emojiImage` jetzt wurde die Größe geändert wurde in einem 50 x 50 Pixel anpassen.

Jetzt müssen wir _platzieren_ der `emojiImage` über die `sourceImage` in der oberen linken Ecke, wie folgt:

```typescript
sourceImage = sourceImage.composite(emojiImage, 0, 0);
```

Wir verwenden die `composite` -Funktion, die platziert `emojiImage` auf der Basis von `sourceImage`, die beiden letzten Argumente definieren, wo die `emojiImage` ist platziert, wir sind ablegen, damit er 0 Pixel vom oberen und 0 Pixel nach unten.

Der `composite` Funktion nicht alter `sourceImage` vorhanden; stattdessen wird eine Kopie des `sourceImage` mit der `emojiImage` platziert nach oben, dies ist, warum wir das Ergebnis an SourceImage zuweisen `sourceImage = ...`

Zum Schluss wir speichern das Ausgabe-Image auf den Datenträger wie folgt:

```typescript
sourceImage.write(path.join(__dirname, "..", "mojified.jpg"));
```

## <a name="try-it-out"></a>Ausprobieren

Testen Sie diesen Code selbst, wie folgt:

```bash
node bin/mojify.js [url-to-image]
```

Wenn es funktioniert hat, und klicken Sie dann eine Datei in das Stammverzeichnis des Projekts gespeichert wird aufgerufen `mojified.jpg` etwa wie folgt suchen:

![Einfaches Image](/media-drafts/6.simple-mojified-image.jpg)

## <a name="full-use-case"></a>Vollständige Anwendungsfall

Hoffentlich haben Sie jetzt ein gutes Verständnis der Funktionsweise `Jimp` funktioniert und wie wir sie um zusammengesetzte Bilder verwenden können. Wenn wir kehren Sie nun über den vollständigen Code für die `createMojifiedImage` -Funktion hergestellt werden soll noch viel mehr Sinn.

Kopieren und fügen Sie den folgenden Code in Ihre `createMojifiedImage` -Funktion in `bin/mojify.ts`.

```typescript
async function createMojifiedImage(imageUrl) {
  let sourceImage = await Jimp.read(imageUrl);
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

Der obige Code ist sehr ähnlich der vereinfachten Fall, die, den wir gerade durchlaufen, anstatt hartcodierung einer Emoji "und" Position ", jedoch wir der Entscheidung, welche Emoji für kombinierte und, wo sie basierend auf dem Array von Gesichtern übergeben.

Das Array von Gesichtern stammt aus dem `getFaces` Funktion, die wir, in der letzten Vorlesung fleshed; es alle miteinander verbunden sich in der main-Funktion wie folgt:

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

Wir bezeichnen `getFaces` mit den übergebenen in `imageUrl` zum Abrufen des Arrays von `Face` Instanzen.
Wir übergeben dieses Array in die `createMojifiedImage` Funktion zusammen mit der das Originalbild, diese Funktion kombinierenden Zeichen ersetzt wurden Emojis auf Peoples Gesichter und speichert die resultierende Datei auf den Stammordner des Projekts als `mojified.jpg`

## <a name="try-it-out"></a>Ausprobieren

Testen Sie diesen Code selbst, wie folgt:

```bash
node bin/mojify.js <url>
```

Wenn es funktioniert hat, und klicken Sie dann eine Mojified-Version der Quelldatei in das Stammverzeichnis des Projekts gespeichert wird aufgerufen `mojified.jpg`, etwa so:

![Komplexe Bild](/media-drafts/6.complex-mojified-image.jpg)

Probieren Sie es mit anderen Bildern!
