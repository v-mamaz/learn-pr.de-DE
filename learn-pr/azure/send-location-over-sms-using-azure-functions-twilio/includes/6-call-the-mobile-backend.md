<span data-ttu-id="c173f-101">Die mobile App wird ausgeführt, und die erste Version der Azure-Funktion wurde erstellt.</span><span class="sxs-lookup"><span data-stu-id="c173f-101">The mobile app runs and the initial version of the Azure function has been created.</span></span> <span data-ttu-id="c173f-102">In dieser Einheit rufen Sie die Azure-Funktion in der mobilen App auf und übergeben den Standort des Benutzers und die Liste der Telefonnummern, an die der Benutzer SMS-Nachrichten senden möchte.</span><span class="sxs-lookup"><span data-stu-id="c173f-102">In this unit, you call the Azure function from the mobile app, passing in the user's location and the list of phone numbers the user wants to send SMS messages to.</span></span>

## <a name="calling-the-azure-function-from-the-mobile-app"></a><span data-ttu-id="c173f-103">Aufrufen der Azure-Funktion in der mobilen App</span><span class="sxs-lookup"><span data-stu-id="c173f-103">Calling the Azure function from the mobile app</span></span>

1. <span data-ttu-id="c173f-104">Öffnen Sie `MainViewModel`.</span><span class="sxs-lookup"><span data-stu-id="c173f-104">Open the `MainViewModel`.</span></span>

1. <span data-ttu-id="c173f-105">Fügen Sie in dieser Klasse ein privates `HttpClient`-Feld namens `client` hinzu.</span><span class="sxs-lookup"><span data-stu-id="c173f-105">In this class, add a private `HttpClient` field called `client`.</span></span> <span data-ttu-id="c173f-106">Sie müssen einen Verweis auf den `System.Net.Http`-Namespace hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c173f-106">You'll need to add a reference to the `System.Net.Http` namespace.</span></span>

    ```cs
    HttpClient client = new HttpClient();
    ```

1. <span data-ttu-id="c173f-107">Fügen Sie ein konstantes Feld für die Basis-URL der Funktion hinzu.</span><span class="sxs-lookup"><span data-stu-id="c173f-107">Add a constant field for the base URL for the function.</span></span> <span data-ttu-id="c173f-108">Legen Sie für dieses Feld die Adresse fest, die die lokale Azure Functions-Runtime abhört.</span><span class="sxs-lookup"><span data-stu-id="c173f-108">Set this to the address that the local Azure Functions runtime is listening on.</span></span> <span data-ttu-id="c173f-109">Nachdem die Funktion in Azure bereitgestellt wurde, kann diese Konstante in die Azure-URL geändert werden.</span><span class="sxs-lookup"><span data-stu-id="c173f-109">Once the function is deployed to Azure, this constant can be changed to be the Azure URL.</span></span>

    ```cs
    const string baseUrl = "http://localhost:7071";
    ```

1. <span data-ttu-id="c173f-110">Erstellen Sie in der `SendLocation`-Methode, nachdem der Standort gefunden wurde, eine neue Instanz von `PostData`, indem Sie den Standort und die Liste mit den vom Benutzer eingegebenen Telefonnummern verwenden.</span><span class="sxs-lookup"><span data-stu-id="c173f-110">Inside the `SendLocation` method, after the location has been found, create a new instance of `PostData` using the location and the list of phone numbers entered by the user.</span></span> <span data-ttu-id="c173f-111">Sie müssen eine using-Anweisung für den `ImHere.Data`-Namespace hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c173f-111">You'll need to add a using directive for the `ImHere.Data` namespace.</span></span>

    ```cs
    PostData postData = new PostData
    {
        Latitude = location.Latitude,
        Longitude = location.Longitude,
        ToNumbers = PhoneNumbers.Split('\n')
    };
    ```

    > <span data-ttu-id="c173f-112">Dabei wird davon ausgegangen, dass die Telefonnummern im richtigen Format eingegeben wurden (also eine Telefonnummer pro Zeile im `Editor`-Steuerelement).</span><span class="sxs-lookup"><span data-stu-id="c173f-112">This assumes that the phone numbers have been entered in the correct format, one per line in the `Editor` control.</span></span> <span data-ttu-id="c173f-113">In einer App mit Produktionsqualität würde mithilfe einer Überprüfung sichergestellt werden, dass eine oder mehrere Telefonnummern im richtigen Format eingegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="c173f-113">In a production-quality app, there would be validation around this to ensure one or more phone numbers were entered and were in the correct format.</span></span>

1. <span data-ttu-id="c173f-114">Zum Serialisieren von `PostData` als JSON verwenden Sie am einfachsten das NuGet-Paket „Newtonsoft.JSON“.</span><span class="sxs-lookup"><span data-stu-id="c173f-114">To serialize the `PostData` as JSON, the easiest way is to use the Newtonsoft.JSON NuGet package.</span></span> <span data-ttu-id="c173f-115">Fügen Sie dieses NuGet-Paket dem `ImHere`-Projekt auf die gleiche Weise zu wie das Xamarin.Essentials-Paket in einer vorherigen Einheit.</span><span class="sxs-lookup"><span data-stu-id="c173f-115">Add this NuGet package to the `ImHere` project in the same way that you added Xamarin.Essentials in an earlier unit.</span></span>

1. <span data-ttu-id="c173f-116">Serialisieren Sie `PostData` zu `string` mithilfe einer statischen `JsonConvert`-Klasse.</span><span class="sxs-lookup"><span data-stu-id="c173f-116">Serialize the `PostData` to a `string` using the `JsonConvert` static class.</span></span> <span data-ttu-id="c173f-117">Sie müssen eine using-Anweisung für den `Newtonsoft.Json`-Namespace hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c173f-117">You'll need to add a using directive for the `Newtonsoft.Json` namespace.</span></span> <span data-ttu-id="c173f-118">Codieren Sie diese Zeichenfolge in eine `StringContent`-Klasse, sodass diese der Azure-Funktion als JSON übergeben werden kann.</span><span class="sxs-lookup"><span data-stu-id="c173f-118">Encode this string into a `StringContent` class so that it can be passed to the Azure function as JSON.</span></span>

    ```cs
    string data = JsonConvert.SerializeObject(postData);
    StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
    ```

1. <span data-ttu-id="c173f-119">Senden Sie diese Daten an die Funktion, und erhalten Sie das Ergebnis zurück.</span><span class="sxs-lookup"><span data-stu-id="c173f-119">Post this data to the function and get the result back.</span></span>

   ```cs
    HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                        content);
   ```

   <span data-ttu-id="c173f-120">Über `/api/<function name>` wird auf Azure-Funktionen zugegriffen. Wenn es sich bei dem Port, der von der lokalen Functions-Runtime ausgewählt wird, beispielsweise um Port 7071 handelt, wird die `SendLocation`-Funktion unter `http://localhost:7071/api/SendLocation` zur Verfügung gestellt.</span><span class="sxs-lookup"><span data-stu-id="c173f-120">Azure functions are accessed using `/api/<function name>`, so assuming the port chosen by the local Functions runtime is 7071, the `SendLocation` function will be accessible at `http://localhost:7071/api/SendLocation`.</span></span>

1. <span data-ttu-id="c173f-121">Abhängig vom Ergebnis wird auf der Benutzeroberfläche eine Meldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c173f-121">Depending on the result, show a message on the UI.</span></span>

    ```cs
    if (result.IsSuccessStatusCode)
        Message = "Location sent successfully";
    else
        Message = $"Error - {result.ReasonPhrase}";
    ```

<span data-ttu-id="c173f-122">Der vollständige Code für die neuen Felder und die `SendLocation`-Methode wird unten angegeben.</span><span class="sxs-lookup"><span data-stu-id="c173f-122">The full code for the new fields and the `SendLocation` method is below.</span></span>

```cs
HttpClient client = new HttpClient();
const string baseUrl = "http://localhost:7071";

async Task SendLocation()
{
    Location location = await Geolocation.GetLastKnownLocationAsync();

    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";

        PostData postData = new PostData
        {
            Latitude = location.Latitude,
            Longitude = location.Longitude,
            ToNumbers = PhoneNumbers.Split('\n')
        };

        string data = JsonConvert.SerializeObject(postData);
        StringContent content = new StringContent(data, Encoding.UTF8, "application/json");
        HttpResponseMessage result = await client.PostAsync($"{baseUrl}/api/SendLocation",
                                                            content);

        if (result.IsSuccessStatusCode)
            Message = "Location sent successfully";
        else
            Message = $"Error - {result.ReasonPhrase}";
    }
}
```

## <a name="testing-it-out"></a><span data-ttu-id="c173f-123">Testen Sie es</span><span class="sxs-lookup"><span data-stu-id="c173f-123">Testing it out</span></span>

1. <span data-ttu-id="c173f-124">Stellen Sie sicher, dass die Azure-Funktion noch lokal ausgeführt wird und der Port der `SendLocation`-Methode entspricht.</span><span class="sxs-lookup"><span data-stu-id="c173f-124">Make sure the Azure function is still running locally and the port matches the `SendLocation` method.</span></span>

1. <span data-ttu-id="c173f-125">Legen Sie die UWP-App als Start-App fest, und führen Sie diese aus.</span><span class="sxs-lookup"><span data-stu-id="c173f-125">Set the UWP app as the startup app and run it.</span></span> <span data-ttu-id="c173f-126">Klicken Sie auf die Schaltfläche **Standort senden**.</span><span class="sxs-lookup"><span data-stu-id="c173f-126">Click the **Send Location** button.</span></span> <span data-ttu-id="c173f-127">Im Konsolenfenster der Functions-Runtime, welches die aufgerufene Funktion angezeigt, wird die Ausgabe und die Protokollierung mit der generierten URL angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c173f-127">You'll see output in the Functions runtime console window showing the function being called, and the logging showing the generated URL.</span></span>

    ![Ausgabe der aufgerufenen Funktion](../media/6-function-called.png)

1. <span data-ttu-id="c173f-129">Um die URL-Generierung zu testen, fügen Sie sie von der Konsole in einem Browser ein.</span><span class="sxs-lookup"><span data-stu-id="c173f-129">To test the URL generation, paste it from the console into a browser.</span></span> <span data-ttu-id="c173f-130">Ihr aktueller Standort sollte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="c173f-130">It should show your current location.</span></span>

## <a name="summary"></a><span data-ttu-id="c173f-131">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c173f-131">Summary</span></span>

<span data-ttu-id="c173f-132">In dieser Einheit haben Sie gelernt, wie Sie in der mobilen App eine Azure-Funktion aufrufen.</span><span class="sxs-lookup"><span data-stu-id="c173f-132">In this unit, you learned how to call an Azure function from the mobile app.</span></span> <span data-ttu-id="c173f-133">Dieser Aufruf gibt den Standort des Benutzers und die Telefonnummern weiter, die als JSON eingegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="c173f-133">This call passed the user's location and the phone numbers they entered as JSON.</span></span> <span data-ttu-id="c173f-134">In der nächsten Einheit müssen Sie die Azure-Funktion an Twilio binden, um den Standort als SMS-Nachricht zu senden.</span><span class="sxs-lookup"><span data-stu-id="c173f-134">In the next unit, you'll bind the Azure function to Twilio to send this location as an SMS message.</span></span>