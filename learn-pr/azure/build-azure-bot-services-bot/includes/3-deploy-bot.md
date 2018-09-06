### <a name="exercise-3-deploy-a-bot-with-visual-studio-code"></a><span data-ttu-id="edf6c-101">Übung 3: Bereitstellen eines Bots mit Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="edf6c-101">Exercise 3: Deploy a bot with Visual Studio Code</span></span>

<span data-ttu-id="edf6c-102">Als Sie in [Übung 1](#Exercise1) einen Azure-Web-App-Bot erstellt haben, wurde eine Azure-Web-App bereitgestellt, um ihn zu hosten.</span><span class="sxs-lookup"><span data-stu-id="edf6c-102">When you created an Azure Web App Bot in [Exercise 1](#Exercise1), an Azure Web App was deployed to host it.</span></span> <span data-ttu-id="edf6c-103">Der Bot erfordert jedoch etwas Code und muss immer noch für die Azure-Web-App bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="edf6c-103">But the bot does require some code, and it still needs to be deployed to the Azure Web app.</span></span> <span data-ttu-id="edf6c-104">Glücklicherweise wurde der Code für Sie vom Azure Bot Service generiert.</span><span class="sxs-lookup"><span data-stu-id="edf6c-104">Fortunately, the code was generated for you by the Azure Bot Service.</span></span> <span data-ttu-id="edf6c-105">In dieser Übung verwenden Sie Visual Studio Code, um den Code in einem lokalen Git-Repository zu platzieren und den Bot durch Pushen von Änderungen aus dem lokalen Repository in ein mit der Azure-Web-App verbundenes Remoterepository, das den Bot hostet, in Azure zu veröffentlichen – ein als [fortlaufende Integration](https://en.wikipedia.org/wiki/Continuous_integration) bekannter Prozess.</span><span class="sxs-lookup"><span data-stu-id="edf6c-105">In this exercise, you will use Visual Studio Code to place the code in a local Git repository and publish the bot to Azure by pushing changes from the local repository to a remote repository connected to the Azure Web App that hosts the bot — a process known as [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration).</span></span>

1. <span data-ttu-id="edf6c-106">Wenn [Git](https://git-scm.com/) nicht auf Ihrem PC installiert ist, wechseln Sie zu https://git-scm.com/downloads, und installieren Sie den Git-Client für Ihr Betriebssystem.</span><span class="sxs-lookup"><span data-stu-id="edf6c-106">If [Git](https://git-scm.com/) isn't installed on your PC, go to https://git-scm.com/downloads and install the Git client for your operating system.</span></span> <span data-ttu-id="edf6c-107">Git ist ein kostenloses, verteiltes und nahtlos in Visual Studio Code integriertes Open-Source-Versionskontrollsystem.</span><span class="sxs-lookup"><span data-stu-id="edf6c-107">Git is a free and open-source distributed version-control system, and it integrates seamlessly into Visual Studio Code.</span></span> <span data-ttu-id="edf6c-108">Wenn Sie nicht sicher sind, ob Git installiert ist, öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, und führen Sie den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="edf6c-108">If you aren't sure whether Git is installed, open a Command Prompt or terminal window and execute the following command:</span></span>

    ``` 
    git --version
    ```

    <span data-ttu-id="edf6c-109">Wenn eine Versionsnummer angezeigt wird, ist der Git-Client installiert.</span><span class="sxs-lookup"><span data-stu-id="edf6c-109">If a version number is displayed, then the Git client is installed.</span></span>

1. <span data-ttu-id="edf6c-110">Wenn Node.js nicht auf Ihrem PC installiert ist, fahren Sie mit https://nodejs.org/ fort, und installieren Sie die neueste LTS-Version.</span><span class="sxs-lookup"><span data-stu-id="edf6c-110">If Node.js isn't installed on your PC, go to https://nodejs.org/ and install the latest LTS version.</span></span> <span data-ttu-id="edf6c-111">Sie können ermitteln, ob Node installiert ist, indem Sie eine Eingabeaufforderung oder ein Terminalfenster öffnen und den folgenden Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="edf6c-111">You can determine whether Node is installed by opening a Command Prompt or terminal window and typing the following command:</span></span>

    ```
    node --version
    ```

    <span data-ttu-id="edf6c-112">Wenn Node installiert ist, wird die Versionsnummer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="edf6c-112">If Node is installed, the version number will be displayed.</span></span>

1. <span data-ttu-id="edf6c-113">Wenn Visual Studio Code nicht auf Ihrem PC installiert ist, fahren Sie mit https://code.visualstudio.com/ fort, und installieren Sie es jetzt.</span><span class="sxs-lookup"><span data-stu-id="edf6c-113">If Visual Studio Code isn't installed on your PC, go to https://code.visualstudio.com/ and install it now.</span></span>

1. <span data-ttu-id="edf6c-114">Erstellen Sie auf Ihrer Festplatte einen Ordner namens „Factbot“ am Speicherort Ihrer Wahl, der den Quellcode des Bots enthalten soll.</span><span class="sxs-lookup"><span data-stu-id="edf6c-114">Create a folder named "Factbot" in the location of your choice on your hard disk to hold the bot's source code.</span></span>

1. <span data-ttu-id="edf6c-115">Kehren Sie zum Azure-Portal zurück, und öffnen Sie die Ressourcengruppe „factbot-rg“.</span><span class="sxs-lookup"><span data-stu-id="edf6c-115">Return to the Azure Portal and open the "factbot-rg" resource group.</span></span> <span data-ttu-id="edf6c-116">Klicken Sie dann auf den Web-App-Bot, den Sie in [Übung 1](#Exercise1) erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="edf6c-116">Then click the Web App Bot you created in [Exercise 1](#Exercise1).</span></span>

    ![Öffnen des Web-App-Bots](../images/open-web-app-bot.png)

    <span data-ttu-id="edf6c-118">_Öffnen des Web-App-Bots_</span><span class="sxs-lookup"><span data-stu-id="edf6c-118">_Opening the Web App Bot_</span></span>

1. <span data-ttu-id="edf6c-119">Klicken Sie im Menü auf der linken Seite auf **Erstellen** und dann auf **ZIP-Datei herunterladen**, um eine ZIP-Datei vorzubereiten, die den Quellcode des Bots enthält.</span><span class="sxs-lookup"><span data-stu-id="edf6c-119">Click **Build** in the menu on the left, and then click **Download zip file** to prepare a zip file containing the bot's source code.</span></span> <span data-ttu-id="edf6c-120">Sobald die ZIP-Datei vorbereitet ist, klicken Sie auf die Schaltfläche **ZIP-Datei herunterladen**, um sie herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="edf6c-120">Once the zip file is prepared, click the **Download zip file** button to download it.</span></span> <span data-ttu-id="edf6c-121">Wenn der Download abgeschlossen ist, kopieren Sie den Inhalt der ZIP-Datei in den Ordner „Factbot“, den Sie in Schritt 4 erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="edf6c-121">When the download is complete, copy the contents of the zip file to the "Factbot" folder that you created in Step 4.</span></span>

    ![Herunterladen des Quellcodes](../images/download-source.png)

    <span data-ttu-id="edf6c-123">_Herunterladen des Quellcodes_</span><span class="sxs-lookup"><span data-stu-id="edf6c-123">_Downloading the source code_</span></span>
  
1. <span data-ttu-id="edf6c-124">Klicken Sie – immer noch auf dem Blatt „Erstellen“ – auf **Konfigurieren von Continuous Deployment**.</span><span class="sxs-lookup"><span data-stu-id="edf6c-124">Still on the "Build" blade, click **Configure continuous deployment**.</span></span> <span data-ttu-id="edf6c-125">Klicken Sie am oberen Rand des folgenden Blatts auf **Setup**, gefolgt von **Quelle auswählen**.</span><span class="sxs-lookup"><span data-stu-id="edf6c-125">Click **Setup** at the top of the ensuing blade, followed by **Choose Source**.</span></span> <span data-ttu-id="edf6c-126">Wählen Sie dann **Lokales Git-Repository** als Bereitstellungsquelle aus, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="edf6c-126">Then select **Local Git Repository** as the deployment source and click **OK**.</span></span> 
 
    ![Angeben eines lokalen Git-Repositorys als Bereitstellungsquelle](../images/portal-set-local-git.png)

    <span data-ttu-id="edf6c-128">_Angeben eines lokalen Git-Repositorys als Bereitstellungsquelle_</span><span class="sxs-lookup"><span data-stu-id="edf6c-128">_Specifying a local Git repository as the deployment source_</span></span>  

1. <span data-ttu-id="edf6c-129">Schließen Sie das Blatt „Bereitstellungen“, und klicken Sie im Menü auf der linken Seite auf **Alle App Service-Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="edf6c-129">Close the "Deployments" blade and click **All App service settings** in the menu on the left.</span></span>

1. <span data-ttu-id="edf6c-130">Klicken Sie auf **Anmeldeinformationen für die Bereitstellung**, und geben Sie einen Benutzernamen und ein Kennwort ein.</span><span class="sxs-lookup"><span data-stu-id="edf6c-130">Click **Deployment credentials**, and then enter a user name and password.</span></span> <span data-ttu-id="edf6c-131">Wahrscheinlich müssen Sie einen anderen Benutzernamen als „FactbotAdministrator“ eingeben, da der Name innerhalb von Azure eindeutig sein muss.</span><span class="sxs-lookup"><span data-stu-id="edf6c-131">You will probably have to enter a user name other than "FactbotAdministrator" because the name must be unique within Azure.</span></span> <span data-ttu-id="edf6c-132">Klicken Sie dann auf **Speichern**, und schließen Sie das Blatt.</span><span class="sxs-lookup"><span data-stu-id="edf6c-132">Then click **Save** and close the blade.</span></span>

    ![Eingeben von Anmeldeinformationen für die Bereitstellung](../images/portal-enter-ci-creds.png)

    <span data-ttu-id="edf6c-134">_Eingeben von Anmeldeinformationen für die Bereitstellung_</span><span class="sxs-lookup"><span data-stu-id="edf6c-134">_Entering deployment credentials_</span></span>  

1. <span data-ttu-id="edf6c-135">Starten Sie Visual Studio Code, und öffnen Sie mit dem Befehl **Datei** > **Ordner öffnen...** den Ordner „Factbot“, in den Sie in Schritt 6 den Quellcode des Bots kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="edf6c-135">Start Visual Studio Code and use the **File** > **Open Folder...** command to open the "Factbot" folder that you copied the bot's source code to in Step 6.</span></span>

1. <span data-ttu-id="edf6c-136">Klicken Sie in der Aktivitätsleiste auf der linken Seite von Visual Studio Code auf die Schaltfläche **Quellcodeverwaltung** und dann oben auf das Symbol **Repository initialisieren**.</span><span class="sxs-lookup"><span data-stu-id="edf6c-136">Click the **Source Control** button in the activity bar on the left side of Visual Studio Code, and click the **Initialize Repository** icon at the top.</span></span> <span data-ttu-id="edf6c-137">Klicken Sie dann im folgenden Dialogfeld auf die Schaltfläche **Repository initialisieren**.</span><span class="sxs-lookup"><span data-stu-id="edf6c-137">Then click the **Intialize Repository** button in the ensuing dialog.</span></span>

    ![Initialisieren eines lokalen Git-Repositorys](../images/vs-init-git-repo.png)

    <span data-ttu-id="edf6c-139">_Initialisieren eines lokalen Git-Repositorys_</span><span class="sxs-lookup"><span data-stu-id="edf6c-139">_Initializing a local Git repository_</span></span>  

1. <span data-ttu-id="edf6c-140">Geben Sie „First commit“ (Erster Commit)</span><span class="sxs-lookup"><span data-stu-id="edf6c-140">Type "First commit."</span></span> <span data-ttu-id="edf6c-141">in das Nachrichtenfeld ein, und klicken Sie dann auf das Häkchen, um Ihre Änderungen zu übernehmen.</span><span class="sxs-lookup"><span data-stu-id="edf6c-141">into the message box, and then click the check mark to commit your changes.</span></span>

    ![Committen von Änderungen an das lokale Repository](../images/vs-first-git-commit.png)

    <span data-ttu-id="edf6c-143">_Committen von Änderungen an das lokale Repository_</span><span class="sxs-lookup"><span data-stu-id="edf6c-143">_Committing changes to the local repository_</span></span>  

1. <span data-ttu-id="edf6c-144">Wählen Sie **Integriertes Terminal** im Menü **Ansicht** von Visual Studio Code aus, um ein integriertes Terminal zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="edf6c-144">Select **Integrated Terminal** from Visual Studio Code's **View** menu to open an integrated terminal.</span></span> <span data-ttu-id="edf6c-145">Führen Sie dann den folgenden Befehl im integrierten Terminal aus, wobei Sie BOT_NAME an zwei Stellen durch den Bot-Namen ersetzen, den Sie in Übung 1, Schritt 3 eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="edf6c-145">Then execute the following command in the integrated terminal, replacing BOT_NAME in two places with the bot name you entered in Exercise 1, Step 3.</span></span>

    ```
    git remote add qna-factbot https://BOT_NAME.scm.azurewebsites.net:443/BOT_NAME.git
    ```

1. <span data-ttu-id="edf6c-146">Klicken Sie auf die Auslassungspunkte (drei Punkte) am oberen Rand der QUELLCODEVERWALTUNG, und wählen Sie **Branch veröffentlichen** im Menü aus, um den Botcode aus dem lokalen Repository nach Azure zu pushen.</span><span class="sxs-lookup"><span data-stu-id="edf6c-146">Click the ellipsis (the three dots) at the top of the SOURCE CONTROL panel and select **Publish Branch** from the menu to push the bot code from the local repository to Azure.</span></span> <span data-ttu-id="edf6c-147">Wenn Sie zur Eingabe von Anmeldeinformationen aufgefordert werden, geben Sie den Benutzernamen und das Kennwort ein, die Sie in Schritt 9 dieser Übung angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="edf6c-147">If prompted for credentials, enter the user name and password you specified in Step 9 of this exercise.</span></span>

<span data-ttu-id="edf6c-148">Ihr Bot wurde in Azure veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="edf6c-148">Your bot has been published to Azure.</span></span> <span data-ttu-id="edf6c-149">Aber bevor Sie ihn dort testen, lassen Sie uns ihn lokal ausführen, und erfahren Sie, wie Sie ihn in Visual Studio Code debuggen können.</span><span class="sxs-lookup"><span data-stu-id="edf6c-149">But before you test it there, let's run it locally and learn how to debug it in Visual Studio Code.</span></span>
