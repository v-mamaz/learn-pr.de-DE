<span data-ttu-id="61095-101">In dieser Übung erstellen Sie über das Azure-Portal ein Speicherkonto für eine Web-App, mit der fiktive Surfberichte für Südkalifornien bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="61095-101">In this exercise, you will use the Azure portal to create a storage account that is appropriate for a fictitious southern California surf report Web App.</span></span>

## <a name="design-goals"></a><span data-ttu-id="61095-102">Entwurfsziele</span><span class="sxs-lookup"><span data-stu-id="61095-102">Design goals</span></span>

<span data-ttu-id="61095-103">Auf einer Website mit Surfberichten können Benutzer Fotos und Videos von den Surfbedingungen an Stränden hochladen.</span><span class="sxs-lookup"><span data-stu-id="61095-103">The surf-report site lets users upload photos and videos of their local beach conditions.</span></span> <span data-ttu-id="61095-104">Andere Personen können sich diese Inhalte ansehen und sich dann für einen geeigneten Strand zum Surfen entscheiden.</span><span class="sxs-lookup"><span data-stu-id="61095-104">Viewers will use the content to help them choose the beach with the best surfing conditions.</span></span> <span data-ttu-id="61095-105">Sie verfolgen die folgenden Ziele im Hinblick auf die Features und das Design:</span><span class="sxs-lookup"><span data-stu-id="61095-105">Your list of design and feature goals is:</span></span>

- <span data-ttu-id="61095-106">Videoinhalte müssen schnell geladen werden.</span><span class="sxs-lookup"><span data-stu-id="61095-106">Video content must load quickly</span></span>
- <span data-ttu-id="61095-107">Die Website muss mit unerwarteten Lastspitzen beim Upload umgehen können.</span><span class="sxs-lookup"><span data-stu-id="61095-107">The site must handle unexpected spikes in upload volume</span></span>
- <span data-ttu-id="61095-108">Veraltete Inhalte werden entfernt, wenn sich die Surfbedingungen ändern. Damit wird sichergestellt, dass immer die aktuellen Bedingungen auf der Website angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="61095-108">Outdated content will be removed as surf conditions change so the site always shows current conditions</span></span>

<span data-ttu-id="61095-109">Sie entscheiden sich für eine Implementierung, die hochgeladene Inhalte in einer Azure Queue Storage-Warteschlange für die Verarbeitung puffert und diese anschließend zur Speicherung in Azure Blob Storage verschiebt.</span><span class="sxs-lookup"><span data-stu-id="61095-109">You decide on an implementation that buffers uploaded content in an Azure Queue for processing and then moves it into an Azure Blob for storage.</span></span> <span data-ttu-id="61095-110">Sie benötigen nun ein Speicherkonto, das sowohl Warteschlangen als auch Blobs aufnehmen kann, während Inhalte mit niedriger Latenz übertragen werden.</span><span class="sxs-lookup"><span data-stu-id="61095-110">You need a storage account that can hold both Queues and Blobs while delivering low-latency access to your content.</span></span>

## <a name="exercise-steps"></a><span data-ttu-id="61095-111">Schritte in dieser Übung</span><span class="sxs-lookup"><span data-stu-id="61095-111">Exercise steps</span></span>

### <a name="launch-the-blade"></a><span data-ttu-id="61095-112">Aufrufen des Blatts</span><span class="sxs-lookup"><span data-stu-id="61095-112">Launch the blade</span></span>

1. <span data-ttu-id="61095-113">Rufen Sie in Ihrem Webbrowser das [Azure-Portal](https://portal.azure.com?azure-portal=true) auf, und melden Sie sich bei Ihrem Konto an.</span><span class="sxs-lookup"><span data-stu-id="61095-113">In your web browser, navigate to the [Azure Portal](https://portal.azure.com?azure-portal=true) and sign into your account.</span></span>

1. <span data-ttu-id="61095-114">Klicken Sie in der linken Randleiste auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="61095-114">In the left sidebar, select **Create a resource**.</span></span>

1. <span data-ttu-id="61095-115">Klicken Sie auf die Überschrift **Storage** im Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="61095-115">Select the **Storage** heading in the Azure Marketplace.</span></span>

1. <span data-ttu-id="61095-116">Klicken Sie auf **Speicherkonto**.</span><span class="sxs-lookup"><span data-stu-id="61095-116">Select **Storage account**.</span></span> <span data-ttu-id="61095-117">Im Portal wird das Blatt **Speicherkonto erstellen** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="61095-117">The portal will display the **Create storage account** blade.</span></span>

### <a name="configure-the-basic-options"></a><span data-ttu-id="61095-118">Konfigurieren der grundlegenden Optionen</span><span class="sxs-lookup"><span data-stu-id="61095-118">Configure the basic options</span></span>

1. <span data-ttu-id="61095-119">Klicken Sie oben auf dem Blatt auf die Registerkarte **Basics** (Grundeinstellungen).</span><span class="sxs-lookup"><span data-stu-id="61095-119">Select the **Basics** tab at the top of the blade.</span></span>

1. <span data-ttu-id="61095-120">**Abonnement:** Wählen Sie eines Ihrer Abonnements aus.</span><span class="sxs-lookup"><span data-stu-id="61095-120">**Subscription**: Select one of your subscriptions.</span></span>

1. <span data-ttu-id="61095-121">**Ressourcengruppe:** Erstellen Sie eine neue Ressourcengruppe mit dem Namen **SurfReportResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="61095-121">**Resource group**: Create a new resource group named **SurfReportResourceGroup**.</span></span>

1. <span data-ttu-id="61095-122">**Speicherkontoname:** Geben Sie einen global eindeutigen Wert ein, der sich beispielsweise aus `surfreport`, Ihren Initialen und einer Zahl zusammensetzt.</span><span class="sxs-lookup"><span data-stu-id="61095-122">**Storage account name**: Enter a globally-unique value like `surfreport` + your initials + a number.</span></span>

 1. <span data-ttu-id="61095-123">**Speicherort:** Wählen Sie **USA, Westen** aus.</span><span class="sxs-lookup"><span data-stu-id="61095-123">**Location**: Select **West US**.</span></span>

    <span data-ttu-id="61095-124">Begründung: Die Anwendung ist für Benutzer in Südkalifornien vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="61095-124">Rationale: The application is intended for users in southern California.</span></span> <span data-ttu-id="61095-125">Zur Minimierung der Latenz beim Laden von Videos sollten die Blobs in der Nähe dieser Benutzer gehostet werden. Daher ist **USA, Westen** in diesem Fall eine gute Wahl.</span><span class="sxs-lookup"><span data-stu-id="61095-125">To minimize latency when loading videos, the Blobs should be hosted close to these users; this makes **West US** a good choice.</span></span>

1. <span data-ttu-id="61095-126">**Bereitstellungsmodell:** Wählen Sie **Resource Manager** aus.</span><span class="sxs-lookup"><span data-stu-id="61095-126">**Deployment model**: Select **Resource manager**.</span></span>
    
    <span data-ttu-id="61095-127">Begründung: **Resource Manager** ist geeignet, da Sie damit eine Ressourcengruppe verwenden können, um beispielsweise die Web-App und das Speicherkonto für die Anwendung zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="61095-127">Rationale: **Resource manager** is appropriate because it will let you use a resource group to manage the Web App, storage account, etc. for the application.</span></span>

1. <span data-ttu-id="61095-128">**Leistung:** Wählen Sie **Standard** aus.</span><span class="sxs-lookup"><span data-stu-id="61095-128">**Performance**: Select **Standard**.</span></span>

    <span data-ttu-id="61095-129">Begründung: Sie können die Option **Premium** nicht auswählen, da hierdurch nur Seitenblobs für das Speicherkonto verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="61095-129">Rationale: You cannot use the **Premium** option because it would limit the storage account to page Blobs.</span></span> <span data-ttu-id="61095-130">Sie benötigen für Ihre Videos jedoch Blockblobs und zur Pufferung Warteschlangen. Beides ist nur verfügbar, wenn Sie die Option **Standard** auswählen.</span><span class="sxs-lookup"><span data-stu-id="61095-130">You need block Blobs for your videos and a Queue for buffering both of which are only available in the **Standard** option.</span></span>

1. <span data-ttu-id="61095-131">**Kontoart:** Wählen Sie **StorageV2 (general purpose v2)** (StorageV2 (allgemein, Version 2)) aus.</span><span class="sxs-lookup"><span data-stu-id="61095-131">**Account kind**: Select **StorageV2 (general purpose v2)**.</span></span>

    <span data-ttu-id="61095-132">Begründung: **StorageV2 (general purpose v2)** (StorageV2 (allgemein, Version 2)) ist hier die richtige Wahl.</span><span class="sxs-lookup"><span data-stu-id="61095-132">Rationale: **StorageV2 (general purpose v2)** is the right choice here.</span></span> <span data-ttu-id="61095-133">Sie benötigen sowohl Blobs als auch eine Warteschlange. Die Option **Blob-Speicher** kann daher nicht verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="61095-133">You need a mix of Blobs and a Queue, so the **Blob storage** option will not work.</span></span> <span data-ttu-id="61095-134">Für diese Anwendung ergäben sich beim Auswählen des Kontotyps **Speicher (Allgemein v1)** keine Vorteile, da hierdurch die Anzahl der verfügbaren Features beschränkt würde. Außerdem wäre es unwahrscheinlich, dass Sie so die Kosten für die erwartete Arbeitsauslastung reduzieren können.</span><span class="sxs-lookup"><span data-stu-id="61095-134">For this application, there would be no benefit to choosing a **Storage (general purpose v1)** account since that would limit the features you could access and would be unlikely to reduce the cost of your expected workload.</span></span>

1. <span data-ttu-id="61095-135">**Replikation:** Wählen Sie **Lokal redundanter Speicher (LRS)** aus.</span><span class="sxs-lookup"><span data-stu-id="61095-135">**Replication**: Select **Locally-redundant storage (LRS)**.</span></span>

    <span data-ttu-id="61095-136">Begründung: Die Bilder und Videos veralten schnell und werden dann von der Website entfernt.</span><span class="sxs-lookup"><span data-stu-id="61095-136">Rationale: The images and videos quickly become out-of-date and are removed from the site.</span></span> <span data-ttu-id="61095-137">Die Zusatzkosten globaler Redundanz würden hier zu keinem Mehrwert führen.</span><span class="sxs-lookup"><span data-stu-id="61095-137">This means there is little value to paying extra for global redundancy.</span></span> <span data-ttu-id="61095-138">Wenn es durch einen Notfall zu einem Datenverlust käme, könnten Sie die Website mit neuen Benutzerinhalten neu starten.</span><span class="sxs-lookup"><span data-stu-id="61095-138">If a catastrophic event results in data loss, you can restart the site with fresh content from your users.</span></span>

1. <span data-ttu-id="61095-139">**Zugriffsebene (Standard)**: Wählen Sie **Hot** (Heiße Ebene) aus.</span><span class="sxs-lookup"><span data-stu-id="61095-139">**Access tier (default)**: Select **Hot**.</span></span>
   
    <span data-ttu-id="61095-140">Begründung: Videos sollen schnell geladen werden. Daher muss die Hochleistungsoption für Blobs ausgewählt werden.</span><span class="sxs-lookup"><span data-stu-id="61095-140">Rationale: You want the videos to load quickly so you will use the high-performance option for your Blobs.</span></span>
   
<span data-ttu-id="61095-141">Auf dem folgenden Screenshot werden alle vorgenommenen Einstellungen für die Registerkarte **Basics** (Grundeinstellungen) angezeigt.</span><span class="sxs-lookup"><span data-stu-id="61095-141">The following screenshot shows the completed settings for the **Basics** tab.</span></span>

![Screenshot des Blatts „Speicherkonto erstellen“ mit ausgewählter Registerkarte **Basics** (Grundlagen)](../media-drafts/5-create-storage-account-basics.png)

### <a name="configure-the-advanced-options"></a><span data-ttu-id="61095-143">Konfigurieren der erweiterten Optionen</span><span class="sxs-lookup"><span data-stu-id="61095-143">Configure the advanced options</span></span>

1. <span data-ttu-id="61095-144">Klicken Sie oben auf dem Blatt auf die Registerkarte **Erweitert**.</span><span class="sxs-lookup"><span data-stu-id="61095-144">Select the **Advanced** tab at the top of the blade.</span></span>

1. <span data-ttu-id="61095-145">**Sichere Übertragung erforderlich:** Wählen Sie **Aktiviert** aus.</span><span class="sxs-lookup"><span data-stu-id="61095-145">**Secure transfer required**: Select **Enabled**.</span></span>

    <span data-ttu-id="61095-146">Begründung: HTTPS-Übertragungen gehören in der Regel zu den Best Practices.</span><span class="sxs-lookup"><span data-stu-id="61095-146">Rationale: Https across the wire is generally considered best practice.</span></span>

1. <span data-ttu-id="61095-147">**Virtuelle Netzwerke:** Wählen Sie **Deaktiviert** aus.</span><span class="sxs-lookup"><span data-stu-id="61095-147">**Virtual Networks**: Select **Disabled**.</span></span>

    <span data-ttu-id="61095-148">Begründung: Der Inhalt ist öffentlich verfügbar. Sie müssen daher den Zugriff über öffentliche Clients zulassen.</span><span class="sxs-lookup"><span data-stu-id="61095-148">Rationale: The content is public facing and you need to allow access from public clients.</span></span>

<span data-ttu-id="61095-149">Auf dem folgenden Screenshot werden alle vorgenommenen Einstellungen für die Registerkarte **Erweitert** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="61095-149">The following screenshot shows the completed settings for the **Advanced** tab.</span></span>

![Screenshot des Blatts „Speicherkonto erstellen“ mit ausgewählter Registerkarte **Erweitert**](../media-drafts/5-create-storage-account-advanced.png)

### <a name="create"></a><span data-ttu-id="61095-151">Erstellen</span><span class="sxs-lookup"><span data-stu-id="61095-151">Create</span></span>

1. <span data-ttu-id="61095-152">Klicken Sie unten auf dem Blatt auf **Überprüfen + erstellen**.</span><span class="sxs-lookup"><span data-stu-id="61095-152">Click the **Review + create** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="61095-153">Klicken Sie auf dem nächsten Bildschirm unten auf dem Blatt auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="61095-153">On the next screen, click the **Create** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="61095-154">Warten Sie, bis die Ressource erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="61095-154">Wait for the resource to be created.</span></span>

### <a name="verify"></a><span data-ttu-id="61095-155">Überprüfen</span><span class="sxs-lookup"><span data-stu-id="61095-155">Verify</span></span>

1. <span data-ttu-id="61095-156">Klicken Sie in der linken Randleiste auf den Link **Speicherkonten**.</span><span class="sxs-lookup"><span data-stu-id="61095-156">Select the **Storage accounts** link in the left sidebar.</span></span>

1. <span data-ttu-id="61095-157">Suchen Sie das neue Speicherkonto in der Liste, um zu überprüfen, ob die Erstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="61095-157">Locate the new storage account in the list to verify that creation succeeded.</span></span>

### <a name="clean-up"></a><span data-ttu-id="61095-158">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="61095-158">Clean up</span></span>

1. <span data-ttu-id="61095-159">Klicken Sie in der linken Randleiste auf den Link **Ressourcengruppen**.</span><span class="sxs-lookup"><span data-stu-id="61095-159">Select the **Resource groups** link in the left sidebar.</span></span>

1. <span data-ttu-id="61095-160">Suchen Sie **SurfReportResourceGroup** in der Liste.</span><span class="sxs-lookup"><span data-stu-id="61095-160">Locate **SurfReportResourceGroup** in the list.</span></span>

1. <span data-ttu-id="61095-161">Klicken Sie mit der rechten Maustaste auf den Eintrag **SurfReportResourceGroup**, und wählen Sie aus dem Kontextmenü **Ressourcengruppe löschen** aus.</span><span class="sxs-lookup"><span data-stu-id="61095-161">Right-click on the **SurfReportResourceGroup** entry and select **Delete resource group** from the context menu.</span></span>

1. <span data-ttu-id="61095-162">Geben Sie den Namen der Ressourcengruppe in das Bestätigungsfeld ein.</span><span class="sxs-lookup"><span data-stu-id="61095-162">Type the resource group name into the confirmation field.</span></span>

1. <span data-ttu-id="61095-163">Klicken Sie auf die Schaltfläche **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="61095-163">Click the **Delete** button.</span></span>

## <a name="summary"></a><span data-ttu-id="61095-164">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="61095-164">Summary</span></span>

<span data-ttu-id="61095-165">Sie haben ein Speicherkonto erstellt und die zugehörigen Einstellungen an Ihre geschäftlichen Anforderungen angepasst.</span><span class="sxs-lookup"><span data-stu-id="61095-165">You created a storage account with settings driven by your business requirements.</span></span> <span data-ttu-id="61095-166">Beispielsweise haben Sie für das Rechenzentrum die Region „USA, Westen“ ausgewählt, weil Ihre Kunden sich in erster Linie in Südkalifornien befinden.</span><span class="sxs-lookup"><span data-stu-id="61095-166">For example, you selected a West US datacenter because your customers were primarily located in southern California.</span></span> <span data-ttu-id="61095-167">Dieser Ablauf ist typisch: Zunächst analysieren Sie Ihre Daten und Ziele, und anschließend konfigurieren Sie die entsprechenden Optionen für das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="61095-167">This is a typical flow: first analyze your data and goals and then configure the storage account options to match.</span></span>