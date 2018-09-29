<span data-ttu-id="a73a9-101">Nachdem Sie gelernt haben, welche Arten von Abfragen erstellt werden können, verwenden Sie nun den Daten-Explorer im Azure-Portal zum Abrufen und Filtern Ihrer Produktdaten.</span><span class="sxs-lookup"><span data-stu-id="a73a9-101">Now that you've learned about what kinds of queries you can create, let's use the Data Explorer in the Azure portal to retrieve and filter your product data.</span></span>

<span data-ttu-id="a73a9-102">Beachten Sie, dass die Abfrage wie in der folgenden Abbildung gezeigt auf der Registerkarte **Dokument** im Fenster „Daten-Explorer“ standardmäßig auf `SELECT * FROM c` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="a73a9-102">In your Data Explorer window, note that by default, the query on the **Document** tab is set to `SELECT * FROM c` as shown in the following image.</span></span> <span data-ttu-id="a73a9-103">Diese Standardabfrage ruft alle Dokumente in der Sammlung ab und zeigt sie an.</span><span class="sxs-lookup"><span data-stu-id="a73a9-103">This default query retrieves and displays all documents in the collection.</span></span>

![Die Standardabfrage im Daten-Explorer ist SELECT \* FROM c.](../media/5-azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a><span data-ttu-id="a73a9-105">Erstellen einer neuen Abfrage</span><span class="sxs-lookup"><span data-stu-id="a73a9-105">Create a new query</span></span>

1. <span data-ttu-id="a73a9-106">Klicken Sie im Daten-Explorer auf **Neue SQL-Abfrage**.</span><span class="sxs-lookup"><span data-stu-id="a73a9-106">In Data Explorer, click **New SQL Query**.</span></span> <span data-ttu-id="a73a9-107">Beachten Sie, dass die Standardabfrage auf der neuen Registerkarte **Abfrage 1** wieder `SELECT * from c` ist, wodurch alle Dokumente in der Sammlung zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="a73a9-107">Note that the default query on the new  **Query 1** tab is again `SELECT * from c`, which will return all documents in the collection.</span></span> 

1. <span data-ttu-id="a73a9-108">Klicken Sie auf **Abfrage ausführen**.</span><span class="sxs-lookup"><span data-stu-id="a73a9-108">Click **Execute Query**.</span></span> <span data-ttu-id="a73a9-109">Diese Abfrage gibt alle Ergebnisse in der Datenbank zurück.</span><span class="sxs-lookup"><span data-stu-id="a73a9-109">This query returns all results in the database.</span></span>

    ![Ändern Sie die Standardabfrage, indem Sie ORDER BY c._ts DESC hinzufügen und auf „Filter anwenden“ klicken.](../media/5-azure-cosmosdb-data-explorer-edit-query.png)

2. <span data-ttu-id="a73a9-111">Lassen Sie uns jetzt einige der in der vorherigen Einheit erörterten Abfragen ausführen.</span><span class="sxs-lookup"><span data-stu-id="a73a9-111">Now, let's run some of the queries discussed in the previous unit.</span></span> <span data-ttu-id="a73a9-112">Löschen Sie `SELECT * from c` auf der Registerkarte „Abfrage“, kopieren Sie die folgende Abfrage, fügen Sie diese ein, und klicken Sie dann auf **Abfragen ausführen**.</span><span class="sxs-lookup"><span data-stu-id="a73a9-112">On the query tab, delete `SELECT * from c`, copy and paste the following query, and then click **Execute Query**:</span></span>

    ```sql
    SELECT * 
    FROM Products p 
    WHERE p.id ="1"
    ```

    <span data-ttu-id="a73a9-113">Die Ergebnisse geben das Produkt zurück, dessen `productId`-Wert 1 ist.</span><span class="sxs-lookup"><span data-stu-id="a73a9-113">The results return the product whose `productId` is 1.</span></span>

    ![Abfragen einer ID von 1](../media/5-azure-cosmosdb-data-explorer-query-by-id.png)

3. <span data-ttu-id="a73a9-115">Löschen Sie die vorherige Abfrage, kopieren Sie die folgende Abfrage, fügen Sie diese ein, und klicken Sie dann auf **Abfrage ausführen**.</span><span class="sxs-lookup"><span data-stu-id="a73a9-115">Delete the previous query, copy and paste the following query, and click **Execute Query**.</span></span> <span data-ttu-id="a73a9-116">Diese Abfrage gibt in aufsteigender Reihenfolge und nach dem Preis sortiert den Preis, die Beschreibung und die Produkt-ID für alle Produkte zurück.</span><span class="sxs-lookup"><span data-stu-id="a73a9-116">This query returns the price, description, and product ID for all products, ordered by price, in ascending order.</span></span>
 
    ```sql
    SELECT p.price, p.description, p.productId 
    FROM Products p 
    ORDER BY p.price ASC
    ```

## <a name="summary"></a><span data-ttu-id="a73a9-117">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="a73a9-117">Summary</span></span>

<span data-ttu-id="a73a9-118">Sie haben nun einige grundlegende Abfragen für Ihre Daten in Azure Cosmos DB abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="a73a9-118">You have now completed some basic queries on your data in Azure Cosmos DB.</span></span> 