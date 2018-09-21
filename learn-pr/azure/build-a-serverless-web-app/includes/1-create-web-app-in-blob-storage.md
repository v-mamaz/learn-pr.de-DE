<span data-ttu-id="c926c-101">Im Rahmen dieses Moduls stellen Sie eine einfache Web-App bereit, die über eine HTML-basierte Benutzeroberfläche verfügt.</span><span class="sxs-lookup"><span data-stu-id="c926c-101">In this module, you will deploy a simple web application that presents an HTML-based user interface.</span></span> <span data-ttu-id="c926c-102">Mit einem serverlosen Back-End kann die Anwendung Bilder hochladen und automatisch beschreibende Bildtitel generieren.</span><span class="sxs-lookup"><span data-stu-id="c926c-102">A serverless back end enables the application to upload images and automatically generate descriptive captions.</span></span>

![Ausführen der Web-App](../media/0-app-screenshot-finished.png)

<span data-ttu-id="c926c-104">Im folgenden Diagramm sind die Azure-Dienste aufgeführt, die von der Anwendung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c926c-104">The following illustration shows the Azure services that are used by the application.</span></span>

![<span data-ttu-id="c926c-105">Die Abbildung zeigt, wie verschiedene Azure-Dienste wie Azure Blob Storage, Azure Functions, Cosmos DB, Azure Logic Apps und Azure Active Directory von der Anwendung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c926c-105">An illustration showing how different Azure services such as, Azure Blob storage, Azure functions, Cosmos DB, Azure logic apps, and Azure active directory are used by the application.</span></span> ](../media/0-architecture.jpg)

1. <span data-ttu-id="c926c-106">Azure Blob Storage stellt statischen Webinhalt (HTML, CSS, JS) bereit und speichert Bilder.</span><span class="sxs-lookup"><span data-stu-id="c926c-106">Azure Blob storage serves static web content (HTML, CSS, JS) and stores images.</span></span>
2. <span data-ttu-id="c926c-107">Azure Functions verwaltet das Hochladen von Bildern, die Größenänderung und die Speicherung von Metadaten.</span><span class="sxs-lookup"><span data-stu-id="c926c-107">Azure Functions manages image uploads, resizing, and metadata storage.</span></span>
3. <span data-ttu-id="c926c-108">Azure Cosmos DB speichert Bildmetadaten.</span><span class="sxs-lookup"><span data-stu-id="c926c-108">Azure Cosmos DB stores image metadata.</span></span>
4. <span data-ttu-id="c926c-109">Azure Logic Apps ruft Bildtitel von der Maschinelles Sehen-API von Cognitive Services ab.</span><span class="sxs-lookup"><span data-stu-id="c926c-109">Azure Logic Apps retrieves image captions from the Cognitive Services Computer Vision API.</span></span>
5. <span data-ttu-id="c926c-110">Azure Active Directory wird zum Verwalten der Benutzerauthentifizierung verwendet.</span><span class="sxs-lookup"><span data-stu-id="c926c-110">Azure Active Directory manages user authentication.</span></span>

<span data-ttu-id="c926c-111">Azure Blob Storage ist ein kostengünstiger und extrem skalierbarer Dienst, der zum Hosten von statischen Dateien verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="c926c-111">Azure Blob storage is a low-cost and massively scalable service that can be used to host static files.</span></span> <span data-ttu-id="c926c-112">In diesem Modul verwenden Sie Blob Storage, um statische Inhalte (z.B. HTML, JavaScript oder CSS) für die Web-App bereitzustellen, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="c926c-112">In this module, you will use Blob storage to serve static content (for example, HTML, JavaScript, or CSS) for a web app you build.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="c926c-113">Erstellen eines Azure-Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="c926c-113">Create an Azure Storage account</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="c926c-114">Ein Azure Storage-Konto ist eine Azure-Ressource, mit der Sie Tabellen, Warteschlangen, Dateien, Blobs (Objekte) und VM-Datenträger speichern können.</span><span class="sxs-lookup"><span data-stu-id="c926c-114">An Azure Storage account is an Azure resource that allows you to store tables, queues, files, blobs (objects), and virtual machine disks.</span></span>

1. <span data-ttu-id="c926c-115">Der statische Inhalt (HTML-, CSS- und JavaScript-Dateien) für dieses Modul wird in Blob Storage gehostet.</span><span class="sxs-lookup"><span data-stu-id="c926c-115">The static content (HTML, CSS, and JavaScript files) for this module is hosted in Blob storage.</span></span> <span data-ttu-id="c926c-116">Für Blob Storage ist ein Speicherkonto erforderlich.</span><span class="sxs-lookup"><span data-stu-id="c926c-116">Blob storage requires a Storage account.</span></span> <span data-ttu-id="c926c-117">Erstellen Sie ein Speicherkonto vom Typ „General-purpose v2“(GPv2) in der Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="c926c-117">Create a general-purpose v2 (GPv2) Storage account in the resource group.</span></span> <span data-ttu-id="c926c-118">Ersetzen Sie `<storage account name>` durch einen eindeutigen Namen.</span><span class="sxs-lookup"><span data-stu-id="c926c-118">Replace `<storage account name>` with a unique name.</span></span>

    ```azurecli
    az storage account create \
        -n <storage account name> \
        -g <rgn>[Sandbox resource group name]</rgn> \
        --kind StorageV2 \
        --https-only true \
        --sku Standard_LRS
    ```
    
1. <span data-ttu-id="c926c-119">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="c926c-119">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="c926c-120">Verwenden Sie die Suchleiste oben im Portal, um das Speicherkonto zu finden, das Sie eben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c926c-120">Use the Search bar at the top of the portal to find the storage account that you just created.</span></span> <span data-ttu-id="c926c-121">Öffnen Sie das Konto.</span><span class="sxs-lookup"><span data-stu-id="c926c-121">Open the account.</span></span>

1. <span data-ttu-id="c926c-122">Klicken Sie im linken Navigationsbereich auf **Statische Website (Vorschau)**, um einen Container für das Hosten von statischen Websites zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="c926c-122">On the left navigation, select **Static website (preview)** to configure a container for static website hosting.</span></span>
    - <span data-ttu-id="c926c-123">Klicken Sie auf **Aktiviert**, um eine statische Website zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="c926c-123">Select **Enabled** to enable a static website.</span></span>
    - <span data-ttu-id="c926c-124">Geben Sie **index.html** als Name des Indexdokuments ein.</span><span class="sxs-lookup"><span data-stu-id="c926c-124">Enter **index.html** as the index document name.</span></span> <span data-ttu-id="c926c-125">Im Feld steht *index.html* bereits in grauer Schrift, jedoch ist dies nur ein Beispieltext.</span><span class="sxs-lookup"><span data-stu-id="c926c-125">The box already has *index.html* in a gray font, but this is only example text.</span></span> <span data-ttu-id="c926c-126">Sie müssen trotzdem **index.html** in das Feld eingeben.</span><span class="sxs-lookup"><span data-stu-id="c926c-126">You still have to enter **index.html** in the box.</span></span>
    - <span data-ttu-id="c926c-127">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c926c-127">Click **Save**.</span></span>
    
    ![Eingeben der Einstellungen für die statische Website](../media/1-storage-static-website.png)

1. <span data-ttu-id="c926c-129">Speichern Sie den **primären Endpunkt** an einem Ort, an dem Sie ihn beim Durcharbeiten des Moduls bequem kopieren können.</span><span class="sxs-lookup"><span data-stu-id="c926c-129">Save the **Primary Endpoint** in a place where you can conveniently copy it from while working through the module.</span></span> <span data-ttu-id="c926c-130">Dieser Endpunkt ist die URL Ihrer Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="c926c-130">This endpoint is the URL of your web application.</span></span>

## <a name="upload-the-web-application"></a><span data-ttu-id="c926c-131">Hochladen der Webanwendung</span><span class="sxs-lookup"><span data-stu-id="c926c-131">Upload the web application</span></span>

1. <span data-ttu-id="c926c-132">Die Quelldateien für die Anwendung, die Sie in diesem Modul erstellen, befinden sich in einem [GitHub-Repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span><span class="sxs-lookup"><span data-stu-id="c926c-132">The source files for the application that you build in this module are located in a [GitHub repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span></span> <span data-ttu-id="c926c-133">Navigieren Sie in Cloud Shell zu Ihrem Basisverzeichnis, und klonen Sie dieses Repository.</span><span class="sxs-lookup"><span data-stu-id="c926c-133">Go to your home directory in Cloud Shell and clone this repository.</span></span>

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    <span data-ttu-id="c926c-134">Das Repository wird in `/home/<username>/functions-first-serverless-web-application` geklont.</span><span class="sxs-lookup"><span data-stu-id="c926c-134">The repository is cloned to `/home/<username>/functions-first-serverless-web-application`</span></span>

1. <span data-ttu-id="c926c-135">Die clientseitige Webanwendung befindet sich im Ordner **www** und wird mit dem JavaScript-Framework „Vue.js“ erstellt.</span><span class="sxs-lookup"><span data-stu-id="c926c-135">The client-side web application is located in the **www** folder and is built using the Vue.js JavaScript framework.</span></span> <span data-ttu-id="c926c-136">Öffnen Sie den Ordner **www**, und führen Sie **npm**-Befehle aus, um die Anwendungsabhängigkeiten zu installieren und die Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c926c-136">Open the **www** folder and run **npm** commands to install the application dependencies and build the application.</span></span> <span data-ttu-id="c926c-137">Es kann mehrere Minuten dauern, bis der letzte dieser Befehle abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="c926c-137">The last of these commands might take several minutes to complete.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www
    npm install
    npm run generate
    ```

    <span data-ttu-id="c926c-138">Die Anwendung wird im Ordner **dist** generiert.</span><span class="sxs-lookup"><span data-stu-id="c926c-138">The application is generated in the **dist** folder.</span></span>

1. <span data-ttu-id="c926c-139">Legen Sie den **dist**-Ordner als das aktuelle Verzeichnis fest, und laden Sie die Anwendung in den Blobcontainer **$web** hoch.</span><span class="sxs-lookup"><span data-stu-id="c926c-139">Change the current directory to the **dist** folder and upload the application to the **$web** blob container.</span></span>

    ```azurecli
    cd dist
    az storage blob upload-batch -s . -d \$web --account-name <storage account name>
    ```

1. <span data-ttu-id="c926c-140">Öffnen Sie die URL des primären Endpunkts der statischen Websites in einem Webbrowser, um die Anwendung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c926c-140">To view the application, open the static website’s primary endpoint URL in a web browser.</span></span>

    ![Startseite der ersten serverlosen Web-App](../media/1-app-screenshot-new.png)


## <a name="summary"></a><span data-ttu-id="c926c-142">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c926c-142">Summary</span></span>

<span data-ttu-id="c926c-143">In dieser Lektion haben Sie ein Speicherkonto erstellt.</span><span class="sxs-lookup"><span data-stu-id="c926c-143">In this unit, you created a storage account.</span></span> <span data-ttu-id="c926c-144">Der statische Inhalt für Ihre Webanwendung wird in einem Blobcontainer namens **$web** im Speicherkonto gespeichert, und der Inhalt wird öffentlich zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="c926c-144">A blob container named **$web** in the storage account stores the static content for your web application and makes the content publicly available.</span></span> <span data-ttu-id="c926c-145">Als Nächstes erfahren Sie, wie Sie eine serverlose Funktion zum Hochladen von Bildern in Blob Storage aus dieser Webanwendung verwenden.</span><span class="sxs-lookup"><span data-stu-id="c926c-145">Next, you will learn how to use a serverless function to upload images to Blob storage from this web application.</span></span>