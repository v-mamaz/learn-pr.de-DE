::: Zone Pivot = "Csharp" Im Folgenden fügen wir unserer .NET Core-Anwendung Unterstützung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzu. Als Erstes fügen wir die benötigte Infrastruktur zum Verwalten der Konfiguration in einer JSON-Datei hinzu.

## <a name="create-a-json-configuration-file"></a>Erstellen einer JSON-Konfigurationsdatei

1. Vergewissern Sie sich, dass Sie das richtige Arbeitsverzeichnis Ihres Projekts ausgewählt haben.

1. Verwenden Sie das Tool `touch` in der Befehlszeile, um eine Datei mit dem Namen **appsettings.json** zu erstellen.

    ```bash
    touch appsettings.json
    ```

1. Öffnen Sie das Projekt mit dem interaktiven Editor. Falls Sie lokal arbeiten, verwenden Sie den Editor Ihrer Wahl – wir empfehlen **Visual Studio Code**, eine erweiterbare plattformübergreifende integrierte Entwicklungsumgebung (IDE). Die folgenden Befehle gelten für den Cloud Shell-Editor, sind VS Code aber sehr ähnlich.
    
    ```bash
    code .
    ```

1. Wählen Sie die Datei **appsettings.json** im Editor aus, und fügen Sie den folgenden Text hinzu. Speichern Sie die Datei. Im Online-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```

1. Wählen Sie als Nächstes die Projektdatei (**PhotoSharingApp.csproj**) aus, um sie im Editor zu öffnen.

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

::: zone-pivot="javascript"

Als Nächstes fügen wir unserer Node.js-Anwendung Unterstützung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzu. Als Erstes fügen wir die benötigte Infrastruktur zum Verwalten der Konfiguration über die JavaScript-Datei hinzu.

## <a name="create-a-env-configuration-file"></a>Erstellen einer ENV-Konfigurationsdatei

1. Vergewissern Sie sich, dass Sie das richtige Arbeitsverzeichnis Ihres Projekts ausgewählt haben.

1. Verwenden Sie das Tool `touch` in der Befehlszeile, um eine Datei mit der Erweiterung **.env** zu erstellen.

    ```bash
    touch .env
    ```

1. Öffnen Sie das Projekt mit dem interaktiven Editor. Falls Sie lokal arbeiten, verwenden Sie den Editor Ihrer Wahl – wir empfehlen **Visual Studio Code**, eine erweiterbare plattformübergreifende integrierte Entwicklungsumgebung (IDE). Die folgenden Befehle gelten für den Cloud Shell-Editor, sind VS Code aber sehr ähnlich.
    
    ```bash
    code .
    ```

1. Wählen Sie die **ENV**-Datei im Editor aus, und fügen Sie den folgenden Text hinzu. Speichern Sie die Datei. Im Online-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.

    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > Der Wert **AZURE_STORAGE_CONNECTION_STRING** ist eine hartcodierte Umgebungsvariable, die für Storage-APIs zum Suchen nach Zugriffsschlüsseln verwendet wird. Sie können einen eigenen Namen verwenden, müssen diesen jedoch angeben, wenn Sie das `BlobService`-Objekt erstellen.

1. Speichern Sie die Datei.

## <a name="add-support-to-read-an-environment-configuration-file"></a>Hinzufügen von Unterstützung zum Lesen einer Umgebungskonfigurationsdatei

Sie können Node.js-Apps Unterstützung zum Lesen aus der **ENV**-Datei hinzufügen, indem Sie ihnen das **dotenv**-Paket hinzufügen.

1. Fügen Sie im Eingabeaufforderungsabschnitt des Fensters eine Abhängigkeit vom *dotenv**-Paket hinzu.

    ```bash
    node install dotenv --save
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

## <a name="add-the-connection-string-to-the-configuration-file"></a>Hinzufügen der Verbindungszeichenfolge zur Konfigurationsdatei

Nun müssen wir die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true)an.

1. Navigieren Sie zu Ihrem Speicherkonto. Sie können im Abschnitt **Alle Ressourcen** nach dem Speicherkonto suchen oder den Namen in das _Suchfeld_ oben im Portalfenster eingeben. 

1. Wählen Sie im Portal das Blatt **Zugriffsschlüssel** des Speicherkontos aus.

1. Kopieren Sie die Verbindungszeichenfolge **key1**.

1. Fügen Sie den Inhalt des Zugriffsschlüssels, den Sie aus dem Portal kopiert haben, als Wert der Konfigurationsvariable für die Verbindungszeichenfolge ein.

Die Konfiguration sollte nun etwa wie folgt aussehen:

::: zone pivot="csharp"
    ```json
    {
        "StorageAccountConnectionString": "DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net"
    }
    ```
::: zone-end

::: zone-pivot="javascript"
    ```
    AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net
    ```
::: zone-end

Nachdem wir diese Vorbereitungsschritte durchgeführt haben, können wir mit dem Hinzufügen von Code zur Verwendung unseres Speicherkontos beginnen.