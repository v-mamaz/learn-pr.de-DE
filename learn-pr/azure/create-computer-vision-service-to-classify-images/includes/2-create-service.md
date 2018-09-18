<span data-ttu-id="d32fa-101">In dieser Einheit erstellen Sie einen Maschinelles Sehen-API-Dienst mithilfe der Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d32fa-101">In this unit, you will create a Computer Vision API service using the Azure CLI.</span></span>

# <a name="exercise-create-a-computer-vision-service"></a><span data-ttu-id="d32fa-102">Übung: Erstellen eines Maschinelles Sehen-Diensts</span><span class="sxs-lookup"><span data-stu-id="d32fa-102">Exercise: Create a Computer Vision service</span></span>

<span data-ttu-id="d32fa-103">[Maschinelles Sehen](/azure/cognitive-services/computer-vision/home) ist Teil von [Microsoft Cognitive Services](/azure/cognitive-services/welcome), einer vollständigen Sammlung von Algorithmen für maschinelles Lernen, die als Dienst für alle Benutzer verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="d32fa-103">[Computer Vision](/azure/cognitive-services/computer-vision/home) is part of [Azure Cognitive Services](/azure/cognitive-services/welcome), which is a complete set of machine learning algorithms available as a service for anyone to use.</span></span> <span data-ttu-id="d32fa-104">Anstatt genügend Daten zu generieren, um ein Modell von Grund auf neu zu trainieren, stellen wir vortrainierte Modelle für jedermann zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="d32fa-104">Instead of generating enough data to train a model from scratch, we make available pre-trained models for anyone to use.</span></span>

<span data-ttu-id="d32fa-105">Unter den vielen verfügbaren Diensten bieten wir Dienste an, die Sprache, Bilder, Videos, Suchen und mehr verarbeiten können.</span><span class="sxs-lookup"><span data-stu-id="d32fa-105">Among the many services available, we provide services that can handle voice, image, video, search, language, and more.</span></span>

<span data-ttu-id="d32fa-106">In dieser Übung konzentrieren wir uns darauf, den erforderlichen Dienst zu erstellen, der es uns ermöglicht, Bilder zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="d32fa-106">In this exercise, we're going to focus on creating the necessary service that will allow us to handle images.</span></span> <span data-ttu-id="d32fa-107">Nach dem Abschluss dieser Übung können Sie einen API-Endpunkt erstellen, der Bilder identifizieren kann.</span><span class="sxs-lookup"><span data-stu-id="d32fa-107">After this exercise, you will be able to create an API endpoint that will be able to identify images.</span></span>

# <a name="create-a-computer-vision-api-service"></a><span data-ttu-id="d32fa-108">Erstellen eines Maschinelles Sehen-API-Diensts</span><span class="sxs-lookup"><span data-stu-id="d32fa-108">Create a Computer Vision API service</span></span>

<span data-ttu-id="d32fa-109">Bevor Sie den Maschinelles Sehen-API-Dienst erstellen können, benötigen Sie eine *Ressourcengruppe* für die Bereitstellung.</span><span class="sxs-lookup"><span data-stu-id="d32fa-109">Before you create your Computer Vision API service, you need a *resource group* to deploy it to.</span></span> <span data-ttu-id="d32fa-110">Eine Azure-Ressourcengruppe ist eine logische Sammlung, in der alle Azure-Ressourcen bereitgestellt und verwaltet werden.</span><span class="sxs-lookup"><span data-stu-id="d32fa-110">A resource group is a logical collection into which all Azure resources are deployed and managed.</span></span>

```azurecli
az group create --name ComputerVisionRG --location westus2
```

<span data-ttu-id="d32fa-111">Nachdem Sie die Ressourcengruppe erstellt haben, erstellen Sie den Dienst mit dem Befehl `az cognitiveservices account create` und dem Namen Ihres Diensts.</span><span class="sxs-lookup"><span data-stu-id="d32fa-111">Once you've created the resource group, create the service with the `az cognitiveservices account create` command and the name of your service.</span></span> 

```azurecli
az cognitiveservices account create --kind ComputerVision -l westus2 -n ComputerVisionService --sku F0 -g ComputerVisionRG
```
