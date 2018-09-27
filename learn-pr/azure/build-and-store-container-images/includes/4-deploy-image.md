Containerimages können über viele Containerverwaltungsplattformen aus Azure Container Registry abgerufen werden – etwa mit Azure Container Instances, Azure Kubernetes Registry und Docker für Windows oder Mac. Für das Ausführen von Containerimages aus Azure Container Registry können Authentifizierungsanmeldeinformationen erforderlich sein. 

Es wird empfohlen, einen Azure-Dienstprinzipal für die Authentifizierung mit Container Registry zu verwenden. Darüber hinaus empfiehlt es sich, die Anmeldeinformationen für den Azure-Dienstprinzipal in Azure Key Vault zu schützen. In dieser Einheit wenden wir die empfohlene Vorgehensweise an.

Für die Liveübung verwenden wir jedoch das integrierte Administratorkonto, das in jeder Azure Container Registry-Instanz aktiviert werden kann. Das Administratorkonto kann zusammen mit den kostenlosen Sandboxressourcen verwendet werden.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

Erstellen Sie eine Variable mit dem Namen Ihrer Containerregistrierung in Kleinbuchstaben. (Verwenden Sie also beispielsweise „meincontainer“ anstatt „MeinContainer“.) Diese Variable wird im gesamten Verlauf dieser Einheit verwendet.

```azurecli
ACR_NAME=<acrName>
```

### <a name="service-principal"></a>Dienstprinzipal

Für eine Produktionsanwendung würden wir an dieser Stelle einen Dienstprinzipal erstellen. **In der Sandboxumgebung funktioniert das nicht.** Es empfiehlt sich aber, dies in Ihren eigenen Systemen umzusetzen. Verwenden Sie für die Liveübung die nachstehenden Anweisungen zum Administratorkonto.

Zum Erstellen des Dienstprinzipals können Sie den Befehl `az ad sp create-for-rbac` verwenden. Das Argument `--role` konfiguriert den Dienstprinzipal mit der Rolle *reader* (Leser), die ihm ausschließlich Pullzugriff auf die Registrierung gewährt. Um sowohl Push- als auch Pullzugriff zu gewähren, würden Sie das Argument `--role` in *contributor* (Mitwirkender) ändern.

```azurecli
az ad sp create-for-rbac --scopes $(az acr show --name $ACR_NAME --query id --output tsv) --role reader
```

So würde die Ausgabe der Erstellung des Dienstprinzipals aussehen. Notieren Sie sich die Werte `appId` und `password`. Diese werden in Azure Key Vault gespeichert.

```output
{
  "appId": "1fa05179-0000-0000-0000-e269a4e97c41",
  "displayName": "azure-cli-2018-08-19-22-35-26",
  "name": "http://azure-cli-2018-08-19-22-35-26",
  "password": "72377509-0000-0000-0000-c8edbcb2d950",
  "tenant": "00000000-0000-0000-0000-000000000000"
}
```

### <a name="admin-account"></a>Administratorkonto

Azure-Containerregistrierungen verfügen über ein integriertes Administratorkonto. Dieses ist nicht an Azure AD oder an rollenbasierte Zugriffssteuerungen gebunden und sollte daher **nur zu Testzwecken verwendet werden**. 

1. Aktivieren Sie das Administratorkonto.
    ```azurecli
      az acr update -n $ACR_NAME --admin-enabled true
    ```

2. Abfrage zum Abrufen des automatisch generierten Benutzernamens und Kennworts

    ```azurecli
      az acr credential show --name $ACR_NAME
    ```

Die Ausgabe sieht in etwa wie folgt aus. Notieren Sie sich Folgendes: `username` und `value` in Verbindung mit `name` „password“. Diese werden später in einem Schlüsseltresor gespeichert.

```output
{  "passwords": [
    {
      "name": "password",
      "value": "aaaaa"
    },
    {
      "name": "password2",
      "value": "bbbbb"
    }
  ],
  "username": "ccccc"
}
```

### <a name="save-the-username-and-password-to-the-key-vault"></a>Speichern von Benutzername und Kennwort im Schlüsseltresor

1. Erstellen Sie mit dem Befehl `az keyvault create` eine Azure Key Vault-Instanz.

    ```azurecli
    az keyvault create --resource-group <rgn>[sandbox resource group name]</rgn> --name $ACR_NAME-keyvault
    ```

1. Verwenden Sie den Befehl `az keyvault secret set`, um den Benutzernamen für die ACR-Instanz im Tresor speichern. Bei der Nutzung von Dienstprinzipalen würden Sie die App-ID für diesen Wert verwenden. Da Sie hier das Administratorkonto verwenden, speichern Sie den Benutzernamen aus der obigen Abfrage. Geben Sie den folgenden Befehl ein, und vergessen Sie nicht, `<username>` zu ersetzen.

    ```azurecli
    az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --value <username>
    ```

1. Verwenden Sie nun den Befehl `az keyvault secret set`, um das *Kennwort* im Tresor zu speichern. Ersetzen Sie `<password>` durch `password` aus der obigen Abfrage.

    ```azurecli
    az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --value <password>
    ```

Sie haben nun einen Azure-Schlüsseltresor erstellt und zwei Geheimnisse darin gespeichert:

* `$ACR_NAME-pull-usr`: der **Benutzername** für die Containerregistrierung
* `$ACR_NAME-pull-pwd`: das **Kennwort** für die Containerregistrierung

Sie können nun anhand des Namens auf diese Geheimnisse verweisen, wenn Sie oder Ihre Anwendungen und Dienste Images per Pull aus der Registrierung abrufen.

### <a name="deploy-a-container-with-azure-cli"></a>Bereitstellen eines Containers mit Azure CLI

Jetzt, da die Anmeldeinformationen des Dienstprinzipals in Azure Key Vault gespeichert sind, können Ihre Anwendungen und Dienste diese verwenden, um auf Ihre private Registrierung zuzugreifen.

Führen Sie den folgenden `az container create`-Befehl aus, um eine Containerinstanz bereitzustellen. Der Befehl verwendet die in Azure Key Vault gespeicherten Anmeldeinformationen des Dienstprinzipals, um sich bei Ihrer Containerregistrierung zu authentifizieren.

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name acr-tasks \
    --image $ACR_NAME.azurecr.io/helloacrtasks:v1 \
    --registry-login-server $ACR_NAME.azurecr.io \
    --ip-address Public \
    --location eastus \
    --registry-username $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --query value -o tsv) \
    --registry-password $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --query value -o tsv)
```

Rufen Sie die IP-Adresse der Azure-Containerinstanz ab.

```azurecli
az container show --resource-group  <rgn>[sandbox resource group name]</rgn> --name acr-tasks --query ipAddress.ip --output table
```

Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers. Wenn alles ordnungsgemäß konfiguriert wurde, sollten jetzt die folgenden Ergebnisse angezeigt werden:

![Beispiel-Web-App mit dem Text „Hello World“](../media/hello.png)

