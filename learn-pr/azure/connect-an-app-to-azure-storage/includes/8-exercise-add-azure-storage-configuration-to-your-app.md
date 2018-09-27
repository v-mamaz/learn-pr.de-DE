<span data-ttu-id="d6bb2-101">::: Zone Pivot = "Csharp" Im Folgenden fügen wir unserer .NET Core-Anwendung Unterstützung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-101">::: zone pivot="csharp" Let's add support to our .NET core application to retrieve a connection string from a configuration file.</span></span> <span data-ttu-id="d6bb2-102">Als Erstes fügen wir die benötigte Infrastruktur zum Verwalten der Konfiguration in einer JSON-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-102">We'll start by adding the necessary plumbing to manage configuration in a JSON file.</span></span>

## <a name="create-a-json-configuration-file"></a><span data-ttu-id="d6bb2-103">Erstellen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="d6bb2-103">Create a JSON configuration file</span></span>

1. <span data-ttu-id="d6bb2-104">Wechseln Sie mit `cd` in das Verzeichnis „PhotoSharingApp“, wenn Sie dieses nicht bereits aufgerufen haben.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-104">`cd` to the PhotoSharingApp directory if you aren't already there.</span></span>

1. <span data-ttu-id="d6bb2-105">Verwenden Sie das Tool `touch` über die Befehlszeile, um eine Datei mit dem Namen **appsettings.json** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-105">Use the `touch` tool on the command line to create a file named **appsettings.json**.</span></span>

    ```bash
    touch appsettings.json
    ```

1. <span data-ttu-id="d6bb2-106">Öffnen Sie das Projekt in einem Editor.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-106">Open the project in an editor.</span></span> <span data-ttu-id="d6bb2-107">Wenn Sie lokal arbeiten, können Sie einen beliebigen Editor verwenden.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-107">If you are working locally, use your editor of choice.</span></span> <span data-ttu-id="d6bb2-108">Empfohlen wird die erweiterbare, plattformübergreifende IDE **Visual Studio Code**.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-108">We recommend **Visual Studio Code**, which is an extensible cross-platform IDE.</span></span> <span data-ttu-id="d6bb2-109">Wenn Sie in Cloud Shell arbeiten, wird der Cloud Shell-Editor empfohlen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-109">If you are working in the Cloud Shell, we recommend the Cloud Shell editor.</span></span> <span data-ttu-id="d6bb2-110">Der folgende Befehl funktioniert in beiden Editoren.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-110">The following command works for both.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="d6bb2-111">Wählen Sie die Datei **appsettings.json** im Editor aus, und fügen Sie den folgenden Text hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-111">Select the **appsettings.json** file in the editor and add the following text.</span></span> <span data-ttu-id="d6bb2-112">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-112">Save the file.</span></span> <span data-ttu-id="d6bb2-113">Im Cloud Shell-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-113">In the Cloud Shell editor, there is a menu in the top right corner that has common file operations.</span></span>

    ```json
    {
      "StorageAccountConnectionString": "<value>"
    }
    ```

1. <span data-ttu-id="d6bb2-114">Nun müssen Sie die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-114">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span> <span data-ttu-id="d6bb2-115">Führen Sie in Cloud Shell den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-115">In Cloud Shell run the following command.</span></span>

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name <name> \
        --query connectionString
    ```

1. <span data-ttu-id="d6bb2-116">Kopieren Sie die Verbindungszeichenfolge, die von diesem Befehl zurückgegeben wird, und ersetzen Sie `"<value>"` in der Datei **appsettings.json** durch diese Verbindungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-116">Copy the connection string that is returned from that command, and replace `"<value>"` in the **appsettings.json** file with this connection string.</span></span> <span data-ttu-id="d6bb2-117">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-117">Save the file.</span></span>

1. <span data-ttu-id="d6bb2-118">Öffnen Sie als Nächstes die Projektdatei (**PhotoSharingApp.csproj**) im Editor.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-118">Next, open the project file (**PhotoSharingApp.csproj**) in the editor.</span></span>

1. <span data-ttu-id="d6bb2-119">Fügen Sie den folgenden Konfigurationsblock hinzu, um die neue Datei in das Projekt einzuschließen und sie in den Ausgabeordner zu kopieren.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-119">Add the following configuration block to include the new file in the project and copy it to the output folder.</span></span> <span data-ttu-id="d6bb2-120">Dadurch wird sichergestellt, dass die App-Konfigurationsdatei beim Kompilieren/Erstellen der App im Ausgabeverzeichnis abgelegt wird.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-120">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

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

1. <span data-ttu-id="d6bb2-121">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-121">Save the file.</span></span> <span data-ttu-id="d6bb2-122">(Andernfalls gehen die Änderungen verloren, wenn Sie das Paket weiter unten hinzufügen!)</span><span class="sxs-lookup"><span data-stu-id="d6bb2-122">(Make sure you do this or you will lose the change when you add the package below!)</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="d6bb2-123">Hinzufügen von Unterstützung zum Lesen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="d6bb2-123">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="d6bb2-124">Eine .NET Core-Anwendung benötigt zusätzliche NuGet-Pakete, um eine JSON-Konfigurationsdatei zu lesen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-124">A .NET Core application requires additional NuGet packages to read a JSON configuration file.</span></span>

1. <span data-ttu-id="d6bb2-125">Fügen Sie im Eingabeaufforderungsabschnitt des Fensters einen Verweis auf das NuGet-Paket **Microsoft.Extensions.Configuration.Json** hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-125">In the command prompt section of the window, add a reference to the  **Microsoft.Extensions.Configuration.Json** NuGet package.</span></span>

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="d6bb2-126">Hinzufügen von Code zum Lesen der Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="d6bb2-126">Add code to read the configuration file</span></span>

<span data-ttu-id="d6bb2-127">Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Konsolenanwendung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-127">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="d6bb2-128">Wählen Sie im Editor die Datei **Program.cs** aus.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-128">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="d6bb2-129">Die Datei enthält am Anfang eine Zeile **using System;**.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-129">At the top of the file, a **using System;** line is present.</span></span> <span data-ttu-id="d6bb2-130">Fügen Sie unter dieser Zeile die folgenden Codezeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="d6bb2-130">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="d6bb2-131">Ersetzen Sie den Inhalt der **Main**-Methode durch den nachstehenden Code.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-131">Replace the contents of the **Main** method with the following code.</span></span> <span data-ttu-id="d6bb2-132">Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-132">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

<span data-ttu-id="d6bb2-133">Ihre Datei **Program.cs** sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="d6bb2-133">Your **Program.cs** file should now look like the following:</span></span>

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

<span data-ttu-id="d6bb2-134">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="d6bb2-134">::: zone-end</span></span>

<span data-ttu-id="d6bb2-135">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="d6bb2-135">::: zone pivot="javascript"</span></span>

<span data-ttu-id="d6bb2-136">Als Nächstes fügen Sie der Node.js-Anwendung Unterstützung zum Abrufen einer Verbindungszeichenfolge aus einer Konfigurationsdatei hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-136">Let's add support to our Node.js application to retrieve a connection string from a configuration file.</span></span> <span data-ttu-id="d6bb2-137">Als Erstes fügen wir die benötigte Infrastruktur zum Verwalten der Konfiguration über die JavaScript-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-137">We'll start by adding the necessary plumbing to manage configuration from our JavaScript file.</span></span>

## <a name="create-a-env-configuration-file"></a><span data-ttu-id="d6bb2-138">Erstellen einer ENV-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="d6bb2-138">Create a .env configuration file</span></span>

1. <span data-ttu-id="d6bb2-139">Vergewissern Sie sich, dass Sie das richtige Arbeitsverzeichnis Ihres Projekts ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-139">Make sure you are in the correct working directory for your project.</span></span>

1. <span data-ttu-id="d6bb2-140">Verwenden Sie das Tool `touch` über die Befehlszeile, um eine Datei mit der Erweiterung **ENV** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-140">Use the `touch` tool on the command line to create a file named **.env**.</span></span>

    ```bash
    touch .env
    ```

1. <span data-ttu-id="d6bb2-141">Öffnen Sie das Projekt im Cloud Shell-Editor.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-141">Open the project in the Cloud Shell editor.</span></span>

    ```bash
    code .
    ```

1. <span data-ttu-id="d6bb2-142">Wählen Sie die **ENV**-Datei im Editor aus, und fügen Sie den folgenden Text hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-142">Select the **.env** file in the editor and add the following text.</span></span> <span data-ttu-id="d6bb2-143">Sie müssen möglicherweise auf die Aktualisierungsschaltfläche im Code klicken, damit die neuen Dateien angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-143">You may need to click the refresh button in code to see the new files.</span></span> <span data-ttu-id="d6bb2-144">Speichern Sie die Datei. Im Online-Editor steht in der oberen rechten Ecke ein Menü mit gängigen Dateivorgängen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-144">Save the file - in the online editor, there is a menu in the top right corner which has common file operations.</span></span>

    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > <span data-ttu-id="d6bb2-145">Der Wert **AZURE_STORAGE_CONNECTION_STRING** ist eine hartcodierte Umgebungsvariable, die für Storage-APIs zum Suchen nach Zugriffsschlüsseln verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-145">The **AZURE_STORAGE_CONNECTION_STRING** value is a hard-coded environment variable used for Storage APIs to look up access keys.</span></span> <span data-ttu-id="d6bb2-146">Sie können einen eigenen Namen verwenden, müssen diesen jedoch angeben, wenn Sie das `BlobService`-Objekt in Ihrer Node.js-App erstellen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-146">You can use your own name if you prefer, but you must supply the name to the when you create the `BlobService` object in your Node.js app.</span></span>

1. <span data-ttu-id="d6bb2-147">Nun müssen Sie die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-147">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span> <span data-ttu-id="d6bb2-148">Führen Sie in Cloud Shell den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-148">In Cloud Shell run the following command.</span></span>

    ```azurecli
    az storage account show-connection-string \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name <name> \
        --query connectionString
    ```

1. <span data-ttu-id="d6bb2-149">Kopieren Sie die Verbindungszeichenfolge, die von diesem Befehl zurückgegeben wird (ohne die Anführungszeichen), und ersetzen Sie `<value>` in der **ENV**-Datei durch diese Verbindungszeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-149">Copy the connection string that is returned from that command, minus the quotes, and replace `<value>` in the **.env** file with this connection string.</span></span>

1. <span data-ttu-id="d6bb2-150">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-150">Save the file.</span></span>

## <a name="add-support-to-read-an-environment-configuration-file"></a><span data-ttu-id="d6bb2-151">Hinzufügen von Unterstützung zum Lesen einer Umgebungskonfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="d6bb2-151">Add support to read an environment configuration file</span></span>

<span data-ttu-id="d6bb2-152">Sie können Node.js-Apps Unterstützung zum Lesen aus der **ENV**-Datei hinzufügen, indem Sie ihnen das **dotenv**-Paket hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-152">Node.js apps can include support to read from the **.env** file by adding the **dotenv** package.</span></span>

1. <span data-ttu-id="d6bb2-153">Fügen Sie im Eingabeaufforderungsabschnitt des Fensters mithilfe von `npm` eine Abhängigkeit vom \*dotenv\*\*-Paket hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-153">In the command prompt section of the window, add a dependency to the  *dotenv*\* package using `npm`.</span></span>

    ```bash
    npm install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="d6bb2-154">Hinzufügen von Code zum Lesen der Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="d6bb2-154">Add code to read the configuration file</span></span>

<span data-ttu-id="d6bb2-155">Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Anwendung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-155">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our application.</span></span>

1. <span data-ttu-id="d6bb2-156">Wählen Sie im Editor *index.js*\* aus.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-156">Select *index.js*\* in the editor.</span></span>

1. <span data-ttu-id="d6bb2-157">Die Datei enthält am Anfang eine Zeile **#!/usr/bin/env node**.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-157">At the top of the file, a **#!/usr/bin/env node** line is present.</span></span> <span data-ttu-id="d6bb2-158">Fügen Sie unterhalb dieser Zeile eine `require`-Anweisung zum Laden des **dotenv**-Pakets hinzu.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-158">Underneath that line, add a `require` statement to load the **dotenv** package.</span></span> <span data-ttu-id="d6bb2-159">Dadurch werden die in der **ENV**-Datei definierten Umgebungsvariablen für das Programm verfügbar gemacht.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-159">This will make environment variables defined in our **.env** file available to the program.</span></span>

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    ```
<span data-ttu-id="d6bb2-160">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="d6bb2-160">::: zone-end</span></span>

<span data-ttu-id="d6bb2-161">Nachdem wir diese Vorbereitungsschritte durchgeführt haben, können wir mit dem Hinzufügen von Code zur Verwendung unseres Speicherkontos beginnen.</span><span class="sxs-lookup"><span data-stu-id="d6bb2-161">Now that we have that all wired up, we can start adding code to use our storage account.</span></span>