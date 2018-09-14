Sie entscheiden, erstellen Sie ein Azure-Datenbank für PostgreSQL-Server zum Speichern von Routen, die von Runner Fitness Geräten erfasst. Basierend auf historischen erfasste Datenvolumen, wissen Sie, dass die Server-speicheranforderungen auf 20 GB festgelegt werden soll. Um Ihre verarbeitungsanforderungen zu unterstützen, müssen Sie 5 Gen-Unterstützung mit 1 virtueller Kern berechnen. Sie wissen auch, dass Sie eine Beibehaltungsdauer von 15 Tagen für datensicherungen benötigen.

Wir beginnen.

Beachten Beachten Sie möchten Ihre Größe des Serverspeichers auf 20 GB festgelegt, compute Gen 5-Unterstützung mit 1 virtueller Kern und eine Beibehaltungsdauer von 15 Tagen bei datensicherungen.

Es gibt mehrere Parameter, die Sie angeben müssen:

- `--resource-group <resource_group_name>`
- `--name <new_server_name>`
- `--location <location>`
- `--admin-user <admin_user_name>`
- `--admin-password <server_admin_password>`
- `--sku-name <sku>`
- `--storage-size <size>`
- `--backup-retention <days>`
- `--version <version_number>`

Wenn können Sie schreiben den Befehl und führen die Parameter ohne eine Betrachtung der unten beschriebenen Lösung angezeigt. Ersetzen Sie die Werte in `<>` durch Ihre eigenen Werte.

> [!NOTE]
> Sie können eine Liste mit allen Standorten, die mit dem folgenden Befehl abrufen `az account list-locations`. Wählen Sie die `displayName` oder `name` und verwenden sie für die `<location>` Parameter.

```bash
az postgres server create --resource-group <rgn>[Sandbox resource group name]</rgn> --name <unique_server_name>  --location "UK West" --admin-user <server_admin_login_id> --admin-password <server_admin_password> --sku-name B_Gen5_1 --storage-size 20480 --backup-retention 15 --version 10
```

Sie sehen, dass das System einige Zeit zum Verarbeiten der Informationen, die bei Ausführung in Anspruch nehmen. Eine Zeichenfolge von JavaScript Object Notation (JSON), die beschreibt, den Server wird zurückgegeben, wenn der Server erstellt wurde. Eine Fehlermeldung wird angezeigt, wenn der Server nicht erstellt wird. Sie müssen diese Fehlerinformationen verwenden, um zu überprüfen und beheben Sie die Befehlsparameter.

Sie haben erfolgreich einen PostgreSQL-Server mithilfe der Azure CLI erstellt. In der nächsten Einheit sehen Sie, wie Sie die Sicherheitseinstellungen Ihres Servers konfigurieren.
