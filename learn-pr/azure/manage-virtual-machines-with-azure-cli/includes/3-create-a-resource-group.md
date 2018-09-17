Unser Ziel ist, einen neuen virtuellen Azure-Computer zu erstellen. Wir müssen mehrere Informationen angeben, um den Speicherort der Ressource, das zu verwendende Betriebssystem und die für die VM erforderliche Hardwarekonfiguration zu definieren. Lassen Sie uns mit der **Ressourcengruppe** beginnen.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Azure verwendet _Ressourcengruppen_, um zusammengehörige Ressourcen wie virtuelle Computer und Datenbanken zu gruppieren. Die Ressourcengruppe bestimmt auch einen Standort (als „Region“ bezeichnet), der entscheidet, in welchem Rechenzentrum die Ressource platziert wird.

> [!NOTE]
> Die Azure-Sandbox stellt eine vorab erstellte Ressourcengruppe mit dem Namen <rgn>[Sandbox resource group name]</rgn> (Sandbox Ressourcengruppenname) bereit. Die Ausführung der folgenden Schritte ist optional. Wenn Sie allerdings Ihre _eigenen_ Ressourcen für echte Projekte erstellen, werden Sie die aufgeführten Befehle nutzen müssen. Sie können mit der Azure-Sandbox Ressourcengruppen nicht direkt erstellen.

Geben Sie in Azure Cloud Shell beispielsweise den folgenden Azure CLI-Befehl ein, um eine Ressourcengruppe in der Region **USA, Osten** zu erstellen. **[resource-group]** ersetzen Sie durch einen gültigen Namen, der im aktiven Abonnement eindeutig ist.

```azurecli
az group create --name [resource-group] --location eastus
```

Dadurch wird ein JSON-Block zurückgegeben, der angibt, dass die Ressourcengruppe erstellt wurde.

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/<resourcegroup>",
  "location": "eastus",
  "managedBy": null,
  "name": "<resourcegroup>",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

Beachten Sie, dass der eindeutige Bezeichner, Standort und Name des Abonnements als Teil der Antwort zurückgegeben wird. Sie können diese Informationen verwenden, um zu überprüfen, ob die Ressourcengruppe im richtigen Abonnement und am richtigen Standort erstellt wurde.

Da wir nun wissen, wie eine Ressourcengruppe erstellt wird, können wir einen neuen virtuellen Computer erstellen.