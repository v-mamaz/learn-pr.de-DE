In diesem Modul erstellen Sie eine einfache Konsolen-App mit dem integrierten Terminal, installieren NuGet-Pakete und verwenden die Azure Cosmos DB-Erweiterung, um die im vorherigen Modul erstellten Datenbanken und Sammlungen anzuzeigen. Sie rufen Ihre Azure Cosmos DB-Verbindungszeichenfolge aus der Erweiterung ab und beginnen mit dem Konfigurieren der Verbindung mit Azure Cosmos DB, um Ihre Benutzerdatenbank zu erstellen.

## <a name="create-a-console-app"></a>Erstellen einer Konsolen-App

1. Öffnen Sie Visual Studio Code, und wählen Sie **Datei** > **Ordner öffnen** aus.

1. Erstellen Sie einen neuen Ordner für Ihr neues C#-Projekt, und klicken Sie dann auf **Ordner auswählen**.

1. Vergewissern Sie sich, dass das automatisches Speichern aktiviert ist, indem Sie auf das Menü „Datei“ klicken und überprüfen, ob **Automatisch speichern** leer ist.

1. Öffnen Sie das integrierte Terminal aus Visual Studio Code, indem Sie im Hauptmenü **Ansicht** > **Terminal** auswählen.

1. Geben Sie im Terminalfenster den folgenden Befehl ein.

    ```
    dotnet new console
    ```

    Mit diesem Befehl wird eine Datei **Program.cs** in Ihrem Ordner erstellt, die ein bereits geschriebenes einfaches Programm „Hello World“ enthält, gemeinsam mit einem C#-Projekt namens **learning-module.csproj**.

1. Geben Sie im Terminalfenster den folgenden Befehl ein, um das Programm „Hello World“ auszuführen. 

    ```
    dotnet run
    ```

    Im Terminalfenster wird „Hello World!“ als Ausgabe angezeigt.

## <a name="connect-the-app-to-azure-cosmos-db"></a>Verbinden der App mit Azure Cosmos DB

1. Melden Sie sich bei Azure an, indem Sie auf **Ansicht** > **Befehlspalette** klicken und **Azure: Sign In** eingeben.

    Folgen Sie den Anweisungen, um den bereitgestellten Code zu kopieren und in den Webbrowser einzufügen, wodurch Ihre Visual Studio Code-Sitzung authentifiziert wird.

1. Klicken Sie im Menü links auf das ![Azure-Symbol](../media/2-setup/visual-studio-code-explorer-icon.png) **Azure**-Symbol, und erweitern Sie dann **Azure Cosmos DB**.

1. Erweitern Sie „Azure-Abonnement“ > „Azure Cosmos DB-Konto“. Wenn Sie in den vorherigen Modulen die Datenbank **Products** und die Sammlung **Clothing** erstellt haben, werden diese in der Erweiterung angezeigt.

   ![Azure Cosmos DB-Erweiterung in Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

1. Erstellen wir jetzt eine neue Datenbank und Sammlung für Ihre Kunden.

    Klicken Sie im Azure-Fenster mit der rechten Maustaste auf Ihr Konto, und klicken Sie dann auf **Datenbank erstellen**.
    
    Geben Sie im Textfeld im oberen Bildschirmbereich als Datenbankname **Users** ein, und gehen Sie dann folgendermaßen vor: **EINGABETASTE** > **WebCustomers** für den Sammlungsnamen > **EINGABETASTE** > **userId** für den Partitionsschlüssel > **EINGABETASTE** > **1000** für die anfängliche Durchsatzkapazität > **EINGABETASTE**.

    ![Azure Cosmos DB-Erweiterung in Visual Studio Code](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) 

    Die neue Datenbank „Users“ und die Sammlung „WebCustomers“ werden im Explorer-Fenster angezeigt.

1. Führen Sie im integrierten Terminal jeden der folgenden Befehle an einer neuen Eingabeaufforderung aus, um die erforderlichen NuGet-Pakete zu installieren.

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

1. Klicken Sie oben im Explorer-Bereich auf **Program.cs**, um die Datei zu öffnen.

1. Fügen Sie nach `using System;` die folgenden using-Anweisungen hinzu.

    ```csharp
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

1. Erstellen Sie eine neue Datei namens „App.config“ im Ordner „learning-module“, und fügen Sie den folgenden Code hinzu.
  
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. Kopieren Sie Ihre Verbindungszeichenfolge aus der Azure Cosmos DB-Erweiterung, indem Sie mit der rechten Maustaste auf das learning-module-Konto und dann auf **Verbindungszeichenfolge kopieren** klicken.

1. Fügen Sie die Verbindungszeichenfolge in eine Textdatei ein, und kopieren Sie den **AccountEndpoint**-Abschnitt aus der Textdatei in **accountEndpoint** in „App.config“.

    „accountEndpoint“ sollte wie im folgenden Code aussehen:

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

1. Kopieren Sie jetzt den Wert für **AccountKey** aus dem Textwert in den Wert **accountKey** in „App.config“.

1. Geben Sie im integrierten Terminal den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.

    ```csharp
    dotnet run
    ```

1. Fügen Sie eine neue asynchrone Aufgabe zum Erstellen eines neuen Clients hinzu, und überprüfen Sie, ob die Datenbank „Users“ vorhanden ist, indem Sie die folgende Methode nach der main-Methode hinzufügen.
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpointUrl"]), ConfigurationManager.AppSettings["primaryKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

1. Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.

    ```csharp
    dotnet run
    ```

1. Kopieren Sie den folgenden Code, und fügen Sie ihn in die **Main**-Methode ein. Überschreiben Sie hierbei die aktuelle `Console.WriteLine("Hello World!");`-Zeile.

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

1. Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.

    ```csharp
    dotnet run
    ```

    Auf der Konsole wird nun Folgendes ausgegeben:
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie das Fundament für Ihre Azure Cosmos DB-Anwendung gelegt. Sie haben Ihre Entwicklungsumgebung in Visual Studio Code eingerichtet, ein einfaches Hello World-Projekt erstellt, das Projekt mit dem Azure Cosmos DB-Endpunkt verbunden und sichergestellt, dass Ihre Datenbank und Ihre Sammlung vorhanden sind.