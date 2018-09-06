In dieser Übung laden Sie die Verbindungszeichenfolge des Azure Storage-Kontos aus der Konfiguration, und Sie verwenden diese zum Herstellen einer Verbindung mit dem Azure Storage-Konto.

## <a name="retrieve-the-connection-string"></a>Abrufen der Verbindungszeichenfolge

1. Stellen Sie sicher, dass die Konsolenanwendung aus der vorherigen Einheit in Visual Studio geladen ist.
1. Fügen Sie am Anfang der Datei **Program.cs** eine *using*-Anweisung hinzu, um die **Microsoft.WindowsAzure.Storage**-Bibliothek zu referenzieren.
    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. Fügen Sie die folgende Zeile am Ende der **Main**-Methode hinzu, um die Verbindungszeichenfolge des Azure Storage-Kontos aus der Konfigurationsdatei abzurufen:
    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a>Erstellen eines Blobclients

1. Fügen Sie den folgenden Code am Ende der **Main**-Methode ein, um die Verbindungszeichenfolge zu analysieren und einen Blobclient zu erstellen:
    ```csharp
    CloudStorageAccount storageAccount;
    if (!CloudStorageAccount.TryParse(connectionString,out storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```
1. Fügen Sie den folgenden Code ein, um einen Blobclient zu erstellen und einen Verweis auf einen Container abzurufen. Optional erstellen Sie diesen, wenn er nicht am Ende der **Main**-Methode vorhanden ist:
    ```csharp
    var containerName = "MyBlobContainer";
    var success = blobClient
        .GetContainerReference(containerName)
        .CreateIfNotExistsAsync()
        .Result;
    ```

  *Beachten Sie die Verwendung der **async**-Methode **CreateIfNotExistsAsync()** und die entsprechende **Ergebniseigenschaft**. In einer typischen Anwendung würde normalerweise das Schlüsselwort **await** verwendet werden. Allerdings ist diese Anwendung eine Konsolenanwendung, die nicht asynchron ist, weshalb die **Ergebniseigenschaft** aufgerufen werden muss, um die Ergebnisse der asynchronen Aufgabe abzurufen, die von der Methode **CreateIfNotExistsAsync()** erstellt wurde.*

## <a name="print-a-status-message"></a>Ausgeben einer Statusmeldung

1. Fügen Sie den folgenden Code am Ende der **Main**-Methode hinzu, um eine Erfolgs- oder Fehlermeldung auszugeben.
    ```csharp
    if (!success)
    {
        Console.WriteLine("Error: Could not connect to Azure Storage container");
        return;
    }
    Console.WriteLine("Successfully connected to Azure Storage container");
    ```
1. Führen Sie abschließend die Anwendung aus, um zu überprüfen, ob die Verbindung erfolgreich hergestellt wurde, und sehen Sie sich das Azure-Portal an, um sicherzustellen, dass der Speichercontainer erstellt wurde, sofern dieser zuvor nicht vorhanden war.
1. **Optional:** Wenn Sie nicht vorhaben, den Container zu verwenden, löschen Sie die Ressourcengruppe, in der der Container gespeichert ist, um sicherzustellen, dass keine Kosten für Ressourcen anfallen, die Sie nicht verwenden.


