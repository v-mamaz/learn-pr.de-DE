<span data-ttu-id="7ec4e-101">So sieht der typische Workflow für Apps aus, die Azure Blob Storage verwenden:</span><span class="sxs-lookup"><span data-stu-id="7ec4e-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="7ec4e-102">**Abrufen der Konfiguration**: Laden Sie beim Start die Konfiguration des Speicherkontos.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-102">**Retrieve configuration**: At startup, load the storage account configuration.</span></span> <span data-ttu-id="7ec4e-103">Dies ist in der Regel eine Verbindungszeichenfolge für das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-103">This is typically a storage account connection string.</span></span>

1. <span data-ttu-id="7ec4e-104">**Initialisieren des Clients**: Verwenden Sie die Verbindungszeichenfolge, um die Azure Storage-Clientbibliothek zu initialisieren.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="7ec4e-105">Dabei werden Objekte erstellt, die die App für die Arbeit mit der Blob Storage-API verwendet.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-105">This creates the objects the app will use to work with the Blob storage API.</span></span>

1. <span data-ttu-id="7ec4e-106">**Verwenden**: Führen Sie API-Aufrufe mit der Clientbibliothek aus, um mit Containern und Blobs zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="7ec4e-107">Konfigurieren der Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="7ec4e-107">Configure your connection string</span></span>

<span data-ttu-id="7ec4e-108">Bevor Sie Code schreiben, benötigen Sie die Verbindungszeichenfolge für das von Ihnen verwendete Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-108">Before writing any code, you'll need the connection string for the storage account you will use.</span></span>

<span data-ttu-id="7ec4e-109">Diese enthält den Kontoschlüssel.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-109">Storage account connection strings include the account key.</span></span> <span data-ttu-id="7ec4e-110">Der Kontoschlüssel gilt als geheim und sollte sicher aufbewahrt werden.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-110">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="7ec4e-111">Hier speichern wir die Verbindungszeichenfolge in einer App Service-Anwendungseinstellung.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-111">Here, we will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="7ec4e-112">App Service-Anwendungseinstellungen sind ein sicherer Ort für Anwendungsgeheimnisse. Dieser Ansatz unterstützt jedoch keine lokale Entwicklung und ist keine robuste, eigenständige End-to-End-Lösung.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-112">App Service application settings are a secure place for application secrets, but this design does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="7ec4e-113">**Platzieren Sie Speicherkontoschlüssel nicht im Code oder in ungeschützten Konfigurationsdateien.**</span><span class="sxs-lookup"><span data-stu-id="7ec4e-113">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="7ec4e-114">Speicherkontoschlüssel ermöglichen Vollzugriff auf Ihr Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-114">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="7ec4e-115">Der Verlust eines Schlüssels kann zu nicht behebbaren Schäden und hohen Rechnungen führen.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-115">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="7ec4e-116">Im Abschnitt „Weitere nützliche Informationen“ am Ende dieses Moduls finden Sie eine Anleitung zum Speichern und Hinweise zum Wiederherstellen verlorener Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-116">See the Further Reading section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="7ec4e-117">Initialisieren des Blob Storage-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="7ec4e-117">Initialize the Blob storage object model</span></span>

<span data-ttu-id="7ec4e-118">Im Azure Storage SDK für .NET Core besteht das Standardmuster für die Verwendung von Blob Storage aus den folgenden Schritten:</span><span class="sxs-lookup"><span data-stu-id="7ec4e-118">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="7ec4e-119">Rufen Sie `CloudStorageAccount.Parse` (oder `TryParse`) mit Ihrer Verbindungszeichenfolge auf, um `CloudStorageAccount` abzurufen.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-119">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>

1. <span data-ttu-id="7ec4e-120">Rufen Sie `CreateCloudBlobClient` im `CloudStorageAccount` auf, um `CloudBlobClient` abzurufen.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-120">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>

1. <span data-ttu-id="7ec4e-121">Rufen Sie `GetContainerReference` im `CloudBlobClient` auf, um `CloudBlobContainer` abzurufen.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-121">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>

1. <span data-ttu-id="7ec4e-122">Verwenden Sie Methoden für den Container, um eine Liste von Blobs und/oder Referenzen für einzelne Blobs zum Hoch- und Herunterladen von Daten abzurufen.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-122">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="7ec4e-123">Im Code sehen die Schritte 1&ndash;3 so aus:</span><span class="sxs-lookup"><span data-stu-id="7ec4e-123">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="7ec4e-124">Keiner dieser Initialisierungscodes führt Aufrufe über das Netzwerk durch.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-124">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="7ec4e-125">Das bedeutet, dass einige Ausnahmen, die aufgrund fehlerhafter Informationen auftreten, erst zu einem späteren Zeitpunkt ausgelöst werden.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-125">This means that some exceptions that occur because of incorrect information won't be thrown until later.</span></span> <span data-ttu-id="7ec4e-126">Der Aufruf von `CloudStorageAccount.Parse` löst beispielsweise sofort eine Ausnahme aus, wenn die Verbindungszeichenfolge falsch formatiert ist. Es wird jedoch keine Ausnahme ausgelöst, wenn das Speicherkonto, auf das eine Verbindungszeichenfolge verweist, nicht vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-126">For example, the call to `CloudStorageAccount.Parse` will throw an exception immediately if the connection string is formatted incorrectly, but no exception will be thrown if the storage account that a connection string points to doesn't exist.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="7ec4e-127">Erstellen von Containern beim Start</span><span class="sxs-lookup"><span data-stu-id="7ec4e-127">Create containers at startup</span></span>

<span data-ttu-id="7ec4e-128">Das Aufrufen von `CreateIfNotExistsAsync` für einen `CloudBlobContainer` ist die beste Methode, einen Container zu erstellen, wenn Ihre Anwendung gestartet wird oder wenn sie zum ersten Mal versucht, ihn zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-128">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to create a container when your application starts or when it first tries to use it.</span></span>

<span data-ttu-id="7ec4e-129">`CreateIfNotExistsAsync` löst keine Ausnahme aus, wenn der Container bereits vorhanden ist, veranlasst aber einen Netzwerkaufruf an Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-129">`CreateIfNotExistsAsync` won't throw an exception if the container already exists, but it does make a network call to Azure Storage.</span></span> <span data-ttu-id="7ec4e-130">Rufen Sie dieses Element einmalig während der Initialisierung auf, nicht bei jedem Versuch, einen Container zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-130">Call it once during initialization, not every time you try to use a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="7ec4e-131">Übung</span><span class="sxs-lookup"><span data-stu-id="7ec4e-131">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="7ec4e-132">Klonen und Untersuchen nicht fertiger Apps</span><span class="sxs-lookup"><span data-stu-id="7ec4e-132">Clone and explore the unfinished app</span></span>

<span data-ttu-id="7ec4e-133">Klonen Sie zuerst die Start-App aus GitHub.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-133">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="7ec4e-134">Führen Sie im Cloud Shell-Terminal den folgenden Befehl aus, um eine Kopie des Quellcodes zu erstellen und im Editor zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="7ec4e-134">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

<span data-ttu-id="7ec4e-135">**TODO update to final repo URL**</span><span class="sxs-lookup"><span data-stu-id="7ec4e-135">**TODO update to final repo URL**</span></span>

```console
git clone https://github.com/nickwalkmsft/FileUploader.git
cd FileUploader
code .
```

<span data-ttu-id="7ec4e-136">Öffnen Sie die Datei `Controllers/FilesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-136">Open the file `Controllers/FilesController.cs`.</span></span> <span data-ttu-id="7ec4e-137">Hier gibt es nichts zu tun, aber wir werfen einen kurzen Blick darauf, was die App macht.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-137">There's no work to do here, but we're going to have a quick look at what the app does.</span></span>

<span data-ttu-id="7ec4e-138">Dieser Controller implementiert eine API mit drei Aktionen:</span><span class="sxs-lookup"><span data-stu-id="7ec4e-138">This controller implements an API with three actions:</span></span>

- <span data-ttu-id="7ec4e-139">**Index** (GET/API/Dateien) gibt eine Liste von URLs zurück – eine für jede hochgeladene Datei.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-139">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="7ec4e-140">Das App-Front-End ruft diese Methode auf, um eine Liste von Hyperlinks zu den hochgeladenen Dateien zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-140">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
- <span data-ttu-id="7ec4e-141">**Hochladen** (POST/API/Dateien) empfängt eine hochgeladene Datei und speichert sie.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-141">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
- <span data-ttu-id="7ec4e-142">**Herunterladen** (GET/API/Dateien/{Dateiname}) lädt eine einzelne Datei nach ihrem Namen herunter.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-142">**Download** (GET /api/Files/{filename}) downloads an individual file by its name.</span></span>

<span data-ttu-id="7ec4e-143">Jede Methode verwendet eine `IStorage`-Instanz mit der Bezeichnung `storage`.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-143">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="7ec4e-144">Es gibt eine unvollständige Implementierung von `IStorage` in `Models/BlobStorage.cs`, die wir vervollständigen.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-144">There is an incomplete implementation of `IStorage` in `Models/BlobStorage.cs` that we're going to fill in.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="7ec4e-145">Hinzufügen des NuGet-Pakets</span><span class="sxs-lookup"><span data-stu-id="7ec4e-145">Add the NuGet package</span></span>

<span data-ttu-id="7ec4e-146">Fügen Sie zunächst einen Verweis auf das Azure Storage SDK hinzu.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-146">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="7ec4e-147">Führen Sie im Terminal Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="7ec4e-147">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="7ec4e-148">So wird sichergestellt, dass Sie die neueste Version der Blob Storage-Clientbibliothek verwenden.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-148">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="7ec4e-149">Konfigurieren</span><span class="sxs-lookup"><span data-stu-id="7ec4e-149">Configure</span></span>

<span data-ttu-id="7ec4e-150">Die Konfigurationswerte, die wir für die Ausführung der App benötigen, sind die Verbindungszeichenfolge des Speicherkontos und der Name des Containers, den die App für die Speicherung von Dateien verwenden wird.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-150">The configuration values we need to run the app are the storage account connection string and the name of the container the app will use to store files.</span></span> <span data-ttu-id="7ec4e-151">In dieser Einheit führen wir die App nur in Azure App Service aus. Dabei befolgen wir die bewährten Vorgehensweisen für App Service und speichern die Werte in den Anwendungseinstellungen von App Service.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-151">In this unit, we're only going to run the app in Azure App Service, so we'll follow App Service best practice and store the values in App Service application settings.</span></span> <span data-ttu-id="7ec4e-152">Das machen wir, wenn wir die App Service-Instanz erstellen, weshalb wir im Moment nichts zu tun haben.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-152">We'll do that when we create the App Service instance, so there's nothing we need to do at the moment.</span></span>

<span data-ttu-id="7ec4e-153">Wenn es zum *Einsatz* der Konfiguration kommt, enthält unsere Einsteiger-App bereits die von uns benötigten Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-153">When it comes to *using* the configuration, our starter app already includes the plumbing we need.</span></span> <span data-ttu-id="7ec4e-154">Der `IOptions<AzureStorageConfig>`-Konstruktorparameter in `BlobStorage` hat zwei Eigenschaften: die Speicherkonto-Verbindungszeichenfolge und den Namen des Containers, in dem die App Blobs speichert.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-154">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="7ec4e-155">In der `ConfigureServices`-Methode von `Startup.cs` gibt es einen Code, der die Werte aus der Konfiguration lädt, wenn die App startet.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-155">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

### <a name="initialize"></a><span data-ttu-id="7ec4e-156">Initialisieren</span><span class="sxs-lookup"><span data-stu-id="7ec4e-156">Initialize</span></span>

<span data-ttu-id="7ec4e-157">Öffnen Sie `Models/BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-157">Open `Models/BlobStorage.cs`.</span></span> <span data-ttu-id="7ec4e-158">Fügen Sie die folgenden `using`-Anweisungen am Anfang der Datei hinzu, um sie für den Code vorzubereiten, den Sie während der Übung hinzufügen werden.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-158">Add the following `using` statements to the top of the file to prepare it for the code you're going to add during the exercise.</span></span>

```csharp
using System.Linq;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="7ec4e-159">Wechseln Sie zur `Initialize`-Methode.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-159">Locate the `Initialize` method.</span></span> <span data-ttu-id="7ec4e-160">Unsere App ruft diese Methode auf, wenn `BlobStorage` zum ersten Mal verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-160">Our app will call this method when `BlobStorage` is used for the first time.</span></span> <span data-ttu-id="7ec4e-161">`ConfigureServices` in `Startup.cs` zeigt, wie das funktioniert.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-161">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span>

<span data-ttu-id="7ec4e-162">Erstellen Sie den Container in `Initialize`, falls er nicht bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="7ec4e-162">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="7ec4e-163">Ersetzen Sie die aktuelle Implementierung von `Initialize` durch den folgenden Code, und speichern Sie Ihre Arbeit:</span><span class="sxs-lookup"><span data-stu-id="7ec4e-163">Replace the current implementation of `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```