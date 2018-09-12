<span data-ttu-id="232ef-101">Nachdem Sie gelernt haben, welche Arten von Abfragen erstellt werden können, verwenden wir nun den Daten-Explorer im Azure-Portal zum Abrufen und Filtern Ihrer Produktdaten.</span><span class="sxs-lookup"><span data-stu-id="232ef-101">Now that you've learned about what kinds of queries you can create, let's use the Data Explorer in the Azure portal to retrieve and filter your product data.</span></span>

<span data-ttu-id="232ef-102">Beachten Sie, dass die Abfrage auf der Registerkarte **Dokument** im Fenster Ihres Daten-Explorers standardmäßig auf `SELECT * FROM c` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="232ef-102">In your Data Explorer window, note that by default, the query on the **Document** tab is set to `SELECT * FROM c`.</span></span> <span data-ttu-id="232ef-103">Diese Standardabfrage ruft alle Dokumente in der Sammlung ab und zeigt sie an.</span><span class="sxs-lookup"><span data-stu-id="232ef-103">This default query retrieves and displays all documents in the collection.</span></span>

![Die Standardabfrage im Daten-Explorer ist SELECT \* FROM c.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a><span data-ttu-id="232ef-105">Erstellen einer neuen Abfrage</span><span class="sxs-lookup"><span data-stu-id="232ef-105">Create a new query</span></span>

1. <span data-ttu-id="232ef-106">Klicken Sie im Daten-Explorer auf die Registerkarte **Neue SQL-Abfrage**. Beachten Sie, dass `SELECT * from c` die Standardabfrage auf der neuen Registerkarte **Abfrage 1** ist, und klicken Sie dann auf **Abfrage ausführen**.</span><span class="sxs-lookup"><span data-stu-id="232ef-106">In Data Explorer, click the **New SQL Query** tab. Note that the default query on the new  **Query 1** tab is `SELECT * from c`, and then click **Execute Query**.</span></span> <span data-ttu-id="232ef-107">Diese Abfrage gibt alle Ergebnisse in der Datenbank zurück.</span><span class="sxs-lookup"><span data-stu-id="232ef-107">This query returns all results in the database.</span></span>

    ![Ändern Sie die Standardabfrage, indem Sie ORDER BY c._ts DESC hinzufügen und auf „Filter anwenden“ klicken.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-edit-query.png)

2. <span data-ttu-id="232ef-109">Lassen Sie uns jetzt einige der in der vorherigen Einheit erörterten Abfragen ausführen.</span><span class="sxs-lookup"><span data-stu-id="232ef-109">Now, let's run some of the queries discussed in the previous unit.</span></span> <span data-ttu-id="232ef-110">Löschen Sie `SELECT * from c` auf der Registerkarte „Abfrage“, kopieren Sie die folgende Abfrage, fügen Sie diese ein, und klicken Sie dann auf **Abfragen ausführen**.</span><span class="sxs-lookup"><span data-stu-id="232ef-110">On the query tab, delete `SELECT * from c`, copy and paste the following query, and then click **Execute Query**:</span></span>

    ```
    SELECT *
    FROM Products p
    WHERE p.id ="1"
    ```

    <span data-ttu-id="232ef-111">Die Ergebnisse geben das Produkt zurück, dessen `productId` 1 ist.</span><span class="sxs-lookup"><span data-stu-id="232ef-111">The results return the product whose `productId` is 1.</span></span>

    ![Ändern Sie die Standardabfrage, indem Sie ORDER BY c._ts DESC hinzufügen und auf „Filter anwenden“ klicken.](../media-draft/4-run-queries/azure-cosmosdb-data-explorer-query-by-id.png)

3. <span data-ttu-id="232ef-113">Löschen Sie die vorherige Abfrage, kopieren Sie die folgende Abfrage, fügen Sie diese ein, und klicken Sie dann auf **Abfrage ausführen**.</span><span class="sxs-lookup"><span data-stu-id="232ef-113">Delete the previous query, copy and paste the following query, and click **Execute Query**.</span></span> <span data-ttu-id="232ef-114">Diese Abfrage gibt in aufsteigender Reihenfolge und nach dem Preis sortiert den Preis, die Beschreibung und die Produkt-ID für alle Produkte zurück.</span><span class="sxs-lookup"><span data-stu-id="232ef-114">This query returns the price, description, and product ID for all products, ordered by price, in ascending order.</span></span>
 
    ```
    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC
    ```

## <a name="summary"></a><span data-ttu-id="232ef-115">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="232ef-115">Summary</span></span>

<span data-ttu-id="232ef-116">Sie haben nun einige grundlegende Abfragen für Ihre Daten in Azure Cosmos DB abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="232ef-116">You have now completed some basic queries on your data in Azure Cosmos DB.</span></span> 