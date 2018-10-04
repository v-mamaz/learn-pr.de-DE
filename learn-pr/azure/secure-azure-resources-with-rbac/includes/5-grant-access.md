<span data-ttu-id="de87a-101">Ein Kollege bei First Up Consultants mit dem Namen Alain muss für ein Projekt, an dem er aktuell arbeitet, virtuelle Computer erstellen und verwalten können.</span><span class="sxs-lookup"><span data-stu-id="de87a-101">A co-worker named Alain at First Up Consultants needs the ability to create and manage virtual machines for a project he is working on.</span></span> <span data-ttu-id="de87a-102">Ihr Manager hat Sie darum gebeten, diese Anforderung zu bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="de87a-102">Your manager has asked that you handle this request.</span></span> <span data-ttu-id="de87a-103">Unter Verwendung der Best Practices zur Gewährung minimaler Berechtigungen für Benutzer, damit diese ihren Auftrag durchführen können, entscheiden Sie sich dazu, Alain die Rolle „Mitwirkender für virtuelle Computer“ für eine Ressourcengruppe zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="de87a-103">Using the best practice to grant users the least privileges to get their work done, you decide to assign Alain the Virtual Machine Contributor role for a resource group.</span></span>

## <a name="grant-access"></a><span data-ttu-id="de87a-104">Gewähren von Zugriff</span><span class="sxs-lookup"><span data-stu-id="de87a-104">Grant access</span></span>

<span data-ttu-id="de87a-105">Führen Sie diese Schritte aus, um einem Benutzer im Bereich der Ressourcengruppen die Rolle „Mitwirkender für virtuelle Computer“ zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="de87a-105">Follow these steps to assign the Virtual Machine Contributor role to a user at the resource group scope.</span></span>

1. <span data-ttu-id="de87a-106">Klicken Sie in der Navigationsliste auf **Ressourcengruppen**.</span><span class="sxs-lookup"><span data-stu-id="de87a-106">In the navigation list, click **Resource groups**.</span></span>

1. <span data-ttu-id="de87a-107">Suchen Sie die Ressourcengruppe **FirstUpConsultantsRG1-_XXXXXXX_**, und klicken Sie darauf.</span><span class="sxs-lookup"><span data-stu-id="de87a-107">Find and click the **FirstUpConsultantsRG1-_XXXXXXX_** resource group.</span></span>

1. <span data-ttu-id="de87a-108">Klicken Sie auf **Zugriffssteuerung (IAM)**, um die aktuelle Liste der Rollenzuweisungen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="de87a-108">Click **Access control (IAM)** to see the current list of role assignments.</span></span>

   ![Zugriffssteuerung: Rollenzuweisung für die Ressourcengruppe](../media/5-resource-group-role-assignment.png)

1. <span data-ttu-id="de87a-110">Klicken Sie im oberen Bereich auf **Hinzufügen**, um den Bereich **Berechtigungen hinzufügen** zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="de87a-110">At the top, click **Add** to open the **Add permissions** pane.</span></span>

   ![Bereich „Berechtigungen hinzufügen“](../media/5-add-permissions.png)

1. <span data-ttu-id="de87a-112">Wählen Sie in der Dropdownliste **Rolle** die Rolle **Mitwirkender für virtuelle Computer** aus.</span><span class="sxs-lookup"><span data-stu-id="de87a-112">In the **Role** drop-down list, select **Virtual Machine Contributor**.</span></span>

1. <span data-ttu-id="de87a-113">Wählen Sie aus der Liste **Auswählen** den Benutzer **LabUser-_XXXXXXX_** aus.</span><span class="sxs-lookup"><span data-stu-id="de87a-113">In the **Select** list, select **LabUser-_XXXXXXX_**.</span></span>

    <span data-ttu-id="de87a-114">Der Benutzername befindet sich auf der Registerkarte **Ressourcen** neben den Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="de87a-114">You can find the username on the **Resources** tab next to the instructions.</span></span>

   ![Bereich „Berechtigungen hinzufügen“ abgeschlossen](../media/5-add-permissions-save.png)

1. <span data-ttu-id="de87a-116">Klicken Sie auf **Speichern**, um die Rollenzuweisung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="de87a-116">Click **Save** to create the role assignment.</span></span>

   <span data-ttu-id="de87a-117">Nach einigen Augenblicken wird der Benutzer **LabUser-_XXXXXXX_** der Rolle „Mitwirkender für virtuelle Computer“ im Bereich **FirstUpConsultantsRG1-_XXXXXXX_** der Ressourcengruppen zugewiesen.</span><span class="sxs-lookup"><span data-stu-id="de87a-117">After a few moments, the **LabUser-_XXXXXXX_** user is assigned the Virtual Machine Contributor role at the **FirstUpConsultantsRG1-_XXXXXXX_** resource group scope.</span></span> <span data-ttu-id="de87a-118">Der Benutzer kann nun nur in dieser Ressourcengruppe virtuelle Computer erstellen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="de87a-118">The user can now create and manage virtual machines just within this resource group.</span></span>

   ![Zuweisung der Rolle „Mitwirkender für virtuelle Computer“](../media/5-vm-contributor-assignment.png)

## <a name="remove-access"></a><span data-ttu-id="de87a-120">Entfernen des Zugriffs</span><span class="sxs-lookup"><span data-stu-id="de87a-120">Remove access</span></span>

<span data-ttu-id="de87a-121">In RBAC entfernen Sie eine Rollenzuweisung, um den Zugriff zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="de87a-121">In RBAC, to remove access, you remove a role assignment.</span></span>

1. <span data-ttu-id="de87a-122">Wählen Sie in der Liste der Rollenzuweisungen den Benutzer **LabUser-_XXXXXXX_** mit der Rolle „Mitwirkender für virtuelle Computer“ aus.</span><span class="sxs-lookup"><span data-stu-id="de87a-122">In the list of role assignments, select the **LabUser-_XXXXXXX_** user with the Virtual Machine Contributor role.</span></span>

1. <span data-ttu-id="de87a-123">Klicken Sie auf **Entfernen**.</span><span class="sxs-lookup"><span data-stu-id="de87a-123">Click **Remove**.</span></span>

   ![Nachricht zum Entfernen der Rollenzuweisung](../media/5-remove-role-assignment.png)

1. <span data-ttu-id="de87a-125">Klicken Sie in der Nachricht zum **Entfernen von Rollenzuweisungen** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="de87a-125">In the **Remove role assignments** message that appears, click **Yes**.</span></span>

<span data-ttu-id="de87a-126">In dieser Einheit haben Sie gelernt, wie Sie einem Benutzer über das Azure-Portal Zugriff gewähren, damit dieser virtuelle Computer in einer Ressourcengruppe erstellen und verwalten kann.</span><span class="sxs-lookup"><span data-stu-id="de87a-126">In this unit, you learned how to grant a user access to create and manage virtual machines in a resource group using the Azure portal.</span></span>