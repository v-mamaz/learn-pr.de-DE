<span data-ttu-id="02841-101">Jetzt ist es an der Zeit, dass unsere App in Azure ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="02841-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="02841-102">Wir müssen eine Azure App Service-App erstellen, sie mit der MSI und unserer Tresorkonfiguration einrichten und Code bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="02841-102">We need to create an Azure App Service app, set it up with MSI and our vault configuration, and deploy our code.</span></span>

## <a name="exercise"></a><span data-ttu-id="02841-103">Übung</span><span class="sxs-lookup"><span data-stu-id="02841-103">Exercise</span></span>

### <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="02841-104">Erstellen des App Service-Plans und der App</span><span class="sxs-lookup"><span data-stu-id="02841-104">Create the App Service plan and app</span></span>

<span data-ttu-id="02841-105">Das Erstellen einer App Service-App ist ein zweistufiger Prozess: Erstellen Sie zuerst den *Plan* und dann die *App*.</span><span class="sxs-lookup"><span data-stu-id="02841-105">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="02841-106">Der Name des *Plans* muss nur innerhalb Ihres Abonnements eindeutig sein. Daher können Sie den gleichen Namen wie wir verwenden: **keyvault-exercise-plan**.</span><span class="sxs-lookup"><span data-stu-id="02841-106">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="02841-107">Der App-Name muss global eindeutig sein. Daher müssen Sie Ihren eigenen auswählen.</span><span class="sxs-lookup"><span data-stu-id="02841-107">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span>

<span data-ttu-id="02841-108">Führen Sie in Azure Cloud Shell Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="02841-108">In Azure Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a><span data-ttu-id="02841-109">Hinzufügen der Konfiguration zur App</span><span class="sxs-lookup"><span data-stu-id="02841-109">Add configuration to the app</span></span>

<span data-ttu-id="02841-110">Zum Bereitstellen in Azure folgen wir der bewährten App Service-Methode, die Konfiguration in die Anwendungseinstellungen aufzunehmen, statt eine Konfigurationsdatei zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="02841-110">For deploying to Azure, we'll follow the App Service best practice of putting configuration in Application Settings instead of a configuration file.</span></span>

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a><span data-ttu-id="02841-111">Aktivieren der MSI</span><span class="sxs-lookup"><span data-stu-id="02841-111">Enable MSI</span></span>

<span data-ttu-id="02841-112">Die MSI wird für eine App mit einer Zeile aktiviert:</span><span class="sxs-lookup"><span data-stu-id="02841-112">Enabling MSI on an app is a one-liner:</span></span>

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="02841-113">Kopieren Sie aus der resultierenden JSON-Ausgabe den **principalId**-Wert.</span><span class="sxs-lookup"><span data-stu-id="02841-113">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="02841-114">„PrincipalId“ ist die eindeutige ID der neuen Identität der App in Azure Active Directory, und wir verwenden sie im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="02841-114">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

### <a name="grant-access-to-the-vault"></a><span data-ttu-id="02841-115">Gewähren von Zugriff auf den Tresor</span><span class="sxs-lookup"><span data-stu-id="02841-115">Grant access to the vault</span></span>

<span data-ttu-id="02841-116">Nun müssen Sie Ihrer App Identitätsberechtigungen erteilen, um Geheimnisse aus Ihrem Tresor für die Produktionsumgebung abzurufen und aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="02841-116">Now you need to give your app identity permissions to get and list secrets from your production-environment vault.</span></span> <span data-ttu-id="02841-117">Verwenden Sie den **principalId**-Wert, den Sie im vorherigen Schritt kopiert haben, als Wert für **object-id** im folgenden Befehl.</span><span class="sxs-lookup"><span data-stu-id="02841-117">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span>

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="02841-118">Bereitstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="02841-118">Deploy the app and try it out</span></span>

<span data-ttu-id="02841-119">Die Konfiguration ist festgelegt, und Sie können die App jetzt bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="02841-119">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="02841-120">Mit den folgenden Befehlen wird die Site im Ordner `pub` veröffentlicht, in `site.zip` komprimiert und die ZIP-Datei in App Service bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="02841-120">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="02841-121">Sie müssen mit `cd` wieder in das Verzeichnis „KeyVaultDemoApp“ wechseln, sofern noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="02841-121">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="02841-122">Sobald ein Ergebnis anzeigt, dass die Site bereitgestellt wurde, öffnen Sie `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="02841-122">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="02841-123">Der Geheimniswert **reindeer_flotilla** sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="02841-123">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="02841-124">Ihre App ist fertig und wurde bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="02841-124">Your app is finished and deployed!</span></span>