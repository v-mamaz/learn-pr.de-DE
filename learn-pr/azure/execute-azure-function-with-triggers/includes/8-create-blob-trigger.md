<span data-ttu-id="42134-101">In dieser Einheit erfahren Sie, wie Sie eine Azure-Funktion erstellen, die den Namen und die Größe eines Blobs beim Erstellen oder Aktualisieren anzeigt.</span><span class="sxs-lookup"><span data-stu-id="42134-101">In this unit, we're going to create an Azure function that displays the name and size of a blob when it's created or updated.</span></span>

## <a name="create-a-blob-trigger"></a><span data-ttu-id="42134-102">Erstellen eines Blobtriggers</span><span class="sxs-lookup"><span data-stu-id="42134-102">Create a blob trigger</span></span>

<span data-ttu-id="42134-103">Verwenden Sie wieder Ihre vorhandene Azure Functions-Anwendung und fügen Sie einen Blobtrigger hinzu.</span><span class="sxs-lookup"><span data-stu-id="42134-103">Again, let's continue using our existing Azure Functions application and add a blob trigger.</span></span>

1. <span data-ttu-id="42134-104">Melden Sie sich im [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="42134-104">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="42134-105">Zeigen Sie auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).</span><span class="sxs-lookup"><span data-stu-id="42134-105">Point to **Functions** and select the plus (+) icon.</span></span>

1. <span data-ttu-id="42134-106">Klicken Sie auf **Benutzerdefinierte Funktion** und anschließend auf **Blobtrigger**.</span><span class="sxs-lookup"><span data-stu-id="42134-106">Select **Custom Function** and then **Blob trigger**.</span></span>

1. <span data-ttu-id="42134-107">Wählen Sie **C#** als Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="42134-107">Select **C#** as the language.</span></span>

1. <span data-ttu-id="42134-108">Behalten Sie für **Name** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="42134-108">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="42134-109">Behalten Sie für **Pfad** den Standardwert bei.</span><span class="sxs-lookup"><span data-stu-id="42134-109">Leave the **Path** set to the default value.</span></span>

1. <span data-ttu-id="42134-110">Wählen Sie ein vorhandenes Azure Storage-Konto aus, oder klicken Sie auf **Erstellen**, wenn Azure ein neues Konto für Sie erstellen soll.</span><span class="sxs-lookup"><span data-stu-id="42134-110">Select an existing Azure Storage account, or select **Create** if you want Azure to create a new account for you.</span></span>

## <a name="create-a-blob-container"></a><span data-ttu-id="42134-111">Erstellen eines Blobcontainers</span><span class="sxs-lookup"><span data-stu-id="42134-111">Create a blob container</span></span>

<span data-ttu-id="42134-112">Nun, da wir einen Blobtrigger erstellt haben, verwenden wir den Storage-Explorer, um ein Blob zu erstellen und die Funktion auszulösen.</span><span class="sxs-lookup"><span data-stu-id="42134-112">Now that we've created a blob trigger, let's use the Storage Explorer to create a blob and trigger the function.</span></span>

1. <span data-ttu-id="42134-113">Öffnen Sie das verwendete (oder erstellte) Speicherkonto auf einer neuen Registerkarte. Eine einfache Möglichkeit hierzu besteht darin, eine neue Registerkarte im Azure-Portal zu öffnen und auf der Seitenleiste auf **Speicherkonten** zu klicken. Alternativ können Sie in der Seitenleiste auf **Alle Dienste** klicken und dann nach Namen filtern.</span><span class="sxs-lookup"><span data-stu-id="42134-113">Open the storage account you used (or created) in a new tab. An easy way to do this is to open a new Azure Portal tab and click on **Storage accounts** in the sidebar, or to use **All services** in the sidebar and then filter by the name.</span></span> <span data-ttu-id="42134-114">Wir verwenden in diesem Fall eine neue Registerkarte, damit wir während der Arbeit zwischen den zwei Diensten wechseln können.</span><span class="sxs-lookup"><span data-stu-id="42134-114">We want to use a new tab so we can switch between the two services we are working with.</span></span>

1. <span data-ttu-id="42134-115">Klicken Sie auf den Abschnitt **Storage-Explorer (Vorschau)**, um ein neues Blatt zu öffnen, in dem Sie mit Blobs und Dateien arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="42134-115">Click on the **Storage Explorer (preview)** section - this will open a new blade where you can work with blobs and files.</span></span>

<span data-ttu-id="42134-116">Beachten Sie, dass der Blobtrigger nur den Speicherort überwacht, der im Feld **Pfad** angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="42134-116">Remember that our blob trigger is monitoring only the location described in the **Path** field.</span></span> <span data-ttu-id="42134-117">Standardmäßig sollte der Pfad so aussehen:</span><span class="sxs-lookup"><span data-stu-id="42134-117">By default, our path should be:</span></span>

> <span data-ttu-id="42134-118">samples-workitems/{name}</span><span class="sxs-lookup"><span data-stu-id="42134-118">samples-workitems/{name}</span></span>

<span data-ttu-id="42134-119">Wir müssen einen Container mit dem Namen **samples-workitems** erstellen.</span><span class="sxs-lookup"><span data-stu-id="42134-119">We need to create a container called **samples-workitems**.</span></span>

1. <span data-ttu-id="42134-120">Klicken Sie mit der rechten Maustaste auf **BLOBCONTAINER**, und wählen Sie **Blobcontainer erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="42134-120">Right-click **BLOB CONTAINERS** and select **Create blob container**.</span></span>

1. <span data-ttu-id="42134-121">Geben Sie als Name **samples-workitems** ein, und behalten Sie für die Zugriffsebene die Standardeinstellung **Privat** bei.</span><span class="sxs-lookup"><span data-stu-id="42134-121">Enter **samples-workitems** as the name, leave the access level at the default **Private** setting.</span></span>

## <a name="turn-on-your-blob-trigger"></a><span data-ttu-id="42134-122">Aktivieren Ihres Blobtriggers</span><span class="sxs-lookup"><span data-stu-id="42134-122">Turn on your blob trigger</span></span>

<span data-ttu-id="42134-123">Nachdem wir einen Container zum Überwachen erstellt haben, führen wir jetzt Ihre Funktion aus, um beim Erstellen eines Blobs eine Ausgabe anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="42134-123">Now that we've created our container to monitor, let's run our function so we can see output when a blob is created.</span></span>

1. <span data-ttu-id="42134-124">Wechseln Sie zurück zur Registerkarte der Azure-Funktion (um sie erneut zu öffnen).</span><span class="sxs-lookup"><span data-stu-id="42134-124">Switch back to the Azure Function tab (or reopen it).</span></span>

1. <span data-ttu-id="42134-125">Wählen Sie Ihren Blobtrigger aus, um den Codebildschirm zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="42134-125">Select your blob trigger to open the code screen.</span></span>

1. <span data-ttu-id="42134-126">Klicken Sie auf **Ausführen** – dadurch wird das Ausgabefenster angezeigt.</span><span class="sxs-lookup"><span data-stu-id="42134-126">Select **Run** - this will open the output window.</span></span>

## <a name="create-a-blob"></a><span data-ttu-id="42134-127">Erstellen eines Blobs</span><span class="sxs-lookup"><span data-stu-id="42134-127">Create a blob</span></span>

<span data-ttu-id="42134-128">Der Blobtrigger ist nun aktiviert und wartet auf Aktivität.</span><span class="sxs-lookup"><span data-stu-id="42134-128">Our blob trigger is now up and listening for activity.</span></span> <span data-ttu-id="42134-129">Erstellen Sie ein Blob, um zu überprüfen, ob Sie eine Protokollmeldung erhalten.</span><span class="sxs-lookup"><span data-stu-id="42134-129">Let's create a blob to see if we get a log message.</span></span>

1. <span data-ttu-id="42134-130">Wählen Sie im Storage-Explorer den Container **samples-workitems** aus.</span><span class="sxs-lookup"><span data-stu-id="42134-130">In Storage explorer, select the **samples-workitems** container.</span></span>

1. <span data-ttu-id="42134-131">Klicken Sie auf der Symbolleiste auf **Hochladen**.</span><span class="sxs-lookup"><span data-stu-id="42134-131">Select **Upload** from the toolbar.</span></span>

1. <span data-ttu-id="42134-132">Wählen Sie eine beliebige Datei auf Ihrem Computer aus.</span><span class="sxs-lookup"><span data-stu-id="42134-132">Select any file from your computer.</span></span>

1. <span data-ttu-id="42134-133">Klicken Sie auf **Hochladen**.</span><span class="sxs-lookup"><span data-stu-id="42134-133">Select **Upload**.</span></span>

1. <span data-ttu-id="42134-134">Wechseln Sie zurück zur Registerkarte der Azure-Funktion, und suchen Sie in den Ausgabeprotokollen nach einer Meldung, die anzeigt, dass die Datei hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="42134-134">Switch back to the Azure Function tab and check the output logs for a message that displays what file was uploaded.</span></span>

## <a name="pause-the-function"></a><span data-ttu-id="42134-135">Anhalten der Funktion</span><span class="sxs-lookup"><span data-stu-id="42134-135">Pause the Function</span></span>

<span data-ttu-id="42134-136">Sie können über dem Protokollfenster auf **Anhalten** klicken, um sicherzustellen, dass keine Gebühren für zusätzliche Anforderungen anfallen.</span><span class="sxs-lookup"><span data-stu-id="42134-136">To ensure that you aren't charged for additional requests, you can click **Pause** above the log window.</span></span>
