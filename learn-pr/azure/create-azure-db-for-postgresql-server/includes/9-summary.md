In diesem Modul haben Sie erfahren, was Azure Database for PostgreSQL Ihnen bietet. Sie haben erfahren, wie eine Instanz von Azure Database for PostgreSQL über das Azure-Portal oder die Azure CLI erstellt wird.

Sie haben die verfügbaren Optionen zur Konfiguration einer PostgreSQL-Firewallregel auf Serverebene und zum Erzwingen von SSL-Verbindungen kennen gelernt. Abschließend erfuhren Sie, wie die Verbindung mit einem Azure Database for PostgreSQL-Server in Azure Cloud Shell mit _psql_ hergestellt wird.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?--->

Jetzt müssen Sie nur noch die in den Labs erstellten Ressourcen bereinigen. Denken Sie daran, dass der Server auch dann eine monatliche Gebühr generiert, wenn Sie ihn nicht verwenden. Wenn Sie Ressourcen zu Testzwecken erstellen, können Sie diese ohne großen Aufwand entfernen, indem Sie die Ressourcengruppe löschen, zu der diese gehören.

> [!NOTE]
> Zur Erinnerung: Eine Ressourcengruppe ist eine Sammlung von Ressourcen, die in Bezug auf Lebenszyklus, Berechtigungen und Richtlinien gleich sind. Diese Aktionen löschen alle Ressourcen in dieser Ressourcengruppe, einschließlich aller Daten, die Sie möglicherweise den Datenbanken auf dem Server, die Sie erstellt haben, hinzugefügt haben.

- Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

- Wählen Sie im linken Menü **Ressourcengruppen** aus, um alle Ressourcengruppen anzuzeigen, die derzeit für Ihr Konto verwendet werden.

- Klicken Sie auf den Namen der Ressourcengruppe, die Sie erstellt haben, und klicken Sie in der Symbolleiste im oberen Bereich auf die Schaltfläche **Ressourcengruppe löschen**.

- In einem Dialogfeld mit dem Titel **Möchten Sie `<resource_group_name>` löschen?** werden Sie aufgefordert, den Namen der Ressourcengruppe einzugeben, um den Löschvorgang zu bestätigen. Bestätigen Sie den Namen der Ressourcengruppe, und klicken Sie unten auf die Schaltfläche „Löschen“.
