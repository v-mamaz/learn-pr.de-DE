<span data-ttu-id="6420c-101">Sie entscheiden sich für die Erstellung eines Azure Database for PostgreSQL-Servers, um Routen zu speichern, die durch Fitnessgeräte von Läufern erfasst wurden.</span><span class="sxs-lookup"><span data-stu-id="6420c-101">You decide to create an Azure Database for PostgreSQL server to store routes captured from runners' fitness devices.</span></span> <span data-ttu-id="6420c-102">Aufgrund des Verlaufs der Erfassung von Datenvolumes wissen Sie, dass für Ihren Serverspeicher mindestens 20 GB benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="6420c-102">Based on historic captured data volumes, you know your server storage requirements should be set at 20 GB.</span></span> <span data-ttu-id="6420c-103">Zur Unterstützung Ihrer Verarbeitungsanforderungen ist die Unterstützung von Compute Gen 5 mit einem virtuellen Kern erforderlich.</span><span class="sxs-lookup"><span data-stu-id="6420c-103">To support your processing requirements, you need compute Gen 5 support with 1 vCore.</span></span> <span data-ttu-id="6420c-104">Außerdem wissen Sie, dass für Datensicherungen eine Aufbewahrungsdauer von 15 Tagen erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="6420c-104">You also know that you require a retention period of 15 days for data backups.</span></span>

## <a name="create-an-azure-postgresql-database-with-the-azure-cli"></a><span data-ttu-id="6420c-105">Erstellen einer Azure PostGreSQL-Datenbank mithilfe der Azure-Befehlszeilenschnittstelle</span><span class="sxs-lookup"><span data-stu-id="6420c-105">Create an Azure PostGreSQL database with the Azure CLI</span></span>

<span data-ttu-id="6420c-106">Denken Sie daran, dass Sie die Speichergröße des Servers auf 20 GB festlegen, Compute Gen 5-Unterstützung mit einem einzelnen virtuellen Kern konfigurieren und für Datensicherungen eine Aufbewahrungsdauer von 15 Tagen festlegen möchten.</span><span class="sxs-lookup"><span data-stu-id="6420c-106">Keep in mind you want to set your server storage size at 20 GB, compute Gen 5 support with 1 vCore and a retention period of 15 days for data backups.</span></span>

1. <span data-ttu-id="6420c-107">Verwenden Sie die Methode `az postgres server create`, um die neue Datenbank zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6420c-107">Use the `az postgres server create` method to create a new database.</span></span> <span data-ttu-id="6420c-108">Dazu müssen mehrere Parameter angegeben werden:</span><span class="sxs-lookup"><span data-stu-id="6420c-108">There are several parameters that you'll specify:</span></span>
    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`
    
2. <span data-ttu-id="6420c-109">Versuchen Sie, den Befehl und die Parameter zu erstellen, ohne sich die weiter unten bereitgestellte Lösung anzusehen.</span><span class="sxs-lookup"><span data-stu-id="6420c-109">See if you can build the command and complete the parameters without looking at the solution below.</span></span> <span data-ttu-id="6420c-110">Hier sind einige Tipps.</span><span class="sxs-lookup"><span data-stu-id="6420c-110">Here are some tips.</span></span>
    - <span data-ttu-id="6420c-111">Ersetzen Sie `<values>` durch Ihre eigenen Werte.</span><span class="sxs-lookup"><span data-stu-id="6420c-111">Replace the `<values>` with your own values.</span></span> 
    - <span data-ttu-id="6420c-112">Der Servername darf wie bereits erwähnt nur aus Kleinbuchstaben (a–z), Zahlen (0–9) und Bindestrichen bestehen.</span><span class="sxs-lookup"><span data-stu-id="6420c-112">Remember that the server name must be  made up of lowercase letters 'a'-'z', the numbers 0-9 and the hyphen.</span></span>
    - <span data-ttu-id="6420c-113">Verwenden Sie <rgn>[Sandbox-Ressourcengruppenname]</rgn> als Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="6420c-113">Use <rgn>[Sandbox resource group name]</rgn> as the resource group.</span></span>
    - <span data-ttu-id="6420c-114">Verwenden Sie einen Standort aus der folgenden Liste: [!include[](../../../includes/azure-sandbox-regions-note.md)]</span><span class="sxs-lookup"><span data-stu-id="6420c-114">Use a location from the following list:   [!include[](../../../includes/azure-sandbox-regions-note.md)]</span></span>
    
```bash
az postgres server create --name <unique_server_name> \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \ 
    --location eastus \
    --sku-name B_Gen5_1 \
    --storage-size 20480 \
    --backup-retention 15 \
    --version 10 \
    --admin-user <admin_user_name> \
    --admin-password <server_admin_password>
```

<span data-ttu-id="6420c-115">Die Verarbeitung der Informationen durch das System dauert einen Moment.</span><span class="sxs-lookup"><span data-stu-id="6420c-115">The system will take a few moments to process the information when executed.</span></span> <span data-ttu-id="6420c-116">Warten Sie, bis der Befehl ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="6420c-116">Go ahead and wait for the command to complete.</span></span>

<span data-ttu-id="6420c-117">Anschließend wird eine JSON-Zeichenfolge (JavaScript Object Notation) zurückgegeben, die den Server beschreibt.</span><span class="sxs-lookup"><span data-stu-id="6420c-117">Once it's done, a JavaScript Object Notation (JSON) string that describes the server is returned.</span></span> <span data-ttu-id="6420c-118">Sollte ein Fehler aufgetreten sein, wird eine Fehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6420c-118">If there was a failure, an error message is displayed.</span></span> <span data-ttu-id="6420c-119">Anhand der Fehlerinformationen können Sie Ihre Befehlsparameter überprüfen, den Fehler korrigieren und den Vorgang erneut ausführen.</span><span class="sxs-lookup"><span data-stu-id="6420c-119">You can use this error information to review and fix your command parameters and try again.</span></span>

<span data-ttu-id="6420c-120">Das JSON-Objekt sieht in etwa wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="6420c-120">The JSON object will look something like:</span></span>

```json
{
  "administratorLogin": "azureuser",
  "earliestRestoreDate": "2018-09-17T00:35:50.170000+00:00",
  "fullyQualifiedDomainName": "secondserver8.postgres.database.azure.com",
  "id": "/subscriptions/xxxxx/resourceGroups/<rgn>[Sandbox Resource Group]</rgn>/providers/Microsoft.DBforPostgreSQL/servers/secondserver8",
  "location": "eastus",
  "name": "secondserver8",
  "resourceGroup": "<rgn>[Sandbox Resource Group]</rgn>",
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

<span data-ttu-id="6420c-121">Sie haben erfolgreich einen PostgreSQL-Server mithilfe der Azure-Befehlszeilenschnittstelle erstellt.</span><span class="sxs-lookup"><span data-stu-id="6420c-121">You've successfully created a PostgreSQL server using the Azure CLI.</span></span> <span data-ttu-id="6420c-122">In der nächsten Einheit erfahren Sie, wie Sie die Sicherheitseinstellungen Ihres Servers konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="6420c-122">In the next unit, you'll see how to configure your server's security settings.</span></span>
