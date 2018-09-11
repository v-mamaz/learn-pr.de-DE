<span data-ttu-id="2b77c-101">Das Hinzufügen von Daten zu Ihrer Azure Cosmos DB-Datenbank sollte kein Problem sein.</span><span class="sxs-lookup"><span data-stu-id="2b77c-101">Adding data to your Azure Cosmos DB database should be simple.</span></span> <span data-ttu-id="2b77c-102">Sie öffnen das Azure-Portal, navigieren zu Ihrer Datenbank und verwenden den **Daten-Explorer**, um der Datenbank JSON-Dokumente hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="2b77c-102">You open the Azure portal, navigate to your database, and use the **Data Explorer** to add json documents to the database.</span></span> <span data-ttu-id="2b77c-103">Es gibt zwar auch komplexere Möglichkeiten, um Daten hinzuzufügen, wir beginnen aber mit dieser Methode, da sich der Daten-Explorer sehr gut dazu eignet, sich mit den internen Abläufen und Funktionen von Azure Cosmos DB vertraut zu machen.</span><span class="sxs-lookup"><span data-stu-id="2b77c-103">There are more advanced ways to add data, but we'll start here as the Data Explorer is a great tool to get you aquainted with the inner workings and functionality provided by Azure Cosmos DB.</span></span>

## <a name="what-is-the-data-explorer"></a><span data-ttu-id="2b77c-104">Was ist der Daten-Explorer?</span><span class="sxs-lookup"><span data-stu-id="2b77c-104">What is the Data Explorer?</span></span>
<span data-ttu-id="2b77c-105">Der Daten-Explorer von Azure Cosmos DB ist ein Tool im Azure-Portal, mit dem Sie in Azure Cosmos DB gespeicherte Daten verwalten können.</span><span class="sxs-lookup"><span data-stu-id="2b77c-105">The Azure Cosmos DB Data Explorer is a tool built included in the Azure Portal that is used to manage data stored in an Azure Cosmos DB.</span></span> <span data-ttu-id="2b77c-106">Es stellt eine Benutzeroberfläche zum Anzeigen von und Navigieren durch Datensammlungen sowie zum Bearbeiten von Dokumenten in der Datenbank bereit.</span><span class="sxs-lookup"><span data-stu-id="2b77c-106">It provides UI to view and navigate data collections as well as edit documents within the db.</span></span>

## <a name="add-data-using-the-data-explorer"></a><span data-ttu-id="2b77c-107">Hinzufügen von Daten mit dem Daten-Explorer</span><span class="sxs-lookup"><span data-stu-id="2b77c-107">Add data using the Data Explorer</span></span>

1. <span data-ttu-id="2b77c-108">Wenn Sie zuvor das vorherige Modul absolviert haben, klicken Sie im Fenster des Azure-Portals auf **Daten-Explorer** und anschließend auf **Vollbildmodus öffnen**.</span><span class="sxs-lookup"><span data-stu-id="2b77c-108">If you're continuing from the previous module, click **Data Explorer** in the Azure portal window, and then click **Open Full Screen**.</span></span>

    <span data-ttu-id="2b77c-109">Melden Sie sich andernfalls beim [Azure-Portal](https://portal.azure.com/) an, und klicken Sie auf **Alle Dienste** > **Datenbanken** > **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="2b77c-109">Otherwise, sign in to the [Azure portal](https://portal.azure.com/), click **All services** > **Databases** > **Azure Cosmos DB**.</span></span> <span data-ttu-id="2b77c-110">Wählen Sie anschließend Ihr Konto aus, klicken Sie auf **Daten-Explorer**, und klicken Sie anschließend auf **Vollbildmodus öffnen**</span><span class="sxs-lookup"><span data-stu-id="2b77c-110">Then select your account, click **Data Explorer**, and then click **Open Full Screen**</span></span>
 
   ![Erstellen neuer Dokumente im Daten-Explorer im Azure-Portal](../media-draft/2-add-data/azure-cosmosdb-data-explorer-full-screen.png)

2. <span data-ttu-id="2b77c-112">Klicken Sie im Feld **Vollbildmodus öffnen** auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="2b77c-112">In the **Open Full Screen** box, click **Open**.</span></span>

    <span data-ttu-id="2b77c-113">Im Webbrowser wird der neue Daten-Explorer im Vollbildmodus angezeigt. Dadurch haben Sie mehr Platz und verfügen über eine dedizierte Umgebung für die Arbeit mit Ihrer Datenbank.</span><span class="sxs-lookup"><span data-stu-id="2b77c-113">The web browser displays the new full screen Data Explorer, which gives you more space and a dedicated environment for working with your database.</span></span>

3. <span data-ttu-id="2b77c-114">Klicken Sie auf **Neues Dokument**, um ein neues JSON-Dokument zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="2b77c-114">To create a new json document, click **New Document**.</span></span>

   ![Erstellen neuer Dokumente im Daten-Explorer im Azure-Portal](../media-draft/2-add-data/azure-cosmosdb-data-explorer-new-document.png)

4. <span data-ttu-id="2b77c-116">Nun können Sie ein Dokument in der folgenden Struktur zur Sammlung hinzufügen. Kopieren Sie dafür einfach den folgenden Code, und fügen Sie diesen auf der Registerkarte **Dokumente** ein.</span><span class="sxs-lookup"><span data-stu-id="2b77c-116">Now add a document to the collection with the following structure, just copy and paste the following code into the **Documents** tab.</span></span>

     ```
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "shipping": {
            "weight": 1,
            "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
           }
        }
     ```

5. <span data-ttu-id="2b77c-117">Nachdem Sie den JSON-Code auf der Registerkarte **Dokumente** hinzugefügt haben, klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="2b77c-117">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Kopieren Sie JSON-Daten, und klicken Sie im Azure-Portal im Daten-Explorer auf „Speichern“.](../media-draft/2-add-data/azure-cosmosdb-data-explorer-save-document.png)

6. <span data-ttu-id="2b77c-119">Erstellen und speichern Sie ein weiteres Dokument, indem Sie das folgende JSON-Objekt in den Daten-Explorer kopieren und auf **Speichern** klicken.</span><span class="sxs-lookup"><span data-stu-id="2b77c-119">Create and save one more document by copying the following json object into Data Explorer and clicking **Save**.</span></span>

     ```
    {
        "id": "2",
        "productId": "33218897",
        "category": "Women's Outerwear",
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
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

7. <span data-ttu-id="2b77c-120">Vergewissern Sie sich, dass die Dokumente gespeichert wurden, indem Sie im linken Menü auf **Dokumente** klicken.</span><span class="sxs-lookup"><span data-stu-id="2b77c-120">Confirm the documents have been saved by clicking **Documents** on the left-hand menu.</span></span> 

    <span data-ttu-id="2b77c-121">Die beiden Dokumente werden im Daten-Explorer auf der Registerkarte **Dokumente** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2b77c-121">Data Explorer displays the two documents in the **Documents** tab.</span></span>

## <a name="summary"></a><span data-ttu-id="2b77c-122">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="2b77c-122">Summary</span></span>

<span data-ttu-id="2b77c-123">In diesem Modul haben Sie Ihrer Datenbank mithilfe des Daten-Explorers zwei Dokumente hinzugefügt, die jeweils ein Produkt in Ihrem Produktkatalog darstellen.</span><span class="sxs-lookup"><span data-stu-id="2b77c-123">In this module you added two documents, each representing a product in your product catalog, to your database by using the Data Explorer.</span></span> <span data-ttu-id="2b77c-124">Der Daten-Explorer eignet sich sehr gut, um Dokumente zu erstellen, Dokumente zu ändern und sich mit Azure Cosmos DB vertraut zu machen.</span><span class="sxs-lookup"><span data-stu-id="2b77c-124">The Data Explorer is a good way to create documents, modify documents, and get started with Azure Cosmos DB.</span></span>  
