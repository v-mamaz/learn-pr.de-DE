<span data-ttu-id="14492-101">Sie können nun Ihre Herausgeber- und Consumeranwendungen für Ihren Event Hub konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="14492-101">You're now ready to configure your publisher and consumer applications for your event hub.</span></span>

<span data-ttu-id="14492-102">In dieser Einheit konfigurieren Sie diese Anwendungen zum Senden oder Empfangen von Nachrichten über Ihren Event Hub.</span><span class="sxs-lookup"><span data-stu-id="14492-102">In this unit, you'll configure these applications to send or receive messages through your event hub.</span></span> <span data-ttu-id="14492-103">Diese Anwendungen werden in einem GitHub-Repository gespeichert.</span><span class="sxs-lookup"><span data-stu-id="14492-103">These applications are stored in a GitHub repository.</span></span>

<span data-ttu-id="14492-104">Sie konfigurieren zwei getrennte Anwendungen. Eine fungiert als Nachrichtenabsender (**SimpleSend**), die andere als Nachrichtenempfänger (**EventProcessorSample**).</span><span class="sxs-lookup"><span data-stu-id="14492-104">You'll configure two separate applications; one acts as the message sender (**SimpleSend**), the other as the message receiver (**EventProcessorSample**).</span></span> <span data-ttu-id="14492-105">Dies sind Java-Anwendungen, die es Ihnen ermöglichen, sämtliche Aufgaben im Browser zu erledigen.</span><span class="sxs-lookup"><span data-stu-id="14492-105">These are Java applications, which enable you to do everything within the browser.</span></span> <span data-ttu-id="14492-106">Die gleiche Konfiguration wird jedoch für jede Plattform benötigt, wie z.B. .NET.</span><span class="sxs-lookup"><span data-stu-id="14492-106">However, the same configuration is needed for any platform, such as .NET.</span></span>

## <a name="create-a-general-purpose-standard-storage-account"></a><span data-ttu-id="14492-107">Erstellen eines allgemeinen Standardspeicherkontos</span><span class="sxs-lookup"><span data-stu-id="14492-107">Create a general-purpose, standard storage account</span></span>

<span data-ttu-id="14492-108">Die Java-Empfängeranwendung, die Sie in dieser Einheit konfigurieren, speichert Nachrichten in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="14492-108">The Java receiver application, that you'll configure in this unit, stores messages in Azure Blob Storage.</span></span> <span data-ttu-id="14492-109">Für Blob Storage ist ein Speicherkonto erforderlich.</span><span class="sxs-lookup"><span data-stu-id="14492-109">Blob Storage requires a storage account.</span></span>

1. <span data-ttu-id="14492-110">Erstellen Sie in der Ressourcengruppe mit dem folgenden Befehl ein Speicherkonto (Allgemein V2):</span><span class="sxs-lookup"><span data-stu-id="14492-110">Create a storage account (general-purpose V2) in the resource group using the following command:</span></span>

    ```azurecli
    az storage account create --name <storage account name> --resource-group <resource group name>  --location <location> --sku Standard_RAGRS --encryption blob
    ```

    |<span data-ttu-id="14492-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="14492-111">Parameter</span></span>      |<span data-ttu-id="14492-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="14492-112">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="14492-113">--name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="14492-113">--name (required)</span></span>  |<span data-ttu-id="14492-114">Geben Sie einen Namen für Ihr Speicherkonto ein.</span><span class="sxs-lookup"><span data-stu-id="14492-114">Enter a name for your storage account.</span></span>|
    |<span data-ttu-id="14492-115">--resource-group (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="14492-115">--resource-group (required)</span></span>  |<span data-ttu-id="14492-116">Geben Sie die Ressourcengruppe an, die Sie in der vorherigen Einheit erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="14492-116">Enter the resource group you created in the previous unit.</span></span>|
    |<span data-ttu-id="14492-117">-location (optional)</span><span class="sxs-lookup"><span data-stu-id="14492-117">--location (optional)</span></span>    |<span data-ttu-id="14492-118">Geben Sie den Speicherort ein, an dem Sie Ihre Ressourcengruppe in der vorherigen Einheit erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="14492-118">Enter the location you used to create your resource group in the previous unit.</span></span>|

1. <span data-ttu-id="14492-119">Listen Sie mit dem folgenden Befehl alle Zugriffsschlüssel auf, die Ihrem Speicherkonto zugeordnet sind:</span><span class="sxs-lookup"><span data-stu-id="14492-119">List all the access keys associated with your storage account using the following command:</span></span>

    ```azurecli
    az storage account keys list --account-name <storage account name> --resource-group <resource group name>
    ```

    |<span data-ttu-id="14492-120">Parameter</span><span class="sxs-lookup"><span data-stu-id="14492-120">Parameter</span></span>      |<span data-ttu-id="14492-121">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="14492-121">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="14492-122">--account-name (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="14492-122">--account-name (required)</span></span>  |<span data-ttu-id="14492-123">Geben Sie den Namen Ihres Speicherkontos ein.</span><span class="sxs-lookup"><span data-stu-id="14492-123">Enter the name for your storage account.</span></span>|
    |<span data-ttu-id="14492-124">--resource-group (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="14492-124">--resource-group (required)</span></span>  |<span data-ttu-id="14492-125">Geben Sie die Ressourcengruppe an, die Sie in der vorherigen Einheit erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="14492-125">Enter the resource group you created in the previous unit.</span></span>|

     <span data-ttu-id="14492-126">Die Ihrem Speicherkonto zugeordneten Zugriffsschlüssel werden aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="14492-126">Access keys associated with your storage account are listed.</span></span> <span data-ttu-id="14492-127">Kopieren und speichern Sie den Wert von **key** für die künftige Verwendung.</span><span class="sxs-lookup"><span data-stu-id="14492-127">Copy and save the value of **key** for future use.</span></span> <span data-ttu-id="14492-128">Sie benötigen diesen Schlüssel für den Zugriff auf Ihr Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="14492-128">You'll need this key to access your storage account.</span></span>

1. <span data-ttu-id="14492-129">Zeigen Sie die Verbindungszeichenfolge für Ihr Speicherkonto mit dem folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="14492-129">View the connections string for your storage account using the following command:</span></span>

    ```azurecli
    az storage account show-connection-string -n <storage account name> -g <resource group name>
    ```

    |<span data-ttu-id="14492-130">Parameter</span><span class="sxs-lookup"><span data-stu-id="14492-130">Parameter</span></span>      |<span data-ttu-id="14492-131">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="14492-131">Description</span></span>|
    |---------------|-----------|
    |<span data-ttu-id="14492-132">-n (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="14492-132">-n (required)</span></span>  |<span data-ttu-id="14492-133">Geben Sie den Namen Ihres Speicherkontos ein.</span><span class="sxs-lookup"><span data-stu-id="14492-133">Enter the name for your storage account.</span></span>|
    |<span data-ttu-id="14492-134">-g (erforderlich)</span><span class="sxs-lookup"><span data-stu-id="14492-134">-g (required)</span></span>  |<span data-ttu-id="14492-135">Geben Sie den Namen Ihrer Ressourcengruppe ein.</span><span class="sxs-lookup"><span data-stu-id="14492-135">Enter the name of your resource group.</span></span>|

    <span data-ttu-id="14492-136">Dieser Befehl gibt die Verbindungsdetails für das Speicherkonto zurück.</span><span class="sxs-lookup"><span data-stu-id="14492-136">This command returns the connection details for the storage account.</span></span> <span data-ttu-id="14492-137">Kopieren und speichern Sie den Wert von **connectionString**.</span><span class="sxs-lookup"><span data-stu-id="14492-137">Copy and save the value of **connectionString**.</span></span>

1. <span data-ttu-id="14492-138">Erstellen Sie mit dem folgenden Befehl in Ihrem Speicherkonto einen Container namens **messages**.</span><span class="sxs-lookup"><span data-stu-id="14492-138">Create a container called **messages** in your storage account using the following command.</span></span> <span data-ttu-id="14492-139">Verwenden Sie den Wert von **connectionString**, den Sie im vorherigen Schritt kopiert haben:</span><span class="sxs-lookup"><span data-stu-id="14492-139">Use the **connectionString** you copied in the previous step:</span></span>

    ```azurecli
    az storage container create -n messages --connection-string "<connection string>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a><span data-ttu-id="14492-140">Klonen des GitHub-Repositorys „Event Hubs“</span><span class="sxs-lookup"><span data-stu-id="14492-140">Clone the Event Hubs GitHub repository</span></span>

<span data-ttu-id="14492-141">Klonen Sie das GitHub-Repository „Event Hubs“, indem Sie die folgenden Schritte ausführen.</span><span class="sxs-lookup"><span data-stu-id="14492-141">Use the following steps to clone the Event Hubs GitHub repository.</span></span>

1. <span data-ttu-id="14492-142">Melden Sie sich bei Azure Cloud Shell (Bash) an.</span><span class="sxs-lookup"><span data-stu-id="14492-142">Sign in to Azure Cloud Shell (Bash).</span></span>

1. <span data-ttu-id="14492-143">Die Quelldateien für die Anwendung, die Sie in dieser Einheit erstellen, befinden sich in einem [GitHub-Repository](https://github.com/Azure/azure-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="14492-143">The source files for the applications that you'll build In this unit are located in a [GitHub repository](https://github.com/Azure/azure-event-hubs).</span></span> <span data-ttu-id="14492-144">Stellen Sie mit den folgenden Befehlen sicher, dass Sie sich in Ihrem Startverzeichnis in Cloud Shell befinden, und klonen Sie dann dieses Repository:</span><span class="sxs-lookup"><span data-stu-id="14492-144">Use the following commands to make sure that you are in your home directory in Cloud Shell, and then to clone this repository:</span></span>

    ```azurecli
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    <span data-ttu-id="14492-145">Das Repository wird in `/home/<username>/azure-event-hubs` geklont.</span><span class="sxs-lookup"><span data-stu-id="14492-145">The repository is cloned to `/home/<username>/azure-event-hubs`.</span></span>

## <a name="use-nano-to-edit-simplesendjava"></a><span data-ttu-id="14492-146">Verwenden von Nano zum Bearbeiten von „SimpleSend.java“</span><span class="sxs-lookup"><span data-stu-id="14492-146">Use nano to edit SimpleSend.java</span></span>

<span data-ttu-id="14492-147">Verwenden Sie den Editor **Nano**, um die Anwendung SimpleSend zu bearbeiten, und fügen Sie den Namespace und Namen Ihres Event Hubs, den Namen der freigegebenen Zugriffsrichtlinie und den Primärschlüssel hinzu.</span><span class="sxs-lookup"><span data-stu-id="14492-147">Use the **nano** editor to edit the SimpleSend application and add your Event Hubs namespace, event hub name, shared access policy name, and primary key.</span></span> <span data-ttu-id="14492-148">Die wichtigsten Befehle werden unten im Editorfenster angezeigt. In dieser Einheit müssen Sie Ihre Bearbeitungen mit STRG+O schreiben, dann die EINGABETASTE drücken, um den Namen der Ausgabedatei zu bestätigen, und den Editor mit STRG+X verlassen.</span><span class="sxs-lookup"><span data-stu-id="14492-148">The main commands are displayed at the bottom of the editor window; in this unit, you'll need to write out your edits using CTRL +O, and then ENTER to confirm the output file name, and exit the editor using CTRL +X.</span></span>

1. <span data-ttu-id="14492-149">Wechseln Sie mit dem folgenden Befehl zum Ordner **SimpleSend**:</span><span class="sxs-lookup"><span data-stu-id="14492-149">Change to the **SimpleSend** folder using the following command:</span></span>

    ```azurecli
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. <span data-ttu-id="14492-150">Öffnen Sie in **Nano** die Datei **SimpleSend.java** mithilfe des folgenden Befehls:</span><span class="sxs-lookup"><span data-stu-id="14492-150">Open the **SimpleSend.java** file in the **nano** editor using the following command:</span></span>

    ```azurecli
    nano SimpleSend.java
    ```

1. <span data-ttu-id="14492-151">Suchen und ersetzen Sie in Nano die folgenden Zeichenfolgen:</span><span class="sxs-lookup"><span data-stu-id="14492-151">In the nano editor, locate and replace the following strings:</span></span>

    - <span data-ttu-id="14492-152">`"Your Event Hubs namespace name"` durch den Namespace Ihres Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="14492-152">`"Your Event Hubs namespace name"` with the name of your event hub namespace.</span></span>
    - <span data-ttu-id="14492-153">`"Your event hub"` durch den Namen Ihres Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="14492-153">`"Your event hub"` with the name of your event hub.</span></span>
    - <span data-ttu-id="14492-154">`"Your primary SAS key"` durch den Wert des Schlüssels **primaryKey** für Ihren Event Hub-Namespace, den Sie zuvor gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="14492-154">`"Your primary SAS key"` with the value of the **primaryKey** key for your event hub namespace that you saved earlier.</span></span>
    - <span data-ttu-id="14492-155">`"Your policy name"` durch **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="14492-155">`"Your policy name"` with **RootManageSharedAccessKey**.</span></span>
 
        <span data-ttu-id="14492-156">Wenn Sie einen Event Hubs-Namespace erstellen, wird ein 256-Bit-SAS-Schlüssel namens **RootManageSharedAccessKey** erstellt. Diesem ist ein Paar von Primär- und Sekundärschlüsseln zugeordnet, die Sende-, Lausch- und Verwaltungsrechte für den Namespace gewähren.</span><span class="sxs-lookup"><span data-stu-id="14492-156">When you create an Event Hubs namespace, a 256-bit SAS key called **RootManageSharedAccessKey** is created that has an associated pair of primary and secondary keys that grant send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="14492-157">Im vorherigen Kapitel haben Sie den Schlüssel mit einem Azure CLI-Befehl angezeigt. Sie können diesen Schlüssel auch finden, indem Sie im Azure-Portal die Seite **Freigegebene Zugriffsrichtlinien** für Ihren Event Hubs-Namespace öffnen.</span><span class="sxs-lookup"><span data-stu-id="14492-157">In the previous unit, you displayed the key using an Azure CLI command, and you can also find this key by opening the **Shared access policies** page for your Event Hubs namespace in the Azure portal.</span></span>

    ![Konfigurationsdetails für die Absenderanwendung](../media-draft/5-sender-configure.png)

1. <span data-ttu-id="14492-159">Speichern Sie **SimpleSend.java** mit dem folgenden Befehl, und beenden Sie Nano:</span><span class="sxs-lookup"><span data-stu-id="14492-159">Save **SimpleSend.java** using the following command, and exit nano:</span></span>

    ```azurecli
    CTRL +O
    ENTER
    CTRL +X
    ```

## <a name="use-maven-to-build-simplesendjava"></a><span data-ttu-id="14492-160">Verwenden von Maven zum Erstellen von „SimpleSend.java“</span><span class="sxs-lookup"><span data-stu-id="14492-160">Use Maven to build SimpleSend.java</span></span>

<span data-ttu-id="14492-161">Nun erstellen Sie mit **mvn**-Befehlen die Java-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="14492-161">You'll now build the Java application using **mvn** commands.</span></span>

1. <span data-ttu-id="14492-162">Wechseln Sie mit dem folgenden Befehl zum Hauptordner **SimpleSend**:</span><span class="sxs-lookup"><span data-stu-id="14492-162">Change to the main **SimpleSend** folder using the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. <span data-ttu-id="14492-163">Führen Sie den Buildvorgang für die Java-Anwendung SimpleSend mit dem folgenden Befehl durch.</span><span class="sxs-lookup"><span data-stu-id="14492-163">Build the Java SimpleSend application using the following command.</span></span> <span data-ttu-id="14492-164">Dadurch wird sichergestellt, dass Ihre Anwendung die Verbindungsdetails für Ihren Event Hub verwendet:</span><span class="sxs-lookup"><span data-stu-id="14492-164">This ensures that your application  uses the connection details for your event hub:</span></span>

    ```azurecli
    mvn clean package -DskipTests
    ```

    <span data-ttu-id="14492-165">Der Buildprozess kann mehrere Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="14492-165">The build process may take several minutes to complete.</span></span> <span data-ttu-id="14492-166">Stellen Sie sicher, dass die Meldung **[INFO] BUILD SUCCESS** angezeigt wird, ehe Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="14492-166">Ensure that you see the **[INFO] BUILD SUCCESS** message before continuing.</span></span>

    ![Buildergebnisse für Absenderanwendung](../media-draft/5-sender-build.png)

## <a name="use-nano-to-edit-eventprocessorsamplejava"></a><span data-ttu-id="14492-168">Verwenden von Nano zum Bearbeiten von „EventProcessorSample.java“</span><span class="sxs-lookup"><span data-stu-id="14492-168">Use nano to edit EventProcessorSample.java</span></span>

<span data-ttu-id="14492-169">Sie konfigurieren nun eine **Empfänger**- (auch bekannt als **Abonnenten**- oder **Consumer**-) Anwendung, um Daten von Ihrem Event Hub zu erfassen.</span><span class="sxs-lookup"><span data-stu-id="14492-169">You'll now configure a **receiver** (also known as **subscribers** or **consumers**) application to ingest data from your event hub.</span></span>

<span data-ttu-id="14492-170">Für die Empfängeranwendung stehen zwei Methoden zur Verfügung: **EventHubReceiver** und **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="14492-170">For the receiver application, two methods are available; **EventHubReceiver** and **EventProcessorHost**.</span></span> <span data-ttu-id="14492-171">EventProcessorHost setzt auf EventHubReceiver auf, bietet aber eine einfachere Programmierschnittstelle als EventHubReceiver.</span><span class="sxs-lookup"><span data-stu-id="14492-171">EventProcessorHost is built on top of EventHubReceiver, but provides simpler programmatic interface than EventHubReceiver.</span></span> <span data-ttu-id="14492-172">EventProcessorHost kann Nachrichtenpartitionen unter Verwendung desselben Speicherkontos automatisch auf mehrere Instanzen von EventProcessorHost verteilen.</span><span class="sxs-lookup"><span data-stu-id="14492-172">EventProcessorHost can automatically distribute message partitions across multiple instances of EventProcessorHost using the same storage account.</span></span>

<span data-ttu-id="14492-173">In dieser Einheit verwenden Sie die EventProcessorHost-Methode.</span><span class="sxs-lookup"><span data-stu-id="14492-173">In this unit, you’ll use the EventProcessorHost method.</span></span> <span data-ttu-id="14492-174">Sie verwenden wiederum Nano und bearbeiten die Anwendung EventProcessorSample, indem Sie Ihren Event Hubs-Namespace, den Namen des Event Hubs und der freigegebenen Zugriffsrichtlinie sowie den Primärschlüssel, den Namen des Speicherkontos, die Verbindungszeichenfolge und den Containernamen hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="14492-174">You'll again use nano, and edit the EventProcessorSample application to add your Event Hubs namespace, event hub name, shared access policy name and primary key, storage account name, connection string, and container name.</span></span>

1. <span data-ttu-id="14492-175">Wechseln Sie mit dem folgenden Befehl zum Ordner **EventProcessorSample**:</span><span class="sxs-lookup"><span data-stu-id="14492-175">Change to the **EventProcessorSample** folder using the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. <span data-ttu-id="14492-176">Öffnen Sie in **Nano** die Datei **EventProcessorSample.java** mithilfe des folgenden Befehls:</span><span class="sxs-lookup"><span data-stu-id="14492-176">Open the **EventProcessorSample.java** file in the **nano** editor using the following command:</span></span>

    ```azurecli
    nano EventProcessorSample.java
    ```
1. <span data-ttu-id="14492-177">Suchen und ersetzen Sie in Nano die folgenden Zeichenfolgen:</span><span class="sxs-lookup"><span data-stu-id="14492-177">Locate and replace the following strings in the nano editor:</span></span>

    - <span data-ttu-id="14492-178">`----ServiceBusNamespaceName----` durch den Namespace Ihres Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="14492-178">`----ServiceBusNamespaceName----` with the name of your Event Hubs namespace.</span></span>
    - <span data-ttu-id="14492-179">`----EventHubName----` durch den Namen Ihres Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="14492-179">`----EventHubName----` with the name of your event hub.</span></span>
    - <span data-ttu-id="14492-180">`----SharedAccessSignatureKeyName----` durch **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="14492-180">`----SharedAccessSignatureKeyName----` with **RootManageSharedAccessKey**.</span></span>
    - <span data-ttu-id="14492-181">`----SharedAccessSignatureKey----` durch den Wert des Schlüssels **primaryKey** für Ihren Event Hubs-Namespace, den Sie zuvor gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="14492-181">`----SharedAccessSignatureKey----` with the value of the **primaryKey** key for your Event Hubs namespace that you saved earlier.</span></span>
    - <span data-ttu-id="14492-182">`----AzureStorageConnectionString----` durch die Verbindungszeichenfolge des Speicherkontos, die Sie zuvor gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="14492-182">`----AzureStorageConnectionString----` with your storage account connection string that you saved earlier.</span></span>
    - <span data-ttu-id="14492-183">`----StorageContainerName----` durch **messages**.</span><span class="sxs-lookup"><span data-stu-id="14492-183">`----StorageContainerName----` with **messages**.</span></span>
    - <span data-ttu-id="14492-184">`----HostNamePrefix----` durch den Namen Ihres Speicherkontos.</span><span class="sxs-lookup"><span data-stu-id="14492-184">`----HostNamePrefix----` with the name of your storage account.</span></span>

    ![Konfigurationsdetails für die Empfängeranwendung](../media-draft/5-receiver-configure.png)

1. <span data-ttu-id="14492-186">Speichern Sie **EventProcessorSample.java** mit dem folgenden Befehl, und beenden Sie Nano:</span><span class="sxs-lookup"><span data-stu-id="14492-186">Save **EventProcessorSample.java** using the following command and exit nano:</span></span>

    ```azurecli
    CTRL +O
    ENTER
    CTRL +X
    ```

## <a name="use-maven-to-build-eventprocessorsamplejava"></a><span data-ttu-id="14492-187">Verwenden von Maven zum Durchführen des Buildvorgangs für „EventProcessorSample.java“</span><span class="sxs-lookup"><span data-stu-id="14492-187">Use Maven to build EventProcessorSample.java</span></span>

1. <span data-ttu-id="14492-188">Wechseln Sie mit dem folgenden Befehl zum Hauptordner **EventProcessorSample**:</span><span class="sxs-lookup"><span data-stu-id="14492-188">Change to the main **EventProcessorSample** folder using the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. <span data-ttu-id="14492-189">Führen Sie den Buildvorgang für die Java-Anwendung SimpleSend mit dem folgenden Befehl durch.</span><span class="sxs-lookup"><span data-stu-id="14492-189">Build the Java SimpleSend application using the following command.</span></span> <span data-ttu-id="14492-190">Dadurch wird sichergestellt, dass Ihre Anwendung die Verbindungsdetails für Ihren Event Hub verwendet:</span><span class="sxs-lookup"><span data-stu-id="14492-190">This ensures that your application uses the connection details for your event hub:</span></span>

    ```azurecli
    mvn clean package -DskipTests
    ```

    <span data-ttu-id="14492-191">Der Buildprozess kann mehrere Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="14492-191">The build process may take several minutes to complete.</span></span> <span data-ttu-id="14492-192">Stellen Sie sicher, dass die Meldung **[INFO] BUILD SUCCESS** angezeigt wird, ehe Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="14492-192">Ensure that you see a **[INFO] BUILD SUCCESS** message before continuing.</span></span>

    ![Buildergebnisse für Empfängeranwendung](../media-draft/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a><span data-ttu-id="14492-194">Starten der Absender- und Empfänger-App</span><span class="sxs-lookup"><span data-stu-id="14492-194">Start the sender and receiver apps</span></span>

1. <span data-ttu-id="14492-195">Führen Sie die Java-Anwendung über die Befehlszeile aus, indem Sie den Befehl **java** verwenden und ein JAR-Paket angeben.</span><span class="sxs-lookup"><span data-stu-id="14492-195">Run Java application from the command line by using the **java** command, and specifying a .jar package.</span></span> <span data-ttu-id="14492-196">Verwenden Sie die folgenden Befehle, um die Anwendung SimpleSend zu starten:</span><span class="sxs-lookup"><span data-stu-id="14492-196">Use the following commands to start the SimpleSend application:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. <span data-ttu-id="14492-197">Wenn Sie **Send Complete...** (Sendevorgang abgeschlossen) sehen, drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="14492-197">When you see **Send Complete...**, press ENTER.</span></span>

    ![Ausführungsergebnisse für Absenderanwendung](../media-draft/5-sender-run.png)

1. <span data-ttu-id="14492-199">Starten Sie die Anwendung EventProcessorSample mit dem folgenden Befehl.</span><span class="sxs-lookup"><span data-stu-id="14492-199">Start the EventProcessorSample application using the following command.</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. <span data-ttu-id="14492-200">Wenn in der Konsole keine Nachrichten mehr angezeigt werden, drücken Sie die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="14492-200">When messages stop being displayed to the console, press ENTER.</span></span>

    ![Ausführungsergebnisse für Empfängeranwendung](../media-draft/5-receiver-run.png)

## <a name="summary"></a><span data-ttu-id="14492-202">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="14492-202">Summary</span></span>

<span data-ttu-id="14492-203">Sie haben soeben eine Absenderanwendung konfiguriert, die zum Senden von Nachrichten an Ihren Event Hub bereit ist.</span><span class="sxs-lookup"><span data-stu-id="14492-203">You've now configured a sender application ready to send messages to your event hub.</span></span> <span data-ttu-id="14492-204">Sie haben außerdem eine Empfängeranwendung konfiguriert, die zum Empfangen von Nachrichten von Ihren Event Hub bereit ist.</span><span class="sxs-lookup"><span data-stu-id="14492-204">You've also configured a receiver application ready to receive messages from your event hub.</span></span>
