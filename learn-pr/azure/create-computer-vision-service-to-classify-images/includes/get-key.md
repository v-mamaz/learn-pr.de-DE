## <a name="get-an-access-key"></a>Abrufen eines Zugriffsschlüssels

Führen Sie, falls noch nicht geschehen, den folgenden Befehl in Azure Cloud Shell aus, um den API-Zugriffsschlüssel in einer Variablen mit dem Namen `key` zu speichern. Diese Variable wird auch in späteren Aufrufen verwendet.

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
