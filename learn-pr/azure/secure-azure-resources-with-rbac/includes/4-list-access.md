<span data-ttu-id="a34ca-101">Bei First Up Consultants wurde Ihnen Zugriff auf das Azure-Abonnement für das Marketingteam gewährt.</span><span class="sxs-lookup"><span data-stu-id="a34ca-101">At First Up Consultants, you've been granted access to the Azure subscription for the marketing team.</span></span> <span data-ttu-id="a34ca-102">Sie möchten sich mit dem Azure-Portal vertraut machen und sehen, welche Rollen derzeit zugewiesen sind.</span><span class="sxs-lookup"><span data-stu-id="a34ca-102">You want to familiarize yourself with the Azure portal and see what roles are currently assigned.</span></span>

## <a name="list-role-assignments-for-yourself"></a><span data-ttu-id="a34ca-103">Liste von Rollenzuweisungen für Sie selbst</span><span class="sxs-lookup"><span data-stu-id="a34ca-103">List role assignments for yourself</span></span>

<span data-ttu-id="a34ca-104">Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen Ihnen zurzeit zugewiesen sind.</span><span class="sxs-lookup"><span data-stu-id="a34ca-104">Follow these steps to see what roles are currently assigned to you.</span></span>

1. <span data-ttu-id="a34ca-105">Navigieren Sie zum [Azure-Portal](https://portal.azure.com/?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="a34ca-105">Navigate to the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

1. <span data-ttu-id="a34ca-106">Klicken Sie in der Navigationsliste auf **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a34ca-106">In the navigation list, click **Azure Active Directory**.</span></span>

1. <span data-ttu-id="a34ca-107">Klicken Sie auf **Benutzer**, um **Alle Benutzer** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="a34ca-107">Click **Users** to open **All users**.</span></span>

    ![Benutzer von Azure Active Directory](../media-draft/4-aad-all-users.png)

1. <span data-ttu-id="a34ca-109">Suchen Sie den Benutzernamen **LabAdmin-_XXXXXXX_**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="a34ca-109">Find and click the **LabAdmin-_XXXXXXX_** user name.</span></span>

    ![Lab-User von Azure Active Directory](../media-draft/4-aad-all-users-lab.png)

1. <span data-ttu-id="a34ca-111">Klicken Sie im Abschnitt **Verwalten** auf **Azure-Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="a34ca-111">In the **Manage** section, click **Azure resources**.</span></span>

    ![Azure-Ressourcen](../media-draft/4-aad-user-azure-resources.png)

    <span data-ttu-id="a34ca-113">Auf dem Blatt „Azure-Ressourcen“ können Sie die Ressourcen und Rollen sehen, auf die Sie Zugriff haben.</span><span class="sxs-lookup"><span data-stu-id="a34ca-113">On the Azure resources blade, you can see the resources and roles you have access to.</span></span> <span data-ttu-id="a34ca-114">Ihre Liste wird anders aussehen.</span><span class="sxs-lookup"><span data-stu-id="a34ca-114">Your list will look different.</span></span>

## <a name="list-role-assignments-for-a-resource-group"></a><span data-ttu-id="a34ca-115">Auflisten von Rollenzuweisungen für eine Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="a34ca-115">List role assignments for a resource group</span></span>

<span data-ttu-id="a34ca-116">Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen im Bereich der Ressourcengruppen zugewiesen wurden.</span><span class="sxs-lookup"><span data-stu-id="a34ca-116">Follow these steps to see what roles are assigned at the resource group scope.</span></span>

1. <span data-ttu-id="a34ca-117">Klicken Sie in der Navigationsliste auf **Ressourcengruppen**.</span><span class="sxs-lookup"><span data-stu-id="a34ca-117">In the navigation list, click **Resource groups**.</span></span>

   ![Ressourcengruppen](../media-draft/4-resource-groups.png)

1. <span data-ttu-id="a34ca-119">Klicken Sie auf die Ressourcengruppe mit dem Namen **FirstUpConsultantsRG1-_XXXXXXX_**.</span><span class="sxs-lookup"><span data-stu-id="a34ca-119">Click the resource group named **FirstUpConsultantsRG1-_XXXXXXX_**.</span></span>

1. <span data-ttu-id="a34ca-120">Klicken Sie auf **Zugriffssteuerung (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="a34ca-120">Click **Access control (IAM)**.</span></span>

   <span data-ttu-id="a34ca-121">Auf dem Blatt „Zugriffssteuerung (IAM)“ wird angezeigt, wer Zugriff auf diese Ressourcengruppe hat.</span><span class="sxs-lookup"><span data-stu-id="a34ca-121">On the Access control (IAM) blade, you can see who has access to this resource group.</span></span> <span data-ttu-id="a34ca-122">Beachten Sie, dass einige Rollen auf **Diese Ressource** begrenzt sind, während andere von einem übergeordneten Bereich **geerbt** werden.</span><span class="sxs-lookup"><span data-stu-id="a34ca-122">Notice that some roles are scoped to **This resource** while others are **(Inherited)** from a parent scope.</span></span>

   ![Zugriffssteuerung (IAM) für Ressourcengruppe](../media-draft/4-resource-group-access-control.png)

## <a name="list-roles"></a><span data-ttu-id="a34ca-124">Auflisten der Rollen</span><span class="sxs-lookup"><span data-stu-id="a34ca-124">List roles</span></span>

<span data-ttu-id="a34ca-125">Wie Sie in der vorherigen Einheit gelernt haben, ist eine Rolle eine Sammlung von Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="a34ca-125">As you learned in the previous unit, a role is a collection of permissions.</span></span> <span data-ttu-id="a34ca-126">Azure verfügt über mehr als 70 integrierte Rollen, die Sie in Ihren Rollenzuweisungen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="a34ca-126">Azure has over 70 built-in roles that you can use in your role assignments.</span></span> <span data-ttu-id="a34ca-127">Führen Sie die folgenden Schritte aus, um die Rollen aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="a34ca-127">Follow these steps to list the roles.</span></span>

- <span data-ttu-id="a34ca-128">Klicken Sie oben auf dem Blatt „Zugriffssteuerung (IAM)“ auf **Rollen**, um eine Liste aller integrierten und benutzerdefinierten Rollen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="a34ca-128">At the top of the Access control (IAM) blade, click **Roles** to see a list of all the built-in and custom roles.</span></span>

   ![Rollenoption](../media-draft/4-roles-option.png)

   <span data-ttu-id="a34ca-130">Sie können die Anzahl von Benutzern und Gruppen anzeigen, die jeder Rolle zugewiesen sind.</span><span class="sxs-lookup"><span data-stu-id="a34ca-130">You can see the number of users and groups that are assigned to each role.</span></span>

   ![Rollenliste](../media-draft/4-roles-list.png)

## <a name="summary"></a><span data-ttu-id="a34ca-132">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="a34ca-132">Summary</span></span>

<span data-ttu-id="a34ca-133">In dieser Einheit haben Sie gelernt, wie Sie die Rollenzuweisungen im Azure-Portal für sich selbst auflisten.</span><span class="sxs-lookup"><span data-stu-id="a34ca-133">In this unit, you learned how to list the role assignments for yourself in the Azure portal.</span></span> <span data-ttu-id="a34ca-134">Außerdem haben Sie gelernt, wie die Rollenzuweisungen in verschiedenen Bereichen aufgelistet werden.</span><span class="sxs-lookup"><span data-stu-id="a34ca-134">You also learned how to list the role assignments at different scopes.</span></span> <span data-ttu-id="a34ca-135">In der nächsten Einheit lernen Sie, wie Sie einem Benutzer über die rollenbasierte Zugriffssteuerung Zugriff gewähren.</span><span class="sxs-lookup"><span data-stu-id="a34ca-135">In the next unit, you take the next step and use RBAC to grant access to a user.</span></span>
