<span data-ttu-id="574ed-101">Jetzt ist es an der Zeit, die App in Azure auszuführen.</span><span class="sxs-lookup"><span data-stu-id="574ed-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="574ed-102">Sie müssen eine Azure App Service-App erstellen, sie mit einer verwalteten Identität und der Tresorkonfiguration einrichten und Code bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="574ed-102">We need to create an Azure App Service app, set it up with a managed identity and our vault configuration, and deploy our code.</span></span>

## <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="574ed-103">Erstellen des App Service-Plans und der App</span><span class="sxs-lookup"><span data-stu-id="574ed-103">Create the App Service plan and app</span></span>

<span data-ttu-id="574ed-104">Das Erstellen einer App Service-App ist ein zweistufiger Prozess: Erstellen Sie zuerst den *Plan* und dann die *App*.</span><span class="sxs-lookup"><span data-stu-id="574ed-104">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="574ed-105">Der Name des *Plans* muss nur innerhalb Ihres Abonnements eindeutig sein. Daher können Sie den gleichen Namen wie wir verwenden: **keyvault-exercise-plan**.</span><span class="sxs-lookup"><span data-stu-id="574ed-105">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="574ed-106">Der App-Name muss global eindeutig sein. Daher müssen Sie Ihren eigenen auswählen.</span><span class="sxs-lookup"><span data-stu-id="574ed-106">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span> <span data-ttu-id="574ed-107">Verwenden Sie den gleichen Speicherort, den Sie beim Erstellen Ihres Caches verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="574ed-107">Use the same location you used when creating the vault.</span></span>

<span data-ttu-id="574ed-108">Führen Sie in Azure Cloud Shell Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="574ed-108">In Azure Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create \
    --name keyvault-exercise-plan \
    --resource-group <rgn>[sandbox resource group name]</rgn>
    --location eastus

az webapp create \
    --name <your-unique-app-name> \
    --plan keyvault-exercise-plan \
    --resource-group <rgn>[sandbox resource group name]</rgn>
```

## <a name="add-configuration-to-the-app"></a><span data-ttu-id="574ed-109">Hinzufügen von Konfiguration zur App</span><span class="sxs-lookup"><span data-stu-id="574ed-109">Add configuration to the app</span></span>

<span data-ttu-id="574ed-110">Folgen Sie zum Bereitstellen in Azure der bewährten App Service-Methode, die VaultName-Konfiguration in eine Anwendungseinstellung anstatt in eine Konfigurationsdatei aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="574ed-110">For deploying to Azure, we'll follow the App Service best practice of putting the VaultName configuration in an application setting instead of a configuration file.</span></span> <span data-ttu-id="574ed-111">Führen Sie diesen Befehl zum Erstellen der Anwendungseinstellung aus:</span><span class="sxs-lookup"><span data-stu-id="574ed-111">Run this command to create the application setting:</span></span>

```azurecli
az webapp config appsettings set \
    --name <your-unique-app-name> \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --settings VaultName=<your-unique-vault-name>
```

## <a name="enable-managed-identity"></a><span data-ttu-id="574ed-112">Aktivieren der verwalteten Identität</span><span class="sxs-lookup"><span data-stu-id="574ed-112">Enable managed identity</span></span>

<span data-ttu-id="574ed-113">Zum Aktivieren der verwalteten Identität in einer App reicht eine Zeile aus &mdash; führen Sie dies zur Aktivierung in Ihrer App aus:</span><span class="sxs-lookup"><span data-stu-id="574ed-113">Enabling managed identity on an app is a one-liner &mdash; run this to enable it on your app:</span></span>

```azurecli
az webapp identity assign \
    --name <your-unique-app-name> \
    --resource-group <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="574ed-114">Kopieren Sie aus der resultierenden JSON-Ausgabe den **principalId**-Wert.</span><span class="sxs-lookup"><span data-stu-id="574ed-114">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="574ed-115">„PrincipalId“ ist die eindeutige ID der neuen Identität der App in Azure Active Directory, und wir verwenden sie im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="574ed-115">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

## <a name="grant-access-to-the-vault"></a><span data-ttu-id="574ed-116">Gewähren von Zugriff auf den Tresor</span><span class="sxs-lookup"><span data-stu-id="574ed-116">Grant access to the vault</span></span>

<span data-ttu-id="574ed-117">Im letzten Schritt vor der Bereitstellung weisen Sie der verwalteten Identität Ihrer App Key Vault-Berechtigungen zu.</span><span class="sxs-lookup"><span data-stu-id="574ed-117">The last step before deploying is to assign Key Vault permissions to your app's managed identity.</span></span> <span data-ttu-id="574ed-118">Verwenden Sie den **principalId**-Wert, den Sie im vorherigen Schritt kopiert haben, als Wert für **object-id** im folgenden Befehl.</span><span class="sxs-lookup"><span data-stu-id="574ed-118">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span> <span data-ttu-id="574ed-119">Die Ausführung dieses Befehls gewährt **Get**- und **List**-Zugriff:</span><span class="sxs-lookup"><span data-stu-id="574ed-119">Running this command will grant **Get** and **List** access:</span></span>

```azurecli
az keyvault set-policy \
    --name <your-unique-vault-name> \
    --object-id <your-managed-identity-principleid> \
    --secret-permissions get list
```

## <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="574ed-120">Bereitstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="574ed-120">Deploy the app and try it out</span></span>

<span data-ttu-id="574ed-121">Die Konfiguration ist festgelegt, und Sie können die App jetzt bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="574ed-121">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="574ed-122">Mit den folgenden Befehlen wird die Site im Ordner `pub` veröffentlicht, in `site.zip` komprimiert und die ZIP-Datei in App Service bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="574ed-122">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="574ed-123">Sie müssen mit `cd` wieder in das Verzeichnis „KeyVaultDemoApp“ wechseln, sofern noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="574ed-123">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```azurecli
dotnet publish -o pub
zip -j site.zip pub/*

az webapp deployment source config-zip \
    --src site.zip \
    --name <your-unique-app-name> \
    --resource-group <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="574ed-124">Sobald ein Ergebnis anzeigt, dass die Site bereitgestellt wurde, öffnen Sie `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="574ed-124">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="574ed-125">Der Geheimniswert **reindeer_flotilla** sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="574ed-125">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="574ed-126">Ihre App ist fertig und wurde bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="574ed-126">Your app is finished and deployed!</span></span>