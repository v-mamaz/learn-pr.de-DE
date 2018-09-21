<span data-ttu-id="115fe-101">Die Azure App Service-Authentifizierung ermöglicht in einer Azure Functions-App die Unterstützung der Authentifizierung ohne weiteren Einrichtungsaufwand.</span><span class="sxs-lookup"><span data-stu-id="115fe-101">Azure App Service authentication enables turn-key authentication support in an Azure Functions app.</span></span> <span data-ttu-id="115fe-102">Sie kann nahtlos in Facebook, Twitter, Microsoft-Konten, Google und Azure Active Directory integriert werden.</span><span class="sxs-lookup"><span data-stu-id="115fe-102">It integrates seamlessly with Facebook, Twitter, Microsoft accounts, Google, and Azure Active Directory.</span></span> <span data-ttu-id="115fe-103">Sie fügen die App Service-Authentifizierung hinzu, um die Back-End-APIs für Ihre Web-App zu schützen.</span><span class="sxs-lookup"><span data-stu-id="115fe-103">You'll add App Service authentication to protect the back-end APIs of your web app.</span></span>

## <a name="enable-app-service-authentication"></a><span data-ttu-id="115fe-104">Aktivieren der App Service-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="115fe-104">Enable App Service authentication</span></span>

1. <span data-ttu-id="115fe-105">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="115fe-105">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="115fe-106">Öffnen Sie die Funktions-App.</span><span class="sxs-lookup"><span data-stu-id="115fe-106">Open the function app.</span></span>

1. <span data-ttu-id="115fe-107">Wählen Sie unter **Plattformfeatures** die Option **Authentifizierung/Autorisierung** aus.</span><span class="sxs-lookup"><span data-stu-id="115fe-107">Under **Platform features**, select **Authentication/Authorization**.</span></span>

    ![Wählen Sie „Authentifizierung und Autorisierung“ aus.](../media/6-authorization.jpg)

1. <span data-ttu-id="115fe-109">Wählen Sie folgende Werte aus:</span><span class="sxs-lookup"><span data-stu-id="115fe-109">Select the following values:</span></span>

    | <span data-ttu-id="115fe-110">Einstellung</span><span class="sxs-lookup"><span data-stu-id="115fe-110">Setting</span></span>      |  <span data-ttu-id="115fe-111">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="115fe-111">Suggested value</span></span>   | <span data-ttu-id="115fe-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="115fe-112">Description</span></span>                                        |
    | --- | --- | ---|
    | <span data-ttu-id="115fe-113">**App Service-Authentifizierung**</span><span class="sxs-lookup"><span data-stu-id="115fe-113">**App Service Authentication**</span></span> | <span data-ttu-id="115fe-114">Ein</span><span class="sxs-lookup"><span data-stu-id="115fe-114">On</span></span> | <span data-ttu-id="115fe-115">Aktiviert die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="115fe-115">Enable authentication.</span></span> |
    | <span data-ttu-id="115fe-116">**Aktion, wenn die Anforderung nicht authentifiziert ist**</span><span class="sxs-lookup"><span data-stu-id="115fe-116">**Action when request is not authenticated**</span></span> | <span data-ttu-id="115fe-117">Anmeldung mit Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="115fe-117">Sign in with Azure Active Directory.</span></span> | <span data-ttu-id="115fe-118">Auswahl einer konfigurierte Authentifizierungsmethode (siehe unten).</span><span class="sxs-lookup"><span data-stu-id="115fe-118">Select a configured authentication method (See below).</span></span> |
    | <span data-ttu-id="115fe-119">**Authentifizierungsanbieter**</span><span class="sxs-lookup"><span data-stu-id="115fe-119">**Authentication Providers**</span></span> | <span data-ttu-id="115fe-120">Siehe unten.</span><span class="sxs-lookup"><span data-stu-id="115fe-120">See below.</span></span> | <span data-ttu-id="115fe-121">Siehe unten.</span><span class="sxs-lookup"><span data-stu-id="115fe-121">See below.</span></span> |
    | <span data-ttu-id="115fe-122">**Tokenspeicher**</span><span class="sxs-lookup"><span data-stu-id="115fe-122">**Token store**</span></span> | <span data-ttu-id="115fe-123">Ein</span><span class="sxs-lookup"><span data-stu-id="115fe-123">On</span></span> | <span data-ttu-id="115fe-124">Ermöglicht App Service das Speichern und Verwalten von Token.</span><span class="sxs-lookup"><span data-stu-id="115fe-124">Allow App Service to store and manage tokens.</span></span> |
    | <span data-ttu-id="115fe-125">**Zulässige externe Umleitungs-URLs**</span><span class="sxs-lookup"><span data-stu-id="115fe-125">**Allowed external redirect URLs**</span></span> | <span data-ttu-id="115fe-126">Die URL Ihrer Anwendung, z.B. https://firstserverlessweb.z4.web.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="115fe-126">The URL of your application, for example https://firstserverlessweb.z4.web.core.windows.net/.</span></span> | <span data-ttu-id="115fe-127">URLs, an die App Service Anforderungen umleiten darf, nachdem ein Benutzer authentifiziert wurde.</span><span class="sxs-lookup"><span data-stu-id="115fe-127">URLs that App Service is allowed to redirect to, after a user is authenticated.</span></span> |

1. <span data-ttu-id="115fe-128">Wählen Sie **Azure Active Directory**, um die **Azure Active Directory-Einstellungen** anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="115fe-128">Select **Azure Active Directory** to reveal **Azure Active Directory Settings**.</span></span>

    1. <span data-ttu-id="115fe-129">Wählen Sie **Express** als **Verwaltungsmodus** aus, und fügen Sie die unten angegebenen Informationen ein.</span><span class="sxs-lookup"><span data-stu-id="115fe-129">Select **Express** as the **Management Mode** and fill in the following information.</span></span>

        | <span data-ttu-id="115fe-130">Einstellung</span><span class="sxs-lookup"><span data-stu-id="115fe-130">Setting</span></span>      |  <span data-ttu-id="115fe-131">Empfohlener Wert</span><span class="sxs-lookup"><span data-stu-id="115fe-131">Suggested value</span></span>   | <span data-ttu-id="115fe-132">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="115fe-132">Description</span></span>                                        |
        | --- | --- | ---|
        | <span data-ttu-id="115fe-133">**Verwaltungsmodus**</span><span class="sxs-lookup"><span data-stu-id="115fe-133">**Management mode**</span></span> | <span data-ttu-id="115fe-134">Express: Neue AD-App erstellen</span><span class="sxs-lookup"><span data-stu-id="115fe-134">Express, Create new AD app</span></span> | <span data-ttu-id="115fe-135">Automatische Einrichtung eines Dienstprinzipal und der Azure Active Directory-Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="115fe-135">Automatically set up a service principal and Azure Active Directory authentication.</span></span> |
        | <span data-ttu-id="115fe-136">**App erstellen**</span><span class="sxs-lookup"><span data-stu-id="115fe-136">**Create app**</span></span> | <span data-ttu-id="115fe-137">my-serverless-webapp</span><span class="sxs-lookup"><span data-stu-id="115fe-137">my-serverless-webapp</span></span> | <span data-ttu-id="115fe-138">Eingabe eines eindeutigen Anwendungsnamens.</span><span class="sxs-lookup"><span data-stu-id="115fe-138">Enter a unique application name.</span></span> |

    1. <span data-ttu-id="115fe-139">Klicken Sie auf **OK**, um die Azure Active Directory-Einstellungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="115fe-139">Click **OK** to save the Azure Active Directory settings.</span></span>

    ![„Authentifizierung und Autorisierung“ und „Azure Active Directory-Einstellungen“](../media/6-create-aad.png)

1. <span data-ttu-id="115fe-141">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="115fe-141">Click **Save**.</span></span>

## <a name="modify-the-web-app-to-enable-authentication"></a><span data-ttu-id="115fe-142">Ändern der Web-App zum Aktivieren der Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="115fe-142">Modify the web app to enable authentication</span></span>

1. <span data-ttu-id="115fe-143">Stellen Sie in Cloud Shell sicher, dass das aktuelle Verzeichnis der Ordner **www/dist** ist.</span><span class="sxs-lookup"><span data-stu-id="115fe-143">In Cloud Shell, ensure that the current directory is the **www/dist** folder.</span></span>

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. <span data-ttu-id="115fe-144">Zum Aktivieren von Authentifizierung in Ihrer Funktions-App ändern Sie **settings.js**.</span><span class="sxs-lookup"><span data-stu-id="115fe-144">You enable authentication in your function app by modifying **settings.js**.</span></span> <span data-ttu-id="115fe-145">Öffnen Sie die Datei im Cloud Shell-Editor.</span><span class="sxs-lookup"><span data-stu-id="115fe-145">Open the file in Cloud Shell Editor.</span></span>

    ```azurecli
    code settings.js
    ```

1. <span data-ttu-id="115fe-146">Fügen Sie der Datei die folgende Zeile hinzu, und speichern Sie sie.</span><span class="sxs-lookup"><span data-stu-id="115fe-146">Append the following line to the file and save it.</span></span>

    ```azurecli
    window.authEnabled = true
    ```

1. <span data-ttu-id="115fe-147">Vergewissern Sie sich, dass die Änderung an der Datei vorgenommen wurde.</span><span class="sxs-lookup"><span data-stu-id="115fe-147">Confirm the change was made to the file.</span></span>

    ```azurecli
    cat settings.js
    ```

1. <span data-ttu-id="115fe-148">Laden Sie die Datei in Blog Storage hoch.</span><span class="sxs-lookup"><span data-stu-id="115fe-148">Upload the file to Blob storage.</span></span>

    ```azurecli
    az storage blob upload \
        -c \$web \
        --account-name <storage account name> \
        -f settings.js \
        -n settings.js
    ```

## <a name="test-the-application"></a><span data-ttu-id="115fe-149">Testen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="115fe-149">Test the application</span></span>

1. <span data-ttu-id="115fe-150">Öffnen Sie die Anwendung in einem Browser.</span><span class="sxs-lookup"><span data-stu-id="115fe-150">Open the application in a browser.</span></span> <span data-ttu-id="115fe-151">Klicken Sie auf **Anmelden**, und melden Sie sich an.</span><span class="sxs-lookup"><span data-stu-id="115fe-151">Click **Log in** and log in.</span></span>

1. <span data-ttu-id="115fe-152">Wählen Sie eine Bilddatei aus, und laden Sie sie hoch.</span><span class="sxs-lookup"><span data-stu-id="115fe-152">Select an image file and upload it.</span></span>

    ![Anmeldeseite](../media/6-aad-auth.png)

## <a name="summary"></a><span data-ttu-id="115fe-154">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="115fe-154">Summary</span></span>

<span data-ttu-id="115fe-155">In dieser Einheit wurde beschrieben, wie Sie der Anwendung mithilfe der Azure App Service-Authentifizierung Authentifizierungsfunktionalität hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="115fe-155">In this unit, you learned how to add authentication to the application using Azure App Service authentication.</span></span>