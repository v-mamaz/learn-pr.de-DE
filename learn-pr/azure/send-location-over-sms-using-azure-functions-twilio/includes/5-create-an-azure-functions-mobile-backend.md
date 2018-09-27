<span data-ttu-id="baad2-101">An diesem Punkt ruft die App den Benutzerstandort ab und ist bereit, an eine Azure-Funktion gesendet zu werden.</span><span class="sxs-lookup"><span data-stu-id="baad2-101">At this point, the app is working to get the user's location and is ready to be sent to an Azure function.</span></span> <span data-ttu-id="baad2-102">In dieser Einheit erstellen Sie die Azure-Funktion.</span><span class="sxs-lookup"><span data-stu-id="baad2-102">In this unit, you build the Azure function.</span></span>

## <a name="create-an-azure-functions-project"></a><span data-ttu-id="baad2-103">Erstellen eines Azure Functions-Projekts</span><span class="sxs-lookup"><span data-stu-id="baad2-103">Create an Azure Functions project</span></span>

1. <span data-ttu-id="baad2-104">Fügen Sie der Projektmappe `ImHere` ein neues Projekt hinzu, indem Sie mit der rechten Maustaste auf die Projektmappe klicken und *Hinzufügen > Neues Projekt* auswählen.</span><span class="sxs-lookup"><span data-stu-id="baad2-104">Add a new project to the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

1. <span data-ttu-id="baad2-105">Wählen Sie in der Struktur links *Visual C# > Cloud* aus, und klicken Sie dann im Arbeitsbereich in der Mitte auf *Azure Functions*.</span><span class="sxs-lookup"><span data-stu-id="baad2-105">From the tree on the left-hand side, select *Visual C#->Cloud*, and then select *Azure Functions* from the panel in the center.</span></span>

1. <span data-ttu-id="baad2-106">Geben Sie dem Projekt den Namen „ImHere.Functions“, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="baad2-106">Name the project "ImHere.Functions", and then click **OK**.</span></span>

    ![Dialogfeld „Neues Projekt hinzufügen“](../media/5-add-new-functions-project.png)

1. <span data-ttu-id="baad2-108">Das Konfigurationsdialogfeld **Neues Projekt** wird angezeigt, und es ist möglicherweise unten links ein Wartekreisel zu sehen, während aktualisierte Vorlagen geladen werden.</span><span class="sxs-lookup"><span data-stu-id="baad2-108">The **New Project** configuration dialog will appear, and it may show a spinner in the bottom-left whilst loading updated templates.</span></span> <span data-ttu-id="baad2-109">Solange dieser angezeigt wird, warten Sie, bis der Ladevorgang beendet ist. Wenn dann aktualisierte Vorlagen verfügbar sind, klicken Sie auf die angezeigte Option **Aktualisieren**, um sicherzustellen, dass Sie die neuesten Funktionsvorlagen erhalten.</span><span class="sxs-lookup"><span data-stu-id="baad2-109">If you see this, wait until this has finished loading, then if updated templates are available, click the **Refresh** option that will appear to ensure you get the latest Function templates.</span></span>

    ![Ladevorgang der neuesten Vorlagen im Dialogfeld „Neues Projekt“](../media/5-loading-templates.png)

1. <span data-ttu-id="baad2-111">Stellen Sie sicher, dass im Konfigurationsdialogfeld **Neues Projekt** die Functions-Version *Azure Functions v2 (.NET Standard)* (**nicht** _v1 (.NET Framework)_) ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="baad2-111">In the **New Project** configuration dialog, ensure the Functions version is set to *Azure Functions v2 (.NET Standard)* (**NOT** _v1 (.NET Framework)_).</span></span> <span data-ttu-id="baad2-112">Wählen Sie *HTTP-Trigger* aus, behalten Sie für das Speicherkonto die Einstellung *Speicheremulator* bei, und legen Sie die Zugriffsrechte auf *Anonym* fest.</span><span class="sxs-lookup"><span data-stu-id="baad2-112">Select *Http Trigger*, leave the storage account set to *Storage Emulator*, and set the access rights to *Anonymous*.</span></span> <span data-ttu-id="baad2-113">Klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="baad2-113">Then click **OK**.</span></span>

    ![Dialogfeld zur Azure Functions-Projektkonfiguration](../media/5-configure-trigger.png)

    <span data-ttu-id="baad2-115">Das neue Projekt wird erstellt und enthält die Standardfunktion `Function1`.</span><span class="sxs-lookup"><span data-stu-id="baad2-115">The new project will be created and have a default function called `Function1`.</span></span>

> [!NOTE]
> <span data-ttu-id="baad2-116">Diese Funktion wurde mit anonymem Zugriff erstellt.</span><span class="sxs-lookup"><span data-stu-id="baad2-116">This function was created with anonymous access.</span></span> <span data-ttu-id="baad2-117">Nach der Veröffentlichung in Azure kann diese Funktion von jedem Benutzer aufgerufen werden, der die zugehörige URL kennt.</span><span class="sxs-lookup"><span data-stu-id="baad2-117">Once published to Azure, anybody who knows the URL will be able to call this function.</span></span> <span data-ttu-id="baad2-118">In der Praxis würden Sie die Funktion über eine Authentifizierung schützen, beispielsweise über die [Azure App Service-Authentifizierung](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview?azure-portal=true) oder über [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="baad2-118">In a real-world scenario, you would protect this with some form of authentication, such as [Azure App Service authentication](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview?azure-portal=true) or [Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c?azure-portal=true).</span></span>

## <a name="create-the-function"></a><span data-ttu-id="baad2-119">Erstellen der Funktion</span><span class="sxs-lookup"><span data-stu-id="baad2-119">Create the function</span></span>

<span data-ttu-id="baad2-120">Das Azure Functions-Projekt wird mit einer einzigen HTTP-Triggerfunktion namens `Function1` erstellt.</span><span class="sxs-lookup"><span data-stu-id="baad2-120">The Azure Functions project is created with a single HTTP trigger function called `Function1`.</span></span> <span data-ttu-id="baad2-121">HTTP-Trigger ermöglichen es Ihnen, Ihre Funktionen über HTTP-Anforderungen aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="baad2-121">HTTP triggers allow you to invoke your functions using HTTP requests.</span></span> <span data-ttu-id="baad2-122">Die Funktion selbst wird als statische `Run`-Methode in der Klasse `Function1` implementiert.</span><span class="sxs-lookup"><span data-stu-id="baad2-122">The function itself is implemented as a static `Run` method in the `Function1` class.</span></span>

1. <span data-ttu-id="baad2-123">Benennen Sie die Datei im Projektmappen-Explorer von „Function1.cs“ in „SendLocation.cs“ um.</span><span class="sxs-lookup"><span data-stu-id="baad2-123">Rename the file in Solution Explorer from "Function1.cs" to "SendLocation.cs".</span></span> <span data-ttu-id="baad2-124">Klicken Sie auf `Function1`Ja **, wenn Sie zur Umbenennung aller Verweise auf das Codeelement**  aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="baad2-124">When prompted to rename all references to the code element `Function1`, click **Yes**.</span></span>

1. <span data-ttu-id="baad2-125">Benennen Sie den Funktionsnamen im Attribut in „SendLocation“ um.</span><span class="sxs-lookup"><span data-stu-id="baad2-125">Rename the function name in the attribute to "SendLocation".</span></span>

    ```cs
    [FunctionName("SendLocation")]
    ```

1. <span data-ttu-id="baad2-126">Löschen Sie den Inhalt der Funktion bis auf die erste Zeile, mit der eine Informationsmeldung an die Protokollierung ausgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="baad2-126">Delete the contents of the function, except the first line that writes an information message to the logger.</span></span>

    ```cs
    public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                             "get", "post",
                                                             Route = null)]HttpRequestMessage req,
                                                ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");
    }
    ```

## <a name="create-a-class-to-share-data-between-the-mobile-app-and-function"></a><span data-ttu-id="baad2-127">Erstellen einer Klasse zur Freigabe von Daten zwischen der mobilen App und der Funktion</span><span class="sxs-lookup"><span data-stu-id="baad2-127">Create a class to share data between the mobile app and function</span></span>

<span data-ttu-id="baad2-128">Wenn Daten an die Azure-Funktion gesendet werden, werden Sie als JSON gesendet.</span><span class="sxs-lookup"><span data-stu-id="baad2-128">When data is sent to the Azure function, it will be sent as JSON.</span></span> <span data-ttu-id="baad2-129">Die mobile App serialisiert die Daten in JSON, und die Funktion führt eine Deserialisierung aus JSON durch.</span><span class="sxs-lookup"><span data-stu-id="baad2-129">The mobile app will serialize data into JSON and the function will deserialize from JSON.</span></span> <span data-ttu-id="baad2-130">Um für konsistente Daten zwischen der mobilen App und der Funktion zu sorgen, erstellen Sie ein neues Projekt, das eine Klasse zum Speichern der Daten zu Standort und Telefonnummern enthält.</span><span class="sxs-lookup"><span data-stu-id="baad2-130">To keep this data consistent between the mobile app and the function, create a new project that contains a class to hold the location and phone number data.</span></span> <span data-ttu-id="baad2-131">Anschließend wird durch die App und die Funktion auf dieses Projekt verwiesen.</span><span class="sxs-lookup"><span data-stu-id="baad2-131">This project will then be referenced by the app and function.</span></span>

1. <span data-ttu-id="baad2-132">Erstellen Sie ein neues Projekt unterhalb der Projektmappe `ImHere`, indem Sie mit der rechten Maustaste auf die Projektmappe klicken und *Hinzufügen > Neues Projekt* auswählen.</span><span class="sxs-lookup"><span data-stu-id="baad2-132">Create a new project under the `ImHere` solution by right-clicking on the solution and selecting *Add->New Project...*.</span></span>

1. <span data-ttu-id="baad2-133">Wählen Sie in der Struktur links *Visual C# > .NET Standard* aus, und klicken Sie dann im Arbeitsbereich in der Mitte auf *Klassenbibliothek (.NET Standard)*.</span><span class="sxs-lookup"><span data-stu-id="baad2-133">From the tree on the left-hand side, select *Visual C#->.NET Standard*, and then select *Class Library (.NET Standard)* from the panel in the center.</span></span>

1. <span data-ttu-id="baad2-134">Geben Sie dem Projekt den Namen „ImHere.Data“, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="baad2-134">Name the project "ImHere.Data", and then click **OK**.</span></span>

    ![Dialogfeld „Neues Projekt hinzufügen“](../media/5-add-new-net-standard-project.png)

1. <span data-ttu-id="baad2-136">Löschen Sie die automatisch generierte Datei „Class1.cs“.</span><span class="sxs-lookup"><span data-stu-id="baad2-136">Delete the auto-generated "Class1.cs" file.</span></span>

1. <span data-ttu-id="baad2-137">Erstellen Sie eine neue Klasse im `ImHere.Data`-Projekt namens `PostData`, indem Sie mit der rechten Maustaste auf das Projekt und anschließend auf *Hinzufügen > Klasse* klicken. Geben Sie der neuen Klasse den Namen „PostData“, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="baad2-137">Create a new class in the `ImHere.Data` project called `PostData` by right-clicking on the project and then selecting *Add->Class...*. Name the new class "PostData" and click **OK**.</span></span> <span data-ttu-id="baad2-138">Markieren Sie diese neue Klasse als `public`.</span><span class="sxs-lookup"><span data-stu-id="baad2-138">Mark this new class as `public`.</span></span>

1. <span data-ttu-id="baad2-139">Fügen Sie `double`-Eigenschaften für Längen- und Breitengrad sowie eine `string[]`-Eigenschaft für die Telefonnummern hinzu, die als Sendeziel verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="baad2-139">Add `double` properties for the latitude and longitude, as well as a `string[]` property for the phone numbers to send to.</span></span>

    ```cs
    public class PostData
    {
        public double Latitude { get; set; }
        public double Longitude { get; set; }
        public string[] ToNumbers { get; set; }
    }
    ```

1. <span data-ttu-id="baad2-140">Fügen Sie den Projekten `ImHere.Functions` und `ImHere` einen Verweis auf dieses Projekt hinzu, indem Sie mit der rechten Maustaste auf das Projekt und anschließend auf *Hinzufügen > Verweis* klicken. Wählen Sie in der Struktur links *Projekte* aus, und aktivieren Sie dann das Feld neben *ImHere.Data*.</span><span class="sxs-lookup"><span data-stu-id="baad2-140">Add a reference to this project to both the `ImHere.Functions` and `ImHere` projects by right-clicking on the project and then selecting *Add->Reference...*. Select *Projects* from the tree on the left-hand side, and then check the box next to *ImHere.Data*.</span></span>

    ![Konfigurieren von Projektverweisen](../media/5-configure-project-references.png)

## <a name="read-the-data-sent-to-the-function"></a><span data-ttu-id="baad2-142">Lesen der an die Funktion gesendeten Daten</span><span class="sxs-lookup"><span data-stu-id="baad2-142">Read the data sent to the function</span></span>

<span data-ttu-id="baad2-143">In der Azure-Funktion enthält der `req`-Parameter die gesendete HTTP-Anforderung, und die Daten in dieser Anforderung sind ein als JSON serialisiertes `PostData`-Objekt.</span><span class="sxs-lookup"><span data-stu-id="baad2-143">In the Azure function, the `req` parameter contains the HTTP request that was made and the data inside this request will be a JSON serialized `PostData` object.</span></span>

1. <span data-ttu-id="baad2-144">Öffnen Sie die Klasse `SendLocation` im `ImHere.Functions`-Projekt.</span><span class="sxs-lookup"><span data-stu-id="baad2-144">Open the `SendLocation` class in the `ImHere.Functions` project.</span></span>

1. <span data-ttu-id="baad2-145">Lesen Sie den Inhalt der HTTP-Anforderung in eine Zeichenfolge aus, deserialisieren Sie diese in ein `PostData`-Objekt, und fügen Sie eine using-Direktive für den `ImHere.Data`-Namespace hinzu.</span><span class="sxs-lookup"><span data-stu-id="baad2-145">Read the contents of the HTTP request into a string, then deserialize it into a `PostData` object, adding a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
    ```

1. <span data-ttu-id="baad2-146">Erstellen Sie unter Verwendung des Längen- und Breitengrads aus `PostData` eine Google Maps-URL.</span><span class="sxs-lookup"><span data-stu-id="baad2-146">Construct a Google Maps URL using the latitude and longitude from the `PostData`.</span></span>

   ```cs
   string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
   ```

1. <span data-ttu-id="baad2-147">Protokollieren Sie die URL.</span><span class="sxs-lookup"><span data-stu-id="baad2-147">Log the URL.</span></span>

    ```cs
    log.LogInformation($"URL created - {url}");
    ```

1. <span data-ttu-id="baad2-148">Geben Sie einen Statuscode 200 zurück, um anzuzeigen, dass die Funktion fehlerfrei ausgeführt wurde.</span><span class="sxs-lookup"><span data-stu-id="baad2-148">Return a 200 status code to show the function completed without error.</span></span>

    ```cs
    return new OkResult();
    ```

<span data-ttu-id="baad2-149">Die vollständige Funktion wird unten gezeigt.</span><span class="sxs-lookup"><span data-stu-id="baad2-149">The complete function is shown below.</span></span>

```cs
[FunctionName("SendLocation")]
public static async Task<IActionResult> Run([HttpTrigger(AuthorizationLevel.Anonymous,
                                                                "get", "post",
                                                         Route = null)]HttpRequest req,
                                                    ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");
    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    PostData data = JsonConvert.DeserializeObject<PostData>(requestBody);
    string url = $"https://www.google.com/maps/search/?api=1&query={data.Latitude},{data.Longitude}";
    log.LogInformation($"URL created - {url}");
    return new OkResult();
}
```

## <a name="run-the-azure-function-locally"></a><span data-ttu-id="baad2-150">Lokales Ausführen der Azure-Funktion</span><span class="sxs-lookup"><span data-stu-id="baad2-150">Run the Azure function locally</span></span>

<span data-ttu-id="baad2-151">Funktionen können mit einem lokalen Speicherkonto und einer lokalen Azure Functions-Runtime lokal ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="baad2-151">Functions can be run locally using a local storage account and local Azure Functions runtime.</span></span> <span data-ttu-id="baad2-152">Mithilfe dieser lokalen Runtime können Sie Ihre Funktion testen, bevor Sie sie in Azure bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="baad2-152">This local runtime allows you to test out your function before deploying it to Azure.</span></span>

1. <span data-ttu-id="baad2-153">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt `ImHere.Functions`, und wählen Sie *Als Startprojekt festlegen* aus.</span><span class="sxs-lookup"><span data-stu-id="baad2-153">Right-click on the `ImHere.Functions` project in the solution explorer, and then select *Set as StartUp project*.</span></span>

1. <span data-ttu-id="baad2-154">Wählen Sie im Menü *Debuggen* die Option *Ohne Debuggen starten* aus.</span><span class="sxs-lookup"><span data-stu-id="baad2-154">From the *Debug* menu, select *Start Without Debugging*.</span></span> <span data-ttu-id="baad2-155">Die lokale Azure Functions-Runtime wird in einem Konsolenfenster gestartet und startet Ihre Funktion. Hierbei wird auf einem verfügbaren Port auf `localhost` gelauscht.</span><span class="sxs-lookup"><span data-stu-id="baad2-155">The local Azure Functions runtime will launch inside a console window and start your function, listening on an available port on `localhost`.</span></span> <span data-ttu-id="baad2-156">Wenn ein Dialogfeld angezeigt wird, in dem nach dem Zugriff auf die Firewall gefragt wird, erlauben Sie den Zugriff auf private Netzwerke (die Standardoption).</span><span class="sxs-lookup"><span data-stu-id="baad2-156">If you see a dialog asking for firewall access, allow access to private networks (the default option).</span></span>

    ![Lokal ausgeführte Azure-Funktion](../media/5-function-running-locally.png)

1. <span data-ttu-id="baad2-158">Notieren Sie den Port, auf dem die Funktion lauscht.</span><span class="sxs-lookup"><span data-stu-id="baad2-158">Take a note of the port that the function is listening on.</span></span> <span data-ttu-id="baad2-159">Sie benötigen diese Angabe in der nächsten Einheit, um die mobile App zu testen.</span><span class="sxs-lookup"><span data-stu-id="baad2-159">You'll need this in the next unit to test out the mobile app.</span></span> <span data-ttu-id="baad2-160">In der Abbildung unten lauscht die Funktion auf Port **7071**.</span><span class="sxs-lookup"><span data-stu-id="baad2-160">In the image above, the function is listening on port **7071**.</span></span>

    ```sh
    Listening on http://localhost:7071/
    ```

1. <span data-ttu-id="baad2-161">Führen Sie die Funktion weiterhin aus, damit Sie in der nächsten Einheit die mobile App testen können.</span><span class="sxs-lookup"><span data-stu-id="baad2-161">Leave the function running so that you can test the mobile app in the next unit.</span></span>

## <a name="summary"></a><span data-ttu-id="baad2-162">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="baad2-162">Summary</span></span>

<span data-ttu-id="baad2-163">In dieser Einheit haben Sie gelernt, wie ein Azure Functions-Projekt in Visual Studio erstellt wird, und Sie haben ein freigegebenes Objekt mit einem Datenobjekt für die gemeinsame Verwendung durch die mobile App und die Funktion hinzugefügt. Außerdem haben Sie erfahren, wie Sie eine grundlegende Implementierung der Funktion erstellen, um die übergebenen Daten zu deserialisieren.</span><span class="sxs-lookup"><span data-stu-id="baad2-163">In this unit, you learned how to create an Azure Functions project in Visual Studio, added a shared project with a data object to be shared between the mobile app and the function, and learned how to create a basic implementation of the function to deserialize the data passed in.</span></span> <span data-ttu-id="baad2-164">Ferner haben Sie erfahren, wie eine Azure-Funktion lokal ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="baad2-164">You also learned how to run an Azure function locally.</span></span> <span data-ttu-id="baad2-165">In der nächsten Einheit rufen Sie die Azure-Funktion aus der mobilen App auf.</span><span class="sxs-lookup"><span data-stu-id="baad2-165">In the next unit, you'll call the Azure function from the mobile app.</span></span>