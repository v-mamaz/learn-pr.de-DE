<span data-ttu-id="c1c63-101">In vorherigen Einheit haben Sie erfahren, wie eine serverlose Funktion das sichere Hochladen von Bildern in den blobspeicher aus einer Webanwendung ermöglichen kann.</span><span class="sxs-lookup"><span data-stu-id="c1c63-101">In the previous unit, you saw how a serverless function can facilitate the secure uploading of images to Blob storage from a web application.</span></span> <span data-ttu-id="c1c63-102">In diesem Modul erstellen Sie eine andere serverlose Funktion, um sehen Sie sich für die hochgeladene Bilder und Miniaturansichten daraus zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-102">In this module, you create another serverless function to watch for uploaded images and create thumbnails from them.</span></span>

## <a name="create-a-blob-storage-container-for-thumbnails"></a><span data-ttu-id="c1c63-103">Erstellen Sie einen Blob-Speichercontainer für Miniaturansichten</span><span class="sxs-lookup"><span data-stu-id="c1c63-103">Create a blob storage container for thumbnails</span></span>

<span data-ttu-id="c1c63-104">Die vollständige Größe-Images werden gespeichert, in einem Container namens **Images**.</span><span class="sxs-lookup"><span data-stu-id="c1c63-104">The full size images are stored in a container named **images**.</span></span> <span data-ttu-id="c1c63-105">Sie benötigen einen anderen Container zum Speichern von Miniaturansichten dieser Images.</span><span class="sxs-lookup"><span data-stu-id="c1c63-105">You need another container to store thumbnails of those images.</span></span>

1. <span data-ttu-id="c1c63-106">Stellen Sie sicher, dass Sie immer noch in der Cloud Shell (Bash) angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="c1c63-106">Ensure you are still signed in to the Cloud Shell (bash).</span></span>  <span data-ttu-id="c1c63-107">Wählen Sie andernfalls **EINGABETASTE fokusmodus** um eine Cloud Shell-Fenster zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-107">If not, select **Enter focus mode** to open a Cloud Shell window.</span></span> 

1. <span data-ttu-id="c1c63-108">Erstellen Sie einen neuen Container namens **Miniaturansichten** in Ihrem Storage-Konto mit öffentlichem Zugriff auf alle Blobs.</span><span class="sxs-lookup"><span data-stu-id="c1c63-108">Create a new container named **thumbnails** in your storage account with public access to all blobs.</span></span>

    ```azurecli
    az storage container create -n thumbnails --account-name <storage account name> --public-access blob
    ```


## <a name="create-a-blob-triggered-serverless-function"></a><span data-ttu-id="c1c63-109">Erstellen einer serverlosen blobtrigger-Funktion</span><span class="sxs-lookup"><span data-stu-id="c1c63-109">Create a blob-triggered serverless function</span></span>

<span data-ttu-id="c1c63-110">Ein Trigger definiert, wie eine Funktion aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="c1c63-110">A trigger defines how a function is invoked.</span></span> <span data-ttu-id="c1c63-111">Verwendet die Funktion, die als Nächstes Sie erstellen einen Blob-Trigger: die Funktion wird automatisch aufgerufen, wenn ein Blob (Image-Datei) in hochgeladen wird die **Images** Container.</span><span class="sxs-lookup"><span data-stu-id="c1c63-111">The function you create next uses a blob trigger: the function is automatically invoked when a blob (image file) is uploaded to the **images** container.</span></span> <span data-ttu-id="c1c63-112">Eine Funktion muss einen Trigger haben.</span><span class="sxs-lookup"><span data-stu-id="c1c63-112">A function must have one trigger.</span></span> <span data-ttu-id="c1c63-113">Trigger haben zugeordnete Daten, in üblicherweise mit der Nutzlast identisch sind, von der die Funktion ausgelöst wurde.</span><span class="sxs-lookup"><span data-stu-id="c1c63-113">Triggers have associated data, which is usually the payload that triggered the function.</span></span>

<span data-ttu-id="c1c63-114">Bindungen definieren, wie eine Funktion liest oder schreibt Daten in Azure oder Diensten von Drittanbietern.</span><span class="sxs-lookup"><span data-stu-id="c1c63-114">Bindings define how a function reads or writes data in Azure or third-party services.</span></span> <span data-ttu-id="c1c63-115">Diese Funktion erstellt eine Miniaturansicht des Bilds, das ausgelöst und speichert die Miniaturansicht in einem *Miniaturansichten* Container.</span><span class="sxs-lookup"><span data-stu-id="c1c63-115">This function creates a thumbnail version of the image that triggers it and saves the thumbnail in a *thumbnails* container.</span></span>

1. <span data-ttu-id="c1c63-116">Öffnen Sie Ihre Funktionen-app im Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="c1c63-116">Open your function app in the Azure Portal.</span></span>

1. <span data-ttu-id="c1c63-117">Klicken Sie im linken Navigationsbereich das Funktion app-Fenster, zeigen Sie auf **Funktionen** , und klicken Sie auf **+** zum Erstellen einer neuen serverlosen Funktion.</span><span class="sxs-lookup"><span data-stu-id="c1c63-117">In the function app window's left hand navigation, hover over **Functions** and click **+** to start creating a new serverless function.</span></span> <span data-ttu-id="c1c63-118">Wenn eine Seite "Quickstart" angezeigt wird, klicken Sie auf **benutzerdefinierte Funktion** um eine Liste von Funktionsvorlagen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-118">If a quickstart page appears, click **Custom function** to see a list of function templates.</span></span>

1. <span data-ttu-id="c1c63-119">Suchen der **BlobTrigger** Vorlage, und wählen Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="c1c63-119">Find the **BlobTrigger** template and select it.</span></span>

1. <span data-ttu-id="c1c63-120">Verwenden Sie diese Werte zum Erstellen einer Funktion, die Miniaturansichten erstellt wird, wie Bilder hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="c1c63-120">Use these values to create a function that creates thumbnails as images are uploaded.</span></span>

    | <span data-ttu-id="c1c63-121">Einstellung</span><span class="sxs-lookup"><span data-stu-id="c1c63-121">Setting</span></span>      |  <span data-ttu-id="c1c63-122">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="c1c63-122">Suggested value</span></span>   | <span data-ttu-id="c1c63-123">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="c1c63-123">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="c1c63-124">**Sprache**</span><span class="sxs-lookup"><span data-stu-id="c1c63-124">**Language**</span></span> | <span data-ttu-id="c1c63-125">C#- oder JavaScript</span><span class="sxs-lookup"><span data-stu-id="c1c63-125">C# or JavaScript</span></span> | <span data-ttu-id="c1c63-126">Wählen Sie Ihre bevorzugte Sprache an.</span><span class="sxs-lookup"><span data-stu-id="c1c63-126">Choose your preferred language.</span></span> |
    | <span data-ttu-id="c1c63-127">**Name Ihrer Funktion**</span><span class="sxs-lookup"><span data-stu-id="c1c63-127">**Name your function**</span></span> | <span data-ttu-id="c1c63-128">ResizeImage</span><span class="sxs-lookup"><span data-stu-id="c1c63-128">ResizeImage</span></span> | <span data-ttu-id="c1c63-129">Geben Sie diesen Namen genau wie angezeigt, damit die Anwendung die Funktion ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="c1c63-129">Type this name exactly as shown so the application can discover the function.</span></span> |
    | <span data-ttu-id="c1c63-130">**Path**</span><span class="sxs-lookup"><span data-stu-id="c1c63-130">**Path**</span></span> | <span data-ttu-id="c1c63-131">Bilder / {name}</span><span class="sxs-lookup"><span data-stu-id="c1c63-131">images/{name}</span></span> | <span data-ttu-id="c1c63-132">Führen Sie die Funktion ein, wenn eine Datei angezeigt, in wird der **Images** Container.</span><span class="sxs-lookup"><span data-stu-id="c1c63-132">Execute the function when a file appears in the **images** container.</span></span> |
    | <span data-ttu-id="c1c63-133">**Informationen zum Speicherkonto**</span><span class="sxs-lookup"><span data-stu-id="c1c63-133">**Storage account information**</span></span> | <span data-ttu-id="c1c63-134">AZURE_STORAGE_CONNECTION_STRING</span><span class="sxs-lookup"><span data-stu-id="c1c63-134">AZURE_STORAGE_CONNECTION_STRING</span></span> | <span data-ttu-id="c1c63-135">Verwenden Sie die Umgebungsvariable, die zuvor erstellt haben, durch die Verbindungszeichenfolge an.</span><span class="sxs-lookup"><span data-stu-id="c1c63-135">Use the environment variable previously created with the connection string.</span></span> |

    ![Geben Sie Einstellungen für die neue Funktion](../images/3-new-function.png)

1. <span data-ttu-id="c1c63-137">Klicken Sie auf **erstellen** zum Erstellen der Funktion.</span><span class="sxs-lookup"><span data-stu-id="c1c63-137">Click **Create** to create the function.</span></span>

1. <span data-ttu-id="c1c63-138">Wenn die Funktion erstellt wurde, klicken Sie auf **integrieren** klicken Sie zum Anzeigen der Trigger, Eingabe- und ausgabebindungen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-138">When the function is created, click **Integrate** to view its trigger, input, and output bindings.</span></span>

1. <span data-ttu-id="c1c63-139">Klicken Sie auf **neue Ausgabe** zum Erstellen eines neuen ausgabebindung.</span><span class="sxs-lookup"><span data-stu-id="c1c63-139">Click **New output** to create a new output binding.</span></span>

    ![Wählen Sie auf der Registerkarte "Integrieren" neue Ausgabe](../images/3-new-output.jpg)

1. <span data-ttu-id="c1c63-141">Wählen Sie **Azure Blob Storage** , und klicken Sie auf **wählen**.</span><span class="sxs-lookup"><span data-stu-id="c1c63-141">Select **Azure Blob Storage** and click **Select**.</span></span> <span data-ttu-id="c1c63-142">Möglicherweise finden Sie unter Bildlauf zu der **wählen** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="c1c63-142">You may have to scroll down to see the **Select** button.</span></span>

    ![Wählen Sie Azure Blob storage](../images/3-storage-output.jpg)

1. <span data-ttu-id="c1c63-144">Geben Sie die folgenden Werte ein.</span><span class="sxs-lookup"><span data-stu-id="c1c63-144">Enter the following values.</span></span>

    | <span data-ttu-id="c1c63-145">Einstellung</span><span class="sxs-lookup"><span data-stu-id="c1c63-145">Setting</span></span>      |  <span data-ttu-id="c1c63-146">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="c1c63-146">Suggested value</span></span>   | <span data-ttu-id="c1c63-147">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="c1c63-147">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="c1c63-148">**Blobparametername**</span><span class="sxs-lookup"><span data-stu-id="c1c63-148">**Blob parameter name**</span></span> | <span data-ttu-id="c1c63-149">Miniaturansicht</span><span class="sxs-lookup"><span data-stu-id="c1c63-149">thumbnail</span></span> | <span data-ttu-id="c1c63-150">Die Funktion verwendet den Parameter mit diesem Namen, um die Miniaturansicht zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="c1c63-150">The function uses the parameter with this name to write the thumbnail.</span></span> |
    | <span data-ttu-id="c1c63-151">**Funktionsrückgabewert verwenden**</span><span class="sxs-lookup"><span data-stu-id="c1c63-151">**Use function return value**</span></span> | <span data-ttu-id="c1c63-152">Nein</span><span class="sxs-lookup"><span data-stu-id="c1c63-152">No</span></span> |  |
    | <span data-ttu-id="c1c63-153">**Path**</span><span class="sxs-lookup"><span data-stu-id="c1c63-153">**Path**</span></span> | <span data-ttu-id="c1c63-154">Miniaturansichten / {name}</span><span class="sxs-lookup"><span data-stu-id="c1c63-154">thumbnails/{name}</span></span> | <span data-ttu-id="c1c63-155">Die Miniaturbilder werden geschrieben, auf einen Container namens **Miniaturansichten**.</span><span class="sxs-lookup"><span data-stu-id="c1c63-155">The thumbnails are written to a container named **thumbnails**.</span></span> |
    | <span data-ttu-id="c1c63-156">**Speicherkontoverbindung**</span><span class="sxs-lookup"><span data-stu-id="c1c63-156">**Storage account connection**</span></span> | <span data-ttu-id="c1c63-157">AZURE_STORAGE_CONNECTION_STRING</span><span class="sxs-lookup"><span data-stu-id="c1c63-157">AZURE_STORAGE_CONNECTION_STRING</span></span> | <span data-ttu-id="c1c63-158">Verwenden Sie die Umgebungsvariable, die zuvor erstellt haben, durch die Verbindungszeichenfolge an.</span><span class="sxs-lookup"><span data-stu-id="c1c63-158">Use the environment variable previously created with the connection string.</span></span> |

    ![Geben Sie Einstellungen für das Blob-ausgabebindung](../images/3-blob-output.png)

1. <span data-ttu-id="c1c63-160">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="c1c63-160">**JavaScript**</span></span>

    1. <span data-ttu-id="c1c63-161">(JavaScript) Klicken Sie auf **erweiterter Editor** in der oberen rechten Ecke des Fensters, um den JSON-Code, der die Bindungen darstellt anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-161">(JavaScript) Click on **Advanced editor** in the top right corner of the window to reveal the JSON representing the bindings.</span></span>

    1. <span data-ttu-id="c1c63-162">(JavaScript) In der `blobTrigger` binden, fügen Sie eine Eigenschaft, die mit dem Namen `dataType` mit einem Wert von `binary`.</span><span class="sxs-lookup"><span data-stu-id="c1c63-162">(JavaScript) In the `blobTrigger` binding, add a property named `dataType` with a value of `binary`.</span></span> <span data-ttu-id="c1c63-163">Dadurch wird die Bindung an den Blob-Inhalt an die Funktion als Binärdaten übergeben konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="c1c63-163">This configures the binding to pass the blob contents to the function as binary data.</span></span>

    ```json
    {
      "name": "myBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "images/{name}",
      "connection": "AZURE_STORAGE_CONNECTION_STRING",
      "dataType": "binary"
    }
    ```

1. <span data-ttu-id="c1c63-164">Klicken Sie auf **speichern** die neue Bindung erstellen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-164">Click **Save** to create the new binding.</span></span>

1. <span data-ttu-id="c1c63-165">**C#**</span><span class="sxs-lookup"><span data-stu-id="c1c63-165">**C#**</span></span>

    1. <span data-ttu-id="c1c63-166">(C#) Wählen Sie die **ResizeImage** Funktionsnamen im linken Navigationsbereich auf den Quellcode der Funktion zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-166">(C#) Select the **ResizeImage** function name on the left navigation to open the function's source code.</span></span>

    1. <span data-ttu-id="c1c63-167">(C#) Die Funktion erfordert ein NuGet-Paket namens **ImageResizer** zum Generieren von Miniaturansichten.</span><span class="sxs-lookup"><span data-stu-id="c1c63-167">(C#) The function requires a NuGet package called **ImageResizer** to generate the thumbnails.</span></span> <span data-ttu-id="c1c63-168">NuGet-Pakete werden hinzugefügt, um c#-Funktionen, die mit einem **"Project.JSON"** Datei.</span><span class="sxs-lookup"><span data-stu-id="c1c63-168">NuGet packages are added to C# functions using a **project.json** file.</span></span> <span data-ttu-id="c1c63-169">Um die Datei zu erstellen, klicken Sie auf **Ansichtsdateien** auf der rechten Seite, um die Dateien anzuzeigen, aus denen die Funktion besteht.</span><span class="sxs-lookup"><span data-stu-id="c1c63-169">To create the file, click **View Files** on the right to reveal the files that make up the function.</span></span>
    
    1. <span data-ttu-id="c1c63-170">(C#) Klicken Sie auf **hinzufügen** zum Hinzufügen einer neuen Datei mit dem Namen **"Project.JSON"**.</span><span class="sxs-lookup"><span data-stu-id="c1c63-170">(C#) Click **Add** to add a new file named **project.json**.</span></span>
    
    1. <span data-ttu-id="c1c63-171">(C#) Kopieren Sie den Inhalt der [ **/csharp/ResizeImage/project.json** ](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/project.json) in die neu erstellte Datei.</span><span class="sxs-lookup"><span data-stu-id="c1c63-171">(C#) Copy the contents of [**/csharp/ResizeImage/project.json**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/project.json) into the newly created file.</span></span> <span data-ttu-id="c1c63-172">Speichern Sie die Datei .</span><span class="sxs-lookup"><span data-stu-id="c1c63-172">Save the file.</span></span> <span data-ttu-id="c1c63-173">Pakete werden automatisch wiederhergestellt, wenn die Datei aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="c1c63-173">Packages are automatically restored when the file is updated.</span></span>
    
        ![die Datei "Project.JSON" mit ImageResizer](../images/3-project-json.png)
    
    1. <span data-ttu-id="c1c63-175">(C#) Wählen Sie **"Run.csx"** unter **Ansichtsdateien** und seinen Inhalt zu ersetzen, mit dem Inhalt [ **/csharp/ResizeImage/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run.csx).</span><span class="sxs-lookup"><span data-stu-id="c1c63-175">(C#) Select **run.csx** under **View Files** and replace its content with the content in [**/csharp/ResizeImage/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run.csx).</span></span>

1. <span data-ttu-id="c1c63-176">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="c1c63-176">**JavaScript**</span></span> 

    1. <span data-ttu-id="c1c63-177">(JavaScript) Diese Funktion erfordert die `jimp` Paket von Npm zum Ändern der Größe des Fotos.</span><span class="sxs-lookup"><span data-stu-id="c1c63-177">(JavaScript) This function requires the `jimp` package from npm to resize the photo.</span></span> <span data-ttu-id="c1c63-178">Klicken Sie zum Installieren des Npm-Pakets klicken Sie auf der Funktions-App-Namen im linken Navigationsbereich, und klicken Sie auf **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="c1c63-178">To install the npm package, click on the Function App's name on the left navigation and click **Platform features**.</span></span>

    1. <span data-ttu-id="c1c63-179">(JavaScript) Klicken Sie auf **Konsole** um ein Konsolenfenster anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-179">(JavaScript) Click **Console** to reveal a console window.</span></span>

    1. <span data-ttu-id="c1c63-180">(JavaScript) Führen Sie den Befehl `npm install jimp` in der Konsole.</span><span class="sxs-lookup"><span data-stu-id="c1c63-180">(JavaScript) Run the command `npm install jimp` in the console.</span></span> <span data-ttu-id="c1c63-181">Es dauert etwas, um den Vorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-181">It may take a minute or two to complete the operation.</span></span>

    1. <span data-ttu-id="c1c63-182">(JavaScript) Klicken Sie auf die **ResizeImage** Funktionsnamen im linken Navigationsbereich auf die Funktion anzuzeigen, ersetzen Sie alle **"Index.js"** mit dem Inhalt des [ **/javascript/ResizeImage / "Index.js"**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index.js).</span><span class="sxs-lookup"><span data-stu-id="c1c63-182">(JavaScript) Click on the **ResizeImage** function name in the left navigation to reveal the function, replace all of **index.js** with the content of [**/javascript/ResizeImage/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index.js).</span></span>

1. <span data-ttu-id="c1c63-183">Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="c1c63-183">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="c1c63-184">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c1c63-184">Click **Save**.</span></span> <span data-ttu-id="c1c63-185">Überprüfen Sie im Bereich Protokolle, um sicherzustellen, dass die Funktion wurde erfolgreich gespeichert. keine Fehler vorliegen.</span><span class="sxs-lookup"><span data-stu-id="c1c63-185">Check the logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="test-the-serverless-function"></a><span data-ttu-id="c1c63-186">Testen Sie die serverlose Funktion</span><span class="sxs-lookup"><span data-stu-id="c1c63-186">Test the serverless function</span></span>

1. <span data-ttu-id="c1c63-187">Öffnen Sie die Anwendung in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="c1c63-187">Open the application in a browser.</span></span> <span data-ttu-id="c1c63-188">Wählen Sie eine Bilddatei, und Laden Sie es hoch.</span><span class="sxs-lookup"><span data-stu-id="c1c63-188">Select an image file and upload it.</span></span> <span data-ttu-id="c1c63-189">Der Upload abgeschlossen ist, aber da wir die Möglichkeit zum Anzeigen von Bildern noch hinzugefügt haben, nicht die app das hochgeladene Foto angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c1c63-189">The upload completes, but because we haven't added the ability to display images yet, the app doesn't show the uploaded photo.</span></span>

1. <span data-ttu-id="c1c63-190">Vergewissern Sie sich in der Cloud Shell das Image hochgeladen wurde, um die **Images** Container.</span><span class="sxs-lookup"><span data-stu-id="c1c63-190">In the Cloud Shell, confirm the image was uploaded to the **images** container.</span></span>

    ```azurecli
    az storage blob list --account-name <storage account name> -c images -o table
    ```

1. <span data-ttu-id="c1c63-191">Vergewissern Sie sich die Miniaturansicht wurde erstellt, in einem Container namens **Miniaturansichten**.</span><span class="sxs-lookup"><span data-stu-id="c1c63-191">Confirm the thumbnail was created in a container named **thumbnails**.</span></span>

    ```azurecli
    az storage blob list --account-name <storage account name> -c thumbnails -o table
    ```

1. <span data-ttu-id="c1c63-192">Rufen Sie die URL der Miniaturansicht ab.</span><span class="sxs-lookup"><span data-stu-id="c1c63-192">Obtain the thumbnail's URL.</span></span>

    ```azurecli
    az storage blob url --account-name <storage account name> -c thumbnails -n <filename> --output tsv
    ```

    <span data-ttu-id="c1c63-193">Öffnen Sie die URL in einem Browser, und bestätigen Sie, dass die Miniaturansicht ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="c1c63-193">Open the URL in a browser and confirm the thumbnail was properly created.</span></span>

1. <span data-ttu-id="c1c63-194">Bevor Sie mit dem nächsten Tutorial fortfahren, löschen Sie alle Dateien in die **Images** und **Miniaturansichten** Container.</span><span class="sxs-lookup"><span data-stu-id="c1c63-194">Before moving on to the next tutorial, delete all files in the **images** and **thumbnails** containers.</span></span>

    ```azurecli
    az storage blob delete-batch -s images --account-name <storage account name>
    ```
    ```azurecli
    az storage blob delete-batch -s thumbnails --account-name <storage account name>
    ```


## <a name="summary"></a><span data-ttu-id="c1c63-195">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c1c63-195">Summary</span></span>

<span data-ttu-id="c1c63-196">In dieser Einheit erstellt Sie eine serverlose Funktion, um eine Miniaturansicht zu erstellen, wenn ein Bild in einen Blob-Speichercontainer hochgeladen wird.</span><span class="sxs-lookup"><span data-stu-id="c1c63-196">In this unit, you created a serverless function to create a thumbnail whenever an image is uploaded to a Blob storage container.</span></span> <span data-ttu-id="c1c63-197">Als Nächstes erfahren Sie, wie Sie Azure Cosmos DB zum Speichern und die Liste Bildmetadaten verwenden.</span><span class="sxs-lookup"><span data-stu-id="c1c63-197">Next, you learn how to use Azure Cosmos DB to store and list image metadata.</span></span>