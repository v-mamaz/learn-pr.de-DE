Azure Cosmos DB ist die serverlose, Global verteilte, multimodell-Datenbank von Microsoft. In diesem Modul erfahren Sie, wie Sie mithilfe von Azure Functions zum Speichern und Abrufen von Metadaten zu Bildern als JSON-Dokumente in Cosmos DB.

## <a name="create-a-cosmos-db-account-database-and-collection"></a>Erstellen einer Cosmos DB-Konto, Datenbank und Sammlung

Cosmos DB-Konto ist eine Azure-Ressource, die Cosmos DB-Datenbanken enthält.

1. Stellen Sie sicher, dass Sie immer noch in der Cloud Shell angemeldet sind.  Wählen Sie andernfalls **EINGABETASTE fokusmodus** um eine Cloud Shell-Fenster zu öffnen. 

1. Erstellen Sie ein Cosmos DB-Konto mit einem eindeutigen Namen in der gleichen Ressourcengruppe wie die anderen Ressourcen in diesem Tutorial.

    ```azurecli
    az cosmosdb create -g first-serverless-app -n <cosmos db account name>
    ```

1. Nachdem das Cosmos DB-Konto erstellt wurde, erstellen Sie eine neue Datenbank namens **Imagesdb** im Konto.

    ```azurecli
    az cosmosdb database create -g first-serverless-app -n <cosmos db account name> --db-name imagesdb
    ```

1. Nachdem die Datenbank erstellt wurde, erstellen Sie eine neue Sammlung mit dem Namen **Images** in der Datenbank mit einem Durchsatz von 400 anforderungseinheiten (RUs).

    ```azurecli
    az cosmosdb collection create -g first-serverless-app -n <cosmos db account name> --db-name imagesdb --collection-name images --throughput 400
    ```


## <a name="save-a-document-to-cosmos-db-when-a-thumbnail-is-created"></a>Speichern eines Dokuments in Cosmos DB, wenn eine Miniaturansicht erstellt wird

Die Cosmos DB-ausgabebindung ermöglicht erstellen Sie mit Dokumenten in einer Cosmos DB-Sammlung in Azure Functions. In den folgenden Schritten konfigurieren Sie eine Cosmos DB-ausgabebindung in der **ResizeImage** Funktion, und ändern Sie die Funktion zum Zurückgeben von einem Dokument (Objekt) gespeichert werden soll.

1. Öffnen Sie die Funktions-app im Azure-Portal an.

1. Erweitern Sie im linken Navigationsbereich, der **ResizeImage** funktionieren, und wählen Sie dann **integrieren**.

1. Klicken Sie unter **Ausgaben**, klicken Sie auf **neue Ausgabe**.

1. Suchen der **Azure Cosmos DB** Element aus, und wählen Sie ihn. Klicken Sie dann auf **Auswählen**.

    ![Wählen Sie die neue Ausgabe](../images/4-new-output.jpg)

1. Füllen Sie die Felder unter **Azure Cosmos DB-Ausgabe** mit den folgenden Werten.

    | Einstellung      |  Empfohlener Wert   | BESCHREIBUNG                                        |
    | --- | --- | ---|
    | **Dokumentparametername** | Wählen Sie **Funktionsrückgabewert verwenden** | Der Wert des Textfelds wird automatisch festgelegt, um **$return**. |
    | **Datenbankname** | imagesdb | Verwenden Sie den Namen der Datenbank, die Sie erstellt haben. |
    | **Sammlungsname** | Images | Verwenden Sie den Namen der Auflistung, die Sie erstellt haben. |

1. Neben **Azure Cosmos DB-Kontoverbindung**, klicken Sie auf **neue**. Wählen Sie das Cosmos DB-Konto, die, das Sie zuvor erstellt haben.

    ![Geben Sie Einstellungen für Azure Cosmos DB-ausgabebindung](../images/4-cosmos-db-output.png)

1. Klicken Sie auf **speichern** zum Erstellen der Cosmos DB-ausgabebindung.

1. Klicken Sie auf die **ResizeImage** Funktionsnamen auf der linken Seite, um die Funktion zu öffnen.

1. **C#**

    1. (C#) Ändern des Rückgabetyps der Funktion von **"void"** zu **Objekt**.

    1. (C#) Am Ende der Funktion fügen Sie den folgenden Codeblock, um das zu speichernde Dokument zurückzugeben:
    
        ```csharp
        return new {
            id = name,
            imgPath = "/images/" + name,
            thumbnailPath = "/thumbnails/" + name
        };
        ```
    
        !["Run.csx" für ResizeImages-Funktion nach Änderungen](../images/4-update-function.png)

1. **JavaScript**

    1. (JavaScript) Ändern der `context.done()` -Anweisung in der `else` Klausel zur Rückgabe des Dokuments in Cosmos DB gespeichert werden.

    ```javascript
    if (error) {
        context.done(error);
    } else {
        context.bindings.thumbnail = stream;
        context.done(null, {
            id: context.bindingData.name,
            imgPath: "/images/" + context.bindingData.name,
            thumbnailPath: "/thumbnails/" + context.bindingData.name
        });
    }
    ```

1. Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.

1. Klicken Sie auf **Speichern**. Überprüfen Sie im Bereich Protokolle, um sicherzustellen, dass die Funktion wurde erfolgreich gespeichert. keine Fehler vorliegen.


## <a name="create-a-function-to-list-images-from-cosmos-db"></a>Erstellen Sie eine Funktion zum Auflisten von Images aus Cosmos DB

Die Webanwendung benötigt eine API zum Abrufen von Metadaten zu Bildern von Cosmos DB. In den folgenden Schritten. So erstellen Sie eine per HTTP ausgelöste-Funktion, die eine Cosmos DB-eingabebindung verwendet wird, um die datenbankauflistung abzufragen.

1. Zeigen Sie Sie in Ihrer Funktionen-app auf **Funktionen** auf der linken Seite und auf **+** zum Erstellen einer neuen Funktion.

1. Suchen der **"httptrigger"** Vorlage, und wählen Sie ihn.

1. Verwenden Sie diese Werte zum Erstellen einer Funktion, die eine Get-Images-URL generiert.

    | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **Name Ihrer Funktion** | GetImages | Geben Sie diesen Namen genau wie angezeigt, damit die Anwendung die Funktion ermitteln kann. |
    | **Autorisierungsstufe** | Anonym | Ermöglichen Sie die Funktion, die öffentlich zugegriffen werden. |

1. Klicken Sie auf **Erstellen**.

1. Wenn die neue Funktion erstellt wird, klicken Sie auf **integrieren** unter dem Funktionsnamen im linken Navigationsbereich.

1. Klicken Sie auf **neue Eingabe** , und wählen Sie **Azure Cosmos DB**. 

    ![Wählen Sie die neue Eingabe](../images/4-new-input.jpg)

1. Klicken Sie auf **Auswählen**.

1. Füllen Sie die folgenden Werte:

    | Einstellung      |  Empfohlener Wert   | BESCHREIBUNG                                        |
    | --- | --- | ---|
    | **Dokumentparametername** | Dokumente | Übereinstimmungen von Parameternamen in der Funktion. |
    | **Datenbankname** | imagesdb |  |
    | **Sammlungsname** | Images |  |
    | **SQL query** | Wählen Sie * from c sortiert nach c. _ts Desc | Dokumente, die neuesten Dokumente erste abrufen. |
    | **Azure Cosmos DB-Kontoverbindung** | Wählen Sie die vorhandene Verbindungszeichenfolge |  |

1. Klicken Sie auf **speichern** die eingabebindung zu erstellen.

1. **C#**

    1. Klicken Sie auf den Namen der Funktion im Code-Fenster zu öffnen, und Ersetzen Sie alle **"Run.csx"** mit dem Inhalt [ **/csharp/GetImages/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetImages/run.csx).

1. **JavaScript**

    1. Klicken Sie auf den Namen der Funktion im Code-Fenster zu öffnen, und Ersetzen Sie alle **"Index.js"** mit dem Inhalt [ **/javascript/GetImages/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetImages/index.js).

1. Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.

1. Klicken Sie auf **Speichern**. Überprüfen Sie im Bereich Protokolle, um sicherzustellen, dass die Funktion wurde erfolgreich gespeichert. keine Fehler vorliegen.


## <a name="test-the-application"></a>Testen der Anwendung

1. Öffnen Sie die Anwendung in einem Browser. Wählen Sie eine Bilddatei, und Laden Sie es hoch.

1. Nach wenigen Sekunden wird die Miniaturansicht des neuen Images auf der Seite angezeigt.

1. Verwenden Sie das Suchfeld im Azure-Portal für Ihr Cosmos DB-Konto nach Namen suchen. Klicken Sie auf, um es zu öffnen.

1. Klicken Sie auf **Daten-Explorer** auf der linken Seite zum Durchsuchen von Sammlungen und Dokumente.

1. Unter den **Imagesdb** Datenbank, wählen die **Images** Auflistung.

1. Vergewissern Sie sich, dass ein Dokument für das hochgeladene Bild erstellt wurde.

    ![Daten-Explorer mit der ein Dokument für eines hochgeladenen Bilds](../images/4-data-explorer.png)



## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie eine Cosmos DB-Konto, Datenbank und einer Sammlung zu erstellen. Sie haben zudem so verwenden Sie die Cosmos DB-Bindungen zum Speichern und Abrufen von Metadaten zu Bildern in Cosmos DB-Sammlung. Als Nächstes erfahren Sie, wie Sie eine Beschriftung für jedes hochgeladene Bild mithilfe von Microsoft Cognitive Services automatisch zu generieren.