<span data-ttu-id="352a3-101">In dieser Einheit laden Sie Ihre ASP.NET Core-Anwendung in eine Azure-Web-App hoch.</span><span class="sxs-lookup"><span data-stu-id="352a3-101">In this unit, you'll upload your ASP.NET Core application to an Azure Web App.</span></span>

## <a name="create-a-staging-deployment-slot"></a><span data-ttu-id="352a3-102">Erstellen eines Stagingbereitstellungsslots</span><span class="sxs-lookup"><span data-stu-id="352a3-102">Create a staging deployment slot</span></span>

1. <span data-ttu-id="352a3-103">Öffnen Sie die zuvor erstellte Web-App-Ressource.</span><span class="sxs-lookup"><span data-stu-id="352a3-103">Open the Web App resource you created previously.</span></span> <span data-ttu-id="352a3-104">Wenn Sie ihr Ressourcenblatt geschlossen haben, können Sie es wiederfinden, indem Sie unter **Alle Ressourcen** oder in der enthaltenden Ressourcengruppe unter **Ressourcengruppen** nach der App suchen.</span><span class="sxs-lookup"><span data-stu-id="352a3-104">If you have closed its resource blade, you can find it again by searching for the app in **All resources** or the containing resource group in **Resource groups**.</span></span>

1. <span data-ttu-id="352a3-105">Klicken Sie im linken Navigationsbereich auf das Menüelement **Bereitstellungsslots**.</span><span class="sxs-lookup"><span data-stu-id="352a3-105">Click the **Deployment slots** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="352a3-106">Klicken Sie auf dem Blatt **Bereitstellungsslots** in der oberen Navigationsleiste des Blatts auf die Schaltfläche **Slot hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="352a3-106">Inside the **Deployment slots** blade, click the **Add Slot** button on the top navigation bar of the deployment slots blade.</span></span>

1. <span data-ttu-id="352a3-107">Im Azure-Portal wird das Blatt **Slot hinzufügen** geöffnet, wie unten gezeigt.</span><span class="sxs-lookup"><span data-stu-id="352a3-107">The Azure portal opens the **Add a slot** blade as shown below.</span></span>

    1. <span data-ttu-id="352a3-108">Geben Sie einen Namen für Ihren Bereitstellungsslot ein.</span><span class="sxs-lookup"><span data-stu-id="352a3-108">Give your deployment slot a name.</span></span> <span data-ttu-id="352a3-109">Verwenden Sie in diesem Fall `staging`.</span><span class="sxs-lookup"><span data-stu-id="352a3-109">In this case, use `staging`.</span></span>

    2. <span data-ttu-id="352a3-110">Sie haben zwei Möglichkeiten, eine **Konfigurationsquelle** auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="352a3-110">To choose a **Configuration Source**, you have two options.</span></span>

        * <span data-ttu-id="352a3-111">Sie können sich entscheiden, die Konfigurationselemente eines beliebigen vorhandenen Bereitstellungsslots oder einer in Azure erstellten Web-App zu klonen.</span><span class="sxs-lookup"><span data-stu-id="352a3-111">You can choose to clone the configuration elements from any existing deployment slot or Web App created on Azure.</span></span>
        * <span data-ttu-id="352a3-112">Oder Sie können sich gegen das Klonen von Konfigurationselementen entscheiden.</span><span class="sxs-lookup"><span data-stu-id="352a3-112">Or you can choose not to clone any configuration elements.</span></span> <span data-ttu-id="352a3-113">Wählen Sie die Option **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen) aus.</span><span class="sxs-lookup"><span data-stu-id="352a3-113">Select the option **Don't clone configuration from an existing slot**.</span></span>

        <span data-ttu-id="352a3-114">Wählen Sie für diesen Bereitstellungsslot die zweite Option aus, **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen).</span><span class="sxs-lookup"><span data-stu-id="352a3-114">For this deployment slot, choose the second option: **Don't clone configuration from an existing slot**.</span></span> <span data-ttu-id="352a3-115">Sie werden ihn direkt konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="352a3-115">You will configure it directly.</span></span>

    ![Screenshot des Azure-Portals mit der Konfiguration für einen neuen Stagingbereitstellungsslot.](../media/7-new-deployment-slot-blade.png)

1. <span data-ttu-id="352a3-117">Klicken Sie unten auf dem Blatt auf die Schaltfläche **OK**, um Ihren neuen Bereitstellungsslot zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="352a3-117">Click the **OK** button at the bottom of the blade to create your new deployment slot.</span></span>

1. <span data-ttu-id="352a3-118">Nachdem der Bereitstellungsslot erfolgreich erstellt wurde, wird im Azure-Portal wieder das Blatt **Bereitstellungsslots** Ihrer Web-App angezeigt.</span><span class="sxs-lookup"><span data-stu-id="352a3-118">Once the deployment slot is successfully created, the Azure portal navigates you back to the **Deployment slots** blade of your web app.</span></span>

    <span data-ttu-id="352a3-119">Sie sehen nun den neuen Bereitstellungsslot, den Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="352a3-119">Now, you can see the new deployment slot that you have just created.</span></span>

    ![Screenshot des Azure-Portals mit dem Blatt „Slots“ und dem neu erstellten Slot.](../media/7-deployment-slot-created.png)

1. <span data-ttu-id="352a3-121">Wählen Sie den neuen Bereitstellungsslot aus.</span><span class="sxs-lookup"><span data-stu-id="352a3-121">Select the new deployment slot.</span></span>

1. <span data-ttu-id="352a3-122">Im Azure-Portal wird die Seite **Übersicht** des neu erstellten Bereitstellungsslots angezeigt.</span><span class="sxs-lookup"><span data-stu-id="352a3-122">The Azure portal navigates to the **Overview** page of the newly created deployment slot.</span></span>

    ![Stagingbereitstellungsslot](../media/7-deployment-slot-staging.png)

    <span data-ttu-id="352a3-124">Beachten Sie die **URL** des Stagingbereitstellungsslots.</span><span class="sxs-lookup"><span data-stu-id="352a3-124">Notice the **URL** of the staging deployment slot.</span></span> <span data-ttu-id="352a3-125">Die URL unterscheidet sich von der zuvor angezeigten, sie enthält den angefügten Slotnamen.</span><span class="sxs-lookup"><span data-stu-id="352a3-125">It is a different URL from what you saw previously, with the slot name appended.</span></span>

    <span data-ttu-id="352a3-126">Ein Bereitstellungsslot wird Azure-intern als vollständige Web-App behandelt.</span><span class="sxs-lookup"><span data-stu-id="352a3-126">A deployment slot is treated as a full Web App inside Azure.</span></span> <span data-ttu-id="352a3-127">Allerdings handelt es sich um einen speziellen Typ, der ein untergeordnetes Element der ursprünglichen Web-App ist und nicht gegen die ursprüngliche Web-App ausgetauscht werden kann.</span><span class="sxs-lookup"><span data-stu-id="352a3-127">However, it is a special type that is a child of the original web app and can be swapped with the original web app.</span></span>

    <span data-ttu-id="352a3-128">Wenn Sie auf die **URL** klicken, sehen Sie dieselbe Standardseite, die Azure für die Web-App erstellt hat, als wir die App erstmals im Azure-Portal erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="352a3-128">If you click the **URL**, you will see the same default page that Azure created for the web app the first time we created it in the Azure portal.</span></span>

<span data-ttu-id="352a3-129">Nachdem der Stagingbereitstellungsslot erfolgreich erstellt wurde, müssen Sie nun **Anmeldeinformationen für die Bereitstellung** konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="352a3-129">Now that the staging deployment slot is created successfully, you need to configure **deployment credentials**.</span></span>

## <a name="create-deployment-credentials"></a><span data-ttu-id="352a3-130">Erstellen von Anmeldeinformationen für die Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="352a3-130">Create deployment credentials</span></span>

<span data-ttu-id="352a3-131">In Azure müssen Anmeldeinformationen für die Bereitstellung eingerichtet werden, bevor Sie mit dem eigentlichen Bereitstellungsvorgang beginnen können.</span><span class="sxs-lookup"><span data-stu-id="352a3-131">Azure requires deployment credentials to be set up before you can start the actual deployment process.</span></span> <span data-ttu-id="352a3-132">Aus diesem Grund lernen Sie, wie Sie Ihre eigenen Anmeldeinformationen für die Bereitstellung erstellen.</span><span class="sxs-lookup"><span data-stu-id="352a3-132">For that reason, you will learn how to create your own deployment credentials.</span></span>

1. <span data-ttu-id="352a3-133">Klicken Sie im linken Navigationsbereich auf das Menüelement **Anmeldeinformationen für Bereitstellung**.</span><span class="sxs-lookup"><span data-stu-id="352a3-133">Click the **Deployment credentials** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="352a3-134">Das Azure-Portal navigiert wie unten gezeigt zum Blatt **Anmeldeinformationen für Bereitstellung**.</span><span class="sxs-lookup"><span data-stu-id="352a3-134">The Azure portal navigates to the **Deployment credentials** blade as shown below.</span></span>

    <span data-ttu-id="352a3-135">Geben Sie einen **Benutzernamen** und ein **Kennwort** Ihrer Wahl ein, und bestätigen Sie nochmals Ihr Kennwort.</span><span class="sxs-lookup"><span data-stu-id="352a3-135">Enter a **username** and **password** of your choice, and then confirm your password once again.</span></span>

    > [!NOTE]
    > <span data-ttu-id="352a3-136">Notieren Sie sich unbedingt Ihren Benutzernamen und das Kennwort, damit Sie beides nicht vergessen!</span><span class="sxs-lookup"><span data-stu-id="352a3-136">Make sure you write down your username and password so that you don't forget them!</span></span> <span data-ttu-id="352a3-137">Sie werden diese Informationen später benötigen, wenn wir beginnen, Ihren Code in Azure hochzuladen und bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="352a3-137">You will need them later when we start uploading and deploying our code to Azure.</span></span>

    ![Screenshot des Azure-Portals mit dem Blatt „Anmeldeinformationen für die Bereitstellung“ mit Beispielanmeldeinformationen in den erforderlichen Feldern.](../media/7-deployment-credentials.png)

1. <span data-ttu-id="352a3-139">Klicken Sie oben auf dem Blatt **Anmeldeinformationen für die Bereitstellung** auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="352a3-139">Click the **Save** button at the top of the **Deployment credentials** blade.</span></span>

<span data-ttu-id="352a3-140">Nachdem die Anmeldeinformationen für die Bereitstellung erfolgreich erstellt wurden, müssen Sie nun weitere Bereitstellungsoptionen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="352a3-140">Now that the deployment credentials are created successfully, you need to configure other deployment options.</span></span>

## <a name="use-a-local-git-repository-as-your-deployment-option"></a><span data-ttu-id="352a3-141">Verwenden eines lokalen Git-Repositorys als Ihre Bereitstellungsoption</span><span class="sxs-lookup"><span data-stu-id="352a3-141">Use a local Git repository as your deployment option</span></span>

<span data-ttu-id="352a3-142">Als Nächstes erstellen wir ein lokales Git-Repository in Azure, damit Sie mit dem Hochladen Ihres Codes beginnen können.</span><span class="sxs-lookup"><span data-stu-id="352a3-142">Next, we'll create a local Git repository in Azure so you can start uploading your code.</span></span>

1. <span data-ttu-id="352a3-143">Klicken Sie in der Bereitstellungsslot-Web-App **staging** im linken Navigationsbereich auf das Menüelement **Bereitstellungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="352a3-143">Within the **staging** deployment slot Web App, click the **Deployment options** menu item on the left-hand navigation.</span></span>

1. <span data-ttu-id="352a3-144">Das Azure-Portal navigiert zum Blatt **Bereitstellungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="352a3-144">The Azure portal navigates to the **Deployment options** blade.</span></span>

1. <span data-ttu-id="352a3-145">Klicken Sie auf **Quelle auswählen**, um die erforderlichen Einstellungen zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="352a3-145">Click on the **Choose Source** to configure the required settings.</span></span>

1. <span data-ttu-id="352a3-146">Im Azure-Portal werden die verfügbaren Optionen angezeigt, die Sie konfigurieren und verwenden können.</span><span class="sxs-lookup"><span data-stu-id="352a3-146">The Azure portal displays the available options that you can configure and use.</span></span> <span data-ttu-id="352a3-147">Wählen Sie in unserem Fall die Option **Lokales Git-Repository** aus.</span><span class="sxs-lookup"><span data-stu-id="352a3-147">In our case, choose the **Local Git Repository** option.</span></span>

1. <span data-ttu-id="352a3-148">Sie gelangen wieder zum Blatt **Bereitstellungsoption** zurück.</span><span class="sxs-lookup"><span data-stu-id="352a3-148">You will be returned to the **Deployment option** blade.</span></span> <span data-ttu-id="352a3-149">Klicken Sie unten auf dem Blatt auf die Schaltfläche **OK**, um die Bereitstellungsquelle zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="352a3-149">Click the **OK** button at the bottom of the blade to set up the deployment source.</span></span>

1. <span data-ttu-id="352a3-150">Navigieren Sie jetzt zum Abschnitt **Deployment Center (Preview)** (Bereitstellungscenter (Vorschau)) im linken Navigationsbereich, um die neuen Bereitstellungsdetails anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="352a3-150">Now, navigate to the **Deployment Center (Preview)** section on the left-side navigation to view the new deployment details.</span></span>

    ![Screenshot des Azure-Portals mit dem Blatt „Bereitstellungscenter“ mit dem Git Clone-URI für den hervorgehobenen Slot.](../media/7-staging-after-setting-git.png)

    <span data-ttu-id="352a3-152">Die wichtige Information hier, die zu beachten ist, ist der **Git Clone-URI**, bei dem es sich um die URL des lokalen Git-Repositorys handelt, die Sie als **Remote** für Ihr Lokales Webanwendungsrepository verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="352a3-152">The important information to note here is the **Git Clone Uri**, which is the local Git repository URL that you will use as a **remote** for your local web application repository.</span></span>

<span data-ttu-id="352a3-153">Nun wird es Zeit, mit dem Hochladen Ihres Codes in den Stagingbereitstellungsslot zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="352a3-153">It is time to start uploading your code to the staging deployment slot.</span></span>

## <a name="install-git-on-your-machine"></a><span data-ttu-id="352a3-154">Installieren von Git auf Ihrem Computer</span><span class="sxs-lookup"><span data-stu-id="352a3-154">Install Git on your machine</span></span>

<span data-ttu-id="352a3-155">Installieren Sie Git auf Ihrem Linux-Computer, wenn dies noch nicht geschehen ist.</span><span class="sxs-lookup"><span data-stu-id="352a3-155">If you don't already have it, install Git on your Linux machine.</span></span>

> [!NOTE]
> <span data-ttu-id="352a3-156">Diese Anweisungen beziehen sich auf Ubuntu 18.04, daher können die Schritte zum Installieren von Git für Ihre Distribution und Version abweichen.</span><span class="sxs-lookup"><span data-stu-id="352a3-156">These instructions are for Ubuntu 18.04, so the steps to install Git may differ for your distribution and version.</span></span> <span data-ttu-id="352a3-157">Suchen Sie in den [Installationsanweisungen für Git unter Linux](https://git-scm.com/download/linux) nach den passenden Schritten.</span><span class="sxs-lookup"><span data-stu-id="352a3-157">Check out the [Linux Git installation instructions](https://git-scm.com/download/linux) for the appropriate steps.</span></span>

1. <span data-ttu-id="352a3-158">Öffnen Sie ein neues **Terminal**fenster.</span><span class="sxs-lookup"><span data-stu-id="352a3-158">Open a new **Terminal** window</span></span>

1. <span data-ttu-id="352a3-159">Geben Sie den folgenden Befehl ein.</span><span class="sxs-lookup"><span data-stu-id="352a3-159">Type the following command.</span></span> <span data-ttu-id="352a3-160">Sie werden aufgefordert, Ihr Ubuntu-Benutzerkennort einzugeben.</span><span class="sxs-lookup"><span data-stu-id="352a3-160">You will be prompted to enter your Ubuntu user password.</span></span>

    ```console
    sudo apt-get update
    ```

1. <span data-ttu-id="352a3-161">Sobald das Update erfolgreich abgeschlossen wurde, geben Sie den folgenden Befehl ein, um Git lokal zu installieren.</span><span class="sxs-lookup"><span data-stu-id="352a3-161">Once the update is successful, type the following command to install Git locally.</span></span> <span data-ttu-id="352a3-162">Sie werden aufgefordert, die Installation von Git auf Ihrem Computer zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="352a3-162">You will be prompted to accept the installation of Git on your machine.</span></span>

    ```console
    sudo apt-get install git-core
    ```

1. <span data-ttu-id="352a3-163">Um sicherzustellen, dass Git jetzt installiert ist, geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="352a3-163">To verify that Git is now installed, type the following command:</span></span>

    ```console
    git --version
    ```

   <span data-ttu-id="352a3-164">Wenn die Installation erfolgreich war, wird die folgende Ausgabe angezeigt:</span><span class="sxs-lookup"><span data-stu-id="352a3-164">If the installation is successful, you will see the following output:</span></span>

    ```console
    git version 2.17.1
    ```

1. <span data-ttu-id="352a3-165">Es empfiehlt sich stets, Git-Einstellungen zu konfigurieren, indem Sie Ihren Namen und Ihre E-Mail-Adresse bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="352a3-165">It is always a good practice to configure Git settings by providing your name and email.</span></span> <span data-ttu-id="352a3-166">Hierzu müssen Sie die folgenden Befehle verwenden. Ersetzen Sie dabei die Platzhalter für `{your name}` und `{your email}` durch Ihren eigenen Namen und Ihre E-Mail-Adresse, jedoch ohne die geschweiften Klammern `{}`:</span><span class="sxs-lookup"><span data-stu-id="352a3-166">For that, you need to issue the following commands, replacing the `{your name}` and `{your email}` placeholders with your own name and email (without the `{}` curly braces):</span></span>

    ```console
    git config --global user.name "{your name}"
    git config --global user.email "{your email}"
    ```

1. <span data-ttu-id="352a3-167">Um zu überprüfen, ob Ihre Daten von Git erfasst wurden, geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="352a3-167">To verify that your information has been recorded by Git, type the following command:</span></span>

    ```console
    cat ~/.gitconfig
    ```

   <span data-ttu-id="352a3-168">Sie sollten Folgendes sehen, einschließlich Ihres Namens und Ihrer E-Mail-Adresse:</span><span class="sxs-lookup"><span data-stu-id="352a3-168">You should be seeing the following, with your name and email shown:</span></span>

    ```console
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-web-app"></a><span data-ttu-id="352a3-169">Initialisieren eines lokalen Git-Repositorys für Ihre Web-App</span><span class="sxs-lookup"><span data-stu-id="352a3-169">Initialize a local Git repository for your web app</span></span>

<span data-ttu-id="352a3-170">Um mit der Verwendung von Git zu beginnen, müssen Sie ein lokales Git-Repository für die Web-App initialisieren.</span><span class="sxs-lookup"><span data-stu-id="352a3-170">To start using Git, you need to initialize a local Git repository for the web app.</span></span>

1. <span data-ttu-id="352a3-171">Öffnen Sie ein neues **Terminal**fenster.</span><span class="sxs-lookup"><span data-stu-id="352a3-171">Open a new **Terminal** window.</span></span>

1. <span data-ttu-id="352a3-172">Navigieren Sie zum Inhaltsstammordner der Web-App, die Sie zuvor erstellt hatten.</span><span class="sxs-lookup"><span data-stu-id="352a3-172">Navigate to the content root folder of the web app you created previously.</span></span> <span data-ttu-id="352a3-173">Sie können Folgendes eingeben:</span><span class="sxs-lookup"><span data-stu-id="352a3-173">You can type the following:</span></span>

    ```console
    cd ~/Documents/BestBikeApp/
    ```

1. <span data-ttu-id="352a3-174">Verwenden Sie den folgenden Befehl, um ein neues Git-Repository zu initialisieren:</span><span class="sxs-lookup"><span data-stu-id="352a3-174">Initialize a new Git repository by issuing the following command:</span></span>

    ```console
    git init
    ```

    <span data-ttu-id="352a3-175">Wenn der Befehl erfolgreich ist, erhalten Sie sinngemäß die folgende Meldung:</span><span class="sxs-lookup"><span data-stu-id="352a3-175">If the command is successful, you receive a message like the following:</span></span>

    ```console
    Initialized empty Git repository in /home/{your-user}/Documents/BestBikeApp/.git/
    ```

1. <span data-ttu-id="352a3-176">Stellen Sie alle Web-App-Dateien für Git bereit.</span><span class="sxs-lookup"><span data-stu-id="352a3-176">Stage all the web app files to Git.</span></span>

   <span data-ttu-id="352a3-177">Der nächste Schritt besteht darin, Git die Existenz Ihrer Web-App-Dateien mitzuteilen.</span><span class="sxs-lookup"><span data-stu-id="352a3-177">The next step is to let Git know about your web app files.</span></span> <span data-ttu-id="352a3-178">Hierzu fügen Sie alle Dateien des Arbeitsverzeichnisses hinzu, sodass sie von Git **bereitgestellt** werden.</span><span class="sxs-lookup"><span data-stu-id="352a3-178">Do that by adding all the files of the working directory so that they get **staged** by Git.</span></span> <span data-ttu-id="352a3-179">Geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="352a3-179">Type the following command:</span></span>

    ```console
    git add .
    ```

    <span data-ttu-id="352a3-180">Der obige Befehl fügt alle durch „.“ dargestellten Dateien zum Stagingstatus von Git hinzu.</span><span class="sxs-lookup"><span data-stu-id="352a3-180">The command above adds all files, represented by the ".", to the staging state of Git.</span></span>

1. <span data-ttu-id="352a3-181">Nun müssen Sie Ihre Änderungen an Git committen.</span><span class="sxs-lookup"><span data-stu-id="352a3-181">Now, you need to commit your changes to Git.</span></span>

   <span data-ttu-id="352a3-182">Nachdem Sie die Dateien mit Git bereitgestellt haben, müssen Sie Ihre Dateien an den **Git-Commitverlauf** auf Ihrem lokalen Computer committen.</span><span class="sxs-lookup"><span data-stu-id="352a3-182">Once you stage the files with Git, you need to commit your files to the **Git commit history** on your local machine.</span></span> <span data-ttu-id="352a3-183">Hierzu geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="352a3-183">You do that by typing the following command:</span></span>

    ```console
   git commit -m "Initial create"
    ```

   <span data-ttu-id="352a3-184">Der `commit`-Befehl akzeptiert das `-m`-Argument, um eine Nachricht mit dem von Ihnen erstellten Commit einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="352a3-184">The `commit` command accepts  `-m` argument to include a message with the commit you are creating.</span></span> <span data-ttu-id="352a3-185">Wenn Sie später Ihren Code an Azure übertragen, sehen Sie diese Nachricht, die mit diesem konkreten Commit gespeichert wurde.</span><span class="sxs-lookup"><span data-stu-id="352a3-185">Later on, when you push your code to Azure, you will be able to see the same message stored with this particular commit.</span></span>

## <a name="add-a-remote-for-the-local-git-repository"></a><span data-ttu-id="352a3-186">Hinzufügen eines Remoterepositorys für das lokale Git-Repository</span><span class="sxs-lookup"><span data-stu-id="352a3-186">Add a remote for the local Git repository</span></span>

<span data-ttu-id="352a3-187">Sie haben nun erfolgreich ein neues lokales Git-Repository initialisiert.</span><span class="sxs-lookup"><span data-stu-id="352a3-187">At this point, you have successfully initialized a new local Git repository.</span></span> <span data-ttu-id="352a3-188">Außerdem haben Sie alle Ihre Web-App-Dateien an Git committet.</span><span class="sxs-lookup"><span data-stu-id="352a3-188">In addition, you've committed all of your web app files to Git.</span></span> <span data-ttu-id="352a3-189">Nun müssen Sie lediglich noch ein **Remote**repository hinzufügen, um Ihr lokales Git-Repository mit dem auf Azure gehosteten Repository zu verbinden.</span><span class="sxs-lookup"><span data-stu-id="352a3-189">What remains is to add a **remote** to connect your local Git repository to that hosted on Azure.</span></span>

<span data-ttu-id="352a3-190">Hierzu müssen Sie Folgendes durchführen:</span><span class="sxs-lookup"><span data-stu-id="352a3-190">To do so, you need to:</span></span>

1. <span data-ttu-id="352a3-191">Kopieren Sie die **GIT-Klon-URL**, die Sie weiter oben gesehen haben.</span><span class="sxs-lookup"><span data-stu-id="352a3-191">Copy the **Git clone url** that you saw above.</span></span>

1. <span data-ttu-id="352a3-192">Nach dem Kopieren kehren Sie zum **Terminal**fenster zurück und verwenden den folgenden Git-Befehl:</span><span class="sxs-lookup"><span data-stu-id="352a3-192">Once copied, you go back to the **Terminal** window and issue the following Git command:</span></span>

    ```console
    git remote add origin https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    <span data-ttu-id="352a3-193">Mit dem obigen Git-Befehl wird Ihr lokales Git-Repository mit dem in Azure gehosteten Repository verbunden.</span><span class="sxs-lookup"><span data-stu-id="352a3-193">The above Git command hooks your local Git repository to the one hosted on Azure.</span></span> <span data-ttu-id="352a3-194">Nun ist Push und Pull zwischen dem lokalen Git-Repository und dem Remote-Git-Repository möglich.</span><span class="sxs-lookup"><span data-stu-id="352a3-194">Now, you can start pushing and pulling between the local and remote Git repositories!</span></span>

1. <span data-ttu-id="352a3-195">Geben Sie zum Überprüfen des obigen Befehls den folgenden Git-Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="352a3-195">To verify the above command, type the following Git command:</span></span>

    ```console
    git remote -v
    ```

    <span data-ttu-id="352a3-196">Mit dem obigen Befehl wird die folgende Ausgabe generiert:</span><span class="sxs-lookup"><span data-stu-id="352a3-196">The command above generates the following output:</span></span>

    ```console
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a><span data-ttu-id="352a3-197">Übertragen Ihres Codes an Azure mithilfe von Push</span><span class="sxs-lookup"><span data-stu-id="352a3-197">Push your code to Azure</span></span>

<span data-ttu-id="352a3-198">Nachdem Ihr lokales Git-Repository nun mit dem Remote-Git-Repository in Azure verbunden ist, werden Sie die App entwickeln und erstellen und anschließend Ihre Web-App mithilfe von Push an Azure übertragen.</span><span class="sxs-lookup"><span data-stu-id="352a3-198">Now that you have your local Git repository hooked to the remote Git repository on Azure, you will develop and build the app, and then push your web app to Azure.</span></span>

1. <span data-ttu-id="352a3-199">Geben Sie den folgenden Git-Befehl ein, um Ihren **Haupt**branch mithilfe von Push an das Remote-Git-Repository in Azure zu übertragen:</span><span class="sxs-lookup"><span data-stu-id="352a3-199">Type the following Git command to push your **master** branch to the remote Git repository on Azure:</span></span>

    ```console
    git push origin master
    ```

1. <span data-ttu-id="352a3-200">Sie werden aufgefordert, das Kennwort einzugeben, das Sie im Abschnitt **Anmeldeinformationen für die Bereitstellung** weiter oben konfiguriert haben.</span><span class="sxs-lookup"><span data-stu-id="352a3-200">You will be prompted to enter the password that you have configured in the **Deployment credentials** section above.</span></span> <span data-ttu-id="352a3-201">Geben Sie Ihr Kennwort ein, und drücken Sie die Eingabetaste.</span><span class="sxs-lookup"><span data-stu-id="352a3-201">Enter your password and hit Enter.</span></span> <span data-ttu-id="352a3-202">Git beginnt, Ihre Commit-Dateien in das Remote-Git-Repository von Azure hochzuladen, das unter dem Stagingbereitstellungsslot konfiguriert wurde.</span><span class="sxs-lookup"><span data-stu-id="352a3-202">Git starts uploading your committed files to the Azure remote Git repository configured under the staging deployment slot.</span></span>

## <a name="verify-the-web-app-is-uploaded-to-azure"></a><span data-ttu-id="352a3-203">Überprüfen, ob die Web-App in Azure hochgeladen wird</span><span class="sxs-lookup"><span data-stu-id="352a3-203">Verify the web app is uploaded to Azure</span></span>

1. <span data-ttu-id="352a3-204">Melden Sie sich beim Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="352a3-204">Sign in to the Azure portal.</span></span>

1. <span data-ttu-id="352a3-205">Klicken Sie im linken Navigationsbereich auf das Menüelement **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="352a3-205">Click on the **All Resources** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="352a3-206">Sie gelangen im Azure-Portal zur Liste aller Ressourcen, die bisher in Azure erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="352a3-206">The Azure portal navigates you to the list of all resources created on Azure so far.</span></span>

1. <span data-ttu-id="352a3-207">Klicken Sie auf den oben erstellten Stagingslot.</span><span class="sxs-lookup"><span data-stu-id="352a3-207">Click on the staging slot created above.</span></span> <span data-ttu-id="352a3-208">Beachten Sie, dass ein Bereitstellungsslot als Web-App angesehen wird. Daher wird er unter **Alle Ressourcen** als Web-App-Ressource angezeigt.</span><span class="sxs-lookup"><span data-stu-id="352a3-208">Remember, a deployment slot is considered a web app, and hence, it will appear as a web app resource under **All Resources**.</span></span>

1. <span data-ttu-id="352a3-209">Wenn das Blatt „Stagingbereitstellungsslot“ angezeigt wird, wechseln Sie zu **Bereitstellungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="352a3-209">Once you arrive to the staging deployment slot blade, go to **Deployment options**.</span></span>

    <span data-ttu-id="352a3-210">Sie sehen, dass Ihr erster Commit, der sich lokal auf Ihrem Computer befindet, jetzt in das Azure-Portal hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="352a3-210">You will see that your first commit that you have locally on your machine is now uploaded to the Azure portal.</span></span>

    <span data-ttu-id="352a3-211">Indem Ihr Code lokal mithilfe von Push an das in Azure gehostete Remote-Git-Repository übertragen wurde, hat Azure diesen Vorgang aufgezeichnet.</span><span class="sxs-lookup"><span data-stu-id="352a3-211">By pushing your code locally to the remote Git repository hosted on Azure, Azure has recorded this operation.</span></span>

    <span data-ttu-id="352a3-212">Jedes Mal, wenn Sie Ihren Code an Azure übertragen, wird ein neuer Datensatz zusammen mit der Nachricht angezeigt, die Sie eingeben, wenn Sie Ihre Änderungen lokal auf Ihrem Computer committen.</span><span class="sxs-lookup"><span data-stu-id="352a3-212">Every time you push your code to Azure, you will see a new record, together with the message that you type when committing your changes locally on your machine.</span></span>

    ![Screenshot des Azure-Portals mit einer kürzlich erfolgten Bereitstellung im Git-Repository auf dem Blatt „Entwicklungsoptionen“.](../media/7-staging-deployment-slot-after-uploading-files.png)

1. <span data-ttu-id="352a3-214">Sehen wir uns nun die **Stagingslot**-URL an.</span><span class="sxs-lookup"><span data-stu-id="352a3-214">Let's visit the **staging slot** URL.</span></span> <span data-ttu-id="352a3-215">Auf die URL wurde bereits oben eingegangen. Sollten Sie jedoch Ihre URL vergessen haben, können Sie stets zur Seite **Übersicht** des Stagingbereitstellungsslots wechseln und von dort die URL übernehmen.</span><span class="sxs-lookup"><span data-stu-id="352a3-215">The URL was mentioned above, however, if you forget that URL, you can always go to the **Overview** page of the staging deployment slot and pick up the URL.</span></span>

1. <span data-ttu-id="352a3-216">Geben Sie die folgende URL in die Adressleiste Ihres Browsers ein: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="352a3-216">Type the following URL in your browser address bar: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).</span></span>

    ![Screenshot einer Webbrowseransicht der Website des Stagingbereitstellungsslots.](../media/7-staging-slot-hosted-online.png)

<span data-ttu-id="352a3-218">Sie haben Ihre lokalen Web-App-Dateien erfolgreich in den Stagingbereitstellungsslot in Azure hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="352a3-218">You have successfully uploaded your local web app files to the staging deployment slot on Azure.</span></span>

## <a name="swapping-the-staging-and-production-deployment-slots"></a><span data-ttu-id="352a3-219">Austauschen von Staging- und Produktionsbereitstellungsslots</span><span class="sxs-lookup"><span data-stu-id="352a3-219">Swapping the staging and production deployment slots</span></span>

<span data-ttu-id="352a3-220">Nachdem die Anwendung nun in dem Stagingbereitstellungsslot ausgeführt wird, der in Azure gehostet wird, ist es Zeit, diesen Slot gegen den Produktionsbereitstellungsslot austauschen.</span><span class="sxs-lookup"><span data-stu-id="352a3-220">Now that the application is up and running on the staging deployment slot hosted on Azure, it is time to swap this slot with the production one.</span></span> <span data-ttu-id="352a3-221">Gehen Sie dazu folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="352a3-221">To do so, follow these steps:</span></span>

1. <span data-ttu-id="352a3-222">Navigieren Sie zum Blatt der ursprünglichen Web-App, die Sie früher erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="352a3-222">Navigate to the original Web App blade created early.</span></span> <span data-ttu-id="352a3-223">Sie finden die ursprüngliche Web-App auf dem Blatt **Alle Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="352a3-223">You can find the original Web App from the **All resources** blade.</span></span>

1. <span data-ttu-id="352a3-224">Klicken Sie im linken Navigationsbereich auf das Menüelement **Bereitstellungsslots**.</span><span class="sxs-lookup"><span data-stu-id="352a3-224">Click the **Deployment slots** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="352a3-225">Klicken Sie oben auf dem Blatt auf die Schaltfläche **Austauschen**.</span><span class="sxs-lookup"><span data-stu-id="352a3-225">Click on the **Swap** button at the top of the blade.</span></span>

1. <span data-ttu-id="352a3-226">Sie gelangen im Azure-Portal zum Blatt **Austauschen**.</span><span class="sxs-lookup"><span data-stu-id="352a3-226">The Azure portal navigates you to the **Swap** blade.</span></span>

1. <span data-ttu-id="352a3-227">Wählen Sie für das Feld **Austauschen** die Option **Austauschen** aus.</span><span class="sxs-lookup"><span data-stu-id="352a3-227">For the **Swap** field, select **Swap**.</span></span>

1. <span data-ttu-id="352a3-228">Wählen Sie für das Feld **Quelle** die Option **Staging** aus.</span><span class="sxs-lookup"><span data-stu-id="352a3-228">For the **Source** field, select **Staging**.</span></span>

1. <span data-ttu-id="352a3-229">Wählen Sie für das Feld **Ziel** die Option **Produktion** aus.</span><span class="sxs-lookup"><span data-stu-id="352a3-229">For the **Destination** field, select **Production**.</span></span>

    ![Screenshot des Azure-Portals mit dem Blatt „Austauschen“ des Bereitstellungsslots.](../media/7-swap-blade.png)

1. <span data-ttu-id="352a3-231">Klicken Sie am unteren Blattrand auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="352a3-231">Click on the **OK** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="352a3-232">Azure beginnt mit dem Austauschprozess.</span><span class="sxs-lookup"><span data-stu-id="352a3-232">Azure starts the swapping process.</span></span> <span data-ttu-id="352a3-233">Dieser Vorgang dauert in der Regel einige Sekunden, je nach der Größe der ausgetauschten Web-App.</span><span class="sxs-lookup"><span data-stu-id="352a3-233">Usually, this operation takes a few seconds, depending on the size of the web app being swapped.</span></span>

1. <span data-ttu-id="352a3-234">Wechseln Sie nach Abschluss des Vorgangs zur Web-App-URL: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="352a3-234">Once the operation ends, visit the web app URL: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).</span></span>

    ![Screenshot mit einer Webbrowseransicht des früheren Stagingbereitstellungsslots, der jetzt als primäre Web-App gehostet ist.](../media/7-web-app-page.png)

    <span data-ttu-id="352a3-236">Der Austauschvorgang war erfolgreich!</span><span class="sxs-lookup"><span data-stu-id="352a3-236">The swapping operation has been successful!</span></span> <span data-ttu-id="352a3-237">Sie sehen nun, dass der Code, den Sie in den Stagingbereitstellungsslot hochgeladen haben, auch im Produktionsslot gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="352a3-237">You can now see the code that you uploaded to the staging deployment slot also being hosted on the production slot.</span></span>

1. <span data-ttu-id="352a3-238">Wechseln Sie nun zur URL des Stagingslots: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="352a3-238">Now, visit the URL of the staging slot: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).</span></span>

    ![Screenshot mit einer Webbrowseransicht des zuvor primären Bereitstellungsslots, der jetzt als Stagingbereitstellungsslot-Web-App gehostet ist.](../media/7-staging-after-swapping.png)

    <span data-ttu-id="352a3-240">Der Stagingbereitstellungsslot enthält jetzt die ursprünglichen Standard-Webanwendungsdateien, die zuvor unter dem Produktionsslot gehostet wurden.</span><span class="sxs-lookup"><span data-stu-id="352a3-240">The staging deployment slot now contains the original, default web application files that were previously hosted under the production slot.</span></span>

<span data-ttu-id="352a3-241">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="352a3-241">Congratulations!</span></span> <span data-ttu-id="352a3-242">Sie haben Ihre Web-App erfolgreich in Azure hochgeladen und die Bereitstellungsslots getauscht.</span><span class="sxs-lookup"><span data-stu-id="352a3-242">You have successfully uploaded your web app to Azure and swapped deployment slots.</span></span>
