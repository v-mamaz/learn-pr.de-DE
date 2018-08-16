Während des Buildprozesses erstellt Packer temporäre Azure-Ressourcen, für die Basis-VM. Wenn diese Basis-VM für die Verwendung als Image erfassen möchten, müssen Sie eine Ressourcengruppe definieren. Eine Azure-Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen bereitgestellt und verwaltet werden.

Erstellen Sie zuerst eine Ressourcengruppe in Azure Cloud Shell mit [az-Gruppe erstellen](/cli/azure/group#az_group_create). Im folgenden Beispiel wird eine Ressourcengruppe mit dem Namen *myResourceGroup* am Standort *eastus* erstellt:

```azurecli
az group create -n myResourceGroup -l eastus
```

Packer authentifiziert sich bei Azure mithilfe eines Dienstprinzipals. Ein Azure-Dienstprinzipal ist eine Sicherheitsidentität, die Sie mit Apps, Diensten und Automatisierungstools wie Packer verwenden können. Sie steuern und definieren die Berechtigungen hinsichtlich der Vorgänge, die der Dienstprinzipal in Azure ausführen können soll.

Erstellen eines dienstprinzipals in Azure Cloud Shell mit [az Ad sp create-for-Rbac](/cli/azure/ad/sp#create-for-rbac) und geben Sie die Anmeldeinformationen, die Packer benötigt:

```azurecli
az ad sp create-for-rbac --query "{ client_id: appId, client_secret: password, tenant_id: tenant }"
```

Ein Beispiel der Ausgabe der vorherigen Befehle lautet wie folgt:

```azurecli
{
    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
}
```

Kopieren Sie Ihre eigenen Ausgabe für die Verwendung im nächsten Schritt ein.

Zur Authentifizierung bei Azure müssen Sie auch Ihre Azure-Abonnement-ID mit [az account show](/cli/azure/account#az_account_show) abrufen:

```azurecli
az account show --query '{ "subscription_id": "id" }'
```

Die Ausgabe dieser beiden Befehle verwenden Sie im nächsten Schritt.