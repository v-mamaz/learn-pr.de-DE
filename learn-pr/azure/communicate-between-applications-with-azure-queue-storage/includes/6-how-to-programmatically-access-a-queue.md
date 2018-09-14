Warteschlangen speichern Nachrichten – Datenpakete, deren Form Sender und Empfänger bekannt ist. Der Sender erstellt die Warteschlange und fügt eine Nachricht hinzu. Der Empfänger empfängt eine Nachricht, verarbeitet sie und löscht dann die Nachricht aus der Warteschlange. Die folgende Abbildung zeigt einen typischen Fluss dieses Prozesses.

![Abbildung eines typischen Nachrichtenflusses durch die Azure-Warteschlange.](../media/6-message-flow.png)

Beachten Sie, dass `get` und `delete` separate Vorgänge sind. In dieser Anordnung werden potenzielle Ausfälle im Empfänger behandelt und ein Konzept namens _at-least-once-delivery_ implementiert. Nachdem der Empfänger eine Nachricht erhalten hat, verbleibt die Nachricht in der Warteschlange, ist jedoch 30 Sekunden lang unsichtbar. Wenn der Empfänger abstürzt oder dort während der Verarbeitung ein Stromausfall auftritt, wird die Nachricht dadurch niemals aus der Warteschlange entfernt. Nach 30 Sekunden wird die Nachricht erneut in der Warteschlange angezeigt, und eine andere Instanz des Empfängers kann sie abschließend verarbeiten.

## <a name="the-azure-storage-client-library-for-net"></a>Die Azure-Speicherclientbibliothek für .NET

Die **Azure-Speicherclientbibliothek für .NET** bietet Typen zur Darstellung aller Objekte, mit denen Sie interagieren müssen:

- `CloudStorageAccount` stellt Ihr Azure-Speicherkonto dar.
- `CloudQueueClient` stellt Ihre Azure-Warteschlange dar.
- `CloudQueue` stellt eine Ihrer Warteschlangeninstanzen dar.
- `CloudQueueMessage` stellt eine Nachricht dar.

Sie verwenden diese Klassen zum programmgesteuerten Zugriff auf Ihre Warteschlange. Die Bibliothek enthält synchrone und asynchrone Methoden; Sie sollten die asynchronen Versionen verwenden, um ein Blockieren der Client-App zu vermeiden.

> [!NOTE]
> Die Azure-Speicherclientbibliothek für .NET finden Sie im **WindowsAzure.Storage**-NuGet-Paket. Sie können sie über eine IDE, die Azure-Befehlszeilenschnittstelle oder PowerShell `Install-Package WindowsAzure.Storage` installieren.

## <a name="how-to-connect-to-a-queue"></a>Herstellen einer Verbindung mit einer Warteschlange

Um eine Verbindung mit einer Warteschlange herzustellen, erstellen Sie zunächst ein `CloudStorageAccount` mit Ihrer Verbindungszeichenfolge. Das resultierende Objekt kann dann einen `CloudQueueClient` erstellen, der wiederum eine `CloudQueue`-Instanz öffnen kann. Der grundlegende Codefluss ist unten dargestellt.

```csharp
CloudStorageAccount account = CloudStorageAccount.Parse(connectionString);

CloudQueueClient client = account.CreateCloudQueueClient();

CloudQueue queue = client.GetQueueReference("myqueue");
```

Das Erstellen einer `CloudQueue` bedeutet nicht unbedingt, dass die _tatsächliche_ Speicherwarteschlange vorhanden ist. Allerdings können Sie mit diesem Objekt eine Warteschlange erstellen, löschen und prüfen, ob eine Warteschlange vorhanden ist. Wie oben erwähnt, unterstützen alle Methoden sowohl synchrone als auch asynchrone Versionen, aber wir verwenden nur die `Task`-basierten asynchronen Versionen.

## <a name="how-to-create-a-queue"></a>Erstellen von Warteschlangen

Sie verwenden ein allgemeines Muster für die Warteschlangenerstellung: Die Senderanwendung sollte immer für das Erstellen der Warteschlange verantwortlich sein. Auf diese Weise bleibt Ihre Anwendung eigenständiger und ist weniger abhängig vom Administratorsetup. 

Um die Erstellung zu vereinfachen, macht die Clientbibliothek eine `CreateIfNotExistsAsync`-Methode verfügbar, die ggf. die Warteschlange erstellt oder `false` zurückgibt, wenn die Warteschlange bereits vorhanden ist. 

Der typische Code wird im Folgenden gezeigt.

```csharp
CloudQueue queue;
//...

await queue.CreateIfNotExistsAsync();
```

> [!NOTE]
> Sie benötigen `Write`- oder `Create`-Berechtigungen, damit das Speicherkonto diese API verwenden kann. Dies ist bei Verwendung des **Zugriffsschlüssel**-Sicherheitsmodells immer zutreffend, aber Sie können Berechtigungen für das Konto mit anderen Ansätzen sperren, die nur Lesevorgänge für die Warteschlange zulassen.

## <a name="how-to-send-a-message"></a>Senden einer Nachricht

Um eine Nachricht zu senden, instanziieren Sie ein `CloudQueueMessage`-Objekt. Die Klasse verfügt über einige überladene Konstruktoren, die Ihre Daten in die Nachricht laden. Wir verwenden den Konstruktor, der einen `string` entgegennimmt. Nach dem Erstellen der Nachricht senden Sie sie mit einem `CloudQueue`-Objekt.

Hier sehen Sie ein typisches Beispiel:

```csharp
var message = new CloudQueueMessage("your message here");

CloudQueue queue;
//...

await queue.AddMessageAsync(message);
```

> [!NOTE]
> Die gesamte Warteschlangengröße kann bis zu 500TB betragen, die einzelnen Nachrichten darin können nur bis zu 64KB groß sein (48KB bei Base64-Codierung). Wenn Sie eine größere Nutzlast benötigen, können Sie Warteschlangen und Blobs kombinieren – übergeben Sie die URL den (als Blob gespeicherten) eigentlichen Daten in der Nachricht. Mit diesem Ansatz könnten Sie bis zu 200GB für ein einzelnes Element in die Warteschlange einreihen.

## <a name="how-to-receive-and-delete-a-message"></a>Empfangen und Löschen einer Nachricht

Im Empfänger erhalten Sie die nächste Nachricht, verarbeiten sie und löschen sie nach erfolgreicher Verarbeitung. Hier ist ein einfaches Beispiel:

```C#
CloudQueue queue;
//...

CloudQueueMessage message = await queue.GetMessageAsync();

if (message != null)
{
    // Process the message
    //...

    await queue.DeleteMessageAsync(message);
}
```

Lassen Sie uns jetzt dieses neuen Wissen auf unsere Anwendung anwenden!