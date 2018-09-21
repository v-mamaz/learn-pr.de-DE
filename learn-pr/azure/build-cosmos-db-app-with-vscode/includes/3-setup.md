Mit Visual Studio Code können Sie eine Konsolen-App erstellen, indem Sie das integrierte Terminal und einige kurze Befehle verwenden.

In dieser Einheit erstellen Sie eine einfache Konsolen-App über das integrierte Terminal, rufen Ihre Azure Cosmos DB-Verbindungszeichenfolge aus der Erweiterung ab und konfigurieren anschließend die Verbindung zwischen Ihrer Konsolen-App und Azure Cosmos DB.

## <a name="create-a-console-app"></a>Erstellen einer Konsolen-App

1. Klicken Sie in Visual Studio Code auf **Datei** > **Ordner öffnen**.

1. Erstellen Sie am Speicherort Ihrer Wahl einen neuen Ordner namens `learning-module`, und klicken Sie dann auf **Ordner auswählen**.

1. Vergewissern Sie sich, dass das automatische Speichern aktiviert ist, indem Sie auf das Menü „Datei“ klicken und überprüfen, ob **Automatisch speichern** leer ist. Sie werden mehrere Codeblöcke kopieren. Dadurch wird sichergestellt, dass Sie immer mit den neuesten Versionen Ihrer Dateien arbeiten.

1. Öffnen Sie das integrierte Terminal aus Visual Studio Code, indem Sie im Hauptmenü auf **Ansicht** > **Terminal** klicken.

1. Kopieren Sie den folgenden Befehl, und fügen Sie ihn in das Terminalfenster ein.

    ```bash
    dotnet new console
    ```

    Mit diesem Befehl werden in Ihrem Ordner die Datei **Program.cs** mit einem einfachen Hallo Welt-Programm und eine C#-Projektdatei namens **learning-module.csproj** erstellt.

1. Kopieren Sie den folgenden Befehl, und fügen Sie ihn in das Terminalfenster ein, um das Hallo Welt-Programm auszuführen.

    ```bash
    dotnet run
    ```

    Im Terminalfenster wird „Hello World!“ (Hallo Welt!) als Ausgabe angezeigt.

## <a name="connect-the-app-to-azure-cosmos-db"></a>Herstellen einer Verbindung zwischen der App und Azure Cosmos DB

1. Kopieren Sie den folgenden Befehlsblock, und fügen Sie ihn an der Terminaleingabeaufforderung ein, um die erforderlichen NuGet-Pakete zu installieren.

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

1. Klicken Sie oben im Bereich „Explorer“ auf **Program.cs**, um die Datei zu öffnen.

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

    Wenn eine Meldung zum Hinzufügen von fehlenden erforderlichen Ressourcen angezeigt wird, klicken Sie auf **Ja**.

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

1. Kopieren Sie die Verbindungszeichenfolge, indem Sie zuerst links auf das Azure-Symbol ![Azure-Symbol](../media/2-setup/visual-studio-code-explorer-icon.png) klicken und das Concierge-Abonnement erweitern. Klicken Sie anschließend mit der rechten Maustaste auf Ihr Azure Cosmos DB-Konto und dann auf **Copy Connection String** (Verbindungszeichenfolge kopieren).

1. Fügen Sie die Verbindungszeichenfolge am Ende der Datei „App.config“ ein, kopieren Sie den Abschnitt **AccountEndpoint** aus der Verbindungszeichenfolge, und fügen Sie ihn für den Wert **accountEndpoint** in „App.config“ ein.

    „accountEndpoint“ sollte wie im folgenden Code aussehen:

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

1. Kopieren Sie nun den Wert **AccountKey** aus der Verbindungszeichenfolge in den Wert **accountKey**, und löschen Sie anschließend die ursprüngliche Verbindungszeichenfolge, aus der Sie die Werte kopiert haben.

1. Kopieren Sie den folgenden Befehl, und fügen Sie ihn in die Terminaleingabeaufforderung ein, um das Programm auszuführen.

    ```csharp
    dotnet run
    ```

    Das Programm zeigt „Hello World!“ im Terminal an.

## <a name="create-the-documentclient"></a>Erstellen von DocumentClient

Jetzt ist es Zeit, eine Instanz von DocumentClient zu erstellen. Dies ist die clientseitige Darstellung des Azure Cosmos DB-Diensts. Mit diesem Client werden Anforderungen für den Dienst konfiguriert und ausgeführt.

1. Fügen Sie Folgendes am Anfang der Klasse „Program“ in der Datei „Program.cs“ hinzu.

    ```csharp
    private DocumentClient client;
    ```

1. Fügen Sie eine neue asynchrone Aufgabe zum Erstellen eines neuen Clients hinzu, und überprüfen Sie, ob die Datenbank „Users“ vorhanden ist, indem Sie die folgende Methode nach der `Main`-Methode hinzufügen.

    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["accountEndpoint"]), ConfigurationManager.AppSettings["accountKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });

        Console.WriteLine("Database and collection validation complete");
    }
    ```

1. Kopieren Sie den folgenden Befehl, und fügen Sie ihn erneut im integrierten Terminal zum Ausführen des Programms ein, um sicherzustellen, dass er ausgeführt wird.

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

    In der Konsole wird nun Folgendes ausgegeben:

    ```output
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

In dieser Einheit haben Sie das Fundament für Ihre Azure Cosmos DB-Anwendung gelegt. Sie haben Ihre Entwicklungsumgebung in Visual Studio Code eingerichtet, ein einfaches Hello World-Projekt erstellt, das Projekt mit dem Azure Cosmos DB-Endpunkt verbunden und sichergestellt, dass Ihre Datenbank und Ihre Sammlung vorhanden sind.
