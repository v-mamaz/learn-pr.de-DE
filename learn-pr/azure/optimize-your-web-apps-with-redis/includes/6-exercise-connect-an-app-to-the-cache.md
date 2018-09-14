Nun, da wir einen Redis-Cache in Azure erstellt haben, erstellen wir eine Anwendung verwenden. Stellen Sie sicher, dass Sie die Informationen der Verbindungszeichenfolge aus dem Azure-Portal verfügen.

> [!NOTE]
> Der integrierte Cloud Shell ist verfügbar auf der rechten Seite. Sie können diese Eingabeaufforderung verwenden, erstellen und führen Sie den Beispielcode, den wir erstellen hier oder lokal verwendet werden, wenn Sie eine Entwicklungsumgebung haben, diese Schritte ausführen. Wenn Sie die Cloud Shell verwenden möchten, und wählen Sie die Bash-Shell, wenn Sie eine Auswahl aufgefordert werden.

## <a name="create-a-console-application"></a>Erstellen einer Konsolenanwendung

Wir verwenden eine einfache Konsolenanwendung, damit wir auf die Redis-Implementierung konzentrieren können.

1. Klicken Sie in der Cloud Shell erstellen Sie eine neue .NET Core-Konsolenanwendung zu, nennen Sie es mit "SportsStatsTracker"

    ```bash
    dotnet new console --name SportsStatsTracker
    ```
    
1. Wird erstellt einen Ordner für das Projekt, fahren Sie fort, und ändern Sie das aktuelle Verzeichnis.

    ```bash
    cd SportsStatsTracker
    ```
    
## <a name="add-the-connection-string"></a>Fügen Sie die Verbindungszeichenfolge hinzu.

Fügen Sie die Verbindungszeichenfolge aus dem Azure-Portal in den Code sehen. Speichern Sie niemals Anmeldeinformationen wie folgt im Quellcode. Um dieses Beispiel einfach zu halten, werden wir eine Konfigurationsdatei verwenden. Ein besserer Ansatz für eine serverseitige Anwendung in Azure wäre mit Azure Key Vault mit Zertifikaten.

1. Erstellen Sie ein neues **"appSettings.JSON"** Datei, die dem Projekt hinzugefügt.

    ```bash
    touch appsettings.json
    ```

1. Öffnen Sie den Code-Editor, indem Sie eingeben `code .` im Projektordner. Wenn Sie lokal arbeiten, sollten Sie mithilfe von **Visual Studio Code**. Bei den folgenden Schritten werden größtenteils nur ausgerichtet.

1. Wählen Sie die **"appSettings.JSON"** Datei im Editor, und fügen Sie den folgenden Text hinzu. Fügen Sie die Verbindungszeichenfolge in der **Wert** der Einstellung.

    ```json
    {
      "CacheConnection": "[value-goes-here]"
    }
    ```

1. Speichern Sie die Datei - online-Editor müssen Sie ein Menü vorhanden ist, in der oberen rechten Ecke die häufiger Dateivorgänge verfügt.

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
    var config = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json")
        .Build();
    ```

Ihre Datei **Program.cs** sollte jetzt wie folgt aussehen:

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace SportsStatsTracker
{
    class Program
    {
        static void Main(string[] args)
        {
            var config = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json")
                .Build();
        }
    }
}
```

## <a name="get-the-connection-string-from-configuration"></a>Abrufen der Verbindungszeichenfolge aus der Konfiguration

1. In **"Program.cs"**, am Ende der **Main** -Methode, verwenden Sie die neue **Config** Variable, die die Verbindungszeichenfolge abzurufen, und speichern es in eine neue Variable namens  **"ConnectionString"**.
    - Die **Config** Variable verfügt über einen Indexer, können Sie in einer Zeichenfolge zum Abrufen von übergeben Ihrer **"appSettings.JSON"** Datei.

    ```csharp
    string connectionString = config["CacheConnection"];
    ```
    
## <a name="add-support-for-the-redis-cache-net-client"></a>Hinzufügen von Unterstützung für den Redis Cache .NET client

Als Nächstes konfigurieren wir die Konsolenanwendung verwendet die **"stackexchange.redis"** -Client für .NET.

1. Hinzufügen der **"stackexchange.redis"** NuGet-Paket auf das Projekt, das über die Eingabeaufforderung am unteren Rand der Cloud Shell-Editor.

    ```bash
    dotnet add package StackExchange.Redis
    ```

1. Wählen Sie **"Program.cs"** im Editor, und fügen eine `using` für den Namespace **"stackexchange.redis"**

    ```csharp
    using StackExchange.Redis;
    ```
    
Sobald die Installation abgeschlossen ist, ist die Redis-Cache-Client zur Verwendung mit Ihrem Projekt verfügbar sind.

## <a name="connect-to-the-cache"></a>Herstellen einer Verbindung mit dem Cache

Fügen Sie den Code für die Verbindung mit dem Cache an.

1. Wählen Sie **"Program.cs"** im Editor.

1. Erstellen Sie eine `ConnectionMultiplexer` mit `ConnectionMultiplexer.Connect` durch Übergabe der Verbindungszeichenfolge. Nennen Sie den zurückgegebenen Wert **Cache**.

1. Da die erstellte Verbindung ist _verwerfbare_, binden Sie diese in eine `using` Block. Ihr Code sollte ungefähr wie folgt aussehen:

    ```csharp
    string connectionString = config["CacheConnection"];
    
    using (var cache = ConnectionMultiplexer.Connect(connectionString))
    {
        
    }
    ```

> [!NOTE] 
> Die Verbindung mit Azure Redis Cache wird verwaltet, indem die `ConnectionMultiplexer` Klasse. Diese Klasse sollte für Ihre gesamte Clientanwendung genutzt und wiederverwendet werden. Wir _nicht_ für jeden Vorgang eine neue Verbindung erstellen möchten. Stattdessen möchten wir als ein Feld in unserer Klasse aus speichern und für jeden Vorgang wiederzuverwenden. Hier sind nur in verwenden wir die **Main** -Methode, aber in einer produktionsanwendung sollten sie in einem Klassenfeld oder eines Singleton gespeichert werden.

## <a name="add-a-value-to-the-cache"></a>Fügen Sie einen Wert in den cache

Nun, wir die Verbindung haben, fügen Sie einen Wert in den Cache ein.

1. In der `using` block auf, nachdem die Verbindung hergestellt wurde, verwenden Sie die `GetDatabase` Methode zum Abrufen einer `IDatabase` Instanz.

1. Rufen Sie `StringSet` auf die `IDatabase` Objekt, das dem Schlüssel "Test: Key" auf den Wert "einige Value" festgelegt.
    - der Rückgabewert `StringSet` ist eine `bool` , der angibt, ob der Schlüssel hinzugefügt wurde.

1. Zeigt den Rückgabewert von `StringSet` auf der Konsole ausgegeben.

    ```csharp
    bool setValue = db.StringSet("test:key", "some value");
    Console.WriteLine($"SET: {setValue}");
    ```
    
## <a name="get-a-value-from-the-cache"></a>Abrufen eines Werts aus dem cache

1. Rufen Sie dann den Wert mit `StringGet`. Dadurch wird der Schlüssel zum Abrufen und den Wert zurückgibt.

1. Die Ausgabe der zurückgegebene Wert.

    ```csharp
    string getValue = db.StringGet("test:key");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. Ihr Code sollte wie folgt aussehen:

    ```csharp
    using System;
    using Microsoft.Extensions.Configuration;
    using System.IO;
    using StackExchange.Redis;
    
    namespace SportsStatsTracker
    {
        class Program
        {
            static void Main(string[] args)
            {
                var config = new ConfigurationBuilder()
                    .SetBasePath(Directory.GetCurrentDirectory())
                    .AddJsonFile("appsettings.json")
                    .Build();
    
                string connectionString = config["CacheConnection"];
    
                using (var cache = ConnectionMultiplexer.Connect(connectionString))
                {
                    var db = cache.GetDatabase();
    
                    bool setValue = db.StringSet("test:key", "some value");
                    Console.WriteLine($"SET: {setValue}");
    
                    string getValue = db.StringGet("test:key");
                    Console.WriteLine($"GET: {getValue}");
                }
            }
        }
    }
    ```
    
1. Führen Sie die Anwendung aus, um das Ergebnis anzuzeigen. Typ `dotnet run` in die terminal-Fenster unterhalb des Editors. Stellen Sie sicher, dass es nicht finden, Ihren Code zum Erstellen und ausführen oder Sie sind im Projektordner.
    
    ```bash
    dotnet run
    ```
    
## <a name="use-the-async-versions-of-the-methods"></a>Verwenden Sie die asynchronen Versionen der Methoden

Wir konnten abrufen und Festlegen von Werten aus dem Cache, aber wir verwenden die synchronen ältere Versionen. In der serverseitigen Anwendungen sind dies keine effektive Verwendung von unserem Threads. Wir möchten stattdessen verwenden die _asynchrone_ Versionen der Methoden. Sie können leicht erkennen, dass sie – alle enden **Async**.

Um diese Methoden einfach zu machen, wir können die C#- `async` und `await` Schlüsselwörter. Wir müssen allerdings verwenden _mindestens_ c# 7.1 zum Anwenden dieser Schlüsselwörter können unsere **Main** Methode.

### <a name="switch-to-c-71"></a>Wechseln Sie in c# 7.1

# `async` Und `await` Schlüsselwörter waren keine gültigen Schlüsselwörter in **Main** Methoden bis c# 7.1. Wir können problemlos auf die über ein Flag in die der Compiler die **csproj** Datei.

1. Öffnen der **SportsStatsTracker.csproj** Datei im Editor.

1. Hinzufügen `<LangVersion>7.1</LangVersion>` in die erste `PropertyGroup` in der Datei erstellen. Es sollte wie folgt aussehen, wenn Sie fertig sind.
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a>Wenden Sie das Schlüsselwort "Async"

Weisen Sie dann die `async` Schlüsselwort, um die **Main** Methode. Es müssen drei Dinge erreichen.

1. Hinzufügen der `async` -Schlüsselwort auf die **Main** Methodensignatur.
1. Ändern des Rückgabetyps von `void` zu `Task`.
1. Hinzufügen einer `using` -Anweisung zum einschließen `System.Threading.Tasks`.

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using StackExchange.Redis;
using System.Threading.Tasks;

namespace SportsStatsTracker
{
    class Program
    {
        static async Task Main(string[] args)
        {
        ...
```

### <a name="get-and-set-values-asynchronously"></a>Abrufen und Festlegen von Werten asynchron

1. Verwenden der `StringSetAsync` und `StringGetAsync` Methoden zum Festlegen und Abrufen eines Schlüssels namens "counter". Legen Sie den Wert auf "100".

1. Anwenden der `await` Schlüsselwort, um die Ergebnisse von jeder Methode erhalten.

1. Die Ergebnisse an das Konsolenfenster – genauso wie Sie mit der synchronen Versionen.

    ```csharp
    // Simple get and put of integral data types into the cache
    setValue = await db.StringSetAsync("test", "100");
    Console.WriteLine($"SET: {setValue}");
    
    getValue = await db.StringGetAsync("test");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. Führen Sie die Anwendung wieder – sollte weiterhin funktionieren und verfügen nun über zwei Werte.

#### <a name="increment-the-value"></a>Erhöhen Sie den Wert

1. Verwenden der `StringIncrementAsync` Methode zum Erhöhen Ihrer **Leistungsindikator** Wert. Übergeben Sie die Anzahl **50** um den Indikator hinzuzufügen.
    - Beachten Sie, dass die Methode den Schlüssel akzeptiert _und_ entweder eine `long` oder `double`.
    - Abhängig von den Parametern übergeben, gibt es entweder einen `long` oder `double`.

1. Die Ergebnisse der Methode in der Konsole ausgegeben.

    ```csharp
    long newValue = await db.StringIncrementAsync("counter", 50);
    Console.WriteLine($"INCR new value = {newValue}");
    ```
    
## <a name="other-operations"></a>Andere Vorgänge

Abschließend sehen wir führen einige zusätzliche Methoden, mit der `ExecuteAsync` unterstützen.

1. Führen Sie "PING", um die Server-Verbindung zu testen. Es sollte mit "PINGPONG" Antworten.
1. Führen Sie "FLUSHDB" die Datenbankwerte gelöscht. Es sollte mit "OK" antwortet.

```csharp
var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

result = await db.ExecuteAsync("flushdb");
Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
```

## <a name="challenge"></a>Herausforderung

Ein Problem versuchen Sie einen Objekttyp in den Cache zu serialisieren. Hier sind die grundlegenden Schritte aus.

1. Erstellen Sie ein neues `class` mit einigen öffentlichen Eigenschaften. Sie können ein eigenes erfinden ("Person" oder "Car" sind gängige), oder verwenden Sie das Beispiel "GameStats" in der vorherigen Einheit.
1. Hinzufügen von Unterstützung für die **"newtonsoft.JSON"** mithilfe von NuGet-Paket `dotnet add package`.
1. Hinzufügen einer `using` für die `Newtonsoft.Json` Namespace.
1. Erstellen Sie eines der Objekte.
1. Serialisieren mit `JsonConvert.SerializeObject` und `StringSetAsync` , die sie in den Cache übertragen.
1. Erhalten sie aus dem Cache mit `StringGetAsync` und anschließend deserialisiert mit `JsonConvert.DeserializeObject<T>`.

