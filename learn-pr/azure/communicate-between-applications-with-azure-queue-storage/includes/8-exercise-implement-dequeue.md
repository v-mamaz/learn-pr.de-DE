Nun wollen wir die Anwendung komplettieren, indem wir Code schreiben, um die nächste Nachricht in der Warteschlange zu lesen, sie zu verarbeiten und dann aus der Warteschlange zu löschen. 

Wir binden diesen Code in die gleiche Anwendung ein und führen ihn aus, wenn Sie keine Parameter übergeben. Aber in unserem Nachrichtenservice-Szenario fügen wir diesen Code unseren Servern auf mittlerer Ebene zu, um die Meldungen weiterzuverarbeiten.

## <a name="dequeue-a-message"></a>Entfernen einer Nachricht aus der Warteschlange

Lassen Sie uns eine neue Methode hinzufügen, die die nächste Nachricht aus der Warteschlange abruft.

1. Wechseln Sie in der Cloud Shell zum Ordner `QueueApp` und geben Sie `code .` ein, um den Online-Editor zu öffnen.
 
2. Öffnen Sie die Quelldatei `Program.cs`.

3. Erstellen Sie eine statische Methode in der `Program`-Klasse mit dem Namen `ReceiveArticleAsync`, die keine Parameter verwendet und `Task<string>` zurückgibt. Wir nutzen diese Methode, um eine Nachrichtenmeldung der Warteschlange zu entnehmen und zurückzugeben.
    - Fahren Sie fort, indem Sie das Schlüsselwort `async` der Methode hinzufügen, da wir einige asynchrone, auf `Task` basierende Methoden verwenden werden.

    ```csharp
    static async Task<string> ReceiveArticleAsync()
    {
    }

4. All of the setup code to get a `CloudQueue` will be identical to what we did in the last exercise. Code duplication is a bad habit, even in samples so go ahead and, refactor the code that obtains the `CloudQueue` to a new method named `GetQueue` and change the `SendArticleAsync` to use your new method.
     - Make sure to leave the code that _creates_ the queue in the `SendArticleAsync` method; remember only the **publisher** should create the queue.

    ```csharp
    const string ConnectionString = ...;
    // ...

    static CloudQueue GetQueue()
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
    
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        return queueClient.GetQueueReference("newsqueue");
    }
    ```
    
5. Rufen Sie in Ihrer `ReceiveArticleAsync`-Methode die neue `GetQueue`-Methode auf, um Ihren Warteschlangenverweis abzurufen und ihn einer Variablen zuzuweisen.

6. Rufen Sie als Nächstes die `ExistsAsync`-Methode für das `CloudQueue`-Objekt auf, die zurückgibt, ob die Warteschlange erstellt wurde. Wenn wir versuchen, eine Nachricht aus einer nicht vorhandenen Warteschlange abzurufen, löst die API eine Ausnahme aus.
    - Diese Methode ist asynchron, weshalb Sie `await` verwenden, um den Rückgabewert abzurufen.
    - Das Schlüsselwort `async` sollte bereits für die `ReceiveArticleAsync`-Methode vorhanden sein. Falls nicht, fügen Sie es jetzt hinzu.


7. Fügen Sie einen `if`-Block hinzu, der den Rückgabewert von `ExistsAsync` verwendet. Wir fügen unseren Code hinzu, um einen Wert aus der Warteschlange in den Block einzulesen. Fügen Sie eine abschließende Rückgabezeichenfolge zur Methode hinzu, die angibt, dass kein Wert gelesen wurde. Ihre Methode sollte in etwa so aussehen:

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
    }

    return "<queue empty or not created>";
}
```

8. Rufen Sie `GetMessageAsync` für das `CloudQueue`-Objekt auf, um die erste `CloudQueueMessage` aus der Warteschlange abzurufen. Der zurückgegebene Wert ist `null`, wenn die Warteschlange leer ist.

9. Falls nicht NULL, verwenden Sie die `AsString`-Eigenschaft für das `CloudQueueMessage`-Objekt, um den Inhalt der Nachricht abzurufen.

10. Rufen Sie `DeleteMessageAsync` für das `CloudQueue`-Objekt auf, um die Nachricht aus der Warteschlange zu löschen.

Die letzte Implementierung der Methode sollte so aussehen:

```csharp
static async Task<string> ReceiveArticleAsync()
{
    CloudQueue queue = GetQueue();
    bool exists = await queue.ExistsAsync();
    if (exists)
    {
        CloudQueueMessage retrievedArticle = await queue.GetMessageAsync();
        if (retrievedArticle != null)
        {
            string newsMessage = retrievedArticle.AsString;
            await queue.DeleteMessageAsync(retrievedArticle);
            return newsMessage;
        }
    }

    return "<queue empty or not created>";
}
```
## <a name="call-the-receivearticleasync-method"></a>Aufrufen der ReceiveArticleAsync-Methode

Abschließend fügen wir noch Unterstützung zum Aufrufen unserer neuen Methode hinzu. Dies erfolgt, wenn wir keine Parameter an das Programm übergeben.

1. Navigieren Sie zur `Main`-Methode und insbesondere zum `if`-Block, den Sie zuvor hinzugefügt haben, um nach Parametern zu suchen.
1. Fügen Sie eine `else`-Bedingung hinzu, und rufen die `ReceiveArticleAsync`-Methode auf. 
1. Da sie asynchron ist, würden wir normalerweise `await` verwenden. Wie jedoch bereits erläutert, funktioniert das nicht in allen Versionen von C#. Nutzen Sie also einfach die `Result`-Eigenschaft, um den Rückgabewert abzurufen und ihn im Konsolenfenster auszugeben.

Ihr Code sollte ungefähr wie folgt aussehen:

```csharp
if (args.Length > 0)
{
    // ...
}
else
{
    string value = ReceiveArticleAsync().Result;
    Console.WriteLine($"Received {value}");
}
```

## <a name="execute-the-application"></a>Ausführen der Anwendung

Der Code ist nun vollständig. Er kann jetzt Nachrichten senden und abrufen. Um ihn zu testen, verwenden Sie `dotnet run`, und übergeben Sie Parameter, um Nachrichten zu senden, und lassen Sie Parameter weg, um eine einzelne Nachricht zu lesen.

Falls Sie testen möchten, wenn keine Warteschlange vorhanden ist, können Sie die Warteschlange (und alle Daten) mit der Azure CLI löschen. Ersetzen Sie unbedingt den Parameter `<connection-string>` (oder legen Sie die Umgebungsvariable fest).

```azurecli
az storage queue delete --name newsqueue --connection-string <connection-string> 
```

Beim nächsten Hinzufügen einer Nachricht muss die Warteschlange neu erstellt werden.