Azure Cosmos DB ist der serverlose, global verteilte Microsoft-Datenbankdienst mit mehreren Modellen. In diesem Modul erfahren Sie, wie Sie Azure Functions zum Speichern und Abrufen von Bildmetadaten als JSON-Dokumente in Azure Cosmos DB verwenden.

## <a name="create-an-azure-cosmos-db-account-database-and-collection"></a>Erstellen eines Kontos, einer Datenbank und einer Sammlung für Azure Cosmos DB

Ein Azure Cosmos DB-Konto ist eine Azure-Ressource, die Azure Cosmos DB-Datenbanken enthält.

1. Stellen Sie sicher, dass Sie noch in Cloud Shell angemeldet sind. Klicken Sie andernfalls auf die Option **Enter focus mode** (Fokusmodus aktivieren), um ein Cloud Shell-Fenster zu öffnen. 

1. Erstellen Sie ein Azure Cosmos DB-Konto mit einem eindeutigen Namen in derselben Ressourcengruppe, in der Sie auch die anderen Ressourcen dieses Tutorials erstellt haben.

    ```azurecli
    az cosmosdb create -g <rgn>[Sandbox resource group name]</rgn> -n <cosmos db account name>
    ```

1. Erstellen Sie nach der Erstellung des Azure Cosmos DB-Kontos eine neue Datenbank mit dem Namen **imagesdb** im Konto.

    ```azurecli
    az cosmosdb database create -g <rgn>[Sandbox resource group name]</rgn> -n <cosmos db account name> --db-name imagesdb
    ```

1. Erstellen Sie nach der Erstellung der Datenbank eine neue Sammlung namens **images** darin, die über einen Durchsatz von 400 Anforderungseinheiten (Request Units, RUs) verfügt.

    ```azurecli
    az cosmosdb collection create -g <rgn>[Sandbox resource group name]</rgn> -n <cosmos db account name> --db-name imagesdb --collection-name images --throughput 400
    ```


## <a name="save-a-document-to-azure-cosmos-db-when-a-thumbnail-is-created"></a>Speichern eines Dokuments in Azure Cosmos DB bei der Erstellung einer Miniaturansicht

Mit der Azure Cosmos DB-Ausgabebindung können Sie Dokumente in einer Azure Cosmos DB-Sammlung über Azure Functions erstellen. In den folgenden Schritten konfigurieren Sie eine Azure Cosmos DB-Ausgabebindung in der Funktion **ResizeImage** und ändern die Funktion, um ein zu speicherndes Dokument (Objekt) zurückzugeben.

1. Öffnen Sie die Funktions-app in der [Azure-Portal](https://portal.azure.com/?azure-portal=true).

1. Erweitern Sie im linken Navigationsbereich die Funktion **ResizeImage**, und klicken Sie dann auf **Integrieren**.

1. Klicken Sie unter **Ausgaben** auf **Neue Ausgabe**.

1. Suchen Sie nach dem Element **Azure Cosmos DB**, und wählen Sie es aus. Klicken Sie dann auf **Auswählen**.

    ![Auswählen von „Neue Ausgabe“](../media/4-new-output.jpg)

1. Füllen Sie die Felder der **Azure Cosmos DB-Ausgabe** mit den unten angegebenen Werten.

    | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **Dokumentparametername** | Wählen Sie **Funktionsrückgabewert verwenden** aus. | Der Wert im Feld wird automatisch auf **$return** festgelegt. |
    | **Datenbankname** | imagesdb | Verwenden Sie den Namen der Datenbank, die Sie erstellt haben. |
    | **Sammlungsname** | images | Verwenden Sie den Namen der Sammlung, die Sie erstellt haben. |

1. Klicken Sie neben **Azure Cosmos DB-Kontoverbindung** auf **Neu**. Wählen Sie das Azure Cosmos DB-Konto aus, das Sie zuvor erstellt haben.

    ![Eingeben der Einstellungen für Azure Cosmos DB-Ausgabebindung](../media/4-cosmos-db-output.png)

1. Klicken Sie auf **Speichern**, um die Azure Cosmos DB-Ausgabebindung zu erstellen.

1. Klicken Sie links auf den Funktionsnamen **ResizeImage**, um die Funktion zu öffnen.

::: zone pivot="csharp"
1. (C#) Ändern Sie den Rückgabetyp der Funktion von **void** in **object**.

1. (C#) Fügen Sie am Ende der Funktion den folgenden Codeblock hinzu, um das zu speichernde Dokument zurückzugeben:

    ```csharp
    return new {
        id = name,
        imgPath = "/images/" + name,
        thumbnailPath = "/thumbnails/" + name
    };
    ```

    ![„run.csx“ für die Funktion „ResizeImages“ nach den Änderungen](../media/4-update-function.png)

::: zone-end

::: zone pivot="javascript"
1. (JavaScript) Ändern Sie die `context.done()`-Anweisung in der `else`-Klausel, um das in Azure Cosmos DB zu speichernde Dokument zurückzugeben.

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

::: zone-end

1. Klicken Sie unter dem Codefenster auf **Protokolle**, um den Protokollbereich zu erweitern.

1. Klicken Sie auf **Speichern**. Überprüfen Sie den Protokollbereich, um sicherzustellen, dass die Funktion erfolgreich gespeichert wird und keine Fehler vorliegen.

## <a name="create-a-function-to-list-images-from-azure-cosmos-db"></a>Erstellen einer Funktion zum Auflisten von Bildern aus Azure Cosmos DB

Für die Webanwendung ist eine API zum Abrufen der Bildmetadaten aus Azure Cosmos DB erforderlich. In den folgenden Schritten erstellen Sie eine per HTTP ausgelöste Funktion, bei der eine Azure Cosmos DB-Eingabebindung erstellt wird, um die Datenbanksammlung abzufragen.

1. Zeigen Sie in Ihrer Funktions-App auf der linken Seite auf **Funktionen**, und klicken Sie auf das Pluszeichen (+), um eine neue Funktion zu erstellen.

1. Suchen Sie nach der Vorlage **HttpTrigger**, und wählen Sie sie aus.

1. Verwenden Sie diese Werte, um eine Funktion zu erstellen, mit der eine URL zum Abrufen von Bildern generiert wird:

    | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **Name Ihrer Funktion** | GetImages | Geben Sie diesen Namen genau wie hier angezeigt ein, damit die Anwendung die Funktion ermitteln kann. |
    | **Autorisierungsstufe** | Anonym | Lässt den öffentlichen Zugriff auf die Funktion zu. |

1. Klicken Sie auf **Erstellen**.

1. Klicken Sie nach der Erstellung der neuen Funktion im linken Navigationsbereich unter dem Namen der Funktion auf **Integrieren**.

1. Klicken Sie auf **Neue Eingabe**, und wählen Sie **Azure Cosmos DB** aus. 

    ![Auswählen von „Neue Eingabe“](../media/4-new-input.jpg)

1. Klicken Sie auf **Auswählen**.

1. Geben Sie die folgenden Werte an:

    | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **Dokumentparametername** | documents | Entspricht dem Parameternamen in der Funktion. |
    | **Datenbankname** | imagesdb |  |
    | **Sammlungsname** | images |  |
    | **SQL-Abfrage** | SELECT * FROM c ORDER BY c._ts DESC | Dient zum Abrufen von Dokumenten (letzte Dokumente zuerst). |
    | **Azure Cosmos DB-Kontoverbindung** | Wählen Sie die vorhandene Verbindungszeichenfolge aus. |  |

1. Klicken Sie auf **Speichern**, um die Eingabebindung zu erstellen.

::: zone pivot="csharp"

1. Klicken Sie auf den Funktionsnamen, um das Codefenster zu öffnen. Ersetzen Sie den gesamten Inhalt der Datei **run.csx** durch den Inhalt der Datei [**/csharp/GetImages/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetImages/run.csx).

::: zone-end

::: zone pivot="javascript"

1. Klicken Sie auf den Funktionsnamen, um das Codefenster zu öffnen. Ersetzen Sie den gesamten Inhalt der Datei **index.js** durch den Inhalt der Datei [**/javascript/GetImages/index.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetImages/index.js).

::: zone-end

1. Klicken Sie unter dem Codefenster auf **Protokolle**, um den Protokollbereich zu erweitern.

1. Klicken Sie auf **Speichern**. Überprüfen Sie den Protokollbereich, um sicherzustellen, dass die Funktion erfolgreich gespeichert wird und keine Fehler aufgetreten sind.

## <a name="test-the-application"></a>Testen der Anwendung

1. Öffnen Sie die Anwendung in einem Browser. Wählen Sie eine Bilddatei aus, und laden Sie sie hoch.

1. Nach einigen Sekunden wird die Miniaturansicht des neuen Bilds auf der Seite angezeigt.

1. Verwenden Sie im Azure-Portal das **Suchfeld**, um anhand des Namens nach Ihrem Azure Cosmos DB-Konto zu suchen. Klicken Sie auf den Namen, um das Konto zu öffnen.

1. Klicken Sie links auf **Daten-Explorer**, um Sammlungen und Dokumente zu durchsuchen.

1. Wählen Sie unter der Datenbank **imagesdb** die Sammlung **images** aus.

1. Vergewissern Sie sich, dass ein Dokument für das hochgeladene Bild erstellt wurde.

    ![Anzeige eines Dokuments für ein hochgeladenes Bild im Daten-Explorer](../media/4-data-explorer.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie erfahren, wie Sie ein Konto, eine Datenbank und eine Sammlung für Azure Cosmos DB erstellen. Außerdem wurde beschrieben, wie Sie die Azure Cosmos DB-Bindungen zum Speichern und Abrufen von Bildmetadaten in der Azure Cosmos DB-Sammlung verwenden. Als Nächstes lernen Sie, wie Sie eine Beschriftung für jedes hochgeladene Bild mithilfe von Microsoft Cognitive Services automatisch zu generieren.