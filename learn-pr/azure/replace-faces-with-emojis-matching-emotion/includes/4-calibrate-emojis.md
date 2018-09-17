<span data-ttu-id="77baa-101">Wir können an die Gesichtserkennungs-API kein Bild des Emojis übergeben, um dessen Emotion zu ermitteln, da es sich dabei nicht um ein menschliches Gesicht handelt.</span><span class="sxs-lookup"><span data-stu-id="77baa-101">We can’t pass an image of the emoji to the Face API to get it’s emotion because, well because it’s not human.</span></span> <span data-ttu-id="77baa-102">Für jedes Emoji war also ein menschlicher Ersatz (ich) erforderlich.</span><span class="sxs-lookup"><span data-stu-id="77baa-102">So for each emoji, I needed a human proxy, me.</span></span>

<span data-ttu-id="77baa-103">Ich habe daher Bilder von mir aufgenommen, auf denen ich jedes Emoji _exakt_ nachstelle, und habe den _emotionalen Punkt_ für dieses Bild als Ersatz für das Emoji verwendet.</span><span class="sxs-lookup"><span data-stu-id="77baa-103">I took pictures of myself _accurately_ mimicking each emoji, and used the _emotional point_ for that image as the proxy for the emoji.</span></span> <span data-ttu-id="77baa-104">Darüber hinaus habe ich Mitglieder meines Teams ausgewählt und sie ebenfalls Emojis zugeordnet:</span><span class="sxs-lookup"><span data-stu-id="77baa-104">To keep things interesting I also chose people from my team and associated them with emojis as well, like so:</span></span>

![Emoji-Team](/media-drafts/team.jpg)

<span data-ttu-id="77baa-106">Für das Emoji mit den Herzaugen (😍) habe ich ein Bild von meiner Frau verwendet (❤️).</span><span class="sxs-lookup"><span data-stu-id="77baa-106">For the emoji of love eyes (😍) I chose a picture of my wife ❤️.</span></span> <span data-ttu-id="77baa-107">Zur Darstellung von 🤔 habe ich im Gedenken an [Stephen Hawking](https://en.wikipedia.org/wiki/Stephen_Hawking) ein Bild von ihm gewählt.</span><span class="sxs-lookup"><span data-stu-id="77baa-107">In memory of [Stephen Hawking](https://en.wikipedia.org/wiki/Stephen_Hawking) I picked a picture of him to represent 🤔.</span></span>

<span data-ttu-id="77baa-108">Die Liste mit den Ersatzbildern für die einzelnen Emojis finden Sie im Beispielcode zu diesem Tutorial im Ordner `bin/proxy-images`.</span><span class="sxs-lookup"><span data-stu-id="77baa-108">You can see the list of proxy images for each emoji in the `bin/proxy-images` folder in the sample code associated with this tutorial.</span></span>

<span data-ttu-id="77baa-109">In diesem Kapitel generieren Sie einen Schlüssel, um die Gesichtserkennungs-API verwenden zu können, und verwenden anschließend die Gesichtserkennungs-API, um alle Emojis mit Ersatzbildern von mir zu kalibrieren.</span><span class="sxs-lookup"><span data-stu-id="77baa-109">In this chapter you will generate a key so you can use the Azure Face API and then use the Face API to calibrate all the emojies using proxied images of me.</span></span>

## <a name="generate-an-azure-face-api-key"></a><span data-ttu-id="77baa-110">Generieren eines Schlüssels für die Gesichtserkennungs-API von Azure</span><span class="sxs-lookup"><span data-stu-id="77baa-110">Generate an Azure Face API Key</span></span>

<!-- To make calls to the Azure Face API we will need a special authorization key.

We are going to create one using the `az` CLI. -->

<span data-ttu-id="77baa-111">Um die Gesichtserkennungs-API von Azure verwenden zu können, benötigen wir einen speziellen Authentifizierungsschlüssel. Navigieren Sie daher zu https://azure.microsoft.com/try/cognitive-services/, und registrieren Sie sich für eine Testversion der Gesichtserkennungs-API.</span><span class="sxs-lookup"><span data-stu-id="77baa-111">To use the Azure Face API we need a special authentication key, head over to https://azure.microsoft.com/try/cognitive-services/ and signup to trial the Face API.</span></span>

![Emoji-Team](/media-drafts/4.calibrating-emojis.get-face-api.png)

> <span data-ttu-id="77baa-113">TODO: Ermitteln von az-Befehlen zum Erstellen der Gesichtserkennungs-API und Abrufen von Schlüsseln</span><span class="sxs-lookup"><span data-stu-id="77baa-113">TODO: Find az commands to create faceAPI and grab keys</span></span>

<!-- > NOTE the Azure Face API doesn't return the emotion information by default, we need to switch on this behavior by setting some query parameters, like so:
> https://westeurope.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion -->

## <a name="setup-the-environment-variables"></a><span data-ttu-id="77baa-114">Einrichten der Umgebungsvariablen</span><span class="sxs-lookup"><span data-stu-id="77baa-114">Setup the environment variables</span></span>

<span data-ttu-id="77baa-115">Für das Kalibrierungsskript müssen die URL und der Schlüssel der Gesichtserkennungs-API angegeben werden, um die korrekten Aufrufe ausführen zu können. Anstelle einer Hartcodierung im Skript verwenden wir Umgebungsvariablen. Führen Sie die folgenden Befehle in dem Terminal aus, in dem Sie voraussichtlich die Anwendung ausführen:</span><span class="sxs-lookup"><span data-stu-id="77baa-115">The calibration script needs to know your Face API URL and Key in order to make the correct calls, rather than hardcoding these in the script we are going to use environment varialbes, run these commands in the terminal you expect to run the application in:</span></span>

```bash
FACE_API_URL=<the-face-api-url>
FACE_API_KEY=<your-face-api-key>
```

<!-- > NOTE
> Don't forget to add the query param returnFaceAttributes=emotion to ensure the Face API returns emotion as well -->

## <a name="create-some-proxy-images-for-emojis"></a><span data-ttu-id="77baa-116">Erstellen einiger Ersatzbilder für Emojis</span><span class="sxs-lookup"><span data-stu-id="77baa-116">Create some proxy images for emojis</span></span>

<span data-ttu-id="77baa-117">Ich habe alle Ersatzbilder bereitgestellt – Sie können aber gerne eigene erstellen.</span><span class="sxs-lookup"><span data-stu-id="77baa-117">I've provided all the proxy images myself, but feel free to generate your own!</span></span>

<span data-ttu-id="77baa-118">Nehmen Sie für jedes Emoji im Ordner `bin/proxy-images` ein Foto von sich selbst auf, auf dem Sie das Emoji nachstellen, und ersetzen Sie das Bild durch Ihr eigenes.</span><span class="sxs-lookup"><span data-stu-id="77baa-118">For each emoji in the `bin/proxy-images` folder, take a picture of yourself mimicking that emoji and replace the image with your image.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="77baa-119">Ausprobieren</span><span class="sxs-lookup"><span data-stu-id="77baa-119">Try it out</span></span>

<span data-ttu-id="77baa-120">Nun kommt der spaßige Teil!</span><span class="sxs-lookup"><span data-stu-id="77baa-120">Now comes the fun part!</span></span> <span data-ttu-id="77baa-121">Wir schicken jedes der Bilder aus `bin/proxy-images` durch die Gesichtserkennungs-API, um einen emotionalen Punkt für das Emoji im _emotionalen Raum_ zu berechnen:</span><span class="sxs-lookup"><span data-stu-id="77baa-121">We are going to run each of the images in the `bin/proxy-images` through the Face API to calculate an emotional point for that emoji in _emotional space_, run:</span></span>

```bash
node bin/calibrate.js
```

<span data-ttu-id="77baa-122">Die Ausgabe dieses Befehls sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="77baa-122">The output of this command should look something like so:</span></span>

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

<span data-ttu-id="77baa-123">Als Erstes werden die verarbeiteten Emojis ausgegeben. Danach folgt ein Array, das `EmotivePoint` für alle Emojis definiert.</span><span class="sxs-lookup"><span data-stu-id="77baa-123">It will first print out the emoji's it is processing and then finally print out to the console an array which defines the `EmotivePoint` of all the emoji's.</span></span> <span data-ttu-id="77baa-124">Das Format entspricht dabei dem Format des Arrays in `shared/mojis.ts`.</span><span class="sxs-lookup"><span data-stu-id="77baa-124">This is the same format as the array in `shared/mojis.ts`.</span></span>

<span data-ttu-id="77baa-125">Falls Sie Ersatzbilder geändert haben, kopieren Sie die Ausgabe dieses Skripts in den entsprechenden Abschnitt von `mojis.ts`.</span><span class="sxs-lookup"><span data-stu-id="77baa-125">If you changed some of the proxied images then copy the output of this script to the relevant section of `mojis.ts`</span></span>
