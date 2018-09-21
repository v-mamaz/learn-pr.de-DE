<!--TODO: explain Etag in knowledge needed-->

<span data-ttu-id="9c3e0-101">Nach dem Herstellen der Verbindung mit Azure Cosmos DB besteht der nächste Schritt darin, die in der Datenbank gespeicherten Dokumente zu erstellen, zu lesen, zu ersetzen und zu löschen.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-101">Once the connection to Azure Cosmos DB has been made, the next step is to create, read, replace, and delete the documents that are stored in the database.</span></span> <span data-ttu-id="9c3e0-102">In dieser Einheit erstellen Sie Benutzerdokumente in Ihrer WebCustomer-Sammlung.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-102">In this unit, you will create User documents in your WebCustomer collection.</span></span> <span data-ttu-id="9c3e0-103">Anschließend rufen Sie diese anhand der ID ab, ersetzen sie und löschen sie.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-103">Then, you'll retrieve them by ID, replace them, and delete them.</span></span>

## <a name="working-with-documents-programmatically"></a><span data-ttu-id="9c3e0-104">Programmgesteuertes Arbeiten mit Dokumenten</span><span class="sxs-lookup"><span data-stu-id="9c3e0-104">Working with documents programmatically</span></span>

<span data-ttu-id="9c3e0-105">Daten werden in Azure Cosmos DB als JSON-Dokumente gespeichert.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-105">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="9c3e0-106">[Dokumente](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) können im Portal erstellt, abgerufen, ersetzt oder gelöscht werden, und zwar wie im vorherigen Modul oder wie in diesem Modul beschrieben programmgesteuert.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-106">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="9c3e0-107">Azure Cosmos DB bietet clientseitige SDKs für .NET, .NET Core, Java, Node.js und Python, die diese Vorgänge unterstützen.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-107">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="9c3e0-108">In diesem Modul wird das .NET Core SDK verwendet, um CRUD-Vorgänge (Create, Retrieve, Update, Delete – Erstellen, Abrufen, Aktualisieren, Löschen) für die in Azure Cosmos DB gespeicherten NoSQL-Daten auszuführen.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-108">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations on the NoSQL data stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="9c3e0-109">Die wichtigsten Vorgänge für Azure Cosmos DB-Dokumente sind Teil der Klasse [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):</span><span class="sxs-lookup"><span data-stu-id="9c3e0-109">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="9c3e0-110">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="9c3e0-110">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="9c3e0-111">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="9c3e0-111">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="9c3e0-112">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="9c3e0-112">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="9c3e0-113">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="9c3e0-113">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="9c3e0-114">Upsert führt einen Vorgang zum Erstellen oder Ersetzen durch, je nachdem, ob das Dokument bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-114">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="9c3e0-115">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="9c3e0-115">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="9c3e0-116">Um diese Vorgänge auszuführen, müssen Sie eine Klasse erstellen, die das in der Datenbank gespeicherte Objekt darstellt.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-116">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="9c3e0-117">Da Sie mit einer Datenbank von Benutzern arbeiten, sollten Sie eine **User**-Klasse erstellen, um primäre Daten wie den Vor- und Nachnamen sowie die Benutzer-ID (diese ist erforderlich, da sie der Partitionsschlüssel für die horizontale Skalierung ist) zu speichern, sowie Unterklassen für die Versandeinstellungen und den Bestellverlauf.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-117">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their first name, last name, and user id (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="9c3e0-118">Nachdem Sie die Klassen, die Ihre Benutzer darstellen, erstellt haben, erstellen Sie neue Benutzerdokumente für jede Instanz und führen dann einige einfache CRUD-Operationen für die Dokumente durch.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-118">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="9c3e0-119">Erstellen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="9c3e0-119">Create documents</span></span>

1. <span data-ttu-id="9c3e0-120">Erstellen Sie zunächst eine **User**-Klasse, die die Objekte zum Speichern in Azure Cosmos DB darstellt.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-120">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="9c3e0-121">Außerdem werden die Unterklassen **OrderHistory** und **ShippingPreference** erstellt, die in **User** verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-121">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="9c3e0-122">Beachten Sie, dass Dokumente eine **Id**-Eigenschaft enthalten müssen, die in JSON als **id** serialisiert wird.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-122">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span>

    <span data-ttu-id="9c3e0-123">Um diese Klassen zu erstellen, kopieren Sie die folgenden Klassen **User**, **OrderHistory**, **ShippingPreference** und fügen Sie unterhalb der Methode **BasicOperations** ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-123">To create these classes, copy and paste the following **User**, **OrderHistory**, and **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

    ```csharp
    public class User
    {
        [JsonProperty("id")]
        public string Id { get; set; }
        [JsonProperty("userId")]
        public string UserId { get; set; }
        [JsonProperty("lastName")]
        public string LastName { get; set; }
        [JsonProperty("firstName")]
        public string FirstName { get; set; }
        [JsonProperty("email")]
        public string Email { get; set; }
        [JsonProperty("dividend")]
        public string Dividend { get; set; }
        [JsonProperty("OrderHistory")]
        public OrderHistory[] OrderHistory { get; set; }
        [JsonProperty("ShippingPreference")]
        public ShippingPreference[] ShippingPreference { get; set; }
        [JsonProperty("CouponsUsed")]
        public CouponsUsed[] Coupons { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class OrderHistory
    {
        public string OrderId { get; set; }
        public string DateShipped { get; set; }
        public string Total { get; set; }
    }

    public class ShippingPreference
    {
        public int Priority { get; set; }
        public string AddressLine1 { get; set; }
        public string AddressLine2 { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string ZipCode { get; set; }
        public string Country { get; set; }
    }

    public class CouponsUsed
    {
        public string CouponCode { get; set; }

    }

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. <span data-ttu-id="9c3e0-124">Geben Sie im integrierten Terminal den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-124">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

1. <span data-ttu-id="9c3e0-125">Kopieren Sie jetzt die Aufgabe **CreateUserDocumentIfNotExists**, und fügen Sie diese unter der Funktion **WriteToConsoleAndPromptToContinue** am Ende der Datei „Program.cs“ ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-125">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **WriteToConsoleAndPromptToContinue** function at the end of the Program.cs file.</span></span>

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("User {0} already exists in the database", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="9c3e0-126">Kehren Sie dann zur Methode **BasicOperations** zurück, und fügen Sie Folgendes am Ende der Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-126">Then, return to the **BasicOperations** method and add the following to the end of that method.</span></span>

    ```csharp
    User yanhe = new User
    {
        Id = "1",
        UserId = "yanhe",
        LastName = "He",
        FirstName = "Yan",
        Email = "yanhe@contoso.com",
        OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
            ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);

    User nelapin = new User
    {
        Id = "2",
        UserId = "nelapin",
        LastName = "Pindakova",
        FirstName = "Nela",
        Email = "nelapin@contoso.com",
        Dividend = "8.50",
        OrderHistory = new OrderHistory[]
        {
            new OrderHistory {
                OrderId = "1001",
                DateShipped = "08/17/2018",
                Total = "105.89"
            }
        },
         ShippingPreference = new ShippingPreference[]
        {
            new ShippingPreference {
                    Priority = 1,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            },
            new ShippingPreference {
                    Priority = 2,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            }
        },
        Coupons = new CouponsUsed[]
        {
            new CouponsUsed{
                CouponCode = "Fall2018"
            }
        }
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

1. <span data-ttu-id="9c3e0-127">Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-127">In the integrated terminal, again, type the following command to run the program.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="9c3e0-128">Im Terminal wird jeweils eine Ausgabe angezeigt, während die Anwendung die einzelnen neuen Benutzerdokumente erstellt.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-128">The terminal will display output as the application creates each new user document.</span></span> <span data-ttu-id="9c3e0-129">Drücken Sie eine beliebige Taste, um die Anwendung zu beenden.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-129">Press any key to complete the program.</span></span>

    ```output
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="9c3e0-130">Lesen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="9c3e0-130">Read documents</span></span>

1. <span data-ttu-id="9c3e0-131">Um Dokumente aus der Datenbank zu lesen, kopieren Sie den folgenden Code, und fügen Sie ihn nach der WriteToConsoleAndPromptToContinue-Methode in die Datei „Program.cs“ ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-131">To read documents from the database, copy in the following code and place after the WriteToConsoleAndPromptToContinue method in the Program.cs file.</span></span>

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("Read user {0}", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not read", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="9c3e0-132">Kopieren Sie den folgenden Code, und fügen Sie ihn am Ende der Methode **BasicOperations** nach der Zeile `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-132">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="9c3e0-133">Geben Sie im integrierten Terminal den folgenden Befehl zum Ausführen des Programms ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-133">In the integrated terminal, type the following command to run the program.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="9c3e0-134">Das Terminal zeigt die folgende Ausgabe an, wobei die Ausgabe „Read user 1“ angibt, dass das Dokument abgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-134">The terminal displays the following output, where the output "Read user 1" indicates the document was retrieved.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a><span data-ttu-id="9c3e0-135">Ersetzen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="9c3e0-135">Replace documents</span></span>

<span data-ttu-id="9c3e0-136">Azure Cosmos DB unterstützt das Ersetzen von JSON-Dokumenten.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-136">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="9c3e0-137">In diesem Fall wird ein Benutzerdatensatz aktualisiert, um eine Änderung an den Nachnamen zu berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-137">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="9c3e0-138">Kopieren Sie die Methode **ReplaceFamilyDocument**, und fügen Sie sie nach der ReadUserDocument-Methode in die Datei „Program.cs“ ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-138">Copy and paste the **ReplaceFamilyDocument** method after the ReadUserDocument method in the Program.cs file.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, User updatedUser)
    {
        try
        {
            await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, updatedUser.Id), updatedUser, new RequestOptions { PartitionKey = new PartitionKey(updatedUser.UserId) });
            this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", updatedUser.LastName);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for replacement", updatedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="9c3e0-139">Kopieren Sie den folgenden Code, und fügen Sie ihn am Ende der Methode **BasicOperations** nach der Zeile `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-139">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="9c3e0-140">Führen Sie im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-140">In the integrated terminal, run the following command.</span></span>

    ```bash
    dotnet run
    ```
    <span data-ttu-id="9c3e0-141">Das Terminal zeigt die folgende Ausgabe an, wobei „Replaced last name for Suh“ angibt, dass das Dokument ersetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-141">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a><span data-ttu-id="9c3e0-142">Löschen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="9c3e0-142">Delete documents</span></span>

1. <span data-ttu-id="9c3e0-143">Kopieren Sie die Methode **DeleteUserDocument**, und fügen Sie sie unterhalb der Methode **ReplaceUserDocument** ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-143">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>

    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, User deletedUser)
    {
        try
        {
            await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, deletedUser.Id), new RequestOptions { PartitionKey = new PartitionKey(deletedUser.UserId) });
            Console.WriteLine("Deleted user {0}", deletedUser.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for deletion", deletedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="9c3e0-144">Kopieren Sie den folgenden Code, und fügen Sie ihn am Ende der Methode **BasicOperations** ein.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-144">Copy and paste the following code in the end of the **BasicOperations** method.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="9c3e0-145">Führen Sie im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-145">In the integrated terminal, run the following command.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="9c3e0-146">Im Terminal wird die folgende Ausgabe angezeigt, wobei die Ausgabe „Deleted user 1“ (Benutzer 1 gelöscht) angibt, dass das Dokument gelöscht wurde.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-146">The terminal displays the following output, where the output "Deleted user 1" indicates the document was deleted.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    Deleted user 1
    End of demo, press any key to exit.
    ```

<span data-ttu-id="9c3e0-147">In dieser Einheit haben Sie Dokumente in Ihrer Azure Cosmos DB-Datenbank erstellt, ersetzt und gelöscht.</span><span class="sxs-lookup"><span data-stu-id="9c3e0-147">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>
