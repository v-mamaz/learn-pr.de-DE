> [!NOTE]
> Nachdem das Lab gestartet wurde, finden Sie auf der Registerkarte **Ressourcen** neben den Anweisungen die erforderlichen Anmeldeinformationen.

Bei First Up Consultants wurde Ihnen Zugriff auf eine Ressourcengruppe für das Marketingteam gewährt. Sie möchten sich mit dem Azure-Portal vertraut machen und sehen, welche Rollen derzeit zugewiesen sind.

## <a name="list-role-assignments-for-yourself"></a>Liste von Rollenzuweisungen für Sie selbst

Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen Ihnen zurzeit zugewiesen sind.

1. Klicken Sie in der oberen rechten Ecke des Azure-Portals auf Ihren Benutzernamen, um das Menü zu öffnen.

    ![Menü „Meine Berechtigungen“](../media/4-my-permissions-menu.png)

1. Klicken Sie auf **Meine Berechtigungen**, um den Bereich „Meine Berechtigungen“ zu öffnen.

    ![Bereich „Meine Berechtigungen“](../media/4-my-permissions-pane.png)

    Im Bereich „Meine Berechtigungen“ wird eine Liste der Ihnen zugewiesenen Rollen und deren Bereich angezeigt. Ihre Liste wird anders aussehen.

## <a name="list-role-assignments-for-a-resource-group"></a>Auflisten von Rollenzuweisungen für eine Ressourcengruppe

Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen im Bereich der Ressourcengruppen zugewiesen wurden.

1. Klicken Sie in der Navigationsliste auf **Ressourcengruppen**.

   ![Ressourcengruppen](../media/4-resource-groups.png)

1. Suchen Sie die Ressourcengruppe mit dem Namen **FirstUpConsultantsRG1-_XXXXXXX_**, und klicken Sie darauf.

1. Klicken Sie auf **Zugriffssteuerung (IAM)**.

   ![Zugriffssteuerung für die Ressourcengruppe](../media/4-resource-group-access-control.png)

    Ihnen wird angezeigt, wer über Zugriff auf diese Ressourcengruppe verfügt. Beachten Sie, dass einige Rollen auf **diese Ressource** begrenzt sind, während andere von einem übergeordneten Bereich **geerbt** werden.

   ![Zugriffssteuerung: Rollenzuweisung für die Ressourcengruppe](../media/4-resource-group-role-assignment.png)

## <a name="list-roles"></a>Auflisten der Rollen

Wie Sie in der vorherigen Einheit gelernt haben, ist eine Rolle eine Sammlung von Berechtigungen. Azure verfügt über mehr als 70 integrierte Rollen, die Sie in Ihren Rollenzuweisungen verwenden können. Führen Sie diesen Schritt aus, um die Rollen aufzulisten.

- Klicken Sie am oberen Rand des Bereichs auf **Rollen**, um eine Liste aller integrierten und benutzerdefinierten Rollen anzuzeigen.

   Sie können die Anzahl von Benutzern und Gruppen anzeigen, die jeder Rolle zugewiesen sind.

   ![Rollenliste](../media/4-roles-list.png)

In dieser Einheit haben Sie gelernt, wie Sie die Rollenzuweisungen im Azure-Portal für sich selbst auflisten. Außerdem haben Sie gelernt, wie Sie die Rollenzuweisungen für eine Ressourcengruppe auflisten.