<span data-ttu-id="5c6ba-101">Jetzt wissen Sie, wie das Aktivieren von MSI erstellt einer Identität für die app zur Authentifizierung verwenden erstellen wir eine app, die dieser Identität verwendet wird, um die geheimen Schlüssel im Tresor zugreifen.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-101">Now that you know how enabling MSI creates an identity for our app to use for authentication, we'll create an app that uses that identity to access secrets in the vault.</span></span>

## <a name="reading-secrets-in-an-aspnet-core-app"></a><span data-ttu-id="5c6ba-102">Lesen von Geheimnissen in einer ASP.NET Core-app</span><span class="sxs-lookup"><span data-stu-id="5c6ba-102">Reading secrets in an ASP.NET Core app</span></span>

<span data-ttu-id="5c6ba-103">Die Key Vault-API ist eine REST-API, die gesamte Verwaltung und Verwendung von Schlüsseln und Tresore behandelt.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-103">The Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="5c6ba-104">Jeden geheimen Schlüssel in einem Tresor hat eine eindeutige URL ein, und geheime Werte mit HTTP GET-Anforderungen abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-104">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="5c6ba-105">Die offizielle Key Vault-Clientbibliothek für .NET Core ist die `KeyVaultClient` Klasse im Microsoft.Azure.KeyVault NuGet-Paket.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-105">The official Key Vault client library for .NET Core is the `KeyVaultClient` class in the Microsoft.Azure.KeyVault NuGet package.</span></span> <span data-ttu-id="5c6ba-106">Sie müssen es jedoch direkt verwenden &mdash; mit ASP.NET Core `AddAzureKeyVault` -Methode können Sie alle Geheimnisse aus einem Tresor in der Konfigurations-API beim Start laden.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-106">You don't need to use it directly, though &mdash; with ASP.NET Core's `AddAzureKeyVault` method, you can load all the secrets from a vault into the Configuration API at startup.</span></span> <span data-ttu-id="5c6ba-107">Mit dieser Technik können Sie alle Ihre Geheimnisse anhand des Namens mit dem gleichen Zugriff auf `IConfiguration` Schnittstelle, die Sie für den Rest der Konfiguration verwenden.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-107">This technique enables you to access all of your secrets by name using the same `IConfiguration` interface you use for the rest of your configuration.</span></span> <span data-ttu-id="5c6ba-108">Apps, mit denen `AddAzureKeyVault` benötigen **erhalten** und **Liste** Berechtigungen für den Tresor.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-108">Apps that use `AddAzureKeyVault` require both **Get** and **List** permissions to the vault.</span></span>

> [!TIP]
> <span data-ttu-id="5c6ba-109">Laden Sie unabhängig vom Framework oder eine Sprache aus, die Sie verwenden, um Ihre app zu erstellen, geheime Schlüssel in den Arbeitsspeicher, einmal beim Starten der app, wenn Sie nicht zu einen bestimmten Grund haben.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-109">Regardless of the framework or language you use to build your app, load secrets into memory once at app startup unless you have a specific reason not to.</span></span> <span data-ttu-id="5c6ba-110">Sie direkt aus dem Tresor gelesen werden jedes Mal, wenn Sie sie benötigen, ist unnötig langsame und kostspielige.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-110">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

<span data-ttu-id="5c6ba-111">`AddAzureKeyVault` erfordert nur den Namen des schlüsseltresors, als Eingabe, die wir aus unseren lokalen app-Konfiguration erhalten.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-111">`AddAzureKeyVault` only requires the vault name as an input, which we'll get from our local app configuration.</span></span> <span data-ttu-id="5c6ba-112">Er behandelt auch automatisch die MSI-Authentifizierung &mdash; bei Verwendung in einer app in App Service mit MSI-Aktivierung bereitgestellt, sie erkennt den MSI-token-Dienst und zum Authentifizieren verwenden.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-112">It also automatically handles MSI authentication &mdash; when used in an app deployed to App Service with MSI enabled, it will detect the MSI token service and use it to authenticate.</span></span> <span data-ttu-id="5c6ba-113">Es eignet sich gut für die meisten Szenarien und alle bewährte Methoden implementiert, und wir verwenden sie in dieser Einheit Übung.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-113">It's a good fit for most scenarios and implements all best practices, and we'll use it in this unit's exercise.</span></span>

## <a name="handling-secrets-in-an-app"></a><span data-ttu-id="5c6ba-114">Behandeln von Geheimnissen in einer app</span><span class="sxs-lookup"><span data-stu-id="5c6ba-114">Handling secrets in an app</span></span>

<span data-ttu-id="5c6ba-115">Nachdem Sie ein geheimen Schlüssel in Ihrer app geladen wird, liegt es an Ihre app aus, um es sicher behandeln.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-115">Once a secret is loaded into your app, it's up to your app to handle it securely.</span></span> <span data-ttu-id="5c6ba-116">In der app, die wir in diesem Modul zu erstellen, müssen wir unsere geheimniswert der Clientantwort schreiben und anzeigen in einem Webbrowser, um zu veranschaulichen, dass sie erfolgreich geladen wurde.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-116">In the app we build in this module, we write our secret value out to the client response and view it in a web browser to demonstrate that it has been loaded successfully.</span></span> <span data-ttu-id="5c6ba-117">**Einen geheimen Wert an den Client zurückgegeben wird *nicht* etwas gewohnt!**</span><span class="sxs-lookup"><span data-stu-id="5c6ba-117">**Returning a secret value to the client is *not* something you'd normally do!**</span></span> <span data-ttu-id="5c6ba-118">In der Regel verwenden Sie geheime Schlüssel, beispielsweise Clientbibliotheken für Datenbanken oder remote-APIs zu initialisieren.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-118">Usually, you'll use secrets to do things like initialize client libraries for databases or remote APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c6ba-119">Überprüfen Sie immer sorgfältig den Code, um sicherzustellen, dass Ihre app niemals geheime Schlüssel für jede Art von Ausgabe, einschließlich der Protokolle, Speicher und Antworten schreibt.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-119">Always carefully review your code to ensure that your app never writes secrets to any kind of output, including logs, storage, and responses.</span></span>

# <a name="exercise"></a><span data-ttu-id="5c6ba-120">Übung</span><span class="sxs-lookup"><span data-stu-id="5c6ba-120">Exercise</span></span>

<span data-ttu-id="5c6ba-121">Wir erstellen eine neue ASP.NET Core-Web-API und Verwendung `AddAzureKeyVault` den geheimen Schlüssel aus unseren schlüsseltresor zu laden.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-121">We'll create a new ASP.NET Core web API and use `AddAzureKeyVault` to load the secret from our vault.</span></span>

## <a name="create-the-app"></a><span data-ttu-id="5c6ba-122">Erstellen der App</span><span class="sxs-lookup"><span data-stu-id="5c6ba-122">Create the app</span></span>

<span data-ttu-id="5c6ba-123">Führen Sie in der Cloud Shell terminal Folgendes ein, um ein neues ASP.NET Core-Web-API-Anwendung erstellen und öffnen Sie sie im Editor ein.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-123">In the Cloud Shell terminal, run the following to create a new ASP.NET Core web API application and open it in the editor.</span></span>

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

<span data-ttu-id="5c6ba-124">Nach dem Laden der Editor, führen die folgenden Befehle in der Shell Hinzufügen der NuGet-Pakets mit `AddAzureKeyVault` und Wiederherstellen des gesamten von der app Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-124">After the editor loads, run the following commands in the shell to add the NuGet package containing `AddAzureKeyVault` and restore all of the app's dependencies.</span></span>

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

## <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="5c6ba-125">Hinzufügen von Code zum Laden und Verwenden von Geheimnissen</span><span class="sxs-lookup"><span data-stu-id="5c6ba-125">Add code to load and use secrets</span></span>

<span data-ttu-id="5c6ba-126">Um die richtige Verwendung von Key Vault zu demonstrieren, ändern wir unsere app aus, um Geheimnisse aus dem Tresor beim Start geladen werden.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-126">To demonstrate good usage of Key Vault, we will modify our app to load secrets from the vault at startup.</span></span> <span data-ttu-id="5c6ba-127">Wir fügen auch einen neuen Domänencontroller mit einem Endpunkt, der ruft unsere **SecretPassword** Geheimnis aus dem Tresor.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-127">We'll also add a new controller with an endpoint that gets our **SecretPassword** secret from the vault.</span></span>

<span data-ttu-id="5c6ba-128">"First", die beim Start der app: Öffnen Sie `Program.cs`, löschen Sie den Inhalt, und Ersetzen Sie sie durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="5c6ba-128">First, the app startup: open `Program.cs`, delete the contents and replace them with the following code:</span></span>

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
> <span data-ttu-id="5c6ba-129">Stellen Sie sicher, dass zum Speichern von Dateien mit `Ctrl+S` Wenn Sie fertig sind sie bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-129">Make sure to save files with `Ctrl+S` when you're done editing them.</span></span>

<span data-ttu-id="5c6ba-130">Die einzige Änderung aus dem Startcode ist das Hinzufügen von `ConfigureAppConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-130">The only change from the starter code is the addition of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="5c6ba-131">Dies ist, in dem wir den Namen des schlüsseltresors aus Konfiguration und rufen laden `AddAzureKeyVault` mit.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-131">This is where we load the vault name from configuration and call `AddAzureKeyVault` with it.</span></span>

<span data-ttu-id="5c6ba-132">Anschließend wird der Controller: Erstellen einer neuen Datei in die `Controllers` Ordner mit dem Namen `SecretTestController.cs` , und fügen Sie den folgenden Code ein.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-132">Next, the controller: create a new file in the `Controllers` folder called `SecretTestController.cs` and paste the following code into it.</span></span>

> [!NOTE]
> <span data-ttu-id="5c6ba-133">Verwenden Sie zum Erstellen einer neuen Datei den `touch` -Befehl in der Shell.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-133">To create a new file, use the `touch` command in the shell.</span></span> <span data-ttu-id="5c6ba-134">Verwenden Sie in diesem Fall `touch Controllers/SecretTestController.cs`.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-134">In this case, use `touch Controllers/SecretTestController.cs`.</span></span> <span data-ttu-id="5c6ba-135">Sie müssen sich auf die Schaltfläche "Aktualisieren" im Bereich "Dateien" des Editors zum Anzeigen vorhanden.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-135">You'll need to click the refresh button in the Files pane of the editor to see it there.</span></span>

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

<span data-ttu-id="5c6ba-136">Führen Sie `dotnet build` in der Shell aus, um sicherzustellen, dass alles kompiliert wird.</span><span class="sxs-lookup"><span data-stu-id="5c6ba-136">Run `dotnet build` in the shell to make sure everything compiles.</span></span> <span data-ttu-id="5c6ba-137">Die app ist bereit zur Ausführung &mdash; nun erfahren Sie es in Azure!</span><span class="sxs-lookup"><span data-stu-id="5c6ba-137">The app is ready to run &mdash; now let's get it into Azure!</span></span>