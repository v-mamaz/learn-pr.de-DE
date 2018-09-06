<span data-ttu-id="e591a-101">Azure Container Instances erleichtert die Erstellung und Verwaltung von Docker-Containern in Azure, ohne dass Sie virtuelle Computer bereitstellen oder einen übergeordneten Dienst einführen müssen.</span><span class="sxs-lookup"><span data-stu-id="e591a-101">Azure Container Instances makes it easy to create and manage Docker containers in Azure, without having to provision virtual machines or adopt a higher-level service.</span></span> <span data-ttu-id="e591a-102">In dieser Einheit erstellen Sie einen Container in Azure und machen ihn mit einem vollqualifizierten Domänennamen (FQDN) über das Internet verfügbar.</span><span class="sxs-lookup"><span data-stu-id="e591a-102">In this unit, you create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="e591a-103">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="e591a-103">Create a resource group</span></span>

<span data-ttu-id="e591a-104">Wie alle Azure-Ressourcen müssen auch Azure-Containerinstanzen in einer Ressourcengruppe (einer logische Sammlung für die Bereitstellung und Verwaltung von Azure-Ressourcen) platziert werden.</span><span class="sxs-lookup"><span data-stu-id="e591a-104">Azure container instances, like all Azure resources, must be placed in a resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="e591a-105">Erstellen Sie mit dem Befehl `az group create` eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="e591a-105">Create a resource group with the `az group create` command.</span></span>

<span data-ttu-id="e591a-106">Im folgenden Beispiel wird eine Ressourcengruppe mit dem Namen *myResourceGroup* am Standort *eastus* erstellt.</span><span class="sxs-lookup"><span data-stu-id="e591a-106">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="creat-a-container"></a><span data-ttu-id="e591a-107">Erstellen eines Containers</span><span class="sxs-lookup"><span data-stu-id="e591a-107">Creat a container</span></span>

<span data-ttu-id="e591a-108">Zum Erstellen eines Containers müssen Sie einen Namen, ein Docker-Image und eine Azure-Ressourcengruppe für den Befehl „az container create“ angeben.</span><span class="sxs-lookup"><span data-stu-id="e591a-108">You can create a container by providing a name, a Docker image, and an Azure resource group to the az container create command.</span></span> <span data-ttu-id="e591a-109">Durch Angeben einer DNS-Namensbezeichnung kann der Container optional auch für das Internet verfügbar gemacht werden.</span><span class="sxs-lookup"><span data-stu-id="e591a-109">You can optionally expose the container to the internet by specifying a DNS name label.</span></span> <span data-ttu-id="e591a-110">In diesem Beispiel stellen Sie einen Container bereit, der eine kompakte Webanwendung hostet.</span><span class="sxs-lookup"><span data-stu-id="e591a-110">In this example, you deploy a container that hosts a small web app.</span></span>

<span data-ttu-id="e591a-111">Führen Sie den folgenden Befehl aus, um eine Containerinstanz zu starten.</span><span class="sxs-lookup"><span data-stu-id="e591a-111">Execute the following command to start a container instance.</span></span> <span data-ttu-id="e591a-112">Der *--dns-name-label*-Wert muss innerhalb der Azure-Region, in der Sie die Instanz erstellen, eindeutig sein. Passen Sie den Wert also ggf. entsprechend an.</span><span class="sxs-lookup"><span data-stu-id="e591a-112">The *--dns-name-label* value must be unique within the Azure region you create the instance, so you might need to modify this value to ensure uniqueness.</span></span>

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image microsoft/aci-helloworld \
    --ports 80 \
    --dns-name-label aci-demo
```

<span data-ttu-id="e591a-113">Innerhalb weniger Sekunden erhalten Sie eine Antwort auf Ihre Anforderung.</span><span class="sxs-lookup"><span data-stu-id="e591a-113">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="e591a-114">Der Container befindet sich zunächst im Zustand **Wird erstellt...**, wird aber innerhalb weniger Sekunden gestartet.</span><span class="sxs-lookup"><span data-stu-id="e591a-114">Initially, the container is in the **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="e591a-115">Sie können den Status mit dem Befehl `az container show` überprüfen:</span><span class="sxs-lookup"><span data-stu-id="e591a-115">You can check the status using the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group myResourceGroup \
    --name mycontainer \
    --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
    --out table
```

<span data-ttu-id="e591a-116">Wenn Sie den Befehl ausführen, werden der vollqualifizierte Domänenname (FQDN) des Containers und der Bereitstellungsstatus angezeigt:</span><span class="sxs-lookup"><span data-stu-id="e591a-116">When you run the command, the container's fully qualified domain name (FQDN) and its provisioning state are displayed:</span></span>

```bash
FQDN                                    ProvisioningState
--------------------------------------  -------------------
aci-demo.eastus.azurecontainer.io       Succeeded
```

<span data-ttu-id="e591a-117">Rufen Sie in Ihrem Browser den FQDN des Containers auf, sobald sich dieser im Zustand „Erfolgreich“ befindet:</span><span class="sxs-lookup"><span data-stu-id="e591a-117">Once the container moves to the Succeeded state, navigate to its FQDN in your browser:</span></span>

![Screenshot eines Browsers mit ausgeführter Anwendung in einer Azure-Containerinstanz](../media-draft/aci-app-browser.png)

## <a name="summary"></a><span data-ttu-id="e591a-119">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="e591a-119">Summary</span></span>

<span data-ttu-id="e591a-120">In dieser Einheit haben Sie eine Azure-Containerinstanz erstellt, in der ein Webserver und eine Anwendung ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="e591a-120">In this unit, you created an Azure Container Instance that is running a web server and application.</span></span> <span data-ttu-id="e591a-121">Mithilfe des FQDN der Containerinstanz haben Sie außerdem auf die Anwendung zugegriffen.</span><span class="sxs-lookup"><span data-stu-id="e591a-121">You also accessed this application using the FQDN of the container instance.</span></span>

<span data-ttu-id="e591a-122">In der nächsten Einheit konfigurieren Sie Neustartrichtlinien für Containerinstanzen.</span><span class="sxs-lookup"><span data-stu-id="e591a-122">In the next unit, you will configure container instance restart policies.</span></span>

