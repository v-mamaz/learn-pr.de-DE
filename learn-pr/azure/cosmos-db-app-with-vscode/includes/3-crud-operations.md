<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


<span data-ttu-id="35e9c-101">Daten werden als JSON-Dokumente in Azure Cosmos DB gespeichert.</span><span class="sxs-lookup"><span data-stu-id="35e9c-101">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="35e9c-102">[Dokumente](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) können im Portal erstellt, abgerufen, ersetzt oder gelöscht werden, und zwar wie im vorherigen Modul oder wie in diesem Modul beschrieben programmgesteuert.</span><span class="sxs-lookup"><span data-stu-id="35e9c-102">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="35e9c-103">Azure Cosmos DB bietet clientseitige SDKs für .NET, .NET Core, Java, Node.js und Python, die alle diese Vorgänge unterstützen.</span><span class="sxs-lookup"><span data-stu-id="35e9c-103">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="35e9c-104">In diesem Modul wird das .NET Core SDK zum Ausführen von CRUD-Vorgängen (Create, Retrieve, Update, Delete – Erstellen, Abrufen, Aktualisieren, Löschen) verwendet.</span><span class="sxs-lookup"><span data-stu-id="35e9c-104">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations.</span></span> 

<span data-ttu-id="35e9c-105">Die wichtigsten Vorgänge für Azure Cosmos DB-Dokumente sind Teil der [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet)-Klasse:</span><span class="sxs-lookup"><span data-stu-id="35e9c-105">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="35e9c-106">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="35e9c-106">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="35e9c-107">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="35e9c-107">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="35e9c-108">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="35e9c-108">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="35e9c-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="35e9c-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="35e9c-110">Upsert führt einen Vorgang zum Erstellen oder Ersetzen durch, je nachdem, ob das Dokument bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="35e9c-110">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="35e9c-111">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="35e9c-111">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="35e9c-112">Um diese Vorgänge auszuführen, müssen Sie eine Klasse erstellen, die das in der Datenbank gespeicherte Objekt darstellt.</span><span class="sxs-lookup"><span data-stu-id="35e9c-112">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="35e9c-113">Da wir mit einer Datenbank von Benutzern arbeiten, sollten Sie eine **User**-Klasse erstellen, um primäre Daten wie „name“ und „UserId“ zu speichern (diese sind erforderlich, da dies der Partitionsschlüssel zur horizontalen Skalierung ist), und Unterklassen für die Versandeinstellungen und den Bestellverlauf.</span><span class="sxs-lookup"><span data-stu-id="35e9c-113">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their name and UserId (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="35e9c-114">Nachdem Sie diese Klassen, die Ihre Benutzer darstellen, erstellt haben, erstellen Sie neue Benutzerdokumente für jede Instanz und führen dann einige einfache CRUD-Vorgänge für die Dokumente durch.</span><span class="sxs-lookup"><span data-stu-id="35e9c-114">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="35e9c-115">Erstellen eines Dokuments</span><span class="sxs-lookup"><span data-stu-id="35e9c-115">Create documents</span></span>

1. <span data-ttu-id="35e9c-116">Erstellen Sie zunächst eine **User**-Klasse, die die Objekte zum Speichern in Azure Cosmos DB darstellt.</span><span class="sxs-lookup"><span data-stu-id="35e9c-116">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="35e9c-117">Außerdem werden die Unterklassen **OrderHistory** und **ShippingPreference** erstellt, die in **User** verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="35e9c-117">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="35e9c-118">Beachten Sie, dass Dokumente eine **Id**-Eigenschaft enthalten müssen, die in JSON als **id** serialisiert wird.</span><span class="sxs-lookup"><span data-stu-id="35e9c-118">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> 

    <span data-ttu-id="35e9c-119">Um diese Klassen zu erstellen, kopieren Sie die folgenden Klassen **User**, **OrderHistory**, **ShippingPreference** und fügen Sie unterhalb der Methode **BasicOperations** ein.</span><span class="sxs-lookup"><span data-stu-id="35e9c-119">To create these classes, copy and paste the following **User**, **OrderHistory**, **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

    <!--TODO: specify JSON for all of these? -->
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
            public OrderHistory[] OrderHistory { get; set; }
            public ShippingPreference[] ShippingPreference { get; set; }
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

2. <span data-ttu-id="35e9c-120">Geben Sie im integrierten Terminal den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="35e9c-120">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

3. <span data-ttu-id="35e9c-121">Kopieren Sie nun den Task **CreateUserDocumentIfNotExists**, und fügen Sie ihn unter der Klasse **ShippingPreference** ein.</span><span class="sxs-lookup"><span data-stu-id="35e9c-121">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **ShippingPreference** class.</span></span>

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

4. <span data-ttu-id="35e9c-122">Fügen Sie dann Folgendes zur Methode **BasicOperations** hinzu.</span><span class="sxs-lookup"><span data-stu-id="35e9c-122">Then add the following to the **BasicOperations** method.</span></span>

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

5. <span data-ttu-id="35e9c-123">Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.</span><span class="sxs-lookup"><span data-stu-id="35e9c-123">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="35e9c-124">Das Terminal zeigt die folgende Ausgabe an, die angibt, dass beide Benutzerdatensätze erfolgreich erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="35e9c-124">The terminal displays the following output, indicating that both user records were successfully created.</span></span> 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="35e9c-125">Lesen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="35e9c-125">Read documents</span></span>

1. <span data-ttu-id="35e9c-126">Um Dokumente aus der Datenbank zu lesen, kopieren Sie den folgenden Code, und fügen Sie ihn am Ende der Datei „Program.cs“ ein.</span><span class="sxs-lookup"><span data-stu-id="35e9c-126">To read documents from the database, copy in the following code and place it at the end of the Program.cs file.</span></span>

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
                this.WriteToConsoleAndPromptToContinue("User {0} not found", user.Id);
            }
            else
            {
                throw;
            }
            }
    }
    ```

2.  <span data-ttu-id="35e9c-127">Kopieren Sie den folgenden Code, und fügen Sie ihn an das Ende der **BasicOperations**-Methode nach der Zeile `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` ein.</span><span class="sxs-lookup"><span data-stu-id="35e9c-127">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. <span data-ttu-id="35e9c-128">Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="35e9c-128">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="35e9c-129">Das Terminal zeigt die folgende Ausgabe an, wobei die Ausgabe „Found user 1“ angibt, dass das Dokument gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="35e9c-129">The terminal displays the following output, where the output "Found user 1" indicates the document was found.</span></span>

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

## <a name="replace-documents"></a><span data-ttu-id="35e9c-130">Ersetzen von Dokumenten</span><span class="sxs-lookup"><span data-stu-id="35e9c-130">Replace documents</span></span>
<span data-ttu-id="35e9c-131">Azure Cosmos DB unterstützt das Ersetzen von JSON-Dokumenten.</span><span class="sxs-lookup"><span data-stu-id="35e9c-131">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="35e9c-132">In diesem Fall wird ein Benutzerdatensatz aktualisiert, um eine Änderung an den Nachnamen zu berücksichtigen.</span><span class="sxs-lookup"><span data-stu-id="35e9c-132">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="35e9c-133">Kopieren Sie die **ReplaceFamilyDocument**-Methode, und fügen Sie sie unterhalb der **CreateUserDocumentIfNotExists**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="35e9c-133">Copy and paste the **ReplaceFamilyDocument** method underneath your **CreateUserDocumentIfNotExists** method.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. <span data-ttu-id="35e9c-134">Kopieren Sie den folgenden Code, und fügen Sie ihn an das Ende der **BasicOperations**-Methode nach der Zeile `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` ein.</span><span class="sxs-lookup"><span data-stu-id="35e9c-134">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. <span data-ttu-id="35e9c-135">Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="35e9c-135">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="35e9c-136">Das Terminal zeigt die folgende Ausgabe an, wobei die Ausgabe „Replaced last name for Suh“ angibt, dass das Dokument ersetzt wurde.</span><span class="sxs-lookup"><span data-stu-id="35e9c-136">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

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

## <a name="delete-documents"></a><span data-ttu-id="35e9c-137">Dokumente löschen</span><span class="sxs-lookup"><span data-stu-id="35e9c-137">Delete documents</span></span>

1. <span data-ttu-id="35e9c-138">Kopieren Sie die **DeleteUserDocument**-Methode, und fügen Sie sie unterhalb der **ReplaceUserDocument**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="35e9c-138">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. <span data-ttu-id="35e9c-139">Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb der zweiten Abfrageausführung in die **BasicOperations**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="35e9c-139">Copy and paste the following code to your **BasicOperations** method underneath the second query execution.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. <span data-ttu-id="35e9c-140">Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="35e9c-140">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="35e9c-141">Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="35e9c-141">Congratulations!</span></span> <span data-ttu-id="35e9c-142">Sie haben erfolgreich ein Azure Cosmos DB-Dokument gelöscht.</span><span class="sxs-lookup"><span data-stu-id="35e9c-142">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a name="summary"></a><span data-ttu-id="35e9c-143">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="35e9c-143">Summary</span></span>

<span data-ttu-id="35e9c-144">In dieser Einheit haben Sie Dokumente in Ihrer Azure Cosmos DB-Datenbank erstellt, ersetzt und gelöscht.</span><span class="sxs-lookup"><span data-stu-id="35e9c-144">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>