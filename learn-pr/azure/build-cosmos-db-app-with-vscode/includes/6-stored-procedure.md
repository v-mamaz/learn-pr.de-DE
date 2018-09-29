<span data-ttu-id="29fe7-101">In Ihrer Datenbank befinden sich mehrere Dokumente, die gleichzeitig aktualisiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="29fe7-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="29fe7-102">In dieser Lektion wird erläutert, wie Sie gespeicherte Prozeduren über eine .NET-Konsolenanwendung erstellen, registrieren und ausführen.</span><span class="sxs-lookup"><span data-stu-id="29fe7-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="29fe7-103">Erstellen einer gespeicherten Prozedur in Ihrer App</span><span class="sxs-lookup"><span data-stu-id="29fe7-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="29fe7-104">In dieser gespeicherten Prozedur wird mithilfe der OrderId (Bestell-ID), die eine Liste aller Auftragspositionen enthält, die Gesamtbestellsumme berechnet.</span><span class="sxs-lookup"><span data-stu-id="29fe7-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="29fe7-105">Diese ergibt sich aus der Summe der Auftragspositionen abzüglich aller Gutschriften des Kunden, wobei sämtliche Gutscheincodes berücksichtigt werden.</span><span class="sxs-lookup"><span data-stu-id="29fe7-105">The order total is calculated from the sum of the items in the order, less any dividends (credits) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="29fe7-106">Erweitern Sie in Visual Studio Code auf der Registerkarte **Azure Cosmos DB** Ihr Azure Cosmos DB-Konto, klicken Sie auf **Benutzer** > **WebCustomers**, klicken Sie dann mit der rechten Maustaste auf **Gespeicherte Prozeduren**, und klicken Sie anschließend auf **Gespeicherte Prozedur erstellen**.</span><span class="sxs-lookup"><span data-stu-id="29fe7-106">In Visual Studio Code, in the **Azure: Cosmos DB** tab, expand your Azure Cosmos DB account > **Users** > **WebCustomers** and then right-click **Stored Procedures** and then click **Create Stored Procedure**.</span></span>

1. <span data-ttu-id="29fe7-107">Geben Sie im Textfeld am oberen Rand des Bildschirms `UpdateOrderTotal` ein, und drücken Sie die EINGABETASTE, um der gespeicherten Prozedur einen Namen zu geben.</span><span class="sxs-lookup"><span data-stu-id="29fe7-107">In the text box at the top of the screen, type `UpdateOrderTotal` and press Enter to give the stored procedure a name.</span></span>

1. <span data-ttu-id="29fe7-108">Erweitern Sie **Gespeicherte Prozeduren** auf der Registerkarte **Azure Cosmos DB**, und klicken Sie auf **UpdateOrderTotal**.</span><span class="sxs-lookup"><span data-stu-id="29fe7-108">In the **Azure: Cosmos DB** tab, expand **Stored Procedures** and click **UpdateOrderTotal**.</span></span>

    <span data-ttu-id="29fe7-109">Standardmäßig wird eine gespeicherte Prozedur bereitgestellt, die das erste Element abruft.</span><span class="sxs-lookup"><span data-stu-id="29fe7-109">By default, a stored procedure that retrieves the first item is provided.</span></span>

1. <span data-ttu-id="29fe7-110">Fügen Sie den folgenden Code in die Datei **Program.cs** ein, um diese gespeicherte Standardprozedur über Ihre Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="29fe7-110">To run this default stored procedure from your application, add the following code to the **Program.cs** file.</span></span>

    ```csharp
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "UpdateOrderTotal"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
        Console.WriteLine("Stored procedure complete");
    }
    ```

1. <span data-ttu-id="29fe7-111">Kopieren Sie nun den folgenden Code, und fügen Sie diesen vor der `await this.DeleteUserDocument("Users", "WebCustomers", yanhe);`-Zeile der **BasicOperations**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="29fe7-111">Now copy the following code and paste it before the `await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` line in the **BasicOperations** method.</span></span>

    ```csharp
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="29fe7-112">Führen Sie im integrierten Terminal den folgenden Befehl aus, um das Beispiel mit der gespeicherten Prozedur auszuführen.</span><span class="sxs-lookup"><span data-stu-id="29fe7-112">In the integrated terminal, run the following command to run the sample with the stored procedure.</span></span>

    ```bash
    dotnet run
    ```

<span data-ttu-id="29fe7-113">Die Konsole zeigt eine Ausgabe an, die angibt, dass die gespeicherte Prozedur abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="29fe7-113">The console displays output indicating that the stored procedure was completed.</span></span>
