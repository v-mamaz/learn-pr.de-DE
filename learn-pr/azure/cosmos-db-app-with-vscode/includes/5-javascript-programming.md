In Ihrer Datenbank befinden sich mehrere Dokumente, die gleichzeitig aktualisiert werden müssen. In dieser Lektion wird erläutert, wie Sie gespeicherte Prozeduren über eine .NET-Konsolenanwendung erstellen, registrieren und ausführen.

## <a name="create-a-stored-procedure-in-your-app"></a>Erstellen einer gespeicherten Prozedur in Ihrer App

In dieser gespeicherten Prozedur wird mithilfe der OrderId (Bestell-ID), die eine Liste aller Auftragspositionen enthält, die Gesamtbestellsumme berechnet. Diese ergibt sich aus der Summe der Auftragspositionen abzüglich aller Gutschriften des Kunden, wobei sämtliche Gutscheincodes berücksichtigt werden.

1. Kopieren Sie den folgenden Code, und fügen Sie diesen in die Datei „Program.cs“ ein.

    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->
    ```csharp
    private async Task UpdateOrderTotal(string databaseName, string collectionName, Order orderId)
    {
    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    
    
                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }
    
                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };
    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;
    
    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "ValidateDocumentAge"), document, 1920);
    }
    ```

2. Kopieren Sie nun den folgenden Code, und fügen Sie diesen am Ende der **BasicOperations**-Methode ein.

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus:

    ```
    dotnet run
    ```

    Auf der Konsole wird nun Folgendes ausgegeben:

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a>Bereinigen

Wenn Sie weiterhin an den Modulen in diesem Lernpfad arbeiten möchten, können Sie den Bereinigungsvorgang überspringen. Andernfalls müssen Sie mithilfe der folgenden Schritte den Bereinigungsvorgang für Ihre Ressourcen ausführen, da Ihnen sonst die Nutzung des Diensts in Rechnung gestellt wird.

1. Klicken Sie im Azure-Portal ganz links auf **Ressourcengruppen** und anschließend auf die erstellte Ressourcengruppe.  

    Sollte das linke Menü reduziert sein, klicken Sie auf ![Schaltfläche „Erweitern“](../media/5-javascript-programming/expand.png) , um es zu erweitern.

   ![Metriken im Azure-Portal](../media/5-javascript-programming/delete-resources-select.png)

2. Wählen Sie in dem neuen Fenster die Ressourcengruppe aus, und klicken Sie auf **Ressourcengruppe löschen**.

   ![Metriken im Azure-Portal](../media/5-javascript-programming/delete-resources.png)

3. Geben Sie im neuen Fenster den Namen der zu löschenden Ressourcengruppe ein, und klicken Sie dann auf **Löschen**.

## <a name="summary"></a>Zusammenfassung

In diesem Modul haben Sie eine .NET Core-Konsolenanwendung erstellt, mit der Benutzerdatensätze erstellt, aktualisiert und gelöscht werden. Außerdem werden mithilfe von SQL und LINQ Benutzerdatensätze abgefragt. Durch die Ausführung einer gespeicherten Prozedur wird eine Gesamtbestellsumme errechnet, wobei Benutzergutschriften und Gutscheine berücksichtigt werden.