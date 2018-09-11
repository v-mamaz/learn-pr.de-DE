<span data-ttu-id="f0a12-101">In dieser Übung bewerten Sie eine vorhandene Datenbank mithilfe des Datenmigrations-Assistenten und überprüfen alle Features, die in der lokalen SQL Server-Instanz verwendet und derzeit nicht von Azure SQL-Datenbank unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="f0a12-101">In this exercise, you'll assess an existing database using Data Migration Assistant and review any features used in the local SQL Server instance that aren't currently supported in by Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="f0a12-102">Setup</span><span class="sxs-lookup"><span data-stu-id="f0a12-102">Setup</span></span>

1. <span data-ttu-id="f0a12-103">[Installieren Sie den **Datenmigrations-Assistent**](https://www.microsoft.com/en-us/download/details.aspx?id=53595), wenn Sie dies noch nicht getan haben.</span><span class="sxs-lookup"><span data-stu-id="f0a12-103">[Install the **Data Migration Assistant**](https://www.microsoft.com/en-us/download/details.aspx?id=53595) if you haven't done so already.</span></span>

1. <span data-ttu-id="f0a12-104">Dazu muss eine SQL Server-Instanz ausgeführt werden. Außerdem müssen Sie die Verbindungsdetails zur Hand haben.</span><span class="sxs-lookup"><span data-stu-id="f0a12-104">You'll need a SQL Server instance running, ensure you have connection details available.</span></span>
1. <span data-ttu-id="f0a12-105">[\*\*\* wahrscheinlich durch eine LOD-VM ersetzen \*\*\*] <!-- TODO: --></span><span class="sxs-lookup"><span data-stu-id="f0a12-105">[\*\*\*\* likely replace with an LOD VM \*\*\*\*\*] <!-- TODO: --></span></span>

1. <span data-ttu-id="f0a12-106">Öffnen Sie einen Internetbrowser, und navigieren Sie zu https://docs.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span><span class="sxs-lookup"><span data-stu-id="f0a12-106">Start an Internet browser and navigate to https://docs.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="f0a12-107">Klicken Sie unter **OLTP downloads** (OLTP-Downloads) auf **AdventureWorks2008R2.bak**, und speichern Sie die Datei auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="f0a12-107">In **OLTP downloads**, click **AdventureWorks2008R2.bak** and save it to your local machine.</span></span>

1. <span data-ttu-id="f0a12-108">Stellen Sie *AdventureWorks 2008R2* in Management Studio auf Ihrer Standardinstanz wieder her.</span><span class="sxs-lookup"><span data-stu-id="f0a12-108">In Management Studio, restore *AdventureWorks 2008R2* to your default instance.</span></span>

## <a name="create-an-assessment"></a><span data-ttu-id="f0a12-109">Erstellen einer Bewertung</span><span class="sxs-lookup"><span data-stu-id="f0a12-109">Create an assessment</span></span>

1. <span data-ttu-id="f0a12-110">Starten Sie den **Microsoft-Datenmigrations-Assistenten**.</span><span class="sxs-lookup"><span data-stu-id="f0a12-110">Start the **Microsoft Data Migration Assistant**.</span></span>

1. <span data-ttu-id="f0a12-111">Klicken Sie im linken Navigationsbereich der App auf __+__, um ein neues DMA-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="f0a12-111">In the app's left-hand navigation, click __+__ to create a new DMA project.</span></span>

1. <span data-ttu-id="f0a12-112">Geben Sie die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="f0a12-112">Specify the following options:</span></span>
    - <span data-ttu-id="f0a12-113">**Projekttyp:** Wählen Sie *Bewertung* aus.</span><span class="sxs-lookup"><span data-stu-id="f0a12-113">**Project type** - Select *Assessment*</span></span>
    - <span data-ttu-id="f0a12-114">**Projektname:** Geben Sie einen Namen für Ihr Projekt ein, z.B. „FahrradDB-Bewertung“.</span><span class="sxs-lookup"><span data-stu-id="f0a12-114">**Project name** - Enter a name for your project - for example "Bicycle DB Assessment"</span></span>
    - <span data-ttu-id="f0a12-115">**Typ des Quellservers:** Wählen Sie *SQL Server* aus.</span><span class="sxs-lookup"><span data-stu-id="f0a12-115">**Source server type** - Select *SQL Server*</span></span>
    - <span data-ttu-id="f0a12-116">**Typ des Zielservers:** Wählen Sie *Azure SQL-Datenbank*.</span><span class="sxs-lookup"><span data-stu-id="f0a12-116">**Target server type** - Select *Azure SQL Database*</span></span>

1. <span data-ttu-id="f0a12-117">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="f0a12-117">Click **Create**.</span></span>
    <span data-ttu-id="f0a12-118">![Screenshot der beschriebenen Konfiguration im Datenmigrations-Assistent für Ihre AdventureWorks-SQL Server-Daten](../media-draft/3-create-assessment.png)</span><span class="sxs-lookup"><span data-stu-id="f0a12-118">![Screenshot showing the described configuration in the Data Migration Assistant for your AdventureWorks SQL Server data.](../media-draft/3-create-assessment.png)</span></span>

1. <span data-ttu-id="f0a12-119">Wählen Sie den Typ des Bewertungsberichts aus, und überprüfen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="f0a12-119">Select the assessment report type - check both:</span></span>
    - <span data-ttu-id="f0a12-120">Datenbankkompatibilität überprüfen</span><span class="sxs-lookup"><span data-stu-id="f0a12-120">Check database compatibility</span></span>
    - <span data-ttu-id="f0a12-121">Check feature parity (Featureparität prüfen)</span><span class="sxs-lookup"><span data-stu-id="f0a12-121">Check feature parity</span></span>

1. <span data-ttu-id="f0a12-122">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="f0a12-122">Click **Next**.</span></span>

## <a name="add-databases-to-assess"></a><span data-ttu-id="f0a12-123">Auswählen zu bewertender Datenbanken</span><span class="sxs-lookup"><span data-stu-id="f0a12-123">Add databases to assess</span></span>

1. <span data-ttu-id="f0a12-124">Klicken Sie auf **Quellen hinzufügen**, um das Verbindungsmenü zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="f0a12-124">Click **Add Sources** to open the connection menu.</span></span>
2. <span data-ttu-id="f0a12-125">Geben Sie die folgenden Informationen ein:</span><span class="sxs-lookup"><span data-stu-id="f0a12-125">Enter the following information</span></span>
    - <span data-ttu-id="f0a12-126">Geben Sie den Namen Ihrer vorhandenen SQL Server-Instanz ein.</span><span class="sxs-lookup"><span data-stu-id="f0a12-126">Enter your existing SQL server instance name</span></span>
    - <span data-ttu-id="f0a12-127">Wählen Sie den **Authentifizierungstyp** aus.</span><span class="sxs-lookup"><span data-stu-id="f0a12-127">Select the **Authentication** type</span></span>
    - <span data-ttu-id="f0a12-128">Geben Sie die Verbindungseigenschaften für Ihren Server ein.</span><span class="sxs-lookup"><span data-stu-id="f0a12-128">Specify the connection properties for your server</span></span>
3. <span data-ttu-id="f0a12-129">Klicken Sie auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="f0a12-129">CLick **Connect**.</span></span>
4. <span data-ttu-id="f0a12-130">Wählen Sie unter **Quellen hinzufügen** die Datenbanken aus, die bewertet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="f0a12-130">In **Add sources**, select the databases to assess.</span></span> <span data-ttu-id="f0a12-131">Wählen Sie für diese Übung **AdventureWorks2008R2** aus.</span><span class="sxs-lookup"><span data-stu-id="f0a12-131">For this exercise, select **AdventureWorks2008R2**.</span></span>
5. <span data-ttu-id="f0a12-132">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="f0a12-132">Click **Add**.</span></span>
    > [!NOTE]
    > <span data-ttu-id="f0a12-133">Verwenden Sie zum Hinzufügen von Datenbanken aus mehreren SQL Server-Instanzen die Schaltfläche **Quellen hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="f0a12-133">To add databases from multiple SQL Server instances, use the **Add Sources** button.</span></span> <span data-ttu-id="f0a12-134">Wenn Sie mehrere Datenbanken entfernen möchten, drücken Sie UMSCHALT+STRG, wählen Sie die zu entfernenden Datenbanken aus, und klicken Sie auf **Quellen entfernen**.</span><span class="sxs-lookup"><span data-stu-id="f0a12-134">To remove multiple databases, hold the SHIFT+CTRL keys and select the databases to remove then click **Remove Sources**.</span></span>

6. <span data-ttu-id="f0a12-135">Klicken Sie auf **Bewertung starten**.</span><span class="sxs-lookup"><span data-stu-id="f0a12-135">Click **Start Assessment**.</span></span>

## <a name="view-results"></a><span data-ttu-id="f0a12-136">Anzeigen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="f0a12-136">View results</span></span>

<span data-ttu-id="f0a12-137">Wenn mehrere Datenbanken vorhanden sind, werden die Ergebnisse der einzelnen Datenbanken angezeigt, sobald diese verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="f0a12-137">If there are multiple databases, the results for each database will appear as soon as it is available.</span></span> <span data-ttu-id="f0a12-138">Sie müssen nicht warten, bis alle Datenbankbewertungen abgeschlossen wurden.</span><span class="sxs-lookup"><span data-stu-id="f0a12-138">You don't need to wait for all database assessments to complete.</span></span>

1. <span data-ttu-id="f0a12-139">Nachdem die Bewertung für **AdventureWorks** abgeschlossen wurde, klicken Sie auf **Compatibility issues** (Kompatibilitätsprobleme) und **Featureempfehlungen**, um die Ergebnisse anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f0a12-139">Once the assessment for **AdventureWorks** is complete, click **Compatibility issues** and **Feature recommendations** to view the results.</span></span>
    - <span data-ttu-id="f0a12-140">Die Kategorie „SQL Server-Featureparität“ enthält Features, die möglicherweise nicht vollständig unterstützt werden, und Schritte, um diese Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f0a12-140">The SQL Server feature parity category lists features that might not be fully supported and steps to remedy these issues.</span></span> <span data-ttu-id="f0a12-141">Migrationen werden jedoch aufgrund von Problemen mit der Featureparität nicht beendet.</span><span class="sxs-lookup"><span data-stu-id="f0a12-141">Feature parity issues will not stop a migration.</span></span>
    - <span data-ttu-id="f0a12-142">Die Kategorie „Kompatibilitätsprobleme“ enthält Features, die eine Migration beenden würden, und Schritte, um diese Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f0a12-142">The Compatibility issues category lists features that would block a migration and steps to remedy these issues.</span></span>

## <a name="summary"></a><span data-ttu-id="f0a12-143">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="f0a12-143">Summary</span></span>

<span data-ttu-id="f0a12-144">In dieser Übung haben Sie eine lokal installierte SQL Server-Datenbank bewertet, um zu überprüfen, ob Features nicht verfügbar wären, wenn Sie die Datenbank zu Azure SQL-Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="f0a12-144">In this exercise, you assessed a locally installed SQL Server database to verify if any features would be unavailable when you migrate the database to Azure SQL Database.</span></span>