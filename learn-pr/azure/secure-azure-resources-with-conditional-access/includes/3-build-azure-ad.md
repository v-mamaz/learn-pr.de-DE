<span data-ttu-id="8265c-101">Angenommen, Sie möchten Azure Active Directory bereitstellen und verwenden Richtlinien für bedingten Zugriff, sodass für den Zugriff auf das Azure-Portal Multi-Factor Authentication erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="8265c-101">You decide to deploy Azure AD and use conditional access policies that Azure require Multi-Factor Authentication when anyone accesses the Azure portal.</span></span> <span data-ttu-id="8265c-102">Sie müssen ein Verzeichnis erstellen und temporäre Lizenzen zuweisen.</span><span class="sxs-lookup"><span data-stu-id="8265c-102">You need to create a directory and get temporary licenses in place.</span></span>

## <a name="launch-lab-and-sign-in-to-the-azure-portal"></a><span data-ttu-id="8265c-103">Starten des Labs und Anmelden beim Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="8265c-103">Launch lab and sign in to the Azure portal</span></span>

1. <span data-ttu-id="8265c-104">Klicken Sie auf den obigen Link **Lab starten**, um das Lab zu starten.</span><span class="sxs-lookup"><span data-stu-id="8265c-104">Click the **Launch Lab** link above to launch the lab.</span></span>

> [!NOTE]
> <span data-ttu-id="8265c-105">Nachdem das Lab gestartet wurde, finden Sie die erforderlichen Anmeldeinformationen auf der Registerkarte **Ressourcen** neben den Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="8265c-105">After launching the lab, the username and password you need to sign in with is located on the **Resources** tab next to the instructions.</span></span>

## <a name="create-a-directory"></a><span data-ttu-id="8265c-106">Erstellen eines Verzeichnisses</span><span class="sxs-lookup"><span data-stu-id="8265c-106">Create a directory</span></span>

<span data-ttu-id="8265c-107">Zuerst wird ein neues Verzeichnis für First Up Consultants erstellt, in dem ohne Auswirkungen auf die Produktionsbenutzer getestet werden kann.</span><span class="sxs-lookup"><span data-stu-id="8265c-107">We will create a new directory for First Up Consultants where we can test without fear of impacting production users.</span></span>

1. <span data-ttu-id="8265c-108">Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="8265c-108">Sign into the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

2. <span data-ttu-id="8265c-109">Klicken Sie im linken Navigationsbereich auf **Ressource erstellen** > **Identität** > **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8265c-109">In the left navigation pane, click **Create a resource** > **Identity** > **Azure Active Directory**.</span></span>

3. <span data-ttu-id="8265c-110">Geben Sie auf dem Blatt **Verzeichnis erstellen** die folgenden Werte für **Organisationsname** und **Name der Anfangsdomäne** ein:</span><span class="sxs-lookup"><span data-stu-id="8265c-110">In the **Create directory** blade, provide the following values for the **Organization name** and **Initial domain name**:</span></span>

   1. <span data-ttu-id="8265c-111">Organisationsname: `First Up Consultants`</span><span class="sxs-lookup"><span data-stu-id="8265c-111">Organization Name: `First Up Consultants`.</span></span>
   2. <span data-ttu-id="8265c-112">Name der Anfangsdomäne: `firstupconsultants<XXXXXXX>`, wobei <XXXXXXX> die Zahl ist, die nach dem Benutzernamen auf der Registerkarte **Ressourcen** am oberen Rand des Fensters mit den Anweisungen angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="8265c-112">Initial Domain Name: `firstupconsultants<XXXXXXX>` where <XXXXXXX> is the number after the username on the **Resources** tab at the top of the instructions window.</span></span>

4. <span data-ttu-id="8265c-113">Warten Sie, bis das Verzeichnis erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="8265c-113">Wait for the directory to be created.</span></span> <span data-ttu-id="8265c-114">Klicken Sie auf den Link, um in das neue Verzeichnis zu wechseln, oder klicken Sie oben im Fenster auf **Verzeichnis- und Abonnementfilter**, und wählen Sie das neu erstellte Verzeichnis aus.</span><span class="sxs-lookup"><span data-stu-id="8265c-114">Click the link to switch to the new directory or click the **Directory and subscription filter** at the top of the window and then choose the newly created directory.</span></span>

## <a name="get-trial-licenses"></a><span data-ttu-id="8265c-115">Erhalten von Testlizenzen</span><span class="sxs-lookup"><span data-stu-id="8265c-115">Get trial licenses</span></span>

<span data-ttu-id="8265c-116">Um Features wie den bedingten Zugriff und Multi-Factor Authentication zu verwenden, benötigen Sie mindestens eine Testlizenz.</span><span class="sxs-lookup"><span data-stu-id="8265c-116">To use features like conditional access and Multi-Factor Authentication, you will need at least a trial license.</span></span> <span data-ttu-id="8265c-117">Im Anschluss finden Sie eine Anleitung für das Aktivieren einer Testlizenz:</span><span class="sxs-lookup"><span data-stu-id="8265c-117">The following steps walk you through how to enable a trial license:</span></span>

1. <span data-ttu-id="8265c-118">Klicken Sie im Azure AD-Bereich **Übersicht** auf den Link **Kostenlose Testversion starten**.</span><span class="sxs-lookup"><span data-stu-id="8265c-118">In the Azure AD **Overview** pane, click the **Start a free trial** link.</span></span>

1. <span data-ttu-id="8265c-119">Klicken Sie unter dem Element **Azure AD Premium P2** auf **Kostenlose Testversion**, und klicken Sie dann auf **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="8265c-119">Under the item **Azure AD Premium P2**, click **Free trial**, and then click **Activate**.</span></span>

## <a name="create-a-test-user"></a><span data-ttu-id="8265c-120">Erstellen eines Testbenutzers</span><span class="sxs-lookup"><span data-stu-id="8265c-120">Create a test user</span></span>

<span data-ttu-id="8265c-121">Die Lizenz muss mit einem Benutzer getestet werden.</span><span class="sxs-lookup"><span data-stu-id="8265c-121">We're going to need to test this out with a user.</span></span> <span data-ttu-id="8265c-122">Isabella Simonsen, ein Mitglied Ihres Teams, hilft Ihnen dabei. Sie benötigt dazu ein Konto für das Verzeichnis. Wie Sie eines erstellen, erfahren Sie in den folgenden Schritten.</span><span class="sxs-lookup"><span data-stu-id="8265c-122">Isabella Simonsen (another member of your team) has volunteered to help you out. She will need an account in the directory, so we will go through the steps to create her account.</span></span>

1. <span data-ttu-id="8265c-123">Navigieren Sie zu **Azure Active Directory** > **Benutzer**.</span><span class="sxs-lookup"><span data-stu-id="8265c-123">Browse to **Azure Active Directory** > **Users**.</span></span>

1. <span data-ttu-id="8265c-124">Klicken Sie auf **Neuer Benutzer**.</span><span class="sxs-lookup"><span data-stu-id="8265c-124">Click **New user**.</span></span>

1. <span data-ttu-id="8265c-125">Erstellen Sie einen Benutzer namens **Isabella Simonsen** mit dem folgenden Benutzernamen:</span><span class="sxs-lookup"><span data-stu-id="8265c-125">Create a user named **Isabella Simonsen** with a user name of:</span></span>

   `Isabella@firstupconsultants<XXXXXXX>.onmicrosoft.com`

   <span data-ttu-id="8265c-126">Ordnen Sie die Domäne nach dem @-Zeichen der Domäne zu, die Sie im Abschnitt *Erstellen eines Verzeichnisses* oben erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="8265c-126">Match the domain after the @ with the domain you created in the *Create a directory* section above.</span></span>

1. <span data-ttu-id="8265c-127">Aktivieren Sie das Kontrollkästchen **Kennwort anzeigen** für den Benutzer.</span><span class="sxs-lookup"><span data-stu-id="8265c-127">Check the box to **Show Password** for the user.</span></span> <span data-ttu-id="8265c-128">Notieren Sie sich das Kennwort, damit Sie es später beim Testen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="8265c-128">Make a note of the password so you can use it later when testing.</span></span>

1. <span data-ttu-id="8265c-129">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="8265c-129">Click **Create**.</span></span>

## <a name="create-a-pilot-group"></a><span data-ttu-id="8265c-130">Erstellen einer Pilotgruppe</span><span class="sxs-lookup"><span data-stu-id="8265c-130">Create a pilot group</span></span>

<span data-ttu-id="8265c-131">Die Richtlinie, die erstellt wird, soll einer Benutzergruppe zugewiesen werden. Dazu muss zunächst eine Gruppe für diese Richtlinie erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="8265c-131">We will be assigning the policy that we create to a group of users, but we need to create a group for this policy.</span></span> <span data-ttu-id="8265c-132">Anhand der folgenden Schritte können Sie eine Sicherheitsgruppe für die Pilotbereitstellung erstellen.</span><span class="sxs-lookup"><span data-stu-id="8265c-132">The following steps help you create a security group for the pilot deployment.</span></span>

1. <span data-ttu-id="8265c-133">Navigieren Sie zu **Azure Active Directory** > **Gruppen**.</span><span class="sxs-lookup"><span data-stu-id="8265c-133">Browse to **Azure Active Directory** > **Groups**.</span></span>

1. <span data-ttu-id="8265c-134">Klicken Sie auf **Neue Gruppe**.</span><span class="sxs-lookup"><span data-stu-id="8265c-134">Click **New group**.</span></span>

1. <span data-ttu-id="8265c-135">Legen Sie als Gruppentyp **Sicherheit** fest.</span><span class="sxs-lookup"><span data-stu-id="8265c-135">Group type **Security**.</span></span>

1. <span data-ttu-id="8265c-136">Legen Sie als Gruppenname **CA-MFA-AzurePortal** fest.</span><span class="sxs-lookup"><span data-stu-id="8265c-136">Group name **CA-MFA-AzurePortal**.</span></span>

1. <span data-ttu-id="8265c-137">Legen Sie als Mitgliedschaftstyp **Zugewiesen** fest.</span><span class="sxs-lookup"><span data-stu-id="8265c-137">Membership type **Assigned**.</span></span>

1. <span data-ttu-id="8265c-138">Wählen Sie den Benutzer aus, der im vorherigen Schritt erstellt wurde, und klicken Sie auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="8265c-138">Select the user that we created in the previous step and choose **Select**.</span></span>

1. <span data-ttu-id="8265c-139">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="8265c-139">Click **Create**.</span></span>

<span data-ttu-id="8265c-140">In dieser Einheit haben Sie erfahren, wie Sie ein Verzeichnis mit einer Testlizenz, einen Testbenutzer und eine Pilotgruppe im Azure-Portal erstellen.</span><span class="sxs-lookup"><span data-stu-id="8265c-140">In this unit, you learned how to create a trial licensed directory, a test user, and a pilot group in the Azure portal.</span></span>