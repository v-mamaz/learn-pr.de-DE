<span data-ttu-id="cc1e6-101">Jetzt ist es an der Zeit, die App in Azure auszuführen.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-101">Now it's time to run our app in Azure.</span></span> <span data-ttu-id="cc1e6-102">Sie müssen eine Azure App Service-App erstellen, sie mit einer verwalteten Identität und der Tresorkonfiguration einrichten und Code bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-102">We need to create an Azure App Service app, set it up with a managed identity and our vault configuration, and deploy our code.</span></span>

## <a name="create-the-app-service-plan-and-app"></a><span data-ttu-id="cc1e6-103">Erstellen des App Service-Plans und der App</span><span class="sxs-lookup"><span data-stu-id="cc1e6-103">Create the App Service plan and app</span></span>

<span data-ttu-id="cc1e6-104">Das Erstellen einer App Service-App ist ein zweistufiger Prozess: Erstellen Sie zuerst den *Plan* und dann die *App*.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-104">Creating an App Service app is a two-step process: First create the *plan*, then the *app*.</span></span>

<span data-ttu-id="cc1e6-105">Der Name des *Plans* muss nur innerhalb Ihres Abonnements eindeutig sein. Daher können Sie den gleichen Namen wie wir verwenden: **keyvault-exercise-plan**.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-105">The *plan* name only needs to be unique within your subscription, so you can use the same name we've used: **keyvault-exercise-plan**.</span></span> <span data-ttu-id="cc1e6-106">Der App-Name muss global eindeutig sein. Daher müssen Sie Ihren eigenen auswählen.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-106">The app name needs to be globally unique, though, so you'll need to pick your own.</span></span>

<span data-ttu-id="cc1e6-107">Führen Sie in Azure Cloud Shell Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="cc1e6-107">In Azure Cloud Shell, run the following:</span></span>

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

## <a name="add-configuration-to-the-app"></a><span data-ttu-id="cc1e6-108">Hinzufügen von Konfiguration zur App</span><span class="sxs-lookup"><span data-stu-id="cc1e6-108">Add configuration to the app</span></span>

<span data-ttu-id="cc1e6-109">Folgen Sie zum Bereitstellen in Azure der bewährten App Service-Methode, die VaultName-Konfiguration in eine Anwendungseinstellung anstatt in eine Konfigurationsdatei aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-109">For deploying to Azure, we'll follow the App Service best practice of putting the VaultName configuration in an application setting instead of a configuration file.</span></span>

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

## <a name="enable-managed-identity"></a><span data-ttu-id="cc1e6-110">Aktivieren der verwalteten Identität</span><span class="sxs-lookup"><span data-stu-id="cc1e6-110">Enable managed identity</span></span>

<span data-ttu-id="cc1e6-111">Das Aktivieren der verwalteten Identität für eine App findet in einer Zeile statt:</span><span class="sxs-lookup"><span data-stu-id="cc1e6-111">Enabling managed identity on an app is a one-liner:</span></span>

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="cc1e6-112">Kopieren Sie aus der resultierenden JSON-Ausgabe den **principalId**-Wert.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-112">From the JSON output that results, copy the **principalId** value.</span></span> <span data-ttu-id="cc1e6-113">„PrincipalId“ ist die eindeutige ID der neuen Identität der App in Azure Active Directory, und wir verwenden sie im nächsten Schritt.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-113">PrincipalId is the unique ID of the app's new identity in Azure Active Directory, and we're going to use it in the next step.</span></span>

## <a name="grant-access-to-the-vault"></a><span data-ttu-id="cc1e6-114">Gewähren von Zugriff auf den Tresor</span><span class="sxs-lookup"><span data-stu-id="cc1e6-114">Grant access to the vault</span></span>

<span data-ttu-id="cc1e6-115">Nun müssen Sie Ihrer App Identitätsberechtigungen erteilen, um Geheimnisse aus Ihrem Tresor für die Produktionsumgebung abzurufen und aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-115">Now you need to give your app identity permissions to get and list secrets from your production-environment vault.</span></span> <span data-ttu-id="cc1e6-116">Verwenden Sie den **principalId**-Wert, den Sie im vorherigen Schritt kopiert haben, als Wert für **object-id** im folgenden Befehl.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-116">Use the **principalId** value you copied from the previous step as the value for **object-id** in the command below.</span></span>

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-managed-identity-principleid> --secret-permissions get list
```

## <a name="deploy-the-app-and-try-it-out"></a><span data-ttu-id="cc1e6-117">Bereitstellen und Testen der App</span><span class="sxs-lookup"><span data-stu-id="cc1e6-117">Deploy the app and try it out</span></span>

<span data-ttu-id="cc1e6-118">Die Konfiguration ist festgelegt, und Sie können die App jetzt bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-118">All your configuration is set and you're ready to deploy!</span></span> <span data-ttu-id="cc1e6-119">Mit den folgenden Befehlen wird die Site im Ordner `pub` veröffentlicht, in `site.zip` komprimiert und die ZIP-Datei in App Service bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-119">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="cc1e6-120">Sie müssen mit `cd` wieder in das Verzeichnis „KeyVaultDemoApp“ wechseln, sofern noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-120">You'll need to `cd` back to the KeyVaultDemoApp directory if you haven't already.</span></span>

```azurecli
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

<span data-ttu-id="cc1e6-121">Sobald ein Ergebnis anzeigt, dass die Site bereitgestellt wurde, öffnen Sie `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-121">Once you get a result that indicates the site has deployed, open `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in a browser.</span></span> <span data-ttu-id="cc1e6-122">Der Geheimniswert **reindeer_flotilla** sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-122">You should see the secret value, **reindeer_flotilla**.</span></span>

<span data-ttu-id="cc1e6-123">Ihre App ist fertig und wurde bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="cc1e6-123">Your app is finished and deployed!</span></span>