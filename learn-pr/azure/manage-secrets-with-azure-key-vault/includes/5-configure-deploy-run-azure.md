<span data-ttu-id="c4607-101">Jetzt ist es Zeit für unsere app in Azure ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="c4607-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="c4607-102">Wir müssen erstellen eine App Service-app, richten sie Sie mit MSI-Datei und unseren schlüsseltresor-Konfiguration und unser Code bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c4607-102">We need to create an App Service app, set it up with MSI and our vault configuration, and deploy our code.</span></span>

# <a name="exercise"></a><span data-ttu-id="c4607-103">Übung</span><span class="sxs-lookup"><span data-stu-id="c4607-103">Exercise</span></span>

## <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="c4607-104">Erstellen Sie die App Service-Plan und die app</span><span class="sxs-lookup"><span data-stu-id="c4607-104">Create the App Service plan and app</span></span>

<span data-ttu-id="c4607-105">Erstellen einer App Service-app ist ein zweistufiger Prozess: Erstellen Sie zunächst die *Plan*, und klicken Sie dann die *app*.</span><span class="sxs-lookup"><span data-stu-id="c4607-105">Creating an App Service app is a two-step process: first create the *plan*, then the *app*.</span></span>

<span data-ttu-id="c4607-106">Die *Plan* nur muss innerhalb Ihres Abonnements eindeutig sein, damit Sie den gleichen Namen verwenden können, die wir verwendet haben: **Keyvault-Übung-Plan**.</span><span class="sxs-lookup"><span data-stu-id="c4607-106">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="c4607-107">Der app-Name muss global eindeutig sein, jedoch so Sie wählen Sie Ihre eigenen müssen.</span><span class="sxs-lookup"><span data-stu-id="c4607-107">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span>

<span data-ttu-id="c4607-108">Führen Sie in Cloud Shell die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="c4607-108">In Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

## <a name="add-configuration-to-the-app"></a><span data-ttu-id="c4607-109">Konfiguration für die app hinzufügen</span><span class="sxs-lookup"><span data-stu-id="c4607-109">Add configuration to the app</span></span>

<span data-ttu-id="c4607-110">Für in Azure bereitstellen, müssen wir Konfiguration in den Anwendungseinstellungen zu platzieren, statt eine Konfigurationsdatei der App Service-Empfehlung zu folgen.</span><span class="sxs-lookup"><span data-stu-id="c4607-110">For deploying to Azure, we'll follow the App Service best practice of putting configuration in Application Settings instead of a configuration file.</span></span>

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

## <a name="enable-msi"></a><span data-ttu-id="c4607-111">Aktivieren der MSI</span><span class="sxs-lookup"><span data-stu-id="c4607-111">Enable MSI</span></span>

<span data-ttu-id="c4607-112">Aktivieren von MSI für eine app ist eine Einzeiler:</span><span class="sxs-lookup"><span data-stu-id="c4607-112">Enabling MSI on an app is a one-liner:</span></span>

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="c4607-113">Kopieren Sie aus der JSON-Ausgabe, die sich ergibt, der **PrincipalId** Wert.</span><span class="sxs-lookup"><span data-stu-id="c4607-113">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="c4607-114">PrincipalId ist die eindeutige ID des neuen der app-Identität in Azure Active Directory, und wir werden es im nächsten Schritt verwenden.</span><span class="sxs-lookup"><span data-stu-id="c4607-114">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

## <a name="grant-access-to-the-vault"></a><span data-ttu-id="c4607-115">Gewähren des Zugriffs auf den Tresor</span><span class="sxs-lookup"><span data-stu-id="c4607-115">Grant access to the vault</span></span>

<span data-ttu-id="c4607-116">Nun müssen wir unsere app bereitstellen Identitätsberechtigungen abrufen und Auflisten von Geheimnissen aus die produktionsumgebung Vault.</span><span class="sxs-lookup"><span data-stu-id="c4607-116">Now we need to give our app identity permissions to get and list secrets from our production-environment vault.</span></span> <span data-ttu-id="c4607-117">Verwenden der **PrincipalId** als Wert für aus dem vorherigen Schritt kopierten Wert **Objekt-Id** in den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="c4607-117">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span>

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

## <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="c4607-118">Bereitstellen der app, und probieren Sie es aus</span><span class="sxs-lookup"><span data-stu-id="c4607-118">Deploy the app and try it out</span></span>

<span data-ttu-id="c4607-119">Alle unsere-Konfiguration festgelegt ist, und wir sind für die Bereitstellung bereit!</span><span class="sxs-lookup"><span data-stu-id="c4607-119">All our configuration is set and we're ready to deploy!</span></span> <span data-ttu-id="c4607-120">Die folgenden Befehle wird den Standort veröffentlicht die `pub` Ordner komprimieren sie Sie in `site.zip`, und die ZIP-Datei in App Service bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="c4607-120">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="c4607-121">Sie müssen `cd` zurück in das Verzeichnis KeyVaultDemoApp, sofern Sie noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="c4607-121">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="c4607-122">Die Website wurde bereitgestellt, sobald Sie ein Ergebnis zu erhalten, der angibt, öffnen Sie `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="c4607-122">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="c4607-123">Daraufhin sollte das Geheimnis, **Reindeer_flotilla**.</span><span class="sxs-lookup"><span data-stu-id="c4607-123">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="c4607-124">Die app beendet und bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="c4607-124">Our app is finished and deployed!</span></span>