<span data-ttu-id="c135a-101">An diesem Punkt hat die Anwendung den Status einer funktionierenden Galerie, die Ihnen das Hochladen und Anzeigen von Bildern ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="c135a-101">At this point, the application is a functional gallery that allows you to upload and view images.</span></span> <span data-ttu-id="c135a-102">In diesem Modul wird beschrieben, wie Sie die Maschinelles Sehen-API von Microsoft Cognitive Services verwenden, um Titel für hochgeladene Bilder zu generieren und diese mit den Bildmetadaten in Azure Cosmos DB zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c135a-102">In this module, you learn how to use the Computer Vision API from Microsoft Cognitive Services to generate captions for uploaded images and save the captions with the image metadata in Azure Cosmos DB.</span></span>

## <a name="create-a-computer-vision-account"></a><span data-ttu-id="c135a-103">Erstellen eines Kontos vom Typ „Maschinelles Sehen“</span><span class="sxs-lookup"><span data-stu-id="c135a-103">Create a Computer Vision account</span></span>

<span data-ttu-id="c135a-104">Microsoft Cognitive Services ist eine Sammlung von Diensten, mit denen Entwickler ihre Anwendungen um intelligente Funktionen und Features erweitern können.</span><span class="sxs-lookup"><span data-stu-id="c135a-104">Microsoft Cognitive Services is a collection of services that are available to developers to make their applications more intelligent.</span></span> <span data-ttu-id="c135a-105">Die Maschinelles Sehen-API ist ein serverloser Dienst, der Bilder mithilfe von erweiterten Algorithmen verarbeitet und Informationen zu jedem Bild zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="c135a-105">The Computer Vision API is a serverless service that processes images using advanced algorithms and returns information about each image.</span></span> <span data-ttu-id="c135a-106">Sie verfügt über einen kostenlosen Tarif, in dem bis zu 5.000 API-Aufrufe pro Monat möglich sind.</span><span class="sxs-lookup"><span data-stu-id="c135a-106">It has a free tier that provides up to 5,000 API calls per month.</span></span>

1. <span data-ttu-id="c135a-107">Stellen Sie sicher, dass Sie noch in Cloud Shell angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="c135a-107">Ensure you're still signed into Cloud Shell.</span></span> <span data-ttu-id="c135a-108">Klicken Sie andernfalls auf die Option **Enter focus mode** (Fokusmodus aktivieren), um ein Cloud Shell-Fenster zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="c135a-108">If you aren't, select **Enter focus mode** to open a Cloud Shell window.</span></span> 

1. <span data-ttu-id="c135a-109">Erstellen Sie in Ihrer Ressourcengruppe ein neues Cognitive Services-Konto vom Typ **ComputerVision** mit einem eindeutigen Namen.</span><span class="sxs-lookup"><span data-stu-id="c135a-109">Create a new Cognitive Services account of type **ComputerVision** with a unique name in your resource group.</span></span> <span data-ttu-id="c135a-110">Verwenden Sie für den kostenlosen Tarif **F0** als SKU.</span><span class="sxs-lookup"><span data-stu-id="c135a-110">For the free tier, use **F0** as the SKU.</span></span> <span data-ttu-id="c135a-111">Falls Sie bereits über ein vorhandenes Konto vom Typ „Maschinelles Sehen“ verfügen, müssen Sie ggf. ein Standard-Konto (S1) erstellen. Hierfür können jedoch Kosten anfallen.</span><span class="sxs-lookup"><span data-stu-id="c135a-111">If you already have an existing Computer Vision account, you may need to create a Standard account (S1), which may incur some costs.</span></span>

    ```azurecli
    az cognitiveservices account create -g first-serverless-app -n <computer vision account name> --kind ComputerVision --sku F0 -l westcentralus
    ```


## <a name="create-function-app-settings-for-computer-vision-url-and-key"></a><span data-ttu-id="c135a-112">Erstellen von Funktions-App-Einstellungen für die Maschinelles Sehen-API und den Schlüssel</span><span class="sxs-lookup"><span data-stu-id="c135a-112">Create function app settings for Computer Vision URL and key</span></span>

<span data-ttu-id="c135a-113">Sie benötigen eine URL und einen Schlüssel, um die Maschinelles Sehen-API aufrufen zu können.</span><span class="sxs-lookup"><span data-stu-id="c135a-113">To call the Computer Vision API, a URL and key are required.</span></span>

1. <span data-ttu-id="c135a-114">Rufen Sie den Schlüssel und die URL für die Maschinelles Sehen-API ab, und speichern Sie diese Angaben in Bash-Variablen.</span><span class="sxs-lookup"><span data-stu-id="c135a-114">Get the Computer Vision API key and URL and save them in Bash variables.</span></span>

    ```azurecli
    export COMP_VISION_KEY=$(az cognitiveservices account keys list -g first-serverless-app -n <computer vision account name> --query key1 --output tsv)
    ```
    ```azurecli
    export COMP_VISION_URL=$(az cognitiveservices account show -g first-serverless-app -n <computer vision account name> --query endpoint --output tsv)
    ```

1. <span data-ttu-id="c135a-115">Erstellen Sie in der Funktions-App App-Einstellungen mit den Namen **COMP_VISION_KEY** und **COMP_VISION_URL**.</span><span class="sxs-lookup"><span data-stu-id="c135a-115">Create app settings named **COMP_VISION_KEY** and **COMP_VISION_URL**, respectively, in the function app.</span></span>

    ```azurecli
    az functionapp config appsettings set -n <function app name> -g first-serverless-app --settings COMP_VISION_KEY=$COMP_VISION_KEY COMP_VISION_URL=$COMP_VISION_URL -o table
    ```

## <a name="call-the-computer-vision-api-from-the-resizeimage-function"></a><span data-ttu-id="c135a-116">Aufrufen der Maschinelles Sehen-API über die ResizeImage-Funktion</span><span class="sxs-lookup"><span data-stu-id="c135a-116">Call the Computer Vision API from the ResizeImage function</span></span>

<span data-ttu-id="c135a-117">Wenn Sie die folgenden Schritte ausführen, ändern Sie die **ResizeImage**-Funktion, um die Maschinelles Sehen-API aufzurufen, um hochgeladene Bilder zu beschreiben und die Beschreibung in Azure Cosmos DB zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c135a-117">In the following steps, you modify the **ResizeImage** function to call the Computer Vision API to describe each uploaded image and save the description in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="c135a-118">Öffnen Sie Ihre Funktions-App im [Azure-Portal](https://portal.azure.com/?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="c135a-118">Open your function app in the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

<span data-ttu-id="c135a-119">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="c135a-119">::: zone pivot="csharp"</span></span>
1. <span data-ttu-id="c135a-120">(C#) Verwenden Sie den Navigationsbereich auf der linken Seite, um nach der Funktion **ResizeImage** zu suchen und das zugehörige Codefenster zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="c135a-120">(C#) Using the left navigation, locate the **ResizeImage** function and open its code window.</span></span>

1. <span data-ttu-id="c135a-121">(C#) Ersetzen Sie den Code durch den Inhalt der Datei [**/csharp/ResizeImage/run-module5.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run-module5.csx).</span><span class="sxs-lookup"><span data-stu-id="c135a-121">(C#) Replace the code with the contents of the [**/csharp/ResizeImage/run-module5.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run-module5.csx) file.</span></span> <span data-ttu-id="c135a-122">In diesem Code wird `HttpClient` verwendet, um die Maschinelles Sehen-API aufzurufen und das Ergebnis in Azure Cosmos DB zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c135a-122">This code uses `HttpClient` to call the Computer Vision API and save its result in Azure Cosmos DB.</span></span>

<span data-ttu-id="c135a-123">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="c135a-123">::: zone-end</span></span>

<span data-ttu-id="c135a-124">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="c135a-124">::: zone pivot="javascript"</span></span>
1. <span data-ttu-id="c135a-125">(JavaScript) Für diese Funktion wird das `axios`-Paket aus npm benötigt, um einen HTTP-Aufruf an die Maschinelles Sehen-API zu senden.</span><span class="sxs-lookup"><span data-stu-id="c135a-125">(JavaScript) This function requires the `axios` package from npm to make an HTTP call to the Computer Vision API.</span></span> <span data-ttu-id="c135a-126">Klicken Sie zum Installieren des npm-Pakets im linken Navigationsbereich erst auf den Namen der Funktions-App und dann auf **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="c135a-126">To install the npm package, click on the function app name on the left navigation and click **Platform features**.</span></span>

1. <span data-ttu-id="c135a-127">(JavaScript) Klicken Sie auf **Konsole**, um ein Konsolenfenster anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c135a-127">(JavaScript) Click **Console** to reveal a console window.</span></span>

1. <span data-ttu-id="c135a-128">(JavaScript) Führen Sie den Befehl `npm install axios` in der Konsole aus.</span><span class="sxs-lookup"><span data-stu-id="c135a-128">(JavaScript) Run the command `npm install axios` in the console.</span></span> <span data-ttu-id="c135a-129">Es kann einige Minuten dauern, bis der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="c135a-129">It may take a few minutes to complete the operation.</span></span>

1. <span data-ttu-id="c135a-130">(JavaScript) Klicken Sie im Navigationsbereich auf der linken Seite auf den Funktionsnamen (**ResizeImage**), um die Funktion anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c135a-130">(JavaScript) Click on the function name (**ResizeImage**) in the left navigation to reveal the function.</span></span> <span data-ttu-id="c135a-131">Ersetzen Sie den Inhalt der **index.js**-Datei durch den Inhalt der Datei [**/javascript/ResizeImage/index-module5.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index-module5.js).</span><span class="sxs-lookup"><span data-stu-id="c135a-131">Replace all of the **index.js** file with the contents of the [**/javascript/ResizeImage/index-module5.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index-module5.js) file.</span></span>

<span data-ttu-id="c135a-132">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="c135a-132">::: zone-end</span></span>

1. <span data-ttu-id="c135a-133">Klicken Sie unter dem Codefenster auf **Protokolle**, um den Protokollbereich zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="c135a-133">Click **Logs** below the code window to expand the Logs panel.</span></span>

1. <span data-ttu-id="c135a-134">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c135a-134">Click **Save**.</span></span> <span data-ttu-id="c135a-135">Überprüfen Sie den Protokollbereich, um sicherzustellen, dass die Funktion erfolgreich gespeichert wird und keine Fehler aufgetreten sind.</span><span class="sxs-lookup"><span data-stu-id="c135a-135">Check the Logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="test-the-application"></a><span data-ttu-id="c135a-136">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="c135a-136">Test the application</span></span>

1. <span data-ttu-id="c135a-137">Öffnen Sie die Anwendung in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="c135a-137">Open the application in a browser.</span></span> 

1. <span data-ttu-id="c135a-138">Wählen Sie eine Bilddatei aus, und laden Sie sie hoch.</span><span class="sxs-lookup"><span data-stu-id="c135a-138">Select an image file and upload it.</span></span>

1. <span data-ttu-id="c135a-139">Nach einigen Sekunden sollte die Miniaturansicht des neuen Bilds auf der Seite angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c135a-139">After a few seconds, the thumbnail of the new image should appear on the page.</span></span> <span data-ttu-id="c135a-140">Zeigen Sie auf das Bild, um die von der Maschinelles Sehen-API generierte Beschreibung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c135a-140">Point to the image to see the description that's generated by Computer Vision.</span></span>

## <a name="summary"></a><span data-ttu-id="c135a-141">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c135a-141">Summary</span></span>

<span data-ttu-id="c135a-142">In dieser Einheit haben Sie erfahren, wie Sie mithilfe der Maschinelles Sehen-API von Microsoft Cognitive Services die automatische Generierung von Bildtiteln für hochgeladene Bilder verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c135a-142">In this unit, you learned how to automatically generate captions for each uploaded image using Microsoft Cognitive Services Computer Vision API.</span></span> <span data-ttu-id="c135a-143">Als Nächstes wird beschrieben, wie Sie der Anwendung mithilfe der Azure App Service-Authentifizierung eine Authentifizierung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c135a-143">Next, you learn how to add authentication to the application using Azure App Service authentication.</span></span>