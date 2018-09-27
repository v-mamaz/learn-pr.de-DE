Mithilfe von Umgebungsvariablen in Ihren Containerinstanzen können Sie eine dynamische Konfiguration der Anwendung oder des Skripts vornehmen, die bzw. das der Container ausführt. Sie können entweder die Azure-Befehlszeilenschnittstelle, PowerShell oder das Azure-Portal verwenden, um Variablen bei der Containererstellung festzulegen. Abgesicherte Umgebungsvariablen werden zum Schutz vor der Preisgabe sensibler Informationen in der Ausgabe von Containern verwendet.

Hier erstellen Sie eine Azure Cosmos DB-Instanz und verwenden Umgebungsvariablen, um die Verbindungsinformationen an eine Azure-Containerinstanz zu übergeben. Eine Anwendung im Container nutzt die Variablen, um Cosmos DB-Daten zu schreiben und zu lesen. Sie erstellen sowohl eine Umgebungsvariable als auch eine abgesicherte Umgebungsvariable.

## <a name="deploy-azure-cosmos-db"></a>Bereitstellen von Azure Cosmos DB

Erstellen Sie mithilfe des Befehls `az cosmosdb create` die Azure Cosmos DB-Instanz. Bei diesem Beispiel wird auch die Azure Cosmos DB-Endpunktadresse in einer Variablen mit dem Namen *COSMOS_DB_ENDPOINT* angegeben. Geben Sie einen eindeutigen Namen für `[cosmos-db-name]` an.

Die Ausführung dieses Befehls kann einige Minuten dauern:

```azurecli
COSMOS_DB_ENDPOINT=$(az cosmosdb create --resource-group <rgn>[sandbox resource group name]</rgn> --name [cosmos-db-name] --query documentEndpoint --output tsv)
```

Rufen Sie als Nächstes den Azure Cosmos DB-Verbindungsschlüssel mit dem Befehl `az cosmosdb list-keys` ab, und speichern Sie ihn in einer Variablen namens *COSMOS_DB_DB_MASTERKEY*. Denken Sie daran, `[cosmos-db-name]` erneut zu ersetzen:

```azurecli
COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys --resource-group <rgn>[sandbox resource group name]</rgn> --name [cosmos-db-name] --query primaryMasterKey --output tsv)
```

## <a name="deploy-a-container-instance"></a>Bereitstellen einer Containerinstanz

Führen Sie den Befehl `az container create` aus, um eine Azure-Containerinstanz zu erstellen. Beachten Sie, dass zwei Umgebungsvariablen erstellt werden, `COSMOS_DB_ENDPOINT` und `COSMOS_DB_MASTERKEY`. Diese Variablen enthalten die Werte, die für die Verbindung mit der Azure Cosmos DB-Instanz benötigt werden:

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --location eastus \
    --environment-variables COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
```

Rufen Sie nach Abschluss der Containererstellung mithilfe des Befehls `az container show` die IP-Adresse ab:

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo \
    --query ipAddress.ip \
    --output tsv
```

Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers. 

> [!IMPORTANT]
> Manchmal brauchen Container ein oder zwei Minuten, um vollständig betriebsbereit zu sein und Verbindungen aufnehmen zu können. Wenn beim Navigieren zur IP-Adresse in Ihrem Browser keine Antwort angezeigt wird, warten Sie einen Moment, und aktualisieren Sie dann die Seite.

 Sobald die App verfügbar ist, sollte die folgende Anwendung angezeigt werden. Abgegebene Stimmen werden in der Azure Cosmos DB-Instanz gespeichert.

![Azure-Abstimmungsanwendung mit zwei Wahlmöglichkeiten: Katzen oder Hunde.](../media/4-azure-vote.png)

## <a name="secured-environment-variables"></a>Abgesicherte Umgebungsvariablen

In der vorherigen Übung wurde ein Container mit Verbindungsinformationen für Azure Cosmos DB erstellt, die in zwei Umgebungsvariablen gespeichert wurden. Standardmäßig werden Umgebungsvariablen im Azure-Portal und in Befehlszeilentools als Klartext angezeigt.

Wenn Sie beispielsweise mit dem Befehl `az container show` Informationen zu dem Container abrufen, der in der vorherigen Übung erstellt wurde, stehen die Umgebungsvariablen als Klartext zur Verfügung:

```azurecli
az container show --resource-group <rgn>[sandbox resource group name]</rgn> --name aci-demo --query containers[0].environmentVariables
```

Beispielausgabe:

```json
[
  {
    "name": "COSMOS_DB_ENDPOINT",
    "secureValue": null,
    "value": "https://aci-cosmos.documents.azure.com:443/"
  },
  {
    "name": "COSMOS_DB_MASTERKEY",
    "secureValue": null,
    "value": "Xm5BwdLlCllBvrR26V00000000S2uOusuglhzwkE7dOPMBQ3oA30n3rKd8PKA13700000000095ynys863Ghgw=="
  }
]
```

Abgesicherte Umgebungsvariablen verhindern die Ausgabe als Klartext. Um abgesicherte Umgebungsvariablen zu verwenden, ersetzen Sie das Argument `--environment-variables` durch das Argument `--secure-environment-variables`.

Führen Sie das folgende Beispiel aus, um einen Container mit dem Namen *aci-demo-secure* zu erstellen, der abgesicherte Umgebungsvariablen verwendet:

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --location eastus \
    --secure-environment-variables COSMOS_DB_ENDPOINT=$COSMOS_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_KEY
```

Wenn der Container nun mit dem Befehl `az container show` zurückgegeben wird, werden die Umgebungsvariablen nicht angezeigt:

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --query containers[0].environmentVariables
```

Beispielausgabe:

```json
[
  {
    "name": "COSMOS_DB_ENDPOINT",
    "secureValue": null,
    "value": null
  },
  {
    "name": "COSMOS_DB_MASTERKEY",
    "secureValue": null,
    "value": null
  }
]
```