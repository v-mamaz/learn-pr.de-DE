Unser Ziel ist, einen neuen virtuellen Azure-Computer zu erstellen. Wir müssen mehrere Informationen angeben, um den Speicherort der Ressource, das zu verwendende Betriebssystem und die für die VM erforderliche Hardwarekonfiguration zu definieren. Lassen Sie uns mit der **Ressourcengruppe** beginnen.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Azure verwendet _Ressourcengruppen_, um zusammengehörige Ressourcen wie virtuelle Computer und Datenbanken zu gruppieren. Die Ressourcengruppe bestimmt auch einen Standort (als „Region“ bezeichnet), der entscheidet, in welchem Rechenzentrum die Ressource platziert wird.

> [!NOTE]
> Die Azure-Sandbox bietet eine vorab erstellte Ressourcengruppe mit dem Namen <rgn>[Ressourcengruppennamen Sandkasten]</rgn>. Sie müssen sich nicht zum Ausführen dieser Schritte. Allerdings sind für die Erstellung Ihrer _eigenen_ Ressourcen für tatsächliche Projekte, diese werden die Befehle, die Sie ausführen müssen. Die Azure-Sandbox lässt nicht zu, dass Sie Ressourcengruppen direkt zu erstellen.

Beispielsweise können Sie den folgenden Azure CLI-Befehl eingeben, in Azure Cloud Shell zum Erstellen einer Ressourcengruppe in der **USA, Osten** Region. Ersetzen Sie **[Ressourcengruppe]** durch einen gültigen Namen an, die in das aktive Abonnement eindeutig ist.

```azurecli
az group create --name [resource-group] --location eastus
```

Dies würde zurückgeben, eine JSON-Block, der angibt, ob die Ressourcengruppe erstellt wurde.

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

Beachten Sie, dass der eindeutige Bezeichner, Standort und Name des Abonnements als Teil der Antwort zurückgegeben wird. Sie können diese Informationen verwenden, um zu überprüfen, ob sie im richtigen Abonnement und am richtigen Standort erstellt wurden.

Nun wir wissen, wie eine Ressourcengruppe zu erstellen erstellen wir einen neuen virtuellen Computer an.