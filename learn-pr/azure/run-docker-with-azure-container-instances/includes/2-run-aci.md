<span data-ttu-id="b6d15-101">Hier erstellen Sie einen Container in Azure und machen ihn mit einem vollqualifizierten Domänennamen (FQDN) über das Internet verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b6d15-101">Here, you create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="why-use-azure-container-instances"></a><span data-ttu-id="b6d15-102">Was spricht für die Verwendung von Azure Container Instances?</span><span class="sxs-lookup"><span data-stu-id="b6d15-102">Why use Azure Container Instances?</span></span>

<span data-ttu-id="b6d15-103">Azure Container Instances ist hilfreich für Szenarien mit isolierten Containern. Hierzu zählen unter anderem einfache Anwendungen, Aufgabenautomatisierung und Buildaufträge.</span><span class="sxs-lookup"><span data-stu-id="b6d15-103">Azure Container Instances is useful for scenarios that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="b6d15-104">Azure Container Instances bietet folgende Vorteile:</span><span class="sxs-lookup"><span data-stu-id="b6d15-104">Azure Container Instances offers the following benefits:</span></span>

- <span data-ttu-id="b6d15-105">**Schneller Start:** Containern können in Sekundenschnelle gestartet werden.</span><span class="sxs-lookup"><span data-stu-id="b6d15-105">**Fast startup**: Launch containers in seconds.</span></span>
- <span data-ttu-id="b6d15-106">**Sekundengenaue Abrechnung:** Kosten fallen nur während der Containerausführung an.</span><span class="sxs-lookup"><span data-stu-id="b6d15-106">**Per second billing**: Incur costs only while the container is running.</span></span>
- <span data-ttu-id="b6d15-107">**Sicherheit auf Hypervisor-Ebene:** Isolieren Sie Ihre Anwendung so umfassend wie auf einem virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="b6d15-107">**Hypervisor-level security**: Isolate your application as completely as it would be in a VM.</span></span>
- <span data-ttu-id="b6d15-108">**Benutzerdefinierte Größen:** Geben Sie exakte Werte für CPU-Kerne und Arbeitsspeicher an.</span><span class="sxs-lookup"><span data-stu-id="b6d15-108">**Custom sizes**: Specify exact values for CPU cores and memory.</span></span>
- <span data-ttu-id="b6d15-109">**Persistenter Speicher:** Binden Sie Azure Files-Freigaben direkt in einen Container ein, um den Zustand abzurufen und zu speichern.</span><span class="sxs-lookup"><span data-stu-id="b6d15-109">**Persistent storage**: Mount Azure Files shares directly to a container to retrieve and persist state.</span></span>
- <span data-ttu-id="b6d15-110">**Linux und Windows:** Erstellen Sie Zeitpläne für Windows- und Linux-Container über die gleiche API.</span><span class="sxs-lookup"><span data-stu-id="b6d15-110">**Linux and Windows**: Schedule both Windows and Linux containers using the same API.</span></span>

<span data-ttu-id="b6d15-111">Für Szenarien, die eine umfassende Containerorchestrierung erfordern (etwa für die containerübergreifende Dienstermittlung, automatische Skalierung und für koordinierte Anwendungsupgrades), empfehlen wir Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="b6d15-111">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend Azure Kubernetes Service (AKS).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="b6d15-112">Erstellen eines Containers</span><span class="sxs-lookup"><span data-stu-id="b6d15-112">Create a container</span></span>

<span data-ttu-id="b6d15-113">Um einen Container zu erstellen, müssen Sie einen Namen, ein Docker-Image und eine Azure-Ressourcengruppe für den Befehl **az container create** angeben.</span><span class="sxs-lookup"><span data-stu-id="b6d15-113">You create a container by providing a name, a Docker image, and an Azure resource group to the **az container create** command.</span></span> <span data-ttu-id="b6d15-114">Durch Angeben einer DNS-Namensbezeichnung kann der Container optional auch für das Internet verfügbar gemacht werden.</span><span class="sxs-lookup"><span data-stu-id="b6d15-114">You can optionally expose the container to the Internet by specifying a DNS name label.</span></span> <span data-ttu-id="b6d15-115">In diesem Beispiel stellen Sie einen Container bereit, der eine kompakte Web-App hostet.</span><span class="sxs-lookup"><span data-stu-id="b6d15-115">In this example, you deploy a container that hosts a small web app.</span></span> <span data-ttu-id="b6d15-116">Außerdem können Sie den Standort des Images auswählen. Im Beispiel unten wird „USA, Osten“ verwendet, allerdings können Sie diese Angabe durch einen Ihnen am nächstgelegenen Standort aus der folgenden Liste ersetzen.</span><span class="sxs-lookup"><span data-stu-id="b6d15-116">You can also select the location to place the image - we're defaulting to "East US" below, but you can change it to a location close to you from the following list.</span></span>

<span data-ttu-id="b6d15-117"><!-- TODO: fix region list so it's not hardcoded here --> Mit der kostenlosen Sandbox können Sie in einem Teil der globalen Azure-Regionen Ressourcen erstellen.</span><span class="sxs-lookup"><span data-stu-id="b6d15-117"><!-- TODO: fix region list so it's not hardcoded here --> The free sandbox allows you to create resources in a subset of Azure's global regions.</span></span> <span data-ttu-id="b6d15-118">Wählen Sie eine Region aus der folgenden Liste aus, wenn Sie Ressourcen erstellen:</span><span class="sxs-lookup"><span data-stu-id="b6d15-118">Select a region from the following list when creating any resources:</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="b6d15-119">- USA, Westen 2 - USA, Mitte - USA, Osten - Europa, Westen - Asien, Südosten</span><span class="sxs-lookup"><span data-stu-id="b6d15-119">- westus2 - centralus - eastus - westeurope - southeastasia</span></span> :::column-end:::
:::row-end:::

<span data-ttu-id="b6d15-120">Führen Sie in Cloud Shell den folgenden Befehl aus, um eine Containerinstanz zu starten.</span><span class="sxs-lookup"><span data-stu-id="b6d15-120">Execute the following command in the Cloud Shell to start a container instance.</span></span> <span data-ttu-id="b6d15-121">Der Wert `--dns-name-label` muss innerhalb der Azure-Region, in der Sie die Instanz erstellen, eindeutig sein. Passen Sie `[dns-name]` also ggf. entsprechend an.</span><span class="sxs-lookup"><span data-stu-id="b6d15-121">The `--dns-name-label` value must be unique within the Azure region you create the instance, so you will need to replace `[dns-name]` with something unique.</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --image microsoft/aci-helloworld \
    --ports 80 \
    --dns-name-label [dns-name] \
    --location eastus
```

<span data-ttu-id="b6d15-122">Innerhalb weniger Sekunden erhalten Sie eine Antwort auf Ihre Anforderung.</span><span class="sxs-lookup"><span data-stu-id="b6d15-122">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="b6d15-123">Der Container befindet sich zunächst im Zustand **Wird erstellt...**, wird aber innerhalb weniger Sekunden gestartet.</span><span class="sxs-lookup"><span data-stu-id="b6d15-123">Initially, the container is in the **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="b6d15-124">Sie können den Status mit dem Befehl `az container show` überprüfen:</span><span class="sxs-lookup"><span data-stu-id="b6d15-124">You can check the status using the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
    --out table
```

<span data-ttu-id="b6d15-125">Wenn Sie den Befehl ausführen, werden der vollqualifizierte Domänenname (FQDN) des Containers und der Bereitstellungsstatus angezeigt:</span><span class="sxs-lookup"><span data-stu-id="b6d15-125">When you run the command, the container's fully qualified domain name (FQDN) and its provisioning state are displayed:</span></span>

```output
FQDN                                    ProvisioningState
--------------------------------------  -------------------
aci-demo.eastus.azurecontainer.io       Succeeded
```

<span data-ttu-id="b6d15-126">Wenn der Container den Status **Erfolgreich** erreicht, navigieren Sie in Ihrem Browser zu seinem FQDN, um den Status zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="b6d15-126">Once the container moves to the **Succeeded** state, navigate to its FQDN in your browser to verify success.</span></span>

<span data-ttu-id="b6d15-127">Hier haben Sie eine Azure-Containerinstanz erstellt, in der ein Webserver und eine Anwendung ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b6d15-127">Here, you created an Azure container instance to run a web server and application.</span></span> <span data-ttu-id="b6d15-128">Mithilfe des FQDN der Containerinstanz haben Sie außerdem auf die Anwendung zugegriffen.</span><span class="sxs-lookup"><span data-stu-id="b6d15-128">You also accessed this application using the FQDN of the container instance.</span></span>