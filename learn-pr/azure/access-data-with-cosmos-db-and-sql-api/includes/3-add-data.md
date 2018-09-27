<span data-ttu-id="c25eb-101">Sie können Ihrer Azure Cosmos DB-Datenbank ganz einfach Daten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c25eb-101">Adding data to your Azure Cosmos DB database is simple.</span></span> <span data-ttu-id="c25eb-102">Öffnen Sie dazu das Azure-Portal, navigieren Sie zu Ihrer Datenbank und verwenden den Daten-Explorer, um der Datenbank JSON-Dokumente hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="c25eb-102">You open the Azure portal, navigate to your database, and use the Data Explorer to add JSON documents to the database.</span></span> <span data-ttu-id="c25eb-103">Es gibt zwar auch komplexere Möglichkeiten, um Daten hinzuzufügen, wir beginnen aber mit dieser Methode, da sich der Daten-Explorer sehr gut dazu eignet, sich mit den internen Abläufen und Funktionen von Azure Cosmos DB vertraut zu machen.</span><span class="sxs-lookup"><span data-stu-id="c25eb-103">There are more advanced ways to add data, but we'll start here because the Data Explorer is a great tool to get you acquainted with the inner workings and functionality provided by Azure Cosmos DB.</span></span>

## <a name="what-is-the-data-explorer"></a><span data-ttu-id="c25eb-104">Was ist der Daten-Explorer?</span><span class="sxs-lookup"><span data-stu-id="c25eb-104">What is the Data Explorer?</span></span>
<span data-ttu-id="c25eb-105">Der Daten-Explorer von Azure Cosmos DB ist ein Tool im Azure-Portal, mit dem Sie in Azure Cosmos DB gespeicherte Daten verwalten können.</span><span class="sxs-lookup"><span data-stu-id="c25eb-105">The Azure Cosmos DB Data Explorer is a tool included in the Azure portal that is used to manage data stored in an Azure Cosmos DB.</span></span> <span data-ttu-id="c25eb-106">Über die bereitgestellte Benutzeroberfläche können Sie Datensammlungen anzeigen, durch Datensammlungen navigieren und Dokumente in der Datenbank bearbeiten. Außerdem lassen sich Daten abfragen und gespeicherte Prozeduren erstellen und ausführen.</span><span class="sxs-lookup"><span data-stu-id="c25eb-106">It provides a UI for viewing and navigating data collections, as well as for editing documents within the database, querying data, and creating and running stored procedures.</span></span>

## <a name="add-data-using-the-data-explorer"></a><span data-ttu-id="c25eb-107">Hinzufügen von Daten mit dem Daten-Explorer</span><span class="sxs-lookup"><span data-stu-id="c25eb-107">Add data using the Data Explorer</span></span>

1. <span data-ttu-id="c25eb-108">Melden Sie sich beim [Azure-Portal für die Sandbox](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit demselben Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="c25eb-108">Sign into the [Azure portal for sandbox](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c25eb-109">Melden Sie sich beim Azure-Portal und der Sandbox mit demselben Konto an.</span><span class="sxs-lookup"><span data-stu-id="c25eb-109">Login to the Azure portal and the sandbox with the same account.</span></span>
    >
    > <span data-ttu-id="c25eb-110">Melden Sie sich beim Azure-Portal über den obigen Link an, um sicherzustellen, dass Sie mit der Sandbox verbunden sind, die Zugriff auf ein Concierge-Abonnement ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="c25eb-110">Login to the Azure portal using the link above to ensure you are connected to the sandbox, which provides access to a Concierge Subscription.</span></span>

1. <span data-ttu-id="c25eb-111">Klicken Sie auf **Alle Dienste** > **Datenbanken** > **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="c25eb-111">Click **All services** > **Databases** > **Azure Cosmos DB**.</span></span> <span data-ttu-id="c25eb-112">Wählen Sie anschließend Ihr Konto aus, und klicken Sie zuerst auf **Daten-Explorer** und anschließend auf **Im Vollbildmodus öffnen**.</span><span class="sxs-lookup"><span data-stu-id="c25eb-112">Then select your account, click **Data Explorer**, and then click **Open Full Screen**.</span></span>

   ![Erstellen neuer Dokumente im Daten-Explorer im Azure-Portal](../media/3-azure-cosmosdb-data-explorer-full-screen.png)

2. <span data-ttu-id="c25eb-114">Klicken Sie im Feld **Vollbildmodus öffnen** auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="c25eb-114">In the **Open Full Screen** box, click **Open**.</span></span>

    <span data-ttu-id="c25eb-115">Im Webbrowser wird der neue Daten-Explorer im Vollbildmodus angezeigt. Dadurch haben Sie mehr Platz und verfügen über eine dedizierte Umgebung für die Arbeit mit Ihrer Datenbank.</span><span class="sxs-lookup"><span data-stu-id="c25eb-115">The web browser displays the new full-screen Data Explorer, which gives you more space and a dedicated environment for working with your database.</span></span>

3. <span data-ttu-id="c25eb-116">Um ein neues JSON-Dokument zu erstellen, erweitern Sie im Bereich für die SQL-API **Clothing** (Kleidung), und klicken Sie zuerst auf **Dokumente** und anschließend auf **Neues Dokument**.</span><span class="sxs-lookup"><span data-stu-id="c25eb-116">To create a new JSON document, in the SQL API pane, expand **Clothing**, click **Documents**, then click **New Document**.</span></span>

   ![Erstellen neuer Dokumente im Daten-Explorer im Azure-Portal](../media/3-azure-cosmosdb-data-explorer-new-document.png)

4. <span data-ttu-id="c25eb-118">Fügen Sie der Sammlung ein Dokument hinzu, und verwenden Sie dabei die folgende Struktur.</span><span class="sxs-lookup"><span data-stu-id="c25eb-118">Now, add a document to the collection with the following structure.</span></span> <span data-ttu-id="c25eb-119">Kopieren Sie einfach den folgenden Code, und fügen Sie ihn auf der Registerkarte **Dokumente** ein. Überschreiben Sie hierbei den aktuellen Inhalt:</span><span class="sxs-lookup"><span data-stu-id="c25eb-119">Just copy and paste the following code into the **Documents** tab, overwriting the current content:</span></span>

     ```json
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "price": "14.99",
        "shipping": {
            "weight": 1,
            "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
           }
        }
    }
     ```

5. <span data-ttu-id="c25eb-120">Nachdem Sie den JSON-Code auf der Registerkarte **Dokumente** hinzugefügt haben, klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="c25eb-120">Once you've added the JSON to the **Documents** tab, click **Save**.</span></span>

    ![Kopieren Sie JSON-Daten, fügen Sie sie ein, und klicken Sie im Azure-Portal im Daten-Explorer auf „Speichern“.](../media/3-azure-cosmosdb-data-explorer-save-document.png)

6. <span data-ttu-id="c25eb-122">Erstellen und speichern Sie ein weiteres Dokument, indem Sie erneut auf **Neues Dokument** klicken, das folgende JSON-Objekt kopieren und in den Daten-Explorer einfügen und auf **Speichern** klicken.</span><span class="sxs-lookup"><span data-stu-id="c25eb-122">Create and save one more document clicking **New Document** again, and copying the following JSON object into Data Explorer and clicking **Save**.</span></span>

     ```json
    {
        "id": "2",
        "productId": "33218897",
        "category": "Women's Outerwear",
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
        "price": "49.99",
        "shipping": {
            "weight": 2,
            "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
           }
        }
    }
     ```

7. <span data-ttu-id="c25eb-123">Vergewissern Sie sich, dass die Dokumente gespeichert wurden, indem Sie im linken Menü auf **Dokumente** klicken.</span><span class="sxs-lookup"><span data-stu-id="c25eb-123">Confirm the documents have been saved by clicking **Documents** on the left-hand menu.</span></span>

    <span data-ttu-id="c25eb-124">Die beiden Dokumente werden im Daten-Explorer auf der Registerkarte **Dokumente** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c25eb-124">Data Explorer displays the two documents in the **Documents** tab.</span></span>

<span data-ttu-id="c25eb-125">In dieser Einheit haben Sie Ihrer Datenbank mithilfe des Daten-Explorers zwei Dokumente hinzugefügt, die jeweils ein Produkt in Ihrem Produktkatalog darstellen.</span><span class="sxs-lookup"><span data-stu-id="c25eb-125">In this unit, you added two documents, each representing a product in your product catalog, to your database by using the Data Explorer.</span></span> <span data-ttu-id="c25eb-126">Der Daten-Explorer eignet sich sehr gut, um Dokumente zu erstellen, Dokumente zu ändern und sich mit Azure Cosmos DB vertraut zu machen.</span><span class="sxs-lookup"><span data-stu-id="c25eb-126">The Data Explorer is a good way to create documents, modify documents, and get started with Azure Cosmos DB.</span></span>
