Mehrere Dokumente in Ihrer Datenbank müssen häufig zur gleichen Zeit aktualisiert werden. 

Wenn ein Benutzer in Ihrer Anwendung für den Onlineeinzelhandel eine Bestellung aufgibt und einen Gutscheincode, eine Gutschrift oder einen Gewinn (oder alle drei auf einmal) einlöst, müssen Sie sein Konto nach diesen Optionen abfragen, Aktualisierungen an seinem Konto vornehmen, um anzugeben, dass eine Rabattaktion verwendet wurde, die Bestellsumme aktualisieren und die Bestellung verarbeiten.

Diese Aktionen müssen alle gleichzeitig innerhalb einer Transaktion durchgeführt werden. Wenn der Benutzer den Bestellvorgang abbricht, sollten Sie ein Rollback ausführen und die Kontoinformationen nicht ändern, sodass der Gutscheincode, die Gutschrift oder die Gewinnsumme beim nächsten Einkauf eingelöst werden können.

Diese Art von Transaktionen können Sie in Azure Cosmos DB ausführen, indem Sie gespeicherte Prozeduren und benutzerdefinierte Funktionen verwenden. Gespeicherte Prozeduren sind die einzige Möglichkeit, ACID-Transaktionen (Atomarität, Konsistenz, Isolation, Dauerhaftigkeit) sicherzustellen, da sie auf dem Server ausgeführt werden. Sie werden daher als serverseitige Programmierung bezeichnet. Auch benutzerdefinierte Funktionen werden auf dem Server gespeichert und innerhalb von Abfragen verwendet, um Rechenlogik auf Werte oder Dokumente in der Abfrage anzuwenden. 

In diesem Modul erhalten Sie Informationen zu gespeicherten Prozeduren und benutzerdefinierten Funktionen. Anschließend wird erläutert, wie Sie diese im Portal ausführen.

## <a name="stored-procedure-basics"></a>Grundlagen zu gespeicherten Prozeduren

Gespeicherte Prozeduren führen komplexe Transaktionen für Dokumente und Eigenschaften aus. Sie werden in JavaScript geschrieben und in Azure Cosmos DB in einer Sammlung gespeichert. Wenn Sie gespeicherte Prozeduren für die Datenbank-Engine und in der Nähe der Daten ausführen, können Sie die Leistung mithilfe clientseitiger Programmierung verbessern.

Gespeicherte Prozeduren stellen die einzige Möglichkeit dar, atomische Transaktionen in Azure Cosmos DB zu erzielen. Clientseitige SDKs unterstützen keine Transaktionen.

Außerdem wird empfohlen, Batchvorgänge in gespeicherten Prozeduren auszuführen, da dann weniger separate Transaktionen erstellt werden müssen.

<!--TODO: Ideally I'd like to list some cases where a stored procedure is not the best option.-->

## <a name="stored-procedure-example"></a>Beispiel für eine gespeicherte Prozedur

Bei dem folgenden Beispiel handelt es sich um eine einfache gespeicherten HelloWorld-Prozedur, die den aktuellen Kontext abruft und eine Antwort sendet, die „Hello, World“ anzeigt. Beachten Sie, dass gespeicherte Prozeduren genauso wie Azure Cosmos DB-Dokumente einen ID-Wert aufweisen.

```javascript
function helloWorld() {
    var context = getContext();
    var response = context.getResponse();

    response.setBody("Hello, World");
}
```

## <a name="user-defined-function-basics"></a>Grundlagen zu benutzerdefinierten Funktionen

Mithilfe von benutzerdefinierten Funktionen (UDFs) ist es möglich, die Grammatik der SQL-Abfragesprache von Azure Cosmos DB zu erweitern und eine benutzerdefinierte Geschäftslogik wie Berechnungen für Eigenschaften und Dokumente zu implementieren. Benutzerdefinierte Funktionen können anders als gespeicherte Prozeduren nur innerhalb von Abfragen aufgerufen werden. Sie besitzen keinen Zugriff auf das Kontextobjekt und können daher Dokumente weder lesen noch schreiben.

In einer Anwendung für den Onlineeinzelhandel sollten benutzerdefinierte Funktionen verwendet werden, um die Umsatzsteuer für eine Bestellung zu ermitteln oder einen Rabatt auf ein Produkt oder eine Bestellung anzuwenden.

## <a name="user-defined-function-example"></a>Beispiel für eine benutzerdefinierte Funktion

Das folgende Beispiel erstellt eine benutzerdefinierte Funktion zur Berechnung der Steuer auf ein Produkt in einem fiktiven Unternehmen auf Basis der Produktkosten:

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

## <a name="create-a-stored-procedure-in-the-portal"></a>Erstellen einer gespeicherten Prozedur im Portal

Nachfolgend wird erläutert, wie Sie eine neue gespeicherte Prozedur im Portal erstellen. Das Portal füllt automatisch eine einfache gespeicherte Prozedur auf, die das erste Element in der Sammlung aufruft, damit diese als erstes ausgeführt wird.

1. Klicken Sie im Daten-Explorer auf **Neue gespeicherte Prozedur**.

    Im Daten-Explorer wird eine neue Registerkarte mit einem Beispiel für eine gespeicherte Prozedur angezeigt.

2. Geben Sie in das Feld **ID der gespeicherten Prozedur** den Namen *sample* ein, klicken Sie auf **Speichern** und dann auf **Ausführen**.


3. Geben Sie in das Feld **Eingabeparameter** den Namen eines Partitionsschlüssels (*33218896*) ein, und klicken Sie dann auf **Ausführen**. Beachten Sie, dass gespeicherte Prozeduren innerhalb einer Partition ausgeführt werden.

    ![Ausführen einer gespeicherten Prozedur im Portal](../media/6-stored-procedure.gif)

    Im Bereich **Ergebnis** wird der Feed aus dem ersten Dokument in der Sammlung angezeigt.

## <a name="create-a-stored-procedure-that-creates-documents"></a>Erstellen einer gespeicherten Prozedur, die Dokumente erstellt

Nachfolgend wird erläutert, wie Sie eine gespeicherte Prozedur erstellen, die Dokumente erstellt.

1. Klicken Sie im Daten-Explorer auf **Neue gespeicherte Prozedur**. Nennen Sie diese gespeicherte Prozedur *createMyDocument*. Kopieren Sie den folgenden Code, und fügen Sie ihn in das Feld **Text der gespeicherten Prozedur** ein. Klicken Sie auf **Speichern** und dann auf **Ausführen**.

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

2. Geben Sie in das Feld „Eingabeparameter“ den Partitionsschlüssels *33218898* ein, und klicken Sie dann auf **Ausführen**.

    Der Daten-Explorer zeigt das neu erstellte Dokument im Bereich „Ergebnis“ an.

    Sie können erneut die Registerkarte „Dokumente“ aufrufen. Klicken Sie auf **Aktualisieren**, um sich das neue Dokument anzeigen zu lassen. 

## <a name="create-a-user-defined-function"></a>Erstellen einer benutzerdefinierten Funktion

Nun erstellen wir eine benutzerdefinierte Funktion im Daten-Explorer.

Klicken Sie im Daten-Explorer auf **New UDF** (Neue benutzerdefinierte Funktion). Möglicherweise müssen Sie auf den Abwärtspfeil neben **New Stored Prodedure** (Neue gespeicherte Prozedur) klicken, damit **New UDF**(Neue benutzerdefinierte Funktion) angezeigt wird. Kopieren Sie den folgenden Code in das Fenster, geben Sie der benutzerdefinierten Funktion den Namen *producttax*, und klicken Sie auf **Speichern**.

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

Wechseln Sie nach der Erstellung der benutzerdefinierten Funktion zur Registerkarte **Query 1** (Abfrage 1), kopieren Sie die folgende Abfrage, und fügen Sie sie in den Abfragebereich ein, um die benutzerdefinierte Funktion auszuführen.

```sql
SELECT c.id, c.productId, c.price, udf.producttax(c.price) AS producttax FROM c
```
