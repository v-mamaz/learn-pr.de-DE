<span data-ttu-id="1950d-101">Die Azure App Service-Authentifizierung ermöglicht in einer Azure Functions-App die Unterstützung der Authentifizierung ohne weiteren Einrichtungsaufwand.</span><span class="sxs-lookup"><span data-stu-id="1950d-101">Azure App Service authentication enables turn-key authentication support in an Azure Functions app.</span></span> <span data-ttu-id="1950d-102">Sie kann nahtlos in Facebook, Twitter, Microsoft-Konten, Google und Azure Active Directory integriert werden.</span><span class="sxs-lookup"><span data-stu-id="1950d-102">It integrates seamlessly with Facebook, Twitter, Microsoft accounts, Google, and Azure Active Directory.</span></span> <span data-ttu-id="1950d-103">Sie fügen die App Service-Authentifizierung hinzu, um die Back-End-APIs für Ihre Web-App zu schützen.</span><span class="sxs-lookup"><span data-stu-id="1950d-103">You'll add App Service authentication to protect the back-end APIs of your web app.</span></span>

## <a name="enable-app-service-authentication"></a><span data-ttu-id="1950d-104">Aktivieren der App Service-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="1950d-104">Enable App Service authentication</span></span>

1. <span data-ttu-id="1950d-105">Öffnen Sie die Funktions-App im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="1950d-105">Open the function app in the Azure portal.</span></span>

1. <span data-ttu-id="1950d-106">Wählen Sie unter **Plattformfeatures** die Option **Authentifizierung/Autorisierung**.</span><span class="sxs-lookup"><span data-stu-id="1950d-106">Under **Platform features**, select **Authentication/Authorization**.</span></span>

    ![Wählen Sie „Authentifizierung und Autorisierung“ aus.](../media/6-authorization.jpg)


1. <span data-ttu-id="1950d-108">Wählen Sie folgende Werte aus:</span><span class="sxs-lookup"><span data-stu-id="1950d-108">Select the following values:</span></span>
    
    | <span data-ttu-id="1950d-109">Einstellung</span><span class="sxs-lookup"><span data-stu-id="1950d-109">Setting</span></span>      |  <span data-ttu-id="1950d-110">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="1950d-110">Suggested value</span></span>   | <span data-ttu-id="1950d-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1950d-111">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="1950d-112">**App Service-Authentifizierung**</span><span class="sxs-lookup"><span data-stu-id="1950d-112">**App Service Authentication**</span></span> | <span data-ttu-id="1950d-113">Ein</span><span class="sxs-lookup"><span data-stu-id="1950d-113">On</span></span> | <span data-ttu-id="1950d-114">Aktiviert die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="1950d-114">Enable authentication.</span></span> |
    | <span data-ttu-id="1950d-115">**Aktion, wenn die Anforderung nicht authentifiziert ist**</span><span class="sxs-lookup"><span data-stu-id="1950d-115">**Action when request is not authenticated**</span></span> | <span data-ttu-id="1950d-116">Anmeldung mit Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1950d-116">Sign in with Azure Active Directory.</span></span> | <span data-ttu-id="1950d-117">Auswahl einer konfigurierte Authentifizierungsmethode (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="1950d-117">Select a configured authentication method (See below).</span></span> |
    | <span data-ttu-id="1950d-118">**Authentifizierungsanbieter**</span><span class="sxs-lookup"><span data-stu-id="1950d-118">**Authentication Providers**</span></span> | <span data-ttu-id="1950d-119">Siehe unten.</span><span class="sxs-lookup"><span data-stu-id="1950d-119">See below.</span></span> | <span data-ttu-id="1950d-120">Siehe unten.</span><span class="sxs-lookup"><span data-stu-id="1950d-120">See below.</span></span> |
    | <span data-ttu-id="1950d-121">**Tokenspeicher**</span><span class="sxs-lookup"><span data-stu-id="1950d-121">**Token store**</span></span> | <span data-ttu-id="1950d-122">Ein</span><span class="sxs-lookup"><span data-stu-id="1950d-122">On</span></span> | <span data-ttu-id="1950d-123">Ermöglicht App Service das Speichern und Verwalten von Token.</span><span class="sxs-lookup"><span data-stu-id="1950d-123">Allow App Service to store and manage tokens.</span></span> |
    | <span data-ttu-id="1950d-124">**Zulässige externe Umleitungs-URLs**</span><span class="sxs-lookup"><span data-stu-id="1950d-124">**Allowed external redirect URLs**</span></span> | <span data-ttu-id="1950d-125">Die URL Ihrer Anwendung, z.B. https://firstserverlessweb.z4.web.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="1950d-125">The URL of your application, for example https://firstserverlessweb.z4.web.core.windows.net/.</span></span> | <span data-ttu-id="1950d-126">URLs, an die App Service Anforderungen umleiten darf, nachdem ein Benutzer authentifiziert wurde.</span><span class="sxs-lookup"><span data-stu-id="1950d-126">URLs that App Service is allowed to redirect to, after a user is authenticated.</span></span> |

1. <span data-ttu-id="1950d-127">Wählen Sie **Azure Active Directory**, um die **Azure Active Directory-Einstellungen** anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="1950d-127">Select **Azure Active Directory** to reveal **Azure Active Directory Settings**.</span></span>

    1. <span data-ttu-id="1950d-128">Wählen Sie **Express** als **Verwaltungsmodus** aus, und fügen Sie die unten angegebenen Informationen ein.</span><span class="sxs-lookup"><span data-stu-id="1950d-128">Select **Express** as the **Management Mode** and fill in the following information.</span></span>
    
        | <span data-ttu-id="1950d-129">Einstellung</span><span class="sxs-lookup"><span data-stu-id="1950d-129">Setting</span></span>      |  <span data-ttu-id="1950d-130">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="1950d-130">Suggested value</span></span>   | <span data-ttu-id="1950d-131">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1950d-131">Description</span></span>                                        |
        | --- | --- | ---|
        | <span data-ttu-id="1950d-132">**Verwaltungsmodus**</span><span class="sxs-lookup"><span data-stu-id="1950d-132">**Management mode**</span></span> | <span data-ttu-id="1950d-133">Express: Neue AD-App erstellen</span><span class="sxs-lookup"><span data-stu-id="1950d-133">Express, Create new AD app</span></span> | <span data-ttu-id="1950d-134">Automatische Einrichtung eines Dienstprinzipal und der Azure Active Directory-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="1950d-134">Automatically set up a service principal and Azure Active Directory authentication.</span></span> |
        | <span data-ttu-id="1950d-135">**App erstellen**</span><span class="sxs-lookup"><span data-stu-id="1950d-135">**Create app**</span></span> | <span data-ttu-id="1950d-136">my-serverless-webapp</span><span class="sxs-lookup"><span data-stu-id="1950d-136">my-serverless-webapp</span></span> | <span data-ttu-id="1950d-137">Eingabe eines eindeutigen Anwendungsnamens.</span><span class="sxs-lookup"><span data-stu-id="1950d-137">Enter a unique application name.</span></span> |
    
    1. <span data-ttu-id="1950d-138">Klicken Sie auf **OK**, um die Azure Active Directory-Einstellungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="1950d-138">Click **OK** to save the Azure Active Directory settings.</span></span>

    ![„Authentifizierung und Autorisierung“ und „Azure Active Directory-Einstellungen“](../media/6-create-aad.png)


1. <span data-ttu-id="1950d-140">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="1950d-140">Click **Save**.</span></span>


## <a name="modify-the-web-app-to-enable-authentication"></a><span data-ttu-id="1950d-141">Ändern der Web-App zum Aktivieren der Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="1950d-141">Modify the web app to enable authentication</span></span>

1. <span data-ttu-id="1950d-142">Stellen Sie in Cloud Shell sicher, dass das aktuelle Verzeichnis der Ordner **www/dist** ist.</span><span class="sxs-lookup"><span data-stu-id="1950d-142">In Cloud Shell, ensure that the current directory is the **www/dist** folder.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. <span data-ttu-id="1950d-143">Fügen Sie der Datei **settings.js** die folgende Codezeile hinzu, um die Authentifizierung in Ihrer Funktions-App zu aktivieren:</span><span class="sxs-lookup"><span data-stu-id="1950d-143">To enable authentication in your function app, append the following line of code to the **settings.js** file:</span></span>

    `window.authEnabled = true`

    <span data-ttu-id="1950d-144">Nehmen Sie die Änderung vor, und zeigen Sie das Ergebnis an, indem Sie die folgenden Befehle oder einen Befehlszeilen-Editor wie VIM verwenden.</span><span class="sxs-lookup"><span data-stu-id="1950d-144">Make the change and view the result by using the following commands, or by using a command-line editor like VIM.</span></span>

    ```azurecli
    echo "window.authEnabled = true" >> settings.js
    ```

    <span data-ttu-id="1950d-145">Vergewissern Sie sich, dass die Änderung an der Datei vorgenommen wurde.</span><span class="sxs-lookup"><span data-stu-id="1950d-145">Confirm that the change was made to the file.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="1950d-146">Laden Sie die Datei in Blob Storage hoch.</span><span class="sxs-lookup"><span data-stu-id="1950d-146">Upload the file to Blob storage.</span></span>

    ```azurecli
    az storage blob upload -c \$web --account-name <storage account name> -f settings.js -n settings.js
    ```


## <a name="test-the-application"></a><span data-ttu-id="1950d-147">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="1950d-147">Test the application</span></span>

1. <span data-ttu-id="1950d-148">Öffnen Sie die Anwendung in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="1950d-148">Open the application in a browser.</span></span> <span data-ttu-id="1950d-149">Klicken Sie auf **Anmelden**, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="1950d-149">Click **Log in** and log in.</span></span>

1. <span data-ttu-id="1950d-150">Wählen Sie eine Bilddatei aus, und laden Sie sie hoch.</span><span class="sxs-lookup"><span data-stu-id="1950d-150">Select an image file and upload it.</span></span>

    ![Anmeldeseite](../media/6-aad-auth.png)
    

## <a name="summary"></a><span data-ttu-id="1950d-152">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="1950d-152">Summary</span></span>

<span data-ttu-id="1950d-153">In dieser Einheit wurde beschrieben, wie Sie der Anwendung mithilfe der Azure App Service-Authentifizierung Authentifizierungsfunktionalität hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="1950d-153">In this unit, you learned how to add authentication to the application using Azure App Service authentication.</span></span>