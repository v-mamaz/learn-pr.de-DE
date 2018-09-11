<span data-ttu-id="c0ee7-101">In dieser Übung rufen Sie den Zugriffsschlüssel ab und fügen ihn Ihrer App-Konfiguration hinzu.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-101">In this exercise you will retrieve the access key and add it to your app configuration.</span></span> <span data-ttu-id="c0ee7-102">Da wir eine .NET Core-Konsolenanwendung erstellt haben, müssen wir darüber hinaus Unterstützung für das Lesen von Konfigurationsdateien zur Anwendung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-102">In addition, since we created a .NET Core console application, we need to add support for reading from configuration files to the application.</span></span>

## <a name="create-a-json-configuration-file"></a><span data-ttu-id="c0ee7-103">Erstellen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="c0ee7-103">Create a JSON configuration file</span></span>

1. <span data-ttu-id="c0ee7-104">Klicken Sie im Visual Studio-Projekt, das wir in der vorherigen Einheit erstellt haben, mit der rechten Maustaste auf das Projekt, wählen Sie **Hinzufügen** und dann **Neues Element** aus (oder drücken Sie STRG+UMSCHALT+A).</span><span class="sxs-lookup"><span data-stu-id="c0ee7-104">In your Visual Studio project that we created in the previous unit, right click the project, select **Add**, then select **New Item** (or hold down CTRL-SHIFT-A).</span></span>
1. <span data-ttu-id="c0ee7-105">Ein modales Dialogfeld wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-105">A modal dialog is presented.</span></span> <span data-ttu-id="c0ee7-106">Wählen Sie **JavaScript-JSON-Konfigurationsdatei** aus, und geben Sie **appsettings.json** in das Textfeld *Name* ein. Klicken Sie dann auf **Hinzufügen**.
  ![appsettings](..\media-draft\9-appsettings.png)</span><span class="sxs-lookup"><span data-stu-id="c0ee7-106">Select **JavaScript JSON Configuration File** and type **appsettings.json** into the *Name* textbox, then click **Add**
![appsettings](..\media-draft\9-appsettings.png)</span></span>
1. <span data-ttu-id="c0ee7-107">Eine Datei wird mit Inhalt, der etwa wie folgt aussieht, zum Projekt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="c0ee7-107">A file is added to the project with contents similar to the following:</span></span>
    ```json
    {
      "exclude": [
        "**/bin",
        "**/bower_components",
        "**/jspm_packages",
        "**/node_modules",
        "**/obj",
        "**/platforms"
      ]
    }
    ```
1. <span data-ttu-id="c0ee7-108">Entfernen Sie den Eintrag **exclude** sowie die zugehörigen Inhalte, und ersetzen Sie ihn durch einen einzelnen Eintrag **StorageAccountConnectionString** mit einem leeren Zeichenfolgenwert.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-108">Remove the **exclude** entry and its associated contents and replace with a single entry **StorageAccountConnectionString** with an empty string value.</span></span> <span data-ttu-id="c0ee7-109">Es sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="c0ee7-109">It should look similar to the following:</span></span>
    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```
1. <span data-ttu-id="c0ee7-110">Wählen Sie die Datei **appsettings.json** aus, klicken Sie mit der rechten Maustaste darauf, und wählen Sie **Eigenschaften** aus (drücken Sie alternativ ALT+EINGABE oder F4).</span><span class="sxs-lookup"><span data-stu-id="c0ee7-110">Select the **appsettings.json** file, right click it and select **Properties** (alternatively press ALT+ENTER or F4).</span></span>
1. <span data-ttu-id="c0ee7-111">Ändern Sie **In Ausgabeverzeichnis kopieren** in **Kopieren, wenn neuer**.
  ![Buildvorgang](..\media-draft\10-build-action.png)</span><span class="sxs-lookup"><span data-stu-id="c0ee7-111">Change the **Copy to Output Directory** to **Copy if newer**
![build action](..\media-draft\10-build-action.png)</span></span>

  > <span data-ttu-id="c0ee7-112">Dadurch wird sichergestellt, dass die App-Konfigurationsdatei in das Ausgabeverzeichnis aufgenommen wird, wenn die App kompiliert/erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-112">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="c0ee7-113">Hinzufügen von Unterstützung zum Lesen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="c0ee7-113">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="c0ee7-114">Zu einer .NET Core-Konsolenanwendung müssen bestimmte Bibliotheken hinzugefügt werden, damit sie problemlos eine JSON-Konfigurationsdatei lesen kann.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-114">A .NET Core console application requires certain libraries to be added to allow it to easily read from a JSON configuration file.</span></span>

1. <span data-ttu-id="c0ee7-115">Klicken Sie mit der rechten Maustaste auf das Projekt, und wählen Sie **NuGet-Pakete verwalten** aus.
  ![NuGet-Pakete verwalten](..\media-draft\11-manage-nuget-packages.png)</span><span class="sxs-lookup"><span data-stu-id="c0ee7-115">Right click on the project and select **Manage Nuget Packages …**
![Manage NuGet packages](..\media-draft\11-manage-nuget-packages.png)</span></span>
1. <span data-ttu-id="c0ee7-116">Dann wird eine Seite angezeigt, auf der die zu diesem Zeitpunkt installierten NuGet-Pakete aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-116">A page is displayed showing currently installed Nuget packages.</span></span> <span data-ttu-id="c0ee7-117">Klicken Sie auf die Option **Durchsuchen**, und geben Sie **Microsoft.Extensions.Configuration.Json** in das Suchfeld ein.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-117">Click on the **Browse** option and type in **Microsoft.Extensions.Configuration.Json** in the search field.</span></span> <span data-ttu-id="c0ee7-118">Das Paket **Microsoft.Extensions.Configuration.Json** wird in den Suchergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-118">**Microsoft.Extensions.Configuration.Json** package is displayed in the search results.</span></span>
1. <span data-ttu-id="c0ee7-119">Wählen Sie das Paket **Microsoft.Extensions.Configuration.Json** aus, und wählen Sie im rechten Bereich **Installieren** aus.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-119">Select the **Microsoft.Extensions.Configuration.Json** package and in the right pane select **Install**</span></span>
1. <span data-ttu-id="c0ee7-120">Ein Dialogfeld **Vorschau der Änderungen** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-120">A **Preview Changes** dialog is displayed.</span></span> <span data-ttu-id="c0ee7-121">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-121">Click **OK**</span></span>
1. <span data-ttu-id="c0ee7-122">Ein Dialogfeld „Zustimmung zur Lizenz“ wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-122">A License acceptance dialog is displayed.</span></span> <span data-ttu-id="c0ee7-123">Klicken Sie auf **Ich stimme zu**.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-123">Click **I Accept**</span></span>

## <a name="read-from-the-configuration-file"></a><span data-ttu-id="c0ee7-124">Lesen der Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="c0ee7-124">Read from the configuration file</span></span>

<span data-ttu-id="c0ee7-125">Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Konsolenanwendung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-125">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="c0ee7-126">Suchen Sie die Datei **Program.cs** in Ihrem Projekt, und öffnen Sie sie in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-126">Locate the **Program.cs** file in your project and open it in Visual Studio.</span></span>
1. <span data-ttu-id="c0ee7-127">Am Anfang der Datei ist die Zeile **using System;** vorhanden.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-127">At the top of the file, a **using System;** is present.</span></span> <span data-ttu-id="c0ee7-128">Fügen Sie unter dieser Zeile die folgenden Codezeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="c0ee7-128">Underneath that line, add the following lines of code:</span></span>
    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```
1. <span data-ttu-id="c0ee7-129">Ersetzen Sie den Inhalt der Methode **Main** durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="c0ee7-129">Replace the contents of the **Main** method with the following code:</span></span>
    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```
1. <span data-ttu-id="c0ee7-130">Ihre Datei **Program.cs** sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="c0ee7-130">Your **Program.cs** file should now look like the following:</span></span>
    ```csharp
    using System;
    using Microsoft.Extensions.Configuration;
    using System.IO;

    namespace DemoConsoleApp
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

> <span data-ttu-id="c0ee7-131">Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-131">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

## <a name="add-your-storage-connection-string-to-the-configuration-file"></a><span data-ttu-id="c0ee7-132">Hinzufügen der Speicherverbindungszeichenfolge zur Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="c0ee7-132">Add your Storage connection string to the configuration file</span></span>

<span data-ttu-id="c0ee7-133">Nun müssen wir die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-133">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span>

1. <span data-ttu-id="c0ee7-134">Navigieren Sie zum Azure-Portal für Ihr Abonnement, das Ihr Speicherkonto enthält.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-134">Navigate to the Azure portal for your subscription that contains your storage account.</span></span>
1. <span data-ttu-id="c0ee7-135">Navigieren Sie zum Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-135">Navigate to your storage account.</span></span>
1. <span data-ttu-id="c0ee7-136">Navigieren Sie zum Blatt „Kontoschlüssel“ des Speicherkontos im Portal.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-136">Navigate to the Account Keys blade of the storage account in the portal.</span></span>
1. <span data-ttu-id="c0ee7-137">Kopieren Sie die Verbindungszeichenfolge **key1**.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-137">Copy the **key1** connection string.</span></span>
1. <span data-ttu-id="c0ee7-138">Fügen Sie den Inhalt des Zugriffsschlüssels, den Sie aus dem Portal kopiert haben, als Wert für **StorageAccountConnectionString** ein.</span><span class="sxs-lookup"><span data-stu-id="c0ee7-138">Paste in the contents of the access key you copied from the portal as the value for the **StorageAccountConnectionString**.</span></span> <span data-ttu-id="c0ee7-139">Die Konfiguration sollte nun etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="c0ee7-139">Your configuration should now look similar to the following:</span></span>
    ```json
    {
      "StorageAccountConnectionString": "your-access-key-connection-string-goes-here"
    }
    ```


