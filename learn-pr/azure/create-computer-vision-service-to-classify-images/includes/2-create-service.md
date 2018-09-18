In dieser Einheit erstellen Sie einen Maschinelles Sehen-API-Dienst mithilfe der Azure CLI.

# <a name="exercise-create-a-computer-vision-service"></a>Übung: Erstellen eines Maschinelles Sehen-Diensts

[Maschinelles Sehen](/azure/cognitive-services/computer-vision/home) ist Teil von [Microsoft Cognitive Services](/azure/cognitive-services/welcome), einer vollständigen Sammlung von Algorithmen für maschinelles Lernen, die als Dienst für alle Benutzer verfügbar ist. Anstatt genügend Daten zu generieren, um ein Modell von Grund auf neu zu trainieren, stellen wir vortrainierte Modelle für jedermann zur Verfügung.

Unter den vielen verfügbaren Diensten bieten wir Dienste an, die Sprache, Bilder, Videos, Suchen und mehr verarbeiten können.

In dieser Übung konzentrieren wir uns darauf, den erforderlichen Dienst zu erstellen, der es uns ermöglicht, Bilder zu verarbeiten. Nach dem Abschluss dieser Übung können Sie einen API-Endpunkt erstellen, der Bilder identifizieren kann.

# <a name="create-a-computer-vision-api-service"></a>Erstellen eines Maschinelles Sehen-API-Diensts

Bevor Sie den Maschinelles Sehen-API-Dienst erstellen können, benötigen Sie eine *Ressourcengruppe* für die Bereitstellung. Eine Azure-Ressourcengruppe ist eine logische Sammlung, in der alle Azure-Ressourcen bereitgestellt und verwaltet werden.

```azurecli
az group create --name ComputerVisionRG --location westus2
```

Nachdem Sie die Ressourcengruppe erstellt haben, erstellen Sie den Dienst mit dem Befehl `az cognitiveservices account create` und dem Namen Ihres Diensts. 

```azurecli
az cognitiveservices account create --kind ComputerVision -l westus2 -n ComputerVisionService --sku F0 -g ComputerVisionRG
```
