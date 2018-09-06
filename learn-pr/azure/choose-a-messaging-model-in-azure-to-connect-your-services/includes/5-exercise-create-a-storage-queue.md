<span data-ttu-id="b44fd-101">In dieser Übung erstellen Sie ein neues Speicherkonto für Ihr Azure-Abonnement.</span><span class="sxs-lookup"><span data-stu-id="b44fd-101">In this exercise, you will create a new storage account in your Azure subscription.</span></span> <span data-ttu-id="b44fd-102">Verwenden Sie anschließend Azure Cloud Shell, um eine neue Warteschlange zu erstellen, eine Nachricht hinzuzufügen und diese dann zu lesen und aus der Warteschlange zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="b44fd-102">You will then use Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="b44fd-103">Hierbei handelt es sich um die gleichen Aktionen, die von Komponenten in einer verteilten Anwendung durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b44fd-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="b44fd-104">Beispielsweise kann eine mobile App einer Warteschlange eine Nachricht hinzufügen, die dann darauf wartet, dass ein Webdienst sie abruft und verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="b44fd-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="b44fd-105">Erstellen eines Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="b44fd-105">Create a storage account</span></span>

<span data-ttu-id="b44fd-106">Da Azure Storage-Warteschlangen ein Bestandteil von universellen Azure-Speicherkonten ist, müssen Sie zunächst ein Speicherkonto erstellen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-106">Since Azure Storage queues are part of Azure general purpose storage accounts, you must start by creating a storage account:</span></span>

1. <span data-ttu-id="b44fd-107">Navigieren Sie in einem Browser zum [Azure-Portal](http://portal.azure.com), und melden Sie sich mit Ihren regulären Anmeldeinformationen an.</span><span class="sxs-lookup"><span data-stu-id="b44fd-107">In a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your normal credentials.</span></span>
1. <span data-ttu-id="b44fd-108">Klicken Sie oben links auf **Alle Dienste**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-108">In the top left, click **All services**.</span></span>
1. <span data-ttu-id="b44fd-109">Scrollen Sie nach unten zum Abschnitt **Speicher**, und klicken Sie dann auf **Speicherkonten**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-109">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>
1. <span data-ttu-id="b44fd-110">Klicken Sie oben links auf dem Blatt **Speicherkonten** auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-110">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

    ![Screenshot: Blatt „Speicherkonten“ mit Hervorhebung der Option „Hinzufügen“](../images/5-create-a-storage-account-1.png)

1. <span data-ttu-id="b44fd-112">Geben Sie im Textfeld **Name** einen eindeutigen Namen für das Speicherkonto ein.</span><span class="sxs-lookup"><span data-stu-id="b44fd-112">In the **Name** text box, type a unique name for the storage account.</span></span>
1. <span data-ttu-id="b44fd-113">Stellen Sie unter **Bereitstellungsmodell** sicher, dass **Resource Manager** ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="b44fd-113">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
1. <span data-ttu-id="b44fd-114">Wählen Sie in der Dropdownliste **Kontoart** die Option **StorageV2 (universell, Version 2)** aus.</span><span class="sxs-lookup"><span data-stu-id="b44fd-114">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
1. <span data-ttu-id="b44fd-115">Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="b44fd-115">In the **Location** drop-down list, select a region near you.</span></span>
1. <span data-ttu-id="b44fd-116">Wählen Sie in der Dropdownliste **Replikation** den Wert **Lokal redundanter Speicher** aus.</span><span class="sxs-lookup"><span data-stu-id="b44fd-116">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
1. <span data-ttu-id="b44fd-117">Wählen Sie unter **Leistung** die Option **Standard** aus.</span><span class="sxs-lookup"><span data-stu-id="b44fd-117">Under **Performance**, select **Standard**.</span></span>
1. <span data-ttu-id="b44fd-118">Wählen Sie unter **Zugriffsebene** die Option **Kalt** aus.</span><span class="sxs-lookup"><span data-stu-id="b44fd-118">Under **Access tier**, select **Cool**.</span></span>
1. <span data-ttu-id="b44fd-119">Klicken Sie unter **Sichere Übertragung erforderlich** auf die Option **Deaktiviert**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-119">Under **Secure transfer required**, select **Disabled**.</span></span>
1. <span data-ttu-id="b44fd-120">Wählen Sie unter **Abonnement** Ihr Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="b44fd-120">Under **Subscription**, select your subscription.</span></span>

    ![Screenshot: Dialogfeld „Speicherkonto erstellen“](../images/5-create-a-storage-account-2.png)

1. <span data-ttu-id="b44fd-122">Klicken Sie unter **Ressourcengruppe** auf die Option **Neu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-122">Under **Resource group**, select **Create new**.</span></span> <span data-ttu-id="b44fd-123">Geben Sie **MusicSharingResourceGroup** in das Textfeld ein.</span><span class="sxs-lookup"><span data-stu-id="b44fd-123">In the text box, type **MusicSharingResourceGroup**.</span></span>
1. <span data-ttu-id="b44fd-124">Wählen Sie unter **Virtuelle Netzwerke** die Option **Deaktiviert** aus, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-124">Under **Virtual networks**, select **Disabled**, and then click **Create**.</span></span>

    ![Screenshot: Dialogfeld „Speicherkonto erstellen“ mit Hervorhebung der Option „Erstellen“](../images/5-create-a-storage-account-3.png)

<span data-ttu-id="b44fd-126">Azure erstellt das neue Speicherkonto und die neue Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="b44fd-126">Azure creates the new storage account and the new resource group.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="b44fd-127">Erstellen einer Warteschlange</span><span class="sxs-lookup"><span data-stu-id="b44fd-127">Create a queue</span></span>

<span data-ttu-id="b44fd-128">Nun ist das Speicherkonto erstellt, und Sie können eine neue Warteschlange hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b44fd-128">Now that the storage account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="b44fd-129">Sie müssen die Warteschlange mit PowerShell-Befehlen erstellen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-129">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="b44fd-130">Klicken Sie in der oberen rechten Ecke des Portals auf den Link **Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-130">In the top right of the portal, click the **Cloud Shell** link.</span></span>

    ![Screenshot: Azure-Portal mit Hervorhebung des Symbols „Cloud Shell“](../images/5-create-a-storage-queue-1.png)

1. <span data-ttu-id="b44fd-132">Klicken Sie im Bildschirm **Willkommen bei Azure Cloud Shell** auf **PowerShell (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-132">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>
1. <span data-ttu-id="b44fd-133">Wenn der Bildschirm **Sie haben keinen Speicher bereitgestellt** angezeigt wird, klicken Sie auf **Speicher erstellen**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-133">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>
1. <span data-ttu-id="b44fd-134">Wenn die `PS Azure`-Eingabeaufforderung angezeigt wird, geben Sie den folgenden Befehl ein, um das Speicherkonto aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="b44fd-134">When the `PS Azure` prompt appears, to obtain the storage account, type the following command.</span></span> <span data-ttu-id="b44fd-135">Ersetzen Sie `<storageaccountname>` durch den eindeutigen Namen Ihres Speicherkontos, und drücken Sie dann die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="b44fd-135">Substitute `<storageaccountname>` with the unique name of your storage account, and then press Enter:</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. <span data-ttu-id="b44fd-136">Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um den Kontext des Speicherkontos abzurufen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-136">To obtain the context of the storage account, type the following command, and then press Enter:</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

1. <span data-ttu-id="b44fd-137">Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um eine neue Warteschlange zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-137">To create a new queue, type the following command, and then press Enter:</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="b44fd-138">Hinzufügen einer Nachricht zu einer Warteschlange</span><span class="sxs-lookup"><span data-stu-id="b44fd-138">Add a message to the queue</span></span>

<span data-ttu-id="b44fd-139">Da Sie nun eine Warteschlange im Speicherkonto erstellt haben, können Sie ihr eine Nachricht hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b44fd-139">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="b44fd-140">Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um eine neue Nachricht zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-140">To create a new message, type the following command, and then press Enter:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. <span data-ttu-id="b44fd-141">Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um die neue Nachricht der neuen Warteschlange hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-141">To add the new message to the new queue, type the following command, and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. <span data-ttu-id="b44fd-142">Klicken Sie im Azure-Portal im Navigationsbereich auf der linken Seite auf **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-142">In the Azure portal, in the navigation on the left, click **All resources**.</span></span>
1. <span data-ttu-id="b44fd-143">Klicken Sie in der Liste der Ressourcen auf das Speicherkonto, das Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="b44fd-143">In the list of resources, click the storage account you created earlier.</span></span>
1. <span data-ttu-id="b44fd-144">Klicken Sie im Speicherkontoblatt auf **Storage-Explorer (Vorschau)**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-144">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>
1. <span data-ttu-id="b44fd-145">Klicken Sie im Storage-Explorer unter **WARTESCHLANGEN** auf **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-145">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="b44fd-146">Der Storage-Explorer zeigt die Nachricht an, die Sie gerade hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="b44fd-146">The Storage Explorer displays the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="b44fd-147">Abrufen und Entfernen der Nachricht</span><span class="sxs-lookup"><span data-stu-id="b44fd-147">Retrieve and remove the message</span></span>

<span data-ttu-id="b44fd-148">Zielkomponenten für eine Nachricht in einer Speicherwarteschlange müssen die Nachricht abrufen, die sich am Anfang der Warteschlange befindet.</span><span class="sxs-lookup"><span data-stu-id="b44fd-148">A destination component for a message in a Storage queue must retrieve the message at the front of the queue.</span></span> <span data-ttu-id="b44fd-149">Anschließend muss die Zielkomponente die Nachricht verarbeiten und aus der Warteschlange löschen, damit andere Komponenten diese nicht abrufen.</span><span class="sxs-lookup"><span data-stu-id="b44fd-149">Then the destination component must process the message, and delete it from the queue so that other components do not retrieve it.</span></span>

1. <span data-ttu-id="b44fd-150">Geben Sie den folgenden Befehl in Cloud Shell ein, und drücken Sie dann die EINGABETASTE, um die Nachricht am Anfang der Warteschlange abzurufen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-150">In Cloud Shell, to get the message at the front of the queue, type the following command, and then press Enter:</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. <span data-ttu-id="b44fd-151">Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um die Nachricht anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-151">To display the message, type the following command, and then press Enter:</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

1. <span data-ttu-id="b44fd-152">Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um alle Eigenschaften der Nachricht anzuzeigen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-152">To display all the properties of the message, type the following command, and then press Enter:</span></span>

    ```powershell
    $retrievedMessage
    ```

1. <span data-ttu-id="b44fd-153">Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE, um die Nachricht aus der Warteschlange zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-153">To remove the message from the queue, type the following command, and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. <span data-ttu-id="b44fd-154">Navigieren Sie im Azure-Portal zum Blatt „Speicherkonto“, um die Warteschlangenanzeige zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b44fd-154">In the Azure portal, to refresh the queue display, go to the Storage Account blade.</span></span> <span data-ttu-id="b44fd-155">Klicken Sie auf **Übersicht**, und klicken Sie dann auf **Storage-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-155">Click **Overview**, and then click **Storage Explorer**.</span></span>
1. <span data-ttu-id="b44fd-156">Klicken Sie unter **WARTESCHLANGEN** auf **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="b44fd-156">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="b44fd-157">Der Storage-Explorer zeigt an, dass die Warteschlange leer ist, da Sie die einzige Nachricht entfernt haben.</span><span class="sxs-lookup"><span data-stu-id="b44fd-157">The Storage Explorer shows that the queue is empty because you removed the only message.</span></span>

## <a name="cleanup"></a><span data-ttu-id="b44fd-158">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="b44fd-158">Cleanup</span></span>

<span data-ttu-id="b44fd-159">Geben Sie den folgenden Befehl in Cloud Shell ein, um alle im Rahmen dieser Übung erstellten Ressourcen zu entfernen:</span><span class="sxs-lookup"><span data-stu-id="b44fd-159">To remove all resources created during this exercise, enter the following command in Cloud Shell:</span></span> 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a><span data-ttu-id="b44fd-160">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="b44fd-160">Summary</span></span>

<span data-ttu-id="b44fd-161">Sie haben ein Speicherkonto in Ihrem Azure-Abonnement erstellt und darin eine neue Warteschlange.</span><span class="sxs-lookup"><span data-stu-id="b44fd-161">Here, you created a storage account in your Azure subscription, and created a new queue in it.</span></span> <span data-ttu-id="b44fd-162">Außerdem haben Sie PowerShell verwendet, um die Aktionen von verteilten Anwendungskomponenten zu simulieren, indem Sie der Warteschlange eine Nachricht hinzugefügt und diese anschließend abgerufen und entfernt haben.</span><span class="sxs-lookup"><span data-stu-id="b44fd-162">You also used PowerShell to simulate the actions of distributed application components by adding a message to the queue, and then retrieving and removing it.</span></span>

<span data-ttu-id="b44fd-163">Warteschlangen für Speicherkonten sind eine gute Lösung, wenn Nachrichten zwischen den Komponenten einer verteilten Anwendung übergeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="b44fd-163">Storage account queues are a good solution when you want to pass messages between the components of a distributed application.</span></span> <span data-ttu-id="b44fd-164">Verwenden Sie keine Speicherwarteschlangen, wenn Sie Ereignisse veröffentlichen möchten.</span><span class="sxs-lookup"><span data-stu-id="b44fd-164">Do not choose Storage queues when you want to publish events.</span></span>