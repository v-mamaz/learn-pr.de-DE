<span data-ttu-id="16e3b-101">::: Zone Pivot = "Csharp" Im Folgenden fügen wir unserer .NET Core-Anwendung Unterstützung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-101">::: zone pivot="csharp" Let's add support to our .NET core application to retrieve a connection string from a configuration file.</span></span> <span data-ttu-id="16e3b-102">Als Erstes fügen wir die benötigte Infrastruktur zum Verwalten der Konfiguration in einer JSON-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-102">We'll start by adding the necessary plumbing to manage configuration in a JSON file.</span></span>

## <a name="create-a-json-configuration-file"></a><span data-ttu-id="16e3b-103">Erstellen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="16e3b-103">Create a JSON configuration file</span></span>

1. <span data-ttu-id="16e3b-104">Vergewissern Sie sich, dass Sie das richtige Arbeitsverzeichnis Ihres Projekts ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="16e3b-104">Make sure you are in the correct working directory for your project.</span></span>

1. <span data-ttu-id="16e3b-105">Verwenden Sie das Tool `touch` in der Befehlszeile, um eine Datei mit dem Namen **appsettings.json** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="16e3b-105">Use the `touch` tool on the command line to create a file named **appsettings.json**.</span></span>

    ```bash
    touch appsettings.json
    ```

1. <span data-ttu-id="16e3b-106">Öffnen Sie das Projekt mit dem interaktiven Editor. Falls Sie lokal arbeiten, verwenden Sie den Editor Ihrer Wahl – wir empfehlen **Visual Studio Code**, eine erweiterbare plattformübergreifende integrierte Entwicklungsumgebung (IDE).</span><span class="sxs-lookup"><span data-stu-id="16e3b-106">Open the project with the interactive editor, if you are working locally, use your editor of choice - we recommend **Visual Studio Code** which is an extensible cross-platform IDE.</span></span> <span data-ttu-id="16e3b-107">Die folgenden Befehle gelten für den Cloud Shell-Editor, sind VS Code aber sehr ähnlich.</span><span class="sxs-lookup"><span data-stu-id="16e3b-107">The following commands are for the Cloud Shell editor, but are very similar to VS Code.</span></span>
    
    ```bash
    code .
    ```

1. <span data-ttu-id="16e3b-108">Wählen Sie die Datei **appsettings.json** im Editor aus, und fügen Sie den folgenden Text hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-108">Select the **appsettings.json** file in the editor and add the following text.</span></span> <span data-ttu-id="16e3b-109">Speichern Sie die Datei. Im Online-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="16e3b-109">Save the file - in the online editor, there is a menu in the top right corner which has common file operations.</span></span>

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```

1. <span data-ttu-id="16e3b-110">Wählen Sie als Nächstes die Projektdatei (**PhotoSharingApp.csproj**) aus, um sie im Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="16e3b-110">Next, select the project file (**PhotoSharingApp.csproj**) to open it in the editor.</span></span>

1. <span data-ttu-id="16e3b-111">Fügen Sie den folgenden Konfigurationsblock hinzu, um die neue Datei in das Projekt einzuschließen und sie in den Ausgabeordner zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="16e3b-111">Add the following configuration block to include the new file in the project and copy it to the output folder.</span></span> <span data-ttu-id="16e3b-112">Dadurch wird sichergestellt, dass die App-Konfigurationsdatei beim Kompilieren/Erstellen der App im Ausgabeverzeichnis abgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="16e3b-112">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
       ...
        <ItemGroup>
            <None Update="appsettings.json">
              <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
            </None>
        </ItemGroup>
    </Project>
    ```

1. <span data-ttu-id="16e3b-113">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="16e3b-113">Save the file.</span></span> <span data-ttu-id="16e3b-114">(Andernfalls gehen die Änderungen verloren, wenn Sie das Paket weiter unten hinzufügen!)</span><span class="sxs-lookup"><span data-stu-id="16e3b-114">(Make sure you do this or you will lose the change when you add the package below!)</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="16e3b-115">Hinzufügen von Unterstützung zum Lesen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="16e3b-115">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="16e3b-116">Eine .NET Core-Anwendung benötigt zusätzliche NuGet-Pakete, um eine JSON-Konfigurationsdatei zu lesen.</span><span class="sxs-lookup"><span data-stu-id="16e3b-116">A .NET Core application requires additional NuGet packages to read a JSON configuration file.</span></span>

1. <span data-ttu-id="16e3b-117">Fügen Sie im Eingabeaufforderungsabschnitt des Fensters einen Verweis auf das NuGet-Paket **Microsoft.Extensions.Configuration.Json** hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-117">In the command prompt section of the window, add a reference to the  **Microsoft.Extensions.Configuration.Json** NuGet package.</span></span>

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="16e3b-118">Hinzufügen von Code zum Lesen der Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="16e3b-118">Add code to read the configuration file</span></span>

<span data-ttu-id="16e3b-119">Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Konsolenanwendung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="16e3b-119">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="16e3b-120">Wählen Sie im Editor die Datei **Program.cs** aus.</span><span class="sxs-lookup"><span data-stu-id="16e3b-120">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="16e3b-121">Die Datei enthält am Anfang eine Zeile **using System;**.</span><span class="sxs-lookup"><span data-stu-id="16e3b-121">At the top of the file, a **using System;** line is present.</span></span> <span data-ttu-id="16e3b-122">Fügen Sie unter dieser Zeile die folgenden Codezeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="16e3b-122">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="16e3b-123">Ersetzen Sie den Inhalt der **Main**-Methode durch den nachstehenden Code.</span><span class="sxs-lookup"><span data-stu-id="16e3b-123">Replace the contents of the **Main** method with the following code.</span></span> <span data-ttu-id="16e3b-124">Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.</span><span class="sxs-lookup"><span data-stu-id="16e3b-124">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

<span data-ttu-id="16e3b-125">Ihre Datei **Program.cs** sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="16e3b-125">Your **Program.cs** file should now look like the following:</span></span>

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace PhotoSharingApp
{
    class Program
    {
        static void Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();            
        }
    }
}
```

<span data-ttu-id="16e3b-126">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="16e3b-126">::: zone-end</span></span>

<span data-ttu-id="16e3b-127">::: zone-pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="16e3b-127">::: zone-pivot="javascript"</span></span>

<span data-ttu-id="16e3b-128">Als Nächstes fügen wir unserer Node.js-Anwendung Unterstützung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-128">Let's add support to our Node.js application to retrieve a connection string from a configuration file.</span></span> <span data-ttu-id="16e3b-129">Als Erstes fügen wir die benötigte Infrastruktur zum Verwalten der Konfiguration über die JavaScript-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-129">We'll start by adding the necessary plumbing to manage configuration from our JavaScript file.</span></span>

## <a name="create-a-env-configuration-file"></a><span data-ttu-id="16e3b-130">Erstellen einer ENV-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="16e3b-130">Create a .env configuration file</span></span>

1. <span data-ttu-id="16e3b-131">Vergewissern Sie sich, dass Sie das richtige Arbeitsverzeichnis Ihres Projekts ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="16e3b-131">Make sure you are in the correct working directory for your project.</span></span>

1. <span data-ttu-id="16e3b-132">Verwenden Sie das Tool `touch` in der Befehlszeile, um eine Datei mit der Erweiterung **.env** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="16e3b-132">Use the `touch` tool on the command line to create a file named **.env**.</span></span>

    ```bash
    touch .env
    ```

1. <span data-ttu-id="16e3b-133">Öffnen Sie das Projekt mit dem interaktiven Editor. Falls Sie lokal arbeiten, verwenden Sie den Editor Ihrer Wahl – wir empfehlen **Visual Studio Code**, eine erweiterbare plattformübergreifende integrierte Entwicklungsumgebung (IDE).</span><span class="sxs-lookup"><span data-stu-id="16e3b-133">Open the project with the interactive editor, if you are working locally, use your editor of choice - we recommend **Visual Studio Code** which is an extensible cross-platform IDE.</span></span> <span data-ttu-id="16e3b-134">Die folgenden Befehle gelten für den Cloud Shell-Editor, sind VS Code aber sehr ähnlich.</span><span class="sxs-lookup"><span data-stu-id="16e3b-134">The following commands are for the Cloud Shell editor, but are very similar to VS Code.</span></span>
    
    ```bash
    code .
    ```

1. <span data-ttu-id="16e3b-135">Wählen Sie die **ENV**-Datei im Editor aus, und fügen Sie den folgenden Text hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-135">Select the **.env** file in the editor and add the following text.</span></span> <span data-ttu-id="16e3b-136">Speichern Sie die Datei. Im Online-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="16e3b-136">Save the file - in the online editor, there is a menu in the top right corner which has common file operations.</span></span>

    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > <span data-ttu-id="16e3b-137">Der Wert **AZURE_STORAGE_CONNECTION_STRING** ist eine hartcodierte Umgebungsvariable, die für Storage-APIs zum Suchen nach Zugriffsschlüsseln verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="16e3b-137">The **AZURE_STORAGE_CONNECTION_STRING** value is a hard-coded environment variable used for Storage APIs to look up access keys.</span></span> <span data-ttu-id="16e3b-138">Sie können einen eigenen Namen verwenden, müssen diesen jedoch angeben, wenn Sie das `BlobService`-Objekt erstellen.</span><span class="sxs-lookup"><span data-stu-id="16e3b-138">You can use your own name if you prefer - but you must supply the name to the when you create the `BlobService` object.</span></span>

1. <span data-ttu-id="16e3b-139">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="16e3b-139">Save the file.</span></span>

## <a name="add-support-to-read-an-environment-configuration-file"></a><span data-ttu-id="16e3b-140">Hinzufügen von Unterstützung zum Lesen einer Umgebungskonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="16e3b-140">Add support to read an environment configuration file</span></span>

<span data-ttu-id="16e3b-141">Sie können Node.js-Apps Unterstützung zum Lesen aus der **ENV**-Datei hinzufügen, indem Sie ihnen das **dotenv**-Paket hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="16e3b-141">Node.js apps can include support to read from the **.env** file by adding the **dotenv** package.</span></span>

1. <span data-ttu-id="16e3b-142">Fügen Sie im Eingabeaufforderungsabschnitt des Fensters eine Abhängigkeit vom \*dotenv\*\*-Paket hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-142">In the command prompt section of the window, add a dependency to the  *dotenv*\* package.</span></span>

    ```bash
    node install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="16e3b-143">Hinzufügen von Code zum Lesen der Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="16e3b-143">Add code to read the configuration file</span></span>

<span data-ttu-id="16e3b-144">Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Anwendung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="16e3b-144">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our application.</span></span>

1. <span data-ttu-id="16e3b-145">Wählen Sie im Editor *index.js*\* aus.</span><span class="sxs-lookup"><span data-stu-id="16e3b-145">Select *index.js*\* in the editor.</span></span>

1. <span data-ttu-id="16e3b-146">Die Datei enthält am Anfang eine Zeile **#!/usr/bin/env node**.</span><span class="sxs-lookup"><span data-stu-id="16e3b-146">At the top of the file, a **#!/usr/bin/env node** line is present.</span></span> <span data-ttu-id="16e3b-147">Fügen Sie unterhalb dieser Zeile eine `require`-Anweisung zum Laden des **dotenv**-Pakets hinzu.</span><span class="sxs-lookup"><span data-stu-id="16e3b-147">Underneath that line, add a `require` statement to load the **dotenv** package.</span></span> <span data-ttu-id="16e3b-148">Dadurch werden die in der **ENV**-Datei definierten Umgebungsvariablen für das Programm verfügbar gemacht.</span><span class="sxs-lookup"><span data-stu-id="16e3b-148">This will make environment variables defined in our **.env** file available to the program.</span></span>

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    ```
<span data-ttu-id="16e3b-149">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="16e3b-149">::: zone-end</span></span>

## <a name="add-the-connection-string-to-the-configuration-file"></a><span data-ttu-id="16e3b-150">Hinzufügen der Verbindungszeichenfolge zur Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="16e3b-150">Add the connection string to the configuration file</span></span>

<span data-ttu-id="16e3b-151">Nun müssen wir die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen.</span><span class="sxs-lookup"><span data-stu-id="16e3b-151">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span>

1. <span data-ttu-id="16e3b-152">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true)an.</span><span class="sxs-lookup"><span data-stu-id="16e3b-152">Sign in to the [Azure Portal](https://portal.azure.com/?azure-portal=true).</span></span>

1. <span data-ttu-id="16e3b-153">Navigieren Sie zu Ihrem Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="16e3b-153">Navigate to your storage account.</span></span> <span data-ttu-id="16e3b-154">Sie können im Abschnitt **Alle Ressourcen** nach dem Speicherkonto suchen oder den Namen in das _Suchfeld_ oben im Portalfenster eingeben.</span><span class="sxs-lookup"><span data-stu-id="16e3b-154">You can use the **All Resources** section to find the storage account, or search by name from the _search box_ at the top of the portal window.</span></span> 

1. <span data-ttu-id="16e3b-155">Wählen Sie im Portal das Blatt **Zugriffsschlüssel** des Speicherkontos aus.</span><span class="sxs-lookup"><span data-stu-id="16e3b-155">Select the **Access Keys** blade of the storage account in the portal.</span></span>

1. <span data-ttu-id="16e3b-156">Kopieren Sie die Verbindungszeichenfolge **key1**.</span><span class="sxs-lookup"><span data-stu-id="16e3b-156">Copy the **key1** Connection string.</span></span>

1. <span data-ttu-id="16e3b-157">Fügen Sie den Inhalt des Zugriffsschlüssels, den Sie aus dem Portal kopiert haben, als Wert der Konfigurationsvariable für die Verbindungszeichenfolge ein.</span><span class="sxs-lookup"><span data-stu-id="16e3b-157">Paste in the contents of the access key you copied from the portal as the value for the connection string configuration variable.</span></span>

<span data-ttu-id="16e3b-158">Die Konfiguration sollte nun etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="16e3b-158">Your configuration should now look similar to the following:</span></span>

<span data-ttu-id="16e3b-159">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="16e3b-159">::: zone pivot="csharp"</span></span>
    ```json
    {
        "StorageAccountConnectionString": "DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net"
    }
    ```
<span data-ttu-id="16e3b-160">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="16e3b-160">::: zone-end</span></span>

<span data-ttu-id="16e3b-161">::: zone-pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="16e3b-161">::: zone-pivot="javascript"</span></span>
    ```
    AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net
    ```
<span data-ttu-id="16e3b-162">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="16e3b-162">::: zone-end</span></span>

<span data-ttu-id="16e3b-163">Nachdem wir diese Vorbereitungsschritte durchgeführt haben, können wir mit dem Hinzufügen von Code zur Verwendung unseres Speicherkontos beginnen.</span><span class="sxs-lookup"><span data-stu-id="16e3b-163">Now that we have that all wired up, we can start adding code to use our storage account.</span></span>