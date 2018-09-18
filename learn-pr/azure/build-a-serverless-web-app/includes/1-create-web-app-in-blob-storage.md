<span data-ttu-id="ef502-101">Im Rahmen dieses Moduls stellen Sie eine einfache Web-App bereit, die über eine HTML-basierte Benutzeroberfläche verfügt.</span><span class="sxs-lookup"><span data-stu-id="ef502-101">In this module, you will deploy a simple web application that presents an HTML-based user interface.</span></span> <span data-ttu-id="ef502-102">Mit einem serverlosen Back-End kann die Anwendung Bilder hochladen und automatisch beschreibende Bildtitel generieren.</span><span class="sxs-lookup"><span data-stu-id="ef502-102">A serverless back end enables the application to upload images and automatically generate descriptive captions.</span></span>

![Ausführen der Web-App](../media/0-app-screenshot-finished.png)

<span data-ttu-id="ef502-104">Im folgenden Diagramm sind die Azure-Dienste aufgeführt, die von der Anwendung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ef502-104">The following diagram shows the Azure services that are used by the application.</span></span>

![Diagramm der Lösungsarchitektur](../media/0-architecture.jpg)

1. <span data-ttu-id="ef502-106">Azure Blob Storage stellt statischen Webinhalt (HTML, CSS, JS) bereit und speichert Bilder.</span><span class="sxs-lookup"><span data-stu-id="ef502-106">Azure Blob storage serves static web content (HTML, CSS, JS) and stores images.</span></span>
2. <span data-ttu-id="ef502-107">Azure Functions verwaltet das Hochladen von Bildern, die Größenänderung und die Speicherung von Metadaten.</span><span class="sxs-lookup"><span data-stu-id="ef502-107">Azure Functions manages image uploads, resizing, and metadata storage.</span></span>
3. <span data-ttu-id="ef502-108">Azure Cosmos DB speichert Bildmetadaten.</span><span class="sxs-lookup"><span data-stu-id="ef502-108">Azure Cosmos DB stores image metadata.</span></span>
4. <span data-ttu-id="ef502-109">Azure Logic Apps ruft Bildtitel von der Maschinelles Sehen-API von Cognitive Services ab.</span><span class="sxs-lookup"><span data-stu-id="ef502-109">Azure Logic Apps retrieves image captions from the Cognitive Services Computer Vision API.</span></span>
5. <span data-ttu-id="ef502-110">Azure Active Directory wird zum Verwalten der Benutzerauthentifizierung verwendet.</span><span class="sxs-lookup"><span data-stu-id="ef502-110">Azure Active Directory manages user authentication.</span></span>

<span data-ttu-id="ef502-111">Azure Blob Storage ist ein kostengünstiger und extrem skalierbarer Dienst, der zum Hosten von statischen Dateien verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="ef502-111">Azure Blob storage is a low-cost and massively scalable service that can be used to host static files.</span></span> <span data-ttu-id="ef502-112">In diesem Modul verwenden Sie Blob Storage, um statische Inhalte (z.B. HTML, JavaScript oder CSS) für die Web-App bereitzustellen, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="ef502-112">In this module, you will use Blob storage to serve static content (for example, HTML, JavaScript, or CSS) for a web app you build.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="ef502-113">Erstellen eines Azure-Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="ef502-113">Create an Azure Storage account</span></span>
<!---TODO: Update for sandbox?--->

<span data-ttu-id="ef502-114">Ein Azure-Speicherkonto ist eine Azure-Ressource, mit der Sie Tabellen, Warteschlangen, Dateien, Blobs (Objekte) und VM-Datenträger speichern können.</span><span class="sxs-lookup"><span data-stu-id="ef502-114">An Azure Storage account is an Azure resource that allows you to store tables, queues, files, blobs (objects), and virtual machine disks.</span></span>

1. <span data-ttu-id="ef502-115">Klicken Sie auf die Schaltfläche **Enter focus mode** (Fokusmodus starten), um Azure Cloud Shell (Bash) zu starten.</span><span class="sxs-lookup"><span data-stu-id="ef502-115">Select the **Enter focus mode** button to launch Azure Cloud Shell (Bash).</span></span> <span data-ttu-id="ef502-116">Diese Schaltfläche befindet sich oben rechts oder unten auf der Seite. Dies hängt davon ab, wie breit Ihr Browserfenster dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="ef502-116">This button is at the top right or the bottom of the page, depending on how wide your browser window is.</span></span> <span data-ttu-id="ef502-117">Im Fokusmodus wird ein Cloud Shell-Fenster im Browserfenster auf der rechten Seite angedockt, damit Sie im Tutorial angezeigte Befehle leicht ausführen können.</span><span class="sxs-lookup"><span data-stu-id="ef502-117">Focus mode docks a Cloud Shell window on the right side of your browser window, so you can easily execute commands that are shown in the tutorial.</span></span>

1. <span data-ttu-id="ef502-118">In Azure ist eine Ressourcengruppe ein Container, der zusammengehörige Azure-Ressourcen enthält, um die Verwaltung zu vereinfachen.</span><span class="sxs-lookup"><span data-stu-id="ef502-118">In Azure, a resource group is a container that holds related Azure resources for ease of management.</span></span> <span data-ttu-id="ef502-119">Erstellen Sie eine neue Ressourcengruppe mit dem Namen **first-serverless-app**.</span><span class="sxs-lookup"><span data-stu-id="ef502-119">Create a new resource group named **first-serverless-app**.</span></span>

    ```azurecli
    az group create -n first-serverless-app -l westcentralus
    ```

1. <span data-ttu-id="ef502-120">Der statische Inhalt (HTML-, CSS- und JavaScript-Dateien) für dieses Tutorial wird in Blob Storage gehostet.</span><span class="sxs-lookup"><span data-stu-id="ef502-120">The static content (HTML, CSS, and JavaScript files) for this tutorial is hosted in Blob storage.</span></span> <span data-ttu-id="ef502-121">Für Blob Storage ist ein Speicherkonto erforderlich.</span><span class="sxs-lookup"><span data-stu-id="ef502-121">Blob storage requires a Storage account.</span></span> <span data-ttu-id="ef502-122">Erstellen Sie ein Speicherkonto vom Typ „General-purpose v2“(GPv2) in der Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="ef502-122">Create a general-purpose v2 (GPv2) Storage account in the resource group.</span></span> <span data-ttu-id="ef502-123">Ersetzen Sie `<storage account name>` durch einen eindeutigen Namen.</span><span class="sxs-lookup"><span data-stu-id="ef502-123">Replace `<storage account name>` with a unique name.</span></span>

    ```azurecli
    az storage account create -n <storage account name> -g first-serverless-app --kind StorageV2 -l westcentralus --https-only true --sku Standard_LRS
    ```
    
1. <span data-ttu-id="ef502-124">Verwenden Sie die Suchleiste oben im [Azure-Portal](https://portal.azure.com/?azure-portal=true), um das Speicherkonto zu finden, das Sie eben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="ef502-124">Use the Search bar at the top of the [Azure portal](https://portal.azure.com/?azure-portal=true) to find the storage account that you just created.</span></span> <span data-ttu-id="ef502-125">Öffnen Sie das Konto.</span><span class="sxs-lookup"><span data-stu-id="ef502-125">Open the account.</span></span>

1. <span data-ttu-id="ef502-126">Klicken Sie im linken Navigationsbereich auf **Statische Website (Vorschau)**, um einen Container für das Hosten von statischen Websites zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="ef502-126">On the left navigation, select **Static website (preview)** to configure a container for static website hosting.</span></span>
    - <span data-ttu-id="ef502-127">Klicken Sie auf **Aktiviert**, um eine statische Website zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="ef502-127">Select **Enabled** to enable a static website.</span></span>
    - <span data-ttu-id="ef502-128">Geben Sie **index.html** als Name des Indexdokuments ein.</span><span class="sxs-lookup"><span data-stu-id="ef502-128">Enter **index.html** as the index document name.</span></span> <span data-ttu-id="ef502-129">Im Feld steht *index.html* bereits in grauer Schrift, jedoch ist dies nur ein Beispieltext.</span><span class="sxs-lookup"><span data-stu-id="ef502-129">The box already has *index.html* in a gray font, but this is only example text.</span></span> <span data-ttu-id="ef502-130">Sie müssen trotzdem **index.html** in das Feld eingeben.</span><span class="sxs-lookup"><span data-stu-id="ef502-130">You still have to enter **index.html** in the box.</span></span>
    - <span data-ttu-id="ef502-131">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="ef502-131">Click **Save**.</span></span>
    
    ![Eingeben der Einstellungen für die statische Website](../media/1-storage-static-website.png)

1. <span data-ttu-id="ef502-133">Speichern Sie den **primären Endpunkt** an einem Ort, an dem Sie ihn beim Durcharbeiten des Tutorials bequem kopieren können.</span><span class="sxs-lookup"><span data-stu-id="ef502-133">Save the **Primary Endpoint** in a place where you can conveniently copy it from while working through the tutorial.</span></span> <span data-ttu-id="ef502-134">Dieser Endpunkt ist die URL Ihrer Web-App.</span><span class="sxs-lookup"><span data-stu-id="ef502-134">This endpoint is the URL of your web application.</span></span>

## <a name="upload-the-web-application"></a><span data-ttu-id="ef502-135">Hochladen der Web-App</span><span class="sxs-lookup"><span data-stu-id="ef502-135">Upload the web application</span></span>

1. <span data-ttu-id="ef502-136">Die Quelldateien für die Anwendung, die Sie in diesem Tutorial erstellen, befinden sich in einem [GitHub-Repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span><span class="sxs-lookup"><span data-stu-id="ef502-136">The source files for the application that you build in this tutorial are located in a [GitHub repository](https://github.com/Azure-Samples/functions-first-serverless-web-application).</span></span> <span data-ttu-id="ef502-137">Navigieren Sie in Cloud Shell zu Ihrem Basisverzeichnis, und klonen Sie dieses Repository.</span><span class="sxs-lookup"><span data-stu-id="ef502-137">Go to your home directory in Cloud Shell and clone this repository.</span></span>

    ```azurecli
    cd ~
    git clone https://github.com/Azure-Samples/functions-first-serverless-web-application
    ```

    <span data-ttu-id="ef502-138">Das Repository wird in `/home/<username>/functions-first-serverless-web-application` geklont.</span><span class="sxs-lookup"><span data-stu-id="ef502-138">The repository is cloned to `/home/<username>/functions-first-serverless-web-application`.</span></span>

1. <span data-ttu-id="ef502-139">Die clientseitige Webanwendung befindet sich im Ordner **www** und wird mit dem JavaScript-Framework „Vue.js“ erstellt.</span><span class="sxs-lookup"><span data-stu-id="ef502-139">The client-side web application is located in the **www** folder and is built using the Vue.js JavaScript framework.</span></span> <span data-ttu-id="ef502-140">Öffnen Sie den Ordner **www**, und führen Sie **npm**-Befehle aus, um die Anwendungsabhängigkeiten zu installieren und die Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ef502-140">Open the **www** folder and run **npm** commands to install the application dependencies and build the application.</span></span> <span data-ttu-id="ef502-141">Es kann mehrere Minuten dauern, bis der letzte dieser Befehle abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="ef502-141">The last of these commands might take several minutes to complete.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www
    npm install
    npm run generate
    ```

    <span data-ttu-id="ef502-142">Die Anwendung wird im Ordner **dist** generiert.</span><span class="sxs-lookup"><span data-stu-id="ef502-142">The application is generated in the **dist** folder.</span></span>

1. <span data-ttu-id="ef502-143">Legen Sie den **dist**-Ordner als das aktuelle Verzeichnis fest, und laden Sie die Anwendung in den Blobcontainer **$web** hoch.</span><span class="sxs-lookup"><span data-stu-id="ef502-143">Change the current directory to the **dist** folder and upload the application to the **$web** blob container.</span></span>

    ```azurecli
    cd dist
    az storage blob upload-batch -s . -d \$web --account-name <storage account name>
    ```

1. <span data-ttu-id="ef502-144">Öffnen Sie die URL des primären Endpunkts der statischen Websites in einem Webbrowser, um die Anwendung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ef502-144">To view the application, open the static website’s primary endpoint URL in a web browser.</span></span>

    ![Startseite der ersten serverlosen Web-App](../media/1-app-screenshot-new.png)


## <a name="summary"></a><span data-ttu-id="ef502-146">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="ef502-146">Summary</span></span>

<span data-ttu-id="ef502-147">In dieser Einheit haben Sie eine Ressourcengruppe mit dem Namen **first-serverless-app** erstellt, die ein Speicherkonto enthält.</span><span class="sxs-lookup"><span data-stu-id="ef502-147">In this unit, you created a resource group named **first-serverless-app** that contains a Storage account.</span></span> <span data-ttu-id="ef502-148">Der statische Inhalt für Ihre Web-App wird in einem Blobcontainer namens **$web** im Speicherkonto gespeichert, und der Inhalt wird öffentlich zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="ef502-148">A blob container named **$web** in the Storage account stores the static content for your web application and makes the content publicly available.</span></span> <span data-ttu-id="ef502-149">Als Nächstes erfahren Sie, wie Sie eine serverlose Funktion zum Hochladen von Bildern in Blob Storage aus dieser Webanwendung verwenden.</span><span class="sxs-lookup"><span data-stu-id="ef502-149">Next, you will learn how to use a serverless function to upload images to Blob storage from this web application.</span></span>