> [!NOTE]
> <span data-ttu-id="95d85-101">Nachdem das Lab gestartet wurde, finden Sie auf der Registerkarte **Ressourcen** neben den Anweisungen die erforderlichen Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="95d85-101">After launching the lab, the username and password you need is located on the **Resources** tab next to the instructions.</span></span>

<span data-ttu-id="95d85-102">Bei First Up Consultants wurde Ihnen Zugriff auf eine Ressourcengruppe für das Marketingteam gewährt.</span><span class="sxs-lookup"><span data-stu-id="95d85-102">At First Up Consultants, you've been granted access to a resource group for the marketing team.</span></span> <span data-ttu-id="95d85-103">Sie möchten sich mit dem Azure-Portal vertraut machen und sehen, welche Rollen derzeit zugewiesen sind.</span><span class="sxs-lookup"><span data-stu-id="95d85-103">You want to familiarize yourself with the Azure portal and see what roles are currently assigned.</span></span>

## <a name="list-role-assignments-for-yourself"></a><span data-ttu-id="95d85-104">Liste von Rollenzuweisungen für Sie selbst</span><span class="sxs-lookup"><span data-stu-id="95d85-104">List role assignments for yourself</span></span>

<span data-ttu-id="95d85-105">Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen Ihnen zurzeit zugewiesen sind.</span><span class="sxs-lookup"><span data-stu-id="95d85-105">Follow these steps to see what roles are currently assigned to you.</span></span>

1. <span data-ttu-id="95d85-106">Klicken Sie in der oberen rechten Ecke des Azure-Portals auf Ihren Benutzernamen, um das Menü zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="95d85-106">In the upper-right corner of the Azure portal, click your user name to open the menu.</span></span>

    ![Menü „Meine Berechtigungen“](../media/4-my-permissions-menu.png)

1. <span data-ttu-id="95d85-108">Klicken Sie auf **Meine Berechtigungen**, um den Bereich „Meine Berechtigungen“ zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="95d85-108">Click **My permissions** to open the My permissions pane.</span></span>

    ![Bereich „Meine Berechtigungen“](../media/4-my-permissions-pane.png)

    <span data-ttu-id="95d85-110">Im Bereich „Meine Berechtigungen“ wird eine Liste der Ihnen zugewiesenen Rollen und deren Bereich angezeigt.</span><span class="sxs-lookup"><span data-stu-id="95d85-110">On the My permissions pane, you can see a list of the roles that you have been assigned and the scope.</span></span> <span data-ttu-id="95d85-111">Ihre Liste wird anders aussehen.</span><span class="sxs-lookup"><span data-stu-id="95d85-111">Your list will look different.</span></span>

## <a name="list-role-assignments-for-a-resource-group"></a><span data-ttu-id="95d85-112">Auflisten von Rollenzuweisungen für eine Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="95d85-112">List role assignments for a resource group</span></span>

<span data-ttu-id="95d85-113">Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen im Bereich der Ressourcengruppen zugewiesen wurden.</span><span class="sxs-lookup"><span data-stu-id="95d85-113">Follow these steps to see what roles are assigned at the resource group scope.</span></span>

1. <span data-ttu-id="95d85-114">Klicken Sie in der Navigationsliste auf **Ressourcengruppen**.</span><span class="sxs-lookup"><span data-stu-id="95d85-114">In the navigation list, click **Resource groups**.</span></span>

   ![Ressourcengruppen](../media/4-resource-groups.png)

1. <span data-ttu-id="95d85-116">Suchen Sie die Ressourcengruppe mit dem Namen **FirstUpConsultantsRG1-_XXXXXXX_**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="95d85-116">Find and click the resource group named **FirstUpConsultantsRG1-_XXXXXXX_**.</span></span>

1. <span data-ttu-id="95d85-117">Klicken Sie auf **Zugriffssteuerung (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="95d85-117">Click **Access control (IAM)**.</span></span>

   ![Zugriffssteuerung für die Ressourcengruppe](../media/4-resource-group-access-control.png)

    <span data-ttu-id="95d85-119">Ihnen wird angezeigt, wer über Zugriff auf diese Ressourcengruppe verfügt.</span><span class="sxs-lookup"><span data-stu-id="95d85-119">You can see who has access to this resource group.</span></span> <span data-ttu-id="95d85-120">Beachten Sie, dass einige Rollen auf **diese Ressource** begrenzt sind, während andere von einem übergeordneten Bereich **geerbt** werden.</span><span class="sxs-lookup"><span data-stu-id="95d85-120">Notice that some roles are scoped to **This resource** while others are **(Inherited)** from a parent scope.</span></span>

   ![Zugriffssteuerung: Rollenzuweisung für die Ressourcengruppe](../media/4-resource-group-role-assignment.png)

## <a name="list-roles"></a><span data-ttu-id="95d85-122">Auflisten der Rollen</span><span class="sxs-lookup"><span data-stu-id="95d85-122">List roles</span></span>

<span data-ttu-id="95d85-123">Wie Sie in der vorherigen Einheit gelernt haben, ist eine Rolle eine Sammlung von Berechtigungen.</span><span class="sxs-lookup"><span data-stu-id="95d85-123">As you learned in the previous unit, a role is a collection of permissions.</span></span> <span data-ttu-id="95d85-124">Azure verfügt über mehr als 70 integrierte Rollen, die Sie in Ihren Rollenzuweisungen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="95d85-124">Azure has over 70 built-in roles that you can use in your role assignments.</span></span> <span data-ttu-id="95d85-125">Führen Sie diesen Schritt aus, um die Rollen aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="95d85-125">Follow this step to list the roles.</span></span>

- <span data-ttu-id="95d85-126">Klicken Sie am oberen Rand des Bereichs auf **Rollen**, um eine Liste aller integrierten und benutzerdefinierten Rollen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="95d85-126">At the top of the pane, click **Roles** to see a list of all the built-in and custom roles.</span></span>

   <span data-ttu-id="95d85-127">Sie können die Anzahl von Benutzern und Gruppen anzeigen, die jeder Rolle zugewiesen sind.</span><span class="sxs-lookup"><span data-stu-id="95d85-127">You can see the number of users and groups that are assigned to each role.</span></span>

   ![Rollenliste](../media/4-roles-list.png)

<span data-ttu-id="95d85-129">In dieser Einheit haben Sie gelernt, wie Sie die Rollenzuweisungen im Azure-Portal für sich selbst auflisten.</span><span class="sxs-lookup"><span data-stu-id="95d85-129">In this unit, you learned how to list the role assignments for yourself in the Azure portal.</span></span> <span data-ttu-id="95d85-130">Außerdem haben Sie gelernt, wie Sie die Rollenzuweisungen für eine Ressourcengruppe auflisten.</span><span class="sxs-lookup"><span data-stu-id="95d85-130">You also learned how to list the role assignments for a resource group.</span></span>