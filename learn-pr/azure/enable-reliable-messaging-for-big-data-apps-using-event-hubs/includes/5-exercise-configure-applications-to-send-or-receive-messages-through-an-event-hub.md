Sie können nun Ihre Herausgeber- und Consumeranwendungen für Ihren Event Hub konfigurieren.

In dieser Einheit konfigurieren Sie diese Anwendungen zum Senden oder Empfangen von Nachrichten über Ihren Event Hub. Diese Anwendungen werden in einem GitHub-Repository gespeichert.

Sie konfigurieren zwei getrennte Anwendungen. Eine fungiert als Nachrichtenabsender (**SimpleSend**), die andere als Nachrichtenempfänger (**EventProcessorSample**). Dies sind Java-Anwendungen, die es Ihnen ermöglichen, sämtliche Aufgaben im Browser zu erledigen. Die gleiche Konfiguration wird jedoch für jede Plattform benötigt, wie z.B. .NET.

## <a name="create-a-general-purpose-standard-storage-account"></a>Erstellen eines allgemeinen Standardspeicherkontos

Die Java-Empfängeranwendung, die Sie in dieser Einheit konfigurieren, speichert Nachrichten in Azure Blob Storage. Für Blob Storage ist ein Speicherkonto erforderlich.

1. Erstellen Sie mit dem Befehl `storage account create` ein Speicherkonto (Allgemein V2). Zur Erinnerung: Wir haben eine Standardressourcengruppe und einen Standort festgelegt, sodass wir diese Parameter, obwohl sie normalerweise _benötigt_ werden, weglassen können.

    |Parameter      |Beschreibung|
    |---------------|-----------|
    |--name (erforderlich)  | Ein Name für Ihr Speicherkonto. |
    |--resource-group (erforderlich)  |Der Ressourcengruppenbesitzer. Wir verwenden die vorab erstellte Ressourcengruppe.|
    |--location (optional)    |Ein optionaler Standort, wenn Sie das Speicherkonto an einem bestimmten Ort und nicht am Standort der Ressourcengruppe wünschen.|

    Geben Sie den Namen des Speicherkontos in eine Variable ein. Dieser darf nur als Kleinbuchstaben und Zahlen mit Bindestrichen als Trennzeichen bestehen. Außerdem muss er in Azure eindeutig sein.

    ```azurecli
    STORAGE_NAME=[name]
    ```

    Führen Sie nun diesen Befehl zum Erstellen des Speicherkontos aus.

    ```azurecli
    az storage account create --name $STORAGE_NAME --sku Standard_RAGRS --encryption blob
    ```

    > [!TIP]
    > Wenn die Erstellung des Speicherkonto nicht erfolgreich ist, ändern Sie Ihre Umgebungsvariable, und versuchen Sie es erneut.

1. Listen Sie mit dem Befehl `account keys list` alle Zugriffsschlüssel auf, die Ihrem Speicherkonto zugeordnet sind. Der Befehl verwendet den Namen Ihres Kontos und die Ressourcengruppe (die als Standardwert vorgegeben ist).

    ```azurecli
    az storage account keys list --account-name $STORAGE_NAME
    ```

     Die Ihrem Speicherkonto zugeordneten Zugriffsschlüssel werden aufgeführt. Kopieren und speichern Sie den Wert von **key** für die künftige Verwendung. Sie benötigen diesen Schlüssel für den Zugriff auf Ihr Speicherkonto.

1. Zeigen Sie die Verbindungszeichenfolge für Ihr Speicherkonto mit dem folgenden Befehl an:

    ```azurecli
    az storage account show-connection-string -n $STORAGE_NAME
    ```

    Dieser Befehl gibt die Verbindungsdetails für das Speicherkonto zurück. Kopieren und speichern Sie den _Wert_ von **connectionString**. Dieser sollte ungefähr wie folgt aussehen:

    ```output
    "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=storage_account_name;AccountKey=VZjXuMeuDqjCkT60xX6L5fmtXixYuY2wiPmsrXwYHIhwo736kSAUAj08XBockRZh7CZwYxuYBPe31hi8XfHlWw=="
    ```

1. Erstellen Sie mit dem folgenden Befehl in Ihrem Speicherkonto einen Container namens **messages**. Verwenden Sie den Wert von **connectionString**, den Sie im vorherigen Schritt kopiert haben:

    ```azurecli
    az storage container create -n messages --connection-string "<connection string here>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a>Klonen des GitHub-Repositorys „Event Hubs“

Klonen Sie das GitHub-Repository „Event Hubs“ mit `git`, indem Sie die folgenden Schritte ausführen. Sie verfügen in Cloud Shell über die Berechtigung dazu.

1. Die Quelldateien für die Anwendung, die Sie in dieser Einheit erstellen, befinden sich in einem [GitHub-Repository](https://github.com/Azure/azure-event-hubs). Stellen Sie mit den folgenden Befehlen sicher, dass Sie sich in Cloud Shell in Ihrem Basisverzeichnis befinden, und klonen Sie dann dieses Repository:

    ```bash
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    Das Repository wird in Ihren Basisordner geklont.

## <a name="edit-simplesendjava"></a>Bearbeiten von „SimpleSend.java“

Wir werden mit dem integrierten Cloud Shell-Code-Editor arbeiten. Dieser basiert auf dem Monaco-Editor und ist Visual Studio Code ähnlich, aber vollständig online.

Wir verwenden den Editor, um die Anwendung SimpleSend zu bearbeiten, und fügen den Namespace und Namen Ihres Event Hubs, den Namen der freigegebenen Zugriffsrichtlinie und den Primärschlüssel hinzu. Die wichtigsten Befehle werden im Fenster des Editors am unteren Rand angezeigt. 

Sie müssen Ihre Bearbeitungen mit <kbd>STRG+O</kbd> speichern, dann die <kbd>EINGABETASTE</kbd> drücken, um den Namen der Ausgabedatei zu bestätigen, und den Editor mit <kbd>STRG+X</kbd> zu beenden. Alternativ verfügt der Editor rechts oben über das Menü „...“, das alle Bearbeitungsbefehle enthält.

1. Navigieren Sie zum Ordner **SimpleSend**.

    ```bash
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. Öffnen Sie den Code-Editor im aktuellen Ordner. Auf der linken Seite wird eine Liste der Dateien und auf der rechten Seite ein Editierbereich angezeigt.

    ```bash
    code .
    ```

1. Öffnen Sie Datei **SimpleSend.java**, indem Sie sie in der Liste auswählen.

1. Suchen und ersetzen Sie im Editor die folgenden Zeichenfolgen:

    - `"Your Event Hubs namespace name"` durch den Namen Ihres Event Hub-Namespace.
    - `"Your Event Hub"` durch den Namen Ihres Event Hubs.
    - `"Your policy name"` durch **RootManageSharedAccessKey**.
    - `"Your primary SAS key"` durch den Wert des Schlüssels **primaryKey** für Ihren Event Hub-Namespace, den Sie zuvor gespeichert haben.
 
    > [!TIP]
    > Im Gegensatz zum Terminalfenster können Sie im Editor die üblichen Tastenkombinationen zum Kopieren/Einfügen Ihres Betriebssystems verwenden.

    Wenn Sie einige davon vergessen haben, können Sie zum Terminalfenster unter dem Editor wechseln und mit dem Befehl `echo` eine der Umgebungsvariablen auswählen. Beispiele:

    ```bash
    echo $NS_NAME
    ```
    Wenn Sie einen Event Hubs-Namespace erstellen, wird ein 256-Bit-SAS-Schlüssel namens **RootManageSharedAccessKey** erstellt. Diesem ist ein Paar von Primär- und Sekundärschlüsseln zugeordnet, die Sende-, Lausch- und Verwaltungsrechte für den Namespace gewähren. Im vorherigen Kapitel haben Sie den Schlüssel mit einem Azure CLI-Befehl angezeigt. Sie können diesen Schlüssel auch ermitteln, indem Sie im Azure-Portal die Seite **Freigegebene Zugriffsrichtlinien** für Ihren Event Hubs-Namespace öffnen.

1. Speichern Sie **SimpleSend.java** entweder über das Menü („...“) oder per Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux, <kbd>Cmd+S</kbd> unter macOS).

1. Schließen Sie den Editor über das Kontextmenü „...“.oder die Tastenkombination <kbd>STRG+Q</kbd>.

## <a name="use-maven-to-build-simplesendjava"></a>Verwenden von Maven zum Erstellen von „SimpleSend.java“

Nun erstellen Sie mit **mvn**-Befehlen die Java-Anwendung.

1. Navigieren Sie zurück zum Hauptordner **SimpleSend**.

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. Führen Sie den Buildvorgang für die Java-Anwendung SimpleSend durch. Dadurch wird sichergestellt, dass Ihre Anwendung die Verbindungsdetails für Ihren Event Hub verwendet:

    ```bash
    mvn clean package -DskipTests
    ```

    Der Buildprozess kann mehrere Minuten dauern. Stellen Sie sicher, dass die Meldung **[INFO] BUILD SUCCESS** angezeigt wird, ehe Sie fortfahren.

    ![Buildergebnisse für Absenderanwendung](../media/5-sender-build.png)

## <a name="edit-eventprocessorsamplejava"></a>Bearbeiten von „EventProcessorSample.java“

Sie konfigurieren nun eine **Empfängeranwendung** (auch **Abonnenten-** oder **Consumeranwendung** genannt), um Daten von Ihrem Event Hub zu erfassen.

Für die Empfängeranwendung stehen zwei Methoden zur Verfügung: **EventHubReceiver** und **EventProcessorHost**. EventProcessorHost setzt auf EventHubReceiver auf, bietet aber eine einfachere Programmierschnittstelle als EventHubReceiver. EventProcessorHost kann Nachrichtenpartitionen unter Verwendung desselben Speicherkontos automatisch auf mehrere Instanzen von EventProcessorHost verteilen.

In dieser Einheit verwenden Sie die EventProcessorHost-Methode. Sie bearbeiten die EventProcessorSample-Anwendung, um Ihren Event Hubs-Namespace, den Namen des Event Hubs und der SAS-Richtlinie sowie den Primärschlüssel, den Namen des Speicherkontos, die Verbindungszeichenfolge und den Containernamen hinzuzufügen.

1. Wechseln Sie mit dem folgenden Befehl zum Ordner **EventProcessorSample**:

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. Öffnen Sie den Code-Editor.

    ```bash
    code .
    ```
    
1. Wählen Sie die Datei **EventProcessorSample.java** aus.

1. Suchen und ersetzen Sie im Editor die folgenden Zeichenfolgen:

    - `----ServiceBusNamespaceName----` durch den Namen Ihres Event Hubs-Namespace.
    - `----EventHubName----` durch den Namen Ihres Event Hubs.
    - `----SharedAccessSignatureKeyName----` durch **RootManageSharedAccessKey**.
    - `----SharedAccessSignatureKey----` durch den Wert des Schlüssels **primaryKey** für Ihren Event Hubs-Namespace, den Sie zuvor gespeichert haben.
    - `----AzureStorageConnectionString----` durch die Verbindungszeichenfolge des Speicherkontos, die Sie zuvor gespeichert haben.
    - `----StorageContainerName----` durch **messages**.
    - `----HostNamePrefix----` durch den Namen Ihres Speicherkontos.

1. Speichern Sie **EventProcessorSample.java** entweder über das Menü („...“) oder per Tastenkombination (<kbd>STRG+S</kbd> unter Windows und Linux, <kbd>Cmd+S</kbd> unter macOS).

1. Schließen Sie den Editor.

## <a name="use-maven-to-build-eventprocessorsamplejava"></a>Verwenden von Maven zum Durchführen des Buildvorgangs für „EventProcessorSample.java“

1. Wechseln Sie mit dem folgenden Befehl zum Hauptordner **EventProcessorSample**:

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. Führen Sie den Buildvorgang für die Java-Anwendung SimpleSend mit dem folgenden Befehl durch. Dadurch wird sichergestellt, dass Ihre Anwendung die Verbindungsdetails für Ihren Event Hub verwendet:

    ```bash
    mvn clean package -DskipTests
    ```

    Der Buildprozess kann mehrere Minuten dauern. Stellen Sie sicher, dass die Meldung **[INFO] BUILD SUCCESS** angezeigt wird, ehe Sie fortfahren.

    ![Buildergebnisse für Empfängeranwendung](../media/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a>Starten der Absender- und Empfänger-App

1. Führen Sie die Java-Anwendung über die Befehlszeile aus, indem Sie den Befehl **java** verwenden und ein JAR-Paket angeben. Verwenden Sie die folgenden Befehle, um die Anwendung SimpleSend zu starten:

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. Wenn **Send Complete...** (Sendevorgang abgeschlossen) angezeigt wird, drücken Sie die <kbd>EINGABETASTE</kbd>.

    ```output
    jar-with-dependencies.jar
    SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
    SLF4J: Defaulting to no-operation (NOP) logger implementation
    SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
    2018-09-18T19:42:15.146Z: Send Complete...
    ```

1. Starten Sie die Anwendung EventProcessorSample mit dem folgenden Befehl.

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. Wenn in der Konsole keine Meldungen mehr angezeigt werden, drücken Sie die <kbd>EINGABETASTE</kbd> oder <kbd>STRG+C</kbd>, um das Programm zu beenden.

    ```output
    ...
    SAMPLE: Partition 0 checkpointing at 1064,19
    SAMPLE (3,1120,20): "Message 80"
    SAMPLE (3,1176,21): "Message 84"
    SAMPLE (3,1232,22): "Message 88"
    SAMPLE (3,1288,23): "Message 92"
    SAMPLE (3,1344,24): "Message 96"
    SAMPLE: Partition 3 checkpointing at 1344,24
    SAMPLE (2,1120,20): "Message 83"
    SAMPLE (2,1176,21): "Message 87"
    SAMPLE (2,1232,22): "Message 91"
    SAMPLE (2,1288,23): "Message 95"
    SAMPLE (2,1344,24): "Message 99"
    SAMPLE: Partition 2 checkpointing at 1344,24
    SAMPLE: Partition 1 batch size was 3 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE (0,1120,20): "Message 81"
    SAMPLE (0,1176,21): "Message 85"
    SAMPLE: Partition 0 batch size was 10 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 0 got event batch
    SAMPLE (0,1232,22): "Message 89"
    SAMPLE (0,1288,23): "Message 93"
    SAMPLE (0,1344,24): "Message 97"
    SAMPLE: Partition 0 checkpointing at 1344,24
    SAMPLE: Partition 3 batch size was 8 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 2 batch size was 9 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 0 batch size was 3 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    ```

## <a name="summary"></a>Zusammenfassung

Sie haben soeben eine Absenderanwendung konfiguriert, die zum Senden von Nachrichten an Ihren Event Hub bereit ist. Sie haben außerdem eine Empfängeranwendung konfiguriert, die zum Empfangen von Nachrichten von Ihrem Event Hub bereit ist.