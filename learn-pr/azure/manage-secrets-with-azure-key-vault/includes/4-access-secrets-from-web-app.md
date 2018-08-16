Jetzt wissen Sie, wie das Aktivieren von MSI erstellt einer Identität für die app zur Authentifizierung verwenden erstellen wir eine app, die dieser Identität verwendet wird, um die geheimen Schlüssel im Tresor zugreifen.

## <a name="reading-secrets-in-an-aspnet-core-app"></a>Lesen von Geheimnissen in einer ASP.NET Core-app

Die Key Vault-API ist eine REST-API, die gesamte Verwaltung und Verwendung von Schlüsseln und Tresore behandelt. Jeden geheimen Schlüssel in einem Tresor hat eine eindeutige URL ein, und geheime Werte mit HTTP GET-Anforderungen abgerufen werden.

Die offizielle Key Vault-Clientbibliothek für .NET Core ist die `KeyVaultClient` Klasse im Microsoft.Azure.KeyVault NuGet-Paket. Sie müssen es jedoch direkt verwenden &mdash; mit ASP.NET Core `AddAzureKeyVault` -Methode können Sie alle Geheimnisse aus einem Tresor in der Konfigurations-API beim Start laden. Mit dieser Technik können Sie alle Ihre Geheimnisse anhand des Namens mit dem gleichen Zugriff auf `IConfiguration` Schnittstelle, die Sie für den Rest der Konfiguration verwenden. Apps, mit denen `AddAzureKeyVault` benötigen **erhalten** und **Liste** Berechtigungen für den Tresor.

> [!TIP]
> Laden Sie unabhängig vom Framework oder eine Sprache aus, die Sie verwenden, um Ihre app zu erstellen, geheime Schlüssel in den Arbeitsspeicher, einmal beim Starten der app, wenn Sie nicht zu einen bestimmten Grund haben. Sie direkt aus dem Tresor gelesen werden jedes Mal, wenn Sie sie benötigen, ist unnötig langsame und kostspielige.

`AddAzureKeyVault` erfordert nur den Namen des schlüsseltresors, als Eingabe, die wir aus unseren lokalen app-Konfiguration erhalten. Er behandelt auch automatisch die MSI-Authentifizierung &mdash; bei Verwendung in einer app in App Service mit MSI-Aktivierung bereitgestellt, sie erkennt den MSI-token-Dienst und zum Authentifizieren verwenden. Es eignet sich gut für die meisten Szenarien und alle bewährte Methoden implementiert, und wir verwenden sie in dieser Einheit Übung.

## <a name="handling-secrets-in-an-app"></a>Behandeln von Geheimnissen in einer app

Nachdem Sie ein geheimen Schlüssel in Ihrer app geladen wird, liegt es an Ihre app aus, um es sicher behandeln. In der app, die wir in diesem Modul zu erstellen, müssen wir unsere geheimniswert der Clientantwort schreiben und anzeigen in einem Webbrowser, um zu veranschaulichen, dass sie erfolgreich geladen wurde. **Einen geheimen Wert an den Client zurückgegeben wird *nicht* etwas gewohnt!** In der Regel verwenden Sie geheime Schlüssel, beispielsweise Clientbibliotheken für Datenbanken oder remote-APIs zu initialisieren.

> [!IMPORTANT]
> Überprüfen Sie immer sorgfältig den Code, um sicherzustellen, dass Ihre app niemals geheime Schlüssel für jede Art von Ausgabe, einschließlich der Protokolle, Speicher und Antworten schreibt.

# <a name="exercise"></a>Übung

Wir erstellen eine neue ASP.NET Core-Web-API und Verwendung `AddAzureKeyVault` den geheimen Schlüssel aus unseren schlüsseltresor zu laden.

## <a name="create-the-app"></a>Erstellen der App

Führen Sie in der Cloud Shell terminal Folgendes ein, um ein neues ASP.NET Core-Web-API-Anwendung erstellen und öffnen Sie sie im Editor ein.

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

Nach dem Laden der Editor, führen die folgenden Befehle in der Shell Hinzufügen der NuGet-Pakets mit `AddAzureKeyVault` und Wiederherstellen des gesamten von der app Abhängigkeiten.

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

## <a name="add-code-to-load-and-use-secrets"></a>Hinzufügen von Code zum Laden und Verwenden von Geheimnissen

Um die richtige Verwendung von Key Vault zu demonstrieren, ändern wir unsere app aus, um Geheimnisse aus dem Tresor beim Start geladen werden. Wir fügen auch einen neuen Domänencontroller mit einem Endpunkt, der ruft unsere **SecretPassword** Geheimnis aus dem Tresor.

"First", die beim Start der app: Öffnen Sie `Program.cs`, löschen Sie den Inhalt, und Ersetzen Sie sie durch den folgenden Code:

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
> Stellen Sie sicher, dass zum Speichern von Dateien mit `Ctrl+S` Wenn Sie fertig sind sie bearbeiten.

Die einzige Änderung aus dem Startcode ist das Hinzufügen von `ConfigureAppConfiguration`. Dies ist, in dem wir den Namen des schlüsseltresors aus Konfiguration und rufen laden `AddAzureKeyVault` mit.

Anschließend wird der Controller: Erstellen einer neuen Datei in die `Controllers` Ordner mit dem Namen `SecretTestController.cs` , und fügen Sie den folgenden Code ein.

> [!NOTE]
> Verwenden Sie zum Erstellen einer neuen Datei den `touch` -Befehl in der Shell. Verwenden Sie in diesem Fall `touch Controllers/SecretTestController.cs`. Sie müssen sich auf die Schaltfläche "Aktualisieren" im Bereich "Dateien" des Editors zum Anzeigen vorhanden.

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

Führen Sie `dotnet build` in der Shell aus, um sicherzustellen, dass alles kompiliert wird. Die app ist bereit zur Ausführung &mdash; nun erfahren Sie es in Azure!