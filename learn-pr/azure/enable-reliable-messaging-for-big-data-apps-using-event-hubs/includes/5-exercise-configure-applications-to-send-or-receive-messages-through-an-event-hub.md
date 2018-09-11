Sie können nun Ihre Herausgeber- und Consumeranwendungen für Ihren Event Hub konfigurieren.

In dieser Einheit konfigurieren Sie diese Anwendungen zum Senden oder Empfangen von Nachrichten über Ihren Event Hub. Diese Anwendungen werden in einem GitHub-Repository gespeichert.

Sie konfigurieren zwei getrennte Anwendungen. Eine fungiert als Nachrichtenabsender (**SimpleSend**), die andere als Nachrichtenempfänger (**EventProcessorSample**). Dies sind Java-Anwendungen, die es Ihnen ermöglichen, sämtliche Aufgaben im Browser zu erledigen. Die gleiche Konfiguration wird jedoch für jede Plattform benötigt, wie z.B. .NET.

## <a name="create-a-general-purpose-standard-storage-account"></a>Erstellen eines allgemeinen Standardspeicherkontos

Die Java-Empfängeranwendung, die Sie in dieser Einheit konfigurieren, speichert Nachrichten in Azure Blob Storage. Für Blob Storage ist ein Speicherkonto erforderlich.

1. Erstellen Sie in der Ressourcengruppe mit dem folgenden Befehl ein Speicherkonto (Allgemein V2):

    ```azurecli
    az storage account create --name <storage account name> --resource-group <resource group name>  --location <location> --sku Standard_RAGRS --encryption blob
    ```

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |--name (erforderlich)  |Geben Sie einen Namen für Ihr Speicherkonto ein.|
    |--resource-group (erforderlich)  |Geben Sie die Ressourcengruppe an, die Sie in der vorherigen Einheit erstellt haben.|
    |-location (optional)    |Geben Sie den Speicherort ein, an dem Sie Ihre Ressourcengruppe in der vorherigen Einheit erstellt haben.|

1. Listen Sie mit dem folgenden Befehl alle Zugriffsschlüssel auf, die Ihrem Speicherkonto zugeordnet sind:

    ```azurecli
    az storage account keys list --account-name <storage account name> --resource-group <resource group name>
    ```

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |--account-name (erforderlich)  |Geben Sie den Namen Ihres Speicherkontos ein.|
    |--resource-group (erforderlich)  |Geben Sie die Ressourcengruppe an, die Sie in der vorherigen Einheit erstellt haben.|

     Die Ihrem Speicherkonto zugeordneten Zugriffsschlüssel werden aufgeführt. Kopieren und speichern Sie den Wert von **key** für die künftige Verwendung. Sie benötigen diesen Schlüssel für den Zugriff auf Ihr Speicherkonto.

1. Zeigen Sie die Verbindungszeichenfolge für Ihr Speicherkonto mit dem folgenden Befehl ein:

    ```azurecli
    az storage account show-connection-string -n <storage account name> -g <resource group name>
    ```

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |-n (erforderlich)  |Geben Sie den Namen Ihres Speicherkontos ein.|
    |-g (erforderlich)  |Geben Sie den Namen Ihrer Ressourcengruppe ein.|

    Dieser Befehl gibt die Verbindungsdetails für das Speicherkonto zurück. Kopieren und speichern Sie den Wert von **connectionString**.

1. Erstellen Sie mit dem folgenden Befehl in Ihrem Speicherkonto einen Container namens **messages**. Verwenden Sie den Wert von **connectionString**, den Sie im vorherigen Schritt kopiert haben:

    ```azurecli
    az storage container create -n messages --connection-string "<connection string>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a>Klonen des GitHub-Repositorys „Event Hubs“

Klonen Sie das GitHub-Repository „Event Hubs“, indem Sie die folgenden Schritte ausführen.

1. Melden Sie sich bei Azure Cloud Shell (Bash) an.

1. Die Quelldateien für die Anwendung, die Sie in dieser Einheit erstellen, befinden sich in einem [GitHub-Repository](https://github.com/Azure/azure-event-hubs). Stellen Sie mit den folgenden Befehlen sicher, dass Sie sich in Ihrem Startverzeichnis in Cloud Shell befinden, und klonen Sie dann dieses Repository:

    ```azurecli
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    Das Repository wird in `/home/<username>/azure-event-hubs` geklont.

## <a name="use-nano-to-edit-simplesendjava"></a>Verwenden von Nano zum Bearbeiten von „SimpleSend.java“

Verwenden Sie den Editor **Nano**, um die Anwendung SimpleSend zu bearbeiten, und fügen Sie den Namespace und Namen Ihres Event Hubs, den Namen der freigegebenen Zugriffsrichtlinie und den Primärschlüssel hinzu. Die wichtigsten Befehle werden unten im Editorfenster angezeigt. In dieser Einheit müssen Sie Ihre Bearbeitungen mit STRG+O schreiben, dann die EINGABETASTE drücken, um den Namen der Ausgabedatei zu bestätigen, und den Editor mit STRG+X verlassen.

1. Wechseln Sie mit dem folgenden Befehl zum Ordner **SimpleSend**:

    ```azurecli
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. Öffnen Sie in **Nano** die Datei **SimpleSend.java** mithilfe des folgenden Befehls:

    ```azurecli
    nano SimpleSend.java
    ```

1. Suchen und ersetzen Sie in Nano die folgenden Zeichenfolgen:

    - `"Your Event Hubs namespace name"` durch den Namespace Ihres Event Hubs.
    - `"Your event hub"` durch den Namen Ihres Event Hubs.
    - `"Your primary SAS key"` durch den Wert des Schlüssels **primaryKey** für Ihren Event Hub-Namespace, den Sie zuvor gespeichert haben.
    - `"Your policy name"` durch **RootManageSharedAccessKey**.
 
        Wenn Sie einen Event Hubs-Namespace erstellen, wird ein 256-Bit-SAS-Schlüssel namens **RootManageSharedAccessKey** erstellt. Diesem ist ein Paar von Primär- und Sekundärschlüsseln zugeordnet, die Sende-, Lausch- und Verwaltungsrechte für den Namespace gewähren. Im vorherigen Kapitel haben Sie den Schlüssel mit einem Azure CLI-Befehl angezeigt. Sie können diesen Schlüssel auch finden, indem Sie im Azure-Portal die Seite **Freigegebene Zugriffsrichtlinien** für Ihren Event Hubs-Namespace öffnen.

    ![Konfigurationsdetails für die Absenderanwendung](../media-draft/5-sender-configure.png)

1. Speichern Sie **SimpleSend.java** mit dem folgenden Befehl, und beenden Sie Nano:

    ```azurecli
    CTRL +O
    ENTER
    CTRL +X
    ```

## <a name="use-maven-to-build-simplesendjava"></a>Verwenden von Maven zum Erstellen von „SimpleSend.java“

Nun erstellen Sie mit **mvn**-Befehlen die Java-Anwendung.

1. Wechseln Sie mit dem folgenden Befehl zum Hauptordner **SimpleSend**:

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. Führen Sie den Buildvorgang für die Java-Anwendung SimpleSend mit dem folgenden Befehl durch. Dadurch wird sichergestellt, dass Ihre Anwendung die Verbindungsdetails für Ihren Event Hub verwendet:

    ```azurecli
    mvn clean package -DskipTests
    ```

    Der Buildprozess kann mehrere Minuten dauern. Stellen Sie sicher, dass die Meldung **[INFO] BUILD SUCCESS** angezeigt wird, ehe Sie fortfahren.

    ![Buildergebnisse für Absenderanwendung](../media-draft/5-sender-build.png)

## <a name="use-nano-to-edit-eventprocessorsamplejava"></a>Verwenden von Nano zum Bearbeiten von „EventProcessorSample.java“

Sie konfigurieren nun eine **Empfänger**- (auch bekannt als **Abonnenten**- oder **Consumer**-) Anwendung, um Daten von Ihrem Event Hub zu erfassen.

Für die Empfängeranwendung stehen zwei Methoden zur Verfügung: **EventHubReceiver** und **EventProcessorHost**. EventProcessorHost setzt auf EventHubReceiver auf, bietet aber eine einfachere Programmierschnittstelle als EventHubReceiver. EventProcessorHost kann Nachrichtenpartitionen unter Verwendung desselben Speicherkontos automatisch auf mehrere Instanzen von EventProcessorHost verteilen.

In dieser Einheit verwenden Sie die EventProcessorHost-Methode. Sie verwenden wiederum Nano und bearbeiten die Anwendung EventProcessorSample, indem Sie Ihren Event Hubs-Namespace, den Namen des Event Hubs und der freigegebenen Zugriffsrichtlinie sowie den Primärschlüssel, den Namen des Speicherkontos, die Verbindungszeichenfolge und den Containernamen hinzuzufügen.

1. Wechseln Sie mit dem folgenden Befehl zum Ordner **EventProcessorSample**:

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. Öffnen Sie in **Nano** die Datei **EventProcessorSample.java** mithilfe des folgenden Befehls:

    ```azurecli
    nano EventProcessorSample.java
    ```
1. Suchen und ersetzen Sie in Nano die folgenden Zeichenfolgen:

    - `----ServiceBusNamespaceName----` durch den Namespace Ihres Event Hubs.
    - `----EventHubName----` durch den Namen Ihres Event Hubs.
    - `----SharedAccessSignatureKeyName----` durch **RootManageSharedAccessKey**.
    - `----SharedAccessSignatureKey----` durch den Wert des Schlüssels **primaryKey** für Ihren Event Hubs-Namespace, den Sie zuvor gespeichert haben.
    - `----AzureStorageConnectionString----` durch die Verbindungszeichenfolge des Speicherkontos, die Sie zuvor gespeichert haben.
    - `----StorageContainerName----` durch **messages**.
    - `----HostNamePrefix----` durch den Namen Ihres Speicherkontos.

    ![Konfigurationsdetails für die Empfängeranwendung](../media-draft/5-receiver-configure.png)

1. Speichern Sie **EventProcessorSample.java** mit dem folgenden Befehl, und beenden Sie Nano:

    ```azurecli
    CTRL +O
    ENTER
    CTRL +X
    ```

## <a name="use-maven-to-build-eventprocessorsamplejava"></a>Verwenden von Maven zum Durchführen des Buildvorgangs für „EventProcessorSample.java“

1. Wechseln Sie mit dem folgenden Befehl zum Hauptordner **EventProcessorSample**:

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. Führen Sie den Buildvorgang für die Java-Anwendung SimpleSend mit dem folgenden Befehl durch. Dadurch wird sichergestellt, dass Ihre Anwendung die Verbindungsdetails für Ihren Event Hub verwendet:

    ```azurecli
    mvn clean package -DskipTests
    ```

    Der Buildprozess kann mehrere Minuten dauern. Stellen Sie sicher, dass die Meldung **[INFO] BUILD SUCCESS** angezeigt wird, ehe Sie fortfahren.

    ![Buildergebnisse für Empfängeranwendung](../media-draft/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a>Starten der Absender- und Empfänger-App

1. Führen Sie die Java-Anwendung über die Befehlszeile aus, indem Sie den Befehl **java** verwenden und ein JAR-Paket angeben. Verwenden Sie die folgenden Befehle, um die Anwendung SimpleSend zu starten:

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. Wenn Sie **Send Complete...** (Sendevorgang abgeschlossen) sehen, drücken Sie die EINGABETASTE.

    ![Ausführungsergebnisse für Absenderanwendung](../media-draft/5-sender-run.png)

1. Starten Sie die Anwendung EventProcessorSample mit dem folgenden Befehl.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. Wenn in der Konsole keine Nachrichten mehr angezeigt werden, drücken Sie die EINGABETASTE.

    ![Ausführungsergebnisse für Empfängeranwendung](../media-draft/5-receiver-run.png)

## <a name="summary"></a>Zusammenfassung

Sie haben soeben eine Absenderanwendung konfiguriert, die zum Senden von Nachrichten an Ihren Event Hub bereit ist. Sie haben außerdem eine Empfängeranwendung konfiguriert, die zum Empfangen von Nachrichten von Ihren Event Hub bereit ist.
