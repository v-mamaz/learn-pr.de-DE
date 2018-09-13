<span data-ttu-id="10d30-101">Im Rahmen dieses Moduls stellen Sie eine einfache Web-App bereit, die eine HTML-basierte Benutzeroberfläche darstellt.</span><span class="sxs-lookup"><span data-stu-id="10d30-101">In this module, you will deploy a simple web application that presents an HTML-based user interface.</span></span> <span data-ttu-id="10d30-102">Mit einem serverlosen Back-End kann die Anwendung Bilder hochladen und automatisch Bildtitel abrufen, die diese beschreiben.</span><span class="sxs-lookup"><span data-stu-id="10d30-102">A serverless back end enables the application to upload images and automatically get captions that describe them.</span></span>

![Ausführen der Web-App](../media/0-app-screenshot-finished.png)

<span data-ttu-id="10d30-104">Im folgenden Diagramm sind die Azure-Dienste aufgeführt, die von der Anwendung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="10d30-104">The following diagram shows the Azure services that are used by the application.</span></span>

1. <span data-ttu-id="10d30-105">Azure Blob Storage stellt statischen Webinhalt (HTML, CSS, JS) bereit und speichert Bilder.</span><span class="sxs-lookup"><span data-stu-id="10d30-105">Azure Blob storage serves static web content (HTML, CSS, JS) and stores images.</span></span>
2. <span data-ttu-id="10d30-106">Azure Functions verwaltet das Hochladen von Bildern, die Größenänderung und die Speicherung von Metadaten.</span><span class="sxs-lookup"><span data-stu-id="10d30-106">Azure Functions manages image uploads, resizing, and metadata storage.</span></span>
3. <span data-ttu-id="10d30-107">Azure Cosmos DB speichert Bildmetadaten.</span><span class="sxs-lookup"><span data-stu-id="10d30-107">Azure Cosmos DB stores image metadata.</span></span>
4. <span data-ttu-id="10d30-108">Azure Logic Apps ruft Bildtitel von der Maschinelles Sehen-API von Cognitive Services ab.</span><span class="sxs-lookup"><span data-stu-id="10d30-108">Azure Logic Apps gets image captions from the Cognitive Services Computer Vision API.</span></span>
5. <span data-ttu-id="10d30-109">Azure Active Directory wird zum Verwalten der Benutzerauthentifizierung verwendet.</span><span class="sxs-lookup"><span data-stu-id="10d30-109">Azure Active Directory manages user authentication.</span></span>

![Diagramm der Lösungsarchitektur](../media/0-architecture.jpg)

<span data-ttu-id="10d30-111">In dieser Einheit lernen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="10d30-111">In this unit, you will learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="10d30-112">Konfigurieren von Azure Blob Storage zum Hosten einer statischen Website und von hochgeladenen Bildern</span><span class="sxs-lookup"><span data-stu-id="10d30-112">Configure Azure Blob storage to host a static website and uploaded images.</span></span>
> * <span data-ttu-id="10d30-113">Hochladen von Bildern in Azure Blob Storage mit Azure Functions</span><span class="sxs-lookup"><span data-stu-id="10d30-113">Upload images to Azure Blob storage using Azure Functions.</span></span>
> * <span data-ttu-id="10d30-114">Ändern der Größe von Bildern mit Azure Functions</span><span class="sxs-lookup"><span data-stu-id="10d30-114">Resize images using Azure Functions.</span></span>
> * <span data-ttu-id="10d30-115">Speichern von Bildmetadaten in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10d30-115">Store image metadata in Azure Cosmos DB.</span></span>
> * <span data-ttu-id="10d30-116">Verwenden der Maschinelles Sehen-API von Cognitive Services zum automatischen Generieren von Bildtiteln</span><span class="sxs-lookup"><span data-stu-id="10d30-116">Use the Cognitive Services Vision API to auto-generate image captions.</span></span>
> * <span data-ttu-id="10d30-117">Nutzen von Azure Active Directory zum Schützen der Web-App durch das Authentifizieren von Benutzern</span><span class="sxs-lookup"><span data-stu-id="10d30-117">Use Azure Active Directory to secure the web app by authenticating users.</span></span>

<span data-ttu-id="10d30-118">Azure Blob Storage ist ein kostengünstiger und extrem skalierbarer Dienst, der zum Hosten von statischen Dateien verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="10d30-118">Azure Blob storage is a low-cost and massively scalable service that can be used to host static files.</span></span> <span data-ttu-id="10d30-119">Für dieses Tutorial verwenden Sie den Dienst zum Bereitstellen von statischem Inhalt (z.B. HTML, JavaScript, CSS) für die von Ihnen erstellte Web-App.</span><span class="sxs-lookup"><span data-stu-id="10d30-119">For this tutorial, you use it to serve static content (for example, HTML, JavaScript, CSS) for the web app that you build.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="10d30-120">Erstellen eines Azure-Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="10d30-120">Create an Azure Storage account</span></span>

<span data-ttu-id="10d30-121">Ein Azure-Speicherkonto ist eine Azure-Ressource, mit der Sie Tabellen, Warteschlangen, Dateien, Blobs (Objekte) und VM-Datenträger speichern können.</span><span class="sxs-lookup"><span data-stu-id="10d30-121">An Azure Storage account is an Azure resource that allows you to store tables, queues, files, blobs (objects), and virtual machine disks.</span></span>

1. <span data-ttu-id="10d30-122">Klicken Sie auf die Schaltfläche **Enter focus mode** (Fokusmodus starten), um Azure Cloud Shell (Bash) zu starten.</span><span class="sxs-lookup"><span data-stu-id="10d30-122">Select the **Enter focus mode** button to launch Azure Cloud Shell (Bash).</span></span> <span data-ttu-id="10d30-123">Diese Schaltfläche befindet sich oben rechts oder unten auf der Seite. Dies hängt davon ab, wie breit Ihr Browserfenster dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="10d30-123">This button is at the top right or the bottom of the page, depending on how wide your browser window is.</span></span> <span data-ttu-id="10d30-124">Im Fokusmodus wird ein Cloud Shell-Fenster im Browserfenster auf der rechten Seite angedockt, damit Sie im Tutorial angezeigte Befehle leicht ausführen können.</span><span class="sxs-lookup"><span data-stu-id="10d30-124">Focus mode docks a Cloud Shell window on the right side of your browser window, so you can easily execute commands that are shown in the tutorial.</span></span>

1. <span data-ttu-id="10d30-125">In Azure ist eine Ressourcengruppe ein Container, der zusammengehörige Azure-Ressourcen enthält, um die Verwaltung zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="10d30-125">In Azure, a resource group is a container that holds related Azure resources for ease of management.</span></span> <span data-ttu-id="10d30-126">Erstellen Sie eine neue Ressourcengruppe mit dem Namen **first-serverless-app**.</span><span class="sxs-lookup"><span data-stu-id="10d30-126">Create a new resource group named **first-serverless-app**.</span></span>

    ```azurecli
    az group create -n first-serverless-app -l westcentralus
    ```

1. <span data-ttu-id="10d30-127">Der statische Inhalt (HTML-, CSS- und JavaScript-Dateien) für dieses Tutorial wird in Blob Storage gehostet.</span><span class="sxs-lookup"><span data-stu-id="10d30-127">The static content (HTML, CSS, and JavaScript files) for this tutorial is hosted in Blob storage.</span></span> <span data-ttu-id="10d30-128">Für Blob Storage ist ein Speicherkonto erforderlich.</span><span class="sxs-lookup"><span data-stu-id="10d30-128">Blob storage requires a Storage account.</span></span> <span data-ttu-id="10d30-129">Erstellen Sie ein Speicherkonto (Allgemein V2) in der Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="10d30-129">Create a Storage account (general-purpose V2) in the resource group.</span></span> <span data-ttu-id="10d30-130">Ersetzen Sie `<storage account name>` durch einen eindeutigen Namen.</span><span class="sxs-lookup"><span data-stu-id="10d30-130">Replace `<storage account name>` with a unique name.</span></span>

    ```azurecli
    az storage account create -n <storage account name> -g first-serverless-app --kind StorageV2 -l westcentralus --https-only true --sku Standard_LRS
    ```
    
1. <span data-ttu-id="10d30-131">Verwenden Sie die Suchleiste oben im [Azure-Portal](https://portal.azure.com/?azure-portal=true), um das Speicherkonto zu finden, das Sie eben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="10d30-131">Use the Search bar at the top of the [Azure portal](https://portal.azure.com/?azure-portal=true) to find the storage account that you just created.</span></span> <span data-ttu-id="10d30-132">Öffnen Sie das Konto.</span><span class="sxs-lookup"><span data-stu-id="10d30-132">Open the account.</span></span>

1. <span data-ttu-id="10d30-133">Klicken Sie im linken Navigationsbereich auf **Statische Website (Vorschau)**, um einen Container für das Hosten von statischen Websites zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="10d30-133">On the left navigation, select **Static website (preview)** to configure a container for static website hosting.</span></span>
    - <span data-ttu-id="10d30-134">Klicken Sie auf **Aktiviert**, um eine statische Website zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="10d30-134">Select **Enabled** to enable a static website.</span></span>
    - <span data-ttu-id="10d30-135">Geben Sie **index.html** als Name des Indexdokuments ein.</span><span class="sxs-lookup"><span data-stu-id="10d30-135">Enter **index.html** as the index document name.</span></span> <span data-ttu-id="10d30-136">Im Feld steht *index.html* bereits in grauer Schrift, jedoch ist dies nur ein Beispieltext.</span><span class="sxs-lookup"><span data-stu-id="10d30-136">The box already has *index.html* in a gray font, but this is only example text.</span></span> <span data-ttu-id="10d30-137">Sie müssen trotzdem **index.html** in das Feld eingeben.</span><span class="sxs-lookup"><span data-stu-id="10d30-137">You still have to enter **index.html** in the box.</span></span>
    - <span data-ttu-id="10d30-138">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="10d30-138">Click **Save**.</span></span>
    
    ![Eingeben der Einstellungen für die statische Website](../media/1-storage-static-website.png)

1. <span data-ttu-id="10d30-140">Speichern Sie den **primären Endpunkt** an einem Ort, an dem Sie ihn beim Durcharbeiten des Tutorials bequem kopieren können.</span><span class="sxs-lookup"><span data-stu-id="10d30-140">Save the **Primary Endpoint** in a place where you can conveniently copy it from while working through the tutorial.</span></span> <span data-ttu-id="10d30-141">Dieser Endpunkt ist die URL Ihrer Web-App.</span><span class="sxs-lookup"><span data-stu-id="10d30-141">This endpoint is the URL of your web application.</span></span>

## <a name="upload-the-web-application"></a><span data-ttu-id="10d30-142">Hochladen der Web-App</span><span class="sxs-lookup"><span data-stu-id="10d30-142">Upload the web application</span></span>

1. <span data-ttu-id="10d30-143">Die Quelldateien für die Anwendung, die Sie in diesem Tutorial erstellen, befinden sich in einem [GitHub-Repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span><span class="sxs-lookup"><span data-stu-id="10d30-143">The source files for the application that you build in this tutorial are located in a [GitHub repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span></span> <span data-ttu-id="10d30-144">Stellen Sie sicher, dass Sie sich in Cloud Shell in Ihrem Basisverzeichnis befinden, und klonen Sie dieses Repository.</span><span class="sxs-lookup"><span data-stu-id="10d30-144">Make sure that you're in your home directory in Cloud Shell and clone this repository.</span></span>

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    <span data-ttu-id="10d30-145">Das Repository wird in `/home/<username>/functions-first-serverless-web-application` geklont.</span><span class="sxs-lookup"><span data-stu-id="10d30-145">The repository is cloned to `/home/<username>/functions-first-serverless-web-application`.</span></span>

1. <span data-ttu-id="10d30-146">Die clientseitige Webanwendung befindet sich im Ordner **www** und wird mit dem JavaScript-Framework „Vue.js“ erstellt.</span><span class="sxs-lookup"><span data-stu-id="10d30-146">The client-side web application is located in the **www** folder and is built using the Vue.js JavaScript framework.</span></span> <span data-ttu-id="10d30-147">Wechseln Sie in den Ordner, und führen Sie **npm**-Befehle aus, um die Anwendungsabhängigkeiten zu installieren und die Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="10d30-147">Change into the folder and run **npm** commands to install the application dependencies and build the application.</span></span> <span data-ttu-id="10d30-148">Es kann mehrere Minuten dauern, bis der letzte dieser Befehle abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="10d30-148">The last of these commands might take several minutes to complete.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www
    npm install
    npm run generate
    ```

    <span data-ttu-id="10d30-149">Die Anwendung wird im Ordner **dist** generiert.</span><span class="sxs-lookup"><span data-stu-id="10d30-149">The application is generated in the **dist** folder.</span></span>

1. <span data-ttu-id="10d30-150">Legen Sie den **dist**-Ordner als das aktuelle Verzeichnis fest, und laden Sie die Anwendung in den Blobcontainer **$web** hoch.</span><span class="sxs-lookup"><span data-stu-id="10d30-150">Change the current directory to the **dist** folder and upload the application to the **$web** blob container.</span></span>

    ```azurecli
    cd dist
    az storage blob upload-batch -s . -d \$web --account-name <storage account name>
    ```

1. <span data-ttu-id="10d30-151">Öffnen Sie die URL des primären Endpunkts für statische Storage-Websites in einem Webbrowser, um die Anwendung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="10d30-151">To view the application, open the Storage static websites primary endpoint URL in a web browser.</span></span>

    ![Startseite der ersten serverlosen Web-App](../media/1-app-screenshot-new.png)


## <a name="summary"></a><span data-ttu-id="10d30-153">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="10d30-153">Summary</span></span>

<span data-ttu-id="10d30-154">In dieser Einheit haben Sie eine Ressourcengruppe mit dem Namen **first-serverless-app** erstellt, die ein Speicherkonto enthält.</span><span class="sxs-lookup"><span data-stu-id="10d30-154">In this unit, you created a resource group named **first-serverless-app** that contains a Storage account.</span></span> <span data-ttu-id="10d30-155">Der statische Inhalt für Ihre Web-App wird in einem Blobcontainer namens **$web** im Speicherkonto gespeichert, und der Inhalt wird öffentlich zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="10d30-155">A blob container named **$web** in the Storage account stores the static content for your web application and makes the content publicly available.</span></span> <span data-ttu-id="10d30-156">Als Nächstes erfahren Sie, wie Sie eine serverlose Funktion zum Hochladen von Bildern in Blob Storage aus dieser Anwendung verwenden.</span><span class="sxs-lookup"><span data-stu-id="10d30-156">Next, you learn how to use a serverless function to upload images to Blob storage from this web application.</span></span>