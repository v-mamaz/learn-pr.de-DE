Sie haben erfahren, wie MSI eine Identität für Ihre Anwendung zur Authentifizierung erstellt. Erstellen Sie nun eine App, die diese Identität verwendet, um auf Geheimnisse im Tresor zuzugreifen.

## <a name="reading-secrets-in-an-aspnet-core-app"></a>Lesen von Geheimnissen in einer ASP.NET Core-App

Die Azure Key Vault-API ist eine REST-API, die die gesamte Verwaltung und Nutzung von Schlüsseln und Tresoren verarbeitet. Jedes Geheimnis in einem Tresor hat eine eindeutige URL. Die Werte des Geheimnisses werden mit HTTP-GET-Anforderungen abgerufen.

Die offizielle Key Vault-Clientbibliothek für .NET Core ist die `KeyVaultClient`-Klasse im NuGet-Paket Microsoft.Azure.KeyVault. Sie müssen sie nicht direkt verwenden &mdash; mit der `AddAzureKeyVault`-Methode von ASP.NET Core können Sie alle Geheimnisse in einem Tresor in die Konfigurations-API beim Start laden. So erhalten Sie Zugriff auf alle Ihre Geheimnisse anhand des Namens über dieselbe `IConfiguration`-Schnittstelle, die Sie für den Rest Ihrer Konfiguration verwenden. Apps, die `AddAzureKeyVault` verwenden, benötigen für den Tresor die Berechtigungen zum **Abrufen** und **Auflisten**.

> [!TIP]
> Unabhängig davon, mit welchem Framework und welcher Sprache Sie Ihre App erstellen, sollten Sie die Werte von Geheimnissen speichern oder diese beim App-Start in den Speicher laden – es sei denn, ein bestimmter Grund spricht dagegen. Es ist unnötig langsam und teuer, Geheimnisse bei Bedarf direkt aus dem Tresor zu lesen.

`AddAzureKeyVault` benötigt nur den Tresornamen als Eingabe, den Sie aus Ihrer lokalen App-Konfiguration abrufen können. Außerdem erfolgt die Verarbeitung der MSI-Authentifizierung automatisch &mdash; beim Einsatz in einer App, die für Azure App Service mit aktiviertem MSI bereitgestellt ist, wird der MSI-Tokendienst erkannt und zur Authentifizierung verwendet. Dieser Ablauf eignet sich für die meisten Szenarien und umfasst alle Best Practices, deswegen gehen wir genauso in dieser Übung vor.

## <a name="handling-secrets-in-an-app"></a>Verarbeiten von Geheimnissen in einer App

Sobald ein Geheimnis in die App geladen wurde, muss diese es sicher verarbeiten. In der App, die in diesem Modul erstellt wurde, wird der Wert des Geheimnisses in die Clientantwort geschrieben und in einem Webbrowser angezeigt, um zu demonstrieren, dass das Geheimnis erfolgreich geladen wurde. **Das Zurückgeben des Geheimniswerts an den Client ist *nicht* die übliche Vorgehensweise.** In der Regel werden mit Geheimnissen beispielsweise Clientbibliotheken für Datenbanken oder Remote-APIs initialisiert.

> [!IMPORTANT]
> Überprüfen Sie Ihren Code immer sorgfältig, um sicherzustellen, dass Ihre App nie Geheimnisse in Ausgaben (z.B. Protokolle, Speicherung und Antworten) schreibt.

## <a name="exercise"></a>Übung

Erstellen Sie eine neue ASP.NET Core-Web-API und verwenden Sie `AddAzureKeyVault`, um das Geheimnis aus dem Tresor zu laden.

### <a name="create-the-app"></a>Erstellen der App

Führen Sie im Azure Cloud Shell-Terminal die folgenden Schritte aus, um eine neue ASP.NET Core-Web-API-Anwendung zu erstellen und im Editor zu öffnen.

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

Nachdem der Editor geladen wurde, führen Sie die folgenden Befehle in der Shell aus, um das NuGet-Paket mit `AddAzureKeyVault` hinzuzufügen und alle Abhängigkeiten der App wiederherzustellen.

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a>Hinzufügen von Code zum Laden und Verwenden von Geheimnissen

Um die richtige Verwendung von Key Vault zu demonstrieren, modifizieren Sie die App so, dass Geheimnisse beim Start aus dem Tresor geladen werden. Fügen Sie außerdem einen neuen Controller mit einem Endpunkt hinzu, der das Geheimnis **SecretPassword** aus dem Tresor abruft.

Starten Sie zuerst die App: Öffnen Sie `Program.cs`, löschen Sie den Inhalt, und ersetzen Sie diesen durch den folgenden Code:

```csharp
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp
{
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .ConfigureAppConfiguration((context, config) =>
                {
                    // Build the current set of configuration to load values from
                    // JSON files and environment variables, including VaultName.
                    var builtConfig = config.Build();

                    // Use VaultName from the configuration to create the full vault URL.
                    var vaultUrl = $"https://{builtConfig["VaultName"]}.vault.azure.net/";

                    // Load all secrets from the vault into configuration. This will automatically
                    // authenticate to the vault using MSI. If MSI is not available, it will
                    // check if Visual Studio and/or the Azure CLI are installed locally and
                    // see if they are configured with credentials that can access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!NOTE]
> Speichern Sie Dateien unbedingt mit `Ctrl+S`, wenn Sie diese fertig bearbeitet haben.

Die einzige Änderung gegenüber dem Startercode ist das Hinzufügen von `ConfigureAppConfiguration`. Hier laden Sie den Tresornamen aus der Konfiguration und rufen `AddAzureKeyVault` damit auf.

Nun kommen wir zum Controller: Erstellen Sie im Ordner `Controllers` die neue Datei `SecretTestController.cs`, und fügen Sie den folgenden Code darin ein.

> [!NOTE]
> Verwenden Sie den Befehl `touch` in der Shell, um eine neue Datei zu erstellen. Verwenden Sie in diesem Fall `touch Controllers/SecretTestController.cs`. Klicken Sie im Editor im Bereich „Dateien“ auf die Schaltfläche „Aktualisieren“, damit es dort angezeigt wird.

```csharp
using System;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp.Controllers
{
    [Route("api/[controller]")]
    public class SecretTestController : ControllerBase
    {
        private readonly IConfiguration _configuration;

        public SecretTestController(IConfiguration configuration)
        {
            _configuration = configuration;
        }

        [HttpGet]
        public IActionResult Get()
        {
            // Get the secret value from configuration. This can be done anywhere
            // we have access to IConfiguration. This does not call the Key Vault
            // API, because the secrets were loaded at startup.
            var secretName = "SecretPassword";
            var secretValue = _configuration[secretName];

            if (secretValue == null)
            {
                return StatusCode(
                    StatusCodes.Status500InternalServerError,
                    $"Error: No secret named {secretName} was found...");
            }
            else {
                return Content($"Secret value: {secretValue}" +
                    Environment.NewLine + Environment.NewLine +
                    "This is for testing only! Never output a secret " +
                    "to a response or anywhere else in a real app!");
            }
        }
    }
}
```

Führen Sie `dotnet build` in der Shell aus, um sicherzustellen, dass alles kompiliert wird. Die App kann nun ausgeführt werden &mdash; machen wir weiter in Azure!