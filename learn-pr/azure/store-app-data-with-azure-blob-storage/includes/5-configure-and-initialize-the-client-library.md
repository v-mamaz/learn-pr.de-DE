<span data-ttu-id="a340d-101">So sieht der typische Workflow für Apps aus, die Azure Blob Storage verwenden:</span><span class="sxs-lookup"><span data-stu-id="a340d-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="a340d-102">**Abrufen der Konfiguration**: Laden Sie beim Starten die Konfiguration, z.B. die Verbindungszeichenfolge mit dem Kontoschlüssel.</span><span class="sxs-lookup"><span data-stu-id="a340d-102">**Retrieve configuration**: At startup, load the configuration, such as the connection string with the account key.</span></span> <span data-ttu-id="a340d-103">Dies ist erforderlich, um API-Aufrufe zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="a340d-103">This is needed to authenticate API calls.</span></span>
1. <span data-ttu-id="a340d-104">**Initialisieren Sie den Client**: Verwenden Sie die Verbindungszeichenfolge, um die Azure Storage-Clientbibliothek zu initialisieren.</span><span class="sxs-lookup"><span data-stu-id="a340d-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="a340d-105">Dabei werden Objekte erstellt, die die App für die Arbeit mit der Blob Storage-API verwendet.</span><span class="sxs-lookup"><span data-stu-id="a340d-105">This creates the objects the app will use to work with the Blob storage API.</span></span>
1. <span data-ttu-id="a340d-106">**Verwenden**: Führen Sie API-Aufrufe mit der Clientbibliothek aus, um mit Containern und Blobs zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="a340d-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="a340d-107">Konfigurieren der Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="a340d-107">Configure your connection string</span></span>

<span data-ttu-id="a340d-108">Bevor Sie einen Code schreiben, benötigen Sie die Verbindungszeichenfolge für das von Ihnen verwendete Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="a340d-108">Before writing any code, you'll need the connection string for the storage account you will use.</span></span> 

<span data-ttu-id="a340d-109">Die Verbindungszeichenfolge enthält Ihren Kontoschlüssel.</span><span class="sxs-lookup"><span data-stu-id="a340d-109">The connection string includes your account key.</span></span> <span data-ttu-id="a340d-110">Der Kontoschlüssel gilt als geheim und sollte sicher aufbewahrt werden.</span><span class="sxs-lookup"><span data-stu-id="a340d-110">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="a340d-111">Wir speichern die Verbindungszeichenfolge in einer App Service-Anwendungseinstellung.</span><span class="sxs-lookup"><span data-stu-id="a340d-111">We will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="a340d-112">Eine Anwendungseinstellung ist ein sicherer Ort für Anwendungsgeheimnisse, unterstützt jedoch keine lokale Entwicklung und ist keine robuste, eigenständige End-to-End-Lösung.</span><span class="sxs-lookup"><span data-stu-id="a340d-112">An application setting is a secure place for application secrets, but it does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="a340d-113">**Platzieren Sie Speicherkontoschlüssel nicht im Code oder in ungeschützten Konfigurationsdateien.**</span><span class="sxs-lookup"><span data-stu-id="a340d-113">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="a340d-114">Speicherkontoschlüssel ermöglichen Vollzugriff auf Ihr Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="a340d-114">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="a340d-115">Der Verlust eines Schlüssels kann zu nicht behebbaren Schäden und hohen Rechnungen führen.</span><span class="sxs-lookup"><span data-stu-id="a340d-115">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="a340d-116">Im Abschnitt „Zusätzliche Ressourcen“ am Ende dieses Moduls finden Sie eine Anleitung zum Speichern und Hinweise zum Wiederherstellen verlorener Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="a340d-116">See the Additional Resources section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="a340d-117">Initialisieren des Blob Storage-Objektmodells</span><span class="sxs-lookup"><span data-stu-id="a340d-117">Initialize the Blob storage object model</span></span>

<span data-ttu-id="a340d-118">Im Azure Storage SDK für .NET Core besteht das Standardmuster für die Verwendung von Blob Storage aus den folgenden Schritten:</span><span class="sxs-lookup"><span data-stu-id="a340d-118">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="a340d-119">Rufen Sie `CloudStorageAccount.Parse` (oder `TryParse`) mit Ihrer Verbindungszeichenfolge auf, um `CloudStorageAccount` abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a340d-119">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>
1. <span data-ttu-id="a340d-120">Rufen Sie `CreateCloudBlobClient` im `CloudStorageAccount` auf, um `CloudBlobClient` abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a340d-120">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>
1. <span data-ttu-id="a340d-121">Rufen Sie `GetContainerReference` im `CloudBlobClient` auf, um `CloudBlobContainer` abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a340d-121">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>
1. <span data-ttu-id="a340d-122">Verwenden Sie Methoden für den Container, um eine Liste von Blobs und/oder Referenzen für einzelne Blobs zum Hoch- und Herunterladen von Daten abzurufen.</span><span class="sxs-lookup"><span data-stu-id="a340d-122">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="a340d-123">Im Code sehen die Schritte 1&ndash;3 so aus:</span><span class="sxs-lookup"><span data-stu-id="a340d-123">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="a340d-124">Keiner dieser Initialisierungscodes führt Aufrufe über das Netzwerk durch.</span><span class="sxs-lookup"><span data-stu-id="a340d-124">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="a340d-125">Das bedeutet, dass Ausnahmen, die durch falsche Informationen entstehen, erst später ausgelöst. Beispielsweise wird der Aufruf von `GetContainerReference` erfolgreich sein, unabhängig davon, ob der Container tatsächlich im Konto existiert.</span><span class="sxs-lookup"><span data-stu-id="a340d-125">This means exceptions that occur from incorrect information won't be thrown until later; for example, the call to `GetContainerReference` will succeed whether or not the container actually exists in the account.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="a340d-126">Erstellen von Containern beim Start</span><span class="sxs-lookup"><span data-stu-id="a340d-126">Create containers at startup</span></span>

<span data-ttu-id="a340d-127">Anwendungen erstellen benötigte Container in der Regel im Code, auch wenn Sie deren Funktion im Voraus kennen.</span><span class="sxs-lookup"><span data-stu-id="a340d-127">Common practice is for applications to create needed containers in code, even when we know what those containers will be up-front.</span></span> <span data-ttu-id="a340d-128">Rufen Sie `CreateIfNotExistsAsync` im `CloudBlobContainer` auf, um Container zu erstellen, von denen Sie wissen, dass Sie sie brauchen.</span><span class="sxs-lookup"><span data-stu-id="a340d-128">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to do this, and we should use it to create each container we know we'll need before we use them.</span></span>

<span data-ttu-id="a340d-129">`CreateIfNotExistsAsync` *führt* einen Netzwerkaufruf in Azure Storage aus.</span><span class="sxs-lookup"><span data-stu-id="a340d-129">`CreateIfNotExistsAsync` *does* make a network call to Azure Storage.</span></span> <span data-ttu-id="a340d-130">Am besten ist es, den Aufruf einmal beim Start auszuführen und nicht jedes Mal, wenn Sie auf einen Container zugreifen.</span><span class="sxs-lookup"><span data-stu-id="a340d-130">Best practice is to call it once at startup and not every time we access a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="a340d-131">Übung</span><span class="sxs-lookup"><span data-stu-id="a340d-131">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="a340d-132">Klonen und Untersuchen nicht fertiger Apps</span><span class="sxs-lookup"><span data-stu-id="a340d-132">Clone and explore the unfinished app</span></span>

<span data-ttu-id="a340d-133">Klonen Sie zuerst die Start-App aus GitHub.</span><span class="sxs-lookup"><span data-stu-id="a340d-133">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="a340d-134">Führen Sie im Cloud Shell-Terminal den folgenden Befehl aus, um eine Kopie des Quellcodes zu erstellen und im Editor zu öffnen:</span><span class="sxs-lookup"><span data-stu-id="a340d-134">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

```console
git clone TODO
cd TODO
code .
```

<span data-ttu-id="a340d-135">Öffnen Sie die Datei `Controllers/FilesController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a340d-135">Open the file `Controllers/FilesController.cs`.</span></span>

<span data-ttu-id="a340d-136">Dieser Controller implementiert eine API mit drei Aktionen:</span><span class="sxs-lookup"><span data-stu-id="a340d-136">This controller implements an API with three actions:</span></span>

* <span data-ttu-id="a340d-137">**Index** (GET/API/Dateien) gibt eine Liste von URLs zurück – eine für jede hochgeladene Datei.</span><span class="sxs-lookup"><span data-stu-id="a340d-137">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="a340d-138">Das App-Front-End ruft diese Methode auf, um eine Liste von Hyperlinks zu den hochgeladenen Dateien zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a340d-138">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
* <span data-ttu-id="a340d-139">**Hochladen** (POST/API/Dateien) empfängt eine hochgeladene Datei und speichert sie.</span><span class="sxs-lookup"><span data-stu-id="a340d-139">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
* <span data-ttu-id="a340d-140">**Herunterladen** (GET/API/Dateien/{Dateiname}) lädt eine einzelne Datei nach ihrem Namen herunter.</span><span class="sxs-lookup"><span data-stu-id="a340d-140">**Download** (GET /api/Files/{file-name}) downloads an individual file by its name.</span></span>

<span data-ttu-id="a340d-141">Jede Methode verwendet eine `IStorage`-Instanz mit der Bezeichnung `storage`.</span><span class="sxs-lookup"><span data-stu-id="a340d-141">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="a340d-142">Es gibt eine unvollständige Implementierung von `IStorage` in `Models/BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="a340d-142">There is an incomplete implementation of `IStorage` in  `Models/BlobStorage.cs`.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="a340d-143">Hinzufügen des NuGet-Pakets</span><span class="sxs-lookup"><span data-stu-id="a340d-143">Add the NuGet package</span></span>

<span data-ttu-id="a340d-144">Fügen Sie zunächst einen Verweis auf das Azure Storage SDK hinzu.</span><span class="sxs-lookup"><span data-stu-id="a340d-144">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="a340d-145">Führen Sie im Terminal Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="a340d-145">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="a340d-146">So wird sichergestellt, dass Sie die neueste Version der Blob Storage-Clientbibliothek verwenden.</span><span class="sxs-lookup"><span data-stu-id="a340d-146">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="a340d-147">Konfigurieren</span><span class="sxs-lookup"><span data-stu-id="a340d-147">Configure</span></span>

<span data-ttu-id="a340d-148">Die Start-App enthält bereits die erforderliche Konfigurationsinfrastruktur.</span><span class="sxs-lookup"><span data-stu-id="a340d-148">Our starter app already includes the configuration plumbing we need.</span></span> <span data-ttu-id="a340d-149">Der `IOptions<AzureStorageConfig>`-Konstruktorparameter in `BlobStorage` hat zwei Eigenschaften: die Speicherkonto-Verbindungszeichenfolge und den Namen des Containers, in dem die App Blobs speichert.</span><span class="sxs-lookup"><span data-stu-id="a340d-149">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="a340d-150">In der `ConfigureServices`-Methode von `Startup.cs` gibt es einen Code, der die Werte aus der Konfiguration lädt, wenn die App startet.</span><span class="sxs-lookup"><span data-stu-id="a340d-150">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

<span data-ttu-id="a340d-151">In dieser Übung führen Sie die App in Azure App Service aus, um die Konfigurationswerte später den App Service-Anwendungseinstellungen hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="a340d-151">In this exercise, we will run the app in Azure App Service, so we will add the configuration values to the App Service application settings later.</span></span> <span data-ttu-id="a340d-152">Im Moment sind keine Aktionen in Zusammenhang mit der Konfiguration erforderlich.</span><span class="sxs-lookup"><span data-stu-id="a340d-152">For now, we don't need to do any work related to configuration.</span></span>

### <a name="initialize"></a><span data-ttu-id="a340d-153">Initialisieren</span><span class="sxs-lookup"><span data-stu-id="a340d-153">Initialize</span></span>

<span data-ttu-id="a340d-154">Öffnen Sie `BlobStorage.cs`.</span><span class="sxs-lookup"><span data-stu-id="a340d-154">Open `BlobStorage.cs`.</span></span>

<span data-ttu-id="a340d-155">Suchen Sie die `Initialize`-Methode.</span><span class="sxs-lookup"><span data-stu-id="a340d-155">Location the `Initialize` method.</span></span> <span data-ttu-id="a340d-156">Ihre App ruft diese Methode auf, wenn sie zum ersten Mal verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a340d-156">Our app will call this method when it's first used.</span></span> <span data-ttu-id="a340d-157">`ConfigureServices` in `Startup.cs` zeigt an, wie das funktioniert.</span><span class="sxs-lookup"><span data-stu-id="a340d-157">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span> 

<span data-ttu-id="a340d-158">Erstellen Sie den Container in `Initialize`, falls er nicht bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="a340d-158">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="a340d-159">Füllen Sie `Initialize` mit dem folgenden Code aus, und speichern Sie Ihre Arbeit:</span><span class="sxs-lookup"><span data-stu-id="a340d-159">Fill in `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```