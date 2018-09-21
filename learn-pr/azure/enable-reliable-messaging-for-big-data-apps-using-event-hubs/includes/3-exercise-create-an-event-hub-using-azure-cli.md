Sie können nun einen neuen Event Hub erstellen. Nachdem der Event Hub erstellt wurde, verwenden Sie das Azure-Portal, um Ihren neuen Hub anzuzeigen.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="set-some-defaults-in-the-azure-cli"></a>Festlegen von Standardwerten in der Azure CLI

Zunächst geben wir einige Standardwerte für die Azure CLI in Cloud Shell an. So wird verhindert, dass Sie diese Werte jedes Mal eingeben müssen. Es geht hierbei vor allem um die _Ressourcengruppe_ und den _Standort_. Wählen Sie in der folgenden Liste einen Standort aus.

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

Geben Sie anschließend den folgenden Befehl in die Azure CLI ein, und ersetzen Sie den Standort durch einen Standort in Ihrer Nähe.

```azurecli
az configure --defaults group=<rgn>[Sandbox Resource Group]</rgn> location=westus2
```

## <a name="create-an-event-hubs-namespace"></a>Erstellen eines Event Hubs-Namespace

Wenn Sie die folgenden Schritte ausführen, können Sie einen Event Hubs-Namespace mithilfe der von Azure Cloud Shell unterstützten Bash-Shell erstellen:

1. Erstellen Sie mit dem Befehl `az eventhubs namespace create` den Event Hubs-Namespace. Verwenden Sie die folgenden Parameter.

    > [!div class="mx-tableFixed"]
    > |Parameter      |Beschreibung|
    > |---------------|-----------|
    > |--name (erforderlich)      |Geben Sie Ihrem Event Hubs-Namespace einen eindeutigen Namen, der zwischen 6 und 50 Zeichen lang ist. Der Name darf nur Buchstaben, Zahlen und Bindestriche enthalten. Er muss zudem mit einem Buchstaben beginnen und mit einem Buchstaben oder einer Zahl enden.|
    > |--resource-group (erforderlich) | Dies ist die vorab erstellte Ressourcengruppe der Azure-Sandbox, die über die Standardwerte bereitgestellt wird. |
    > |--l (optional)     |Geben Sie den Standort Ihres nächstgelegenen Azure-Rechenzentrums ein. Hierfür wird Ihr Standardwert verwendet.|
    > |--sku (optional) | Der Tarif für den Namespace [Basic | Standard], standardmäßig _Standard_. Hiermit werden die Verbindungen und Consumerschwellenwerte bestimmt. |

    Legen Sie den Namen in einer Umgebungsvariablen fest, damit Sie ihn wiederverwenden können.

    ```azurecli
    NS_NAME=myEvt-HubNs1
    ````

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```azurecli
    az eventhubs namespace create --name $NS_NAME
    ```

    > [!NOTE] 
    > Azure ist beim Namen sehr wählerisch, und die CLI gibt **Ungültige Anforderung** zurück, wenn der Name bereits vorhanden oder ungültig ist. Probieren Sie es mit einem anderen Namen, indem Sie die Umgebungsvariable ändern und den Befehl erneut ausführen.


1. Rufen Sie die Verbindungszeichenfolge für Ihren Event Hubs-Namespace mithilfe des folgenden Befehls ab. Sie benötigen diese, wenn Sie Anwendungen zum Senden und Empfangen von Nachrichten über Ihren Event Hub konfigurieren.

    ```azurecli
    az eventhubs namespace authorization-rule keys list --name RootManageSharedAccessKey --namespace-name $NS_NAME 
    ```

    > [!div class="mx-tableFixed"]
    > |Parameter      |Beschreibung|
    > |---------------|-----------|
    > |--resource-group (erforderlich)  | Dies ist die vorab erstellte Ressourcengruppe der Azure-Sandbox, die über die Standardwerte bereitgestellt wird. |
    > |--namespace-name (erforderlich)  | Geben Sie den Namen des von Ihnen erstellten Namespace ein. |

    Dieser Befehl gibt einen JSON-Block mit der Verbindungszeichenfolge für Ihren Event Hubs-Namespace zurück, den Sie später zum Konfigurieren Ihrer Herausgeber- und Consumeranwendungen verwenden. Speichern Sie den Wert der folgenden Schlüssel für den späteren Gebrauch.

    - **primaryConnectionString**
    - **primaryKey**

## <a name="create-an-event-hub"></a>Erstellen eines Event Hubs

Führen Sie die folgenden Schritte aus, um Ihren neuen Event Hub zu erstellen:

1. Erstellen Sie mit dem Befehl `eventhub create` einen neuen Event Hub. Hierfür sind die folgenden Parameter erforderlich:

    > [!div class="mx-tableFixed"]
    > |Parameter      |Beschreibung|
    > |---------------|-----------|
    > |--name (erforderlich)  |Geben Sie einen Namen für Ihren Event Hub ein.|
    > |--resource-group (erforderlich)  |Ressourcengruppenbesitzer|
    > |--namespace-name (erforderlich)      |Geben Sie den Namespace ein, den Sie erstellt haben.|

    Wir definieren den Event Hub-Namen zuerst in einer Umgebungsvariablen.

    ```azurecli
    HUB_NAME=[name]
    ```

    ```azurecli
    az eventhubs eventhub create --name $HUB_NAME --namespace-name $NS_NAME
    ```

1. Zeigen Sie mit dem Befehl `eventhub show` die Informationen zu Ihrem Event Hub an. Hierfür wird Folgendes verwendet:

    > [!div class="mx-tableFixed"]
    > |Parameter      |Beschreibung|
    > |---------------|-----------|
    > |--resource-group (erforderlich)  |Ressourcengruppenbesitzer|
    > |--namespace-name (erforderlich)      |Geben Sie den Namespace ein, den Sie erstellt haben.|
    > |--name (erforderlich)|Name des Event Hubs.|

    ```azurecli
    az eventhubs eventhub show --namespace-name $NS_NAME --name $HUB_NAME
    ```

## <a name="view-the-event-hub-in-the-azure-portal"></a>Anzeigen des Event Hubs im Azure-Portal

Als Nächstes wird beschrieben, wie dies im Azure-Portal aussieht. 

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit demselben Konto an, über das Sie die Sandbox aktiviert haben.

1. Suchen Sie über die Suchleiste am oberen Rand des Portals nach Ihrem Event Hubs-Namespace.

1. Wählen Sie Ihren Namespace aus, um ihn zu öffnen.

1. Wählen Sie unter dem Abschnitt **ENTITÄTEN** die Option **Event Hubs-Namespace**.

1. Klicken Sie auf **Event Hubs**.

    Ihr Event Hub wird mit dem Zustand **Aktiv** sowie mit den Standardwerten für die **Nachrichtenaufbewahrung** (*7*) und **Partitionsanzahl** (*4*) angezeigt.

    ![Event Hub, der im Azure-Portal angezeigt wird](../media/3-event-hub.png)

## <a name="summary"></a>Zusammenfassung

Sie haben nun einen neuen Event Hub erstellt. Sie verfügen über alle erforderlichen Informationen zum Konfigurieren Ihrer Herausgeber- und Consumeranwendungen.
