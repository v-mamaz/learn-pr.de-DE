<span data-ttu-id="28616-101">In dieser Übung erstellen Sie ein neues Speicherkonto in Ihrem Azure-Abonnement.</span><span class="sxs-lookup"><span data-stu-id="28616-101">In this exercise, you will create a new Storage Account in your Azure subscription.</span></span> <span data-ttu-id="28616-102">Sie werden dann Azure Cloud Shell verwenden, um eine neue Warteschlange zu erstellen, eine Nachricht hinzuzufügen und dann diese Nachricht zu lesen und aus der Warteschlange zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="28616-102">You will then use the Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="28616-103">Hierbei handelt es sich um die gleichen Aktionen, die von Komponenten in einer verteilten Anwendung durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="28616-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="28616-104">Beispielsweise kann eine mobile App einer Warteschlange eine Nachricht hinzufügen, die dann darauf wartet, dass ein Webdienst sie abruft und verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="28616-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="28616-105">Erstellen eines Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="28616-105">Create a Storage Account</span></span>

<span data-ttu-id="28616-106">Speicherwarteschlangen gehören in Azure zu den Speicherkonten für allgemeine Zwecke.</span><span class="sxs-lookup"><span data-stu-id="28616-106">Since Storage queues are part of Azure general purpose Storage accounts.</span></span> <span data-ttu-id="28616-107">Sie müssen zunächst ein Speicherkonto erstellen:</span><span class="sxs-lookup"><span data-stu-id="28616-107">You must start by creating a Storage account:</span></span>

1. <span data-ttu-id="28616-108">Navigieren Sie in einem Browser zum [Azure-Portal](http://portal.azure.com), und melden Sie sich mit Ihren üblichen Anmeldeinformationen an.</span><span class="sxs-lookup"><span data-stu-id="28616-108">In a browser, navigate to the [Azure Portal](http://portal.azure.com) and sign in with your normal credentials.</span></span>
1. <span data-ttu-id="28616-109">Klicken Sie oben links auf **Alle Dienste**.</span><span class="sxs-lookup"><span data-stu-id="28616-109">In the top left, click **All services**.</span></span>
1. <span data-ttu-id="28616-110">Scrollen Sie nach unten zum Abschnitt **Speicher**, und klicken Sie dann auf **Speicherkonten**.</span><span class="sxs-lookup"><span data-stu-id="28616-110">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>
1. <span data-ttu-id="28616-111">Klicken Sie oben links auf dem Blatt **Speicherkonten** auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="28616-111">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

    ![Erstellen eines Speicherkontos](../images/5-create-a-storage-account-1.png)

1. <span data-ttu-id="28616-113">Geben Sie im Textfeld **Name** einen eindeutigen Namen für das Speicherkonto ein.</span><span class="sxs-lookup"><span data-stu-id="28616-113">In the **Name** text box, type a unique name for the storage account.</span></span>
1. <span data-ttu-id="28616-114">Stellen Sie unter **Bereitstellungsmodell** sicher, dass **Resource Manager** ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="28616-114">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
1. <span data-ttu-id="28616-115">Wählen Sie in der Dropdownliste **Kontoart** die Option **StorageV2 (universell, Version 2)** aus.</span><span class="sxs-lookup"><span data-stu-id="28616-115">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
1. <span data-ttu-id="28616-116">Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="28616-116">In the **Location** drop-down list, select a region near you.</span></span>
1. <span data-ttu-id="28616-117">Wählen Sie in der Dropdownliste **Replikation** den Wert **Lokal redundanter Speicher** aus.</span><span class="sxs-lookup"><span data-stu-id="28616-117">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
1. <span data-ttu-id="28616-118">Wählen Sie unter **Leistung** die Option **Standard** aus.</span><span class="sxs-lookup"><span data-stu-id="28616-118">Under **Performance**, select **Standard**.</span></span>
1. <span data-ttu-id="28616-119">Wählen Sie unter **Zugriffsebene** die Option **Kalt** aus.</span><span class="sxs-lookup"><span data-stu-id="28616-119">Under **Access tier**, select **Cool**.</span></span>
1. <span data-ttu-id="28616-120">Wählen Sie unter **Sichere Übertragung erforderlich** die Option **Deaktiviert** aus.</span><span class="sxs-lookup"><span data-stu-id="28616-120">Under **Secure transfer required** select, **Disabled**.</span></span>
1. <span data-ttu-id="28616-121">Wählen Sie unter **Abonnement** Ihr Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="28616-121">Under **Subscription**, select your subscription.</span></span>

    ![Erstellen eines Speicherkontos](../images/5-create-a-storage-account-2.png)

1. <span data-ttu-id="28616-123">Wählen Sie unter **Ressourcengruppe** die Option **Neu erstellen** aus, und klicken Sie dann im Textfeld auf den Typ **MusicSharingResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="28616-123">Under **Resource group** select **Create new**, and then in the textbox type **MusicSharingResourceGroup**.</span></span>
1. <span data-ttu-id="28616-124">Wählen Sie unter **Virtuelle Netzwerke** die Option **Deaktiviert** aus, und klicken Sie dann auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="28616-124">Under **Virtual networks** select **Disabled** and then click **Create**.</span></span>

    ![Erstellen eines Speicherkontos](../images/5-create-a-storage-account-3.png)

<span data-ttu-id="28616-126">Azure erstellt das neue Speicherkonto und die neue Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="28616-126">Azure creates the new storage account and the new resource group.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="28616-127">Erstellen einer Warteschlange</span><span class="sxs-lookup"><span data-stu-id="28616-127">Create a Queue</span></span>

<span data-ttu-id="28616-128">Nun ist das Speicherkonto erstellt, und Sie können eine neue Warteschlange hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="28616-128">Now that the Storage Account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="28616-129">Sie müssen die Warteschlange mit PowerShell-Befehlen erstellen:</span><span class="sxs-lookup"><span data-stu-id="28616-129">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="28616-130">Klicken Sie in der oberen rechten Ecke des Portals auf den Link **Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="28616-130">In the top right of the portal, click the **Cloud Shell** link.</span></span>

    ![Starten von Cloud Shell](../images/5-create-a-storage-queue-1.png)

1. <span data-ttu-id="28616-132">Klicken Sie im Bildschirm **Willkommen bei Azure Cloud Shell** auf **PowerShell (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="28616-132">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>
1. <span data-ttu-id="28616-133">Klicken Sie auf dem Bildschirm **Sie haben keinen Speicher bereitgestellt** auf **Speicher erstellen**.</span><span class="sxs-lookup"><span data-stu-id="28616-133">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>
1. <span data-ttu-id="28616-134">Wenn die `PS Azure`-Eingabeaufforderung angezeigt wird, geben Sie – um das Speicherkonto zu erhalten – den folgenden Befehl ein, wobei Sie `<storageaccountname>` durch den eindeutigen Namen Ihres Speicherkontos ersetzen, und drücken Sie dann die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-134">When the `PS Azure` prompt appears, to obtain the storage account, type the following command, substituting `<storageaccountname>` with the unique name of your storage account, and then press Enter:</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. <span data-ttu-id="28616-135">Um den Kontext des Speicherkontos zu erhalten, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-135">To obtain the context of the storage account, type the following command and then press Enter:</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

1. <span data-ttu-id="28616-136">Um eine neue Warteschlange zu erstellen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-136">To create a new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="28616-137">Hinzufügen einer Nachricht zur Warteschlange</span><span class="sxs-lookup"><span data-stu-id="28616-137">Add a Message to the Queue</span></span>

<span data-ttu-id="28616-138">Da Sie nun eine Warteschlange im Speicherkonto erstellt haben, können Sie ihr eine Nachricht hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="28616-138">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="28616-139">Um eine neue Nachricht zu erstellen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-139">To create a new message, type the following command and then press Enter:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. <span data-ttu-id="28616-140">Um der Warteschlange eine neue Nachricht hinzuzufügen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-140">To add the new message to the new queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. <span data-ttu-id="28616-141">Klicken Sie im Azure-Portal in der Navigation auf der linken Seite auf **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="28616-141">In the Azure Portal, in the navigation on the left, click **All resources**.</span></span>
1. <span data-ttu-id="28616-142">Klicken Sie in der Liste der Ressourcen auf das Speicherkonto, das Sie früher erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="28616-142">In the list of resources, click the storage account you created earlier.</span></span>
1. <span data-ttu-id="28616-143">Klicken Sie im Speicherkontoblatt auf **Storage-Explorer (Vorschau)**.</span><span class="sxs-lookup"><span data-stu-id="28616-143">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>
1. <span data-ttu-id="28616-144">Klicken Sie im Storage-Explorer unter **WARTESCHLANGEN** auf **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="28616-144">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="28616-145">Der Storage-Explorer zeigt die Nachricht an, die Sie gerade hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="28616-145">The Storage Explorer displays the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="28616-146">Abrufen und Entfernen der Nachricht</span><span class="sxs-lookup"><span data-stu-id="28616-146">Retrieve and Remove the Message</span></span>

<span data-ttu-id="28616-147">Eine Zielkomponente für eine Nachricht in einer Speicherwarteschlange muss die Nachricht am Anfang der Warteschlange abrufen, verarbeiten und dann aus der Warteschlange löschen, damit andere Komponenten sie nicht abrufen:</span><span class="sxs-lookup"><span data-stu-id="28616-147">A destination component for a message in a Storage queue, must retrieve the message at the front of the queue, process it, and then delete it from the queue so that other components do not retrieve it:</span></span>

1. <span data-ttu-id="28616-148">Um die Nachricht am Anfang der Warteschlange abzurufen, geben Sie den folgenden Befehl in Azure Cloud Shell ein, und drücken Sie dann die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-148">In the Azure Cloud Shell, to get the message at the front of the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. <span data-ttu-id="28616-149">Um die Nachricht anzuzeigen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-149">To display the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

1. <span data-ttu-id="28616-150">Um alle Eigenschaften der Nachricht anzuzeigen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-150">To display all the properties of the message, type the following command and then press Enter:</span></span>

    ```powershell
    $retrievedMessage
    ```

1. <span data-ttu-id="28616-151">Um die Nachricht aus der Warteschlange zu entfernen, geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:</span><span class="sxs-lookup"><span data-stu-id="28616-151">To remove the message from the queue, type the following command and then press Enter:</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. <span data-ttu-id="28616-152">Um die Warteschlangenanzeige zu aktualisieren, klicken Sie im Azure-Portal auf dem Speicherkontoblatt auf **Übersicht** und dann auf **Storage-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="28616-152">In the Azure Portal, to refresh the queue display, in the Storage Account blade, click **Overview** and then click **Storage Explorer**.</span></span>
1. <span data-ttu-id="28616-153">Klicken Sie unter **WARTESCHLANGEN** auf **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="28616-153">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="28616-154">Der Storage-Explorer zeigt an, dass die Warteschlange leer ist, da Sie die einzige Nachricht entfernt haben.</span><span class="sxs-lookup"><span data-stu-id="28616-154">The Storage Explorer shows that the queue is empty because you removed the only message.</span></span>

## <a name="cleanup"></a><span data-ttu-id="28616-155">Cleanup</span><span class="sxs-lookup"><span data-stu-id="28616-155">Cleanup</span></span>

<span data-ttu-id="28616-156">Geben Sie zum Entfernen aller in dieser Übung erstellten Ressourcen den folgenden Befehl in Azure Cloud Shell ein.</span><span class="sxs-lookup"><span data-stu-id="28616-156">To remove all resources created during this exercise enter the following command in the Azure Cloud Shell</span></span> 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a><span data-ttu-id="28616-157">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="28616-157">Summary</span></span>

<span data-ttu-id="28616-158">Hier haben Sie ein Speicherkonto in Ihrem Azure-Abonnement erstellt und darin eine neue Warteschlange.</span><span class="sxs-lookup"><span data-stu-id="28616-158">Here, you created a Storage Account in your Azure subscription and created a new queue in it.</span></span> <span data-ttu-id="28616-159">Sie haben PowerShell auch verwendet, um die Aktionen der verteilten Anwendungskomponenten durch Hinzufügen einer Nachricht zur Warteschlange und anschließendes Abrufen und Entfernen zu simulieren.</span><span class="sxs-lookup"><span data-stu-id="28616-159">You also used PowerShell to simulate the actions of distributed application components by adding a message to the queue and then retrieving and removing it.</span></span>

<span data-ttu-id="28616-160">Azure-Speicherkonto-Warteschlangen sind eine gute Lösung, wenn Nachrichten zwischen den Komponenten einer verteilten Anwendung übergeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="28616-160">Azure Storage Account queues are a good solution when you want to pass messages between the components of a distributed application.</span></span> <span data-ttu-id="28616-161">Wählen Sie Speicherwarteschlangen nicht aus, wenn Sie Ereignisse veröffentlichen möchten.</span><span class="sxs-lookup"><span data-stu-id="28616-161">Do not choose Storage queues when you want to publish events.</span></span>