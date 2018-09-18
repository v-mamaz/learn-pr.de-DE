<span data-ttu-id="082c1-101">Bevor Sie eine Verbindung der Datenbank mit Ihrer App herstellen, sollten Sie überprüfen, ob Sie eine Verbindung zu ihr herstellen, ihr eine einfache Tabelle hinzufügen und mit Beispieldaten arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="082c1-101">Before you connect the database to your app, you want to check that you can connect to it, add a basic table, and work with sample data.</span></span>

<span data-ttu-id="082c1-102">Wir verwalten die Infrastruktur, Softwareupdates und Patches für Ihre Azure SQL-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="082c1-102">We maintain the infrastructure, software updates, and patches for your Azure SQL database.</span></span> <span data-ttu-id="082c1-103">Darüber hinaus können Sie Ihre Azure SQL-Datenbank wie jede andere SQL Server-Installation behandeln.</span><span class="sxs-lookup"><span data-stu-id="082c1-103">Beyond that, you can treat your Azure SQL database like you would any other SQL Server installation.</span></span> <span data-ttu-id="082c1-104">Sie können z.B. Visual Studio, SQL Server Management Studio, SQL Server Operations Studio oder andere Tools zum Verwalten von Azure SQL-Datenbank verwenden.</span><span class="sxs-lookup"><span data-stu-id="082c1-104">For example, you can use Visual Studio, SQL Server Management Studio, SQL Server Operations Studio, or other tools to manage your Azure SQL database.</span></span>

<span data-ttu-id="082c1-105">Wie Sie auf die Datenbank zugreifen und die Verbindung zwischen ihr und Ihrer App herstellen, bleibt Ihnen überlassen.</span><span class="sxs-lookup"><span data-stu-id="082c1-105">How you access your database and connect it to your app is up to you.</span></span> <span data-ttu-id="082c1-106">Aber um ein wenig Erfahrung in der Arbeit mit Ihrer Datenbank zu sammeln, stellen Sie hier direkt aus dem Portal eine Verbindung mit ihr her, erstellen eine Tabelle und führen einige grundlegende CRUD-Vorgänge aus.</span><span class="sxs-lookup"><span data-stu-id="082c1-106">But to get some experience working with your database, here you'll connect to it directly from the portal, create a table, and run a few basic CRUD operations.</span></span> <span data-ttu-id="082c1-107">Sie lernen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="082c1-107">You'll learn:</span></span>

- <span data-ttu-id="082c1-108">Was Cloud Shell ist und wie Sie über das Portal darauf zugreifen.</span><span class="sxs-lookup"><span data-stu-id="082c1-108">What Cloud Shell is and how to access it from the portal.</span></span>
- <span data-ttu-id="082c1-109">Wie Sie über Azure CLI auf Informationen zu Ihrer Datenbank zugreifen, einschließlich der Verbindungszeichenfolgen.</span><span class="sxs-lookup"><span data-stu-id="082c1-109">How to access information about your database from the Azure CLI, including connection strings.</span></span>
- <span data-ttu-id="082c1-110">Wie Sie mittels `sqlcmd` eine Verbindung mit Ihrer Datenbank herstellen.</span><span class="sxs-lookup"><span data-stu-id="082c1-110">How to connect to your database using `sqlcmd`.</span></span>
- <span data-ttu-id="082c1-111">Wie Sie die Datenbank mit einer grundlegenden Tabelle und einigen Beispieldaten initialisieren.</span><span class="sxs-lookup"><span data-stu-id="082c1-111">How to initialize your database with a basic table and some sample data.</span></span>

## <a name="what-is-azure-cloud-shell"></a><span data-ttu-id="082c1-112">Was ist Azure Cloud Shell?</span><span class="sxs-lookup"><span data-stu-id="082c1-112">What is Azure Cloud Shell?</span></span>

<span data-ttu-id="082c1-113">Azure Cloud Shell ist eine browserbasierte Shell zum Verwalten und Entwickeln von Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="082c1-113">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span> <span data-ttu-id="082c1-114">Stellen Sie sich Cloud Shell als eine interaktive Konsole vor, die in der Cloud ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="082c1-114">Think of Cloud Shell as an interactive console that runs in the cloud.</span></span>

<span data-ttu-id="082c1-115">Hinter den Kulissen wird Cloud Shell unter Linux ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="082c1-115">Behind the scenes, Cloud Shell runs on Linux.</span></span> <span data-ttu-id="082c1-116">Aber abhängig davon, ob Sie eine Linux- oder Windows-Umgebung bevorzugen, haben Sie zwei Oberflächen zur Auswahl: Bash und PowerShell.</span><span class="sxs-lookup"><span data-stu-id="082c1-116">But depending on whether you prefer a Linux or Windows environment, you have two experiences to choose from: Bash and PowerShell.</span></span>

<span data-ttu-id="082c1-117">Auf Cloud Shell können Sie von überall zugreifen.</span><span class="sxs-lookup"><span data-stu-id="082c1-117">Cloud Shell is accessible from anywhere.</span></span> <span data-ttu-id="082c1-118">Außer vom Portal können Sie auch von [shell.azure.com](https://shell.azure.com/), der mobilen Azure-App oder Visual Studio Code aus auf Cloud Shell zugreifen.</span><span class="sxs-lookup"><span data-stu-id="082c1-118">Besides the portal, you can also access Cloud Shell from [shell.azure.com](https://shell.azure.com/), the Azure mobile app, or from Visual Studio Code.</span></span>

<span data-ttu-id="082c1-119">Cloud Shell umfasst beliebte Tools und Text-Editoren.</span><span class="sxs-lookup"><span data-stu-id="082c1-119">Cloud Shell includes popular tools and text editors.</span></span> <span data-ttu-id="082c1-120">Hier lernen Sie kurz `az`, `jq` und `sqlcmd` kennen, drei Tools, die Sie für unsere aktuelle Aufgabe verwenden.</span><span class="sxs-lookup"><span data-stu-id="082c1-120">Here's a brief look at `az`, `jq`, and `sqlcmd`, three tools you'll use for our current task.</span></span>

- <span data-ttu-id="082c1-121">`az` wird auch als Azure CLI bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="082c1-121">`az` is also known as the Azure CLI.</span></span> <span data-ttu-id="082c1-122">Dies ist die Befehlszeilenschnittstelle für die Arbeit mit Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="082c1-122">It's the command-line interface for working with Azure resources.</span></span> <span data-ttu-id="082c1-123">Sie verwenden sie, um Informationen zu Ihrer Datenbank einschließlich der Verbindungszeichenfolge zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="082c1-123">You'll use this to get information about your database, including the connection string.</span></span>
- <span data-ttu-id="082c1-124">`jq` ist ein Befehlszeilen-JSON-Parser.</span><span class="sxs-lookup"><span data-stu-id="082c1-124">`jq` is a command-line JSON parser.</span></span> <span data-ttu-id="082c1-125">Sie reichen die Ausgabe von `az`-Befehlen an dieses Tool weiter, um wichtige Felder aus der JSON-Ausgabe zu extrahieren.</span><span class="sxs-lookup"><span data-stu-id="082c1-125">You'll pipe output from `az` commands to this tool to extract important fields from JSON output.</span></span>
- <span data-ttu-id="082c1-126">Mit `sqlcmd` können Sie Anweisungen auf einer SQL Server-Instanz ausführen.</span><span class="sxs-lookup"><span data-stu-id="082c1-126">`sqlcmd` enables you to execute statements on SQL Server.</span></span> <span data-ttu-id="082c1-127">Mit `sqlcmd` erstellen Sie eine interaktive Sitzung mit Ihrer Azure SQL-Datenbankinstanz.</span><span class="sxs-lookup"><span data-stu-id="082c1-127">You'll use `sqlcmd` to create an interactive session with your Azure SQL database.</span></span>

## <a name="get-information-about-your-azure-sql-database"></a><span data-ttu-id="082c1-128">Abrufen von Informationen zu Ihrer Azure SQL-Datenbankinstanz</span><span class="sxs-lookup"><span data-stu-id="082c1-128">Get information about your Azure SQL database</span></span>

<span data-ttu-id="082c1-129">Bevor Sie eine Verbindung mit Ihrer Datenbank herstellen, sollten Sie überprüfen, ob sie vorhanden und online ist.</span><span class="sxs-lookup"><span data-stu-id="082c1-129">Before you connect to your database, it's a good idea to verify it exists and is online.</span></span>

<span data-ttu-id="082c1-130">Hierzu öffnen Sie Cloud Shell, und verwenden Sie das `az`-Hilfsprogramm zum Auflisten Ihrer Datenbanken und Anzeigen von Informationen zur **Logistics**-Datenbank einschließlich maximaler Größe und Status.</span><span class="sxs-lookup"><span data-stu-id="082c1-130">Here, you bring up Cloud Shell and use the `az` utility to list your databases and show some information about the **Logistics** database, including its maximum size and status.</span></span>

1. <span data-ttu-id="082c1-131">Klicken Sie im Portal im oberen Bereich auf **Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="082c1-131">From the portal, at the top, click **Cloud Shell**.</span></span>

1. <span data-ttu-id="082c1-132">Die von Ihnen ausgeführten `az`-Befehle erfordern den Namen Ihrer Ressourcengruppe und den Namen Ihres logischen Azure SQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="082c1-132">The `az` commands you'll run require the name of your resource group and the name of your Azure SQL logical server.</span></span> <span data-ttu-id="082c1-133">Um sich das Eintippen zu ersparen, führen Sie diesen `azure configure`-Befehl aus, um sie als Standardwerte anzugeben.</span><span class="sxs-lookup"><span data-stu-id="082c1-133">To save typing, run this `azure configure` command to specify them as default values.</span></span>
    <span data-ttu-id="082c1-134">Ersetzen Sie `contoso-logistics` durch den Namen Ihres logischen Azure SQL-Servers.</span><span class="sxs-lookup"><span data-stu-id="082c1-134">Replace `contoso-logistics` with the name of your Azure SQL logical server.</span></span>

    ```azurecli
    az configure --defaults group=logistics-db-rg sql-server=contoso-logistics
    ```

1. <span data-ttu-id="082c1-135">Führen Sie `az sql db list` zum Auflisten aller Datenbanken auf dem logischen Azure SQL-Server aus.</span><span class="sxs-lookup"><span data-stu-id="082c1-135">Run `az sql db list` to list all databases on your Azure SQL logical server.</span></span>

    ```azurecli
    az sql db list
    ```
    <span data-ttu-id="082c1-136">Sie sehen einen großen JSON-Block als Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="082c1-136">You see a large block of JSON as output.</span></span>

1. <span data-ttu-id="082c1-137">Da wir nur die Datenbanknamen benötigen, führen Sie den Befehl ein zweites Mal aus.</span><span class="sxs-lookup"><span data-stu-id="082c1-137">Since we want just the database names, run the command a second time.</span></span> <span data-ttu-id="082c1-138">Reichen Sie die Ausgabe diesmal an `jq` weiter, um nur die Namensfelder auszugeben.</span><span class="sxs-lookup"><span data-stu-id="082c1-138">This time, pipe the output to `jq` to print out only the name fields.</span></span>
    ```azurecli
    az sql db list | jq '[.[] | {name: .name}]'
    ```
    <span data-ttu-id="082c1-139">Sie sehen Folgendes.</span><span class="sxs-lookup"><span data-stu-id="082c1-139">You see this.</span></span>
    ```console
    [
      {
        "name": "Logistics"
      },
      {
        "name": "master"
      }
    ]
    ```
    <span data-ttu-id="082c1-140">**Logistics** ist Ihre Datenbank.</span><span class="sxs-lookup"><span data-stu-id="082c1-140">**Logistics** is your database.</span></span> <span data-ttu-id="082c1-141">Wie SQL Server enthält **master** Servermetadaten wie Anmeldekonten und Systemkonfigurationseinstellungen.</span><span class="sxs-lookup"><span data-stu-id="082c1-141">Like SQL Server, **master** includes server metadata, such as sign-in accounts and system configuration settings.</span></span>

1. <span data-ttu-id="082c1-142">Führen Sie diesen `az sql db show`-Befehl aus, um Details zur **Logistics**-Datenbank zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="082c1-142">Run this `az sql db show` command to get details about the **Logistics** database.</span></span>

    ```azurecli
    az sql db show --name Logistics
    ```
    <span data-ttu-id="082c1-143">Wie bereits zuvor sehen Sie einen großen JSON-Block als Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="082c1-143">As before, you see a large block of JSON as output.</span></span>

1. <span data-ttu-id="082c1-144">Führen Sie den Befehl ein zweites Mal aus.</span><span class="sxs-lookup"><span data-stu-id="082c1-144">Run the command a second time.</span></span> <span data-ttu-id="082c1-145">Reichen Sie die Ausgabe diesmal an `jq` weiter, um die Ausgabe auf den Namen, die maximale Größe und den Status der **Logistics**-Datenbank zu beschränken.</span><span class="sxs-lookup"><span data-stu-id="082c1-145">This time, pipe the output to `jq` to limit output to only the name, maximum size, and status of the **Logistics** database.</span></span>

    ```azurecli
    az sql db show --name Logistics | jq '{name: .name, maxSizeBytes: .maxSizeBytes, status: .status}'
    ```
    <span data-ttu-id="082c1-146">Sie sehen, dass die Datenbank online ist und ca. 2 GB Daten enthalten kann.</span><span class="sxs-lookup"><span data-stu-id="082c1-146">You see that the database is online and can hold around 2 GB of data.</span></span>
    ```console
    {
      "name": "Logistics",
      "maxSizeBytes": 2147483648,
      "status": "Online"
    }
    ```

## <a name="connect-to-your-database"></a><span data-ttu-id="082c1-147">Herstellen einer Verbindung mit Ihrer Datenbank</span><span class="sxs-lookup"><span data-stu-id="082c1-147">Connect to your database</span></span>

<span data-ttu-id="082c1-148">Da Sie nun etwas mit Ihrer Datenbank vertraut sind, lassen Sie uns eine Verbindung mit ihr unter Verwendung von `sqlcmd` herstellen, eine Tabelle erstellen, die Informationen über Transportfahrer enthält, und einige grundlegende CRUD-Vorgänge ausführen.</span><span class="sxs-lookup"><span data-stu-id="082c1-148">Now that you understand a bit about your database, let's connect to it using `sqlcmd`, create a table that holds information about transportation drivers, and perform a few basic CRUD operations.</span></span>

<span data-ttu-id="082c1-149">Beachten Sie, dass CRUD für **Create (Erstellen)**, **Read (Lesen)**, **Update (Aktualisieren)** und **Delete (Löschen)** steht.</span><span class="sxs-lookup"><span data-stu-id="082c1-149">Remember that CRUD stands for **create**, **read**, **update**, and **delete**.</span></span> <span data-ttu-id="082c1-150">Dies bezieht sich auf Vorgänge, die Sie an Tabellendaten ausführen, und diese vier grundlegenden Vorgänge benötigen Sie für Ihre App.</span><span class="sxs-lookup"><span data-stu-id="082c1-150">These terms refer to operations you perform on table data and are the four basic operations you need for your app.</span></span> <span data-ttu-id="082c1-151">Jetzt ist ein guter Zeitpunkt, um zu überprüfen, ob Sie sie jeweils ausführen können.</span><span class="sxs-lookup"><span data-stu-id="082c1-151">Now's a good time to verify you can perform each of them.</span></span>

1. <span data-ttu-id="082c1-152">Führen Sie diesen `az sql db show-connection-string`-Befehl aus, um die Verbindungszeichenfolge zum Herstellen der Verbindung mit der **Logistics**-Datenbank in einem Format abzurufen, das `sqlcmd` verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="082c1-152">Run this `az sql db show-connection-string` command to get the connection string to the **Logistics** database in a format that `sqlcmd` can use.</span></span>

    ```azurecli
    az sql db show-connection-string --client sqlcmd --name Logistics
    ```
    <span data-ttu-id="082c1-153">Die Ausgabe sieht ungefähr so aus.</span><span class="sxs-lookup"><span data-stu-id="082c1-153">Your output resembles this.</span></span>
    ```console
    "sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U <username> -P <password> -N -l 30"
    ```

1. <span data-ttu-id="082c1-154">Führen Sie die `sqlcmd`-Anweisung aus dem vorherigen Schritt aus, um eine interaktive Sitzung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="082c1-154">Run the `sqlcmd` statement from the previous step to create an interactive session.</span></span>
    <span data-ttu-id="082c1-155">Entfernen Sie die umgebenden Anführungszeichen, und ersetzen Sie `<username>` und `<password>` durch den Benutzernamen und das Kennwort, die Sie beim Erstellen der Datenbank angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="082c1-155">Remove the surrounding quotes and replace `<username>` and `<password>` with the username and password you specified when you created your database.</span></span> <span data-ttu-id="082c1-156">Hier sehen Sie ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="082c1-156">Here's an example.</span></span>

    ```console
    sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U martina -P "password1234$" -N -l 30
    ```

    > [!TIP]
    > <span data-ttu-id="082c1-157">Setzen Sie Ihr Kennwort in Anführungszeichen, damit „&“ und andere Sonderzeichen nicht als Verarbeitungsanweisungen interpretiert werden.</span><span class="sxs-lookup"><span data-stu-id="082c1-157">Place your password in quotes so that "&" and other special characters aren't interpreted as processing instructions.</span></span>

1. <span data-ttu-id="082c1-158">Erstellen Sie von Ihrer `sqlcmd`-Sitzung aus eine Tabelle mit dem Namen `Drivers`.</span><span class="sxs-lookup"><span data-stu-id="082c1-158">From your `sqlcmd` session, create a table named `Drivers`.</span></span>

    ```sql
    CREATE TABLE Drivers (DriverID int, LastName varchar(255), FirstName varchar(255), OriginCity varchar(255) );
    GO
    ```

    <span data-ttu-id="082c1-159">Die Tabelle enthält vier Spalten: einen eindeutigen Bezeichner, Nach- und Vorname des Fahrers und den Herkunftsort des Fahrers.</span><span class="sxs-lookup"><span data-stu-id="082c1-159">The table contains four columns: a unique identifier, the driver's last and first name, and the driver's city of origin.</span></span>

    > [!NOTE]
    > <span data-ttu-id="082c1-160">Die hier gezeigte Sprache ist Transact-SQL, auch als T-SQL bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="082c1-160">The language you see here is Transact-SQL, or T-SQL.</span></span>

1. <span data-ttu-id="082c1-161">Überprüfen Sie, ob die `Drivers`-Tabelle vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="082c1-161">Verify that the `Drivers` table exists.</span></span>

    ```sql
    SELECT name FROM sys.tables;
    GO
    ```

    <span data-ttu-id="082c1-162">Sie sehen Folgendes.</span><span class="sxs-lookup"><span data-stu-id="082c1-162">You see this.</span></span>

    ```console
    name
    --------------------------------------------------------------------------------------------------------------------------------
    Drivers

    (1 rows affected)
    ```

1. <span data-ttu-id="082c1-163">Führen Sie diese `INSERT`-T-SQL-Anweisung aus, um der Tabelle eine Beispielzeile hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="082c1-163">Run this `INSERT` T-SQL statement to add a sample row to the table.</span></span> <span data-ttu-id="082c1-164">Dies ist der **Create**-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="082c1-164">This is the **create** operation.</span></span>

    ```sql
    INSERT INTO Drivers (DriverID, LastName, FirstName, OriginCity) VALUES (123, 'Zirne', 'Laura', 'Springfield');
    GO
    ```

    <span data-ttu-id="082c1-165">Dies zeigt Ihnen an, dass der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="082c1-165">You see this to indicate the operation succeeded.</span></span>

    ```console
    (1 rows affected)
    ```

1. <span data-ttu-id="082c1-166">Führen Sie diese `SELECT`-T-SQL-Anweisungsliste für die `DriverID`-Spalte aller Zeilen in der Tabelle aus.</span><span class="sxs-lookup"><span data-stu-id="082c1-166">Run this `SELECT` T-SQL statement list in the `DriverID` column from all rows in the table.</span></span> <span data-ttu-id="082c1-167">Dies ist der **Read**-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="082c1-167">This is the **read** operation.</span></span>

    ```sql
    SELECT DriverID FROM Drivers;
    GO
    ```

    <span data-ttu-id="082c1-168">Daraufhin wird ein Ergebnis angezeigt, die `DriverID` für die Zeile, die Sie im vorherigen Schritt erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="082c1-168">You see one result, the `DriverID` for the row you created in the previous step.</span></span>

    ```console
    DriverID
    -----------
            123

    (1 rows affected)
    ```

1. <span data-ttu-id="082c1-169">Führen Sie diese `UPDATE`-T-SQL-Anweisung aus, um den Herkunftsort für den Fahrer mit der `DriverID` „123“ von „Springfield“ in „Springfield, OR“ zu ändern.</span><span class="sxs-lookup"><span data-stu-id="082c1-169">Run this `UPDATE` T-SQL statement to change the city of origin from "Springfield" to "Springfield, OR" for the driver with a `DriverID` of 123.</span></span> <span data-ttu-id="082c1-170">Dies ist der **Update**-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="082c1-170">This is the **update** operation.</span></span>

    ```sql
    UPDATE Drivers SET OriginCity='Springfield, AK' WHERE DriverID=123;
    GO
    ```

    <span data-ttu-id="082c1-171">Sie sehen Folgendes.</span><span class="sxs-lookup"><span data-stu-id="082c1-171">You see this.</span></span>

    ```console
    (1 rows affected)
    ```

1. <span data-ttu-id="082c1-172">Führen Sie diese `DELETE`-T-SQL-Anweisung aus, um den Datensatz zu löschen.</span><span class="sxs-lookup"><span data-stu-id="082c1-172">Run this `DELETE` T-SQL statement to delete the record.</span></span> <span data-ttu-id="082c1-173">Dies ist der **Delete**-Vorgang.</span><span class="sxs-lookup"><span data-stu-id="082c1-173">This is the **delete** operation.</span></span>

    ```sql
    DELETE FROM Drivers WHERE DriverID=123;
    GO
    ```

    ```console
    (1 rows affected)
    ```

1. <span data-ttu-id="082c1-174">Führen Sie diese `SELECT`-T-SQL-Anweisung aus, um zu überprüfen, ob die `Drivers`-Tabelle leer ist.</span><span class="sxs-lookup"><span data-stu-id="082c1-174">Run this `SELECT` T-SQL statement to verify the `Drivers` table is empty.</span></span>

    ```sql
    SELECT COUNT(*) FROM Drivers;
    GO
    ```

    <span data-ttu-id="082c1-175">Sie sehen, dass die Tabelle keine Zeilen enthält.</span><span class="sxs-lookup"><span data-stu-id="082c1-175">You see that the table contains no rows.</span></span>

    ```console
    -----------
              0

    (1 rows affected)
    ```

## <a name="summary"></a><span data-ttu-id="082c1-176">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="082c1-176">Summary</span></span>

<span data-ttu-id="082c1-177">Da Sie nun wissen, wie Sie mittels Cloud Shell mit Azure SQL-Datenbank arbeiten, können Sie die Verbindungszeichenfolge für Ihr bevorzugtes SQL-Verwaltungstool abrufen &ndash; ganz gleich, ob von SQL Server Management Studio, Visual Studio oder sonst wo aus.</span><span class="sxs-lookup"><span data-stu-id="082c1-177">Now that you have the hang of working with Azure SQL Database from Cloud Shell, you can get the connection string for your favorite SQL management tool &ndash; whether that's from SQL Server Management Studio, Visual Studio, or something else.</span></span>

<span data-ttu-id="082c1-178">Cloud Shell erleichtert Ihnen den Zugriff auf Ihre Azure-Ressourcen und die Arbeit damit.</span><span class="sxs-lookup"><span data-stu-id="082c1-178">Cloud Shell makes it easy to access and work with your Azure resources.</span></span> <span data-ttu-id="082c1-179">Da Cloud Shell browserbasiert ist, können Sie mit Windows, macOS oder Linux darauf zugreifen &ndash; im Wesentlichen mit jedem System, in dem ein Webbrowser zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="082c1-179">Because Cloud Shell is browser-based, you can access it from Windows, macOS, or Linux &ndash; essentially any system with a web browser.</span></span>

<span data-ttu-id="082c1-180">Sie gewannen einige praktische Erfahrungen mit der Ausführung von Azure CLI-Befehlen zum Abrufen von Informationen zu Ihrer SQL Azure-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="082c1-180">You gained some hands-on experience running Azure CLI commands to get information about your Azure SQL database.</span></span> <span data-ttu-id="082c1-181">Als Bonus übten Sie Ihre T-SQL-Fertigkeiten.</span><span class="sxs-lookup"><span data-stu-id="082c1-181">As a bonus, you practiced your T-SQL skills.</span></span>

<span data-ttu-id="082c1-182">Jetzt kommen wir zum Ende und sehen, wie wir Ihre Datenbank entfernen können.</span><span class="sxs-lookup"><span data-stu-id="082c1-182">Finally, let's wrap up and see how to tear down your database.</span></span>
