Am ersten Einrichten-Berater vorgesehen sind haben Sie Zugriff auf eine Ressourcengruppe für das marketing-Team gewährt wurde. Sie möchten sich mit dem Azure-Portal vertraut machen und sehen, welche Rollen derzeit zugewiesen sind.

## <a name="launch-lab-and-sign-in-to-the-azure-portal"></a>Starten Sie Lab, und melden Sie sich beim Azure-portal

1. Klicken Sie auf den Link oben, um das Labor zu starten.

1. Melden Sie sich beim Azure-Portal als **LabAdmin -_XXXXXXX_@_Xxxxxxxxxxxx_. "onmicrosoft.com"**. Den Benutzernamen und das Kennwort finden Sie oben im Fenster auf der Registerkarte **Ressourcen**.

## <a name="list-role-assignments-for-yourself"></a>Liste von Rollenzuweisungen für Sie selbst

Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen Ihnen derzeit zugewiesen sind.

1. Klicken Sie in der oberen rechten Ecke des Azure-Portals auf Ihren Benutzernamen ein, um das Menü zu öffnen.

    ![Meine Berechtigungen-Menü](../media/4-my-permissions-menu.png)

1. Klicken Sie auf **meine Berechtigungen** zum Öffnen der mein Bereich.

    ![Meine Berechtigungen-Bereich](../media/4-my-permissions-pane.png)

    Auf der mein Bereich Berechtigungen können Sie sehen eine Liste der Rollen, die Ihnen zugewiesen wurde und den Bereich. Ihre Liste wird anders aussehen.

## <a name="list-role-assignments-for-a-resource-group"></a>Auflisten von Rollenzuweisungen für eine Ressourcengruppe

Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen im Bereich der Ressourcengruppen zugewiesen wurden.

1. Klicken Sie in der Navigationsliste auf **Ressourcengruppen**.

   ![Ressourcengruppen](../media/4-resource-groups.png)

1. Suchen, und klicken Sie auf die Ressourcengruppe mit dem Namen **FirstUpConsultantsRG1 -_XXXXXXX_**.

1. Klicken Sie auf **Zugriffssteuerung (IAM)**.

   ![Zugriffssteuerung für Ressourcengruppe](../media/4-resource-group-access-control.png)

1. Klicken Sie auf **rollenzuweisung**.

    Sie sehen, wer Zugriff auf diese Ressourcengruppe hat. Beachten Sie, dass einige Rollen auf **Diese Ressource** begrenzt sind, während andere von einem übergeordneten Bereich **geerbt** werden.

   ![Zugriffssteuerung - rollenzuweisung für Ressourcengruppe](../media/4-resource-group-role-assignment.png)

## <a name="list-roles"></a>Auflisten der Rollen

Wie Sie in der vorherigen Einheit gelernt haben, ist eine Rolle eine Sammlung von Berechtigungen. Azure verfügt über mehr als 70 integrierte Rollen, die Sie in Ihren Rollenzuweisungen verwenden können. Führen Sie diesen Schritt zum Auflisten der Rollen aus.

- Klicken Sie unter rollenzuweisung auf **Rollen** um eine Liste aller integrierten und benutzerdefinierten Rollen anzuzeigen.

   Sie können die Anzahl von Benutzern und Gruppen anzeigen, die jeder Rolle zugewiesen sind.

   ![Rollenliste](../media/4-roles-list.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie die Rollenzuweisungen im Azure-Portal für sich selbst auflisten. Sie haben zudem die Vorgehensweise beim Auflisten der rollenzuweisungen für eine Ressourcengruppe aus. In der nächsten Einheit lernen Sie, wie Sie einem Benutzer über die rollenbasierte Zugriffssteuerung Zugriff gewähren.
