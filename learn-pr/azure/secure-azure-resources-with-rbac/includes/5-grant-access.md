<span data-ttu-id="f2bb7-101">Ein Kollege bei First Up Consultants mit dem Namen Alain muss für ein Projekt, an dem er aktuell arbeitet, virtuelle Computer erstellen und verwalten können.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-101">A co-worker named Alain at First Up Consultants needs the ability to create and manage virtual machines for a project he is working on.</span></span> <span data-ttu-id="f2bb7-102">Ihr Manager hat Sie darum gebeten, diese Anforderung zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-102">Your manager has asked that you handle this request.</span></span> <span data-ttu-id="f2bb7-103">Unter Verwendung der Best Practices zur Gewährung minimaler Berechtigungen für Benutzer, damit diese ihren Auftrag durchführen können, entscheiden Sie, eine neue Ressourcengruppe zu erstellen und Alain die Rolle „Mitwirkender für virtuelle Computer“ zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-103">Using the best practice to grant users the least privileges to get their work done, you decide to create a new resource group and assign Alain the Virtual Machine Contributor role.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="f2bb7-104">Anmelden auf dem Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="f2bb7-104">Sign in to the Azure portal</span></span>

- <span data-ttu-id="f2bb7-105">Stellen Sie sicher, dass Sie immer noch als **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com** im Azure-Portal angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-105">Make sure you are still signed in to the Azure portal as **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com**.</span></span> <span data-ttu-id="f2bb7-106">Den Benutzernamen und das Kennwort finden Sie oben im Fenster auf der Registerkarte **Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-106">You can find the username and password on the **Resources** tab at the top of this window.</span></span>

## <a name="grant-access"></a><span data-ttu-id="f2bb7-107">Gewähren von Zugriff</span><span class="sxs-lookup"><span data-stu-id="f2bb7-107">Grant access</span></span>

<span data-ttu-id="f2bb7-108">Führen Sie diese Schritte aus, um einem Benutzer im Bereich der Ressourcengruppen die Rolle „Mitwirkender für virtuelle Computer“ zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-108">Follow these steps to assign the Virtual Machine Contributor role to a user at the resource group scope.</span></span>

1. <span data-ttu-id="f2bb7-109">Klicken Sie in der Navigationsliste auf **Ressourcengruppen**.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-109">In the navigation list, click **Resource groups**.</span></span>

1. <span data-ttu-id="f2bb7-110">Suchen Sie die Ressourcengruppe **FirstUpConsultantsRG1-_XXXXXXX_**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-110">Find and click the **FirstUpConsultantsRG1-_XXXXXXX_** resource group.</span></span>

   ![Ressourcengruppenliste](../media-draft/5-resource-groups.png)

1. <span data-ttu-id="f2bb7-112">Klicken Sie auf **Zugriffssteuerung (IAM)**, um die aktuelle Liste der Rollenzuweisungen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-112">Click **Access control (IAM)** to see the current list of role assignments.</span></span>

   ![Blatt „Zugriffssteuerung (IAM)“ für Ressourcengruppe](../media-draft/5-resource-group-access-control.png)

1. <span data-ttu-id="f2bb7-114">Klicken Sie im oberen Bereich auf **Hinzufügen**, um den Bereich **Berechtigungen hinzufügen** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-114">At the top, click **Add** to open the **Add permissions** pane.</span></span>

   ![Bereich „Berechtigungen hinzufügen“](../media-draft/5-add-permissions.png)

1. <span data-ttu-id="f2bb7-116">Wählen Sie in der Dropdownliste **Rolle** die Rolle **Mitwirkender für virtuelle Computer** aus.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-116">In the **Role** drop-down list, select **Virtual Machine Contributor**.</span></span>

1. <span data-ttu-id="f2bb7-117">Wählen Sie in der Liste **Auswählen** den Benutzer **LabUser-_XXXXXXX_** aus.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-117">In the **Select** list, select **LabUser-_XXXXXXX_**.</span></span>

   ![Bereich „Berechtigungen hinzufügen“ abgeschlossen](../media-draft/5-add-permissions-save.png)

1. <span data-ttu-id="f2bb7-119">Klicken Sie auf **Speichern**, um die Rollenzuweisung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-119">Click **Save** to create the role assignment.</span></span>

   <span data-ttu-id="f2bb7-120">Nach einigen Augenblicken wird der Benutzer **LabUser-_XXXXXXX_** der Rolle „Mitwirkender für virtuelle Computer“ im Bereich **FirstUpConsultantsRG1-_XXXXXXX_** der Ressourcengruppen zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-120">After a few moments, the **LabUser-_XXXXXXX_** user is assigned the Virtual Machine Contributor role at the **FirstUpConsultantsRG1-_XXXXXXX_** resource group scope.</span></span> <span data-ttu-id="f2bb7-121">Der Benutzer kann nun nur in dieser Ressourcengruppe virtuelle Computer erstellen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-121">The user can now create and manage virtual machines just within this resource group.</span></span>

   ![Zuweisung der Rolle „Mitwirkender für virtuelle Computer“](../media-draft/5-vm-contributor-assignment.png)

## <a name="remove-access"></a><span data-ttu-id="f2bb7-123">Entfernen des Zugriffs</span><span class="sxs-lookup"><span data-stu-id="f2bb7-123">Remove access</span></span>

<span data-ttu-id="f2bb7-124">In RBAC entfernen Sie eine Rollenzuweisung, um den Zugriff zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-124">In RBAC, to remove access, you remove a role assignment.</span></span>

1. <span data-ttu-id="f2bb7-125">Wählen Sie in der Liste der Rollenzuweisungen den Benutzer **LabUser-_XXXXXXX_** mit der Rolle „Mitwirkender für virtuelle Computer“ aus.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-125">In the list of role assignments, select the **LabUser-_XXXXXXX_** user with the Virtual Machine Contributor role.</span></span>

1. <span data-ttu-id="f2bb7-126">Klicken Sie auf **Entfernen**.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-126">Click **Remove**.</span></span>

   ![Nachricht zum Entfernen der Rollenzuweisung](../media-draft/5-remove-role-assignment.png)

1. <span data-ttu-id="f2bb7-128">Klicken Sie in der Nachricht zum **Entfernen von Rollenzuweisungen** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-128">In the **Remove role assignments** message that appears, click **Yes**.</span></span>

## <a name="summary"></a><span data-ttu-id="f2bb7-129">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="f2bb7-129">Summary</span></span>

<span data-ttu-id="f2bb7-130">In dieser Einheit haben Sie gelernt, wie Sie einem Benutzer über das Azure-Portal Zugriff gewähren, damit dieser virtuelle Computer in einer Ressourcengruppe erstellen und verwalten kann.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-130">In this unit, you learned how to grant a user access to create and manage virtual machines in a resource group using the Azure portal.</span></span> <span data-ttu-id="f2bb7-131">In der nächsten Einheit erfahren Sie, wie Sie mithilfe von PowerShell Zugriff gewähren können.</span><span class="sxs-lookup"><span data-stu-id="f2bb7-131">In the next unit, you look at how to grant access using PowerShell.</span></span>
