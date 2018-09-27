<span data-ttu-id="d66ba-101">Die App verfügt über eine Benutzeroberfläche und ein ViewModel.</span><span class="sxs-lookup"><span data-stu-id="d66ba-101">The app has a UI and a ViewModel.</span></span> <span data-ttu-id="d66ba-102">In dieser Einheit fügen Sie mit Xamarin.Essentials die Suche nach dem Standort zum ViewModel hinzu.</span><span class="sxs-lookup"><span data-stu-id="d66ba-102">In this unit, you add location lookup to the ViewModel using Xamarin.Essentials.</span></span>

## <a name="enable-location-permissions"></a><span data-ttu-id="d66ba-103">Aktivieren von Standortberechtigungen</span><span class="sxs-lookup"><span data-stu-id="d66ba-103">Enable location permissions</span></span>

<span data-ttu-id="d66ba-104">Alle mobilen Plattformen schützen Benutzerinformationen und Hardware, wie z.B. die Kamera, die Bildergalerie und den Standort des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="d66ba-104">All mobile platforms have security around user information and certain hardware, such as the camera, photo library, and the user's location.</span></span> <span data-ttu-id="d66ba-105">Bevor eine App auf den Standort des Benutzers zugreifen kann, muss der Benutzer diese Berechtigung erteilen. Diese Berechtigungen werden entweder implizit beim Installieren oder zur Laufzeit erteilt.</span><span class="sxs-lookup"><span data-stu-id="d66ba-105">Before an app can access the user's location, the user has to grant permission - either by implicitly granting these permissions at install time or by choosing to grant a permission at runtime.</span></span> <span data-ttu-id="d66ba-106">Wenn Sie eine UWP-App im Store anzeigen, werden die von der App benötigten Berechtigungen aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="d66ba-106">When you view a UWP app on the store, the listing will show the permissions that the app needs.</span></span> <span data-ttu-id="d66ba-107">Wenn Sie die App installieren, erteilen Sie implizit die Berechtigung.</span><span class="sxs-lookup"><span data-stu-id="d66ba-107">By installing the app, you implicitly grant permission.</span></span> <span data-ttu-id="d66ba-108">Diese Berechtigungen werden in einer Manifestdatei der App konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="d66ba-108">These permissions are configured in an app manifest file.</span></span>

1. <span data-ttu-id="d66ba-109">Öffnen Sie im `ImHere.UWP`-App-Projekt die `Package.appxmanifest`-Datei.</span><span class="sxs-lookup"><span data-stu-id="d66ba-109">In the `ImHere.UWP` app project, open the `Package.appxmanifest` file.</span></span>

1. <span data-ttu-id="d66ba-110">Navigieren Sie zur Registerkarte **Funktionen**, und überprüfen Sie die Funktion *Standort*.</span><span class="sxs-lookup"><span data-stu-id="d66ba-110">Head to the **Capabilities** tab and check the *Location* capability.</span></span>

    ![Die Registerkarte „UWP-Funktionen“](../media/4-uwp-location-capability.png)

## <a name="query-for-the-users-location"></a><span data-ttu-id="d66ba-112">Abfragen des Benutzerstandorts</span><span class="sxs-lookup"><span data-stu-id="d66ba-112">Query for the user's location</span></span>

<span data-ttu-id="d66ba-113">Es kann entweder der letzte bekannte oder der aktuelle Standort ermittelt werden.</span><span class="sxs-lookup"><span data-stu-id="d66ba-113">There are two ways to get the user's location - the last known or the current.</span></span> <span data-ttu-id="d66ba-114">Die Ermittlung des aktuellen Standorts dauert möglicherweise länger, da das Gerät gegebenenfalls einen GPS-Link einrichten und warten muss, bis der genaue Standort abgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="d66ba-114">The current location can take some time to get because the device may need to establish a GPS link and wait for the accurate location to be retrieved.</span></span> <span data-ttu-id="d66ba-115">Am schnellsten wird der dem Gerät zuletzt bekannte Standort ermittelt.</span><span class="sxs-lookup"><span data-stu-id="d66ba-115">The fastest way is to get the last known location detected by the device.</span></span> <span data-ttu-id="d66ba-116">Der zuletzt bekannte Speicherort ist möglicherweise ungenauer, kann allerdings schneller aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="d66ba-116">The last known location is potentially less accurate but is a much faster call.</span></span> <span data-ttu-id="d66ba-117">Standorte werden in Längengrad und Breitengrad mit [Dezimalstellen](https://en.wikipedia.org/wiki/Decimal_degrees?azure-portal=true) und der Höhe des Geräts in Metern über dem Meeresspiegel angegeben.</span><span class="sxs-lookup"><span data-stu-id="d66ba-117">Locations come as the latitude and longitude in [decimal degrees](https://en.wikipedia.org/wiki/Decimal_degrees?azure-portal=true) and the altitude of the device in meters above sea level.</span></span>

1. <span data-ttu-id="d66ba-118">Öffnen Sie die `MainViewModel`-Klasse im .NET Standard-Projekt `ImHere`.</span><span class="sxs-lookup"><span data-stu-id="d66ba-118">Open the `MainViewModel` class in the `ImHere` .NET Standard project.</span></span>

1. <span data-ttu-id="d66ba-119">Rufen Sie in der `SendLocation`-Methode die statische `GetLastKnownLocationAsync`-Methode in der `Geolocation`-Klasse im `Xamarin.Essentials`-Namespace auf.</span><span class="sxs-lookup"><span data-stu-id="d66ba-119">In the `SendLocation` method, make a call to the `GetLastKnownLocationAsync` static method on the `Geolocation` class in the `Xamarin.Essentials` namespace.</span></span> <span data-ttu-id="d66ba-120">Sie müssen eine using-Anweisung für den `Xamarin.Essentials`-Namespace hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d66ba-120">You will need to add a using directive for the `Xamarin.Essentials` namespace.</span></span>

    ```csharp
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

1. <span data-ttu-id="d66ba-121">Aktualisieren Sie die `Message`-Eigenschaft mit dem Standort des Benutzers, falls dieser ermittelt werden konnte.</span><span class="sxs-lookup"><span data-stu-id="d66ba-121">Update the `Message` property with the user's location if one is found.</span></span>

    ```csharp
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

    <span data-ttu-id="d66ba-122">Im Folgenden finden Sie den vollständigen Code für diese Methode.</span><span class="sxs-lookup"><span data-stu-id="d66ba-122">The full code for this method is below.</span></span>
    
    ```csharp
    async Task SendLocation()
    {
        Location location = await Geolocation.GetLastKnownLocationAsync();
    
        if (location != null)
        {
            Message = $"Location found: {location.Latitude}, {location.Longitude}.";
        }
    }
    ```

1. <span data-ttu-id="d66ba-123">Führen Sie die App aus, und klicken Sie auf die Schaltfläche **Standort senden**, um den Standort auf der Benutzeroberfläche anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="d66ba-123">Run the app and click the **Send Location** button to see the location on the UI.</span></span>

    ![Die ausgeführte App, die den Standort des Benutzers anzeigt](../media/4-running-app-showing-location.png)    

> [!NOTE]
> <span data-ttu-id="d66ba-125">Diese App verwendet den letzten bekannten Standort.</span><span class="sxs-lookup"><span data-stu-id="d66ba-125">This app uses the last known location.</span></span> <span data-ttu-id="d66ba-126">Wenn Sie in einer App mit Produktionsqualität den exakten aktuellen Standort mit einem Timeout erhalten möchten und dieser nicht ohne Zeitüberschreitung gefunden wird, nutzen Sie den zuletzt bekannten Standort.</span><span class="sxs-lookup"><span data-stu-id="d66ba-126">In a production-quality app, you would want to get the current accurate location with a time-out, and if one is not found in time, fall back to the last known.</span></span> <span data-ttu-id="d66ba-127">Weitere Informationen dazu erhalten Sie unter [Xamarin.Essentials Geolocation-Dokumentation](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="d66ba-127">You can read more on how to do this in the [Xamarin.Essentials Geolocation docs](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation?azure-portal=true).</span></span>
> 
> <span data-ttu-id="d66ba-128">Diese App verfügt nicht über Möglichkeiten zur Fehlerbehandlung.</span><span class="sxs-lookup"><span data-stu-id="d66ba-128">This app does not have error handling.</span></span> <span data-ttu-id="d66ba-129">In einer App mit Produktionsqualität müssen Sie alle Ausnahmen, die auftreten, behandeln, z.B. wenn der Standort nicht verfügbar war.</span><span class="sxs-lookup"><span data-stu-id="d66ba-129">In a production-quality app, you should handle any exceptions that occur, such as if the location was not available.</span></span>

## <a name="summary"></a><span data-ttu-id="d66ba-130">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="d66ba-130">Summary</span></span>

<span data-ttu-id="d66ba-131">In dieser Einheit haben Sie gelernt, wie Sie Xamarin.Essentials verwenden, um den Standort des Benutzers zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="d66ba-131">In this unit, you learned how to use Xamarin.Essentials to get the user's location.</span></span> <span data-ttu-id="d66ba-132">In der nächsten Einheit erstellen Sie eine Azure-Funktion, die als Back-End für die mobile App fungiert.</span><span class="sxs-lookup"><span data-stu-id="d66ba-132">In the next unit, you'll create an Azure function to act as a back end for the mobile app.</span></span>