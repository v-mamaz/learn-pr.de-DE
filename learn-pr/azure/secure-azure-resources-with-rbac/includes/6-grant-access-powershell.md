Sie verwenden immer das Blatt **Zugriffssteuerung (IAM)** im Azure-Portal. Das Vorgehen funktioniert einwandfrei, Sie erhalten jedoch täglich mehrere Berechtigungsanforderungen. Damit Sie Verwaltungsaufgaben zeitnah bearbeiten können, möchten Sie einige Schritte mit PowerShell automatisieren.

## <a name="open-cloud-shell-powershell"></a>Öffnen von Cloud Shell PowerShell

1. Stellen Sie sicher, dass Sie immer noch als **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com** im Azure-Portal angemeldet sind. Den Benutzernamen und das Kennwort finden Sie oben im Fenster auf der Registerkarte **Ressourcen**.

1. Klicken Sie oben im Portal auf **Cloud Shell**, um den Bereich „Cloud Shell“ zu öffnen.

    ![Schaltfläche „Cloud Shell“](../media-draft/6-cloud-shell-button.png)

1. Stellen Sie oben links im Cloud Shell-Bereich sicher, dass **PowerShell** festgelegt ist. Wenn **Bash** festgelegt ist, ändern Sie die Einstellung zu **PowerShell**.

    Das Laden kann einige Minuten in Anspruch nehmen. Die anschließende Ausgabe sieht etwa so aus:

    ![Cloud Shell PowerShell](../media-draft/6-cloud-shell-powershell.png)

## <a name="grant-access"></a>Gewähren von Zugriff

Wenn Sie einem Benutzer mit Azure PowerShell Zugriff gewähren möchten, verwenden Sie den Befehl [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment). Sie müssen den Sicherheitsprinzipal, die Rollendefinition und den Bereich angeben.

Führen Sie diese Schritte aus, um dem Benutzer **LabUser-_XXXXXXX_** die Rolle „Mitwirkender für virtuelle Computer“ im Ressourcengruppenbereich zuzuweisen.

1. Kopieren Sie oben im Fenster auf der Registerkarte **Ressourcen** den Befehl **Grant access PowerShell** (Zugriff erteilen PowerShell).

1. Fügen Sie den Befehl in den PowerShell-Bereich ein, und drücken Sie die EINGABETASTE, um ihn auszuführen. Nachfolgend sehen Sie einen Beispielbefehl und dessen Ausgabe:

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

    Die Ausgabe zeigt, dass die Rolle „Mitwirkender für virtuelle Computer“ dem Benutzer „LabUser-_XXXXXXX_“ im Bereich „FirstUpConsultantsRG1-_XXXXXXX_“ zugewiesen wurde.

## <a name="list-access"></a>Auflisten des Zugriffs

Wenn Sie den Zugriff für die Ressourcengruppe überprüfen möchten, listen Sie mit dem Befehl [Get-AzureRmRoleAssignment](/powershell/module/azurerm.resources/get-azurermroleassignment) die Rollenzuweisungen auf.

Führen Sie diese Schritte aus, um alle Rollenzuweisungen für den Benutzer **LabUser-XXXXXXX** im Ressourcengruppenbereich aufzulisten.

1. Kopieren Sie oben im Fenster auf der Registerkarte **Ressourcen** den Befehl **List access PowerShell** (Zugriff auflisten PowerShell).

1. Fügen Sie den Befehl in den PowerShell-Bereich ein, und drücken Sie die EINGABETASTE, um ihn auszuführen. Nachfolgend sehen Sie einen Beispielbefehl und dessen Ausgabe.

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

    Die Ausgabe zeigt, dass die Rolle „Mitwirkender für virtuelle Computer“ dem Benutzer „LabUser-_XXXXXXX_“ im Bereich „FirstUpConsultantsRG1-_XXXXXXX_“ zugewiesen wurde.

    Wenn Sie das Blatt **Zugriffssteuerung (IAM)** für die Ressourcengruppe im Azure-Portal aktualisieren, sieht die Rollenzuweisung wie folgt aus:

    ![Rollenzuweisungen für einen Benutzer im Ressourcengruppenbereich](../media-draft/6-cloud-shell-access-control.png)

## <a name="remove-access"></a>Entfernen des Zugriffs

Verwenden Sie zum Entfernen des Zugriffs für Benutzer, Gruppen und Anwendungen den Befehl [Remove-AzureRmRoleAssignment](/powershell/module/azurerm.resources/remove-azurermroleassignment), um eine Rollenzuweisung zu entfernen.

Führen Sie diese Schritte aus, um dem Benutzer **LabUser-_XXXXXXX_** die Rollenzuweisung „Mitwirkender für virtuelle Computer“ im Ressourcengruppenbereich zu entziehen.

1. Kopieren Sie oben im Fenster auf der Registerkarte **Ressourcen** den Befehl **Remove access PowerShell** (Zugriff entfernen PowerShell).

1. Fügen Sie den Befehl in den PowerShell-Bereich ein, und drücken Sie die EINGABETASTE, um ihn auszuführen. Nachfolgend ist ein Beispielbefehl dargestellt.

    ```Example
    PS Azure:\> Remove-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -RoleDefinitionName "Virtual Machine Contributor" `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"
    ```

1. Klicken Sie im PowerShell-Bereich auf die Schließen-Schaltfläche (**X**), um den Bereich zu schließen.

    ![Cloud Shell – Schaltfläche „Schließen“](../media-draft/6-cloud-shell-close.png)


## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie einem Benutzer mit Azure PowerShell Zugriff erteilen, damit dieser virtuelle Computer in einer Ressourcengruppe erstellen und verwalten kann. In der nächsten Einheit erfahren Sie, wie Sie RBAC-Änderungen im Zeitverlauf anzeigen.
