Arbeiten mit einem einzelnen Blob im Azure Storage SDK für .NET Core erfordert einen *Blobverweis* &mdash; eine Instanz eines `ICloudBlob`-Objekts.

Sie erhalten ein `ICloudBlob`, wenn Sie es mit den Namen des Blobs anfordern oder aus einer Liste von Blobs im Container auswählen. Beide erfordern einen `CloudBlobContainer` – in der letzten Einheit haben wir erfahren, wie wir ihn bekommen.

## <a name="getting-blobs-by-name"></a>Abrufen von Blobs anhand des Namens

Rufen Sie eine der `GetXXXReference`-Methoden auf einem `CloudBlobContainer` auf, um ein `ICloudBlob` anhand des Namens abzurufen. Wenn Sie den Typ des Blobs kennen, das Sie abrufen, verwenden Sie vorzugsweise eine der spezifischeren Methoden (`GetBlockBlobReference`, `GetAppendBlobReference` oder `GetPageBlobReference`).

Keine dieser Methoden führt einen Netzwerkaufruf durch, noch bestätigen sie, ob das Blob tatsächlich vorhanden ist oder nicht. Eine separate Methode, `GetBlobReferenceFromServerAsync`, ruft die Blobspeicher-API auf und löst eine Ausnahme aus, wenn das Blob noch nicht vorhanden ist.

## <a name="listing-blobs-in-a-container"></a>Auflisten von Blobs in einem Container

Sie erhalten eine Liste der Blobs in einem Container mit `CloudBlobContainer` der `ListBlobsSegmentedAsync`-Methode. *Segmented* bezieht sich auf die separaten Seiten von zurückgegebenen Ergebnissen &mdash; es ist nie garantiert, dass ein einzelner Aufruf von `ListBlobsSegmentedAsync` alle Ergebnisse in einer einzelnen Seite zurückgibt. Möglicherweise ist ein wiederholtes Aufrufen mithilfe des zurückgegebenen `ContinuationToken` erforderlich, um alle Seiten zu erhalten. Dadurch wird der Code für das Auflisten von Blobs ein wenig komplexer als der Code zum Hoch- oder Herunterladen, aber Sie können ein Standardmuster verwenden, um jedes Blob in einem Container zu erhalten:

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null; 

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

Dies ruft `ListBlobsSegmentedAsync` solange wiederholt auf, bis `continuationToken` den Wert `null` hat, was das Ende der Ergebnisse signalisiert.

### <a name="processing-list-results"></a>Verarbeiten von Listenergebnissen

Das Objekt, das `ListBlobsSegmentedAsync` zurückgibt, enthält eine `Results`-Eigenschaft vom Typ `IEnumerable<IListBlobItem>`. `IListBlobItem`s enthalten eine Reihe von Eigenschaften von Container und URL des Blobs, aber keine Methoden zum Hoch- oder Herunterladen. Der Grund hierfür ist, dass einige der Ergebnisobjekte möglicherweise `CloudBlobDirectory`-Objekte sind, die eher virtuelle Verzeichnisse anstatt einzelner Blobs darstellen.

Wenn Sie nur an einzelnen Blobs interessiert sind, können Sie die Ergebnisse mithilfe der `OfType<>`-Methode filtern. Hier sind einige Beispiele:

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

Die Verwendung von `OfType<>` erfordert einen Verweis auf den `System.Linq`-Namespace (`using System.Linq;`).

## <a name="exercise"></a>Übung

Eines der Features in unserer App erfordert das Abrufen einer Liste von Blobs aus der API. Wir verwenden das oben gezeigte Muster, um alle Blobs in unserem Container aufzulisten. Bei Verarbeitung der Liste erhalten wir die Namen der einzelnen Blobs.

Öffnen Sie `BlobStorage.cs` im Editor, und geben Sie in `GetNames` folgenden Code ein:

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

Die von dieser Methode zurückgegebenen Namen werden von `FilesController` verarbeitet, um sie in URLs umzuwandeln. Wenn sie an den Client zurückgegeben werden, werden sie als Hyperlinks auf der Seite gerendert.