<span data-ttu-id="28656-101">Im letzten Kapitel wurde beschrieben, dass die Datei `shared/mojis.ts` über eine Liste mit Emojis und die zugehörigen emotionalen Punkte verfügt.</span><span class="sxs-lookup"><span data-stu-id="28656-101">In the last chapter we learnt that `shared/mojis.ts` file has a list of emojis and their emotional points.</span></span>

<span data-ttu-id="28656-102">In diesem Kapitel wird der Rest des Codes beschrieben, den wir verwenden, um ein Gesicht einem Emoji zuzuordnen.</span><span class="sxs-lookup"><span data-stu-id="28656-102">In this chapter we will learn about the rest of the code that we will use to map a face to an emoji.</span></span>

<span data-ttu-id="28656-103">Sie lernen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="28656-103">You will learn how to:</span></span>

1. <span data-ttu-id="28656-104">Erstellen eines Skripts zum Übergeben einer URL zum Bild eines Gesichts</span><span class="sxs-lookup"><span data-stu-id="28656-104">Create a script where you pass in a URL of an image of a face.</span></span>
2. <span data-ttu-id="28656-105">Berechnen des emotionalen Punkts von Gesichtern im Bild</span><span class="sxs-lookup"><span data-stu-id="28656-105">Calculate the emotional point of any faces in the image.</span></span>
3. <span data-ttu-id="28656-106">Zuordnen der Gesichter im Bild zu den naheliegendsten Emojis</span><span class="sxs-lookup"><span data-stu-id="28656-106">Map the faces in the image to the closest emojis</span></span>

<span data-ttu-id="28656-107">Abschließend implementieren wir dies in Bezug auf die Funktion dann als Slack-Befehl. Jetzt starten wir aber mit einem einfachen Node-Skript, das Sie in der Befehlszeile ausführen können:</span><span class="sxs-lookup"><span data-stu-id="28656-107">Eventually we will be implementing this functionally as a Slack command, but for now we are going to start with a simple node script that you can run on the comand line, like so:</span></span>

```bash
node bin/mojify.js <url-of-image-with-face>
```

## <a name="debugging-typescript"></a><span data-ttu-id="28656-108">Debuggen von TypeScript</span><span class="sxs-lookup"><span data-stu-id="28656-108">Debugging TypeScript</span></span>

<span data-ttu-id="28656-109">Wir schreiben in TypeScript, aber die Ausführung erfolgt per JavaScript.</span><span class="sxs-lookup"><span data-stu-id="28656-109">We are writing in TypeScript but executing JavaScript.</span></span> <span data-ttu-id="28656-110">Dies erschwert das Debuggen, da wir Breakpoints setzen und in den transpilierten JavaScript-Dateien debuggen müssen, die ggf. schwierig zu lesen sind.</span><span class="sxs-lookup"><span data-stu-id="28656-110">This makes debugging hard as we would have to set breakpoints and debug in the transpiled JavaScript files which can be hard to read.</span></span>

<span data-ttu-id="28656-111">Idealerweise sollte das Schreiben _und_ Debuggen in TypeScript erfolgen.</span><span class="sxs-lookup"><span data-stu-id="28656-111">What we ideally want is to write _and_ debug in TypeScript.</span></span>

<span data-ttu-id="28656-112">Die gute Nachricht ist, dass dies mit VS Code bei nur geringem Konfigurationsaufwand möglich ist.</span><span class="sxs-lookup"><span data-stu-id="28656-112">The good news is that it's possible with vs code with just a little bit of configuration.</span></span>

<span data-ttu-id="28656-113">Öffnen Sie die Datei `launch.json`, indem Sie die Befehlspalette verwenden: `Ctrl+P > Debug: Open launch.json`.</span><span class="sxs-lookup"><span data-stu-id="28656-113">Open up the `launch.json` file by using the command paletee `Ctrl+P > Debug: Open launch.json`</span></span>

> <span data-ttu-id="28656-114">TODO: Bild</span><span class="sxs-lookup"><span data-stu-id="28656-114">TODO: Image</span></span>

<span data-ttu-id="28656-115">Fügen Sie wie folgt eine Konfigurationsoption hinzu:</span><span class="sxs-lookup"><span data-stu-id="28656-115">Add in a configuration option like so:</span></span>

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

<span data-ttu-id="28656-116">Im Menü für das Debuggen wird jetzt die Option `Mojify` angezeigt, mit der das mojify-Skript ausgeführt und eine URL als Argument übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="28656-116">Now in the debug menu you will see an option called `Mojify` this will run the mojify script passing in a URL as the argument.</span></span> <span data-ttu-id="28656-117">Sie können in der TypeScript-Datei Breakpoints setzen und darin direkt Variablen untersuchen.</span><span class="sxs-lookup"><span data-stu-id="28656-117">You will be able to set breakpoints in the TypeScript file and inspect variables directly from there.</span></span>

## <a name="open-up-binmojists"></a><span data-ttu-id="28656-118">Öffnen Sie `bin/mojis.ts`.</span><span class="sxs-lookup"><span data-stu-id="28656-118">Open up `bin/mojis.ts`</span></span>

<span data-ttu-id="28656-119">Das Gerüst für die Datei mit allen erforderlichen Importen steht bereits:</span><span class="sxs-lookup"><span data-stu-id="28656-119">The file is already scaffolded with all the required imports, like so:</span></span>

```typescript
require("dotenv").config();
import fetch from "node-fetch";
import { EmotivePoint, Face, Rect } from "../shared/models";
```

<span data-ttu-id="28656-120">`dotenv` ist ein Hilfsprogrammpaket, mit dem der Inhalt einer ENV-Datei im Stamm Ihres Projekts in Form von Umgebungsvariablen geladen wird. Dies ist hilfreich für die Entwicklung.</span><span class="sxs-lookup"><span data-stu-id="28656-120">`dotenv` is a helper package which loads up the contents of a .env file in the root of your project as environment variables, useful for development.</span></span>

<span data-ttu-id="28656-121">Wir verwenden `node-fetch`, um HTTP-Anforderungen an die Azure-Gesichtserkennungs-API zu senden.</span><span class="sxs-lookup"><span data-stu-id="28656-121">`node-fetch` we use to make http requests to the Azure Face API.</span></span>

<span data-ttu-id="28656-122">`EmotivePoint` ist eine Hilfsklasse, mit der ein Punkt im _emotionalen Raum_ beschrieben wird. Hierauf gehen wir weiter unten näher ein.</span><span class="sxs-lookup"><span data-stu-id="28656-122">`EmotivePoint` is a helper class that describes a point in _emotional space_ - we will be discussing this in more details below.</span></span>

<span data-ttu-id="28656-123">`Rect` ist eine Hilfsklasse zum Beschreiben einer rechteckigen Form. Wir nutzen sie, um die Position eines Gesichts in einem Bild zu beschreiben.</span><span class="sxs-lookup"><span data-stu-id="28656-123">`Rect` is a helper class to describe a rectangle shape, we use this to describe the position of a face in an image.</span></span>

<span data-ttu-id="28656-124">`Face` ist eine Hilfsprogrammklasse, mit der die Informationen zum Rechteck und emotionalen Punkt eines Gesichts in einem Bild kombiniert werden.</span><span class="sxs-lookup"><span data-stu-id="28656-124">`Face` is a helper utility class which combines the rectangle and emotive point informatoin about a face in an image.</span></span>

<span data-ttu-id="28656-125">Im mittleren Bereich der Datei sollten einige Stub-Funktionen angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="28656-125">In the middle of the file you should see some stub functions, like so:</span></span>

```typescript
async function getFaces(imageUrl) {
  //TODO
}

async function createMojifiedImage(imageUrl, faces) {
  //TODO
}
```

<span data-ttu-id="28656-126">Hierbei handelt es sich um die Funktionen, die Sie in dieser und der nächsten Lektion gestalten.</span><span class="sxs-lookup"><span data-stu-id="28656-126">These are the functions you will be fleshing out in this lecture and the next</span></span>

<span data-ttu-id="28656-127">Am Ende der Datei sollte dieser Code angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="28656-127">At the end of the file you should see this code</span></span>

```typescript
async function main() {
  const [imageUrl] = process.argv.slice(2);
  console.log(imageUrl);
  const faces = await getFaces(imageUrl);
  await createMojifiedImage(imageUrl, faces);
}
main();
```

## <a name="add-the-environment-variables"></a><span data-ttu-id="28656-128">Hinzufügen der Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="28656-128">Add the environment variables</span></span>

<span data-ttu-id="28656-129">Da wir die Gesichtserkennungs-API aufrufen, müssen wir die zuvor generierten geheimen Schlüssel und URLs verwenden und oben in der Datei unter den Importen hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="28656-129">We are going to call the Face API so we need to use those secret keys and urls we generated before, add this to the top of the file under the imports:</span></span>

```typescript
const API_URL = process.env["FACE_API_URL"];
const API_KEY = process.env["FACE_API_KEY"];
```

## <a name="call-the-face-api-with-the-provided-image-and-get-a-response"></a><span data-ttu-id="28656-130">Aufrufen der Gesichtserkennungs-API mit dem angegebenen Bild und Erhalten einer Antwort</span><span class="sxs-lookup"><span data-stu-id="28656-130">Call the Face API with the provided image and get a response</span></span>

<span data-ttu-id="28656-131">Wir fügen diesen Code oben in der Funktion `getFaces` hinzu, um eine Anforderung an die Gesichtserkennungs-API zu senden.</span><span class="sxs-lookup"><span data-stu-id="28656-131">To make a reques to the Face API we add this code to the top of the `getFaces` function</span></span>

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

<span data-ttu-id="28656-132">Im obigen Code wird der Befehl `fetch` verwendet, um eine `POST`-Anforderung an die Gesichtserkennungs-API zu senden.</span><span class="sxs-lookup"><span data-stu-id="28656-132">The code above uses the `fetch` command to send a `POST` request to the Face API.</span></span>

<span data-ttu-id="28656-133">Wir übergeben den `API_KEY` im Header, damit die Gesichtserkennungs-API über unsere Anforderung informiert ist. Andernfalls wird die Anforderung abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="28656-133">We pass the `API_KEY` in the header so the Face API knows the request comes from us, otherwise the request is rejected.</span></span>

<span data-ttu-id="28656-134">Wir übergeben die `imageUrl`, die von der Gesichtserkennungs-API im Text analysiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="28656-134">We pass the `imageUrl` we want the Face API to analyse in the body.</span></span>

<span data-ttu-id="28656-135">Anschließend erhalten wir die Antwort von der API-Anforderung und geben sie aus.</span><span class="sxs-lookup"><span data-stu-id="28656-135">We then get the responce from the API request and print it out.</span></span>

<span data-ttu-id="28656-136">Bei Ausführung des Skripts mit:</span><span class="sxs-lookup"><span data-stu-id="28656-136">If you now run the script with</span></span>

```bash
node bin/mojify.js <path-to-image>
```

<span data-ttu-id="28656-137">Die JSON-Antwort, die beim Übergeben dieses Bilds an die Gesichtserkennungs-API zurückgegeben wurde, sollte ausgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="28656-137">It should print out the json responce returned from passing that image to the face API.</span></span>

## <a name="parse-the-responce"></a><span data-ttu-id="28656-138">Analysieren der Antwort</span><span class="sxs-lookup"><span data-stu-id="28656-138">Parse the responce</span></span>

<span data-ttu-id="28656-139">Zum Berechnen von Emojis müssen Sie jedes Gesicht, das in der Antwort von der API zurückgegeben wird, in eine Instanz einer `Face`-Klasse konvertieren.</span><span class="sxs-lookup"><span data-stu-id="28656-139">To calculate the emojis ee need to convert each face returned in the responce from the API to an instance of a `Face` class.</span></span>

<span data-ttu-id="28656-140">Wir fügen diesen Code direkt nach dem Aufrufen der API in der Funktion `getFaces` hinzu:</span><span class="sxs-lookup"><span data-stu-id="28656-140">We add this code just after the code to call the API in the `getFaces` fucntion:</span></span>

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

- <span data-ttu-id="28656-141">Wir durchlaufen die einzelnen Gesichter, die in der Antwort zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="28656-141">We loop through each face returned in the responce.</span></span>
- <span data-ttu-id="28656-142">Wir generieren aus dem zurückgegebenen JSON-Code die Elemente `EmotivePoint`, `Rect` und `Face`.</span><span class="sxs-lookup"><span data-stu-id="28656-142">We generate an `EmotivePoint`, a `Rect` and a `Face` from the returned json.</span></span>
- <span data-ttu-id="28656-143">Durch die Erstellung der `Face`-Instanz wird das Gesicht mit einem Emoji abgeglichen.</span><span class="sxs-lookup"><span data-stu-id="28656-143">Creating the `Face` instance matches the face to an emoji</span></span>
- <span data-ttu-id="28656-144">Um zu ermitteln, für welches Emoji sich die Übereinstimmung ergeben hat, geben wir das `mojiicon`-Element aus.</span><span class="sxs-lookup"><span data-stu-id="28656-144">To see which emoji was matched we print out the `mojiicon`.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="28656-145">Testen</span><span class="sxs-lookup"><span data-stu-id="28656-145">Try it out</span></span>

<span data-ttu-id="28656-146">Wenn Sie das Skript jetzt ausführen, sollte Folgendes durchgeführt werden:</span><span class="sxs-lookup"><span data-stu-id="28656-146">Now if you run the script it should:</span></span>

- <span data-ttu-id="28656-147">Übergeben des bereitgestellten Bilds über die Gesichtserkennungs-API und Berechnen der Emotion</span><span class="sxs-lookup"><span data-stu-id="28656-147">Pass the provided image through the Face API and calculate the emotion.</span></span>
- <span data-ttu-id="28656-148">Abgleichen der Emotionen mit Emojis</span><span class="sxs-lookup"><span data-stu-id="28656-148">Match emotions to emojis.</span></span>
- <span data-ttu-id="28656-149">Ausgeben der Emojis im Terminal</span><span class="sxs-lookup"><span data-stu-id="28656-149">Print the emojis to the terminal.</span></span>

<span data-ttu-id="28656-150">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="28656-150">Like so:</span></span>

```bash
node bin/mojify.js <path-to-image>
<path-to-image>
😕
```
