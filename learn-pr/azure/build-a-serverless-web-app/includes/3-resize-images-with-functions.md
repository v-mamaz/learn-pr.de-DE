In vorherigen Einheit haben Sie erfahren, wie eine serverlose Funktion das sichere Hochladen von Bildern in den blobspeicher aus einer Webanwendung ermöglichen kann. In diesem Modul erstellen Sie eine andere serverlose Funktion, um sehen Sie sich für die hochgeladene Bilder und Miniaturansichten daraus zu erstellen.

## <a name="create-a-blob-storage-container-for-thumbnails"></a>Erstellen Sie einen Blob-Speichercontainer für Miniaturansichten

Die vollständige Größe-Images werden gespeichert, in einem Container namens **Images**. Sie benötigen einen anderen Container zum Speichern von Miniaturansichten dieser Images.

1. Stellen Sie sicher, dass Sie immer noch in der Cloud Shell (Bash) angemeldet sind.  Wählen Sie andernfalls **EINGABETASTE fokusmodus** um eine Cloud Shell-Fenster zu öffnen. 

1. Erstellen Sie einen neuen Container namens **Miniaturansichten** in Ihrem Storage-Konto mit öffentlichem Zugriff auf alle Blobs.

    ```azurecli
    az storage container create -n thumbnails --account-name <storage account name> --public-access blob
    ```


## <a name="create-a-blob-triggered-serverless-function"></a>Erstellen einer serverlosen blobtrigger-Funktion

Ein Trigger definiert, wie eine Funktion aufgerufen wird. Verwendet die Funktion, die als Nächstes Sie erstellen einen Blob-Trigger: die Funktion wird automatisch aufgerufen, wenn ein Blob (Image-Datei) in hochgeladen wird die **Images** Container. Eine Funktion muss einen Trigger haben. Trigger haben zugeordnete Daten, in üblicherweise mit der Nutzlast identisch sind, von der die Funktion ausgelöst wurde.

Bindungen definieren, wie eine Funktion liest oder schreibt Daten in Azure oder Diensten von Drittanbietern. Diese Funktion erstellt eine Miniaturansicht des Bilds, das ausgelöst und speichert die Miniaturansicht in einem *Miniaturansichten* Container.

1. Öffnen Sie Ihre Funktionen-app im Azure-Portal an.

1. Klicken Sie im linken Navigationsbereich das Funktion app-Fenster, zeigen Sie auf **Funktionen** , und klicken Sie auf **+** zum Erstellen einer neuen serverlosen Funktion. Wenn eine Seite "Quickstart" angezeigt wird, klicken Sie auf **benutzerdefinierte Funktion** um eine Liste von Funktionsvorlagen anzuzeigen.

1. Suchen der **BlobTrigger** Vorlage, und wählen Sie ihn.

1. Verwenden Sie diese Werte zum Erstellen einer Funktion, die Miniaturansichten erstellt wird, wie Bilder hochgeladen werden.

    | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **Sprache** | C#- oder JavaScript | Wählen Sie Ihre bevorzugte Sprache an. |
    | **Name Ihrer Funktion** | ResizeImage | Geben Sie diesen Namen genau wie angezeigt, damit die Anwendung die Funktion ermitteln kann. |
    | **Path** | Bilder / {name} | Führen Sie die Funktion ein, wenn eine Datei angezeigt, in wird der **Images** Container. |
    | **Informationen zum Speicherkonto** | AZURE_STORAGE_CONNECTION_STRING | Verwenden Sie die Umgebungsvariable, die zuvor erstellt haben, durch die Verbindungszeichenfolge an. |

    ![Geben Sie Einstellungen für die neue Funktion](../images/3-new-function.png)

1. Klicken Sie auf **erstellen** zum Erstellen der Funktion.

1. Wenn die Funktion erstellt wurde, klicken Sie auf **integrieren** klicken Sie zum Anzeigen der Trigger, Eingabe- und ausgabebindungen.

1. Klicken Sie auf **neue Ausgabe** zum Erstellen eines neuen ausgabebindung.

    ![Wählen Sie auf der Registerkarte "Integrieren" neue Ausgabe](../images/3-new-output.jpg)

1. Wählen Sie **Azure Blob Storage** , und klicken Sie auf **wählen**. Möglicherweise finden Sie unter Bildlauf zu der **wählen** Schaltfläche.

    ![Wählen Sie Azure Blob storage](../images/3-storage-output.jpg)

1. Geben Sie die folgenden Werte ein.

    | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **Blobparametername** | Miniaturansicht | Die Funktion verwendet den Parameter mit diesem Namen, um die Miniaturansicht zu schreiben. |
    | **Funktionsrückgabewert verwenden** | Nein |  |
    | **Path** | Miniaturansichten / {name} | Die Miniaturbilder werden geschrieben, auf einen Container namens **Miniaturansichten**. |
    | **Speicherkontoverbindung** | AZURE_STORAGE_CONNECTION_STRING | Verwenden Sie die Umgebungsvariable, die zuvor erstellt haben, durch die Verbindungszeichenfolge an. |

    ![Geben Sie Einstellungen für das Blob-ausgabebindung](../images/3-blob-output.png)

1. **JavaScript**

    1. (JavaScript) Klicken Sie auf **erweiterter Editor** in der oberen rechten Ecke des Fensters, um den JSON-Code, der die Bindungen darstellt anzuzeigen.

    1. (JavaScript) In der `blobTrigger` binden, fügen Sie eine Eigenschaft, die mit dem Namen `dataType` mit einem Wert von `binary`. Dadurch wird die Bindung an den Blob-Inhalt an die Funktion als Binärdaten übergeben konfiguriert.

    ```json
    {
      "name": "myBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "images/{name}",
      "connection": "AZURE_STORAGE_CONNECTION_STRING",
      "dataType": "binary"
    }
    ```

1. Klicken Sie auf **speichern** die neue Bindung erstellen.

1. **C#**

    1. (C#) Wählen Sie die **ResizeImage** Funktionsnamen im linken Navigationsbereich auf den Quellcode der Funktion zu öffnen.

    1. (C#) Die Funktion erfordert ein NuGet-Paket namens **ImageResizer** zum Generieren von Miniaturansichten. NuGet-Pakete werden hinzugefügt, um c#-Funktionen, die mit einem **"Project.JSON"** Datei. Um die Datei zu erstellen, klicken Sie auf **Ansichtsdateien** auf der rechten Seite, um die Dateien anzuzeigen, aus denen die Funktion besteht.
    
    1. (C#) Klicken Sie auf **hinzufügen** zum Hinzufügen einer neuen Datei mit dem Namen **"Project.JSON"**.
    
    1. (C#) Kopieren Sie den Inhalt der [ **/csharp/ResizeImage/project.json** ](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/project.json) in die neu erstellte Datei. Speichern Sie die Datei . Pakete werden automatisch wiederhergestellt, wenn die Datei aktualisiert wird.
    
        ![die Datei "Project.JSON" mit ImageResizer](../images/3-project-json.png)
    
    1. (C#) Wählen Sie **"Run.csx"** unter **Ansichtsdateien** und seinen Inhalt zu ersetzen, mit dem Inhalt [ **/csharp/ResizeImage/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run.csx).

1. **JavaScript** 

    1. (JavaScript) Diese Funktion erfordert die `jimp` Paket von Npm zum Ändern der Größe des Fotos. Klicken Sie zum Installieren des Npm-Pakets klicken Sie auf der Funktions-App-Namen im linken Navigationsbereich, und klicken Sie auf **Plattformfeatures**.

    1. (JavaScript) Klicken Sie auf **Konsole** um ein Konsolenfenster anzuzeigen.

    1. (JavaScript) Führen Sie den Befehl `npm install jimp` in der Konsole. Es dauert etwas, um den Vorgang abzuschließen.

    1. (JavaScript) Klicken Sie auf die **ResizeImage** Funktionsnamen im linken Navigationsbereich auf die Funktion anzuzeigen, ersetzen Sie alle **"Index.js"** mit dem Inhalt des [ **/javascript/ResizeImage / "Index.js"**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index.js).

1. Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.

1. Klicken Sie auf **Speichern**. Überprüfen Sie im Bereich Protokolle, um sicherzustellen, dass die Funktion wurde erfolgreich gespeichert. keine Fehler vorliegen.


## <a name="test-the-serverless-function"></a>Testen Sie die serverlose Funktion

1. Öffnen Sie die Anwendung in einem Browser. Wählen Sie eine Bilddatei, und Laden Sie es hoch. Der Upload abgeschlossen ist, aber da wir die Möglichkeit zum Anzeigen von Bildern noch hinzugefügt haben, nicht die app das hochgeladene Foto angezeigt.

1. Vergewissern Sie sich in der Cloud Shell das Image hochgeladen wurde, um die **Images** Container.

    ```azurecli
    az storage blob list --account-name <storage account name> -c images -o table
    ```

1. Vergewissern Sie sich die Miniaturansicht wurde erstellt, in einem Container namens **Miniaturansichten**.

    ```azurecli
    az storage blob list --account-name <storage account name> -c thumbnails -o table
    ```

1. Rufen Sie die URL der Miniaturansicht ab.

    ```azurecli
    az storage blob url --account-name <storage account name> -c thumbnails -n <filename> --output tsv
    ```

    Öffnen Sie die URL in einem Browser, und bestätigen Sie, dass die Miniaturansicht ordnungsgemäß erstellt wurde.

1. Bevor Sie mit dem nächsten Tutorial fortfahren, löschen Sie alle Dateien in die **Images** und **Miniaturansichten** Container.

    ```azurecli
    az storage blob delete-batch -s images --account-name <storage account name>
    ```
    ```azurecli
    az storage blob delete-batch -s thumbnails --account-name <storage account name>
    ```


## <a name="summary"></a>Zusammenfassung

In dieser Einheit erstellt Sie eine serverlose Funktion, um eine Miniaturansicht zu erstellen, wenn ein Bild in einen Blob-Speichercontainer hochgeladen wird. Als Nächstes erfahren Sie, wie Sie Azure Cosmos DB zum Speichern und die Liste Bildmetadaten verwenden.