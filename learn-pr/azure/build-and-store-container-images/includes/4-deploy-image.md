Containerimages können über viele Containerverwaltungsplattformen aus Azure Container Registry abgerufen werden, z.B. Azure Container Instances, Azure Kubernetes Registry und Docker für Windows oder Mac. Für das Ausführen von Containerimages aus Azure Container Registry können Authentifizierungsanmeldeinformationen erforderlich sein. Es wird empfohlen, einen Azure-Dienstprinzipal für die Authentifizierung mit Container Registry zu verwenden. Darüber hinaus wird ebenfalls empfohlen, die Anmeldeinformationen für den Azure-Dienstprinzipal in Azure Key Vault zu schützen.

In dieser Einheit erstellen Sie einen Dienstprinzipal für die Azure-Containerregistrierung, speichern diesen in Azure Key Vault und stellen dann den Container mithilfe der Anmeldeinformationen des Dienstprinzipals in Azure Container Instances bereit.

## <a name="configure-registry-authentication"></a>Konfigurieren der Authentifizierung der Registrierung

Für alle Produktionsszenarios sollten Dienstprinzipale für den Zugriff auf eine Azure-Containerregistrierung verwendet werden. Mit Dienstprinzipalen können Sie die rollenbasierte Zugriffssteuerung für Ihre Containerimages bereitstellen. Beispielsweise können Sie einen Dienstprinzipal mit ausschließlichem Pullzugriff auf eine Registrierung konfigurieren.

Wenn Sie noch keinen Tresor in Azure Key Vault haben, erstellen Sie einen mit Azure CLI und den folgenden Befehlen.

Erstellen Sie zunächst eine Variable mit dem Namen Ihrer Containerregistrierung. Diese Variable wird im gesamten Verlauf dieser Einheit verwendet.

```azurecli
ACR_NAME=<acrName>
```

Erstellen Sie mit dem Befehl `az keyvault create` einen Azure-Schlüsseltresor.

```azurecli
az keyvault create --resource-group myResourceGroup --name $ACR_NAME-keyvault
```

Nun müssen Sie einen Dienstprinzipal erstellen und dessen Anmeldeinformationen in Ihrem Schlüsseltresor speichern.

Verwenden Sie den Befehl `az ad sp create-for-rbac`, um den Dienstprinzipal zu erstellen. Das Argument `--role` konfiguriert den Dienstprinzipal mit der Rolle *reader* (Leser), die ihm ausschließlich Pullzugriff auf die Registrierung gewährt. Ändern Sie das Argument `--role` in *contributor* (Mitwirkender), um sowohl Push- als auch Pullzugriff zu gewähren.

```azurecli
az ad sp create-for-rbac --scopes $(az acr show --name $ACR_NAME --query id --output tsv) --role reader
```

So würde die Ausgabe der Erstellung des Dienstprinzipals aussehen. Notieren Sie sich die Werte `appId` und `password`. Diese werden im Azure-Schlüsseltresor gespeichert.

```output
{
  "appId": "1fa05179-0000-0000-0000-e269a4e97c41",
  "displayName": "azure-cli-2018-08-19-22-35-26",
  "name": "http://azure-cli-2018-08-19-22-35-26",
  "password": "72377509-0000-0000-0000-c8edbcb2d950",
  "tenant": "00000000-0000-0000-0000-000000000000"
}
```

Verwenden Sie als Nächstes den `az keyvault secret set`-Befehl, um die *App-ID* des Dienstprinzipals im Tresor zu speichern. Ersetzen Sie `<appId>` durch die `appId` des Dienstprinzipals.

```azurecli
az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --value <appId>
```

Verwenden Sie jetzt den Befehl `az keyvault secret set`, um das *Kennwort* des Dienstprinzipals im Schlüsseltresor zu speichern. Ersetzen Sie `<password>` durch die `password` des Dienstprinzipals.

```azurecli
az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --value <password>
```

Sie haben einen Azure-Schlüsseltresor erstellt und zwei Geheimnisse in diesem gespeichert:

* `$ACR_NAME-pull-usr`: Die Dienstprinzipal-ID für die Verwendung als **Benutzername** für die Containerregistrierung.
* `$ACR_NAME-pull-pwd`: Das Kennwort des Dienstprinzipals für die Verwendung als **Kennwort** für die Containerregistrierung.

Sie können nun anhand des Namens auf diese Geheimnisse verweisen, wenn Sie oder Ihre Anwendungen und Dienste Images per Pull aus der Registrierung abrufen.

### <a name="deploy-a-container-with-azure-cli"></a>Bereitstellen eines Containers mit Azure CLI

Jetzt, da die Anmeldeinformationen des Dienstprinzipals in Azure Key Vault gespeichert sind, können Ihre Anwendungen und Dienste diese verwenden, um auf Ihre private Registrierung zuzugreifen.

Führen Sie den folgenden `az container create`-Befehl aus, um eine Containerinstanz bereitzustellen. Der Befehl verwendet die in Azure Key Vault gespeicherten Anmeldeinformationen des Dienstprinzipals, um sich bei Ihrer Containerregistrierung zu authentifizieren.

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name acr-build \
    --image $ACR_NAME.azurecr.io/helloacrbuild:v1 \
    --registry-login-server $ACR_NAME.azurecr.io \
    --ip-address Public \
    --registry-username $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --query value -o tsv) \
    --registry-password $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --query value -o tsv)
```

Rufen Sie die IP-Adresse der Azure-Containerinstanz ab.

```azurecli
az container show --resource-group myResourceGroup --name acr-build --query ipAddress.ip --output table
```

Öffnen Sie einen Browser, und navigieren Sie zur IP-Adresse des Containers. Wenn alles ordnungsgemäß konfiguriert wurde, sollten jetzt die folgenden Ergebnisse angezeigt werden:

![Beispiel-Web-App mit dem Text „Hello World“](../media/hello.png)

