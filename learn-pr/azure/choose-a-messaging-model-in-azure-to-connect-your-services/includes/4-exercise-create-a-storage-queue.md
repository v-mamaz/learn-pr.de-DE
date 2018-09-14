<span data-ttu-id="b4c77-101">In dieser Einheit erstellen Sie ein neues Speicherkonto in Ihrem Azure-Abonnement.</span><span class="sxs-lookup"><span data-stu-id="b4c77-101">In this unit, you will create a new storage account in your Azure subscription.</span></span> <span data-ttu-id="b4c77-102">Sie verwenden anschließend Azure Cloud Shell, um eine neue Warteschlange zu erstellen, eine Nachricht hinzuzufügen und dann diese Nachricht zu lesen und aus der Warteschlange zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="b4c77-102">You will then use Azure Cloud Shell to create a new queue, add a message to it, and then read that message and remove it from the queue.</span></span>

<span data-ttu-id="b4c77-103">Hierbei handelt es sich um die gleichen Aktionen, die von Komponenten in einer verteilten Anwendung durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b4c77-103">These are the same actions taken by components in a distributed application.</span></span> <span data-ttu-id="b4c77-104">Beispielsweise kann eine mobile App einer Warteschlange eine Meldung hinzufügen, die dann darauf wartet, dass ein Webdienst sie abruft und verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="b4c77-104">For example, a mobile app may add a message to a queue, where it waits for a web service to retrieve it and process it.</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="b4c77-105">Erstellen eines Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="b4c77-105">Create a storage account</span></span>
<!---TODO: Update for sandbox.--->

<span data-ttu-id="b4c77-106">Da Azure Storage-Warteschlangen ein Bestandteil von universellen Azure-Speicherkonten ist, müssen Sie zunächst ein Speicherkonto erstellen:</span><span class="sxs-lookup"><span data-stu-id="b4c77-106">Since Azure Storage queues are part of Azure general-purpose storage accounts, you must start by creating a storage account:</span></span>

1. <span data-ttu-id="b4c77-107">Navigieren Sie in einem Browser zum [Azure-Portal](https://portal.azure.com?azure-portal=true), und melden Sie sich mit Ihren regulären Anmeldeinformationen an.</span><span class="sxs-lookup"><span data-stu-id="b4c77-107">In a browser, navigate to the [Azure portal](https://portal.azure.com?azure-portal=true), and sign in with your normal credentials.</span></span>

1. <span data-ttu-id="b4c77-108">Klicken Sie oben links auf **Alle Dienste**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-108">In the top left, click **All services**.</span></span>

1. <span data-ttu-id="b4c77-109">Scrollen Sie nach unten zum Abschnitt **Speicher**, und klicken Sie dann auf **Speicherkonten**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-109">Scroll down to the **Storage** section, and then click **Storage accounts**.</span></span>

1. <span data-ttu-id="b4c77-110">Klicken Sie oben links auf dem Blatt **Speicherkonten** auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-110">At the top left of the **Storage accounts** blade, click **Add**.</span></span>

  ![Screenshot: Blatt „Speicherkonten“ mit Hervorhebung der Option „Hinzufügen“](../media-draft/4-create-a-storage-account-1.png)

1. <span data-ttu-id="b4c77-112">Geben Sie in das daraufhin angezeigte Dialogfeld die folgenden Informationen ein. Alle Optionen verfügen über ein `(i)`-Symbol im Portal, das Sie verwenden können, um mehr Informationen zur Funktionsweise dieser Option abzurufen.</span><span class="sxs-lookup"><span data-stu-id="b4c77-112">In the resulting dialog, enter the following information, each of these options has a `(i)` icon in the portal which you can use to get more information about what the option does.</span></span>

    - <span data-ttu-id="b4c77-113">Geben Sie in das Textfeld **Name** einen eindeutigen Namen für das Speicherkonto ein.</span><span class="sxs-lookup"><span data-stu-id="b4c77-113">In the **Name** text box, type a unique name for the storage account.</span></span>
    - <span data-ttu-id="b4c77-114">Stellen Sie unter **Bereitstellungsmodell** sicher, dass **Resource Manager** ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="b4c77-114">Under **Deployment model**, ensure that **Resource Manager** is selected.</span></span>
    - <span data-ttu-id="b4c77-115">Wählen Sie in der Dropdownliste **Kontoart** die Option **StorageV2 (universell, Version 2)** aus.</span><span class="sxs-lookup"><span data-stu-id="b4c77-115">In the **Account kind** drop-down list, select **Storage (general purpose v2)**.</span></span>
    - <span data-ttu-id="b4c77-116">Wählen Sie in der Dropdownliste **Standort** eine Region in Ihrer Nähe aus.</span><span class="sxs-lookup"><span data-stu-id="b4c77-116">In the **Location** drop-down list, select a region near you.</span></span>
    - <span data-ttu-id="b4c77-117">Wählen Sie in der Dropdownliste **Replikation** den Wert **Lokal redundanter Speicher** aus.</span><span class="sxs-lookup"><span data-stu-id="b4c77-117">In the **Replication** drop-down list, select **Locally-redundant storage (LRS)**.</span></span>
    - <span data-ttu-id="b4c77-118">Wählen Sie unter **Leistung** die Option **Standard** aus.</span><span class="sxs-lookup"><span data-stu-id="b4c77-118">Under **Performance**, select **Standard**.</span></span>
    - <span data-ttu-id="b4c77-119">Klicken Sie unter **Zugriffsebene** auf die Option **Kalt**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-119">Under **Access tier**, select **Cool**.</span></span>
    - <span data-ttu-id="b4c77-120">Klicken Sie unter **Sichere Übertragung erforderlich** auf die Option **Deaktiviert**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-120">Under **Secure transfer required**, select **Disabled**.</span></span>
    - <span data-ttu-id="b4c77-121">Wählen Sie unter **Abonnement** Ihr Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="b4c77-121">Under **Subscription**, select your subscription.</span></span>
    - <span data-ttu-id="b4c77-122">Klicken Sie unter **Ressourcengruppe** auf die Option **Neu erstellen**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-122">Under **Resource group**, select **Create new**.</span></span> <span data-ttu-id="b4c77-123">Geben Sie **MusicSharingResourceGroup** in das Textfeld ein.</span><span class="sxs-lookup"><span data-stu-id="b4c77-123">In the text box, type **MusicSharingResourceGroup**.</span></span>
    - <span data-ttu-id="b4c77-124">Klicken Sie unter **Virtuelle Netzwerke** auf die Option **Deaktiviert**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-124">Under **Virtual networks**, select **Disabled**.</span></span> 

    ![Screenshot: Dialogfeld „Speicherkonto erstellen“](../media-draft/4-create-a-storage-account-2.png)

1. <span data-ttu-id="b4c77-126">Klicken Sie auf **Erstellen**. Dann erstellt Azure eine neue Ressourcengruppe und ein neues Speicherkonto, das diesem zugeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="b4c77-126">Click **Create** - Azure will create a new resource group and a new storage account associated with it.</span></span>

    ![Screenshot: Dialogfeld „Speicherkonto erstellen“ mit Hervorhebung der Option „Erstellen“](../media-draft/4-create-a-storage-account-3.png)

## <a name="create-a-queue"></a><span data-ttu-id="b4c77-128">Erstellen einer Warteschlange</span><span class="sxs-lookup"><span data-stu-id="b4c77-128">Create a queue</span></span>

<span data-ttu-id="b4c77-129">Nun ist das Speicherkonto erstellt, und Sie können eine neue Warteschlange hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b4c77-129">Now that the storage account has been created, you can add a new queue to it.</span></span> <span data-ttu-id="b4c77-130">Sie müssen die Warteschlange mit PowerShell-Befehlen erstellen:</span><span class="sxs-lookup"><span data-stu-id="b4c77-130">You must create the queue by using PowerShell commands:</span></span>

1. <span data-ttu-id="b4c77-131">Klicken Sie in der oberen rechten Ecke des Portals auf den **Cloud Shell**-Link `(>_)`.</span><span class="sxs-lookup"><span data-stu-id="b4c77-131">In the top right of the portal, click the **Cloud Shell** link `(>_)`.</span></span>

    ![Screenshot: Azure-Portal mit Hervorhebung des Symbols „Cloud Shell“](../media-draft/4-create-a-storage-queue-1.png)

1. <span data-ttu-id="b4c77-133">Klicken Sie im Bildschirm **Welcome to Azure Cloud Shell** (Willkommen bei Azure Cloud Shell) auf **PowerShell (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-133">In the **Welcome to Azure Cloud Shell** screen, click **PowerShell (Linux)**.</span></span>

1. <span data-ttu-id="b4c77-134">Klicken Sie auf dem Bildschirm **You have no storage mounted** (Sie haben keinen Speicher bereitgestellt) auf **Speicher erstellen**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-134">If the **You have no storage mounted** screen appears, click **Create storage**.</span></span>

1. <span data-ttu-id="b4c77-135">Wenn die `PS Azure`-Eingabeaufforderung angezeigt wird, das Speicherkonto aufzurufen, geben Sie den folgenden Befehl ein.</span><span class="sxs-lookup"><span data-stu-id="b4c77-135">When the `PS Azure` prompt appears, to obtain the storage account, type the following command.</span></span> <span data-ttu-id="b4c77-136">Ersetzen Sie den `<storageaccountname>` durch den eindeutigen Namen des Speicherkontos, das Sie zuvor erstellt haben, und drücken Sie auf **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-136">Substitute `<storageaccountname>` with the unique name of your storage account you created above, and then press **Enter**.</span></span> <span data-ttu-id="b4c77-137">Das entstandene Objekt soll einer Variablen mit dem Namen `$storageaccount` zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="b4c77-137">We want to assign the resulting object to a variable named `$storageaccount`.</span></span>

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. <span data-ttu-id="b4c77-138">Als nächstes wird der _Kontext_ des Speicherkontos benötigt. Dabei handelt es sich um eine Eigenschaft das zurückgegebenen Objekts.</span><span class="sxs-lookup"><span data-stu-id="b4c77-138">Next, we need to get the storage account _context_ - this is a property on the returned object.</span></span> <span data-ttu-id="b4c77-139">Dieses soll einer anderen Variablen mit dem Namen `$context` zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="b4c77-139">Let's assign it to another variable named `$context`.</span></span>

    ```powershell
    $context = $storageaccount.Context
    ```

1. <span data-ttu-id="b4c77-140">Danach kann die Warteschlange erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="b4c77-140">Now we are ready to create the queue.</span></span> <span data-ttu-id="b4c77-141">Verwenden Sie den `New-AzureStorageQueue`-Befehl, und weisen Sie ihn einer `$messageQueue`-Variablen zu.</span><span class="sxs-lookup"><span data-stu-id="b4c77-141">Use the `New-AzureStorageQueue` command and assign it to a `$messageQueue` variable.</span></span>
    - <span data-ttu-id="b4c77-142">Übergeben Sie einen `-Name`-Parameter mit dem Wert `musicsharingmessages`.</span><span class="sxs-lookup"><span data-stu-id="b4c77-142">Pass a `-Name` parameter with the value `musicsharingmessages`</span></span>
    - <span data-ttu-id="b4c77-143">Übergeben Sie einen `-Context`-Parameter mit dem Wert, den Sie im Schritt zuvor abgerufen haben.</span><span class="sxs-lookup"><span data-stu-id="b4c77-143">Pass a `-Context` parameter with the value you retrieved in the previous step.</span></span>

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a><span data-ttu-id="b4c77-144">Hinzufügen einer Meldung zu einer Warteschlange</span><span class="sxs-lookup"><span data-stu-id="b4c77-144">Add a message to the queue</span></span>

<span data-ttu-id="b4c77-145">Da Sie nun eine Warteschlange im Speicherkonto erstellt haben, können Sie ihr eine Meldung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b4c77-145">Now that you have created a queue in the storage account, you can add a message to it.</span></span>

1. <span data-ttu-id="b4c77-146">Verwenden Sie die `New-Object`-Methode, um eine .NET-`CloudQueueMessage` mit einem zeichenfolgenbasierten Argument zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="b4c77-146">To create a new message, use the `New-Object` method to create a .NET `CloudQueueMessage` with a string-based argument:</span></span>

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. <span data-ttu-id="b4c77-147">Übergeben Sie die erstellte `CloudQueueMessage` an die `AddMessageAsync`-Methode in Ihrer `$messageQueue`-Warteschlange, um die neue Meldung an die neue Warteschlange zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="b4c77-147">To add the new message to the new queue, pass the created `CloudQueueMessage` to the `AddMessageAsync` method on your `$messageQueue` queue.</span></span>

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

## <a name="verify-the-message-was-queued"></a><span data-ttu-id="b4c77-148">Überprüfen, ob die Meldung in die Warteschlange aufgenommen wurde</span><span class="sxs-lookup"><span data-stu-id="b4c77-148">Verify the message was queued</span></span>

<span data-ttu-id="b4c77-149">Sie können den **Storage-Explorer** verwenden, um mit der Warteschlange zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="b4c77-149">We can use the **Storage Explorer** to work with our queue.</span></span> <span data-ttu-id="b4c77-150">Zwei Variationen sind verfügbar:</span><span class="sxs-lookup"><span data-stu-id="b4c77-150">There are two variations available:</span></span>

- <span data-ttu-id="b4c77-151">Eine plattformübergreifende Desktop-App für Linux, macOS und Windows, die Sie herunterladen können</span><span class="sxs-lookup"><span data-stu-id="b4c77-151">A cross-platform desktop app for Linux, macOS, and Windows that you can download.</span></span>
- <span data-ttu-id="b4c77-152">Eine Webvorschauversion für das Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="b4c77-152">A preview web version in the Azure portal.</span></span> <span data-ttu-id="b4c77-153">Im Folgenden wird die Webversion verwendet, aber Sie können auch die Desktopversion installieren. Die Anweisungen sind ähnlich.</span><span class="sxs-lookup"><span data-stu-id="b4c77-153">This is the one we will use here, but you can install the desktop version if you prefer - the instructions are very similar.</span></span>

1. <span data-ttu-id="b4c77-154">Klicken Sie im Azure-Portal in der Navigation auf der linken Seite auf **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-154">In the Azure portal, in the navigation on the left, click **All resources**.</span></span>

1. <span data-ttu-id="b4c77-155">Klicken Sie in der Liste der Ressourcen auf das Speicherkonto, das Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="b4c77-155">In the list of resources, click the storage account you created earlier.</span></span>

1. <span data-ttu-id="b4c77-156">Klicken Sie im Speicherkontoblatt auf **Storage-Explorer (Vorschau)**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-156">In the storage account blade, click **Storage Explorer (Preview)**.</span></span>

1. <span data-ttu-id="b4c77-157">Klicken Sie im Storage-Explorer unter **WARTESCHLANGEN** auf **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-157">In the Storage Explorer, under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="b4c77-158">Der Storage-Explorer sollte die Meldung anzeigen, die Sie gerade hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="b4c77-158">The Storage Explorer should display the message you just added.</span></span>

## <a name="retrieve-and-remove-the-message"></a><span data-ttu-id="b4c77-159">Abrufen und Entfernen der Meldung</span><span class="sxs-lookup"><span data-stu-id="b4c77-159">Retrieve and remove the message</span></span>

<span data-ttu-id="b4c77-160">Zielkomponenten für eine Meldung in einer Speicherwarteschlange müssen die Meldung abrufen, die sich am Anfang der Warteschlange befindet.</span><span class="sxs-lookup"><span data-stu-id="b4c77-160">A destination component for a message in a Storage queue must retrieve the message at the front of the queue.</span></span> <span data-ttu-id="b4c77-161">Anschließend muss die Zielkomponente die Meldung verarbeiten und aus der Warteschlange löschen, damit andere Komponenten diese nicht abrufen.</span><span class="sxs-lookup"><span data-stu-id="b4c77-161">Then the destination component must process the message and delete it from the queue so that other components do not retrieve it.</span></span>

1. <span data-ttu-id="b4c77-162">Sie können die erste in PowerShell verfügbare Meldung mithilfe der `GetMessageAsync`-Methode in der Warteschlange abrufen.</span><span class="sxs-lookup"><span data-stu-id="b4c77-162">We can retrieve the first available message in PowerShell using the `GetMessageAsync` method on our queue.</span></span> <span data-ttu-id="b4c77-163">Es handelt sich dabei um eine asynchrone .NET-Methode. Da dies an dieser Stelle zu lange dauern würde, können Sie einfach die `Result`-Eigenschaft verwenden, um den Rückgabewert abzurufen.</span><span class="sxs-lookup"><span data-stu-id="b4c77-163">This is an asynchronous .NET method, since we want to wait for it we can just use the `Result` property to get the return value.</span></span> <span data-ttu-id="b4c77-164">Dadurch wird ein Objekt zurückgegeben, das für die Meldung steht, die einem Parameter zugewiesen werden kann.</span><span class="sxs-lookup"><span data-stu-id="b4c77-164">This returns an object representing the message which we can assign to a parameter.</span></span>

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. <span data-ttu-id="b4c77-165">Diese Meldung wird in Text dargestellt, wenn Sie `AsString` aufrufen. Dadurch wird der Wert auf der Konsole zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="b4c77-165">We can get a textual version of the message by calling `AsString` - this will output the value on the console.</span></span>

    ```powershell
    $retrievedMessage.AsString
    ```

1. <span data-ttu-id="b4c77-166">Stattdessen können Sie auch alle Eigenschaften der Meldung anzeigen, indem Sie nur den Variablennamen eingeben und die **EINGABETASTE** drücken.</span><span class="sxs-lookup"><span data-stu-id="b4c77-166">Or, we can display all the properties of the message by just typing the variable name and pressing **Enter**.</span></span>

    ```powershell
    $retrievedMessage
    ```

1. <span data-ttu-id="b4c77-167">`GetMessageAsync` entfernt die Meldung *nicht*, sondern gibt sie nur zurück. Dadurch kann der Prozess fortgesetzt werden.</span><span class="sxs-lookup"><span data-stu-id="b4c77-167">`GetMessageAsync` does *not* remove the message - it simply returns it, which means we could process it again.</span></span> <span data-ttu-id="b4c77-168">Wenn Sie diese Meldung aus der Warteschlange entfernen möchten, können Sie die `DeleteMessageAsync`-Methode für die Warteschlange verwenden. Dafür muss die Meldung übergeben werden, die entfernt werden soll.</span><span class="sxs-lookup"><span data-stu-id="b4c77-168">To remove the message from the queue, we can use the `DeleteMessageAsync` method on the queue - this requires that we pass in the message we want to remove.</span></span>

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. <span data-ttu-id="b4c77-169">Wenn Sie prüfen möchten, ob die Meldung entfernt wurde, aktualisieren Sie die Warteschlangenanzeige im Azure-Portal, indem Sie zum Blatt „Speicherkonto“ navigieren und auf **Übersicht > Storage-Explorer** klicken.</span><span class="sxs-lookup"><span data-stu-id="b4c77-169">To verify that the message is gone, refresh the queue display in the Azure portal by navigating to the Storage Account blade and selecting **Overview > Storage Explorer**.</span></span> <span data-ttu-id="b4c77-170">Klicken Sie unter **WARTESCHLANGEN** auf **musicsharingmessages**.</span><span class="sxs-lookup"><span data-stu-id="b4c77-170">Under **QUEUES**, click **musicsharingmessages**.</span></span> <span data-ttu-id="b4c77-171">Der Storage-Explorer sollte jetzt anzeigen, dass die Warteschlange leer ist, da Sie die einzige Meldung entfernt haben.</span><span class="sxs-lookup"><span data-stu-id="b4c77-171">The Storage Explorer should now show that the queue is empty because you removed the only message.</span></span>


## <a name="summary"></a><span data-ttu-id="b4c77-172">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="b4c77-172">Summary</span></span>
<span data-ttu-id="b4c77-173">Warteschlangen für Speicherkonten sind eine gute Lösung, wenn _Meldungen_ zwischen den Komponenten einer verteilten Anwendung übergeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="b4c77-173">Storage account queues are a good solution when you want to pass _messages_ between the components of a distributed application.</span></span> <span data-ttu-id="b4c77-174">Sie eignen sich besonders, wenn Sie sicherstellen wollen, dass die Meldungen in der Reihenfolge zugestellt werden, in der Sie sie senden.</span><span class="sxs-lookup"><span data-stu-id="b4c77-174">This is a great choice if you want to guarantee delivery or to ensure that messages are delivered in the same order you sent them.</span></span> <span data-ttu-id="b4c77-175">Allerdings wird bei der Verwendung von Warteschlangen vorausgesetzt, dass Sender und Empfänger das Format der Daten kennen, die übergeben werden. Es besteht automatisch ein Datenvertrag, durch den die beiden miteinander kommunizierenden Dienste aneinander gekoppelt sind.</span><span class="sxs-lookup"><span data-stu-id="b4c77-175">However, queues imply that the sender and receiver understand the format of the data being passed - there's an implied data contract between them which adds a bit of "coupling" between the two communicating services.</span></span>

<span data-ttu-id="b4c77-176">Nicht alle Architekturen müssen formatierte Datenblöcke übergeben. Einige Architekturen benötigen nur einfache Meldungen, die gesendet werden sollen, ohne zu wissen, wie die Meldung verarbeitet wird.</span><span class="sxs-lookup"><span data-stu-id="b4c77-176">Not all architectures need to pass formatted blocks of data, some really just need simple messages which we want to fire-and-forget without any knowledge of what will handle the message.</span></span> <span data-ttu-id="b4c77-177">In solchen Szenarios eignen sich Warteschlangen nicht.</span><span class="sxs-lookup"><span data-stu-id="b4c77-177">In these scenarios, a queue isn't a great choice.</span></span> <span data-ttu-id="b4c77-178">Daher sollten Sie sich in der nächsten Einheit über eine Meldungsstrategie informieren, die sich besser für diesen Kommunikationsstil eignet.</span><span class="sxs-lookup"><span data-stu-id="b4c77-178">Let's look at another messaging strategy which is more suited to this style of communication.</span></span>