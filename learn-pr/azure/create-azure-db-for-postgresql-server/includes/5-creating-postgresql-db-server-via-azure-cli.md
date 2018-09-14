Nehmen wir an, dass Sie eine lokale PostgreSQL-Datenbank verwenden. Ihr Unternehmen ist Betrachtung jetzt Unterstützung für Geräte, Verfügbarkeit, Überwachung der Daten und Verarbeitungsfunktionen durch das Verschieben Ihrer Server in Azure erweitern. Sie müssen untersuchen, wie viel Aufwand dauert um die Erstellung eines Azure Database for PostgreSQL-Server zu automatisieren.

Erstellen einen einzelnen Azure-Datenbank für PostgreSQL-Server mithilfe von Azure-Portal ist einfach. Erstellen von mehr als eine Datenbank und Ausführen von laufenden Wartung, die über die nur das Portal können mühsam werden. Verwenden Sie die Azure-Befehlszeilenschnittstelle zum Erstellen von Skripts, wenn Sie Verwaltungsaufgaben automatisieren möchten.

Erstellen fast jede Ressource in Microsoft Azure kann mithilfe der Azure CLI automatisiert werden. In dieser Einheit erfahren Sie, wie Sie zum Automatisieren der Verwaltung Ihrer Azure-Datenbank für PostgreSQL-Server mithilfe der Azure CLI.

## <a name="what-is-the-azure-cli"></a>Was ist Azure CLI?

Die [Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/cli/azure/) ist Microsofts plattformübergreifende befehlszeilenumgebung für die Verwaltung von Azure-Ressourcen. Sie können die Azure-Befehlszeilenschnittstelle in Ihrem Browser mit Azure Cloud Shell verwenden, oder Sie können die Azure-Befehlszeilenschnittstelle lokal installieren, auf Mac OS X, Linux oder Windows. Der Azure-Befehlszeilenschnittstelle, die von einer lokalen Befehlszeile aus mithilfe von Bash oder PowerShell ausgeführt wird. Der Azure CLI lokal ausführen, ist zusätzliche Konfigurationsschritte erforderlich. Wir verwenden Azure Cloud Shell, für die Azure CLI-Befehle ausführen.

## <a name="what-is-azure-cloud-shell"></a>Was ist Azure Cloud Shell?

Azure Cloud Shell ist eine browserbasierte Shell-Oberfläche, die in der Cloud gehostet wird, und können Sie in Azure mithilfe einer authentifizierten Sitzungs verbinden. Sie können die Azure CLI-Befehle zur Automatisierung der Verwaltung eines Azure Database for PostgreSQL-Server ausführen. Allgemeine Azure CLI-Tools sind bereits installiert und konfiguriert, die in Cloud Shell für Sie mit Ihrem Konto verwenden.

> [!NOTE]
> Cloudshell muss eine Azure Storage-Ressource, alle Dateien beizubehalten, die Sie bei der Arbeit in Cloud Shell erstellen. Beim ersten Start fordert Cloud Shell zum Erstellen einer Ressourcengruppe, die Storage-Konto und Azure Files-Freigabe in Ihrem Namen. Dies ist ein Einmaliger Schritt, und wird für alle zukünftigen Cloud Shell-Sitzungen automatisch angefügt werden.

## <a name="create-an-azure-database-for-postgresql-server-using-the-azure-cli"></a>Erstellen eines Azure Database for PostgreSQL-Server mithilfe der Azure-Befehlszeilenschnittstelle

Verwenden Sie das Azure Cloud Shell-Terminal auf der rechten Seite eines Azure Database for PostgreSQL-Server mithilfe von Azure-Befehlszeilenschnittstelle erstellen.

Der Azure-Befehlszeilenschnittstelle Server Erstellung Nutzung Hilfe zum Befehl zeigt alle verfügbaren Parameter sieht wie im folgenden Beispiel aus:

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

Die folgende Befehlszeile wird der erforderliche Satz von Parametern zum Erstellen eines Azure Database for PostgreSQL-Server. Sie werden feststellen, dass einige Parameter optional sind und werden nicht aufgeführt.

   ```azurecli
   az postgres server create --resource-group <resource_group_name> --name <new_server_name> --admin-user <admin_user_name> --admin-password <server_admin_password> --sku-name <sku> --version <version_number>  --location <region_name> --storage-size <size> --backup-retention <days>
   ```

### <a name="parameter-descriptions"></a>Beschreibungen der Parameter

Die `--resource-group <resource_group_name>` Parameter gibt an, die Ressourcengruppe, in dem der Server erstellen.

Der Server `admin-user` und `admin-password` die Angabe ist erforderlich, um die Anmeldung mit dem Server und seine Datenbanken. Denken Sie daran, oder notieren Sie diese Informationen später bei der Interaktion mit dem neuen Server.

Sie verwenden die `--sku-name` Parameter Geben Sie einen Teil des Tarifs fest, in diesem Fall, rechen-Ressource. Der Wert folgt der Konvention `{pricing tier}_{compute generation}_{vCores}`.

Beispiele:

- `--sku-name B_Gen4_4` ist „Basic“, „Gen 4“ und „4 V-Kerne“ zugeordnet.
- `--sku-name GP_Gen5_32` ist „Universell“, „Gen 5“ und „32 V-Kerne“ zugeordnet.
- `--sku-name MO_Gen5_2` ist „Arbeitsspeicheroptimiert“, „Gen 5“ und „2 V-Kerne“ zugeordnet.

Denken Sie daran, dass die drei Tarife in die Einheit erläutert, in dem wir den Server über das Portal erstellt.

Nehmen wir an Sie eine einfache, Gen 5 verwenden möchten, und 1 vCore-computeressource. Geben Sie den Parameter als `--sku-name B_Gen5_1`.

Sie verwenden die `--storage-size` Parameter, um Teil des Tarifs anzugeben. Wenn der Wert nicht angegeben ist, wird standardmäßig dann 5.120 MB. Gültiger speicherkontoname Größen reichen von 5.120 MB und in Schritten von 1.024 MB erhöht, bis zu 1.048.576 MB.

Die `--backup-retention` Parameter wird verwendet, wenn müssen Sie die Beibehaltungsdauer für Sicherungen angeben, der in Tagen angegeben ist. Wenn der Wert nicht angegeben ist, wird standardmäßig klicken Sie dann auf sieben Tage.

Sie verwenden die `--version` Parameter, um die Hauptversion von PostgreSQL anzugeben, die Sie verwenden möchten.

Sie haben nun die Schritte zum Erstellen eines Azure Database for PostgreSQL-Server mithilfe der Azure-Befehlszeilenschnittstelle gesehen. In der nächsten Einheit erstellen Sie einen Azure Database for PostgreSQL-Server mithilfe der Azure-Befehlszeilenschnittstelle.