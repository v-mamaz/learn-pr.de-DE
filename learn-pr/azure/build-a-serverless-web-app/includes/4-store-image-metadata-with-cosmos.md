<span data-ttu-id="17cb4-101">Azure Cosmos DB ist die serverlose, Global verteilte, multimodell-Datenbank von Microsoft.</span><span class="sxs-lookup"><span data-stu-id="17cb4-101">Azure Cosmos DB is Microsoft's serverless, globally distributed, multi-model database.</span></span> <span data-ttu-id="17cb4-102">In diesem Modul erfahren Sie, wie Sie mithilfe von Azure Functions zum Speichern und Abrufen von Metadaten zu Bildern als JSON-Dokumente in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17cb4-102">In this module, you learn how to use Azure Functions to store and retrieve image metadata as JSON documents in Cosmos DB.</span></span>

## <a name="create-a-cosmos-db-account-database-and-collection"></a><span data-ttu-id="17cb4-103">Erstellen einer Cosmos DB-Konto, Datenbank und Sammlung</span><span class="sxs-lookup"><span data-stu-id="17cb4-103">Create a Cosmos DB account, database, and collection</span></span>

<span data-ttu-id="17cb4-104">Cosmos DB-Konto ist eine Azure-Ressource, die Cosmos DB-Datenbanken enthält.</span><span class="sxs-lookup"><span data-stu-id="17cb4-104">A Cosmos DB account is an Azure resource that contains Cosmos DB databases.</span></span>

1. <span data-ttu-id="17cb4-105">Stellen Sie sicher, dass Sie immer noch in der Cloud Shell angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="17cb4-105">Ensure you are still signed into the Cloud Shell.</span></span>  <span data-ttu-id="17cb4-106">Wählen Sie andernfalls **EINGABETASTE fokusmodus** um eine Cloud Shell-Fenster zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-106">If not, select **Enter focus mode** to open a Cloud Shell window.</span></span> 

1. <span data-ttu-id="17cb4-107">Erstellen Sie ein Cosmos DB-Konto mit einem eindeutigen Namen in der gleichen Ressourcengruppe wie die anderen Ressourcen in diesem Tutorial.</span><span class="sxs-lookup"><span data-stu-id="17cb4-107">Create a Cosmos DB account with a unique name in the same resource group as the other resources in this tutorial.</span></span>

    ```azurecli
    az cosmosdb create -g first-serverless-app -n <cosmos db account name>
    ```

1. <span data-ttu-id="17cb4-108">Nachdem das Cosmos DB-Konto erstellt wurde, erstellen Sie eine neue Datenbank namens **Imagesdb** im Konto.</span><span class="sxs-lookup"><span data-stu-id="17cb4-108">After the Cosmos DB account is created, create a new database named **imagesdb** in the account.</span></span>

    ```azurecli
    az cosmosdb database create -g first-serverless-app -n <cosmos db account name> --db-name imagesdb
    ```

1. <span data-ttu-id="17cb4-109">Nachdem die Datenbank erstellt wurde, erstellen Sie eine neue Sammlung mit dem Namen **Images** in der Datenbank mit einem Durchsatz von 400 anforderungseinheiten (RUs).</span><span class="sxs-lookup"><span data-stu-id="17cb4-109">After the database is created, create a new collection named **images** in the database with a throughput of 400 request units (RUs).</span></span>

    ```azurecli
    az cosmosdb collection create -g first-serverless-app -n <cosmos db account name> --db-name imagesdb --collection-name images --throughput 400
    ```


## <a name="save-a-document-to-cosmos-db-when-a-thumbnail-is-created"></a><span data-ttu-id="17cb4-110">Speichern eines Dokuments in Cosmos DB, wenn eine Miniaturansicht erstellt wird</span><span class="sxs-lookup"><span data-stu-id="17cb4-110">Save a document to Cosmos DB when a thumbnail is created</span></span>

<span data-ttu-id="17cb4-111">Die Cosmos DB-ausgabebindung ermöglicht erstellen Sie mit Dokumenten in einer Cosmos DB-Sammlung in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="17cb4-111">The Cosmos DB output binding lets you create documents in a Cosmos DB collection from Azure Functions.</span></span> <span data-ttu-id="17cb4-112">In den folgenden Schritten konfigurieren Sie eine Cosmos DB-ausgabebindung in der **ResizeImage** Funktion, und ändern Sie die Funktion zum Zurückgeben von einem Dokument (Objekt) gespeichert werden soll.</span><span class="sxs-lookup"><span data-stu-id="17cb4-112">In the following steps, you configure a Cosmos DB output binding in the **ResizeImage** function and modify the function to return a document (object) to be saved.</span></span>

1. <span data-ttu-id="17cb4-113">Öffnen Sie die Funktions-app im Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="17cb4-113">Open the function app in the Azure Portal.</span></span>

1. <span data-ttu-id="17cb4-114">Erweitern Sie im linken Navigationsbereich, der **ResizeImage** funktionieren, und wählen Sie dann **integrieren**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-114">In the left hand navigation, expand the **ResizeImage** function, and then select **Integrate**.</span></span>

1. <span data-ttu-id="17cb4-115">Klicken Sie unter **Ausgaben**, klicken Sie auf **neue Ausgabe**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-115">Under **Outputs**, click **New Output**.</span></span>

1. <span data-ttu-id="17cb4-116">Suchen der **Azure Cosmos DB** Element aus, und wählen Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="17cb4-116">Find the **Azure Cosmos DB** item and select it.</span></span> <span data-ttu-id="17cb4-117">Klicken Sie dann auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-117">Then click **Select**.</span></span>

    ![Wählen Sie die neue Ausgabe](../images/4-new-output.jpg)

1. <span data-ttu-id="17cb4-119">Füllen Sie die Felder unter **Azure Cosmos DB-Ausgabe** mit den folgenden Werten.</span><span class="sxs-lookup"><span data-stu-id="17cb4-119">Fill out the fields under **Azure Cosmos DB output** with the following values.</span></span>

    | <span data-ttu-id="17cb4-120">Einstellung</span><span class="sxs-lookup"><span data-stu-id="17cb4-120">Setting</span></span>      |  <span data-ttu-id="17cb4-121">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="17cb4-121">Suggested value</span></span>   | <span data-ttu-id="17cb4-122">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="17cb4-122">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="17cb4-123">**Dokumentparametername**</span><span class="sxs-lookup"><span data-stu-id="17cb4-123">**Document parameter name**</span></span> | <span data-ttu-id="17cb4-124">Wählen Sie **Funktionsrückgabewert verwenden**</span><span class="sxs-lookup"><span data-stu-id="17cb4-124">Select **Use function return value**</span></span> | <span data-ttu-id="17cb4-125">Der Wert des Textfelds wird automatisch festgelegt, um **$return**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-125">The value of the textbox is automatically set to **$return**.</span></span> |
    | <span data-ttu-id="17cb4-126">**Datenbankname**</span><span class="sxs-lookup"><span data-stu-id="17cb4-126">**Database name**</span></span> | <span data-ttu-id="17cb4-127">imagesdb</span><span class="sxs-lookup"><span data-stu-id="17cb4-127">imagesdb</span></span> | <span data-ttu-id="17cb4-128">Verwenden Sie den Namen der Datenbank, die Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="17cb4-128">Use the name of the database that you created.</span></span> |
    | <span data-ttu-id="17cb4-129">**Sammlungsname**</span><span class="sxs-lookup"><span data-stu-id="17cb4-129">**Collection name**</span></span> | <span data-ttu-id="17cb4-130">Images</span><span class="sxs-lookup"><span data-stu-id="17cb4-130">images</span></span> | <span data-ttu-id="17cb4-131">Verwenden Sie den Namen der Auflistung, die Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="17cb4-131">Use the name of the collection that you created.</span></span> |

1. <span data-ttu-id="17cb4-132">Neben **Azure Cosmos DB-Kontoverbindung**, klicken Sie auf **neue**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-132">Next to **Azure Cosmos DB account connection**, click **new**.</span></span> <span data-ttu-id="17cb4-133">Wählen Sie das Cosmos DB-Konto, die, das Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="17cb4-133">Select the Cosmos DB account you previously created.</span></span>

    ![Geben Sie Einstellungen für Azure Cosmos DB-ausgabebindung](../images/4-cosmos-db-output.png)

1. <span data-ttu-id="17cb4-135">Klicken Sie auf **speichern** zum Erstellen der Cosmos DB-ausgabebindung.</span><span class="sxs-lookup"><span data-stu-id="17cb4-135">Click **Save** to create the Cosmos DB output binding.</span></span>

1. <span data-ttu-id="17cb4-136">Klicken Sie auf die **ResizeImage** Funktionsnamen auf der linken Seite, um die Funktion zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-136">Click on the **ResizeImage** function name on the left to open the function.</span></span>

1. <span data-ttu-id="17cb4-137">**C#**</span><span class="sxs-lookup"><span data-stu-id="17cb4-137">**C#**</span></span>

    1. <span data-ttu-id="17cb4-138">(C#) Ändern des Rückgabetyps der Funktion von **"void"** zu **Objekt**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-138">(C#) Change the return type of the function from **void** to **object**.</span></span>

    1. <span data-ttu-id="17cb4-139">(C#) Am Ende der Funktion fügen Sie den folgenden Codeblock, um das zu speichernde Dokument zurückzugeben:</span><span class="sxs-lookup"><span data-stu-id="17cb4-139">(C#) At the end of the function, add the following code block to return the document to be saved:</span></span>
    
        ```csharp
        return new {
            id = name,
            imgPath = "/images/" + name,
            thumbnailPath = "/thumbnails/" + name
        };
        ```
    
        !["Run.csx" für ResizeImages-Funktion nach Änderungen](../images/4-update-function.png)

1. <span data-ttu-id="17cb4-141">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="17cb4-141">**JavaScript**</span></span>

    1. <span data-ttu-id="17cb4-142">(JavaScript) Ändern der `context.done()` -Anweisung in der `else` Klausel zur Rückgabe des Dokuments in Cosmos DB gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="17cb4-142">(JavaScript) Change the `context.done()` statement in the `else` clause to return the document to be saved to Cosmos DB.</span></span>

    ```javascript
    if (error) {
        context.done(error);
    } else {
        context.bindings.thumbnail = stream;
        context.done(null, {
            id: context.bindingData.name,
            imgPath: "/images/" + context.bindingData.name,
            thumbnailPath: "/thumbnails/" + context.bindingData.name
        });
    }
    ```

1. <span data-ttu-id="17cb4-143">Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="17cb4-143">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="17cb4-144">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-144">Click **Save**.</span></span> <span data-ttu-id="17cb4-145">Überprüfen Sie im Bereich Protokolle, um sicherzustellen, dass die Funktion wurde erfolgreich gespeichert. keine Fehler vorliegen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-145">Check the logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="create-a-function-to-list-images-from-cosmos-db"></a><span data-ttu-id="17cb4-146">Erstellen Sie eine Funktion zum Auflisten von Images aus Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="17cb4-146">Create a function to list images from Cosmos DB</span></span>

<span data-ttu-id="17cb4-147">Die Webanwendung benötigt eine API zum Abrufen von Metadaten zu Bildern von Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17cb4-147">The web application requires an API to retrieve image metadata from Cosmos DB.</span></span> <span data-ttu-id="17cb4-148">In den folgenden Schritten.</span><span class="sxs-lookup"><span data-stu-id="17cb4-148">In the following steps.</span></span> <span data-ttu-id="17cb4-149">So erstellen Sie eine per HTTP ausgelöste-Funktion, die eine Cosmos DB-eingabebindung verwendet wird, um die datenbankauflistung abzufragen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-149">uou create an HTTP triggered function that uses a Cosmos DB input binding to query the database collection.</span></span>

1. <span data-ttu-id="17cb4-150">Zeigen Sie Sie in Ihrer Funktionen-app auf **Funktionen** auf der linken Seite und auf **+** zum Erstellen einer neuen Funktion.</span><span class="sxs-lookup"><span data-stu-id="17cb4-150">In your function app, hover over **Functions** on the left and click **+** to create a new function.</span></span>

1. <span data-ttu-id="17cb4-151">Suchen der **"httptrigger"** Vorlage, und wählen Sie ihn.</span><span class="sxs-lookup"><span data-stu-id="17cb4-151">Find the **HttpTrigger** template and select it.</span></span>

1. <span data-ttu-id="17cb4-152">Verwenden Sie diese Werte zum Erstellen einer Funktion, die eine Get-Images-URL generiert.</span><span class="sxs-lookup"><span data-stu-id="17cb4-152">Use these values to create a function that generates a get images URL.</span></span>

    | <span data-ttu-id="17cb4-153">Einstellung</span><span class="sxs-lookup"><span data-stu-id="17cb4-153">Setting</span></span>      |  <span data-ttu-id="17cb4-154">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="17cb4-154">Suggested value</span></span>   | <span data-ttu-id="17cb4-155">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="17cb4-155">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="17cb4-156">**Name Ihrer Funktion**</span><span class="sxs-lookup"><span data-stu-id="17cb4-156">**Name your function**</span></span> | <span data-ttu-id="17cb4-157">GetImages</span><span class="sxs-lookup"><span data-stu-id="17cb4-157">GetImages</span></span> | <span data-ttu-id="17cb4-158">Geben Sie diesen Namen genau wie angezeigt, damit die Anwendung die Funktion ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="17cb4-158">Type this name exactly as shown so the application can discover the function.</span></span> |
    | <span data-ttu-id="17cb4-159">**Autorisierungsstufe**</span><span class="sxs-lookup"><span data-stu-id="17cb4-159">**Authorization level**</span></span> | <span data-ttu-id="17cb4-160">Anonym</span><span class="sxs-lookup"><span data-stu-id="17cb4-160">Anonymous</span></span> | <span data-ttu-id="17cb4-161">Ermöglichen Sie die Funktion, die öffentlich zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="17cb4-161">Allow the function to be accessed publicly.</span></span> |

1. <span data-ttu-id="17cb4-162">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-162">Click **Create**.</span></span>

1. <span data-ttu-id="17cb4-163">Wenn die neue Funktion erstellt wird, klicken Sie auf **integrieren** unter dem Funktionsnamen im linken Navigationsbereich.</span><span class="sxs-lookup"><span data-stu-id="17cb4-163">When the new function is created, click **Integrate** under the function's name on the left navigation.</span></span>

1. <span data-ttu-id="17cb4-164">Klicken Sie auf **neue Eingabe** , und wählen Sie **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-164">Click **New Input** and select **Azure Cosmos DB**.</span></span> 

    ![Wählen Sie die neue Eingabe](../images/4-new-input.jpg)

1. <span data-ttu-id="17cb4-166">Klicken Sie auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-166">Click **Select**.</span></span>

1. <span data-ttu-id="17cb4-167">Füllen Sie die folgenden Werte:</span><span class="sxs-lookup"><span data-stu-id="17cb4-167">Fill out the following values:</span></span>

    | <span data-ttu-id="17cb4-168">Einstellung</span><span class="sxs-lookup"><span data-stu-id="17cb4-168">Setting</span></span>      |  <span data-ttu-id="17cb4-169">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="17cb4-169">Suggested value</span></span>   | <span data-ttu-id="17cb4-170">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="17cb4-170">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="17cb4-171">**Dokumentparametername**</span><span class="sxs-lookup"><span data-stu-id="17cb4-171">**Document parameter name**</span></span> | <span data-ttu-id="17cb4-172">Dokumente</span><span class="sxs-lookup"><span data-stu-id="17cb4-172">documents</span></span> | <span data-ttu-id="17cb4-173">Übereinstimmungen von Parameternamen in der Funktion.</span><span class="sxs-lookup"><span data-stu-id="17cb4-173">Matches parameter name in the function.</span></span> |
    | <span data-ttu-id="17cb4-174">**Datenbankname**</span><span class="sxs-lookup"><span data-stu-id="17cb4-174">**Database name**</span></span> | <span data-ttu-id="17cb4-175">imagesdb</span><span class="sxs-lookup"><span data-stu-id="17cb4-175">imagesdb</span></span> |  |
    | <span data-ttu-id="17cb4-176">**Sammlungsname**</span><span class="sxs-lookup"><span data-stu-id="17cb4-176">**Collection name**</span></span> | <span data-ttu-id="17cb4-177">Images</span><span class="sxs-lookup"><span data-stu-id="17cb4-177">images</span></span> |  |
    | <span data-ttu-id="17cb4-178">**SQL query**</span><span class="sxs-lookup"><span data-stu-id="17cb4-178">**SQL query**</span></span> | <span data-ttu-id="17cb4-179">Wählen Sie \* from c sortiert nach c. _ts Desc</span><span class="sxs-lookup"><span data-stu-id="17cb4-179">select \* from c order by c._ts desc</span></span> | <span data-ttu-id="17cb4-180">Dokumente, die neuesten Dokumente erste abrufen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-180">Get documents, latest documents first.</span></span> |
    | <span data-ttu-id="17cb4-181">**Azure Cosmos DB-Kontoverbindung**</span><span class="sxs-lookup"><span data-stu-id="17cb4-181">**Azure Cosmos DB account connection**</span></span> | <span data-ttu-id="17cb4-182">Wählen Sie die vorhandene Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="17cb4-182">Select existing connection string</span></span> |  |

1. <span data-ttu-id="17cb4-183">Klicken Sie auf **speichern** die eingabebindung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-183">Click **Save** to create the input binding.</span></span>

1. <span data-ttu-id="17cb4-184">**C#**</span><span class="sxs-lookup"><span data-stu-id="17cb4-184">**C#**</span></span>

    1. <span data-ttu-id="17cb4-185">Klicken Sie auf den Namen der Funktion im Code-Fenster zu öffnen, und Ersetzen Sie alle **"Run.csx"** mit dem Inhalt [ **/csharp/GetImages/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetImages/run.csx).</span><span class="sxs-lookup"><span data-stu-id="17cb4-185">Click the function's name to open the code window, and then replace all of **run.csx** with the content in [**/csharp/GetImages/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetImages/run.csx).</span></span>

1. <span data-ttu-id="17cb4-186">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="17cb4-186">**JavaScript**</span></span>

    1. <span data-ttu-id="17cb4-187">Klicken Sie auf den Namen der Funktion im Code-Fenster zu öffnen, und Ersetzen Sie alle **"Index.js"** mit dem Inhalt [ **/javascript/GetImages/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetImages/index.js).</span><span class="sxs-lookup"><span data-stu-id="17cb4-187">Click the function's name to open the code window, and then replace all of **index.js** with the content in [**/javascript/GetImages/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetImages/index.js).</span></span>

1. <span data-ttu-id="17cb4-188">Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="17cb4-188">Click **Logs** below the code window to expand the logs panel.</span></span>

1. <span data-ttu-id="17cb4-189">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="17cb4-189">Click **Save**.</span></span> <span data-ttu-id="17cb4-190">Überprüfen Sie im Bereich Protokolle, um sicherzustellen, dass die Funktion wurde erfolgreich gespeichert. keine Fehler vorliegen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-190">Check the logs panel to ensure the function is successfully saved and there are no errors.</span></span>


## <a name="test-the-application"></a><span data-ttu-id="17cb4-191">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="17cb4-191">Test the application</span></span>

1. <span data-ttu-id="17cb4-192">Öffnen Sie die Anwendung in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="17cb4-192">Open the application in a browser.</span></span> <span data-ttu-id="17cb4-193">Wählen Sie eine Bilddatei, und Laden Sie es hoch.</span><span class="sxs-lookup"><span data-stu-id="17cb4-193">Select an image file and upload it.</span></span>

1. <span data-ttu-id="17cb4-194">Nach wenigen Sekunden wird die Miniaturansicht des neuen Images auf der Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="17cb4-194">After a few seconds, the thumbnail of the new image appears on the page.</span></span>

1. <span data-ttu-id="17cb4-195">Verwenden Sie das Suchfeld im Azure-Portal für Ihr Cosmos DB-Konto nach Namen suchen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-195">In the Azure portal, use the Search box to search for your Cosmos DB account by name.</span></span> <span data-ttu-id="17cb4-196">Klicken Sie auf, um es zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-196">Click it to open it.</span></span>

1. <span data-ttu-id="17cb4-197">Klicken Sie auf **Daten-Explorer** auf der linken Seite zum Durchsuchen von Sammlungen und Dokumente.</span><span class="sxs-lookup"><span data-stu-id="17cb4-197">Click **Data Explorer** on the left to browse collections and documents.</span></span>

1. <span data-ttu-id="17cb4-198">Unter den **Imagesdb** Datenbank, wählen die **Images** Auflistung.</span><span class="sxs-lookup"><span data-stu-id="17cb4-198">Under the **imagesdb** database, select the **images** collection.</span></span>

1. <span data-ttu-id="17cb4-199">Vergewissern Sie sich, dass ein Dokument für das hochgeladene Bild erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="17cb4-199">Confirm that a document was created for the uploaded image.</span></span>

    ![Daten-Explorer mit der ein Dokument für eines hochgeladenen Bilds](../images/4-data-explorer.png)



## <a name="summary"></a><span data-ttu-id="17cb4-201">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="17cb4-201">Summary</span></span>

<span data-ttu-id="17cb4-202">In dieser Einheit haben Sie gelernt, wie Sie eine Cosmos DB-Konto, Datenbank und einer Sammlung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="17cb4-202">In this unit, you learned how to create a Cosmos DB account, database, and collection.</span></span> <span data-ttu-id="17cb4-203">Sie haben zudem so verwenden Sie die Cosmos DB-Bindungen zum Speichern und Abrufen von Metadaten zu Bildern in Cosmos DB-Sammlung.</span><span class="sxs-lookup"><span data-stu-id="17cb4-203">You also learned how to use the Cosmos DB bindings to save and retrieve image metadata in the Cosmos DB collection.</span></span> <span data-ttu-id="17cb4-204">Als Nächstes erfahren Sie, wie Sie eine Beschriftung für jedes hochgeladene Bild mithilfe von Microsoft Cognitive Services automatisch zu generieren.</span><span class="sxs-lookup"><span data-stu-id="17cb4-204">Next, you learn how to automatically generate a caption for each uploaded image using Microsoft Cognitive Services.</span></span>