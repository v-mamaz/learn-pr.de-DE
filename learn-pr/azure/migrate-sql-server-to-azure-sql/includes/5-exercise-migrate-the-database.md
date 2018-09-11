Da Sie Ihre Datenbank jetzt geprüft und alle gemeldeten Fehler behoben haben, können Sie die Datenbank migrieren. In dieser Einheit erfahren Sie, wie Sie Ihre SQL-Datenbank zu Azure SQL-Datenbank migrieren.

## <a name="setup"></a>Setup

Laden Sie die Beispieldaten herunter, falls noch nicht geschehen.

1. Öffnen Sie einen Internetbrowser, und navigieren Sie zu https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.

1. Klicken Sie unter **OLTP downloads** (OLTP-Downloads) auf **AdventureWorks2008R2.bak**.

1. Stellen Sie **AdventureWorks 2008R2** in Management Studio auf Ihrer Standardinstanz wieder her.

## <a name="create-an-azure-sql-database"></a>Erstellen einer Datenbank für Azure SQL-Datenbank

1. Melden Sie sich bei Ihrem Azure-Portal-Konto an.

1. Klicken Sie im Azure-Portal links oben auf **Ressource erstellen**.

1. Klicken Sie auf **Datenbanken** > **SQL-Datenbank**.

1. Tragen Sie die folgenden Felder in das SQL-Datenbank-Formular ein:

    |Feld|Beschreibung|
    |-----|---|
    |Datenbankname|Geben Sie einen Namen für die Datenbank ein. Sie können dafür den Namen einer bereits vorhandenen Datenbank, die Sie migrieren möchten, oder einen beliebigen anderen Name auswählen.|
    |Ressourcengruppe|Wählen Sie eine Ressourcengruppe aus, oder geben Sie einen neuen Namen für die Ressourcengruppe ein.|
    |Auswählen einer Quelle|Klicken Sie auf *Leere Datenbank*.|

1. Wählen Sie unter **Server** entweder einen bereits vorhandenen Server aus, oder geben Sie einen eindeutigen **Servernamen**, **Anmeldeinformationen für einen Serveradministrator**, ein **Kennwort** (das Sie bestätigen sollten) und einen **Speicherort** an.

    > [!NOTE]
    > Sie benötigen den Servernamen, die Anmeldeinformationen und das Kennwort, um eine Verbindung für Ihrer Datenbank herzustellen.

1. Klicken Sie auf **Auswählen**.

1. Sie können zwar unter **Tarif** eine Datenbank mit besserer Leistung auswählen, aber für dieses Tutorial sollten Sie die Standarddatenbank verwenden.

1. Klicken Sie auf **Erstellen**. Warten Sie, bis die Datenbank bereitgestellt wurde, bevor Sie mit dem Tutorial fortfahren.

    Im folgenden Screenshot ist eine mögliche Konfiguration Ihrer neuen SQL-Datenbank dargestellt.

    ![Screenshot: Neues SQL-Datenbank-Blatt im Azure-Portal mit einer Beispielkonfiguration](../media-draft/5-create-azure-sql-db.png)

## <a name="create-a-new-migration-project"></a>Erstellen eines neues Migrationsprojekts

1. Öffnen Sie den **Datenmigrations-Assistenten**.

1. Klicken Sie auf das Symbol **Neu**, und geben Sie die folgenden Optionen an:

    - **Projekttyp:** Klicken Sie auf die Option *Migration*.
    - **Projektname:** Geben Sie einen Namen für Ihr Projekt ein, den Sie sich gut merken können.
    - **Typ des Quellservers:** Klicken Sie auf *SQL Server*.
    - **Typ des Zielservers:** Klicken Sie auf *Azure SQL-Datenbank*.
    - **Migrationsumfang:** Klicken Sie auf *Schema and data* (Schema und Daten).

1. Klicken Sie auf **Erstellen**.

## <a name="specify-the-source-server-and-database"></a>Angeben des Quellservers und der Datenbank

1. Geben Sie unter **Connect to source server** (Mit Quellserver verbinden) in das Feld **Servername** den Namen der SQL Server-Quellinstanz ein.

1. Wählen Sie den **Authentifizierungstyp** aus, der von der SQL Server-Quellinstanz unterstützt wird.
    > [!TIP]
    > Es wird empfohlen, dass Sie unter „Verbindungseigenschaften“ das Kontrollkästchen **Verbindung verschlüsseln** aktivieren, um die Verbindung zu verschlüsseln.

1. Klicken Sie auf **Verbinden**.

1. Wählen Sie eine einzelne Quelldatenbank aus, die zu Azure SQL-Datenbank migriert werden soll, und klicken Sie dann auf **Weiter**.

## <a name="specify-the-target-server-and-database"></a>Angeben des Zielservers und der Datenbank

1. Geben Sie unter **Connect to target server** (Mit Zielserver verbinden) in das Feld **Servername** den Namen der Azure SQL Server-Instanz ein. Fügen Sie **database.windows.net** zu der Datenbankinstanz hinzu.

1. Wählen Sie den Authentifizierungstyp aus, der von der Azure SQL Datenbank-Zielinstanz unterstützt wird. Klicken Sie für dieses Tutorial auf **SQL Server-Authentifizierung**.
    > [!TIP]
    > Es wird empfohlen, dass Sie unter „Verbindungseigenschaften“ das Kontrollkästchen **Verbindung verschlüsseln** aktivieren, um die Verbindung zu verschlüsseln.

1. Geben Sie den **Benutzernamen** und das **Kennwort** ein, das Sie beim Erstellen der Datenbank für Azure SQL-Datenbank angegeben haben.

1. Klicken Sie auf **Verbinden**.

1. Wählen Sie eine Zieldatenbank aus, zu der migriert werden soll.
    > [HINWEIS] Wenn Sie Windows-Benutzer migrieren möchten, prüfen Sie im Feld „Target external user domain name“ (Name der externen Zieldomäne der Benutzer), ob der Name der externen Zieldomäne des Benutzers richtig angegeben ist.

1. Klicken Sie auf **Weiter**.

## <a name="select-schema-objects"></a>Auswählen von Schemaobjekten

1. Wählen Sie die Schemaobjekte aus der Quelldatenbank aus , die Sie zu Azure SQL-Datenbank migrieren möchten.

    > [!NOTE]
    > Für die Objekte, an denen Änderungen vorgenommen werden müssen, damit sie migriert werden können, gibt es automatische Möglichkeiten zur Problembehandlung. Wenn Sie im linken Bereich auf diese Objekte klicken, werden die vorgeschlagenen Möglichkeiten zur Fehlerbehebung auf der rechten Seite angezeigt. Prüfen Sie diese, und entscheiden Sie für jedes Objekt, ob Sie alle Änderungen akzeptieren oder ignorieren möchten. Beachten Sie, dass es keine Auswirkungen auf Änderungen anderer Datenbankobjekte hat, wenn Sie alle Änderungen annehmen oder ignorieren. Anweisungen, die nicht konvertiert oder automatisch verbessert werden können, werden in der Zieldatenbank reproduziert und mit einem Kommentar versehen.

    ![Screenshot: Datenmigrations-Assistent, in dem eine Liste mit Migrationsproblemen angezeigt wird, die Auswirkungen auf AdventureWorks-SQL-Server-Daten haben, für die das Problem "Stored Procedure: dbo.uspSearchCandidateResumes" (Gespeicherte Prozedur: dbo.uspSearchCandidateResumes) und die Fehlerdetails angezeigt werden.](../media-draft/5-suggested-fix.png)

1. Klicken Sie **SQL-Skript generieren**.

## <a name="deploy-schema"></a>Bereitstellen des Schemas

1. Klicken Sie auf **Deploy schema** (Schema bereitstellen).

1. Sehen Sie sich die Ergebnisse der Schemabereitstellung an.

## <a name="migrate-data"></a>Migrieren von Daten

1. Klicken Sie auf **Daten migrieren**, um mit der Datenmigration zu beginnen.

1. Wählen Sie die Tabellen mit den Daten aus, die Sie migrieren möchten.

1. Klicken Sie auf **Datenmigration starten**.

Auf dem letzten Bildschirm wird der allgemeine Status angezeigt.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie erfahren, wie Sie eine leere Datenbank für Azure SQL-Datenbank erstellen und eine lokale SQL Server-Datenbank zu dieser neuen Datenbank migrieren.