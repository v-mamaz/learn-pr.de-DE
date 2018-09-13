<span data-ttu-id="821b5-101">In dieser Einheit rufen Sie den Zugriffsschlüssel ab und fügen ihn Ihrer App-Konfiguration hinzu.</span><span class="sxs-lookup"><span data-stu-id="821b5-101">In this unit you will retrieve the access key and add it to your app configuration.</span></span> <span data-ttu-id="821b5-102">Da wir eine .NET Core-Konsolenanwendung erstellt haben, müssen wir darüber hinaus der Anwendung Unterstützung für das Lesen von Konfigurationsdateien hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="821b5-102">In addition, since we created a .NET Core console application, we need to add support for reading from configuration files to the application.</span></span>

## <a name="create-a-json-configuration-file"></a><span data-ttu-id="821b5-103">Erstellen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="821b5-103">Create a JSON configuration file</span></span>

1. <span data-ttu-id="821b5-104">Klicken Sie im Visual Studio-Projekt, das wir in der vorherigen Einheit erstellt haben, mit der rechten Maustaste auf das Projekt, und wählen Sie **Hinzufügen** und dann **Neues Element** aus (oder drücken Sie STRG+UMSCHALT+A).</span><span class="sxs-lookup"><span data-stu-id="821b5-104">In your Visual Studio project that we created in the previous unit, right click the project, select **Add**, and then select **New Item** (or hold down CTRL-SHIFT-A).</span></span>

1. <span data-ttu-id="821b5-105">Ein modales Dialogfeld wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="821b5-105">A modal dialog is presented.</span></span> <span data-ttu-id="821b5-106">Wählen Sie **JavaScript-JSON-Konfigurationsdatei** aus, geben Sie **appsettings.json** in das Textfeld *Name* ein, und klicken Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="821b5-106">Select **JavaScript JSON Configuration File** and type **appsettings.json** into the *Name* textbox, and then click **Add**.</span></span>

  ![App-Einstellungen](..\media-draft\7-appsettings.png)

1. <span data-ttu-id="821b5-108">Eine Datei wird mit Inhalt, der etwa wie folgt aussieht, dem Projekt hinzugefügt:</span><span class="sxs-lookup"><span data-stu-id="821b5-108">A file is added to the project with contents similar to the following:</span></span>

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
1. <span data-ttu-id="821b5-109">Entfernen Sie den Eintrag **exclude** sowie die zugehörigen Inhalte, und ersetzen Sie ihn durch einen einzelnen Eintrag **StorageAccountConnectionString** mit einem leeren Zeichenfolgenwert.</span><span class="sxs-lookup"><span data-stu-id="821b5-109">Remove the **exclude** entry and its associated contents and replace it with the single entry **StorageAccountConnectionString**, with an empty string value.</span></span> <span data-ttu-id="821b5-110">Es sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="821b5-110">It should look similar to the following:</span></span>

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```
1. <span data-ttu-id="821b5-111">Wählen Sie die Datei **appsettings.json** aus, klicken Sie mit der rechten Maustaste darauf, und wählen Sie **Eigenschaften** aus (drücken Sie alternativ ALT+EINGABE oder F4).</span><span class="sxs-lookup"><span data-stu-id="821b5-111">Select the **appsettings.json** file, right click it and select **Properties** (alternatively, press ALT+ENTER or F4).</span></span>

1. <span data-ttu-id="821b5-112">Ändern Sie **In Ausgabeverzeichnis kopieren** in **Kopieren, wenn neuer**.</span><span class="sxs-lookup"><span data-stu-id="821b5-112">Change **Copy to Output Directory** to **Copy if newer**.</span></span>

  ![Buildvorgang](..\media-draft\7-build-action.png)

  > <span data-ttu-id="821b5-114">Dadurch wird sichergestellt, dass die App-Konfigurationsdatei in das Ausgabeverzeichnis aufgenommen wird, wenn die App kompiliert/erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="821b5-114">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="821b5-115">Hinzufügen von Unterstützung zum Lesen einer JSON-Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="821b5-115">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="821b5-116">Einer .NET Core-Konsolenanwendung müssen bestimmte Bibliotheken hinzugefügt werden, damit sie problemlos eine JSON-Konfigurationsdatei lesen kann.</span><span class="sxs-lookup"><span data-stu-id="821b5-116">A .NET Core console application requires certain libraries to be added to allow it to easily read from a JSON configuration file.</span></span>

1. <span data-ttu-id="821b5-117">Klicken Sie mit der rechten Maustaste auf das Projekt, und wählen Sie **NuGet-Pakete verwalten...** aus.</span><span class="sxs-lookup"><span data-stu-id="821b5-117">Right click on the project and select **Manage Nuget Packages…**.</span></span>

![NuGet-Pakete verwalten](..\media-draft\5-manage-nuget-packages.png)

1. <span data-ttu-id="821b5-119">Daraufhin wird eine Seite angezeigt, auf der die zu diesem Zeitpunkt installierten NuGet-Pakete aufgeführt sind.</span><span class="sxs-lookup"><span data-stu-id="821b5-119">A page is displayed, showing currently installed Nuget packages.</span></span> <span data-ttu-id="821b5-120">Klicken Sie auf die Option **Durchsuchen**, und geben Sie **Microsoft.Extensions.Configuration.Json** in das Suchfeld ein.</span><span class="sxs-lookup"><span data-stu-id="821b5-120">Click on the **Browse** option and type **Microsoft.Extensions.Configuration.Json** in the search field.</span></span> <span data-ttu-id="821b5-121">Das Paket **Microsoft.Extensions.Configuration.Json** wird in den Suchergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="821b5-121">The **Microsoft.Extensions.Configuration.Json** package is displayed in the search results.</span></span>

1. <span data-ttu-id="821b5-122">Wählen Sie das Paket **Microsoft.Extensions.Configuration.Json** und im rechten Bereich **Installieren** aus.</span><span class="sxs-lookup"><span data-stu-id="821b5-122">Select the **Microsoft.Extensions.Configuration.Json** package, and in the right pane select **Install**.</span></span>

1. <span data-ttu-id="821b5-123">Ein Dialogfeld **Vorschau der Änderungen** wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="821b5-123">A **Preview Changes** dialog is displayed.</span></span> <span data-ttu-id="821b5-124">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="821b5-124">Click **OK**.</span></span>

1. <span data-ttu-id="821b5-125">Ein Dialogfeld zur Zustimmung zur Lizenz wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="821b5-125">A license acceptance dialog is displayed.</span></span> <span data-ttu-id="821b5-126">Klicken Sie auf **I Accept** (Annehmen).</span><span class="sxs-lookup"><span data-stu-id="821b5-126">Click **I Accept**.</span></span>


## <a name="read-from-the-configuration-file"></a><span data-ttu-id="821b5-127">Lesen der Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="821b5-127">Read from the configuration file</span></span>

<span data-ttu-id="821b5-128">Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Konsolenanwendung aktivieren.</span><span class="sxs-lookup"><span data-stu-id="821b5-128">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="821b5-129">Suchen Sie die Datei **Program.cs** in Ihrem Projekt, und öffnen Sie sie in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="821b5-129">Locate the **Program.cs** file in your project and open it in Visual Studio.</span></span>

1. <span data-ttu-id="821b5-130">Am Anfang der Datei befindet sich die Zeile **using System;**.</span><span class="sxs-lookup"><span data-stu-id="821b5-130">At the top of the file, a **using System;** line is present.</span></span> <span data-ttu-id="821b5-131">Fügen Sie unter dieser Zeile die folgenden Codezeilen hinzu:</span><span class="sxs-lookup"><span data-stu-id="821b5-131">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="821b5-132">Ersetzen Sie den Inhalt der Methode **Main** durch folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="821b5-132">Replace the contents of the **Main** method with the following code:</span></span>

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

1. <span data-ttu-id="821b5-133">Ihre Datei **Program.cs** sollte jetzt wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="821b5-133">Your **Program.cs** file should now look like the following:</span></span>

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

> <span data-ttu-id="821b5-134">Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.</span><span class="sxs-lookup"><span data-stu-id="821b5-134">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

## <a name="add-your-connection-string-to-the-configuration-file"></a><span data-ttu-id="821b5-135">Hinzufügen der Verbindungszeichenfolge zur Konfigurationsdatei</span><span class="sxs-lookup"><span data-stu-id="821b5-135">Add your connection string to the configuration file</span></span>

<span data-ttu-id="821b5-136">Nun müssen wir die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen.</span><span class="sxs-lookup"><span data-stu-id="821b5-136">Now we need to get the storage account connection string and place it into the configuration for our app.</span></span>

1. <span data-ttu-id="821b5-137">Navigieren Sie zum Azure-Portal für Ihr Abonnement, das Ihr Speicherkonto enthält.</span><span class="sxs-lookup"><span data-stu-id="821b5-137">Navigate to the Azure portal for your subscription that contains your storage account.</span></span>

1. <span data-ttu-id="821b5-138">Navigieren Sie zum Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="821b5-138">Navigate to your storage account.</span></span>

1. <span data-ttu-id="821b5-139">Navigieren Sie zum Blatt „Kontoschlüssel“ des Speicherkontos im Portal.</span><span class="sxs-lookup"><span data-stu-id="821b5-139">Navigate to the Account Keys blade of the storage account in the portal.</span></span>

1. <span data-ttu-id="821b5-140">Kopieren Sie die Verbindungszeichenfolge **key1**.</span><span class="sxs-lookup"><span data-stu-id="821b5-140">Copy the **key1** connection string.</span></span>

1. <span data-ttu-id="821b5-141">Fügen Sie den Inhalt des Zugriffsschlüssels, den Sie aus dem Portal kopiert haben, als Wert für **StorageAccountConnectionString** ein.</span><span class="sxs-lookup"><span data-stu-id="821b5-141">Paste in the contents of the access key you copied from the portal as the value for **StorageAccountConnectionString**.</span></span> <span data-ttu-id="821b5-142">Die Konfiguration sollte nun etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="821b5-142">Your configuration should now look similar to the following:</span></span>

    ```json
    {
      "StorageAccountConnectionString": "your-access-key-connection-string-goes-here"
    }
    ```
