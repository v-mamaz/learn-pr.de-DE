<span data-ttu-id="245b4-101">In diesem Modul können Sie eine einfache Webanwendung bereitstellen, in dem eine HTML-basierte Benutzeroberfläche dargestellt.</span><span class="sxs-lookup"><span data-stu-id="245b4-101">In this module, you will deploy a simple web application that presents an HTML-based user interface.</span></span> <span data-ttu-id="245b4-102">Ein serverloses Back-End kann es sich um die Anwendung zum Hochladen von Bildern und erhalten automatisch Untertitel Beschreibung.</span><span class="sxs-lookup"><span data-stu-id="245b4-102">A serverless backend enables the application to upload images and automatically get captions describing them.</span></span>

![Ausgeführte Web-app](../images/0-app-screenshot-finished.png)

<span data-ttu-id="245b4-104">Das folgende Diagramm zeigt die Azure-Dienste, die von der Anwendung verwendet:</span><span class="sxs-lookup"><span data-stu-id="245b4-104">The following diagram shows the Azure services used by the application:</span></span>

1. <span data-ttu-id="245b4-105">BLOB Storage dient die statische Webinhalte (HTML, CSS und JS) und speichert Bilder.</span><span class="sxs-lookup"><span data-stu-id="245b4-105">Blob Storage serves static web content (HTML, CSS, JS) and stores images.</span></span>
2. <span data-ttu-id="245b4-106">Azure Functions verwaltet Bilduploads, Ändern der Größe und Speicher für Metadaten.</span><span class="sxs-lookup"><span data-stu-id="245b4-106">Azure Functions manages image uploads, resizing, and metadata storage.</span></span>
3. <span data-ttu-id="245b4-107">COSMOS DB speichert Metadaten zu Bildern.</span><span class="sxs-lookup"><span data-stu-id="245b4-107">Cosmos DB stores image metadata.</span></span>
4. <span data-ttu-id="245b4-108">Logik-Apps ruft Image Beschriftungen aus Computer Vision-API ab.</span><span class="sxs-lookup"><span data-stu-id="245b4-108">Logic Apps gets image captions from Computer Vision API.</span></span>
5. <span data-ttu-id="245b4-109">Azure Active Directory verwaltet die Benutzerauthentifizierung.</span><span class="sxs-lookup"><span data-stu-id="245b4-109">Azure Active Directory manages user authentication.</span></span>

![Diagramm der Lösungsarchitektur](../images/0-architecture.jpg)

<span data-ttu-id="245b4-111">In dieser Einheit, erfahren Sie, wie Sie:</span><span class="sxs-lookup"><span data-stu-id="245b4-111">In this unit, you will learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="245b4-112">Konfigurieren Sie Azure Blob Storage zum Hosten einer statischen Website und hochgeladene Bilder.</span><span class="sxs-lookup"><span data-stu-id="245b4-112">Configure Azure Blob storage to host a static website and uploaded images.</span></span>
> * <span data-ttu-id="245b4-113">Hochladen von Bildern in Azure Blob Storage mit Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="245b4-113">Upload images to Azure Blob storage using Azure Functions.</span></span>
> * <span data-ttu-id="245b4-114">Ändern der Bildgröße mithilfe von Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="245b4-114">Resize images using Azure Functions.</span></span>
> * <span data-ttu-id="245b4-115">Store Bildmetadaten in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="245b4-115">Store image metadata in Azure Cosmos DB.</span></span>
> * <span data-ttu-id="245b4-116">Verwenden Sie Cognitive Services-maschinelles sehen-API, um das Image Untertitel automatisch generieren.</span><span class="sxs-lookup"><span data-stu-id="245b4-116">Use Cognitive Services Vision API to auto-generate image captions.</span></span>
> * <span data-ttu-id="245b4-117">Verwenden Sie Azure Active Directory, um die Web-app zu sichern, indem Sie die Authentifizierung von Benutzern.</span><span class="sxs-lookup"><span data-stu-id="245b4-117">Use Azure Active Directory to secure the web app by authenticating users.</span></span>

<span data-ttu-id="245b4-118">Azure Blob Storage ist ein kostengünstig und hochgradig skalierbaren Dienst, der zum Hosten von statischer Dateien verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="245b4-118">Azure Blob storage is a low-cost and massively scalable service that can be used to host static files.</span></span> <span data-ttu-id="245b4-119">In diesem Tutorial verwenden Sie diese zum Verarbeiten von statischem Inhalt (z. B. HTML, JavaScript, CSS) für die Web-app, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="245b4-119">For this tutorial, you use it to serve static content (for example, HTML, JavaScript, CSS) for the web app that you build.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="245b4-120">Erstellen eines Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="245b4-120">Create a Storage account</span></span>

<span data-ttu-id="245b4-121">Ein Speicherkonto ist eine Azure-Ressource, die Ihnen ermöglicht, Tabellen, Warteschlangen, Dateien, Blobs (Objekte) und VM-Datenträger zu speichern.</span><span class="sxs-lookup"><span data-stu-id="245b4-121">A Storage account is an Azure resource that allows you to store tables, queues, files, blobs (objects), and virtual machine disks.</span></span>

1. <span data-ttu-id="245b4-122">Melden Sie sich der Cloud Shell (Bash), durch Auswählen der **EINGABETASTE fokusmodus** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="245b4-122">Log in to the Cloud Shell (Bash), by selecting the **Enter focus mode** button.</span></span> <span data-ttu-id="245b4-123">Diese Schaltfläche ist auf der rechten oberen Ecke oder den unteren Rand der Seite, je nachdem, wie breit Ihres Browserfensters ist.</span><span class="sxs-lookup"><span data-stu-id="245b4-123">This button is at the top right or the bottom of the page, depending on how wide your browser window is.</span></span> <span data-ttu-id="245b4-124">Fokusmodus Dockt eine Cloud Shell-Fensters auf der rechten Seite im Browserfenster, an, damit Sie problemlos Befehle ausführen können, die in diesem Tutorial gezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="245b4-124">Focus mode docks a Cloud Shell window on the right side of your browser window, so you can easily execute commands that are shown in the tutorial.</span></span>

1. <span data-ttu-id="245b4-125">In Azure ist eine Ressourcengruppe ein Container, der verwandte Azure-Ressourcen zur besseren Verwaltung enthält.</span><span class="sxs-lookup"><span data-stu-id="245b4-125">In Azure, a Resource Group is a container that holds related Azure resources for ease of management.</span></span> <span data-ttu-id="245b4-126">Erstellen Sie eine neue Ressourcengruppe mit dem Namen **ersten serverlosen app**.</span><span class="sxs-lookup"><span data-stu-id="245b4-126">Create a new resource group named **first-serverless-app**.</span></span>

    ```azurecli
    az group create -n first-serverless-app -l westcentralus
    ```

1. <span data-ttu-id="245b4-127">Der statische Inhalt (HTML, CSS und JavaScript-Dateien) für dieses Tutorial wird in Blob Storage gehostet.</span><span class="sxs-lookup"><span data-stu-id="245b4-127">The static content (HTML, CSS, and JavaScript files) for this tutorial is hosted in Blob Storage.</span></span> <span data-ttu-id="245b4-128">BLOB-Speicher ist ein Speicherkonto erforderlich.</span><span class="sxs-lookup"><span data-stu-id="245b4-128">Blob Storage requires a Storage account.</span></span> <span data-ttu-id="245b4-129">Erstellen Sie ein Speicherkonto (universell V2) in der Ressourcengruppe ein.</span><span class="sxs-lookup"><span data-stu-id="245b4-129">Create a Storage account (general purpose V2) in the resource group.</span></span> <span data-ttu-id="245b4-130">Ersetzen Sie dies `<storage account name>` durch einen eindeutigen Namen.</span><span class="sxs-lookup"><span data-stu-id="245b4-130">Replace `<storage account name>` with a unique name.</span></span>

    ```azurecli
    az storage account create -n <storage account name> -g first-serverless-app --kind StorageV2 -l westcentralus --https-only true --sku Standard_LRS
    ```

1. <span data-ttu-id="245b4-131">Über die Suchleiste am oberen Rand der [Azure-Portal](https://portal.azure.com), suchen Sie das Speicherkonto, das Sie gerade erstellt haben, und öffnen Sie sie.</span><span class="sxs-lookup"><span data-stu-id="245b4-131">Using the Search bar at the top of the [Azure portal](https://portal.azure.com), find the storage account you just created and open it.</span></span>

1. <span data-ttu-id="245b4-132">Wählen Sie auf der linken Navigationsleiste **statische Website (Vorschau)** einen Container für das Hosten statischer Websites konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="245b4-132">On the left navigation, select **Static website (preview)** to configure a container for static website hosting.</span></span>
    - <span data-ttu-id="245b4-133">Wählen Sie **aktiviert** statische Website zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="245b4-133">Select **Enabled** to enable static website.</span></span>
    - <span data-ttu-id="245b4-134">Geben Sie *"Index.HTML"* als der Name des indexdokuments.</span><span class="sxs-lookup"><span data-stu-id="245b4-134">Enter *index.html* as the index document name.</span></span> <span data-ttu-id="245b4-135">Das Feld bereits hat *"Index.HTML"* in einer grauen Schriftart aber nur Beispieltext, müssen diesen Wert in das Feld eingeben.</span><span class="sxs-lookup"><span data-stu-id="245b4-135">The field already has *index.html* in a gray font but this is only example text; you still have to enter that value in the field.</span></span>
    - <span data-ttu-id="245b4-136">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="245b4-136">Click **Save**.</span></span>
    
    ![Geben Sie die Einstellungen für statische website](../images/1-storage-static-website.png)

1. <span data-ttu-id="245b4-138">Speichern Sie die **primären Endpunkt** an einer beliebigen Stelle Sie können bequem kopieren aus beim Durcharbeiten des Tutorials.</span><span class="sxs-lookup"><span data-stu-id="245b4-138">Save the **Primary Endpoint** somewhere you can conveniently copy it from while working through the tutorial.</span></span> <span data-ttu-id="245b4-139">Dies ist die URL der Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="245b4-139">This is the URL of your web application.</span></span>

## <a name="upload-the-web-application"></a><span data-ttu-id="245b4-140">Laden Sie die Webanwendung hoch.</span><span class="sxs-lookup"><span data-stu-id="245b4-140">Upload the web application</span></span>

1. <span data-ttu-id="245b4-141">Die Quelldateien für die Anwendung, die Sie in diesem Tutorial erstellen befinden sich in einem [GitHub-Repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span><span class="sxs-lookup"><span data-stu-id="245b4-141">The source files for the application that you build in this tutorial are located in a [GitHub repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span></span> <span data-ttu-id="245b4-142">Stellen Sie sicher, dass Sie in Ihrem Basisverzeichnis in Cloud Shell und dieses Repository klonen.</span><span class="sxs-lookup"><span data-stu-id="245b4-142">Make sure that you are in your home directory in Cloud Shell and clone this repository.</span></span>

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    <span data-ttu-id="245b4-143">Das Repository geklont `/home/<username>/functions-first-serverless-web-application`.</span><span class="sxs-lookup"><span data-stu-id="245b4-143">The repository is cloned to `/home/<username>/functions-first-serverless-web-application`.</span></span>

1. <span data-ttu-id="245b4-144">Die Client-Side-Web-Anwendung befindet sich in der **Www** Ordner und mit dem Vue.js JavaScript-Framework basiert.</span><span class="sxs-lookup"><span data-stu-id="245b4-144">The client-side web application is located in the **www** folder and is built using the Vue.js JavaScript framework.</span></span> <span data-ttu-id="245b4-145">Ändern Sie in den Ordner, und führen Sie Npm-Befehle zum Installieren der Anwendung Abhängigkeiten und Erstellen der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="245b4-145">Change into the folder and run npm commands to install the application's dependencies and build the application.</span></span> <span data-ttu-id="245b4-146">Die letzte von diesen Befehlen dauert mehrere Minuten in Anspruch.</span><span class="sxs-lookup"><span data-stu-id="245b4-146">The last of these commands might take several minutes to complete.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www
    npm install
    npm run generate
    ```

    <span data-ttu-id="245b4-147">Die Anwendung wird generiert, der **Dist** Ordner.</span><span class="sxs-lookup"><span data-stu-id="245b4-147">The application is generated in the **dist** folder.</span></span>

1. <span data-ttu-id="245b4-148">Wechseln Sie zum aktuelle Verzeichnis **Dist** und die Anwendung zum Hochladen der **$web** Blob-Container.</span><span class="sxs-lookup"><span data-stu-id="245b4-148">Change the current directory to **dist** and upload the application to the **$web** Blob container.</span></span>

    ```azurecli
    cd dist
    az storage blob upload-batch -s . -d \$web --account-name <storage account name>
    ```

1. <span data-ttu-id="245b4-149">Öffnen Sie die Speicher statische Websites primären Endpunkt-URL in einem Webbrowser, um die Anwendung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="245b4-149">Open the Storage static websites primary endpoint URL in a web browser to view the application.</span></span>

    ![Erste serverlose Web-app-Startseite](../images/1-app-screenshot-new.png)


## <a name="summary"></a><span data-ttu-id="245b4-151">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="245b4-151">Summary</span></span>

<span data-ttu-id="245b4-152">In dieser Einheit, die Sie erstellt einer Ressourcengruppe namens **ersten serverlosen app** , enthält ein Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="245b4-152">In this unit, you created a resource group named **first-serverless-app** containing a Storage account.</span></span> <span data-ttu-id="245b4-153">Ein blobcontainer namens **$web** in Storage-Konto speichert die statische Inhalte für Ihre Webanwendung und stellt den Inhalt öffentlich zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="245b4-153">A blob container named **$web** in the Storage account stores the static content for your web application and makes the content available publicly.</span></span> <span data-ttu-id="245b4-154">Als Nächstes erfahren Sie, wie Sie mit einer serverlosen Funktion zum Hochladen von Bildern in Blob Storage von der Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="245b4-154">Next, you learn how to use a serverless function to upload images to Blob storage from this web application.</span></span>