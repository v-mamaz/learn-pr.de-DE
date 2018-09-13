<span data-ttu-id="af04b-101">Da Sie Ihre Datenbank jetzt geprüft und alle gemeldeten Fehler behoben haben, können Sie die Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="af04b-101">Now that you have assessed your database and fixed any errors reported, you're ready to migrate your database.</span></span> <span data-ttu-id="af04b-102">In dieser Einheit erfahren Sie, wie Sie Ihre SQL-Datenbank zu Azure SQL-Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="af04b-102">In this unit, you will migrate your SQL database to Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="af04b-103">Setup</span><span class="sxs-lookup"><span data-stu-id="af04b-103">Setup</span></span>

<span data-ttu-id="af04b-104">Der erste Schritt ist das Herunterladen der Beispieldaten.</span><span class="sxs-lookup"><span data-stu-id="af04b-104">The first step is to download the sample data.</span></span> <span data-ttu-id="af04b-105">Sie können diese Einrichtung überspringen, wenn Sie die Daten bereits lokal installiert haben.</span><span class="sxs-lookup"><span data-stu-id="af04b-105">You can skip this setup if you already have the data installed locally.</span></span>

1. <span data-ttu-id="af04b-106">Öffnen Sie einen Internetbrowser, und navigieren Sie zu https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span><span class="sxs-lookup"><span data-stu-id="af04b-106">Start an internet browser and navigate to https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="af04b-107">Klicken Sie unter **OLTP downloads** (OLTP-Downloads) auf **AdventureWorks2008R2.bak**.</span><span class="sxs-lookup"><span data-stu-id="af04b-107">In **OLTP downloads**, click **AdventureWorks2008R2.bak**.</span></span>

1. <span data-ttu-id="af04b-108">Stellen Sie **AdventureWorks 2008R2** in Management Studio auf Ihrer Standardinstanz wieder her.</span><span class="sxs-lookup"><span data-stu-id="af04b-108">In Management Studio, restore **AdventureWorks 2008R2** to your default instance.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="af04b-109">Erstellen einer Datenbank für Azure SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="af04b-109">Create an Azure SQL Database</span></span>

1. <span data-ttu-id="af04b-110">Melden Sie sich bei Ihrem Azure-Portal-Konto an.</span><span class="sxs-lookup"><span data-stu-id="af04b-110">Sign in to your Azure portal account.</span></span>

1. <span data-ttu-id="af04b-111">Klicken Sie im Azure-Portal links oben auf **Ressource erstellen**.</span><span class="sxs-lookup"><span data-stu-id="af04b-111">Click **Create a resource** in the upper left-hand corner of the portal.</span></span>

1. <span data-ttu-id="af04b-112">Klicken Sie auf **Datenbanken** > **SQL-Datenbank**.</span><span class="sxs-lookup"><span data-stu-id="af04b-112">Click **Databases** > **SQL Database**.</span></span>

1. <span data-ttu-id="af04b-113">Tragen Sie die folgenden Felder in das SQL-Datenbank-Formular ein:</span><span class="sxs-lookup"><span data-stu-id="af04b-113">Enter the following fields on the SQL Database form:</span></span>

    |<span data-ttu-id="af04b-114">Feld</span><span class="sxs-lookup"><span data-stu-id="af04b-114">Field</span></span>|<span data-ttu-id="af04b-115">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="af04b-115">Description</span></span>|
    |-----|---|
    |<span data-ttu-id="af04b-116">Datenbankname</span><span class="sxs-lookup"><span data-stu-id="af04b-116">Database name</span></span>|<span data-ttu-id="af04b-117">Geben Sie einen Namen für die Datenbank ein.</span><span class="sxs-lookup"><span data-stu-id="af04b-117">Enter a name for your database.</span></span> <span data-ttu-id="af04b-118">Sie können dafür den Namen einer bereits vorhandenen Datenbank, die Sie migrieren möchten, oder einen beliebigen anderen Name auswählen.</span><span class="sxs-lookup"><span data-stu-id="af04b-118">This can be the name of your existing database that you're migrating or any new name of your choice</span></span>|
    |<span data-ttu-id="af04b-119">Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="af04b-119">Resource group</span></span>|<span data-ttu-id="af04b-120">Wählen Sie eine Ressourcengruppe aus, oder geben Sie einen neuen Namen für die Ressourcengruppe ein.</span><span class="sxs-lookup"><span data-stu-id="af04b-120">Select a resource group or enter a new resource group name</span></span>|
    |<span data-ttu-id="af04b-121">Auswählen einer Quelle</span><span class="sxs-lookup"><span data-stu-id="af04b-121">Select source</span></span>|<span data-ttu-id="af04b-122">Klicken Sie auf *Leere Datenbank*.</span><span class="sxs-lookup"><span data-stu-id="af04b-122">Select *Blank database*</span></span>|

1. <span data-ttu-id="af04b-123">Wählen Sie unter **Server** entweder einen bereits vorhandenen Server aus, oder geben Sie einen eindeutigen **Servernamen**, **Anmeldeinformationen für einen Serveradministrator**, ein **Kennwort** (das Sie bestätigen sollten) und einen **Speicherort** an.</span><span class="sxs-lookup"><span data-stu-id="af04b-123">Under **Server**, either select an existing server or, enter a globally unique **Server name**, a **Server admin login**, a **Password** (which you should confirm), and a **Location**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af04b-124">Sie benötigen den Servernamen, die Anmeldeinformationen und das Kennwort, um eine Verbindung für Ihrer Datenbank herzustellen.</span><span class="sxs-lookup"><span data-stu-id="af04b-124">You will use the server name, login name, and password to connect to your database.</span></span>

1. <span data-ttu-id="af04b-125">Klicken Sie auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="af04b-125">Click **Select**.</span></span>

1. <span data-ttu-id="af04b-126">Sie können zwar unter **Tarif** eine Datenbank mit besserer Leistung auswählen, aber für dieses Tutorial sollten Sie die Standarddatenbank verwenden.</span><span class="sxs-lookup"><span data-stu-id="af04b-126">In **Pricing tier**, you can select a database with higher performance, but for this tutorial, select default.</span></span>

1. <span data-ttu-id="af04b-127">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="af04b-127">Click **Create**.</span></span> <span data-ttu-id="af04b-128">Warten Sie, bis die Datenbank bereitgestellt ist, bevor Sie mit dem Tutorial fortfahren.</span><span class="sxs-lookup"><span data-stu-id="af04b-128">Wait until the database has been provisioned before continuing the tutorial.</span></span>

    <span data-ttu-id="af04b-129">Im folgenden Screenshot ist eine mögliche Konfiguration Ihrer neuen SQL-Datenbank dargestellt.</span><span class="sxs-lookup"><span data-stu-id="af04b-129">The following screenshot shows a possible configuration for your new SQL database.</span></span>

    ![Screenshot: Neues SQL-Datenbank-Blatt im Azure-Portal mit einer Beispielkonfiguration.](../media-draft/5-create-azure-sql-db.png)

## <a name="create-a-new-migration-project"></a><span data-ttu-id="af04b-131">Erstellen eines neues Migrationsprojekts</span><span class="sxs-lookup"><span data-stu-id="af04b-131">Create a new migration project</span></span>

1. <span data-ttu-id="af04b-132">Öffnen Sie den **Datenmigrations-Assistenten**.</span><span class="sxs-lookup"><span data-stu-id="af04b-132">Start **Data Migration Assistant**.</span></span>

1. <span data-ttu-id="af04b-133">Klicken Sie auf das Symbol **Neu**, und geben Sie die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="af04b-133">Click the **New** icon, and specify the following options:</span></span>

    - <span data-ttu-id="af04b-134">**Projekttyp:** Klicken Sie auf die Option *Migration*.</span><span class="sxs-lookup"><span data-stu-id="af04b-134">**Project type** - Select  the *Migration* option.</span></span>
    - <span data-ttu-id="af04b-135">**Projektname:** Geben Sie einen Namen für Ihr Projekt ein, den Sie sich gut merken können.</span><span class="sxs-lookup"><span data-stu-id="af04b-135">**Project name** - Enter a memorable name for your project.</span></span>
    - <span data-ttu-id="af04b-136">**Typ des Quellservers:** Klicken Sie auf *SQL Server*.</span><span class="sxs-lookup"><span data-stu-id="af04b-136">**Source server type** - Select *SQL Server*.</span></span>
    - <span data-ttu-id="af04b-137">**Typ des Zielservers:** Klicken Sie auf *Azure SQL-Datenbank*.</span><span class="sxs-lookup"><span data-stu-id="af04b-137">**Target server type** - Select *Azure SQL Database*.</span></span>
    - <span data-ttu-id="af04b-138">**Migrationsumfang:** Klicken Sie auf *Schema and data* (Schema und Daten).</span><span class="sxs-lookup"><span data-stu-id="af04b-138">**Migration scope** - Select *Schema and data*.</span></span>

1. <span data-ttu-id="af04b-139">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="af04b-139">Click **Create**.</span></span>

## <a name="specify-the-source-server-and-database"></a><span data-ttu-id="af04b-140">Angeben des Quellservers und der Datenbank</span><span class="sxs-lookup"><span data-stu-id="af04b-140">Specify the source server and database</span></span>

1. <span data-ttu-id="af04b-141">Geben Sie unter **Connect to source server** (Mit Quellserver verbinden) in das Feld **Servername** den Namen der SQL Server-Quellinstanz ein.</span><span class="sxs-lookup"><span data-stu-id="af04b-141">Under **Connect to source server**, in the **Server name** field, enter the name of the source SQL Server instance.</span></span>

1. <span data-ttu-id="af04b-142">Wählen Sie den **Authentifizierungstyp** aus, der von der SQL Server-Quellinstanz unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="af04b-142">Select the **Authentication type** supported by the source SQL Server instance.</span></span>
    > [!TIP]
    > <span data-ttu-id="af04b-143">Es wird empfohlen, dass Sie unter „Verbindungseigenschaften“ das Kontrollkästchen **Verbindung verschlüsseln** aktivieren, um die Verbindung zu verschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="af04b-143">It is recommended that you select the **Encrypt connection** check box under Connection properties to encrypt the connection.</span></span>

1. <span data-ttu-id="af04b-144">Wählen Sie **Verbinden** aus.</span><span class="sxs-lookup"><span data-stu-id="af04b-144">Select **Connect**.</span></span>

> [!NOTE]
> <span data-ttu-id="af04b-145">Wenn bei der Authentifizierung beim Server ein Fehler auftritt, da Sie mit Ihrer IP-Adresse keine Berechtigung haben, öffnen Sie die SQL Server-Instanz in **Azure Management Studio**, wechseln Sie zu **Firewalls und virtuelle Netzwerke**, und fügen Sie eine Regel hinzu.</span><span class="sxs-lookup"><span data-stu-id="af04b-145">If authentication to the server fails because you do not have permission from your IP address, open the SQL Server instance in **Azure Management Studio**, go to **Firewalls and Virtual Networks** and add a rule.</span></span> <span data-ttu-id="af04b-146">Geben Sie ihr einen beliebigen Namen, z.B. **Azure zulassen**.</span><span class="sxs-lookup"><span data-stu-id="af04b-146">Name it whatever you wish, for example, **Allow Azure**.</span></span> <span data-ttu-id="af04b-147">Richten Sie einen Bereich von IP-Adressen ein, die auf diese Instanz zugreifen dürfen.</span><span class="sxs-lookup"><span data-stu-id="af04b-147">Set up a range of IP addresses that are allowed to access this instance.</span></span> <span data-ttu-id="af04b-148">Der Bereich kann von 0.0.0.0 bis 255.255.255.255 reichen.</span><span class="sxs-lookup"><span data-stu-id="af04b-148">The range can be 0.0.0.0 to 255.255.255.255.</span></span> <span data-ttu-id="af04b-149">Speichern Sie diese neue Regel, und nun sollten Sie auf die Azure SQL Server-Instanz zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="af04b-149">Save this new rule, and you should be able to access the Azure SQL Server instance.</span></span> 

1. <span data-ttu-id="af04b-150">Wählen Sie eine einzelne Quelldatenbank aus, die zu Azure SQL-Datenbank migriert werden soll, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="af04b-150">Select a single source database to migrate to Azure SQL Database and click **Next**.</span></span>

## <a name="specify-the-target-server-and-database"></a><span data-ttu-id="af04b-151">Angeben des Zielservers und der Datenbank</span><span class="sxs-lookup"><span data-stu-id="af04b-151">Specify the target server and database</span></span>

1. <span data-ttu-id="af04b-152">Geben Sie unter **Verbindung mit Zielserver herstellen** in das Feld **Servername** den Namen der Azure SQL-Datenbank-Instanz ein.</span><span class="sxs-lookup"><span data-stu-id="af04b-152">Under **Connect to target server**, in the **Server name** field, enter the name of the Azure SQL Database instance.</span></span> <span data-ttu-id="af04b-153">Fügen Sie **database.windows.net** der Datenbankinstanz hinzu.</span><span class="sxs-lookup"><span data-stu-id="af04b-153">Add **.database.windows.net** to the database instance.</span></span>

1. <span data-ttu-id="af04b-154">Wählen Sie den Authentifizierungstyp aus, der von der Azure SQL-Datenbank-Zielinstanz unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="af04b-154">Select the Authentication type supported by the target Azure SQL Database instance.</span></span> <span data-ttu-id="af04b-155">Klicken Sie für dieses Tutorial auf **SQL Server-Authentifizierung**.</span><span class="sxs-lookup"><span data-stu-id="af04b-155">For this tutorial, select **SQL Server Authentication**.</span></span>
    > [!TIP]
    > <span data-ttu-id="af04b-156">Es wird empfohlen, dass Sie unter „Verbindungseigenschaften“ das Kontrollkästchen **Verbindung verschlüsseln** aktivieren, um die Verbindung zu verschlüsseln.</span><span class="sxs-lookup"><span data-stu-id="af04b-156">It is recommended that you select the **Encrypt connection** check box under Connection properties to encrypt the connection.</span></span>

1. <span data-ttu-id="af04b-157">Geben Sie den **Benutzernamen** und das **Kennwort** ein, das Sie beim Erstellen der Datenbank für Azure SQL-Datenbank angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="af04b-157">Enter the **Username** and **Password** that you defined when you created the Azure SQL Database.</span></span>

1. <span data-ttu-id="af04b-158">Klicken Sie auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="af04b-158">Click **Connect**.</span></span>

1. <span data-ttu-id="af04b-159">Wählen Sie eine Zieldatenbank aus, zu der migriert werden soll.</span><span class="sxs-lookup"><span data-stu-id="af04b-159">Select a single target database to which to migrate.</span></span>
    > <span data-ttu-id="af04b-160">[HINWEIS] Wenn Sie Windows-Benutzer migrieren möchten, prüfen Sie im Feld **Name der externen Zielbenutzerdomäne**, ob der Name der externen Zielbenutzerdomäne richtig angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="af04b-160">[NOTE] If you intend to migrate Windows users, in the **Target external user domain name** field, make sure that the target external user domain name is specified correctly.</span></span>

1. <span data-ttu-id="af04b-161">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="af04b-161">Click **Next**.</span></span>

## <a name="select-schema-objects"></a><span data-ttu-id="af04b-162">Auswählen von Schemaobjekten</span><span class="sxs-lookup"><span data-stu-id="af04b-162">Select schema objects</span></span>

1. <span data-ttu-id="af04b-163">Wählen Sie die Schemaobjekte aus der Quelldatenbank aus , die Sie zu Azure SQL-Datenbank migrieren möchten.</span><span class="sxs-lookup"><span data-stu-id="af04b-163">Select the schema objects from the source database that you want to migrate to Azure SQL Database.</span></span>

    > [!NOTE]
    > <span data-ttu-id="af04b-164">Für die Objekte, an denen Änderungen vorgenommen werden müssen, damit sie migriert werden können, gibt es automatische Möglichkeiten zur Problembehandlung.</span><span class="sxs-lookup"><span data-stu-id="af04b-164">Some of the objects that cannot be converted as-is are presented with automatic fix opportunities.</span></span> <span data-ttu-id="af04b-165">Wenn Sie im linken Bereich auf diese Objekte klicken, werden die vorgeschlagenen Möglichkeiten zur Fehlerbehebung auf der rechten Seite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="af04b-165">Clicking these objects on the left pane displays the suggested fixes on the right pane.</span></span> <span data-ttu-id="af04b-166">Prüfen Sie diese, und entscheiden Sie für jedes Objekt, ob Sie alle Änderungen akzeptieren oder ignorieren möchten.</span><span class="sxs-lookup"><span data-stu-id="af04b-166">Review the fixes and choose to either apply or ignore all changes, object by object.</span></span> <span data-ttu-id="af04b-167">Beachten Sie, dass es keine Auswirkungen auf Änderungen anderer Datenbankobjekte hat, wenn Sie alle Änderungen annehmen oder ignorieren.</span><span class="sxs-lookup"><span data-stu-id="af04b-167">Note that applying or ignoring all changes for one object does not affect changes to other database objects.</span></span> <span data-ttu-id="af04b-168">Anweisungen, die nicht konvertiert oder automatisch verbessert werden können, werden in der Zieldatenbank reproduziert und mit einem Kommentar versehen.</span><span class="sxs-lookup"><span data-stu-id="af04b-168">Statements that cannot be converted or automatically fixed are reproduced to the target database and commented.</span></span>

    ![Screenshot: Datenmigrations-Assistent, in dem eine Liste mit Migrationsproblemen angezeigt wird, die Auswirkungen auf AdventureWorks-SQL-Server-Daten haben, für die das Problem "Stored Procedure: dbo.uspSearchCandidateResumes" (Gespeicherte Prozedur: dbo.uspSearchCandidateResumes) und die Fehlerdetails angezeigt werden.](../media-draft/5-suggested-fix.png)

1. <span data-ttu-id="af04b-170">Klicken Sie **SQL-Skript generieren**.</span><span class="sxs-lookup"><span data-stu-id="af04b-170">Click **Generate SQL script**.</span></span>

## <a name="deploy-schema"></a><span data-ttu-id="af04b-171">Bereitstellen des Schemas</span><span class="sxs-lookup"><span data-stu-id="af04b-171">Deploy schema</span></span>

1. <span data-ttu-id="af04b-172">Klicken Sie auf **Deploy schema** (Schema bereitstellen).</span><span class="sxs-lookup"><span data-stu-id="af04b-172">Click **Deploy schema**.</span></span>

1. <span data-ttu-id="af04b-173">Sehen Sie sich die Ergebnisse der Schemabereitstellung an.</span><span class="sxs-lookup"><span data-stu-id="af04b-173">Review the results of the schema deployment.</span></span>

## <a name="migrate-data"></a><span data-ttu-id="af04b-174">Migrieren von Daten</span><span class="sxs-lookup"><span data-stu-id="af04b-174">Migrate data</span></span>

1. <span data-ttu-id="af04b-175">Klicken Sie auf **Daten migrieren**, um mit der Datenmigration zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="af04b-175">Click **Migrate data** to start the data migration process.</span></span>

1. <span data-ttu-id="af04b-176">Wählen Sie die Tabellen mit den Daten aus, die Sie migrieren möchten.</span><span class="sxs-lookup"><span data-stu-id="af04b-176">Select the tables with the data you want to migrate.</span></span>

1. <span data-ttu-id="af04b-177">Klicken Sie auf **Datenmigration starten**.</span><span class="sxs-lookup"><span data-stu-id="af04b-177">Click **Start data migration**.</span></span>

<span data-ttu-id="af04b-178">Auf dem letzten Bildschirm wird der allgemeine Status angezeigt.</span><span class="sxs-lookup"><span data-stu-id="af04b-178">The final screen shows the overall status.</span></span>

## <a name="summary"></a><span data-ttu-id="af04b-179">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="af04b-179">Summary</span></span>

<span data-ttu-id="af04b-180">In dieser Einheit haben Sie erfahren, wie Sie eine leere Datenbank für Azure SQL-Datenbank erstellen und eine lokale SQL Server-Datenbank zu dieser neuen Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="af04b-180">In this unit, you created an empty Azure SQL Database and migrated a local SQL Server database to this new database.</span></span>