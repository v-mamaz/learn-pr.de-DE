::: zone pivot="csharp" Lassen Sie uns Code hinzufügen, um die Verbindungszeichenfolge aus der Konfiguration abzurufen und sie für das Herstellen einer Verbindung mit dem Azure Storage-Konto zu verwenden.

## <a name="retrieve-the-connection-string"></a>Abrufen der Verbindungszeichenfolge

1. Wählen Sie dann **Program.cs** aus, um die Datei im Code-Editor zu öffnen.

1. Fügen Sie eine `using`-Anweisung am Anfang der Datei hinzu, um auf den Namespace `Microsoft.WindowsAzure.Storage` zu verweisen:

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. Fügen Sie am Ende der `Main`-Methode die folgende Zeile hinzu, um die Verbindungszeichenfolge des Azure Storage-Kontos aus der Konfigurationsdatei abzurufen. Der übergebene _Schlüssel_ muss mit dem Namen übereinstimmen, den Sie in Ihrer Datei **appsettings.json** verwendet haben.

    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a>Erstellen eines Blobclients

1. Verwenden Sie die statische `CloudStorageAccount.TryParse`-Methode zum Erstellen eines `CloudStorageAccount`-Objekts. Es verwendet die Verbindungszeichenfolge und einen `out`-Parameter, um das erstellte Objekt zurückzugeben. Es gibt einen `bool`-Wert zurück, der angibt, ob die Zeichenkette erfolgreich analysiert wurde.
    - Geben Sie bei einem Fehler eine Meldung an die Konsole aus, und kehren Sie von der Methode zurück.

    ```csharp
    if (!CloudStorageAccount.TryParse(connectionString, 
            out CloudStorageAccount storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    ```

1. Verwenden Sie das zurückgegebene `CloudStorageAccount`-Objekt, um einen Blobclient zu erstellen.

    ```csharp
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Als Nächstes verwenden Sie den Blobclient, um einen Verweis auf einen Container namens „photoblobs“ abzurufen. Ähnlich wie Kontonamen müssen Blobcontainernamen kleingeschrieben sein und aus Buchstaben und Zahlen bestehen.

    ```csharp
    var blobContainer = blobClient.GetContainerReference("photoblobs");
    ```

1. Verwenden Sie die `CreateIfNotExistsAsync`-Methode, um den Container zu erstellen. Dies gibt einen `bool`-Wert zurück, der angibt, ob der Container erstellt wurde. Speichern Sie diesen in einer Variablen namens `created`.
    - Beachten Sie, dass es sich hierbei um eine **asynchrone** Methode handelt, die daher den tatsächlichen Netzwerkaufruf durchführt.
    - Sie müssen `await`-Schlüsselwörter zum Abrufen des `bool`-Ergebnisses verwenden.

    ```csharp
    bool created = await blobContainer.CreateIfNotExistsAsync();
    ```

1. Da wir das Schlüsselwort `await` verwenden, ändern Sie nun die Signatur der `Main`-Methode in `async`, und geben Sie `Task` zurück.

    ```csharp
    static async Task Main(string[] args)
    {
        ...
    }
    ```

1. Prüfen Sie abschließend, ob wir einen Blobcontainer erstellt haben.

    ```csharp
    Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
    ```

1. Speichern Sie die Datei.

Die endgültige Datei sollte wie folgt aussehen, wenn Sie Ihr Ergebnis überprüfen möchten.

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

## <a name="use-c-71-to-build-our-app"></a>Verwenden von C# 7.1 zum Erstellen unserer App

C# 7.1 unterstütz nun `async` und `await` für `Main`-Methoden. Dies ist möglicherweise nicht die Standardversion des Compilers, den Sie verwenden. Lassen Sie uns sicherstellen, dass wir diese Version des Compilers verwenden, indem wir sie in unserer Konfigurationsdatei festlegen.

1. Öffnen Sie `PhotoSharingApp.csproj`, und fügen Sie `<LangVersion>7.1</LangVersion>` zu `PropertyGroup` hinzu, die das `TargetFramework` angibt. Nach Ausführung dieser Schritte sollte das Ergebnis so aussehen:

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

1. Erstellen Sie die Anwendung, und führen Sie sie aus. **Hinweis:** Vergewissern Sie sich, dass Sie sich im richtigen Arbeitsverzeichnis befinden.

    ```bash
    dotnet run
    ```

::: zone-end

::: zone-pivot="javascript" Fügen wir nun Code hinzu, um über unsere gespeicherte Verbindungszeichenfolge eine Verbindung mit dem Azure Storage-Konto herzustellen. Die Azure-Clientbibliothek verwendet zum Abrufen der Verbindungszeichenfolge automatisch die Umgebungsvariable **AZURE_STORAGE_CONNECTION_STRING**.

## <a name="create-a-blob-client"></a>Erstellen eines Blobclients

1. Öffnen Sie **index.js** im Code-Editor.

1. Beginnen Sie mit dem Hinzufügen des Moduls **azure-storage**. Speichern Sie das Modul in einer Variablen mit dem Namen **storage**.

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    
    const storage = require('azure-storage');
    ```

1. Verwenden Sie im Anschluss das Objekt **storage**, um das Objekt `BlobService` zu erstellen und es in einem globalen Element namens **blobService** zu speichern. Denken Sie daran, dass es sich hierbei um vereinfachte Objekte handelt, die den Zugriff auf das Speicherkonto darstellen.

    ```javascript
    const blobService = storage.createBlobService();
    ```

1. Fügen Sie eine Konstante hinzu, die den Container darstellt, den wir erstellen möchten. Den Container nennen wir „photoblobs“.

    ```javascript
    const containerName = 'photoblobs';
    ```

## <a name="create-a-container"></a>Erstellen eines Containers

Wir können das `BlobService`-Objekt zum Arbeiten mit Blob-APIs in Azure Storage verwenden. Wie bereits erwähnt, sind alle APIs, die Netzwerkaufrufe ausführen, asynchron, um die App reaktionsschnell zu halten. Die `createContainerIfNotExists`-Methode ist eine dieser Methoden. Wir verwenden _Zusagen_, um den Rückruf zu verarbeiten, der die Antwort enthält.

1. Verwenden Sie `util.promisify`, um die Rückrufversion von `createContainerIfNotExists` zu nutzen und sie in eine Methode zur Rückgabe von Zusagen umzuwandeln.
    - Da die Rückrufmethode für ein Objekt gilt, stellen Sie sicher, dass Sie am Ende einen `bind`-Aufruf hinzufügen, um sie mit diesem Kontext zu verbinden.
    - Weisen Sie den Rückgabewert einer Konstanten am Anfang der Datei namens `createContainerAsync` zu, wie unten gezeigt.

```javascript
const storage = require('azure-storage');
const blobService = storage.createBlobService();

const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';
```

1. Entfernen Sie die Ausgabe „Hello, World!“ aus `main()`.

1. Rufen Sie Ihre neue `createContainerAsync`-Zusage auf.
    - Übergeben Sie an sie die Konstante **containerName**.
    - Wenden Sie das Schlüsselwort `await` auf den Aufruf an.
    - Umschließen Sie den Aufruf in einem Konstrukt des Typs `try` / `catch`, und geben Sie Fehler aus.

    ```javascript
    try {
        await createContainerAsync(containerName);
    }
    catch (err) {
        console.log(err.message);
    }
    ```
    
1. Die Zusage `createContainerAsync` gibt den ersten Wert aus dem zugrunde liegenden `createContainerIfNotExists` zurück, der das Containerergebnis ist. Dies umfasst Informationen dazu, ob der Container erstellt wurde oder nicht. Erfassen Sie das Ergebnis in einer Variablen, und geben Sie aus, ob der Container basierend auf der `result.created`-Eigenschaft erstellt wurde.

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

1. Ergänzen Sie schließlich die `main`-Funktion mit dem Schlüsselwort `async`.
        
1. Speichern Sie die Datei.

Die endgültige Datei sollte wie folgt aussehen, wenn Sie Ihr Ergebnis überprüfen möchten.

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

1. Erstellen Sie die Anwendung, und führen Sie sie aus. **Hinweis:** Vergewissern Sie sich, dass Sie sich im richtigen Arbeitsverzeichnis befinden.

    ```bash
    node index.js
    ```

::: zone-end

Es sollte gemeldet werden, dass der Blobcontainer erstellt wurde. Bei der zweiten Ausführung sollte gemeldet werden, dass er bereits vorhanden ist.

So überprüfen Sie den Container

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

1. Navigieren Sie zu Ihrem Speicherkonto. Sie können den Abschnitt **Alle Ressourcen** verwenden, um das Speicherkonto zu finden, oder es anhand des Namens im _Suchfeld_ oben im Portalfenster suchen. 

1. Wählen Sie im Abschnitt **Blobdienste** den Eintrag **Blobs** des Speicherkontos aus.

1. Im Bereich „Blobs“ sollte Ihr Container **photoblobs** angezeigt werden. Sie können den Container über das Menü „...“ rechts neben dem Eintrag löschen, um zu versuchen, ihn mit Ihrer App neu zu erstellen.

> [!NOTE]
> Der Container verschwindet sehr schnell aus dem Portal, aber das eigentliche Löschen dauert einige Minuten. Wenn Sie versuchen, ihn während des Löschvorgangs wiederherzustellen, erhalten Sie von Azure eine Fehlermeldung.

## <a name="delete-the-app"></a>Löschen der App
Wenn Sie sich entscheiden, den Anwendungsquellcode nicht in Ihrer Cloud Shell-Umgebung zu behalten, können Sie mit dem folgenden Befehl den Ordner und alle Inhalte entfernen.

```bash
rm -r PhotoSharingApp/
```
