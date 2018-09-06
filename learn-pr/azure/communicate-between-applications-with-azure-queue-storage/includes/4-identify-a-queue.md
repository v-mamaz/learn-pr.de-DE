Nun, da wir ein Speicherkonto haben, wollen wir uns ansehen, wie wir mit der Warteschlange arbeiten, die darin enthalten sein wird.

Um auf eine Warteschlange zugreifen zu können, benötigen Sie drei Informationen:
 1. Speicherkontoname
 2. Warteschlangenname
 3. Autorisierungstoken

Diese Informationen werden von beiden Anwendungen verwendet, die mit der Warteschlange kommunizieren (dem Web-Front-End, das Nachrichten hinzufügt, und der mittleren Ebene, die sie verarbeitet).

## <a name="queue-identity"></a>Identität der Warteschlange

Jede Warteschlange hat einen Namen, den Sie bei der Erstellung festlegen. Der Name muss innerhalb Ihres Speicherkonto eindeutig, aber nicht global eindeutig sein (im Gegensatz zum Namen des Speicherkontos).

Die Kombination aus Ihrem Speicherkontonamen und Warteschlangennamen ermöglicht die eindeutige Identifizierung einer Warteschlange.

## <a name="access-authorization"></a>Zugriffsautorisierung

Jede Anforderung an eine Warteschlange muss autorisiert werden, wofür mehrere Optionen zur Auswahl stehen.

| Autorisierungstyp | Beschreibung |
|--------------------|-------------|
| **Azure Active Directory** (AAD) | Sie können die rollenbasierte Authentifizierung verwenden und bestimmte Clients anhand von AAD-Anmeldeinformationen identifizieren. |
| **Gemeinsam verwendeter Schlüssel** | Dies ist eine mitunter als **Kontoschlüssel** bezeichnete verschlüsselte Schlüsselsignatur, die dem Speicherkonto zugeordnet ist. Jedes Speicherkonto verfügt über zwei dieser Schlüssel, die bei jeder Anforderung zur Authentifizierung des Zugriffs übergeben werden können. Die Befolgung dieses Ansatzes ist wie die Verwendung eines Root-Kennworts und ermöglicht _Vollzugriff_ auf das Speicherkonto. |
| **Shared Access Signature (SAS)** | Eine Shared Access Signature (SAS) ist ein generierter URI, der Clients eingeschränkten Zugriff auf Objekte in Ihrem Speicherkonto gewährt. Sie können den Zugriff auf bestimmte Ressourcen, Berechtigungen und den Umfang auf einen Datenbereich einschränken, um den Zugriff nach einem bestimmten Zeitraum automatisch zu deaktivieren.  |

> [!NOTE]
> Wir werden die Kontoschlüsselautorisierung verwenden, da dies der einfachste Weg ist, mit dem Arbeiten mit Warteschlangen anzufangen. Es wird jedoch empfohlen, in Produktionsanwendungen entweder die Shared Access Signatur (SAS) oder Azure Active Directory (AAD) zu verwenden.

### <a name="retrieving-the-account-key"></a>Abrufen des Kontoschlüssels
 
Ihr Kontoschlüssel ist im Abschnitt **Einstellungen > Zugriffsschlüssel** Ihres Speicherkontos im Azure-Portal verfügbar. Sie können ihn aber auch über die Befehlszeile abrufen:

```azurecli
az storage account keys list ...
```

```powershell
Get-AzureRmStorageAccountKey ...
```

## <a name="accessing-queues"></a>Zugreifen auf Warteschlangen

Sie greifen auf eine Warteschlange über eine REST-API zu. Dazu verwenden Sie eine URL, die den von Ihnen vergebenen Namen des Speicherkontos mit der Domäne `queue.core.windows.net` und dem Pfad zur Warteschlange kombiniert, mit der Sie arbeiten möchten. Beispiel: `http://<storage account>.queue.core.windows.net/<queue name>`. Ein Header des Typs `Authorization` muss jeder Anforderung hinzugefügt werden. Der Wert kann einer der drei Autorisierungsstile sein.

### <a name="using-the-azure-storage-client-library-for-net"></a>Verwenden der Azure Storage-Clientbibliothek für .NET

Die Azure Storage-Clientbibliothek für .NET ist eine Bibliothek von Microsoft, die REST-Anforderungen formuliert und REST-Antworten für Sie analysiert. Dadurch verringert sich der Umfang des zu schreibenden Codes erheblich. Für den Zugriff über die Clientbibliothek werden weiterhin die gleichen Informationen (Speicherkonto- und Warteschlangenname sowie Kontoschlüssel) benötigt, die jedoch unterschiedlich organisiert sind.

Die Clientbibliothek verwendet eine **Verbindungszeichenfolge**, um Ihre Verbindung herzustellen. Ihre Verbindungszeichenfolge ist im Abschnitt **Einstellungen** Ihres Speicherkontos im Azure-Portal oder über die Azure CLI und PowerShell verfügbar.

Eine Verbindungszeichenfolge ist eine Zeichenfolge, die einen Speicherkontonamen und Kontoschlüssel kombiniert und der Anwendung für den Zugriff auf das Speicherkonto bekannt sein muss. Das Format ist wie folgt:

```csharp
string connectionString = "DefaultEndpointsProtocol=https;AccountName=<your storage account name>;AccountKey=<your key>;EndpointSuffix=core.windows.net"
```

> [!WARNING]
> Dieser Zeichenfolgenwert muss an einem sicheren Ort gespeichert werden, da jeder mit Zugriff auf diese Verbindungszeichenfolge die Warteschlange manipulieren könnte.

Beachten Sie, dass die Verbindungszeichenfolge nicht den Namen der Warteschlange enthält. Der Warteschlangenname wird in Ihrem Code bereitgestellt, wenn Sie eine Verbindung mit der Warteschlange herstellen.

Lassen Sie uns unsere Verbindungszeichenfolge aus Azure abrufen und eine neue Anwendung einrichten, die sie verwendet.
