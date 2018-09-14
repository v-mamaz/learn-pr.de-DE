<span data-ttu-id="2eadc-101">In dieser Übung erstellen Sie eine Azure-Funktion, die den Namen und die Größe eines Blobs beim Erstellen oder Aktualisieren anzeigt.</span><span class="sxs-lookup"><span data-stu-id="2eadc-101">In this exercise, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span> 

> [!NOTE]
> <span data-ttu-id="2eadc-102">Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com/) mit einem gültigen Konto angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="2eadc-102">To complete this exercise, make sure you're signed in to the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="2eadc-103">Erstellen eines Blobtriggers</span><span class="sxs-lookup"><span data-stu-id="2eadc-103">Create a blob trigger</span></span>

<span data-ttu-id="2eadc-104">Verwenden Sie wieder Ihre vorhandene Azure Functions-Anwendung und fügen Sie einen Blobtrigger hinzu.</span><span class="sxs-lookup"><span data-stu-id="2eadc-104">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="2eadc-105">Zeigen Sie auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-105">Point to **Functions** and select the plus (+) icon.</span></span>

    ![Zeigen auf „Funktionen“ und Auswählen des Pluszeichens](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="2eadc-107">Wählen Sie **Blobtrigger** aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="2eadc-108">Wählen Sie **C#** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-108">Select **C#** as the language.</span></span> 

1. <span data-ttu-id="2eadc-109">Behalten Sie für **Name** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="2eadc-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="2eadc-110">Behalten Sie für **Pfad** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="2eadc-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="2eadc-111">Wählen Sie ein vorhandenes Azure Storage-Konto aus, oder wählen Sie **Erstellen** aus, wenn Azure ein neues Konto für Sie erstellen soll.</span><span class="sxs-lookup"><span data-stu-id="2eadc-111">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="download-storage-explorer"></a><span data-ttu-id="2eadc-112">Herunterladen des Storage-Explorers</span><span class="sxs-lookup"><span data-stu-id="2eadc-112">Download Storage explorer</span></span>

<span data-ttu-id="2eadc-113">Nun, da Sie einen Blobtrigger erstellt haben, laden Sie den Storage-Explorer herunter, mit dem Sie einfach ein Blob erstellen können.</span><span class="sxs-lookup"><span data-stu-id="2eadc-113">Now that we've created a blob trigger, let's download Storage explorer, which will allow us to easily create a blob.</span></span>

- <span data-ttu-id="2eadc-114">Laden Sie den [Storage-Explorer](http://storageexplorer.com) herunter.</span><span class="sxs-lookup"><span data-stu-id="2eadc-114">Download [Storage explorer](http://storageexplorer.com).</span></span>

## <a name="connect-to-your-azure-storage-account"></a><span data-ttu-id="2eadc-115">Verbinden mit dem Azure Storage-Konto</span><span class="sxs-lookup"><span data-stu-id="2eadc-115">Connect to your Azure Storage account</span></span>

<span data-ttu-id="2eadc-116">Der Storage-Explorer wurde heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="2eadc-116">We now have Storage explorer downloaded.</span></span> <span data-ttu-id="2eadc-117">Melden Sie sich mit den bereitgestellten Anmeldeinformationen an.</span><span class="sxs-lookup"><span data-stu-id="2eadc-117">Let's sign in using the credentials that were supplied.</span></span>

1. <span data-ttu-id="2eadc-118">Wähen Sie im Storage-Explorer links das Pluszeichen (+) aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-118">In Storage explorer, select the plus (+) icon on the left.</span></span>

1. <span data-ttu-id="2eadc-119">Wählen Sie **Speicherkontonamen und -schlüssel verwenden** aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-119">Select **Use a storage account name and key**.</span></span>

1. <span data-ttu-id="2eadc-120">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="2eadc-120">Select **Next**.</span></span>

1. <span data-ttu-id="2eadc-121">Wählen Sie in Azure unter Ihrem Blobtrigger **Integrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-121">In Azure, under your blob trigger, select **Integrate**.</span></span>

1. <span data-ttu-id="2eadc-122">Wählen Sie **Dokumentation** aus, um die Ansicht zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="2eadc-122">Select **Documentation** to expand the view.</span></span>

1. <span data-ttu-id="2eadc-123">Kopieren Sie den **Kontonamen** und den **Kontoschlüssel**.</span><span class="sxs-lookup"><span data-stu-id="2eadc-123">Copy the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="2eadc-124">Fügen Sie dann im Storage-Explorer den **Kontonamen** und den **Kontoschlüssel** ein.</span><span class="sxs-lookup"><span data-stu-id="2eadc-124">Back in Storage explorer, paste in the **Account Name** and **Account Key**.</span></span>

1. <span data-ttu-id="2eadc-125">Geben Sie einen **Anzeigenamen** ein.</span><span class="sxs-lookup"><span data-stu-id="2eadc-125">Enter a **Display name**.</span></span> <span data-ttu-id="2eadc-126">Dieser Wert ist der Name der Verbindung im Storage-Explorer.</span><span class="sxs-lookup"><span data-stu-id="2eadc-126">This value is the name of the connection in Storage explorer.</span></span>

1. <span data-ttu-id="2eadc-127">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="2eadc-127">Select **Next**.</span></span>

1. <span data-ttu-id="2eadc-128">Wählen Sie **Verbinden**aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-128">Select **Connect**.</span></span> 

## <a name="create-a-blob-container"></a><span data-ttu-id="2eadc-129">Erstellen eines Blobcontainers</span><span class="sxs-lookup"><span data-stu-id="2eadc-129">Create a blob container</span></span>

<span data-ttu-id="2eadc-130">Sie sind nicht mit Ihrem Azure Storage-Konto verbunden.</span><span class="sxs-lookup"><span data-stu-id="2eadc-130">We aren't connected to our Azure Storage account.</span></span> <span data-ttu-id="2eadc-131">Beachten Sie, dass der Blobtrigger nur den Speicherort überwacht, der im Feld **Pfad** beschrieben ist.</span><span class="sxs-lookup"><span data-stu-id="2eadc-131">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="2eadc-132">Standardmäßig sollte der Pfad so aussehen:</span><span class="sxs-lookup"><span data-stu-id="2eadc-132">By default, our path should be:</span></span>

> <span data-ttu-id="2eadc-133">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="2eadc-133">samples-workitems/{name}</span></span>

<span data-ttu-id="2eadc-134">Erstellen Sie einen Container mit dem Namen **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="2eadc-134">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="2eadc-135">Erweitern Sie Ihr Speicherkonto im Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="2eadc-135">In Storage explorer, expand your storage account.</span></span> <span data-ttu-id="2eadc-136">Der Name muss der **Anzeigename** sein, den Sie beim Verbinden angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="2eadc-136">The name should be the **Display name** that you provided during the connection process.</span></span>

1. <span data-ttu-id="2eadc-137">Klicken Sie mit der rechten Maustaste auf **Blobcontainer** und wählen Sie **Blobcontainer erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-137">Right-click **Blob Containers** and select **Create blob container**.</span></span>

1. <span data-ttu-id="2eadc-138">Geben Sie **samples-workitems** ein.</span><span class="sxs-lookup"><span data-stu-id="2eadc-138">Enter **samples-workitems**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="2eadc-139">Aktivieren des Blobtriggers</span><span class="sxs-lookup"><span data-stu-id="2eadc-139">Turn on your blob trigger</span></span>

<span data-ttu-id="2eadc-140">Nachdem Sie einen Container zum Überwachen erstellt haben, führen Sie Ihre Funktion aus, um beim Erstellen eines Blobs die Ausgabe zu sehen.</span><span class="sxs-lookup"><span data-stu-id="2eadc-140">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="2eadc-141">Wählen Sie Ihren Blobtrigger aus, um den Codebildschirm zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="2eadc-141">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="2eadc-142">Klicken Sie auf **Run** (Ausführen).</span><span class="sxs-lookup"><span data-stu-id="2eadc-142">Select **Run**.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="2eadc-143">Erstellen eines Blobs</span><span class="sxs-lookup"><span data-stu-id="2eadc-143">Create a blob</span></span>

<span data-ttu-id="2eadc-144">Der Blobtrigger ist nun aktiviert und wartet auf Aktivität.</span><span class="sxs-lookup"><span data-stu-id="2eadc-144">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="2eadc-145">Erstellen Sie ein Blob, um zu überprüfen, ob Sie eine Protokollmeldung erhalten.</span><span class="sxs-lookup"><span data-stu-id="2eadc-145">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="2eadc-146">Wählen Sie im Storage-Explorer den Container **samples-workitems** aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-146">In Storage explorer, select the **samples-workitems** container.</span></span>

1. <span data-ttu-id="2eadc-147">Wählen Sie die Option **Hochladen**.</span><span class="sxs-lookup"><span data-stu-id="2eadc-147">Select **Upload**.</span></span> 

1. <span data-ttu-id="2eadc-148">Wählen Sie **Dateien hochladen** aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-148">Select **Upload Files**.</span></span>

1. <span data-ttu-id="2eadc-149">Wählen Sie eine beliebige Datei auf Ihrem Computer aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-149">Select any file from your computer.</span></span>

1. <span data-ttu-id="2eadc-150">Wählen Sie die Option **Hochladen**.</span><span class="sxs-lookup"><span data-stu-id="2eadc-150">Select **Upload**.</span></span>

1. <span data-ttu-id="2eadc-151">Kehren Sie zurück zu Azure.</span><span class="sxs-lookup"><span data-stu-id="2eadc-151">Go back to Azure.</span></span> <span data-ttu-id="2eadc-152">Überprüfen Sie Ihre Protokolle auf eine Meldung, die anzeigt, welche Datei hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="2eadc-152">Check your logs for a message that displays what file was uploaded.</span></span>

## <a name="clean-up"></a><span data-ttu-id="2eadc-153">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="2eadc-153">Clean up</span></span>

<span data-ttu-id="2eadc-154">Um sicherzustellen, dass für diese Funktion keine Gebühren anfallen, wählen Sie über dem Protokollfenster **Anhalten** aus.</span><span class="sxs-lookup"><span data-stu-id="2eadc-154">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![Pause](../media-drafts/4-pause-timer.png)


