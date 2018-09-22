Angenommen, Sie arbeiten mit einer lokalen PostgreSQL-Datenbank. Ihr Unternehmen plant jetzt, die Geräteunterstützung, Verfügbarkeit, Datennachverfolgung und Verarbeitungsfunktionen zu erweitern, indem Ihr Server in Azure verschoben wird. Sie untersuchen, wie hoch der Aufwand für das Automatisieren der Erstellung eines Azure Database for PostgreSQL-Servers ist.

Das Erstellen eines einzelnen Azure Database for PostgreSQL-Servers mit dem Azure-Portal ist einfach. Das Erstellen mehrerer Datenbanken und das Ausführen der laufenden Wartung ausschließlich mit dem Portal kann mühsam werden. Sie verwenden die Azure CLI, um Skripts zu erstellen, wenn Sie Verwaltungsaufgaben automatisieren möchten.

Die Erstellung nahezu aller Ressourcen in Microsoft Azure kann per Azure CLI automatisiert werden. In dieser Einheit erfahren Sie, wie Sie die Verwaltung Ihrer Azure Database for PostgreSQL-Server mit der Azure CLI automatisieren.

## <a name="what-is-the-azure-cli"></a>Was ist die Azure CLI?

Die [Azure CLI](https://docs.microsoft.com/cli/azure/) (Azure-Befehlszeilenschnittstelle) ist die plattformübergreifende Befehlszeilenumgebung von Microsoft zum Verwalten von Azure-Ressourcen. Sie können die Azure CLI in Ihrem Browser mit Azure Cloud Shell verwenden oder die Azure CLI unter Mac OS X, Linux oder Windows lokal installieren. Die Azure CLI wird mit Bash oder PowerShell über eine lokale Befehlszeile ausgeführt. Für die lokale Ausführung der Azure CLI ist ein zusätzliches Setup erforderlich. Wir verwenden Azure Cloud Shell, um Azure CLI-Befehle auszuführen.

## <a name="what-is-azure-cloud-shell"></a>Was ist Azure Cloud Shell?

Azure Cloud Shell ist eine browserbasierte Shell, die in der Cloud gehostet wird und es Ihnen ermöglicht, über eine authentifizierte Sitzung eine Verbindung mit Azure herzustellen. Sie können die Azure CLI-Befehle ausführen, um die Verwaltung einer Azure Database for PostgreSQL-Instanz zu automatisieren. Allgemeine Azure CLI-Tools sind in Cloud Shell vorinstalliert und für die Verwendung mit Ihrem Konto konfiguriert.

> [!NOTE]
> Für Cloud Shell ist eine Azure-Speicherressource erforderlich, damit Sie bei der Arbeit in Cloud Shell die erstellten Dateien aufbewahren können. Beim ersten Start werden Sie von Cloud Shell darauf hingewiesen, dass für Sie eine Ressourcengruppe, ein Speicherkonto und eine Azure Files-Freigabe erstellt werden. Dieser Schritt ist nur ein Mal erforderlich. Die Komponenten werden für alle zukünftigen Cloud Shell-Sitzungen automatisch angefügt.

## <a name="create-an-azure-database-for-postgresql-server-using-the-azure-cli"></a>Erstellen eines Azure Database for PostgreSQL-Servers mit der Azure CLI

Sie verwenden das Azure Cloud Shell-Terminal auf der rechten Seite, um einen Azure Database for PostgreSQL-Server über die Azure CLI zu erstellen.

Die Azure CLI-Hilfe zum Befehl für die Servererstellung mit allen verfügbaren Parametern sieht wie im folgenden Beispiel aus:

```azurecli
az postgres server create [-h] [--verbose] [--debug]
                            [--output {json,jsonc,table,tsv}]
                            [--query JMESPATH]
                            --resource-group RESOURCE_GROUP_NAME --name SERVER_NAME
                            --sku-name SKU_NAME [--location LOCATION]
                            --admin-user ADMINISTRATOR_LOGIN
                            [--admin-password ADMINISTRATOR_LOGIN_PASSWORD]
                            [--backup-retention BACKUP_RETENTION]
                            [--geo-redundant-backup GEO_REDUNDANT_BACKUP]
                            [--ssl-enforcement {Enabled,Disabled}]
                            [--storage-size STORAGE_MB]
                            [--tags [TAGS [TAGS ...]]]
                            [--version VERSION]
                            [--subscription _SUBSCRIPTION]

```

Die optionalen Parameter werden in Klammern eingeschlossen. Untersuchen wir einige dieser Parameter.

### <a name="parameters"></a>Parameter

Mit dem Parameter `--resource-group <resource_group_name>` wird die Ressourcengruppe angegeben, in der der Server erstellt werden soll.

Die Elemente `admin-user` und `admin-password` für den Server, die Sie angeben, werden für die Anmeldung am Server und den zugehörigen Datenbanken benötigt. Es ist ratsam, dass Sie sich diese Informationen für die spätere Interaktion mit dem Server merken bzw. notieren.

Sie verwenden den Parameter `--sku-name`, um einen Teil des Tarifs anzugeben. In diesem Fall ist dies die Computeressource. Für den Wert wird die Konvention `{pricing tier}_{compute generation}_{vCores}` verwendet.

Beispiele:

- `--sku-name B_Gen4_4` ist „Basic“, „Gen 4“ und „4 V-Kerne“ zugeordnet.
- `--sku-name GP_Gen5_32` ist „Universell“, „Gen 5“ und „32 V-Kerne“ zugeordnet.
- `--sku-name MO_Gen5_2` ist „Arbeitsspeicheroptimiert“, „Gen 5“ und „2 V-Kerne“ zugeordnet.

Zur Erinnerung: Die drei Tarife wurden in der Einheit beschrieben, in der wir mit dem Portal den Server erstellt haben.

Angenommen, Sie möchten eine Computeressource vom Typ „Basic, Gen 5, 1 V-Kern“ verwenden. In diesem Fall geben Sie für den Parameter `--sku-name B_Gen5_1` an.

Sie verwenden den Parameter `--storage-size`, um einen Teil des Tarifs anzugeben. Wenn der Wert nicht angegeben wird, wird standardmäßig 5.120 MB verwendet. Die gültigen Speichergrößen reichen von 5.120 MB in Inkrementen von 1.024 MB bis 1.048.576 MB.

Der Parameter `--backup-retention` wird verwendet, wenn Sie den Aufbewahrungszeitraum für Sicherungen (in Tagen) angeben müssen. Wenn der Wert nicht angegeben wird, werden standardmäßig sieben Tage verwendet.

Sie verwenden den Parameter `--version`, um die gewünschte Hauptversion von PostgreSQL anzugeben.

Sie haben nun die Schritte kennengelernt, mit denen Sie mit der Azure CLI einen Azure Database for PostgreSQL-Server erstellen. In der nächsten Einheit erstellen Sie mit der Azure CLI einen Azure Database for PostgreSQL-Server.