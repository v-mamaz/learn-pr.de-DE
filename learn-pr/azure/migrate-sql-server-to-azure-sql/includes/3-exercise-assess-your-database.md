<span data-ttu-id="618aa-101">In dieser Einheit bewerten Sie eine vorhandene Datenbank mithilfe des Datenmigrations-Assistenten und überprüfen alle Funktionen, die in der lokalen SQL Server-Instanz verwendet und derzeit nicht von Azure SQL-Datenbank unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="618aa-101">In this unit, you'll assess an existing database using the Data Migration Assistant and review any features used in the local SQL Server instance that aren't currently supported by Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="618aa-102">Einrichtung</span><span class="sxs-lookup"><span data-stu-id="618aa-102">Setup</span></span>

1. <span data-ttu-id="618aa-103">[Installieren Sie den **Datenmigrations-Assistenten**](https://www.microsoft.com/download/details.aspx?id=53595), wenn Sie dies noch nicht getan haben.</span><span class="sxs-lookup"><span data-stu-id="618aa-103">[Install the **Data Migration Assistant**](https://www.microsoft.com/download/details.aspx?id=53595) if you haven't done so already.</span></span>

1. <span data-ttu-id="618aa-104">Dazu muss eine SQL Server-Instanz ausgeführt werden. Außerdem müssen Sie die Verbindungsdetails zur Hand haben.</span><span class="sxs-lookup"><span data-stu-id="618aa-104">You'll need a SQL Server instance running, ensure you have connection details available.</span></span>

<!-- TODO: replace with an LOD VM -->

1. <span data-ttu-id="618aa-105">Öffnen Sie einen Browser, und navigieren Sie zu https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span><span class="sxs-lookup"><span data-stu-id="618aa-105">Open a browser and navigate to https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="618aa-106">Klicken Sie unter **OLTP downloads** (OLTP-Downloads) auf **AdventureWorks2008R2.bak**, und speichern Sie die Datei auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="618aa-106">In **OLTP downloads**, click **AdventureWorks2008R2.bak** and save it to your local machine.</span></span>

1. <span data-ttu-id="618aa-107">Stellen Sie *AdventureWorks 2008R2* in Management Studio auf Ihrer Standardinstanz wieder her.</span><span class="sxs-lookup"><span data-stu-id="618aa-107">In Management Studio, restore *AdventureWorks 2008R2* to your default instance.</span></span>

## <a name="create-an-assessment"></a><span data-ttu-id="618aa-108">Erstellen einer Bewertung</span><span class="sxs-lookup"><span data-stu-id="618aa-108">Create an assessment</span></span>

1. <span data-ttu-id="618aa-109">Starten Sie **Microsoft-Datenmigrations-Assistent**.</span><span class="sxs-lookup"><span data-stu-id="618aa-109">Start the **Microsoft Data Migration Assistant**.</span></span>

1. <span data-ttu-id="618aa-110">Klicken Sie im linken Navigationsbereich der App auf __+__, um ein neues Datenmigrations-Assistent-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="618aa-110">In the app's left-hand navigation, click __+__ to create a new Data Migration Assistant project.</span></span>

1. <span data-ttu-id="618aa-111">Geben Sie die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="618aa-111">Specify the following options:</span></span>

    - <span data-ttu-id="618aa-112">**Projekttyp:** Wählen Sie *Bewertung* aus.</span><span class="sxs-lookup"><span data-stu-id="618aa-112">**Project type** - Select *Assessment*</span></span>
    - <span data-ttu-id="618aa-113">**Projektname:** Geben Sie einen Namen für Ihr Projekt ein, z.B. „FahrradDB-Bewertung“.</span><span class="sxs-lookup"><span data-stu-id="618aa-113">**Project name** - Enter a name for your project - for example, "Bicycle DB Assessment"</span></span>
    - <span data-ttu-id="618aa-114">**Typ des Quellservers:** Wählen Sie *SQL Server* aus.</span><span class="sxs-lookup"><span data-stu-id="618aa-114">**Source server type** - Select *SQL Server*</span></span>
    - <span data-ttu-id="618aa-115">**Typ des Zielservers:** Wählen Sie *Azure SQL-Datenbank*.</span><span class="sxs-lookup"><span data-stu-id="618aa-115">**Target server type** - Select *Azure SQL Database*</span></span>

1. <span data-ttu-id="618aa-116">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="618aa-116">Click **Create**.</span></span>
    <span data-ttu-id="618aa-117">![Screenshot der beschriebenen Konfiguration im Datenmigrations-Assistent für Ihre AdventureWorks-SQL Server-Daten](../media-draft/3-create-assessment.png)</span><span class="sxs-lookup"><span data-stu-id="618aa-117">![Screenshot showing the described configuration in the Data Migration Assistant for your AdventureWorks SQL Server data.](../media-draft/3-create-assessment.png)</span></span>

1. <span data-ttu-id="618aa-118">Wählen Sie den Typ des Bewertungsberichts aus, und überprüfen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="618aa-118">Select the assessment report type - check both:</span></span>
    - <span data-ttu-id="618aa-119">Datenbankkompatibilität überprüfen</span><span class="sxs-lookup"><span data-stu-id="618aa-119">Check database compatibility</span></span>
    - <span data-ttu-id="618aa-120">Check feature parity (Featureparität prüfen)</span><span class="sxs-lookup"><span data-stu-id="618aa-120">Check feature parity</span></span>

1. <span data-ttu-id="618aa-121">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="618aa-121">Click **Next**.</span></span>

## <a name="add-databases-to-assess"></a><span data-ttu-id="618aa-122">Hinzufügen zu bewertender Datenbanken</span><span class="sxs-lookup"><span data-stu-id="618aa-122">Add databases to assess</span></span>

1. <span data-ttu-id="618aa-123">Wenn **Verbindung mit einem Server herstellen** nicht auf der rechten Seite angezeigt wird, klicken Sie auf **Quellen hinzufügen**, um das Verbindungsmenü zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="618aa-123">If **Connect to a Server** is not showing on the right-hand side, click **Add Sources** to open the connection menu.</span></span>

1. <span data-ttu-id="618aa-124">Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="618aa-124">Do the following:</span></span>
    - <span data-ttu-id="618aa-125">Geben Sie den Namen Ihrer vorhandenen SQL Server-Instanz ein.</span><span class="sxs-lookup"><span data-stu-id="618aa-125">Enter your existing SQL server instance name</span></span>
    - <span data-ttu-id="618aa-126">Wählen Sie den **Authentifizierungstyp** aus.</span><span class="sxs-lookup"><span data-stu-id="618aa-126">Select the **Authentication** type</span></span>
    - <span data-ttu-id="618aa-127">Geben Sie die Verbindungseigenschaften für Ihren Server ein.</span><span class="sxs-lookup"><span data-stu-id="618aa-127">Specify the connection properties for your server</span></span>

1. <span data-ttu-id="618aa-128">Klicken Sie auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="618aa-128">Click **Connect**.</span></span>

1. <span data-ttu-id="618aa-129">Wählen Sie unter **Quellen hinzufügen** die Datenbanken aus, die bewertet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="618aa-129">In **Add sources**, select the databases to assess.</span></span> <span data-ttu-id="618aa-130">Wählen Sie für diese Übung **AdventureWorks2008R2** aus.</span><span class="sxs-lookup"><span data-stu-id="618aa-130">For this exercise, select **AdventureWorks2008R2**.</span></span>

1. <span data-ttu-id="618aa-131">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="618aa-131">Click **Add**.</span></span>
    > [!NOTE]
    > <span data-ttu-id="618aa-132">Verwenden Sie zum Hinzufügen von Datenbanken aus mehreren SQL Server-Instanzen die Schaltfläche **Quellen hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="618aa-132">To add databases from multiple SQL Server instances, use the **Add Sources** button.</span></span> <span data-ttu-id="618aa-133">Wenn Sie mehrere Datenbanken entfernen möchten, drücken Sie UMSCHALT+STRG, um die zu entfernenden Datenbanken auszuwählen, und klicken Sie dann auf **Quellen entfernen**.</span><span class="sxs-lookup"><span data-stu-id="618aa-133">To remove multiple databases, hold the SHIFT+CTRL keys to select the databases you want to remove, then click **Remove Sources**.</span></span>

1. <span data-ttu-id="618aa-134">Klicken Sie auf **Bewertung starten**.</span><span class="sxs-lookup"><span data-stu-id="618aa-134">Click **Start Assessment**.</span></span>

## <a name="view-results"></a><span data-ttu-id="618aa-135">Anzeigen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="618aa-135">View results</span></span>

<span data-ttu-id="618aa-136">Wenn mehrere Datenbanken vorhanden sind, werden die Ergebnisse der einzelnen Datenbanken angezeigt, sobald diese verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="618aa-136">If there are multiple databases, the results for each database appears as soon as it is available.</span></span> <span data-ttu-id="618aa-137">Sie müssen nicht warten, bis alle Datenbankbewertungen abgeschlossen wurden.</span><span class="sxs-lookup"><span data-stu-id="618aa-137">You don't need to wait for all database assessments to complete.</span></span>

1. <span data-ttu-id="618aa-138">Nachdem die Bewertung für **AdventureWorks** abgeschlossen wurde, klicken Sie auf **Compatibility issues** (Kompatibilitätsprobleme,) und aktivieren Sie die Optionsfelder neben **SQL Server-Featureparität**, um die Ergebnisse anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="618aa-138">Once the assessment for **AdventureWorks** is complete, click\*\* Compatibility issues\*\* and **SQL Server feature parity** radio buttons to view the results.</span></span>
    - <span data-ttu-id="618aa-139">Die Kategorie „SQL Server-Featureparität“ enthält Features, die möglicherweise nicht vollständig unterstützt werden, und Schritte, um diese Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="618aa-139">The SQL Server feature parity category lists features that might not be fully supported and steps to remedy these issues.</span></span> <span data-ttu-id="618aa-140">Migrationen werden jedoch aufgrund von Problemen mit der Featureparität nicht beendet.</span><span class="sxs-lookup"><span data-stu-id="618aa-140">Feature parity issues will not stop a migration.</span></span>
    - <span data-ttu-id="618aa-141">Die Kategorie „Kompatibilitätsprobleme“ enthält Features, die eine Migration beenden würden, und Schritte, um diese Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="618aa-141">The Compatibility issues category lists features that would block a migration and steps to remedy these issues.</span></span>

## <a name="summary"></a><span data-ttu-id="618aa-142">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="618aa-142">Summary</span></span>

<span data-ttu-id="618aa-143">In dieser Einheit haben Sie eine lokal installierte SQL Server-Datenbank bewertet, um zu überprüfen, ob Features nicht verfügbar wären, wenn Sie die Datenbank zu Azure SQL-Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="618aa-143">In this unit, you assessed a locally installed SQL Server database to verify if any features would be unavailable when you migrate the database to Azure SQL Database.</span></span>