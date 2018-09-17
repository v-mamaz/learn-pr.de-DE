Sie entscheiden sich für die Erstellung einer Azure Database for PostgreSQL-Instanz, um Routen zu speichern, die durch Fitnessgeräte von Läufern erfasst wurden. Aufgrund des Verlaufs der Erfassung von Datenvolumes wissen Sie, dass für Ihren Serverspeicher mindestens 20 GB benötigt werden. Zur Unterstützung Ihrer Verarbeitungsanforderungen ist die Unterstützung von Compute Gen 5 mit einem virtuellen Kern erforderlich. Außerdem wissen Sie, dass für Datensicherungen eine Aufbewahrungsdauer von 15 Tagen erforderlich ist.

> [!TIP]
> Alle Übungen in Microsoft Learn sind kostenlos. Wenn Sie jedoch eigenständig weitere Funktionen nutzen möchten, benötigen Sie ein Azure-Abonnement. Wenn Sie noch nicht über ein Abonnement verfügen, können Sie in wenigen Minuten ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen.

Legen wir los.

Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

Zur Erinnerung: Sie müssen eine Azure Cloud Shell-Sitzung starten. Klicken Sie auf das Cloud Shell-Symbol am oberen Bildschirmrand, um die Sitzung zu starten.

![Cloud Shell-Schaltfläche](../media-draft/cloud-shell-button.png)

Wenn Sie noch nicht über ein Speicherkonto für die Verwendung mit Cloud Shell verfügen, müssen Sie beim ersten Zugriff eines erstellen. Die Portaloberfläche führt Sie Schritt für Schritt durch die Speicherkontoerstellung.

In diesem Lab wird `bash` als Befehlszeilenumgebung verwendet.

1. Wählen Sie das Abonnement aus, das Sie zum Erstellen des Servers verwenden möchten.

    Wenn Sie über mehrere Abonnements verfügen, verwenden Sie den folgenden Befehl, um das richtige Abonnement zu aktivieren. Ersetzen Sie dabei die Nullen durch Ihre Abonnement-ID.

    ``` bash
    az account set --subscription "00000000-0000-0000-0000-000000000000"
    ```

    Zur Erinnerung: Mithilfe des Befehls `az account list --output table` können Sie alle Ihre Abonnements auflisten. Wählen Sie die gewünschte Abonnement-ID aus dieser Liste aus.

1. Erstellen Sie eine Ressourcengruppe, sofern Sie nicht bereits eine in einer vorherigen Einheit erstellt haben. Führen Sie den folgenden Befehl aus.

    ```bash
    az group create --name <resource_group_name> --location <location>
    ```

    > [!Note]
    > Mithilfe des Befehls `az account list-locations` können Sie eine Liste mit allen Standorten abrufen. Verwenden Sie den Wert `displayName` oder `name` für den Parameter `<location>`.

1. Nun können Sie den Befehl `az postgres server create` ausführen.

    Denken Sie daran, dass Sie die Speichergröße des Servers auf 20 GB festlegen, Compute Gen 5-Unterstützung mit einem virtuellen Kern konfigurieren und für Datensicherungen eine Aufbewahrungsdauer von 15 Tagen festlegen möchten.

    Dazu geben Sie mehrere Parameter an:

    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`

    Versuchen Sie, den Befehl und die Parameter zu erstellen, ohne sich die weiter unten bereitgestellte Lösung anzusehen. Ersetzen Sie die Werte in `<>` durch Ihre eigenen Werte.

    > [!NOTE]
    > Mithilfe des Befehls `az account list-locations` können Sie eine Liste mit allen Standorten abrufen. Verwenden Sie den Wert `displayName` oder `name` für den Parameter `<location>`.

    ```bash
    az postgres server create --resource-group <resource_group_name> --name <unique_server_name>  --location "UK West" --admin-user <server_admin_login_id> --admin-password <server_admin_password> --sku-name B_Gen5_1 --storage-size 20480 --backup-retention 15 --version 10
    ```

Die Verarbeitung der Informationen dauert einen Moment. Wenn der Server erstellt wurde, wird eine JSON-Zeichenfolge (Java Script Object Notation) zurückgegeben, die den Server beschreibt. Wurde der Server nicht erstellt, wird eine Fehlermeldung angezeigt. Anhand der Fehlerinformationen können Sie Ihre Befehlsparameter überprüfen und korrigieren.

Sie haben erfolgreich einen PostgreSQL-Server mithilfe der Azure-Befehlszeilenschnittstelle erstellt. In der nächsten Einheit erfahren Sie, wie Sie die Sicherheitseinstellungen Ihres Servers konfigurieren.
