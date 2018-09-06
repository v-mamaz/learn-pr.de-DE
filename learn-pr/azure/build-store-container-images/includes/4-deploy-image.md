<span data-ttu-id="edb19-101">Containerimages können über viele Containerverwaltungsplattformen aus Azure Container Registry abgerufen werden, z.B. Azure Container Instances, Azure Kubernetes Registry und Docker für Windows oder Mac.</span><span class="sxs-lookup"><span data-stu-id="edb19-101">Container images can be pulled from Azure Container Registry from many container management platforms, such as Azure Container Instances, Azure Kubernetes Registry, and Docker for Windows or Mac.</span></span> <span data-ttu-id="edb19-102">Für das Ausführen von Containerimages aus Azure Container Registry können Authentifizierungsanmeldeinformationen erforderlich sein.</span><span class="sxs-lookup"><span data-stu-id="edb19-102">When running container images from Azure Container Registry, authentication credentials may be needed.</span></span> <span data-ttu-id="edb19-103">Es wird empfohlen, einen Azure-Dienstprinzipal für die Authentifizierung mit Container Registry zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="edb19-103">It is recommended to use an Azure service principal for authentication with Container Registry.</span></span> <span data-ttu-id="edb19-104">Darüber hinaus wird ebenfalls empfohlen, die Anmeldeinformationen für den Azure-Dienstprinzipal in Azure Key Vault zu schützen.</span><span class="sxs-lookup"><span data-stu-id="edb19-104">Furthermore, it is also recommended to secure the Azure service principal credentials in Azure Key Vault.</span></span>

<span data-ttu-id="edb19-105">In dieser Einheit erstellen Sie einen Dienstprinzipal für die Azure-Containerregistrierung, speichern diesen in Azure Key Vault und stellen dann den Container mithilfe der Anmeldeinformationen des Dienstprinzipals in Azure Container Instances bereit.</span><span class="sxs-lookup"><span data-stu-id="edb19-105">In this unit, you will create a service principal for your Azure container registry, store it in Azure Key Vault, and then deploy the container to Azure Container Instances using the service principal's credentials.</span></span>

## <a name="configure-registry-authentication"></a><span data-ttu-id="edb19-106">Konfigurieren der Authentifizierung der Registrierung</span><span class="sxs-lookup"><span data-stu-id="edb19-106">Configure registry authentication</span></span>

<span data-ttu-id="edb19-107">Für alle Produktionsszenarios sollten Dienstprinzipale für den Zugriff auf eine Azure-Containerregistrierung verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="edb19-107">All production scenarios should use service principals to access an Azure container registry.</span></span> <span data-ttu-id="edb19-108">Mit Dienstprinzipalen können Sie die rollenbasierte Zugriffssteuerung für Ihre Containerimages bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="edb19-108">Service principals allow you to provide role-based access control (RBAC) to your container images.</span></span> <span data-ttu-id="edb19-109">Beispielsweise können Sie einen Dienstprinzipal mit ausschließlichem Pullzugriff auf eine Registrierung konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="edb19-109">For example, you can configure a service principal with pull-only access to a registry.</span></span>

<span data-ttu-id="edb19-110">Wenn Sie noch keinen Tresor in Azure Key Vault haben, erstellen Sie einen mit Azure CLI und den folgenden Befehlen.</span><span class="sxs-lookup"><span data-stu-id="edb19-110">If you don't already have a vault in Azure Key Vault, create one with the Azure CLI using the following commands.</span></span>

<span data-ttu-id="edb19-111">Erstellen Sie zunächst eine Variable mit dem Namen Ihrer Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="edb19-111">First, create a variable with the name of your container registry.</span></span> <span data-ttu-id="edb19-112">Diese Variable wird im gesamten Verlauf dieser Einheit verwendet.</span><span class="sxs-lookup"><span data-stu-id="edb19-112">This variable is used throughout this unit.</span></span>

```azurecli
ACR_NAME=<acrName>
```

<span data-ttu-id="edb19-113">Erstellen Sie mit dem Befehl `az keyvault create` einen Azure-Schlüsseltresor.</span><span class="sxs-lookup"><span data-stu-id="edb19-113">Create an Azure key vault with the `az keyvault create` command.</span></span>

```azurecli
az keyvault create --resource-group myResourceGroup --name $ACR_NAME-keyvault
```

<span data-ttu-id="edb19-114">Nun müssen Sie einen Dienstprinzipal erstellen und dessen Anmeldeinformationen in Ihrem Schlüsseltresor speichern.</span><span class="sxs-lookup"><span data-stu-id="edb19-114">Now, you need to create a service principal and store its credentials in your key vault.</span></span>

<span data-ttu-id="edb19-115">Verwenden Sie den Befehl `az ad sp create-for-rbac`, um den Dienstprinzipal zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="edb19-115">Use the `az ad sp create-for-rbac` command to create the service principal.</span></span> <span data-ttu-id="edb19-116">Das Argument `--role` konfiguriert den Dienstprinzipal mit der Rolle *reader* (Leser), die ihm ausschließlich Pullzugriff auf die Registrierung gewährt.</span><span class="sxs-lookup"><span data-stu-id="edb19-116">The `--role` argument configures the service principal with the *reader* role, which grants it pull-only access to the registry.</span></span> <span data-ttu-id="edb19-117">Ändern Sie das Argument `--role` in *contributor* (Mitwirkender), um sowohl Push- als auch Pullzugriff zu gewähren.</span><span class="sxs-lookup"><span data-stu-id="edb19-117">To grant both push and pull access, change the `--role` argument to *contributor*.</span></span>

```azurecli
az ad sp create-for-rbac --scopes $(az acr show --name $ACR_NAME --query id --output tsv) --role reader
```

<span data-ttu-id="edb19-118">So würde die Ausgabe der Erstellung des Dienstprinzipals aussehen.</span><span class="sxs-lookup"><span data-stu-id="edb19-118">This is what the output of the service principal creation will look like.</span></span> <span data-ttu-id="edb19-119">Notieren Sie sich die Werte `appId` und `password`.</span><span class="sxs-lookup"><span data-stu-id="edb19-119">Take note of the `appId` and the `password` values.</span></span> <span data-ttu-id="edb19-120">Diese werden im Azure-Schlüsseltresor gespeichert.</span><span class="sxs-lookup"><span data-stu-id="edb19-120">These will be stored in the Azure key vault.</span></span>

```bash
{
  "appId": "1fa05179-0000-0000-0000-e269a4e97c41",
  "displayName": "azure-cli-2018-08-19-22-35-26",
  "name": "http://azure-cli-2018-08-19-22-35-26",
  "password": "72377509-0000-0000-0000-c8edbcb2d950",
  "tenant": "00000000-0000-0000-0000-000000000000"
}
```

<span data-ttu-id="edb19-121">Verwenden Sie als Nächstes den `az keyvault secret set`-Befehl, um die *App-ID* des Dienstprinzipals im Tresor zu speichern.</span><span class="sxs-lookup"><span data-stu-id="edb19-121">Next, use the `az keyvault secret set` command to store the service principal's *appId* in the vault.</span></span> <span data-ttu-id="edb19-122">Ersetzen Sie `<appId>` durch die `appId` des Dienstprinzipals.</span><span class="sxs-lookup"><span data-stu-id="edb19-122">Replace `<appId>` with the `appId` of the service principal.</span></span>

```azurecli
az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --value <appId>
```

<span data-ttu-id="edb19-123">Verwenden Sie jetzt den Befehl `az keyvault secret set`, um das *Kennwort* des Dienstprinzipals im Schlüsseltresor zu speichern.</span><span class="sxs-lookup"><span data-stu-id="edb19-123">Now, use the `az keyvault secret set` command to store the service principal's *password* in the vault.</span></span> <span data-ttu-id="edb19-124">Ersetzen Sie `<password>` durch die `password` des Dienstprinzipals.</span><span class="sxs-lookup"><span data-stu-id="edb19-124">Replace `<password>` with the `password` of the service principal.</span></span>

```azurecli
az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --value <password>
```

<span data-ttu-id="edb19-125">Sie haben einen Azure-Schlüsseltresor erstellt und zwei Geheimnisse in diesem gespeichert:</span><span class="sxs-lookup"><span data-stu-id="edb19-125">You've created an Azure key vault and stored two secrets in it:</span></span>

* <span data-ttu-id="edb19-126">`$ACR_NAME-pull-usr`: Die Dienstprinzipal-ID für die Verwendung als **Benutzername** für die Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="edb19-126">`$ACR_NAME-pull-usr`: The service principal ID, for use as the container registry **username**.</span></span>
* <span data-ttu-id="edb19-127">`$ACR_NAME-pull-pwd`: Das Kennwort des Dienstprinzipals für die Verwendung als **Kennwort** für die Containerregistrierung.</span><span class="sxs-lookup"><span data-stu-id="edb19-127">`$ACR_NAME-pull-pwd`: The service principal password, for use as the container registry **password**.</span></span>

<span data-ttu-id="edb19-128">Sie können nun anhand des Namens auf diese Geheimnisse verweisen, wenn Sie oder Ihre Anwendungen und Dienste Images per Pull aus der Registrierung abrufen.</span><span class="sxs-lookup"><span data-stu-id="edb19-128">You can now reference these secrets by name when you or your applications and services pull images from the registry.</span></span>

### <a name="deploy-a-container-with-azure-cli"></a><span data-ttu-id="edb19-129">Bereitstellen eines Containers mit Azure CLI</span><span class="sxs-lookup"><span data-stu-id="edb19-129">Deploy a container with Azure CLI</span></span>

<span data-ttu-id="edb19-130">Jetzt, da die Anmeldeinformationen des Dienstprinzipals in Azure Key Vault gespeichert sind, können Ihre Anwendungen und Dienste diese verwenden, um auf Ihre private Registrierung zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="edb19-130">Now that the service principal credentials are stored in Azure Key Vault, your applications and services can use them to access your private registry.</span></span>

<span data-ttu-id="edb19-131">Führen Sie den folgenden `az container create`-Befehl aus, um eine Containerinstanz bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="edb19-131">Execute the following `az container create` command to deploy a container instance.</span></span> <span data-ttu-id="edb19-132">Der Befehl verwendet die in Azure Key Vault gespeicherten Anmeldeinformationen des Dienstprinzipals, um sich bei Ihrer Containerregistrierung zu authentifizieren.</span><span class="sxs-lookup"><span data-stu-id="edb19-132">The command uses the service principal's credentials stored in Azure Key Vault to authenticate to your container registry.</span></span>

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name acr-build \
    --image $ACR_NAME.azurecr.io/helloacrbuild:v1 \
    --registry-login-server $ACR_NAME.azurecr.io \
    --ip-address Public \
    --registry-username $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --query value -o tsv) \
    --registry-password $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --query value -o tsv)
```

<span data-ttu-id="edb19-133">Rufen Sie die IP-Adresse der Azure-Containerinstanz ab.</span><span class="sxs-lookup"><span data-stu-id="edb19-133">Get the IP address of the Azure container instance.</span></span>

```azurecli
az container show --resource-group myResourceGroup --name acr-build --query ipAddress.ip --output table
```

<span data-ttu-id="edb19-134">Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers.</span><span class="sxs-lookup"><span data-stu-id="edb19-134">Open up a browser and navigate to the IP address of the container.</span></span> <span data-ttu-id="edb19-135">Wenn alles ordnungsgemäß konfiguriert wurde, sollten jetzt die folgenden Ergebnisse angezeigt werden:</span><span class="sxs-lookup"><span data-stu-id="edb19-135">If everything has been configured correctly, you should see the following results:</span></span>

![Beispiel-Web-App mit dem Text „Hello World“](../media/hello.png)

## <a name="summary"></a><span data-ttu-id="edb19-137">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="edb19-137">Summary</span></span>

<span data-ttu-id="edb19-138">In dieser Einheit haben Sie die Azure Container Registry-Anmeldeinformationen in Azure Key Vault gespeichert.</span><span class="sxs-lookup"><span data-stu-id="edb19-138">In this unit, the Azure Container Registry credentials were stored in Azure Key Vault.</span></span> <span data-ttu-id="edb19-139">Anschließend haben Sie über Azure CLI ein Containerimage in Azure Container Instances bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="edb19-139">A container image was then deployed to Azure Container Instances using the Azure CLI.</span></span> <span data-ttu-id="edb19-140">In der nächsten Einheit verwenden Sie die Georeplikation von Azure Container Registry, um das Containerimage in mehrere Azure-Rechenzentren zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="edb19-140">In the next unit, you will use Azure Container Registry geo-replication to copy the container image to multiple Azure datacenters.</span></span>
