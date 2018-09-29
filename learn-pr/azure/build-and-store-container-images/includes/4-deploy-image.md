<span data-ttu-id="61239-101">Containerimages können über viele Containerverwaltungsplattformen aus Azure Container Registry abgerufen werden – etwa mit Azure Container Instances, Azure Kubernetes Registry und Docker für Windows oder Mac.</span><span class="sxs-lookup"><span data-stu-id="61239-101">Container images can be pulled from Azure Container Registry using many container management platforms, such as Azure Container Instances, Azure Kubernetes Registry, and Docker for Windows or Mac.</span></span> <span data-ttu-id="61239-102">Für das Ausführen von Containerimages aus Azure Container Registry können Authentifizierungsanmeldeinformationen erforderlich sein.</span><span class="sxs-lookup"><span data-stu-id="61239-102">When running container images from Azure Container Registry, authentication credentials may be needed.</span></span> 

<span data-ttu-id="61239-103">Es wird empfohlen, einen Azure-Dienstprinzipal für die Authentifizierung mit Container Registry zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="61239-103">It is recommended to use an Azure service principal for authentication with Container Registry.</span></span> <span data-ttu-id="61239-104">Darüber hinaus empfiehlt es sich, die Anmeldeinformationen für den Azure-Dienstprinzipal in Azure Key Vault zu schützen.</span><span class="sxs-lookup"><span data-stu-id="61239-104">It is also recommended to secure the Azure service principal credentials in Azure Key Vault.</span></span> <span data-ttu-id="61239-105">In dieser Einheit wenden wir die empfohlene Vorgehensweise an.</span><span class="sxs-lookup"><span data-stu-id="61239-105">In this unit we'll follow the recommended approach.</span></span>

<span data-ttu-id="61239-106">Für die Liveübung verwenden wir jedoch das integrierte Administratorkonto, das in jeder Azure Container Registry-Instanz aktiviert werden kann.</span><span class="sxs-lookup"><span data-stu-id="61239-106">However, for our live practice we will use the built-in admin account that can be enabled in all Azure Container Registries.</span></span> <span data-ttu-id="61239-107">Das Administratorkonto kann zusammen mit den kostenlosen Sandboxressourcen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="61239-107">The admin account works with the free sandbox resources.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="61239-108">Erstellen Sie eine Variable mit dem Namen Ihrer Containerregistrierung in Kleinbuchstaben. (Verwenden Sie also beispielsweise „meincontainer“ anstatt „MeinContainer“.)</span><span class="sxs-lookup"><span data-stu-id="61239-108">Create a variable with the name of your container registry in lowercase (for example, instead of "MyContainer" make the value "mycontainer").</span></span> <span data-ttu-id="61239-109">Diese Variable wird im gesamten Verlauf dieser Einheit verwendet.</span><span class="sxs-lookup"><span data-stu-id="61239-109">This variable is used throughout this unit.</span></span>

```azurecli
ACR_NAME=<acrName>
```

### <a name="service-principal"></a><span data-ttu-id="61239-110">Dienstprinzipal</span><span class="sxs-lookup"><span data-stu-id="61239-110">Service Principal</span></span>

<span data-ttu-id="61239-111">Für eine Produktionsanwendung würden wir an dieser Stelle einen Dienstprinzipal erstellen.</span><span class="sxs-lookup"><span data-stu-id="61239-111">For a production application, we would want to create a service principal here.</span></span> <span data-ttu-id="61239-112">**In der Sandboxumgebung funktioniert das nicht.** Es empfiehlt sich aber, dies in Ihren eigenen Systemen umzusetzen.</span><span class="sxs-lookup"><span data-stu-id="61239-112">Remember **this won't work in our sandbox environment**, but it's a best practice to follow in your own systems.</span></span> <span data-ttu-id="61239-113">Verwenden Sie für die Liveübung die nachstehenden Anweisungen zum Administratorkonto.</span><span class="sxs-lookup"><span data-stu-id="61239-113">For our live practice, you'll use the Admin Account instructions below.</span></span>

<span data-ttu-id="61239-114">Zum Erstellen des Dienstprinzipals können Sie den Befehl `az ad sp create-for-rbac` verwenden.</span><span class="sxs-lookup"><span data-stu-id="61239-114">The `az ad sp create-for-rbac` command can be used to create the service principal.</span></span> <span data-ttu-id="61239-115">Das Argument `--role` konfiguriert den Dienstprinzipal mit der Rolle *reader* (Leser), die ihm ausschließlich Pullzugriff auf die Registrierung gewährt.</span><span class="sxs-lookup"><span data-stu-id="61239-115">The `--role` argument configures the service principal with the *reader* role, which grants it pull-only access to the registry.</span></span> <span data-ttu-id="61239-116">Um sowohl Push- als auch Pullzugriff zu gewähren, würden Sie das Argument `--role` in *contributor* (Mitwirkender) ändern.</span><span class="sxs-lookup"><span data-stu-id="61239-116">To grant both push and pull access, you would change the `--role` argument to *contributor*.</span></span>

```azurecli
az ad sp create-for-rbac --scopes $(az acr show --name $ACR_NAME --query id --output tsv) --role reader
```

<span data-ttu-id="61239-117">So würde die Ausgabe der Erstellung des Dienstprinzipals aussehen.</span><span class="sxs-lookup"><span data-stu-id="61239-117">This is what the output of the service principal creation would look like.</span></span> <span data-ttu-id="61239-118">Notieren Sie sich die Werte `appId` und `password`.</span><span class="sxs-lookup"><span data-stu-id="61239-118">Take note of the `appId` and the `password` values.</span></span> <span data-ttu-id="61239-119">Diese werden in Azure Key Vault gespeichert.</span><span class="sxs-lookup"><span data-stu-id="61239-119">These should be stored in the Azure key vault.</span></span>

```output
{
  "appId": "1fa05179-0000-0000-0000-e269a4e97c41",
  "displayName": "azure-cli-2018-08-19-22-35-26",
  "name": "http://azure-cli-2018-08-19-22-35-26",
  "password": "72377509-0000-0000-0000-c8edbcb2d950",
  "tenant": "00000000-0000-0000-0000-000000000000"
}
```

### <a name="admin-account"></a><span data-ttu-id="61239-120">Administratorkonto</span><span class="sxs-lookup"><span data-stu-id="61239-120">Admin Account</span></span>

<span data-ttu-id="61239-121">Azure-Containerregistrierungen verfügen über ein integriertes Administratorkonto.</span><span class="sxs-lookup"><span data-stu-id="61239-121">Azure Container Registries come with a built-in Admin account.</span></span> <span data-ttu-id="61239-122">Dieses ist nicht an Azure AD oder an rollenbasierte Zugriffssteuerungen gebunden und sollte daher **nur zu Testzwecken verwendet werden**.</span><span class="sxs-lookup"><span data-stu-id="61239-122">This isn't tied to Azure AD or role based access controls and therefore **should only be used for testing**.</span></span> 

1. <span data-ttu-id="61239-123">Aktivieren Sie das Administratorkonto.</span><span class="sxs-lookup"><span data-stu-id="61239-123">Enable the Admin Account.</span></span>
    ```azurecli
      az acr update -n $ACR_NAME --admin-enabled true
    ```

2. <span data-ttu-id="61239-124">Abfrage zum Abrufen des automatisch generierten Benutzernamens und Kennworts</span><span class="sxs-lookup"><span data-stu-id="61239-124">Query to get the autogenerated username and password</span></span>

    ```azurecli
      az acr credential show --name $ACR_NAME
    ```

<span data-ttu-id="61239-125">Die Ausgabe sieht in etwa wie folgt aus.</span><span class="sxs-lookup"><span data-stu-id="61239-125">The output is similar to below.</span></span> <span data-ttu-id="61239-126">Notieren Sie sich Folgendes: `username` und `value` in Verbindung mit `name` „password“.</span><span class="sxs-lookup"><span data-stu-id="61239-126">Take note of the `username` and the `value` paired with the `name` "password".</span></span> <span data-ttu-id="61239-127">Diese werden später in einem Schlüsseltresor gespeichert.</span><span class="sxs-lookup"><span data-stu-id="61239-127">You'll save these into key vault.</span></span>

```output
{  "passwords": [
    {
      "name": "password",
      "value": "aaaaa"
    },
    {
      "name": "password2",
      "value": "bbbbb"
    }
  ],
  "username": "ccccc"
}
```

### <a name="save-the-username-and-password-to-the-key-vault"></a><span data-ttu-id="61239-128">Speichern von Benutzername und Kennwort im Schlüsseltresor</span><span class="sxs-lookup"><span data-stu-id="61239-128">Save the username and password to the key vault</span></span>

1. <span data-ttu-id="61239-129">Erstellen Sie mit dem Befehl `az keyvault create` eine Azure Key Vault-Instanz.</span><span class="sxs-lookup"><span data-stu-id="61239-129">Create an Azure Key Vault with the `az keyvault create` command.</span></span>

    ```azurecli
    az keyvault create --resource-group <rgn>[sandbox resource group name]</rgn> --name $ACR_NAME-keyvault
    ```

1. <span data-ttu-id="61239-130">Verwenden Sie den Befehl `az keyvault secret set`, um den Benutzernamen für die ACR-Instanz im Tresor speichern.</span><span class="sxs-lookup"><span data-stu-id="61239-130">Use the `az keyvault secret set` command to store the username for the ACR in the vault.</span></span> <span data-ttu-id="61239-131">Bei der Nutzung von Dienstprinzipalen würden Sie die App-ID für diesen Wert verwenden.</span><span class="sxs-lookup"><span data-stu-id="61239-131">If you were using service principals you'd use the appId for this value.</span></span> <span data-ttu-id="61239-132">Da Sie hier das Administratorkonto verwenden, speichern Sie den Benutzernamen aus der obigen Abfrage.</span><span class="sxs-lookup"><span data-stu-id="61239-132">Since we're using the admin account this time we'll save the username from our query above.</span></span> <span data-ttu-id="61239-133">Geben Sie den folgenden Befehl ein, und vergessen Sie nicht, `<username>` zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="61239-133">Enter the command below, don't forget to replace `<username>`.</span></span>

    ```azurecli
    az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --value <username>
    ```

1. <span data-ttu-id="61239-134">Verwenden Sie nun den Befehl `az keyvault secret set`, um das *Kennwort* im Tresor zu speichern.</span><span class="sxs-lookup"><span data-stu-id="61239-134">Use the `az keyvault secret set` command to store the *password* in the vault.</span></span> <span data-ttu-id="61239-135">Ersetzen Sie `<password>` durch `password` aus der obigen Abfrage.</span><span class="sxs-lookup"><span data-stu-id="61239-135">Replace `<password>` with the `password` from the query above.</span></span>

    ```azurecli
    az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --value <password>
    ```

<span data-ttu-id="61239-136">Sie haben nun einen Azure-Schlüsseltresor erstellt und zwei Geheimnisse darin gespeichert:</span><span class="sxs-lookup"><span data-stu-id="61239-136">You've now created an Azure key vault and stored two secrets in it:</span></span>

* <span data-ttu-id="61239-137">`$ACR_NAME-pull-usr`: der **Benutzername** für die Containerregistrierung</span><span class="sxs-lookup"><span data-stu-id="61239-137">`$ACR_NAME-pull-usr`: the container registry **username**.</span></span>
* <span data-ttu-id="61239-138">`$ACR_NAME-pull-pwd`: das **Kennwort** für die Containerregistrierung</span><span class="sxs-lookup"><span data-stu-id="61239-138">`$ACR_NAME-pull-pwd`: the container registry **password**.</span></span>

<span data-ttu-id="61239-139">Sie können nun anhand des Namens auf diese Geheimnisse verweisen, wenn Sie oder Ihre Anwendungen und Dienste Images per Pull aus der Registrierung abrufen.</span><span class="sxs-lookup"><span data-stu-id="61239-139">You can now reference these secrets by name when you or your applications and services pull images from the registry.</span></span>

### <a name="deploy-a-container-with-azure-cli"></a><span data-ttu-id="61239-140">Bereitstellen eines Containers mit Azure CLI</span><span class="sxs-lookup"><span data-stu-id="61239-140">Deploy a container with Azure CLI</span></span>

<span data-ttu-id="61239-141">Jetzt, da die Anmeldeinformationen des Dienstprinzipals in Azure Key Vault gespeichert sind, können Ihre Anwendungen und Dienste diese verwenden, um auf Ihre private Registrierung zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="61239-141">Now that the service principal credentials are stored in Azure Key Vault, your applications and services can use them to access your private registry.</span></span>

<span data-ttu-id="61239-142">Führen Sie den folgenden `az container create`-Befehl aus, um eine Containerinstanz bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="61239-142">Execute the following `az container create` command to deploy a container instance.</span></span> <span data-ttu-id="61239-143">Der Befehl verwendet die in Azure Key Vault gespeicherten Anmeldeinformationen des Dienstprinzipals, um sich bei Ihrer Containerregistrierung zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="61239-143">The command uses the service principal's credentials stored in Azure Key Vault to authenticate to your container registry.</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name acr-tasks \
    --image $ACR_NAME.azurecr.io/helloacrtasks:v1 \
    --registry-login-server $ACR_NAME.azurecr.io \
    --ip-address Public \
    --location eastus \
    --registry-username $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --query value -o tsv) \
    --registry-password $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --query value -o tsv)
```

<span data-ttu-id="61239-144">Rufen Sie die IP-Adresse der Azure-Containerinstanz ab.</span><span class="sxs-lookup"><span data-stu-id="61239-144">Get the IP address of the Azure container instance.</span></span>

```azurecli
az container show --resource-group  <rgn>[sandbox resource group name]</rgn> --name acr-tasks --query ipAddress.ip --output table
```

<span data-ttu-id="61239-145">Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers.</span><span class="sxs-lookup"><span data-stu-id="61239-145">Open a browser and navigate to the IP address of the container.</span></span> <span data-ttu-id="61239-146">Wenn alles ordnungsgemäß konfiguriert wurde, sollten jetzt die folgenden Ergebnisse angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="61239-146">If everything has been configured correctly, you should see the following results:</span></span>

![Beispiel-Web-App mit dem Text „Hello World“](../media/hello.png)

