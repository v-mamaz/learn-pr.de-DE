Unser Ziel ist, einen neuen virtuellen Azure-Computer zu erstellen. Wir müssen mehrere Informationen angeben, um den Speicherort der Ressource, das zu verwendende Betriebssystem und die für die VM erforderliche Hardwarekonfiguration zu definieren. Lassen Sie uns mit der **Ressourcengruppe** beginnen.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Azure verwendet _Ressourcengruppen_, um zusammengehörige Ressourcen wie virtuelle Computer und Datenbanken zu gruppieren. Die Ressourcengruppe bestimmt auch einen Standort (als „Region“ bezeichnet), der entscheidet, in welchem Rechenzentrum die Ressource platziert wird.

Da wir experimentieren, starten Sie mit dem Erstellen einer neuen Ressourcengruppe namens `ExerciseResources`, die Sie in der Region `eastus` platzieren.

> [!NOTE]
> Vergewissern Sie sich, dass Sie genau diesen Namen für Ihre neue Ressourcengruppe verwenden, da das Microsoft-Lernsystem später diesen Ressourcennamen suchen wird. 

Geben Sie in Azure Cloud Shell den folgenden Azure CLI-Befehl ein, um die Ressourcengruppe in Ihrem Abonnement zu erstellen.

```azurecli
az group create --name ExerciseResources --location eastus
```

Ein JSON-Block wird zurückgegeben, der angibt, dass die Ressourcengruppe erstellt wurde. Dieser sollte ungefähr wie folgt aussehen:

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources",
  "location": "eastus",
  "managedBy": null,
  "name": "ExerciseResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

Beachten Sie, dass der eindeutige Bezeichner, Standort und Name des Abonnements als Teil der Antwort zurückgegeben wird. Sie können diese Informationen verwenden, um zu überprüfen, ob sie im richtigen Abonnement und am richtigen Standort erstellt wurden.

Nachdem wir nun über eine Ressourcengruppe verfügen, lassen Sie uns einen neuen virtuellen Computer erstellen.