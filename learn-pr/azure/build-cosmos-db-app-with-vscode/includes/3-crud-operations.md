<!--TODO: explain Etag in knowledge needed-->

Nach dem Herstellen der Verbindung mit Azure Cosmos DB besteht der nächste Schritt darin, die in der Datenbank gespeicherten Dokumente zu erstellen, zu lesen, zu ersetzen und zu löschen. In dieser Einheit erstellen Sie in Ihrer WebCustomer-Sammlung Benutzerdokumente, rufen sie über die ID ab, ersetzen sie und löschen sie anschließend.

## <a name="working-with-documents-programmatically"></a>Programmgesteuertes Arbeiten mit Dokumenten

Daten werden in Azure Cosmos DB als JSON-Dokumente gespeichert. [Dokumente](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) können im Portal erstellt, abgerufen, ersetzt oder gelöscht werden, und zwar wie im vorherigen Modul oder wie in diesem Modul beschrieben programmgesteuert. Azure Cosmos DB bietet clientseitige SDKs für .NET, .NET Core, Java, Node.js und Python, die alle diese Vorgänge unterstützen. In diesem Modul wird das .NET Core SDK zum Ausführen von CRUD-Vorgängen (Create, Retrieve, Update, Delete – Erstellen, Abrufen, Aktualisieren, Löschen) verwendet. 

Die wichtigsten Vorgänge für Azure Cosmos DB-Dokumente sind Teil der [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet)-Klasse:
* [CreateDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [ReadDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [ReplaceDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet). Upsert führt einen Vorgang zum Erstellen oder Ersetzen durch, je nachdem, ob das Dokument bereits vorhanden ist.
* [DeleteDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

Um diese Vorgänge auszuführen, müssen Sie eine Klasse erstellen, die das in der Datenbank gespeicherte Objekt darstellt. Da Sie mit einer Datenbank von Benutzern arbeiten, sollten Sie eine **User**-Klasse erstellen, um primäre Daten wie den Vor- und Nachnamen sowie die Benutzer-ID (diese ist erforderlich, da sie der Partitionsschlüssel für die horizontale Skalierung ist) zu speichern, sowie Unterklassen für die Versandeinstellungen und den Bestellverlauf.

Nachdem Sie die Klassen, die Ihre Benutzer darstellen, erstellt haben, erstellen Sie neue Benutzerdokumente für jede Instanz und führen dann einige einfache CRUD-Operationen für die Dokumente durch.

## <a name="create-documents"></a>Erstellen von Dokumenten

1. Erstellen Sie zunächst eine **User**-Klasse, die die Objekte zum Speichern in Azure Cosmos DB darstellt. Außerdem werden die Unterklassen **OrderHistory** und **ShippingPreference** erstellt, die in **User** verwendet werden. Beachten Sie, dass Dokumente eine **Id**-Eigenschaft enthalten müssen, die in JSON als **id** serialisiert wird.

    Um diese Klassen zu erstellen, kopieren Sie die folgenden Klassen **User**, **OrderHistory**, **ShippingPreference** und fügen Sie unterhalb der Methode **BasicOperations** ein.

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

1. Geben Sie im integrierten Terminal den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.

    ```csharp
    dotnet run
    ```

1. Kopieren Sie nun den Task **CreateUserDocumentIfNotExists**, und fügen Sie ihn unter der Klasse **ShippingPreference** ein.

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

1. Fügen Sie dann Folgendes zur Methode **BasicOperations** hinzu.

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

1. Geben Sie im integrierten Terminal erneut den folgenden Befehl zum Ausführen des Programms ein, um die Ausführung sicherzustellen.

    ```csharp
    dotnet run
    ```

    Das Terminal zeigt die folgende Ausgabe an, die angibt, dass beide Benutzerdatensätze erfolgreich erstellt wurden.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a>Lesen von Dokumenten

1. Um Dokumente aus der Datenbank zu lesen, kopieren Sie den folgenden Code, und fügen Sie ihn am Ende der Datei „Program.cs“ ein.
    
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

1.  Kopieren Sie den folgenden Code, und fügen Sie ihn an das Ende der **BasicOperations**-Methode nach der Zeile `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` ein.

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

1. Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.

    ```
    dotnet run
    ```
    Das Terminal zeigt die folgende Ausgabe an, wobei die Ausgabe „Read user 1“ angibt, dass das Dokument abgerufen wurde.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a>Ersetzen von Dokumenten

Azure Cosmos DB unterstützt das Ersetzen von JSON-Dokumenten. In diesem Fall wird ein Benutzerdatensatz aktualisiert, um eine Änderung an den Nachnamen zu berücksichtigen.

1. Kopieren Sie die **ReplaceFamilyDocument**-Methode, und fügen Sie diese am Ende der Datei „Program.cs“ ein.

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, User updatedUser)
    {
            try
            {
            await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, updatedUser.Id), updatedUser, new RequestOptions { PartitionKey = new PartitionKey(updatedUser.UserId) } );
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

1. Kopieren Sie den folgenden Code, und fügen Sie ihn am Ende der **BasicOperations**-Methode nach der Zeile `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` ein.

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe);
    ```

1. Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus.

    ```
    dotnet run
    ```
    Das Terminal zeigt die folgende Ausgabe an, wobei „Replaced last name for Suh“ darauf hinweist, dass das Dokument ersetzt wurde.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a>Löschen von Dokumenten

1. Kopieren Sie die **DeleteUserDocument**-Methode, und fügen Sie sie unterhalb der **ReplaceUserDocument**-Methode ein.
    
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

1. Kopieren Sie den folgenden Code, und fügen Sie ihn unterhalb der zweiten Abfrageausführung in die **BasicOperations**-Methode ein.

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", yanhe);
    ```

1. Führen Sie im integrierten Terminal den folgenden Befehl aus.

    ```
    dotnet run
    ```

    Das Terminal zeigt die folgende Ausgabe an, wobei die Ausgabe „Deleted user 1“ angibt, dass das Dokument gelöscht wurde.

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    Deleted user 1
    End of demo, press any key to exit.
    ```

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie Dokumente in Ihrer Azure Cosmos DB-Datenbank erstellt, ersetzt und gelöscht.