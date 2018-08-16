Jetzt ist es Zeit für unsere app in Azure ausgeführt werden. Wir müssen erstellen eine App Service-app, richten sie Sie mit MSI-Datei und unseren schlüsseltresor-Konfiguration und unser Code bereitstellen.

# <a name="exercise"></a>Übung

## <a name="create-the-app-service-plan-and-app"></a>Erstellen Sie die App Service-Plan und die app

Erstellen einer App Service-app ist ein zweistufiger Prozess: Erstellen Sie zunächst die *Plan*, und klicken Sie dann die *app*.

Die *Plan* nur muss innerhalb Ihres Abonnements eindeutig sein, damit Sie den gleichen Namen verwenden können, die wir verwendet haben: **Keyvault-Übung-Plan**. Der app-Name muss global eindeutig sein, jedoch so Sie wählen Sie Ihre eigenen müssen.

Führen Sie in Cloud Shell die folgenden Schritte aus:

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

## <a name="add-configuration-to-the-app"></a>Konfiguration für die app hinzufügen

Für in Azure bereitstellen, müssen wir Konfiguration in den Anwendungseinstellungen zu platzieren, statt eine Konfigurationsdatei der App Service-Empfehlung zu folgen.

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

## <a name="enable-msi"></a>Aktivieren der MSI

Aktivieren von MSI für eine app ist eine Einzeiler:

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Kopieren Sie aus der JSON-Ausgabe, die sich ergibt, der **PrincipalId** Wert. PrincipalId ist die eindeutige ID des neuen der app-Identität in Azure Active Directory, und wir werden es im nächsten Schritt verwenden.

## <a name="grant-access-to-the-vault"></a>Gewähren des Zugriffs auf den Tresor

Nun müssen wir unsere app bereitstellen Identitätsberechtigungen abrufen und Auflisten von Geheimnissen aus die produktionsumgebung Vault. Verwenden der **PrincipalId** als Wert für aus dem vorherigen Schritt kopierten Wert **Objekt-Id** in den folgenden Befehl aus.

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-msi-principleid> --secret-permissions get list
```

## <a name="deploy-the-app-and-try-it-out"></a>Bereitstellen der app, und probieren Sie es aus

Alle unsere-Konfiguration festgelegt ist, und wir sind für die Bereitstellung bereit! Die folgenden Befehle wird den Standort veröffentlicht die `pub` Ordner komprimieren sie Sie in `site.zip`, und die ZIP-Datei in App Service bereitstellen.

> [!NOTE]
> Sie müssen `cd` zurück in das Verzeichnis KeyVaultDemoApp, sofern Sie noch nicht geschehen.

```console
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

Die Website wurde bereitgestellt, sobald Sie ein Ergebnis zu erhalten, der angibt, öffnen Sie `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest` in einem Browser. Daraufhin sollte das Geheimnis, **Reindeer_flotilla**.

Die app beendet und bereitgestellt.