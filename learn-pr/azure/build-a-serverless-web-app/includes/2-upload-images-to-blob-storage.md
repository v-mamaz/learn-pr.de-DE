<span data-ttu-id="0f544-101">Bei der von Ihnen erstellten Anwendung handelt es sich um eine Fotogalerie.</span><span class="sxs-lookup"><span data-stu-id="0f544-101">The application you're building is a photo gallery.</span></span> <span data-ttu-id="0f544-102">Es wird clientseitiger JavaScript-Code verwendet, um APIs zum Hochladen und Anzeigen von Bildern aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="0f544-102">It uses client-side JavaScript to call APIs to upload and display images.</span></span> <span data-ttu-id="0f544-103">In dieser Einheit erstellen Sie eine API, indem Sie eine serverlose Funktion verwenden, mit der eine URL mit zeitlicher Beschränkung zum Hochladen eines Bilds generiert wird.</span><span class="sxs-lookup"><span data-stu-id="0f544-103">In this unit, you will create an API using a serverless function that generates a time-limited URL to upload an image.</span></span> <span data-ttu-id="0f544-104">Die Webanwendung nutzt diese URL zum Hochladen eines Bilds in Blob Storage mit der [Blob Storage-REST-API](https://docs.microsoft.com/rest/api/storageservices/blob-service-rest-api).</span><span class="sxs-lookup"><span data-stu-id="0f544-104">The web application uses this URL to upload an image to Blob storage using the [Blob storage REST API](https://docs.microsoft.com/rest/api/storageservices/blob-service-rest-api).</span></span>

## <a name="create-a-blob-storage-container-for-images"></a><span data-ttu-id="0f544-105">Erstellen eines Blob Storage-Containers für Bilder</span><span class="sxs-lookup"><span data-stu-id="0f544-105">Create a Blob storage container for images</span></span>

<span data-ttu-id="0f544-106">Für die Anwendung ist ein separater Speichercontainer erforderlich, um Bilder hochladen und hosten zu können.</span><span class="sxs-lookup"><span data-stu-id="0f544-106">The application requires a separate storage container to upload and host images.</span></span>

1. <span data-ttu-id="0f544-107">Stellen Sie sicher, dass Sie noch bei der Azure Cloud Shell (Bash) angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="0f544-107">Ensure that you're still signed in to Azure Cloud Shell (Bash).</span></span> <span data-ttu-id="0f544-108">Wählen Sie andernfalls die Option **Enter focus mode** (Fokusmodus aktivieren) aus, um ein Cloud Shell-Fenster zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="0f544-108">If not, select **Enter focus mode** to open a Cloud Shell window.</span></span>

1.  <span data-ttu-id="0f544-109">Erstellen Sie unter Ihrem Speicherkonto einen neuen Container mit dem Namen **images**, der über öffentlichen Zugriff auf alle Blobs verfügt.</span><span class="sxs-lookup"><span data-stu-id="0f544-109">Create a new container in your Storage account named **images** in your Storage account with public access to all blobs.</span></span>

    ```azurecli
    az storage container create -n images --account-name <storage account name> --public-access blob
    ```

## <a name="create-an-azure-functions-app"></a><span data-ttu-id="0f544-110">Erstellen einer Azure Functions-App</span><span class="sxs-lookup"><span data-stu-id="0f544-110">Create an Azure Functions app</span></span>

<span data-ttu-id="0f544-111">Azure Functions ist ein Dienst zum Ausführen serverloser Funktionen.</span><span class="sxs-lookup"><span data-stu-id="0f544-111">Azure Functions is a service for running serverless functions.</span></span> <span data-ttu-id="0f544-112">Eine serverlose Funktion kann von Ereignissen, z.B. einer HTTP-Anforderung, oder bei Erstellung eines Blobs in einem Speichercontainer ausgelöst (aufgerufen) werden.</span><span class="sxs-lookup"><span data-stu-id="0f544-112">A serverless function can be triggered (called) by events, such as an HTTP request, or when a blob is created in a storage container.</span></span>

<span data-ttu-id="0f544-113">Eine Azure Functions-App ist ein Container für mindestens eine serverlose Funktion.</span><span class="sxs-lookup"><span data-stu-id="0f544-113">An Azure Functions app is a container for one or more serverless functions.</span></span>

- <span data-ttu-id="0f544-114">Erstellen Sie eine neue Azure Functions-App mit einem eindeutigen Namen in der Ressourcengruppe **first-serverless-app**, die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="0f544-114">Create a new Functions app with a unique name in the **first-serverless-app** resource group that you created earlier.</span></span> <span data-ttu-id="0f544-115">Azure Functions-Apps erfordern ein Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="0f544-115">Functions apps require a Storage account.</span></span> <span data-ttu-id="0f544-116">In dieser Einheit verwenden Sie das vorhandene Speicherkonto, das Sie in der letzten Einheit erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="0f544-116">In this unit, you will use the existing storage account you created in the last unit.</span></span>

    ```azurecli
    az functionapp create -n <function app name> -g first-serverless-app -s <storage account name> -c westcentralus
    ```

## <a name="create-an-http-triggered-serverless-function"></a><span data-ttu-id="0f544-117">Erstellen einer per HTTP ausgelösten serverlosen Funktion</span><span class="sxs-lookup"><span data-stu-id="0f544-117">Create an HTTP-triggered serverless function</span></span>

<span data-ttu-id="0f544-118">Um ein Bild sicher in Blob Storage hochzuladen, richtet die Fotogalerie-Web-App eine HTTP-Anforderung an die serverlose Funktion, damit eine zeitlich begrenzte URL generiert wird.</span><span class="sxs-lookup"><span data-stu-id="0f544-118">To securely upload an image to Blob storage, the photo gallery web app makes an HTTP request to the serverless function to generate a time-limited URL.</span></span> <span data-ttu-id="0f544-119">Die Funktion wird per HTTP-Anforderung ausgelöst und verwendet das Azure Storage SDK, um die sichere URL zu generieren und zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="0f544-119">The function is triggered by an HTTP request and uses the Azure Storage SDK to generate and return the secure URL.</span></span>

1. <span data-ttu-id="0f544-120">Nachdem die Funktions-App erstellt wurde, können Sie im [Azure-Portal](https://portal.azure.com/?azure-portal=true) über das Feld **Suchen** danach suchen.</span><span class="sxs-lookup"><span data-stu-id="0f544-120">After the Functions app is created, search for it in the [Azure portal](https://portal.azure.com/?azure-portal=true) using the **Search** box.</span></span> <span data-ttu-id="0f544-121">Klicken Sie auf die App, um sie zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="0f544-121">Click on the app to open it.</span></span>

    ![Öffnen der Funktions-App](../media/2-search-function-app.png)

1. <span data-ttu-id="0f544-123">Zeigen Sie im Fenster der Funktions-App im linken Navigationsbereich auf **Funktionen**, und klicken Sie auf das Pluszeichen (+), um eine neue serverlose Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0f544-123">In the left navigation of the Functions app window, point to **Functions** and click the plus sign (+) to create a new serverless function.</span></span>

    ![Erstellen einer neuen Funktion](../media/2-new-function.png)

1. <span data-ttu-id="0f544-125">Klicken Sie auf **Benutzerdefinierte Funktion**, um eine Liste mit Funktionsvorlagen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="0f544-125">Click **Custom function** to see a list of function templates.</span></span>

1. <span data-ttu-id="0f544-126">Suchen Sie nach der Vorlage **HttpTrigger**, und klicken Sie auf C# oder JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0f544-126">Find the **HttpTrigger** template and click C# or JavaScript.</span></span>

1. <span data-ttu-id="0f544-127">Verwenden Sie die folgenden Werte, um eine Funktion zu erstellen, mit der eine URL für das Hochladen in ein Blob generiert wird:</span><span class="sxs-lookup"><span data-stu-id="0f544-127">Use the following values to create a function that generates a blob upload URL:</span></span>

    | <span data-ttu-id="0f544-128">Einstellung</span><span class="sxs-lookup"><span data-stu-id="0f544-128">Setting</span></span>      |  <span data-ttu-id="0f544-129">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="0f544-129">Suggested value</span></span>   | <span data-ttu-id="0f544-130">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="0f544-130">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="0f544-131">**Sprache**</span><span class="sxs-lookup"><span data-stu-id="0f544-131">**Language**</span></span> | <span data-ttu-id="0f544-132">C# oder JavaScript</span><span class="sxs-lookup"><span data-stu-id="0f544-132">C# or JavaScript</span></span> | <span data-ttu-id="0f544-133">Wählen Sie die Sprache aus, die Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="0f544-133">Select the language that you want to use.</span></span> |
    | <span data-ttu-id="0f544-134">**Name Ihrer Funktion**</span><span class="sxs-lookup"><span data-stu-id="0f544-134">**Name your function**</span></span> | <span data-ttu-id="0f544-135">GetUploadUrl</span><span class="sxs-lookup"><span data-stu-id="0f544-135">GetUploadUrl</span></span> | <span data-ttu-id="0f544-136">Geben Sie diesen Namen genau wie hier angezeigt ein, damit die Anwendung die Funktion ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="0f544-136">Enter this name exactly as shown, so the application can discover the function.</span></span> |
    | <span data-ttu-id="0f544-137">**Autorisierungsstufe**</span><span class="sxs-lookup"><span data-stu-id="0f544-137">**Authorization level**</span></span> | <span data-ttu-id="0f544-138">Anonym</span><span class="sxs-lookup"><span data-stu-id="0f544-138">Anonymous</span></span> | <span data-ttu-id="0f544-139">Lässt den öffentlichen Zugriff auf die Funktion zu.</span><span class="sxs-lookup"><span data-stu-id="0f544-139">Allows the function to be accessed publicly.</span></span> |

    ![Eingeben der Einstellungen für eine neue Funktion, die per HTTP ausgelöst wird](../media/2-new-function-httptrigger.png)

1. <span data-ttu-id="0f544-141">Klicken Sie auf **Erstellen**, um die Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0f544-141">Click **Create** to create the function.</span></span>

<span data-ttu-id="0f544-142">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="0f544-142">::: zone pivot="csharp"</span></span>
1. <span data-ttu-id="0f544-143">(C#) Wenn der Quellcode der Funktion angezeigt wird, ersetzen Sie den gesamten Inhalt der Datei **run.csx** durch den Inhalt der Datei [**csharp/GetUploadUrl/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetUploadUrl/run.csx).</span><span class="sxs-lookup"><span data-stu-id="0f544-143">(C#) When the function's source code appears, replace all of the content in the **run.csx** file with the content in the [**csharp/GetUploadUrl/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetUploadUrl/run.csx) file.</span></span>

<span data-ttu-id="0f544-144">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="0f544-144">::: zone-end</span></span>

<span data-ttu-id="0f544-145">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="0f544-145">::: zone pivot="javascript"</span></span>
1. <span data-ttu-id="0f544-146">(JavaScript) Für diese Funktion ist das `azure-storage`-Paket von npm erforderlich.</span><span class="sxs-lookup"><span data-stu-id="0f544-146">(JavaScript) This function requires the `azure-storage` package from npm.</span></span> <span data-ttu-id="0f544-147">Das Paket generiert das SAS-Token (Shared Access Signature), das zum Erstellen der sicheren URL erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="0f544-147">The package generates the shared access signature (SAS) token that's required to build the secure URL.</span></span> <span data-ttu-id="0f544-148">Klicken Sie zum Installieren des npm-Pakets im linken Navigationsbereich auf die Funktionen-App und dann auf **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="0f544-148">To install the npm package, click on the Functions app on the left navigation and click **Platform features**.</span></span>

1. <span data-ttu-id="0f544-149">(JavaScript) Klicken Sie auf **Konsole**, um ein Konsolenfenster anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="0f544-149">(JavaScript) Click **Console** to reveal a console window.</span></span>

    ![Öffnen eines Konsolenfensters](../media/2-open-console.jpg)

1. <span data-ttu-id="0f544-151">(JavaScript) Vergewissern Sie sich, dass **d:\home\site\wwwroot** das aktuelle Verzeichnis ist, indem Sie den Befehl `cd d:\home\site\wwwroot` ausführen.</span><span class="sxs-lookup"><span data-stu-id="0f544-151">(JavaScript) Ensure the current directory is **d:\home\site\wwwroot** by running the command `cd d:\home\site\wwwroot`.</span></span>

1. <span data-ttu-id="0f544-152">(JavaScript) Führen Sie den Befehl `npm init -y` aus, um eine leere Datei mit dem Namen **package.json** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0f544-152">(JavaScript) Run the command `npm init -y` to create an empty **package.json** file.</span></span>

1. <span data-ttu-id="0f544-153">(JavaScript) Führen Sie den Befehl `npm install --save azure-storage` in der Konsole aus, um das Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="0f544-153">(JavaScript) To install the package, run the command `npm install --save azure-storage` in the console.</span></span> <span data-ttu-id="0f544-154">Speichern Sie das Paket als **package.JSON**.</span><span class="sxs-lookup"><span data-stu-id="0f544-154">Save the package as **package.json**.</span></span> <span data-ttu-id="0f544-155">Es kann einige Minuten dauern, bis der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="0f544-155">It may take a few minutes to complete the operation.</span></span>

1. <span data-ttu-id="0f544-156">(JavaScript) Klicken Sie im linken Navigationsbereich auf die Funktion (**GetUploadUrl**), um sie anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="0f544-156">(JavaScript) Click on the function (**GetUploadUrl**) in the left navigation to reveal the function.</span></span> <span data-ttu-id="0f544-157">Ersetzen Sie den gesamten Inhalt der Datei **index.js** durch den Inhalt der Datei [**javascript/GetUploadUrl/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetUploadUrl/index.js).</span><span class="sxs-lookup"><span data-stu-id="0f544-157">Replace all of the content in the **index.js** file with the content in the [**javascript/GetUploadUrl/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetUploadUrl/index.js) file.</span></span>

    ![Inhalt von „index.js“ nach der Aktualisierung](../media/2-paste-js.jpg)

<span data-ttu-id="0f544-159">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="0f544-159">::: zone-end</span></span>

1. <span data-ttu-id="0f544-160">Klicken Sie unter dem Codefenster auf **Protokolle**, um den Protokollbereich zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="0f544-160">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="0f544-161">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="0f544-161">Click **Save**.</span></span> <span data-ttu-id="0f544-162">Überprüfen Sie den Protokollbereich, um sicherzustellen, dass die Funktion erfolgreich kompiliert wird.</span><span class="sxs-lookup"><span data-stu-id="0f544-162">Check the logs panel to ensure the function is successfully compiled.</span></span>

<span data-ttu-id="0f544-163">Mit der Funktion wird eine SAS-URL (Shared Access Signature) generiert, die zum Hochladen einer Datei in Blob Storage genutzt wird.</span><span class="sxs-lookup"><span data-stu-id="0f544-163">The function generates a shared access signature (SAS) URL that's used to upload a file to Blob storage.</span></span> <span data-ttu-id="0f544-164">Die SAS-URL ist nur für kurze Zeit gültig und lässt nur das Hochladen einer einzelnen Datei zu.</span><span class="sxs-lookup"><span data-stu-id="0f544-164">The SAS URL is valid for a short time and only allows a single file to be uploaded.</span></span> <span data-ttu-id="0f544-165">Die Dokumentation zu Blob Storage enthält weitere Informationen zur [Verwendung von Shared Access Signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="0f544-165">Consult the Blob storage documentation for more information on [how to use shared access signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1).</span></span>


## <a name="add-an-environment-variable-for-the-storage-connection-string"></a><span data-ttu-id="0f544-166">Hinzufügen einer Umgebungsvariablen für die Speicherverbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="0f544-166">Add an environment variable for the storage connection string</span></span>

<span data-ttu-id="0f544-167">Für die erstellte Funktion wird eine Verbindungszeichenfolge für das Speicherkonto benötigt, damit die SAS-URL generiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="0f544-167">The function that you created requires a connection string for the Storage account so that it can generate the SAS URL.</span></span> <span data-ttu-id="0f544-168">Anstatt die Verbindungszeichenfolge im Text der Funktion hartzucodieren, kann sie als Anwendungseinstellung gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="0f544-168">Instead of hardcoding the connection string in the function body, it can be stored as an application setting.</span></span> <span data-ttu-id="0f544-169">Auf Anwendungseinstellungen kann von allen Funktionen der Funktionen-App in Form von Umgebungsvariablen zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="0f544-169">Application settings are accessible as environment variables by all functions in the Functions app.</span></span>

1. <span data-ttu-id="0f544-170">Fragen Sie in Cloud Shell die Speicherkonto-Verbindungszeichenfolge ab, und speichern Sie sie in einer Bash-Variablen mit dem Namen **STORAGE_CONNECTION_STRING**.</span><span class="sxs-lookup"><span data-stu-id="0f544-170">In Cloud Shell, query the Storage account connection string and save it to a Bash variable named **STORAGE_CONNECTION_STRING**.</span></span>

    ```azurecli
    export STORAGE_CONNECTION_STRING=$(az storage account show-connection-string -n <storage account name> -g first-serverless-app --query "connectionString" --output tsv)
    ```

    <span data-ttu-id="0f544-171">Vergewissern Sie sich, dass das Festlegen der Variablen erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="0f544-171">Confirm the variable is set successfully.</span></span>

    ```azurecli
    echo $STORAGE_CONNECTION_STRING
    ```

1. <span data-ttu-id="0f544-172">Erstellen Sie eine neue Anwendungseinstellung mit dem Namen **AZURE_STORAGE_CONNECTION_STRING**, indem Sie den im vorherigen Schritt gespeicherten Wert verwenden.</span><span class="sxs-lookup"><span data-stu-id="0f544-172">Create a new application setting named **AZURE_STORAGE_CONNECTION_STRING** using the value saved from the previous step.</span></span>

    ```azurecli
    az functionapp config appsettings set -n <function app name> -g first-serverless-app --settings AZURE_STORAGE_CONNECTION_STRING=$STORAGE_CONNECTION_STRING -o table
    ```

    <span data-ttu-id="0f544-173">Stellen Sie sicher, dass die Ausgabe des Befehls die neue Anwendungseinstellung mit dem richtigen Wert enthält.</span><span class="sxs-lookup"><span data-stu-id="0f544-173">Confirm that the command's output contains the new application setting with the correct value.</span></span>


## <a name="test-the-serverless-function"></a><span data-ttu-id="0f544-174">Testen der serverlosen Funktion</span><span class="sxs-lookup"><span data-stu-id="0f544-174">Test the serverless function</span></span>

<span data-ttu-id="0f544-175">Zusätzlich zum Erstellen und Bearbeiten von Funktionen enthält das Azure-Portal auch ein integriertes Tool zum Testen von Funktionen.</span><span class="sxs-lookup"><span data-stu-id="0f544-175">In addition to creating and editing functions, the Azure portal also provides a built-in tool for testing functions.</span></span>

1. <span data-ttu-id="0f544-176">Klicken Sie zum Testen der serverlosen HTTP-Funktion rechts im Codefenster auf die Registerkarte **Test** (Testen), um den Testbereich zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="0f544-176">To test the HTTP serverless function, on the right of the code window, click on the **Test** tab to expand the test panel.</span></span>

1. <span data-ttu-id="0f544-177">Ändern Sie die **HTTP-Methode** in **GET**.</span><span class="sxs-lookup"><span data-stu-id="0f544-177">Change the **Http method** to **GET**.</span></span>

1. <span data-ttu-id="0f544-178">Klicken Sie unter **Abfrage** auf **Parameter hinzufügen**, und fügen Sie den folgenden Parameter hinzu:</span><span class="sxs-lookup"><span data-stu-id="0f544-178">Under **Query**, click **Add parameter** and add the following parameter:</span></span>

    | <span data-ttu-id="0f544-179">Name</span><span class="sxs-lookup"><span data-stu-id="0f544-179">Name</span></span>      |  <span data-ttu-id="0f544-180">Wert</span><span class="sxs-lookup"><span data-stu-id="0f544-180">Value</span></span>   | 
    | --- | --- |
    | <span data-ttu-id="0f544-181">**filename**</span><span class="sxs-lookup"><span data-stu-id="0f544-181">**filename**</span></span> | <span data-ttu-id="0f544-182">image1.jpg</span><span class="sxs-lookup"><span data-stu-id="0f544-182">image1.jpg</span></span> |

1. <span data-ttu-id="0f544-183">Klicken Sie im Testbereich auf **Ausführen**, um eine HTTP-Anforderung an die Funktion zu senden.</span><span class="sxs-lookup"><span data-stu-id="0f544-183">In the test panel, click **Run** to send an HTTP request to the function.</span></span>

1. <span data-ttu-id="0f544-184">Die Funktion gibt in der Ausgabe eine Upload-URL zurück.</span><span class="sxs-lookup"><span data-stu-id="0f544-184">The function returns an upload URL in the output.</span></span> <span data-ttu-id="0f544-185">Die Funktionsausführung wird im Protokollbereich angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0f544-185">The function execution appears in the Logs panel.</span></span>

    ![Protokolle mit Informationen zur erfolgreichen Ausführung der Funktion](../media/2-test-function.png)


## <a name="configure-cors-in-the-functions-app"></a><span data-ttu-id="0f544-187">Konfigurieren von CORS in der Funktionen-App</span><span class="sxs-lookup"><span data-stu-id="0f544-187">Configure CORS in the Functions app</span></span>

<span data-ttu-id="0f544-188">Da das Front-End der Funktion in Blob Storage gehostet wird, verfügt es über einen anderen Domänennamen als die Azure Functions-App.</span><span class="sxs-lookup"><span data-stu-id="0f544-188">Because the function front end is hosted in Blob storage, it has a different domain name than the Azure Functions app.</span></span> <span data-ttu-id="0f544-189">Damit der clientseitige JavaScript-Code die erstellte Funktion erfolgreich aufrufen kann, muss die Funktionen-App für Cross-Origin Resource Sharing (CORS) konfiguriert sein.</span><span class="sxs-lookup"><span data-stu-id="0f544-189">For the client-side JavaScript to successfully call the function that you created, the Functions app has to be configured for cross-origin resource sharing (CORS).</span></span>

1. <span data-ttu-id="0f544-190">Klicken Sie im Fenster der Funktionen-App im linken Navigationsbereich auf den Namen Ihrer Funktionen-App.</span><span class="sxs-lookup"><span data-stu-id="0f544-190">In the left navigation of the Functions app window, click on the name of your Functions app.</span></span>

1. <span data-ttu-id="0f544-191">Klicken Sie auf **Plattformfeatures**, um eine Liste mit erweiterten Features anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="0f544-191">Click on **Platform features** to view a list of advanced features.</span></span>

1. <span data-ttu-id="0f544-192">Klicken Sie unter **API** auf **CORS**.</span><span class="sxs-lookup"><span data-stu-id="0f544-192">Under **API**, click **CORS**.</span></span>

    ![Auswählen von CORS](../media/2-open-cors.jpg)

1. <span data-ttu-id="0f544-194">Fügen Sie aus dem vorherigen Modul einen zulässigen Ursprung für die Anwendungs-URL hinzu, und lassen Sie den nachgestellten Schrägstrich (/) weg.</span><span class="sxs-lookup"><span data-stu-id="0f544-194">Add an allow origin for the application URL from the previous module and omit the trailing slash (/).</span></span> <span data-ttu-id="0f544-195">Beispiel: `https://firstserverlessweb.z4.web.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="0f544-195">For example: `https://firstserverlessweb.z4.web.core.windows.net`.</span></span>

    ![CORS-Einstellungen mit hinzugefügter URL für serverlose Web-App](../media/2-add-cors.png)

1. <span data-ttu-id="0f544-197">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="0f544-197">Click **Save**.</span></span>

<span data-ttu-id="0f544-198">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="0f544-198">::: zone pivot="csharp"</span></span>
1. <span data-ttu-id="0f544-199">(C#) Navigieren Sie zurück zur Funktion `GetUploadUrl`, und wählen Sie die Registerkarte **Integrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="0f544-199">(C#) Navigate back to the `GetUploadUrl` function and select the **Integrate** tab.</span></span>

1. <span data-ttu-id="0f544-200">(C#) Wählen Sie unter **Ausgewählte HTTP-Methoden** die Option **OPTIONS**.</span><span class="sxs-lookup"><span data-stu-id="0f544-200">(C#) Under **Selected HTTP methods**, select **OPTIONS**.</span></span>

    <span data-ttu-id="0f544-201">**GET**, **POST** und **OPTIONS** sollten jeweils ausgewählt sein.</span><span class="sxs-lookup"><span data-stu-id="0f544-201">**GET**, **POST**, and **OPTIONS** should all be selected.</span></span> <span data-ttu-id="0f544-202">Für CORS wird die **OPTIONS**-Methode verwendet, die für C#-Funktionen nicht standardmäßig ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="0f544-202">CORS uses the **OPTIONS** method, which isn't selected by default for C# functions.</span></span>  

1. <span data-ttu-id="0f544-203">(C#) Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="0f544-203">(C#) Click **Save**.</span></span>

<span data-ttu-id="0f544-204">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="0f544-204">::: zone-end</span></span>

1. <span data-ttu-id="0f544-205">Navigieren Sie im Azure-Portal zur Funktions-App.</span><span class="sxs-lookup"><span data-stu-id="0f544-205">Still in the Azure portal, navigate to the Functions app.</span></span> <span data-ttu-id="0f544-206">Klicken Sie auf die Registerkarte **Übersicht**. Klicken Sie auf **Neu starten**, um sicherzustellen, dass die Änderungen für CORS wirksam werden.</span><span class="sxs-lookup"><span data-stu-id="0f544-206">Select the **Overview** tab. Click **Restart** to make sure that the changes for CORS take effect.</span></span>

## <a name="configure-cors-in-the-storage-account"></a><span data-ttu-id="0f544-207">Konfigurieren von CORS im Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="0f544-207">Configure CORS in the Storage account</span></span>

<span data-ttu-id="0f544-208">Da die Funktionen-App auch clientseitige JavaScript-Aufrufe zum Hochladen von Dateien an Blob Storage richtet, müssen Sie das Speicherkonto für CORS konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="0f544-208">Because the Functions app also makes client-side JavaScript calls to Blob storage to upload files, you have to configure the Storage account for CORS.</span></span>

- <span data-ttu-id="0f544-209">Führen Sie den folgenden Befehl aus, um für alle Ursprungsorte das Hochladen in das Speicherkonto zuzulassen:</span><span class="sxs-lookup"><span data-stu-id="0f544-209">Run the following command to allow all origins to upload files to the Storage account:</span></span>

    ```azurecli
    az storage cors add --methods OPTIONS PUT --origins '*' --exposed-headers '*' --allowed-headers '*' --services b --account-name <storage account name>
    ```


## <a name="modify-the-web-app-to-upload-images"></a><span data-ttu-id="0f544-210">Ändern der Web-App zum Hochladen von Bildern</span><span class="sxs-lookup"><span data-stu-id="0f544-210">Modify the web app to upload images</span></span>

<span data-ttu-id="0f544-211">Die Web-App ruft Einstellungen aus einer Datei mit dem Namen **settings.js** ab.</span><span class="sxs-lookup"><span data-stu-id="0f544-211">The web app retrieves settings from a file named **settings.js**.</span></span> <span data-ttu-id="0f544-212">In den folgenden Schritten erstellen Sie die Datei mit Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="0f544-212">In the following steps, you create the file using Cloud Shell.</span></span> <span data-ttu-id="0f544-213">Sie legen `window.apiBaseUrl` auf die URL der Funktionen-App und `window.blobBaseUrl` auf die URL des Azure Blob Storage-Endpunkts fest.</span><span class="sxs-lookup"><span data-stu-id="0f544-213">You set `window.apiBaseUrl` to the URL of the Functions app, and `window.blobBaseUrl` to the URL of the Azure Blob storage endpoint.</span></span>

1. <span data-ttu-id="0f544-214">Stellen Sie in Cloud Shell sicher, dass das aktuelle Verzeichnis der Ordner **www/dist** ist.</span><span class="sxs-lookup"><span data-stu-id="0f544-214">In Cloud Shell, ensure that the current directory is the **www/dist** folder.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. <span data-ttu-id="0f544-215">Fragen Sie die URL der Funktionen-App ab, und speichern Sie sie in einer Bash-Variablen mit dem Namen **FUNCTION_APP_URL**.</span><span class="sxs-lookup"><span data-stu-id="0f544-215">Query the URL of the Functions app and store it in a Bash variable named **FUNCTION_APP_URL**.</span></span>

    ```azurecli
    export FUNCTION_APP_URL="https://"$(az functionapp show -n <function app name> -g first-serverless-app --query "defaultHostName" --output tsv)
    ```

    <span data-ttu-id="0f544-216">Vergewissern Sie sich, dass die Variable richtig festgelegt wurde.</span><span class="sxs-lookup"><span data-stu-id="0f544-216">Confirm the variable is correctly set.</span></span>

    ```azurecli
    echo $FUNCTION_APP_URL
    ```

1. <span data-ttu-id="0f544-217">Um den Basis-URI für API-Aufrufe Ihrer Funktionen-App festzulegen, erstellen Sie die Datei **settings.js**.</span><span class="sxs-lookup"><span data-stu-id="0f544-217">To set the base URI of API calls to your Functions app, create the **settings.js** file.</span></span> <span data-ttu-id="0f544-218">Fügen Sie die URL der Funktionen-App wie im folgenden Beispiel hinzu:</span><span class="sxs-lookup"><span data-stu-id="0f544-218">Add the URL of the Functions app like the following example:</span></span>

    `window.apiBaseUrl = 'https://fnapp@lab.GlobalLabInstanceId.azurewebsites.net'`

    <span data-ttu-id="0f544-219">Sie können die Änderung vornehmen, indem Sie den folgenden Befehl ausführen oder einen Befehlszeilen-Editor wie VIM verwenden.</span><span class="sxs-lookup"><span data-stu-id="0f544-219">You can make the change by running the following command or by using a command-line editor like VIM.</span></span>

    ```azurecli
    echo "window.apiBaseUrl = '$FUNCTION_APP_URL'" > settings.js
    ```

    <span data-ttu-id="0f544-220">Vergewissern Sie sich, dass das Schreiben der Datei erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="0f544-220">Confirm the file was successfully written.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="0f544-221">Fragen Sie die Blob Storage-Basis-URL ab, und speichern Sie sie in einer Bash-Variablen mit dem Namen **BLOB_BASE_URL**.</span><span class="sxs-lookup"><span data-stu-id="0f544-221">Query the base URL for the Blob storage and store it in a Bash variable named **BLOB_BASE_URL**.</span></span>

    ```azurecli
    export BLOB_BASE_URL=$(az storage account show -n <storage account name> -g first-serverless-app --query primaryEndpoints.blob -o tsv | sed 's/\/$//')
    ```

    <span data-ttu-id="0f544-222">Vergewissern Sie sich, dass die Variable richtig festgelegt wurde.</span><span class="sxs-lookup"><span data-stu-id="0f544-222">Confirm the variable is correctly set.</span></span>

    ```azurecli
    echo $BLOB_BASE_URL
    ```

1. <span data-ttu-id="0f544-223">Um den Basis-URI für API-Aufrufe an Ihre Funktionen-App festzulegen, fügen Sie die Blob Storage-URL wie im folgenden Beispiel an die Datei **settings.js** an:</span><span class="sxs-lookup"><span data-stu-id="0f544-223">To set the base URI of API calls to your Functions app, append the Blob storage URL to the **settings.js** file like the following example:</span></span>

    `window.blobBaseUrl = 'https://mystorage.blob.core.windows.net'`

    <span data-ttu-id="0f544-224">Sie können die Änderung vornehmen, indem Sie den folgenden Befehl ausführen oder einen Befehlszeilen-Editor wie VIM verwenden.</span><span class="sxs-lookup"><span data-stu-id="0f544-224">You can make the change by running the following command or by using a command-line editor like VIM.</span></span>

    ```azurecli
    echo "window.blobBaseUrl = '$BLOB_BASE_URL'" >> settings.js
    ```

    <span data-ttu-id="0f544-225">Vergewissern Sie sich, dass das Schreiben der Datei erfolgreich war und dass sie jetzt zwei Zeilen enthält.</span><span class="sxs-lookup"><span data-stu-id="0f544-225">Confirm the file was successfully written and now contains two lines.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="0f544-226">Laden Sie die Datei in Blog Storage hoch.</span><span class="sxs-lookup"><span data-stu-id="0f544-226">Upload the file to Blob storage.</span></span>

    ```azurecli
    az storage blob upload -c \$web --account-name <storage account name> -f settings.js -n settings.js
    ```


## <a name="test-the-web-application"></a><span data-ttu-id="0f544-227">Testen der Webanwendung</span><span class="sxs-lookup"><span data-stu-id="0f544-227">Test the web application</span></span>

<span data-ttu-id="0f544-228">An diesem Punkt kann die Galerieanwendung ein Bild in Blog Storage hochladen, aber sie kann noch keine Bilder anzeigen.</span><span class="sxs-lookup"><span data-stu-id="0f544-228">At this point, the gallery application is able to upload an image to Blob storage, but it can't display images yet.</span></span> <span data-ttu-id="0f544-229">Die Anwendung versucht, die Funktion `GetImages` aufzurufen. Diese ist aber noch nicht vorhanden, da Sie sie erst in einem späteren Modul erstellen.</span><span class="sxs-lookup"><span data-stu-id="0f544-229">It will try to call a `GetImages` function that doesn't exist yet because you create it in a later module.</span></span> <span data-ttu-id="0f544-230">Der Aufruf ist nicht erfolgreich, und scheinbar hängt die Webseite mit einem Hinweis der Art „Wird analysiert...“, aber der Upload des gewählten Bilds ist trotzdem erfolgreich.</span><span class="sxs-lookup"><span data-stu-id="0f544-230">The call will fail and the web page will appear to be stuck on "Analyzing...," but the image you select will be successfully uploaded.</span></span>

<span data-ttu-id="0f544-231">Sie können sich vergewissern, ob ein Bild erfolgreich hochgeladen wurde, indem Sie im Azure-Portal den Inhalt des Containers **images** überprüfen.</span><span class="sxs-lookup"><span data-stu-id="0f544-231">You can verify that an image is successfully uploaded by checking the contents of the **images** container in the Azure portal.</span></span>

1. <span data-ttu-id="0f544-232">Navigieren Sie in einem Browserfenster zur Anwendung.</span><span class="sxs-lookup"><span data-stu-id="0f544-232">In a browser window, browse to the application.</span></span> <span data-ttu-id="0f544-233">Wählen Sie eine Bilddatei aus, und laden Sie sie hoch.</span><span class="sxs-lookup"><span data-stu-id="0f544-233">Select an image file and upload it.</span></span> <span data-ttu-id="0f544-234">Der Upload wird abgeschlossen. Da wir aber noch nicht die Möglichkeit zum Anzeigen von Bildern hinzugefügt haben, wird das hochgeladene Bild von der App nicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0f544-234">The upload completes, but because we haven't added the ability to display images yet, the app doesn't show the uploaded photo.</span></span> <span data-ttu-id="0f544-235">(Die Webseite scheint beim Vorgang „Bild wird analysiert...“ zu hängen. Dies beheben Sie später.)</span><span class="sxs-lookup"><span data-stu-id="0f544-235">(The web page appears to be stuck on "Analyzing image..." You'll fix that later.)</span></span>

1. <span data-ttu-id="0f544-236">Vergewissern Sie sich in Cloud Shell, dass das Bild in den Container **images** hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="0f544-236">In Cloud Shell, confirm the image was uploaded to the **images** container.</span></span>

    ```azurecli
    az storage blob list --account-name <storage account name> -c images -o table
    ```

1. <span data-ttu-id="0f544-237">Löschen Sie alle Dateien im Container **images**, bevor Sie mit dem nächsten Tutorial fortfahren.</span><span class="sxs-lookup"><span data-stu-id="0f544-237">Before moving on to the next tutorial, delete all files in the **images** container.</span></span>

    ```azurecli
    az storage blob delete-batch -s images --account-name <storage account name>
    ```

## <a name="summary"></a><span data-ttu-id="0f544-238">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="0f544-238">Summary</span></span>

<span data-ttu-id="0f544-239">In dieser Einheit haben Sie eine Azure Functions-App erstellt und erfahren, wie Sie eine serverlose Funktion verwenden, um für eine Webanwendung das Hochladen von Bildern in Blob Storage zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="0f544-239">In this unit, you created an Azure Functions app and learned how to use a serverless function to allow a web application to upload images to Blob storage.</span></span> <span data-ttu-id="0f544-240">Als Nächstes erfahren Sie, wie Sie Miniaturansichten für die hochgeladenen Bilder erstellen, indem Sie eine per Blob ausgelöste serverlose Funktion verwenden.</span><span class="sxs-lookup"><span data-stu-id="0f544-240">Next, you will learn how to create thumbnails for the uploaded images using a blob-triggered serverless function.</span></span>