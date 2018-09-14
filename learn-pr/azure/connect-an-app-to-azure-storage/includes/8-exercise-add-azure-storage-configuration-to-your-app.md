::: zone pivot="csharp" Unterstützung lassen Sie uns auf unsere .NET Core-Anwendung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzufügen. Wir beginnen, indem Sie die erforderlichen Grundlagen zur Verwaltung der Konfiguration in eine JSON-Datei hinzufügen.

## <a name="create-a-json-configuration-file"></a>Erstellen einer JSON-Konfigurationsdatei

1. Stellen Sie sicher, dass das richtige Arbeitsverzeichnis für das Projekt ist.

1. Verwenden der `touch` Tool in der Befehlszeile zum Erstellen einer Datei mit dem Namen **"appSettings.JSON"**.

    ```bash
    touch appsettings.json
    ```

1. Öffnen Sie das Projekt in einem interaktiven Editor ein. Wenn Sie lokal arbeiten, verwenden Sie Editor Ihrer Wahl. Es wird empfohlen **Visual Studio Code**, d.h., dass einer erweiterbaren Plattform-IDE. Die folgenden Befehle sind für die Cloud Shell-Editor jedoch Visual Studio Code sehr ähnlich.

    ```bash
    code .
    ```

1. Wählen Sie die **"appSettings.JSON"** Datei im Editor, und fügen Sie den folgenden Text hinzu. Speichern Sie die Datei. Im online-Editor ist es ein Menü in der oberen rechten Ecke, die häufiger Dateivorgänge ein.

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```

1. Wählen Sie als Nächstes die Projektdatei (**PhotoSharingApp.csproj**), die sie im Editor zu öffnen.

1. Fügen Sie den folgenden Konfigurationsblock, um die neue Datei in das Projekt einfügen, und kopieren Sie ihn in den Ausgabeordner. Dadurch wird sichergestellt, dass die App-Konfigurationsdatei in das Ausgabeverzeichnis aufgenommen wird, wenn die App kompiliert/erstellt wird.

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

1. Speichern Sie die Datei. (Stellen Sie sicher, dass Sie dies tun, oder Sie verlieren die Änderung auf, wenn Sie das folgende Paket hinzufügen.)

## <a name="add-support-to-read-a-json-configuration-file"></a>Hinzufügen von Unterstützung zum Lesen einer JSON-Konfigurationsdatei

Eine .NET Core-Anwendung erfordert zusätzliche NuGet-Pakete in einer JSON-Konfigurationsdatei zu lesen.

1. Fügen Sie im Abschnitt Eingabeaufforderung des Fensters einen Verweis auf die **"Microsoft.Extensions.Configuration.JSON"** NuGet-Paket.

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a>Hinzufügen von Code zum Lesen der Konfigurationsdatei

Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Konsolenanwendung aktivieren.

1. Wählen Sie **"Program.cs"** im Editor.

1. Am Anfang der Datei befindet sich die Zeile **using System;**. Fügen Sie unter dieser Zeile die folgenden Codezeilen hinzu:

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. Ersetzen Sie den Inhalt von der **Main** Methode durch den folgenden Code. Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.

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

Fügen Sie Unterstützung für unsere Node.js-Anwendung, die eine Verbindungszeichenfolge aus einer Konfigurationsdatei abzurufen. Wir beginnen, indem Sie die erforderlichen Grundlagen zum Verwalten der Konfiguration von der JavaScript-Datei hinzufügen.

## <a name="create-a-env-configuration-file"></a>Erstellen einer env-Konfigurationsdatei

1. Stellen Sie sicher, dass das richtige Arbeitsverzeichnis für das Projekt ist.

1. Verwenden der `touch` Tool in der Befehlszeile zum Erstellen einer Datei mit dem Namen **env**.

    ```bash
    touch .env
    ```

1. Öffnen des Projekts mit der interaktiven Editor, wenn Sie lokal arbeiten verwenden-Editor Ihrer Wahl – es wird empfohlen **Visual Studio Code** d.h., dass einer erweiterbaren Plattform-IDE. Die folgenden Befehle sind für die Cloud Shell-Editor, aber Visual Studio Code sehr ähnlich sind.
    
    ```bash
    code .
    ```

1. Wählen Sie die **env** Datei im Editor, und fügen Sie den folgenden Text hinzu. Speichern Sie die Datei - online-Editor müssen Sie ein Menü vorhanden ist, in der oberen rechten Ecke die häufiger Dateivorgänge verfügt.

    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > Die **AZURE_STORAGE_CONNECTION_STRING** Wert ist eine hartcodierte Umgebungsvariable zum Storage-APIs, um Zugriffstasten zu suchen. Sie können Ihre eigenen Namen verwenden, wenn gewünscht, aber Sie müssen den Namen angeben, wann Sie erstellen die `BlobService` Objekt.

1. Speichern Sie die Datei.

## <a name="add-support-to-read-an-environment-configuration-file"></a>Hinzufügen von Unterstützung zum Lesen der Datei zum Konfigurieren einer Umgebung

Node.js-apps zählen die Unterstützung zum Lesen aus der **env** Datei durch Hinzufügen der **Dotenv** Paket.

1. Fügen Sie im Abschnitt Eingabeaufforderung des Fensters eine Abhängigkeit zu der *Dotenv**-Pakets mit `npm`.

    ```bash
    npm install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a>Hinzufügen von Code zum Lesen der Konfigurationsdatei

Nun, da wir die erforderlichen Bibliotheken zum Lesen der Konfiguration aktivieren hinzugefügt haben, müssen wir diese Funktionalität in unserer Anwendung zu aktivieren.

1. Wählen Sie *"Index.js"** im Editor.

1. Am Anfang der Datei eine **#! / Usr/Bin/Env Knoten** Zeile vorhanden ist. Unterhalb dieser Zeile Hinzufügen einer `require` Anweisung beim Laden der **Dotenv** Paket. Dies veranlasst die Umgebungsvariablen, die unserer **env** Datei des Programms zur Verfügung.

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    ```
::: zone-end

## <a name="add-the-connection-string-to-the-configuration-file"></a>Fügen Sie die Verbindungszeichenfolge in die Konfigurationsdatei

Nun müssen wir die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true)an.

1. Navigieren Sie zum Speicherkonto. Können Sie die **alle Ressourcen** Abschnitt, um das Storage-Konto zu suchen, oder eine Suche anhand des Namens aus der _Suchfeld_ am oberen Rand des portalfensters.

1. Wählen Sie die **Zugriffsschlüssel** auf dem Blatt des Speicherkontos im Portal.

1. Kopieren der **"Key1"** Verbindungszeichenfolge.

1. Fügen Sie den Inhalt des Zugriffsschlüssels, die Sie als Wert für die Konfiguration verbindungszeichenfolgenvariablen aus dem Portal kopiert haben.

Die Konfiguration sollte nun etwa wie folgt aussehen:

::: zone pivot="csharp"
```json
{
    "StorageAccountConnectionString": "DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net"
}
```
::: zone-end

::: zone pivot="javascript"
```
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net
```
::: zone-end

Nun, wir haben, dass alle verbunden, beginnen wir, Hinzufügen von Code, um unserem Speicherkonto zu verwenden.
