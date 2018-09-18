Nun, da alle Anforderungen erfüllt sind, können Sie Code schreiben, mit dem eine neue Speicherwarteschlange erstellt und eine Nachricht hinzugefügt wird. Wir fügen diesen Code üblicherweise in unsere Front-End-Anwendungen ein, die die Daten generieren.

## <a name="add-the-client-library-for-azure-storage"></a>Hinzufügen der Clientbibliothek für Azure Storage

Lassen Sie uns beginnen, indem wir unserer App die **Azure Storage-Clientbibliothek für .NET** hinzufügen. Diese kann mit NuGet (einem .NET-Paket-Manager) installiert werden. 

> [!NOTE]
> Auch wenn eine neue Cloud Shell erstellt wurde, sind alle Ihre Dateien weiterhin vorhanden. Sie müssen jedoch zum Ordner `QueueApp` wechseln, da Sie sich nun im Stammverzeichnis Ihres Speicherbereichs befinden. Geben Sie einfach `cd QueueApp` ein, um Ordner zu wechseln. Stellen Sie sicher, dass Sie dies tun, bevor Sie versuchen, das Paket hinzuzufügen, da sich die .NET-App in diesem Ordner befindet.

1. Ändern Sie das aktuelle Verzeichnis in den Ordner `QueueApp`.

1. Installieren Sie mit dem Befehl `dotnet add package` das Paket `WindowsAzure.Storage` im Projekt.

```azurecli
dotnet add package WindowsAzure.Storage
```

## <a name="add-a-method-to-send-a-news-alert"></a>Hinzufügen einer Methode zum Senden neuer Benachrichtigungen

Als Nächstes erstellen wir eine neue Methode, um eine Nachrichtenmeldung in eine Warteschlange zu stellen.

1. Öffnen Sie den Code-Editor durch Eingeben von `code .`.

1. Öffnen Sie die Datei `Program.cs`.

1. Fügen Sie am Anfang der Datei die folgenden Namespaces hinzu. Wir verwenden Typen von beiden, um uns mit Azure Storage zu verbinden und dann mit Warteschlangen zu arbeiten.

    - System.threading.task
    - Microsoft.WindowsAzure.Storage
    - Microsoft.WindowsAzure.Storage.Queue

1. Erstellen Sie eine statische Methode in der `Program`-Klasse mit dem Namen `SendArticleAsync`, die `string` verwendet und `Task` zurückgibt. Wir nutzen diese Methode, um eine Nachrichtenmeldung an unseren Dienst zu senden. Benennen Sie den Eingabeparameter wie unten dargestellt mit `newsMesasage`.

    ```csharp
    ...
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Queue; 
    
    class Program
    {
        ...
    
        static async Task SendArticleAsync(string newsMessage)
        {
        }
    }
    ```
    
1. Verwenden Sie in Ihrer neuen Methode die statische `CloudStorageAccount.Parse`-Methode zum Analysieren der Verbindungszeichenfolge (beachten Sie, dass wir Sie in einer Konstantenzeichenfolge platziert haben). Diese Methode gibt ein `CloudStorageAccount`-Objekt zurück, das in einer Variablen gespeichert werden muss.

1. Rufen Sie die `CreateCloudQueueClient()`-Methode für das Speicherkontenobjekt auf, um ein Clientobjekt abzurufen und es in einer Variablen zu speichern.

1. Rufen Sie als Nächstes die `GetQueueReference`-Methode für das Clientobjekt auf, und übergeben Sie die Zeichenfolge `"newsqueue"` als Warteschlangennamen. Dies gibt ein `CloudQueue`-Objekt zurück, das wir zum Arbeiten mit der Warteschlange verwenden können. Es ist in Ordnung, wenn die Warteschlange noch nicht vorhanden ist.

1. Rufen Sie `CreateIfNotExistsAsync()` für das `CloudQueue`-Objekt auf, um sicherzustellen, dass die Warteschlange einsatzbereit ist. Dadurch wird die Warteschlange bei Bedarf erstellt.
    - Da es sich um eine asynchrone Methode handelt, verwenden Sie das C#-Schlüsselwort `await`, um sicherzustellen, dass wir ordnungsgemäß mit ihr arbeiten. Das bedeutet auch, dass Sie die _Methode_ mit dem Schlüsselwort `async` ergänzen müssen. 
    - `CreateIfNotExistsAsync` gibt den Wert `bool` zurück, der `true` ist, wenn die Warteschlange erstellt wurde, und `false`, wenn sie bereits vorhanden ist. Geben Sie eine Nachricht an die Konsole aus, nachdem wir die Warteschlange erstellt haben.
    - Es folgt ein Beispiel, wenn Sie Hilfe benötigen.

    ```csharp
    static async Task SendArticleAsync(string newsMessage)
    {
        ...
        bool createdQueue = await queue.CreateIfNotExistsAsync();
        if (createdQueue)
        {
            Console.WriteLine("The queue of news articles was created.");
        }
    }
    ```

1. Erstellen Sie eine Instanz von `CloudQueueMessage`. 
    - Sie verwendet einen `string`-Parameter. Übergeben Sie den Methodenparameter (`newsMessage`). Dies wird der _Text_ der Nachricht. Es gibt auch eine statische Methode, die eine binäre Nachrichtennutzlast erzeugen kann.
    

1. Rufen Sie `AddMessageAsync` für das `CloudQueue`-Objekt auf, um die Nachricht zur Warteschlange hinzuzufügen. Dies ist auch eine asynchrone Methode, weshalb Sie das Schlüsselwort `await` verwenden müssen, um sicherzustellen, dass wir richtig mit ihr interagieren.

1. Speichern Sie die Datei, und erstellen Sie sie, indem Sie `dotnet build` in das Befehlsfenster eingeben. Beheben Sie eventuelle Fehler. Sie können den folgenden Code verwenden, um Ihre Arbeit zu prüfen.

    ```csharp
    static async Task SendArticleAsync(string newsMessage)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    
        CloudQueue queue = queueClient.GetQueueReference(QueueName);
        bool createdQueue = await queue.CreateIfNotExistsAsync();
        if (createdQueue)
        {
            Console.WriteLine("The queue of news articles was created.");
        }
    
        CloudQueueMessage articleMessage = new CloudQueueMessage(newsMessage);
        await queue.AddMessageAsync(articleMessage);
    }
    ```

## <a name="add-code-to-send-a-message"></a>Hinzufügen von Code zum Senden einer Nachricht

Lassen Sie uns die `Main`-Methode modifizieren, indem wir alle empfangenen Parameter an unsere neue Methode übergeben, damit wir unsere neue Sendemethode testen können.

1. Wechseln Sie zur `Main`-Methode.

1. Überprüfen Sie den übergebenen Parameter `args`, um zu prüfen, ob Daten an die Befehlszeile übergeben wurden. Falls ja, verwenden Sie `String.Join` zum Erstellen einer einzelnen Zeichenfolge aus allen Wörtern mit einem Leerzeichen als Trennzeichen.

1. Übergeben Sie diese an die neue `SendArticleAsync`-Methode. 

1. Sobald die Rückgabe erfolgt ist, verwenden Sie `Console.WriteLine`, um die von uns gesendete Nachricht auszugeben.

1. Speichern Sie die Datei, und erstellen Sie das Programm (`dotnet build`). Sie können den nachstehenden Code zum Prüfen Ihrer Arbeit nutzen.

> [!NOTE]
> Da unsere Methode technisch asynchron ist, würden wir normalerweise das Schlüsselwort `await` verwenden. Doch dieses Feature ist für Ihre `Main`-Methode nur verfügbar, wenn Sie C# 7.2 verwenden (da es ein neues Feature ist). Um sicherzustellen, dass wir dies bei älteren Versionen der Sprache verwenden können, rufen Sie einfach `Wait()` für die Methode auf, um das Warten auf die Rückgabe der Methode zu blockieren.

    ```csharp
    static void Main(string[] args)
    {
        if (args.Length > 0)
        {
            string value = String.Join(" ", args);
            SendArticleAsync(value).Wait();
            Console.WriteLine($"Sent: {value}");
        }
    }
    ```

## <a name="execute-the-application"></a>Ausführen der Anwendung

Die Anwendung kann nun Nachrichten senden. Um Sie zu testen, können Sie sie über die Befehlszeile mit dem Befehl `dotnet run` ausführen. Zusätzliche Zeichenfolgen werden als Parameter an die Anwendung übergeben. Sie können beispielsweise Folgendes eingeben:

    ```azurecli
    dotnet run Send this message
    ```

> [!WARNING]
> Vergewissern Sie sich, dass Sie alle Dateien im Online-Editor gespeichert haben, bevor Sie das Programm erstellen und ausführen.

Dies sollte die Zeichenfolge `"Send this message"` der Warteschlange hinzufügen.

## <a name="check-your-results"></a>Überprüfen der Ergebnisse

Sie können Warteschlangen im Azure-Portal mit dem **Storage-Explorer** überprüfen. Wenn Sie dieses Produkt öffnen, können Sie die Daten in jedem Ihrer Speicherkonten untersuchen.

Alternativ können Sie auch die Azure CLI oder PowerShell verwenden. Probieren Sie diesen Befehl in der Shell aus, indem Sie den Wert `<connection-string>` durch Ihre spezifische Verbindungszeichenfolge ersetzen:

```azurecli
az storage message peek --queue-name newsqueue --connection-string <connection-string> 
```

Dies sollte die Informationen für Ihre Nachricht ausgeben, die ungefähr so aussieht:

```json
[
  {
    "content": "U2VuZCB0aGlzIG1lc3NhZ2U=",
    "dequeueCount": 0,
    "expirationTime": "2018-09-05T02:43:40+00:00",
    "id": "b47cbe9f-a246-4a81-86ae-fa02ea8d98bc",
    "insertionTime": "2018-09-24T02:43:40+00:00",
    "popReceipt": null,
    "timeNextVisible": null
  }
]
```

Es gibt noch einige andere Befehle, die Sie mit den Tools ausprobieren können. Sehen Sie sich sowohl `az storage queue --help` als auch `az storage message --help` an, um sie zu erkunden.

> [!TIP]
> Geben Sie den Wert Ihrer Verbindungszeichenfolge in eine Umgebungsvariable namens `AZURE_STORAGE_CONNECTION_STRING` ein, damit Sie den Parameter `--connection-string` nicht jedes Mal eingeben müssen!

Nachdem wir nun eine Nachricht gesendet haben, ist der letzte Schritt, Unterstützung für das _Empfangen_ der Nachricht hinzuzufügen.