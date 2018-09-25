## <a name="get-an-access-key"></a><span data-ttu-id="c962f-101">Abrufen eines Zugriffsschlüssels</span><span class="sxs-lookup"><span data-stu-id="c962f-101">Get an access key</span></span>

<span data-ttu-id="c962f-102">Führen Sie, falls noch nicht geschehen, den folgenden Befehl in Azure Cloud Shell aus, um den API-Zugriffsschlüssel in einer Variablen mit dem Namen `key` zu speichern.</span><span class="sxs-lookup"><span data-stu-id="c962f-102">If you haven't done so already, run the following command in Azure Cloud Shell to store the API access key in a variable called `key`.</span></span> <span data-ttu-id="c962f-103">Diese Variable wird auch in späteren Aufrufen verwendet.</span><span class="sxs-lookup"><span data-stu-id="c962f-103">We'll use this variable in subsequent calls.</span></span>

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
