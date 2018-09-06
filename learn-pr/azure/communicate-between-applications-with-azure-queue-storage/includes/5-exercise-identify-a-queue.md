Erstellen Sie eine Client-App für die Arbeit mit einer Warteschlange. Anschließend fügen Sie die Verbindungszeichenfolge in den Code ein.

## <a name="create-the-application"></a>Erstellen der Anwendung

Erstellen Sie eine .NET Core-Anwendung, die Sie unter Linux, macOS oder Windows ausführen können. Geben Sie ihr den Namen **QueueApp**. Der Einfachheit halber verwenden Sie hierzu eine einzelne App, die Nachrichten über die Warteschlange sendet und empfängt.

1. Verwenden Sie den Befehl `dotnet new`, um eine neue Konsolenanwendung mit dem Namen **QueueApp** zu erstellen. Sie können Befehle rechts in Cloud Shell eingeben. Wenn Sie lokal arbeiten, verwenden Sie alternativ ein Terminal bzw. ein Konsolenfenster. Hiermit wird eine einfache App mit einer einzelnen Quelldatei (`Program.cs`) erstellt.

    ```azurecli
    dotnet new console -n QueueApp
    ```

2. Wechseln Sie zum neu erstellten `QueueApp`-Ordner, und erstellen Sie die App, um sicherzustellen, dass alles funktioniert hat.

    ```azurecli
    cd QueueApp
    ```

    ```azurecli
    dotnet build
    ```

## <a name="get-your-connection-string"></a>Abrufen der Verbindungszeichenfolge

Vergessen Sie nicht, dass Sie die Verbindungszeichenfolge im Azure-Portal im Abschnitt **Einstellungen > Zugriffsschlüssel** Ihres Speicherkontos finden können.

Sie können sie auch über Azure CLI oder PowerShell-Tools abrufen. Verwenden Sie den Azure CLI-Befehl. Denken Sie daran, `<name>` durch den spezifischen Namen des Speicherkontos zu ersetzen, das Sie erstellt haben. Sie können `az storage account list` verwenden, wenn Sie eine Erinnerung benötigen.

```azurecli
az storage account show-connection-string --name <name> --resource-group ExerciseResources
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

2. Öffnen Sie die Quelldatei `Program.cs` im Projekt.

3. Fügen Sie einen `const string`-Wert in die `Program`-Klasse hinzu, der die Verbindungszeichenfolge enthält. Nur der Wert ist erforderlich (er beginnt mit dem Text **DefaultEndpointsProtocol**).

4. Speichern Sie die Datei. Sie können in der rechten Ecke des Cloud-Editors auf die Schaltfläche mit den Auslassungspunkten (...) klicken, dabei wird Ihnen auch die Tastenkombination angezeigt.

Der Code sollte etwa wie folgt aussehen (Ihr Zeichenfolgenwert ist für Ihr Konto eindeutig).

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