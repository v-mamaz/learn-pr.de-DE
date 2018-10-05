<span data-ttu-id="5e517-101">Stellen Sie sich vor, Ihr Unternehmen verwendet Containerimages für die Verwaltung von Computeworkloads.</span><span class="sxs-lookup"><span data-stu-id="5e517-101">Suppose your company makes use of container images to manage compute workloads.</span></span> <span data-ttu-id="5e517-102">Für das Erstellen von Containerimages werden die lokalen Docker-Tools verwendet.</span><span class="sxs-lookup"><span data-stu-id="5e517-102">You use the local Docker tooling to build your container images.</span></span>

<span data-ttu-id="5e517-103">Sie können Azure Container Registry Tasks zum Erstellen dieser Container verwenden.</span><span class="sxs-lookup"><span data-stu-id="5e517-103">You can now use Azure Container Registry Tasks to build these containers.</span></span> <span data-ttu-id="5e517-104">Container Registry Tasks ermöglicht auch die Integration von DevOps-Prozessen mit automatischer Builderstellung nach dem Committen von Quellcode.</span><span class="sxs-lookup"><span data-stu-id="5e517-104">Container Registry Tasks also allows for DevOps process integration with automated build on source code commit.</span></span>

<span data-ttu-id="5e517-105">Automatisieren Sie die Erstellung eines Containerimages mit Azure Container Registry Tasks.</span><span class="sxs-lookup"><span data-stu-id="5e517-105">Let's automate the creation of a container image using Azure Container Registry Tasks.</span></span>

## <a name="create-a-container-image-with-azure-container-registry-tasks"></a><span data-ttu-id="5e517-106">Erstellen eines Containerimages mit Azure Container Registry Tasks</span><span class="sxs-lookup"><span data-stu-id="5e517-106">Create a container image with Azure Container Registry Tasks</span></span>

<span data-ttu-id="5e517-107">Eine Dockerfile-Standarddatei stellt Buildanweisungen bereit.</span><span class="sxs-lookup"><span data-stu-id="5e517-107">A standard Dockerfile to provides build instructions.</span></span> <span data-ttu-id="5e517-108">Mit Azure Container Registry Tasks können Sie alle Dockerfile-Dateien wiederverwenden, die Sie derzeit in Ihrer Umgebung verwenden, einschließlich mehrstufiger Builds.</span><span class="sxs-lookup"><span data-stu-id="5e517-108">Azure Container Registry Tasks allows you to reuse any Dockerfile currently in your environment, including multi-staged builds.</span></span>

<span data-ttu-id="5e517-109">In diesem Beispiel wird eine neue Dockerfile-Datei verwendet.</span><span class="sxs-lookup"><span data-stu-id="5e517-109">We'll use a new Dockerfile for our example.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="5e517-110">Hierzu wird im ersten Schritt eine neue Datei mit dem Namen `Dockerfile` erstellt.</span><span class="sxs-lookup"><span data-stu-id="5e517-110">The first step is to create a new file named `Dockerfile`.</span></span> <span data-ttu-id="5e517-111">Sie können einen beliebigen Text-Editor verwenden, um die Datei zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="5e517-111">You can use any text editor to edit the file.</span></span> <span data-ttu-id="5e517-112">In diesem Beispiel verwenden wir den Cloud Shell-Editor.</span><span class="sxs-lookup"><span data-stu-id="5e517-112">We'll use Cloud Shell Editor for this example.</span></span> <span data-ttu-id="5e517-113">Geben Sie den folgenden Befehl im Cloud Shell-Fenster ein, um den Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="5e517-113">Enter the following command into the Cloud Shell window to open the editor.</span></span>

```bash
code
```

<span data-ttu-id="5e517-114">Kopieren Sie den folgenden Inhalt in die neue Dockerfile-Datei.</span><span class="sxs-lookup"><span data-stu-id="5e517-114">Copy the following contents to your new Dockerfile.</span></span> <span data-ttu-id="5e517-115">Speichern Sie die Datei unbedingt.</span><span class="sxs-lookup"><span data-stu-id="5e517-115">Make sure to save the file.</span></span>

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

<span data-ttu-id="5e517-116">Speichern Sie mithilfe der Tastenkombination <kbd>STRG+S</kbd>.</span><span class="sxs-lookup"><span data-stu-id="5e517-116">Use the key combination <kbd>Ctrl+S</kbd> to save.</span></span> <span data-ttu-id="5e517-117">Nennen Sie die Datei nach Aufforderung „`Dockerfile`“.</span><span class="sxs-lookup"><span data-stu-id="5e517-117">Name the file `Dockerfile` when prompted.</span></span>

<span data-ttu-id="5e517-118">Durch diese Konfiguration wird dem `node:9-alpine`-Image eine Node.js-Anwendung hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="5e517-118">This configuration adds a Node.js application to the `node:9-alpine` image.</span></span> <span data-ttu-id="5e517-119">Anschließend wird der Container so konfiguriert, dass er die Anwendung über die Anweisung *EXPOSE* auf Port 80 bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="5e517-119">After that, it configures the container to serve the application on port 80 via the *EXPOSE* instruction.</span></span>

<span data-ttu-id="5e517-120">Führen Sie nun den Azure CLI-Befehl `az acr build` aus, um den Build des Containerimages aus der Dockerfile-Datei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="5e517-120">Now run the Azure CLI command `az acr build` to build the container image from the Dockerfile.</span></span>

```azurecli
az acr build --registry <acrName> --image helloacrtasks:v1 .
```

<span data-ttu-id="5e517-121">Während Sie den Befehl ausführen, können Sie sehen, wie der Build für das Image erstellt und mithilfe von Push in Ihre Containerregistrierung übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="5e517-121">You'll see the image being built and pushed to your Container Registry as you run the command.</span></span>

## <a name="verify-the-image"></a><span data-ttu-id="5e517-122">Überprüfen des Images</span><span class="sxs-lookup"><span data-stu-id="5e517-122">Verify the image</span></span>

<span data-ttu-id="5e517-123">Führen Sie den folgenden Befehl aus, um zu überprüfen, ob das Image erstellt und in der Registrierung gespeichert wurde.</span><span class="sxs-lookup"><span data-stu-id="5e517-123">Run the following command to verify that the image has been created and stored in the registry.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="5e517-124">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="5e517-124">The output should look similar to the following:</span></span>

```console
Result
-------------
helloacrtasks
```

<span data-ttu-id="5e517-125">Das Image `helloacrtasks` kann jetzt verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="5e517-125">The `helloacrtasks` image is now ready to be used.</span></span>
