<span data-ttu-id="50d01-101">Da Sie Ihre Datenbank jetzt geprüft und alle gemeldeten Fehler behoben haben, können Sie die Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="50d01-101">Now that you have assessed your database and fixed any errors reported, you're ready to migrate your database.</span></span> <span data-ttu-id="50d01-102">In dieser Einheit erfahren Sie, wie Sie Ihre SQL-Datenbank zu Azure SQL-Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="50d01-102">In this unit, you will migrate your SQL database to Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="50d01-103">Setup</span><span class="sxs-lookup"><span data-stu-id="50d01-103">Setup</span></span>

<span data-ttu-id="50d01-104">Laden Sie die Beispieldaten herunter, falls noch nicht geschehen.</span><span class="sxs-lookup"><span data-stu-id="50d01-104">If you haven't already, download the sample data.</span></span>

1. <span data-ttu-id="50d01-105">Öffnen Sie einen Internetbrowser, und navigieren Sie zu https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span><span class="sxs-lookup"><span data-stu-id="50d01-105">Start an internet browser and navigate to https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="50d01-106">Klicken Sie unter **OLTP downloads** (OLTP-Downloads) auf **AdventureWorks2008R2.bak**.</span><span class="sxs-lookup"><span data-stu-id="50d01-106">In **OLTP downloads**, click **AdventureWorks2008R2.bak**.</span></span>

1. <span data-ttu-id="50d01-107">Stellen Sie **AdventureWorks 2008R2** in Management Studio auf Ihrer Standardinstanz wieder her.</span><span class="sxs-lookup"><span data-stu-id="50d01-107">In Management Studio, restore **AdventureWorks 2008R2** to your default instance.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="50d01-108">Erstellen einer Datenbank für Azure SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="50d01-108">Create an Azure SQL Database</span></span>

1. <span data-ttu-id="50d01-109">Melden Sie sich bei Ihrem Azure-Portal-Konto an.</span><span class="sxs-lookup"><span data-stu-id="50d01-109">Sign in to your Azure portal account.</span></span>

1. <span data-ttu-id="50d01-110">Klicken Sie im Azure-Portal links oben auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="50d01-110">Click **Create a resource** in the upper left-hand corner of the portal.</span></span>

1. <span data-ttu-id="50d01-111">Klicken Sie auf **Datenbanken** > **SQL-Datenbank**.</span><span class="sxs-lookup"><span data-stu-id="50d01-111">Click **Databases** > **SQL Database**.</span></span>

1. <span data-ttu-id="50d01-112">Tragen Sie die folgenden Felder in das SQL-Datenbank-Formular ein:</span><span class="sxs-lookup"><span data-stu-id="50d01-112">Enter the following fields on the SQL Database form:</span></span>

    |<span data-ttu-id="50d01-113">Feld</span><span class="sxs-lookup"><span data-stu-id="50d01-113">Field</span></span>|<span data-ttu-id="50d01-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="50d01-114">Description</span></span>|
    |-----|---|
    |<span data-ttu-id="50d01-115">Datenbankname</span><span class="sxs-lookup"><span data-stu-id="50d01-115">Database name</span></span>|<span data-ttu-id="50d01-116">Geben Sie einen Namen für die Datenbank ein.</span><span class="sxs-lookup"><span data-stu-id="50d01-116">Enter a name for your database.</span></span> <span data-ttu-id="50d01-117">Sie können dafür den Namen einer bereits vorhandenen Datenbank, die Sie migrieren möchten, oder einen beliebigen anderen Name auswählen.</span><span class="sxs-lookup"><span data-stu-id="50d01-117">This can be the name of your existing database that you're migrating, or any new name of your choice</span></span>|
    |<span data-ttu-id="50d01-118">Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="50d01-118">Resource group</span></span>|<span data-ttu-id="50d01-119">Wählen Sie eine Ressourcengruppe aus, oder geben Sie einen neuen Namen für die Ressourcengruppe ein.</span><span class="sxs-lookup"><span data-stu-id="50d01-119">Select a resource group or enter a new resource group name</span></span>|
    |<span data-ttu-id="50d01-120">Auswählen einer Quelle</span><span class="sxs-lookup"><span data-stu-id="50d01-120">Select source</span></span>|<span data-ttu-id="50d01-121">Klicken Sie auf *Leere Datenbank*.</span><span class="sxs-lookup"><span data-stu-id="50d01-121">Select *Blank database*</span></span>|

1. <span data-ttu-id="50d01-122">Wählen Sie unter **Server** entweder einen bereits vorhandenen Server aus, oder geben Sie einen eindeutigen **Servernamen**, **Anmeldeinformationen für einen Serveradministrator**, ein **Kennwort** (das Sie bestätigen sollten) und einen **Speicherort** an.</span><span class="sxs-lookup"><span data-stu-id="50d01-122">Under **Server**, either select an existing server or, enter a globally unique **Server name**, a **Server admin login**, a **Password** (which you should confirm), and a **Location**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="50d01-123">Sie benötigen den Servernamen, die Anmeldeinformationen und das Kennwort, um eine Verbindung für Ihrer Datenbank herzustellen.</span><span class="sxs-lookup"><span data-stu-id="50d01-123">You will use the server name, login name, and password to connect to your database.</span></span>

1. <span data-ttu-id="50d01-124">Klicken Sie auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="50d01-124">Click **Select**.</span></span>

1. <span data-ttu-id="50d01-125">Sie können zwar unter **Tarif** eine Datenbank mit besserer Leistung auswählen, aber für dieses Tutorial sollten Sie die Standarddatenbank verwenden.</span><span class="sxs-lookup"><span data-stu-id="50d01-125">In **Pricing tier**, you can select a database with higher performance, but for this tutorial, select default.</span></span>

1. <span data-ttu-id="50d01-126">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="50d01-126">Click **Create**.</span></span> <span data-ttu-id="50d01-127">Warten Sie, bis die Datenbank bereitgestellt wurde, bevor Sie mit dem Tutorial fortfahren.</span><span class="sxs-lookup"><span data-stu-id="50d01-127">Wait until the database has been provisioned before continuing the tutorial.</span></span>

    <span data-ttu-id="50d01-128">Im folgenden Screenshot ist eine mögliche Konfiguration Ihrer neuen SQL-Datenbank dargestellt.</span><span class="sxs-lookup"><span data-stu-id="50d01-128">The following screenshot shows a potential configuration for your new SQL database.</span></span>

    ![Screenshot: Neues SQL-Datenbank-Blatt im Azure-Portal mit einer Beispielkonfiguration](../media-draft/5-create-azure-sql-db.png)

## <a name="create-a-new-migration-project"></a><span data-ttu-id="50d01-130">Erstellen eines neues Migrationsprojekts</span><span class="sxs-lookup"><span data-stu-id="50d01-130">Create a new migration project</span></span>

1. <span data-ttu-id="50d01-131">Öffnen Sie den **Datenmigrations-Assistenten**.</span><span class="sxs-lookup"><span data-stu-id="50d01-131">Start **Data Migration Assistant**.</span></span>

1. <span data-ttu-id="50d01-132">Klicken Sie auf das Symbol **Neu**, und geben Sie die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="50d01-132">Click the **New** icon, and specify the following options:</span></span>

    - <span data-ttu-id="50d01-133">**Projekttyp:** Klicken Sie auf die Option *Migration*.</span><span class="sxs-lookup"><span data-stu-id="50d01-133">**Project type** - Select  the *Migration* option.</span></span>
    - <span data-ttu-id="50d01-134">**Projektname:** Geben Sie einen Namen für Ihr Projekt ein, den Sie sich gut merken können.</span><span class="sxs-lookup"><span data-stu-id="50d01-134">**Project name** - Enter a memorable name for your project.</span></span>
    - <span data-ttu-id="50d01-135">**Typ des Quellservers:** Klicken Sie auf *SQL Server*.</span><span class="sxs-lookup"><span data-stu-id="50d01-135">**Source server type** - Select *SQL Server*.</span></span>
    - <span data-ttu-id="50d01-136">**Typ des Zielservers:** Klicken Sie auf *Azure SQL-Datenbank*.</span><span class="sxs-lookup"><span data-stu-id="50d01-136">**Target server type** - Select *Azure SQL Database*.</span></span>
    - <span data-ttu-id="50d01-137">**Migrationsumfang:** Klicken Sie auf *Schema and data* (Schema und Daten).</span><span class="sxs-lookup"><span data-stu-id="50d01-137">**Migration scope** - Select *Schema and data*.</span></span>

1. <span data-ttu-id="50d01-138">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="50d01-138">Click **Create**.</span></span>

## <a name="specify-the-source-server-and-database"></a><span data-ttu-id="50d01-139">Angeben des Quellservers und der Datenbank</span><span class="sxs-lookup"><span data-stu-id="50d01-139">Specify the source server and database</span></span>

1. <span data-ttu-id="50d01-140">Geben Sie unter **Connect to source server** (Mit Quellserver verbinden) in das Feld **Servername** den Namen der SQL Server-Quellinstanz ein.</span><span class="sxs-lookup"><span data-stu-id="50d01-140">Under **Connect to source server**, in the **Server name** field, enter the name of the source SQL Server instance.</span></span>

1. <span data-ttu-id="50d01-141">Wählen Sie den **Authentifizierungstyp** aus, der von der SQL Server-Quellinstanz unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="50d01-141">Select the **Authentication type** supported by the source SQL Server instance.</span></span>
    > [!TIP]
    > <span data-ttu-id="50d01-142">Es wird empfohlen, dass Sie unter „Verbindungseigenschaften“ das Kontrollkästchen **Verbindung verschlüsseln** aktivieren, um die Verbindung zu verschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="50d01-142">It is recommended that you select the **Encrypt connection** check box under Connection properties to encrypt the connection.</span></span>

1. <span data-ttu-id="50d01-143">Klicken Sie auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="50d01-143">Select **Connect**.</span></span>

1. <span data-ttu-id="50d01-144">Wählen Sie eine einzelne Quelldatenbank aus, die zu Azure SQL-Datenbank migriert werden soll, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="50d01-144">Select a single source database to migrate to Azure SQL Database and click **Next**.</span></span>

## <a name="specify-the-target-server-and-database"></a><span data-ttu-id="50d01-145">Angeben des Zielservers und der Datenbank</span><span class="sxs-lookup"><span data-stu-id="50d01-145">Specify the target server and database</span></span>

1. <span data-ttu-id="50d01-146">Geben Sie unter **Connect to target server** (Mit Zielserver verbinden) in das Feld **Servername** den Namen der Azure SQL Server-Instanz ein.</span><span class="sxs-lookup"><span data-stu-id="50d01-146">Under **Connect to target server**, in the **Server name** field, enter the name of the Azure SQL Database instance.</span></span> <span data-ttu-id="50d01-147">Fügen Sie **database.windows.net** zu der Datenbankinstanz hinzu.</span><span class="sxs-lookup"><span data-stu-id="50d01-147">Add **database.windows.net** to the database instance.</span></span>

1. <span data-ttu-id="50d01-148">Wählen Sie den Authentifizierungstyp aus, der von der Azure SQL Datenbank-Zielinstanz unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="50d01-148">Select the Authentication type supported by the target Azure SQL Database instance.</span></span> <span data-ttu-id="50d01-149">Klicken Sie für dieses Tutorial auf **SQL Server-Authentifizierung**.</span><span class="sxs-lookup"><span data-stu-id="50d01-149">For this tutorial, select **SQL Server Authentication**.</span></span>
    > [!TIP]
    > <span data-ttu-id="50d01-150">Es wird empfohlen, dass Sie unter „Verbindungseigenschaften“ das Kontrollkästchen **Verbindung verschlüsseln** aktivieren, um die Verbindung zu verschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="50d01-150">It is recommended that you select the **Encrypt connection** check box under Connection properties to encrypt the connection.</span></span>

1. <span data-ttu-id="50d01-151">Geben Sie den **Benutzernamen** und das **Kennwort** ein, das Sie beim Erstellen der Datenbank für Azure SQL-Datenbank angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="50d01-151">Enter the **Username** and **Password** that you defined when you created the Azure SQL Database.</span></span>

1. <span data-ttu-id="50d01-152">Klicken Sie auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="50d01-152">Click **Connect**.</span></span>

1. <span data-ttu-id="50d01-153">Wählen Sie eine Zieldatenbank aus, zu der migriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="50d01-153">Select a single target database to which to migrate.</span></span>
    > <span data-ttu-id="50d01-154">[HINWEIS] Wenn Sie Windows-Benutzer migrieren möchten, prüfen Sie im Feld „Target external user domain name“ (Name der externen Zieldomäne der Benutzer), ob der Name der externen Zieldomäne des Benutzers richtig angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="50d01-154">[NOTE] If you intend to migrate Windows users, in the Target external user domain name text box, make sure that the target external user domain name is specified correctly.</span></span>

1. <span data-ttu-id="50d01-155">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="50d01-155">Click **Next**.</span></span>

## <a name="select-schema-objects"></a><span data-ttu-id="50d01-156">Auswählen von Schemaobjekten</span><span class="sxs-lookup"><span data-stu-id="50d01-156">Select schema objects</span></span>

1. <span data-ttu-id="50d01-157">Wählen Sie die Schemaobjekte aus der Quelldatenbank aus , die Sie zu Azure SQL-Datenbank migrieren möchten.</span><span class="sxs-lookup"><span data-stu-id="50d01-157">Select the schema objects from the source database that you want to migrate to Azure SQL Database.</span></span>

    > [!NOTE]
    > <span data-ttu-id="50d01-158">Für die Objekte, an denen Änderungen vorgenommen werden müssen, damit sie migriert werden können, gibt es automatische Möglichkeiten zur Problembehandlung.</span><span class="sxs-lookup"><span data-stu-id="50d01-158">Some of the objects that cannot be converted as-is are presented with automatic fix opportunities.</span></span> <span data-ttu-id="50d01-159">Wenn Sie im linken Bereich auf diese Objekte klicken, werden die vorgeschlagenen Möglichkeiten zur Fehlerbehebung auf der rechten Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="50d01-159">Clicking these objects on the left pane displays the suggested fixes on the right pane.</span></span> <span data-ttu-id="50d01-160">Prüfen Sie diese, und entscheiden Sie für jedes Objekt, ob Sie alle Änderungen akzeptieren oder ignorieren möchten.</span><span class="sxs-lookup"><span data-stu-id="50d01-160">Review the fixes and choose to either apply or ignore all changes, object by object.</span></span> <span data-ttu-id="50d01-161">Beachten Sie, dass es keine Auswirkungen auf Änderungen anderer Datenbankobjekte hat, wenn Sie alle Änderungen annehmen oder ignorieren.</span><span class="sxs-lookup"><span data-stu-id="50d01-161">Note that applying or ignoring all changes for one object does not affect changes to other database objects.</span></span> <span data-ttu-id="50d01-162">Anweisungen, die nicht konvertiert oder automatisch verbessert werden können, werden in der Zieldatenbank reproduziert und mit einem Kommentar versehen.</span><span class="sxs-lookup"><span data-stu-id="50d01-162">Statements that cannot be converted or automatically fixed are reproduced to the target database and commented.</span></span>

    ![Screenshot: Datenmigrations-Assistent, in dem eine Liste mit Migrationsproblemen angezeigt wird, die Auswirkungen auf AdventureWorks-SQL-Server-Daten haben, für die das Problem "Stored Procedure: dbo.uspSearchCandidateResumes" (Gespeicherte Prozedur: dbo.uspSearchCandidateResumes) und die Fehlerdetails angezeigt werden.](../media-draft/5-suggested-fix.png)

1. <span data-ttu-id="50d01-164">Klicken Sie **SQL-Skript generieren**.</span><span class="sxs-lookup"><span data-stu-id="50d01-164">Click **Generate SQL script**.</span></span>

## <a name="deploy-schema"></a><span data-ttu-id="50d01-165">Bereitstellen des Schemas</span><span class="sxs-lookup"><span data-stu-id="50d01-165">Deploy schema</span></span>

1. <span data-ttu-id="50d01-166">Klicken Sie auf **Deploy schema** (Schema bereitstellen).</span><span class="sxs-lookup"><span data-stu-id="50d01-166">Click **Deploy schema**.</span></span>

1. <span data-ttu-id="50d01-167">Sehen Sie sich die Ergebnisse der Schemabereitstellung an.</span><span class="sxs-lookup"><span data-stu-id="50d01-167">Review the results of the schema deployment.</span></span>

## <a name="migrate-data"></a><span data-ttu-id="50d01-168">Migrieren von Daten</span><span class="sxs-lookup"><span data-stu-id="50d01-168">Migrate data</span></span>

1. <span data-ttu-id="50d01-169">Klicken Sie auf **Daten migrieren**, um mit der Datenmigration zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="50d01-169">Click **Migrate data** to start the data migration process.</span></span>

1. <span data-ttu-id="50d01-170">Wählen Sie die Tabellen mit den Daten aus, die Sie migrieren möchten.</span><span class="sxs-lookup"><span data-stu-id="50d01-170">Select the tables with the data you want to migrate.</span></span>

1. <span data-ttu-id="50d01-171">Klicken Sie auf **Datenmigration starten**.</span><span class="sxs-lookup"><span data-stu-id="50d01-171">Click **Start data migration**.</span></span>

<span data-ttu-id="50d01-172">Auf dem letzten Bildschirm wird der allgemeine Status angezeigt.</span><span class="sxs-lookup"><span data-stu-id="50d01-172">The final screen shows the overall status.</span></span>

## <a name="summary"></a><span data-ttu-id="50d01-173">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="50d01-173">Summary</span></span>

<span data-ttu-id="50d01-174">In dieser Einheit haben Sie erfahren, wie Sie eine leere Datenbank für Azure SQL-Datenbank erstellen und eine lokale SQL Server-Datenbank zu dieser neuen Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="50d01-174">In this unit, you created an empty Azure SQL Database and migrated a local SQL Server database to this new database.</span></span>