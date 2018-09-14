So sieht der typische Workflow für Apps aus, die Azure Blob Storage verwenden:

1. **Abrufen der Konfiguration**: Laden Sie beim Start die Konfiguration des Speicherkontos. Dies ist in der Regel eine Verbindungszeichenfolge für das Speicherkonto.

1. **Initialisieren des Clients**: Verwenden Sie die Verbindungszeichenfolge, um die Azure Storage-Clientbibliothek zu initialisieren. Dabei werden Objekte erstellt, die die App für die Arbeit mit der Blob Storage-API verwendet.

1. **Verwenden**: Führen Sie API-Aufrufe mit der Clientbibliothek aus, um mit Containern und Blobs zu arbeiten.

## <a name="configure-your-connection-string"></a>Konfigurieren der Verbindungszeichenfolge

Vor dem Ausführen der app, benötigen Sie die Verbindungszeichenfolge für das Speicherkonto an, die Sie verwenden möchten. Sie können alle Azure-Verwaltungsschnittstelle verwenden, um ihn verwenden, einschließlich der Azure-Portal, das Azure-Befehlszeilenschnittstelle oder Azure PowerShell zu erhalten. Wenn wir die Web-app einrichten, um unser Code am Ende dieses Modul ausführen, verwenden wir die Azure-Befehlszeilenschnittstelle, um die Verbindungszeichenfolge für das Speicherkonto zu erhalten, die Sie zuvor erstellt haben.

Diese enthält den Kontoschlüssel. Der Kontoschlüssel gilt als geheim und sollte sicher aufbewahrt werden. Hier speichern wir die Verbindungszeichenfolge in einer App Service-Anwendungseinstellung. App Service-Anwendungseinstellungen sind ein sicherer Ort für Anwendungsgeheimnisse. Dieser Ansatz unterstützt jedoch keine lokale Entwicklung und ist keine robuste, eigenständige End-to-End-Lösung.

> [!WARNING]
> **Platzieren Sie Speicherkontoschlüssel nicht im Code oder in ungeschützten Konfigurationsdateien.** Speicherkontoschlüssel ermöglichen Vollzugriff auf Ihr Speicherkonto. Der Verlust eines Schlüssels kann zu nicht behebbaren Schäden und hohen Rechnungen führen. Im Abschnitt „Weitere nützliche Informationen“ am Ende dieses Moduls finden Sie eine Anleitung zum Speichern und Hinweise zum Wiederherstellen verlorener Schlüssel.

## <a name="initialize-the-blob-storage-object-model"></a>Initialisieren des Blob Storage-Objektmodells

Im Azure Storage SDK für .NET Core besteht das Standardmuster für die Verwendung von Blob Storage aus den folgenden Schritten:

1. Rufen Sie `CloudStorageAccount.Parse` (oder `TryParse`) mit Ihrer Verbindungszeichenfolge auf, um `CloudStorageAccount` abzurufen.

1. Rufen Sie `CreateCloudBlobClient` im `CloudStorageAccount` auf, um `CloudBlobClient` abzurufen.

1. Rufen Sie `GetContainerReference` im `CloudBlobClient` auf, um `CloudBlobContainer` abzurufen.

1. Verwenden Sie Methoden für den Container, um eine Liste von Blobs und/oder Referenzen für einzelne Blobs zum Hoch- und Herunterladen von Daten abzurufen.

Im Code sehen die Schritte 1&ndash;3 so aus:

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

Keiner dieser Initialisierungscodes führt Aufrufe über das Netzwerk durch. Das bedeutet, dass einige Ausnahmen, die aufgrund fehlerhafter Informationen auftreten, erst zu einem späteren Zeitpunkt ausgelöst werden. Der Aufruf von `CloudStorageAccount.Parse` löst beispielsweise sofort eine Ausnahme aus, wenn die Verbindungszeichenfolge falsch formatiert ist. Es wird jedoch keine Ausnahme ausgelöst, wenn das Speicherkonto, auf das eine Verbindungszeichenfolge verweist, nicht vorhanden ist.

## <a name="create-containers-at-startup"></a>Erstellen von Containern beim Start

Das Aufrufen von `CreateIfNotExistsAsync` für einen `CloudBlobContainer` ist die beste Methode, einen Container zu erstellen, wenn Ihre Anwendung gestartet wird oder wenn sie zum ersten Mal versucht, ihn zu verwenden.

`CreateIfNotExistsAsync` löst keine Ausnahme aus, wenn der Container bereits vorhanden ist, veranlasst aber einen Netzwerkaufruf an Azure Storage. Rufen Sie dieses Element einmalig während der Initialisierung auf, nicht bei jedem Versuch, einen Container zu verwenden.

## <a name="exercise"></a>Übung

### <a name="clone-and-explore-the-unfinished-app"></a>Klonen und Untersuchen nicht fertiger Apps

Klonen Sie zuerst die Start-App aus GitHub. Führen Sie im Cloud Shell-Terminal den folgenden Befehl aus, um eine Kopie des Quellcodes zu erstellen und im Editor zu öffnen:

```console
git clone https://github.com/MicrosoftDocs/mslearn-store-data-in-azure.git
cd mslearn-store-data-in-azure/store-app-data-with-azure-blob-storage/src/start
code .
```

Öffnen Sie die Datei `Controllers/FilesController.cs` im Editor. Hier gibt es nichts zu tun, aber wir werfen einen kurzen Blick darauf, was die App macht.

Dieser Controller implementiert eine API mit drei Aktionen:

- **Index** (GET/API/Dateien) gibt eine Liste von URLs zurück – eine für jede hochgeladene Datei. Das App-Front-End ruft diese Methode auf, um eine Liste von Hyperlinks zu den hochgeladenen Dateien zu erstellen.
- **Hochladen** (POST/API/Dateien) empfängt eine hochgeladene Datei und speichert sie.
- **Herunterladen** (GET/API/Dateien/{Dateiname}) lädt eine einzelne Datei nach ihrem Namen herunter.

Jede Methode verwendet eine `IStorage`-Instanz mit der Bezeichnung `storage`. Es gibt eine unvollständige Implementierung von `IStorage` in `Models/BlobStorage.cs`, die wir vervollständigen.

### <a name="add-the-nuget-package"></a>Hinzufügen des NuGet-Pakets

Fügen Sie zunächst einen Verweis auf das Azure Storage SDK hinzu. Führen Sie im Terminal Folgendes aus:

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

So wird sichergestellt, dass Sie die neueste Version der Blob Storage-Clientbibliothek verwenden.

### <a name="configure"></a>Konfigurieren

Die Konfigurationswerte, die wir benötigen wird die Verbindungszeichenfolge für Speicherkonto und der Namen des Containers die app zum Speichern von Dateien. In diesem Modul werden nur wir führen Sie die app in Azure App Service, damit wir führen Sie die bewährte Methode von App Service und speichern Sie die Werte in App Service-Anwendungseinstellungen. Das machen wir, wenn wir die App Service-Instanz erstellen, weshalb wir im Moment nichts zu tun haben.

Wenn es zum *Einsatz* der Konfiguration kommt, enthält unsere Einsteiger-App bereits die von uns benötigten Einstellungen. Der `IOptions<AzureStorageConfig>`-Konstruktorparameter in `BlobStorage` hat zwei Eigenschaften: die Speicherkonto-Verbindungszeichenfolge und den Namen des Containers, in dem die App Blobs speichert. In der `ConfigureServices`-Methode von `Startup.cs` gibt es einen Code, der die Werte aus der Konfiguration lädt, wenn die App startet.

### <a name="initialize"></a>Initialisieren

Open `Models/BlobStorage.cs` im Editor. Fügen Sie die folgenden `using`-Anweisungen am Anfang der Datei hinzu, um sie für den Code vorzubereiten, den Sie während der Übung hinzufügen werden.

```csharp
using System.Linq;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Wechseln Sie zur `Initialize`-Methode. Unsere App ruft diese Methode auf, wenn `BlobStorage` zum ersten Mal verwendet wird. `ConfigureServices` in `Startup.cs` zeigt, wie das funktioniert.

Erstellen Sie den Container in `Initialize`, falls er nicht bereits vorhanden ist. Ersetzen Sie die aktuelle Implementierung von `Initialize` durch den folgenden Code, und speichern Sie Ihre Arbeit:

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```