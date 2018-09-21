In dieser Einheit erstellen Sie eine Azure Container Registry-Instanz über die Azure CLI.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]
 
## <a name="create-an-azure-container-registry"></a>Erstellen einer Azure-Containerregistrierung

Wir arbeiten in einer kostenlosen Sandbox, sodass Sie keine eigene Ressourcengruppe erstellen müssen. Führen Sie den Befehl `az acr create` aus, um eine Azure-Containerregistrierung zu erstellen. Der Name der Containerregistrierung muss innerhalb von Azure eindeutig sein und 5 bis 50 alphanumerische Zeichen enthalten. Ersetzen Sie `<acrName>` durch einen eindeutigen Namen für die Registrierung.

In diesem Beispiel wird eine Premium-Registrierungs-SKU bereitgestellt. Die Premium-SKU ist für die Georeplikation erforderlich. Geben Sie den folgenden Befehl in den Cloud Shell-Editor ein.

```azurecli
az acr create --resource-group <rgn>[Sandbox resource group name]</rgn> --name <acrName> --sku Premium
```

Im Folgenden sehen Sie eine Beispielausgabe für eine neue Azure-Containerregistrierung:

```output
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

In dieser Einheit haben Sie eine Azure Container Registry-Instanz über die Azure CLI erstellt.