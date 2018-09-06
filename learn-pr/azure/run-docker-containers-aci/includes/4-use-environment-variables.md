Das Festlegen von Umgebungsvariablen in Ihren Containerinstanzen ermöglicht Ihnen, eine dynamische Konfiguration der Anwendung oder des Skripts bereitzustellen, die bzw. das vom Container ausgeführt wird. Umgebungsvariablen werden bei der Containererstellung über die Azure CLI, PowerShell oder das Azure-Portal festgelegt. Abgesicherte Umgebungsvariablen werden zum Schutz vor der Preisgabe sensibler Informationen in der Ausgabe von Containervorgängen verwendet.

In dieser Einheit wird eine Azure Cosmos DB-Instanz erstellt. Dann wird eine Azure-Containerinstanz mit den Verbindungsinformationen der Azure Cosmos DB-Instanz ausgeführt, die als Umgebungsvariablen gespeichert sind. Eine Anwendung im Container nutzt die Variablen, um Azure Cosmos DB-Daten zu schreiben und zu lesen. In dieser Einheit erstellen Sie sowohl eine Umgebungsvariable als auch eine abgesicherte Umgebungsvariable.

## <a name="deploy-cosmose-db"></a>Bereitstellen von Cosmos DB

Erstellen Sie mithilfe des Befehls `az Azure Cosmos DB create` die Azure Cosmos DB-Instanz. Bei diesem Beispiel wird auch die Azure Cosmos DB-Endpunktadresse in einer Variablen mit dem Namen *COSMOS_DB_ENDPOINT* angegeben.

Die Ausführung dieses Befehls kann einige Minuten dauern.

```azurecli
COSMOS_DB_ENDPOINT=$(az cosmosdb create --resource-group myResourceGroup --name aci-cosmos --query documentEndpoint -o tsv)
```

Rufen Sie als Nächstes den Azure Cosmos DB-Verbindungsschlüssel mit dem Befehl `az cosmosdb list-keys` ab, und speichern Sie ihn in einer Variablen namens *COSMOS_DB_DB_MASTERKEY*.

```azurecli
COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys --resource-group myResourceGroup --name aci-cosmos --query primaryMasterKey -o tsv)
```

## <a name="deploy-container-instance"></a>Bereitstellen einer Containerinstanz

Führen Sie den Befehl `az container create` aus, um eine Azure-Containerinstanz zu erstellen. Beachten Sie, dass zwei Umgebungsvariablen erstellt werden, `COSMOS_DB_ENDPOINT` und `COSMOS_DB_ENDPOINT`. Diese Variablen enthalten die Werte, die für die Verbindung mit der Azure Cosmos DB-Instanz benötigt werden.

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name aci-demo \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --environment-variables COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
```

Nachdem der Container erstellt wurde, rufen Sie mit dem Befehl `az container show` die öffentliche IP-Adresse ab.

```azurecli
az container show --resource-group myResourceGroup --name aci-demo --query ipAddress.ip --output tsv
```

Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers. Die folgende Anwendung sollte angezeigt werden. Bei der Abgabe einer Stimme wird die Stimme in der Azure Cosmos DB-Instanz gespeichert.

![Azure-Abstimmungsanwendung mit zwei Wahlmöglichkeiten: Katzen oder Hunde.](../media-draft/azure-vote.png)

## <a name="secured-environment-variables"></a>Abgesicherte Umgebungsvariablen

In der vorherigen Übung wurde ein Container mit Verbindungsinformationen für Azure Cosmos DB erstellt, die in zwei Umgebungsvariablen gespeichert wurden. Standardmäßig werden Umgebungsvariablen im Azure-Portal und in Befehlszeilentools als Klartext angezeigt.

Wenn Sie beispielsweise mit dem Befehl `az container show` Informationen über den Container abrufen, der in der vorherigen Übung erstellt wurde, können die Umgebungsvariablen im Klartext angezeigt werden.

```azurecli
az container show --resource-group myResourceGroup --name aci-demo --query containers[0].environmentVariables
```

Beispielausgabe

```bash
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

Führen Sie das folgende Beispiel aus, um einen Container mit dem Namen *aci-demo-secure* zu erstellen, der abgesicherte Umgebungsvariablen verwendet.

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name aci-demo-secure \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --secure-environment-variables COSMOS_DB_ENDPOINT=$COSMOS_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_KEY
```

Wenn der Container nun mit dem Befehl `az container show` zurückgegeben wird, werden die Umgebungsvariablen nicht angezeigt.

```azurecli
az container show --resource-group myResourceGroup --name aci-demo-secure --query containers[0].environmentVariables
```

Beispielausgabe

```bash
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

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie eine Azure Cosmos DB-Instanz und eine Azur- Containerinstanz erstellt. Umgebungsvariablen wurden in der Containerinstanz so festgelegt, dass die im Container ausgeführte Anwendung die Verbindung mit Azure Cosmos DB herstellen konnte.

In der nächsten Lektion binden Sie Datenvolumes in eine Azure-Containerinstanz ein, um Daten dauerhaft zu speichern.
