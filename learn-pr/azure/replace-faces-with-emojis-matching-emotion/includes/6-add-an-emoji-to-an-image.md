<span data-ttu-id="652d1-101">An diesem Punkt im Anwendungsfluss ist uns Folgendes bekannt:</span><span class="sxs-lookup"><span data-stu-id="652d1-101">At this point in the flow of the application we know:</span></span>

1.  <span data-ttu-id="652d1-102">Die Liste der Gesichter im Bild (sofern vorhanden)</span><span class="sxs-lookup"><span data-stu-id="652d1-102">The list of faces in the image (if any).</span></span>
2.  <span data-ttu-id="652d1-103">Das gewünschte Emoji für jedes Gesicht</span><span class="sxs-lookup"><span data-stu-id="652d1-103">The emoji to use for each face.</span></span>
3.  <span data-ttu-id="652d1-104">Der Begrenzungsrahmen für jedes Gesicht im Bild</span><span class="sxs-lookup"><span data-stu-id="652d1-104">The bounding rectangle of each face in the image.</span></span>

<span data-ttu-id="652d1-105">Für jedes im Bild erkannte Gesicht müssen wir also ein Emoji über das Gesicht legen und die Größe des Emojis entsprechend der Größe des Gesichts ändern.</span><span class="sxs-lookup"><span data-stu-id="652d1-105">So for each face discovered in the image, we need to layer an emoji over the face, resizing the emoji to fit the face.</span></span>

<span data-ttu-id="652d1-106">Zum Implementieren dieser Funktion verwenden wir die Open Source-Bildbearbeitungsbibliothek [Jimp](https://www.npmjs.com/package/jimp).</span><span class="sxs-lookup"><span data-stu-id="652d1-106">To implement this functionality, we will use the open source image manipulation library [Jimp](https://www.npmjs.com/package/jimp).</span></span>

<span data-ttu-id="652d1-107">In dieser Lektion erfahren Sie, wie Sie mit der `Jimp`-Bibliothek Bilder bearbeiten und insbesondere ein Emoji über ein Gesicht legen und das Bild wieder auf dem Datenträger speichern.</span><span class="sxs-lookup"><span data-stu-id="652d1-107">The goal of this lecture is to learn how to use the `Jimp` library to manipulate images and specifically to learn how to layer an emoji over a face and save that image back out to disk.</span></span>

<span data-ttu-id="652d1-108">Hierzu erweitern wir das `bin/mojify.ts`-Skript, mit dem wir in der vorherigen Lektion begonnen haben, indem wir die `createMojifiedImage`-Funktion erstellen.</span><span class="sxs-lookup"><span data-stu-id="652d1-108">We are going to expand on the `bin/mojify.ts` script we started in the previous lecture by fleshing out the `createMojifiedImage` function.</span></span>

> <span data-ttu-id="652d1-109">HINWEIS: Wir werden den gesamten Code aus diesem Skript wiederverwenden, wenn wir in späteren Lektionen den Slack-Befehl und die Azure-Funktion erstellen.</span><span class="sxs-lookup"><span data-stu-id="652d1-109">NOTE We will be re-using all the code from this script when we create the Slack command and Azure Function in later lectures.</span></span> <span data-ttu-id="652d1-110">Diese Schritte sind also keine vergeudete Mühe.</span><span class="sxs-lookup"><span data-stu-id="652d1-110">It's not wasted effort!</span></span>

## <a name="steps"></a><span data-ttu-id="652d1-111">Schritte</span><span class="sxs-lookup"><span data-stu-id="652d1-111">Steps</span></span>

### <a name="required-imports"></a><span data-ttu-id="652d1-112">Erforderliche Importe</span><span class="sxs-lookup"><span data-stu-id="652d1-112">Required Imports</span></span>

<span data-ttu-id="652d1-113">Um mit Jimp experimentieren und Dateien in unserem Dateisystem bearbeiten zu können, müssen wir zunächst einige Pakete importieren.</span><span class="sxs-lookup"><span data-stu-id="652d1-113">To play around with Jimp and manipulate files on our filesystem we need to import a few packages at the top</span></span>

```typescript
import * as Jimp from "jimp";
import * as path from "path";
```

> <span data-ttu-id="652d1-114">HINWEIS: `path` ist erforderlich, weil wir Dateien vom Datenträger laden möchten.</span><span class="sxs-lookup"><span data-stu-id="652d1-114">NOTE `path` is needed because we want to load files from disk</span></span>

### <a name="basic-use-case"></a><span data-ttu-id="652d1-115">Einfacher Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="652d1-115">Basic Use Case</span></span>

<span data-ttu-id="652d1-116">Vereinfachen wir das Ganze, indem wir uns fragen, was wir zum Ausführen der folgenden Aufgaben benötigen:</span><span class="sxs-lookup"><span data-stu-id="652d1-116">Let's strip away a lot of the complexity and ask what it would take to:</span></span>

1. <span data-ttu-id="652d1-117">Ein Bild hochladen</span><span class="sxs-lookup"><span data-stu-id="652d1-117">Load up an image</span></span>
2. <span data-ttu-id="652d1-118">Das Emoji 😕 in der oberen rechten Ecke platzieren (nach der Größenänderung auf 50 x 50 Pixel)</span><span class="sxs-lookup"><span data-stu-id="652d1-118">Place the 😕 emoji in the top right corner (resized to 50x50px)</span></span>
3. <span data-ttu-id="652d1-119">Das Bild speichern</span><span class="sxs-lookup"><span data-stu-id="652d1-119">Save the image</span></span>

<span data-ttu-id="652d1-120">All diese Funktionen können wir wie folgt in sechs Codezeilen implementieren:</span><span class="sxs-lookup"><span data-stu-id="652d1-120">We can implement all the functionality above in 6 lines of code, like so:</span></span>

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

<span data-ttu-id="652d1-121">Wir unterteilen den Code Schritt für Schritt.</span><span class="sxs-lookup"><span data-stu-id="652d1-121">We'll break it down step by step.</span></span>

<span data-ttu-id="652d1-122">Um ein Bild mit `Jimp` zu laden, verwenden wir die `Jimp.read`-Funktion wie folgt:</span><span class="sxs-lookup"><span data-stu-id="652d1-122">To load an image using `Jimp` we use the `Jimp.read` function, like so:</span></span>

```typescript
let sourceImage = await Jimp.read(imageUrl);
```

<span data-ttu-id="652d1-123">Wir haben ein Verzeichnis mit PNG‑Dateien für jedes Emoji in `shared/emojis`.</span><span class="sxs-lookup"><span data-stu-id="652d1-123">We have a directory of png files for each emoji in `shared/emojis`.</span></span> <span data-ttu-id="652d1-124">Jede Emoji-PNG-Datei ist als „<emoji>.png“ benannt. `😕.png` ist folglich eine Datei, die eine PNG-Datei des Emojis 😕 enthält.</span><span class="sxs-lookup"><span data-stu-id="652d1-124">Each emoji png is named as <emoji>.png, so `😕.png` is a file that contains a png of the 😕 emoji.</span></span>

<span data-ttu-id="652d1-125">Wir laden `😕.png` wie folgt hoch:</span><span class="sxs-lookup"><span data-stu-id="652d1-125">We load up `😕.png` like so:</span></span>

```typescript
let mojiPath = path.resolve(__dirname, "../shared/emojis/😕.png");
let emojiImage = await Jimp.read(mojiPath);
```

<span data-ttu-id="652d1-126">Als Nächstes müssen wir die Größe des „emojiImage“ in 50 Pixel (Breite) x 50 Pixel (Höhe) ändern. Diese Anpassung können wir mit der Größenänderungsfunktion wie folgt vornehmen:</span><span class="sxs-lookup"><span data-stu-id="652d1-126">Next up we need to resize the emojiImage to 50 pixels width x 50 pixels height, we can do that by using the resize function like so:</span></span>

```typescript
emojiImage.resize(50, 50);
```

<span data-ttu-id="652d1-127">Die Größe von `emojiImage` wurde nun so geändert, dass das Bild in einen 50 x 50 Pixel großen Bereich passt.</span><span class="sxs-lookup"><span data-stu-id="652d1-127">The `emojiImage` has now been resized to fit in a 50x50 px space.</span></span>

<span data-ttu-id="652d1-128">Jetzt müssen wir das „emojiImage“ wie folgt in der oberen linken Ecke auf dem „sourceImage“ _platzieren_:</span><span class="sxs-lookup"><span data-stu-id="652d1-128">We now need to _place_ the emojiImage over the sourceImage in the top left corner, like so:</span></span>

```typescript
sourceImage = sourceImage.composite(emojiImage, 0, 0);
```

<span data-ttu-id="652d1-129">Wir verwenden die `composite`-Funktion, die `emojiImage` 0 Pixel vom oberen Rand und 0 Pixel vom unteren Rand auf `sourceImage` platziert.</span><span class="sxs-lookup"><span data-stu-id="652d1-129">We use the `composite` function, which places `emojiImage` ontop of `sourceImage` 0 pixels from the top and 0 pixels down.</span></span> <span data-ttu-id="652d1-130">Die `composite`-Funktion ändert `sourceImage` nicht direkt, sondern gibt eine Kopie von `sourceImage` mit darüber platziertem `emojiImage` zurück.</span><span class="sxs-lookup"><span data-stu-id="652d1-130">The `composite` fucntion doesn't alter `sourceImage` in place, instead it returns a copy of `sourceImage` with the `emojiImage` placed on top.</span></span>

<span data-ttu-id="652d1-131">Zum Schluss speichern wir das Ausgabebild wie folgt auf dem Datenträger:</span><span class="sxs-lookup"><span data-stu-id="652d1-131">Finally we save the output image to disk like so:</span></span>

```typescript
sourceImage.write(path.join(__dirname, "..", "mojified.jpg"));
```

### <a name="full-use-case"></a><span data-ttu-id="652d1-132">Vollständiger Anwendungsfall</span><span class="sxs-lookup"><span data-stu-id="652d1-132">Full Use Case</span></span>

<span data-ttu-id="652d1-133">Jetzt wissen Sie, wie `Jimp` funktioniert und wie Sie damit Bilder zusammensetzen können.</span><span class="sxs-lookup"><span data-stu-id="652d1-133">Hopefully by now you have a good understanding of how `Jimp` works and how we can use it to composite images.</span></span> <span data-ttu-id="652d1-134">Wenn wir nun den vollständigen Code für die `createMojifiedImage`-Funktion durchgehen, werden Sie das Prinzip noch besser verstehen.</span><span class="sxs-lookup"><span data-stu-id="652d1-134">So now when we go through the full code for the `createMojifiedImage` function it should make a lot more sense.</span></span>

<span data-ttu-id="652d1-135">Kopieren Sie den unten stehenden Code, und fügen Sie ihn in Ihre `createMojifiedImage`-Funktion in `bin/mojify.ts` ein.</span><span class="sxs-lookup"><span data-stu-id="652d1-135">Copy and paste the bellow code into your `createMojifiedImage` function in `bin/mojify.ts`.</span></span>

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

<span data-ttu-id="652d1-136">Der obige Code ist dem Code für den einfachen Anwendungsfall sehr ähnlich. Anstatt ein Emoji und seine Position hartzucodieren, entscheiden wir jedoch basierend auf einem übergebenen Array von Gesichtern, welches Emoji zusammengesetzt und wo es platziert werden soll.</span><span class="sxs-lookup"><span data-stu-id="652d1-136">The above code is very similar to the base case we just went through, rather than hardcoding an emoji and poisition however we are deciding which emoji to composite and where to place it based on the array of faces passed in.</span></span>

<span data-ttu-id="652d1-137">Das Array von Gesichtern stammt aus der `getFaces`-Funktion, die wir in der letzten Lektion erstellt haben. Alle Elemente sind hier wie folgt in der Main-Funktion verbunden:</span><span class="sxs-lookup"><span data-stu-id="652d1-137">The array of faces comes from the `getFaces` function we fleshed out in the last lecture, it's all connected up together in the main function, like so:</span></span>

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

<span data-ttu-id="652d1-138">Wir rufen `getFaces` mit dem übergebenen `imageUrl` auf, um das Array von `Face`-Instanzen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="652d1-138">We call `getFaces` with the passed in `imageUrl` to get the array of `Face` instances.</span></span>
<span data-ttu-id="652d1-139">Dieses Array übergeben wir zusammen mit dem Originalbild an die `createMojifiedImage`-Funktion, die Emojis auf den Gesichtern von Personen zusammensetzt und die resultierende Datei als `mojified.jpg` im Stammordner des Projekts speichert.</span><span class="sxs-lookup"><span data-stu-id="652d1-139">We pass this array to the `createMojifiedImage` function along with the original image, this function composites emojis on peoples faces and saves the resulting file to the project root folder as `mojified.jpg`</span></span>

### <a name="try-it-out"></a><span data-ttu-id="652d1-140">Ausprobieren</span><span class="sxs-lookup"><span data-stu-id="652d1-140">Try it out</span></span>

<span data-ttu-id="652d1-141">Probieren Sie diesen Code selbst aus:</span><span class="sxs-lookup"><span data-stu-id="652d1-141">Try this code out yourself, like so:</span></span>

```bash
node bin/mojify.js <url>
```

<span data-ttu-id="652d1-142">Wenn es funktioniert hat, sollte eine Version der Quelldatei mit Emojis im Stammordner des Projekts `mojified.jpg` gespeichert worden sein.</span><span class="sxs-lookup"><span data-stu-id="652d1-142">If this worked then a mojified version of the source fil should be stored in the project root called `mojified.jpg`.</span></span>

<span data-ttu-id="652d1-143">Probieren Sie es mit anderen Bildern aus.</span><span class="sxs-lookup"><span data-stu-id="652d1-143">Try it out with different images!</span></span>
