<span data-ttu-id="7b0ee-101">In der vorherigen Einheit wurde beschrieben, wie mit einer serverlosen Funktion das sichere Hochladen von Bildern in Blobspeicher aus einer Webanwendung möglich ist.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-101">In the previous unit, you saw how a serverless function can facilitate the secure uploading of images to Blob storage from a web application.</span></span> <span data-ttu-id="7b0ee-102">In diesem Modul erstellen Sie eine weitere serverlose Funktion, um hochgeladene Bilder zu ermitteln und daraus Miniaturansichten zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-102">In this module, you create another serverless function to watch for uploaded images and create thumbnails from them.</span></span>

## <a name="create-a-blob-storage-container-for-thumbnails"></a><span data-ttu-id="7b0ee-103">Erstellen eines Blobspeichercontainers für Miniaturansichten</span><span class="sxs-lookup"><span data-stu-id="7b0ee-103">Create a Blob storage container for thumbnails</span></span>

<span data-ttu-id="7b0ee-104">Die Bilder mit vollständiger Größe werden in einem Container mit dem Namen **images** gespeichert.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-104">The full-size images are stored in a container named **images**.</span></span> <span data-ttu-id="7b0ee-105">Sie benötigen einen weiteren Container, um die Miniaturansichten dieser Bilder zu speichern.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-105">You need another container to store thumbnails of those images.</span></span>

1. <span data-ttu-id="7b0ee-106">Stellen Sie sicher, dass Sie noch in Cloud Shell (Bash) angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-106">Ensure you're still signed in to Cloud Shell (Bash).</span></span> <span data-ttu-id="7b0ee-107">Klicken Sie andernfalls auf die Option **Enter focus mode** (Fokusmodus aktivieren), um ein Cloud Shell-Fenster zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-107">If you aren't, select **Enter focus mode** to open a Cloud Shell window.</span></span> 

1. <span data-ttu-id="7b0ee-108">Erstellen Sie unter Ihrem Speicherkonto einen neuen Container mit dem Namen **thumbnails**, der über öffentlichen Zugriff auf alle Blobs verfügt.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-108">Create a new container named **thumbnails** in your Storage account with public access to all blobs.</span></span>

    ```azurecli
    az storage container create -n thumbnails --account-name <storage account name> --public-access blob
    ```


## <a name="create-a-blob-triggered-serverless-function"></a><span data-ttu-id="7b0ee-109">Erstellen einer per Blob ausgelösten serverlosen Funktion</span><span class="sxs-lookup"><span data-stu-id="7b0ee-109">Create a blob-triggered serverless function</span></span>

<span data-ttu-id="7b0ee-110">Ein Trigger definiert, wie eine Funktion aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-110">A trigger defines how a function is invoked.</span></span> <span data-ttu-id="7b0ee-111">Die Funktion, die Sie als Nächstes erstellen, verwendet einen Blobtrigger.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-111">The function you create next uses a blob trigger.</span></span> <span data-ttu-id="7b0ee-112">Die Funktion wird automatisch aufgerufen, wenn ein Blob (Bilddatei) in den Container **images** hochgeladen wird.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-112">The function is automatically invoked when a blob (image file) is uploaded to the **images** container.</span></span> <span data-ttu-id="7b0ee-113">Eine Funktion muss über einen Trigger verfügen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-113">A function must have one trigger.</span></span> <span data-ttu-id="7b0ee-114">Trigger haben zugeordnete Daten, die üblicherweise mit der Nutzlast identisch sind, von der die Funktion ausgelöst wurde.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-114">Triggers have associated data, which is usually the payload that triggered the function.</span></span>

<span data-ttu-id="7b0ee-115">Mit Bindungen wird definiert, wie eine Funktion das Lesen oder Schreiben von Daten in Azure oder Drittanbieterdiensten durchführt.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-115">Bindings define how a function reads or writes data in Azure or third-party services.</span></span> <span data-ttu-id="7b0ee-116">Diese Funktion erstellt eine Miniaturansichtversion des Bilds, von dem sie ausgelöst wird, und speichert die Miniaturansicht im Container *thumbnails*.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-116">This function creates a thumbnail version of the image that triggers it and saves the thumbnail in a *thumbnails* container.</span></span>

1. <span data-ttu-id="7b0ee-117">Öffnen Sie Ihre Funktions-App im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-117">Open your Functions app in the Azure portal.</span></span>

1. <span data-ttu-id="7b0ee-118">Zeigen Sie im Fenster „Funktionen-App“ im linken Navigationsbereich auf **Funktionen**, und klicken Sie auf das Pluszeichen (+), um eine neue serverlose Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-118">In the Functions app window's left navigation, point to **Functions** and click the plus sign (+) to create a new serverless function.</span></span> <span data-ttu-id="7b0ee-119">Klicken Sie bei der Anzeige einer Schnellstartseite auf **Benutzerdefinierte Funktion**, um eine Liste mit Funktionsvorlagen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-119">If a quickstart page appears, click **Custom function** to see a list of function templates.</span></span>

1. <span data-ttu-id="7b0ee-120">Suchen Sie nach der Vorlage **BlobTrigger**, und wählen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-120">Find the **BlobTrigger** template and select it.</span></span>

1. <span data-ttu-id="7b0ee-121">Verwenden Sie diese Werte, um eine Funktion zu erstellen, mit der beim Hochladen von Bildern Miniaturansichten erstellt werden:</span><span class="sxs-lookup"><span data-stu-id="7b0ee-121">Use these values to create a function that creates thumbnails as images are uploaded:</span></span>

    | <span data-ttu-id="7b0ee-122">Einstellung</span><span class="sxs-lookup"><span data-stu-id="7b0ee-122">Setting</span></span>      |  <span data-ttu-id="7b0ee-123">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="7b0ee-123">Suggested value</span></span>   | <span data-ttu-id="7b0ee-124">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7b0ee-124">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="7b0ee-125">**Sprache**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-125">**Language**</span></span> | <span data-ttu-id="7b0ee-126">C# oder JavaScript</span><span class="sxs-lookup"><span data-stu-id="7b0ee-126">C# or JavaScript</span></span> | <span data-ttu-id="7b0ee-127">Wählen Sie Ihre bevorzugte Sprache aus.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-127">Choose your preferred language.</span></span> |
    | <span data-ttu-id="7b0ee-128">**Name Ihrer Funktion**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-128">**Name your function**</span></span> | <span data-ttu-id="7b0ee-129">ResizeImage</span><span class="sxs-lookup"><span data-stu-id="7b0ee-129">ResizeImage</span></span> | <span data-ttu-id="7b0ee-130">Geben Sie diesen Namen genau wie hier angezeigt ein, damit die Anwendung die Funktion ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-130">Enter this name exactly as shown, so the application can discover the function.</span></span> |
    | <span data-ttu-id="7b0ee-131">**Pfad**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-131">**Path**</span></span> | <span data-ttu-id="7b0ee-132">images/{Name}</span><span class="sxs-lookup"><span data-stu-id="7b0ee-132">images/{name}</span></span> | <span data-ttu-id="7b0ee-133">Führen Sie die Funktion aus, wenn im Container **images** eine Datei angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-133">Execute the function when a file appears in the **images** container.</span></span> |
    | <span data-ttu-id="7b0ee-134">**Speicherkontoinformationen**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-134">**Storage account information**</span></span> | <span data-ttu-id="7b0ee-135">AZURE_STORAGE_CONNECTION_STRING</span><span class="sxs-lookup"><span data-stu-id="7b0ee-135">AZURE_STORAGE_CONNECTION_STRING</span></span> | <span data-ttu-id="7b0ee-136">Verwenden Sie die Umgebungsvariable, die zuvor mit der Verbindungszeichenfolge erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-136">Use the environment variable previously created with the connection string.</span></span> |

    ![Eingeben von Einstellungen für die neue Funktion](../media/3-new-function.png)

1. <span data-ttu-id="7b0ee-138">Klicken Sie auf **Erstellen**, um die Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-138">Click **Create** to create the function.</span></span>

1. <span data-ttu-id="7b0ee-139">Klicken Sie nach dem Erstellen der Funktion auf **Integrieren**, um die Trigger-, Eingabe- und Ausgabebindungen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-139">When the function is created, click **Integrate** to view its trigger, input, and output bindings.</span></span>

1. <span data-ttu-id="7b0ee-140">Klicken Sie auf **Neue Ausgabe**, um eine neue Ausgabebindung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-140">Click **New output** to create a new output binding.</span></span>

    ![Auswählen von „Neue Ausgabe“ auf der Registerkarte „Integrieren“](../media/3-new-output.jpg)

1. <span data-ttu-id="7b0ee-142">Wählen Sie **Azure Blob Storage** aus, und klicken Sie auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-142">Select **Azure Blob Storage** and click **Select**.</span></span> <span data-ttu-id="7b0ee-143">Unter Umständen müssen Sie nach unten scrollen, damit die Schaltfläche **Auswählen** angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-143">You may have to scroll down to see the **Select** button.</span></span>

    ![Auswählen von „Azure Blob Storage“](../media/3-storage-output.jpg)

1. <span data-ttu-id="7b0ee-145">Geben Sie die folgenden Werte ein:</span><span class="sxs-lookup"><span data-stu-id="7b0ee-145">Enter the following values:</span></span>

    | <span data-ttu-id="7b0ee-146">Einstellung</span><span class="sxs-lookup"><span data-stu-id="7b0ee-146">Setting</span></span>      |  <span data-ttu-id="7b0ee-147">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="7b0ee-147">Suggested value</span></span>   | <span data-ttu-id="7b0ee-148">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7b0ee-148">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="7b0ee-149">**Blobparametername**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-149">**Blob parameter name**</span></span> | <span data-ttu-id="7b0ee-150">thumbnail</span><span class="sxs-lookup"><span data-stu-id="7b0ee-150">thumbnail</span></span> | <span data-ttu-id="7b0ee-151">Für die Funktion wird der Parameter mit diesem Namen verwendet, um die Miniaturansicht zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-151">The function uses the parameter with this name to write the thumbnail.</span></span> |
    | <span data-ttu-id="7b0ee-152">**Funktionsrückgabewert verwenden**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-152">**Use function return value**</span></span> | <span data-ttu-id="7b0ee-153">Nein</span><span class="sxs-lookup"><span data-stu-id="7b0ee-153">No</span></span> |  |
    | <span data-ttu-id="7b0ee-154">**Pfad**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-154">**Path**</span></span> | <span data-ttu-id="7b0ee-155">thumbnails/{Name}</span><span class="sxs-lookup"><span data-stu-id="7b0ee-155">thumbnails/{name}</span></span> | <span data-ttu-id="7b0ee-156">Die Miniaturansichten werden in einen Container mit dem Namen **thumbnails** geschrieben.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-156">The thumbnails are written to a container named **thumbnails**.</span></span> |
    | <span data-ttu-id="7b0ee-157">**Speicherkontoverbindung**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-157">**Storage account connection**</span></span> | <span data-ttu-id="7b0ee-158">AZURE_STORAGE_CONNECTION_STRING</span><span class="sxs-lookup"><span data-stu-id="7b0ee-158">AZURE_STORAGE_CONNECTION_STRING</span></span> | <span data-ttu-id="7b0ee-159">Verwenden Sie die Umgebungsvariable, die zuvor mit der Verbindungszeichenfolge erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-159">Use the environment variable previously created with the connection string.</span></span> |

    ![Eingeben der Einstellungen für die Blobausgabebindung](../media/3-blob-output.png)


1. <span data-ttu-id="7b0ee-161">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-161">**JavaScript**</span></span>

    1. <span data-ttu-id="7b0ee-162">(JavaScript) Klicken Sie oben rechts im Fenster auf **Erweiterter Editor**, um den JSON-Code für die Bindungen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-162">(JavaScript) Click on **Advanced editor** in the top right corner of the window to reveal the JSON that represents the bindings.</span></span>

    1. <span data-ttu-id="7b0ee-163">(JavaScript) Fügen Sie in der Bindung `blobTrigger` eine Eigenschaft mit dem Namen `dataType` und dem Wert `binary` hinzu.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-163">(JavaScript) In the `blobTrigger` binding, add a property named `dataType` with a value of `binary`.</span></span> <span data-ttu-id="7b0ee-164">Hiermit wird die Bindung so konfiguriert, dass der Blobinhalt in Form von binären Daten an die Funktion übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-164">This configures the binding to pass the blob contents to the function as binary data.</span></span>

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

1. <span data-ttu-id="7b0ee-165">Klicken Sie auf **Speichern**, um die neue Bindung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-165">Click **Save** to create the new binding.</span></span>

1. <span data-ttu-id="7b0ee-166">**C#**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-166">**C#**</span></span>

    1. <span data-ttu-id="7b0ee-167">(C#) Wählen Sie im linken Navigationsbereich den Funktionsnamen **ResizeImage** aus, um den Quellcode der Funktion zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-167">(C#) Select the **ResizeImage** function name in the left navigation to open the function's source code.</span></span>

    1. <span data-ttu-id="7b0ee-168">(C#) Für die Funktion ist ein NuGet-Paket mit dem Namen **ImageResizer** erforderlich, um die Miniaturansichten zu generieren.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-168">(C#) The function requires a NuGet package called **ImageResizer** to generate the thumbnails.</span></span> <span data-ttu-id="7b0ee-169">NuGet-Pakete werden über die Datei **project.json** zu C#-Funktionen hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-169">NuGet packages are added to C# functions using a **project.json** file.</span></span> <span data-ttu-id="7b0ee-170">Klicken Sie zum Erstellen der Datei rechts auf **Dateien anzeigen**, um die Dateien anzuzeigen, aus denen die Funktion besteht.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-170">To create the file, click **View Files** on the right to reveal the files that make up the function.</span></span>
    
    1. <span data-ttu-id="7b0ee-171">(C#) Klicken Sie auf **Hinzufügen**, um eine neue Datei mit dem Namen **project.json** hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-171">(C#) Click **Add** to add a new file named **project.json**.</span></span>
    
    1. <span data-ttu-id="7b0ee-172">(C#) Kopieren Sie den Inhalt der Datei [**/csharp/ResizeImage/project.json**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/project.json) in die neu erstellte Datei.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-172">(C#) Copy the contents of the [**/csharp/ResizeImage/project.json**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/project.json) file into the newly created file.</span></span> <span data-ttu-id="7b0ee-173">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-173">Save the file.</span></span> <span data-ttu-id="7b0ee-174">Pakete werden automatisch wiederhergestellt, wenn die Datei aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-174">Packages are automatically restored when the file is updated.</span></span>
    
        ![Datei „project.json“ mit ImageResizer](../media/3-project-json.png)
    
    1. <span data-ttu-id="7b0ee-176">(C#) Wählen Sie unter **Dateien anzeigen** die Datei **run.csx** aus.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-176">(C#) Under **View Files**, select **run.csx**.</span></span> <span data-ttu-id="7b0ee-177">Ersetzen Sie den Inhalt durch den Inhalt von [**/csharp/ResizeImage/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run.csx).</span><span class="sxs-lookup"><span data-stu-id="7b0ee-177">Replace its content with the content in the [**/csharp/ResizeImage/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run.csx) file.</span></span>

1. <span data-ttu-id="7b0ee-178">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7b0ee-178">**JavaScript**</span></span> 

    1. <span data-ttu-id="7b0ee-179">(JavaScript) Für diese Funktion ist das `jimp`-Paket von npm erforderlich, um die Größe des Fotos zu ändern.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-179">(JavaScript) This function requires the `jimp` package from npm to resize the photo.</span></span> <span data-ttu-id="7b0ee-180">Klicken Sie zum Installieren des npm-Pakets im linken Navigationsbereich erst auf den Namen der Funktions-App und dann auf **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-180">To install the npm package, click on the Functions app name on the left navigation and click **Platform features**.</span></span>

    1. <span data-ttu-id="7b0ee-181">(JavaScript) Klicken Sie auf **Konsole**, um ein Konsolenfenster anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-181">(JavaScript) Click **Console** to reveal a console window.</span></span>

    1. <span data-ttu-id="7b0ee-182">(JavaScript) Führen Sie den Befehl `npm install jimp` in der Konsole aus.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-182">(JavaScript) Run the command `npm install jimp` in the console.</span></span> <span data-ttu-id="7b0ee-183">Es kann einige Minuten dauern, bis der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-183">It may take a few minutes to complete the operation.</span></span>

    1. <span data-ttu-id="7b0ee-184">(JavaScript) Klicken Sie im Navigationsbereich auf der linken Seite auf den Funktionsnamen **ResizeImage**, um die Funktion anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-184">(JavaScript) Click on the **ResizeImage** function name in the left navigation to reveal the function.</span></span> <span data-ttu-id="7b0ee-185">Ersetzen Sie den gesamten Inhalt der Datei **index.js** durch den Inhalt der Datei [**/javascript/ResizeImage/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index.js).</span><span class="sxs-lookup"><span data-stu-id="7b0ee-185">Replace all the content in the **index.js** file with the content of the [**/javascript/ResizeImage/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index.js) file.</span></span>

1. <span data-ttu-id="7b0ee-186">Klicken Sie unter dem Codefenster auf **Protokolle**, um den Protokollbereich zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-186">To expand the logs panel, click **Logs** below the code window.</span></span>

1. <span data-ttu-id="7b0ee-187">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-187">Click **Save**.</span></span> <span data-ttu-id="7b0ee-188">Überprüfen Sie den Protokollbereich, um sicherzustellen, dass die Funktion erfolgreich gespeichert wird und keine Fehler aufgetreten sind.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-188">Check the Logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="test-the-serverless-function"></a><span data-ttu-id="7b0ee-189">Testen der serverlosen Funktion</span><span class="sxs-lookup"><span data-stu-id="7b0ee-189">Test the serverless function</span></span>

1. <span data-ttu-id="7b0ee-190">Öffnen Sie die Anwendung in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-190">Open the application in a browser.</span></span> <span data-ttu-id="7b0ee-191">Wählen Sie eine Bilddatei aus, und laden Sie sie hoch.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-191">Select an image file and upload it.</span></span> <span data-ttu-id="7b0ee-192">Der Upload wird abgeschlossen. Da die Möglichkeit zum Anzeigen von Bildern jedoch noch nicht hinzugefügt wurde, wird das hochgeladene Bild von der App nicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-192">The upload completes, but because we haven't added the ability to display images yet, the app doesn't show the uploaded photo.</span></span>

1. <span data-ttu-id="7b0ee-193">Vergewissern Sie sich in Cloud Shell, dass das Bild in den Container **images** hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-193">In Cloud Shell, confirm the image was uploaded to the **images** container.</span></span>

    ```azurecli
    az storage blob list --account-name <storage account name> -c images -o table
    ```

1. <span data-ttu-id="7b0ee-194">Vergewissern Sie sich, dass die Miniaturansicht in einem Container mit dem Namen **thumbnails** erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-194">Confirm the thumbnail was created in a container named **thumbnails**.</span></span>

    ```azurecli
    az storage blob list --account-name <storage account name> -c thumbnails -o table
    ```

1. <span data-ttu-id="7b0ee-195">Rufen Sie die URL für die Miniaturansicht ab.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-195">Get the URL for the thumbnail.</span></span>

    ```azurecli
    az storage blob url --account-name <storage account name> -c thumbnails -n <filename> --output tsv
    ```

    <span data-ttu-id="7b0ee-196">Öffnen Sie die URL in einem Browser, und stellen Sie sicher, dass die Miniaturansicht richtig erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-196">Open the URL in a browser and confirm the thumbnail was properly created.</span></span>

1. <span data-ttu-id="7b0ee-197">Löschen Sie alle Dateien in den Containern **images** und **thumbnails**, bevor Sie mit dem nächsten Tutorial fortfahren.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-197">Before continuing to the next tutorial, delete all files in the **images** and **thumbnails** containers.</span></span>

    ```azurecli
    az storage blob delete-batch -s images --account-name <storage account name>
    ```
    ```azurecli
    az storage blob delete-batch -s thumbnails --account-name <storage account name>
    ```


## <a name="summary"></a><span data-ttu-id="7b0ee-198">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="7b0ee-198">Summary</span></span>

<span data-ttu-id="7b0ee-199">In dieser Einheit haben Sie eine serverlose Funktion erstellt, um eine Miniaturansicht zu erstellen, wenn ein Bild in einen Blobspeichercontainer hochgeladen wird.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-199">In this unit, you created a serverless function to create a thumbnail when an image is uploaded to a Blob storage container.</span></span> <span data-ttu-id="7b0ee-200">Als Nächstes erfahren Sie, wie Sie Azure Cosmos DB zum Speichern und Auflisten von Bildmetadaten verwenden.</span><span class="sxs-lookup"><span data-stu-id="7b0ee-200">Next, you learn how to use Azure Cosmos DB to store and list image metadata.</span></span>