<span data-ttu-id="3f43c-101">In dieser Übung bewerten Sie eine vorhandene Datenbank mithilfe des Datenmigrations-Assistenten und überprüfen alle Features, die in der lokalen SQL Server-Instanz verwendet und derzeit nicht von Azure SQL-Datenbank unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="3f43c-101">In this exercise, you'll assess an existing database using the Data Migration Assistant and review any features used in the local SQL Server instance that aren't currently supported by Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="3f43c-102">Setup</span><span class="sxs-lookup"><span data-stu-id="3f43c-102">Setup</span></span>

1. <span data-ttu-id="3f43c-103">[Installieren Sie den **Datenmigrations-Assistenten**](https://www.microsoft.com/download/details.aspx?id=53595), wenn Sie dies noch nicht getan haben.</span><span class="sxs-lookup"><span data-stu-id="3f43c-103">[Install the **Data Migration Assistant**](https://www.microsoft.com/download/details.aspx?id=53595) if you haven't done so already.</span></span>

1. <span data-ttu-id="3f43c-104">Dazu muss eine SQL Server-Instanz ausgeführt werden. Außerdem müssen Sie die Verbindungsdetails zur Hand haben.</span><span class="sxs-lookup"><span data-stu-id="3f43c-104">You'll need a SQL Server instance running, ensure you have connection details available.</span></span>
1. <span data-ttu-id="3f43c-105">[\*\*\* wahrscheinlich durch eine LOD-VM ersetzen \*\*\*] <!-- TODO: --></span><span class="sxs-lookup"><span data-stu-id="3f43c-105">[\*\*\*\* likely replace with an LOD VM \*\*\*\*\*] <!-- TODO: --></span></span>

1. <span data-ttu-id="3f43c-106">Öffnen Sie einen Internetbrowser, und navigieren Sie zu https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span><span class="sxs-lookup"><span data-stu-id="3f43c-106">Start an Internet browser and navigate to https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="3f43c-107">Klicken Sie unter **OLTP downloads** (OLTP-Downloads) auf **AdventureWorks2008R2.bak**, und speichern Sie die Datei auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="3f43c-107">In **OLTP downloads**, click **AdventureWorks2008R2.bak** and save it to your local machine.</span></span>

1. <span data-ttu-id="3f43c-108">Stellen Sie *AdventureWorks 2008R2* in Management Studio auf Ihrer Standardinstanz wieder her.</span><span class="sxs-lookup"><span data-stu-id="3f43c-108">In Management Studio, restore *AdventureWorks 2008R2* to your default instance.</span></span>

## <a name="create-an-assessment"></a><span data-ttu-id="3f43c-109">Erstellen einer Bewertung</span><span class="sxs-lookup"><span data-stu-id="3f43c-109">Create an assessment</span></span>

1. <span data-ttu-id="3f43c-110">Starten Sie **Microsoft-Datenmigrations-Assistent**.</span><span class="sxs-lookup"><span data-stu-id="3f43c-110">Start the **Microsoft Data Migration Assistant**.</span></span>

1. <span data-ttu-id="3f43c-111">Klicken Sie im linken Navigationsbereich der App auf __+__, um ein neues Datenmigrations-Assistent-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="3f43c-111">In the app's left-hand navigation, click __+__ to create a new Data Migration Assistant project.</span></span>

1. <span data-ttu-id="3f43c-112">Geben Sie die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="3f43c-112">Specify the following options:</span></span>
    - <span data-ttu-id="3f43c-113">**Projekttyp:** Wählen Sie *Bewertung* aus.</span><span class="sxs-lookup"><span data-stu-id="3f43c-113">**Project type** - Select *Assessment*</span></span>
    - <span data-ttu-id="3f43c-114">**Projektname:** Geben Sie einen Namen für Ihr Projekt ein, z.B. „FahrradDB-Bewertung“.</span><span class="sxs-lookup"><span data-stu-id="3f43c-114">**Project name** - Enter a name for your project - for example, "Bicycle DB Assessment"</span></span>
    - <span data-ttu-id="3f43c-115">**Typ des Quellservers:** Wählen Sie *SQL Server* aus.</span><span class="sxs-lookup"><span data-stu-id="3f43c-115">**Source server type** - Select *SQL Server*</span></span>
    - <span data-ttu-id="3f43c-116">**Typ des Zielservers:** Wählen Sie *Azure SQL-Datenbank*.</span><span class="sxs-lookup"><span data-stu-id="3f43c-116">**Target server type** - Select *Azure SQL Database*</span></span>

1. <span data-ttu-id="3f43c-117">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="3f43c-117">Click **Create**.</span></span>
    <span data-ttu-id="3f43c-118">![Screenshot der beschriebenen Konfiguration im Datenmigrations-Assistent für Ihre AdventureWorks-SQL Server-Daten](../media-draft/3-create-assessment.png)</span><span class="sxs-lookup"><span data-stu-id="3f43c-118">![Screenshot showing the described configuration in the Data Migration Assistant for your AdventureWorks SQL Server data.](../media-draft/3-create-assessment.png)</span></span>

1. <span data-ttu-id="3f43c-119">Wählen Sie den Typ des Bewertungsberichts aus, und überprüfen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="3f43c-119">Select the assessment report type - check both:</span></span>
    - <span data-ttu-id="3f43c-120">Datenbankkompatibilität überprüfen</span><span class="sxs-lookup"><span data-stu-id="3f43c-120">Check database compatibility</span></span>
    - <span data-ttu-id="3f43c-121">Check feature parity (Featureparität prüfen)</span><span class="sxs-lookup"><span data-stu-id="3f43c-121">Check feature parity</span></span>

1. <span data-ttu-id="3f43c-122">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="3f43c-122">Click **Next**.</span></span>

## <a name="add-databases-to-assess"></a><span data-ttu-id="3f43c-123">Auswählen zu bewertender Datenbanken</span><span class="sxs-lookup"><span data-stu-id="3f43c-123">Add databases to assess</span></span>

1. <span data-ttu-id="3f43c-124">Klicken Sie auf **Quellen hinzufügen**, um das Verbindungsmenü zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="3f43c-124">Click **Add Sources** to open the connection menu.</span></span>
2. <span data-ttu-id="3f43c-125">Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="3f43c-125">Do the following:</span></span>
    - <span data-ttu-id="3f43c-126">Geben Sie den Namen Ihrer vorhandenen SQL Server-Instanz ein.</span><span class="sxs-lookup"><span data-stu-id="3f43c-126">Enter your existing SQL server instance name</span></span>
    - <span data-ttu-id="3f43c-127">Wählen Sie den **Authentifizierungstyp** aus.</span><span class="sxs-lookup"><span data-stu-id="3f43c-127">Select the **Authentication** type</span></span>
    - <span data-ttu-id="3f43c-128">Geben Sie die Verbindungseigenschaften für Ihren Server ein.</span><span class="sxs-lookup"><span data-stu-id="3f43c-128">Specify the connection properties for your server</span></span>
3. <span data-ttu-id="3f43c-129">Klicken Sie auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="3f43c-129">CLick **Connect**.</span></span>
4. <span data-ttu-id="3f43c-130">Wählen Sie unter **Quellen hinzufügen** die Datenbanken aus, die bewertet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3f43c-130">In **Add sources**, select the databases to assess.</span></span> <span data-ttu-id="3f43c-131">Wählen Sie für diese Übung **AdventureWorks2008R2** aus.</span><span class="sxs-lookup"><span data-stu-id="3f43c-131">For this exercise, select **AdventureWorks2008R2**.</span></span>
5. <span data-ttu-id="3f43c-132">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="3f43c-132">Click **Add**.</span></span>
    > [!NOTE]
    > <span data-ttu-id="3f43c-133">Verwenden Sie zum Hinzufügen von Datenbanken aus mehreren SQL Server-Instanzen die Schaltfläche **Quellen hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="3f43c-133">To add databases from multiple SQL Server instances, use the **Add Sources** button.</span></span> <span data-ttu-id="3f43c-134">Wenn Sie mehrere Datenbanken entfernen möchten, drücken Sie UMSCHALT+STRG, um die zu entfernenden Datenbanken auszuwählen, und klicken Sie dann auf **Quellen entfernen**.</span><span class="sxs-lookup"><span data-stu-id="3f43c-134">To remove multiple databases, hold the SHIFT+CTRL keys to select the databases you want to remove, then click **Remove Sources**.</span></span>

6. <span data-ttu-id="3f43c-135">Klicken Sie auf **Bewertung starten**.</span><span class="sxs-lookup"><span data-stu-id="3f43c-135">Click **Start Assessment**.</span></span>

## <a name="view-results"></a><span data-ttu-id="3f43c-136">Anzeigen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="3f43c-136">View results</span></span>

<span data-ttu-id="3f43c-137">Wenn mehrere Datenbanken vorhanden sind, werden die Ergebnisse der einzelnen Datenbanken angezeigt, sobald diese verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="3f43c-137">If there are multiple databases, the results for each database appears as soon as it is available.</span></span> <span data-ttu-id="3f43c-138">Sie müssen nicht warten, bis alle Datenbankbewertungen abgeschlossen wurden.</span><span class="sxs-lookup"><span data-stu-id="3f43c-138">You don't need to wait for all database assessments to complete.</span></span>

1. <span data-ttu-id="3f43c-139">Nachdem die Bewertung für **AdventureWorks** abgeschlossen wurde, klicken Sie auf **Compatibility issues** (Kompatibilitätsprobleme) und **Featureempfehlungen**, um die Ergebnisse anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="3f43c-139">Once the assessment for **AdventureWorks** is complete, click **Compatibility issues** and **Feature recommendations** to view the results.</span></span>
    - <span data-ttu-id="3f43c-140">Die Kategorie „SQL Server-Featureparität“ enthält Features, die möglicherweise nicht vollständig unterstützt werden, und Schritte, um diese Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="3f43c-140">The SQL Server feature parity category lists features that might not be fully supported and steps to remedy these issues.</span></span> <span data-ttu-id="3f43c-141">Migrationen werden jedoch aufgrund von Problemen mit der Featureparität nicht beendet.</span><span class="sxs-lookup"><span data-stu-id="3f43c-141">Feature parity issues will not stop a migration.</span></span>
    - <span data-ttu-id="3f43c-142">Die Kategorie „Kompatibilitätsprobleme“ enthält Features, die eine Migration beenden würden, und Schritte, um diese Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="3f43c-142">The Compatibility issues category lists features that would block a migration and steps to remedy these issues.</span></span>

## <a name="summary"></a><span data-ttu-id="3f43c-143">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="3f43c-143">Summary</span></span>

<span data-ttu-id="3f43c-144">In dieser Übung haben Sie eine lokal installierte SQL Server-Datenbank bewertet, um zu überprüfen, ob Features nicht verfügbar wären, wenn Sie die Datenbank zu Azure SQL-Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="3f43c-144">In this exercise, you assessed a locally installed SQL Server database to verify if any features would be unavailable when you migrate the database to Azure SQL Database.</span></span>