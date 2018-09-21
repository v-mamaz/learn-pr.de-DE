Nachdem wir eine Redis Cache-Instanz in Azure erstellt haben, werden wir jetzt eine Anwendung zur Verwendung von Redis Cache erstellen. Stellen Sie sicher, dass Sie über die Informationen zu Ihrer Verbindungszeichenfolge aus dem Azure-Portal verfügen.

> [!NOTE]
> Die integrierte Cloud Shell-Instanz ist auf der rechten Seite verfügbar. Sie können diese Eingabeaufforderung verwenden, um den hier entwickelten Beispielcode zu erstellen und auszuführen. Alternativ können Sie diese Schritte lokal ausführen, wenn Sie eine .NET Core-Entwicklungsumgebung eingerichtet haben.

## <a name="create-a-console-application"></a>Erstellen einer Konsolenanwendung

Wir verwenden eine einfache Konsolenanwendung, damit wir uns auf die Redis-Implementierung konzentrieren können.

1. Erstellen Sie in der Cloud Shell eine neue .NET Core-Konsolenanwendung namens „SportsStatsTracker“.

    ```bash
    dotnet new console --name SportsStatsTracker
    ```
    
1. Hierdurch wird ein Ordner für das Projekt erstellt. Ändern Sie dann das aktuelle Verzeichnis.

    ```bash
    cd SportsStatsTracker
    ```
    
## <a name="add-the-connection-string"></a>Hinzufügen der Verbindungszeichenfolge

Jetzt fügen wir die Verbindungszeichenfolge zum Code hinzu, die wir aus dem Azure-Portal abgerufen haben. Speichern Sie niemals Anmeldeinformationen wie diese in Ihrem Quellcode. Um dieses Beispiel einfach zu halten, verwenden wir eine Konfigurationsdatei. Ein besserer Ansatz für eine serverseitige Anwendung in Azure wäre die Verwendung von Azure Key Vault mit Zertifikaten.

1. Erstellen Sie eine Datei **appsettings.json**, um sie zum Projekt hinzuzufügen.

    ```bash
    touch appsettings.json
    ```

1. Öffnen Sie den Code-Editor, indem Sie im Projektordner `code .` eingeben. Wenn Sie lokal arbeiten, wird die Verwendung von **Visual Studio Code** empfohlen. Die hier gezeigten Verwendungsschritte sind größtenteils gleich.

1. Wählen Sie die Datei **appsettings.json** im Editor aus, und fügen Sie den folgenden Text hinzu. Fügen Sie Ihre Verbindungszeichenfolge in den **Wert** der Einstellung ein.

    ```json
    {
      "CacheConnection": "[value-goes-here]"
    }
    ```

1. Speichern Sie die Änderungen.

    > [!IMPORTANT]
    > Achten Sie beim Einfügen oder Ändern von Code in einer Datei im Editor darauf, dass Sie anschließend speichern, indem Sie das Menü unter „...“ oder die Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux, <kbd>Cmd+S</kbd> unter macOS) verwenden.

1. Klicken Sie im Editor auf die Datei **SportsStatsTracker.csproj**, um sie zu öffnen.

1. Fügen Sie den folgenden `<ItemGroup>`-Konfigurationsblock in das Stammelement `<Project>`ein, um die neue Datei in das Projekt einzuschließen und in den Ausgabeordner zu kopieren. Dadurch wird sichergestellt, dass die App-Konfigurationsdatei beim Kompilieren/Erstellen der App im Ausgabeverzeichnis abgelegt wird.

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

1. Am Anfang der Datei befindet sich die Zeile `using System`. Fügen Sie unter dieser Zeile die folgenden Codezeilen hinzu:

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. Ersetzen Sie den Inhalt der **Main**-Methode durch den nachstehenden Code. Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.

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

1. Verwenden Sie in **Program.cs** am Ende der Methode **Main** die neue Variable **config**, um die Verbindungszeichenfolge anzurufen und sie in einer neuen Variable namens **connectionString** zu speichern.
    - Die Variable **config** umfasst einen Indexer, an den Sie eine Zeichenfolge übergeben können, die aus Ihrer Datei **appSettings.json** abgerufen werden soll.

    ```csharp
    string connectionString = config["CacheConnection"];
    ```
    
## <a name="add-support-for-the-redis-cache-net-client"></a>Hinzufügen von Unterstützung für den Redis Cache-Client für .NET

Als Nächstes konfigurieren wir die Konsolenanwendung zur Verwendung des **StackExchange.Redis**-Clients für .NET.

1. Fügen Sie dem Projekt mithilfe der Eingabeaufforderung unten im Cloud Shell-Editor das NuGet-Paket **StackExchange.Redis** hinzu.

    ```bash
    dotnet add package StackExchange.Redis
    ```

1. Wählen Sie im Editor **Program.cs** aus, und fügen Sie `using` für den Namespace **StackExchange.Redis** hinzu.

    ```csharp
    using StackExchange.Redis;
    ```
    
Nach Abschluss der Installation kann der Redis Cache-Client für Ihr Projekt verwendet werden.

## <a name="connect-to-the-cache"></a>Herstellen einer Verbindung mit dem Cache

Fügen wir Code zur Verbindungsherstellung mit dem Cache hinzu.

1. Wählen Sie im Editor die Datei **Program.cs** aus.

1. Erstellen Sie einen `ConnectionMultiplexer` unter Verwendung von `ConnectionMultiplexer.Connect`, indem Sie Ihre Verbindungszeichenfolge übergeben. Geben Sie dem Rückgabewert den Namen **cache**.

1. Die erstellte Verbindung ist _verwerfbar_, umschließen Sie sie deshalb mit einem `using`-Block. Ihr Code sollte in etwa wie folgt aussehen:

    ```csharp
    string connectionString = config["CacheConnection"];
    
    using (var cache = ConnectionMultiplexer.Connect(connectionString))
    {
        
    }
    ```

> [!NOTE] 
> Die Verbindung mit Azure Redis Cache wird über die `ConnectionMultiplexer`-Klasse verwaltet. Diese Klasse muss in Ihrer gesamten Clientanwendung freigegeben und wiederverwendet werden. Es soll _nicht_ für jeden Vorgang eine neue Verbindung erstellt werden. Stattdessen soll die Verbindung als Feld in unserer Klasse gespeichert und für jeden Vorgang wiederverwendet werden. Hier wird die Verbindung nur in der Methode **Main** verwendet, aber in einer Produktionsanwendung sollte sie in einem Klassenfeld oder in einem Singleton gespeichert werden.

## <a name="add-a-value-to-the-cache"></a>Hinzufügen eines Werts zum Cache

Nun, da eine Verbindung vorhanden ist, fügen wir dem Cache einen Wert hinzu.

1. Verwenden Sie nach der Verbindungsherstellung im Block `using` die Methode `GetDatabase`, um eine `IDatabase`-Instanz abzurufen.

1. Rufen Sie `StringSet` für das `IDatabase`-Objekt auf, um den Schlüssel „test:key“ auf den Wert „some value“ festzulegen.
    - Der Rückgabewert von `StringSet` ist ein Wert vom Typ `bool`, der angibt, ob der Schlüssel hinzugefügt wurde.

1. Zeigen Sie den Rückgabewert von `StringSet` auf der Konsole an.

    ```csharp
    bool setValue = db.StringSet("test:key", "some value");
    Console.WriteLine($"SET: {setValue}");
    ```
    
## <a name="get-a-value-from-the-cache"></a>Abrufen eines Werts aus dem Cache

1. Als Nächstes rufen wir den Wert mithilfe von `StringGet` ab. Hierbei wird der Schlüssel verwendet, um den Wert abzurufen und zurückzugeben.

1. Geben Sie dem Rückgabewert aus.

    ```csharp
    string getValue = db.StringGet("test:key");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. Ihr Code sollte folgendermaßen aussehen:

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
    
1. Führen Sie die Anwendung aus, um das Ergebnis anzuzeigen. Geben Sie in das Terminalfenster unterhalb des Editors `dotnet run` ein. Vergewissern Sie sich, dass Sie sich im Projektordner befinden. Andernfalls wird der Code für Erstellung und Ausführung nicht gefunden.
    
    ```bash
    dotnet run
    ```
    
> [!TIP] 
> Sollte die Anwendung zwar kompiliert werden, aber nicht wie erwartet funktionieren, haben Sie möglicherweise vergessen, die Änderungen im Editor zu speichern. Denken Sie immer daran, die Änderungen zu speichern, wenn Sie zwischen Terminal- und Editorfenster wechseln. 

## <a name="use-the-async-versions-of-the-methods"></a>Verwenden der asynchronen Versionen der Methoden

Wir konnten Werte aus dem Cache abrufen und im Cache festlegen, aber wir verwenden die älteren, synchronen Versionen. In serverseitigen Anwendungen bieten diese keine effiziente Verwendung unserer Threads. Stattdessen möchten wir die _asynchronen_ Versionen der Methoden verwenden. Diese Methodenversionen sind leicht zu erkennen: sie senden immer auf **Async**.

Zur einfacheren Arbeit mit diesen Methoden können wir die C#-Schlüsselwörter `async` und `await` verwenden. Wir müssen jedoch _mindestens_ C# 7.1 verwenden, um diese Schlüsselwörter auf unsere **Main**-Methode anwenden zu können.

### <a name="switch-to-c-71"></a>Umstellung auf C# 7.1

Die C#-Schlüsselwörter `async` und `await` waren bis C# 7.1 keine gültigen Schlüsselwörter in den **Main**-Methoden. Wir können über ein Flag in der Datei **.csproj** ganz einfach auf diesen Compiler umstellen.

1. Öffnen Sie die Datei **SportsStatsTracker.csproj** im Editor.

1. Fügen Sie `<LangVersion>7.1</LangVersion>` in die erste `PropertyGroup` in der Builddatei ein. Anschließend sollte die Datei so aussehen, wie nachfolgend gezeigt.
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a>Anwenden des async-Schlüsselworts

Als Nächstes wenden wir das `async`-Schlüsselwort auf die **Main**-Methode an. Wir müssen drei Aufgaben erledigen.

1. Hinzufügen des Schlüsselworts `async` zur **Main**-Methodensignatur
1. Ändern des Rückgabetyps von `void` in `Task`
1. Hinzufügen einer `using`-Anweisung zum Einschließen von `System.Threading.Tasks`

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

### <a name="get-and-set-values-asynchronously"></a>Asynchrones Abrufen und Festlegen von Werten

Die synchronen Methoden können unverändert bleiben. Fügen Sie in den Methoden `StringSetAsync` und `StringGetAsync` einen Aufruf hinzu, um dem Cache einen weiteren Wert hinzuzufügen. Legen Sie „counter“ auf den Wert „100“ fest.  

1. Verwenden Sie die Methoden `StringSetAsync` und `StringGetAsync`, um einen Schlüssel namens „counter“ festzulegen und abzurufen. Legen Sie den Wert auf 100 fest.

1. Wenden Sie das Schlüsselwort `await` an, um die Ergebnisse von jeder Methode abzurufen.

1. Geben Sie die Ergebnisse im Konsolenfenster aus – wie zuvor bei den synchronen Versionen.

    ```csharp
    // Simple get and put of integral data types into the cache
    setValue = await db.StringSetAsync("test", "100");
    Console.WriteLine($"SET: {setValue}");
    
    getValue = await db.StringGetAsync("test");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. Führen Sie jetzt erneut die Anwendung aus. Sie sollte weiterhin funktionieren und jetzt zwei Werte aufweisen.

#### <a name="increment-the-value"></a>Erhöhen des Werts

1. Verwenden Sie die Methode `StringIncrementAsync`, um Ihren **counter**-Wert zu erhöhen. Übergeben Sie die Zahl **50**, um sie zu „counter“ hinzuzufügen.
    - Beachten Sie, dass die Methode den Schlüssel _und_ entweder `long` oder `double` verwendet.
    - Je nachdem, welche Parameter übergeben wurden, wird `long` oder `double` zurückgegeben.

1. Geben Sie die Ergebnisse der Methode an die Konsole zurück.

    ```csharp
    long newValue = await db.StringIncrementAsync("counter", 50);
    Console.WriteLine($"INCR new value = {newValue}");
    ```
    
## <a name="other-operations"></a>Weitere Vorgänge

Abschließend versuchen wir, einige zusätzliche Methoden mit Unterstützung von `ExecuteAsync` auszuführen.

1. Führen Sie „PING“ aus, um die Serververbindung zu testen. Die Antwort sollte „PONG“ lauten.
1. Führen Sie „FLUSHDB“ aus, um die Datenbankwerte zu löschen. Die Antwort sollte „OK“ lauten.

```csharp
var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

result = await db.ExecuteAsync("flushdb");
Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
```

Der endgültige Code sollte ungefähr wie folgt aussehen:

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

                setValue = await db.StringSetAsync("test", "100");
                Console.WriteLine($"SET: {setValue}");

                getValue = await db.StringGetAsync("test");
                Console.WriteLine($"GET: {getValue}");

                var result = await db.ExecuteAsync("ping");
                Console.WriteLine($"PING = {result.Type} : {result}");
                
                result = await db.ExecuteAsync("flushdb");
                Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
            }
        }
    }
}
```

## <a name="challenge"></a>Herausforderung

Versuchen Sie, als Herausforderung einen Objekttyp im Cache zu serialisieren. Nachfolgend werden die grundlegenden Schritte gezeigt.

1. Erstellen Sie eine neue `class` mit einigen öffentlichen Eigenschaften. Sie können eine eigene Klasse erfinden (gängig sind z.B. „Person“ oder „Auto“) oder das Beispiel „GameStats“ aus der vorherigen Einheit verwenden.

1. Fügen Sie mit `dotnet add package` Unterstützung für das NuGet-Paket **Newtonsoft.Json** hinzu.

1. Fügen Sie `using` für den `Newtonsoft.Json`-Namespace hinzu.

1. Erstellen Sie eines Ihrer Objekte.

1. Serialisieren Sie es mit `JsonConvert.SerializeObject`, und verwenden Sie `StringSetAsync`, um es per Push in den Cache zu übertragen.

1. Rufen Sie das Objekt mit `StringGetAsync` aus dem Cache ab, und deserialisieren Sie es anschließend mit `JsonConvert.DeserializeObject<T>`.

