<span data-ttu-id="9c674-101">Mit Azure Container Registry Build können Sie ohne lokale Docker-Tools Containerimages in der Cloud erstellen.</span><span class="sxs-lookup"><span data-stu-id="9c674-101">With Azure Container Registry Build, container images can be built in the cloud, without the need for local Docker tooling.</span></span> <span data-ttu-id="9c674-102">Container Registry Build ermöglicht auch die Integration von DevOps-Prozessen mit automatischer Erstellung nach dem Committen von Quellcode.</span><span class="sxs-lookup"><span data-stu-id="9c674-102">Container Registry Build also allows for DevOps process integration with automated build on source code commit.</span></span>

<span data-ttu-id="9c674-103">In dieser Einheit automatisieren Sie die Erstellung eines Containerimages mit Azure Container Registry Build.</span><span class="sxs-lookup"><span data-stu-id="9c674-103">In this unit, you automate the creation of a container image using Azure Container Registry Build.</span></span>

## <a name="create-a-container-image-with-build"></a><span data-ttu-id="9c674-104">Erstellen eines Containerimages mit Build</span><span class="sxs-lookup"><span data-stu-id="9c674-104">Create a container image with Build</span></span>

<span data-ttu-id="9c674-105">Bei Azure Container Registry Build wird für das Bereitstellen von Buildanweisungen eine Dockerfile-Standarddatei verwendet.</span><span class="sxs-lookup"><span data-stu-id="9c674-105">When using Azure Container Registry Build, a standard Dockerfile is used to provide build instructions.</span></span> <span data-ttu-id="9c674-106">Alle Dockerfile-Dateien, die Sie derzeit in Ihrer Umgebung verwenden, einschließlich mehrstufiger Builds, funktionieren mit Azure Container Registry Build.</span><span class="sxs-lookup"><span data-stu-id="9c674-106">Any Dockerfile currently used in your environment, including multistaged builds, works with Azure Container Registry Build.</span></span>

<span data-ttu-id="9c674-107">Erstellen Sie eine Datei mit dem Namen `Dockerfile`, und öffnen Sie diese in einem Text-Editor Ihrer Wahl.</span><span class="sxs-lookup"><span data-stu-id="9c674-107">Create a file named `Dockerfile` and open it with any text editor.</span></span>

```bash
code Dockerfile
```

<span data-ttu-id="9c674-108">Kopieren Sie den folgenden Inhalt in die Datei, speichern Sie sie, und beenden Sie den Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="9c674-108">Copy in the following contents, save the file, and exit the text editor.</span></span> <span data-ttu-id="9c674-109">Die Dockerfile-Datei fügt dem Image `node:9-alpine` eine Node.js-Anwendung hinzu und konfiguriert den Container so, dass die Anwendung an Port 80 zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="9c674-109">This Dockerfile adds a Node.js application to the `node:9-alpine` image and configures the container to server the application on port 80.</span></span>

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

<span data-ttu-id="9c674-110">Führen Sie den folgenden Befehl aus, um das Containerimage aus der Dockerfile-Datei zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="9c674-110">Run the following command to build the container image from the Dockerfile.</span></span>

```azurecli
az acr build --registry <acrName> --image helloacrbuild:v1 .
```

<span data-ttu-id="9c674-111">Während dieses Vorgangs können Sie sehen, wie das Image erstellt und mithilfe von Push an Ihre Containerregistrierung übertragen wird.</span><span class="sxs-lookup"><span data-stu-id="9c674-111">As this operation runs, you will see the image being built and pushed to your container registry.</span></span>

## <a name="verify-the-image"></a><span data-ttu-id="9c674-112">Überprüfen des Images</span><span class="sxs-lookup"><span data-stu-id="9c674-112">Verify the image</span></span>

<span data-ttu-id="9c674-113">Führen Sie nach Abschluss des Buildvorgangs den folgenden Befehl aus, um zu überprüfen, ob das Image erstellt und in der Registrierung gespeichert wurde.</span><span class="sxs-lookup"><span data-stu-id="9c674-113">When the build operation has completed, run the following command to verify that the image has been created and stored in the registry.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="9c674-114">Die Ausgabe sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="9c674-114">The output should look similar to the following:</span></span>

```console
Result
-------------
helloacrbuild
```

<span data-ttu-id="9c674-115">Das Image `helloacrbuild` kann jetzt verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9c674-115">The `helloacrbuild` image is now ready to be used.</span></span>

## <a name="summary"></a><span data-ttu-id="9c674-116">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="9c674-116">Summary</span></span>

<span data-ttu-id="9c674-117">In dieser Einheit wurde mit Azure Container Registry Build die Erstellung eines Containerimages automatisiert.</span><span class="sxs-lookup"><span data-stu-id="9c674-117">In this unit, Azure Container Registry Build was used to automate the creation of a container image.</span></span> <span data-ttu-id="9c674-118">Dieses Image wurde dann in Azure Container Registry gespeichert.</span><span class="sxs-lookup"><span data-stu-id="9c674-118">This image was then stored in the Azure container registry.</span></span> <span data-ttu-id="9c674-119">In der nächsten Einheit stellen Sie eine Instanz des neuen Containerimages in Azure Container Instances bereit.</span><span class="sxs-lookup"><span data-stu-id="9c674-119">In the next unit, you will deploy an instance of the new container image to Azure Container Instances.</span></span>