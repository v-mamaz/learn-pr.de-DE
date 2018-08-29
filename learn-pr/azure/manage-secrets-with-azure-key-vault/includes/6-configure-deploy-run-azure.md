Jetzt ist es an der Zeit, dass unsere App in Azure ausgeführt wird. Wir müssen eine Azure App Service-App erstellen, sie mit der MSI und unserer Tresorkonfiguration einrichten und Code bereitstellen.

## <a name="exercise"></a>Übung

### <a name="create-the-app-service-plan-and-app"></a>Erstellen des App Service-Plans und der App

Das Erstellen einer App Service-App ist ein zweistufiger Prozess: Erstellen Sie zuerst den *Plan* und dann die *App*.

Der Name des *Plans* muss nur innerhalb Ihres Abonnements eindeutig sein. Daher können Sie den gleichen Namen wie wir verwenden: **keyvault-exercise-plan**. Der App-Name muss global eindeutig sein. Daher müssen Sie Ihren eigenen auswählen.

Führen Sie in Azure Cloud Shell Folgendes aus:

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

### <a name="add-configuration-to-the-app"></a>Hinzufügen der Konfiguration zur App

Zum Bereitstellen in Azure folgen wir der bewährten App Service-Methode, die Konfiguration in die Anwendungseinstellungen aufzunehmen, statt eine Konfigurationsdatei zu verwenden.

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

### <a name="enable-msi"></a>Aktivieren der MSI

Die MSI wird für eine App mit einer Zeile aktiviert:

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Kopieren Sie aus der resultierenden JSON-Ausgabe den **principalId**-Wert. „PrincipalId“ ist die eindeutige ID der neuen Identität der App in Azure Active Directory, und wir verwenden sie im nächsten Schritt.

### <a name="grant-access-to-the-vault"></a>Gewähren von Zugriff auf den Tresor

Nun müssen Sie Ihrer App Identitätsberechtigungen erteilen, um Geheimnisse aus Ihrem Tresor für die Produktionsumgebung abzurufen und aufzulisten. Verwenden Sie den **principalId**-Wert, den Sie im vorherigen Schritt kopiert haben, als Wert für **object-id** im folgenden Befehl.

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

### <a name="deploy-the-app-and-try-it-out"></a>Bereitstellen und Testen der App

Die Konfiguration ist festgelegt, und Sie können die App jetzt bereitstellen. Mit den folgenden Befehlen wird die Site im Ordner `pub` veröffentlicht, in `site.zip` komprimiert und die ZIP-Datei in App Service bereitgestellt.

> [!NOTE]
> Sie müssen mit `cd` wieder in das Verzeichnis „KeyVaultDemoApp“ wechseln, sofern noch nicht geschehen.

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Sobald ein Ergebnis anzeigt, dass die Site bereitgestellt wurde, öffnen Sie `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in einem Browser. Der Geheimniswert **reindeer_flotilla** sollte angezeigt werden.

Ihre App ist fertig und wurde bereitgestellt.