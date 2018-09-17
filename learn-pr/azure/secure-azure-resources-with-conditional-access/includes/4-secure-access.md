<span data-ttu-id="c7402-101">In der vorherigen Übung haben wir zum Testen unserer Lösung Testlizenzen aktiviert bzw. ein Verzeichnis, einen Benutzer und eine Gruppe erstellt.</span><span class="sxs-lookup"><span data-stu-id="c7402-101">In the previous exercise, we enabled trial licenses, created a directory, created a user, and created a group to test our solution.</span></span> <span data-ttu-id="c7402-102">In dieser Einheit erstellen wir die Regel für bedingten Zugriff, sodass für den Zugriff auf das Azure-Portal Multi-Factor Authentication erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="c7402-102">In this unit, we will create our conditional access rule to require Azure Multi-Factor Authentication for the Azure portal.</span></span>

## <a name="enable-conditional-access-based-multi-factor-authentication"></a><span data-ttu-id="c7402-103">Aktivieren von MFA mit bedingtem Zugriff</span><span class="sxs-lookup"><span data-stu-id="c7402-103">Enable conditional access-based Multi-Factor Authentication</span></span>

<span data-ttu-id="c7402-104">Durch den bedingten Zugriff können Administratoren konfigurieren, was sie zulassen und was nicht.</span><span class="sxs-lookup"><span data-stu-id="c7402-104">Conditional access allows administrators to configure when they do or do not want something to happen.</span></span> <span data-ttu-id="c7402-105">Sie können gleichzeitig mehrere Regeln verwenden, um den Zugriff auf Ressourcen zu gewähren oder zu verweigern.</span><span class="sxs-lookup"><span data-stu-id="c7402-105">They can use multiple rules in parallel to grant or deny access to resources.</span></span> <span data-ttu-id="c7402-106">Hier ist die Regel, die wir erstellen müssen:</span><span class="sxs-lookup"><span data-stu-id="c7402-106">Here's the rule that we need to create:</span></span>

<span data-ttu-id="c7402-107">**Beim Zugriff auf das Azure-Portal: mehrstufige Authentifizierung anfordern**</span><span class="sxs-lookup"><span data-stu-id="c7402-107">**When accessing the Azure portal - Require multi-factor authentication**</span></span>

<span data-ttu-id="c7402-108">Die folgenden Schritte führen Sie durch den Prozess zum Erstellen einer Regel für den bedingten Zugriff, damit Benutzer eine mehrstufige Authentifizierung durchführen müssen, wenn sie auf das Azure-Portal zugreifen.</span><span class="sxs-lookup"><span data-stu-id="c7402-108">The steps that follow will walk you through the process to create a conditional access rule to require users to perform multi-factor authentication when they access the Azure portal.</span></span>

1. <span data-ttu-id="c7402-109">Navigieren Sie zu **Azure Active Directory** > **Bedingter Zugriff**.</span><span class="sxs-lookup"><span data-stu-id="c7402-109">Browse to **Azure Active Directory** > **Conditional access**.</span></span>

1. <span data-ttu-id="c7402-110">Klicken Sie auf **Neue Richtlinie**.</span><span class="sxs-lookup"><span data-stu-id="c7402-110">Click **New policy**.</span></span>

1. <span data-ttu-id="c7402-111">Benennen Sie die Richtlinie **Mehrstufige Authentifizierung für Zugriff auf Azure-Portal erforderlich**.</span><span class="sxs-lookup"><span data-stu-id="c7402-111">Name the policy **Require MFA for Azure portal**.</span></span>

1. <span data-ttu-id="c7402-112">Klicken Sie unter **Zuweisungen** > **Benutzer und Gruppen** auf **Benutzer und Gruppen**.</span><span class="sxs-lookup"><span data-stu-id="c7402-112">Under **Assignments** > **Users and groups**, select **Users and groups**.</span></span> <span data-ttu-id="c7402-113">Wählen Sie die erstellte Gruppe **CA-MFA-AzurePortal** aus.</span><span class="sxs-lookup"><span data-stu-id="c7402-113">Select the group that we created **CA-MFA-AzurePortal**.</span></span> <span data-ttu-id="c7402-114">Klicken Sie dann auf **Fertig**.</span><span class="sxs-lookup"><span data-stu-id="c7402-114">and click **Done**.</span></span>

1. <span data-ttu-id="c7402-115">Klicken Sie unter **Cloud-Apps** > **Apps auswählen** auf **Microsoft Azure Management**.</span><span class="sxs-lookup"><span data-stu-id="c7402-115">Under **Cloud apps** > **Select apps**, select **Microsoft Azure Management**.</span></span>

1. <span data-ttu-id="c7402-116">Klicken Sie unter **Zugriffssteuerung** > **Gewähren** auf **Mehrstufige Authentifizierung anfordern**.</span><span class="sxs-lookup"><span data-stu-id="c7402-116">Under **Access controls** > **Grant**, select **Require multi-factor authentication**.</span></span>

1. <span data-ttu-id="c7402-117">Legen Sie **Richtlinie aktivieren** auf **Ein** fest.</span><span class="sxs-lookup"><span data-stu-id="c7402-117">Set **Enable policy** to **On**.</span></span>

1. <span data-ttu-id="c7402-118">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="c7402-118">Click **Create**.</span></span>

## <a name="summary"></a><span data-ttu-id="c7402-119">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="c7402-119">Summary</span></span>

<span data-ttu-id="c7402-120">In dieser Einheit haben Sie gelernt, wie Sie eine Regel mit bedingtem Zugriff erstellen.</span><span class="sxs-lookup"><span data-stu-id="c7402-120">In this unit, you learned how to create a conditional access rule.</span></span> <span data-ttu-id="c7402-121">Die Regel erfordert Multi-Factor Authentication beim Zugriff auf das Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="c7402-121">The rule requires Multi-Factor Authentication when accessing the Azure portal.</span></span>
