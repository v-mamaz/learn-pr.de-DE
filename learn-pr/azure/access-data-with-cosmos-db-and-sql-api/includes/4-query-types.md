<span data-ttu-id="515b4-101">Nachfolgend werden einige Grundlagen zu Abfragen erläutert. Die beiden Dokumente, die Sie der Datenbank hinzugefügt haben, sollen als Ziel für die Beispielabfragen dienen.</span><span class="sxs-lookup"><span data-stu-id="515b4-101">Using the two documents you added to the database as the target of our queries, let's walk through some query basics.</span></span> <span data-ttu-id="515b4-102">Genauso wie SQL Server verwendet Azure Cosmos DB SQL-Abfragen, um Abfragevorgänge durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="515b4-102">Azure Cosmos DB uses SQL queries, just like SQL Server, to perform query operations.</span></span> <span data-ttu-id="515b4-103">Sämtliche Eigenschaften werden standardmäßig automatisch indiziert, sodass alle Daten in der Datenbank unmittelbar zur Abfrage zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="515b4-103">All properties are automatically indexed by default, so all data in the database is instantly available to query.</span></span>

## <a name="sql-query-basics"></a><span data-ttu-id="515b4-104">Grundlagen zu SQL-Abfragen</span><span class="sxs-lookup"><span data-stu-id="515b4-104">SQL query basics</span></span>
<span data-ttu-id="515b4-105">Jede SQL-Abfrage besteht aus einer SELECT-Klausel und optionalen FROM- und WHERE-Klauseln.</span><span class="sxs-lookup"><span data-stu-id="515b4-105">Every SQL query consists of a SELECT clause and optional FROM and WHERE clauses.</span></span> <span data-ttu-id="515b4-106">Außerdem können Sie andere Klauseln wie ORDER BY und JOIN hinzufügen, um die erforderlichen Informationen abzufragen.</span><span class="sxs-lookup"><span data-stu-id="515b4-106">In addition, you can add other clauses like ORDER BY and JOIN to get the information you need.</span></span>

<span data-ttu-id="515b4-107">SQL-Abfragen haben das folgende Format:</span><span class="sxs-lookup"><span data-stu-id="515b4-107">A SQL query has the following format:</span></span>

    SELECT <select_list>
    [FROM <optional_from_specification>]
    [WHERE <optional_filter_condition>]
    [ORDER BY <optional_sort_specification>]
    [JOIN <optional_join_specification>]

## <a name="select-clause"></a><span data-ttu-id="515b4-108">SELECT-Klausel</span><span class="sxs-lookup"><span data-stu-id="515b4-108">SELECT clause</span></span>

<span data-ttu-id="515b4-109">Die SELECT-Klausel bestimmt den Typ der Werte, die erstellt werden, wenn die Abfrage ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="515b4-109">The SELECT clause determines the type of values that will be produced when the query is executed.</span></span> <span data-ttu-id="515b4-110">Bei einem Wert vom Typ `SELECT *` wird das gesamte JSON-Dokument zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="515b4-110">A value of `SELECT *` indicates that the entire JSON document is returned.</span></span>

<span data-ttu-id="515b4-111">**Abfrage**</span><span class="sxs-lookup"><span data-stu-id="515b4-111">**Query**</span></span>
```
SELECT *
FROM Products p
WHERE p.id ="1"
```

<span data-ttu-id="515b4-112">**Rückgaben**</span><span class="sxs-lookup"><span data-stu-id="515b4-112">**Returns**</span></span>
```
[
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
        },
        "_rid": "iAEeANrzNAAJAAAAAAAAAA==",
        "_self": "dbs/iAEeAA==/colls/iAEeANrzNAA=/docs/iAEeANrzNAAJAAAAAAAAAA==/",
        "_etag": "\"00003a02-0000-0000-0000-5b9208440000\"",
        "_attachments": "attachments/",
        "_ts": 1536297028
    }
]
```

<span data-ttu-id="515b4-113">Stattdessen können Sie auch die Ausgabe einschränken, sodass nur bestimmte Eigenschaften angezeigt werden, indem Sie der SELECT-Klausel eine Liste mit Eigenschaften hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="515b4-113">Or, you can limit the output to include only certain properties by including a list of properties in the SELECT clause.</span></span> <span data-ttu-id="515b4-114">In der folgenden Abfrage werden nur die ID, der Hersteller und die Produktbeschreibung hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="515b4-114">In the following query, only the ID, manufacturer, and product description are returned.</span></span>

<span data-ttu-id="515b4-115">**Abfrage**</span><span class="sxs-lookup"><span data-stu-id="515b4-115">**Query**</span></span>
```
SELECT 
    p.id, 
    p.manufacturer, 
    p.description
FROM Products p
WHERE p.id ="1"
```

<span data-ttu-id="515b4-116">**Rückgaben**</span><span class="sxs-lookup"><span data-stu-id="515b4-116">**Returns**</span></span>
```
[
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
]
```

## <a name="from-clause"></a><span data-ttu-id="515b4-117">FROM-Klausel</span><span class="sxs-lookup"><span data-stu-id="515b4-117">FROM clause</span></span>

<span data-ttu-id="515b4-118">Die FROM-Klausel bestimmt die Datenquelle der Abfrage.</span><span class="sxs-lookup"><span data-stu-id="515b4-118">The FROM clause specifies the data source upon which the query operates.</span></span> <span data-ttu-id="515b4-119">Sie können sowohl die ganze Sammlung als auch ein Subnetz der Sammlung als Abfragequelle festlegen.</span><span class="sxs-lookup"><span data-stu-id="515b4-119">You can make the whole collection the source of the query or you can specify a subset of the collection instead.</span></span> <span data-ttu-id="515b4-120">Die FROM-Klausel ist optional, sofern die Quelle in der Abfrage später nicht gefiltert oder projiziert wird.</span><span class="sxs-lookup"><span data-stu-id="515b4-120">The FROM clause is optional unless the source is filtered or projected later in the query.</span></span>

<span data-ttu-id="515b4-121">Bei einer Abfrage wie `SELECT * FROM Products` ist die gesamte Products-Sammlung die Quelle der Abfrage.</span><span class="sxs-lookup"><span data-stu-id="515b4-121">A query such as `SELECT * FROM Products` indicates that the entire Products collection is the source over which to enumerate the query.</span></span>

<span data-ttu-id="515b4-122">Eine Sammlung kann Aliase enthalten, z.B. `SELECT p.id FROM Products AS p` oder einfach `SELECT p.id FROM Products p`, wobei `p` `Products` entspricht.</span><span class="sxs-lookup"><span data-stu-id="515b4-122">A collection can be aliased, such as `SELECT p.id FROM Products AS p` or simply `SELECT p.id FROM Products p`, where `p` is the equivalent of `Products`.</span></span> <span data-ttu-id="515b4-123">`AS` ist ein optionales Schlüsselwort, das als Alias für den Bezeichner fungiert.</span><span class="sxs-lookup"><span data-stu-id="515b4-123">`AS` is an optional keyword to alias the identifier.</span></span>

<span data-ttu-id="515b4-124">Sobald ein Alias verwendet wird, kann die Originalquelle nicht mehr gebunden werden.</span><span class="sxs-lookup"><span data-stu-id="515b4-124">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="515b4-125">`SELECT Products.id FROM Products p` ist beispielsweise syntaktisch ungültig, da der Bezeichner „Products“ nicht mehr aufgelöst werden kann.</span><span class="sxs-lookup"><span data-stu-id="515b4-125">For example, `SELECT Products.id FROM Products p` is syntactically invalid because the identifier "Products" cannot be resolved anymore.</span></span>

<span data-ttu-id="515b4-126">Alle Eigenschaften, auf die verwiesen wird, müssen vollqualifiziert sein.</span><span class="sxs-lookup"><span data-stu-id="515b4-126">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="515b4-127">Dies ist ohne strikte Schemaverwendung notwendig, um mehrdeutige Bindungen zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="515b4-127">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="515b4-128">Daher ist `SELECT id FROM Products p` syntaktisch ungültig, weil die `id`-Eigenschaft nicht gebunden ist.</span><span class="sxs-lookup"><span data-stu-id="515b4-128">Therefore, `SELECT id FROM Products p` is syntactically invalid because the property `id` is not bound.</span></span>

### <a name="subdocuments-in-a-from-clause"></a><span data-ttu-id="515b4-129">Unterdokumente in einer FROM-Klausel</span><span class="sxs-lookup"><span data-stu-id="515b4-129">Subdocuments in a FROM clause</span></span>
<span data-ttu-id="515b4-130">Die Quelle kann auch auf eine kleinere Teilmenge reduziert werden.</span><span class="sxs-lookup"><span data-stu-id="515b4-130">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="515b4-131">Wenn Sie beispielsweise nur eine Unterstruktur in jedem Dokument auflisten möchten, kann deren Unterstamm wie im folgenden Beispiel gezeigt als Quelle fungieren:</span><span class="sxs-lookup"><span data-stu-id="515b4-131">For instance, to enumerate only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="515b4-132">**Abfrage**</span><span class="sxs-lookup"><span data-stu-id="515b4-132">**Query**</span></span>
```
SELECT * 
FROM Products.shipping
```

<span data-ttu-id="515b4-133">**Ergebnisse**</span><span class="sxs-lookup"><span data-stu-id="515b4-133">**Results**</span></span>  

```
[
    {
        "weight": 1,
        "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
        }
    },
    {
        "weight": 2,
        "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
        }
    }
]
```

<span data-ttu-id="515b4-134">Im obigen Beispiel wird zwar ein Array als Quelle verwendet, aber Sie können dafür auch wie im folgenden Beispiel ein Objekt verwenden:</span><span class="sxs-lookup"><span data-stu-id="515b4-134">Although the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example.</span></span> <span data-ttu-id="515b4-135">Jeder gültige JSON-Wert (mit Ausnahme von „Undefined“), der in der Quelle gefunden werden kann, wird für die Integration in das Abfrageergebnis herangezogen.</span><span class="sxs-lookup"><span data-stu-id="515b4-135">Any valid JSON value (that's not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="515b4-136">Produkte ohne `shipping.weight`-Wert werden aus dem Abfrageergebnis ausgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="515b4-136">If some products don’t have a `shipping.weight` value, they are excluded in the query result.</span></span>

<span data-ttu-id="515b4-137">**Abfrage**</span><span class="sxs-lookup"><span data-stu-id="515b4-137">**Query**</span></span>

    SELECT * 
    FROM Products.shipping.weight

<span data-ttu-id="515b4-138">**Ergebnisse**</span><span class="sxs-lookup"><span data-stu-id="515b4-138">**Results**</span></span>

    [
        1,
        2
    ]

## <a name="where-clause"></a><span data-ttu-id="515b4-139">WHERE-Klausel</span><span class="sxs-lookup"><span data-stu-id="515b4-139">WHERE clause</span></span>
<span data-ttu-id="515b4-140">Die WHERE-Klausel gibt die Bedingungen an, die die in der Quelle angegebenen JSON-Dokumente erfüllen müssen, um als Teil des Ergebnisses zurückgegeben zu werden.</span><span class="sxs-lookup"><span data-stu-id="515b4-140">The WHERE clause specifies the conditions that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="515b4-141">Jedes JSON-Dokument muss die angegebenen Bedingungen erfüllen (**true**), um in das Ergebnis einbezogen zu werden.</span><span class="sxs-lookup"><span data-stu-id="515b4-141">Any JSON document must evaluate the specified conditions to **true** to be considered for the result.</span></span> <span data-ttu-id="515b4-142">Die WHERE-Klausel ist optional.</span><span class="sxs-lookup"><span data-stu-id="515b4-142">The WHERE clause is optional.</span></span>

<span data-ttu-id="515b4-143">Mit der folgenden Abfrage werden Dokumente angefordert, die eine ID mit dem Wert „1“ enthalten:</span><span class="sxs-lookup"><span data-stu-id="515b4-143">The following query requests documents that contain an ID whose value is 1:</span></span>

<span data-ttu-id="515b4-144">**Abfrage**</span><span class="sxs-lookup"><span data-stu-id="515b4-144">**Query**</span></span>

    SELECT p.description
    FROM Products p 
    WHERE p.id = "1"

<span data-ttu-id="515b4-145">**Ergebnisse**</span><span class="sxs-lookup"><span data-stu-id="515b4-145">**Results**</span></span>

    [
        {
            "description": "Quick dry crew neck t-shirt"
        }
    ]

## <a name="order-by-clause"></a><span data-ttu-id="515b4-146">ORDER BY-Klausel</span><span class="sxs-lookup"><span data-stu-id="515b4-146">ORDER BY clause</span></span>

<span data-ttu-id="515b4-147">Mit der ORDER BY-Klausel können Sie die Ergebnisse in aufsteigender oder absteigender Reihenfolge sortieren.</span><span class="sxs-lookup"><span data-stu-id="515b4-147">The ORDER BY clause enables you to order the results in ascending or descending order.</span></span>

<span data-ttu-id="515b4-148">Die folgende ORDER BY-Abfrage gibt in aufsteigender Reihenfolge der Preise den Preis, die Beschreibung und die Produkt-ID für alle Produkte zurück:</span><span class="sxs-lookup"><span data-stu-id="515b4-148">The following ORDER BY query returns the price, description, and product ID for all products, ordered by price, in ascending order:</span></span>

<span data-ttu-id="515b4-149">**Abfrage**</span><span class="sxs-lookup"><span data-stu-id="515b4-149">**Query**</span></span>

    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC

<span data-ttu-id="515b4-150">**Ergebnisse**</span><span class="sxs-lookup"><span data-stu-id="515b4-150">**Results**</span></span>

```
[
    {
        "price": "14.99",
        "description": "Quick dry crew neck t-shirt",
        "productId": "33218896"
    },
    {
        "price": "49.99",
        "description": "Black wool pea-coat",
        "productId": "33218897"
    }
]
```

## <a name="join-clause"></a><span data-ttu-id="515b4-151">JOIN-Klausel</span><span class="sxs-lookup"><span data-stu-id="515b4-151">JOIN clause</span></span>

<span data-ttu-id="515b4-152">Mit der JOIN-Klausel können Sie innere Joins für das Dokument und dessen Unterstämme ausführen.</span><span class="sxs-lookup"><span data-stu-id="515b4-152">The JOIN clause enables you to perform inner joins with the document and the document subroots.</span></span> <span data-ttu-id="515b4-153">Sie können also beispielsweise in der Produktdatenbank Dokumente mit den Versanddaten verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="515b4-153">So in the product database, for example, you can join the documents with the shipping data.</span></span>  

<span data-ttu-id="515b4-154">In der folgenden Abfrage werden die Produkt-IDs der einzelnen Produkte zurückgegeben, für die eine Versandmethode angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="515b4-154">In the following query, the product IDs are returned for each product that has a shipping method.</span></span> <span data-ttu-id="515b4-155">Wenn Sie ein drittes Produkt ohne Versandeigenschaft hinzufügen, wird dasselbe Ergebnis zurückgegeben, da es aufgrund fehlender Versandeigenschaften ausgeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="515b4-155">If you added a third product that didn't have a shipping property, the result would be the same because the third item would be excluded for not having a shipping property.</span></span>

<span data-ttu-id="515b4-156">**Abfrage**</span><span class="sxs-lookup"><span data-stu-id="515b4-156">**Query**</span></span>

    SELECT p.productId
    FROM Products p
    JOIN p.shipping

<span data-ttu-id="515b4-157">**Ergebnisse**</span><span class="sxs-lookup"><span data-stu-id="515b4-157">**Results**</span></span>

    [
        {
            "productId": "33218896"
        },
        {
            "productId": "33218897"
        }
    ]

## <a name="geospatial-queries"></a><span data-ttu-id="515b4-158">Geoabfragen</span><span class="sxs-lookup"><span data-stu-id="515b4-158">Geospatial queries</span></span>

<span data-ttu-id="515b4-159">Sie können Geoabfragen mithilfe von GeoJSON-Punkten ausführen.</span><span class="sxs-lookup"><span data-stu-id="515b4-159">Geospatial queries enable you to perform spatial queries using GeoJSON Points.</span></span> <span data-ttu-id="515b4-160">Wenn Sie die Koordinaten in der Datenbank verwenden, können Sie die Entfernung zwischen zwei Punkten berechnen und ermitteln, ob sich ein Punkt, ein Polygon oder ein LineString-Element innerhalb eines anderen Punkts, Polygons oder LineString-Elements befindet.</span><span class="sxs-lookup"><span data-stu-id="515b4-160">Using the coordinates in the database, you can calculate the distance between two points and determine whether a Point, Polygon, or LineString is within another Point, Polygon, or LineString.</span></span>

<span data-ttu-id="515b4-161">Hierdurch kann der Benutzer für Produktkatalogdaten seine Standortinformationen eingeben und prüfen, ob es innerhalb eines Radius von 80 Kilometern ein Geschäft gibt, in dem der gesuchte Artikel verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="515b4-161">For product catalog data, this would enable your users to enter their location information and determine whether there were any stores within a 50-mile radius that have the item they're looking for.</span></span> 

## <a name="summary"></a><span data-ttu-id="515b4-162">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="515b4-162">Summary</span></span>

<span data-ttu-id="515b4-163">Wenn Sie in der Lage sind, Ihre gesamten Daten schnell abzufragen, nachdem Sie sie Azure Cosmos DB hinzugefügt haben, und bekannte SQL-Abfragetechniken zu verwenden, können Sie und Ihre Kunden Einblicke in gespeicherte Daten gewinnen.</span><span class="sxs-lookup"><span data-stu-id="515b4-163">Being able to quickly query all your data after adding it to Azure Cosmos DB and using familiar SQL query techniques can help you and your customers to explore and gain insights into your stored data.</span></span>