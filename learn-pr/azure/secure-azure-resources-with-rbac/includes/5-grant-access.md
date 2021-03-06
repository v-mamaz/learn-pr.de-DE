Ein Kollege bei First Up Consultants mit dem Namen Alain muss für ein Projekt, an dem er aktuell arbeitet, virtuelle Computer erstellen und verwalten können. Ihr Manager hat Sie darum gebeten, diese Anforderung zu bearbeiten. Unter Verwendung der Best Practices zur Gewährung minimaler Berechtigungen für Benutzer, damit diese ihren Auftrag durchführen können, entscheiden Sie sich dazu, Alain die Rolle „Mitwirkender für virtuelle Computer“ für eine Ressourcengruppe zuzuweisen.

## <a name="grant-access"></a>Gewähren von Zugriff

Führen Sie diese Schritte aus, um einem Benutzer im Bereich der Ressourcengruppen die Rolle „Mitwirkender für virtuelle Computer“ zuzuweisen.

1. Klicken Sie in der Navigationsliste auf **Ressourcengruppen**.

1. Suchen Sie die Ressourcengruppe **FirstUpConsultantsRG1-_XXXXXXX_**, und klicken Sie darauf.

1. Klicken Sie auf **Zugriffssteuerung (IAM)**, um die aktuelle Liste der Rollenzuweisungen anzuzeigen.

   ![Zugriffssteuerung: Rollenzuweisung für die Ressourcengruppe](../media/5-resource-group-role-assignment.png)

1. Klicken Sie im oberen Bereich auf **Hinzufügen**, um den Bereich **Berechtigungen hinzufügen** zu öffnen.

   ![Bereich „Berechtigungen hinzufügen“](../media/5-add-permissions.png)

1. Wählen Sie in der Dropdownliste **Rolle** die Rolle **Mitwirkender für virtuelle Computer** aus.

1. Wählen Sie aus der Liste **Auswählen** den Benutzer **LabUser-_XXXXXXX_** aus.

    Der Benutzername befindet sich auf der Registerkarte **Ressourcen** neben den Anweisungen.

   ![Bereich „Berechtigungen hinzufügen“ abgeschlossen](../media/5-add-permissions-save.png)

1. Klicken Sie auf **Speichern**, um die Rollenzuweisung zu erstellen.

   Nach einigen Augenblicken wird der Benutzer **LabUser-_XXXXXXX_** der Rolle „Mitwirkender für virtuelle Computer“ im Bereich **FirstUpConsultantsRG1-_XXXXXXX_** der Ressourcengruppen zugewiesen. Der Benutzer kann nun nur in dieser Ressourcengruppe virtuelle Computer erstellen und verwalten.

   ![Zuweisung der Rolle „Mitwirkender für virtuelle Computer“](../media/5-vm-contributor-assignment.png)

## <a name="remove-access"></a>Entfernen des Zugriffs

In RBAC entfernen Sie eine Rollenzuweisung, um den Zugriff zu entfernen.

1. Wählen Sie in der Liste der Rollenzuweisungen den Benutzer **LabUser-_XXXXXXX_** mit der Rolle „Mitwirkender für virtuelle Computer“ aus.

1. Klicken Sie auf **Entfernen**.

   ![Nachricht zum Entfernen der Rollenzuweisung](../media/5-remove-role-assignment.png)

1. Klicken Sie in der Nachricht zum **Entfernen von Rollenzuweisungen** auf **Ja**.

In dieser Einheit haben Sie gelernt, wie Sie einem Benutzer über das Azure-Portal Zugriff gewähren, damit dieser virtuelle Computer in einer Ressourcengruppe erstellen und verwalten kann.