Die Anwendung, die Sie erstellen, ist eine Fotogalerie. Clientseitige JavaScript-Code verwendet, um die APIs zum Hochladen und Anzeigen von Bildern aufrufen. In diesem Modul erstellen Sie eine API über eine serverlose Funktion, die eine zeitlich begrenzte-URL für ein Bild hochladen generiert. Die Webanwendung verwendet die generierte URL, ein Abbild hochzuladen, Blob-Speicher mithilfe der [Blob-Speicher-REST-API](https://docs.microsoft.com/rest/api/storageservices/blob-service-rest-api).

## <a name="create-a-blob-storage-container-for-images"></a>Erstellen Sie einen Blob-Speichercontainer für Bilder

Die Anwendung erfordert einen separaten Speicher-Container hochladen und Host-Images.

1. Stellen Sie sicher, dass Sie immer noch in der Cloud Shell (Bash) angemeldet sind. Wählen Sie andernfalls **EINGABETASTE fokusmodus** um eine Cloud Shell-Fenster zu öffnen.

1.  Erstellen Sie einen neuen Container namens **Images** in Ihrem Storage-Konto mit öffentlichem Zugriff auf alle Blobs.

    ```azurecli
    az storage container create -n images --account-name <storage account name> --public-access blob
    ```

## <a name="create-an-azure-function-app"></a>Erstellen einer Azure Function-App

Azure Functions ist ein Dienst zum Ausführen von serverloser Funktionen. Eine serverlose Funktion kann ausgelöst werden, (bezeichnet) von Ereignissen wie z. B. eine HTTP-Anforderung, oder wenn ein Blob in einem Speichercontainer erstellt wird.

Eine Azure-Funktions-app ist ein Container für eine oder mehrere serverlosen Funktionen.

1. Erstellen Sie eine neue Azure-Funktions-app mit einem eindeutigen Namen in der Ressourcengruppe, die Sie erstellt haben zuvor mit dem Namen **ersten serverlosen app**. Funktionen-apps erfordern ein Speicherkonto. In diesem Tutorial verwenden Sie das vorhandene Speicherkonto an.

    ```azurecli
    az functionapp create -n <function app name> -g first-serverless-app -s <storage account name> -c westcentralus
    ```


## <a name="create-an-http-triggered-serverless-function"></a>Erstellen einer serverlosen per HTTP ausgelöste-Funktion

Die Fotogalerie-Webanwendung führt eine HTTP-Anforderung für serverlose Funktion, um eine zeitlich begrenzte URL sicher ein Bild in blobspeicher hochladen zu generieren. Die Funktion wird durch eine HTTP-Anforderung ausgelöst und verwendet Azure Storage-SDK erstellt und die sichere URL zurückgegeben.

1. Nachdem die Funktionen-app erstellt wurde, suchen sie im Azure-Portal mithilfe des Suchfelds, und klicken Sie auf, um ihn zu öffnen.

    ![Öffnen Sie die Funktions-app](../images/2-search-function-app.png)

1. Klicken Sie im linken Navigationsbereich das Funktion app-Fenster, zeigen Sie auf **Funktionen** , und klicken Sie auf **+** zum Erstellen einer neuen serverlosen Funktion.

    ![Erstellen Sie eine neue Funktion](../images/2-new-function.png)

1. Klicken Sie auf **benutzerdefinierte Funktion** um eine Liste von Funktionsvorlagen anzuzeigen.

1. Suchen der **"httptrigger"** Vorlage, und klicken Sie auf die Sprache um (C#- oder JavaScript) zu verwenden.

1. Verwenden Sie diese Werte zum Erstellen einer Funktion, die eine Blob-Upload-URL generiert.

    | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **Sprache** | C#- oder JavaScript | Wählen Sie die Sprache, die Sie verwenden möchten. |
    | **Name Ihrer Funktion** | GetUploadUrl | Geben Sie diesen Namen genau wie angezeigt, damit die Anwendung die Funktion ermitteln kann. |
    | **Autorisierungsstufe** | Anonym | Ermöglichen Sie die Funktion, die öffentlich zugegriffen werden. |

    ![Geben Sie Einstellungen für eine neue per HTTP ausgelöste Funktion](../images/2-new-function-httptrigger.png)

1. Klicken Sie auf **erstellen** zum Erstellen der Funktion.

1. **C#** 

    1. Wenn Quellcode der Funktion angezeigt wird, ersetzen Sie sämtlichen **"Run.csx"** mit dem Inhalt des [ **csharp/GetUploadUrl/run.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/GetUploadUrl/run.csx).

1. **JavaScript** 

    1. (JavaScript) Diese Funktion erfordert die `azure-storage` Paket von Npm zum Generieren des SAS-Signaturtokens (SAS) erforderlich, um die sichere URL zu erstellen. Klicken Sie zum Installieren des Npm-Pakets klicken Sie auf der Funktions-App-Namen im linken Navigationsbereich, und klicken Sie auf **Plattformfeatures**.

    1. (JavaScript) Klicken Sie auf **Konsole** um ein Konsolenfenster anzuzeigen.

        ![Ein Konsolenfenster geöffnet](../images/2-open-console.jpg)

    1. (JavaScript) Stellen Sie sicher, das aktuelle Verzeichnis ist **d:\home\site\wwwroot** mithilfe des Befehls `cd d:\home\site\wwwroot`.

    1. (JavaScript) Führen Sie den Befehl `npm init -y` zum Erstellen eines leeren **"Package.JSON"** Datei.

    1. (JavaScript) Führen Sie den Befehl `npm install --save azure-storage` in der Konsole zum Installieren des Pakets ein, und speichern Sie ihn in **"Package.JSON"**. Es dauert etwas, um den Vorgang abzuschließen.

    1. (JavaScript) Klicken Sie auf den Namen der Funktion (**GetUploadUrl**) im linken Navigationsbereich auf die Funktion anzuzeigen, ersetzen Sie sämtlichen **"Index.js"** mit dem Inhalt des [ **Javascript/GetUploadUrl / "Index.js"**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/GetUploadUrl/index.js).
    
        ![index.js after update](../images/2-paste-js.jpg)

1. Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.

1. Klicken Sie auf **Speichern**. Überprüfen Sie, dass das Bedienfeld "Protokolle", um sicherzustellen, dass die Funktion erfolgreich kompiliert wurde.

Generiert die Funktion, was eine URL shared Access Signature (SAS) aufgerufen wird, die zum Hochladen einer Datei in Blob Storage verwendet wird. Die SAS-URL ist für einen kurzen Zeitraum gültig und lässt nur eine einzelne Datei hochgeladen werden. Wenden Sie sich an den Blob-speicherdokumentation Informationen auf [Verwenden von shared Access Signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1).


## <a name="add-an-environment-variable-for-the-storage-connection-string"></a>Fügen Sie eine Umgebungsvariable für die Speicher-Verbindungszeichenfolge

Die zuvor erstellte Funktion erfordert eine Verbindungszeichenfolge für das Speicherkonto, damit sie die SAS-URL generieren kann. Anstelle eines hartcodierten die Verbindungszeichenfolge in den Textkörper der Funktion kann sie als anwendungseinstellung gespeichert werden. Anwendungseinstellungen werden als Umgebungsvariablen, die von allen Funktionen in der Funktions-app zugegriffen werden kann.

1. Abfragen von in der Cloud Shell, die Verbindungszeichenfolge für Speicherkonto, und speichern Sie ihn auf eine Bash-Variable, die mit dem Namen **STORAGE_CONNECTION_STRING**.

    ```azurecli
    export STORAGE_CONNECTION_STRING=$(az storage account show-connection-string -n <storage account name> -g first-serverless-app --query "connectionString" --output tsv)
    ```

    Vergewissern Sie sich, dass die Variable wurde erfolgreich festgelegt wurde.

    ```azurecli
    echo $STORAGE_CONNECTION_STRING
    ```

1. Erstellen Sie eine neue anwendungseinstellung mit dem Namen **AZURE_STORAGE_CONNECTION_STRING** mit dem Wert, der im vorherigen Schritt gespeichert wurden.

    ```azurecli
    az functionapp config appsettings set -n <function app name> -g first-serverless-app --settings AZURE_STORAGE_CONNECTION_STRING=$STORAGE_CONNECTION_STRING -o table
    ```

    Vergewissern Sie sich, dass die Ausgabe des Befehls die neue anwendungseinstellung mit dem richtigen Wert enthält.


## <a name="test-the-serverless-function"></a>Testen Sie die serverlose Funktion

Zusätzlich zum Erstellen und Bearbeiten von Funktionen, bietet das Azure-Portal auch ein integriertes Tool zum Testen von Funktionen verwendet wird.

1. Um die HTTP-serverlosen Funktion zu testen, klicken Sie auf die **testen** Registerkarte auf der rechten Seite des Code-Fenster, um den Testbereich zu erweitern.

1. Ändern der **Http-Methode** zu **erhalten**.

1. Klicken Sie unter **Abfrage**, klicken Sie auf *Parameter hinzufügen**, und fügen Sie den folgenden Parameter hinzu:

    | name      |  value   | 
    | --- | --- |
    | filename | image1.jpg |

1. Klicken Sie auf **ausführen** im Testbereich eine HTTP-Anforderung an die Funktion zu senden.

1. Die Funktion gibt eine Upload-URL in der Ausgabe. Die Ausführung der Funktion wird im Bedienfeld "Protokolle" angezeigt.

    ![Protokolle, die mit der Funktion wurde erfolgreich ausgeführt.](../images/2-test-function.png)


## <a name="configure-cors-in-the-function-app"></a>Konfigurieren von CORS in der Funktions-app

Da es sich bei der app-Front-End im Blob-Speicher gehostet wird, hat er einen anderen Domänennamen als Azure-Funktions-app. Für die clientseitige JavaScript-Code auf die Funktion erfolgreich aufzurufen, die Sie gerade erstellt haben, muss die Funktions-app für Cross-Origin Resource sharing (CORS) konfiguriert werden.

1. Klicken Sie auf den Namen der Funktionen-app, in der linken Navigationsleiste auf der app-Fenster der Funktion.

1. Klicken Sie auf **Plattformfeatures** zum Anzeigen einer Liste erweiterter Funktionen.

1. Klicken Sie unter **API**, klicken Sie auf **CORS**.

    ![Aktivieren von CORS](../images/2-open-cors.jpg)

1. Hinzufügen ein Ursprungs zulassen für die Anwendungs-URL aus dem vorherigen Modul, das Auslassen der nachfolgende **/** (z. B.: `https://firstserverlessweb.z4.web.core.windows.net`).

    ![Mit serverlosen CORS-Einstellungen hinzugefügt, Web-app-URL](../images/2-add-cors.png)

1. Klicken Sie auf **Speichern**.

1. C#

   1. (C#) Navigieren Sie zurück zu den `GetUploadUrl` funktionieren, und wählen Sie dann die **integrieren** Registerkarte.

   1. (C#) Wählen Sie die ausgewählte HTTP-Methoden, **Optionen**.

      **ERSTE**, **POST**, und **Optionen** alle ausgewählt werden sollen. CORS wird verwendet, die OPTIONS-Methode, die nicht für c#-Funktionen standardmäßig ausgewählt ist.  

   1. (C#) Klicken Sie auf **speichern**.

1. Im Portal, navigieren Sie zur Funktions-app, wählen die **Übersicht über die** Registerkarte, und klicken Sie dann auf **Neustart** um sicherzustellen, dass die Änderungen für CORS wirksam werden.

## <a name="configure-cors-in-the-storage-account"></a>Konfigurieren von CORS im Storage-Konto

Da die app auch die clientseitige JavaScript-Aufrufe in Blob Storage zum Hochladen von Dateien ist, müssen Sie auch das Speicherkonto für CORS konfigurieren.

1. Führen Sie den folgenden Befehl aus, um alle Ursprünge zum Hochladen von Dateien in das Speicherkonto zu ermöglichen.

    ```azurecli
    az storage cors add --methods OPTIONS PUT --origins '*' --exposed-headers '*' --allowed-headers '*' --services b --account-name <storage account name>
    ```


## <a name="modify-the-web-app-to-upload-images"></a>Ändern Sie die Web-app zum Hochladen von Bildern

Die Web-app ruft Einstellungen ab, aus einer Datei namens **settings.js**. In den folgenden Schritten wird Sie die Datei mit der Cloud Shell zu erstellen und anschließend festlegen `window.apiBaseUrl` an die URL der Funktions-app und `window.blobBaseUrl` an die URL des Azure Blob Storage-Endpunkts.

1. Stellen Sie sicher, dass das aktuelle Verzeichnis ist, in der Cloud Shell die **Www/Dist** Ordner.

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. Abfragen der Funktions-app-URL ein, und speichern Sie sie in einer Bash-Variablen, die mit dem Namen **FUNCTION_APP_URL**.

    ```azurecli
    export FUNCTION_APP_URL="https://"$(az functionapp show -n <function app name> -g first-serverless-app --query "defaultHostName" --output tsv)
    ```

    Vergewissern Sie sich, dass die Variable korrekt festgelegt ist.

    ```azurecli
    echo $FUNCTION_APP_URL
    ```

1. Um die Basis-URI der API-Aufrufe zu Ihrer Funktions-app festzulegen, erstellen Sie **settings.js** und fügen Sie die Funktions-app-URL wie folgt hinzu.

    `window.apiBaseUrl = 'https://fnapp@lab.GlobalLabInstanceId.azurewebsites.net'`

    Sie können die Änderung vorgenommen, durch den folgenden Befehl ausführen oder mit einem Befehlszeilen-Editor, z. B. VIM.

    ```azurecli
    echo "window.apiBaseUrl = '$FUNCTION_APP_URL'" > settings.js
    ```

    Vergewissern Sie sich, dass die Datei erfolgreich geschrieben wurde.

    ```azurecli
    cat settings.js
    ```

1. Die base-BLOB-Speicher-URL Abfragen und speichern Sie sie in einer Bash-Variablen, die mit dem Namen **BLOB_BASE_URL**.

    ```azurecli
    export BLOB_BASE_URL=$(az storage account show -n <storage account name> -g first-serverless-app --query primaryEndpoints.blob -o tsv | sed 's/\/$//')
    ```

    Vergewissern Sie sich, dass die Variable korrekt festgelegt ist.

    ```azurecli
    echo $BLOB_BASE_URL
    ```

1. Um die Basis-URI der API-Aufrufe zu Ihrer Funktions-app festzulegen, fügen Sie die Speicher-URL wie die folgende Codezeile, **settings.js**.

    `window.blobBaseUrl = 'https://mystorage.blob.core.windows.net'`

    Sie können die Änderung vorgenommen, durch den folgenden Befehl ausführen oder mit einem Befehlszeilen-Editor, z. B. VIM.

    ```azurecli
    echo "window.blobBaseUrl = '$BLOB_BASE_URL'" >> settings.js
    ```

    Überprüfen Sie die Datei wurde geschrieben und enthält nun 2 Zeilen.

    ```azurecli
    cat settings.js
    ```

1. Laden Sie die Datei in Blob Storage hoch.

    ```azurecli
    az storage blob upload -c \$web --account-name <storage account name> -f settings.js -n settings.js
    ```


## <a name="test-the-web-application"></a>Testen Sie die Webanwendung

An diesem Punkt werden die im Katalog enthaltene Anwendung ist in der Lage, ein Abbild in Blob Storage hochzuladen, jedoch nicht Images noch angezeigt. Es wird versucht, Sie rufen eine `GetImages` -Funktion, die noch nicht vorhanden ist, da Sie in einem späteren Modul erstellt werden. Dieser Aufruf schlägt fehl, und die Webseite wird angezeigt, auf "Analysieren..." hängen bleiben, aber das ausgewählte Image wurde erfolgreich hochgeladen werden.

Sie können überprüfen, ob ein Bild wurde erfolgreich hochgeladen, durch den Inhalt der überprüfen die **Images** Container im Azure-Portal.

1. Navigieren Sie in einem Browserfenster zu der Anwendung. Wählen Sie eine Bilddatei, und Laden Sie es hoch. Der Upload abgeschlossen ist, aber da wir die Möglichkeit zum Anzeigen von Bildern noch hinzugefügt haben, nicht die app das hochgeladene Foto angezeigt. (Die Webseite angezeigt wird, klicken Sie auf "Bild exportieren… analysieren;" hängen bleiben Sie soll, die später behoben werden.)

1. Vergewissern Sie sich in der Cloud Shell das Image hochgeladen wurde, um die **Images** Container.

    ```azurecli
    az storage blob list --account-name <storage account name> -c images -o table
    ```

1. Bevor Sie mit dem nächsten Tutorial fortfahren, löschen Sie alle Dateien in die **Images** Container.

    ```azurecli
    az storage blob delete-batch -s images --account-name <storage account name>
    ```


## <a name="summary"></a>Zusammenfassung

In dieser Einheit Sie haben eine Azure Function-app erstellt und haben gelernt, wie eine serverlose Funktion zu verwenden, um eine Webanwendung zum Hochladen von Bildern in Blob Storage zu ermöglichen. Als Nächstes erfahren Sie, wie zum Erstellen von Miniaturansichten für die hochgeladenen Bilder mit einer serverlosen BLOBs ausgelösten-Funktion.