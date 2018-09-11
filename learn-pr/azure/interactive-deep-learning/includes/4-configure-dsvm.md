## <a name="introduction-to-jupyter-for-more-interactive-deep-learning"></a><span data-ttu-id="749de-101">Einführung in Jupyter für interaktiveres Deep Learning</span><span class="sxs-lookup"><span data-stu-id="749de-101">Introduction to Jupyter for more interactive deep learning</span></span> 

<span data-ttu-id="749de-102">Jupyter Notebook ist eine Open-Source-Webanwendung, mit der Sie Dokumente mit Livecode, Gleichungen, Visualisierungen und narrativem Text erstellen und teilen können.</span><span class="sxs-lookup"><span data-stu-id="749de-102">Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations, and narrative text.</span></span> <span data-ttu-id="749de-103">Zu den Anwendungsbereichen zählen etwa Datenbereinigung und -transformation, numerische Simulationen, Statistikmodelle, Datenvisualisierungen, Machine Learning und vieles mehr.</span><span class="sxs-lookup"><span data-stu-id="749de-103">Uses include: data cleaning and transformation, numerical simulation, statistical modeling, data visualization, machine learning, and much more.</span></span>

## <a name="serving-jupyter-notebooks-with-nvidia-docker-on-an-azure-dsvm"></a><span data-ttu-id="749de-104">Bereitstellen von Jupyter-Notebooks mit NVIDIA Docker in einer Azure-DSVM-Instanz</span><span class="sxs-lookup"><span data-stu-id="749de-104">Serving Jupyter Notebooks with Nvidia Docker on an Azure DSVM</span></span>

### <a name="step-1-create-a-linux-dsvm"></a><span data-ttu-id="749de-105">Schritt 1: Erstellen einer Linux-DSVM-Instanz</span><span class="sxs-lookup"><span data-stu-id="749de-105">Step 1 Create a Linux DSVM</span></span>

<span data-ttu-id="749de-106">Verwenden von Aufrufcode über die Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="749de-106">Use call code from the Azure CLI</span></span>

```
code .
```

<span data-ttu-id="749de-107">Ausfüllen und Speichern des folgenden Bereitstellungsschemas als „parameter_file.json“</span><span class="sxs-lookup"><span data-stu-id="749de-107">Fill in the following deployment schema and save it as parameter_file.json</span></span>

``` 
{ 
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "adminUsername": { "value" : "YOURUSERNAME FOR NEW DSVM"},
     "adminPassword": { "value" : "PASSWORD FOR NEW DSVM"},
     "vmName": { "value" : "HOSTNAME OF DSVM"},
     "vmSize": { "value" : "VM SIZE For eg: Standard_DS2_v2"},
  }
}
```

<span data-ttu-id="749de-108">Eine Liste mit verfügbaren VM-Größen finden Sie [hier](https://azure.microsoft.com/en-us/global-infrastructure/services/?WT.mc_id=blog-learning-abornst).</span><span class="sxs-lookup"><span data-stu-id="749de-108">A list of available vm sizes can be found here [Ubuntu DSVM ARM template](https://azure.microsoft.com/en-us/global-infrastructure/services/?WT.mc_id=blog-learning-abornst).</span></span>


### <a name="create-a-resource-group-for-your-dsvm-in-a-region-of-your-choice"></a><span data-ttu-id="749de-109">Erstellen Sie in einer Region Ihrer Wahl eine Ressourcengruppe für Ihre DSVM-Instanz:</span><span class="sxs-lookup"><span data-stu-id="749de-109">Create a resource group for your DSVM in a region of your choice:</span></span>
```
az group create --name [[NAME OF RESOURCE GROUP]] --location [[ Data center. For eg: "West US 2"]]
```

<span data-ttu-id="749de-110">Eine Liste mit verfügbaren Regionen finden Sie [hier](https://github.com/Azure/DataScienceVM/blob/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="749de-110">A list of available regions can be found here [Azure Regions](https://github.com/Azure/DataScienceVM/blob/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json).</span></span>

### <a name="deploy-your-dsvm-to-your-new-resource-group"></a><span data-ttu-id="749de-111">Bereitstellen Ihrer DSVM-Instanz in Ihrer neuen Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="749de-111">Deploy your DSVM to your new resource group</span></span>

```
az group deployment create --resource-group  [[NAME OF RESOURCE GROUP ABOVE]]  --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json --parameters parameter_file.json
```

## <a name="step-2-open-the-port-8888-22-on-the-dsvm"></a><span data-ttu-id="749de-112">Schritt 2: Öffnen der Ports 8888 und 22 für die DSVM-Instanz</span><span class="sxs-lookup"><span data-stu-id="749de-112">Step 2 Open the Port 8888, 22 on the DSVM</span></span> 

```
$ az vm open-port -g [[NAME OF RESOURCE GROUP]] -n [[HOSTNAME OF DSVM]] --port 22 --priority 900
$ az vm open-port -g [[NAME OF RESOURCE GROUP]] -n [[HOSTNAME OF DSVM]] --port 8888 --priority 901
```

<span data-ttu-id="749de-113">Port 8888 ist der Standardport für Jupyter-Notebooks. Eine ausführliche Anleitung zum Öffnen von Ports finden Sie [hier](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/nsg-quickstart-portal?WT.mc_id=blog-medium-abornst).</span><span class="sxs-lookup"><span data-stu-id="749de-113">Port 8888 is the default port for Jupyter Notebooks For detailed steps on opening a port [click here](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/nsg-quickstart-portal?WT.mc_id=blog-medium-abornst)</span></span>
 
## <a name="step-3-connect-to-the-dsvm-with-the-azure-shell"></a><span data-ttu-id="749de-114">Schritt 3: Herstellen einer Verbindung mit der DSVM-Instanz über Azure Shell</span><span class="sxs-lookup"><span data-stu-id="749de-114">Step 3 Connect to the DSVM with the Azure Shell</span></span> 
 
``` 
ssh myuser@[[HOSTNAME OF DSVM]].westus2.cloudapp.azure.com 
``` 

## <a name="step-4-run-jupyter-in-docker-container--link-8888-port-to-the-vm-host"></a><span data-ttu-id="749de-115">Schritt 4: Ausführen von Jupyter im Docker-Container und Verknüpfen von Port 8888 mit dem VM-Host</span><span class="sxs-lookup"><span data-stu-id="749de-115">Step 4 Run Jupyter in Docker Container & link 8888 port to the VM Host</span></span> 

<span data-ttu-id="749de-116">Erstellen Sie für den Port 8888 eine Verknüpfung zwischen dem virtuellen Computer und dem Docker-Container, installieren Sie Jupyter, und pullen Sie PyTorch-Tutorials.</span><span class="sxs-lookup"><span data-stu-id="749de-116">Link port 8888 between the VM and the docker container, install jupyter and pull pytorch tutorials.</span></span>  

```  
sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
  'conda install jupyter matplotlib -y &&\
  curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
  jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
``` 

## <a name="step-5-navigate-to-the-jupyter-notebook-in-the-browser"></a><span data-ttu-id="749de-117">Schritt 5: Navigieren zum Jupyter-Notebook im Browser</span><span class="sxs-lookup"><span data-stu-id="749de-117">Step 5 Navigate to the Jupyter Notebook in the Browser</span></span> 

<span data-ttu-id="749de-118">Wenn das Jupyter-Notebook ausgeführt wird, wird eine Meldung wie die folgende angezeigt:</span><span class="sxs-lookup"><span data-stu-id="749de-118">Once the Jupyter notebook is running you will see a message as follows :</span></span> 

> <span data-ttu-id="749de-119">Kopieren Sie bei der ersten Verbindungsherstellung die folgende URL, und fügen Sie sie in Ihren Browser ein, um sich mit einem Token anzumelden: http://(5b8783e7911d oder 127.0.0.1):8888/?token={Token}</span><span class="sxs-lookup"><span data-stu-id="749de-119">Copy/paste this URL into your browser when you connect for the first time, to login with a token: http://(5b8783e7911d or 127.0.0.1):8888/?token={sometoken}</span></span>

<span data-ttu-id="749de-120">Ersetzen Sie den Teil **http://(5b8783e7911d oder 127.0.0.1)** der URL durch **[[HOSTNAME DER DSVM-INSTANZ]].westus2.cloudapp.azure.com**, und navigieren Sie in Ihrem Browser auf einer neuen Registerkarte zu der Adresse:</span><span class="sxs-lookup"><span data-stu-id="749de-120">Replace the **http://(5b8783e7911d or 127.0.0.1)** part of the url with **[[HOSTNAME OF DSVM]].westus2.cloudapp.azure.com** and navigate to the address  in a new a tab in your browser:</span></span>
- <span data-ttu-id="749de-121">[[HOSTNAME DER DSVM-INSTANZ]].westus2.cloudapp.azure.com:8888/?token={Token}</span><span class="sxs-lookup"><span data-stu-id="749de-121">[[HOSTNAME OF DSVM]].westus2.cloudapp.azure.com:8888/?token={sometoken}</span></span>
