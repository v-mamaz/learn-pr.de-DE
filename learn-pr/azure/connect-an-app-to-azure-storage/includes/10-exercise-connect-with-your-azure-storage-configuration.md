::: Zone Pivot = "Csharp" Fügen Sie Code zum Abrufen der Verbindungszeichenfolge aus der Konfiguration und Verbindung mit Azure Storage-Konto verwenden.

## <a name="retrieve-the-connection-string"></a>Abrufen der Verbindungszeichenfolge

1. Wählen Sie **"Program.cs"** um ihn im Code-Editor zu öffnen.

1. Hinzufügen einer `using` -Anweisung am Anfang der Datei auf den `Microsoft.WindowsAzure.Storage` Namespace:

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. Am Ende der `Main` -Methode, die folgende Zeile zum Abrufen der Verbindungszeichenfolge des Azure Storage-Konto aus der Konfigurationsdatei hinzufügen. Der übergebene _Schlüssel_ muss mit dem Namen übereinstimmen, die in verwendet Ihre **"appSettings.JSON"** Datei.

    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a>Erstellen eines Blobclients

1. Verwenden Sie die statische `CloudStorageAccount.TryParse` Methode zum Erstellen einer `CloudStorageAccount` Objekt – dauert die Verbindungszeichenfolge und einem `out` Parameter, um das erstellte Objekt zurückzugeben. Gibt eine `bool` Wert, der angibt, ob sie erfolgreich die Zeichenfolge analysiert.
    - Schlägt fehl, wird eine Nachricht an die Konsole, und von der Methode zurückgegeben.

    ```csharp
    if (!CloudStorageAccount.TryParse(connectionString, 
            out CloudStorageAccount storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    ```

1. Verwenden Sie das zurückgegebene `CloudStorageAccount` Objekt, das ein Blob-Dienstclient zu erstellen.

    ```csharp
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Als Nächstes verwenden Sie die Blob-Dienstclient, um einen Verweis auf einen Container namens "Photoblobs" abzurufen. Z. B. Kontonamen, müssen die Blob-Containernamen viel aus Buchstaben und Zahlen und Kleinbuchstaben sein.

    ```csharp
    var blobContainer = blobClient.GetContainerReference("photoblobs");
    ```

1. Verwenden der `CreateIfNotExistsAsync` Methode, um den Container zu erstellen. Dies gibt eine `bool` , der angibt, ob der Container erstellt wurde. Dies in einer Variablen mit dem Namen Store `created`.
    - Beachten Sie, dass dies eine **Async** -Methode: Das bedeutet, sie führt einen tatsächliche Netzwerk-Aufruf.
    - Sie benötigen, verwenden Sie die `await` Schlüsselwörter zum Abrufen der `bool` Ergebnis.

    ```csharp
    bool created = await blobContainer.CreateIfNotExistsAsync();
    ```

1. Aufgrund von der `await` -Schlüsselwort, fahren Sie fort, und ändern Sie die Signatur für die `Main` Methode werden `async` und Zurückgeben einer `Task`.

    ```csharp
    static async Task Main(string[] args)
    {
        ...
    }
    ```

1. Abschließend, ob wir den Blob-Container erstellt.

    ```csharp
    Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
    ```

1. Speichern Sie die Datei.

Die endgültige Datei sollte wie folgt aussehen, wenn Sie Ihre Arbeit überprüfen möchten.

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using System.Threading.Tasks;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;

namespace PhotoSharingApp
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();
            var connectionString = configuration["StorageAccountConnectionString"];

            if (!CloudStorageAccount.TryParse(connectionString, out CloudStorageAccount storageAccount))
            {
                Console.WriteLine("Unable to parse connection string");
                return;
            }

            var blobClient = storageAccount.CreateCloudBlobClient();
            var blobContainer = blobClient.GetContainerReference("photoblobs");
            bool created = await blobContainer.CreateIfNotExistsAsync();

            Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
        }
    }
}
```

## <a name="use-c-71-to-build-our-app"></a>Verwenden Sie zum Erstellen unserer app c# 7.1

Unterstützung für `async` und `await` auf `Main` Methoden c# 7.1 hinzugefügt wurde. Dies möglicherweise nicht die Standardversion des Compilers, die Sie verwenden. Stellen Sie sicher, dass wir diese Version des Compilers verwenden, indem Sie ihn in der Konfigurationsdatei festlegen.

1. Öffnen der `PhotoSharingApp.csproj` und fügen `<LangVersion>7.1</LangVersion>` auf die `PropertyGroup` , der angibt der `TargetFramework`. Es sollte, wenn Sie fertig sind, wie folgt aussehen:

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <LangVersion>7.1</LangVersion> 
        <TargetFramework>netcoreapp2.0</TargetFramework>
      </PropertyGroup>
      ...
    </Project>
    ```

1. Speichern Sie die Datei.

## <a name="run-the-app"></a>Ausführen der App

1. Erstellen Sie die Anwendung, und führen Sie sie aus. **Hinweis:** sicherzustellen, dass Sie in das richtige Arbeitsverzeichnis sind.

    ```bash
    dotnet run
    ```

::: zone-end

::: Zone Pivot = "Javascript" Fügen Sie Code zum Verbinden mit Azure Storage-Konto mithilfe unserer gespeicherte Verbindungszeichenfolge. Die Azure-Client-Bibliothek verwendet automatisch die **AZURE_STORAGE_CONNECTION_STRING** Umgebungsvariable beim Abrufen der Verbindungszeichenfolge.

## <a name="create-a-blob-client"></a>Erstellen eines Blobclients

1. Open **"Index.js"** im Code-Editor.

1. Starten Sie dazu die **Azure Storage-** Modul. Das Modul in einer Variablen mit dem Namen Store **Storage**.

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    
    const storage = require('azure-storage');
    ```

1. Direkt danach verwenden Sie als Nächstes die **Storage** zu erstellenden Objekts der `BlobService` Objekt aus, und speichern Sie sie in einen globalen Namen **BlobService**. Denken Sie daran, diese einfache Objekte, die Zugriff auf das Speicherkonto darstellt.

    ```javascript
    const blobService = storage.createBlobService();
    ```

1. Fügen Sie eine Konstante, um den Container darstellt, die, den wir erstellen möchten. Den Container nennen "Photoblobs".

    ```javascript
    const containerName = 'photoblobs';
    ```

## <a name="create-a-container"></a>Erstellen eines Containers

Wir können die `BlobService` Objekt, das Arbeiten mit Blob-APIs im Azure-Speicher. Wie bereits erwähnt, sind alle APIs, die Netzwerk-Aufrufe asynchron, um die app reaktionsfähig gehalten wird. Die `createContainerIfNotExists` Methode ist eine dieser Methoden. Wir verwenden _verspricht_ zum Behandeln des Rückrufs, der die Antwort enthält.

1. Verwenden `util.promisify` die Rückruf-Version der auszuführenden `createContainerIfNotExists` und schalten Sie ihn in eine Methode, die Zusage zurückgibt.
    - Da die Callback-Methode für ein Objekt ist, stellen Sie sicher, Hinzufügen einer `bind` am Ende für die Verbindung mit diesen Kontext aufgerufen.
    - Weisen Sie den Rückgabewert einer Konstanten am Anfang der Datei mit dem Namen `createContainerAsync`, wie unten dargestellt.

```javascript
const storage = require('azure-storage');
const blobService = storage.createBlobService();

const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';
```

1. Entfernen Sie die "Hello, World!" Ausgabe von `main()`.

1. Rufen Sie Ihre neue `createContainerAsync` versprechen.
    - Übergeben sie die **ContainerName** Konstanten.
    - Anwenden der `await` -Schlüsselwort auf den Aufruf.
    - Binden Sie den Aufruf in eine `try`  /  `catch` erstellen und ein Fehler ausgegeben.

    ```javascript
    try {
        await createContainerAsync(containerName);
    }
    catch (err) {
        console.log(err.message);
    }
    ```
    
1. Die `createContainerAsync` Promise gibt den ersten Wert aus der zugrunde liegenden `createContainerIfNotExists`, dies ist das Ergebnis des Containers. Dies umfasst Informationen, ob der Container oder nicht erstellt wurde. Das Ergebnis in einer Variablen zu erfassen und Ausgabe basierend gibt an, ob der Container erstellt wurde, auf die `result.created` Eigenschaft.

    ```javascript
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
    ```

1. Schließlich können die `main` -Funktion mit den `async` Schlüsselwort.
        
1. Speichern Sie die Datei.

Die endgültige Datei sollte folgendermaßen aussehen, wenn Sie Ihre Arbeit überprüfen möchten.

```javascript
#!/usr/bin/env node

require('dotenv').load();

const util = require('util');

const storage = require('azure-storage');
const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';

async function run() {
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
}

run();
```

## <a name="run-the-app"></a>Ausführen der App

1. Erstellen Sie die Anwendung, und führen Sie sie aus. **Hinweis:** sicherzustellen, dass Sie in das richtige Arbeitsverzeichnis sind.

    ```bash
    node index.js
    ```

::: zone-end

Es sollten melden, dass der Blob-Container erstellt wurde. Wenn Sie ein zweites Mal ausführen, sollten sie Ihnen mitteilen, dass sie bereits vorhanden ist.

Um den Container zu überprüfen:

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true)an.

1. Navigieren Sie zum Speicherkonto. Können Sie die **alle Ressourcen** Abschnitt erfahren das Speicherkonto oder die Suche anhand des Namens aus der _Suchfeld_ am oberen Rand des portalfensters. 

1. Wählen Sie die **Blobs** Eintrag des Speicherkontos, das die **Blobdienste** Abschnitt.

1. Daraufhin sollte Ihre **Photoblobs** Container im Bedienfeld "Blobs". Sie können den Container über das Menü "..." auf der rechten Seite des Eintrags, versuchen es neu erstellen, mit der app löschen.

> [!NOTE]
> Der Container nicht mehr auf das Portal sehr schnell, aber es dauert einige Minuten, bis Sie tatsächlich gelöscht. Sie erhalten eine Fehlerantwort von Azure, während sie gelöscht wird gerade, wenn Sie versuchen, erneut erstellen.

## <a name="delete-the-app"></a>Löschen Sie die app
Wenn Sie sich, dass Sie nicht den Quellcode der Anwendung in Ihrer Cloud Shell-Umgebung beibehalten möchten entscheiden, können Sie den folgenden Befehl aus, um den Ordner und alle Inhalte zu entfernen.

```bash
rm -r PhotoSharingApp/
```
