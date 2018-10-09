<span data-ttu-id="785d5-101">Standardmäßig ist Azure Container Instances zustandslos.</span><span class="sxs-lookup"><span data-stu-id="785d5-101">By default, Azure Container Instances is stateless.</span></span> <span data-ttu-id="785d5-102">Wenn der Container abstürzt oder beendet wird, gehen alle Zustände verloren.</span><span class="sxs-lookup"><span data-stu-id="785d5-102">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="785d5-103">Um den Zustand nach Ablauf der Lebensdauer des Containers beizubehalten, müssen Sie ein Volume aus einem externen Speicher bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="785d5-103">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span>

<span data-ttu-id="785d5-104">In dieser Einheit stellen Sie eine Azure-Dateifreigabe in einer Azure-Containerinstanz zum Speichern und Abrufen von Daten bereit.</span><span class="sxs-lookup"><span data-stu-id="785d5-104">Here, you will mount an Azure file share to an Azure container instance for data storage and retrieval.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="785d5-105">Erstellen einer Azure-Dateifreigabe</span><span class="sxs-lookup"><span data-stu-id="785d5-105">Create an Azure file share</span></span>

<span data-ttu-id="785d5-106">Führen Sie das folgende Skript aus, um ein Speicherkonto zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="785d5-106">Run the following script to create a storage account.</span></span> <span data-ttu-id="785d5-107">Der Name des Speicherkontos muss global eindeutig sein, daher fügt das Skript der Basiszeichenfolge einen Zufallswert hinzu:</span><span class="sxs-lookup"><span data-stu-id="785d5-107">The storage account name must be globally unique, so the script adds a random value to the base string:</span></span>

```azurecli
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM

az storage account create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --sku Standard_LRS \
    --location eastus
```

<span data-ttu-id="785d5-108">Führen Sie den folgenden Befehl aus, um die Verbindungszeichenfolge für das Speicherkonto in einer Umgebungsvariablen mit dem Namen *AZURE_STORAGE_CONNECTION_STRING* zu platzieren.</span><span class="sxs-lookup"><span data-stu-id="785d5-108">Run the following command to place the storage account connection string into an environment variable named *AZURE_STORAGE_CONNECTION_STRING*.</span></span> <span data-ttu-id="785d5-109">Diese Umgebungsvariable kann von der Azure CLI gelesen und für speicherbezogene Vorgänge verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="785d5-109">This environment variable is understood by the Azure CLI and can be used in storage-related operations:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=$(az storage account show-connection-string --resource-group <rgn>[sandbox resource group name]</rgn> --name $ACI_PERS_STORAGE_ACCOUNT_NAME --output tsv)
```

<span data-ttu-id="785d5-110">Erstellen Sie eine Dateifreigabe im Speicherkonto, indem Sie den `az storage share create`-Befehl ausführen.</span><span class="sxs-lookup"><span data-stu-id="785d5-110">Create a file share in the storage account by running the `az storage share create` command.</span></span> <span data-ttu-id="785d5-111">Im folgenden Beispiel wird eine Freigabe mit dem Namen *aci-share-demo* erstellt:</span><span class="sxs-lookup"><span data-stu-id="785d5-111">The following example creates a share with the name *aci-share-demo*:</span></span>

```azurecli
az storage share create --name aci-share-demo
```

## <a name="get-storage-credentials"></a><span data-ttu-id="785d5-112">Abrufen der Anmeldeinformationen für das Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="785d5-112">Get storage credentials</span></span>

<span data-ttu-id="785d5-113">Um eine Azure-Dateifreigabe als Volume in Azure Container Instances bereitzustellen, benötigen Sie drei Werte: den Namen des Speicherkontos, den Freigabenamen und den Zugriffsschlüssel für das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="785d5-113">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage account access key.</span></span>

<span data-ttu-id="785d5-114">Wenn Sie das oben angegebene Skript verwendet haben, wurde der Name des Speicherkontos mit einem zufälligen Wert am Ende erstellt.</span><span class="sxs-lookup"><span data-stu-id="785d5-114">If you used the script above, the storage account name was created with a random value at the end.</span></span> <span data-ttu-id="785d5-115">Um die endgültige Zeichenfolge (einschließlich des zufälligen Teils) abzufragen, verwenden Sie die folgenden Befehle:</span><span class="sxs-lookup"><span data-stu-id="785d5-115">To query the final string (including the random portion), use the following commands:</span></span>

```azurecli
STORAGE_ACCOUNT=$(az storage account list --resource-group <rgn>[sandbox resource group name]</rgn> --query "[?contains(name,'$ACI_PERS_STORAGE_ACCOUNT_NAME')].[name]" --output tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="785d5-116">Der Freigabename ist bereits bekannt (aci-share-demo), daher verbleibt nur der Speicherkontoschlüssel, der mit dem folgenden Befehl gesucht werden kann:</span><span class="sxs-lookup"><span data-stu-id="785d5-116">The share name is already known (aci-share-demo), so all that remains is the storage account key, which can be found using the following command:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list --resource-group <rgn>[sandbox resource group name]</rgn> --account-name $STORAGE_ACCOUNT --query "[0].value" --output tsv)
echo $STORAGE_KEY
```

## <a name="deploy-container-and-mount-volume"></a><span data-ttu-id="785d5-117">Bereitstellen des Containers und des Volumes</span><span class="sxs-lookup"><span data-stu-id="785d5-117">Deploy container and mount volume</span></span>

<span data-ttu-id="785d5-118">Um eine Azure-Dateifreigabe als Volume in einem Container bereitzustellen, geben Sie die Freigabe und den Bereitstellungspunkt des Volumes bei der Erstellung des Containers an:</span><span class="sxs-lookup"><span data-stu-id="785d5-118">To mount an Azure file share as a volume in a container, specify the share and volume mount point when you create the container:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-files \
    --image microsoft/aci-hellofiles \
    --location eastus \
    --ports 80 \
    --ip-address Public \
    --azure-file-volume-account-name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --azure-file-volume-account-key $STORAGE_KEY \
    --azure-file-volume-share-name aci-share-demo \
    --azure-file-volume-mount-path /aci/logs/
```

<span data-ttu-id="785d5-119">Nachdem der Container erstellt wurde, rufen Sie die öffentliche IP-Adresse ab:</span><span class="sxs-lookup"><span data-stu-id="785d5-119">Once the container has been created, get the public IP address:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-files \
    --query ipAddress.ip \
    --output tsv
```

<span data-ttu-id="785d5-120">Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers.</span><span class="sxs-lookup"><span data-stu-id="785d5-120">Open a browser and navigate to the container's IP address.</span></span> <span data-ttu-id="785d5-121">Es wird ein einfaches Formular angezeigt.</span><span class="sxs-lookup"><span data-stu-id="785d5-121">You will be presented with a simple form.</span></span> <span data-ttu-id="785d5-122">Geben Sie Text ein, und klicken Sie auf **Senden**.</span><span class="sxs-lookup"><span data-stu-id="785d5-122">Enter some text and click **Submit**.</span></span> <span data-ttu-id="785d5-123">Dadurch wird eine Datei in der Azure-Dateifreigabe mit dem eingegebenen Text erstellt.</span><span class="sxs-lookup"><span data-stu-id="785d5-123">This action will create a file in the Azure Files share containing the entered text.</span></span>

![Beispiel für eine Azure Container Instances-Dateifreigabe](../media/5-files-ui.png)

<span data-ttu-id="785d5-125">Zur Überprüfung können Sie zur Dateifreigabe im Azure-Portal navigieren und die Datei herunterladen.</span><span class="sxs-lookup"><span data-stu-id="785d5-125">To validate, you can navigate to the file share in the Azure portal and download the file.</span></span>

<span data-ttu-id="785d5-126">Abrufen des Dateinamens</span><span class="sxs-lookup"><span data-stu-id="785d5-126">Get the filename</span></span>

```azurecli
az storage file list -s aci-share-demo -o table
```

<span data-ttu-id="785d5-127">Laden Sie die Datei in die Cloud Shell herunter.</span><span class="sxs-lookup"><span data-stu-id="785d5-127">Download the file to the cloud shell.</span></span> <span data-ttu-id="785d5-128">Stellen Sie sicher, dass Sie die Datei `<filename>` unten ersetzen.</span><span class="sxs-lookup"><span data-stu-id="785d5-128">Make sure to replace the `<filename>` below.</span></span>

```azurecli
az storage file download -s aci-share-demo -p <filename>
```

<span data-ttu-id="785d5-129">Zeigen Sie den Inhalt der Datei an.</span><span class="sxs-lookup"><span data-stu-id="785d5-129">Show the contents of the file.</span></span>

```azurecli
cat <filename>
```

<span data-ttu-id="785d5-130">Wenn es sich bei den Inhalten, die in der Azure-Dateifreigabe gespeichert sind, um relevante Dateien und Daten handelt, kann diese Freigabe in einer neuen Containerinstanz erneut bereitgestellt werden, um zustandsbehaftete Daten verfügbar zu machen.</span><span class="sxs-lookup"><span data-stu-id="785d5-130">If the files and data stored in the Azure Files share were of any value, this share could be remounted on a new container instance to provide stateful data.</span></span>