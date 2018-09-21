Jetzt ist es an der Zeit, die App in Azure auszuführen. Sie müssen eine Azure App Service-App erstellen, sie mit einer verwalteten Identität und der Tresorkonfiguration einrichten und Code bereitstellen.

## <a name="create-the-app-service-plan-and-app"></a>Erstellen des App Service-Plans und der App

Das Erstellen einer App Service-App ist ein zweistufiger Prozess: Erstellen Sie zuerst den *Plan* und dann die *App*.

Der Name des *Plans* muss nur innerhalb Ihres Abonnements eindeutig sein. Daher können Sie den gleichen Namen wie wir verwenden: **keyvault-exercise-plan**. Der App-Name muss global eindeutig sein. Daher müssen Sie Ihren eigenen auswählen. Verwenden Sie den gleichen Speicherort, den Sie beim Erstellen Ihres Caches verwendet haben.

Führen Sie in Azure Cloud Shell Folgendes aus:

```azurecli
az appservice plan create \
    --name keyvault-exercise-plan \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
    --location eastus

az webapp create \
    --name <your-unique-app-name> \
    --plan keyvault-exercise-plan \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

## <a name="add-configuration-to-the-app"></a>Hinzufügen von Konfiguration zur App

Folgen Sie zum Bereitstellen in Azure der bewährten App Service-Methode, die VaultName-Konfiguration in eine Anwendungseinstellung anstatt in eine Konfigurationsdatei aufzunehmen. Führen Sie diesen Befehl zum Erstellen der Anwendungseinstellung aus:

```azurecli
az webapp config appsettings set \
    --name <your-unique-app-name> \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --settings VaultName=<your-unique-vault-name>
```

## <a name="enable-managed-identity"></a>Aktivieren der verwalteten Identität

Zum Aktivieren der verwalteten Identität in einer App reicht eine Zeile aus &mdash; führen Sie dies zur Aktivierung in Ihrer App aus:

```azurecli
az webapp identity assign \
    --name <your-unique-app-name> \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

Kopieren Sie aus der resultierenden JSON-Ausgabe den **principalId**-Wert. „PrincipalId“ ist die eindeutige ID der neuen Identität der App in Azure Active Directory, und wir verwenden sie im nächsten Schritt.

## <a name="grant-access-to-the-vault"></a>Gewähren von Zugriff auf den Tresor

Im letzten Schritt vor der Bereitstellung weisen Sie der verwalteten Identität Ihrer App Key Vault-Berechtigungen zu. Verwenden Sie den **principalId**-Wert, den Sie im vorherigen Schritt kopiert haben, als Wert für **object-id** im folgenden Befehl. Die Ausführung dieses Befehls gewährt **Get**- und **List**-Zugriff:

```azurecli
az keyvault set-policy \
    --name <your-unique-vault-name> \
    --object-id <your-managed-identity-principleid> \
    --secret-permissions get list
```

## <a name="deploy-the-app-and-try-it-out"></a>Bereitstellen und Testen der App

Die Konfiguration ist festgelegt, und Sie können die App jetzt bereitstellen. Mit den folgenden Befehlen wird die Site im Ordner `pub` veröffentlicht, in `site.zip` komprimiert und die ZIP-Datei in App Service bereitgestellt.

> [!NOTE]
> Sie müssen mit `cd` wieder in das Verzeichnis „KeyVaultDemoApp“ wechseln, sofern noch nicht geschehen.

```azurecli
dotnet publish -o pub
zip -j site.zip pub/*

az webapp deployment source config-zip \
    --src site.zip \
    --name <your-unique-app-name> \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

Sobald ein Ergebnis anzeigt, dass die Site bereitgestellt wurde, öffnen Sie `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in einem Browser. Der Geheimniswert **reindeer_flotilla** sollte angezeigt werden.

Ihre App ist fertig und wurde bereitgestellt.