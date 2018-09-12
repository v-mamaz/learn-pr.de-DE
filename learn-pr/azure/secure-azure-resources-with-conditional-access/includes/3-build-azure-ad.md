<span data-ttu-id="52996-101">Angenommen, Sie möchten Azure Active Directory bereitstellen und verwenden Richtlinien für bedingten Zugriff, sodass für den Zugriff auf das Azure-Portal Multi-Factor Authentication erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="52996-101">You decide to deploy Azure AD and use conditional access policies that Azure require Multi-Factor Authentication when anyone accesses the Azure portal.</span></span> <span data-ttu-id="52996-102">Sie müssen ein Verzeichnis erstellen und temporäre Lizenzen zuweisen.</span><span class="sxs-lookup"><span data-stu-id="52996-102">You need to create a directory and get temporary licenses in place.</span></span>

## <a name="create-a-directory"></a><span data-ttu-id="52996-103">Erstellen eines Verzeichnisses</span><span class="sxs-lookup"><span data-stu-id="52996-103">Create a directory</span></span>
<span data-ttu-id="52996-104">Zuerst wird ein neues Verzeichnis für First Up Consultants, in dem ohne Auswirkungen auf die Produktionsbenutzer getestet werden kann.</span><span class="sxs-lookup"><span data-stu-id="52996-104">We will create a new directory for First Up Consultants where we can test without fear of impacting production users.</span></span>

1. <span data-ttu-id="52996-105">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="52996-105">Sign in to the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

1. <span data-ttu-id="52996-106">Klicken Sie im linken Navigationsbereich auf **Ressource erstellen** > **Identität** > **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52996-106">In the left navigation pane, click **Create a resource** > **Identity** > **Azure Active Directory**.</span></span>

1. <span data-ttu-id="52996-107">Geben Sie auf dem Blatt **Verzeichnis erstellen** die folgenden Werte für **Organisationsname** und **Name der Anfangsdomäne** ein:</span><span class="sxs-lookup"><span data-stu-id="52996-107">In the **Create directory** blade, provide the following values for the **Organization name** and **Initial domain name**:</span></span>

   1. <span data-ttu-id="52996-108">ORGANISATIONSNAME: `First Up Consultants`</span><span class="sxs-lookup"><span data-stu-id="52996-108">ORGANIZATION NAME: `First Up Consultants`.</span></span>
   1. <span data-ttu-id="52996-109">NAME DER ANFANGSDOMÄNE: `firstupconsultants<XXXX>.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="52996-109">INITIAL DOMAIN NAME: `firstupconsultants<XXXX>.onmicrosoft.com`.</span></span>

1. <span data-ttu-id="52996-110">Warten Sie, bis das Verzeichnis erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="52996-110">Wait for the directory to be created.</span></span> <span data-ttu-id="52996-111">Klicken Sie auf den Link, um in das neue Verzeichnis zu wechseln, oder klicken Sie oben im Fenster auf **Directory and subscription filter** (Verzeichnis- und Abonnementfilter), und wählen Sie das neu erstellte Verzeichnis aus.</span><span class="sxs-lookup"><span data-stu-id="52996-111">Click the link to switch to the new directory, or click the **Directory and subscription filter** at the top of the window and then choose the newly created directory.</span></span>

## <a name="get-trial-licenses"></a><span data-ttu-id="52996-112">Erhalten von Testlizenzen</span><span class="sxs-lookup"><span data-stu-id="52996-112">Get trial licenses</span></span>

<span data-ttu-id="52996-113">Damit Sie Features wie den bedingten Zugriff und Multi-Factor Authentication verwenden können, benötigen Sie mindestens eine Testlizenz.</span><span class="sxs-lookup"><span data-stu-id="52996-113">In order for you to use features like conditional access and Multi-Factor Authentication, you will need at least a trial license.</span></span> <span data-ttu-id="52996-114">Im Anschluss finden Sie eine Anleitung für das Aktivieren einer Testlizenz:</span><span class="sxs-lookup"><span data-stu-id="52996-114">The following steps walk you through how to enable a trial license:</span></span>

1. <span data-ttu-id="52996-115">Klicken Sie im Azure AD-Bereich **Übersicht** auf den Link **Kostenlose Testversion starten**.</span><span class="sxs-lookup"><span data-stu-id="52996-115">In the Azure AD **Overview** pane, click the **Start a free trial** link.</span></span>

1. <span data-ttu-id="52996-116">Klicken Sie unter dem Element **Azure AD Premium P2** auf **Kostenlose Testversion**, und klicken Sie dann auf **Aktivieren**.</span><span class="sxs-lookup"><span data-stu-id="52996-116">Under the item **Azure AD Premium P2**, click **Free trial**, and then click **Activate**.</span></span>

## <a name="create-a-test-user"></a><span data-ttu-id="52996-117">Erstellen eines Testbenutzers</span><span class="sxs-lookup"><span data-stu-id="52996-117">Create a test user</span></span>

<span data-ttu-id="52996-118">Die Lizenz muss mit einem Benutzer getestet werden.</span><span class="sxs-lookup"><span data-stu-id="52996-118">We're going to need to test this out with a user.</span></span> <span data-ttu-id="52996-119">Isabella Simonsen, ein Mitglied Ihres Teams, hilft Ihnen dabei. Sie benötigt dazu ein Konto für das Verzeichnis. Wie Sie eines erstellen, erfahren Sie in den folgenden Schritten.</span><span class="sxs-lookup"><span data-stu-id="52996-119">Isabella Simonsen (another member of your team) has volunteered to help you out. She will need an account in the directory, so we will go through the steps to create her account.</span></span>

1. <span data-ttu-id="52996-120">Navigieren Sie zu **Azure Active Directory** > **Benutzer** > **Alle Benutzer**.</span><span class="sxs-lookup"><span data-stu-id="52996-120">Browse to **Azure Active Directory** > **Users** > **All users**.</span></span>

1. <span data-ttu-id="52996-121">Klicken Sie auf **Neuer Benutzer**.</span><span class="sxs-lookup"><span data-stu-id="52996-121">Click **New user**.</span></span>

1. <span data-ttu-id="52996-122">Erstellen Sie einen Benutzer namens **Isabella Simonsen** mit dem folgenden Benutzernamen:</span><span class="sxs-lookup"><span data-stu-id="52996-122">Create a user named **Isabella Simonsen** with a user name of:</span></span>

   * `Isabella@firstupconsultants<XXXX>.onmicrosoft.com`

1. <span data-ttu-id="52996-123">Aktivieren Sie das Kontrollkästchen **Kennwort anzeigen** für den Benutzer.</span><span class="sxs-lookup"><span data-stu-id="52996-123">Check the box to **Show Password** for the user.</span></span> <span data-ttu-id="52996-124">Notieren Sie sich das Kennwort, damit Sie es später beim Testen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="52996-124">Make a note of the password so you can use it later when testing.</span></span>

1. <span data-ttu-id="52996-125">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="52996-125">Click **Create**.</span></span>

## <a name="create-a-pilot-group"></a><span data-ttu-id="52996-126">Erstellen einer Pilotgruppe</span><span class="sxs-lookup"><span data-stu-id="52996-126">Create a pilot group</span></span>

<span data-ttu-id="52996-127">Die Richtlinie, die erstellt wird, soll einer Benutzergruppe zugewiesen werden. Dazu muss zunächst eine Gruppe für diese Richtlinie erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="52996-127">We will be assigning the policy that we create to a group of users, but we need to create a group for this policy.</span></span> <span data-ttu-id="52996-128">Anhand der folgenden Schritte können Sie eine Sicherheitsgruppe für die Pilotbereitstellung erstellen.</span><span class="sxs-lookup"><span data-stu-id="52996-128">The following steps help you create a security group for the pilot deployment.</span></span>

1. <span data-ttu-id="52996-129">Navigieren Sie zu **Azure Active Directory** > **Gruppen** > **Alle Gruppen**.</span><span class="sxs-lookup"><span data-stu-id="52996-129">Browse to **Azure Active Directory** > **Groups** > **All groups**.</span></span>

1. <span data-ttu-id="52996-130">Klicken Sie auf **Neue Gruppe**.</span><span class="sxs-lookup"><span data-stu-id="52996-130">Click **New group**.</span></span>

1. <span data-ttu-id="52996-131">Legen Sie als Gruppentyp **Sicherheit** fest.</span><span class="sxs-lookup"><span data-stu-id="52996-131">Group type **Security**.</span></span>

1. <span data-ttu-id="52996-132">Legen Sie als Gruppenname **CA-MFA-AzurePortal** fest.</span><span class="sxs-lookup"><span data-stu-id="52996-132">Group name **CA-MFA-AzurePortal**.</span></span>

1. <span data-ttu-id="52996-133">Legen Sie als Mitgliedschaftstyp **Zugewiesen** fest.</span><span class="sxs-lookup"><span data-stu-id="52996-133">Membership type **Assigned**.</span></span>

1. <span data-ttu-id="52996-134">Wählen Sie den Benutzer aus, der im vorherigen Schritt erstellt wurde, und klicken Sie auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="52996-134">Select the user that we created in the previous step, and choose **Select**.</span></span>

1. <span data-ttu-id="52996-135">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="52996-135">Click **Create**.</span></span>

## <a name="summary"></a><span data-ttu-id="52996-136">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="52996-136">Summary</span></span>

<span data-ttu-id="52996-137">In dieser Einheit haben Sie erfahren, wie Sie ein Verzeichnis mit einer Testlizenz, einen Testbenutzer und eine Pilotgruppe im Azure-Portal erstellen.</span><span class="sxs-lookup"><span data-stu-id="52996-137">In this unit, you learned how to create a trial licensed directory, a test user, and a pilot group in the Azure portal.</span></span>
