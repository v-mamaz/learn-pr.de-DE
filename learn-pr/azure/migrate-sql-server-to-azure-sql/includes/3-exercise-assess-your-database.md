<span data-ttu-id="e163f-101">In dieser Einheit bewerten Sie eine vorhandene Datenbank mithilfe des Datenmigrations-Assistenten und überprüfen alle Funktionen, die in der lokalen SQL Server-Instanz verwendet und derzeit nicht von Azure SQL-Datenbank unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="e163f-101">In this unit, you'll assess an existing database using the Data Migration Assistant and review any features used in the local SQL Server instance that aren't currently supported by Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="e163f-102">Einrichtung</span><span class="sxs-lookup"><span data-stu-id="e163f-102">Setup</span></span>

1. <span data-ttu-id="e163f-103">[Installieren Sie den **Datenmigrations-Assistenten**](https://www.microsoft.com/download/details.aspx?id=53595), wenn Sie dies noch nicht getan haben.</span><span class="sxs-lookup"><span data-stu-id="e163f-103">[Install the **Data Migration Assistant**](https://www.microsoft.com/download/details.aspx?id=53595) if you haven't done so already.</span></span>

1. <span data-ttu-id="e163f-104">Dazu muss eine SQL Server-Instanz ausgeführt werden. Außerdem müssen Sie die Verbindungsdetails zur Hand haben.</span><span class="sxs-lookup"><span data-stu-id="e163f-104">You'll need a SQL Server instance running, ensure you have connection details available.</span></span>

<!-- 1. [**** likely replace with an LOD VM *****] TODO: -->

1. <span data-ttu-id="e163f-105">Öffnen Sie einen Internetbrowser, und navigieren Sie zu https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span><span class="sxs-lookup"><span data-stu-id="e163f-105">Start an Internet browser and navigate to https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="e163f-106">Klicken Sie unter **OLTP downloads** (OLTP-Downloads) auf **AdventureWorks2008R2.bak**, und speichern Sie die Datei auf Ihrem lokalen Computer.</span><span class="sxs-lookup"><span data-stu-id="e163f-106">In **OLTP downloads**, click **AdventureWorks2008R2.bak** and save it to your local machine.</span></span>

1. <span data-ttu-id="e163f-107">Stellen Sie *AdventureWorks 2008R2* in Management Studio auf Ihrer Standardinstanz wieder her.</span><span class="sxs-lookup"><span data-stu-id="e163f-107">In Management Studio, restore *AdventureWorks 2008R2* to your default instance.</span></span>

## <a name="create-an-assessment"></a><span data-ttu-id="e163f-108">Erstellen einer Bewertung</span><span class="sxs-lookup"><span data-stu-id="e163f-108">Create an assessment</span></span>

1. <span data-ttu-id="e163f-109">Starten Sie **Microsoft-Datenmigrations-Assistent**.</span><span class="sxs-lookup"><span data-stu-id="e163f-109">Start the **Microsoft Data Migration Assistant**.</span></span>

1. <span data-ttu-id="e163f-110">Klicken Sie im linken Navigationsbereich der App auf __+__, um ein neues Datenmigrations-Assistent-Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e163f-110">In the app's left-hand navigation, click __+__ to create a new Data Migration Assistant project.</span></span>

1. <span data-ttu-id="e163f-111">Geben Sie die folgenden Optionen an:</span><span class="sxs-lookup"><span data-stu-id="e163f-111">Specify the following options:</span></span>

    - <span data-ttu-id="e163f-112">**Projekttyp:** Wählen Sie *Bewertung* aus.</span><span class="sxs-lookup"><span data-stu-id="e163f-112">**Project type** - Select *Assessment*</span></span>
    - <span data-ttu-id="e163f-113">**Projektname:** Geben Sie einen Namen für Ihr Projekt ein, z.B. „FahrradDB-Bewertung“.</span><span class="sxs-lookup"><span data-stu-id="e163f-113">**Project name** - Enter a name for your project - for example, "Bicycle DB Assessment"</span></span>
    - <span data-ttu-id="e163f-114">**Typ des Quellservers:** Wählen Sie *SQL Server* aus.</span><span class="sxs-lookup"><span data-stu-id="e163f-114">**Source server type** - Select *SQL Server*</span></span>
    - <span data-ttu-id="e163f-115">**Typ des Zielservers:** Wählen Sie *Azure SQL-Datenbank*.</span><span class="sxs-lookup"><span data-stu-id="e163f-115">**Target server type** - Select *Azure SQL Database*</span></span>

1. <span data-ttu-id="e163f-116">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e163f-116">Click **Create**.</span></span>
    <span data-ttu-id="e163f-117">![Screenshot der beschriebenen Konfiguration in Datenmigrations-Assistent für Ihre AdventureWorks-SQL Server-Daten](../media-draft/3-create-assessment.png)</span><span class="sxs-lookup"><span data-stu-id="e163f-117">![Screenshot showing the described configuration in the Data Migration Assistant for your AdventureWorks SQL Server data.](../media-draft/3-create-assessment.png)</span></span>

1. <span data-ttu-id="e163f-118">Wählen Sie den Typ des Bewertungsberichts aus, und überprüfen Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="e163f-118">Select the assessment report type - check both:</span></span>
    - <span data-ttu-id="e163f-119">Datenbankkompatibilität überprüfen</span><span class="sxs-lookup"><span data-stu-id="e163f-119">Check database compatibility</span></span>
    - <span data-ttu-id="e163f-120">Check feature parity (Featureparität prüfen)</span><span class="sxs-lookup"><span data-stu-id="e163f-120">Check feature parity</span></span>

1. <span data-ttu-id="e163f-121">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="e163f-121">Click **Next**.</span></span>

## <a name="add-databases-to-assess"></a><span data-ttu-id="e163f-122">Auswählen zu bewertender Datenbanken</span><span class="sxs-lookup"><span data-stu-id="e163f-122">Add databases to assess</span></span>

1. <span data-ttu-id="e163f-123">Klicken Sie auf **Quellen hinzufügen**, um das Verbindungsmenü zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="e163f-123">Click **Add Sources** to open the connection menu.</span></span>

1. <span data-ttu-id="e163f-124">Gehen Sie wie folgt vor:</span><span class="sxs-lookup"><span data-stu-id="e163f-124">Do the following:</span></span>

    - <span data-ttu-id="e163f-125">Geben Sie den Namen Ihrer vorhandenen SQL Server-Instanz ein.</span><span class="sxs-lookup"><span data-stu-id="e163f-125">Enter your existing SQL server instance name</span></span>
    - <span data-ttu-id="e163f-126">Wählen Sie den **Authentifizierungstyp** aus.</span><span class="sxs-lookup"><span data-stu-id="e163f-126">Select the **Authentication** type</span></span>
    - <span data-ttu-id="e163f-127">Geben Sie die Verbindungseigenschaften für Ihren Server ein.</span><span class="sxs-lookup"><span data-stu-id="e163f-127">Specify the connection properties for your server</span></span>

1. <span data-ttu-id="e163f-128">Klicken Sie auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="e163f-128">CLick **Connect**.</span></span>

1. <span data-ttu-id="e163f-129">Wählen Sie unter **Quellen hinzufügen** die Datenbanken aus, die bewertet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="e163f-129">In **Add sources**, select the databases to assess.</span></span> <span data-ttu-id="e163f-130">Wählen Sie für diese Übung **AdventureWorks2008R2** aus.</span><span class="sxs-lookup"><span data-stu-id="e163f-130">For this exercise, select **AdventureWorks2008R2**.</span></span>

1. <span data-ttu-id="e163f-131">Klicken Sie auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="e163f-131">Click **Add**.</span></span>
    > [!NOTE]
    > <span data-ttu-id="e163f-132">Verwenden Sie zum Hinzufügen von Datenbanken aus mehreren SQL Server-Instanzen die Schaltfläche **Quellen hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="e163f-132">To add databases from multiple SQL Server instances, use the **Add Sources** button.</span></span> <span data-ttu-id="e163f-133">Wenn Sie mehrere Datenbanken entfernen möchten, drücken Sie UMSCHALT+STRG, um die zu entfernenden Datenbanken auszuwählen, und klicken Sie dann auf **Quellen entfernen**.</span><span class="sxs-lookup"><span data-stu-id="e163f-133">To remove multiple databases, hold the SHIFT+CTRL keys to select the databases you want to remove, then click **Remove Sources**.</span></span>

1. <span data-ttu-id="e163f-134">Klicken Sie auf **Bewertung starten**.</span><span class="sxs-lookup"><span data-stu-id="e163f-134">Click **Start Assessment**.</span></span>

## <a name="view-results"></a><span data-ttu-id="e163f-135">Anzeigen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="e163f-135">View results</span></span>

<span data-ttu-id="e163f-136">Wenn mehrere Datenbanken vorhanden sind, werden die Ergebnisse der einzelnen Datenbanken angezeigt, sobald diese verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="e163f-136">If there are multiple databases, the results for each database appears as soon as it is available.</span></span> <span data-ttu-id="e163f-137">Sie müssen nicht warten, bis alle Datenbankbewertungen abgeschlossen wurden.</span><span class="sxs-lookup"><span data-stu-id="e163f-137">You don't need to wait for all database assessments to complete.</span></span>

1. <span data-ttu-id="e163f-138">Nachdem die Bewertung für **AdventureWorks** abgeschlossen wurde, klicken Sie auf **Compatibility issues** (Kompatibilitätsprobleme) und **Featureempfehlungen**, um die Ergebnisse anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="e163f-138">Once the assessment for **AdventureWorks** is complete, click **Compatibility issues** and **Feature recommendations** to view the results.</span></span>

    - <span data-ttu-id="e163f-139">Die Kategorie „SQL Server-Featureparität“ enthält Features, die möglicherweise nicht vollständig unterstützt werden, und Schritte, um diese Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="e163f-139">The SQL Server feature parity category lists features that might not be fully supported and steps to remedy these issues.</span></span> <span data-ttu-id="e163f-140">Migrationen werden jedoch aufgrund von Problemen mit der Featureparität nicht beendet.</span><span class="sxs-lookup"><span data-stu-id="e163f-140">Feature parity issues will not stop a migration.</span></span>
    - <span data-ttu-id="e163f-141">Die Kategorie „Kompatibilitätsprobleme“ enthält Features, die eine Migration beenden würden, und Schritte, um diese Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="e163f-141">The Compatibility issues category lists features that would block a migration and steps to remedy these issues.</span></span>

## <a name="summary"></a><span data-ttu-id="e163f-142">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="e163f-142">Summary</span></span>

<span data-ttu-id="e163f-143">In dieser Einheit haben Sie eine lokal installierte SQL Server-Datenbank bewertet, um zu überprüfen, ob Features nicht verfügbar wären, wenn Sie die Datenbank zu Azure SQL-Datenbank migrieren.</span><span class="sxs-lookup"><span data-stu-id="e163f-143">In this unit, you assessed a locally installed SQL Server database to verify if any features would be unavailable when you migrate the database to Azure SQL Database.</span></span>