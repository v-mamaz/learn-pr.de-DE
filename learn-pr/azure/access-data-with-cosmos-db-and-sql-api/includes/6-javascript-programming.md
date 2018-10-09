<span data-ttu-id="69577-101">Mehrere Dokumente in Ihrer Datenbank müssen häufig zur gleichen Zeit aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="69577-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> 

<span data-ttu-id="69577-102">Wenn ein Benutzer in Ihrer Anwendung für den Onlineeinzelhandel eine Bestellung aufgibt und einen Gutscheincode, eine Gutschrift oder einen Gewinn (oder alle drei auf einmal) einlöst, müssen Sie sein Konto nach diesen Optionen abfragen, Aktualisierungen an seinem Konto vornehmen, um anzugeben, dass eine Rabattaktion verwendet wurde, die Bestellsumme aktualisieren und die Bestellung verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="69577-102">For your online retail application, when a user places an order and wants to use a coupon code, a credit, or a dividend (or all three at once), you need to query their account for those options, make updates to their account indicating they used them, update the order total, and process the order.</span></span>

<span data-ttu-id="69577-103">Diese Aktionen müssen alle gleichzeitig innerhalb einer Transaktion durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="69577-103">All of these actions need to happen at the same time, within a single transaction.</span></span> <span data-ttu-id="69577-104">Wenn der Benutzer den Bestellvorgang abbricht, sollten Sie ein Rollback ausführen und die Kontoinformationen nicht ändern, sodass der Gutscheincode, die Gutschrift oder die Gewinnsumme beim nächsten Einkauf eingelöst werden können.</span><span class="sxs-lookup"><span data-stu-id="69577-104">If the user chooses to cancel the order, you want to roll back the changes and not modify their account information, so that their coupon codes, credits, and dividends are available for their next purchase.</span></span>

<span data-ttu-id="69577-105">Diese Art von Transaktionen können Sie in Azure Cosmos DB ausführen, indem Sie gespeicherte Prozeduren und benutzerdefinierte Funktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="69577-105">The way to perform these transactions in Azure Cosmos DB is by using stored procedures and user-defined functions (UDFs).</span></span> <span data-ttu-id="69577-106">Gespeicherte Prozeduren sind die einzige Möglichkeit, ACID-Transaktionen (Atomarität, Konsistenz, Isolation, Dauerhaftigkeit) sicherzustellen, da sie auf dem Server ausgeführt werden. Sie werden daher als serverseitige Programmierung bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="69577-106">Stored procedures are the only way to ensure ACID (Atomicity, Consistency, Isolation, Durability) transactions because they are run on the server, and are thus referred to as server-side programming.</span></span> <span data-ttu-id="69577-107">Auch benutzerdefinierte Funktionen werden auf dem Server gespeichert und innerhalb von Abfragen verwendet, um Rechenlogik auf Werte oder Dokumente in der Abfrage anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="69577-107">UDFs are also stored on the server and are used during queries to perform computational logic on values or documents within the query.</span></span> 

<span data-ttu-id="69577-108">In diesem Modul erhalten Sie Informationen zu gespeicherten Prozeduren und benutzerdefinierten Funktionen. Anschließend wird erläutert, wie Sie diese im Portal ausführen.</span><span class="sxs-lookup"><span data-stu-id="69577-108">In this module, you'll learn about stored procedures and UDFs, and then run some in the portal.</span></span>

## <a name="stored-procedure-basics"></a><span data-ttu-id="69577-109">Grundlagen zu gespeicherten Prozeduren</span><span class="sxs-lookup"><span data-stu-id="69577-109">Stored procedure basics</span></span>

<span data-ttu-id="69577-110">Gespeicherte Prozeduren führen komplexe Transaktionen für Dokumente und Eigenschaften aus.</span><span class="sxs-lookup"><span data-stu-id="69577-110">Stored procedures perform complex transactions on documents and properties.</span></span> <span data-ttu-id="69577-111">Sie werden in JavaScript geschrieben und in Azure Cosmos DB in einer Sammlung gespeichert.</span><span class="sxs-lookup"><span data-stu-id="69577-111">Stored procedures are written in JavaScript and are stored in a collection on Azure Cosmos DB.</span></span> <span data-ttu-id="69577-112">Wenn Sie gespeicherte Prozeduren für die Datenbank-Engine und in der Nähe der Daten ausführen, können Sie die Leistung mithilfe clientseitiger Programmierung verbessern.</span><span class="sxs-lookup"><span data-stu-id="69577-112">By performing the stored procedures on the database engine and close to the data, you can improve performance over client-side programming.</span></span>

<span data-ttu-id="69577-113">Gespeicherte Prozeduren stellen die einzige Möglichkeit dar, atomische Transaktionen in Azure Cosmos DB zu erzielen. Clientseitige SDKs unterstützen keine Transaktionen.</span><span class="sxs-lookup"><span data-stu-id="69577-113">Stored procedures are the only way to achieve atomic transactions within Azure Cosmos DB; the client-side SDKs do not support transactions.</span></span>

<span data-ttu-id="69577-114">Außerdem wird empfohlen, Batchvorgänge in gespeicherten Prozeduren auszuführen, da dann weniger separate Transaktionen erstellt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="69577-114">Performing batch operations in stored procedures is also recommended because of the reduced need to create separate transactions.</span></span>

## <a name="stored-procedure-example"></a><span data-ttu-id="69577-115">Beispiel für eine gespeicherte Prozedur</span><span class="sxs-lookup"><span data-stu-id="69577-115">Stored procedure example</span></span>

<span data-ttu-id="69577-116">Bei dem folgenden Beispiel handelt es sich um eine einfache gespeicherten HelloWorld-Prozedur, die den aktuellen Kontext abruft und eine Antwort sendet, die „Hello, World“ anzeigt.</span><span class="sxs-lookup"><span data-stu-id="69577-116">The following sample is a simple HelloWorld stored procedure that gets the current context and sends a response that displays "Hello, World".</span></span>

```javascript
function helloWorld() {
    var context = getContext();
    var response = context.getResponse();

    response.setBody("Hello, World");
}
```

## <a name="user-defined-function-basics"></a><span data-ttu-id="69577-117">Grundlagen zu benutzerdefinierten Funktionen</span><span class="sxs-lookup"><span data-stu-id="69577-117">User-defined function basics</span></span>

<span data-ttu-id="69577-118">Mithilfe von benutzerdefinierten Funktionen (UDFs) ist es möglich, die Grammatik der SQL-Abfragesprache von Azure Cosmos DB zu erweitern und eine benutzerdefinierte Geschäftslogik wie Berechnungen für Eigenschaften und Dokumente zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="69577-118">UDFs are used to extend the Azure Cosmos DB SQL query language grammar and implement custom business logic, such as calculations on properties and documents.</span></span> <span data-ttu-id="69577-119">Benutzerdefinierte Funktionen können anders als gespeicherte Prozeduren nur innerhalb von Abfragen aufgerufen werden. Sie besitzen keinen Zugriff auf das Kontextobjekt und können daher Dokumente weder lesen noch schreiben.</span><span class="sxs-lookup"><span data-stu-id="69577-119">UDFs can be called only from inside queries and, unlike stored procedures, they do not have access to the context object, so they cannot read or write documents.</span></span>

<span data-ttu-id="69577-120">In einer Anwendung für den Onlineeinzelhandel sollten benutzerdefinierte Funktionen verwendet werden, um die Umsatzsteuer für eine Bestellung zu ermitteln oder einen Rabatt auf ein Produkt oder eine Bestellung anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="69577-120">In an online commerce scenario, a UDF could be used to determine the sales tax to apply to an order total or a percentage discount to apply to products or orders.</span></span>

## <a name="user-defined-function-example"></a><span data-ttu-id="69577-121">Beispiel für eine benutzerdefinierte Funktion</span><span class="sxs-lookup"><span data-stu-id="69577-121">User-defined function example</span></span>

<span data-ttu-id="69577-122">Das folgende Beispiel erstellt eine benutzerdefinierte Funktion zur Berechnung der Steuer auf ein Produkt in einem fiktiven Unternehmen auf Basis der Produktkosten:</span><span class="sxs-lookup"><span data-stu-id="69577-122">The following sample creates a UDF to calculate tax on a product in a fictitious company based the product cost:</span></span>

```javascript
function producttax(price) {
    if (price == undefined) 
        throw 'no input';

    var amount = parseFloat(price);

    if (amount < 1000) 
        return amount * 0.1;
    else if (amount < 10000) 
        return amount * 0.2;
    else
        return amount * 0.4;
}
```

## <a name="create-a-stored-procedure-in-the-portal"></a><span data-ttu-id="69577-123">Erstellen einer gespeicherten Prozedur im Portal</span><span class="sxs-lookup"><span data-stu-id="69577-123">Create a stored procedure in the portal</span></span>

<span data-ttu-id="69577-124">Nachfolgend wird erläutert, wie Sie eine neue gespeicherte Prozedur im Portal erstellen.</span><span class="sxs-lookup"><span data-stu-id="69577-124">Let's create a new stored procedure in the portal.</span></span> <span data-ttu-id="69577-125">Das Portal füllt automatisch eine einfache gespeicherte Prozedur auf, die das erste Element in der Sammlung aufruft, damit diese als erstes ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="69577-125">The portal automatically populates a simple stored procedure that retrieves the first item in the collection, so we'll run this stored procedure first.</span></span>

1. <span data-ttu-id="69577-126">Klicken Sie im Daten-Explorer auf **Neue gespeicherte Prozedur**.</span><span class="sxs-lookup"><span data-stu-id="69577-126">In the Data Explorer, click **New Stored Procedure**.</span></span>

    <span data-ttu-id="69577-127">Im Daten-Explorer wird eine neue Registerkarte mit einem Beispiel für eine gespeicherte Prozedur angezeigt.</span><span class="sxs-lookup"><span data-stu-id="69577-127">Data Explorer displays a new tab with a sample stored procedure.</span></span>

2. <span data-ttu-id="69577-128">Geben Sie in das Feld **ID der gespeicherten Prozedur** den Namen *sample* ein, klicken Sie auf **Speichern** und dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="69577-128">In the **Stored Procedure Id** box, enter the name *sample*, click **Save**, and then click **Execute**.</span></span>


3. <span data-ttu-id="69577-129">Geben Sie in das Feld **Eingabeparameter** den Namen eines Partitionsschlüssels (*33218896*) ein, und klicken Sie dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="69577-129">In the **Input parameters** box, type the name of a partition key, *33218896*, and then click **Execute**.</span></span> <span data-ttu-id="69577-130">Beachten Sie, dass gespeicherte Prozeduren innerhalb einer Partition ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="69577-130">Note that stored procedures work within a single partition.</span></span>

    ![Ausführen einer gespeicherten Prozedur im Portal](../media/6-stored-procedure.gif)

    <span data-ttu-id="69577-132">Im Bereich **Ergebnis** wird der Feed aus dem ersten Dokument in der Sammlung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="69577-132">The **Result** pane displays the feed from the first document in the collection.</span></span>

## <a name="create-a-stored-procedure-that-creates-documents"></a><span data-ttu-id="69577-133">Erstellen einer gespeicherten Prozedur, die Dokumente erstellt</span><span class="sxs-lookup"><span data-stu-id="69577-133">Create a stored procedure that creates documents</span></span>

<span data-ttu-id="69577-134">Nachfolgend wird erläutert, wie Sie eine gespeicherte Prozedur erstellen, die Dokumente erstellt.</span><span class="sxs-lookup"><span data-stu-id="69577-134">Now, let's create a stored procedure that creates documents.</span></span>

1. <span data-ttu-id="69577-135">Klicken Sie im Daten-Explorer auf **Neue gespeicherte Prozedur**.</span><span class="sxs-lookup"><span data-stu-id="69577-135">In the Data Explorer, click **New Stored Procedure**.</span></span> <span data-ttu-id="69577-136">Nennen Sie diese gespeicherte Prozedur *createMyDocument*. Kopieren Sie den folgenden Code, und fügen Sie ihn in das Feld **Text der gespeicherten Prozedur** ein. Klicken Sie auf **Speichern** und dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="69577-136">Name this stored procedure *createMyDocument*, copy and paste the following code into the **Stored Procedure Body** box, click **Save**, and then click **Execute**.</span></span>

    ```javascript
    function createMyDocument() {
        var context = getContext();
        var collection = context.getCollection();

        var doc = {
            "id": "3",
            "productId": "33218898",
            "description": "Contoso microfleece zip-up jacket",
            "price": "44.99"
        };

        var accepted = collection.createDocument(collection.getSelfLink(),
            doc,
            function (err, documentCreated) {
                if (err) throw new Error('Error' + err.message);
                context.getResponse().setBody(documentCreated)
            });
        if (!accepted) return;
    }
    ```

2. <span data-ttu-id="69577-137">Geben Sie in das Feld „Eingabeparameter“ den Partitionsschlüssels *33218898* ein, und klicken Sie dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="69577-137">In the Input parameters box, enter a Partition Key Value of *33218898*, and then click **Execute**.</span></span>

    <span data-ttu-id="69577-138">Der Daten-Explorer zeigt das neu erstellte Dokument im Bereich „Ergebnis“ an.</span><span class="sxs-lookup"><span data-stu-id="69577-138">Data Explorer displays the newly created document in the Result area.</span></span>

    <span data-ttu-id="69577-139">Sie können erneut die Registerkarte „Dokumente“ aufrufen. Klicken Sie auf **Aktualisieren**, um sich das neue Dokument anzeigen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="69577-139">You can go back to the Documents tab, click the **Refresh** button and see the new document.</span></span> 

## <a name="create-a-user-defined-function"></a><span data-ttu-id="69577-140">Erstellen einer benutzerdefinierten Funktion</span><span class="sxs-lookup"><span data-stu-id="69577-140">Create a user-defined function</span></span>

<span data-ttu-id="69577-141">Nun erstellen wir eine benutzerdefinierte Funktion im Daten-Explorer.</span><span class="sxs-lookup"><span data-stu-id="69577-141">Now, let's create a UDF in Data Explorer.</span></span>

<span data-ttu-id="69577-142">Klicken Sie im Daten-Explorer auf **New UDF** (Neue benutzerdefinierte Funktion).</span><span class="sxs-lookup"><span data-stu-id="69577-142">In the Data Explorer, click **New UDF**.</span></span> <span data-ttu-id="69577-143">Möglicherweise müssen Sie auf den Abwärtspfeil neben **New Stored Prodedure** (Neue gespeicherte Prozedur) klicken, damit **New UDF**(Neue benutzerdefinierte Funktion) angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="69577-143">You may need to click the down arrow next to **New Stored Prodedure** to see **New UDF**.</span></span> <span data-ttu-id="69577-144">Kopieren Sie den folgenden Code in das Fenster, geben Sie der benutzerdefinierten Funktion den Namen *producttax*, und klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="69577-144">Copy the following code into the window, name the UDF *producttax*, and then click **Save**.</span></span>

```javascript
function producttax(price) {
    if (price == undefined) 
        throw 'no input';

    var amount = parseFloat(price);

    if (amount < 1000) 
        return amount * 0.1;
    else if (amount < 10000) 
        return amount * 0.2;
    else
        return amount * 0.4;
}
```

<span data-ttu-id="69577-145">Wechseln Sie nach der Erstellung der benutzerdefinierten Funktion zur Registerkarte **Query 1** (Abfrage 1), kopieren Sie die folgende Abfrage, und fügen Sie sie in den Abfragebereich ein, um die benutzerdefinierte Funktion auszuführen.</span><span class="sxs-lookup"><span data-stu-id="69577-145">Once you have defined the UDF, go to the **Query 1** tab and copy and paste the following query into the query area to run the UDF.</span></span>

```sql
SELECT c.id, c.productId, c.price, udf.producttax(c.price) AS producttax FROM c
```
