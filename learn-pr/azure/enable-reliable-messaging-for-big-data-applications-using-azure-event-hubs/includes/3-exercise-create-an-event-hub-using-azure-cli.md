Sie können nun einen neuen Event Hub erstellen. Nachdem der Event Hub erstellt wurde, verwenden Sie das Azure-Portal, um Ihren neuen Hub anzuzeigen.

Erstellen Sie einen Event Hub mit Azure CLI. Verwenden Sie für diese Übung Azure CLI 2.0. 

## <a name="create-an-event-hubs-namespace"></a>Erstellen eines Event Hubs-Namespace

Mit den folgenden Schritten können Sie einen Event Hubs-Namespace mithilfe der von Azure Cloud Shell unterstützten Bash-Shell erstellen.

1. Melden Sie sich bei Cloud Shell (Bash) an.  

1. Erstellen Sie mithilfe des folgenden Befehls eine Azure-Ressourcengruppe.

    ```azurecli
        az group create --name <resource group name> --location <location>
    ```

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |--name (erforderlich)      |Geben Sie einen neuen Namen für die Ressourcengruppe ein.|
    |--location (erforderlich)     |Geben Sie den Standort Ihres nächsten Azure-Rechenzentrums an, z.B. „westus“.|

1. Erstellen Sie mit dem folgenden Befehl den Event Hubs-Namespace:

    ```azurecli
        az eventhubs namespace create --name <Event Hubs namespace name> --resource-group <resource group name> -l <location>
    ```

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |--name (erforderlich)      |Geben Sie Ihrem Event Hubs-Namespace einen eindeutigen Namen, der zwischen 6 und 50 Zeichen lang ist. Der Name darf nur Buchstaben, Zahlen und Bindestriche enthalten. Er muss zudem mit einem Buchstaben beginnen und mit einem Buchstaben oder einer Zahl enden.|
    |--resource-group (erforderlich)  |Geben Sie die Ressourcengruppe ein, die Sie in Schritt 1 erstellt haben.
    |--l (optional)     |Geben Sie den Standort Ihres nächsten Azure-Rechenzentrums an, z.B. „westus“.|

1. Rufen Sie die Verbindungszeichenfolge für Ihren Event Hubs-Namespace mithilfe des folgenden Befehls ab. Sie benötigen diese, wenn Sie Anwendungen zum Senden und Empfangen von Nachrichten über Ihren Event Hub konfigurieren.

    ```azurecli
        az eventhubs namespace authorization-rule keys list --resource-group <resource group name> --namespace-name <EventHub namespace name> --name RootManageSharedAccessKey
    ```

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |--resource-group (erforderlich)  |Geben Sie die Ressourcengruppe ein, die Sie in Schritt 1 erstellt haben.|
    |--namespace-name (erforderlich)      |Geben Sie den Namespace ein, den Sie in Schritt 2 erstellt haben.|

    Dieser Befehl gibt die Verbindungszeichenfolge für Ihren Event Hubs-Namespace zurück, den Sie später zum Konfigurieren Ihrer Herausgeber- und Consumeranwendungen verwenden. Speichern Sie den Wert der folgenden Schlüssel für den späteren Gebrauch.

    - **primaryConnectionString**
    - **primaryKey**

## <a name="create-an-event-hub"></a>Erstellen eines Event Hubs

Führen Sie die folgenden Schritte aus, um Ihren neuen Event Hub zu erstellen:

1. Erstellen Sie einen neuen Event Hub über den folgenden Befehl:

    ```azurecli
        az eventhubs eventhub create --name <event hub name> --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name>
    ```

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |--name (erforderlich)  |Geben Sie einen Namen für Ihren Event Hub ein.|
    |--resource-group (erforderlich)  |Geben Sie die Ressourcengruppe ein, die Sie im vorherigen Abschnitt erstellt haben.|
    |--namespace-name (erforderlich)      |Geben Sie den Namespace ein, den Sie im vorherigen Abschnitt erstellt haben.|

1. Zeigen Sie über folgenden Befehl die Informationen Ihres Event Hubs an: 

    ```azurecli
        az eventhubs eventhub show --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name> --name <event hub name>
    ```

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |--resource-group (erforderlich)  |Geben Sie die Ressourcengruppe ein, die Sie im vorherigen Abschnitt erstellt haben.|
    |--namespace-name (erforderlich)      |Geben Sie den Namespace ein, den Sie im vorherigen Abschnitt erstellt haben.|
    |--name (erforderlich)|Geben Sie den Namen des Event Hubs ein, den Sie in Schritt 1 erstellt haben.|

## <a name="view-the-event-hub-in-the-azure-portal"></a>Anzeigen des Event Hubs im Azure-Portal

Befolgen Sie diese Schritte, um Ihren Event Hub im Azure-Portal anzuzeigen.

1. Suchen Sie über die Suchleiste am oberen Rand des [Azure-Portals](https://portal.azure.com?azure-portal=true) nach Ihrem Event Hubs-Namespace.

1. Klicken Sie auf den Namespace, um ihn zu öffnen.

1. Klicken Sie auf den **Event Hubs-Namespace** > **ENTITÄTEN** und dann auf **Event Hubs**.
    Ihr Event Hub wird mit dem Zustand **Aktiv** angezeigt sowie mit den Standardwerten für die **Nachrichtenaufbewahrung** (*7*) und der **Anzahl der Partitionen** (*4*).

    ![Event Hub, der im Azure-Portal angezeigt wird](../media-draft/3-event-hub.png)

## <a name="summary"></a>Zusammenfassung

Sie haben nun einen neuen Event Hub erstellt. Sie verfügen über alle erforderlichen Informationen zum Konfigurieren Ihrer Herausgeber- und Consumeranwendungen.
