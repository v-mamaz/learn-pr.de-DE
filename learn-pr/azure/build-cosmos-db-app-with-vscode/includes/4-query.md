<!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Nun, da Sie Dokumente in Ihrer Anwendung erstellt haben, werden wir diese aus Ihrer Anwendung abrufen. Azure Cosmos DB verwendet SQL- und LINQ-Abfragen. Diese Einheit konzentriert sich auf die Ausführung von SQL- und LINQ-Abfragen aus Ihrer Anwendung, im Gegensatz zur Ausführung aus dem Portal.

Hierbei werden die für Ihre Anwendung für Onlinehändler erstellten Benutzerdokumente verwendet, um diese Abfragen zu testen.

## <a name="linq-query-basics"></a>Grundlegendes zu LINQ-Abfragen

LINQ ist ein .NET-Programmiermodell, das Berechnungen als Abfragen für Streams von Objekten darstellt. Sie können ein **IQueryable**-Objekt für die direkte Abfrage von Azure Cosmos DB erstellen, das die LINQ-Abfrage in eine Cosmos DB-Abfrage übersetzt. Anschließend wird die Abfrage an den Azure Cosmos DB-Server übergeben, um einen Ergebnissatz im JSON-Format abzurufen. Die zurückgegebenen Ergebnisse werden clientseitig in einen Stream von .NET-Objekten deserialisiert. Viele Entwickler bevorzugen LINQ-Abfragen, weil sie ein einziges, konsistentes Programmiermodell für die Arbeit mit Objekten im Anwendungscode und für die Abfragelogik in der Datenbank bieten.

Die folgende Tabelle zeigt, wie LINQ-Abfragen in SQL übersetzt werden.

| LINQ-Ausdruck | SQL-Übersetzung |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a>Ausführen von SQL- und LINQ-Abfragen

1. Im folgenden Beispiel wird gezeigt, wie eine Abfrage aus Ihrem .NET-Code in SQL, LINQ oder LINQ Lambda ausgeführt werden kann. Kopieren Sie den Code, und fügen Sie ihn ans Ende der „Program.cs“-Datei ein.

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

1. Kopieren Sie den folgenden Code, und fügen Sie ihn vor der `await this.DeleteUserDocument("Users", "WebCustomers", "1");`-Zeile in Ihre **BasicOperations**-Methode ein.

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

1. Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.
    
    ```
    dotnet run
    ```

    Die Konsole zeigt die Ausgabe der LINQ und SQL-Abfragen.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie Informationen zu LINQ-Abfragen erhalten und Ihrer Anwendung eine LINQ- und eine SQL-Abfrage hinzugefügt, um Benutzerdatensätze abzurufen.