<span data-ttu-id="89eb6-101">Mojifier ist ein Slack-_Schrägstrich_-Befehl, der die Gesichter von Personen in Bildern durch Emojis ersetzt, die ihren Emotionen entsprechen:</span><span class="sxs-lookup"><span data-stu-id="89eb6-101">TheMojifier is a Slack _slash_ command which replaces peoples faces in images with emojis matching their emotion, like so:</span></span>

![Beispielbild](/media-drafts/example-mojify-image.png)

<span data-ttu-id="89eb6-103">Der Befehl ist so konzipiert, dass er von Slack aus als benutzerdefinierter Befehl ausgeführt werden kann. Sie können den Befehl beliebig benennen. In diesem Beispiel heißt er `mojify`.</span><span class="sxs-lookup"><span data-stu-id="89eb6-103">It's designed to work from Slack as a custom command, you can name the command how you want, for this document I've named it `mojify`.</span></span>

<span data-ttu-id="89eb6-104">Um den Befehlstyp auszuführen, geben Sie `/mojify <image to mojify>` ein:</span><span class="sxs-lookup"><span data-stu-id="89eb6-104">To execute the commmand type `/mojify <image to mojify>`, like so:</span></span>

![Beispielbild](/media-drafts/9.slack-type-mojify.png)

<span data-ttu-id="89eb6-106">Mojifier führt daraufhin folgende Aktionen aus:</span><span class="sxs-lookup"><span data-stu-id="89eb6-106">The mojifier then:</span></span>

1.  <span data-ttu-id="89eb6-107">Berechnen der Emotionen von Personen im Bild</span><span class="sxs-lookup"><span data-stu-id="89eb6-107">Calculates the emotion of any people in the image.</span></span>
2.  <span data-ttu-id="89eb6-108">Zuordnen von Emotionen zu Emojis</span><span class="sxs-lookup"><span data-stu-id="89eb6-108">Matches emotions to emojis.</span></span>
3.  <span data-ttu-id="89eb6-109">Ersetzen von Gesichtern durch Emojis</span><span class="sxs-lookup"><span data-stu-id="89eb6-109">Replaces the faces with emojis.</span></span>
4.  <span data-ttu-id="89eb6-110">Posten des Bilds auf Twitter als Antwort</span><span class="sxs-lookup"><span data-stu-id="89eb6-110">Posts the image back to Twitter as a reply.</span></span>

<span data-ttu-id="89eb6-111">Mojifier wurde mit TypeScript und verschiedenen Azure-Technologien geschrieben, darunter [Azure Functions](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai) und [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai).</span><span class="sxs-lookup"><span data-stu-id="89eb6-111">It’s written using TypeScript and several Azure technologies including [Azure Functions](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai) and [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai)</span></span>

<span data-ttu-id="89eb6-112">In diesem Tutorial erfahren Sie, wie Mojifier entwickelt wurde, und wie Sie Ihren eigenen Slack-Befehl mit Azure-Technologien erstellen.</span><span class="sxs-lookup"><span data-stu-id="89eb6-112">In this tutorial I’m going to explain how TheMojifier was made and show you how to create your own Slack command using Azure technologies.</span></span>

> <span data-ttu-id="89eb6-113">Wo wird TODO nun angezeigt?</span><span class="sxs-lookup"><span data-stu-id="89eb6-113">TODO, where will this be now?</span></span>
> <span data-ttu-id="89eb6-114">Der gesamte Code für Mojifier ist unter [GitHub](https://github.com/jawache/mojifier) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="89eb6-114">All the code for Mojifier is available on [GitHub](https://github.com/jawache/mojifier)</span></span>

# <a name="requirements"></a><span data-ttu-id="89eb6-115">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="89eb6-115">Requirements</span></span>

<span data-ttu-id="89eb6-116">Um Mojifier zu erstellen, benötigen Sie unterschiedliche Azure-Dienste.</span><span class="sxs-lookup"><span data-stu-id="89eb6-116">To build the mojifier, we need to use several Azure services.</span></span>

## <a name="azure-cognitive-services"></a><span data-ttu-id="89eb6-117">Azure Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="89eb6-117">Azure Cognitive Services</span></span>

<span data-ttu-id="89eb6-118">Azure Cognitive Services umfasst eine Reihe von leistungsstarken APIs, mit denen Sie Ihrer Anwendung schnell erweiterte KI-Funktionen hinzufügen können.</span><span class="sxs-lookup"><span data-stu-id="89eb6-118">Azure Cognitive Services are a set of high-level APIs you can use to add advanced AI functionality into your application quickly.</span></span> <span data-ttu-id="89eb6-119">Wenn Sie eine HTTP-Anforderung erstellen können, können Sie Cognitive Services verwenden.</span><span class="sxs-lookup"><span data-stu-id="89eb6-119">If you can make an HTTP request, you can use Cognitive Services.</span></span>

[<span data-ttu-id="89eb6-120">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="89eb6-120">More info</span></span>](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai)

## <a name="azure-functions"></a><span data-ttu-id="89eb6-121">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="89eb6-121">Azure Functions</span></span>

<span data-ttu-id="89eb6-122">So leistungsstark wie Logic Apps ist, müssen Sie Geschäftslogik ggf. mit der gesamten Leistungsfähigkeit einer Programmiersprache schreiben.</span><span class="sxs-lookup"><span data-stu-id="89eb6-122">As powerful as Logic Apps are sometimes you need to write business logic using the full expressiveness of a programming language.</span></span> <span data-ttu-id="89eb6-123">Azure Functions ist eine Technologie, mit der Sie Codeausschnitte hosten können, die auf Ereignisse oder HTTP-Anforderungen reagieren. Azure kümmert sich um die gesamte Skalierung, und Sie bezahlen nur die tatsächlich genutzten Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="89eb6-123">Azure Functions is a technology that lets you host snippets of code that can respond to events or HTTP requests, Azure handles all of the scaling issues for you and you only pay for what you use.</span></span>

[<span data-ttu-id="89eb6-124">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="89eb6-124">More info</span></span>](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai)
