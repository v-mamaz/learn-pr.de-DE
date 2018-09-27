::: Zone Pivot = "Csharp" Im Folgenden fügen wir unserer .NET Core-Anwendung Unterstützung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzu. Als Erstes fügen wir die benötigte Infrastruktur zum Verwalten der Konfiguration in einer JSON-Datei hinzu.

## <a name="create-a-json-configuration-file"></a>Erstellen einer JSON-Konfigurationsdatei

1. Wechseln Sie mit `cd` in das Verzeichnis „PhotoSharingApp“, wenn Sie dieses nicht bereits aufgerufen haben.

1. Verwenden Sie das Tool `touch` über die Befehlszeile, um eine Datei mit dem Namen **appsettings.json** zu erstellen.

    ```bash
    touch appsettings.json
    ```

1. Öffnen Sie das Projekt in einem Editor. Wenn Sie lokal arbeiten, können Sie einen beliebigen Editor verwenden. Empfohlen wird die erweiterbare, plattformübergreifende IDE **Visual Studio Code**. Wenn Sie in Cloud Shell arbeiten, wird der Cloud Shell-Editor empfohlen. Der folgende Befehl funktioniert in beiden Editoren.

    ```bash
    code .
    ```

1. Wählen Sie die Datei **appsettings.json** im Editor aus, und fügen Sie den folgenden Text hinzu. Speichern Sie die Datei. Im Cloud Shell-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.

    ```json
    {
      "StorageAccountConnectionString": "<value>"
    }
    ```

1. Nun müssen Sie die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen. Führen Sie in Cloud Shell den folgenden Befehl aus.

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name <name> \
        --query connectionString
    ```

1. Kopieren Sie die Verbindungszeichenfolge, die von diesem Befehl zurückgegeben wird, und ersetzen Sie `"<value>"` in der Datei **appsettings.json** durch diese Verbindungszeichenfolge. Speichern Sie die Datei.

1. Öffnen Sie als Nächstes die Projektdatei (**PhotoSharingApp.csproj**) im Editor.

1. Fügen Sie den folgenden Konfigurationsblock hinzu, um die neue Datei in das Projekt einzuschließen und sie in den Ausgabeordner zu kopieren. Dadurch wird sichergestellt, dass die App-Konfigurationsdatei beim Kompilieren/Erstellen der App im Ausgabeverzeichnis abgelegt wird.

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
       ...
        <ItemGroup>
            <None Update="appsettings.json">
              <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
            </None>
        </ItemGroup>
    </Project>
    ```

1. Speichern Sie die Datei. (Andernfalls gehen die Änderungen verloren, wenn Sie das Paket weiter unten hinzufügen!)

## <a name="add-support-to-read-a-json-configuration-file"></a>Hinzufügen von Unterstützung zum Lesen einer JSON-Konfigurationsdatei

Eine .NET Core-Anwendung benötigt zusätzliche NuGet-Pakete, um eine JSON-Konfigurationsdatei zu lesen.

1. Fügen Sie im Eingabeaufforderungsabschnitt des Fensters einen Verweis auf das NuGet-Paket **Microsoft.Extensions.Configuration.Json** hinzu.

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a>Hinzufügen von Code zum Lesen der Konfigurationsdatei

Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Konsolenanwendung aktivieren.

1. Wählen Sie im Editor die Datei **Program.cs** aus.

1. Die Datei enthält am Anfang eine Zeile **using System;**. Fügen Sie unter dieser Zeile die folgenden Codezeilen hinzu:

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. Ersetzen Sie den Inhalt der **Main**-Methode durch den nachstehenden Code. Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

Ihre Datei **Program.cs** sollte jetzt wie folgt aussehen:

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace PhotoSharingApp
{
    class Program
    {
        static void Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();
        }
    }
}
```

::: zone-end

::: zone pivot="javascript"

Als Nächstes fügen Sie der Node.js-Anwendung Unterstützung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzu. Als Erstes fügen wir die benötigte Infrastruktur zum Verwalten der Konfiguration über die JavaScript-Datei hinzu.

## <a name="create-a-env-configuration-file"></a>Erstellen einer ENV-Konfigurationsdatei

1. Vergewissern Sie sich, dass Sie das richtige Arbeitsverzeichnis Ihres Projekts ausgewählt haben.

1. Verwenden Sie das Tool `touch` über die Befehlszeile, um eine Datei mit der Erweiterung **ENV** zu erstellen.

    ```bash
    touch .env
    ```

1. Öffnen Sie das Projekt im Cloud Shell-Editor.

    ```bash
    code .
    ```

1. Wählen Sie die **ENV**-Datei im Editor aus, und fügen Sie den folgenden Text hinzu. Sie müssen möglicherweise auf die Aktualisierungsschaltfläche im Code klicken, damit die neuen Dateien angezeigt werden. Speichern Sie die Datei. Im Online-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.

    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > Der Wert **AZURE_STORAGE_CONNECTION_STRING** ist eine hartcodierte Umgebungsvariable, die für Storage-APIs zum Suchen nach Zugriffsschlüsseln verwendet wird. Sie können einen eigenen Namen verwenden, müssen diesen jedoch angeben, wenn Sie das `BlobService`-Objekt in Ihrer Node.js-App erstellen.

1. Nun müssen Sie die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen. Führen Sie in Cloud Shell den folgenden Befehl aus.

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name <name> \
        --query connectionString
    ```

1. Kopieren Sie die Verbindungszeichenfolge, die von diesem Befehl zurückgegeben wird (ohne die Anführungszeichen), und ersetzen Sie `<value>` in der **ENV**-Datei durch diese Verbindungszeichenfolge.

1. Speichern Sie die Datei.

## <a name="add-support-to-read-an-environment-configuration-file"></a>Hinzufügen von Unterstützung zum Lesen einer Umgebungskonfigurationsdatei

Sie können Node.js-Apps Unterstützung zum Lesen aus der **ENV**-Datei hinzufügen, indem Sie ihnen das **dotenv**-Paket hinzufügen.

1. Fügen Sie im Eingabeaufforderungsabschnitt des Fensters mithilfe von `npm` eine Abhängigkeit vom *dotenv**-Paket hinzu.

    ```bash
    npm install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a>Hinzufügen von Code zum Lesen der Konfigurationsdatei

Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Anwendung aktivieren.

1. Wählen Sie im Editor *index.js** aus.

1. Die Datei enthält am Anfang eine Zeile **#!/usr/bin/env node**. Fügen Sie unterhalb dieser Zeile eine `require`-Anweisung zum Laden des **dotenv**-Pakets hinzu. Dadurch werden die in der **ENV**-Datei definierten Umgebungsvariablen für das Programm verfügbar gemacht.

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    ```
::: zone-end

Nachdem wir diese Vorbereitungsschritte durchgeführt haben, können wir mit dem Hinzufügen von Code zur Verwendung unseres Speicherkontos beginnen.