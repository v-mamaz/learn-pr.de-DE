<!--TODO: explain Etag in knowledge needed-->

<span data-ttu-id="de32e-101">Nach der Verbindung mit Azure Cosmos DB besteht der nächste Schritt darin, die Datenbankdokumente zu erstellen, zu lesen, zu ersetzen und zu löschen.</span><span class="sxs-lookup"><span data-stu-id="de32e-101">Once the connection to Azure Cosmos DB has been made, the next step is to create, read, replace and delete the documents that are stored in the database.</span></span> <span data-ttu-id="de32e-102">In diesem Modul erstellen Sie in Ihrer WebCustomer-Sammlung Benutzerdokumente, rufen sie über die ID ab, ersetzen sie und löschen sie anschließend.</span><span class="sxs-lookup"><span data-stu-id="de32e-102">In this module, you will create User documents in your WebCustomer collection, then you'll retrieve them by ID, replace them, and delete them.</span></span>

## <a name="working-with-documents-programmatically"></a><span data-ttu-id="de32e-103">Programmgesteuertes Arbeiten mit Dokumenten</span><span class="sxs-lookup"><span data-stu-id="de32e-103">Working with documents programmatically</span></span>

<span data-ttu-id="de32e-104">Daten werden in Azure Cosmos DB als JSON-Dokumente gespeichert.</span><span class="sxs-lookup"><span data-stu-id="de32e-104">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="de32e-105">[Dokumente](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) können im Portal erstellt, abgerufen, ersetzt oder gelöscht werden, und zwar wie im vorherigen Modul oder wie in diesem Modul beschrieben programmgesteuert.</span><span class="sxs-lookup"><span data-stu-id="de32e-105">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="de32e-106">Azure Cosmos DB bietet clientseitige SDKs für .NET, .NET Core, Java, Node.js und Python, die alle diese Vorgänge unterstützen.</span><span class="sxs-lookup"><span data-stu-id="de32e-106">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="de32e-107">In diesem Modul wird das .NET Core SDK zum Ausführen von CRUD-Vorgängen (Create, Retrieve, Update, Delete – Erstellen, Abrufen, Aktualisieren, Löschen) verwendet.</span><span class="sxs-lookup"><span data-stu-id="de32e-107">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations.</span></span> 

<span data-ttu-id="de32e-108">Die wichtigsten Vorgänge für Azure Cosmos DB-Dokumente sind Teil der [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet)-Klasse:</span><span class="sxs-lookup"><span data-stu-id="de32e-108">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="de32e-109">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="de32e-109">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="de32e-110">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="de32e-110">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="de32e-111">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="de32e-111">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="de32e-112">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="de32e-112">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="de32e-113">Upsert führt einen Vorgang zum Erstellen oder Ersetzen durch, je nachdem, ob das Dokument bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="de32e-113">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="de32e-114">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="de32e-114">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="de32e-115">Um diese Vorgänge auszuführen, müssen Sie eine Klasse erstellen, die das in der Datenbank gespeicherte Objekt darstellt.</span><span class="sxs-lookup"><span data-stu-id="de32e-115">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="de32e-116">Da Sie mit einer Datenbank von Benutzern arbeiten, sollten Sie eine **User**-Klasse erstellen, um primäre Daten wie den Vor- und Nachnamen sowie die Benutzer-ID (diese ist erforderlich, da sie der Partitionsschlüssel für die horizontale Skalierung ist) zu speichern, und Unterklassen für die Versandeinstellungen und den Bestellverlauf.</span><span class="sxs-lookup"><span data-stu-id="de32e-116">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their first name, last name and user id (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="de32e-117">Nachdem Sie die Klassen, die Ihre Benutzer darstellen, erstellt haben, erstellen Sie neue Benutzerdokumente für jede Instanz und führen dann einige einfache CRUD-Operationen für die Dokumente durch.</span><span class="sxs-lookup"><span data-stu-id="de32e-117">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="de32e-118">Erstellen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="de32e-118">Create documents</span></span>

1. <span data-ttu-id="de32e-119">Erstellen Sie zunächst eine **User**-Klasse, die die Objekte zum Speichern in Azure Cosmos DB darstellt.</span><span class="sxs-lookup"><span data-stu-id="de32e-119">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="de32e-120">Außerdem werden die Unterklassen **OrderHistory** und **ShippingPreference** erstellt, die in **User** verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="de32e-120">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="de32e-121">Beachten Sie, dass Dokumente eine **Id**-Eigenschaft enthalten müssen, die in JSON als **id** serialisiert wird.</span><span class="sxs-lookup"><span data-stu-id="de32e-121">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span>

    <span data-ttu-id="de32e-122">Um diese Klassen zu erstellen, kopieren Sie die folgenden Klassen **User**, **OrderHistory**, **ShippingPreference** und fügen Sie unterhalb der Methode **BasicOperations** ein.</span><span class="sxs-lookup"><span data-stu-id="de32e-122">To create these classes, copy and paste the following **User**, **OrderHistory**, **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

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

2. <span data-ttu-id="de32e-123">Geben Sie im integrierten Terminal den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="de32e-123">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

3. <span data-ttu-id="de32e-124">Kopieren Sie nun den Task **CreateUserDocumentIfNotExists**, und fügen Sie ihn unter der Klasse **ShippingPreference** ein.</span><span class="sxs-lookup"><span data-stu-id="de32e-124">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **ShippingPreference** class.</span></span>

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found {0}", user.Id);
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

4. <span data-ttu-id="de32e-125">Fügen Sie dann Folgendes zur Methode **BasicOperations** hinzu.</span><span class="sxs-lookup"><span data-stu-id="de32e-125">Then add the following to the **BasicOperations** method.</span></span>

    ```csharp
     User yanhe = new User
                {
                    Id = "1",
                    UserId = "yanhe",
                    LastName = "He",
                    FirstName = "Yan",
                    Email = "yanhe@todo.com",
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
                    Email = "nelapin@todo.com",
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

5. <span data-ttu-id="de32e-126">Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="de32e-126">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="de32e-127">Das Terminal zeigt die folgende Ausgabe an, die angibt, dass beide Benutzerdatensätze erfolgreich erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="de32e-127">The terminal displays the following output, indicating that both user records were successfully created.</span></span>

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="de32e-128">Lesen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="de32e-128">Read documents</span></span>

1. <span data-ttu-id="de32e-129">Um Dokumente aus der Datenbank zu lesen, kopieren Sie den folgenden Code, und fügen Sie ihn am Ende der Datei „Program.cs“ ein.</span><span class="sxs-lookup"><span data-stu-id="de32e-129">To read documents from the database, copy in the following code and place it at the end of the Program.cs file.</span></span>
    <!--TODO: This is not finding the user-->

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found user {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not retrieved", user.Id);
            }
            else
            {
                throw;
            }
            }
    }
    ```

2.  <span data-ttu-id="de32e-130">Kopieren Sie den folgenden Code, und fügen Sie ihn an das Ende der **BasicOperations**-Methode nach der Zeile `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` ein.</span><span class="sxs-lookup"><span data-stu-id="de32e-130">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. <span data-ttu-id="de32e-131">Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="de32e-131">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="de32e-132">Das Terminal zeigt die folgende Ausgabe an, wobei die Ausgabe „Found user 1“ angibt, dass das Dokument gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="de32e-132">The terminal displays the following output, where the output "Found user 1" indicates the document was found.</span></span>

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a><span data-ttu-id="de32e-133">Ersetzen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="de32e-133">Replace documents</span></span>
<span data-ttu-id="de32e-134">Azure Cosmos DB unterstützt das Ersetzen von JSON-Dokumenten.</span><span class="sxs-lookup"><span data-stu-id="de32e-134">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="de32e-135">In diesem Fall wird ein Benutzerdatensatz aktualisiert, um eine Änderung an den Nachnamen zu berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="de32e-135">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="de32e-136">Kopieren Sie die **ReplaceFamilyDocument**-Methode, und fügen Sie diese am Ende der Datei „Program.cs“ ein.</span><span class="sxs-lookup"><span data-stu-id="de32e-136">Copy and paste the **ReplaceFamilyDocument** method at the end of the Program.cs file.</span></span>
    <!--TODO: This is not finding user to replace-->
    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        try
        {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), new RequestOptions { PartitionKey = new PartitionKey("updatedUser.UserId") });
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", updatedUser);
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

2. <span data-ttu-id="de32e-137">Kopieren Sie den folgenden Code, und fügen Sie ihn am Ende der **BasicOperations**-Methode nach der Zeile `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` ein.</span><span class="sxs-lookup"><span data-stu-id="de32e-137">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```

4. <span data-ttu-id="de32e-138">Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="de32e-138">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="de32e-139">Das Terminal zeigt die folgende Ausgabe an, wobei die Ausgabe „Replaced last name for Suh“ angibt, dass das Dokument ersetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="de32e-139">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    Replaced last name for Suh
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a><span data-ttu-id="de32e-140">Löschen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="de32e-140">Delete documents</span></span>

1. <span data-ttu-id="de32e-141">Kopieren Sie die **DeleteUserDocument**-Methode, und fügen Sie sie unterhalb der **ReplaceUserDocument**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="de32e-141">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string id, User deletedUser)
    {
        try
        {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, id), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted user {0}", id);
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

2. <span data-ttu-id="de32e-142">Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb der zweiten Abfrageausführung in die **BasicOperations**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="de32e-142">Copy and paste the following code to your **BasicOperations** method underneath the second query execution.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1", yanhe);
    ```

3. <span data-ttu-id="de32e-143">Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="de32e-143">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="de32e-144">Das Terminal zeigt die folgende Ausgabe an, wobei „Replaced last name for Suh“ darauf hinweist, dass das Dokument ersetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="de32e-144">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    Deleted user 1
    End of demo, press any key to exit.
    ```

    <span data-ttu-id="de32e-145">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="de32e-145">Congratulations!</span></span> <span data-ttu-id="de32e-146">Sie haben erfolgreich ein Azure Cosmos DB-Dokument gelöscht.</span><span class="sxs-lookup"><span data-stu-id="de32e-146">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a name="summary"></a><span data-ttu-id="de32e-147">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="de32e-147">Summary</span></span>

<span data-ttu-id="de32e-148">In dieser Einheit haben Sie Dokumente in Ihrer Azure Cosmos DB-Datenbank erstellt, ersetzt und gelöscht.</span><span class="sxs-lookup"><span data-stu-id="de32e-148">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>