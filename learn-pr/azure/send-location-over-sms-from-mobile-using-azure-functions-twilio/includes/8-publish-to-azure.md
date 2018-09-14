<span data-ttu-id="ec26f-101">Die App und Azure-Funktion sind nun vollständig und werden lokal ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="ec26f-101">The app and Azure Function are now complete and running locally.</span></span> <span data-ttu-id="ec26f-102">In dieser Einheit veröffentlichen Sie die Funktion in Azure, um diese in der Cloud auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ec26f-102">In this unit, you publish the function to Azure to run in the cloud.</span></span>

> <span data-ttu-id="ec26f-103">In dieser Einheit veröffentlichen Sie Ihre Funktion über Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec26f-103">In this unit, you will publish your function from Visual Studio.</span></span> <span data-ttu-id="ec26f-104">Dies ist ein guter Einstieg in Proof of Concepts, Prototypen und zum Lernen. Für Apps mit Produktionsqualität sollten Sie diese Methode jedoch **nicht** verwenden.</span><span class="sxs-lookup"><span data-stu-id="ec26f-104">This is a great way to get started for proof-of-concepts, prototypes, and learning, but for a production-quality app you should **not** use this method.</span></span> <span data-ttu-id="ec26f-105">Sie sollte eine CI-basierte Bereitstellung verwenden.</span><span class="sxs-lookup"><span data-stu-id="ec26f-105">You should use some form of CI-based deployment.</span></span> <span data-ttu-id="ec26f-106">Weitere Informationen zu diesem Thema finden Sie in der [Dokumentation zur Bereitstellung von Azure-Funktionen](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span><span class="sxs-lookup"><span data-stu-id="ec26f-106">You can read more about doing this in the [Azure Functions Deployment docs](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).</span></span>
>

## <a name="publishing-your-app-to-azure"></a><span data-ttu-id="ec26f-107">Veröffentlichen der App in Azure</span><span class="sxs-lookup"><span data-stu-id="ec26f-107">Publishing your app to Azure</span></span>

<span data-ttu-id="ec26f-108">Azure-Funktionen können über Visual Studio in Azure veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="ec26f-108">Azure functions can be published to Azure from inside Visual Studio.</span></span>

1. <span data-ttu-id="ec26f-109">Beenden Sie die lokale Azure Functions-Runtime, wenn diese noch von der vorherigen Einheit ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="ec26f-109">Stop the local Azure Functions runtime if it's still running from the previous unit.</span></span>

1. <span data-ttu-id="ec26f-110">Klicken Sie mit der rechten Maustaste auf die `ImHere.Functions`-App im Projektmappen-Explorer, und klicken Sie dann auf *Veröffentlichen...*.</span><span class="sxs-lookup"><span data-stu-id="ec26f-110">Right-click on the `ImHere.Functions` app in the solution explorer and select *Publish...*.</span></span>

    ![Veröffentlichen per Rechtsklick über die Funktions-App](../media-drafts/8-right-click-publish.png)

1. <span data-ttu-id="ec26f-112">Klicken Sie im Dialogfeld **Veröffentlichungsziel auswählen** auf *Azure-Funktions-App*, und klicken Sie bei **Azure App Service** auf *Neu erstellen*.</span><span class="sxs-lookup"><span data-stu-id="ec26f-112">From the **Pick a publish target** dialog, select *Azure Function App*, and for **Azure App Service**, select *Create New*.</span></span> <span data-ttu-id="ec26f-113">Klicken Sie auf **Veröffentlichen**.</span><span class="sxs-lookup"><span data-stu-id="ec26f-113">Click **Publish**.</span></span>

    ![Erstellen eines neuen Azure App Service, in den veröffentlicht werden soll](../media-drafts/8-pick-publish-target.png)

1. <span data-ttu-id="ec26f-115">Wählen Sie in der Dropdownliste in der oberen rechten Ecke Ihr Azure-Konto aus, wenn Sie mehrere Azure-Konten besitzen und nicht das richtige Konto ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="ec26f-115">Select your Azure account from the drop-down in the top-right corner; if you have more than one Azure accounts and the right one isn't selected.</span></span>

1. <span data-ttu-id="ec26f-116">Benennen Sie Ihre Funktions-App.</span><span class="sxs-lookup"><span data-stu-id="ec26f-116">Give your Functions app a name.</span></span> <span data-ttu-id="ec26f-117">Dieser Name muss für alle Funktions-Apps in Azure global eindeutig sein, also verwenden Sie einen Namen wie „ImHere-\<IhrName\>“.</span><span class="sxs-lookup"><span data-stu-id="ec26f-117">This name needs to be globally unique across all the Functions apps in the whole of Azure, so use something like "ImHere-\<YourName\>".</span></span>

1. <span data-ttu-id="ec26f-118">Wählen Sie das Abonnement aus, unter dem Sie die Funktions-App erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="ec26f-118">Select the subscription you want to create this Functions app under.</span></span>

1. <span data-ttu-id="ec26f-119">Erstellen Sie eine neue Ressourcengruppe für diese Funktions-App, indem Sie auf die Schaltfläche **Neu...** neben dem Dropdownmenü **Ressourcengruppe** klicken und dieser einen Namen wie „ImHere“ geben.</span><span class="sxs-lookup"><span data-stu-id="ec26f-119">Create a new resource group for this Functions app by clicking the **New...** button next to the **Resource Group** drop-down and giving it a name such as "ImHere".</span></span> <span data-ttu-id="ec26f-120">Die Namen von Ressourcengruppen müssen nur in Ihrem Abonnement, nicht global in Azure eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="ec26f-120">Resource group names need to be unique to your subscription, not globally unique across Azure.</span></span> <span data-ttu-id="ec26f-121">Klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec26f-121">Then, click **OK**.</span></span>

    ![Erstellen einer neuen Ressourcengruppe](../media-drafts/8-create-new-resource-group.png)

   <span data-ttu-id="ec26f-123">Das Erstellen einer neuen Ressourcengruppe erleichtert später die Bereinigung.</span><span class="sxs-lookup"><span data-stu-id="ec26f-123">Creating a new resource group makes it easier to clean up later.</span></span> <span data-ttu-id="ec26f-124">Sie können die Ressourcengruppe löschen und wissen, dass alle für die Funktions-App erstellten Elemente gleichzeitig gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="ec26f-124">You can delete the resource group and know that everything you've created for this Functions app will all be deleted at the same time.</span></span>

1. <span data-ttu-id="ec26f-125">Erstellen Sie einen neuen Hostingplan, indem Sie auf die Schaltfläche **Neu...** neben dem Dropdownmenü **Hostingplan** klicken.</span><span class="sxs-lookup"><span data-stu-id="ec26f-125">Create a new hosting plan by clicking the **New...** button next to the **Hosting Plan** drop-down.</span></span> <span data-ttu-id="ec26f-126">Der Name des App Service-Plans wird standardmäßig auf den Namen Ihrer App mit „Plan“ am Ende festgelegt.</span><span class="sxs-lookup"><span data-stu-id="ec26f-126">The App Service plan name will default to your app name with "Plan" on the end.</span></span> <span data-ttu-id="ec26f-127">Legen Sie den **Standort** auf den nächstgelegenen Standort fest, und stellen Sie sicher, dass **Größe** auf „Verbrauch“ festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="ec26f-127">Set the **Location** to the closest location to you and make sure **Size** is set to consumption.</span></span> <span data-ttu-id="ec26f-128">Klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec26f-128">Then, click **OK**.</span></span>

    ![Konfigurieren des Hostingplans](../media-drafts/8-configure-hosting-plan.png)

1. <span data-ttu-id="ec26f-130">Erstellen Sie ein neues Speicherkonto, indem Sie auf die Schaltfläche **Neu...** neben dem Dropdownmenü **Speicherkonto** klicken.</span><span class="sxs-lookup"><span data-stu-id="ec26f-130">Create a new storage account by clicking the **New...** button next to the **Storage Account** drop-down.</span></span> <span data-ttu-id="ec26f-131">Ein Standardname wird bereitgestellt, also behalten Sie die Standardwerte bei, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec26f-131">A default name will be provided, so keep all the default values and click **OK**.</span></span>

    ![Erstellen eines Speicherkontos](../media-drafts/8-create-storage-account.png)

1. <span data-ttu-id="ec26f-133">Klicken Sie auf **Erstellen**, um alle Ressourcen in Azure bereitzustellen und Ihre Azure-Funktions-Apps zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="ec26f-133">Click **Create** to provision all the resources on Azure and publish your Azure Functions app.</span></span>

    ![Erstellen des App Service](../media-drafts/8-create-app-service.png)

<span data-ttu-id="ec26f-135">Die Bereitstellung dauert einige Minuten.</span><span class="sxs-lookup"><span data-stu-id="ec26f-135">Provisioning will take a couple of minutes or so to run.</span></span> <span data-ttu-id="ec26f-136">Folgende Ressourcen werden bereitgestellt:</span><span class="sxs-lookup"><span data-stu-id="ec26f-136">The following resources will be provisioned:</span></span>

- <span data-ttu-id="ec26f-137">Ein Speicherkonto, um die Dateien zu speichern, die für die Azure-Funktions-App erforderlich sind</span><span class="sxs-lookup"><span data-stu-id="ec26f-137">A storage account to store the files needed for the Azure Functions app</span></span>
- <span data-ttu-id="ec26f-138">Ein App Service-Plan, um die Computeressourcen zu verwalten, die für die Azure-Funktions-App erforderlich sind</span><span class="sxs-lookup"><span data-stu-id="ec26f-138">An App Service plan to manage the compute resources needed by the Azure Functions app</span></span>
- <span data-ttu-id="ec26f-139">Der App Service, der die Azure-Funktion ausführt</span><span class="sxs-lookup"><span data-stu-id="ec26f-139">The App Service that runs the Azure function</span></span>

<span data-ttu-id="ec26f-140">Die Funktion wird nun veröffentlicht und kann über https://<Name_Ihrer_App>.azurewebsites.net/api/SendLocation abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="ec26f-140">The function will now be published and available to call at https://<your-app-name>.azurewebsites.net/api/SendLocation.</span></span>

## <a name="configuring-your-app"></a><span data-ttu-id="ec26f-141">Konfigurieren der App</span><span class="sxs-lookup"><span data-stu-id="ec26f-141">Configuring your app</span></span>

<span data-ttu-id="ec26f-142">Als die Azure-Funktion lokal ausgeführt wurde, wurden Twilio-Anmeldeinformationen verwendet, die in einer `local.settings.json`-Datei gespeichert wurden.</span><span class="sxs-lookup"><span data-stu-id="ec26f-142">When the Azure function was running locally, it was using Twilio credentials that were stored in a `local.settings.json` file.</span></span> <span data-ttu-id="ec26f-143">Wie der Name erkennen lässt, ist diese Datei für lokale Einstellungen, nicht für Azure-Einstellungen gedacht.</span><span class="sxs-lookup"><span data-stu-id="ec26f-143">As the name suggests, this file is for local settings, not Azure settings.</span></span> <span data-ttu-id="ec26f-144">Bevor die Azure-Funktion in Azure aufgerufen werden kann, müssen die Einstellungen `TwilioAccountSid` und `TwilioAuthToken` konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="ec26f-144">Before the Azure function can be called inside Azure, the `TwilioAccountSid` and `TwilioAuthToken` settings need to be configured.</span></span>

1. <span data-ttu-id="ec26f-145">Klicken Sie in der Registerkarte „Veröffentlichen“ auf die Option **Anwendungseinstellungen verwalten**.</span><span class="sxs-lookup"><span data-stu-id="ec26f-145">From the Publish tab, click the **Manage Application Settings** option.</span></span>

    ![Option „Anwendungseinstellungen verwalten“](../media-drafts/8-application-settings-option.png)

1. <span data-ttu-id="ec26f-147">Klicken Sie auf die Schaltfläche **Hinzufügen**, um eine neue Einstellung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="ec26f-147">Click the **Add** button to add a new setting.</span></span> <span data-ttu-id="ec26f-148">Nennen Sie diese „TwilioAccountSid“, und legen Sie den Wert auf die SID Ihres Twilio-Kontos fest.</span><span class="sxs-lookup"><span data-stu-id="ec26f-148">Name it "TwilioAccountSid" and set the value to your Twilio account SID.</span></span> <span data-ttu-id="ec26f-149">Wiederholen Sie diesen Schritt für Ihr Authentifizierungstoken, indem Sie den Namen „TwilioAuthToken“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="ec26f-149">Repeat this step for your Auth Token using the name "TwilioAuthToken".</span></span>

    ![Festlegen der Twilio-Anmeldeinformationen in den Anwendungseinstellungen](../media-drafts/8-set-creds-in-app-settings.png)

1. <span data-ttu-id="ec26f-151">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec26f-151">Click **OK**.</span></span>

1. <span data-ttu-id="ec26f-152">Klicken Sie auf **Veröffentlichen**, um die Azure-Funktions-App mit den neuen Anwendungseinstellungen erneut zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="ec26f-152">Click **Publish** to republish the Azure Functions app with the new application settings.</span></span>

    ![Schaltfläche „Veröffentlichen“](../media-drafts/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a><span data-ttu-id="ec26f-154">Verweisen der mobilen App auf Azure</span><span class="sxs-lookup"><span data-stu-id="ec26f-154">Pointing the mobile app to Azure</span></span>

1. <span data-ttu-id="ec26f-155">Kopieren Sie die **Website-URL** von der Registerkarte „Veröffentlichen“ mithilfe der Schaltfläche zum Kopieren, die sich neben dem Wert befindet.</span><span class="sxs-lookup"><span data-stu-id="ec26f-155">From the Publish tab, copy the **Site URL** using the copy button next to the value.</span></span>

    ![Kopieren der Website-URL von der Registerkarte „Veröffentlichen“](../media-drafts/8-copy-site-url.png)

1. <span data-ttu-id="ec26f-157">Öffnen Sie `MainViewModel` über das `ImHere`-Projekt.</span><span class="sxs-lookup"><span data-stu-id="ec26f-157">Open the `MainViewModel` from the `ImHere` project.</span></span>

1. <span data-ttu-id="ec26f-158">Aktualisieren Sie den Wert des `baseUrl`-Felds, damit dieser der Website-URL entspricht, die Sie von der Registerkarte „Veröffentlichen“ kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="ec26f-158">Update the value of the `baseUrl` field to be the site URL copied from the Publish tab.</span></span>

1. <span data-ttu-id="ec26f-159">Ändern Sie das Protokoll für diesen Wert von `http` in `https`.</span><span class="sxs-lookup"><span data-stu-id="ec26f-159">Change the protocol for this value from `http` to `https`.</span></span> <span data-ttu-id="ec26f-160">Die Website-URL wird immer mit HTTP bereitgestellt, Sie müssen jedoch HTTPS verwenden, um eine Azure-Funktion aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="ec26f-160">The site URL is always given using HTTP, but you have to use HTTPS to call an Azure function.</span></span>

## <a name="test-it-out"></a><span data-ttu-id="ec26f-161">Testen</span><span class="sxs-lookup"><span data-stu-id="ec26f-161">Test it out</span></span>

1. <span data-ttu-id="ec26f-162">Legen Sie die `ImHere.UWP`-App als Start-App fest, und führen Sie diese aus.</span><span class="sxs-lookup"><span data-stu-id="ec26f-162">Set the `ImHere.UWP` app as the startup app and run it.</span></span>

1. <span data-ttu-id="ec26f-163">Geben Sie eine Telefonnummer ein, und klicken Sie auf die Schaltfläche **Standort senden**.</span><span class="sxs-lookup"><span data-stu-id="ec26f-163">Enter a phone number and click the **Send Location** button.</span></span>

1. <span data-ttu-id="ec26f-164">Sie sollten den Standort als SMS-Nachricht erhalten.</span><span class="sxs-lookup"><span data-stu-id="ec26f-164">You should receive the location as an SMS message.</span></span>

## <a name="summary"></a><span data-ttu-id="ec26f-165">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="ec26f-165">Summary</span></span>

<span data-ttu-id="ec26f-166">In dieser Einheit haben Sie gelernt, wie Sie ein Azure Functions-Projekt über Visual Studio in Azure veröffentlichen und die Anwendungseinstellungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="ec26f-166">In this unit, you learned how to publish an Azure Functions project to Azure from inside Visual Studio and configure application settings.</span></span>