<span data-ttu-id="235ea-101">In dieser Einheit erfahren Sie, wie Sie eine Azure-Funktion erstellen, die den Namen und die Größe eines Blobs beim Erstellen oder Aktualisieren anzeigt.</span><span class="sxs-lookup"><span data-stu-id="235ea-101">In this unit, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="235ea-102">Erstellen eines Blobtriggers</span><span class="sxs-lookup"><span data-stu-id="235ea-102">Create a blob trigger</span></span>

<span data-ttu-id="235ea-103">Verwenden Sie wieder Ihre vorhandene Azure Functions-Anwendung, und fügen Sie einen Blobtrigger hinzu.</span><span class="sxs-lookup"><span data-stu-id="235ea-103">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="235ea-104">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="235ea-104">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="235ea-105">Navigieren Sie zum Bildschirm **Alle Ressourcen**, und wählen Sie Ihre Funktions-App aus.</span><span class="sxs-lookup"><span data-stu-id="235ea-105">Navigate to the **All resources** screen and select your function app.</span></span>

1. <span data-ttu-id="235ea-106">Zeigen Sie auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).</span><span class="sxs-lookup"><span data-stu-id="235ea-106">Point to **Functions** and select the plus (+) icon.</span></span>

1. <span data-ttu-id="235ea-107">Wählen Sie **Blobtrigger** aus.</span><span class="sxs-lookup"><span data-stu-id="235ea-107">Select **Blob trigger**.</span></span>

1. <span data-ttu-id="235ea-108">Wählen Sie **C#** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="235ea-108">Select **C#** as the language.</span></span>

1. <span data-ttu-id="235ea-109">Behalten Sie für **Name** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="235ea-109">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="235ea-110">Behalten Sie für **Pfad** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="235ea-110">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="235ea-111">Klicken Sie auf den _neuen_ Link neben dem Dropdownmenü **Speicherkontoverbindung**.</span><span class="sxs-lookup"><span data-stu-id="235ea-111">Select the _new_ link next to the **Storage account connection** dropdown.</span></span> <span data-ttu-id="235ea-112">Klicken Sie auf dem Blatt, das geöffnet wird, auf **Neu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="235ea-112">In the blade that pops up, click **Create new**.</span></span> <span data-ttu-id="235ea-113">Geben Sie einen eindeutigen Namen für das neue Speicherkonto ein, und klicken Sie auf **OK**, um das Speicherkonto zu erstellen und den Bereich zu schließen.</span><span class="sxs-lookup"><span data-stu-id="235ea-113">Enter a unique name for the new storage account and select **OK** to create the storage account and close pane.</span></span>

1. <span data-ttu-id="235ea-114">Klicken Sie auf dem Bildschirm „Neue Funktion“ auf **Erstellen**, um die Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="235ea-114">Once you have returned to the New Function screen, select **Create** to create the function.</span></span>

## <a name="create-a-blob-container"></a><span data-ttu-id="235ea-115">Erstellen eines Blobcontainers</span><span class="sxs-lookup"><span data-stu-id="235ea-115">Create a blob container</span></span>

<span data-ttu-id="235ea-116">Nun, da wir einen Blobtrigger erstellt haben, verwenden wir den Storage-Explorer, um ein Blob zu erstellen und die Funktion auszulösen.</span><span class="sxs-lookup"><span data-stu-id="235ea-116">Now that we've created a blob trigger, let's use the Storage Explorer to create a blob and trigger the function.</span></span>

1. <span data-ttu-id="235ea-117">Öffnen Sie das verwendete (oder erstellte) Speicherkonto auf einer neuen Registerkarte.</span><span class="sxs-lookup"><span data-stu-id="235ea-117">Open the storage account you used (or created) in a new tab.</span></span>

    > [!TIP]
    > <span data-ttu-id="235ea-118">Sie können eine Registerkarte in den meisten Browsern duplizieren, indem Sie mit der rechten Maustaste auf sie klicken und aus dem Menü **Duplizieren** oder eine gleichwertige Option auswählen.</span><span class="sxs-lookup"><span data-stu-id="235ea-118">You can duplicate a tab in most browsers by right-clicking on the tab in question and selecting **Duplicate** from the menu that appears.</span></span> <span data-ttu-id="235ea-119">Sie verwenden in diesem Fall eine neue Registerkarte, um während der Arbeit zwischen den beiden Diensten wechseln zu können.</span><span class="sxs-lookup"><span data-stu-id="235ea-119">We want to use a new tab so we can switch between the two services we are working with.</span></span>

1. <span data-ttu-id="235ea-120">Klicken Sie in der Randleiste auf **Speicherkonten**, oder klicken Sie dort alternativ auf **Alle Ressourcen**, und filtern Sie anschließend nach Name.</span><span class="sxs-lookup"><span data-stu-id="235ea-120">Select **Storage accounts** in the sidebar, or select **All resources** in the sidebar and then filter by the name.</span></span>

1. <span data-ttu-id="235ea-121">Klicken Sie auf den Abschnitt **Storage-Explorer (Vorschau)**, um ein neues Panel zu öffnen, in dem Sie mit Blobs und Dateien arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="235ea-121">Click on the **Storage Explorer (preview)** section - this will open a new panel where you can work with blobs and files.</span></span>

<span data-ttu-id="235ea-122">Beachten Sie, dass der Blobtrigger nur den Speicherort überwacht, der im Feld **Pfad** angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="235ea-122">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="235ea-123">Standardmäßig sollte der Pfad so aussehen:</span><span class="sxs-lookup"><span data-stu-id="235ea-123">By default, our path should be:</span></span>

> <span data-ttu-id="235ea-124">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="235ea-124">samples-workitems/{name}</span></span>

<span data-ttu-id="235ea-125">Erstellen Sie nun einen Container mit dem Namen **samples-workitems**.</span><span class="sxs-lookup"><span data-stu-id="235ea-125">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="235ea-126">Klicken Sie mit der rechten Maustaste auf **BLOBCONTAINER** und anschließend auf **BLOB-Container erstellen**.</span><span class="sxs-lookup"><span data-stu-id="235ea-126">Right-click **BLOB CONTAINERS** and select **Create Blob Container**.</span></span>

1. <span data-ttu-id="235ea-127">Geben Sie als Name **samples-workitems** ein, und behalten Sie für die Zugriffsebene die Standardeinstellung **Privat** bei. Klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="235ea-127">Enter **samples-workitems** as the name, leave the access level at the default **Private** setting, and select **OK**.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="235ea-128">Aktivieren des Blobtriggers</span><span class="sxs-lookup"><span data-stu-id="235ea-128">Turn on your blob trigger</span></span>

<span data-ttu-id="235ea-129">Nachdem Sie einen Container zum Überwachen erstellt haben, führen Sie nun Ihre Funktion aus, um beim Erstellen eines Blobs eine Ausgabe anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="235ea-129">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="235ea-130">Wechseln Sie zurück zur Browserregisterkarte mit Ihrer Azure-Funktion, oder öffnen Sie diese erneut.</span><span class="sxs-lookup"><span data-stu-id="235ea-130">Switch back to the browser tab with your Azure Function (or reopen it).</span></span>

1. <span data-ttu-id="235ea-131">Wählen Sie Ihren Blobtrigger aus, um den Codebildschirm zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="235ea-131">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="235ea-132">Öffnen Sie im unteren Bildschirmbereich die Registerkarte **Protokolle**.</span><span class="sxs-lookup"><span data-stu-id="235ea-132">Open the **Logs** tab at the bottom of the screen.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="235ea-133">Erstellen eines Blobs</span><span class="sxs-lookup"><span data-stu-id="235ea-133">Create a blob</span></span>

<span data-ttu-id="235ea-134">Der Blobtrigger ist nun aktiviert und wartet auf Aktivität.</span><span class="sxs-lookup"><span data-stu-id="235ea-134">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="235ea-135">Erstellen Sie ein Blob, um zu überprüfen, ob Sie eine Protokollmeldung erhalten.</span><span class="sxs-lookup"><span data-stu-id="235ea-135">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="235ea-136">Wechseln Sie zurück zur Browserregisterkarte mit dem Storage-Explorer.</span><span class="sxs-lookup"><span data-stu-id="235ea-136">Switch back to the browser tab with Storage Explorer.</span></span>

1. <span data-ttu-id="235ea-137">Wählen Sie im Storage-Explorer den Container **samples-workitems** aus der Liste **BLOBCONTAINER** aus.</span><span class="sxs-lookup"><span data-stu-id="235ea-137">In Storage Explorer, select the **samples-workitems** container from the **BLOB CONTAINERS** list.</span></span>

1. <span data-ttu-id="235ea-138">Klicken Sie in der Symbolleiste auf **Hochladen**.</span><span class="sxs-lookup"><span data-stu-id="235ea-138">Select **Upload** from the toolbar.</span></span>

1. <span data-ttu-id="235ea-139">Wählen Sie eine beliebige Datei auf Ihrem Computer aus.</span><span class="sxs-lookup"><span data-stu-id="235ea-139">Select any file from your computer.</span></span>

1. <span data-ttu-id="235ea-140">Wählen Sie unter **Authentifizierungstyp** die Option **SAS** aus.</span><span class="sxs-lookup"><span data-stu-id="235ea-140">Under **Authentication type**, select **SAS**.</span></span>

1. <span data-ttu-id="235ea-141">Klicken Sie auf **Hochladen**.</span><span class="sxs-lookup"><span data-stu-id="235ea-141">Select **Upload**.</span></span>

1. <span data-ttu-id="235ea-142">Wechseln Sie zurück zur Registerkarte „Azure-Funktion“, und suchen Sie in den Ausgabeprotokollen nach einer Meldung, die angibt, welche Datei hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="235ea-142">Switch back to the Azure Function tab and check the output logs for a message that displays what file was uploaded.</span></span>