Die Clientbibliothek von Azure Storage stellt ein Objektmodell bereit, das für die Interaktion mit Azure Storage-Konten verwendet wird. Es wird dazu verwendet, schnell eine Verbindung mit dem Azure Storage-Konto herzustellen und die Dienst-APIs von Azure Storage zu verwenden.

Hier verwenden Sie das Objektmodell des Kontos in Ihrem Code, um eine Verbindung mit Ihrem Azure Storage-Konto herzustellen.

## <a name="azure-storage-client-library-object-model"></a>Objektmodell der Azure Storage-Clientbibliothek

Die Verwendung des Objektmodells der Azure Storage-Clientbibliothek ist der Schlüssel zum einfachen Implementieren beim Herstellen der Verbindung mit dem Azure Storage-Konto.

In der .NET Core-Clientbibliothek stellt **CloudStorageAccount** die Grundlage des Objektmodells des Azure Storage-Kontos dar. Die einfachste Methode zum Initialisieren des Objektmodells ist die Verwendung von `CloudStorageAccount.Parse` oder `CloudStorageAccount.TryParse` zum Analysieren der Verbindungszeichenfolge.

Die Clientbibliothek versucht erst eine Verbindung herzustellen, wenn ein Vorgang aufgerufen wird, für den eine Verbindung erforderlich ist. `Parse()` und `TryParse()` stellen nur sicher, dass die Verbindungszeichenfolge korrekt formatiert ist, es wird nicht überprüft, ob das Konto existiert oder der Schlüssel richtig ist. Die resultierende `CloudStorageAccount`-Instanz, die vom Aufruf der `Parse()`- oder `TryParse()`-Methode zurückgegeben wird, stellt Methoden zum Erstellen eines Clients für die Speichertypen Blob, Datei, Tabelle oder Warteschlange zur Verfügung. Diese wird dann zum Erstellen von Instanzen von Clientobjekten für die Azure Blob-, Datei-, Warteschlangen- und Tabellenspeicherdienste verwendet. Der folgende Codeausschnitt veranschaulicht ein Beispiel zum Erstellen eines Clients zur Verwendung eines Blobspeichers:

```c#
using Microsoft.WindowsAzure.Storage;

var storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");
var blobClient = storageAccount.CreateCloudBlobClient()
```

`CloudStorageAccount` und die Clientobjekte sind einfach, sie können bei Bedarf oder direkt für die Freigabe in der Anwendung erstellt werden. Die Verwendung von `CloudStorageAccount.TryParse()` in der Nähe des Einstiegspunkts Ihrer Anwendung ist ein standardisierter Ansatz, mit dem Sie eine Instanz erstellen und in Ihrer Anwendung zur Verfügung stellen können, um Clientinstanzen zu erstellen.

## <a name="summary"></a>Zusammenfassung

Das Objektmodell der Azure Storage-Clientbibliothek bietet eine einfache Möglichkeit zum Herstellen einer Verbindung mit Ihrem Azure Storage-Konto. Ihre Aufgabe besteht darin, eine Verbindungszeichenfolge bereitzustellen. Deren Format und das Vorhandensein des Kontos wird vom Objektmodell überprüft. Sobald Sie über eine `CloudStorageAccount`-Instanz verfügen, können Sie Clients für die Speichertypen Blob, Datei, Tabelle oder Warteschlange erstellen.
