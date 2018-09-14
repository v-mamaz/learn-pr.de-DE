## <a name="introduction-to-jupyter-for-more-interactive-deep-learning"></a>Einführung in Jupyter für interaktiveres Deep Learning 

Jupyter Notebook ist eine Open-Source-Webanwendung, mit der Sie Dokumente mit Livecode, Gleichungen, Visualisierungen und narrativem Text erstellen und teilen können. Zu den Anwendungsbereichen zählen etwa Datenbereinigung und -transformation, numerische Simulationen, Statistikmodelle, Datenvisualisierungen, Machine Learning und vieles mehr.

## <a name="serving-jupyter-notebooks-with-nvidia-docker-on-an-azure-dsvm"></a>Bereitstellen von Jupyter-Notebooks mit NVIDIA Docker in einer Azure-DSVM-Instanz

### <a name="step-1-create-a-linux-dsvm"></a>Schritt 1: Erstellen einer Linux-DSVM-Instanz

Verwenden von Aufrufcode über die Azure-Befehlszeilenschnittstelle

```
code .
```

Ausfüllen und Speichern des folgenden Bereitstellungsschemas als „parameter_file.json“

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

Eine Liste mit verfügbaren VM-Größen finden Sie [hier](https://azure.microsoft.com/global-infrastructure/services/?WT.mc_id=blog-learning-abornst).


### <a name="create-a-resource-group-for-your-dsvm-in-a-region-of-your-choice"></a>Erstellen Sie in einer Region Ihrer Wahl eine Ressourcengruppe für Ihre DSVM-Instanz:
```
az group create --name [[NAME OF RESOURCE GROUP]] --location [[ Data center. For eg: "West US 2"]]
```

Eine Liste mit verfügbaren Regionen finden Sie [hier](https://github.com/Azure/DataScienceVM/blob/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json).

### <a name="deploy-your-dsvm-to-your-new-resource-group"></a>Bereitstellen Ihrer DSVM-Instanz in Ihrer neuen Ressourcengruppe

```
az group deployment create --resource-group  [[NAME OF RESOURCE GROUP ABOVE]]  --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json --parameters parameter_file.json
```

## <a name="step-2-open-the-port-8888-22-on-the-dsvm"></a>Schritt 2: Öffnen der Ports 8888 und 22 für die DSVM-Instanz 

```
$ az vm open-port -g [[NAME OF RESOURCE GROUP]] -n [[HOSTNAME OF DSVM]] --port 22 --priority 900
$ az vm open-port -g [[NAME OF RESOURCE GROUP]] -n [[HOSTNAME OF DSVM]] --port 8888 --priority 901
```

Port 8888 ist der Standardport für Jupyter-Notebooks. Eine ausführliche Anleitung zum Öffnen von Ports finden Sie [hier](https://docs.microsoft.com/azure/virtual-machines/windows/nsg-quickstart-portal?WT.mc_id=blog-medium-abornst).
 
## <a name="step-3-connect-to-the-dsvm-with-the-azure-shell"></a>Schritt 3: Herstellen einer Verbindung mit der DSVM-Instanz über Azure Shell 
 
``` 
ssh myuser@[[HOSTNAME OF DSVM]].westus2.cloudapp.azure.com 
``` 

## <a name="step-4-run-jupyter-in-docker-container--link-8888-port-to-the-vm-host"></a>Schritt 4: Ausführen von Jupyter im Docker-Container und Verknüpfen von Port 8888 mit dem VM-Host 

Erstellen Sie für den Port 8888 eine Verknüpfung zwischen dem virtuellen Computer und dem Docker-Container, installieren Sie Jupyter, und pullen Sie PyTorch-Tutorials.  

```  
sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
  'conda install jupyter matplotlib -y &&\
  curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
  jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
``` 

## <a name="step-5-navigate-to-the-jupyter-notebook-in-the-browser"></a>Schritt 5: Navigieren zum Jupyter-Notebook im Browser 

Wenn das Jupyter-Notebook ausgeführt wird, wird eine Meldung wie die folgende angezeigt: 

> Kopieren Sie bei der ersten Verbindungsherstellung die folgende URL, und fügen Sie sie in Ihren Browser ein, um sich mit einem Token anzumelden: http://(5b8783e7911d oder 127.0.0.1):8888/?token={Token}

Ersetzen Sie den Teil **http://(5b8783e7911d oder 127.0.0.1)** der URL durch **[[HOSTNAME DER DSVM-INSTANZ]].westus2.cloudapp.azure.com**, und navigieren Sie in Ihrem Browser auf einer neuen Registerkarte zu der Adresse:
- [[HOSTNAME DER DSVM-INSTANZ]].westus2.cloudapp.azure.com:8888/?token={Token}
