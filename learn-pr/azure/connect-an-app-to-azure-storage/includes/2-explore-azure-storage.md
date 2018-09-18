<span data-ttu-id="7d5e3-101">Zunächst werfen wir einen kurzen Blick auf die Azure-Speicherdienste, -Datenformate und -Konten.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-101">Let's start by taking a quick look at Azure storage services, data styles, and accounts.</span></span> 

<span data-ttu-id="7d5e3-102">Microsoft Azure Storage ist ein verwalteter Dienst, der die permanente, sichere und skalierbare Speicherung in der Cloud ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-102">Microsoft Azure Storage is a managed service that provides durable, secure, and scalable storage in the cloud.</span></span> <span data-ttu-id="7d5e3-103">Diese Begriffe werden nun einzeln beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-103">Let's break those terms down.</span></span>

| | |
|-|-|
| <span data-ttu-id="7d5e3-104">**Permanent**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-104">**Durable**</span></span> | <span data-ttu-id="7d5e3-105">Mithilfe von Redundanz wird sichergestellt, dass Ihre Daten sicher sind, falls es zu vorübergehenden Hardwareausfällen kommt.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-105">Redundancy ensures that your data is safe in the event of transient hardware failures.</span></span> <span data-ttu-id="7d5e3-106">Sie können Daten auch über Rechenzentren oder geografische Regionen hinweg replizieren, um eine weitere Schutzebene vor lokalen Notfällen oder Naturkatastrophen zu schaffen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-106">You can also replicate data across datacenters or geographical regions for additional protection from local catastrophe or natural disaster.</span></span> <span data-ttu-id="7d5e3-107">Daten, die auf diese Weise repliziert werden, sind bei einem unerwarteten Ausfall weiterhin hoch verfügbar.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-107">Data replicated in this way remains highly available in the event of an unexpected outage.</span></span> |
| <span data-ttu-id="7d5e3-108">**Sicher**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-108">**Secure**</span></span> | <span data-ttu-id="7d5e3-109">Alle Daten, die in Azure Storage geschrieben werden, werden vom Dienst verschlüsselt.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-109">All data written to Azure Storage is encrypted by the service.</span></span> <span data-ttu-id="7d5e3-110">Bei Azure Storage können Sie genau steuern, wer Zugriff auf Ihre Daten hat.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-110">Azure Storage provides you with fine-grained control over who has access to your data.</span></span> |
| <span data-ttu-id="7d5e3-111">**Skalierbar**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-111">**Scalable**</span></span> | <span data-ttu-id="7d5e3-112">Azure Storage ist auf hohe Skalierbarkeit ausgelegt, um die Datenspeicherungs- und Leistungsanforderungen heutiger Anwendungen zu erfüllen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-112">Azure Storage is designed to be massively scalable to meet the data storage and performance needs of today's applications.</span></span> |
| <span data-ttu-id="7d5e3-113">**Verwaltet**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-113">**Managed**</span></span> | <span data-ttu-id="7d5e3-114">Microsoft Azure übernimmt für Sie die Wartung und Behandlung aller kritischen Probleme.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-114">Microsoft Azure handles maintenance and any critical problems for you.</span></span> |

<span data-ttu-id="7d5e3-115">Unter einem einzelnen Azure-Abonnement können bis zu 200 Speicherkonten gehostet werden, die jeweils bis zu 500 TB an Daten enthalten können.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-115">A single Azure subscription can host up to 200 storage accounts, each of which can hold 500 TB of data.</span></span> <span data-ttu-id="7d5e3-116">Wenn Sie über einen Business Case verfügen, können Sie sich an das Azure Storage-Team wenden und die Genehmigung für bis zu 250 Speicherkonten unter einem Abonnement einholen. Der maximale Speicher erhöht sich hierdurch auf bis zu 125 Petabyte!</span><span class="sxs-lookup"><span data-stu-id="7d5e3-116">If you have a business case, you can talk to the Azure Storage team and get approval for up to 250 storage accounts in a subscription which pushes your max storage up to 125 Petabytes!</span></span>

## <a name="azure-data-services"></a><span data-ttu-id="7d5e3-117">Azure-Datendienste</span><span class="sxs-lookup"><span data-stu-id="7d5e3-117">Azure data services</span></span>

<span data-ttu-id="7d5e3-118">Azure Storage umfasst vier Typen von Daten.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-118">Azure storage includes four types of data.</span></span>

- <span data-ttu-id="7d5e3-119">**Blobs**: Ein extrem skalierbarer Objektspeicher für Text- und Binärdaten.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-119">**Blobs**: A massively scalable object store for text and binary data.</span></span>
- <span data-ttu-id="7d5e3-120">**Files**: Verwaltete Dateifreigaben für Bereitstellungen lokal oder in der Cloud.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-120">**Files**: Managed file shares for cloud or on-premises deployments.</span></span>
- <span data-ttu-id="7d5e3-121">**Warteschlangen**: Ein Messagingspeicher für zuverlässiges Messaging zwischen Anwendungskomponenten.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-121">**Queues**: A messaging store for reliable messaging between application components.</span></span>
- <span data-ttu-id="7d5e3-122">**Tables**: Ein NoSQL-Speicher für die schemalose Speicherung von strukturierten Daten.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-122">**Tables**: A NoSQL store for schemaless storage of structured data.</span></span> <span data-ttu-id="7d5e3-123">Dieser Dienst wurde durch Cosmos DB ersetzt und wird hier nicht beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-123">This service has been replaced by Cosmos DB and will not discussed here.</span></span>

<span data-ttu-id="7d5e3-124">Auf alle diese Datentypen kann in Azure Storage von jedem Ort der Welt aus per HTTP oder HTTPS zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-124">All of these data types in Azure Storage are accessible from anywhere in the world over HTTP or HTTPS.</span></span> <span data-ttu-id="7d5e3-125">Microsoft stellt SDKs für Azure Storage in verschiedenen Sprachen sowie eine REST-API bereit.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-125">Microsoft provides SDKs for Azure Storage in a variety of languages, as well as a REST API.</span></span> <span data-ttu-id="7d5e3-126">Sie können Ihre Daten auch direkt im Azure-Portal visuell erkunden.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-126">You can also visually explore your data right in the Azure portal.</span></span>

### <a name="blob-storage"></a><span data-ttu-id="7d5e3-127">Blobspeicher</span><span class="sxs-lookup"><span data-stu-id="7d5e3-127">Blob storage</span></span>
<span data-ttu-id="7d5e3-128">Azure-Blobspeicher ist eine Objektspeicherlösung, die für die Speicherung großer Mengen von unstrukturierten Daten, z.B. Text oder Binärdaten, optimiert ist.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-128">Azure Blob storage is an object storage solution optimized for storing massive amounts of unstructured data, such as text or binary data.</span></span> <span data-ttu-id="7d5e3-129">Blobspeicher ist für folgende Zwecke ideal geeignet:</span><span class="sxs-lookup"><span data-stu-id="7d5e3-129">Blob storage is ideal for:</span></span>

- <span data-ttu-id="7d5e3-130">Bereitstellen von Bildern oder Dokumenten direkt in einem Browser, einschließlich vollständiger statischer Websites</span><span class="sxs-lookup"><span data-stu-id="7d5e3-130">Serving images or documents directly to a browser, including full static websites.</span></span>
- <span data-ttu-id="7d5e3-131">Speichern von Dateien für verteilten Zugriff</span><span class="sxs-lookup"><span data-stu-id="7d5e3-131">Storing files for distributed access.</span></span>
- <span data-ttu-id="7d5e3-132">Video- und Audio-Streaming</span><span class="sxs-lookup"><span data-stu-id="7d5e3-132">Streaming video and audio.</span></span>
- <span data-ttu-id="7d5e3-133">Speichern von Daten für Sicherung und Wiederherstellung, Notfallwiederherstellung und Archivierung</span><span class="sxs-lookup"><span data-stu-id="7d5e3-133">Storing data for backup and restore, disaster recovery, and archiving.</span></span>
- <span data-ttu-id="7d5e3-134">Speichern von Daten für Analysen durch einen lokalen oder von Azure gehosteten Dienst</span><span class="sxs-lookup"><span data-stu-id="7d5e3-134">Storing data for analysis by an on-premises or Azure-hosted service.</span></span>

<span data-ttu-id="7d5e3-135">Azure Storage unterstützt drei Arten von Blobs:</span><span class="sxs-lookup"><span data-stu-id="7d5e3-135">Azure Storage supports three kinds of blobs:</span></span>

| <span data-ttu-id="7d5e3-136">Blobtyp</span><span class="sxs-lookup"><span data-stu-id="7d5e3-136">Blob type</span></span> | <span data-ttu-id="7d5e3-137">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7d5e3-137">Description</span></span> |
|-----------|-------------|
| <span data-ttu-id="7d5e3-138">**Blockblobs**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-138">**Block blobs**</span></span> | <span data-ttu-id="7d5e3-139">Blockblobs werden für Text- oder Binärdateien mit einer Größe von bis zu 5 TB (50.000 Blöcke mit 100 MB) verwendet.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-139">Block blobs are used to hold text or binary files up to ~5 TB (50,000 blocks of 100 MB) in size.</span></span> <span data-ttu-id="7d5e3-140">Der wichtigste Anwendungsfall für Blockblobs ist die Speicherung von Dateien, die von Anfang bis Ende gelesen werden, z.B. Mediendateien oder Imagedateien für Websites.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-140">The primary use case for block blobs is the storage of files that are read from beginning to end, such as media files or image files for websites.</span></span> <span data-ttu-id="7d5e3-141">Sie werden als Blockblobs bezeichnet, weil Dateien, die größer als 100 MB sind, als kleine Blöcke hochgeladen werden müssen, die dann zu einem endgültigen Blob zusammengefasst (committet) werden.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-141">They are named block blobs because files larger than 100 MB must be uploaded as small blocks, which are then consolidated (or committed) into the final blob.</span></span> |
| <span data-ttu-id="7d5e3-142">**Seitenblobs**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-142">**Page blobs**</span></span> | <span data-ttu-id="7d5e3-143">Seitenblobs werden für Random-Access-Dateien mit einer Größe von bis zu 8 TB verwendet.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-143">Page blobs are used to hold random-access files up to 8 TB in size.</span></span> <span data-ttu-id="7d5e3-144">Seitenblobs werden hauptsächlich als Hintergrundspeicher für die VHDs verwendet, die zum Bereitstellen von dauerhaften Datenträgern für Azure Virtual Machines (Azure VMs) genutzt werden.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-144">Page blobs are used primarily as the backing storage for the VHDs used to provide durable disks for Azure Virtual Machines (Azure VMs).</span></span> <span data-ttu-id="7d5e3-145">Sie werden als Seitenblobs bezeichnet, da sie zufälligen Lese-/Schreibzugriff auf 512-Byte-Seiten ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-145">They are named page blobs because they provide random read/write access to 512-byte pages.</span></span> |
| <span data-ttu-id="7d5e3-146">**Anfügeblobs**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-146">**Append blobs**</span></span> | <span data-ttu-id="7d5e3-147">Anfügeblobs bestehen wie Blockblobs auch aus Blöcken, aber sie sind für Anfügevorgänge optimiert.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-147">Append blobs are made up of blocks like block blobs, but they are optimized for append operations.</span></span> <span data-ttu-id="7d5e3-148">Diese werden häufig eingesetzt, um Informationen aus mindestens einer Quelle in demselben Blob zu protokollieren.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-148">These are frequently used for logging information from one or more sources into the same blob.</span></span> <span data-ttu-id="7d5e3-149">Beispielsweise können Sie die gesamte Protokollierung der Ablaufverfolgung für eine Anwendung, die auf mehreren VMs ausgeführt wird, in dasselbe Anfügeblob schreiben.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-149">For example, you might write all of your trace logging to the same append blob for an application running on multiple VMs.</span></span> <span data-ttu-id="7d5e3-150">Ein einzelnes Anfügeblob kann eine maximale Größe von 195 GB haben.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-150">A single append blob can be up to 195 GB.</span></span> |

### <a name="files"></a><span data-ttu-id="7d5e3-151">Files</span><span class="sxs-lookup"><span data-stu-id="7d5e3-151">Files</span></span>
<span data-ttu-id="7d5e3-152">Azure Files ermöglicht die Einrichtung hochverfügbarer Netzwerkdateifreigaben, auf die über das standardmäßige SMB-Protokoll (Server Message Block) zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-152">Azure Files enables you to set up highly available network file shares that can be accessed by using the standard Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="7d5e3-153">Dadurch können mehrere virtuelle Computer gemeinsam die gleichen Dateien mit Lese- und Schreibzugriff nutzen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-153">That means that multiple VMs can share the same files with both read and write access.</span></span> <span data-ttu-id="7d5e3-154">Die Dateien können auch mithilfe der REST-Schnittstelle oder mithilfe der Speicherclientbibliotheken gelesen werden.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-154">You can also read the files using the REST interface or the storage client libraries.</span></span> <span data-ttu-id="7d5e3-155">Sie können eine eindeutige URL auch einer beliebigen Datei zuordnen, um für einen festgelegten Zeitraum den präzisen Zugriff auf eine private Datei zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-155">You can also associate a unique URL to any file to allow fine-grained access to a private file for a set period of time.</span></span> <span data-ttu-id="7d5e3-156">Dateifreigaben können in zahlreichen Szenarien verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="7d5e3-156">File shares can be used for many common scenarios:</span></span>

- <span data-ttu-id="7d5e3-157">Speichern von freigegebenen Konfigurationsdateien für VMs, Tools oder Hilfsprogramme, damit alle Benutzer die gleiche Version verwenden</span><span class="sxs-lookup"><span data-stu-id="7d5e3-157">Storing shared configuration files for VMs, tools, or utilities so that everyone is using the same version.</span></span>
- <span data-ttu-id="7d5e3-158">Protokollieren von Dateien, z.B. Diagnose, Metriken und Absturzabbilder</span><span class="sxs-lookup"><span data-stu-id="7d5e3-158">Log files such as diagnostics, metrics, and crash dumps.</span></span>
- <span data-ttu-id="7d5e3-159">Freigeben von Daten zwischen lokalen Anwendungen und virtuellen Azure-Computern, um die Migration von Apps in die Cloud für einen bestimmten Zeitraum zuzulassen</span><span class="sxs-lookup"><span data-stu-id="7d5e3-159">Shared data between on-premises applications and Azure VMs to allow migration of apps to the cloud over a period of time.</span></span>

### <a name="queues"></a><span data-ttu-id="7d5e3-160">Warteschlangen</span><span class="sxs-lookup"><span data-stu-id="7d5e3-160">Queues</span></span>
<span data-ttu-id="7d5e3-161">Der Azure-Warteschlangendienst wird zum Speichern und Abrufen von Nachrichten verwendet.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-161">The Azure Queue service is used to store and retrieve messages.</span></span> <span data-ttu-id="7d5e3-162">Warteschlangennachrichten können eine Größe von bis zu 64 KB haben, und eine Warteschlange kann Millionen von Nachrichten enthalten.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-162">Queue messages can be up to 64 KB in size, and a queue can contain millions of messages.</span></span> <span data-ttu-id="7d5e3-163">Warteschlangen dienen im Allgemeinen zum Speichern von Listen mit Nachrichten, die asynchron verarbeitet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-163">Queues are generally used to store lists of messages to be processed asynchronously.</span></span>

<span data-ttu-id="7d5e3-164">Sie können Warteschlangen verwenden, um unterschiedliche Teile Ihrer Anwendung lose zu verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-164">You can use queues to loosely connect different parts of your application together.</span></span> <span data-ttu-id="7d5e3-165">Beispielsweise können Sie die Bildverarbeitung für die Fotos durchführen, die von Ihren Benutzern hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-165">For example, we could perform image processing on the photos uploaded by our users.</span></span> <span data-ttu-id="7d5e3-166">Es kann sein, dass Sie die Gesichtserkennung oder eine Markierungsfunktion bereitstellen möchten, damit die Benutzer alle Bilder durchsuchen können, die sie unter dem Dienst gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-166">Perhaps we want to provide some sort of face detection, or tagging capability so people can search through all the images they have stored in our service.</span></span> <span data-ttu-id="7d5e3-167">Sie können Warteschlangen zum Senden von Nachrichten an den Bildverarbeitungsdienst nutzen, um anzugeben, dass neue Bilder hochgeladen wurden und bereit für die Verarbeitung sind.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-167">We could use queues to pass messages to our image processing service to let it know that new images have been uploaded and are ready for processing.</span></span> <span data-ttu-id="7d5e3-168">Diese Art der Architektur ermöglicht es Ihnen, die einzelnen Teile des Diensts unabhängig voneinander zu entwickeln und zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-168">This sort of architecture would allow you to develop and update each part of the service independently.</span></span>

## <a name="azure-storage-accounts"></a><span data-ttu-id="7d5e3-169">Azure-Speicherkonten</span><span class="sxs-lookup"><span data-stu-id="7d5e3-169">Azure storage accounts</span></span>

<span data-ttu-id="7d5e3-170">Sie müssen ein _Speicherkonto_ erstellen, um über eine Anwendung auf diese Dienste zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-170">To access any of these services from an application, you have to create a _storage account_.</span></span> <span data-ttu-id="7d5e3-171">Das Speicherkonto stellt in Azure einen eindeutigen Namespace zum Speichern Ihrer Datenobjekte sowie für den Zugriff darauf bereit.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-171">The storage account provides a unique namespace in Azure to store and access your data objects.</span></span> <span data-ttu-id="7d5e3-172">Ein Speicherkonto enthält alle Blobs, Dateien, Warteschlangen, Tabellen und VM-Datenträger, die Sie unter diesem Konto erstellen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-172">A storage account contains any blobs, files, queues, tables, and VM disks that you create under that account.</span></span>

### <a name="creating-a-storage-account"></a><span data-ttu-id="7d5e3-173">Erstellen eines Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="7d5e3-173">Creating a storage account</span></span>

<span data-ttu-id="7d5e3-174">Ein Azure-Speicherkonto kann über das Azure-Portal, mithilfe von Azure PowerShell oder über die Azure-Befehlszeilenschnittstelle erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-174">You can create an Azure storage account using the Azure portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="7d5e3-175">Azure Storage enthält drei verschiedene Kontooptionen, für die jeweils unterschiedliche Preise und unterstützte Features gelten.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-175">Azure Storage provides three distinct account options, with different pricing and features supported.</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="7d5e3-176">Kontotyp</span><span class="sxs-lookup"><span data-stu-id="7d5e3-176">Account type</span></span> | <span data-ttu-id="7d5e3-177">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7d5e3-177">Description</span></span> |
> |--------------|-------------|
> | <span data-ttu-id="7d5e3-178">**Allgemein v2 (GPv2)**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-178">**General-purpose v2 (GPv2)**</span></span> | <span data-ttu-id="7d5e3-179">Speicherkonten vom Typ „Allgemein v2 (GPv2)“ unterstützen alle aktuellen Features für Blobs, Dateien, Warteschlangen und Tabellen.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-179">General-purpose v2 (GPv2) accounts are storage accounts that support all of the latest features for blobs, files, queues, and tables.</span></span> <span data-ttu-id="7d5e3-180">Die Preise für GPv2-Konten wurden so ausgelegt, dass sich die niedrigsten Kosten pro Gigabyte ergeben.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-180">Pricing for GPv2 accounts has been designed to deliver the lowest per gigabyte prices.</span></span> |
> | <span data-ttu-id="7d5e3-181">**Allgemein v1 (GPv1)**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-181">**General-purpose v1 (GPv1)**</span></span> | <span data-ttu-id="7d5e3-182">Speicherkonten vom Typ „Allgemein v1 (GPv1)“ ermöglichen den Zugriff auf alle Azure Storage-Dienste, bieten aber ggf. nicht die aktuellen Features oder die niedrigsten GB-Preise.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-182">General-purpose v1 (GPv1) accounts provide access to all Azure Storage services, but may not have the latest features or the lowest per gigabyte pricing.</span></span> <span data-ttu-id="7d5e3-183">Beispielsweise werden die Speicherebenen „Cool“ und „Archiv“ in GPv1 nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-183">For example, cool storage and archive storage are not supported in GPv1.</span></span> <span data-ttu-id="7d5e3-184">Die Preise für GPv1-Transaktionen sind niedriger, sodass Workloads mit hohen Datenänderungs- oder Leseraten ggf. von der Nutzung dieses Kontotyps profitieren.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-184">Pricing is lower for GPv1 transactions, so workloads with high churn or high read rates may benefit from this account type.</span></span> |
> | <span data-ttu-id="7d5e3-185">**Blobspeicherkonten**</span><span class="sxs-lookup"><span data-stu-id="7d5e3-185">**Blob storage accounts**</span></span> | <span data-ttu-id="7d5e3-186">Blobspeicherkonten stellen einen älteren Kontotyp dar und unterstützen alle Blockblobfeatures, die auch für GPv2 unterstützt werden, aber sie sind ausschließlich auf die Unterstützung von Block- und Anfügeblobs beschränkt.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-186">A legacy account type, blob storage accounts support all the same block blob features as GPv2, but are limited to supporting only block and append blobs.</span></span> <span data-ttu-id="7d5e3-187">Die Preise sind weitestgehend mit den Preisen für allgemeine Konten vom Typ „Allgemein v2“ identisch.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-187">Pricing is broadly similar to pricing for general-purpose v2 accounts.</span></span> |
    
<span data-ttu-id="7d5e3-188">Wenn Sie daran interessiert sind, mehr über die Erstellung von Speicherkonten zu erfahren, hilft Ihnen das Modul **Erstellen eines Azure-Speicherkontos** im Lernportal weiter.</span><span class="sxs-lookup"><span data-stu-id="7d5e3-188">If you are interested in learning more about creating storage accounts, make sure to go through the **Create an Azure storage account** module in the learning portal.</span></span>