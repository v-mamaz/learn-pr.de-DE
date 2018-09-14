<span data-ttu-id="98d14-101">In Ihrer Datenbank befinden sich mehrere Dokumente, die gleichzeitig aktualisiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="98d14-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="98d14-102">In dieser Lektion wird erläutert, wie Sie gespeicherte Prozeduren über eine .NET-Konsolenanwendung erstellen, registrieren und ausführen.</span><span class="sxs-lookup"><span data-stu-id="98d14-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="98d14-103">Erstellen einer gespeicherten Prozedur in Ihrer App</span><span class="sxs-lookup"><span data-stu-id="98d14-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="98d14-104">In dieser gespeicherten Prozedur wird mithilfe der OrderId (Bestell-ID), die eine Liste aller Auftragspositionen enthält, die Gesamtbestellsumme berechnet.</span><span class="sxs-lookup"><span data-stu-id="98d14-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="98d14-105">Diese ergibt sich aus der Summe der Auftragspositionen abzüglich aller Gutschriften des Kunden, wobei sämtliche Gutscheincodes berücksichtigt werden.</span><span class="sxs-lookup"><span data-stu-id="98d14-105">The order total is calculated from the sum of the items in the order, less any dividend (credit) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="98d14-106">Kopieren Sie den folgenden Code, und fügen Sie diesen in die Datei „Program.cs“ ein.</span><span class="sxs-lookup"><span data-stu-id="98d14-106">Copy the following code and paste it into the end of the Program.cs file.</span></span>

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

2. <span data-ttu-id="98d14-107">Kopieren Sie nun den folgenden Code, und fügen Sie diesen am Ende der **BasicOperations**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="98d14-107">Now copy the following code and paste it into the end of the **BasicOperations** method.</span></span>

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. <span data-ttu-id="98d14-108">Speichern Sie die Datei „Program.cs“, und führen Sie dann im integrierten Terminal den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="98d14-108">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="98d14-109">Auf der Konsole wird nun Folgendes ausgegeben:</span><span class="sxs-lookup"><span data-stu-id="98d14-109">The console displays the following output.</span></span>

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a><span data-ttu-id="98d14-110">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="98d14-110">Clean up</span></span>

<span data-ttu-id="98d14-111">Wenn Sie weiterhin an den Modulen in diesem Lernpfad arbeiten möchten, können Sie den Bereinigungsvorgang überspringen. Andernfalls müssen Sie mithilfe der folgenden Schritte den Bereinigungsvorgang für Ihre Ressourcen ausführen, da Ihnen sonst die Nutzung des Diensts in Rechnung gestellt wird.</span><span class="sxs-lookup"><span data-stu-id="98d14-111">If you plan to continue working on the modules in this learning path, skip the clean-up process, or else use the following steps to delete your resources to avoid incurring charges for use of the service.</span></span>

1. <span data-ttu-id="98d14-112">Klicken Sie im Azure-Portal ganz links auf **Ressourcengruppen** und anschließend auf die erstellte Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="98d14-112">In the Azure portal, select **Resource groups** on the far left, and then select the resource group you created.</span></span>  

    <span data-ttu-id="98d14-113">Sollte das linke Menü reduziert sein, klicken Sie auf</span><span class="sxs-lookup"><span data-stu-id="98d14-113">If the left menu is collapsed, click</span></span> ![Schaltfläche „Erweitern“](../media/5-javascript-programming/expand.png) <span data-ttu-id="98d14-115">, um es zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="98d14-115">to expand it.</span></span>

   ![Metriken im Azure-Portal](../media/5-javascript-programming/delete-resources-select.png)

2. <span data-ttu-id="98d14-117">Wählen Sie in dem neuen Fenster die Ressourcengruppe aus, und klicken Sie auf **Ressourcengruppe löschen**.</span><span class="sxs-lookup"><span data-stu-id="98d14-117">In the new window select the resource group, and then click **Delete resource group**.</span></span>

   ![Metriken im Azure-Portal](../media/5-javascript-programming/delete-resources.png)

3. <span data-ttu-id="98d14-119">Geben Sie im neuen Fenster den Namen der zu löschenden Ressourcengruppe ein, und klicken Sie dann auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="98d14-119">In the new window, type the name of the resource group to delete, and then click **Delete**.</span></span>

## <a name="summary"></a><span data-ttu-id="98d14-120">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="98d14-120">Summary</span></span>

<span data-ttu-id="98d14-121">In diesem Modul haben Sie eine .NET Core-Konsolenanwendung erstellt, mit der Benutzerdatensätze erstellt, aktualisiert und gelöscht werden. Außerdem werden mithilfe von SQL und LINQ Benutzerdatensätze abgefragt. Durch die Ausführung einer gespeicherten Prozedur wird eine Gesamtbestellsumme errechnet, wobei Benutzergutschriften und Gutscheine berücksichtigt werden.</span><span class="sxs-lookup"><span data-stu-id="98d14-121">In this module you've created a .NET Core console application that creates, updates, and deletes user records, queries the users by using SQL and LINQ, and runs a stored procedure to create an order total that takes the users dividends and coupons into account.</span></span>