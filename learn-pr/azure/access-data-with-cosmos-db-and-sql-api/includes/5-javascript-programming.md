<span data-ttu-id="d4bad-101">Mehrere Dokumente in Ihrer Datenbank müssen häufig zur gleichen Zeit aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="d4bad-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> 

<span data-ttu-id="d4bad-102">Wenn ein Benutzer in Ihrer Anwendung für den Onlineeinzelhandel eine Bestellung aufgibt und einen Gutscheincode, eine Gutschrift oder einen Gewinn (oder alle drei auf einmal) einlöst, müssen Sie sein Konto nach diesen Optionen abfragen, Aktualisierungen an seinem Konto vornehmen, um anzugeben, dass eine Rabattaktion verwendet wurde, die Bestellsumme aktualisieren und die Bestellung verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="d4bad-102">For your online retail application, when a user places an order and wants to use a coupon code, a credit, or a dividend (or all three at once), you need to query their account for those options, make updates to their account indicating they used them, update the order total, and process the order.</span></span>

<span data-ttu-id="d4bad-103">Diese Aktionen müssen alle gleichzeitig innerhalb einer Transaktion durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="d4bad-103">All of these actions need to happen at the same time, within a single transaction.</span></span> <span data-ttu-id="d4bad-104">Wenn der Benutzer den Bestellvorgang abbricht, sollten Sie ein Rollback ausführen und die Kontoinformationen nicht ändern, sodass der Gutscheincode, die Gutschrift oder die Gewinnsumme beim nächsten Einkauf eingelöst werden können.</span><span class="sxs-lookup"><span data-stu-id="d4bad-104">If the user chooses to cancel the order, you want to roll back the changes and not modify their account information, so that their coupon codes, credits, and dividends are available for their next purchase.</span></span>

<span data-ttu-id="d4bad-105">Diese Art von Transaktionen können Sie in Azure Cosmos DB ausführen, indem Sie gespeicherte Prozeduren und benutzerdefinierte Funktionen verwenden.</span><span class="sxs-lookup"><span data-stu-id="d4bad-105">The way to perform these transactions in Azure Cosmos DB is by using stored procedures and user-defined functions (UDFs).</span></span> <span data-ttu-id="d4bad-106">Gespeicherte Prozeduren sind die einzige Möglichkeit, ACID-Transaktionen (Atomarität, Konsistenz, Isolation, Dauerhaftigkeit) sicherzustellen, da sie auf dem Server ausgeführt werden. Sie werden daher als serverseitige Programmierung bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="d4bad-106">Stored procedures are the only way to ensure ACID (Atomicity, Consistency, Isolation, Durability) transactions because they are run on the server, and are thus referred to as server-side programming.</span></span> <span data-ttu-id="d4bad-107">Auch benutzerdefinierte Funktionen werden auf dem Server gespeichert und innerhalb von Abfragen verwendet, um Rechenlogik auf Werte oder Dokumente in der Abfrage anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="d4bad-107">UDFs are also stored on the server and are used during queries to perform computational logic on values or documents within the query.</span></span> 

<span data-ttu-id="d4bad-108">In diesem Modul erhalten Sie Informationen zu gespeicherten Prozeduren und benutzerdefinierten Funktionen. Anschließend wird erläutert, wie Sie diese im Portal ausführen.</span><span class="sxs-lookup"><span data-stu-id="d4bad-108">In this module, you'll learn about stored procedures and UDFs, and then run some in the portal.</span></span>

## <a name="stored-procedure-basics"></a><span data-ttu-id="d4bad-109">Grundlagen zu gespeicherten Prozeduren</span><span class="sxs-lookup"><span data-stu-id="d4bad-109">Stored procedure basics</span></span>

<span data-ttu-id="d4bad-110">Gespeicherte Prozeduren führen komplexe Transaktionen für Dokumente und Eigenschaften aus.</span><span class="sxs-lookup"><span data-stu-id="d4bad-110">Stored procedures perform complex transactions on documents and properties.</span></span> <span data-ttu-id="d4bad-111">Sie werden in JavaScript geschrieben und in Azure Cosmos DB in einer Sammlung gespeichert.</span><span class="sxs-lookup"><span data-stu-id="d4bad-111">Stored procedures are written in JavaScript and are stored in a collection on Azure Cosmos DB.</span></span> <span data-ttu-id="d4bad-112">Wenn Sie gespeicherte Prozeduren für die Datenbank-Engine und in der Nähe der Daten ausführen, können Sie die Leistung mithilfe clientseitiger Programmierung verbessern.</span><span class="sxs-lookup"><span data-stu-id="d4bad-112">By performing the stored procedures on the database engine and close to the data, you can improve performance over client-side programming.</span></span>

<span data-ttu-id="d4bad-113">Gespeicherte Prozeduren stellen die einzige Möglichkeit dar, atomische Transaktionen in Azure Cosmos DB zu erzielen. Clientseitige SDKs unterstützen keine Transaktionen.</span><span class="sxs-lookup"><span data-stu-id="d4bad-113">Stored procedures are the only way to achieve atomic transactions within Azure Cosmos DB; the client-side SDKs do not support transactions.</span></span>

<span data-ttu-id="d4bad-114">Außerdem wird empfohlen, Batchvorgänge in gespeicherten Prozeduren auszuführen, da dann weniger separate Transaktionen erstellt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="d4bad-114">Performing batch operations in stored procedures is also recommended because of the reduced need to create separate transactions.</span></span>

<!--TODO: Ideally I'd like to list some cases where a stored procedure is not the best option.-->

## <a name="stored-procedure-example"></a><span data-ttu-id="d4bad-115">Beispiel für eine gespeicherte Prozedur</span><span class="sxs-lookup"><span data-stu-id="d4bad-115">Stored procedure example</span></span>

<span data-ttu-id="d4bad-116">Bei dem folgenden Beispiel handelt es sich um eine einfache gespeicherten HelloWorld-Prozedur, die den aktuellen Kontext abruft und eine Antwort sendet, die „Hello, World“ anzeigt.</span><span class="sxs-lookup"><span data-stu-id="d4bad-116">The following sample is a simple HelloWorld stored procedure that gets the current context and sends a response that displays "Hello, World".</span></span> <span data-ttu-id="d4bad-117">Beachten Sie, dass gespeicherte Prozeduren genauso wie Azure Cosmos DB-Dokumente einen ID-Wert aufweisen.</span><span class="sxs-lookup"><span data-stu-id="d4bad-117">Note that the stored procedure has an ID value, just like Azure Cosmos DB documents.</span></span>

```java
var helloWorldStoredProc = {
    id: "helloWorld",
    serverScript: function () {
        var context = getContext();
        var response = context.getResponse();

        response.setBody("Hello, World");
    }
}
```

## <a name="user-defined-function-basics"></a><span data-ttu-id="d4bad-118">Grundlagen zu benutzerdefinierten Funktionen</span><span class="sxs-lookup"><span data-stu-id="d4bad-118">User-defined function basics</span></span>

<span data-ttu-id="d4bad-119">Mithilfe von benutzerdefinierten Funktionen (UDFs) ist es möglich, die Grammatik der SQL-Abfragesprache von Azure Cosmos DB zu erweitern und eine benutzerdefinierte Geschäftslogik wie Berechnungen für Eigenschaften und Dokumente zu implementieren.</span><span class="sxs-lookup"><span data-stu-id="d4bad-119">UDFs are used to extend the Azure Cosmos DB SQL query language grammar and implement custom business logic, such as calculations on properties and documents.</span></span> <span data-ttu-id="d4bad-120">Benutzerdefinierte Funktionen können anders als gespeicherte Prozeduren nur innerhalb von Abfragen aufgerufen werden. Sie besitzen keinen Zugriff auf das Kontextobjekt und können daher Dokumente weder lesen noch schreiben.</span><span class="sxs-lookup"><span data-stu-id="d4bad-120">UDFs can be called only from inside queries and, unlike stored procedures, they do not have access to the context object, so they cannot read or write documents.</span></span>

<span data-ttu-id="d4bad-121">In einer Anwendung für den Onlineeinzelhandel sollten benutzerdefinierte Funktionen verwendet werden, um die Umsatzsteuer für eine Bestellung zu ermitteln oder einen Rabatt auf ein Produkt oder eine Bestellung anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="d4bad-121">In an online commerce scenario, a UDF could be used to determine the sales tax to apply to an order total or a percentage discount to apply to products or orders.</span></span>

## <a name="user-defined-function-example"></a><span data-ttu-id="d4bad-122">Beispiel zu benutzerdefinierten Funktionen</span><span class="sxs-lookup"><span data-stu-id="d4bad-122">User-defined function example</span></span>

<span data-ttu-id="d4bad-123">Im folgenden Beispiel wird eine benutzerdefinierte Funktion erstellt, um anhand der Gesamtsumme einer Bestellung Rabatte zu berechnen. Anschließend wird die geänderte Bestellsumme zurückgegeben:</span><span class="sxs-lookup"><span data-stu-id="d4bad-123">The following sample creates a UDF to calculate discounts based on an order total, and then it returns the modified order total based on the discount:</span></span>

```java
var discountUdf = {
    id: "discount",
    serverScript: function discount(orderTotal) {

        if(orderTotal == undefined) 
            throw 'no input';

        if (orderTotal < 50) 
            return orderTotal * 0.9;
        else if (orderTotal < 100) 
            return orderTotal * 0.8;
        else
            return orderTotal * 0.7;
    }
}
```

## <a name="create-a-stored-procedure-in-the-portal"></a><span data-ttu-id="d4bad-124">Erstellen einer gespeicherten Prozedur im Portal</span><span class="sxs-lookup"><span data-stu-id="d4bad-124">Create a stored procedure in the portal</span></span>

<span data-ttu-id="d4bad-125">Nachfolgend wird erläutert, wie Sie eine neue gespeicherte Prozedur im Portal erstellen.</span><span class="sxs-lookup"><span data-stu-id="d4bad-125">Let's create a new stored procedure in the portal.</span></span> <span data-ttu-id="d4bad-126">Das Portal füllt automatisch eine einfache gespeicherte Prozedur auf, die das erste Element in der Sammlung aufruft, damit diese als erstes ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="d4bad-126">The portal automatically populates a simple stored procedure that retrieves the first item in the collection, so we'll run this stored procedure first.</span></span>

1. <span data-ttu-id="d4bad-127">Klicken Sie im Daten-Explorer auf **Neue gespeicherte Prozedur**.</span><span class="sxs-lookup"><span data-stu-id="d4bad-127">In the Data Explorer, click **New Stored Procedure**.</span></span>

    <span data-ttu-id="d4bad-128">Im Daten-Explorer wird eine neue Registerkarte mit einem Beispiel für eine gespeicherte Prozedur angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d4bad-128">Data Explorer displays a new tab with a sample stored procedure.</span></span>

  <!--TODO: Insert animated .gif of creating the stored procedure.-->

2. <span data-ttu-id="d4bad-129">Geben Sie in das Feld **ID der gespeicherten Prozedur** den Namen *sample* ein, klicken Sie auf **Speichern** und dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="d4bad-129">In the **Stored Procedure Id** box, enter the name *sample*, click **Save**, and then click **Execute**.</span></span>


3. <span data-ttu-id="d4bad-130">Geben Sie in das Feld **Eingabeparameter** den Namen eines Partitionsschlüssels (*33218896*) ein, und klicken Sie dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="d4bad-130">In the **Input parameters** box, type the name of a partition key, *33218896*, and then click **Execute**.</span></span> <span data-ttu-id="d4bad-131">Beachten Sie, dass gespeicherte Prozeduren innerhalb einer Partition ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="d4bad-131">Note that stored procedures work within a single partition.</span></span>

    ![Ausführen einer gespeicherten Prozedur im Portal](../media-draft/5-javascript-programming/stored-procedure.gif)

    <span data-ttu-id="d4bad-133">Im Bereich **Ergebnis** wird der Feed aus dem ersten Dokument in der Sammlung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d4bad-133">The **Result** pane displays the feed from the first document in the collection.</span></span>

## <a name="create-a-stored-procedure-that-creates-documents"></a><span data-ttu-id="d4bad-134">Erstellen einer gespeicherten Prozedur, die Dokumente erstellt</span><span class="sxs-lookup"><span data-stu-id="d4bad-134">Create a stored procedure that creates documents</span></span>

<span data-ttu-id="d4bad-135">Nachfolgend wird erläutert, wie Sie eine gespeicherte Prozedur erstellen, die Dokumente erstellt.</span><span class="sxs-lookup"><span data-stu-id="d4bad-135">Now, let's create a stored procedure that creates documents.</span></span>

1. <span data-ttu-id="d4bad-136">Klicken Sie im Daten-Explorer auf **Neue gespeicherte Prozedur**.</span><span class="sxs-lookup"><span data-stu-id="d4bad-136">In the Data Explorer, click **New Stored Procedure**.</span></span> <span data-ttu-id="d4bad-137">Nennen Sie diese gespeicherte Prozedur *createDocuments*, und klicken Sie auf **Speichern** und dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="d4bad-137">Name this stored procedure *createDocuments*, click **Save**, and then click **Execute**.</span></span>

    ```java
    var createDocumentStoredProc = {
        id: "createMyDocument",
        productid: "5"
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();
    
            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }
    ```

<!--TODO: Need to fix code above.-->

2. <span data-ttu-id="d4bad-138">Geben Sie den Partitionsschlüsselwert *3* ein, und klicken Sie dann auf **Ausführen**.</span><span class="sxs-lookup"><span data-stu-id="d4bad-138">Enter a partition key value of *3*, and then click **Execute**.</span></span>

    <span data-ttu-id="d4bad-139">Der Daten-Explorer zeigt das neu erstellte Dokument an.</span><span class="sxs-lookup"><span data-stu-id="d4bad-139">Data Explorer displays the newly created document.</span></span> 

## <a name="create-a-user-defined-function"></a><span data-ttu-id="d4bad-140">Erstellen einer benutzerdefinierten Funktion</span><span class="sxs-lookup"><span data-stu-id="d4bad-140">Create a user-defined function</span></span>

<span data-ttu-id="d4bad-141">Nun erstellen wir eine benutzerdefinierte Funktion im Daten-Explorer.</span><span class="sxs-lookup"><span data-stu-id="d4bad-141">Now, let's create a UDF in Data Explorer.</span></span>

<span data-ttu-id="d4bad-142">Klicken Sie im Daten-Explorer auf **Neue benutzerdefinierte Funktion**.</span><span class="sxs-lookup"><span data-stu-id="d4bad-142">In the Data Explorer, click **New UDF**.</span></span> <span data-ttu-id="d4bad-143">Kopieren Sie den folgenden Code in das Fenster, geben Sie der benutzerdefinierten Funktion den Namen *Steuer*, und klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="d4bad-143">Copy the following code into the window, name the UDF *tax*, and then click **Save**.</span></span> <span data-ttu-id="d4bad-144">Die benutzerdefinierte Funktion kann zwar nicht über das Portal ausgeführt werden, aber sie wird in einem späteren Modul verwendet.</span><span class="sxs-lookup"><span data-stu-id="d4bad-144">There's no way to run the UDF from the portal, but we'll use it in a later module.</span></span>

```java
function userDefinedFunction(){
    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }
}
```

