<span data-ttu-id="ea363-101">Die App und Azure-Funktion sind nun vollständig und werden lokal ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="ea363-101">The app and Azure Function are now complete and running locally.</span></span> <span data-ttu-id="ea363-102">In dieser Einheit veröffentlichen Sie die Funktion in Azure, um diese in der Cloud auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ea363-102">In this unit, you publish the function to Azure to run in the cloud.</span></span>

> [!Note]
> <span data-ttu-id="ea363-103">Sie veröffentlichen Ihre Funktion über Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea363-103">You will publish your function from Visual Studio.</span></span> <span data-ttu-id="ea363-104">Dies ist ein guter Einstieg in Proof of Concepts, Prototypen und zum Lernen. Für Apps mit Produktionsqualität sollten Sie diese Methode jedoch **nicht** verwenden.</span><span class="sxs-lookup"><span data-stu-id="ea363-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="ea363-105">Sie sollte eine CI-basierte Bereitstellung verwenden.</span><span class="sxs-lookup"><span data-stu-id="ea363-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="ea363-106">Weitere Informationen zu diesem Thema finden Sie in der [Dokumentation zur Bereitstellung von Azure-Funktionen](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="ea363-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true).</span></span>

## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="ea363-107">Veröffentlichen der App in Azure</span><span class="sxs-lookup"><span data-stu-id="ea363-107">Publishing your app to Azure</span></span>

<span data-ttu-id="ea363-108">Azure-Funktionen können über Visual Studio in Azure veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="ea363-108">Azure functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="ea363-109">Beenden Sie die lokale Azure Functions-Runtime, wenn diese noch von der vorherigen Einheit ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="ea363-109">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="ea363-110">Klicken Sie mit der rechten Maustaste auf die `ImHere.Functions`-App im Projektmappen-Explorer, und klicken Sie dann auf *Veröffentlichen...*.</span><span class="sxs-lookup"><span data-stu-id="ea363-110">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![Veröffentlichen per Rechtsklick über die Funktions-App](../media/8-right-click-publish.png)

1. <span data-ttu-id="ea363-112">Klicken Sie im Dialogfeld **Veröffentlichungsziel auswählen** auf *Azure-Funktions-App*, und klicken Sie bei **Azure App Service** auf *Neu erstellen*.</span><span class="sxs-lookup"><span data-stu-id="ea363-112">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="ea363-113">Klicken Sie auf **Veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="ea363-113">Click **Publish**.</span></span>

    ![Erstellen eines neuen Azure App Service, mit dem veröffentlicht werden soll](../media/8-pick-publish-target.png)

1. <span data-ttu-id="ea363-115">Melden Sie sich mit Ihrem Benutzernamen und Kennwort auf der Registerkarte **Ressourcen** dieser Anweisungen bei Azure an.</span><span class="sxs-lookup"><span data-stu-id="ea363-115">Sign in to Azure using the username and password in the **Resources** tab of these instructions.</span></span> <span data-ttu-id="ea363-116">Wenn Sie diese App lokal und nicht auf einer VM erstellen, melden Sie sich mit Ihrem Azure-Konto an, und erstellen Sie bei Bedarf ein neues über die Links im Dialogfeld.</span><span class="sxs-lookup"><span data-stu-id="ea363-116">If you are building this app locally instead of using the VM, log in with your Azure account, creating a new one if necessary using the links on the dialog.</span></span>

1. <span data-ttu-id="ea363-117">Übernehmen Sie in allen Feldern die Standardwerte, denn so wird die notwendige Infrastruktur zum Ausführen Ihrer Funktions-App erstellt.</span><span class="sxs-lookup"><span data-stu-id="ea363-117">Leave all the values as the defaults, as this will create all the necessary infrastructure to run your Functions app.</span></span>

1. <span data-ttu-id="ea363-118">Klicken Sie auf **Erstellen**, um alle Ressourcen in Azure bereitzustellen und Ihre Azure-Funktions-Apps zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="ea363-118">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![Erstellen des App Service](../media/8-create-app-service.png)

1. <span data-ttu-id="ea363-120">Möglicherweise werden Sie gefragt, ob Sie die Azure Functions-Version in Azure aktualisieren möchten.</span><span class="sxs-lookup"><span data-stu-id="ea363-120">You may be asked if you want to update the functions version on Azure.</span></span> <span data-ttu-id="ea363-121">Wenn dieses Dialogfeld angezeigt wird, wählen Sie **Ja** aus, um sicherzustellen, dass Ihre Funktions-App mit der neuesten Version der Azure Functions-Runtime veröffentlicht wird.</span><span class="sxs-lookup"><span data-stu-id="ea363-121">If this dialog appears, select **Yes** to ensure your function app is published with the latest Azure Functions runtime version.</span></span>
    <span data-ttu-id="ea363-122">![Das Dialogfeld für das Update von Azure Functions](../media/8-update-functions-on-azure.png)</span><span class="sxs-lookup"><span data-stu-id="ea363-122">![The update Azure Functions dialog](../media/8-update-functions-on-azure.png)</span></span>

<span data-ttu-id="ea363-123">Die Bereitstellung dauert einige Minuten.</span><span class="sxs-lookup"><span data-stu-id="ea363-123">Provisioning will take a couple of minutes to complete.</span></span> <span data-ttu-id="ea363-124">Die folgenden Ressourcen werden bereitgestellt:</span><span class="sxs-lookup"><span data-stu-id="ea363-124">The following resources will be provisioned:</span></span>

- <span data-ttu-id="ea363-125">Ein Speicherkonto, um die Dateien zu speichern, die für die Azure-Funktions-App erforderlich sind</span><span class="sxs-lookup"><span data-stu-id="ea363-125">A storage account to store the files needed for the Azure Functions app</span></span>
- <span data-ttu-id="ea363-126">Ein App Service-Plan, um die Computeressourcen zu verwalten, die für die Azure-Funktions-App erforderlich sind</span><span class="sxs-lookup"><span data-stu-id="ea363-126">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
- <span data-ttu-id="ea363-127">Der App Service, der die Azure-Funktion ausführt</span><span class="sxs-lookup"><span data-stu-id="ea363-127">The App Service that runs the Azure function</span></span>

<span data-ttu-id="ea363-128">Die Funktion wird nun veröffentlicht und kann über **https://\<Name_Ihrer_App\>.azurewebsites.net/api/SendLocation** abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="ea363-128">The function will now be published and available to call at **https://\<your-app-name\>.azurewebsites.net/api/SendLocation**.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="ea363-129">Konfigurieren der App</span><span class="sxs-lookup"><span data-stu-id="ea363-129">Configuring your app</span></span>

<span data-ttu-id="ea363-130">Als die Azure-Funktion lokal ausgeführt wurde, wurden Twilio-Anmeldeinformationen verwendet, die in einer `local.settings.json`-Datei gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="ea363-130">When the Azure function was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="ea363-131">Wie der Name erkennen lässt, ist diese Datei für lokale Einstellungen, nicht für Azure-Einstellungen gedacht.</span><span class="sxs-lookup"><span data-stu-id="ea363-131">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="ea363-132">Bevor die Azure-Funktion in Azure aufgerufen werden kann, müssen die Einstellungen `TwilioAccountSid` und `TwilioAuthToken` konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="ea363-132">Before the Azure function can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="ea363-133">Klicken Sie in der Registerkarte „Veröffentlichen“ auf die Option **Anwendungseinstellungen verwalten**.</span><span class="sxs-lookup"><span data-stu-id="ea363-133">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    ![Option „Anwendungseinstellungen verwalten“](../media/8-application-settings-option.png)

1. <span data-ttu-id="ea363-135">Im Dialogfeld **Anwendungseinstellungen** werden die Anwendungseinstellungen mit einem lokalen und einem Remotewert angezeigt. Der lokale Wert stammt dabei aus Ihrer `local.settings.json`-Datei, und der Remotewert wird von Ihrer Funktion verwendet, wenn sie in Azure gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="ea363-135">The **Application Settings** dialog will show application settings with both a local and remote value - the local coming from your `local.settings.json` file, and the remote value is the one your function will use when it is hosted in Azure.</span></span> <span data-ttu-id="ea363-136">Kopieren Sie die Werte aus dem Feld *Lokal* in das Feld *Remote* für die Werte **TwilioAccountSid** und **TwilioAuthToken**.</span><span class="sxs-lookup"><span data-stu-id="ea363-136">Copy the values from the *Local* to the *Remote* boxes for the **TwilioAccountSid** and **TwilioAuthToken** values.</span></span>

    ![Festlegen der Twilio-Anmeldeinformationen in den Anwendungseinstellungen](../media/8-set-creds-in-app-settings.png)

1. <span data-ttu-id="ea363-138">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea363-138">Click **OK**.</span></span> <span data-ttu-id="ea363-139">Dadurch werden die Werte in der Azure-Funktions-App veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="ea363-139">This will publish the values to the Azure functions app.</span></span>

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="ea363-140">Verweisen der mobilen App auf Azure</span><span class="sxs-lookup"><span data-stu-id="ea363-140">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="ea363-141">Kopieren Sie die **Website-URL** von der Registerkarte „Veröffentlichen“ mithilfe der Schaltfläche **In Zwischenablage kopieren**, die sich neben dem Wert befindet.</span><span class="sxs-lookup"><span data-stu-id="ea363-141">From the Publish tab, copy the **Site URL** using the **Copy to clipboard** button next to the value.</span></span>

    ![Kopieren der Website-URL von der Registerkarte „Veröffentlichen“](../media/8-copy-site-url.png)

1. <span data-ttu-id="ea363-143">Öffnen Sie `MainViewModel` über das `ImHere`-Projekt.</span><span class="sxs-lookup"><span data-stu-id="ea363-143">Open the `MainViewModel` from the `ImHere` project.</span></span>

1. <span data-ttu-id="ea363-144">Aktualisieren Sie den Wert des `baseUrl`-Felds auf die Website-URL, die Sie von der Registerkarte „Veröffentlichen“ kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="ea363-144">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="ea363-145">Testen</span><span class="sxs-lookup"><span data-stu-id="ea363-145">Test it out</span></span>

1. <span data-ttu-id="ea363-146">Legen Sie die `ImHere.UWP`-App als Start-App fest, und führen Sie diese aus.</span><span class="sxs-lookup"><span data-stu-id="ea363-146">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

1. <span data-ttu-id="ea363-147">Geben Sie eine Telefonnummer ein, und klicken Sie auf die Schaltfläche **Standort senden**.</span><span class="sxs-lookup"><span data-stu-id="ea363-147">Enter a phone number and click the **Send Location** button.</span></span>

1. <span data-ttu-id="ea363-148">Sie sollten den Standort als SMS-Nachricht erhalten.</span><span class="sxs-lookup"><span data-stu-id="ea363-148">You should receive the location as an SMS message.</span></span>

1. <span data-ttu-id="ea363-149">Wenn der Fehler *Dienst nicht verfügbar* zurückgegeben wird, überprüfen Sie, welche Version des NuGet-Pakets „Microsoft.Azure.WebJobs.Extensions.Twilio“ Ihre Funktions-App verwendet. Es sollte 3.0.0-rc1, nicht 3.0.0 sein.</span><span class="sxs-lookup"><span data-stu-id="ea363-149">If you get back a *Service Unavailable* error, check what version of the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package your functions app is using, it should be 3.0.0-rc1, NOT 3.0.0.</span></span>
1. <span data-ttu-id="ea363-150">Wenn der Fehler *Dienst nicht verfügbar* zurückgegeben wird, überprüfen Sie, welche Version des NuGet-Pakets „Microsoft.Azure.WebJobs.Extensions.Twilio“ Ihre Funktions-App verwendet. Es sollte 3.0.0-rc1, **nicht** 3.0.0 sein.</span><span class="sxs-lookup"><span data-stu-id="ea363-150">If you get back a *Service Unavailable* error, check what version of the "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet package your functions app is using, it should be 3.0.0-rc1, **NOT** 3.0.0.</span></span>

## <a name="summary"></a><span data-ttu-id="ea363-151">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="ea363-151">Summary</span></span>

<span data-ttu-id="ea363-152">In dieser Einheit haben Sie gelernt, wie Sie ein Azure Functions-Projekt über Visual Studio in Azure veröffentlichen und die Anwendungseinstellungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="ea363-152">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>