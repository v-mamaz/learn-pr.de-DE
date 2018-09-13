Da Ihre Azure SQL-Datenbank nun in Betrieb ist, können Sie sie nun mit Ihrem bevorzugten SQL Server-Verwaltungstool verknüpfen, um sie mit echten Daten zu füllen.

Anfangs haben Sie sich Gedanken darüber gemacht, ob Sie Ihre Datenbank lokal oder in der Cloud ausführen. Mit Azure SQL-Datenbank müssen Sie nur einige grundlegende Optionen konfigurieren, um eine voll funktionsfähige SQL-Datenbank zu erhalten, die Sie mit Ihren Apps verbinden können.

Sie müssen keine Infrastruktur- oder Softwarepatches verwalten. Sie können sich nun darauf konzentrieren, den Prototyp Ihrer Transportlogistik-App in Betrieb zu nehmen, anstatt sich mit der Datenbankverwaltung zu beschäftigen. Der Prototyp soll auch nicht als weggeworfene Demo enden. Azure SQL-Datenbank bietet Sicherheits- und Leistungsfeatures auf Produktionsniveau.

Denken Sie daran, dass jeder logische Azure SQL-Server mindestens eine Datenbank enthält. Azure SQL-Datenbank bietet zwei Preismodelle, nach Datenbanktransaktionseinheit (DTU) oder virtuellen Kernen, damit Sie die Kosten mit den Leistungen über alle Datenbanken hinweg ausgleichen können.

Wählen Sie das DTU-Modell aus, wenn Sie erst anfangen oder eine einfache vorkonfigurierte Kaufoption möchten. Wählen Sie das Modell für virtuelle Kerne aus, wenn Sie mehr Kontrolle über die Compute- und Speicherressourcen möchten, die Sie erstellen und bezahlen.

Azure Cloud Shell erleichtert den Einstieg in die Arbeit mit Datenbanken. Über Cloud Shell können Sie auf Azure CLI zugreifen, um Informationen über Azure-Ressourcen abzurufen. Cloud Shell bietet auch viele andere allgemeine Hilfsprogramme, z.B. `sqlcmd`, damit Sie sofort mit Ihrer neuen Datenbank arbeiten können.

## <a name="cleanup"></a>Bereinigen

Sie können mehr mit der Installation der Azure SQL-Datenbank herumexperimentieren. Wenn Sie fertig sind, besteht die einfachste Möglichkeit zum Löschen der Datenbank darin, die übergeordnete Ressourcengruppe zu löschen.

1. Klicken Sie im Azure-Portal auf **Ressourcengruppen**.

1. Wählen Sie **logistics-db-rg** aus.

1. Klicken Sie auf **Ressourcengruppe löschen**.

    ![Löschen der Ressourcengruppe](../media-draft/delete-rg.png)

1. Geben Sie „logistics-db-rg“ in der Eingabeaufforderung ein, und klicken Sie auf **Löschen**.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Die Dokumentation enthält viele weitere Informationen sowie Tutorials und Beispiele. Unter den folgenden Links finden Sie Informationen zu den hier behandelten Themen:

- [Dokumentation zu Azure SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/)
- [Kaufmodelle für Azure SQL-Datenbank und Ressourcen](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)
- [Logischer Azure SQL-Datenbankserver und dessen Verwaltung](https://docs.microsoft.com/azure/sql-database/sql-database-logical-servers)
- [Azure SQL Database and SQL Data Warehouse firewall rules (Firewallregeln für Azure SQL-Datenbank und SQL Data Warehouse)](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)

Weitere Informationen über Cloud Shell finden Sie in der [Übersicht über Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).

Weitere Informationen über das `sqlcmd`-Hilfsprogramm finden Sie im Artikel zum [sqlcmd-Hilfsprogramm](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-2017).
