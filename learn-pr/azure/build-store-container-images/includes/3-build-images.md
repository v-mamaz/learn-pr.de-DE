<span data-ttu-id="642df-101">Ihr Unternehmen verwendet Containerimages für die Verwaltung von Computeworkloads im Unternehmen.</span><span class="sxs-lookup"><span data-stu-id="642df-101">Your company makes use of container images to manage compute workloads in the company.</span></span> <span data-ttu-id="642df-102">Für das Erstellen von Containerimages werden lokale Docker-Tools verwendet.</span><span class="sxs-lookup"><span data-stu-id="642df-102">You use local Docker tooling to build your container images.</span></span> <span data-ttu-id="642df-103">Wenn Sie sich für Azure Container Registry entscheiden, können Sie nun Containerimages in der Cloud erstellen.</span><span class="sxs-lookup"><span data-stu-id="642df-103">The decision to make use of an Azure Container Registry now allows you to build container images in the cloud.</span></span> 

<span data-ttu-id="642df-104">Sie können Azure Container Registry Build zum Erstellen dieser Container verwenden.</span><span class="sxs-lookup"><span data-stu-id="642df-104">You can now use Azure Container Registry Build to build these containers.</span></span> <span data-ttu-id="642df-105">Container Registry Build ermöglicht auch die Integration von DevOps-Prozessen mit automatischer Builderstellung nach dem Committen von Quellcode.</span><span class="sxs-lookup"><span data-stu-id="642df-105">Container Registry Build also allows for DevOps process integration with automated build on source code commit.</span></span>

<span data-ttu-id="642df-106">Automatisieren Sie die Erstellung eines Containerimages mit Azure Container Registry Build.</span><span class="sxs-lookup"><span data-stu-id="642df-106">Let's automate the creation of a container image using Azure Container Registry Build.</span></span>

## <a name="create-a-container-image-with-azure-container-registry-build"></a><span data-ttu-id="642df-107">Erstellen eines Containerimage mit Azure Container Registry Build</span><span class="sxs-lookup"><span data-stu-id="642df-107">Create a container image with Azure Container Registry Build</span></span>

<span data-ttu-id="642df-108">Verwenden Sie eine standardmäßige Dockerfile-Datei, um Buildanweisungen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="642df-108">You use a standard Dockerfile to provide build instructions.</span></span> <span data-ttu-id="642df-109">Mit Azure Container Registry Build können Sie alle Dockerfile-Dateien wiederverwenden, die Sie derzeit in Ihrer Umgebung verwenden, einschließlich mehrstufiger Builds.</span><span class="sxs-lookup"><span data-stu-id="642df-109">Azure Container Registry Build allows you to reuse any Dockerfile currently in your environment, including multi-staged builds.</span></span>

<span data-ttu-id="642df-110">In diesem Beispiel verwenden wir eine neue Dockerfile-Datei.</span><span class="sxs-lookup"><span data-stu-id="642df-110">We'll use new Dockerfile for our example.</span></span> 

<span data-ttu-id="642df-111">Hierzu wird im ersten Schritt eine neue Datei mit dem Namen `Dockerfile` erstellt.</span><span class="sxs-lookup"><span data-stu-id="642df-111">The first step is to create a new file named `Dockerfile`.</span></span> <span data-ttu-id="642df-112">Sie können einen beliebigen Text-Editor verwenden, um die Datei zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="642df-112">You can use any text editor to edit the file.</span></span> <span data-ttu-id="642df-113">In diesem Beispiel verwenden wir Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="642df-113">We'll use Visual Studio Code for this example.</span></span>

```bash
code Dockerfile
```

<span data-ttu-id="642df-114">Kopieren Sie den folgenden Inhalt in die neue Dockerfile-Datei.</span><span class="sxs-lookup"><span data-stu-id="642df-114">Copy the following contents to your new Dockerfile.</span></span> <span data-ttu-id="642df-115">Speichern Sie die Datei unbedingt.</span><span class="sxs-lookup"><span data-stu-id="642df-115">Make sure to safe the file.</span></span> 

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

<span data-ttu-id="642df-116">Durch diese Konfiguration wird dem `node:9-alpine`-Image eine Node.js-Anwendung hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="642df-116">This configuration adds a Node.js application to the `node:9-alpine` image.</span></span> <span data-ttu-id="642df-117">Anschließend wird der Container so konfiguriert, dass er die Anwendung über die Anweisung *EXPOSE* auf Port 80 bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="642df-117">Then configures the container to serve the application on port 80 via the *EXPOSE* instruction.</span></span>

<span data-ttu-id="642df-118">Führen Sie nun den Azure CLI-Befehl `az acr build` aus, um den Build des Containerimages aus der Dockerfile-Datei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="642df-118">Now run the Azure CLI command, `az acr build`, to build the container image from the Dockerfile.</span></span>

```azurecli
az acr build --registry <acrName> --image helloacrbuild:v1 .
```

<span data-ttu-id="642df-119">Während Sie den Befehl ausführen, können Sie sehen, wie der Build für das Image erstellt und mithilfe von Push in Ihre Containerregistrierung übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="642df-119">You'll see the image being built and pushed to your Container Registry as you run the command.</span></span>

## <a name="verify-the-image"></a><span data-ttu-id="642df-120">Überprüfen des Images</span><span class="sxs-lookup"><span data-stu-id="642df-120">Verify the image</span></span>

<span data-ttu-id="642df-121">Führen Sie den folgenden Befehl aus, um zu überprüfen, ob das Image erstellt und in der Registrierung gespeichert wurde.</span><span class="sxs-lookup"><span data-stu-id="642df-121">Run the following command to verify that the image has been created and stored in the registry.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="642df-122">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="642df-122">The output should look similar to the following:</span></span>

```console
Result
-------------
helloacrbuild
```

<span data-ttu-id="642df-123">Das Image `helloacrbuild` kann jetzt verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="642df-123">The `helloacrbuild` image is now ready to be used.</span></span>
