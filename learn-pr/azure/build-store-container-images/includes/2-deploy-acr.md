In dieser Einheit erstellen Sie eine Azure Container Registry-Instanz über die Azure CLI.

## <a name="create-an-azure-container-registry"></a>Erstellen einer Azure Container Registry-Instanz

Zum Erstellen einer Azure Container Registry-Instanz benötigen Sie eine *Ressourcengruppe*, in der die Instanz bereitgestellt wird. Eine Azure-Ressourcengruppe ist eine logische Sammlung, in der alle Azure-Ressourcen bereitgestellt und verwaltet werden.

Erstellen Sie mit dem Befehl `az group create` eine Ressourcengruppe. Im folgenden Beispiel wird eine Ressourcengruppe mit dem Namen *myResourceGroup* in der Region *eastus* erstellt:

```azurecli
az group create --name myResourceGroup --location eastus
```

Erstellen Sie nach der Erstellung der Ressourcengruppe mit dem Befehl `az acr create` eine Azure-Containerregistrierung. Der Containerregistrierungsname muss innerhalb von Azure eindeutig sein und zwischen 5 und 50 alphanumerische Zeichen enthalten. Ersetzen Sie `<acrName>` durch einen eindeutigen Namen für die Registrierung.

In diesem Beispiel wird eine Premium-Registrierungs-SKU bereitgestellt. Die Premium-SKU ist für die Georeplikation erforderlich. Weitere Informationen zu Container Registry-SKUs finden Sie unter [Azure Container Registry-SKUs](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-skus).

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Premium
```

Im Folgenden sehen Sie eine Beispielausgabe für eine neue Azure-Containerregistrierung.

```console
{
  "adminUserEnabled": false,
  "creationDate": "2018-08-15T19:19:07.042178+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myACR0007",
  "location": "eastus",
  "loginServer": "myacr.azurecr.io",
  "name": "myACR",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Premium",
    "tier": "Premium"
  },
  "status": null,
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Im verbleibenden Teil dieses Moduls wird `<acrName>` als Platzhalter für den Namen der Containerregistrierung verwendet, den Sie in diesem Schritt angegeben haben.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie über die Azure CLI eine Azure Container Registry-Instanz erstellt. In der nächsten Einheit verwenden Sie Azure Container Registry zum Erstellen eines Containerimages und Speichern des Images in der Containerregistrierung.