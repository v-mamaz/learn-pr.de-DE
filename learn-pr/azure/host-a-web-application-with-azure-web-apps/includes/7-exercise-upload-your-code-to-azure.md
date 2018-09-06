<span data-ttu-id="f83e5-101">In dieser Übung laden Sie Ihre ASP.NET Core-Anwendung in Azure hoch.</span><span class="sxs-lookup"><span data-stu-id="f83e5-101">In this exercise, you'll upload your ASP.NET Core application to Azure.</span></span>

## <a name="create-a-staging-deployment-slot"></a><span data-ttu-id="f83e5-102">Erstellen eines Stagingbereitstellungsslots</span><span class="sxs-lookup"><span data-stu-id="f83e5-102">Create a staging deployment slot</span></span>

1. <span data-ttu-id="f83e5-103">Suchen Sie das Menüelement **Bereitstellungsslots** im linken Navigationsbereich, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-103">Locate and click the **Deployment slots** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="f83e5-104">Azure öffnet wie unten gezeigt das Blatt **Bereitstellungsslots**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-104">Azure opens the **Deployment slots** blade as shown below.</span></span>

    ![Bereitstellungsslots](../media-draft/7-deployment-slot-blade.png)

1. <span data-ttu-id="f83e5-106">Suchen Sie die Schaltfläche **+ Slot hinzufügen** auf der oberen Navigationsleiste des Blatts „Bereitstellungsslots“, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-106">Locate and click the **+ Add Slot** button on the top navigation bar of the deployment slots blade.</span></span>

1. <span data-ttu-id="f83e5-107">Im Azure-Portal wird wie unten gezeigt das Blatt **Slot hinzufügen** geöffnet.</span><span class="sxs-lookup"><span data-stu-id="f83e5-107">The Azure portal opens the **Add a slot** blade as shown below.</span></span>

    ![Hinzufügen eines Slots](../media-draft/7-new-deployment-slot-blade.png)

    <span data-ttu-id="f83e5-109">Geben Sie einen Namen für Ihren Bereitstellungsslot ein.</span><span class="sxs-lookup"><span data-stu-id="f83e5-109">Give your deployment slot a name.</span></span> <span data-ttu-id="f83e5-110">Verwenden Sie in diesem Fall **Staging**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-110">In this case, use **Staging**.</span></span>

    <span data-ttu-id="f83e5-111">Sie haben zwei Möglichkeiten, um eine **Konfigurationsquelle** auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-111">To choose a **Configuration Source**, you have 2 options.</span></span>

    1. <span data-ttu-id="f83e5-112">Sie können die Konfigurationselemente eines anderen Slots oder der in Azure erstellten Web-App klonen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-112">Select to clone the configuration elements from any other slot or web app created on Azure.</span></span>

    1. <span data-ttu-id="f83e5-113">Sie können auch auswählen, keine Konfigurationselemente zu klonen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-113">You can choose not to clone any configuration elements.</span></span> <span data-ttu-id="f83e5-114">In diesem Fall wählen Sie die Option **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen) aus.</span><span class="sxs-lookup"><span data-stu-id="f83e5-114">In this case, you select the option **Don't clone configuration from an existing slot**.</span></span>

    <span data-ttu-id="f83e5-115">Wählen Sie die zweite Option, **Don't clone configuration from an existing slot** (Konfiguration nicht aus vorhandenem Slot klonen), aus.</span><span class="sxs-lookup"><span data-stu-id="f83e5-115">Choose the second option, **Don't clone configuration from an existing slot**.</span></span>

1. <span data-ttu-id="f83e5-116">Suchen Sie am unteren Blattrand die Schaltfläche **OK**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-116">Locate and click the **OK** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="f83e5-117">Nachdem der Bereitstellungsslot erfolgreich erstellt wurde, wird im Azure-Portal wieder das Blatt **Bereitstellungsslots** Ihrer Web-App angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f83e5-117">Once the deployment slot is successfully created, the Azure portal navigates you back to the **Deployment slots** blade of your web app.</span></span>

    <span data-ttu-id="f83e5-118">Sie sehen nun den neuen Bereitstellungsslot, den Sie gerade erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="f83e5-118">Now, you can see the new deployment slot that you have just created.</span></span>

    ![Erstellter Bereitstellungsslot](../media-draft/7-deployment-slot-created.png)

1. <span data-ttu-id="f83e5-120">Suchen Sie den neuen Bereitstellungsslot, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-120">Locate and click the new deployment slot.</span></span>

1. <span data-ttu-id="f83e5-121">Im Azure-Portal wird die Seite **Übersicht** des neu erstellten Bereitstellungsslots angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f83e5-121">The Azure portal navigates to the **Overview** page of the newly created deployment slot.</span></span>

    ![Stagingbereitstellungsslot](../media-draft/7-deployment-slot-staging.png)

    <span data-ttu-id="f83e5-123">Beachten Sie die **URL** des Stagingbereitstellungsslots.</span><span class="sxs-lookup"><span data-stu-id="f83e5-123">Notice the **URL** of the staging deployment slot.</span></span> <span data-ttu-id="f83e5-124">Es handelt sich dabei um dieselbe URL, die Sie zuvor zu Beginn dieser Einheit gesehen haben.</span><span class="sxs-lookup"><span data-stu-id="f83e5-124">It is the exact same URL you saw previously at the beginning of this unit.</span></span>

    <span data-ttu-id="f83e5-125">Ein Bereitstellungsslot wird in Azure als Web-App behandelt.</span><span class="sxs-lookup"><span data-stu-id="f83e5-125">A deployment slot is treated as a web app inside Azure.</span></span> <span data-ttu-id="f83e5-126">Allerdings handelt es sich um einen speziellen Typen, der ein untergeordnetes Element der ursprünglichen Web-App ist und nicht gegen die ursprüngliche Web-App ausgetauscht werden kann.</span><span class="sxs-lookup"><span data-stu-id="f83e5-126">However, it is a special type that is a child of the original web app and can be swapped with the original web app.</span></span>

    <span data-ttu-id="f83e5-127">Wenn Sie auf die **URL** klicken, sehen Sie dieselbe Standardseite, die Azure für die Web-App erstellt hat, als wir die App erstmals im Azure-Portal erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="f83e5-127">If you click the **URL**, you will see the same default page that Azure created for the web app the first time we created it in the Azure portal.</span></span>

<span data-ttu-id="f83e5-128">Nachdem der Stagingbereitstellungsslot erfolgreich erstellt wurde, müssen Sie nun **Anmeldeinformationen für die Bereitstellung** konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="f83e5-128">Now that the staging deployment slot is created successfully, you need to configure **deployment credentials**.</span></span>

## <a name="create-deployment-credentials"></a><span data-ttu-id="f83e5-129">Erstellen von Anmeldeinformationen für die Bereitstellung</span><span class="sxs-lookup"><span data-stu-id="f83e5-129">Create deployment credentials</span></span>

<span data-ttu-id="f83e5-130">In Azure müssen Anmeldeinformationen für die Bereitstellung eingerichtet werden, bevor Sie mit dem eigentlichen Bereitstellungsvorgang beginnen können.</span><span class="sxs-lookup"><span data-stu-id="f83e5-130">Azure requires deployment credentials to be set up before you can start the actual deployment process.</span></span> <span data-ttu-id="f83e5-131">Aus diesem Grund lernen Sie, wie Sie Ihre eigenen Anmeldeinformationen für die Bereitstellung erstellen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-131">For that reason, you will learn how to create your own deployment credentials.</span></span>

1. <span data-ttu-id="f83e5-132">Suchen Sie das Menüelement **Anmeldeinformationen für Bereitstellung** im linken Navigationsbereich, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-132">Locate and click the **Deployment credentials** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="f83e5-133">Das Azure-Portal navigiert wie unten gezeigt zum Blatt **Anmeldeinformationen für Bereitstellung**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-133">The Azure portal navigates to the **Deployment credentials** blade as shown below.</span></span>

    ![Anmeldeinformationen für die Bereitstellung](../media-draft/7-deployment-credentials.png)

    <span data-ttu-id="f83e5-135">Geben Sie einen **Benutzernamen** und ein **Kennwort** Ihrer Wahl ein, und bestätigen Sie nochmals Ihr Kennwort.</span><span class="sxs-lookup"><span data-stu-id="f83e5-135">Enter a **username** and **password** of your choice, and then confirm your password once again.</span></span>

    > <span data-ttu-id="f83e5-136">Notieren Sie sich unbedingt Ihren Benutzernamen und das Kennwort, damit Sie beides nicht vergessen!</span><span class="sxs-lookup"><span data-stu-id="f83e5-136">Make sure you write down your username and password so that you don't forget them!</span></span> <span data-ttu-id="f83e5-137">Sie werden diese Informationen später benötigen, wenn wir beginnen, Ihren Code in Azure hochzuladen und bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-137">You will need them later when we start uploading and deploying our code to Azure.</span></span>

    <span data-ttu-id="f83e5-138">Suchen Sie nach dem Festlegen des Benutzernamens und des Kennworts die Schaltfläche **Speichern** am oberen Rand des Blatts **Anmeldeinformationen für Bereitstellung**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-138">Once you decide on the username and password, locate and click the **Save** button at the top of the **Deployment credentials** blade.</span></span>

<span data-ttu-id="f83e5-139">Nachdem die Anmeldeinformationen für die Bereitstellung erfolgreich erstellt wurden, müssen Sie nun **Bereitstellungsoptionen** konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="f83e5-139">Now that the deployment credentials are created successfully, you need to configure **deployment options**.</span></span>

## <a name="use-a-local-git-repository-as-your-deployment-option"></a><span data-ttu-id="f83e5-140">Verwenden eines lokalen Git-Repositorys als Ihre Bereitstellungsoption</span><span class="sxs-lookup"><span data-stu-id="f83e5-140">Use a local Git repository as your deployment option</span></span>

<span data-ttu-id="f83e5-141">Nun wird es Zeit, ein lokales Git-Repository in Azure zu erstellen, damit Sie mit dem Hochladen Ihres Codes beginnen können.</span><span class="sxs-lookup"><span data-stu-id="f83e5-141">Now, it is time to create a local Git repository in Azure so that you can start the process of uploading your code.</span></span>

1. <span data-ttu-id="f83e5-142">Suchen Sie das Menüelement **Bereitstellungsoptionen** im linken Navigationsbereich, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-142">Locate and click the **Deployment options** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="f83e5-143">Das Azure-Portal navigiert wie unten gezeigt zum Blatt **Bereitstellungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-143">The Azure portal navigates to the **Deployment options** blade as shown below.</span></span>

    ![Bereitstellungsoptionen](../media-draft/7-deployment-options.png)

1. <span data-ttu-id="f83e5-145">Klicken Sie auf **Quelle auswählen / Erforderliche Einstellungen konfigurieren**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-145">Click on **Choose source / Configure required settings**.</span></span>

    ![Anmeldeinformationen für die Bereitstellung](../media-draft/7-deployment-sources.png)

1. <span data-ttu-id="f83e5-147">Im Azure-Portal werden die verfügbaren Optionen angezeigt, die Sie konfigurieren und verwenden können.</span><span class="sxs-lookup"><span data-stu-id="f83e5-147">The Azure portal displays the available options that you can configure and use.</span></span> <span data-ttu-id="f83e5-148">Wählen Sie in unserem Fall die Option **Lokales Git-Repository** aus.</span><span class="sxs-lookup"><span data-stu-id="f83e5-148">In our case, choose the **Local Git Repository** option.</span></span>

    ![Lokales Git-Repository](../media-draft/7-local-git-repo.png)

1. <span data-ttu-id="f83e5-150">Suchen Sie am unteren Blattrand die Schaltfläche **OK**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-150">Locate and click the **OK** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="f83e5-151">Suchen Sie das Menüelement **Übersicht** im linken Navigationsbereich, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-151">Locate and click the **Overview** menu item on the left-side navigation.</span></span>

    ![Mit Git konfigurierter Bereitstellungsslot](../media-draft/7-staging-after-setting-git.png)

    <span data-ttu-id="f83e5-153">Beachten Sie zwei wichtige Informationen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-153">Notice two important pieces of information:</span></span>
    - <span data-ttu-id="f83e5-154">**GIT/Bereitstellungsbenutzername**: Hierbei handelt es sich um die Anmeldeinformationen, die Sie später für die Verbindung zum lokalen Git-Repository in Azure verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="f83e5-154">**Git/Deployment username**: These are the credentials that you will use later on to connect to the local Git repository on Azure.</span></span>

    - <span data-ttu-id="f83e5-155">**GIT-Klon-URL**: Dies ist die lokale Git-Repository-URL, die Sie als **Remote**-URL für Ihr lokales Webanwendungsrepository verwenden werden.</span><span class="sxs-lookup"><span data-stu-id="f83e5-155">**Git clone url**: This is the local Git repository URL that you will use as a **remote** for your local web application repository.</span></span>

<span data-ttu-id="f83e5-156">Nun wird es Zeit, mit dem Hochladen Ihres Codes in den Stagingbereitstellungsslot zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-156">It is time to start uploading your code to the staging deployment slot.</span></span>

## <a name="install-git-on-your-machine"></a><span data-ttu-id="f83e5-157">Installieren von Git auf Ihrem Computer</span><span class="sxs-lookup"><span data-stu-id="f83e5-157">Install Git on your machine</span></span>

<span data-ttu-id="f83e5-158">Ich werde Git auf meinem Ubuntu 18.04-Computer installieren.</span><span class="sxs-lookup"><span data-stu-id="f83e5-158">I will be installing Git on my Ubuntu 18.04 machine.</span></span>

1. <span data-ttu-id="f83e5-159">Öffnen Sie ein neues **Terminal**fenster.</span><span class="sxs-lookup"><span data-stu-id="f83e5-159">Open a new **Terminal** window</span></span>

1. <span data-ttu-id="f83e5-160">Geben Sie den folgenden Befehl ein.</span><span class="sxs-lookup"><span data-stu-id="f83e5-160">Type the following command.</span></span> <span data-ttu-id="f83e5-161">Sie werden aufgefordert, Ihr Ubuntu-Benutzerkennort einzugeben.</span><span class="sxs-lookup"><span data-stu-id="f83e5-161">You will be prompted to enter your Ubuntu user password.</span></span>

    ```console
    sudo apt-get update
    ```

1. <span data-ttu-id="f83e5-162">Sobald das Update erfolgreich abgeschlossen wurde, geben Sie den folgenden Befehl ein, um Git lokal zu installieren.</span><span class="sxs-lookup"><span data-stu-id="f83e5-162">Once the update is successful, type the following command to install Git locally.</span></span> <span data-ttu-id="f83e5-163">Sie werden aufgefordert, die Installation von Git auf Ihrem Computer zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="f83e5-163">You will be prompted to accept the installation of Git on your machine.</span></span>

    ```console
    sudo apt-get install git-core
    ```

1. <span data-ttu-id="f83e5-164">Um sicherzustellen, dass Git jetzt installiert ist, geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="f83e5-164">To verify that Git is now installed, type the following command:</span></span>

    ```console
    git --version
    ```

   <span data-ttu-id="f83e5-165">Wenn die Installation erfolgreich war, wird die folgende Ausgabe angezeigt:</span><span class="sxs-lookup"><span data-stu-id="f83e5-165">If the installation is successful, you will see the following output:</span></span>

    ```console
    git version 2.17.1
    ```

1. <span data-ttu-id="f83e5-166">Es empfiehlt sich stets, Git-Einstellungen zu konfigurieren, indem Sie Ihren Namen und Ihre E-Mail-Adresse bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-166">It is always a good practice to configure Git settings by providing your name and email.</span></span> <span data-ttu-id="f83e5-167">Hierzu müssen Sie die folgenden Befehle verwenden. Ersetzen Sie dabei die Platzhalter für Name und E-Mail, jedoch ohne die geschweiften Klammern (`{}`):</span><span class="sxs-lookup"><span data-stu-id="f83e5-167">For that, you need to issue the following commands, replacing the placeholders for name and email, without the curly braces (`{}`):</span></span>

    ```console
    git config --global user.name "{your name}"
    git config --global user.email "{your email}"
    ```

1. <span data-ttu-id="f83e5-168">Um sicherzustellen, dass Ihre Daten von Git erfasst wurden, geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="f83e5-168">To verify that your information has been recorded by Git, type the following command:</span></span>

    ```console
    cat ~/.gitconfig
    ```

   <span data-ttu-id="f83e5-169">Sie sollten Folgendes sehen, einschließlich Ihres Namens und Ihrer E-Mail-Adresse:</span><span class="sxs-lookup"><span data-stu-id="f83e5-169">You should be seeing the following, with your name and email shown:</span></span>

    ```console
    [user]
        name = {your name}
        email = {your email}
    ```

## <a name="initialize-a-local-git-repository-for-your-web-app"></a><span data-ttu-id="f83e5-170">Initialisieren eines lokalen Git-Repositorys für Ihre Web-App</span><span class="sxs-lookup"><span data-stu-id="f83e5-170">Initialize a local Git repository for your web app</span></span>

<span data-ttu-id="f83e5-171">Um mit der Verwendung von Git zu beginnen, müssen Sie ein lokales Git-Repository für die Web-App initialisieren.</span><span class="sxs-lookup"><span data-stu-id="f83e5-171">To start using Git, you need to initialize a local Git repository for the web app.</span></span>

1. <span data-ttu-id="f83e5-172">Öffnen Sie ein neues **Terminal**fenster.</span><span class="sxs-lookup"><span data-stu-id="f83e5-172">Open a new **Terminal** window.</span></span>

1. <span data-ttu-id="f83e5-173">Navigieren Sie zum Inhaltsstammordner Ihrer Web-App.</span><span class="sxs-lookup"><span data-stu-id="f83e5-173">Navigate to the content root folder of your web app.</span></span> <span data-ttu-id="f83e5-174">Sie können Folgendes eingeben:</span><span class="sxs-lookup"><span data-stu-id="f83e5-174">You can type the following:</span></span>

    ```console
    cd ~/Documents/BestBikeApp/
    ```

    ![Inhaltsstammordner der Web-App](../media-draft/7-web-app-content-root-folder.png)

1. <span data-ttu-id="f83e5-176">Verwenden Sie den folgenden Befehl, um ein neues Git-Repository zu initialisieren:</span><span class="sxs-lookup"><span data-stu-id="f83e5-176">Initialize a new Git repository by issuing the following command:</span></span>

    ```console
    git init
    ```

    <span data-ttu-id="f83e5-177">Wenn der Befehl erfolgreich ist, erhalten Sie sinngemäß die folgende Meldung:</span><span class="sxs-lookup"><span data-stu-id="f83e5-177">If the command is successful, you receive a message like the following:</span></span>

    ```console
    Initialized empty Git repository in /home/your-user/Documents/BestBikeApp/.git/
    ```

1. <span data-ttu-id="f83e5-178">Stellen Sie alle Web-App-Dateien für Git bereit.</span><span class="sxs-lookup"><span data-stu-id="f83e5-178">Stage all the web app files to Git.</span></span>

   <span data-ttu-id="f83e5-179">Der nächste Schritt besteht darin, Git die Existenz Ihrer Web-App-Dateien mitzuteilen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-179">The next step is to let Git know about your web app files.</span></span> <span data-ttu-id="f83e5-180">Hierzu fügen Sie alle Dateien des Arbeitsverzeichnisses hinzu, sodass sie von Git **bereitgestellt** werden.</span><span class="sxs-lookup"><span data-stu-id="f83e5-180">Do that by adding all the files of the working directory so that they get **staged** by Git.</span></span> <span data-ttu-id="f83e5-181">Geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="f83e5-181">Type the following command:</span></span>

    ```console
    git add .
    ```

    <span data-ttu-id="f83e5-182">Der obige Befehl fügt alle durch „.“ dargestellten Dateien zum Stagingstatus von Git hinzu.</span><span class="sxs-lookup"><span data-stu-id="f83e5-182">The command above adds all files, represented by the ".", to the staging state of Git.</span></span>

1. <span data-ttu-id="f83e5-183">Nun müssen Sie Ihre Änderungen an Git committen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-183">Now, you need to commit your changes to Git.</span></span>

   <span data-ttu-id="f83e5-184">Nachdem Sie die Dateien mit Git bereitgestellt haben, müssen Sie Ihre Dateien an den **Git-Commitverlauf** auf Ihrem lokalen Computer committen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-184">Once you stage the files with Git, you need to commit your files to the **Git commit history** on your local machine.</span></span> <span data-ttu-id="f83e5-185">Hierzu geben Sie den folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="f83e5-185">You do that by typing the following command:</span></span>

   `git commit -m "Initial create"`

   <span data-ttu-id="f83e5-186">Der `commit`-Befehl akzeptiert das `-m`-Argument, um eine Nachricht mit dem von Ihnen erstellten Commit einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-186">The `commit` command accepts  `-m` argument to include a message with the commit you are creating.</span></span> <span data-ttu-id="f83e5-187">Wenn Sie später Ihren Code an Azure übertragen, sehen Sie diese Nachricht, die mit diesem konkreten Commit gespeichert wurde.</span><span class="sxs-lookup"><span data-stu-id="f83e5-187">Later on, when you push your code to Azure, you will be able to see the same message stored with this particular commit.</span></span>

## <a name="add-a-remote-for-the-local-git-repository"></a><span data-ttu-id="f83e5-188">Hinzufügen eines Remoterepositorys für das lokale Git-Repository</span><span class="sxs-lookup"><span data-stu-id="f83e5-188">Add a remote for the local Git repository</span></span>

<span data-ttu-id="f83e5-189">Sie haben nun erfolgreich ein neues lokales Git-Repository initialisiert.</span><span class="sxs-lookup"><span data-stu-id="f83e5-189">At this point, you have successfully initialized a new local Git repository.</span></span> <span data-ttu-id="f83e5-190">Außerdem haben Sie alle Ihre Web-App-Dateien an Git committet.</span><span class="sxs-lookup"><span data-stu-id="f83e5-190">In addition, you've committed all of your web app files to Git.</span></span> <span data-ttu-id="f83e5-191">Nun müssen Sie lediglich noch ein **Remote**repository hinzufügen, um Ihr lokales Git-Repository mit dem auf Azure gehosteten Repository zu verbinden.</span><span class="sxs-lookup"><span data-stu-id="f83e5-191">What remains is to add a **remote** to connect your local Git repository to that hosted on Azure.</span></span>

<span data-ttu-id="f83e5-192">Hierzu müssen Sie Folgendes durchführen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-192">To do so, you need to:</span></span>

1. <span data-ttu-id="f83e5-193">Kopieren Sie die **GIT-Klon-URL**, die Sie weiter oben gesehen haben.</span><span class="sxs-lookup"><span data-stu-id="f83e5-193">Copy the **Git clone url** that you saw above.</span></span>

1. <span data-ttu-id="f83e5-194">Nach dem Kopieren kehren Sie zum **Terminal**fenster zurück und verwenden den folgenden Git-Befehl:</span><span class="sxs-lookup"><span data-stu-id="f83e5-194">Once copied, you go back to the **Terminal** window and issue the following Git command:</span></span>

    ```console
    git remote add origin https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git
    ```

    <span data-ttu-id="f83e5-195">Mit dem obigen Git-Befehl wird Ihr lokales Git-Repository mit dem in Azure gehosteten Repository verbunden.</span><span class="sxs-lookup"><span data-stu-id="f83e5-195">The above Git command hooks your local Git repository to the one hosted on Azure.</span></span> <span data-ttu-id="f83e5-196">Nun ist Push und Pull zwischen dem lokalen Git-Repository und dem Remote-Git-Repository möglich.</span><span class="sxs-lookup"><span data-stu-id="f83e5-196">Now, you can start pushing and pulling between the local and remote Git repositories!</span></span>

1. <span data-ttu-id="f83e5-197">Geben Sie zum Überprüfen des obigen Befehls den folgenden Git-Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="f83e5-197">To verify the above command, type the following Git command:</span></span>

    ```
    git remote -v
    ```

    <span data-ttu-id="f83e5-198">Mit dem obigen Befehl wird die folgende Ausgabe generiert:</span><span class="sxs-lookup"><span data-stu-id="f83e5-198">The command above generates the following output:</span></span>

    ```console
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (fetch)
    origin  https://BESTBIKE-git@BESTBIKE-staging.scm.azurewebsites.net:443/BESTBIKE.git (push)
    ```

## <a name="push-your-code-to-azure"></a><span data-ttu-id="f83e5-199">Übertragen Ihres Codes an Azure mithilfe von Push</span><span class="sxs-lookup"><span data-stu-id="f83e5-199">Push your code to Azure</span></span>

<span data-ttu-id="f83e5-200">Nachdem Ihr lokales Git-Repository nun mit dem Remote-Git-Repository in Azure verbunden ist, werden Sie die App entwickeln und erstellen und anschließend Ihre Web-App mithilfe von Push an Azure übertragen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-200">Now that you have your local Git repository hooked to the remote Git repository on Azure, you will develop and build the app, and then push your web app to Azure.</span></span>

1. <span data-ttu-id="f83e5-201">Geben Sie den folgenden Git-Befehl ein, um Ihren **Haupt**branch mithilfe von Push an das Remote-Git-Repository in Azure zu übertragen:</span><span class="sxs-lookup"><span data-stu-id="f83e5-201">Type the following Git command to push your **master** branch to the remote Git repository on Azure:</span></span>

    ```console
    git push origin master
    ```

1. <span data-ttu-id="f83e5-202">Sie werden aufgefordert, das Kennwort einzugeben, das Sie im Abschnitt **Anmeldeinformationen für die Bereitstellung** weiter oben konfiguriert haben.</span><span class="sxs-lookup"><span data-stu-id="f83e5-202">You will be prompted to enter the password that you have configured in the **Deployment credentials** section above.</span></span> <span data-ttu-id="f83e5-203">Geben Sie Ihr Kennwort ein, und drücken Sie die Eingabetaste.</span><span class="sxs-lookup"><span data-stu-id="f83e5-203">Enter your password and hit Enter.</span></span> <span data-ttu-id="f83e5-204">Git beginnt, Ihre Commit-Dateien in das Remote-Git-Repository von Azure hochzuladen, das unter dem Stagingbereitstellungsslot konfiguriert wurde.</span><span class="sxs-lookup"><span data-stu-id="f83e5-204">Git starts uploading your committed files to the Azure remote Git repository configured under the staging deployment slot.</span></span>

## <a name="verify-the-web-app-is-uploaded-to-azure"></a><span data-ttu-id="f83e5-205">Sicherstellen, dass die Web-App in Azure hochgeladen wird</span><span class="sxs-lookup"><span data-stu-id="f83e5-205">Verify the web app is uploaded to Azure</span></span>

1. <span data-ttu-id="f83e5-206">Melden Sie sich beim Azure-Portal an.</span><span class="sxs-lookup"><span data-stu-id="f83e5-206">Log in to the Azure portal.</span></span>

1. <span data-ttu-id="f83e5-207">Suchen Sie das Menüelement **Alle Ressourcen** im linken Navigationsbereich, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-207">Locate and click on the **All Resources** menu item on the left-side navigation.</span></span>

1. <span data-ttu-id="f83e5-208">Sie gelangen im Azure-Portal zur Liste aller Ressourcen, die bisher in Azure erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="f83e5-208">The Azure portal navigates you to the list of all resources created on Azure so far.</span></span>

1. <span data-ttu-id="f83e5-209">Suchen Sie den oben erstellten Stagingslot, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-209">Locate and click on the staging slot created above.</span></span> <span data-ttu-id="f83e5-210">Beachten Sie, dass ein Bereitstellungsslot als Web-App angesehen wird. Daher wird er unter **Alle Ressourcen** als Web-App-Ressource angezeigt.</span><span class="sxs-lookup"><span data-stu-id="f83e5-210">Remember, a deployment slot is considered a web app, and hence, it will appear as a web app resource under **All Resources**.</span></span>

1. <span data-ttu-id="f83e5-211">Wenn das Blatt „Stagingbereitstellungsslot“ angezeigt wird, wechseln Sie zu **Bereitstellungsoptionen**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-211">Once you arrive to the staging deployment slot blade, go to **Deployment options**.</span></span>

    ![Stagingbereitstellungsslot nach dem Hochladen der Web-App](../media-draft/7-staging-deployment-slot-after-uploading-files.png)

    <span data-ttu-id="f83e5-213">Sie sehen, dass Ihr erster Commit, der sich lokal auf Ihrem Computer befindet, jetzt in das Azure-Portal hochgeladen wurde.</span><span class="sxs-lookup"><span data-stu-id="f83e5-213">You will see that your first commit that you have locally on your machine is now uploaded to the Azure portal!</span></span>

    <span data-ttu-id="f83e5-214">Indem Ihr Code lokal mithilfe von Push an das in Azure gehostete Remote-Git-Repository übertragen wurde, hat Azure diesen Vorgang aufgezeichnet.</span><span class="sxs-lookup"><span data-stu-id="f83e5-214">By pushing your code locally to the remote Git repository hosted on Azure, Azure has recorded this operation.</span></span>

    <span data-ttu-id="f83e5-215">Jedes Mal, wenn Sie Ihren Code an Azure übertragen, wird ein neuer Datensatz zusammen mit der Nachricht angezeigt, die Sie eingeben, wenn Sie Ihre Änderungen lokal auf Ihrem Computer committen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-215">Every time you push your code to Azure, you will see a new record, together with the message that you type when committing your changes locally on your machine.</span></span>

1. <span data-ttu-id="f83e5-216">Sehen wir uns nun die **Stagingslot**-URL an.</span><span class="sxs-lookup"><span data-stu-id="f83e5-216">Let's visit the **staging slot** URL.</span></span> <span data-ttu-id="f83e5-217">Auf die URL wurde bereits oben eingegangen. Sollten Sie jedoch Ihre URL vergessen haben, können Sie stets zur Seite **Übersicht** des Stagingbereitstellungsslots wechseln und von dort die URL übernehmen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-217">The URL was mentioned above, however, if your forget that URL, you can always go to the **Overview** page of the staging deployment slot and pick up the URL.</span></span>

1. <span data-ttu-id="f83e5-218">Geben Sie die folgende URL in die Adressleiste Ihres Browsers ein: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="f83e5-218">Type the following URL in your browser address bar: [https://BESTBIKE-staging.azurewebsites.net/](https://BESTBIKE-staging.azurewebsites.net/).</span></span>

    ![Online gehosteter Stagingslot](../media-draft/7-staging-slot-hosted-online.png)

<span data-ttu-id="f83e5-220">Sie haben erfolgreich Ihre lokalen Web-App-Dateien in den Stagingbereitstellungsslot in Azure hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-220">You have successfully uploaded your local web app files to the staging deployment slot on Azure.</span></span>

## <a name="swapping-the-staging-and-production-deployment-slots"></a><span data-ttu-id="f83e5-221">Austauschen von Staging- und Produktionsbereitstellungsslots</span><span class="sxs-lookup"><span data-stu-id="f83e5-221">Swapping the staging and production deployment slots</span></span>

<span data-ttu-id="f83e5-222">Nachdem die Anwendung nun in dem Stagingbereitstellungsslot ausgeführt wird, der in Azure gehostet wird, ist es Zeit, diesen Slot gegen den Produktionsbereitstellungsslot austauschen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-222">Now that the application is up and running on the staging deployment slot hosted on Azure, it is time to swap this slot with the production one.</span></span> <span data-ttu-id="f83e5-223">Gehen Sie dazu folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="f83e5-223">To do so, follow these steps:</span></span>

1. <span data-ttu-id="f83e5-224">Suchen Sie das ursprüngliche Blatt der Web-App, das Sie in Einheit #2 erstellt haben, und wechseln Sie dorthin.</span><span class="sxs-lookup"><span data-stu-id="f83e5-224">Locate and navigate to the original web app blade, created in Unit #2.</span></span>

1. <span data-ttu-id="f83e5-225">Suchen Sie das Menüelement **Bereitstellungsslots** im linken Navigationsbereich, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-225">Locate and click the **Deployment slots** menu item on the left-side navigation.</span></span>

    ![Das Blatt „Web-App-Bereitstellungsslots“](../media-draft/7-web-app-slots.png)

1. <span data-ttu-id="f83e5-227">Suchen Sie die Schaltfläche **Austauschen** am oberen Rand des Blatts, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-227">Locate and click on the **Swap** button at the top of the blade.</span></span>

1. <span data-ttu-id="f83e5-228">Sie gelangen im Azure-Portal zum Blatt **Austauschen**.</span><span class="sxs-lookup"><span data-stu-id="f83e5-228">The Azure portal navigates you to the **Swap** blade.</span></span>

    ![Das Blatt „Austauschen“](../media-draft/7-swap-blade.png)

1. <span data-ttu-id="f83e5-230">Wählen Sie für das Feld **Austauschen** die Option **Austauschen** aus.</span><span class="sxs-lookup"><span data-stu-id="f83e5-230">For the **Swap** field, select **Swap**.</span></span>

1. <span data-ttu-id="f83e5-231">Wählen Sie für das Feld **Quelle** die Option **Staging** aus.</span><span class="sxs-lookup"><span data-stu-id="f83e5-231">For the **Source** field, select **Staging**.</span></span>

1. <span data-ttu-id="f83e5-232">Wählen Sie für das Feld **Ziel** die Option **Produktion** aus.</span><span class="sxs-lookup"><span data-stu-id="f83e5-232">For the **Destination** field, select **Production**.</span></span>

1. <span data-ttu-id="f83e5-233">Suchen Sie am unteren Blattrand die Schaltfläche **OK**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f83e5-233">Locate and click on the **OK** button at the bottom of the blade.</span></span>

1. <span data-ttu-id="f83e5-234">Azure beginnt mit dem Austauschprozess.</span><span class="sxs-lookup"><span data-stu-id="f83e5-234">Azure starts the swapping process.</span></span> <span data-ttu-id="f83e5-235">Dieser Vorgang dauert in der Regel einige Sekunden, je nach der Größe der ausgetauschten Web-App.</span><span class="sxs-lookup"><span data-stu-id="f83e5-235">Usually, this operation takes a few seconds, depending on the size of the web app being swapped.</span></span>

1. <span data-ttu-id="f83e5-236">Wechseln Sie nach Abschluss des Vorgangs zur Web-App-URL: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="f83e5-236">Once the operation ends, visit the web app URL: [https://bestbike.azurewebsites.net/](https://bestbike.azurewebsites.net/).</span></span>

    ![Web-App-Seite](../media-draft/7-web-app-page.png)

    <span data-ttu-id="f83e5-238">Der Austauschvorgang war erfolgreich!</span><span class="sxs-lookup"><span data-stu-id="f83e5-238">The swapping operation has been successful!</span></span> <span data-ttu-id="f83e5-239">Sie sehen nun, dass der Code, den Sie in den Stagingbereitstellungsslot hochgeladen haben, auch im Produktionsslot gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="f83e5-239">You can now see the code that you uploaded to the staging deployment slot also being hosted on the production slot!</span></span>

1. <span data-ttu-id="f83e5-240">Wechseln Sie nun zur URL des Stagingslots: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="f83e5-240">Now, visit the URL of the staging slot: [https://bestbike-staging.azurewebsites.net/](https://bestbike-staging.azurewebsites.net/).</span></span>

    ![Staging-Web-App](../media-draft/7-staging-after-swapping.png)

    <span data-ttu-id="f83e5-242">Der Stagingbereitstellungsslot enthält jetzt die ursprünglichen Standard-Webanwendungsdateien, die zuvor unter dem Produktionsslot gehostet wurden.</span><span class="sxs-lookup"><span data-stu-id="f83e5-242">The staging deployment slot now contains the original, default web application files that were previously hosted under the production slot.</span></span>

<span data-ttu-id="f83e5-243">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="f83e5-243">Congratulations!</span></span> <span data-ttu-id="f83e5-244">Sie haben erfolgreich Ihre Web-App in Azure hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="f83e5-244">You have successfully uploaded your web app to Azure!</span></span>
