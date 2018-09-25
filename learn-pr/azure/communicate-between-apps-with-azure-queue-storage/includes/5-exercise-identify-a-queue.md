Erstellen Sie eine Client-App für die Arbeit mit einer Warteschlange. Anschließend fügen wir die Verbindungszeichenfolge in den Code ein.

> [!NOTE]
> Sie können die Clientanwendung entweder auf Ihrem lokalen Computer erstellen, sofern dort .NET Core installiert ist, oder aber direkt in der Cloud Shell-Umgebung.

## <a name="create-the-application"></a>Erstellen der Anwendung

Erstellen Sie eine .NET Core-Anwendung, die Sie unter Linux, macOS oder Windows ausführen können. Geben Sie ihr den Namen **QueueApp**. Der Einfachheit halber verwenden Sie hierzu eine einzelne App, die Nachrichten über die Warteschlange sendet und empfängt.

1. Verwenden Sie den Befehl `dotnet new`, um eine neue Konsolenanwendung mit dem Namen **QueueApp** zu erstellen. Sie können Befehle rechts in Cloud Shell eingeben. Wenn Sie lokal arbeiten, verwenden Sie alternativ ein Terminal- bzw. ein Konsolenfenster. Mit diesem Befehl wird eine einfache App mit einer einzelnen Quelldatei (`Program.cs`) erstellt.

    ```azurecli
    dotnet new console -n QueueApp
    ```

1. Wechseln Sie zum neu erstellten Ordner `QueueApp`, und erstellen Sie die App, um sich zu vergewissern, dass alles funktioniert hat.

    ```azurecli
    cd QueueApp
    ```

    ```azurecli
    dotnet build
    ```

## <a name="get-your-connection-string"></a>Abrufen der Verbindungszeichenfolge

Vergessen Sie nicht, dass Sie die Verbindungszeichenfolge im Azure-Portal im Abschnitt **Einstellungen > Zugriffsschlüssel** Ihres Speicherkontos finden.

Sie können sie auch über die Azure CLI oder PowerShell-Tools abrufen. Verwenden Sie den Azure CLI-Befehl. Denken Sie daran, `<name>` durch den spezifischen Namen des Speicherkontos zu ersetzen, das Sie erstellt haben. Sie können `az storage account list` verwenden, wenn Sie eine Erinnerung benötigen.

```azurecli
az storage account show-connection-string --name <name> --resource-group <rgn>[sandbox resource group name]</rgn>
```

Dieser Befehl gibt einen JSON-Block mit Ihrer Verbindungszeichenfolge zurück. Er enthält den Namen und den Kontoschlüssel des Speicherkontos:

```json
{
  "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=<name>;AccountKey=vyw6aKz2PtSAgQ4ljJQgJFgxbCETdXt39ZyYQ5fLqoBJj/gT+43TbrhoVco7Rqj/AAJVlvFORRfnYqGHiX9QcQ=="
}
```

## <a name="add-the-connection-string-to-the-application"></a>Hinzufügen der Verbindungszeichenfolge in die Anwendung

Abschließend fügen Sie die Verbindungszeichenfolge in die App ein, damit sie auf das Speicherkonto zugreifen kann.

> [!WARNING]
> Der Einfachheit halber platzieren Sie die Verbindungszeichenfolge in die Datei **Program.cs**. Für eine Produktionsanwendung sollten Sie sie an einem sicheren Ort speichern. Für die serverseitige Verwendung wird Azure Key Vault empfohlen.

1. Geben Sie `code .` im Terminal ein, um den Onlinecode-Editor zu öffnen. Wenn Sie alleine arbeiten, können Sie alternativ die IDE Ihrer Wahl verwenden. Hierfür empfiehlt sich Visual Studio Code, da es sich dabei um eine hervorragende plattformübergreifende IDE handelt.

1. Öffnen Sie die Quelldatei `Program.cs` im Projekt.

1. Fügen Sie einen `const string`-Wert in die `Program`-Klasse hinzu, der die Verbindungszeichenfolge enthält. Nur der Wert ist erforderlich (er beginnt mit dem Text **DefaultEndpointsProtocol**).

1. Speichern Sie die Datei. Dazu können Sie entweder auf die drei Punkte (...) auf der rechten Seite des Cloud-Editors klicken oder die entsprechende Tastenkombination verwenden (<kbd>STRG+S</kbd> unter Windows und Linux, <kbd>CMD+S</kbd> unter macOS).

Der Code sollte etwa wie folgt aussehen (der Zeichenfolgenwert ist für Ihr Konto eindeutig).

```csharp
...
namespace QueueApp
{
    class Program
    {
        private const string ConnectionString = "DefaultEndpointsProtocol=https; ...";
        
        ...
    }
}
```

Da Sie das Starterprojekt nun eingerichtet haben, sehen Sie sich als Nächstes an, wie Sie im Code mit einer Warteschlange arbeiten können. _Meldungen_ stellen den Anfang dar.