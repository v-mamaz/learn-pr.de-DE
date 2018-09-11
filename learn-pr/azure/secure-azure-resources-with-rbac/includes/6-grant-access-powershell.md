<span data-ttu-id="222ec-101">Sie verwenden immer das Blatt **Zugriffssteuerung (IAM)** im Azure-Portal. Das Vorgehen funktioniert einwandfrei, Sie erhalten jedoch täglich mehrere Berechtigungsanforderungen.</span><span class="sxs-lookup"><span data-stu-id="222ec-101">Using the **Access control (IAM)** blade in the Azure portal has been working fine, but you are getting several permission requests each day.</span></span> <span data-ttu-id="222ec-102">Damit Sie Verwaltungsaufgaben zeitnah bearbeiten können, möchten Sie einige Schritte mit PowerShell automatisieren.</span><span class="sxs-lookup"><span data-stu-id="222ec-102">To keep up with the access management tasks, you decide to use PowerShell to help automate some of the steps.</span></span>

## <a name="open-cloud-shell-powershell"></a><span data-ttu-id="222ec-103">Öffnen von Cloud Shell PowerShell</span><span class="sxs-lookup"><span data-stu-id="222ec-103">Open Cloud Shell PowerShell</span></span>

1. <span data-ttu-id="222ec-104">Stellen Sie sicher, dass Sie immer noch als **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com** im Azure-Portal angemeldet sind.</span><span class="sxs-lookup"><span data-stu-id="222ec-104">Make sure you are still signed in to the Azure portal as **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com**.</span></span> <span data-ttu-id="222ec-105">Den Benutzernamen und das Kennwort finden Sie oben im Fenster auf der Registerkarte **Ressourcen**.</span><span class="sxs-lookup"><span data-stu-id="222ec-105">You can find the username and password on the **Resources** tab at the top of this window.</span></span>

1. <span data-ttu-id="222ec-106">Klicken Sie oben im Portal auf **Cloud Shell**, um den Bereich „Cloud Shell“ zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="222ec-106">At the top of the portal, click **Cloud Shell** to open the Cloud Shell pane.</span></span>

    ![Schaltfläche „Cloud Shell“](../media-draft/6-cloud-shell-button.png)

1. <span data-ttu-id="222ec-108">Stellen Sie oben links im Cloud Shell-Bereich sicher, dass **PowerShell** festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="222ec-108">In the upper left of the Cloud Shell pane, make sure it is set to **PowerShell**.</span></span> <span data-ttu-id="222ec-109">Wenn **Bash** festgelegt ist, ändern Sie die Einstellung zu **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="222ec-109">If it is set to **Bash**, change it to **PowerShell**.</span></span>

    <span data-ttu-id="222ec-110">Das Laden kann einige Minuten in Anspruch nehmen.</span><span class="sxs-lookup"><span data-stu-id="222ec-110">It might take a few moments to load.</span></span> <span data-ttu-id="222ec-111">Die anschließende Ausgabe sieht etwa so aus:</span><span class="sxs-lookup"><span data-stu-id="222ec-111">When finished, it will look similar to the following:</span></span>

    ![Cloud Shell PowerShell](../media-draft/6-cloud-shell-powershell.png)

## <a name="grant-access"></a><span data-ttu-id="222ec-113">Gewähren von Zugriff</span><span class="sxs-lookup"><span data-stu-id="222ec-113">Grant access</span></span>

<span data-ttu-id="222ec-114">Wenn Sie einem Benutzer mit Azure PowerShell Zugriff gewähren möchten, verwenden Sie den Befehl [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment).</span><span class="sxs-lookup"><span data-stu-id="222ec-114">To grant access to a user using Azure PowerShell, you use the [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) command.</span></span> <span data-ttu-id="222ec-115">Sie müssen den Sicherheitsprinzipal, die Rollendefinition und den Bereich angeben.</span><span class="sxs-lookup"><span data-stu-id="222ec-115">You must specify the security principal, role definition, and scope.</span></span>

<span data-ttu-id="222ec-116">Führen Sie diese Schritte aus, um dem Benutzer **LabUser-_XXXXXXX_** die Rolle „Mitwirkender für virtuelle Computer“ im Ressourcengruppenbereich zuzuweisen.</span><span class="sxs-lookup"><span data-stu-id="222ec-116">Follow these steps to assign the Virtual Machine Contributor role to the **LabUser-_XXXXXXX_** user at the resource group scope.</span></span>

1. <span data-ttu-id="222ec-117">Kopieren Sie oben im Fenster auf der Registerkarte **Ressourcen** den Befehl **Grant access PowerShell** (Zugriff erteilen PowerShell).</span><span class="sxs-lookup"><span data-stu-id="222ec-117">On the **Resources** tab at the top of this window, copy the **Grant access PowerShell** command.</span></span>

1. <span data-ttu-id="222ec-118">Fügen Sie den Befehl in den PowerShell-Bereich ein, und drücken Sie die EINGABETASTE, um ihn auszuführen.</span><span class="sxs-lookup"><span data-stu-id="222ec-118">Paste the command into the PowerShell pane and press the Enter key to run it.</span></span> <span data-ttu-id="222ec-119">Nachfolgend sehen Sie einen Beispielbefehl und dessen Ausgabe:</span><span class="sxs-lookup"><span data-stu-id="222ec-119">The following shows an example command and the output:</span></span>

    ```Example
    PS Azure:\> New-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -RoleDefinitionName "Virtual Machine Contributor" `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"

    RoleAssignmentId   : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX/providers/Microsoft.Authorization/roleAssignments/33333333-3333-3333-3333-333333333333
    Scope              : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX
    DisplayName        : LabUser-XXXXXXX
    SignInName         : LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com
    RoleDefinitionName : Virtual Machine Contributor
    RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
    ObjectId           : 11111111-1111-1111-1111-111111111111
    ObjectType         : User
    CanDelegate        : False
    ```

    <span data-ttu-id="222ec-120">Die Ausgabe zeigt, dass die Rolle „Mitwirkender für virtuelle Computer“ dem Benutzer „LabUser-_XXXXXXX_“ im Bereich „FirstUpConsultantsRG1-_XXXXXXX_“ zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="222ec-120">The output shows that the Virtual Machine Contributor role has been assigned to LabUser-_XXXXXXX_ at the FirstUpConsultantsRG1-_XXXXXXX_ scope.</span></span>

## <a name="list-access"></a><span data-ttu-id="222ec-121">Auflisten des Zugriffs</span><span class="sxs-lookup"><span data-stu-id="222ec-121">List access</span></span>

<span data-ttu-id="222ec-122">Wenn Sie den Zugriff für die Ressourcengruppe überprüfen möchten, listen Sie mit dem Befehl [Get-AzureRmRoleAssignment](/powershell/module/azurerm.resources/get-azurermroleassignment) die Rollenzuweisungen auf.</span><span class="sxs-lookup"><span data-stu-id="222ec-122">To verify the access for the resource group, you use the [Get-AzureRmRoleAssignment](/powershell/module/azurerm.resources/get-azurermroleassignment) command to list the role assignments.</span></span>

<span data-ttu-id="222ec-123">Führen Sie diese Schritte aus, um alle Rollenzuweisungen für den Benutzer **LabUser-XXXXXXX** im Ressourcengruppenbereich aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="222ec-123">Follow these steps to list all the role assignments for the **LabUser-XXXXXXX** user at the resource group scope.</span></span>

1. <span data-ttu-id="222ec-124">Kopieren Sie oben im Fenster auf der Registerkarte **Ressourcen** den Befehl **List access PowerShell** (Zugriff auflisten PowerShell).</span><span class="sxs-lookup"><span data-stu-id="222ec-124">On the **Resources** tab at the top of this window, copy the **List access PowerShell** command.</span></span>

1. <span data-ttu-id="222ec-125">Fügen Sie den Befehl in den PowerShell-Bereich ein, und drücken Sie die EINGABETASTE, um ihn auszuführen.</span><span class="sxs-lookup"><span data-stu-id="222ec-125">Paste the command into the PowerShell pane and press the Enter key to run it.</span></span> <span data-ttu-id="222ec-126">Nachfolgend sehen Sie einen Beispielbefehl und dessen Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="222ec-126">The following shows an example command and the output.</span></span>

    ```Example
    PS Azure:\> Get-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"

    RoleAssignmentId   : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX/providers/Microsoft.Authorization/roleAssignments/33333333-3333-3333-3333-333333333333
    Scope              : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX
    DisplayName        : LabUser-XXXXXXX
    SignInName         : LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com 
    RoleDefinitionName : Virtual Machine Contributor
    RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
    ObjectId           : 11111111-1111-1111-1111-111111111111
    ObjectType         : User
    CanDelegate        : False
    ```

    <span data-ttu-id="222ec-127">Die Ausgabe zeigt, dass die Rolle „Mitwirkender für virtuelle Computer“ dem Benutzer „LabUser-_XXXXXXX_“ im Bereich „FirstUpConsultantsRG1-_XXXXXXX_“ zugewiesen wurde.</span><span class="sxs-lookup"><span data-stu-id="222ec-127">The output shows that the Virtual Machine Contributor role has been assigned to LabUser-_XXXXXXX_ at the FirstUpConsultantsRG1-_XXXXXXX_ scope.</span></span>

    <span data-ttu-id="222ec-128">Wenn Sie das Blatt **Zugriffssteuerung (IAM)** für die Ressourcengruppe im Azure-Portal aktualisieren, sieht die Rollenzuweisung wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="222ec-128">If you refresh the **Access control (IAM)** blade for the resource group in the Azure portal, this is how the role assignment looks:</span></span>

    ![Rollenzuweisungen für einen Benutzer im Ressourcengruppenbereich](../media-draft/6-cloud-shell-access-control.png)

## <a name="remove-access"></a><span data-ttu-id="222ec-130">Entfernen des Zugriffs</span><span class="sxs-lookup"><span data-stu-id="222ec-130">Remove access</span></span>

<span data-ttu-id="222ec-131">Verwenden Sie zum Entfernen des Zugriffs für Benutzer, Gruppen und Anwendungen den Befehl [Remove-AzureRmRoleAssignment](/powershell/module/azurerm.resources/remove-azurermroleassignment), um eine Rollenzuweisung zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="222ec-131">To remove access for users, groups, and applications, you use [Remove-AzureRmRoleAssignment](/powershell/module/azurerm.resources/remove-azurermroleassignment) to remove a role assignment.</span></span>

<span data-ttu-id="222ec-132">Führen Sie diese Schritte aus, um dem Benutzer **LabUser-_XXXXXXX_** die Rollenzuweisung „Mitwirkender für virtuelle Computer“ im Ressourcengruppenbereich zu entziehen.</span><span class="sxs-lookup"><span data-stu-id="222ec-132">Follow these steps to remove the Virtual Machine Contributor role assignment for the **LabUser-_XXXXXX_** user at the resource group scope.</span></span>

1. <span data-ttu-id="222ec-133">Kopieren Sie oben im Fenster auf der Registerkarte **Ressourcen** den Befehl **Remove access PowerShell** (Zugriff entfernen PowerShell).</span><span class="sxs-lookup"><span data-stu-id="222ec-133">On the **Resources** tab at the top of this window, copy the **Remove access PowerShell** command.</span></span>

1. <span data-ttu-id="222ec-134">Fügen Sie den Befehl in den PowerShell-Bereich ein, und drücken Sie die EINGABETASTE, um ihn auszuführen.</span><span class="sxs-lookup"><span data-stu-id="222ec-134">Paste the command into the PowerShell pane and press the Enter key to run it.</span></span> <span data-ttu-id="222ec-135">Nachfolgend ist ein Beispielbefehl dargestellt.</span><span class="sxs-lookup"><span data-stu-id="222ec-135">The following shows an example command.</span></span>

    ```Example
    PS Azure:\> Remove-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -RoleDefinitionName "Virtual Machine Contributor" `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"
    ```

1. <span data-ttu-id="222ec-136">Klicken Sie im PowerShell-Bereich auf die Schließen-Schaltfläche (**X**), um den Bereich zu schließen.</span><span class="sxs-lookup"><span data-stu-id="222ec-136">In the PowerShell pane, click the close (**X**) button to close the pane.</span></span>

    ![Cloud Shell – Schaltfläche „Schließen“](../media-draft/6-cloud-shell-close.png)


## <a name="summary"></a><span data-ttu-id="222ec-138">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="222ec-138">Summary</span></span>

<span data-ttu-id="222ec-139">In dieser Einheit haben Sie gelernt, wie Sie einem Benutzer mit Azure PowerShell Zugriff erteilen, damit dieser virtuelle Computer in einer Ressourcengruppe erstellen und verwalten kann.</span><span class="sxs-lookup"><span data-stu-id="222ec-139">In this unit, you learned how to grant a user access to create and manage virtual machines in a resource group using Azure PowerShell.</span></span> <span data-ttu-id="222ec-140">In der nächsten Einheit erfahren Sie, wie Sie RBAC-Änderungen im Zeitverlauf anzeigen.</span><span class="sxs-lookup"><span data-stu-id="222ec-140">In the next unit, you learn how to view the RBAC changes over time.</span></span>
