<span data-ttu-id="1ef9a-101">Azure App Service-Authentifizierung ermöglicht die Unterstützung von einsetzbare Authentifizierung in einer Azure-Funktions-app.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-101">Azure App Service Authentication enables turn-key authentication support in an Azure Function app.</span></span> <span data-ttu-id="1ef9a-102">Es kann nahtlos in Facebook, Twitter, Microsoft Account, Google und Azure Active Directory integriert.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-102">It integrates seamlessly with Facebook, Twitter, Microsoft Account, Google, and Azure Active Directory.</span></span> <span data-ttu-id="1ef9a-103">Fügen Sie App Service-Authentifizierung, um die APIs der Web-app-Back-End zu schützen.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-103">You'll add App Service Authentication to protect the backend APIs of your web app.</span></span>

## <a name="enable-app-service-authentication"></a><span data-ttu-id="1ef9a-104">App Service-Authentifizierung aktivieren</span><span class="sxs-lookup"><span data-stu-id="1ef9a-104">Enable App Service Authentication</span></span>

1. <span data-ttu-id="1ef9a-105">Öffnen Sie die Funktions-app im Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-105">Open the function app in the Azure Portal.</span></span>

1. <span data-ttu-id="1ef9a-106">Klicken Sie unter **Plattformfeatures**Option **Authentifizierung/Autorisierung**.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-106">Under **Platform features**, select **Authentication/Authorization**.</span></span>

    ![Wählen Sie die Authentifizierung / Autorisierung](../images/6-authorization.jpg)

1. <span data-ttu-id="1ef9a-108">Wählen Sie folgende Werte aus:</span><span class="sxs-lookup"><span data-stu-id="1ef9a-108">Select the following values:</span></span>
    
    | <span data-ttu-id="1ef9a-109">Einstellung</span><span class="sxs-lookup"><span data-stu-id="1ef9a-109">Setting</span></span>      |  <span data-ttu-id="1ef9a-110">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="1ef9a-110">Suggested value</span></span>   | <span data-ttu-id="1ef9a-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1ef9a-111">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="1ef9a-112">**App Service-Authentifizierung**</span><span class="sxs-lookup"><span data-stu-id="1ef9a-112">**App Service Authentication**</span></span> | <span data-ttu-id="1ef9a-113">Andererseits</span><span class="sxs-lookup"><span data-stu-id="1ef9a-113">On</span></span> | <span data-ttu-id="1ef9a-114">Aktivieren der Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-114">Enable authentication.</span></span> |
    | <span data-ttu-id="1ef9a-115">**Aktion, wenn die Anforderung nicht authentifiziert ist**</span><span class="sxs-lookup"><span data-stu-id="1ef9a-115">**Action when request is not authenticated**</span></span> | <span data-ttu-id="1ef9a-116">Mit Azure Active Directory anmelden</span><span class="sxs-lookup"><span data-stu-id="1ef9a-116">Log in with Azure Active Directory</span></span> | <span data-ttu-id="1ef9a-117">Wählen Sie eine konfigurierte Authentifizierungsmethode (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="1ef9a-117">Select a configured authentication method (below).</span></span> |
    | <span data-ttu-id="1ef9a-118">**Authentifizierungsanbieter**</span><span class="sxs-lookup"><span data-stu-id="1ef9a-118">**Authentication Providers**</span></span> | <span data-ttu-id="1ef9a-119">Siehe unten</span><span class="sxs-lookup"><span data-stu-id="1ef9a-119">See below</span></span> | <span data-ttu-id="1ef9a-120">Siehe unten</span><span class="sxs-lookup"><span data-stu-id="1ef9a-120">See below</span></span> |
    | <span data-ttu-id="1ef9a-121">**Tokenspeicher**</span><span class="sxs-lookup"><span data-stu-id="1ef9a-121">**Token store**</span></span> | <span data-ttu-id="1ef9a-122">Andererseits</span><span class="sxs-lookup"><span data-stu-id="1ef9a-122">On</span></span> | <span data-ttu-id="1ef9a-123">Ermöglichen Sie die App Service zum Speichern und Verwalten von Token.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-123">Allow App Service to store and manage tokens.</span></span> |
    | <span data-ttu-id="1ef9a-124">**Zulässige externe umleitungs-URLs**</span><span class="sxs-lookup"><span data-stu-id="1ef9a-124">**Allowed external redirect URLs**</span></span> | <span data-ttu-id="1ef9a-125">Die URL Ihrer Anwendung, z.B.: https://firstserverlessweb.z4.web.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="1ef9a-125">The URL of your application, for example: https://firstserverlessweb.z4.web.core.windows.net/</span></span> | <span data-ttu-id="1ef9a-126">URLs, die App Service zulässig ist, um umgeleitet werden soll, nachdem ein Benutzer authentifiziert ist.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-126">URL(s) that App Service is allowed to redirect to after a user is authenticated.</span></span> |

1. <span data-ttu-id="1ef9a-127">Wählen Sie **Azure Active Directory** offengelegt **Azure Active Directory-Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-127">Select **Azure Active Directory** to reveal **Azure Active Directory Settings**.</span></span>

    1. <span data-ttu-id="1ef9a-128">Wählen Sie **Express** als die **Verwaltungsmodus** und füllen Sie die folgenden Informationen.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-128">Select **Express** as the **Management Mode** and fill in the following information.</span></span>
    
        | <span data-ttu-id="1ef9a-129">Einstellung</span><span class="sxs-lookup"><span data-stu-id="1ef9a-129">Setting</span></span>      |  <span data-ttu-id="1ef9a-130">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="1ef9a-130">Suggested value</span></span>   | <span data-ttu-id="1ef9a-131">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1ef9a-131">Description</span></span>                                        |
        | --- | --- | ---|
        | <span data-ttu-id="1ef9a-132">**Verwaltungsmodus**</span><span class="sxs-lookup"><span data-stu-id="1ef9a-132">**Management mode**</span></span> | <span data-ttu-id="1ef9a-133">Express, erstellen Sie neue AD-app</span><span class="sxs-lookup"><span data-stu-id="1ef9a-133">Express, Create new AD app</span></span> | <span data-ttu-id="1ef9a-134">Um einen Dienstprinzipal und eine Azure Active Directory-Authentifizierung automatisch festgelegt.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-134">Automatically set up a service principal and Azure Active Directory authentication.</span></span> |
        | <span data-ttu-id="1ef9a-135">**Erstellen einer App**</span><span class="sxs-lookup"><span data-stu-id="1ef9a-135">**Create app**</span></span> | <span data-ttu-id="1ef9a-136">my-serverless-webapp</span><span class="sxs-lookup"><span data-stu-id="1ef9a-136">my-serverless-webapp</span></span> | <span data-ttu-id="1ef9a-137">Geben Sie einen eindeutigen Anwendungsnamen ein.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-137">Enter a unique application name.</span></span> |
    
    1. <span data-ttu-id="1ef9a-138">Klicken Sie auf **OK** zum Speichern der Azure Active Directory-Einstellungen.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-138">Click **OK** to save the Azure Active Directory settings.</span></span>

    ![Authentifizierung/Autorisierung und Azure Active Directory-Einstellungen](../images/6-create-aad.png)

1. <span data-ttu-id="1ef9a-140">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-140">Click **Save**.</span></span>


## <a name="modify-the-web-app-to-enable-authentication"></a><span data-ttu-id="1ef9a-141">Ändern Sie die Web-app zum Aktivieren der Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="1ef9a-141">Modify the web app to enable authentication</span></span>

1. <span data-ttu-id="1ef9a-142">Stellen Sie sicher, dass das aktuelle Verzeichnis ist, in der Cloud Shell die **Www/Dist** Ordner.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-142">In the Cloud Shell, ensure that the current directory is the **www/dist** folder.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. <span data-ttu-id="1ef9a-143">Fügen Sie zum Aktivieren der Authentifizierung in Ihrer Funktions-app die folgende Codezeile, **settings.js**.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-143">To enable authentication in your function app, append the following line of code to **settings.js**.</span></span>

    `window.authEnabled = true`

    <span data-ttu-id="1ef9a-144">Nehmen Sie die Änderung, und zeigen Sie das Ergebnis mit den folgenden Befehlen oder mithilfe eines Befehlszeile Editors wie z. B. VIM.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-144">Make the change and view the result by using the following commands or by using a command-line editor like VIM.</span></span>

    ```azurecli
    echo "window.authEnabled = true" >> settings.js
    ```

    <span data-ttu-id="1ef9a-145">Vergewissern Sie sich, dass die Änderung an der Datei vorgenommen wurde.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-145">Confirm the change was made to the file.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="1ef9a-146">Laden Sie die Datei in Blob Storage hoch.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-146">Upload the file to Blob storage.</span></span>

    ```azurecli
    az storage blob upload -c \$web --account-name <storage account name> -f settings.js -n settings.js
    ```


## <a name="test-the-application"></a><span data-ttu-id="1ef9a-147">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="1ef9a-147">Test the application</span></span>

1. <span data-ttu-id="1ef9a-148">Öffnen Sie die Anwendung in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-148">Open the application in a browser.</span></span> <span data-ttu-id="1ef9a-149">Klicken Sie auf **melden Sie sich bei** und melden Sie sich.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-149">Click **Log in** and log in.</span></span>

1. <span data-ttu-id="1ef9a-150">Wählen Sie eine Bilddatei, und Laden Sie es hoch.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-150">Select an image file and upload it.</span></span>

    ![Anmeldeseite](../images/6-aad-auth.png)
    

## <a name="summary"></a><span data-ttu-id="1ef9a-152">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="1ef9a-152">Summary</span></span>

<span data-ttu-id="1ef9a-153">In dieser Einheit haben Sie gelernt, wie die Verwendung von Azure App Service-Authentifizierung Applcation Authentifizierung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="1ef9a-153">In this unit, you learned how to add authentication to the applcation using Azure App Service Authentication.</span></span>