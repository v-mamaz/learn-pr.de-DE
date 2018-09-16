<span data-ttu-id="ad1af-101">In diesem Modul erstellen Sie eine einfache Konsolen-App mit dem integrierten Terminal, installieren NuGet-Pakete und verwenden die Azure Cosmos DB-Erweiterung, um die im vorherigen Modul erstellten Datenbanken und Sammlungen anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-101">In this module you will create a simple console app using the integrated terminal, install NuGet packages, and use the Azure Cosmos DB extension to see databases and collections created in the previous module.</span></span> <span data-ttu-id="ad1af-102">Sie rufen Ihre Azure Cosmos DB-Verbindungszeichenfolge aus der Erweiterung ab und beginnen mit dem Konfigurieren der Verbindung mit Azure Cosmos DB, um Ihre Benutzerdatenbank zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-102">You'll retrieve your Azure Cosmos DB connection string from the extension, and then start configuring the connection to Azure Cosmos DB to create your User database.</span></span>

## <a name="create-a-console-app"></a><span data-ttu-id="ad1af-103">Erstellen einer Konsolen-App</span><span class="sxs-lookup"><span data-stu-id="ad1af-103">Create a console app</span></span>

1. <span data-ttu-id="ad1af-104">Öffnen Sie Visual Studio Code, und wählen Sie **Datei** > **Ordner öffnen** aus.</span><span class="sxs-lookup"><span data-stu-id="ad1af-104">Open Visual Studio Code, and then select **File** > **Open Folder**.</span></span>

1. <span data-ttu-id="ad1af-105">Erstellen Sie einen neuen Ordner für Ihr neues C#-Projekt, und klicken Sie dann auf **Ordner auswählen**.</span><span class="sxs-lookup"><span data-stu-id="ad1af-105">Create a new folder where you want your new C# project to be, and then click **Select Folder**.</span></span>

1. <span data-ttu-id="ad1af-106">Vergewissern Sie sich, dass das automatisches Speichern aktiviert ist, indem Sie auf das Menü „Datei“ klicken und überprüfen, ob **Automatisch speichern** leer ist.</span><span class="sxs-lookup"><span data-stu-id="ad1af-106">Ensure that file auto save is enabled by clicking on the File menu and checking **Auto Save** if it is blank.</span></span>

1. <span data-ttu-id="ad1af-107">Öffnen Sie das integrierte Terminal aus Visual Studio Code, indem Sie im Hauptmenü **Ansicht** > **Terminal** auswählen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-107">Open the integrated terminal from Visual Studio Code by selecting **View** > **Terminal** from the main menu.</span></span>

1. <span data-ttu-id="ad1af-108">Geben Sie im Terminalfenster den folgenden Befehl ein.</span><span class="sxs-lookup"><span data-stu-id="ad1af-108">In the terminal window, type the following command.</span></span>

    ```
    dotnet new console
    ```

    <span data-ttu-id="ad1af-109">Mit diesem Befehl wird eine Datei **Program.cs** in Ihrem Ordner erstellt, die ein bereits geschriebenes einfaches Programm „Hello World“ enthält, gemeinsam mit einem C#-Projekt namens **learning-module.csproj**.</span><span class="sxs-lookup"><span data-stu-id="ad1af-109">This command creates a **Program.cs** file in your folder with a simple "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

1. <span data-ttu-id="ad1af-110">Geben Sie im Terminalfenster den folgenden Befehl ein, um das Programm „Hello World“ auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-110">In the terminal window, type the following command to run the "Hello World" program.</span></span> 

    ```
    dotnet run
    ```

    <span data-ttu-id="ad1af-111">Im Terminalfenster wird „Hello World!“</span><span class="sxs-lookup"><span data-stu-id="ad1af-111">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="ad1af-112">als Ausgabe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ad1af-112">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="ad1af-113">Verbinden der App mit Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ad1af-113">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="ad1af-114">Melden Sie sich bei Azure an, indem Sie auf **Ansicht** > **Befehlspalette** klicken und **Azure: Sign In** eingeben.</span><span class="sxs-lookup"><span data-stu-id="ad1af-114">Sign in to Azure by clicking **View** > **Command Palette** and typing **Azure: Sign In**.</span></span>

    <span data-ttu-id="ad1af-115">Folgen Sie den Anweisungen, um den bereitgestellten Code zu kopieren und in den Webbrowser einzufügen, wodurch Ihre Visual Studio Code-Sitzung authentifiziert wird.</span><span class="sxs-lookup"><span data-stu-id="ad1af-115">Follow the prompts to copy and paste the code provided in the web browser, which authenticates your Visual Studio Code session.</span></span>

1. <span data-ttu-id="ad1af-116">Klicken Sie im Menü links auf das ![Azure-Symbol](../media/2-setup/visual-studio-code-explorer-icon.png) **Azure**-Symbol, und erweitern Sie dann **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ad1af-116">Click the ![Azure icon](../media/2-setup/visual-studio-code-explorer-icon.png) **Azure** icon on the left menu, and then expand **Azure Cosmos DB**.</span></span>

1. <span data-ttu-id="ad1af-117">Erweitern Sie „Azure-Abonnement“ > „Azure Cosmos DB-Konto“.</span><span class="sxs-lookup"><span data-stu-id="ad1af-117">Expand your Azure subscription > Azure Cosmos DB account.</span></span> <span data-ttu-id="ad1af-118">Wenn Sie in den vorherigen Modulen die Datenbank **Products** und die Sammlung **Clothing** erstellt haben, werden diese in der Erweiterung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ad1af-118">If you created the **Products** database and **Clothing** collection in the previous modules, the extension displays them.</span></span>

   ![Azure Cosmos DB-Erweiterung in Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

1. <span data-ttu-id="ad1af-120">Erstellen wir jetzt eine neue Datenbank und Sammlung für Ihre Kunden.</span><span class="sxs-lookup"><span data-stu-id="ad1af-120">Now let's create a new database and collection for your customers.</span></span>

    <span data-ttu-id="ad1af-121">Klicken Sie im Azure-Fenster mit der rechten Maustaste auf Ihr Konto, und klicken Sie dann auf **Datenbank erstellen**.</span><span class="sxs-lookup"><span data-stu-id="ad1af-121">In the Azure window, right-click your account, and then click **Create Database**.</span></span>
    
    <span data-ttu-id="ad1af-122">Geben Sie im Textfeld im oberen Bildschirmbereich als Datenbankname **Users** ein, und gehen Sie dann folgendermaßen vor: **EINGABETASTE** > **WebCustomers** für den Sammlungsnamen > **EINGABETASTE** > **userId** für den Partitionsschlüssel > **EINGABETASTE** > **1000** für die anfängliche Durchsatzkapazität > **EINGABETASTE**.</span><span class="sxs-lookup"><span data-stu-id="ad1af-122">In the text box at the top of the screen, type **Users** for the database name > **Enter** > **WebCustomers** for the collection name > **Enter** > **userId** for the partition key > **Enter** > **1000** for the initial throughput capacity > **Enter**.</span></span>

    ![Azure Cosmos DB-Erweiterung in Visual Studio Code](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) 

    <span data-ttu-id="ad1af-124">Die neue Datenbank „Users“ und die Sammlung „WebCustomers“ werden im Explorer-Fenster angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ad1af-124">The new Users database and WebCustomers collection are displayed in the Explorer window.</span></span>

1. <span data-ttu-id="ad1af-125">Führen Sie im integrierten Terminal jeden der folgenden Befehle an einer neuen Eingabeaufforderung aus, um die erforderlichen NuGet-Pakete zu installieren.</span><span class="sxs-lookup"><span data-stu-id="ad1af-125">In the integrated terminal, run each of the following commands at a new prompt to install the required NuGet packages.</span></span>

    ```
    dotnet add package System.Net.Http
    dotnet add package System.Configuration
    dotnet add package System.Configuration.ConfigurationManager
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

1. <span data-ttu-id="ad1af-126">Klicken Sie oben im Explorer-Bereich auf **Program.cs**, um die Datei zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-126">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

1. <span data-ttu-id="ad1af-127">Fügen Sie nach `using System;` die folgenden using-Anweisungen hinzu.</span><span class="sxs-lookup"><span data-stu-id="ad1af-127">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="ad1af-128">Erstellen Sie eine neue Datei namens „App.config“ im Ordner „learning-module“, und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="ad1af-128">Create a new file named App.config in the learning-module folder, and add the following code.</span></span>
  
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. <span data-ttu-id="ad1af-129">Kopieren Sie Ihre Verbindungszeichenfolge aus der Azure Cosmos DB-Erweiterung, indem Sie mit der rechten Maustaste auf das learning-module-Konto und dann auf **Verbindungszeichenfolge kopieren** klicken.</span><span class="sxs-lookup"><span data-stu-id="ad1af-129">Copy your connection string from the Azure Cosmos DB extension by right-clicking the learning-module account, and clicking **Copy Connection String**.</span></span>

1. <span data-ttu-id="ad1af-130">Fügen Sie die Verbindungszeichenfolge in eine Textdatei ein, und kopieren Sie den **AccountEndpoint**-Abschnitt aus der Textdatei in **accountEndpoint** in „App.config“.</span><span class="sxs-lookup"><span data-stu-id="ad1af-130">Paste the connection string into a text file, and then copy the **AccountEndpoint** portion from the text file into the **accountEndpoint** in App.config.</span></span>

    <span data-ttu-id="ad1af-131">„accountEndpoint“ sollte wie im folgenden Code aussehen:</span><span class="sxs-lookup"><span data-stu-id="ad1af-131">The accountEndpoint should look like the following code:</span></span>

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

1. <span data-ttu-id="ad1af-132">Kopieren Sie jetzt den Wert für **AccountKey** aus dem Textwert in den Wert **accountKey** in „App.config“.</span><span class="sxs-lookup"><span data-stu-id="ad1af-132">Now copy the **AccountKey** value from the text value into the **accountKey** value in App.config.</span></span>

1. <span data-ttu-id="ad1af-133">Geben Sie im integrierten Terminal den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-133">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

1. <span data-ttu-id="ad1af-134">Fügen Sie eine neue asynchrone Aufgabe zum Erstellen eines neuen Clients hinzu, und überprüfen Sie, ob die Datenbank „Users“ vorhanden ist, indem Sie die folgende Methode nach der main-Methode hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-134">Add a new asynchronous task to create a new client, and check whether the Users database exists by adding the following method after the main method.</span></span>
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpointUrl"]), ConfigurationManager.AppSettings["primaryKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

1. <span data-ttu-id="ad1af-135">Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-135">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

1. <span data-ttu-id="ad1af-136">Kopieren Sie den folgenden Code, und fügen Sie ihn in die **Main**-Methode ein. Überschreiben Sie hierbei die aktuelle `Console.WriteLine("Hello World!");`-Zeile.</span><span class="sxs-lookup"><span data-stu-id="ad1af-136">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

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

1. <span data-ttu-id="ad1af-137">Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="ad1af-137">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="ad1af-138">Auf der Konsole wird nun Folgendes ausgegeben:</span><span class="sxs-lookup"><span data-stu-id="ad1af-138">The console displays the following output.</span></span>
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a><span data-ttu-id="ad1af-139">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="ad1af-139">Summary</span></span>

<span data-ttu-id="ad1af-140">In dieser Einheit haben Sie das Fundament für Ihre Azure Cosmos DB-Anwendung gelegt.</span><span class="sxs-lookup"><span data-stu-id="ad1af-140">In this unit, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="ad1af-141">Sie haben Ihre Entwicklungsumgebung in Visual Studio Code eingerichtet, ein einfaches Hello World-Projekt erstellt, das Projekt mit dem Azure Cosmos DB-Endpunkt verbunden und sichergestellt, dass Ihre Datenbank und Ihre Sammlung vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="ad1af-141">You set up your development environment in Visual Studio Code, created a simple HelloWorld project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>