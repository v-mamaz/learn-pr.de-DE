Unser Ziel ist die Erstellung einer neuen Azure-VM. Wir benötigen, geben Sie die verschiedenen informationsbestandteilen um den Speicherort der Ressource, Betriebssystem verwenden und die Hardwarekonfiguration, die erforderlich sind, für den virtuellen Computer zu identifizieren. Beginnen wir mit der **Ressourcengruppe**.

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Azure verwendet _Ressourcengruppen_ um zusammengehörige Ressourcen wie virtuelle Computer und Datenbanken zu gruppieren. Die Ressourcengruppe identifiziert auch einen bestimmten Standort (eine "Region" bezeichnet), der entscheiden, welche Datencenter wird in die Ressource platziert wird.

Da wir experimentieren können, starten Sie durch das Erstellen einer neuen Ressourcengruppe mit dem Namen `ExerciseResources` und platzieren Sie sie in der `eastus` Region.

> [!NOTE]
> Achten Sie darauf, die exakt diesem Namen für die neue Ressourcengruppe zu verwenden, das Microsoft-Learn-System wird, und sehen uns für diese Ressourcennamen später noch mal. 

Geben Sie den folgenden Azure CLI-Befehl in der Cloud Shell, um die Ressourcengruppe in Ihrem Abonnement zu erstellen.

```azurecli
az group create --name ExerciseResources --location eastus
```

Dadurch wird zurückgegeben, eine JSON-Block, der angibt, ob die Ressourcengruppe erstellt wurde. Es sollte etwa so aussehen:

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

Beachten Sie, dass die eindeutige Abonnement-ID, den Speicherort und Namen als Teil der Antwort zurückgegeben: Sie können diese verwenden, um sicherzustellen, dass es in die richtige Abonnement und den Standort erstellt wurde.

Nun, da wir eine Ressourcengruppe erstellt haben, erstellen wir einen neuen virtuellen Computer an.