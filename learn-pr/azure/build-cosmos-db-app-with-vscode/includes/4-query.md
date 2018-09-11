<span data-ttu-id="f1952-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Nun, da Sie Dokumente in Ihrer Anwendung erstellt haben, werden wir diese aus Ihrer Anwendung abrufen.</span><span class="sxs-lookup"><span data-stu-id="f1952-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Now that you've created documents in your application, let's query them from your application.</span></span> <span data-ttu-id="f1952-102">Azure Cosmos DB verwendet SQL- und LINQ-Abfragen.</span><span class="sxs-lookup"><span data-stu-id="f1952-102">Azure Cosmos DB uses SQL queries and LINQ queries.</span></span> <span data-ttu-id="f1952-103">Diese Einheit konzentriert sich auf die Ausführung von SQL- und LINQ-Abfragen aus Ihrer Anwendung, im Gegensatz zur Ausführung aus dem Portal.</span><span class="sxs-lookup"><span data-stu-id="f1952-103">This unit focuses on running SQL queries and LINQ queries from your application, as opposed to the portal.</span></span>

<span data-ttu-id="f1952-104">Hierbei werden die für Ihre Anwendung für Onlinehändler erstellten Benutzerdokumente verwendet, um diese Abfragen zu testen.</span><span class="sxs-lookup"><span data-stu-id="f1952-104">We'll use the user documents you've created for your online retailer application to test these queries.</span></span>

## <a name="linq-query-basics"></a><span data-ttu-id="f1952-105">Grundlegendes zu LINQ-Abfragen</span><span class="sxs-lookup"><span data-stu-id="f1952-105">LINQ query basics</span></span>

<span data-ttu-id="f1952-106">LINQ ist ein .NET-Programmiermodell, das Berechnungen als Abfragen für Streams von Objekten darstellt.</span><span class="sxs-lookup"><span data-stu-id="f1952-106">LINQ is a .NET programming model that expresses computations as queries on streams of objects.</span></span> <span data-ttu-id="f1952-107">Sie können ein **IQueryable**-Objekt für die direkte Abfrage von Azure Cosmos DB erstellen, das die LINQ-Abfrage in eine Cosmos DB-Abfrage übersetzt.</span><span class="sxs-lookup"><span data-stu-id="f1952-107">You can create an **IQueryable** object that directly queries Azure Cosmos DB, which translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="f1952-108">Anschließend wird die Abfrage an den Azure Cosmos DB-Server übergeben, um einen Ergebnissatz im JSON-Format abzurufen.</span><span class="sxs-lookup"><span data-stu-id="f1952-108">The query is then passed to the Azure Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="f1952-109">Die zurückgegebenen Ergebnisse werden clientseitig in einen Stream von .NET-Objekten deserialisiert.</span><span class="sxs-lookup"><span data-stu-id="f1952-109">The returned results are deserialized into a stream of .NET objects on the client side.</span></span> <span data-ttu-id="f1952-110">Viele Entwickler bevorzugen LINQ-Abfragen, weil sie ein einziges, konsistentes Programmiermodell für die Arbeit mit Objekten im Anwendungscode und für die Abfragelogik in der Datenbank bieten.</span><span class="sxs-lookup"><span data-stu-id="f1952-110">Many developers prefer LINQ queries, as they provide a single consistent programming model across how they work with objects in application code and how they express query logic running in the database.</span></span>

<span data-ttu-id="f1952-111">Die folgende Tabelle zeigt, wie LINQ-Abfragen in SQL übersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="f1952-111">The following table shows how LINQ queries are translated into SQL.</span></span>

| <span data-ttu-id="f1952-112">LINQ-Ausdruck</span><span class="sxs-lookup"><span data-stu-id="f1952-112">LINQ expression</span></span> | <span data-ttu-id="f1952-113">SQL-Übersetzung</span><span class="sxs-lookup"><span data-stu-id="f1952-113">SQL translation</span></span> |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a><span data-ttu-id="f1952-114">Ausführen von SQL- und LINQ-Abfragen</span><span class="sxs-lookup"><span data-stu-id="f1952-114">Run SQL and LINQ queries</span></span>

1. <span data-ttu-id="f1952-115">Im folgenden Beispiel wird gezeigt, wie eine Abfrage aus Ihrem .NET-Code in SQL, LINQ oder LINQ Lambda ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="f1952-115">The following sample shows how a query could be performed in SQL, LINQ, or LINQ lambda from your .NET code.</span></span> <span data-ttu-id="f1952-116">Kopieren Sie den Code, und fügen Sie ihn ans Ende der „Program.cs“-Datei ein.</span><span class="sxs-lookup"><span data-stu-id="f1952-116">Copy the code and add it to the end of the Program.cs file.</span></span>

    ```csharp
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1, EnableCrossPartitionQuery = true };
    
            // Here we find nelapin via their LastName
            IQueryable<User> userQuery = this.client.CreateDocumentQuery<User>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(u => u.LastName == "Pindakova");
    
            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (User user in userQuery)
            {
                Console.WriteLine("\tRead {0}", user);
            }
    
            // Now execute the same query via direct SQL
            IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), 
                    "SELECT * FROM User WHERE User.lastName = 'Pindakova'", queryOptions );
    
            Console.WriteLine("Running direct SQL query...");
            foreach (User user in userQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", user);
            }
    
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

1. <span data-ttu-id="f1952-117">Kopieren Sie den folgenden Code, und fügen Sie ihn vor der `await this.DeleteUserDocument("Users", "WebCustomers", "1");`-Zeile in Ihre **BasicOperations**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="f1952-117">Copy and paste the following code to your **BasicOperations** method, before the `await this.DeleteUserDocument("Users", "WebCustomers", "1");` line.</span></span>

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

1. <span data-ttu-id="f1952-118">Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="f1952-118">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>
    
    ```
    dotnet run
    ```

    <span data-ttu-id="f1952-119">Die Konsole zeigt die Ausgabe der LINQ und SQL-Abfragen.</span><span class="sxs-lookup"><span data-stu-id="f1952-119">The console displays the output of the LINQ and SQL queries.</span></span>

## <a name="summary"></a><span data-ttu-id="f1952-120">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="f1952-120">Summary</span></span>

<span data-ttu-id="f1952-121">In dieser Einheit haben Sie Informationen zu LINQ-Abfragen erhalten und Ihrer Anwendung eine LINQ- und eine SQL-Abfrage hinzugefügt, um Benutzerdatensätze abzurufen.</span><span class="sxs-lookup"><span data-stu-id="f1952-121">In this unit you learned about LINQ queries, and then added a LINQ and SQL query to your application to retrieve user records.</span></span>