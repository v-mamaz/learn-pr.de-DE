Sie entscheiden sich für die Erstellung eines Azure Database for PostgreSQL-Servers, um Routen zu speichern, die durch Fitnessgeräte von Läufern erfasst wurden. Aufgrund des Verlaufs der Erfassung von Datenvolumes wissen Sie, dass für Ihren Serverspeicher mindestens 20 GB benötigt werden. Zur Unterstützung Ihrer Verarbeitungsanforderungen ist die Unterstützung von Compute Gen 5 mit einem virtuellen Kern erforderlich. Außerdem wissen Sie, dass für Datensicherungen eine Aufbewahrungsdauer von 15 Tagen erforderlich ist.

## <a name="create-an-azure-postgresql-database-with-the-azure-cli"></a>Erstellen einer Azure PostGreSQL-Datenbank mithilfe der Azure-Befehlszeilenschnittstelle

Denken Sie daran, dass Sie die Speichergröße des Servers auf 20 GB festlegen, Compute Gen 5-Unterstützung mit einem einzelnen virtuellen Kern konfigurieren und für Datensicherungen eine Aufbewahrungsdauer von 15 Tagen festlegen möchten.

1. Verwenden Sie die Methode `az postgres server create`, um die neue Datenbank zu erstellen. Dazu müssen mehrere Parameter angegeben werden:
    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`
    
2. Versuchen Sie, den Befehl und die Parameter zu erstellen, ohne sich die weiter unten bereitgestellte Lösung anzusehen. Hier sind einige Tipps.
    - Ersetzen Sie `<values>` durch Ihre eigenen Werte. 
    - Der Servername darf wie bereits erwähnt nur aus Kleinbuchstaben (a–z), Zahlen (0–9) und Bindestrichen bestehen.
    - Verwenden Sie <rgn>[Name der Sandboxressourcengruppe]</rgn> als Ressourcengruppe.
    - Verwenden Sie einen Standort aus der folgenden Liste: [!include[](../../../includes/azure-sandbox-regions-note.md)]
    
```bash
az postgres server create --name <unique_server_name> \
    --resource-group <rgn>[sandbox resource group name]</rgn> \ 
    --location eastus \
    --sku-name B_Gen5_1 \
    --storage-size 20480 \
    --backup-retention 15 \
    --version 10 \
    --admin-user <admin_user_name> \
    --admin-password <server_admin_password>
```

Die Verarbeitung der Informationen durch das System dauert einen Moment. Warten Sie, bis der Befehl ausgeführt wurde.

Anschließend wird eine JSON-Zeichenfolge (JavaScript Object Notation) zurückgegeben, die den Server beschreibt. Sollte ein Fehler aufgetreten sein, wird eine Fehlermeldung angezeigt. Anhand der Fehlerinformationen können Sie Ihre Befehlsparameter überprüfen, den Fehler korrigieren und den Vorgang erneut ausführen.

Das JSON-Objekt sieht in etwa wie folgt aus:

```json
{
  "administratorLogin": "azureuser",
  "earliestRestoreDate": "2018-09-17T00:35:50.170000+00:00",
  "fullyQualifiedDomainName": "secondserver8.postgres.database.azure.com",
  "id": "/subscriptions/xxxxx/resourceGroups/<rgn>[sandbox Resource Group]</rgn>/providers/Microsoft.DBforPostgreSQL/servers/secondserver8",
  "location": "eastus",
  "name": "secondserver8",
  "resourceGroup": "<rgn>[sandbox Resource Group]</rgn>",
  "sku": {
    "capacity": 1,
    "family": "Gen5",
    "name": "B_Gen5_1",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": "Enabled",
  "storageProfile": {
    "backupRetentionDays": 15,
    "geoRedundantBackup": "Disabled",
    "storageMb": 20480
  },
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "10"
}
```

Sie haben erfolgreich einen PostgreSQL-Server mithilfe der Azure-Befehlszeilenschnittstelle erstellt. In der nächsten Einheit erfahren Sie, wie Sie die Sicherheitseinstellungen Ihres Servers konfigurieren.
