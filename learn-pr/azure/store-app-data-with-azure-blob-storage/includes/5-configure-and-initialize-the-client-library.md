So sieht der typische Workflow für Apps aus, die Azure Blob Storage verwenden:

1. **Abrufen der Konfiguration**: Laden Sie beim Starten die Konfiguration, z.B. die Verbindungszeichenfolge mit dem Kontoschlüssel. Dies ist erforderlich, um API-Aufrufe zu authentifizieren.
1. **Initialisieren Sie den Client**: Verwenden Sie die Verbindungszeichenfolge, um die Azure Storage-Clientbibliothek zu initialisieren. Dabei werden Objekte erstellt, die die App für die Arbeit mit der Blob Storage-API verwendet.
1. **Verwenden**: Führen Sie API-Aufrufe mit der Clientbibliothek aus, um mit Containern und Blobs zu arbeiten.

## <a name="configure-your-connection-string"></a>Konfigurieren der Verbindungszeichenfolge

Bevor Sie einen Code schreiben, benötigen Sie die Verbindungszeichenfolge für das von Ihnen verwendete Speicherkonto. 

Die Verbindungszeichenfolge enthält Ihren Kontoschlüssel. Der Kontoschlüssel gilt als geheim und sollte sicher aufbewahrt werden. Wir speichern die Verbindungszeichenfolge in einer App Service-Anwendungseinstellung. Eine Anwendungseinstellung ist ein sicherer Ort für Anwendungsgeheimnisse, unterstützt jedoch keine lokale Entwicklung und ist keine robuste, eigenständige End-to-End-Lösung.

> [!WARNING]
> **Platzieren Sie Speicherkontoschlüssel nicht im Code oder in ungeschützten Konfigurationsdateien.** Speicherkontoschlüssel ermöglichen Vollzugriff auf Ihr Speicherkonto. Der Verlust eines Schlüssels kann zu nicht behebbaren Schäden und hohen Rechnungen führen. Im Abschnitt „Zusätzliche Ressourcen“ am Ende dieses Moduls finden Sie eine Anleitung zum Speichern und Hinweise zum Wiederherstellen verlorener Schlüssel.

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

Keiner dieser Initialisierungscodes führt Aufrufe über das Netzwerk durch. Das bedeutet, dass Ausnahmen, die durch falsche Informationen entstehen, erst später ausgelöst. Beispielsweise wird der Aufruf von `GetContainerReference` erfolgreich sein, unabhängig davon, ob der Container tatsächlich im Konto existiert.

## <a name="create-containers-at-startup"></a>Erstellen von Containern beim Start

Anwendungen erstellen benötigte Container in der Regel im Code, auch wenn Sie deren Funktion im Voraus kennen. Rufen Sie `CreateIfNotExistsAsync` im `CloudBlobContainer` auf, um Container zu erstellen, von denen Sie wissen, dass Sie sie brauchen.

`CreateIfNotExistsAsync` *führt* einen Netzwerkaufruf in Azure Storage aus. Am besten ist es, den Aufruf einmal beim Start auszuführen und nicht jedes Mal, wenn Sie auf einen Container zugreifen.

## <a name="exercise"></a>Übung

### <a name="clone-and-explore-the-unfinished-app"></a>Klonen und Untersuchen nicht fertiger Apps

Klonen Sie zuerst die Start-App aus GitHub. Führen Sie im Cloud Shell-Terminal den folgenden Befehl aus, um eine Kopie des Quellcodes zu erstellen und im Editor zu öffnen:

```console
git clone TODO
cd TODO
code .
```

Öffnen Sie die Datei `Controllers/FilesController.cs`.

Dieser Controller implementiert eine API mit drei Aktionen:

* **Index** (GET/API/Dateien) gibt eine Liste von URLs zurück – eine für jede hochgeladene Datei. Das App-Front-End ruft diese Methode auf, um eine Liste von Hyperlinks zu den hochgeladenen Dateien zu erstellen.
* **Hochladen** (POST/API/Dateien) empfängt eine hochgeladene Datei und speichert sie.
* **Herunterladen** (GET/API/Dateien/{Dateiname}) lädt eine einzelne Datei nach ihrem Namen herunter.

Jede Methode verwendet eine `IStorage`-Instanz mit der Bezeichnung `storage`. Es gibt eine unvollständige Implementierung von `IStorage` in `Models/BlobStorage.cs`.

### <a name="add-the-nuget-package"></a>Hinzufügen des NuGet-Pakets

Fügen Sie zunächst einen Verweis auf das Azure Storage SDK hinzu. Führen Sie im Terminal Folgendes aus:

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

So wird sichergestellt, dass Sie die neueste Version der Blob Storage-Clientbibliothek verwenden.

### <a name="configure"></a>Konfigurieren

Die Start-App enthält bereits die erforderliche Konfigurationsinfrastruktur. Der `IOptions<AzureStorageConfig>`-Konstruktorparameter in `BlobStorage` hat zwei Eigenschaften: die Speicherkonto-Verbindungszeichenfolge und den Namen des Containers, in dem die App Blobs speichert. In der `ConfigureServices`-Methode von `Startup.cs` gibt es einen Code, der die Werte aus der Konfiguration lädt, wenn die App startet.

In dieser Übung führen Sie die App in Azure App Service aus, um die Konfigurationswerte später den App Service-Anwendungseinstellungen hinzuzufügen. Im Moment sind keine Aktionen in Zusammenhang mit der Konfiguration erforderlich.

### <a name="initialize"></a>Initialisieren

Öffnen Sie `BlobStorage.cs`.

Suchen Sie die `Initialize`-Methode. Ihre App ruft diese Methode auf, wenn sie zum ersten Mal verwendet wird. `ConfigureServices` in `Startup.cs` zeigt an, wie das funktioniert. 

Erstellen Sie den Container in `Initialize`, falls er nicht bereits vorhanden ist. Füllen Sie `Initialize` mit dem folgenden Code aus, und speichern Sie Ihre Arbeit:

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```