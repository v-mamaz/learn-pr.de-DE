<span data-ttu-id="c2122-101">Bei der von Ihnen erstellten Anwendung handelt es sich um eine Fotogalerie.</span><span class="sxs-lookup"><span data-stu-id="c2122-101">The application you're building is a photo gallery.</span></span> <span data-ttu-id="c2122-102">Es wird clientseitiger JavaScript-Code verwendet, um APIs zum Hochladen und Anzeigen von Bildern aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="c2122-102">It uses client-side JavaScript to call APIs to upload and display images.</span></span> <span data-ttu-id="c2122-103">In dieser Einheit erstellen Sie eine API, indem Sie eine serverlose Funktion verwenden, mit der eine URL mit zeitlicher Beschränkung zum Hochladen eines Bilds generiert wird.</span><span class="sxs-lookup"><span data-stu-id="c2122-103">In this unit, you will create an API using a serverless function that generates a time-limited URL to upload an image.</span></span> <span data-ttu-id="c2122-104">Die Webanwendung nutzt diese URL zum Hochladen eines Bilds in Blob Storage mit der [Blob Storage-REST-API](https://docs.microsoft.com/rest/api/storageservices/blob-service-rest-api).</span><span class="sxs-lookup"><span data-stu-id="c2122-104">The web application uses this URL to upload an image to Blob storage using the [Blob storage REST API](https://docs.microsoft.com/rest/api/storageservices/blob-service-rest-api).</span></span>

## <a name="create-a-blob-storage-container-for-images"></a><span data-ttu-id="c2122-105">Erstellen eines Blob Storage-Containers für Bilder</span><span class="sxs-lookup"><span data-stu-id="c2122-105">Create a Blob storage container for images</span></span>

<span data-ttu-id="c2122-106">Für die Anwendung ist ein separater Speichercontainer erforderlich, um Bilder hochladen und hosten zu können.</span><span class="sxs-lookup"><span data-stu-id="c2122-106">The application requires a separate storage container to upload and host images.</span></span>

<span data-ttu-id="c2122-107">Erstellen Sie unter Ihrem Speicherkonto einen neuen Container mit dem Namen **images**, der über öffentlichen Zugriff auf alle Blobs verfügt.</span><span class="sxs-lookup"><span data-stu-id="c2122-107">Create a new container in your Storage account named **images** in your Storage account with public access to all blobs.</span></span>

```azurecli
az storage container create \
    -n images \
    --account-name <storage account name> \
    --public-access blob
```

## <a name="create-a-function-app"></a><span data-ttu-id="c2122-108">Erstellen einer Funktions-App</span><span class="sxs-lookup"><span data-stu-id="c2122-108">Create a function app</span></span>

<span data-ttu-id="c2122-109">Azure Functions ist ein Dienst zum Ausführen serverloser Funktionen.</span><span class="sxs-lookup"><span data-stu-id="c2122-109">Azure Functions is a service for running serverless functions.</span></span> <span data-ttu-id="c2122-110">Eine serverlose Funktion kann von Ereignissen, z.B. einer HTTP-Anforderung, oder bei Erstellung eines Blobs in einem Speichercontainer ausgelöst (aufgerufen) werden.</span><span class="sxs-lookup"><span data-stu-id="c2122-110">A serverless function can be triggered (called) by events, such as an HTTP request, or when a blob is created in a storage container.</span></span>

<span data-ttu-id="c2122-111">Eine Funktions-App ist ein Container für mindestens eine serverlose Funktion.</span><span class="sxs-lookup"><span data-stu-id="c2122-111">A function app is a container for one or more serverless functions.</span></span>

<span data-ttu-id="c2122-112">Erstellen Sie eine neue Funktions-App mit einem eindeutigen Namen.</span><span class="sxs-lookup"><span data-stu-id="c2122-112">Create a new function app with a unique name.</span></span> <span data-ttu-id="c2122-113">Funktions-App erfordern ein Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="c2122-113">Function apps require a Storage account.</span></span> <span data-ttu-id="c2122-114">In dieser Einheit verwenden Sie das vorhandene Speicherkonto, das Sie in der letzten Einheit erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c2122-114">In this unit, you will use the existing storage account you created in the last unit.</span></span>

```azurecli
az functionapp create \
    -n <function app name> \
    -g <rgn>[Sandbox resource group name]</rgn> \
    -s <storage account name> \
    --consumption-plan-location $(az group show -n <rgn>[Sandbox resource group name]</rgn> --query location --output tsv)
```

## <a name="create-an-http-triggered-serverless-function"></a><span data-ttu-id="c2122-115">Erstellen einer per HTTP ausgelösten serverlosen Funktion</span><span class="sxs-lookup"><span data-stu-id="c2122-115">Create an HTTP-triggered serverless function</span></span>

<span data-ttu-id="c2122-116">Um ein Bild sicher in Blob Storage hochzuladen, richtet die Fotogalerie-Web-App eine HTTP-Anforderung an die serverlose Funktion, damit eine zeitlich begrenzte URL generiert wird.</span><span class="sxs-lookup"><span data-stu-id="c2122-116">To securely upload an image to Blob storage, the photo gallery web app makes an HTTP request to the serverless function to generate a time-limited URL.</span></span> <span data-ttu-id="c2122-117">Die Funktion wird per HTTP-Anforderung ausgelöst und verwendet das Azure Storage SDK, um die sichere URL zu generieren und zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="c2122-117">The function is triggered by an HTTP request and uses the Azure Storage SDK to generate and return the secure URL.</span></span>

1. <span data-ttu-id="c2122-118">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="c2122-118">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="c2122-119">Suchen Sie im Feld **Suchen** nach der Funktions-App, die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c2122-119">Search for the function app you just created using the **Search** box.</span></span> <span data-ttu-id="c2122-120">Klicken Sie auf das Ergebnis aus, um es zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="c2122-120">Click on the result to open it.</span></span>

    ![Öffnen der Funktions-App](../media/2-search-function-app.png)

1. <span data-ttu-id="c2122-122">Zeigen Sie im Fenster der Funktions-App im linken Navigationsbereich auf **Funktionen**, und klicken Sie auf das Pluszeichen (+), um eine neue serverlose Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c2122-122">In the left navigation of the Function Apps window, point to **Functions** and click the plus sign (+) to create a new serverless function.</span></span>

    ![Erstellen einer neuen Funktion](../media/2-new-function.png)

1. <span data-ttu-id="c2122-124">Klicken Sie auf **Benutzerdefinierte Funktion**, um eine Liste mit Funktionsvorlagen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c2122-124">Click **Custom function** to see a list of function templates.</span></span>

1. <span data-ttu-id="c2122-125">Suchen Sie nach der Vorlage **HttpTrigger**, und klicken Sie auf C# oder JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c2122-125">Find the **HttpTrigger** template and click C# or JavaScript.</span></span>

1. <span data-ttu-id="c2122-126">Verwenden Sie die folgenden Werte, um eine Funktion zu erstellen, mit der eine URL für das Hochladen in ein Blob generiert wird:</span><span class="sxs-lookup"><span data-stu-id="c2122-126">Use the following values to create a function that generates a blob upload URL:</span></span>

    | <span data-ttu-id="c2122-127">Einstellung</span><span class="sxs-lookup"><span data-stu-id="c2122-127">Setting</span></span>      |  <span data-ttu-id="c2122-128">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="c2122-128">Suggested value</span></span>   | <span data-ttu-id="c2122-129">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="c2122-129">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="c2122-130">**Sprache**</span><span class="sxs-lookup"><span data-stu-id="c2122-130">**Language**</span></span> | <span data-ttu-id="c2122-131">C# oder JavaScript</span><span class="sxs-lookup"><span data-stu-id="c2122-131">C# or JavaScript</span></span> | <span data-ttu-id="c2122-132">Wählen Sie die Sprache aus, die Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="c2122-132">Select the language that you want to use.</span></span> |
    | <span data-ttu-id="c2122-133">**Name Ihrer Funktion**</span><span class="sxs-lookup"><span data-stu-id="c2122-133">**Name your function**</span></span> | <span data-ttu-id="c2122-134">GetUploadUrl</span><span class="sxs-lookup"><span data-stu-id="c2122-134">GetUploadUrl</span></span> | <span data-ttu-id="c2122-135">Geben Sie diesen Namen genau wie hier angezeigt ein, damit die Anwendung die Funktion ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="c2122-135">Enter this name exactly as shown, so the application can discover the function.</span></span> |
    | <span data-ttu-id="c2122-136">**Autorisierungsstufe**</span><span class="sxs-lookup"><span data-stu-id="c2122-136">**Authorization level**</span></span> | <span data-ttu-id="c2122-137">Anonym</span><span class="sxs-lookup"><span data-stu-id="c2122-137">Anonymous</span></span> | <span data-ttu-id="c2122-138">Lässt den öffentlichen Zugriff auf die Funktion zu.</span><span class="sxs-lookup"><span data-stu-id="c2122-138">Allows the function to be accessed publicly.</span></span> |

    ![Eingeben der Einstellungen für eine neue Funktion, die per HTTP ausgelöst wird](../media/2-new-function-httptrigger.png)

1. <span data-ttu-id="c2122-140">Klicken Sie auf **Erstellen**, um die Funktion zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c2122-140">Click **Create** to create the function.</span></span>

<span data-ttu-id="c2122-141">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="c2122-141">::: zone pivot="csharp"</span></span>

8. <span data-ttu-id="c2122-142">Wenn der Quellcode der Funktion angezeigt wird, ersetzen Sie den gesamten Inhalt der Datei **run.csx** durch den Inhalt der Datei [**csharp/GetUploadUrl/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetUploadUrl/run.csx).</span><span class="sxs-lookup"><span data-stu-id="c2122-142">When the function's source code appears, replace all of the content in the **run.csx** file with the content in the [**csharp/GetUploadUrl/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetUploadUrl/run.csx) file.</span></span>

1. <span data-ttu-id="c2122-143">Klicken Sie unter dem Codefenster auf **Protokolle**, um den Protokollbereich zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="c2122-143">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="c2122-144">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c2122-144">Click **Save**.</span></span> <span data-ttu-id="c2122-145">Überprüfen Sie den Protokollbereich, um sicherzustellen, dass die Funktion erfolgreich kompiliert wird.</span><span class="sxs-lookup"><span data-stu-id="c2122-145">Check the logs panel to ensure the function is successfully compiled.</span></span>

<span data-ttu-id="c2122-146">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="c2122-146">::: zone-end</span></span>

<span data-ttu-id="c2122-147">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="c2122-147">::: zone pivot="javascript"</span></span>

8. <span data-ttu-id="c2122-148">Für diese Funktion ist das `azure-storage`-Paket von npm erforderlich.</span><span class="sxs-lookup"><span data-stu-id="c2122-148">This function requires the `azure-storage` package from npm.</span></span> <span data-ttu-id="c2122-149">Das Paket generiert das SAS-Token (Shared Access Signature), das zum Erstellen der sicheren URL erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="c2122-149">The package generates the shared access signature (SAS) token that's required to build the secure URL.</span></span> <span data-ttu-id="c2122-150">Klicken Sie zum Installieren des npm-Pakets im linken Navigationsbereich auf die Funktions-App und dann auf **Plattformfeatures**.</span><span class="sxs-lookup"><span data-stu-id="c2122-150">To install the npm package, click on the Functions app on the left navigation and click **Platform features**.</span></span>

1. <span data-ttu-id="c2122-151">Klicken Sie auf **Konsole**, um ein Konsolenfenster anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c2122-151">Click **Console** to reveal a console window.</span></span>

    ![Öffnen eines Konsolenfensters](../media/2-open-console.jpg)

1. <span data-ttu-id="c2122-153">Vergewissern Sie sich, dass **d:\home\site\wwwroot** das aktuelle Verzeichnis ist, indem Sie den Befehl `cd d:\home\site\wwwroot` ausführen.</span><span class="sxs-lookup"><span data-stu-id="c2122-153">Ensure the current directory is **d:\home\site\wwwroot** by running the command `cd d:\home\site\wwwroot`.</span></span>

1. <span data-ttu-id="c2122-154">Führen Sie den Befehl `npm init -y` aus, um eine leere Datei mit dem Namen **package.json** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="c2122-154">Run the command `npm init -y` to create an empty **package.json** file.</span></span>

1. <span data-ttu-id="c2122-155">Führen Sie den Befehl `npm install --save azure-storage` in der Konsole aus, um das Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="c2122-155">To install the package, run the command `npm install --save azure-storage` in the console.</span></span> <span data-ttu-id="c2122-156">Speichern Sie das Paket als **package.JSON**.</span><span class="sxs-lookup"><span data-stu-id="c2122-156">Save the package as **package.json**.</span></span> <span data-ttu-id="c2122-157">Es kann einige Minuten dauern, bis der Vorgang abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="c2122-157">It may take a few minutes to complete the operation.</span></span>

1. <span data-ttu-id="c2122-158">Klicken Sie im linken Navigationsbereich auf die Funktion (**GetUploadUrl**), um sie anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c2122-158">Click on the function (**GetUploadUrl**) in the left navigation to reveal the function.</span></span> <span data-ttu-id="c2122-159">Ersetzen Sie den gesamten Inhalt der Datei **index.js** durch den Inhalt der Datei [**javascript/GetUploadUrl/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetUploadUrl/index.js).</span><span class="sxs-lookup"><span data-stu-id="c2122-159">Replace all of the content in the **index.js** file with the content in the [**javascript/GetUploadUrl/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetUploadUrl/index.js) file.</span></span>

    ![Inhalt von „index.js“ nach der Aktualisierung](../media/2-paste-js.jpg)

1. <span data-ttu-id="c2122-161">Klicken Sie unter dem Codefenster auf **Protokolle**, um den Protokollbereich zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="c2122-161">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="c2122-162">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c2122-162">Click **Save**.</span></span> <span data-ttu-id="c2122-163">Überprüfen Sie den Protokollbereich, um sicherzustellen, dass die Funktion erfolgreich kompiliert wird.</span><span class="sxs-lookup"><span data-stu-id="c2122-163">Check the logs panel to ensure the function is successfully compiled.</span></span>

<span data-ttu-id="c2122-164">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="c2122-164">::: zone-end</span></span>

<span data-ttu-id="c2122-165">Mit der Funktion wird eine SAS-URL (Shared Access Signature) generiert, die zum Hochladen einer Datei in Blob Storage genutzt wird.</span><span class="sxs-lookup"><span data-stu-id="c2122-165">The function generates a shared access signature (SAS) URL that's used to upload a file to Blob storage.</span></span> <span data-ttu-id="c2122-166">Die SAS-URL ist nur für kurze Zeit gültig und lässt nur das Hochladen einer einzelnen Datei zu.</span><span class="sxs-lookup"><span data-stu-id="c2122-166">The SAS URL is valid for a short time and only allows a single file to be uploaded.</span></span> <span data-ttu-id="c2122-167">Die Dokumentation zu Blob Storage enthält weitere Informationen zur [Verwendung von Shared Access Signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="c2122-167">Consult the Blob storage documentation for more information on [how to use shared access signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1).</span></span>


## <a name="add-an-environment-variable-for-the-storage-connection-string"></a><span data-ttu-id="c2122-168">Hinzufügen einer Umgebungsvariablen für die Speicherverbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="c2122-168">Add an environment variable for the storage connection string</span></span>

<span data-ttu-id="c2122-169">Für die erstellte Funktion wird eine Verbindungszeichenfolge für das Speicherkonto benötigt, damit die SAS-URL generiert werden kann.</span><span class="sxs-lookup"><span data-stu-id="c2122-169">The function that you created requires a connection string for the Storage account so that it can generate the SAS URL.</span></span> <span data-ttu-id="c2122-170">Anstatt die Verbindungszeichenfolge im Text der Funktion hartzucodieren, kann sie als Anwendungseinstellung gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="c2122-170">Instead of hardcoding the connection string in the function body, it can be stored as an application setting.</span></span> <span data-ttu-id="c2122-171">Auf Anwendungseinstellungen kann von allen Funktionen der Funktions-App in Form von Umgebungsvariablen zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="c2122-171">Application settings are accessible as environment variables by all functions in the function app.</span></span>

1. <span data-ttu-id="c2122-172">Fragen Sie in Cloud Shell die Verbindungszeichenfolge des Speicherkontos ab, und speichern Sie sie in einer Bash-Variablen mit dem Namen **STORAGE_CONNECTION_STRING**.</span><span class="sxs-lookup"><span data-stu-id="c2122-172">In Cloud Shell, query the Storage account connection string and save it to a Bash variable named **STORAGE_CONNECTION_STRING**.</span></span>

    ```azurecli
    export STORAGE_CONNECTION_STRING=$(az storage account show-connection-string -n <storage account name> -g <rgn>[Sandbox resource group name]</rgn> --query "connectionString" --output tsv)
    ```

    <span data-ttu-id="c2122-173">Vergewissern Sie sich, dass das Festlegen der Variablen erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="c2122-173">Confirm the variable is set successfully.</span></span>

    ```azurecli
    echo $STORAGE_CONNECTION_STRING
    ```

1. <span data-ttu-id="c2122-174">Erstellen Sie eine neue Anwendungseinstellung mit dem Namen **AZURE_STORAGE_CONNECTION_STRING**, indem Sie den im vorherigen Schritt gespeicherten Wert verwenden.</span><span class="sxs-lookup"><span data-stu-id="c2122-174">Create a new application setting named **AZURE_STORAGE_CONNECTION_STRING** using the value saved from the previous step.</span></span>

    ```azurecli
    az functionapp config appsettings set \
        -n <function app name> \
        -g <rgn>[Sandbox resource group name]</rgn> \
        --settings AZURE_STORAGE_CONNECTION_STRING=$STORAGE_CONNECTION_STRING \
        -o table
    ```

    <span data-ttu-id="c2122-175">Stellen Sie sicher, dass die Ausgabe des Befehls die neue Anwendungseinstellung mit dem richtigen Wert enthält.</span><span class="sxs-lookup"><span data-stu-id="c2122-175">Confirm that the command's output contains the new application setting with the correct value.</span></span>

## <a name="test-the-serverless-function"></a><span data-ttu-id="c2122-176">Testen der serverlosen Funktion</span><span class="sxs-lookup"><span data-stu-id="c2122-176">Test the serverless function</span></span>

<span data-ttu-id="c2122-177">Zusätzlich zum Erstellen und Bearbeiten von Funktionen enthält das Azure-Portal auch ein integriertes Tool zum Testen von Funktionen.</span><span class="sxs-lookup"><span data-stu-id="c2122-177">In addition to creating and editing functions, the Azure portal also provides a built-in tool for testing functions.</span></span>

1. <span data-ttu-id="c2122-178">Klicken Sie zum Testen der serverlosen HTTP-Funktion rechts im Codefenster auf die Registerkarte **Test** (Testen), um den Testbereich zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="c2122-178">To test the HTTP serverless function, on the right of the code window, click on the **Test** tab to expand the test panel.</span></span>

1. <span data-ttu-id="c2122-179">Ändern Sie die **HTTP-Methode** in **GET**.</span><span class="sxs-lookup"><span data-stu-id="c2122-179">Change the **Http method** to **GET**.</span></span>

1. <span data-ttu-id="c2122-180">Klicken Sie unter **Abfrage** auf **Parameter hinzufügen**, und fügen Sie den folgenden Parameter hinzu:</span><span class="sxs-lookup"><span data-stu-id="c2122-180">Under **Query**, click **Add parameter** and add the following parameter:</span></span>

    | <span data-ttu-id="c2122-181">Name</span><span class="sxs-lookup"><span data-stu-id="c2122-181">Name</span></span>      |  <span data-ttu-id="c2122-182">Wert</span><span class="sxs-lookup"><span data-stu-id="c2122-182">Value</span></span>   | 
    | --- | --- |
    | <span data-ttu-id="c2122-183">**filename**</span><span class="sxs-lookup"><span data-stu-id="c2122-183">**filename**</span></span> | <span data-ttu-id="c2122-184">image1.jpg</span><span class="sxs-lookup"><span data-stu-id="c2122-184">image1.jpg</span></span> |

1. <span data-ttu-id="c2122-185">Klicken Sie im Testbereich auf **Ausführen**, um eine HTTP-Anforderung an die Funktion zu senden.</span><span class="sxs-lookup"><span data-stu-id="c2122-185">In the test panel, click **Run** to send an HTTP request to the function.</span></span>

1. <span data-ttu-id="c2122-186">Die Funktion gibt in der Ausgabe eine Upload-URL zurück.</span><span class="sxs-lookup"><span data-stu-id="c2122-186">The function returns an upload URL in the output.</span></span> <span data-ttu-id="c2122-187">Die Funktionsausführung wird im Protokollbereich angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c2122-187">The function execution appears in the Logs panel.</span></span>

    ![Protokolle mit Informationen zur erfolgreichen Ausführung der Funktion](../media/2-test-function.png)

## <a name="configure-cors-in-the-function-app"></a><span data-ttu-id="c2122-189">Konfigurieren von CORS in der Funktions-App</span><span class="sxs-lookup"><span data-stu-id="c2122-189">Configure CORS in the function app</span></span>

<span data-ttu-id="c2122-190">Da das Front-End der Funktion in Blob Storage gehostet wird, verfügt es über einen anderen Domänennamen als die Funktions-App.</span><span class="sxs-lookup"><span data-stu-id="c2122-190">Because the function front end is hosted in Blob storage, it has a different domain name than the function app.</span></span> <span data-ttu-id="c2122-191">Damit der clientseitige JavaScript-Code die erstellte Funktion erfolgreich aufrufen kann, muss die Funktions-App für CORS (Cross-Origin Resource Sharing) konfiguriert sein.</span><span class="sxs-lookup"><span data-stu-id="c2122-191">For the client-side JavaScript to successfully call the function that you created, the function app has to be configured for cross-origin resource sharing (CORS).</span></span>

1. <span data-ttu-id="c2122-192">Klicken Sie im Fenster der Funktions-App auf der linken Navigationsleiste auf den Namen Ihrer Funktions-App.</span><span class="sxs-lookup"><span data-stu-id="c2122-192">In the left navigation of the Function Apps window, click on the name of your function app.</span></span>

1. <span data-ttu-id="c2122-193">Klicken Sie auf **Plattformfeatures**, um eine Liste mit erweiterten Features anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c2122-193">Click on **Platform features** to view a list of advanced features.</span></span>

1. <span data-ttu-id="c2122-194">Klicken Sie unter **API** auf **CORS**.</span><span class="sxs-lookup"><span data-stu-id="c2122-194">Under **API**, click **CORS**.</span></span>

    ![Auswählen von CORS](../media/2-open-cors.jpg)

1. <span data-ttu-id="c2122-196">Fügen Sie einen zulässigen Ursprung für die URL Ihrer Website hinzu, die Sie in der vorherigen Einheit erstellt haben, und lassen Sie den nachfolgenden Schrägstrich (/) weg.</span><span class="sxs-lookup"><span data-stu-id="c2122-196">Add an allow origin for the URL of your web site you created in the previous unit and omit the trailing slash (/).</span></span> <span data-ttu-id="c2122-197">Beispiel: `https://firstserverlessweb.z4.web.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="c2122-197">For example: `https://firstserverlessweb.z4.web.core.windows.net`.</span></span>

    ![CORS-Einstellungen mit hinzugefügter URL für serverlose Web-App](../media/2-add-cors.png)

1. <span data-ttu-id="c2122-199">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c2122-199">Click **Save**.</span></span>

<span data-ttu-id="c2122-200">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="c2122-200">::: zone pivot="javascript"</span></span>

6. <span data-ttu-id="c2122-201">Navigieren Sie noch immer im Azure-Portal zum Fenster „Funktions-App“, und klicken Sie auf den Namen Ihrer Funktions-App.</span><span class="sxs-lookup"><span data-stu-id="c2122-201">Still in the Azure portal, navigate to the Function Apps window and click on the name of your function app.</span></span> <span data-ttu-id="c2122-202">Klicken Sie auf die Registerkarte **Übersicht**. Klicken Sie auf **Neu starten**, um sicherzustellen, dass die Änderungen für CORS wirksam werden.</span><span class="sxs-lookup"><span data-stu-id="c2122-202">Select the **Overview** tab. Click **Restart** to make sure that the changes for CORS take effect.</span></span>

<span data-ttu-id="c2122-203">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="c2122-203">::: zone-end</span></span>

<span data-ttu-id="c2122-204">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="c2122-204">::: zone pivot="csharp"</span></span>

6. <span data-ttu-id="c2122-205">Navigieren Sie zurück zur Funktion `GetUploadUrl`, und wählen Sie die Registerkarte **Integrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="c2122-205">Navigate back to the `GetUploadUrl` function and select the **Integrate** tab.</span></span>

1. <span data-ttu-id="c2122-206">Wählen Sie unter **Ausgewählte HTTP-Methoden** die Option **OPTIONS** aus.</span><span class="sxs-lookup"><span data-stu-id="c2122-206">Under **Selected HTTP methods**, select **OPTIONS**.</span></span>

    <span data-ttu-id="c2122-207">**GET**, **POST** und **OPTIONS** sollten jeweils ausgewählt sein.</span><span class="sxs-lookup"><span data-stu-id="c2122-207">**GET**, **POST**, and **OPTIONS** should all be selected.</span></span> <span data-ttu-id="c2122-208">Für CORS wird die **OPTIONS**-Methode verwendet, die für C#-Funktionen nicht standardmäßig ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="c2122-208">CORS uses the **OPTIONS** method, which isn't selected by default for C# functions.</span></span>  

1. <span data-ttu-id="c2122-209">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c2122-209">Click **Save**.</span></span>

1. <span data-ttu-id="c2122-210">Navigieren Sie noch immer im Azure-Portal zum Fenster „Funktions-App“, und klicken Sie auf den Namen Ihrer Funktions-App.</span><span class="sxs-lookup"><span data-stu-id="c2122-210">Still in the Azure portal, navigate to the Function Apps window and click on the name of your function app.</span></span> <span data-ttu-id="c2122-211">Klicken Sie auf die Registerkarte **Übersicht**. Klicken Sie auf **Neu starten**, um sicherzustellen, dass die Änderungen für CORS wirksam werden.</span><span class="sxs-lookup"><span data-stu-id="c2122-211">Select the **Overview** tab. Click **Restart** to make sure that the changes for CORS take effect.</span></span>

<span data-ttu-id="c2122-212">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="c2122-212">::: zone-end</span></span>

## <a name="configure-cors-in-the-storage-account"></a><span data-ttu-id="c2122-213">Konfigurieren von CORS im Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="c2122-213">Configure CORS in the Storage account</span></span>

<span data-ttu-id="c2122-214">Da die Funktions-App auch clientseitige JavaScript-Aufrufe zum Hochladen von Dateien an Blob Storage richtet, müssen Sie das Speicherkonto für CORS konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="c2122-214">Because the function app also makes client-side JavaScript calls to Blob storage to upload files, you have to configure the Storage account for CORS.</span></span>

- <span data-ttu-id="c2122-215">Führen Sie den folgenden Befehl aus, um für alle Ursprungsorte das Hochladen in das Speicherkonto zuzulassen:</span><span class="sxs-lookup"><span data-stu-id="c2122-215">Run the following command to allow all origins to upload files to the Storage account:</span></span>

    ```azurecli
    az storage cors add --methods OPTIONS PUT --origins '*' --exposed-headers '*' --allowed-headers '*' --services b --account-name <storage account name>
    ```

## <a name="modify-the-web-app-to-upload-images"></a><span data-ttu-id="c2122-216">Ändern der Web-App zum Hochladen von Bildern</span><span class="sxs-lookup"><span data-stu-id="c2122-216">Modify the web app to upload images</span></span>

<span data-ttu-id="c2122-217">Die Web-App ruft Einstellungen aus einer Datei mit dem Namen **settings.js** ab.</span><span class="sxs-lookup"><span data-stu-id="c2122-217">The web app retrieves settings from a file named **settings.js**.</span></span> <span data-ttu-id="c2122-218">In den folgenden Schritten erstellen Sie die Datei mit Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="c2122-218">In the following steps, you create the file using Cloud Shell.</span></span> <span data-ttu-id="c2122-219">Sie legen `window.apiBaseUrl` auf die URL der Funktions-App und `window.blobBaseUrl` auf die URL des Azure Blob Storage-Endpunkts fest.</span><span class="sxs-lookup"><span data-stu-id="c2122-219">You set `window.apiBaseUrl` to the URL of the function app, and `window.blobBaseUrl` to the URL of the Azure Blob storage endpoint.</span></span>

1. <span data-ttu-id="c2122-220">Stellen Sie in Cloud Shell sicher, dass das aktuelle Verzeichnis der Ordner **www/dist** ist.</span><span class="sxs-lookup"><span data-stu-id="c2122-220">In Cloud Shell, ensure that the current directory is the **www/dist** folder.</span></span>

    ```bash
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. <span data-ttu-id="c2122-221">Öffnen Sie den Cloud Shell-Editor im aktuellen Verzeichnis durch Eingabe des Befehls `code .` samt Punkt.</span><span class="sxs-lookup"><span data-stu-id="c2122-221">Open the Cloud Shell Editor in the current directory by typing the command `code .`, including the dot.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="c2122-222">Fragen Sie im Fenster „Cloud Shell“ unter dem Editor die URL der Funktions-App ab.</span><span class="sxs-lookup"><span data-stu-id="c2122-222">In the Cloud Shell window below the editor, query the function app's URL.</span></span>

    ```azurecli
    echo "https://"$(az functionapp show -n <function app name> -g <rgn>[Sandbox resource group name]</rgn> --query "defaultHostName" --output tsv)
    ```

1. <span data-ttu-id="c2122-223">Fügen Sie unter Verwendung der App-URL, die Sie im vorherigen Schritt abgerufen haben, die folgende Zeile in das Editorfenster ein.</span><span class="sxs-lookup"><span data-stu-id="c2122-223">Add the following line into the editor window, using the function app URL you retrieved in the previous step.</span></span>

    ```bash
    window.apiBaseUrl = '<function app url>'
    ```

1. <span data-ttu-id="c2122-224">Fragen Sie im Fenster „Cloud Shell“ unter dem Editor die URL des Azure Blob Storage-Endpunkts ab.</span><span class="sxs-lookup"><span data-stu-id="c2122-224">In the Cloud Shell window below the editor, query the Azure Blob Storage endpoint URL.</span></span>

    ```azurecli
    echo $(az storage account show -n <storage account name> -g <rgn>[Sandbox resource group name]</rgn> --query primaryEndpoints.blob -o tsv | sed 's/\/$//')
    ```

1. <span data-ttu-id="c2122-225">Fügen Sie eine zweite Zeile in das Editorfenster ein, indem Sie die URL des Storage-Endpunkts verwenden, die Sie im vorherigen Schritt abgerufen haben.</span><span class="sxs-lookup"><span data-stu-id="c2122-225">Append a second line into the editor window, using the Storage endpoint URL you retrieved in the previous step.</span></span>

    ```bash
    window.blobBaseUrl = '<blob storage endpoint url>'
    ```

1. <span data-ttu-id="c2122-226">Speichern Sie die Datei **settings.js**, und schließen Sie den Editor.</span><span class="sxs-lookup"><span data-stu-id="c2122-226">Save the file as **settings.js** and close the editor.</span></span>

1. <span data-ttu-id="c2122-227">Vergewissern Sie sich, dass das Schreiben der Datei erfolgreich war und dass sie jetzt zwei Zeilen enthält.</span><span class="sxs-lookup"><span data-stu-id="c2122-227">Confirm the file was successfully written and it now contains 2 lines.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="c2122-228">Laden Sie die Datei in Blobspeicher hoch.</span><span class="sxs-lookup"><span data-stu-id="c2122-228">Upload the file to Blob storage.</span></span>

    ```azurecli
    az storage blob upload \
        -c \$web \
        --account-name <storage account name> \
        -f settings.js \
        -n settings.js
    ```

## <a name="test-the-web-application"></a><span data-ttu-id="c2122-229">Testen der Webanwendung</span><span class="sxs-lookup"><span data-stu-id="c2122-229">Test the web application</span></span>

<span data-ttu-id="c2122-230">An diesem Punkt kann die Galerieanwendung ein Bild in Blog Storage hochladen, aber sie kann noch keine Bilder anzeigen.</span><span class="sxs-lookup"><span data-stu-id="c2122-230">At this point, the gallery application is able to upload an image to Blob storage, but it can't display images yet.</span></span> <span data-ttu-id="c2122-231">Die Anwendung versucht, die Funktion `GetImages` aufzurufen. Diese ist aber noch nicht vorhanden, da Sie sie erst in einem späteren Modul erstellen.</span><span class="sxs-lookup"><span data-stu-id="c2122-231">It will try to call a `GetImages` function that doesn't exist yet because you create it in a later module.</span></span> <span data-ttu-id="c2122-232">Der Aufruf ist nicht erfolgreich, und scheinbar hängt die Webseite mit einem Hinweis der Art „Wird analysiert...“, aber der Upload des gewählten Bilds ist trotzdem erfolgreich.</span><span class="sxs-lookup"><span data-stu-id="c2122-232">The call will fail and the web page will appear to be stuck on "Analyzing...," but the image you select will be successfully uploaded.</span></span>

<span data-ttu-id="c2122-233">Sie können sich vergewissern, ob ein Bild erfolgreich hochgeladen wurde, indem Sie im Azure-Portal den Inhalt des Containers **images** überprüfen.</span><span class="sxs-lookup"><span data-stu-id="c2122-233">You can verify that an image is successfully uploaded by checking the contents of the **images** container in the Azure portal.</span></span>

1. <span data-ttu-id="c2122-234">Navigieren Sie in einem Browserfenster zur Anwendung.</span><span class="sxs-lookup"><span data-stu-id="c2122-234">In a browser window, browse to the application.</span></span> <span data-ttu-id="c2122-235">Wählen Sie eine Bilddatei aus, und laden Sie sie hoch.</span><span class="sxs-lookup"><span data-stu-id="c2122-235">Select an image file and upload it.</span></span> <span data-ttu-id="c2122-236">Der Upload wird abgeschlossen. Da wir aber noch nicht die Möglichkeit zum Anzeigen von Bildern hinzugefügt haben, wird das hochgeladene Bild von der App nicht angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c2122-236">The upload completes, but because we haven't added the ability to display images yet, the app doesn't show the uploaded photo.</span></span> <span data-ttu-id="c2122-237">(Die Webseite scheint beim Vorgang „Bild wird analysiert...“ zu hängen. Dies beheben Sie später.)</span><span class="sxs-lookup"><span data-stu-id="c2122-237">(The web page appears to be stuck on "Analyzing image..." You'll fix that later.)</span></span>

1. <span data-ttu-id="c2122-238">Vergewissern Sie sich in Cloud Shell, dass das Bild in den Container **images** hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="c2122-238">In Cloud Shell, confirm the image was uploaded to the **images** container.</span></span>

    ```azurecli
    az storage blob list \
        --account-name <storage account name> \
        -c images \
        -o table
    ```

1. <span data-ttu-id="c2122-239">Löschen Sie alle Dateien im Container **images**, bevor Sie mit der nächsten Einheit fortfahren.</span><span class="sxs-lookup"><span data-stu-id="c2122-239">Before moving on to the next unit, delete all files in the **images** container.</span></span>

    ```azurecli
    az storage blob delete-batch \
        -s images \
        --account-name <storage account name>
    ```

## <a name="summary"></a><span data-ttu-id="c2122-240">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c2122-240">Summary</span></span>

<span data-ttu-id="c2122-241">In dieser Einheit haben Sie eine Azure Functions-App erstellt und erfahren, wie Sie eine serverlose Funktion verwenden, um für eine Webanwendung das Hochladen von Bildern in Blob Storage zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="c2122-241">In this unit, you created an Azure Functions app and learned how to use a serverless function to allow a web application to upload images to Blob storage.</span></span> <span data-ttu-id="c2122-242">Als Nächstes erfahren Sie, wie Sie Miniaturansichten für die hochgeladenen Bilder erstellen, indem Sie eine per Blob ausgelöste serverlose Funktion verwenden.</span><span class="sxs-lookup"><span data-stu-id="c2122-242">Next, you will learn how to create thumbnails for the uploaded images using a blob-triggered serverless function.</span></span>