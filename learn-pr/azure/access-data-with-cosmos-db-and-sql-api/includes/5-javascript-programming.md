In Ihrer Datenbank befinden sich mehrere Dokumente, die gleichzeitig aktualisiert werden müssen. 

Wenn ein Benutzer in Ihrer Anwendung für den Onlineeinzelhandel eine Bestellung aufgibt und einen Gutscheincode, eine Gutschrift oder einen Gewinn (oder alles gleichzeitig) einlösen möchte, sollte sein Konto im Hinblick auf diese Optionen abgefragt und darin hervorgehoben werden, dass eine Rabattaktion verwendet wurde. Außerdem sollte die Gesamtsumme der Bestellung aktualisiert und die Bestellung anschließend verarbeitet werden.

Diese Aktionen müssen alle gleichzeitig innerhalb einer Transaktion durchgeführt werden. Wenn der Benutzer den Bestellvorgang abbricht, sollten Sie ein Rollback ausführen und die Kontoinformationen nicht ändern, sodass der Gutscheincode, die Gutschrift oder die Gewinnsumme beim nächsten Einkauf eingelöst werden können.

Diese Art von Transaktionen können Sie in Azure Cosmos DB durchführen, indem Sie gespeicherte Prozeduren und benutzerdefinierte Funktionen verwenden. Gespeicherte Prozeduren stellen die einzige Möglichkeit dar, zu gewährleisten, dass ACID-Transaktionen (Atomarität, Konsistenz, Isolation, Dauerhaftigkeit) ausgeführt werden können. Da sie auf dem Server ausgeführt werden, spricht man hierbei von serverseitigem Programmieren. Auch benutzerdefinierte Funktionen werden auf dem Server gespeichert und innerhalb von Abfragen verwendet, um Rechenlogik auf Werte oder Dokumente anzuwenden. 

In diesem Modul erhalten Sie Informationen zu gespeicherten Prozeduren und benutzerdefinierten Funktionen. Anschließend wird erläutert, wie Sie diese im Portal ausführen.

## <a name="stored-procedure-basics"></a>Grundlagen zu gespeicherten Prozeduren

Gespeicherte Prozeduren führen komplexe Transaktionen für Dokumente und Eigenschaften aus. Sie werden in JavaScript geschrieben und in Azure Cosmos DB in einer Sammlung gespeichert. Wenn Sie gespeicherte Prozeduren auf der Datenbank-Engine datennah ausführen, können Sie die Leistung mithilfe des clientseitigen Programmierens verbessern.

Gespeicherte Prozeduren stellen die einzige Möglichkeit dar, unteilbare Transaktionen in Azure Cosmos DB zu erzielen. Clientseitige SDKs unterstützen keine Transaktionen.

Außerdem wird empfohlen, Batchvorgänge in gespeicherten Prozeduren durchzuführen, da dann weniger separate Transaktionen erstellt werden müssen.

<!--TODO: Ideally I'd like to list some cases where a stored proc is not the best option-->

## <a name="stored-procedure-example"></a>Beispiel für eine gespeicherte Prozedur

Bei dem folgenden Beispiel handelt es sich um eine einfache gespeicherten HelloWorld-Prozedur, die den aktuellen Kontext abruft und die Antwort „Hallo Welt“ sendet. Beachten Sie, dass gespeicherte Prozeduren genauso wie Azure Cosmos DB-Dokumente einen ID-Wert aufweisen.

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

## <a name="user-defined-function-basics"></a>Grundlagen zu benutzerdefinierten Funktionen

Mithilfe von benutzerdefinierten Funktionen (UDFs) ist es möglich, die Grammatik der SQL-Abfragesprache von Azure Cosmos DB zu erweitern und eine benutzerdefinierte Geschäftslogik wie Berechnungen zu Eigenschaften und Dokumenten zu implementieren. Benutzerdefinierte Funktionen können anders als gespeicherte Prozeduren nur innerhalb von Abfragen aufgerufen werden. Sie haben keinen Zugriff auf das Kontextobjekt und können daher Dokumente weder lesen noch schreiben.

In einer Anwendung für den Onlineeinzelhandel sollten benutzerdefinierte Funktionen verwendet werden, um die Umsatzsteuer auf eine Bestellung zu ermitteln oder einen Rabatt auf ein Produkt oder eine Bestellung anzuwenden.

## <a name="user-defined-function-example"></a>Beispiel zu benutzerdefinierten Funktionen

Im folgenden Beispiel wird eine benutzerdefinierte Funktion erstellt, um anhand der Gesamtsumme einer Bestellung Rabatte zu berechnen. Anschließend wird die geänderte Bestellsumme zurückgegeben.

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

## <a name="create-a-stored-procedure-in-the-portal"></a>Erstellen einer gespeicherten Prozedur im Portal

Nachfolgend wird erläutert, wie Sie eine neue gespeicherte Prozedur im Portal erstellen. Das Portal füllt automatisch eine einfache gespeicherte Prozedur auf, die das erste Element in der Sammlung aufruft, damit diese als erstes ausgeführt wird.

1. Klicken Sie im Daten-Explorer auf **Neue gespeicherte Prozedur**.

    Im Daten-Explorer wird eine neue Registerkarte mit einem Beispiel für eine gespeicherte Prozedur angezeigt.

  <!--TODO: Insert animated gif of creating the stored proc-->

2. Geben Sie in das Feld **Stored Procedure Id** (ID der gespeicherten Prozedur) den Namen *Beispiel* ein, klicken Sie erst auf **Speichern** und dann auf **Ausführen**.


3. Geben Sie in das Feld **Eingabeparameter** den Namen des Partitionsschlüssels ein (*33218896*), und klicken Sie dann auf **Ausführen**. Beachten Sie, dass die gespeicherten Prozeduren innerhalb einer Partition arbeiten.

    ![Ausführen einer gespeicherten Prozedur im Portal](../media-draft/5-javascript-programming/stored-procedure.gif)

    Im Bereich „Ergebnis“ wird der Feed aus dem ersten Dokument in der Sammlung angezeigt.

## <a name="create-a-stored-procedure-that-creates-documents"></a>Erstellen einer gespeicherten Prozedur, die Dokumente erstellt

Nachfolgend wird erläutert, wie Sie eine gespeicherten Prozedur erstellen, die Dokumente erstellt.

1. Klicken Sie im Daten-Explorer auf **Neue gespeicherte Prozedur**. Geben sie dieser gespeicherten Prozedur den Namen *createDocuments*, und klicken Sie erst auf **Speichern** und anschließend auf **Ausführen**.

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

<!--TODO: Need to fix code above-->

2. Geben Sie den Partitionsschlüsselwert *3* ein, und klicken Sie auf **Ausführen**.

    Der Daten-Explorer zeigt das neu erstellte Dokument an. 

## <a name="create-a-user-defined-functions"></a>Erstellen von benutzerdefinierten Funktionen

Nachfolgend wird erläutert, wie Sie eine benutzerdefinierte Funktion im Daten-Explorer erstellen.

1. Klicken Sie im Daten-Explorer auf **New UDF** (Neue benutzerdefinierte Funktion). Kopieren Sie den folgenden Code in das Fenster, geben Sie der benutzerdefinierten Funktion den Namen *Steuer*, und klicken Sie auf **Speichern**. Die benutzerdefinierte Funktion kann zwar nicht über das Portal ausgeführt werden, aber sie wird in einem späteren Modul verwendet.

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

