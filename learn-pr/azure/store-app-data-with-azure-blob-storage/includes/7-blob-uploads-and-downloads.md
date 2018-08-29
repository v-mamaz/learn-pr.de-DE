Sobald wir einen Verweis auf ein Blob haben, können wir Daten hoch- und herunterladen. `ICloudBlob`-Objekte verfügen über die Methoden `Upload` und `Download`, die Bytearrays, Datenströme und Dateien als Quellen und Ziele unterstützen. Bestimmte Typen bieten zur Vereinfachung zusätzliche Methoden. `CloudBlockBlob` unterstützt z.B. das Hoch- und Herunterladen von Zeichenfolgen mit `UploadTextAsync` und `DownloadTextAsync`.

## <a name="creating-new-blobs"></a>Erstellen neuer Blobs

Um ein neues Blob zu erstellen, rufen Sie eine der `Upload`-Methoden für ein Blob auf, das nicht vorhanden ist. Dies bewirkt das Erstellen des Blobs und Hochladen der Daten. 

## <a name="moving-data-to-and-from-blobs"></a>Verschieben von Daten in und aus Blobs

Das Verschieben von Daten in und aus einem Blob ist ein Netzwerkvorgang, der Zeit benötigt. Im Azure Storage SDK für .NET Core geben alle Methoden, die Netzwerkaktivität erfordern, Aufgaben des Typs `Task` zurück. Stellen Sie deshalb sicher, dass Ihre Controllermethoden entsprechend `async` sind und dass Sie mit `await` und nicht mit `Wait` auf Methodenaufrufe warten.

Eine gängige Empfehlung beim Arbeiten mit großen Datenobjekten ist die Verwendung von Datenströmen anstelle von In-Memory-Strukturen wie Bytearrays oder Zeichenfolgen. Dadurch wird vermieden, dass der gesamte Inhalt vor dem Senden zum Ziel im Speicher gepuffert wird. ASP.NET Core unterstützt das Lesen und Schreiben von Datenströmen aus Anforderungen und Antworten.

## <a name="concurrent-access"></a>Paralleler Zugriff

Es ist möglich, dass andere Prozesse Blobs hinzufügen, ändern oder löschen, während Ihre App sie verwendet. Programmieren Sie stets defensiv, und denken Sie an Probleme, die durch Parallelität verursacht werden, wie z.B. Blobs, die direkt gelöscht werden, wenn Sie versuchen, aus ihnen Daten herunterzuladen, oder Blobs, deren Inhalt sich ändert, wenn Sie dies nicht erwarten. Weitere Informationen zur Verwendung von „AccessConditions“ und Leases von Blobs zum Verwalten des parallelen Zugriffs auf Blobs finden Sie im Abschnitt „Weitere Ressourcen“ am Ende dieses Moduls.

## <a name="exercise"></a>Übung

Lassen Sie uns unsere App fertig stellen, indem wir Code zum Hoch- und Herunterladen hinzufügen und ihn dann zum Testen an Azure App Service verteilen.

### <a name="upload"></a>Hochladen

Um ein Blob hochzuladen, implementieren wir die `BlobStorage.Save`-Methode `GetBlockBlobReference` zum Abrufen von `CloudBlockBlob` aus dem Container. `FilesController.Upload` übergibt den Dateidatenstrom an `Save`, sodass wir `UploadFromStreamAsync` zum Durchführen des Hochladens mit maximaler Effizienz nutzen können.

Öffnen Sie `BlobStorage.cs` im Editor, und geben Sie die `Save`-Implementierung mit dem folgenden Code ein:

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> Der hier gezeigte datenstrombasierte Uploadcode ist effizienter als das Einlesen der Datei in ein Bytearray, bevor sie an Azure Blob Storage gesendet wird. Die Technik `IFormFile`, die wir verwenden, um die Datei vom Client abzurufen, ist jedoch keine echte durchgängige Streamingimplementierung und eignet sich nur für das Hochladen kleiner Dateien. Informationen zu vollständig gestreamten Uploads von Dateien finden Sie im Abschnitt „Weitere Ressourcen“ am Ende dieses Moduls.

### <a name="download"></a>Herunterladen

`BlobStorage.Load` gibt einen `Stream` zurück, was bedeutet, dass unser Code die Bytes aus dem Blobspeicher überhaupt nicht verschieben muss. Wir müssen nur einen Verweis auf den Blobdatenstrom zurückgeben. Dazu verwenden wir `OpenReadAsync`. ASP.NET Core übernimmt das Lesen und Schließen des Datenstroms, wenn die Clientantwort erstellt wird.

Füllen Sie `Load` mit diesem Code aus:

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a>Bereitstellen und Ausführen in Azure

Unsere App ist fertig. Lassen Sie sie uns nun bereitstellen und verfolgen, wie sie funktioniert. Führen Sie den folgenden Code im Azure Cloud Shell-Terminal aus, um unseren Code zu erstellen und in einer neuen App Service-Instanz bereitzustellen. Wir fügen auch die Verbindungszeichenfolge unseres Speicherkontos zur Konfiguration hinzu.

```console

```

...

Laden Sie einige Dateien hoch und herunter, um die App zu testen. Führen Sie dann die folgenden Befehle in der Shell aus, um die hochgeladenen Blobs anzuzeigen:

```console

```

**TODO pic from portal**