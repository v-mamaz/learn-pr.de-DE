<span data-ttu-id="b3941-101">Die Anwendung, die Sie erstellen, ist eine Fotogalerie.</span><span class="sxs-lookup"><span data-stu-id="b3941-101">The application that you're building is a photo gallery.</span></span> <span data-ttu-id="b3941-102">Clientseitige JavaScript-Code verwendet, um die APIs zum Hochladen und Anzeigen von Bildern aufrufen.</span><span class="sxs-lookup"><span data-stu-id="b3941-102">It uses client-side JavaScript to call APIs to upload and display images.</span></span> <span data-ttu-id="b3941-103">In diesem Modul erstellen Sie eine API über eine serverlose Funktion, die eine zeitlich begrenzte-URL für ein Bild hochladen generiert.</span><span class="sxs-lookup"><span data-stu-id="b3941-103">In this module, you create an API using a serverless function that generates a time-limited URL to upload an image.</span></span> <span data-ttu-id="b3941-104">Die Webanwendung verwendet die generierte URL, ein Abbild hochzuladen, Blob-Speicher mithilfe der [Blob-Speicher-REST-API](https://docs.microsoft.com/rest/api/storageservices/blob-service-rest-api).</span><span class="sxs-lookup"><span data-stu-id="b3941-104">The web application uses the generated URL to upload an image to Blob storage using the [Blob storage REST API](https://docs.microsoft.com/rest/api/storageservices/blob-service-rest-api).</span></span>

## <a name="create-a-blob-storage-container-for-images"></a><span data-ttu-id="b3941-105">Erstellen Sie einen Blob-Speichercontainer für Bilder</span><span class="sxs-lookup"><span data-stu-id="b3941-105">Create a blob storage container for images</span></span>

<span data-ttu-id="b3941-106">Die Anwendung erfordert einen separaten Speicher-Container hochladen und Host-Images.</span><span class="sxs-lookup"><span data-stu-id="b3941-106">The application requires a separate storage container to upload and host images.</span></span>

1. <span data-ttu-id="b3941-107">Stellen Sie sicher, dass Sie immer noch in der Cloud Shell (Bash) angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="b3941-107">Ensure you are still signed in to the Cloud Shell (bash).</span></span> <span data-ttu-id="b3941-108">Wählen Sie andernfalls **EINGABETASTE fokusmodus** um eine Cloud Shell-Fenster zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="b3941-108">If not, select **Enter focus mode** to open a Cloud Shell window.</span></span>

1.  <span data-ttu-id="b3941-109">Erstellen Sie einen neuen Container namens **Images** in Ihrem Storage-Konto mit öffentlichem Zugriff auf alle Blobs.</span><span class="sxs-lookup"><span data-stu-id="b3941-109">Create a new container named **images** in your storage account with public access to all blobs.</span></span>

    ```azurecli
    az storage container create -n images --account-name <storage account name> --public-access blob
    ```

## <a name="create-an-azure-function-app"></a><span data-ttu-id="b3941-110">Erstellen einer Azure Function-App</span><span class="sxs-lookup"><span data-stu-id="b3941-110">Create an Azure Function app</span></span>

<span data-ttu-id="b3941-111">Azure Functions ist ein Dienst zum Ausführen von serverloser Funktionen.</span><span class="sxs-lookup"><span data-stu-id="b3941-111">Azure Functions is a service for running serverless functions.</span></span> <span data-ttu-id="b3941-112">Eine serverlose Funktion kann ausgelöst werden, (bezeichnet) von Ereignissen wie z. B. eine HTTP-Anforderung, oder wenn ein Blob in einem Speichercontainer erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="b3941-112">A serverless function can be triggered (called) by events such as an HTTP request or when a blob is created in a storage container.</span></span>

<span data-ttu-id="b3941-113">Eine Azure-Funktions-app ist ein Container für eine oder mehrere serverlosen Funktionen.</span><span class="sxs-lookup"><span data-stu-id="b3941-113">An Azure Function app is a container for one or more serverless functions.</span></span>

1. <span data-ttu-id="b3941-114">Erstellen Sie eine neue Azure-Funktions-app mit einem eindeutigen Namen in der Ressourcengruppe, die Sie erstellt haben zuvor mit dem Namen **ersten serverlosen app**.</span><span class="sxs-lookup"><span data-stu-id="b3941-114">Create a new Azure Function app with a unique name in the resource group you created earlier named **first-serverless-app**.</span></span> <span data-ttu-id="b3941-115">Funktionen-apps erfordern ein Speicherkonto. In diesem Tutorial verwenden Sie das vorhandene Speicherkonto an.</span><span class="sxs-lookup"><span data-stu-id="b3941-115">Function apps require a Storage account; in this tutorial, you use the existing storage account.</span></span>

    ```azurecli
    az functionapp create -n <function app name> -g first-serverless-app -s <storage account name> -c westcentralus
    ```


## <a name="create-an-http-triggered-serverless-function"></a><span data-ttu-id="b3941-116">Erstellen einer serverlosen per HTTP ausgelöste-Funktion</span><span class="sxs-lookup"><span data-stu-id="b3941-116">Create an HTTP-triggered serverless function</span></span>

<span data-ttu-id="b3941-117">Die Fotogalerie-Webanwendung führt eine HTTP-Anforderung für serverlose Funktion, um eine zeitlich begrenzte URL sicher ein Bild in blobspeicher hochladen zu generieren.</span><span class="sxs-lookup"><span data-stu-id="b3941-117">The photo gallery web application makes an HTTP request to serverless function to generate a time-limited URL to securely upload an image to Blob storage.</span></span> <span data-ttu-id="b3941-118">Die Funktion wird durch eine HTTP-Anforderung ausgelöst und verwendet Azure Storage-SDK erstellt und die sichere URL zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="b3941-118">The function is triggered by an HTTP request and uses the Azure Storage SDK to generate and return the secure URL.</span></span>

1. <span data-ttu-id="b3941-119">Nachdem die Funktionen-app erstellt wurde, suchen sie im Azure-Portal mithilfe des Suchfelds, und klicken Sie auf, um ihn zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="b3941-119">After the Function app is created, search for it in the Azure Portal using the Search box and click to open it.</span></span>

    ![Öffnen Sie die Funktions-app](../images/2-search-function-app.png)

1. <span data-ttu-id="b3941-121">Klicken Sie im linken Navigationsbereich das Funktion app-Fenster, zeigen Sie auf **Funktionen** , und klicken Sie auf **+** zum Erstellen einer neuen serverlosen Funktion.</span><span class="sxs-lookup"><span data-stu-id="b3941-121">In the function app window's left hand navigation, hover over **Functions** and click **+** to start creating a new serverless function.</span></span>

    ![Erstellen Sie eine neue Funktion](../images/2-new-function.png)

1. <span data-ttu-id="b3941-123">Klicken Sie auf **benutzerdefinierte Funktion** um eine Liste von Funktionsvorlagen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b3941-123">Click **Custom function** to see a list of function templates.</span></span>

1. <span data-ttu-id="b3941-124">Suchen der **"httptrigger"** Vorlage, und klicken Sie auf die Sprache um (C#- oder JavaScript) zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="b3941-124">Find the **HttpTrigger** template and click the language to use (C# or JavaScript).</span></span>

1. <span data-ttu-id="b3941-125">Verwenden Sie diese Werte zum Erstellen einer Funktion, die eine Blob-Upload-URL generiert.</span><span class="sxs-lookup"><span data-stu-id="b3941-125">Use these values to create a function that generates a blob upload URL.</span></span>

    | <span data-ttu-id="b3941-126">Einstellung</span><span class="sxs-lookup"><span data-stu-id="b3941-126">Setting</span></span>      |  <span data-ttu-id="b3941-127">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="b3941-127">Suggested value</span></span>   | <span data-ttu-id="b3941-128">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b3941-128">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="b3941-129">**Sprache**</span><span class="sxs-lookup"><span data-stu-id="b3941-129">**Language**</span></span> | <span data-ttu-id="b3941-130">C#- oder JavaScript</span><span class="sxs-lookup"><span data-stu-id="b3941-130">C# or JavaScript</span></span> | <span data-ttu-id="b3941-131">Wählen Sie die Sprache, die Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="b3941-131">Select the language you want to use.</span></span> |
    | <span data-ttu-id="b3941-132">**Name Ihrer Funktion**</span><span class="sxs-lookup"><span data-stu-id="b3941-132">**Name your function**</span></span> | <span data-ttu-id="b3941-133">GetUploadUrl</span><span class="sxs-lookup"><span data-stu-id="b3941-133">GetUploadUrl</span></span> | <span data-ttu-id="b3941-134">Geben Sie diesen Namen genau wie angezeigt, damit die Anwendung die Funktion ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="b3941-134">Type this name exactly as shown so the application can discover the function.</span></span> |
    | <span data-ttu-id="b3941-135">**Autorisierungsstufe**</span><span class="sxs-lookup"><span data-stu-id="b3941-135">**Authorization level**</span></span> | <span data-ttu-id="b3941-136">Anonym</span><span class="sxs-lookup"><span data-stu-id="b3941-136">Anonymous</span></span> | <span data-ttu-id="b3941-137">Ermöglichen Sie die Funktion, die öffentlich zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="b3941-137">Allow the function to be accessed publicly.</span></span> |

    ![Geben Sie Einstellungen für eine neue per HTTP ausgelöste Funktion](../images/2-new-function-httptrigger.png)

1. <span data-ttu-id="b3941-139">Klicken Sie auf **erstellen** zum Erstellen der Funktion.</span><span class="sxs-lookup"><span data-stu-id="b3941-139">Click **Create** to create the function.</span></span>

1. <span data-ttu-id="b3941-140">**C#**</span><span class="sxs-lookup"><span data-stu-id="b3941-140">**C#**</span></span> 

    1. <span data-ttu-id="b3941-141">Wenn Quellcode der Funktion angezeigt wird, ersetzen Sie sämtlichen **"Run.csx"** mit dem Inhalt des [ **csharp/GetUploadUrl/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetUploadUrl/run.csx).</span><span class="sxs-lookup"><span data-stu-id="b3941-141">When the function's source code appears, replace all of **run.csx** with the content of [**csharp/GetUploadUrl/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetUploadUrl/run.csx).</span></span>

1. <span data-ttu-id="b3941-142">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="b3941-142">**JavaScript**</span></span> 

    1. <span data-ttu-id="b3941-143">(JavaScript) Diese Funktion erfordert die `azure-storage` Paket von Npm zum Generieren des SAS-Signaturtokens (SAS) erforderlich, um die sichere URL zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b3941-143">(JavaScript) This function requires the `azure-storage` package from npm to generate the shared access signature (SAS) token required to build the secure URL.</span></span> <span data-ttu-id="b3941-144">Klicken Sie zum Installieren des Npm-Pakets klicken Sie auf der Funktions-App-Namen im linken Navigationsbereich, und klicken Sie auf **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="b3941-144">To install the npm package, click on the Function App's name on the left navigation and click **Platform features**.</span></span>

    1. <span data-ttu-id="b3941-145">(JavaScript) Klicken Sie auf **Konsole** um ein Konsolenfenster anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="b3941-145">(JavaScript) Click **Console** to reveal a console window.</span></span>

        ![Ein Konsolenfenster geöffnet](../images/2-open-console.jpg)

    1. <span data-ttu-id="b3941-147">(JavaScript) Stellen Sie sicher, das aktuelle Verzeichnis ist **d:\home\site\wwwroot** mithilfe des Befehls `cd d:\home\site\wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="b3941-147">(JavaScript) Ensure the current directory is **d:\home\site\wwwroot** by running the command `cd d:\home\site\wwwroot`.</span></span>

    1. <span data-ttu-id="b3941-148">(JavaScript) Führen Sie den Befehl `npm init -y` zum Erstellen eines leeren **"Package.JSON"** Datei.</span><span class="sxs-lookup"><span data-stu-id="b3941-148">(JavaScript) Run the command `npm init -y` to create an empty **package.json** file.</span></span>

    1. <span data-ttu-id="b3941-149">(JavaScript) Führen Sie den Befehl `npm install --save azure-storage` in der Konsole zum Installieren des Pakets ein, und speichern Sie ihn in **"Package.JSON"**.</span><span class="sxs-lookup"><span data-stu-id="b3941-149">(JavaScript) Run the command `npm install --save azure-storage` in the console to install the package and save it in **package.json**.</span></span> <span data-ttu-id="b3941-150">Es dauert etwas, um den Vorgang abzuschließen.</span><span class="sxs-lookup"><span data-stu-id="b3941-150">It may take a minute or two to complete the operation.</span></span>

    1. <span data-ttu-id="b3941-151">(JavaScript) Klicken Sie auf den Namen der Funktion (**GetUploadUrl**) im linken Navigationsbereich auf die Funktion anzuzeigen, ersetzen Sie sämtlichen **"Index.js"** mit dem Inhalt des [ **Javascript/GetUploadUrl / "Index.js"**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetUploadUrl/index.js).</span><span class="sxs-lookup"><span data-stu-id="b3941-151">(JavaScript) Click on the function name (**GetUploadUrl**) in the left navigation to reveal the function, replace all of **index.js** with the content of [**javascript/GetUploadUrl/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetUploadUrl/index.js).</span></span>
    
        ![index.js after update](../images/2-paste-js.jpg)

1. <span data-ttu-id="b3941-153">Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="b3941-153">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="b3941-154">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="b3941-154">Click **Save**.</span></span> <span data-ttu-id="b3941-155">Überprüfen Sie, dass das Bedienfeld "Protokolle", um sicherzustellen, dass die Funktion erfolgreich kompiliert wurde.</span><span class="sxs-lookup"><span data-stu-id="b3941-155">Check the logs panel to ensure the function is successfully compiled.</span></span>

<span data-ttu-id="b3941-156">Generiert die Funktion, was eine URL shared Access Signature (SAS) aufgerufen wird, die zum Hochladen einer Datei in Blob Storage verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b3941-156">The function generates what is called a shared access signature (SAS) URL that is used to upload a file to Blob storage.</span></span> <span data-ttu-id="b3941-157">Die SAS-URL ist für einen kurzen Zeitraum gültig und lässt nur eine einzelne Datei hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="b3941-157">The SAS URL is valid for a short period of time and only allows a single file to be uploaded.</span></span> <span data-ttu-id="b3941-158">Wenden Sie sich an den Blob-speicherdokumentation Informationen auf [Verwenden von shared Access Signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="b3941-158">Consult the Blob storage documentation for more information on [using shared access signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1).</span></span>


## <a name="add-an-environment-variable-for-the-storage-connection-string"></a><span data-ttu-id="b3941-159">Fügen Sie eine Umgebungsvariable für die Speicher-Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="b3941-159">Add an environment variable for the storage connection string</span></span>

<span data-ttu-id="b3941-160">Die zuvor erstellte Funktion erfordert eine Verbindungszeichenfolge für das Speicherkonto, damit sie die SAS-URL generieren kann.</span><span class="sxs-lookup"><span data-stu-id="b3941-160">The function you just created requires a connection string for the Storage account so that it can generate the SAS URL.</span></span> <span data-ttu-id="b3941-161">Anstelle eines hartcodierten die Verbindungszeichenfolge in den Textkörper der Funktion kann sie als anwendungseinstellung gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="b3941-161">Instead of hardcoding the connection string in the function's body, it can be stored as an application setting.</span></span> <span data-ttu-id="b3941-162">Anwendungseinstellungen werden als Umgebungsvariablen, die von allen Funktionen in der Funktions-app zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="b3941-162">Application settings are accessible as environment variables by all functions in the Function app.</span></span>

1. <span data-ttu-id="b3941-163">Abfragen von in der Cloud Shell, die Verbindungszeichenfolge für Speicherkonto, und speichern Sie ihn auf eine Bash-Variable, die mit dem Namen **STORAGE_CONNECTION_STRING**.</span><span class="sxs-lookup"><span data-stu-id="b3941-163">In the Cloud Shell, query the Storage account connection string and save it to a bash variable named **STORAGE_CONNECTION_STRING**.</span></span>

    ```azurecli
    export STORAGE_CONNECTION_STRING=$(az storage account show-connection-string -n <storage account name> -g first-serverless-app --query "connectionString" --output tsv)
    ```

    <span data-ttu-id="b3941-164">Vergewissern Sie sich, dass die Variable wurde erfolgreich festgelegt wurde.</span><span class="sxs-lookup"><span data-stu-id="b3941-164">Confirm the variable is set successfully.</span></span>

    ```azurecli
    echo $STORAGE_CONNECTION_STRING
    ```

1. <span data-ttu-id="b3941-165">Erstellen Sie eine neue anwendungseinstellung mit dem Namen **AZURE_STORAGE_CONNECTION_STRING** mit dem Wert, der im vorherigen Schritt gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="b3941-165">Create a new application setting named **AZURE_STORAGE_CONNECTION_STRING** using the value saved from the previous step.</span></span>

    ```azurecli
    az functionapp config appsettings set -n <function app name> -g first-serverless-app --settings AZURE_STORAGE_CONNECTION_STRING=$STORAGE_CONNECTION_STRING -o table
    ```

    <span data-ttu-id="b3941-166">Vergewissern Sie sich, dass die Ausgabe des Befehls die neue anwendungseinstellung mit dem richtigen Wert enthält.</span><span class="sxs-lookup"><span data-stu-id="b3941-166">Confirm that the command's output contains the new application setting with the correct value.</span></span>


## <a name="test-the-serverless-function"></a><span data-ttu-id="b3941-167">Testen Sie die serverlose Funktion</span><span class="sxs-lookup"><span data-stu-id="b3941-167">Test the serverless function</span></span>

<span data-ttu-id="b3941-168">Zusätzlich zum Erstellen und Bearbeiten von Funktionen, bietet das Azure-Portal auch ein integriertes Tool zum Testen von Funktionen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b3941-168">In addition to creating and editing functions, the Azure portal also provides an built-in tool for testing functions.</span></span>

1. <span data-ttu-id="b3941-169">Um die HTTP-serverlosen Funktion zu testen, klicken Sie auf die **testen** Registerkarte auf der rechten Seite des Code-Fenster, um den Testbereich zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="b3941-169">To test the HTTP serverless function, click on the **Test** tab on the right of the code window to expand the test panel.</span></span>

1. <span data-ttu-id="b3941-170">Ändern der **Http-Methode** zu **erhalten**.</span><span class="sxs-lookup"><span data-stu-id="b3941-170">Change the **Http method** to **GET**.</span></span>

1. <span data-ttu-id="b3941-171">Klicken Sie unter **Abfrage**, klicken Sie auf \*Parameter hinzufügen\*\*, und fügen Sie den folgenden Parameter hinzu:</span><span class="sxs-lookup"><span data-stu-id="b3941-171">Under **Query**, click *Add parameter*\* and add the following parameter:</span></span>

    | <span data-ttu-id="b3941-172">name</span><span class="sxs-lookup"><span data-stu-id="b3941-172">name</span></span>      |  <span data-ttu-id="b3941-173">value</span><span class="sxs-lookup"><span data-stu-id="b3941-173">value</span></span>   | 
    | --- | --- |
    | <span data-ttu-id="b3941-174">filename</span><span class="sxs-lookup"><span data-stu-id="b3941-174">filename</span></span> | <span data-ttu-id="b3941-175">image1.jpg</span><span class="sxs-lookup"><span data-stu-id="b3941-175">image1.jpg</span></span> |

1. <span data-ttu-id="b3941-176">Klicken Sie auf **ausführen** im Testbereich eine HTTP-Anforderung an die Funktion zu senden.</span><span class="sxs-lookup"><span data-stu-id="b3941-176">Click **Run** in the test panel to send an HTTP request to the function.</span></span>

1. <span data-ttu-id="b3941-177">Die Funktion gibt eine Upload-URL in der Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="b3941-177">The function returns an upload URL in the output.</span></span> <span data-ttu-id="b3941-178">Die Ausführung der Funktion wird im Bedienfeld "Protokolle" angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b3941-178">The function execution appears in the logs panel.</span></span>

    ![Protokolle, die mit der Funktion wurde erfolgreich ausgeführt.](../images/2-test-function.png)


## <a name="configure-cors-in-the-function-app"></a><span data-ttu-id="b3941-180">Konfigurieren von CORS in der Funktions-app</span><span class="sxs-lookup"><span data-stu-id="b3941-180">Configure CORS in the function app</span></span>

<span data-ttu-id="b3941-181">Da es sich bei der app-Front-End im Blob-Speicher gehostet wird, hat er einen anderen Domänennamen als Azure-Funktions-app.</span><span class="sxs-lookup"><span data-stu-id="b3941-181">Because the app's frontend is hosted in Blob storage, it has a different domain name than the Azure Function app.</span></span> <span data-ttu-id="b3941-182">Für die clientseitige JavaScript-Code auf die Funktion erfolgreich aufzurufen, die Sie gerade erstellt haben, muss die Funktions-app für Cross-Origin Resource sharing (CORS) konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="b3941-182">For the client-side JavaScript to successfully call the function you just created, the function app needs to be configured for cross-origin resource sharing (CORS).</span></span>

1. <span data-ttu-id="b3941-183">Klicken Sie auf den Namen der Funktionen-app, in der linken Navigationsleiste auf der app-Fenster der Funktion.</span><span class="sxs-lookup"><span data-stu-id="b3941-183">In the left navigation bar of the function app window, click on the name of your function app.</span></span>

1. <span data-ttu-id="b3941-184">Klicken Sie auf **Plattformfeatures** zum Anzeigen einer Liste erweiterter Funktionen.</span><span class="sxs-lookup"><span data-stu-id="b3941-184">Click on **Platform features** to view a list of advanced features.</span></span>

1. <span data-ttu-id="b3941-185">Klicken Sie unter **API**, klicken Sie auf **CORS**.</span><span class="sxs-lookup"><span data-stu-id="b3941-185">Under **API**, click **CORS**.</span></span>

    ![Aktivieren von CORS](../images/2-open-cors.jpg)

1. <span data-ttu-id="b3941-187">Hinzufügen ein Ursprungs zulassen für die Anwendungs-URL aus dem vorherigen Modul, das Auslassen der nachfolgende **/** (z. B.: `https://firstserverlessweb.z4.web.core.windows.net`).</span><span class="sxs-lookup"><span data-stu-id="b3941-187">Add an allow origin for the application URL from the previous module, omitting the trailing **/** (for example: `https://firstserverlessweb.z4.web.core.windows.net`).</span></span>

    ![Mit serverlosen CORS-Einstellungen hinzugefügt, Web-app-URL](../images/2-add-cors.png)

1. <span data-ttu-id="b3941-189">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="b3941-189">Click **Save**.</span></span>

1. <span data-ttu-id="b3941-190">C#</span><span class="sxs-lookup"><span data-stu-id="b3941-190">C#</span></span>

   1. <span data-ttu-id="b3941-191">(C#) Navigieren Sie zurück zu den `GetUploadUrl` funktionieren, und wählen Sie dann die **integrieren** Registerkarte.</span><span class="sxs-lookup"><span data-stu-id="b3941-191">(C#) Navigate back to the `GetUploadUrl` function, and then select the **Integrate** tab.</span></span>

   1. <span data-ttu-id="b3941-192">(C#) Wählen Sie die ausgewählte HTTP-Methoden, **Optionen**.</span><span class="sxs-lookup"><span data-stu-id="b3941-192">(C#) Under Selected HTTP methods, select **OPTIONS**.</span></span>

      <span data-ttu-id="b3941-193">**ERSTE**, **POST**, und **Optionen** alle ausgewählt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="b3941-193">**GET**, **POST**, and **OPTIONS** should all be selected.</span></span> <span data-ttu-id="b3941-194">CORS wird verwendet, die OPTIONS-Methode, die nicht für c#-Funktionen standardmäßig ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="b3941-194">CORS uses the OPTIONS method, which is not selected by default for C# functions.</span></span>  

   1. <span data-ttu-id="b3941-195">(C#) Klicken Sie auf **speichern**.</span><span class="sxs-lookup"><span data-stu-id="b3941-195">(C#) Click **Save**.</span></span>

1. <span data-ttu-id="b3941-196">Im Portal, navigieren Sie zur Funktions-app, wählen die **Übersicht über die** Registerkarte, und klicken Sie dann auf **Neustart** um sicherzustellen, dass die Änderungen für CORS wirksam werden.</span><span class="sxs-lookup"><span data-stu-id="b3941-196">Still in the portal, navigate to the function app, select the **Overview** tab, and then click **Restart** to make sure that the changes for CORS take effect.</span></span>

## <a name="configure-cors-in-the-storage-account"></a><span data-ttu-id="b3941-197">Konfigurieren von CORS im Storage-Konto</span><span class="sxs-lookup"><span data-stu-id="b3941-197">Configure CORS in the Storage account</span></span>

<span data-ttu-id="b3941-198">Da die app auch die clientseitige JavaScript-Aufrufe in Blob Storage zum Hochladen von Dateien ist, müssen Sie auch das Speicherkonto für CORS konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="b3941-198">Because the app also makes client-side JavaScript calls to Blob Storage to upload files, you also have to configure the Storage account for CORS.</span></span>

1. <span data-ttu-id="b3941-199">Führen Sie den folgenden Befehl aus, um alle Ursprünge zum Hochladen von Dateien in das Speicherkonto zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="b3941-199">Run the following command to allow all origins to upload files to the Storage account.</span></span>

    ```azurecli
    az storage cors add --methods OPTIONS PUT --origins '*' --exposed-headers '*' --allowed-headers '*' --services b --account-name <storage account name>
    ```


## <a name="modify-the-web-app-to-upload-images"></a><span data-ttu-id="b3941-200">Ändern Sie die Web-app zum Hochladen von Bildern</span><span class="sxs-lookup"><span data-stu-id="b3941-200">Modify the web app to upload images</span></span>

<span data-ttu-id="b3941-201">Die Web-app ruft Einstellungen ab, aus einer Datei namens **settings.js**.</span><span class="sxs-lookup"><span data-stu-id="b3941-201">The web app retrieves settings from a file named **settings.js**.</span></span> <span data-ttu-id="b3941-202">In den folgenden Schritten wird Sie die Datei mit der Cloud Shell zu erstellen und anschließend festlegen `window.apiBaseUrl` an die URL der Funktions-app und `window.blobBaseUrl` an die URL des Azure Blob Storage-Endpunkts.</span><span class="sxs-lookup"><span data-stu-id="b3941-202">In the following steps, you create the file using Cloud Shell, then set `window.apiBaseUrl` to the URL of the Function app and `window.blobBaseUrl` to the URL of the Azure Blob Storage endpoint.</span></span>

1. <span data-ttu-id="b3941-203">Stellen Sie sicher, dass das aktuelle Verzeichnis ist, in der Cloud Shell die **Www/Dist** Ordner.</span><span class="sxs-lookup"><span data-stu-id="b3941-203">In the Cloud Shell, ensure that the current directory is the **www/dist** folder.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. <span data-ttu-id="b3941-204">Abfragen der Funktions-app-URL ein, und speichern Sie sie in einer Bash-Variablen, die mit dem Namen **FUNCTION_APP_URL**.</span><span class="sxs-lookup"><span data-stu-id="b3941-204">Query the function app's URL and store it in a bash variable named **FUNCTION_APP_URL**.</span></span>

    ```azurecli
    export FUNCTION_APP_URL="https://"$(az functionapp show -n <function app name> -g first-serverless-app --query "defaultHostName" --output tsv)
    ```

    <span data-ttu-id="b3941-205">Vergewissern Sie sich, dass die Variable korrekt festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="b3941-205">Confirm the variable is correctly set.</span></span>

    ```azurecli
    echo $FUNCTION_APP_URL
    ```

1. <span data-ttu-id="b3941-206">Um die Basis-URI der API-Aufrufe zu Ihrer Funktions-app festzulegen, erstellen Sie **settings.js** und fügen Sie die Funktions-app-URL wie folgt hinzu.</span><span class="sxs-lookup"><span data-stu-id="b3941-206">To set the base URI of API calls to your function app, create **settings.js** and add the function app URL like the following.</span></span>

    `window.apiBaseUrl = 'https://fnapp@lab.GlobalLabInstanceId.azurewebsites.net'`

    <span data-ttu-id="b3941-207">Sie können die Änderung vorgenommen, durch den folgenden Befehl ausführen oder mit einem Befehlszeilen-Editor, z. B. VIM.</span><span class="sxs-lookup"><span data-stu-id="b3941-207">You can make the change by running the following command or by using a command-line editor like VIM.</span></span>

    ```azurecli
    echo "window.apiBaseUrl = '$FUNCTION_APP_URL'" > settings.js
    ```

    <span data-ttu-id="b3941-208">Vergewissern Sie sich, dass die Datei erfolgreich geschrieben wurde.</span><span class="sxs-lookup"><span data-stu-id="b3941-208">Confirm the file was successfully written.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="b3941-209">Die base-BLOB-Speicher-URL Abfragen und speichern Sie sie in einer Bash-Variablen, die mit dem Namen **BLOB_BASE_URL**.</span><span class="sxs-lookup"><span data-stu-id="b3941-209">Query the Blob Storage base URL and store it in a bash variable named **BLOB_BASE_URL**.</span></span>

    ```azurecli
    export BLOB_BASE_URL=$(az storage account show -n <storage account name> -g first-serverless-app --query primaryEndpoints.blob -o tsv | sed 's/\/$//')
    ```

    <span data-ttu-id="b3941-210">Vergewissern Sie sich, dass die Variable korrekt festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="b3941-210">Confirm the variable is correctly set.</span></span>

    ```azurecli
    echo $BLOB_BASE_URL
    ```

1. <span data-ttu-id="b3941-211">Um die Basis-URI der API-Aufrufe zu Ihrer Funktions-app festzulegen, fügen Sie die Speicher-URL wie die folgende Codezeile, **settings.js**.</span><span class="sxs-lookup"><span data-stu-id="b3941-211">To set the base URI of API calls to your function app, append the storage URL like the following line of code to **settings.js**.</span></span>

    `window.blobBaseUrl = 'https://mystorage.blob.core.windows.net'`

    <span data-ttu-id="b3941-212">Sie können die Änderung vorgenommen, durch den folgenden Befehl ausführen oder mit einem Befehlszeilen-Editor, z. B. VIM.</span><span class="sxs-lookup"><span data-stu-id="b3941-212">You can make the change by running the following command or by using a command-line editor like VIM.</span></span>

    ```azurecli
    echo "window.blobBaseUrl = '$BLOB_BASE_URL'" >> settings.js
    ```

    <span data-ttu-id="b3941-213">Überprüfen Sie die Datei wurde geschrieben und enthält nun 2 Zeilen.</span><span class="sxs-lookup"><span data-stu-id="b3941-213">Confirm the file was successfully written and it now contains 2 lines.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="b3941-214">Laden Sie die Datei in Blob Storage hoch.</span><span class="sxs-lookup"><span data-stu-id="b3941-214">Upload the file to Blob storage.</span></span>

    ```azurecli
    az storage blob upload -c \$web --account-name <storage account name> -f settings.js -n settings.js
    ```


## <a name="test-the-web-application"></a><span data-ttu-id="b3941-215">Testen Sie die Webanwendung</span><span class="sxs-lookup"><span data-stu-id="b3941-215">Test the web application</span></span>

<span data-ttu-id="b3941-216">An diesem Punkt werden die im Katalog enthaltene Anwendung ist in der Lage, ein Abbild in Blob Storage hochzuladen, jedoch nicht Images noch angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b3941-216">At this point, the gallery application is able to upload an image to Blob storage, but it can't display images yet.</span></span> <span data-ttu-id="b3941-217">Es wird versucht, Sie rufen eine `GetImages` -Funktion, die noch nicht vorhanden ist, da Sie in einem späteren Modul erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="b3941-217">It will try to call a `GetImages` function that doesn't exist yet because you create it in a later module.</span></span> <span data-ttu-id="b3941-218">Dieser Aufruf schlägt fehl, und die Webseite wird angezeigt, auf "Analysieren..." hängen bleiben, aber das ausgewählte Image wurde erfolgreich hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="b3941-218">That call will fail, and the web page will appear to be stuck on "Analyzing...", but the image you select will be successfully uploaded.</span></span>

<span data-ttu-id="b3941-219">Sie können überprüfen, ob ein Bild wurde erfolgreich hochgeladen, durch den Inhalt der überprüfen die **Images** Container im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="b3941-219">You can verify an image is successfully uploaded by checking the contents of the **images** container in the Azure portal.</span></span>

1. <span data-ttu-id="b3941-220">Navigieren Sie in einem Browserfenster zu der Anwendung.</span><span class="sxs-lookup"><span data-stu-id="b3941-220">In a browser window, browse to the application.</span></span> <span data-ttu-id="b3941-221">Wählen Sie eine Bilddatei, und Laden Sie es hoch.</span><span class="sxs-lookup"><span data-stu-id="b3941-221">Select an image file and upload it.</span></span> <span data-ttu-id="b3941-222">Der Upload abgeschlossen ist, aber da wir die Möglichkeit zum Anzeigen von Bildern noch hinzugefügt haben, nicht die app das hochgeladene Foto angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b3941-222">The upload completes, but because we haven't added the ability to display images yet, the app doesn't show the uploaded photo.</span></span> <span data-ttu-id="b3941-223">(Die Webseite angezeigt wird, klicken Sie auf "Bild exportieren… analysieren;" hängen bleiben Sie soll, die später behoben werden.)</span><span class="sxs-lookup"><span data-stu-id="b3941-223">(The web page appears to be stuck on "Analyzing image..."; you'll fix that later.)</span></span>

1. <span data-ttu-id="b3941-224">Vergewissern Sie sich in der Cloud Shell das Image hochgeladen wurde, um die **Images** Container.</span><span class="sxs-lookup"><span data-stu-id="b3941-224">In the Cloud Shell, confirm the image was uploaded to the **images** container.</span></span>

    ```azurecli
    az storage blob list --account-name <storage account name> -c images -o table
    ```

1. <span data-ttu-id="b3941-225">Bevor Sie mit dem nächsten Tutorial fortfahren, löschen Sie alle Dateien in die **Images** Container.</span><span class="sxs-lookup"><span data-stu-id="b3941-225">Before moving on to the next tutorial, delete all files in the **images** container.</span></span>

    ```azurecli
    az storage blob delete-batch -s images --account-name <storage account name>
    ```


## <a name="summary"></a><span data-ttu-id="b3941-226">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="b3941-226">Summary</span></span>

<span data-ttu-id="b3941-227">In dieser Einheit Sie haben eine Azure Function-app erstellt und haben gelernt, wie eine serverlose Funktion zu verwenden, um eine Webanwendung zum Hochladen von Bildern in Blob Storage zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="b3941-227">In this unit, you created an Azure Function app and learned how to use a serverless function to allow a web application to upload images to Blob storage.</span></span> <span data-ttu-id="b3941-228">Als Nächstes erfahren Sie, wie zum Erstellen von Miniaturansichten für die hochgeladenen Bilder mit einer serverlosen BLOBs ausgelösten-Funktion.</span><span class="sxs-lookup"><span data-stu-id="b3941-228">Next, you learn how to create thumbnails for the uploaded images using a Blob triggered serverless function.</span></span>