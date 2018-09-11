Bei First Up Consultants wurde Ihnen Zugriff auf das Azure-Abonnement für das Marketingteam gewährt. Sie möchten sich mit dem Azure-Portal vertraut machen und sehen, welche Rollen derzeit zugewiesen sind.

## <a name="list-role-assignments-for-yourself"></a>Liste von Rollenzuweisungen für Sie selbst

Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen Ihnen derzeit zugewiesen sind.

1. Klicken Sie in der Navigationsliste auf **Azure Active Directory**.

1. Klicken Sie auf **Benutzer**, um **Alle Benutzer** zu öffnen.

    ![Benutzer von Azure Active Directory](../media-draft/4-aad-all-users.png)

1. Suchen Sie den Benutzernamen **LabAdmin-_XXXXXXX_**, und klicken Sie darauf.

    ![Lab-User von Azure Active Directory](../media-draft/4-aad-all-users-lab.png)

1. Klicken Sie im Abschnitt **Verwalten** auf **Azure-Ressourcen**.

    ![Azure-Ressourcen](../media-draft/4-aad-user-azure-resources.png)

    Auf dem Blatt „Azure-Ressourcen“ können Sie die Ressourcen und Rollen sehen, auf die Sie Zugriff haben. Ihre Liste wird anders aussehen.

## <a name="list-role-assignments-for-a-resource-group"></a>Auflisten von Rollenzuweisungen für eine Ressourcengruppe

Führen Sie die folgenden Schritte aus, um zu sehen, welche Rollen im Bereich der Ressourcengruppen zugewiesen wurden.

1. Klicken Sie in der Navigationsliste auf **Ressourcengruppen**.

   ![Ressourcengruppen](../media-draft/4-resource-groups.png)

1. Klicken Sie auf die Ressourcengruppe mit dem Namen **FirstUpConsultantsRG1-_XXXXXXX_**.

1. Klicken Sie auf **Zugriffssteuerung (IAM)**.

   Auf dem Blatt „Zugriffssteuerung (IAM)“ wird angezeigt, wer Zugriff auf diese Ressourcengruppe hat. Beachten Sie, dass einige Rollen auf **Diese Ressource** begrenzt sind, während andere von einem übergeordneten Bereich **geerbt** werden.

   ![Zugriffssteuerung (IAM) für Ressourcengruppe](../media-draft/4-resource-group-access-control.png)

## <a name="list-roles"></a>Auflisten der Rollen

Wie Sie in der vorherigen Einheit gelernt haben, ist eine Rolle eine Sammlung von Berechtigungen. Azure verfügt über mehr als 70 integrierte Rollen, die Sie in Ihren Rollenzuweisungen verwenden können. Führen Sie die folgenden Schritte aus, um die Rollen aufzulisten.

- Klicken Sie oben auf dem Blatt „Zugriffssteuerung (IAM)“ auf **Rollen**, um eine Liste aller integrierten und benutzerdefinierten Rollen anzuzeigen.

   ![Rollenoption](../media-draft/4-roles-option.png)

   Sie können die Anzahl von Benutzern und Gruppen anzeigen, die jeder Rolle zugewiesen sind.

   ![Rollenliste](../media-draft/4-roles-list.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie die Rollenzuweisungen im Azure-Portal für sich selbst auflisten. Außerdem haben Sie gelernt, wie die Rollenzuweisungen in verschiedenen Bereichen aufgelistet werden. In der nächsten Einheit lernen Sie, wie Sie einem Benutzer über die rollenbasierte Zugriffssteuerung Zugriff gewähren.
