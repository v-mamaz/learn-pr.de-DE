Standardmäßig ist Azure Container Instances zustandslos. Wenn der Container abstürzt oder beendet wird, gehen alle Zustände verloren. Um den Zustand nach Ablauf der Lebensdauer des Containers beizubehalten, müssen Sie ein Volume aus einem externen Speicher bereitstellen.

In dieser Einheit stellen Sie eine Azure-Dateifreigabe in einer Azure-Containerinstanz zum Speichern und Abrufen von Daten bereit.

## <a name="create-an-azure-file-share"></a>Erstellen einer Azure-Dateifreigabe

Bevor Sie eine Azure-Dateifreigabe in Azure Container Instances einbinden, müssen Sie sie erstellen. Führen Sie das folgende Skript aus, um ein Speicherkonto zu erstellen. Der Name des Speicherkontos muss global eindeutig sein, daher fügt das Skript der Basiszeichenfolge einen Zufallswert hinzu:

```azurecli
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM

az storage account create --resource-group <rgn>[Sandbox resource group name]</rgn> --name $ACI_PERS_STORAGE_ACCOUNT_NAME --sku Standard_LRS
```

Führen Sie den folgenden Befehl aus, um die Verbindungszeichenfolge für das Speicherkonto in einer Umgebungsvariablen mit dem Namen *AZURE_STORAGE_CONNECTION_STRING* zu platzieren. Diese Umgebungsvariable kann von der Azure CLI gelesen und für speicherbezogene Vorgänge verwendet werden:

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string --resource-group myResourceGroup --name $ACI_PERS_STORAGE_ACCOUNT_NAME --output tsv`
```

Erstellen Sie die Dateifreigabe durch Ausführen des Befehls `az storage share create`. Im folgenden Beispiel wird eine Freigabe mit dem Namen *aci-share-demo* erstellt:

```azurecli
az storage share create --name aci-share-demo
```

## <a name="get-storage-credentials"></a>Erhalten der Anmeldeinformationen für das Speicherkonto

Um eine Azure-Dateifreigabe als Volume in Azure Container Instances bereitzustellen, benötigen Sie drei Werte: den Namen des Speicherkontos, den Freigabenamen und den Speicherzugriffsschlüssel.

Wenn Sie das oben angegebene Skript verwendet haben, wurde der Name des Speicherkontos mit einem zufälligen Wert am Ende erstellt. Um die endgültige Zeichenfolge (einschließlich des zufälligen Teils) abzufragen, verwenden Sie die folgenden Befehle:

```azurecli
STORAGE_ACCOUNT=$(az storage account list --resource-group <rgn>[Sandbox resource group name]</rgn> --query "[?contains(name,'$ACI_PERS_STORAGE_ACCOUNT_NAME')].[name]" --output tsv)
echo $STORAGE_ACCOUNT
```

Der Freigabename ist bereits bekannt (aci-share-demo), daher verbleibt nur der Speicherkontoschlüssel, der mit dem folgenden Befehl gesucht werden kann:

```azurecli
STORAGE_KEY=$(az storage account keys list --resource-group <rgn>[Sandbox resource group name]</rgn> --account-name $STORAGE_ACCOUNT --query "[0].value" --output tsv)
echo $STORAGE_KEY
```

## <a name="deploy-container-and-mount-volume"></a>Bereitstellen des Containers und des Volumes

Um eine Azure-Dateifreigabe als Volume in einem Container bereitzustellen, geben Sie die Freigabe und den Bereitstellungspunkt des Volumes bei der Erstellung des Containers an:

```azurecli
az container create \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --name aci-demo-files \
    --image microsoft/aci-hellofiles \
    --ports 80 \
    --ip-address Public \
    --azure-file-volume-account-name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --azure-file-volume-account-key $STORAGE_KEY \
    --azure-file-volume-share-name aci-share-demo \
    --azure-file-volume-mount-path /aci/logs/
```

Nachdem der Container erstellt wurde, rufen Sie die öffentliche IP-Adresse ab:

```azurecli
az container show --resource-group <rgn>[Sandbox resource group name]</rgn> --name aci-demo-files --query ipAddress.ip -o tsv
```

Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers. Es wird ein einfaches Formular angezeigt. Geben Sie Text ein, und klicken Sie auf **Senden**. Dadurch wird eine Datei in der Azure-Dateifreigabe mit dem hier eingegebenen Text als Textkörper erstellt.

![Beispiel für eine Azure Container Instances-Dateifreigabe](../media-draft/files-ui.png)

Zur Überprüfung können Sie zur Dateifreigabe im Azure-Portal navigieren und die Datei herunterladen.

![Beispieltextdatei mit Inhalten – Demoanwendung](../media-draft/sample-text.png)

Wenn es sich bei den Inhalten, die in der Azure-Dateifreigabe gespeichert sind, um wertvolle Dateien und Daten handelt, kann diese Freigabe auf einer neuen Containerinstanz erneut bereitgestellt werden, um zustandsbehaftete Daten verfügbar zu machen.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie eine Azure-Dateifreigabe sowie einen Container erstellt und die Dateifreigabe anschließend in dem Container bereitgestellt. Diese Freigabe wurde dann verwendet, um Anwendungsdaten zu speichern.

In der nächsten Einheit werden Sie einige gängige Vorgänge zur Problembehandlung in Container Instances durchführen.
