<span data-ttu-id="f3132-101">In dieser Übung laden Sie die Verbindungszeichenfolge des Azure Storage-Kontos aus der Konfiguration, und Sie verwenden diese zum Herstellen einer Verbindung mit dem Azure Storage-Konto.</span><span class="sxs-lookup"><span data-stu-id="f3132-101">In this exercise, you'll load the Azure Storage account connection string from configuration and use it to connect to the Azure Storage account.</span></span>

## <a name="retrieve-the-connection-string"></a><span data-ttu-id="f3132-102">Abrufen der Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="f3132-102">Retrieve the connection string</span></span>

1. <span data-ttu-id="f3132-103">Stellen Sie sicher, dass die Konsolenanwendung aus der vorherigen Einheit in Visual Studio geladen ist.</span><span class="sxs-lookup"><span data-stu-id="f3132-103">Ensure the console application from the previous unit is loaded into Visual Studio.</span></span>
1. <span data-ttu-id="f3132-104">Fügen Sie am Anfang der Datei **Program.cs** eine *using*-Anweisung hinzu, um die **Microsoft.WindowsAzure.Storage**-Bibliothek zu referenzieren.</span><span class="sxs-lookup"><span data-stu-id="f3132-104">In the **Program.cs** file, add a *using* statement at the top of the file to reference the **Microsoft.WindowsAzure.Storage** library:</span></span>
    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. <span data-ttu-id="f3132-105">Fügen Sie die folgende Zeile am Ende der **Main**-Methode hinzu, um die Verbindungszeichenfolge des Azure Storage-Kontos aus der Konfigurationsdatei abzurufen:</span><span class="sxs-lookup"><span data-stu-id="f3132-105">At the bottom of the **Main** method, add the following line to retrieve the Azure Storage account connection string from the configuration file:</span></span>
    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a><span data-ttu-id="f3132-106">Erstellen eines Blobclients</span><span class="sxs-lookup"><span data-stu-id="f3132-106">Create a blob client</span></span>

1. <span data-ttu-id="f3132-107">Fügen Sie den folgenden Code am Ende der **Main**-Methode ein, um die Verbindungszeichenfolge zu analysieren und einen Blobclient zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="f3132-107">Insert the following code at the bottom of the **Main** method to parse the connection string and create a blob client:</span></span>
    ```csharp
    CloudStorageAccount storageAccount;
    if (!CloudStorageAccount.TryParse(connectionString,out storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```
1. <span data-ttu-id="f3132-108">Fügen Sie den folgenden Code ein, um einen Blobclient zu erstellen und einen Verweis auf einen Container abzurufen. Optional erstellen Sie diesen, wenn er nicht am Ende der **Main**-Methode vorhanden ist:</span><span class="sxs-lookup"><span data-stu-id="f3132-108">Insert the following code to create a blob client and retrieve a reference to a container, optionally creating it if it does not exist at the bottom of the **Main** method:</span></span>
    ```csharp
    var containerName = "MyBlobContainer";
    var success = blobClient
        .GetContainerReference(containerName)
        .CreateIfNotExistsAsync()
        .Result;
    ```

  <span data-ttu-id="f3132-109">*Beachten Sie die Verwendung der **async**-Methode **CreateIfNotExistsAsync()** und die entsprechende **Ergebniseigenschaft**. In einer typischen Anwendung würde normalerweise das Schlüsselwort **await** verwendet werden. Allerdings ist diese Anwendung eine Konsolenanwendung, die nicht asynchron ist, weshalb die **Ergebniseigenschaft** aufgerufen werden muss, um die Ergebnisse der asynchronen Aufgabe abzurufen, die von der Methode **CreateIfNotExistsAsync()** erstellt wurde.*</span><span class="sxs-lookup"><span data-stu-id="f3132-109">*Note the use of the **async** method **CreateIfNotExistsAsync()** and corresponding **Result** property. In a typical application, we would normally use the **await** keyword. However, this application a console application and is not async, we need to call the **Result** property to get the results of the async task created by the **CreateIfNotExistsAsync()** method.*</span></span>

## <a name="print-a-status-message"></a><span data-ttu-id="f3132-110">Ausgeben einer Statusmeldung</span><span class="sxs-lookup"><span data-stu-id="f3132-110">Print a status message</span></span>

1. <span data-ttu-id="f3132-111">Fügen Sie den folgenden Code am Ende der **Main**-Methode hinzu, um eine Erfolgs- oder Fehlermeldung auszugeben.</span><span class="sxs-lookup"><span data-stu-id="f3132-111">Add the following code at the bottom of the **Main** method to print a success or failure message.</span></span>
    ```csharp
    if (!success)
    {
        Console.WriteLine("Error: Could not connect to Azure Storage container");
        return;
    }
    Console.WriteLine("Successfully connected to Azure Storage container");
    ```
1. <span data-ttu-id="f3132-112">Führen Sie abschließend die Anwendung aus, um zu überprüfen, ob die Verbindung erfolgreich hergestellt wurde, und sehen Sie sich das Azure-Portal an, um sicherzustellen, dass der Speichercontainer erstellt wurde, sofern dieser zuvor nicht vorhanden war.</span><span class="sxs-lookup"><span data-stu-id="f3132-112">Finally, run the application to verify that a successful connection is made, and view the Azure Portal to ensure the Storage container is created if it did not exist previously.</span></span>
1. <span data-ttu-id="f3132-113">**Optional:** Wenn Sie nicht vorhaben, den Container zu verwenden, löschen Sie die Ressourcengruppe, in der der Container gespeichert ist, um sicherzustellen, dass keine Kosten für Ressourcen anfallen, die Sie nicht verwenden.</span><span class="sxs-lookup"><span data-stu-id="f3132-113">**Optional**: If you don't plan on using the container, delete the resource group where the container is located to ensure you are not charged for resources you are not using.</span></span>


