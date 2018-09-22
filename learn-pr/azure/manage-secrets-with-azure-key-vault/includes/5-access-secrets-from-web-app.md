<span data-ttu-id="49c6b-101">Sie haben erfahren, wie verwaltete Identitäten für Azure-Ressourcen eine Identität für Ihre Anwendung zur Authentifizierung erstellen. Erstellen Sie nun eine App, die diese Identität verwendet, um auf Geheimnisse im Tresor zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="49c6b-101">Now that you know how enabling managed identities for Azure resources creates an identity for our app to use for authentication, we'll create an app that uses that identity to access secrets in the vault.</span></span>

## <a name="reading-secrets-in-an-aspnet-core-app"></a><span data-ttu-id="49c6b-102">Lesen von Geheimnissen in einer ASP.NET Core-App</span><span class="sxs-lookup"><span data-stu-id="49c6b-102">Reading secrets in an ASP.NET Core app</span></span>

<span data-ttu-id="49c6b-103">Die Azure Key Vault-API ist eine REST-API, die die gesamte Verwaltung und Nutzung von Schlüsseln und Tresoren verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="49c6b-103">The Azure Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="49c6b-104">Jedes Geheimnis in einem Tresor hat eine eindeutige URL. Die Werte des Geheimnisses werden mit HTTP-GET-Anforderungen abgerufen.</span><span class="sxs-lookup"><span data-stu-id="49c6b-104">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="49c6b-105">Die offizielle Key Vault-Clientbibliothek für .NET Core ist die `KeyVaultClient`-Klasse im NuGet-Paket Microsoft.Azure.KeyVault.</span><span class="sxs-lookup"><span data-stu-id="49c6b-105">The official Key Vault client library for .NET Core is the `KeyVaultClient` class in the Microsoft.Azure.KeyVault NuGet package.</span></span> <span data-ttu-id="49c6b-106">Sie müssen sie nicht direkt verwenden &mdash; mit der `AddAzureKeyVault`-Methode von ASP.NET Core können Sie alle Geheimnisse in einem Tresor in die Konfigurations-API beim Start laden.</span><span class="sxs-lookup"><span data-stu-id="49c6b-106">You don't need to use it directly, though &mdash; with ASP.NET Core's `AddAzureKeyVault` method, you can load all the secrets from a vault into the Configuration API at startup.</span></span> <span data-ttu-id="49c6b-107">So erhalten Sie Zugriff auf alle Ihre Geheimnisse anhand des Namens über dieselbe `IConfiguration`-Schnittstelle, die Sie für den Rest Ihrer Konfiguration verwenden.</span><span class="sxs-lookup"><span data-stu-id="49c6b-107">This technique enables you to access all of your secrets by name using the same `IConfiguration` interface you use for the rest of your configuration.</span></span> <span data-ttu-id="49c6b-108">Apps, die `AddAzureKeyVault` verwenden, benötigen für den Tresor die Berechtigungen zum **Abrufen** und **Auflisten**.</span><span class="sxs-lookup"><span data-stu-id="49c6b-108">Apps that use `AddAzureKeyVault` require both **Get** and **List** permissions to the vault.</span></span>

> [!TIP]
> <span data-ttu-id="49c6b-109">Unabhängig davon, mit welchem Framework und welcher Sprache Sie Ihre App erstellen, sollten Sie sie dafür konzipieren, die Werte von Geheimnissen zu speichern oder diese beim App-Start in den Speicher zu laden – es sei denn, ein bestimmter Grund spricht dagegen.</span><span class="sxs-lookup"><span data-stu-id="49c6b-109">Regardless of the framework or language you use to build your app, you should design it to cache secret values locally or load them into memory at startup unless you have a specific reason not to.</span></span> <span data-ttu-id="49c6b-110">Es ist unnötig langsam und teuer, Geheimnisse bei Bedarf direkt aus dem Tresor zu lesen.</span><span class="sxs-lookup"><span data-stu-id="49c6b-110">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

<span data-ttu-id="49c6b-111">`AddAzureKeyVault` benötigt nur den Tresornamen als Eingabe, den Sie aus Ihrer lokalen App-Konfiguration abrufen können.</span><span class="sxs-lookup"><span data-stu-id="49c6b-111">`AddAzureKeyVault` only requires the vault name as an input, which we'll get from our local app configuration.</span></span> <span data-ttu-id="49c6b-112">Außerdem erfolgt die Verarbeitung der Authentifizierung verwalteter Identitäten automatisch. Beim Einsatz in einer App, die für Azure App Service mit aktivierten verwalteten Identitäten bereitgestellt ist, wird der Tokendienst für verwaltete Identitäten erkannt und zur Authentifizierung verwendet.</span><span class="sxs-lookup"><span data-stu-id="49c6b-112">It also automatically handles managed identity authentication &mdash; when used in an app deployed to Azure App Service with managed identities for Azure resources enabled, it will detect the managed identities token service and use it to authenticate.</span></span> <span data-ttu-id="49c6b-113">Dieser Ablauf eignet sich für die meisten Szenarien und umfasst alle bewährten Methode. Deswegen gehen wir genauso in dieser Übung vor.</span><span class="sxs-lookup"><span data-stu-id="49c6b-113">It's a good fit for most scenarios and implements all best practices, and we'll use it in this unit's exercise.</span></span>

## <a name="handling-secrets-in-an-app"></a><span data-ttu-id="49c6b-114">Verarbeiten von Geheimnissen in einer App</span><span class="sxs-lookup"><span data-stu-id="49c6b-114">Handling secrets in an app</span></span>

<span data-ttu-id="49c6b-115">Sobald ein Geheimnis in die App geladen wurde, muss diese es sicher verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="49c6b-115">Once a secret is loaded into your app, it's up to your app to handle it securely.</span></span> <span data-ttu-id="49c6b-116">In der App, die in diesem Modul erstellt wurde, wird der Wert des Geheimnisses in die Clientantwort geschrieben und in einem Webbrowser angezeigt, um zu demonstrieren, dass das Geheimnis erfolgreich geladen wurde.</span><span class="sxs-lookup"><span data-stu-id="49c6b-116">In the app we build in this module, we write our secret value out to the client response and view it in a web browser to demonstrate that it has been loaded successfully.</span></span> <span data-ttu-id="49c6b-117">**Das Zurückgeben des Geheimniswerts an den Client ist *nicht* die übliche Vorgehensweise.**</span><span class="sxs-lookup"><span data-stu-id="49c6b-117">**Returning a secret value to the client is *not* something you'd normally do!**</span></span> <span data-ttu-id="49c6b-118">In der Regel werden mit Geheimnissen beispielsweise Clientbibliotheken für Datenbanken oder Remote-APIs initialisiert.</span><span class="sxs-lookup"><span data-stu-id="49c6b-118">Usually, you'll use secrets to do things like initialize client libraries for databases or remote APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49c6b-119">Überprüfen Sie Ihren Code immer sorgfältig, um sicherzustellen, dass Ihre App nie Geheimnisse in Ausgaben (z.B. Protokolle, Speicherung und Antworten) schreibt.</span><span class="sxs-lookup"><span data-stu-id="49c6b-119">Always carefully review your code to ensure that your app never writes secrets to any kind of output, including logs, storage, and responses.</span></span>

## <a name="exercise"></a><span data-ttu-id="49c6b-120">Übung</span><span class="sxs-lookup"><span data-stu-id="49c6b-120">Exercise</span></span>

<span data-ttu-id="49c6b-121">Erstellen Sie eine neue ASP.NET Core-Web-API und verwenden Sie `AddAzureKeyVault`, um das Geheimnis aus dem Tresor zu laden.</span><span class="sxs-lookup"><span data-stu-id="49c6b-121">We'll create a new ASP.NET Core web API and use `AddAzureKeyVault` to load the secret from our vault.</span></span>

### <a name="create-the-app"></a><span data-ttu-id="49c6b-122">Erstellen der App</span><span class="sxs-lookup"><span data-stu-id="49c6b-122">Create the app</span></span>

<span data-ttu-id="49c6b-123">Führen Sie im Azure Cloud Shell-Terminal die folgenden Schritte aus, um eine neue ASP.NET Core-Web-API-Anwendung zu erstellen und im Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="49c6b-123">In the Azure Cloud Shell terminal, run the following to create a new ASP.NET Core web API application and open it in the editor.</span></span>

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

<span data-ttu-id="49c6b-124">Nachdem der Editor geladen wurde, führen Sie die folgenden Befehle in der Shell aus, um das NuGet-Paket mit `AddAzureKeyVault` hinzuzufügen und alle Abhängigkeiten der App wiederherzustellen.</span><span class="sxs-lookup"><span data-stu-id="49c6b-124">After the editor loads, run the following commands in the shell to add the NuGet package containing `AddAzureKeyVault` and restore all of the app's dependencies.</span></span>

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="49c6b-125">Hinzufügen von Code zum Laden und Verwenden von Geheimnissen</span><span class="sxs-lookup"><span data-stu-id="49c6b-125">Add code to load and use secrets</span></span>

<span data-ttu-id="49c6b-126">Um die richtige Verwendung von Key Vault zu demonstrieren, modifizieren Sie die App so, dass Geheimnisse beim Start aus dem Tresor geladen werden.</span><span class="sxs-lookup"><span data-stu-id="49c6b-126">To demonstrate good usage of Key Vault, we will modify our app to load secrets from the vault at startup.</span></span> <span data-ttu-id="49c6b-127">Fügen Sie außerdem einen neuen Controller mit einem Endpunkt hinzu, der das Geheimnis **SecretPassword** aus dem Tresor abruft.</span><span class="sxs-lookup"><span data-stu-id="49c6b-127">We'll also add a new controller with an endpoint that gets our **SecretPassword** secret from the vault.</span></span>

<span data-ttu-id="49c6b-128">Starten Sie zuerst die App: Öffnen Sie `Program.cs`, löschen Sie den Inhalt, und ersetzen Sie diesen durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="49c6b-128">First, the app startup: Open `Program.cs`, delete the contents and replace them with the following code:</span></span>

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
                    // authenticate to the vault using a managed identity. If a managed identity
                    // is not available, it will check if Visual Studio and/or the Azure CLI are
                    // installed locally and see if they are configured with credentials that can
                    // access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="49c6b-129">Speichern Sie Dateien unbedingt, wenn Sie diese fertig bearbeitet haben.</span><span class="sxs-lookup"><span data-stu-id="49c6b-129">Make sure to save files when you're done editing them.</span></span> <span data-ttu-id="49c6b-130">Verwenden Sie zu diesem Zweck das Menü „...“ oder die entsprechende Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux bzw. <kbd>CMD+S</kbd> unter macOS).</span><span class="sxs-lookup"><span data-stu-id="49c6b-130">You can do this either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

<span data-ttu-id="49c6b-131">Die einzige Änderung gegenüber dem Startercode ist das Hinzufügen von `ConfigureAppConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="49c6b-131">The only change from the starter code is the addition of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="49c6b-132">Hier laden Sie den Tresornamen aus der Konfiguration und rufen `AddAzureKeyVault` damit auf.</span><span class="sxs-lookup"><span data-stu-id="49c6b-132">This is where we load the vault name from configuration and call `AddAzureKeyVault` with it.</span></span>

<span data-ttu-id="49c6b-133">Nun kommen wir zum Controller: Erstellen Sie im Ordner `Controllers` die neue Datei `SecretTestController.cs`, und fügen Sie den folgenden Code darin ein.</span><span class="sxs-lookup"><span data-stu-id="49c6b-133">Next, the controller: Create a new file in the `Controllers` folder called `SecretTestController.cs` and paste the following code into it.</span></span>

> [!TIP]
> <span data-ttu-id="49c6b-134">Verwenden Sie den Befehl `touch` in der Shell, um eine neue Datei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="49c6b-134">To create a new file, use the `touch` command in the shell.</span></span> <span data-ttu-id="49c6b-135">Verwenden Sie in diesem Fall `touch Controllers/SecretTestController.cs`.</span><span class="sxs-lookup"><span data-stu-id="49c6b-135">In this case, use `touch Controllers/SecretTestController.cs`.</span></span> <span data-ttu-id="49c6b-136">Klicken Sie im Editor im Bereich „Dateien“ auf die Schaltfläche „Aktualisieren“, damit es dort angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="49c6b-136">You'll need to click the refresh button in the Files pane of the editor to see it there.</span></span>

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

<span data-ttu-id="49c6b-137">Führen Sie `dotnet build` in der Shell aus, um sicherzustellen, dass alles kompiliert wird.</span><span class="sxs-lookup"><span data-stu-id="49c6b-137">Run `dotnet build` in the shell to make sure everything compiles.</span></span> <span data-ttu-id="49c6b-138">Die App kann nun ausgeführt werden &mdash; machen wir weiter in Azure!</span><span class="sxs-lookup"><span data-stu-id="49c6b-138">The app is ready to run &mdash; now let's get it into Azure!</span></span>