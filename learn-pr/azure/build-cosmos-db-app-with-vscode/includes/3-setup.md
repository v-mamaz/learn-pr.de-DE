<span data-ttu-id="0c69c-101">Mit Visual Studio Code können Sie eine Konsolen-App erstellen, indem Sie das integrierte Terminal und einige kurze Befehle verwenden.</span><span class="sxs-lookup"><span data-stu-id="0c69c-101">Visual Studio Code enables you to create a console application by using the integrated terminal and a few short commands.</span></span>

<span data-ttu-id="0c69c-102">In dieser Einheit erstellen Sie eine einfache Konsolen-App über das integrierte Terminal, rufen Ihre Azure Cosmos DB-Verbindungszeichenfolge aus der Erweiterung ab und konfigurieren anschließend die Verbindung zwischen Ihrer Konsolen-App und Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0c69c-102">In this unit, you will create a simple console app using the integrated terminal, retrieve your Azure Cosmos DB connection string from the extension, and then configure the connection from your application to Azure Cosmos DB.</span></span>

## <a name="create-a-console-app"></a><span data-ttu-id="0c69c-103">Erstellen einer Konsolen-App</span><span class="sxs-lookup"><span data-stu-id="0c69c-103">Create a console app</span></span>

1. <span data-ttu-id="0c69c-104">Klicken Sie in Visual Studio Code auf **Datei** > **Ordner öffnen**.</span><span class="sxs-lookup"><span data-stu-id="0c69c-104">In Visual Studio Code, select **File** > **Open Folder**.</span></span>

1. <span data-ttu-id="0c69c-105">Erstellen Sie am Speicherort Ihrer Wahl einen neuen Ordner namens `learning-module`, und klicken Sie dann auf **Ordner auswählen**.</span><span class="sxs-lookup"><span data-stu-id="0c69c-105">Create a new folder named `learning-module` in the location of your choice, and then click **Select Folder**.</span></span>

1. <span data-ttu-id="0c69c-106">Vergewissern Sie sich, dass das automatische Speichern aktiviert ist, indem Sie auf das Menü „Datei“ klicken und überprüfen, ob **Automatisch speichern** leer ist.</span><span class="sxs-lookup"><span data-stu-id="0c69c-106">Ensure that file auto-save is enabled by clicking on the File menu and checking **Auto Save** if it is blank.</span></span> <span data-ttu-id="0c69c-107">Sie werden mehrere Codeblöcke kopieren. Dadurch wird sichergestellt, dass Sie immer mit den neuesten Versionen Ihrer Dateien arbeiten.</span><span class="sxs-lookup"><span data-stu-id="0c69c-107">You will be copying in several blocks of code, and this will ensure you are always operating against the latest edits of your files.</span></span>

1. <span data-ttu-id="0c69c-108">Öffnen Sie das integrierte Terminal aus Visual Studio Code, indem Sie im Hauptmenü auf **Ansicht** > **Terminal** klicken.</span><span class="sxs-lookup"><span data-stu-id="0c69c-108">Open the integrated terminal from Visual Studio Code by selecting **View** > **Terminal** from the main menu.</span></span>

1. <span data-ttu-id="0c69c-109">Kopieren Sie den folgenden Befehl, und fügen Sie ihn in das Terminalfenster ein.</span><span class="sxs-lookup"><span data-stu-id="0c69c-109">In the terminal window, copy and paste the following command.</span></span>

    ```bash
    dotnet new console
    ```

    <span data-ttu-id="0c69c-110">Mit diesem Befehl werden in Ihrem Ordner die Datei **Program.cs** mit einem einfachen Hallo Welt-Programm und eine C#-Projektdatei namens **learning-module.csproj** erstellt.</span><span class="sxs-lookup"><span data-stu-id="0c69c-110">This command creates a **Program.cs** file in your folder with a simple "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

1. <span data-ttu-id="0c69c-111">Kopieren Sie den folgenden Befehl, und fügen Sie ihn in das Terminalfenster ein, um das Hallo Welt-Programm auszuführen.</span><span class="sxs-lookup"><span data-stu-id="0c69c-111">In the terminal window, copy and paste the following command to run the "Hello World" program.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="0c69c-112">Im Terminalfenster wird „Hello World!“ (Hallo Welt!)</span><span class="sxs-lookup"><span data-stu-id="0c69c-112">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="0c69c-113">als Ausgabe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0c69c-113">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="0c69c-114">Herstellen einer Verbindung zwischen der App und Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0c69c-114">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="0c69c-115">Kopieren Sie den folgenden Befehlsblock, und fügen Sie ihn an der Terminaleingabeaufforderung ein, um die erforderlichen NuGet-Pakete zu installieren.</span><span class="sxs-lookup"><span data-stu-id="0c69c-115">At the terminal prompt, copy and paste the following command block to install the required NuGet packages.</span></span>

    ```bash
    dotnet add package System.Net.Http
    dotnet add package System.Configuration
    dotnet add package System.Configuration.ConfigurationManager
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet restore
    ```

1. <span data-ttu-id="0c69c-116">Klicken Sie oben im Bereich „Explorer“ auf **Program.cs**, um die Datei zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="0c69c-116">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

1. <span data-ttu-id="0c69c-117">Fügen Sie nach `using System;` die folgenden using-Anweisungen hinzu.</span><span class="sxs-lookup"><span data-stu-id="0c69c-117">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

    <span data-ttu-id="0c69c-118">Wenn eine Meldung zum Hinzufügen von fehlenden erforderlichen Ressourcen angezeigt wird, klicken Sie auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="0c69c-118">If you get a message about adding required missing assets, click **Yes**.</span></span>

1. <span data-ttu-id="0c69c-119">Erstellen Sie eine neue Datei namens „App.config“ im Ordner „learning-module“, und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="0c69c-119">Create a new file named App.config in the learning-module folder, and add the following code.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. <span data-ttu-id="0c69c-120">Kopieren Sie die Verbindungszeichenfolge, indem Sie zuerst links auf das Azure-Symbol ![Azure-Symbol](../media/2-setup/visual-studio-code-explorer-icon.png) klicken und das Concierge-Abonnement erweitern. Klicken Sie anschließend mit der rechten Maustaste auf Ihr Azure Cosmos DB-Konto und dann auf **Copy Connection String** (Verbindungszeichenfolge kopieren).</span><span class="sxs-lookup"><span data-stu-id="0c69c-120">Copy your connection string by clicking the ![Azure icon](../media/2-setup/visual-studio-code-explorer-icon.png) Azure icon on the left, expanding your Concierge Subscription, right-clicking your new Azure Cosmos DB account, and then clicking **Copy Connection String**.</span></span>

1. <span data-ttu-id="0c69c-121">Fügen Sie die Verbindungszeichenfolge am Ende der Datei „App.config“ ein, kopieren Sie den Abschnitt **AccountEndpoint** aus der Verbindungszeichenfolge, und fügen Sie ihn für den Wert **accountEndpoint** in „App.config“ ein.</span><span class="sxs-lookup"><span data-stu-id="0c69c-121">Paste the connection string into the end of the App.config file, and then copy the **AccountEndpoint** portion from the connection string into the **accountEndpoint** value in App.config.</span></span>

    <span data-ttu-id="0c69c-122">„accountEndpoint“ sollte wie im folgenden Code aussehen:</span><span class="sxs-lookup"><span data-stu-id="0c69c-122">The accountEndpoint should look like the following code:</span></span>

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

1. <span data-ttu-id="0c69c-123">Kopieren Sie nun den Wert **AccountKey** aus der Verbindungszeichenfolge in den Wert **accountKey**, und löschen Sie anschließend die ursprüngliche Verbindungszeichenfolge, aus der Sie die Werte kopiert haben.</span><span class="sxs-lookup"><span data-stu-id="0c69c-123">Now copy the **AccountKey** value from the connection string into the **accountKey** value, and then delete the original connection string you copied in.</span></span>

1. <span data-ttu-id="0c69c-124">Kopieren Sie den folgenden Befehl, und fügen Sie ihn in die Terminaleingabeaufforderung ein, um das Programm auszuführen.</span><span class="sxs-lookup"><span data-stu-id="0c69c-124">At the terminal prompt, copy and paste the following command to run the program.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="0c69c-125">Das Programm zeigt „Hello World!“</span><span class="sxs-lookup"><span data-stu-id="0c69c-125">The program displays Hello World!</span></span> <span data-ttu-id="0c69c-126">im Terminal an.</span><span class="sxs-lookup"><span data-stu-id="0c69c-126">in the terminal.</span></span>

## <a name="create-the-documentclient"></a><span data-ttu-id="0c69c-127">Erstellen von DocumentClient</span><span class="sxs-lookup"><span data-stu-id="0c69c-127">Create the DocumentClient</span></span>

<span data-ttu-id="0c69c-128">Jetzt ist es Zeit, eine Instanz von DocumentClient zu erstellen. Dies ist die clientseitige Darstellung des Azure Cosmos DB-Diensts.</span><span class="sxs-lookup"><span data-stu-id="0c69c-128">Now it's time to create an instance of the DocumentClient, which is the client-side representation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="0c69c-129">Mit diesem Client werden Anforderungen für den Dienst konfiguriert und ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="0c69c-129">This client is used to configure and execute requests against the service.</span></span>

1. <span data-ttu-id="0c69c-130">Fügen Sie Folgendes am Anfang der Klasse „Program“ in der Datei „Program.cs“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="0c69c-130">In Program.cs, add the following to the beginning of the Program class.</span></span>

    ```csharp
    private DocumentClient client;
    ```

1. <span data-ttu-id="0c69c-131">Fügen Sie eine neue asynchrone Aufgabe zum Erstellen eines neuen Clients hinzu, und überprüfen Sie, ob die Datenbank „Users“ vorhanden ist, indem Sie die folgende Methode nach der `Main`-Methode hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="0c69c-131">Add a new asynchronous task to create a new client, and check whether the Users database exists by adding the following method after the `Main` method.</span></span>

    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["accountEndpoint"]), ConfigurationManager.AppSettings["accountKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });

        Console.WriteLine("Database and collection validation complete");
    }
    ```

1. <span data-ttu-id="0c69c-132">Kopieren Sie den folgenden Befehl, und fügen Sie ihn erneut im integrierten Terminal zum Ausführen des Programms ein, um sicherzustellen, dass er ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="0c69c-132">In the integrated terminal, again, copy and paste the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

1. <span data-ttu-id="0c69c-133">Kopieren Sie den folgenden Code, und fügen Sie ihn in die **Main**-Methode ein. Überschreiben Sie hierbei die aktuelle `Console.WriteLine("Hello World!");`-Zeile.</span><span class="sxs-lookup"><span data-stu-id="0c69c-133">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

    ```csharp
    try
    {
        Program p = new Program();
        p.BasicOperations().Wait();
    }
    catch (DocumentClientException de)
    {
        Exception baseException = de.GetBaseException();
        Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
    }
    catch (Exception e)
    {
        Exception baseException = e.GetBaseException();
        Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
    }
    finally
    {
        Console.WriteLine("End of demo, press any key to exit.");
        Console.ReadKey();
    }
    ```

1. <span data-ttu-id="0c69c-134">Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="0c69c-134">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="0c69c-135">In der Konsole wird nun Folgendes ausgegeben:</span><span class="sxs-lookup"><span data-stu-id="0c69c-135">The console displays the following output.</span></span>

    ```output
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

<span data-ttu-id="0c69c-136">In dieser Einheit haben Sie das Fundament für Ihre Azure Cosmos DB-Anwendung gelegt.</span><span class="sxs-lookup"><span data-stu-id="0c69c-136">In this unit, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="0c69c-137">Sie haben Ihre Entwicklungsumgebung in Visual Studio Code eingerichtet, ein einfaches Hello World-Projekt erstellt, das Projekt mit dem Azure Cosmos DB-Endpunkt verbunden und sichergestellt, dass Ihre Datenbank und Ihre Sammlung vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="0c69c-137">You set up your development environment in Visual Studio Code, created a simple HelloWorld project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>
