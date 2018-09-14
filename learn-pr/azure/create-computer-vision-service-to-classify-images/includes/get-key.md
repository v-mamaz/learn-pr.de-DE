## <a name="get-an-access-key"></a>Abrufen eines Zugriffsschlüssels

Falls dies noch nicht geschehen, führen Sie den folgenden Befehl in Azure Cloud Shell zum Speichern des Schlüssels für die API-Zugriff in einer Variablen namens `key`. Wir verwenden diese Variable in nachfolgenden Aufrufen.

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[Sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
