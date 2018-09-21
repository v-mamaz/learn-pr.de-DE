<span data-ttu-id="6f4a2-101">In dieser Einheit laden Sie Ihre ASP.NET Core-Anwendung in Azure App Service hoch.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-101">In this unit, you'll upload your ASP.NET Core application to Azure App Service.</span></span>

## <a name="create-a-staging-deployment-slot"></a><span data-ttu-id="6f4a2-102">Erstellen eines Stagingbereitstellungsslots</span><span class="sxs-lookup"><span data-stu-id="6f4a2-102">Create a staging deployment slot</span></span>

1. <span data-ttu-id="6f4a2-103">Wechseln Sie zurück zum [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="6f4a2-103">Switch back to the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true).</span></span>

1. <span data-ttu-id="6f4a2-104">Öffnen Sie die zuvor erstellte App Service-Ressource (die Web-App).</span><span class="sxs-lookup"><span data-stu-id="6f4a2-104">Open the App Service resource (the web app) you created previously.</span></span> <span data-ttu-id="6f4a2-105">Sie können sie erneut öffnen, indem Sie unter **Alle Ressourcen** oder in der enthaltenden Ressourcengruppe unter **Ressourcengruppen** nach der App suchen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-105">You can find it again by searching for the app in **All resources** or the containing resource group in **Resource groups**.</span></span>

1. <span data-ttu-id="6f4a2-106">Klicken Sie im linken Navigationsbereich auf das Menüelement **Bereitstellungsslots**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-106">Click the **Deployment slots** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="6f4a2-107">Klicken Sie auf der Seite **Bereitstellungsslots** in der oberen Navigationsleiste der Seite auf die Schaltfläche **Slot hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-107">Inside the **Deployment slots** page, click the **Add Slot** button on the top navigation bar of the deployment slots page.</span></span>

1. <span data-ttu-id="6f4a2-108">Im Azure-Portal wird wie unten gezeigt die Seite **Slot hinzufügen** geöffnet.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-108">The Azure portal opens the **Add a slot** page as shown below.</span></span>

    1. <span data-ttu-id="6f4a2-109">Geben Sie einen Namen für Ihren Bereitstellungsslot ein.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-109">Give your deployment slot a name.</span></span> <span data-ttu-id="6f4a2-110">Verwenden Sie in diesem Fall `staging`.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-110">In this case, use `staging`.</span></span>

    2. <span data-ttu-id="6f4a2-111">Sie haben zwei Möglichkeiten, eine **Konfigurationsquelle** auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-111">To choose a **Configuration Source**, you have two options.</span></span>

        * <span data-ttu-id="6f4a2-112">Sie können sich entscheiden, die Konfigurationselemente eines beliebigen vorhandenen Bereitstellungsslots oder einer in Azure erstellten App Service-App zu klonen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-112">You can choose to clone the configuration elements from any existing deployment slot or App Service app.</span></span>
        * <span data-ttu-id="6f4a2-113">Sie können sich auch gegen das Klonen von Konfigurationselementen entscheiden.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-113">Or you can choose not to clone any configuration elements.</span></span> <span data-ttu-id="6f4a2-114">Wählen Sie die Option **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen) aus.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-114">Select the option **Don't clone configuration from an existing slot**.</span></span>

        <span data-ttu-id="6f4a2-115">Wählen Sie für diesen Bereitstellungsslot die zweite Option aus, **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen).</span><span class="sxs-lookup"><span data-stu-id="6f4a2-115">For this deployment slot, choose the second option: **Don't clone configuration from an existing slot**.</span></span> <span data-ttu-id="6f4a2-116">Sie werden ihn direkt konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-116">You will configure it directly.</span></span>

    ![Screenshot des Azure-Portals mit der Konfiguration für einen neuen Stagingbereitstellungsslot.](../media/7-new-deployment-slot-blade.png)

1. <span data-ttu-id="6f4a2-118">Klicken Sie unten auf der Seite auf die Schaltfläche **OK**, um Ihren neuen Bereitstellungsslot zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-118">Click the **OK** button at the bottom of the page to create your new deployment slot.</span></span>

1. <span data-ttu-id="6f4a2-119">Nachdem der Bereitstellungsslot erfolgreich erstellt wurde, wird im Azure-Portal erneut die Seite **Bereitstellungsslots** Ihrer Web-App angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-119">Once the deployment slot is successfully created, the Azure portal navigates you back to the **Deployment slots** page of your web app.</span></span>

    <span data-ttu-id="6f4a2-120">Sie sehen nun den neuen Bereitstellungsslot, den Sie soeben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-120">Now, you can see the new deployment slot that you have just created.</span></span>

    ![Screenshot des Azure-Portals mit der Seite „Bereitstellungsslots“ und dem neu erstellten Slot.](../media/7-deployment-slot-created.png)

1. <span data-ttu-id="6f4a2-122">Wählen Sie den neuen Bereitstellungsslot aus.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-122">Select the new deployment slot.</span></span>

1. <span data-ttu-id="6f4a2-123">Im Azure-Portal wird die Seite **Übersicht** des neu erstellten Bereitstellungsslots angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-123">The Azure portal navigates to the **Overview** page of the newly created deployment slot.</span></span>

    ![Stagingbereitstellungsslot](../media/7-deployment-slot-staging.png)

    <span data-ttu-id="6f4a2-125">Beachten Sie die **URL** des Stagingbereitstellungsslots.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-125">Notice the **URL** of the staging deployment slot.</span></span> <span data-ttu-id="6f4a2-126">Die URL unterscheidet sich von der zuvor angezeigten URL. Sie enthält den angefügten Slotnamen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-126">It is a different URL from what you saw previously, with the slot name appended.</span></span>

    <span data-ttu-id="6f4a2-127">Ein Bereitstellungsslot wird Azure-intern als vollständige App Service-App behandelt.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-127">A deployment slot is treated as a full App Service app inside Azure.</span></span> <span data-ttu-id="6f4a2-128">Allerdings handelt es sich um einen speziellen Typ, der ein untergeordnetes Element der ursprünglichen App ist und nicht gegen die ursprüngliche App ausgetauscht werden kann.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-128">However, it is a special type that is a child of the original app and can be swapped with the original app.</span></span>

    <span data-ttu-id="6f4a2-129">Wenn Sie auf die **URL** klicken, wird die gleiche Standardseite angezeigt, die Azure für die Bereitstellungsslot-„App“ erstellt hat, als wir die App erstmals im Azure-Portal erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-129">If you click the **URL**, you will see the same default page that Azure created for the deployment slot "app" the first time we created it in the Azure portal.</span></span>

<span data-ttu-id="6f4a2-130">Nachdem der Stagingbereitstellungsslot erfolgreich erstellt wurde, müssen Sie nun **Anmeldeinformationen für die Bereitstellung** konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-130">Now that the staging deployment slot is created successfully, you need to configure **deployment credentials**.</span></span>

## <a name="create-deployment-credentials"></a><span data-ttu-id="6f4a2-131">Erstellen von Anmeldeinformationen für die Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="6f4a2-131">Create deployment credentials</span></span>

<span data-ttu-id="6f4a2-132">In Azure müssen Anmeldeinformationen für die Bereitstellung eingerichtet werden, bevor Sie mit dem eigentlichen Bereitstellungsvorgang beginnen können.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-132">Azure requires deployment credentials to be set up before you can start the actual deployment process.</span></span> <span data-ttu-id="6f4a2-133">Aus diesem Grund lernen Sie, wie Sie Ihre eigenen Anmeldeinformationen für die Bereitstellung erstellen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-133">For that reason, you will learn how to create your own deployment credentials.</span></span>

1. <span data-ttu-id="6f4a2-134">Klicken Sie im linken Navigationsbereich auf das Menüelement **Anmeldeinformationen für die Bereitstellung**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-134">Click the **Deployment credentials** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="6f4a2-135">Das Azure-Portal navigiert wie unten gezeigt zur Seite **Anmeldeinformationen für die Bereitstellung**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-135">The Azure portal navigates to the **Deployment credentials** page as shown below.</span></span>

    <span data-ttu-id="6f4a2-136">Geben Sie einen **Benutzernamen** und ein **Kennwort** Ihrer Wahl ein, und bestätigen Sie nochmals Ihr Kennwort.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-136">Enter a **username** and **password** of your choice, and then confirm your password once again.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6f4a2-137">Stellen Sie sicher, dass Sie Ihren Benutzernamen und Ihr Kennwort nicht vergessen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-137">Make sure you don't forget your username and password!</span></span> <span data-ttu-id="6f4a2-138">Sie werden diese Informationen später benötigen, wenn wir beginnen, Ihren Code in Azure hochzuladen und bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-138">You will need them later when we start uploading and deploying our code to Azure.</span></span>

    ![Screenshot des Azure-Portals mit der Seite „Anmeldeinformationen für die Bereitstellung“ mit Beispielanmeldeinformationen in den erforderlichen Feldern.](../media/7-deployment-credentials.png)

1. <span data-ttu-id="6f4a2-140">Klicken Sie oben auf der Seite **Anmeldeinformationen für die Bereitstellung** auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-140">Click the **Save** button at the top of the **Deployment credentials** page.</span></span>

<span data-ttu-id="6f4a2-141">Nachdem die Anmeldeinformationen für die Bereitstellung erfolgreich erstellt wurden, müssen Sie nun weitere Bereitstellungsoptionen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-141">Now that the deployment credentials are created successfully, you need to configure other deployment options.</span></span>

## <a name="use-a-local-git-repository-as-your-deployment-option"></a><span data-ttu-id="6f4a2-142">Verwenden eines lokalen Git-Repositorys als Bereitstellungsoption</span><span class="sxs-lookup"><span data-stu-id="6f4a2-142">Use a local Git repository as your deployment option</span></span>

<span data-ttu-id="6f4a2-143">Als Nächstes erstellen wir ein lokales Git-Repository in Azure, damit Sie mit dem Hochladen Ihres Codes beginnen können.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-143">Next, we'll create a local Git repository in Azure, so you can start uploading your code.</span></span>

1. <span data-ttu-id="6f4a2-144">Klicken Sie in der „App“ mit dem Bereitstellungsslot **Staging** im linken Navigationsbereich auf das Menüelement **Bereitstellungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-144">Within the **staging** deployment slot "app", click the **Deployment options** menu item on the left-hand navigation.</span></span>

1. <span data-ttu-id="6f4a2-145">Das Azure-Portal navigiert zur Seite **Bereitstellungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-145">The Azure portal navigates to the **Deployment options** page.</span></span>

1. <span data-ttu-id="6f4a2-146">Klicken Sie auf **Quelle auswählen**, um die erforderlichen Einstellungen zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-146">Click on the **Choose Source** to configure the required settings.</span></span>

1. <span data-ttu-id="6f4a2-147">Im Azure-Portal werden die verfügbaren Optionen angezeigt, die Sie konfigurieren und verwenden können.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-147">The Azure portal displays the available options that you can configure and use.</span></span> <span data-ttu-id="6f4a2-148">Wählen Sie in unserem Fall die Option **Lokales Git-Repository** aus.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-148">In our case, choose the **Local Git Repository** option.</span></span>

1. <span data-ttu-id="6f4a2-149">Sie gelangen wieder zur Seite **Bereitstellungsoption** zurück.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-149">You will be returned to the **Deployment option** page.</span></span> <span data-ttu-id="6f4a2-150">Klicken Sie unten auf der Seite auf **OK**, um die Bereitstellungsquelle einzurichten.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-150">Click the **OK** button at the bottom of the page to set up the deployment source.</span></span>

1. <span data-ttu-id="6f4a2-151">Navigieren Sie nun im linken Navigationsbereich zum Abschnitt **Übersicht**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-151">Now, navigate to the **Overview** section on the left-side navigation.</span></span>

    <span data-ttu-id="6f4a2-152">Die wichtige Information, die hier zu beachten ist, ist die **Git Clone-URL**, bei der es sich um die URL des lokalen Git-Repositorys handelt, die Sie als **Remote** für Ihr lokales Anwendungscoderepository verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-152">The important information to note here is the **Git Clone Uri**, which is the local Git repository URL that you will use as a **remote** for your local application code repository.</span></span>

<span data-ttu-id="6f4a2-153">Nun ist es an der Zeit, mit dem Hochladen Ihres Codes in den Stagingbereitstellungsslot zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-153">It is time to start uploading your code to the staging deployment slot.</span></span>

## <a name="set-up-git-on-cloud-shell"></a><span data-ttu-id="6f4a2-154">Einrichten von Git in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="6f4a2-154">Set up git on Cloud Shell</span></span>

<span data-ttu-id="6f4a2-155">Git ist bereits in Azure Cloud Shell installiert, jedoch sollten Sie Ihren Benutzernamen und Ihre E-Mail-Adresse für Ihr Cloud Shell-Konto einrichten.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-155">Git is already installed Azure Cloud Shell but you'll want to set your username and email for your cloud shell account.</span></span>

1. <span data-ttu-id="6f4a2-156">Geben Sie die folgenden Befehle rechts in Cloud Shell ein, und ersetzen Sie die Platzhalter `[your name]` und `[your email]` durch Ihren Namen und Ihre E-Mail-Adresse (ohne Klammern):</span><span class="sxs-lookup"><span data-stu-id="6f4a2-156">In the Cloud Shell on the right, type the following commands, replacing the `[your name]` and `[your email]` placeholders with your own name and email (without the braces):</span></span>

    ```bash
    git config --global user.name "[your name]"
    git config --global user.email "[your email]"
    ```

1. <span data-ttu-id="6f4a2-157">Um sicherzustellen, dass Ihre Daten von Git erfasst wurden, geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-157">To verify that your information has been recorded by Git, type the following command:</span></span>

    ```bash
    cat ~/.gitconfig
    ```

   <span data-ttu-id="6f4a2-158">Folgendes sollte angezeigt werden, einschließlich Ihres Namens und Ihrer E-Mail-Adresse:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-158">You should be seeing the following, with your name and email shown:</span></span>

    ```output
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-code"></a><span data-ttu-id="6f4a2-159">Initialisieren eines lokalen Git-Repositorys für Ihren Code</span><span class="sxs-lookup"><span data-stu-id="6f4a2-159">Initialize a local Git repository for your code</span></span>

<span data-ttu-id="6f4a2-160">Um mit der Verwendung von Git zu beginnen, müssen Sie ein lokales Git-Repository für Ihren.NET Core-Anwendungscode initialisieren.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-160">To start using Git, you need to initialize a local Git repository for your .NET Core application code.</span></span>

1. <span data-ttu-id="6f4a2-161">Stellen Sie sicher, dass Sie im Projektordner sind, den Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-161">Make sure you are in the project folder you created earlier.</span></span>

    ```bash
    cd ~/BestBikeApp/
    ```

1. <span data-ttu-id="6f4a2-162">Verwenden Sie den folgenden Befehl, um ein neues Git-Repository zu initialisieren:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-162">Initialize a new Git repository by issuing the following command:</span></span>

    ```bash
    git init
    ```

    <span data-ttu-id="6f4a2-163">Wenn der Befehl erfolgreich ist, erhalten Sie sinngemäß die folgende Meldung:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-163">If the command is successful, you receive a message like the following:</span></span>

    ```output
    Initialized empty Git repository in /home/{your-user}/BestBikeApp/.git/
    ```

1. <span data-ttu-id="6f4a2-164">Nehmen Sie das Staging aller Anwendungsdateien in Git vor.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-164">Stage all the application files to Git.</span></span>

   <span data-ttu-id="6f4a2-165">Der nächste Schritt besteht darin, Git über Ihre Anwendungsdateien zu informieren.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-165">The next step is to let Git know about your application files.</span></span> <span data-ttu-id="6f4a2-166">Hierzu fügen Sie alle Dateien des Arbeitsverzeichnisses hinzu, sodass sie von Git **bereitgestellt** werden.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-166">Do that by adding all the files of the working directory so that they get **staged** by Git.</span></span> <span data-ttu-id="6f4a2-167">Geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-167">Type the following command:</span></span>

    ```bash
    git add .
    ```

    <span data-ttu-id="6f4a2-168">Der obige Befehl fügt alle durch „.“ dargestellten Dateien zum Stagingstatus von Git hinzu.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-168">The command above adds all files, represented by the ".", to the staging state of Git.</span></span>

1. <span data-ttu-id="6f4a2-169">Nun müssen Sie Ihre Änderungen an Git committen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-169">Now, you need to commit your changes to Git.</span></span>

   <span data-ttu-id="6f4a2-170">Nachdem Sie die Dateien mit Git bereitgestellt haben, müssen Sie Ihre Dateien an den **Git-Commitverlauf** auf Ihrem lokalen Computer committen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-170">Once you stage the files with Git, you need to commit your files to the **Git commit history** on your local machine.</span></span> <span data-ttu-id="6f4a2-171">Hierzu geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-171">You do that by typing the following command:</span></span>

    ```bash
   git commit -m "Initial create"
    ```

   <span data-ttu-id="6f4a2-172">Der `commit`-Befehl akzeptiert das `-m`-Argument, um eine Nachricht mit dem von Ihnen erstellten Commit einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-172">The `commit` command accepts  `-m` argument to include a message with the commit you are creating.</span></span> <span data-ttu-id="6f4a2-173">Wenn Sie später Ihren Code an Azure übertragen, sehen Sie diese Nachricht, die mit diesem konkreten Commit gespeichert wurde.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-173">Later on, when you push your code to Azure, you will be able to see the same message stored with this particular commit.</span></span>

## <a name="add-a-remote-for-the-local-git-repository"></a><span data-ttu-id="6f4a2-174">Hinzufügen eines Remoterepositorys für das lokale Git-Repository</span><span class="sxs-lookup"><span data-stu-id="6f4a2-174">Add a remote for the local Git repository</span></span>

<span data-ttu-id="6f4a2-175">Sie haben nun erfolgreich ein neues lokales Git-Repository initialisiert.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-175">At this point, you have successfully initialized a new local Git repository.</span></span> <span data-ttu-id="6f4a2-176">Außerdem haben Sie alle Ihre Anwendungsdateien an Git committet.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-176">In addition, you've committed all of your application files to Git.</span></span> <span data-ttu-id="6f4a2-177">Nun müssen Sie lediglich noch ein **Remote**repository hinzufügen, um Ihr lokales Git-Repository mit dem in Azure gehosteten Repository zu verbinden.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-177">What remains is to add a **remote** to connect your local Git repository to that hosted on Azure.</span></span>

<span data-ttu-id="6f4a2-178">Hierzu müssen Sie Folgendes durchführen:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-178">To do so, you need to:</span></span>

1. <span data-ttu-id="6f4a2-179">Kopieren Sie die **GIT-Klon-URL**, die Sie weiter oben gesehen haben.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-179">Copy the **Git clone url** that you saw above.</span></span>

1. <span data-ttu-id="6f4a2-180">Sobald Sie sie kopiert haben, navigieren Sie zurück zum Fenster **Terminal**, und führen Sie den folgenden Git-Befehl mit der URL aus:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-180">Once copied, you go back to the **Terminal** window and issue the following Git command with your url:</span></span>

    ```bash
    git remote add origin https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    <span data-ttu-id="6f4a2-181">Mit dem obigen Git-Befehl wird Ihr lokales Git-Repository mit dem in Azure gehosteten Repository verbunden.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-181">The above Git command hooks your local Git repository to the one hosted on Azure.</span></span> <span data-ttu-id="6f4a2-182">Nun ist Push und Pull zwischen dem lokalen Git-Repository und dem Remote-Git-Repository möglich.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-182">Now, you can start pushing and pulling between the local and remote Git repositories!</span></span>

1. <span data-ttu-id="6f4a2-183">Geben Sie zum Überprüfen des obigen Befehls den folgenden Git-Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-183">To verify the above command, type the following Git command:</span></span>

    ```bash
    git remote -v
    ```

    <span data-ttu-id="6f4a2-184">Mit dem obigen Befehl wird die folgende Ausgabe generiert:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-184">The command above generates the following output:</span></span>

    ```output
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a><span data-ttu-id="6f4a2-185">Pushen Ihres Codes in Azure</span><span class="sxs-lookup"><span data-stu-id="6f4a2-185">Push your code to Azure</span></span>

<span data-ttu-id="6f4a2-186">Nachdem Ihr lokales Git-Repository nun mit dem Git-Remoterepository in Azure verbunden ist, entwickeln und erstellen Sie die App und pushen anschließend Ihren Anwendungscode in Azure.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-186">Now that you have your local Git repository hooked to the remote Git repository on Azure, you will develop and build the app, and then push your application code to Azure.</span></span>

1. <span data-ttu-id="6f4a2-187">Geben Sie den folgenden Git-Befehl ein, um Ihren **Haupt**branch in das Git-Remoterepository in Azure zu pushen:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-187">Type the following Git command to push your **master** branch to the remote Git repository on Azure:</span></span>

    ```bash
    git push origin master
    ```

1. <span data-ttu-id="6f4a2-188">Sie werden aufgefordert, das Kennwort einzugeben, das Sie im Abschnitt **Anmeldeinformationen für die Bereitstellung** weiter oben konfiguriert haben.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-188">You will be prompted to enter the password that you have configured in the **Deployment credentials** section above.</span></span> <span data-ttu-id="6f4a2-189">Geben Sie Ihr Kennwort ein, und drücken Sie die Eingabetaste.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-189">Enter your password and hit Enter.</span></span> <span data-ttu-id="6f4a2-190">Git beginnt, Ihre committeten Dateien in das Git-Remoterepository von Azure hochzuladen, das unter dem Stagingbereitstellungsslot konfiguriert wurde.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-190">Git starts uploading your committed files to the Azure remote Git repository configured under the staging deployment slot.</span></span>

## <a name="verify-the-code-is-uploaded-to-azure"></a><span data-ttu-id="6f4a2-191">Bestätigen, dass der Code in Azure hochgeladen wurde</span><span class="sxs-lookup"><span data-stu-id="6f4a2-191">Verify the code is uploaded to Azure</span></span>

1. <span data-ttu-id="6f4a2-192">Wechseln Sie zurück zum Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-192">Switch back to the Azure portal.</span></span>

1. <span data-ttu-id="6f4a2-193">Klicken Sie im linken Navigationsbereich auf das Menüelement **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-193">Click on the **All Resources** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="6f4a2-194">Sie gelangen im Azure-Portal zur Liste aller Ressourcen, die bisher in Azure erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-194">The Azure portal navigates you to the list of all resources created on Azure so far.</span></span>

1. <span data-ttu-id="6f4a2-195">Klicken Sie auf den oben erstellten Stagingslot.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-195">Click on the staging slot created above.</span></span> <span data-ttu-id="6f4a2-196">Denken Sie daran, dass ein Bereitstellungsslot als eine App angesehen wird. Daher wird er unter **Alle Ressourcen** als App Service-Ressource angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-196">Remember, a deployment slot is considered as an app, and hence, it will appear as an App Service resource under **All Resources**.</span></span>

1. <span data-ttu-id="6f4a2-197">Wenn die Seite „Stagingbereitstellungsslot“ angezeigt wird, navigieren Sie zu **Bereitstellungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-197">Once you arrive to the staging deployment slot page, go to **Deployment options**.</span></span>

    <span data-ttu-id="6f4a2-198">Sie sehen, dass Ihr erster Commit, der sich lokal auf Ihrem Computer befindet, jetzt in das Azure-Portal hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-198">You will see that your first commit that you have locally on your machine is now uploaded to the Azure portal.</span></span>

    <span data-ttu-id="6f4a2-199">Wenn Sie Ihren Code lokal in das Git-Remoterepository in App Service pushen, zeichnet Azure diesen Vorgang auf.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-199">When you push your code locally to the remote Git repository in App Service, Azure records this operation.</span></span>

    <span data-ttu-id="6f4a2-200">Jedes Mal, wenn Sie Ihren Code in Azure pushen, wird ein neuer Datensatz zusammen mit der Nachricht angezeigt, die Sie eingeben, wenn Sie Ihre Änderungen lokal auf Ihrem Computer committen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-200">Every time you push your code to Azure, you will see a new record, together with the message that you type when committing your changes locally on your machine.</span></span>

    ![Screenshot des Azure-Portals mit einer kürzlich erfolgten Bereitstellung im Git-Repository auf der Seite „Entwicklungsoptionen“.](../media/7-staging-deployment-slot-after-uploading-files.png)

1. <span data-ttu-id="6f4a2-202">Sehen wir uns nun die **Stagingslot**-URL an.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-202">Let's visit the **staging slot** URL.</span></span> <span data-ttu-id="6f4a2-203">Auf die URL wurde bereits oben eingegangen. Sollten Sie jedoch Ihre URL vergessen haben, können Sie stets zur Seite **Übersicht** des Stagingbereitstellungsslots wechseln und von dort die URL übernehmen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-203">The URL was mentioned above, however, if you forget that URL, you can always go to the **Overview** page of the staging deployment slot and pick up the URL.</span></span>

1. <span data-ttu-id="6f4a2-204">Geben Sie die folgende URL in die Adressleiste Ihres Browsers ein: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="6f4a2-204">Type the following URL in your browser address bar: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).</span></span>

    ![Screenshot einer Webbrowseransicht der Website des Stagingbereitstellungsslots.](../media/7-staging-slot-hosted-online.png)

<span data-ttu-id="6f4a2-206">Sie haben erfolgreich Ihre lokalen Anwendungsdateien in den Stagingbereitstellungsslot in Azure hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-206">You have successfully uploaded your local application files to the staging deployment slot on Azure.</span></span>

## <a name="swapping-the-staging-and-production-deployment-slots"></a><span data-ttu-id="6f4a2-207">Austauschen von Staging- und Produktionsbereitstellungsslots</span><span class="sxs-lookup"><span data-stu-id="6f4a2-207">Swapping the staging and production deployment slots</span></span>

<span data-ttu-id="6f4a2-208">Nachdem die Anwendung nun in dem Stagingbereitstellungsslot ausgeführt wird, der in Azure gehostet wird, ist es Zeit, diesen Slot gegen den Produktionsbereitstellungsslot austauschen.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-208">Now that the application is up and running on the staging deployment slot hosted on Azure, it is time to swap this slot with the production one.</span></span> <span data-ttu-id="6f4a2-209">Gehen Sie dazu folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="6f4a2-209">To do so, follow these steps:</span></span>

1. <span data-ttu-id="6f4a2-210">Navigieren Sie zur Seite der ursprünglichen App, die Sie zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-210">Navigate to the original app page created earlier.</span></span> <span data-ttu-id="6f4a2-211">Sie finden die ursprüngliche Web-App auf der Seite **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-211">You can find the original web app from the **All resources** page.</span></span>

1. <span data-ttu-id="6f4a2-212">Klicken Sie im linken Navigationsbereich auf das Menüelement **Bereitstellungsslots**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-212">Click the **Deployment slots** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="6f4a2-213">Klicken Sie oben auf der Seite auf die Schaltfläche **Austauschen**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-213">Click on the **Swap** button at the top of the page.</span></span>

1. <span data-ttu-id="6f4a2-214">Sie gelangen im Azure-Portal zur Seite **Austauschen**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-214">The Azure portal navigates you to the **Swap** page.</span></span>

1. <span data-ttu-id="6f4a2-215">Wählen Sie für das Feld **Austauschen** die Option **Austauschen** aus.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-215">For the **Swap** field, select **Swap**.</span></span>

1. <span data-ttu-id="6f4a2-216">Wählen Sie für das Feld **Quelle** die Option **Staging** aus.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-216">For the **Source** field, select **Staging**.</span></span>

1. <span data-ttu-id="6f4a2-217">Wählen Sie für das Feld **Ziel** die Option **Produktion** aus.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-217">For the **Destination** field, select **Production**.</span></span>

    ![Screenshot des Azure-Portals mit der Seite „Austauschen“ des Bereitstellungsslots.](../media/7-swap-blade.png)

1. <span data-ttu-id="6f4a2-219">Klicken Sie am unteren Rand der Seite auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-219">Click on the **OK** button at the bottom of the page.</span></span>

1. <span data-ttu-id="6f4a2-220">Azure beginnt mit dem Austauschvorgang.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-220">Azure starts the swapping process.</span></span> <span data-ttu-id="6f4a2-221">In der Regel beansprucht dieser Vorgang je nach Größe der ausgetauschten Web-App einige Sekunden.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-221">Usually, this operation takes a few seconds, depending on the size of the web app being swapped.</span></span>

1. <span data-ttu-id="6f4a2-222">Nach dem Vorgang können Sie die URL der Web-App öffnen. Sie finden sie im Portal auf der Übersichtsseite für Ihren App-Dienst: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="6f4a2-222">Once the operation ends, visit your web app URL; you can find it in the Overview page for your app service in the portal: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).</span></span>

    ![Screenshot mit einer Webbrowseransicht des früheren Stagingbereitstellungsslots, der jetzt als primäre Web-App gehostet wird.](../media/7-web-app-page.png)

    <span data-ttu-id="6f4a2-224">Der Austauschvorgang war erfolgreich!</span><span class="sxs-lookup"><span data-stu-id="6f4a2-224">The swapping operation has been successful!</span></span> <span data-ttu-id="6f4a2-225">Sie sehen nun, dass der Code, den Sie in den Stagingbereitstellungsslot hochgeladen haben, auch im Produktionsslot gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-225">You can now see the code that you uploaded to the staging deployment slot also being hosted on the production slot.</span></span>

1. <span data-ttu-id="6f4a2-226">Wechseln Sie nun zur URL des Stagingslots: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="6f4a2-226">Now, visit the URL of the staging slot: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).</span></span>

    ![Screenshot mit einer Webbrowseransicht des zuvor primären Bereitstellungsslots, der jetzt als Stagingbereitstellungsslot-Web-App gehostet wird.](../media/7-staging-after-swapping.png)

    <span data-ttu-id="6f4a2-228">Der Stagingbereitstellungsslot stellt jetzt die ursprünglichen HTML-Standarddateien bereit, die zuvor vom Produktionsslot bereitgestellt wurden.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-228">The staging deployment slot now serves the original, default HTML files that were previously served from the production slot.</span></span>

<span data-ttu-id="6f4a2-229">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="6f4a2-229">Congratulations!</span></span> <span data-ttu-id="6f4a2-230">Sie haben Ihren Anwendungscode erfolgreich in Azure hochgeladen und die Bereitstellungsslots getauscht.</span><span class="sxs-lookup"><span data-stu-id="6f4a2-230">You have successfully uploaded your application code to Azure and swapped deployment slots.</span></span>
