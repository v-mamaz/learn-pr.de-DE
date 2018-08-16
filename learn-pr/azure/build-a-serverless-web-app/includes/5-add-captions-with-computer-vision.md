<span data-ttu-id="cddb5-101">An diesem Punkt ist die Anwendung eine funktionale Katalog, der Ihnen die Möglichkeit zum Hochladen und Anzeigen von Bildern.</span><span class="sxs-lookup"><span data-stu-id="cddb5-101">At this point, the application is a functional gallery that allows you to upload and view images.</span></span> <span data-ttu-id="cddb5-102">In diesem Modul erfahren Sie, wie Sie mit der maschinelles sehen-API von Microsoft Cognitive Services zum Generieren von Untertiteln für hochgeladene Bilder, und speichern die Beschriftungen der Image-Metadaten in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cddb5-102">In this module, you learn how to use the Computer Vision API from Microsoft Cognitive Services to generate captions for uploaded images and save the captions with the image metadata in Cosmos DB.</span></span>

## <a name="create-a-computer-vision-account"></a><span data-ttu-id="cddb5-103">Erstellen Sie ein Konto für die maschinelles sehen</span><span class="sxs-lookup"><span data-stu-id="cddb5-103">Create a Computer Vision account</span></span>

<span data-ttu-id="cddb5-104">Microsoft Cognitive Services ist eine Sammlung von Diensten, die für Entwickler, um ihre Anwendungen intelligenter zu machen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-104">Microsoft Cognitive Services is a collection of services available to developers to make their applications more intelligent.</span></span> <span data-ttu-id="cddb5-105">Das Computer Vision-API ist ein serverlose Dienst, der Images, die mithilfe von erweiterten Algorithmen verarbeitet, und gibt Informationen über jedes Image zurück.</span><span class="sxs-lookup"><span data-stu-id="cddb5-105">The Computer Vision API is a serverless service that processes images using advanced algorithms and returns information about each image.</span></span> <span data-ttu-id="cddb5-106">Er verfügt über einen free-Tarif, der bis zu 5000-API-Aufrufe pro Monat bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="cddb5-106">It has a free tier that provides up to 5000 API calls per month.</span></span>

1. <span data-ttu-id="cddb5-107">Stellen Sie sicher, dass Sie immer noch in der Cloud Shell angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="cddb5-107">Ensure you are still signed into the Cloud Shell.</span></span> <span data-ttu-id="cddb5-108">Wählen Sie andernfalls **EINGABETASTE fokusmodus** um eine Cloud Shell-Fenster zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-108">If not, select **Enter focus mode** to open a Cloud Shell window.</span></span> 

1. <span data-ttu-id="cddb5-109">Erstellen eines neuen Cognitive Services-Kontos Art **ComputerVision** durch einen eindeutigen Namen in der Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="cddb5-109">Create a new Cognitive Services account of kind **ComputerVision** with a unique name in your resource group.</span></span> <span data-ttu-id="cddb5-110">Verwenden Sie für den free-Tarif, **F0** als SKU.</span><span class="sxs-lookup"><span data-stu-id="cddb5-110">For the free tier, use **F0** as the SKU.</span></span> <span data-ttu-id="cddb5-111">Wenn Sie bereits ein vorhandenes Computer Vision-Konto verfügen, müssen Sie möglicherweise zum Erstellen eines Standard-Kontos (S1); Allerdings kann dies einige Kosten anfallen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-111">If you already have an existing Computer Vision account, you may need to create a Standard account (S1); however, this may incur some costs.</span></span>

    ```azurecli
    az cognitiveservices account create -g first-serverless-app -n <computer vision account name> --kind ComputerVision --sku F0 -l westcentralus
    ```


## <a name="create-function-app-settings-for-computer-vision-url-and-key"></a><span data-ttu-id="cddb5-112">Erstellen von Funktionen-App-Einstellungen für Computer Vision-URL und Schlüssel</span><span class="sxs-lookup"><span data-stu-id="cddb5-112">Create Function App settings for Computer Vision URL and key</span></span>

<span data-ttu-id="cddb5-113">Zum Aufrufen der maschinelles sehen-API sind eine URL und den Schlüssel erforderlich.</span><span class="sxs-lookup"><span data-stu-id="cddb5-113">To call the Computer Vision API, a URL and key are required.</span></span>

1. <span data-ttu-id="cddb5-114">Erhalten Sie das Computer Vision-API-Schlüssel und die URL zu, und speichern Sie sie in der Bash-Variablen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-114">Obtain the Computer Vision API key and URL and save them in bash variables.</span></span>

    ```azurecli
    export COMP_VISION_KEY=$(az cognitiveservices account keys list -g first-serverless-app -n <computer vision account name> --query key1 --output tsv)
    ```
    ```azurecli
    export COMP_VISION_URL=$(az cognitiveservices account show -g first-serverless-app -n <computer vision account name> --query endpoint --output tsv)
    ```

1. <span data-ttu-id="cddb5-115">Erstellen von Appeinstellungen, die mit dem Namen **COMP_VISION_KEY** und **COMP_VISION_URL**, in der Funktions-app.</span><span class="sxs-lookup"><span data-stu-id="cddb5-115">Create app settings named **COMP_VISION_KEY** and **COMP_VISION_URL**, respectively, in the function app.</span></span>

    ```azurecli
    az functionapp config appsettings set -n <function app name> -g first-serverless-app --settings COMP_VISION_KEY=$COMP_VISION_KEY COMP_VISION_URL=$COMP_VISION_URL -o table
    ```


## <a name="call-computer-vision-api-from-resizeimage-function"></a><span data-ttu-id="cddb5-116">Rufen Sie die Computer Vision-API von ResizeImage-Funktion</span><span class="sxs-lookup"><span data-stu-id="cddb5-116">Call Computer Vision API from ResizeImage function</span></span>

<span data-ttu-id="cddb5-117">In den folgenden Schritten ändern Sie die **ResizeImage** Funktion zum Aufrufen der maschinelles sehen-API zum Beschreiben jedes hochgeladene Bild aus, und speichern die Beschreibung in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cddb5-117">In the following steps, you modify the **ResizeImage** function to call the Computer Vision API to describe each uploaded image and save the description in Cosmos DB.</span></span>

1. <span data-ttu-id="cddb5-118">Öffnen Sie Ihre Funktionen-app im Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="cddb5-118">Open your function app in the Azure Portal.</span></span>

1. <span data-ttu-id="cddb5-119">**C#**</span><span class="sxs-lookup"><span data-stu-id="cddb5-119">**C#**</span></span>

    1. <span data-ttu-id="cddb5-120">(C#) Suchen Sie im linken Navigationsbereich mit der **ResizeImage** Funktion, und öffnen Sie das Codefenster.</span><span class="sxs-lookup"><span data-stu-id="cddb5-120">(C#) Using the left navigation, locate the **ResizeImage** function and open its code window.</span></span>

    1. <span data-ttu-id="cddb5-121">(C#) Ersetzen Sie den Code mit dem Inhalt der [ **/csharp/ResizeImage/run-module5.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run-module5.csx).</span><span class="sxs-lookup"><span data-stu-id="cddb5-121">(C#) Replace the code with the contents of [**/csharp/ResizeImage/run-module5.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run-module5.csx).</span></span> <span data-ttu-id="cddb5-122">Dieser Code verwendet `HttpClient` Computer Vision-API aufrufen, und speichern das Ergebnis in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cddb5-122">This code uses `HttpClient` to call Computer Vision API and save its result in Cosmos DB.</span></span>

1. <span data-ttu-id="cddb5-123">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="cddb5-123">**JavaScript**</span></span>

    1. <span data-ttu-id="cddb5-124">(JavaScript) Diese Funktion erfordert die `axios` Paket von Npm, um die Computer Vision-API eine HTTP-aufrufen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-124">(JavaScript) This function requires the `axios` package from npm to make an HTTP call to the Computer Vision API.</span></span> <span data-ttu-id="cddb5-125">Klicken Sie zum Installieren des Npm-Pakets klicken Sie auf der Funktions-App-Namen im linken Navigationsbereich, und klicken Sie auf **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="cddb5-125">To install the npm package, click on the Function App's name on the left navigation and click **Platform features**.</span></span>

    1. <span data-ttu-id="cddb5-126">(JavaScript) Klicken Sie auf **Konsole** um ein Konsolenfenster anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-126">(JavaScript) Click **Console** to reveal a console window.</span></span>

    1. <span data-ttu-id="cddb5-127">(JavaScript) Führen Sie den Befehl `npm install axios` in der Konsole.</span><span class="sxs-lookup"><span data-stu-id="cddb5-127">(JavaScript) Run the command `npm install axios` in the console.</span></span> <span data-ttu-id="cddb5-128">Es dauert etwas, um den Vorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-128">It may take a minute or two to complete the operation.</span></span>

    1. <span data-ttu-id="cddb5-129">(JavaScript) Klicken Sie auf den Namen der Funktion (**ResizeImage**) im linken Navigationsbereich auf die Funktion anzuzeigen, und Ersetzen Sie alle **"Index.js"** mit dem Inhalt der [ **/javascript/ ResizeImage/Index-module5.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index-module5.js).</span><span class="sxs-lookup"><span data-stu-id="cddb5-129">(JavaScript) Click on the function name (**ResizeImage**) in the left navigation to reveal the function, and then replace all of **index.js** with the contents of [**/javascript/ResizeImage/index-module5.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index-module5.js).</span></span>

1. <span data-ttu-id="cddb5-130">Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="cddb5-130">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="cddb5-131">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="cddb5-131">Click **Save**.</span></span> <span data-ttu-id="cddb5-132">Überprüfen Sie im Bereich Protokolle, um sicherzustellen, dass die Funktion wurde erfolgreich gespeichert. keine Fehler vorliegen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-132">Check the logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="test-the-application"></a><span data-ttu-id="cddb5-133">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="cddb5-133">Test the application</span></span>

1. <span data-ttu-id="cddb5-134">Öffnen Sie die Anwendung in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="cddb5-134">Open the application in a browser.</span></span> <span data-ttu-id="cddb5-135">Wählen Sie eine Bilddatei, und Laden Sie es hoch.</span><span class="sxs-lookup"><span data-stu-id="cddb5-135">Select an image file, and upload it.</span></span>

1. <span data-ttu-id="cddb5-136">Nach einigen Sekunden sollte die Miniaturansicht des neuen Images auf der Seite angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="cddb5-136">After a few seconds, the thumbnail of the new image should appear on the page.</span></span> <span data-ttu-id="cddb5-137">Zeigen Sie auf das Bild, das die Beschreibung, die vom Computer Vision anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-137">Hover over the image to see the description generated by Computer Vision.</span></span>


## <a name="summary"></a><span data-ttu-id="cddb5-138">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="cddb5-138">Summary</span></span>

<span data-ttu-id="cddb5-139">In dieser Einheit haben Sie gelernt, wie Beschriftungen für jedes hochgeladene Bild mithilfe von Microsoft Cognitive Services-Computer Vision-API automatisch zu generieren.</span><span class="sxs-lookup"><span data-stu-id="cddb5-139">In this unit, you learned how to automatically generate captions for each uploaded image using Microsoft Cognitive Services Computer Vision API.</span></span> <span data-ttu-id="cddb5-140">Als Nächstes erfahren Sie, wie Sie Authentifizierung mithilfe von Azure App Service-Authentifizierung zur Anwendung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="cddb5-140">Next, you learn how to add authentication to the application using Azure App Service Authentication.</span></span>