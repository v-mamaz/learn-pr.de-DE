
## <a name="what-is-microsoft-cognitive-services"></a><span data-ttu-id="3f578-101">Was ist Microsoft Cognitive Services?</span><span class="sxs-lookup"><span data-stu-id="3f578-101">What is Microsoft Cognitive Services?</span></span>

<span data-ttu-id="3f578-102">Microsoft Cognitive Services ist eine Sammlung von Algorithmen für maschinelles Lernen, die als Dienst für alle Benutzer verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="3f578-102">Microsoft Cognitive Services is a set of machine learning algorithms available as a service for anyone to use.</span></span> <span data-ttu-id="3f578-103">Statt diese Intelligenz selbst von Grund auf zu erstellen, können wir diese Dienste für Sehen, Sprache, Wissen und Suche verwenden.</span><span class="sxs-lookup"><span data-stu-id="3f578-103">Instead of building this intelligence for our apps from scratch, we can use these services for vision, speech, language, knowledge, and search.</span></span> <span data-ttu-id="3f578-104">Sie können jeden Dienst kostenlos ausprobieren.</span><span class="sxs-lookup"><span data-stu-id="3f578-104">You can try each service for free.</span></span> <span data-ttu-id="3f578-105">Wenn Sie sich dafür entscheiden, einen Dienst in Ihre App zu integrieren, müssen Sie die Registrierung für ein kostenpflichtiges Abonnement durchführen.</span><span class="sxs-lookup"><span data-stu-id="3f578-105">When you decide to integrate a service into your app, you sign up for a paid subscription.</span></span> <span data-ttu-id="3f578-106">Wir konzentrieren uns auf die Maschinelles Sehen-API in diesem Modell.</span><span class="sxs-lookup"><span data-stu-id="3f578-106">We'll focus our attention on the Computer Vision API in this model.</span></span>

> [!TIP]
> <span data-ttu-id="3f578-107">Im [Cognitive Services-Verzeichnis](https://azure.microsoft.com/services/cognitive-services/directory/) finden Sie eine Liste mit sämtlichen Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="3f578-107">To see a list of all Cognitive Services, check out the [Cognitive Services Directory](https://azure.microsoft.com/services/cognitive-services/directory/).</span></span> 

## <a name="what-is-the-computer-vision-api"></a><span data-ttu-id="3f578-108">Was ist die Maschinelles Sehen-API?</span><span class="sxs-lookup"><span data-stu-id="3f578-108">What is the Computer Vision API?</span></span>

<span data-ttu-id="3f578-109">Die Maschinelles Sehen-API stellt Algorithmen für die Verarbeitung von Abbildungen und die Rückgabe von Einblicken bereit.</span><span class="sxs-lookup"><span data-stu-id="3f578-109">The Computer Vision API provides algorithms to process images and return insights.</span></span> <span data-ttu-id="3f578-110">Sie können beispielsweise herausfinden, ob eine Abbildung potenziell anstößige Inhalte aufweist oder mithilfe der API alle Gesichter in einer Abbildung finden.</span><span class="sxs-lookup"><span data-stu-id="3f578-110">For example, you can find out if an image has mature content, or can use it to find all the faces in an image.</span></span> <span data-ttu-id="3f578-111">Die API verfügt auch über weitere Features, wie z.B. das Schätzen von dominanten Farben und Akzentfarben, das Kategorisieren des Inhalts von Abbildungen sowie das Beschreiben einer Abbildung in vollständigen Sätzen auf Englisch.</span><span class="sxs-lookup"><span data-stu-id="3f578-111">It also has other features like estimating dominant and accent colors, categorizing the content of images, and describing an image with complete English sentences.</span></span> <span data-ttu-id="3f578-112">Darüber hinaus kann die Maschinelles Sehen-API zur effektiven Darstellung großer Bilder auf intelligente Weise Miniaturansichten generieren.</span><span class="sxs-lookup"><span data-stu-id="3f578-112">Additionally, it can also intelligently generate images thumbnails for displaying large images effectively.</span></span>

> [!TIP]
> <span data-ttu-id="3f578-113">Die Maschinelles Sehen-API ist weltweit in vielen Regionen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="3f578-113">The Computer Vision API is available in many regions across the globe.</span></span> <span data-ttu-id="3f578-114">Unter [Verfügbare Produkte nach Region](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all) können Sie nach der nächstgelegenen Region suchen.</span><span class="sxs-lookup"><span data-stu-id="3f578-114">To find the region nearest you, see the [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all).</span></span>

<span data-ttu-id="3f578-115">Sie können mit der Maschinelles Sehen-API folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="3f578-115">You can use the Computer Vision API to:</span></span>

- <span data-ttu-id="3f578-116">Analysieren von Bildern, um Erkenntnisse zu gewinnen</span><span class="sxs-lookup"><span data-stu-id="3f578-116">Analyze images for insight</span></span>
- <span data-ttu-id="3f578-117">Extrahieren von gedrucktem Text aus Bildern mittels optischer Zeichenerkennung (Optical Character Recognition, OCR).</span><span class="sxs-lookup"><span data-stu-id="3f578-117">Extract printed text from images using optical character recognition (OCR).</span></span>
- <span data-ttu-id="3f578-118">Erkennen von gedrucktem und handschriftlichem Text in Bildern</span><span class="sxs-lookup"><span data-stu-id="3f578-118">Recognize printed and handwritten text from images</span></span>
- <span data-ttu-id="3f578-119">Erkennen von Prominenten und Sehenswürdigkeiten</span><span class="sxs-lookup"><span data-stu-id="3f578-119">Recognize celebrities and landmarks</span></span>
- <span data-ttu-id="3f578-120">Analysieren von Videos</span><span class="sxs-lookup"><span data-stu-id="3f578-120">Analyze video</span></span> 
- <span data-ttu-id="3f578-121">Generieren von Miniaturansichten eines Bilds</span><span class="sxs-lookup"><span data-stu-id="3f578-121">Generate a thumbnail of an image</span></span> 

## <a name="how-to-call-the-computer-vision-api"></a><span data-ttu-id="3f578-122">Aufrufen der Maschinelles Sehen-API</span><span class="sxs-lookup"><span data-stu-id="3f578-122">How to call the Computer Vision API</span></span>

<span data-ttu-id="3f578-123">Sie rufen die Maschinelles Sehen-API in Ihrer Anwendung über Clientbibliotheken oder direkt über die REST-API auf.</span><span class="sxs-lookup"><span data-stu-id="3f578-123">You call Computer Vision in your application using client libraries or the REST API directly.</span></span> <span data-ttu-id="3f578-124">In diesem Modul rufen wir die REST-API auf.</span><span class="sxs-lookup"><span data-stu-id="3f578-124">We'll call the REST API in this module.</span></span> <span data-ttu-id="3f578-125">So rufen Sie die API auf:</span><span class="sxs-lookup"><span data-stu-id="3f578-125">To make a call:</span></span>

1. <span data-ttu-id="3f578-126">Abrufen eines API-Zugriffsschlüssels</span><span class="sxs-lookup"><span data-stu-id="3f578-126">Get an API access key</span></span>

    <span data-ttu-id="3f578-127">Wenn Sie sich für ein Maschinelles Sehen-Dienstkonto registrieren, werden Ihnen Zugriffsschlüssel zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="3f578-127">You are assigned access keys when you sign up for a Computer Vision service account.</span></span> <span data-ttu-id="3f578-128">Im Header **jeder** Anforderung muss ein Schlüssel übergeben werden.</span><span class="sxs-lookup"><span data-stu-id="3f578-128">A key must be passed in the header of **every** request.</span></span> 

1. <span data-ttu-id="3f578-129">POST-Aufruf in der API</span><span class="sxs-lookup"><span data-stu-id="3f578-129">Make a POST call to the API</span></span>

    <span data-ttu-id="3f578-130">Formatieren Sie die URL wie folgt: **Region**.api.cognitive.microsoft.com/vision/v2.0/**Ressource**/**[Parameter]**</span><span class="sxs-lookup"><span data-stu-id="3f578-130">Format the URL as follows: **region**.api.cognitive.microsoft.com/vision/v2.0/**resource**/**[parameters]**</span></span> 

    - <span data-ttu-id="3f578-131">**Region**: die Region, in der Sie das Konto erstellt, z.B. *westus*.</span><span class="sxs-lookup"><span data-stu-id="3f578-131">**region** - the region where you created the account, for example, *westus*.</span></span>
    - <span data-ttu-id="3f578-132">**Ressource**: Die von Ihnen aufgerufene Maschinelles Sehen-Ressource, z.B. `analyze`, `describe`, `generateThumbnail`, `ocr`, `models`, `recognizeText` oder `tag`.</span><span class="sxs-lookup"><span data-stu-id="3f578-132">**resource** - the Computer Vision resource you are calling such as `analyze`, `describe`, `generateThumbnail`, `ocr`, `models`, `recognizeText`, `tag`.</span></span>

    <span data-ttu-id="3f578-133">Sie können das zu verarbeitende Bild entweder als unformatiertes Binärbild oder als Bild-URL übermitteln.</span><span class="sxs-lookup"><span data-stu-id="3f578-133">You can supply the image to be processed either as a raw image binary or an image URL.</span></span>

    <span data-ttu-id="3f578-134">Der Anforderungsheader muss den Abonnementschlüssel enthalten, der Zugriff auf diese API ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="3f578-134">The request header must contain the subscription key, which provides access to this API.</span></span>

1. <span data-ttu-id="3f578-135">Analysieren der Antwort</span><span class="sxs-lookup"><span data-stu-id="3f578-135">Parse the response</span></span>

    <span data-ttu-id="3f578-136">Die Antwort enthält den Einblick, den die Maschinelles Sehen-API als JSON-Nutzlust in Ihr Bild hatte.</span><span class="sxs-lookup"><span data-stu-id="3f578-136">The response holds the insight the Computer Vision API had about your image as a JSON payload.</span></span>

<span data-ttu-id="3f578-137">Angenommen, Sie haben ein Maschinelles Sehen-Abonnement in der Region `westus` erstellt und einen Abonnementschlüssel für den Zugriff auf die API erhalten.</span><span class="sxs-lookup"><span data-stu-id="3f578-137">Suppose you created my Computer Vision subscription in the `westus` region and got a subscription key to access the API.</span></span> <span data-ttu-id="3f578-138">Geben wir diesem Schlüssel den fiktiven Wert `xxxx-xxxxx-xxxx-xxxx`.</span><span class="sxs-lookup"><span data-stu-id="3f578-138">Let's give the key a fictitious value of `xxxx-xxxxx-xxxx-xxxx`.</span></span> <span data-ttu-id="3f578-139">Nun möchten Sie für ein Bild unter `http://example.com/images/test.jpg` eine Miniaturansicht generieren.</span><span class="sxs-lookup"><span data-stu-id="3f578-139">You now want to generate a thumbnail for an image located at `http://example.com/images/test.jpg`.</span></span> <span data-ttu-id="3f578-140">Unter Verwendung von `generateThumbnail` würde die Anforderung wie folgt aussehen.</span><span class="sxs-lookup"><span data-stu-id="3f578-140">Using `generateThumbnail`, the request would look like the following.</span></span>

```
curl POST "https://westus2.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {xxxx-xxxxx-xxxx-xxxx}"
-d "{'url':'http://example.com/images/test.jpg'}"
```

<span data-ttu-id="3f578-141">In diesem Modul führen wir alle Übungen in der Azure CLI mithilfe der integrierten Cloud Shell aus.</span><span class="sxs-lookup"><span data-stu-id="3f578-141">In this module, we'll run all exercises in the Azure CLI using the integrated Cloud Shell.</span></span> <span data-ttu-id="3f578-142">Lassen Sie uns mehr über dieses Setup herausfinden.</span><span class="sxs-lookup"><span data-stu-id="3f578-142">Let's find out a little more about this setup.</span></span>

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="3f578-143">Was ist die Azure CLI?</span><span class="sxs-lookup"><span data-stu-id="3f578-143">What is the Azure CLI</span></span>

<span data-ttu-id="3f578-144">Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="3f578-144">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources.</span></span> <span data-ttu-id="3f578-145">Sie steht für macOS, Linux und Windows sowie unter Verwendung von [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) im Browser zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="3f578-145">It's available for macOS, Linux, and Windows, or in the browser using [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f578-146">Es gibt aktuell zwei Versionen der Azure CLI: Azure CLI 1.0 und Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3f578-146">There are two versions of the Azure CLI tool available today: Azure CLI 1.0 and Azure CLI 2.0.</span></span> <span data-ttu-id="3f578-147">Wir verwenden hier die neueste Version, Azure CLI 2.0, die empfohlen wird, außer wenn Sie ältere Skripts ausführen.</span><span class="sxs-lookup"><span data-stu-id="3f578-147">We'll be using Azure CLI 2.0, which is the latest version and is recommended unless you're running legacy scripts.</span></span> <span data-ttu-id="3f578-148">Die Azure CLI 1.0 wird mit dem Befehl `azure` gestartet, und die Azure CLI 2.0 mit dem Befehl `az`.</span><span class="sxs-lookup"><span data-stu-id="3f578-148">Azure CLI 1.0 is started with the `azure` command, and Azure CLI 2.0 is started with the `az` command.</span></span>

## <a name="az-cognitiveservices-commands"></a><span data-ttu-id="3f578-149">„az cognitiveservices“-Befehle</span><span class="sxs-lookup"><span data-stu-id="3f578-149">az cognitiveservices commands</span></span>

<span data-ttu-id="3f578-150">Die Azure CLI enthält den Befehl `cognitiveservices` zum Verwalten von Cognitive Services-Konten in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f578-150">The Azure CLI includes the `cognitiveservices` command to manage Cognitive Services accounts in Azure.</span></span> <span data-ttu-id="3f578-151">Wir können verschiedene Unterbefehle bereitstellen, um bestimmte Aufgaben auszuführen.</span><span class="sxs-lookup"><span data-stu-id="3f578-151">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="3f578-152">Folgende werden am häufigsten verwendeten:</span><span class="sxs-lookup"><span data-stu-id="3f578-152">The most common include:</span></span>

| <span data-ttu-id="3f578-153">Unterbefehl</span><span class="sxs-lookup"><span data-stu-id="3f578-153">Subcommand</span></span> | <span data-ttu-id="3f578-154">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3f578-154">Description</span></span> |
|-------------|-------------|
| `list` | <span data-ttu-id="3f578-155">Auflisten der verfügbaren Azure Cognitive Services-Konten.</span><span class="sxs-lookup"><span data-stu-id="3f578-155">List available Azure Cognitive Services accounts.</span></span> |
| `account show` | <span data-ttu-id="3f578-156">Abrufen der Details eines Azure Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="3f578-156">Get the details of an Azure Cognitive Services account.</span></span> |
| `account create` | <span data-ttu-id="3f578-157">Erstellen eines Azure Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="3f578-157">Create an Azure Cognitive Services account.</span></span> |
| `account delete` | <span data-ttu-id="3f578-158">Löschen eines Azure Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="3f578-158">Delete an Azure Cognitive Services account.</span></span> |
| `keys list` | <span data-ttu-id="3f578-159">Auflisten der Details eines Azure Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="3f578-159">List the keys of an Azure Cognitive Services account.</span></span> |

<span data-ttu-id="3f578-160">Lassen Sie uns nun mithilfe der Azure CLI ein Cognitive Services-Konto.</span><span class="sxs-lookup"><span data-stu-id="3f578-160">Let's create a Cognitive Services with the Azure CLI.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="3f578-161">Erstellen eines Cognitive Services-Kontos</span><span class="sxs-lookup"><span data-stu-id="3f578-161">Create a Cognitive Services account</span></span>

<span data-ttu-id="3f578-162">Für Aufrufe in der Maschinelles Sehen-API benötigen wir einen API-Zugriffsschlüssel.</span><span class="sxs-lookup"><span data-stu-id="3f578-162">We need an API access key to make calls to the Computer Vision API.</span></span> <span data-ttu-id="3f578-163">Damit wir Zugriffsschlüssel abrufen können, benötigen wir ein Cognitive Services-Konto für die Maschinelles Sehen-API.</span><span class="sxs-lookup"><span data-stu-id="3f578-163">To get access keys, we need a Cognitive Services account for the Computer Vision API.</span></span> <span data-ttu-id="3f578-164">Wir verwenden `az cognitiveservices create` zum Erstellen des Kontos in unserem Abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f578-164">We'll use `az cognitiveservices create` to create the account in our subscription.</span></span>

 <span data-ttu-id="3f578-165">Mit dem Befehl `az cognitiveservices create` wird ein Cognitive Services-Konto in einer Ressourcengruppe erstellt.</span><span class="sxs-lookup"><span data-stu-id="3f578-165">The command `az cognitiveservices create` is used to create a Cognitive Services account in a resource group.</span></span>  <span data-ttu-id="3f578-166">Die folgenden fünf Parameter müssen beim Aufrufen dieses Befehls angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="3f578-166">The following five parameters must be supplied when calling this command.</span></span>

> [!Tip]
> <span data-ttu-id="3f578-167">Die meisten Flags für Azure CLI-Parameter können so abgekürzt werden, dass sie aus einem einzelnen Zeichen bestehen.</span><span class="sxs-lookup"><span data-stu-id="3f578-167">Most flags for Azure CLI parameters can be abbreviated to a single character.</span></span> <span data-ttu-id="3f578-168">Wir könnten beispielsweise `-l` anstelle von `--location` sagen.</span><span class="sxs-lookup"><span data-stu-id="3f578-168">For example, we could say `-l` instead of `--location`.</span></span> <span data-ttu-id="3f578-169">Die lange Form wird aus Gründen der Übersichtlichkeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="3f578-169">The long-form is used for clarity.</span></span>

| <span data-ttu-id="3f578-170">Parameter</span><span class="sxs-lookup"><span data-stu-id="3f578-170">Parameter</span></span> | <span data-ttu-id="3f578-171">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3f578-171">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="3f578-172">Die Ressourcengruppe, zu der das Cognitive Services-Konto gehört.</span><span class="sxs-lookup"><span data-stu-id="3f578-172">The resource group that will own the cognitive services account.</span></span> <span data-ttu-id="3f578-173">In dieser interaktiven Sandboxsitzung verwenden Sie <rgn>[Name der Sandboxressourcengruppe]</rgn>.</span><span class="sxs-lookup"><span data-stu-id="3f578-173">In this interactive sandbox session, you'll use <rgn>[sandbox resource group name]</rgn></span></span> |
| `kind` | <span data-ttu-id="3f578-174">Der API-Name des Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="3f578-174">The API name of cognitive services account.</span></span> |
| `name` | <span data-ttu-id="3f578-175">Der Name des Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="3f578-175">Cognitive service account name.</span></span> |
| `sku` | <span data-ttu-id="3f578-176">Die SKU des Cognitive Services-Kontos.</span><span class="sxs-lookup"><span data-stu-id="3f578-176">The Sku of cognitive services account.</span></span>|
| `location` | <span data-ttu-id="3f578-177">Der Standort oder die Region, von dem bzw. von der aus Sie Aufrufe in dieser API durchführen möchten.</span><span class="sxs-lookup"><span data-stu-id="3f578-177">The location, or region, from which you want to make calls to this API.</span></span> <span data-ttu-id="3f578-178">Wählen Sie mindestens einen Standort aus der nachfolgenden Liste aus.</span><span class="sxs-lookup"><span data-stu-id="3f578-178">Select one of the locations from the list below.</span></span> |

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)] 

<span data-ttu-id="3f578-179">Führen Sie in Azure Cloud Shell folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="3f578-179">Execute the following command in Azure Cloud Shell.</span></span> <span data-ttu-id="3f578-180">Stellen Sie sicher, dass Sie `[location]` durch einen Standort in Ihrer Nähe ersetzen.</span><span class="sxs-lookup"><span data-stu-id="3f578-180">Make sure to replace `[location]` with a location near you.</span></span>

```azurecli
az cognitiveservices account create \
--kind ComputerVision \
--name ComputerVisionService \
--sku S1 \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--location [location]
```

> [!NOTE]
> <span data-ttu-id="3f578-181">Merken Sie sich den ausgewählten Standort.</span><span class="sxs-lookup"><span data-stu-id="3f578-181">Remember the location you have selected.</span></span> <span data-ttu-id="3f578-182">Sie müssen alle Aufrufe in der API von dieser Region aus durchführen.</span><span class="sxs-lookup"><span data-stu-id="3f578-182">You'll make all calls to the API from that region.</span></span>

<span data-ttu-id="3f578-183">Wir haben ein Cognitive Services-Konto für die **Maschinelles Lernen**-API erstellt.</span><span class="sxs-lookup"><span data-stu-id="3f578-183">We've created a cognitive services account for the **ComputerVision** API.</span></span> <span data-ttu-id="3f578-184">Wir haben die SKU *S1* ausgewählt und unserem Konto den Namen **ComputerVisionService** gegeben.</span><span class="sxs-lookup"><span data-stu-id="3f578-184">We selected the *S1* sku and named our account **ComputerVisionService**.</span></span> <span data-ttu-id="3f578-185">Unser Konto gehört zur Ressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**, und wir rufen die API von dem im Parameter `--location` festgelegten Standort aus auf.</span><span class="sxs-lookup"><span data-stu-id="3f578-185">Our account is owned by the resource group **<rgn>[sandbox resource group name]</rgn>** and we'll call the API from the location we set in the `--location` parameter.</span></span> 

<span data-ttu-id="3f578-186">Sobald die Erstellung des Cognitive Services-Kontos durch den Befehl abgeschlossen ist, erhalten Sie eine Antwort im JSON-Format. Diese beinhaltet, dass die Eigenschaft **provisioningState** auf **Erfolgreich** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="3f578-186">Once the command finishes creating the cognitive services account, you'll get a JSON response, which includes **provisioningState** property set to **Succeeded**.</span></span>

## <a name="get-an-access-key"></a><span data-ttu-id="3f578-187">Abrufen eines Zugriffsschlüssels</span><span class="sxs-lookup"><span data-stu-id="3f578-187">Get an access key</span></span>

<span data-ttu-id="3f578-188">Sobald wir unser Konto erfolgreich erstellt haben, können wir die Abonnementschlüssel, oder Zugriffsschlüssel, für dieses Konto abrufen.</span><span class="sxs-lookup"><span data-stu-id="3f578-188">Once we have our account successfully created we can retrieve the subscription keys, or access keys, for this account.</span></span>

1. <span data-ttu-id="3f578-189">Führen Sie in Azure Cloud Shell folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="3f578-189">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[sandbox resource group name]</rgn>
    ```
    
    <span data-ttu-id="3f578-190">Der obige Befehl gibt die Schlüssel zurück, die dem Cognitive Services-Konto **ComputerVisionService** zugeordnet sind, das zu der angegebenen Ressourcengruppe gehört.</span><span class="sxs-lookup"><span data-stu-id="3f578-190">The above command returns the keys associated with the cognitive services account called **ComputerVisionService**, which is owned by the given resource group.</span></span> <span data-ttu-id="3f578-191">Zwei Schlüssel werden zurückgegeben, einer davon ist ein Ersatzschlüssel.</span><span class="sxs-lookup"><span data-stu-id="3f578-191">It returns two keys - one is a spare key.</span></span> <span data-ttu-id="3f578-192">Die Schlüssel sind schwer zu merken. Daher speichern wir den ersten Schlüssel in einer Variable, die wir für sämtliche Aufrufe in der API verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="3f578-192">The keys are difficult to remember, so we'll store the first key in a variable that we'll use for all calls to the API.</span></span>

2.  <span data-ttu-id="3f578-193">Führen Sie in Azure Cloud Shell folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="3f578-193">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    key=$(az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query key1 -o tsv)
    ```
    
    <span data-ttu-id="3f578-194">Die Azure CLI 2.0 verwendet das Argument `--query`, um eine JMESPath-Abfrage für die Ergebnisse von Befehlen auszuführen.</span><span class="sxs-lookup"><span data-stu-id="3f578-194">The Azure CLI 2.0 uses the `--query` argument to execute a JMESPath query on the results of commands.</span></span> <span data-ttu-id="3f578-195">JMESPath ist eine Abfragesprache für JSON, die es ermöglicht, Daten aus der CLI-Ausgabe auszuwählen und zu präsentieren.</span><span class="sxs-lookup"><span data-stu-id="3f578-195">JMESPath is a query language for JSON, giving you the ability to select and present data from CLI output.</span></span> <span data-ttu-id="3f578-196">Diese Abfragen werden für die JSON-Ausgabe vor einer anderen Anzeigeformatierung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="3f578-196">These queries are executed on the JSON output before any display formatting.</span></span>
    <span data-ttu-id="3f578-197">Das Argument `--query` wird von allen Befehlen in der Azure CLI unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3f578-197">The `--query` argument is supported by all commands in the Azure CLI.</span></span> 
    
    <span data-ttu-id="3f578-198">In unserem Beispiel wird die Liste der Schlüssel für einen Eintrag mit dem Namen „key1“ abgefragt und das Ergebnis im **TSV**-Format ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="3f578-198">In our example, we query the list of keys for an entry named "key1" and output the result to **tsv** format.</span></span> <span data-ttu-id="3f578-199">In diesem Format werden Anführungszeichen um den Zeichenfolgenwert entfernt.</span><span class="sxs-lookup"><span data-stu-id="3f578-199">This format removes quotations around the string value.</span></span> <span data-ttu-id="3f578-200">Wir weisen das Ergebnis der Variable **Schlüssel** zu.</span><span class="sxs-lookup"><span data-stu-id="3f578-200">We assign the result to a variable **key**.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="3f578-201">Dieser Schlüssel wird während des gesamten Moduls verwendet. Sie sollten ihn daher am besten in einer Variable speichern.</span><span class="sxs-lookup"><span data-stu-id="3f578-201">We're going to use this key throughout the module, so saving it in a variable is a good idea.</span></span> <span data-ttu-id="3f578-202">Wenn Sie den Wert verlieren oder die Variable gelöscht wird, führen Sie den Befehl erneut aus, um die Variable festzulegen.</span><span class="sxs-lookup"><span data-stu-id="3f578-202">If you lose the value or the variable becomes unset, run the command again to set it.</span></span>  

3. <span data-ttu-id="3f578-203">Führen Sie in Azure Cloud Shell den folgenden Befehl aus, um den Wert unseres Schlüssels anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="3f578-203">To see the value of our key, execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    echo $key
    ```

<span data-ttu-id="3f578-204">Nun, da wir über ein Konto und einen Schlüssel verfügen, können wir einige Aufrufe in der API durchführen.</span><span class="sxs-lookup"><span data-stu-id="3f578-204">Now that we have an account and a key, it's time to make some calls to the API.</span></span>