<span data-ttu-id="ac74f-101">In Ihrer Datenbank befinden sich mehrere Dokumente, die gleichzeitig aktualisiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="ac74f-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="ac74f-102">In dieser Lektion wird erläutert, wie Sie gespeicherte Prozeduren über eine .NET-Konsolenanwendung erstellen, registrieren und ausführen.</span><span class="sxs-lookup"><span data-stu-id="ac74f-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="ac74f-103">Erstellen einer gespeicherten Prozedur in Ihrer App</span><span class="sxs-lookup"><span data-stu-id="ac74f-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="ac74f-104">In dieser gespeicherten Prozedur wird mithilfe der OrderId (Bestell-ID), die eine Liste aller Auftragspositionen enthält, die Gesamtbestellsumme berechnet.</span><span class="sxs-lookup"><span data-stu-id="ac74f-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="ac74f-105">Diese ergibt sich aus der Summe der Auftragspositionen abzüglich aller Gutschriften des Kunden, wobei sämtliche Gutscheincodes berücksichtigt werden.</span><span class="sxs-lookup"><span data-stu-id="ac74f-105">The order total is calculated from the sum of the items in the order, less any dividends (credits) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="ac74f-106">Erweitern Sie auf der Registerkarte „Azure“ in Visual Studio Code das **Learning-Modul (SQL)** > **Benutzer** > **WebCustomers**, und klicken Sie dann mit der rechten Maustaste auf **Gespeicherte Prozeduren** und anschließend auf **Gespeicherte Prozedur erstellen**.</span><span class="sxs-lookup"><span data-stu-id="ac74f-106">In Visual Studio Code, in the Azure tab, expand the **learning-module (SQL)** > **Users** > **WebCustomers** and then right-click **Stored Procedures** and then click **Create Stored Procedure**.</span></span>

1. <span data-ttu-id="ac74f-107">Geben Sie im Textfeld am oberen Rand des Bildschirms *UpdateOrderTotal* ein, und drücken Sie die EINGABETASTE, um der gespeicherten Prozedur einen Namen zu geben.</span><span class="sxs-lookup"><span data-stu-id="ac74f-107">In the text box at the top of the screen, type *UpdateOrderTotal* and click Enter to give the stored procedure a name.</span></span>

1. <span data-ttu-id="ac74f-108">Erweitern Sie **Gespeicherte Prozeduren**, und klicken Sie auf **UpdateOrderTotal**.</span><span class="sxs-lookup"><span data-stu-id="ac74f-108">Expand **Stored Procedures** and click **UpdateOrderTotal**.</span></span>

1. <span data-ttu-id="ac74f-109">Standardmäßig wird eine gespeicherte Prozedur bereitgestellt, die das erste Element abruft.</span><span class="sxs-lookup"><span data-stu-id="ac74f-109">By default, a stored procedure that retrieves the first item is provided.</span></span>

1. <span data-ttu-id="ac74f-110">Fügen Sie zum Ausführen dieser gespeicherten Prozedur in Ihrer Anwendung der Datei „Program.cs“ den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="ac74f-110">To run this stored procedure from your application, add the following code to the Program.cs file.</span></span>

    ```csharp
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        try
        {
            await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "sample"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            Console.WriteLine("Stored procedure complete");
        }
        catch (DocumentClientException de)
        {
            throw;
        }
    }
    ```
    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->

1. <span data-ttu-id="ac74f-111">Kopieren Sie nun den folgenden Code, und fügen Sie diesen am Ende der **BasicOperations**-Methode ein.</span><span class="sxs-lookup"><span data-stu-id="ac74f-111">Now copy the following code and paste it into the end of the **BasicOperations** method.</span></span>

    ```
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="ac74f-112">Führen Sie im integrierten Terminal den folgenden Befehl aus, um das Beispiel mit der gespeicherte Prozedur auszuführen.</span><span class="sxs-lookup"><span data-stu-id="ac74f-112">In the integrated terminal, run the following command to run the sample with the stored procedure.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="ac74f-113">Auf der Konsole wird die Meldung ausgegeben, dass die gespeicherte Prozedur abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="ac74f-113">The console displays output indicating that the stored procedure was completed.</span></span>

## <a name="clean-up"></a><span data-ttu-id="ac74f-114">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="ac74f-114">Clean up</span></span>

<span data-ttu-id="ac74f-115">Wenn Sie weiterhin an den Modulen in diesem Lernpfad arbeiten möchten, können Sie den Bereinigungsvorgang überspringen. Andernfalls müssen Sie mithilfe der folgenden Schritte den Bereinigungsvorgang für Ihre Ressourcen ausführen, da Ihnen sonst die Nutzung des Diensts in Rechnung gestellt wird.</span><span class="sxs-lookup"><span data-stu-id="ac74f-115">If you plan to continue working on the modules in this learning path, skip the clean-up process, or else use the following steps to delete your resources to avoid incurring charges for use of the service.</span></span>

1. <span data-ttu-id="ac74f-116">Klicken Sie im Azure-Portal ganz links auf **Ressourcengruppen** und anschließend auf die erstellte Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="ac74f-116">In the Azure portal, select **Resource groups** on the far left, and then select the resource group you created.</span></span>  

    <span data-ttu-id="ac74f-117">Sollte das linke Menü reduziert sein, klicken Sie auf</span><span class="sxs-lookup"><span data-stu-id="ac74f-117">If the left menu is collapsed, click</span></span> ![Schaltfläche „Erweitern“](../media/5-javascript-programming/expand.png) <span data-ttu-id="ac74f-119">, um es zu erweitern.</span><span class="sxs-lookup"><span data-stu-id="ac74f-119">to expand it.</span></span>

   ![Metriken im Azure-Portal](../media/5-javascript-programming/delete-resources-select.png)

1. <span data-ttu-id="ac74f-121">Wählen Sie in dem neuen Fenster die Ressourcengruppe aus, und klicken Sie auf **Ressourcengruppe löschen**.</span><span class="sxs-lookup"><span data-stu-id="ac74f-121">In the new window select the resource group, and then click **Delete resource group**.</span></span>

   ![Metriken im Azure-Portal](../media/5-javascript-programming/delete-resources.png)

1. <span data-ttu-id="ac74f-123">Geben Sie im neuen Fenster den Namen der zu löschenden Ressourcengruppe ein, und klicken Sie dann auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="ac74f-123">In the new window, type the name of the resource group to delete, and then click **Delete**.</span></span>

## <a name="summary"></a><span data-ttu-id="ac74f-124">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="ac74f-124">Summary</span></span>

<span data-ttu-id="ac74f-125">In diesem Modul haben Sie eine .NET Core-Konsolenanwendung erstellt, mit der Benutzerdatensätze erstellt, aktualisiert und gelöscht werden. Außerdem werden mithilfe von SQL und LINQ Benutzerdatensätze abgefragt. Durch die Konsolenanwendung wird eine gespeicherte Prozedur ausgeführt, um Elemente in der Datenbank abzufragen.</span><span class="sxs-lookup"><span data-stu-id="ac74f-125">In this module you've created a .NET Core console application that creates, updates, and deletes user records, queries the users by using SQL and LINQ, and runs a stored procedure to query items in the database.</span></span>